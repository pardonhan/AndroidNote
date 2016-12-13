#  Android Handler 机制学习记录

## Handler 作用
	
	包含线程队列和消息队列，实现异步的消息处理机制：
		
		1.运行在某个线程上，共享线程的消息队列。
		2.接收消息、调度消息，派发消息，和处理消息；
		3.实现消息的异步处理。

## Handler简单使用
```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    private TextView tv;

    private Handler handler = new Handler(){

        @Override
        public void handleMessage(Message msg) {
        	if(msg.what ==0){
        		tv.setText("got msg!!");
        	}
            
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        tv = (TextView)findViewById(R.id.show);
    }

     @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.show:
                post();
                break;
        }
    }

    public void post(View view){
    	 new Thread(){
            @Override
            public void run() {
                super.run();
                // 省略代码，进行网络请求，数据库，文件等耗时操作
                handler.sendEmptyMessage(0);
            }
        }.start();
       
    }
}
```
