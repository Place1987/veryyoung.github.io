---
layout: post
title: Set up Vagrant
date: 2015-11-2 19:30:01
author: VERYYOUNG
comments: true
categories: [Linux]
---

>Create and configure lightweight, reproducible, and portable development environments.

上面这段话来自 Vagrant 官网，我翻译一下：创建和配置轻量级的，可重复的，可移植的开发环境。

通俗点说就是，我们可以通过 Vagrant 封装一个 Linux 的开发环境，分发给团队成员。成员可以在自己喜欢的桌面系统（Mac/Windows/Linux）上开发程序，代码却能统一在封装好的环境里运行，非常霸气。



<!-- more -->

----------

Segmentfault 上有一份不错的 start up 教程 [http://segmentfault.com/a/1190000000264347](http://segmentfault.com/a/1190000000264347)，跟着走。

在

	vagrant up
	
的时候出现

	λ vagrant up
	Bringing machine 'default' up with 'virtualbox' provider...
	==> default: Importing base box 'dev'...
	==> default: Matching MAC address for NAT networking...
	==> default: Setting the name of the VM: vagrant_default_1446021251338_43189
	==> default: Clearing any previously set network interfaces...
	==> default: Preparing network interfaces based on configuration...
		default: Adapter 1: nat
	==> default: Forwarding ports...
		default: 22 => 2222 (adapter 1)
	==> default: Booting VM...
	==> default: Waiting for machine to boot. This may take a few minutes...
		default: SSH address: 127.0.0.1:2222
		default: SSH username: vagrant
		default: SSH auth method: private key
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		default: Warning: Connection timeout. Retrying...
		
找到 Vagrantfile 里的这一段

	# config.vm.provider "virtualbox" do |vb|
	#   # Display the VirtualBox GUI when booting the machine
	#   vb.gui = true
	#
	#   # Customize the amount of memory on the VM:
	#   vb.memory = "1024"
	# end
	
去掉注释，这样 Vagrant 启动的时候会启动 GUI，有异常也会抛出来。

果然，看到了如下的异常。

![](http://veryyoung.u.qiniudn.com/20151028165452.png)

这表示本机电脑没有开启虚拟化。

重启，进入 bios，开启虚拟化，如图：

![](http://veryyoung.u.qiniudn.com/20151030184904.jpg)

再次 

	vagrant up

异常没了。

然后 

	vagrant ssh
	
感觉和登录了 vps 一样。


开启公网访问（桥接）

找到 Vagrantfile 

	#config.vm.network "public_network"
	
取消注释。

这样就和访问局域网内的机器一样了。

再来张截图：本地浏览器访问 Vagrant

![](http://veryyoung.u.qiniudn.com/20151102194747.png)

还可以设置本地机器和 Vagrant 的共享目录，类似如下配置

	config.vm.synced_folder "../data", "/vagrant_data"
	
Done！~


以后只用在本地起个 IDE 或者编辑器，其他编程相关的东东都可以放在 Vagrant 里了，配置完之后还可以

	vagrant package

打成一个包，给团队其他人用，或者带回家继续开发啦！



	

