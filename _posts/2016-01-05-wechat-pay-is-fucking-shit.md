---
layout: post
title: 微信支付（公众号）的流程以及各种坑
date: 2016-1-5 22:03:49
author: VERYYOUNG
comments: true
categories: [Others]
---

微信支付的用户体验确实很不错，能在公众号内直接唤醒微信支付，非常方便，最近尝试接入了一把，发现处处都是坑，简直是噩梦。


<!-- more -->

----------

##申请认证

这步省略，自己对着流程走就行了，走完之后微信会给你发生一份邮件。


##得到各种 key

申请通过之后收到的邮件中会有一份如下图的材料

![](http://veryyoung.u.qiniudn.com/20160105221017.png)

然后根据提示设置 pay_sign_key，在加上公众号的 app_id、token 等


一共需要 app_id、token、secret、mch_id、pay_sign_key 这几个东东，都整理好后就可以开始开发了！


**噩梦正式开始！！**

##统一下单
支付之前必须得先下单，得调用微信的 [统一下单](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=9_1) 接口，注意，用 JSAPI 的订单一定要带上 openId，至于 openId 怎么获得可以参考[OpenID的获取指引](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=4_4)。


获得 openId 之前要记得如图配置

![](http://veryyoung.u.qiniudn.com/20160105231137.png)

不然会报 redirect uri 参数错误。



##微信JS-SDK

既然是微信内的 html5 应用，那应该得用[微信JS-SDK](https://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html)吧！


###config

按照官方说的，先 config

    wx.config({
        debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
        appId: '', // 必填，公众号的唯一标识
        timestamp: , // 必填，生成签名的时间戳
        nonceStr: '', // 必填，生成签名的随机串
        signature: '',// 必填，签名，见附录1
        jsApiList: [] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2
    });
    
开始总是报，config:fail， 具体原因木有了！！

找了半天，发现我后端返回的 json 解析不正常，OK，正常配置后，不报错了！

###发起一个微信支付请求

    wx.chooseWXPay({
        timestamp: 0, // 支付签名时间戳，注意微信jssdk中的所有使用timestamp字段均为小写。但最新版的支付后台生成签名使用的timeStamp字段名需大写其中的S字符
        nonceStr: '', // 支付签名随机串，不长于 32 位
        package: '', // 统一支付接口返回的prepay_id参数值，提交格式如：prepay_id=***）
        signType: '', // 签名方式，默认为'SHA1'，使用新版支付需传入'MD5'
        paySign: '', // 支付签名
        success: function (res) {
            // 支付成功后的回调函数
        }
    });
    
   
好几个坑点，你跟着这个走肯定走不通！！

timestamp 中的 ‘t’ 必须小写，但同时生成 paySign 的过程一定要大写！！！

然后开始按照微信提供的 [签名算法](https://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html#.E9.99.84.E5.BD.951-JS-SDK.E4.BD.BF.E7.94.A8.E6.9D.83.E9.99.90.E7.AD.BE.E5.90.8D.E7.AE.97.E6.B3.95)生成 paySign。

>最后参与签名的参数有appId, timeStamp, nonceStr, package, signType。

按照这一句来死活不成功啊，最后发现还得带上 &key=pay_sign_key 再加密

OK，paySign 终于算对了，我的前端代码是这样写的：

    $("#btn_pay").click(function () {
        $.getJSON("/h5/pay/pay", function (data) {
            wx.chooseWXPay({
                appId: data.appId,
                timestamp: data.timestamp,
                nonceStr: data.nonceStr,
                package: data.package_,
                signType: data.signType,
                paySign: data.signType,
                success: function (res) {
                    if (res.err_msg == 'chooseWXPay:ok') {
                        alert('支付成功');
                    } else {
                        alert('支付失败');
                    }
                },
                fail: function (res) {
                    alert(JSON.stringify(res));
                    alert('支付请求失败');
                }
            });
        });
    });
    
    
然后永远走到 fail 里面来！！永远返回 chooseWxpay:fail。

各种 Google，发现要先如图配置

![](http://veryyoung.u.qiniudn.com/20160105230837.png)

注意这里配置的是目录，而不是具体路径。


配置完继续 fail，木有具体原因！！

Google 一番，发现我又踩到一个大坑里面去了！！

公众号支付测试的时候测试链接要从公众号里点进去才能出现支付界面，不然会一直报chooseWXPay fail。

OK，给对应的微信号发，还是不行啊我擦！！！


各种查文档，最后又发现了一个这样的文档 [网页端调起支付API](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_7&index=6)


示例代码如下：

    function onBridgeReady(){
        WeixinJSBridge.invoke(
            'getBrandWCPayRequest', {
                "appId" ： "wx2421b1c4370ec43b",     //公众号名称，由商户传入     
                "timeStamp"：" 1395712654",         //时间戳，自1970年以来的秒数     
                "nonceStr" ： "e61463f8efa94090b1f366cccfbbb444", //随机串     
                "package" ： "prepay_id=u802345jgfjsdfgsdg888",     
                "signType" ： "MD5",         //微信签名方式：     
                "paySign" ： "70EA570631E4BB79628FBCA90534C63FF7FADD89" //微信签名 
            },
            function(res){     
                if(res.err_msg == "get_brand_wcpay_request：ok" ) {}     // 使用以上方式判断前端返回,微信团队郑重提示：res.err_msg将在用户支付成功后返回    ok，但并不保证它绝对可靠。 
            }
        ); 
    }
    if (typeof WeixinJSBridge == "undefined"){
        if( document.addEventListener ){
            document.addEventListener('WeixinJSBridgeReady', onBridgeReady, false);
        }else if (document.attachEvent){
            document.attachEvent('WeixinJSBridgeReady', onBridgeReady); 
            document.attachEvent('onWeixinJSBridgeReady', onBridgeReady);
        }
    } else{
        onBridgeReady();
    }
    
    
这样改完代码之后，终于出现了熟悉的微信支付窗口，我差点留下激动的泪水。。



---

吐槽下，微信这样的大厂从微信公众平台开始到现在，文档和 demo 到处都是坑，各版本之间不兼容，demo 几乎没法用，不得不让人怀疑微信内部的开发实力以及内部流程是不是各种混乱。

对比下支付宝，拿来 demo 随便改一改就能直接用了, 集成其他厂商的服务，比如邮件、短信、图片 CDN 等都是非常简单，同时有很完善的文档和 demo，而微信基本得摸着石头过河...









