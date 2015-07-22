---
layout: post
title: 基于注解的权限认证
date: 2015-01-06 22:06
author: VERYYOUNG
comments: true
categories: [Java]
---
<p>在上一篇博文中简要介绍了下Java注解。</p>

<p>想到既然注解能做很多事，为嘛不让它来做权限控制呢？
ok，开工。</p>

<pre><code>/**
* Created by veryyoung on 2014/12/24.
*/

public abstract class AbstractAuthenticationFilter extends    
  HandlerInterceptorAdapter {

@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    HandlerMethod method = (HandlerMethod) handler;
    FreeAccess freeAccess = method.getMethodAnnotation(FreeAccess.class);
    if (freeAccess != null) {
        return true;
    }
    Set&amp;lt;Privilege&amp;gt; priv = new HashSet&amp;lt;&amp;gt;();
    PrivilegeRequired pr = method.getClass().getAnnotation(PrivilegeRequired.class);
    if (pr != null &amp;amp;&amp;amp; pr.value() != null &amp;amp;&amp;amp; pr.value().length &amp;gt; 0) {
        priv.addAll(Arrays.asList(pr.value()));
    }
    pr = method.getMethodAnnotation(PrivilegeRequired.class);
    if (pr != null &amp;amp;&amp;amp; pr.value() != null &amp;amp;&amp;amp; pr.value().length &amp;gt; 0) {
        priv.addAll(Arrays.asList(pr.value()));
    }

    Privilege[] privileges = priv.toArray(new Privilege[priv.size()]);

    boolean loginRequired = privileges.length &amp;gt; 0
            || AnnotationUtils.findAnnotation(method.getBean().getClass(), LoginRequired.class) != null
            || method.getMethodAnnotation(LoginRequired.class) != null;
    if (loginRequired &amp;amp;&amp;amp; !checkLogin(request)) {
        response.setStatus(401);
        String uri = request.getRequestURI();
        uri = new String(Base64.encodeBase64(uri.getBytes()));
        uri = URLEncoder.encode(uri);
        response.sendRedirect(&amp;quot;/login?redirect=&amp;quot; + uri);
        return false;
    }
    if (privileges.length &amp;gt; 0 &amp;amp;&amp;amp; !checkPrivileges(request, privileges)) {
        request.setAttribute(&amp;quot;insufficientPrivilege&amp;quot;, privileges[0].getKey());
        response.setStatus(403);
    }
    return true;
}


public abstract boolean checkLogin(HttpServletRequest request);

public abstract boolean checkPrivileges(HttpServletRequest request, Privilege... privileges);
</code></pre>

<p>}</p>

<p>大致意思是继承springmvc的HandlerInterceptorAdapter，然后拦截每个请求，判断是否有@LoginRequired或者PrivilegeRequired的注解，如果有，
记录下当前uri（base64 URLEncoder之后），然后403到登陆界面，登陆成功后再跳回来。</p>

<p>可以在一个需要验证的Controller class上写上@LoginRequired，然后整个Controller的所有method都会去做权限验证。
可以用@FreeAccess 去排除不需要的的method</p>

