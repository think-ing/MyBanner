# MyBanner
图片轮播

# Banner的功能主要有：

实现图片 & 标语展示
循环播放
支持手动切换
支持加载本地 & 网络图片


# 实现步骤：
### 步骤1. 加入依赖包
compile 'com.youth.banner:banner:1.1.5'  //指定版本

### 步骤2. 在需要展示的布局定义Banner布局
<com.youth.banner.Banner   
 xmlns:app="http://schemas.android.com/apk/res-auto"  
  android:id="@+id/banner"    
  android:layout_width="match_parent" 
  android:layout_height="300dp" />


### 步骤3. 在MainActivity布局中定义配置Banner
public class MainActivity extends AppCompatActivity {

    private Banner banner;
    //设置图片资源:url或本地资源
    String[] images= new String[] {
            "http://218.192.170.132/BS80.jpg",
            "http://img.zcool.cn/community/0166c756e1427432f875520f7cc838.jpg",
            "http://img.zcool.cn/community/018fdb56e1428632f875520f7b67cb.jpg",
            "http://img.zcool.cn/community/01c8dc56e1428e6ac72531cbaa5f2c.jpg",
            "http://img.zcool.cn/community/01fda356640b706ac725b2c8b99b08.jpg",
            "http://img.zcool.cn/community/01fd2756e142716ac72531cbf8bbbf.jpg",
            "http://img.zcool.cn/community/0114a856640b6d32f87545731c076a.jpg"};

    //设置图片标题:自动对应
    String[] titles=new String[]{
            "十大星级品牌联盟，全场2折起",
            "全场2折起","十大星级品牌联盟",
            "嗨购5折不要停",
            "12趁现在",
            "嗨购5折不要停，12.12趁现在",
            "实打实大顶顶顶顶"};
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        banner = (Banner) findViewById(R.id.banner);

        //设置样式,默认为:Banner.NOT_INDICATOR(不显示指示器和标题)
        //可选样式如下:
        //1. Banner.CIRCLE_INDICATOR    显示圆形指示器
        //2. Banner.NUM_INDICATOR   显示数字指示器
        //3. Banner.NUM_INDICATOR_TITLE 显示数字指示器和标题
        //4. Banner.CIRCLE_INDICATOR_TITLE  显示圆形指示器和标题
        banner.setBannerStyle(Banner.CIRCLE_INDICATOR_TITLE);

        //设置轮播样式（没有标题默认为右边,有标题时默认左边）
        //可选样式:
        //Banner.LEFT   指示器居左
        //Banner.CENTER 指示器居中
        //Banner.RIGHT  指示器居右
        banner.setIndicatorGravity(Banner.CENTER);

        //设置轮播要显示的标题和图片对应（如果不传默认不显示标题）
        banner.setBannerTitle(titles);

        //设置是否自动轮播（不设置则默认自动）
        banner.isAutoPlay(true) ;

        //设置轮播图片间隔时间（不设置默认为2000）
        banner.setDelayTime(5000);
        //设置图片资源:可选图片网址/资源文件，默认用Glide加载,也可自定义图片的加载框架
        //所有设置参数方法都放在此方法之前执行
        //banner.setImages(images);

        //自定义图片加载框架
        banner.setImages(images, new Banner.OnLoadImageListener() {
            @Override
            public void OnLoadImage(ImageView view, Object url) {
                System.out.println("加载中");
                Glide.with(getApplicationContext()).load(url).into(view);
                System.out.println("加载完");
            }
        });
        //设置点击事件，下标是从1开始
        banner.setOnBannerClickListener(new Banner.OnBannerClickListener() {//设置点击事件
            @Override
            public void OnBannerClick(View view, int position) {
                Log.i("---mzw---","你点击了：" + position);
            }
        });
    }
}


### 步骤4. 在Manifest加入网络请求权限
<uses-permission android:name="android.permission.INTERNET"/>

拷贝自：https://www.jianshu.com/p/d229a647e705
亲测OK
