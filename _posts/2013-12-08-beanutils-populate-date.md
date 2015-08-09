---
layout: post
title: BeanUtils.populate Date转换异常
date: 2013-12-08 13:30
author: VERYYOUNG
comments: true
categories: [Java]
---
今天在用BeanUtils polulate bean的时候遇到了一下的异常：
org.springframework.web.util.NestedServletException: Request processing failed; nested exception is org.apache.commons.beanutils.ConversionException: DateConverter does not support default String to 'Date' conversion.

看异常消息，是前端传来的字符串不能转换为Date类型的问题


解决方案：
编写String转换为Date的DateTimeConverter，并注册到 ConvertUtils
然后BeanUtilsBean 使用这个ConvertUtils 去转换
代码如下：
<pre lang="java">
SnsScore score = new SnsScore();
DateTimeConverter dtConverter = new DateConverter();
dtConverter.setPattern("yyyy-MM-dd");
ConvertUtilsBean convertUtilsBean = new ConvertUtilsBean();
convertUtilsBean.deregister(Date.class);
convertUtilsBean.register(dtConverter, Date.class);
BeanUtilsBean beanUtilsBean = new BeanUtilsBean(convertUtilsBean,
	new PropertyUtilsBean());
beanUtilsBean.populate(score, request.getParameterMap());
//BeanUtils.populate(score, request.getParameterMap());
</pre>
