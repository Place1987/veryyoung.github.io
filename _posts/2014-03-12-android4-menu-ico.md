---
layout: post
title: 解决android4.0系统中菜单(Menu)添加Icon无效问题
date: 2014-03-12 15:54
author: VERYYOUNG
comments: true
categories: [Android]
---
在Android4.0系统中，创建菜单Menu，通过setIcon方法给菜单添加图标是无效的，图标没有显出来，2.3系统中是可以显示出来的。这个问题的根本原因在于4.0系统中，涉及到菜单的源码类 MenuBuilder做了改变，该类的部分源码如下：


	public class MenuBuilder implements Menu {
	...
	private boolean mOptionalIconsVisible = false;
	....
	    void setOptionalIconsVisible(boolean visible) {
	        mOptionalIconsVisible = visible;
	    }
	
	    boolean getOptionalIconsVisible() {
	        return mOptionalIconsVisible;
	    }
	...
	}


   上面的代码中，mOptionalIconsVisible成员初始值默认为false，这就是为什么给菜单设置图标没有效果的原因；

  所以，只要我们在创建菜单时通过调用setOptionalIconsVisible方法设置mOptionalIconsVisible为true就可以了；这时候问题来了，要想调用该方法，就需要创建MenuBuilder对象，但是，我们是无法在开发的应用程序中创建MenuBuilder这个对象的（MenuBuilder为系统内部的框架类）；


   这时候就需要考虑用反射了，在代码运行创建菜单的时候通过反射调用setOptionalIconsVisible方法设置mOptionalIconsVisible为true，然后在给菜单添加Icon，这样就可以在菜单中显示添加的图标了；


  代码实现如下：

	
	import java.lang.reflect.Method;
	
	import android.app.Activity;
	import android.os.Bundle;
	import android.util.Log;
	import android.view.Menu;
	import android.view.MenuItem;
	
	public class MainActivity extends Activity {
	    /** Called when the activity is first created. */
	    @Override
	    public void onCreate(Bundle savedInstanceState)
	    {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.main);
	    }
	
		@Override
		    @Override
	    public boolean onCreateOptionsMenu(Menu menu) {
	
	        setIconEnable(menu, true);
	        getMenuInflater().inflate(R.menu.main, menu);
	        return super.onCreateOptionsMenu(menu);
	    }
	
	    @Override
	    public boolean onOptionsItemSelected(MenuItem item) {
	        Toast toast = Toast.makeText(this, &quot;这是个Menu菜单的练习&quot;, Toast.LENGTH_SHORT);
	        toast.show();
	        return super.onOptionsItemSelected(item);
	    }
	
	    //enable为true时，菜单添加图标有效，enable为false时无效。4.0系统默认无效
	    private void setIconEnable(Menu menu, boolean enable) {
	        try {
	            Class&lt;?&gt; clazz = Class.forName(&quot;com.android.internal.view.menu.MenuBuilder&quot;);
	            Method m = clazz.getDeclaredMethod(&quot;setOptionalIconsVisible&quot;, boolean.class);
	            m.setAccessible(true);
	
	            //MenuBuilder实现Menu接口，创建菜单时，传进来的menu其实就是MenuBuilder对象(java的多态特征)
	            m.invoke(menu, enable);
	
	        } catch (Exception e) {
	            e.printStackTrace();
	        }
	    }
	
	}



效果如下：

<img src="http://veryyoung.u.qiniudn.com/7niu_menuwithico.png" alt="http://veryyoung.u.qiniudn.com/7niu_menuwithico.png" />


