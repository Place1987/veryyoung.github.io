---
layout: post
title: Java破解简单验证码
date: 2013-12-30 21:48
author: VERYYOUNG
comments: true
categories: [Java]
---
前段时间写基于俺们学校教学管理平台的App,需要破解验证码,模拟登陆,然后抓取数据,显示在Android端
验证码破解的一般思路是下载验证码,提取出需要的部分,平均拆分成N(N=验证码字符个数)份
二值化(转化为黑白色,黑色为1,白色为0),取模,然后保存摸板
俺们学校的验证码比较弱,只有0-9 10个数字,建好这十个数字的模型
在模拟登陆之前先把验证码下载下来,也是提取出需要的部分,拆分,然后与摸板进行比较,这样验证码就能破解啦!
步骤总结如下:
（1）批量下载一部分验证码图片
（2）将这部分图片提取出需要的部分
（3）将提取出来的部分平均拆分成N(N=验证码字符个数)份
（4) 去噪，将图片灰度化与二值化
（5）提取每一个字符的特征，生成特征矢量或特征矩阵
（6）分类与学习。将特征矢量或特征矩阵与样本库进行比对，挑选出相似的那类样本，将这类样本的值作为输出结果。

下面借助代码和图片,具体讲解步骤:
（1）批量下载一部分验证码图片
  这里借助了Apache的<a href="http://hc.apache.org/httpclient-3.x/" title="HttpClient" target="_blank"></a>
  这个比较简单，代码就不贴了。所做的工作就是从 http://run.hbut.edu.cn/Account/GetValidateCode 
  下载了100张图片,保存到checkcode文件夹,命名为code_i.jgp 
  如图所示：
<img src="http://veryyoung.u.qiniudn.com/7niu_hbutcode.png" alt="" />

(2).将这部分图片提取出需要的部分
 用windows自带的画图工具编辑图片,缩放到最大,如下图所示
 <img src="http://veryyoung.u.qiniudn.com/7niu_edithbutcode.png" alt="" />
可观察到周围有很多空白像素点,这些都是不需要的.裁剪出需要的部分,注意:要确保裁剪之后能平均裁剪为4等分
代码如下:
<pre lang="java">
public static BufferedImage getSingleCode(BufferedImage image) {
      return image.getSubimage(6, 5, 36, 12);
}
</pre>
裁剪之后效果如下:
<img src="http://veryyoung.u.qiniudn.com/7niu_hbutsinglecode.png" alt="" />
（3）将提取出来的部分平均拆分成N(N=验证码字符个数)份
 我需要破解的验证码为4位,所以需平均裁剪为4等份
代码如下:
<pre lang="java">
public static BufferedImage[] getCheckCodes(BufferedImage image) {
	BufferedImage checkCode[] = new BufferedImage[4];
	int height = image.getHeight();
	int width = image.getWidth();
	int x = 0 * (width / checkCode.length);
	int y = 0;
	int w = width / checkCode.length;
	int h = height;
	checkCode[0] = image.getSubimage(x, y, w, h);
	checkCode[1] = image.getSubimage(1 * (width / checkCode.length), 0,
				width / checkCode.length, height);
	checkCode[2] = image.getSubimage(2 * (width / checkCode.length), 0,
				width / checkCode.length, height);
	checkCode[3] = image.getSubimage(3 * (width / checkCode.length), 0,
				width / checkCode.length, height);
	return checkCode;
}
</pre>
效果如下<img src="http://veryyoung.u.qiniudn.com/7niu_hbutsingle4.png" alt="" />
（4) 去噪，将图片灰度化与二值化
图片黑白化原理：
获取到R、G、B的值，然后根据黑白化的公式R*R +G*G +B*B < 3*128*128为黑色，否则为白色，这种方法对于绝大多数是有效的。
还有一种是根据灰度图，然后在根据灰度来确定是黑还是白。
像素点灰度的公式：
1.浮点算法：Gray=R*0.3+G*0.59+B*0.11
　　2.整数方法：Gray=(R*30+G*59+B*11)/100
　　3.移位方法：Gray =(R*28+G*151+B*77)>>8;
　　4.平均值法：Gray=（R+G+B）/3;
5.仅取绿色：Gray=G；
参考：http://baike.baidu.com/view/1184366.html
可以根据需要做出微调

本例采用黑白化公式来黑白化
<pre lang="java">
	public static int pixelConvert(int pixel) {
		int result = 0;

		int r = (pixel >> 16) & 0xff;
		int g = (pixel >> 8) & 0xff;
		int b = (pixel) & 0xff;


		int tmp = r * r + g * g + b * b;
		if (tmp > 3 * 128 * 128) {
			result = 1;			
		}
]		return result;
	}
</pre>


（5）提取每一个字符的特征，生成特征矢量或特征矩阵
   代码如下
<pre lang="java">
public class Filter {
	public static void blackAndWhiteFilter(BufferedImage image) {
		if (image == null) {
			return;
		}

		for (int i = 0; i < image.getHeight(); i++) {
			for (int j = 0; j < image.getWidth(); j++) {
				image.setRGB(j, i, Tools.pixelConvert(image.getRGB(j, i)));
			}
		}
	}

