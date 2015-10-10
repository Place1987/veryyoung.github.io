---
layout: post
title: 链接还是用户名？？
date: 2015-10-8 10:04:06
author: VERYYOUNG
comments: true
categories: [Java]
---

一次偶然在社区看到两条有意思的回复，大概意思是他们为了让内部链接不和用户名冲突，做了很 low 的处理。

然后本人据此展开各种联想和探索，期间也遇到了几个莫名其妙的问题...

<!-- more -->

----------

回复如下：

![](http://veryyoung.u.qiniudn.com/20151008095218.png)


然后联想到 [GitHub](https://github.com/) 就处理得比较优雅。

比如 [https://github.com/a](https://github.com/a) 是一个人，而 [https://github.com/c](https://github.com/c) 却是一个链接。

那么自己编程起来应该怎么实现呢？

本人用的比较顺手的是 SpringMVC，下面就用 SpringMVC 为例子来说明，其它的 MVC 框架应该大同小异。

先试试如下代码，请求 /c 会打印出什么。

	    @RequestMapping("{username}")
		@ResponseBody
		public String username(@PathVariable String username) {
			logger.info("there");
			return username;
		}
	
	
	
		@RequestMapping("c")
		@ResponseBody
		public String c() {
			logger.info("here");
			return "c";
		}
		
	
	
结果令人大跌眼镜。

![](http://veryyoung.u.qiniudn.com/20150930093042.png)

居然是 “here” 和 “there” 各一次。


对调两个方法的顺序，结果一样。


难道是因为 SpringMVC 觉得这个链接两个都可以匹配到，就两个都访问了一次？

如果真是这样，那这个需求该怎么实现？

提供一个入口，然后各种 if else？

类似下面

	   if(username is url){
    
            ModelAndView modelAndView = new ModelAndView(username);

            if(username.equals("login")){
                modelAndView.addObject("valueForLogin","valueForLogin");
            }else if(username.equals("register")){
                modelAndView.addObject("valueForRegister","valueForRegister");
            }
			
			.... 无穷无尽的 else 
        }else{
            // username
        }


那将是一个多么糟糕的体验！！

同时每个请求返回的东西可能并不全是 modelAndView，还有可能是图片、 json、 xml、 文件等各式各样的东西。

这样都合在一起处理简直是一场灾难，我选择狗带！！

后来 debug 了一下，发现请求 username 不是 c，而且一个奇怪的东西。

![](http://veryyoung.u.qiniudn.com/20150930093355.png)

很明显，这是在请求 ico，在 Chrome console 找了下，果然发现了对应的请求日志。

针对浏览器自动请求 ico，我专门整理了一篇文章，[favicon.ico 的一些优化意见](/blog/2015/09/30/browser-request-favicon-ico.html)


username 的值是 favicon，为啥 .ico 消失了呢？ 

针对 SpringMVC 丢失请求的小数点后面的数据的原因以及解决方案，我专门整理了一篇文章，[SpringMVC PathVariable 丢失小数点后面的数据](/blog/2015/09/30/spring-mvc-path-variable-dot.html)


--------


把上面两点搞定之后，再次请求 /c，只有一个方法响应了。

看来 SpringMVC 还是比较智能的，比我想的聪明多了！！

-------

那 SpringMVC 为何最后找到了 username 这个方法，而不是 c 呢？

一步步 debug 试试。

SpringMVC 监听的是

	org.springframework.web.servlet.DispatcherServlet
	
所以直接从 DispatcherServlet 的 doService 方法看起。

通过 getHandler 方法来决定具体调用哪个 handler 来处理请求。

继续跟到 AbstractHandlerMapping 的 getHandler 方法 -》 AbstractHandlerMethodMapping 的 getHandlerInternal 方法。
		
![](http://veryyoung.u.qiniudn.com/20151008145336.png)		

在方法第一行得到了 lookupPath = "/c"， 然后再调用 lookupHandlerMethod 方法类根据 path 找到 handlerMethod。 

终于要进入重点了！

lookupHandlerMethod 方法调用 addMatchingMappings 找到能匹配上的 handler。

正如我们意料之中的，找到了如下两个：

![](http://veryyoung.u.qiniudn.com/20151008145954.png)	


注意，这里的 directPathMatches 是 null，代表没有能直接匹配上的。

然后程序走到下面，根据某些策略给这两个 “matches” 排序，取第一个作为 “bestMatch”

![](http://veryyoung.u.qiniudn.com/20151008151250.png)	

如果有多个 “matches” ，取第二个作为 “secondBestMatch”，如果 bestMatch 和 secondBestMatch 是一样的，会抛出旨意不明的异常。

	AbstractHandlerMethodMapping.Match bestMatch = (AbstractHandlerMethodMapping.Match)matches.get(0);
	if(matches.size() > 1) {
		AbstractHandlerMethodMapping.Match secondBestMatch = (AbstractHandlerMethodMapping.Match)matches.get(1);
		if(comparator.compare(bestMatch, secondBestMatch) == 0) {
			 Method m1 = bestMatch.handlerMethod.getMethod();
			 Method m2 = secondBestMatch.handlerMethod.getMethod();
			 throw new IllegalStateException("Ambiguous handler methods mapped for HTTP path \'" + request.getRequestURL() + "\': {" + m1 + ", " + m2 + "}");
			 }
	}

*事实上这也不太可能发生，因为在应用启动扫描 mapping 的时候就会检查，如果存在重复会抛出异常 *

	Invocation of init method failed; nested exception is java.lang.IllegalStateException: Ambiguous mapping found. Cannot map 'homeController' bean method 
	
	
<br>
根据 bestMatch 找到对应的方法去响应。


我这里最后选择到的方法是 c 方法。


---

现在焦点全部聚集到

	AbstractHandlerMethodMapping.MatchComparator comparator = new AbstractHandlerMethodMapping.MatchComparator(this.getMappingComparator(request));
	
	

重点是 getMappingComparator 这个方法。

getMappingComparator 方法在 RequestMappingInfoHandlerMapping 中实现的，实现如下：

	    protected Comparator<RequestMappingInfo> getMappingComparator(final HttpServletRequest request) {
			return new Comparator() {
				public int compare(RequestMappingInfo info1, RequestMappingInfo info2) {
					return info1.compareTo(info2, request);
				}
			};
		}
		
		
很简单，就是返回了一个 Comparator，具体的比较策略得到 RequestMappingInfo 的 compareTo 方法去找。

RequestMappingInfo 的 compareTo 看起来真是醉醉哒！！


	    public int compareTo(RequestMappingInfo other, HttpServletRequest request) {
			int result = this.patternsCondition.compareTo(other.getPatternsCondition(), request);
			if(result != 0) {
				return result;
			} else {
				result = this.paramsCondition.compareTo(other.getParamsCondition(), request);
				if(result != 0) {
					return result;
				} else {
					result = this.headersCondition.compareTo(other.getHeadersCondition(), request);
					if(result != 0) {
						return result;
					} else {
						result = this.consumesCondition.compareTo(other.getConsumesCondition(), request);
						if(result != 0) {
							return result;
						} else {
							result = this.producesCondition.compareTo(other.getProducesCondition(), request);
							if(result != 0) {
								return result;
							} else {
								result = this.methodsCondition.compareTo(other.getMethodsCondition(), request);
								if(result != 0) {
									return result;
								} else {
									result = this.customConditionHolder.compareTo(other.customConditionHolder, request);
									return result != 0?result:0;
								}
							}
						}
					}
				}
			}
		}



可以用 switch 来优化下逻辑，或者最简单的方式就是 if 里面 return 了，下面就不用 else 了。

这样可以把这复杂的嵌套逻辑判断变得一目了然。

还好我们的这种情况下第一个 if 就匹配到了。

继续跟到 PatternsRequestCondition 的 compareTo 方法。

![](http://veryyoung.u.qiniudn.com/20151008154317.png)	

重点是这一句：
	
	Comparator patternComparator = this.pathMatcher.getPatternComparator(lookupPath);
	
依然要继续生成比较器。

找到 AntPathMatcher 的 getPatternComparator 方法。

    public Comparator<String> getPatternComparator(String path) {
        return new AntPathMatcher.AntPatternComparator(path);
    }
	

返回了一个实现了 Comparator 的内部类 AntPatternComparator。

直接看 compare 方法。


        public int compare(String pattern1, String pattern2) {
            AntPathMatcher.AntPatternComparator.PatternInfo info1 = new AntPathMatcher.AntPatternComparator.PatternInfo(pattern1);
            AntPathMatcher.AntPatternComparator.PatternInfo info2 = new AntPathMatcher.AntPatternComparator.PatternInfo(pattern2);
            if(info1.isLeastSpecific() && info2.isLeastSpecific()) {
                return 0;
            } else if(info1.isLeastSpecific()) {
                return 1;
            } else if(info2.isLeastSpecific()) {
                return -1;
            } else {
                boolean pattern1EqualsPath = pattern1.equals(this.path);
                boolean pattern2EqualsPath = pattern2.equals(this.path);
                return pattern1EqualsPath && pattern2EqualsPath?0:(pattern1EqualsPath?-1:(pattern2EqualsPath?1:(info1.isPrefixPattern() && info2.getDoubleWildcards() == 0?1:(info2.isPrefixPattern() && info1.getDoubleWildcards() == 0?-1:(info1.getTotalCount() != info2.getTotalCount()?info1.getTotalCount() - info2.getTotalCount():(info1.getLength() != info2.getLength()?info2.getLength() - info1.getLength():(info1.getSingleWildcards() < info2.getSingleWildcards()?-1:(info2.getSingleWildcards() < info1.getSingleWildcards()?1:(info1.getUriVars() < info2.getUriVars()?-1:(info2.getUriVars() < info1.getUriVars()?1:0))))))))));
            }
        }
		

前两行代码生成了该内部类的一个内部类 PatternInfo。

下面就根据 内部类 PatternInfo 的 isLeastSpecific 方法来排序了！

	public boolean isLeastSpecific() {
		return this.pattern == null || this.catchAllPattern;
    }
	

catchAllPattern 判断在 PatternInfo 的构造函数里面

	  this.catchAllPattern = this.pattern.equals("/**");
	  
判断是否是根目录，这里 的 //c 和 //{username} 都没匹配到，排序失败，走到最后一个 else 里面去。

else 的前面两行判断是否连接匹配到了，我这里 controller 上面多加了行

	@RequestMapping("/")
	
导致链接多了个 / ，所以 pattern1EqualsPath 和 pattern2EqualsPath 的值都是 false，然后进入最后那个长长的 return 方法。

再次吐槽下，这是我见过最牛逼的三目表达式！！

没有之一！！

这么复杂的三目表达式嵌套你还不如搞成一长串的 if else 呢！

由于上面两个都没匹配到，舍弃前面部分，所以 return 可以简化成

	return pattern1EqualsPath?-1:(pattern2EqualsPath?1:(info1.isPrefixPattern() && info2.getDoubleWildcards() == 0?1:(info2.isPrefixPattern() && info1.getDoubleWildcards() == 0?-1:(info1.getTotalCount() != info2.getTotalCount()?info1.getTotalCount() - info2.getTotalCount():(info1.getLength() != info2.getLength()?info2.getLength() - info1.getLength():(info1.getSingleWildcards() < info2.getSingleWildcards()?-1:(info2.getSingleWildcards() < info1.getSingleWildcards()?1:(info1.getUriVars() < info2.getUriVars()?-1:(info2.getUriVars() < info1.getUriVars()?1:0)))))))));
	
	
继续简化：

	return pattern2EqualsPath?1:(info1.isPrefixPattern() && info2.getDoubleWildcards() == 0?1:(info2.isPrefixPattern() && info1.getDoubleWildcards() == 0?-1:(info1.getTotalCount() != info2.getTotalCount()?info1.getTotalCount() - info2.getTotalCount():(info1.getLength() != info2.getLength()?info2.getLength() - info1.getLength():(info1.getSingleWildcards() < info2.getSingleWildcards()?-1:(info2.getSingleWildcards() < info1.getSingleWildcards()?1:(info1.getUriVars() < info2.getUriVars()?-1:(info2.getUriVars() < info1.getUriVars()?1:0))))))));
	

简化无极限：

	return info1.isPrefixPattern() && info2.getDoubleWildcards() == 0?1:(info2.isPrefixPattern() && info1.getDoubleWildcards() == 0?-1:(info1.getTotalCount() != info2.getTotalCount()?info1.getTotalCount() - info2.getTotalCount():(info1.getLength() != info2.getLength()?info2.getLength() - info1.getLength():(info1.getSingleWildcards() < info2.getSingleWildcards()?-1:(info2.getSingleWildcards() < info1.getSingleWildcards()?1:(info1.getUriVars() < info2.getUriVars()?-1:(info2.getUriVars() < info1.getUriVars()?1:0)))))));
	
	
	
	
这里调用到了 PatternInfo 的 isPrefixPattern、 getDoubleWildcards、 getTotalCount、 getLength、 getSingleWildcards、 getUriVars 方法。

分别解释下每个方法的作用以及返回值。




| 方法                  |作用                            |返回值 info1(//{username})、info2(//c)  |
| --------------------- |:-----------------------------:|----------------:| 
| isPrefixPattern       | 判断 pattern 是否以 /** 结尾   |   false、false  |
| getDoubleWildcards    | pattern 匹配到 ** 的个数       |   0、0  		|
| getSingleWildcards    | pattern 匹配到 单个 * 的个数   |   0、0          |
| getUriVars            | pattern 匹配到 { 的个数        |   1、0     |
| getTotalCount         | pattern 匹配到 url 符号的个数：uriVars + singleWildcards + 2 * doubleWildcards   |   1、0     |
| getLength             | pattern string 中的字符个数 （{username}算一个字符）   |   null（没执行到，如果执行到了也会是3）、3    |


继续化简

	return info2.isPrefixPattern() && info1.getDoubleWildcards() == 0?-1:(info1.getTotalCount() != info2.getTotalCount()?info1.getTotalCount() - info2.getTotalCount():(info1.getLength() != info2.getLength()?info2.getLength() - info1.getLength():(info1.getSingleWildcards() < info2.getSingleWildcards()?-1:(info2.getSingleWildcards() < info1.getSingleWildcards()?1:(info1.getUriVars() < info2.getUriVars()?-1:(info2.getUriVars() < info1.getUriVars()?1:0))))));
	
	return info1.getTotalCount() != info2.getTotalCount()?info1.getTotalCount() - info2.getTotalCount():(info1.getLength() != info2.getLength()?info2.getLength() - info1.getLength():(info1.getSingleWildcards() < info2.getSingleWildcards()?-1:(info2.getSingleWildcards() < info1.getSingleWildcards()?1:(info1.getUriVars() < info2.getUriVars()?-1:(info2.getUriVars() < info1.getUriVars()?1:0)))));
	
info1.getTotalCount() != info2.getTotalCount() ，三目表达式前面的条件终于匹配到了，舍去后面部分：
	
	return info1.getTotalCount() - info2.getTotalCount();
	
	
最终的结果返回 1 啦！！！

返回 1，从小到大排，排序结果如下：

![](http://veryyoung.u.qiniudn.com/20151008151258.png)	


所以 选择 //c，而不是 //{username}

回到 RequestMappingInfo 的 compareTo 方法，一路往上回到 AbstractHandlerMethodMapping 的 lookupHandlerMethod 方法。

排完序了，最后选择到的成了 c 方法，而不是 username 方法。



回来再请求下 /a，排序的时候只有一个东东，那第一个东东就是 bestMatch 咯，也就会直接找到 //{username}。



------

将 controller 上的注解

	@RequestMapping("/") 
	
改为

	@RequestMapping("") 
	
或者直接去掉，以前的 mapping 前面会少个斜杠，会变为 /c 和 /{username}


看看比较的效果。

![](http://veryyoung.u.qiniudn.com/20151009095659.png)

这次 matches 的 size 是 1了， directPathMatches 不再是 null 了，而是 /c  !!!

意思就是一下子直接找到了，上面的排序都不用了！

按道理这种情况下应该也需要 directMatche 到，因为请求来的 uri 会被过滤掉前面的多个斜杠

比如 uri 为 ////c 的请求，lookupPath 的值 为 /c ，而 HandlerMethod 为 //c 与它是匹配不上的。

btw， 我已经发了一个 pr 让 HandlerMethod 也过滤掉前面的重复的斜杠了！！


------

**结论：SpringMVC 会优先匹配完全匹配到的 url，如果没匹配到，会根据 getTotalCount 函数的返回值，也就是 pattern 匹配到 url 符号的个数：uriVars + singleWildcards + 2 * doubleWildcards，去选择，越小越优先选取。**

**也就是会找到尽量简单的方法，并且固定的 requestMapping 会比带 PathVariable 的优先考虑。**

**同时建议在编码的时候要避免 path 出现 双斜杠的现象，如果没能直接匹配上，后面那么长的逻辑，效率肯定会差很多，而且万一有 bug 呢？**








<br>
<br>



------


还有一个问题就是，万一哪个用户名叫 "c", SpingMVC 优先选择链接而不是用户名，那这个用户的界面岂不是没法进入了？

看看 GitHub 是怎么做的。

![](http://veryyoung.u.qiniudn.com/20151008200857.png)	

![](http://veryyoung.u.qiniudn.com/20151008200906.png)	


很显然，GitHub 维护了一个链接的列表，不让对应链接的用户名被注册到。

所以在设置之初得想好哪些链接是需要用的，他维护起来。

-----

其实最简单的方案就是在用户名前面再加个东东，比如 /u/{username}，这样就能永远不冲突啦！

[Coding](https://coding.net/) 就是这样做的。  

比如 [https://coding.net/about](https://coding.net/about) 是关于 Coding 网站的一些介绍，而 [https://coding.net/u/about](https://coding.net/u/about)  则是一个用户的主页。

