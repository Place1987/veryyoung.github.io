---
layout: post
title: 把WordPress迁移到Jekyll
date: 2015-7-24 10:27:21
author: VERYYOUNG
comments: true
categories: [Uncategorized]
---
#把WordPress迁移到Jekyll

早就无法忍受WordPress蜗牛般的反应速度了，抽时间狠狠心给它迁移到Gitpages了，骄傲的使用了Jekyll。可以使用github管理文章，免费无流量限制，最重要的是可以用Markdown哦！

下面说一下迁移步骤


1.导出WordPress文章</br>
本来想使用[jekyll-exporter](https://wordpress.org/plugins/jekyll-exporter/ "jekyll-exporter")，但是部署到SAE，run，报错

	Warning: dir(saestor://wordpress/uploads) [function.dir]: failed to open dir: "SaeStorageWrapper::dir_opendir" call failed in wp-content/plugins/jekyll-exporter/jekyll-exporter.php on line 390

	Fatal error: Call to a member function read() on a non-object in wp-content/plugins/jekyll-exporter/jekyll-exporter.php on line 391

再也不想用所谓的Paas了，一点自由都木有！

WordPress自带导出功能，可以把文章导出成xml文件。![](http://ww4.sinaimg.cn/large/9732f922jw1eudn1xqz9ej20xw0l244k.jpg)

然后再借助[wpXml2Jekyll](https://github.com/theaob/wpXml2Jekyll "wpXml2Jekyll")这款神器把xml导出成md文件，导出的文章需要进行微调，比如文章标题，代码格式之类的。


2.安装Jekyll<br>
JekyllBootstrap官网有个[jekyll-quick-start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html "jekyll-quick-start")，对着上面走一遍，就Ok了，中间涉及到github的一些操作，ruby的安装之类的...


3.放入博文<br>
将第一步得到的md放入到_posts文件夹下，git push


4.绑定域名<br>
参考[https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/ "https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/")，具体方法是在repo的根目录下面，新建一个名为CNAME的文本文件，里面写入你要绑定的域名，比如veryyoung.me,然后在域名商添加A记录，指向Gitpages的IP
![](http://ww2.sinaimg.cn/large/9732f922jw1eudng7rcm8j20mp0ajdhx.jpg)

---
这就完了，接下来换主题改界面之类的随便折腾去吧！！