	public static void dotFilter(BufferedImage image) {
		if (image == null) {
			return;
		}

		for (int i = 0; i < image.getHeight(); i++) {
			for (int j = 0; j < image.getWidth(); j++) {
				if (i > 0 && j > 0 && i < (image.getHeight() - 1)
						&& j < (image.getWidth() - 1)) {
					if (image.getRGB(j, i) == 0xff000000) {
						if (image.getRGB(j - 1, i) == 0xffffffff
								&& image.getRGB(j - 1, i - 1) == 0xffffffff
								&& image.getRGB(j, i - 1) == 0xffffffff
								&& image.getRGB(j + 1, i) == 0xffffffff
								&& image.getRGB(j + 1, i + 1) == 0xffffffff
								&& image.getRGB(j, i + 1) == 0xffffffff) {
							image.setRGB(j, i, 0xffffffff);
						}
					}
				}
			}
		}
	}
}
</pre>
经过步骤4和5之后得到如下效果，这就是我们需要的模型！<img src="http://veryyoung.u.qiniudn.com/7niu_hbutmodel.png" alt="" />

（6）分类与学习。将特征矢量或特征矩阵与样本库进行比对，挑选出相似的那类样本，将这类样本的值作为输出结果。
  根据图片模型得到数字模型。我所得到的模型如下:
<pre lang="java">
	private static final int[][][] model = { { // 0
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 0, 1, 0, 0, 0, 1, 1 },
					{ 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0 },
					{ 1, 0, 0, 1, 0, 1, 1, 1, 1, 1, 0, 0 },
					{ 0, 0, 0, 1, 1, 1, 1, 1, 0, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0 },
					{ 0, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 1 },
					{ 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1 },
					{ 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1 }, }, { // 1
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 0, 1 },
					{ 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 },
					{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1 },
					{ 0, 1, 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 }, }, { // 2
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0 },
					{ 1, 1, 0, 0, 1, 1, 1, 1, 1, 0, 0, 0 },
					{ 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0 },
					{ 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1 },
					{ 0, 0, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0 },
					{ 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0 },
					{ 1, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1 }, }, {// 3
			{ 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1 },
					{ 1, 1, 0, 1, 1, 1, 1, 1, 1, 0, 0, 1 },
					{ 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 0, 1 },
					{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1 },
					{ 1, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1 }, }, {// 4
			{ 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1 },
					{ 1, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1 },
					{ 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 1, 1 },
					{ 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, 0 },
					{ 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
					{ 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1 },
					{ 0, 0, 0, 1, 1, 1, 1, 1, 1, 0, 1, 1 }, }, {// 5
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1 },
					{ 1, 1, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0 },
					{ 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0 },
					{ 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 0, 0, 1, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 1, 1, 1, 0, 0, 1 },
					{ 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1 },
					{ 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 1 }, }, {// 6
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 1, 1 },
					{ 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
					{ 1, 0, 0, 0, 1, 1, 0, 1, 1, 1, 0, 0 },
					{ 0, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 0 },
					{ 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1 },
					{ 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 1 },
					{ 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1 }, }, {// 7
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0 },
					{ 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1 },
					{ 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 1, 1 },
					{ 0, 0, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1 },
					{ 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1 }, }, {// 8
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 1 },
					{ 1, 1, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0 },
					{ 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0 },
					{ 0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 1 },
					{ 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, 1 },
					{ 1, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1 }, }, {// 9
			{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
					{ 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 1 },
					{ 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0 },
					{ 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0 },
					{ 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0 },
					{ 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0 },
					{ 0, 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 1 },
					{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1 },
					{ 1, 1, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1 }, } };
</pre>

验证码识别代码:
<pre lang="java">
public static String compare(BufferedImage image) {
		BufferedImage checkCode[] = Tools.getCheckCodes(image);
		StringBuffer code = new StringBuffer();
		for (int t = 0; t < 4; t++) {
			int[] result = new int[10];
			boolean ckFlg = false;
			int num = -1;
			for (int i = 0; i < 10; i++) {
				num = -1;
				ckFlg = true;
				for (int x = 0; x < checkCode[t].getWidth(); x++) {
					for (int y = 0; y < checkCode[t].getHeight(); y++) {
						int expRGB = Tools.pixelConvert(checkCode[t].getRGB(x,
								y));
						int cmpRGB = model[i][x][y];
						if (expRGB == cmpRGB) {
							result[i]++;
						}
					}
				}

				if (result[i] > 90) {
					ckFlg = true;
					num = i;
					break;
				}

			}
			if (ckFlg) {
				code.append(num);
				ckFlg = false;
			} else {
				ckFlg = false;
			}
		}
		return code.toString();

	}
</pre>


我所得到的模型为9*12像素，包括一些杂点，但是杂点不太影响图片识别，杂点只是少数几个点
取一个临界值，如果能匹配的像素点达到这个值，则代表识别成功。我取的值为90

下面是识别效果
<img src="http://veryyoung.u.qiniudn.com/7niu_coderesult.png" alt="" />

亲测识别率为100%

当然,这是因为我们学校教学管理平台的验证码太过于规则,没有太多的杂点和扭曲,也没有任何的交叉,所以才能破解成功.

本人水平有限,只能破解这样简单的验证码,大致思路就是这样的,over!
