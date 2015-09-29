---
layout: post
title: Ajax 下载文件
date: 2015-9-29 14:14:36
author: VERYYOUNG
comments: true
categories: [Front End]
---
AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

是异步请求，只能返回简单的文本，而下载文件一般都是同步的。

最近遇到一个需求，需要在用户选择的条件有错的情况下 alert 出提示，没错的情况下下载文件。

Google 了好久，方案大都是伪造一个 form 或者 iframe， 感觉不太靠谱，自己摸索了下。

<!-- more -->

----------

具体方案如下：先发起一个 Ajax 请求去校验数据，如果请求数据不合格，弹出错误信息；如果请求合格，新开一个窗口去访问刚刚的链接（带参数）。

前端代码如下：

        download: function () {
            var downloadArgs = {
                name1: 'name1',
                value1 "value"
            };
            //下载
            $.post('../download.do', downloadArgs, function (data) {
                    if (!data.success) {
                        alert(data.errors[0]);
                    } else {
                        window.location = "../download.do?" + T.url.jsonToQuery(downloadArgs);
                    }
                }
            );
        }
        
       
       
 后端代码大致如下：
 
    @RequestMapping(value = "/download.do")
    @ResponseBody
    public Result download(String name1, String name2) {
        Result result = new Result();
        if(validate(name1,name2)){
            result.setMessage("参数不正确");
            result.setSuccess(false);
            return result;
        }

        // Ajax 请求不提供下载
        if (StringUtils.isEmpty(request.getHeader("X-Requested-With"))) {
            download(request,response,name1,name2);
        }
        return result;
    }
    
    
相当于前半部分代码只用 Ajax 做数据校验， 后半部分代码只提供下载。

比拆分成两部分的优点在于在后端严格校验了数据，不会让用户下载到非法的数据。


