# AutoSwipe
##这是一个自动刷新的官方SwipeRefreshLayout控件，只增加自动刷新方法，其他方法不变
 ![image](https://github.com/zynote/AutoSwipe/blob/master/app/ts.gif)
 
 ##重写SwipeRefreshLayout
 
 public class AutoSwipeRefreshLayout extends SwipeRefreshLayout {
 
    public AutoSwipeRefreshLayout(Context context) {
        super(context);
    }

    public AutoSwipeRefreshLayout(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    /**
     * 自动刷新
     */
    public void autoRefresh() {
        try {
            Field mCircleView = SwipeRefreshLayout.class.getDeclaredField("mCircleView");//获取下拉进度条动画的控件
            mCircleView.setAccessible(true);
            View progress = (View) mCircleView.get(this);
            progress.setVisibility(VISIBLE);
            
            //获取刷新函数
            Method setRefreshing = SwipeRefreshLayout.class.getDeclaredMethod("setRefreshing", boolean.class, boolean.class);
            setRefreshing.setAccessible(true);
            setRefreshing.invoke(this, true, true);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

##调用
  AutoSwipeRefreshLayout swipeLayout = (AutoSwipeRefreshLayout) findViewById(R.id.swipeLayout);
  swipeLayout.autoRefresh();
