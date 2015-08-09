---
layout: post
title: Android中线程和进度条的使用
date: 2013-11-08 20:16
author: VERYYOUNG
comments: true
categories: [Android]
---
当涉及到耗时的任务时，要用到进度条提示，也就是工作者线程和UI主线程的交互问题。
Andriod提供了几种在其他线程中访问UI线程的方法。

	Activity.runOnUiThread( Runnable )
	View.post( Runnable )
	View.postDelayed( Runnable, long )

---
下面给出两个例子分别用handler和runOnUiThread访问UI主线程。

1、使用handler，普通进度条控件

	TextView tvShowMessage; 
	Message message=null;    
	Handler handler = new Handler() { 
     public void handleMessage(Message msg) {  
            switch (msg.what) {      
            case 1:  
                tvShowMessage.setText("步骤一");                         
                break; 
            case 2: 
                tvShowMessage.setText("步骤二"); 
                break; 
            case 3:                   
                 tvShowMessage.setText("步骤三"); 
                break;
            }      
            super.handleMessage(msg);  
        }  
	};

	class myThread implements Runnable {    
	          public void run() {   
	               message = new Message();      
	              message.what = 1;      
	              handler.sendMessage(message);              
	   
	              try { 
	                  Thread.sleep(500); 
	            } catch (InterruptedException e1) { 
	                // TODO Auto-generated catch block 
	                e1.printStackTrace(); 
	            } 
	            message = new Message();      
	            message.what = 2;      
	            handler.sendMessage(message); 
	              try { 
	                  Thread.sleep(500); 
	            } catch (InterruptedException e1) { 
	                // TODO Auto-generated catch block 
	                e1.printStackTrace(); 
	            }
		message = new Message();      
	            message.what = 3;      
	            handler.sendMessage(message);
			}
		}




	@Override 
    protected void onCreate(Bundle savedInstanceState) { 
        super.onCreate(savedInstanceState);
        // Request for the progress bar to be shown in the title 
        requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS); 
        setContentView(R.layout.main); 
        tvShowMessage=(TextView)findViewById(R.id.tvShowMessage); 
        setProgressBarVisibility(true);     // Make sure the progress bar is visible 
        new Thread(new myThread()).start();//启动线程   
    }


2、进度条对话框

	private ProgressDialog m_ProgressDialog = null; 
	private Runnable viewOrders;
	try { 
	     //用线程启动进度条 
	       viewOrders = new Runnable(){ 
	           @Override 
	           public void run() { 
	               dosomething(); 
	           } 
	       }; 
	       Thread thread =  new Thread(null, viewOrders, "Background"); 
	       thread.start(); 
	       m_ProgressDialog = ProgressDialog.show(CarSourceAdd.this,    
	             "加载中", "请稍等...", true); 
	} 
	catch(Exception e) { 
	     //。。。 
	}
 
    private void dosomething() 
    { 
          try { 
       //耗时工作。。。
        } catch (Exception e) { 
            // TODO Auto-generated catch block 
            e.printStackTrace(); 
        }     
      runOnUiThread(returnRes); 
    } 
    private Runnable returnRes = new Runnable() { 
        @Override 
        public void run() { 
            m_ProgressDialog.dismiss(); 
            //执行成功后。。。 
        } 
    };

