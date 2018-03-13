# GraphLearn
Something to learn at my leisure


# 福利社1.2迭代
### 1、需求
>* 需求链接：  `https://pro.modao.cc/app/y1w0vvfYzEGs1NMpIXMIlq1Ul3PiFUn#screen=s95F68145581506478436605`
>* 需求添加：
    ① 变更福利社首页，添加可配置的新首页
    ② 新增限时抢购（抢购中和即将开始）
    ③ 添加优惠券，包括领券中心，商品页面优惠券领取，优惠券下单等
    
### 2、新增首页
>* 新增首页实现是使用Recycleriew的多布局实现的，每一个布局都是后台可配置的，通过后台传递的类型参数进行区别。（注意以后新版本新加类型的兼容问题。。。。。）
>* 首页的下拉刷新是使用的IRecyclerView（整体带有下拉加载布局都是选用的IRecyclerView）附上github链接：`https://github.com/Aspsine/IRecyclerView`(项目将源码拷贝下来，做了一些自定义)
>* 首页的RecyclerView使用的适配器方式是采用的section方式区分多布局逻辑。使用链接：`https://github.com/drakeet/Effective-MultiType/blob/master/README.md`
>* 不同条目的跳转也是后台动态配置：①专题列表 ②专题详情 ③商品详情 ④淘宝客的内跳链接 ⑤领券中心 ⑥其他类型（web页面内链和外链）
>* 之前的主页修改为专题列表页面

### 3、新增限时抢购
>* 限时抢购页面分为进行中和即将开抢页面，点击商品可以跳转到商品页面,商品页面会有相对应的状态。
>* 限时抢购主逻辑回调 
```   
        //刷新两个页面（所有）
        MallCallBack.getInstance().setUpDateAllFlashSaleInfoListener(this);
        //两个页面加载失败的回掉
        MallCallBack.getInstance().setupdateErrorInfoListener(this);
        //活动动态消失时候（浏览页面时纯在活动，浏览中活动关闭的监听，用于关闭已关掉的活动页面）
        MallCallBack.getInstance().setNoActivityListener(this);
        //活动时间结束，刷新两个页面（连个页面里面内容都刷新）
        MallCallBack.getInstance().setNeedRefreshAllListener(this);
        //刷新完成，关闭loading的回掉
        MallCallBack.getInstance().setRefreshFinishListener(this);
```
> 以上为限时抢购页面的逻辑回掉
>* 限时抢购为LinearLayout + ViewPager， 如果数据中只有一天的限时抢购，没有即将开抢页面，隐藏顶部标题栏。

### 4、优惠券
>* 商品优惠券
   1、商品优惠券是在商品详情页面，点击领取优惠券，弹出pop，根据商品的id领取相关优惠券。
>* 下单页面优惠券
   1、下单页面，可选优惠券操作，每次进入下单页面默认选择最优优惠券（最有优惠券由服务端提供）。点击选择优惠券（如果有优惠券可以领），弹出pop，选择优惠券。
>* 领券中心，领取优惠券页面，可以通过直接领取，积分兑换，兑换码兑换等方式获取。具体标记代码中会有介绍





# 福利社1.3版本迭代
### 1、需求
>* 需求链接： `https://pro.modao.cc/app/46ab4b1be1d08191474de1ed0a69c61390d1da65#screen=s721A3DA0861511748846791`
>* 需求添加：①订单服务中添加包裹概念，订单的最小原子定位到包裹，一个订单可以分为多包裹。②添加美人笔记模块，订单页面评论笔记，商品页面可查看笔记。③专题添加富文本内容。

### 2、订单添加多包裹
>* 接口修改，订单服务接口基本全部修改为带包裹的接口，包括售后部分。
>* 订单列表页面添加多包裹类型（列表类型），并且规范按钮的长度（区分三个字和四个字的按钮长度）。订单详情页面相同，添加多包裹的新类型。`public static final int ITEM_PACKAGE = 6`   `private static final int ITEM_INCOMPLETE_SEND = 4;//包含新增不完全发货的订单类型`

### 3、美人笔记
>* 订单页面可以发布美人笔记，订单在用户选择收货成功之后。发布订单的按钮会显示出来（订单列表页面和订单详情页面），跳转到发布笔记页面（注意笔记发布和显示许要进行），图片发布先上传oss，之后将url发布到笔记后台。
>* 商品页面显示笔记，商品详情页面可拖动的笔记列，附带贝塞尔曲线阴影效果（根据拖动距离动态计算）。
>* 笔记详情页面，由商品页笔记标签跳转，并动态滚动到相应位置。笔记页面点击查看大图由共享元素实现。

### 4、专题详情
>* 富文本添加，使用webView加载富文本。
