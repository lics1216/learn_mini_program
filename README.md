#### 小程序前端入门
>1. 对页面结构不熟悉，可以看一下，入门小程序

#### 一、了解小程序页面结构
1. [下载微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html), 并创建一个用户授权显示头像的示例小程序。
2. [阅读小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/)
    * 指南，到自定义组件（**可以先不看**）
    * 框架，理解WXML/WXS
3. 理解 示例小程序基本配置，和页面组成逻辑


####  二、写页面
写小程序页面和html/css 写页面是一样的，如果你对html/css 页面布局不是很熟悉，可以参考下面步骤
1. [元素怎样组成页面](https://lics1216.github.io/2018/09/25/html+css/#more)
2. [可以先利用 绝对、相对布局写html/css 页面](https://git.mingchao.com/lichangsong/miniTest)
3. 如果发现元素老是没法 垂直居中，可以学习 flex布局
4. [再学习慢慢接触 css细节](https://www.runoob.com/css/css-tutorial.html)

#### 三、处理用户 openid 
[小程序前后端交互过程](https://www.jianshu.com/p/0b03cbb73e6f)
1. wx.login()获得code，传给后台服务器
2. 后台服务器请微信服务器请求，返回openId/sessionKey（用于获取用户已授权的其他数据，如运动步数），后台把openId/sessionKey存储在session，前端header里就会得到一个set-cookie 
3. 小程序前端要缓存（setStorageSync），每次请求携带cookie，后台就可以判断是哪个用户，这个过程要自己实现（和浏览器不一样）
4. 后台可以设置session 的时长，当用户放置打开的小程序几十分钟，session 是否失效

#### 四、自定义组件
小程序中如果一个页面UI太过复杂，亦或者某个UI组件复用次数多，可以考虑抽取出自定组件。抽离组件可以
1. **分而治之**，使代码结构更清晰，也是重构的目的。
2. **复用**，使逻辑出现在唯一处

学习可以参考下面步骤
1. [阅读官方文档 自定义组件模块](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/)
2. [实践一下](https://git.mingchao.com/lichangsong/miniTest)
3. [可以阅读这篇抽离组件的总结，不懂vue 没关系](https://www.jianshu.com/p/82ffcf1eba20)

#### 五、遇到过的前端 bug
1. 图片展示要设置 懒加载，手机很容易发烫
```
<image src='xx' lazy-load/>
```
2. ios 下video 出问题，无法部分视频
```
# 设置 video 属性
custom-cache="{{false}}"  
```
3. video 组件数量一个页面不能超过三个，建议用image 代替video，点击时替换
4. video 设置静音播放后，在安卓机器点击 取消静音 无效
5. 长列表数据导致页面加载很慢，比如不断触发下拉刷新函数，加载数据时