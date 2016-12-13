## SwipeRefreshLayout+RecyclerView之EmptyView展示

 	在使用RecyclerView的时候，有时是需要在没有数据的时候展示EmptyView的。
 	类似淘宝上的没有相关订单的提示如图，

 	记录一下实现这个功能的方法：

### 创建EmptyView的布局---layout_empty_view.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:id="@+id/iv_empty"
        android:layout_width="90dp"
        android:layout_height="90dp"
        android:layout_marginBottom="10dp"
        android:layout_centerHorizontal="true"
        android:layout_above="@+id/empty_tip_tv"
        android:src="@drawable/icon_empty"
        android:tint="#ABABAB" />

    <TextView
        android:id="@+id/empty_tip_tv"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@+id/empty_msg_tv"
        android:gravity="center"
        android:layout_centerHorizontal="true"
        android:text="您还没有相关的订单"
        android:textSize="18sp" />

    <TextView
        android:id="@+id/empty_msg_tv"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:layout_marginTop="5dp"
        android:text="可以去看看有哪些想买的"
        android:textSize="12sp" />
</RelativeLayout>

```

### 创建EmptyView的 Holder ----EmptyViewHolder.java
```java
public class EmptyViewHolder extends RecyclerView.ViewHolder {
    @BindView(R.id.iv_empty)
    public ImageView img;
    @BindView(R.id.empty_tip_tv)
    public TextView tipTv;
    @BindView(R.id.empty_msg_tv)
    public TextView msgTv;

    public EmptyViewHolder(View itemView) {
        super(itemView);
        ButterKnife.bind(this, itemView);
    }
}
```

### 创建Adapter---RecyclerAdapter.java
```java
public class RecyclerAdapter extends RecyclerView.Adapter<RecyclerView.ViewHolder> {
    private Context mContext;
    private List<Object> list;
    private String status;
    private static final int EMPTY_VIEW = 1;

    public RecyclerAdapter(Context context, List<Object> list, String status) {
        this.mContext = context;
        this.list = list;
        this.status = status;
    }

    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        LayoutInflater inflater = LayoutInflater.from(parent.getContext());
        if (viewType == EMPTY_VIEW) {
            View view = inflater.inflate(R.layout.layout_empty_view, parent, false);
            return new EmptyViewHolder(view);
        } else {
            View view = inflater.inflate(R.layout.activity_wait_goods_parent_item, parent, false);
            return new OtherViewHodler(view);
        }
    }

    @Override
    public void onBindViewHolder(RecyclerView.ViewHolder itemHolder, int position) {
        Log.d("TAG",itemHolder);
        if (itemHolder instanceof OtherViewHodler) {
            OtherViewHodler holder = (OtherViewHodler) itemHolder;
            // 其他操作
        }
    }

    @Override
    public int getItemCount() {
        return list.size() > 0 ? list.size() : 1;
    }

    @Override
    public int getItemViewType(int position) {
        if (list.size() == 0) {
            return EMPTY_VIEW;
        }
        return super.getItemViewType(position);
    }
}

```
关键部位就在 ```getItemViewType(int position)``` 方法，
该方法默返回0
在该方法中判断数据源的个数，为空的时候返回为空的值，加载不同的ViewHolder