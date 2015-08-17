---
layout: post
title: Android反编译植入广告教程
date: 2014-06-30 22:33
author: VERYYOUNG
comments: true
categories: [Android]
---

原理：Android是基于Java的，要编译成类似Java字节码运行在类似JVM的Dalvik虚拟机上，市面上有很多Java反编译工具，所以反编译一般的安卓程序并修改程序其实是不太难的。

下面讲一讲怎么反编译安卓程序并植入广告（以有米广告为例），仅供学习参考，如若用在商业软件上，造成的后果本人概不负责。



----------

###工具下载
本例子用到了两个工具,APKTOOL和AUTO-SIGN，前者用来对程序进行反编译和重编译，后者用来给生成的APK文件进行签名。

本人在Ubuntu 下进行的测试，windows和,mac下应该不会有太大的区别。

1. 下载apktool <a title=" https://code.google.com/p/android-apktool/" href=" https://code.google.com/p/android-apktool/" target="_blank"> https://code.google.com/p/android-apktool/</a>

2. 下载auto-sign <a title="http://dl.vmall.com/c0shg7qvki" href="http://dl.vmall.com/c0shg7qvki" target="_blank">http://dl.vmall.com/c0shg7qvki</a>

3. 下载有米SDK，<a title="http://www.youmi.net/page/download/sdk" href="http://www.youmi.net/page/download/sdk" target="_blank">http://www.youmi.net/page/download/sdk</a>


----------

###操作步骤

1.反编译有米SDK Demo获得反编译后字节码和配置文件
执行命令

	　./apktool d demp.apk

会生成一个demo文件夹，进入该文件夹，打开AndroidManifest.xml
复制权限配置代码和广告组建代码

	 <uses-permission android:name="android.permission.INTERNET" />
	    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
	    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
	    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
	    <uses-permission android:name="android.permission.GET_TASKS" />
	　　<uses-permission android:name="com.android.launcher.permission.INSTALL_SHORTCUT" />
	　　        <activity	android:name="net.youmi.android.AdBrowser" android:configChanges="keyboard|keyboardHidden|orientation" />
	　　        <service android:name="net.youmi.android.AdService" android:exported="false" />
	　　        <receiver android:name="net.youmi.android.AdReceiver">
	　　            <intent-filter>
	　　                <action android:name="android.intent.action.PACKAGE_ADDED" />
	　　                <data android:scheme="package" />
	　　            </intent-filter>
	　　        </receiver>
	　　        <activity	android:name="net.youmi.android.SmartBannerActivity" android:configChanges="keyboard|keyboardHidden|orientation" />
	　　        <service android:name="net.youmi.android.SmartBannerService" android:exported="false" />
	　　        <receiver android:name="net.youmi.android.offers.OffersReceiver" android:exported="false" />


  打开layout/activity_main.xml,复制布局代码

	<LinearLayout android:gravity="center_horizontal" 
	android:orientation="horizontal" 
	android:id="@+id/adLayout"
	 android:layout_width="fill_parent"
	android:layout_height="wrap_content" />


2.编写自己的有米工程代码，反编译，得到actvity字节码
加入如下代码

		  private void addAd(){
	        AdManager.getInstance(this).init("71a2165bdbad68b4", "42866e56516313c1", false);
	        AdView adView = new AdView(this, AdSize.FIT_SCREEN);
	        //实例化广告条
	        //获取要嵌入广告条的布局
	        LinearLayout adLayout=(LinearLayout)findViewById(R.id.adLayout);
	        //将广告条加入到布局中
	        adLayout.addView(adView);
	    }

3.反编译，会得到

		method private addAd()V
	    .locals 6
	
	    .prologue
	    .line 21
	    invoke-static {p0}, Lnet/youmi/android/AdManager;->getInstance(Landroid/content/Context;)Lnet/youmi/android/AdManager;
	
	    move-result-object v2
	
	    const-string v3, "71a2165bdbad68b4"
	
	    const-string v4, "42866e56516313c1"
	
	    const/4 v5, 0x0
	
	    invoke-virtual {v2, v3, v4, v5}, Lnet/youmi/android/AdManager;->init(Ljava/lang/String;Ljava/lang/String;Z)V
	
	    .line 22
	    new-instance v1, Lnet/youmi/android/banner/AdView;
	
	    sget-object v2, Lnet/youmi/android/banner/AdSize;->FIT_SCREEN:Lnet/youmi/android/banner/AdSize;
	
	    invoke-direct {v1, p0, v2}, Lnet/youmi/android/banner/AdView;-><init>(Landroid/content/Context;Lnet/youmi/android/banner/AdSize;)V
	
	    .line 25
	    .local v1, adView:Lnet/youmi/android/banner/AdView;
	    const v2, 0x7f070003
	
	    invoke-virtual {p0, v2}, Lhbut/hgdonline/activity/SelectResultActivity;->findViewById(I)Landroid/view/View;
	
	    move-result-object v0
	
	    check-cast v0, Landroid/widget/LinearLayout;
	
	    .line 27
	    .local v0, adLayout:Landroid/widget/LinearLayout;
	    invoke-virtual {v0, v1}, Landroid/widget/LinearLayout;->addView(Landroid/view/View;)V
	
	    .line 28
	    return-void
		.end method


4.反编译待植入广告apk
 
		./apktool d　2048.apk

5.把initAD()对应的smali代码添加到MainActivity中 ，并在onCreate()方法中调用initAD()显示广告。

		（invoke-direct {p0}, Lcom/uberspot/a2048/MainActivity;->initAD()V

6.在2048/AndroidManifest.xml中对应节点加入上面复制的xml代码

在2048的activity_main.xml中加入上面复制的布局代码
这里添加了一个新的id“adLayout”,我们需要把这个id手动写到R$id.smali中。注意这里的16位value值是递增的。


7.在libs目录下加入有米sdk的jar文件，编译代码生成apk

		./apktool b　2048

   会在dist目录下生成2048.apk



8.给生成的apk签名：把apk移动到auto-sign目录下，执行以下命令

		java -jar signapk.jar testkey.x509.pem testkey.pk8 2048.apk 2048_signed.apk 

会生成签好名的apk 2048_signed.apk

最后，对比下植入广告前后效果

<img src="http://veryyoung.u.qiniudn.com/7niu_20140630215832.png" alt="http://veryyoung.u.qiniudn.com/7niu_20140630215832.png" />

<img src="http://veryyoung.u.qiniudn.com/7niu_QQ20140630215738.png" alt="http://veryyoung.u.qiniudn.com/7niu_QQ20140630215738.png" />

原理大概就是这样的。想定制更详细的功能，相信每个android-developer应该都可以搞定了!
