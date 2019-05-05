---
title: Hexo+icarus主题配置
date: 2019-04-29 17:31:10
tags: Hexo
categories: 教程 
thumbnail: false
comments: true
toc: true
disqusId: ccyhweb
---


---

## 下载icarus主题

1. 进入博客主目录，点击鼠标右键Git Bash Here,进入命令行界面
<!-- more -->
2. 输入：
```bash
git clone https://github.com/ppoffice/hexo-theme-icarus themes/icarus
```

3. 打开themes文件夹，就会发现多了一个icarus文件夹，这就是主题的所有文件


---

## 配置主题
1. 更改站点配置文件_config.yml,将主题改为icarus
```yml
theme: icarus
```
2. Icarus文件目录概览：
![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+icarus主题配置/20190429082811950.png)
>*  $config.yml$是主题的配置文件
>* $/layout$ 文件夹中是主题各种模板文件
>* 我们主要的超作就是在这两个文件中了

---

### 主题配置文件（部分）
```yml
# Version of the Icarus theme that is currently used
version: 2.3.0
# 你的网站图标，可以搜索在线图标制作，并将其放在images文件夹中
favicon: /images/favicons.ico
# Path or URL to RSS atom.xml
rss: /atom.xml
# 显示在导航栏左侧的网站logo，同样可以自己制作
logo: /images/gen.svg
# Open Graph metadata
# https://hexo.io/docs/helpers.html#open-graph
open_graph:
    # Facebook App ID
    fb_app_id: 
    # Facebook Admin ID
    fb_admins: 
    # Twitter ID
    twitter_id: 
    # Twitter site
    twitter_site: 
    # Google+ profile link
    google_plus: 
#  导航栏
navbar:
    #菜单（显示名称：对应文件夹）
    menu:
        主页: /
        归档: /archives
        分类: /categories
        标签: /tags
        关于: /about   
    # 导航栏右侧图标链接
    links:
        My GitHub:
            icon: fab fa-github
            url: '你的gityhub地址'
# Footer section link settings
footer:
    # 页脚图标链接
    links:
        Creative Commons:
            icon: fab fa-creative-commons
            url: 'https://creativecommons.org/'
        Attribution 4.0 International:
            icon: fab fa-creative-commons-by
            url: 'https://creativecommons.org/licenses/by/4.0/'
        Download on GitHub:
            icon: fab fa-github
            url: 'http://github.com/ppoffice/hexo-theme-icarus'
# 文章显示设置
article:
    # Code highlight theme
    # https://github.com/highlightjs/highlight.js/tree/master/src/styles
    #代码主题atom-one-light亮色，atom-one-dark暗色
    highlight: atom-one-dark
    # 是否显示文章主图
    thumbnail: true
    # 是否显示估算阅读时间
    readtime: true
# 搜索插件设置
# http://ppoffice.github.io/hexo-theme-icarus/categories/Configuration/Search-Plugins
search:
    # Name of the search plugin
    type: insight
# 评论插件设置
# http://ppoffice.github.io/hexo-theme-icarus/categories/Configuration/Comment-Plugins
comment:
    #可选valine，disqus（科学上网）等
    # Name of the comment plugin
    #type: valine
    #app_id: 不为空
    #app_key: 不为空
    #notify: true
    #verify: true
    #placeholder:
    type: disqus
    shortname: 不能为空
# 打赏功能
# http://ppoffice.github.io/hexo-theme-icarus/categories/Donation/
donate:
    -
        # 阿里巴巴支付宝
        type: alipay
        # 二维码图片
        qrcode: '/images/honbao.PNG'
    -
        # 微信
        type: wechat
        # 二维码图片
        qrcode: '/images/yjtp.png'
    -
# 分享插件设置
# http://ppoffice.github.io/hexo-theme-icarus/categories/Configuration/Share-Plugins
share:
    # 插件类型，有多种，可选，自行百度
    type: sharejs
# Sidebar settings.
# Please be noted that a sidebar is only visible when it has at least one widget
sidebar:
    # 左侧边栏设置
    left:
        # 是否不随页面滚动
        # http://ppoffice.github.io/hexo-theme-icarus/Configuration/Theme/make-a-sidebar-sticky-when-page-scrolls/
        sticky: false
    # 右侧边栏设置
    right:
        # 是否不随页面滚动
        # http://ppoffice.github.io/hexo-theme-icarus/Configuration/Theme/make-a-sidebar-sticky-when-page-scrolls/
        sticky: false
# 边栏小部件设置
# http://ppoffice.github.io/hexo-theme-icarus/categories/Widgets/
widgets:
    -
        # 个人信息
        type: profile
        # 部件位置（左）
        position: left
        # 作者名（字符串）
        author: 飞鱼
        # 作者身份描述（字符串）
        author_title: Student
        # 作者当前居住地
        location: China,Fujian
        # 头像（可用本地图片或网络图片链接）
        avatar: '/images/ava.png'
        # Email address for the Gravatar to be shown in the profile widget
        gravatar: 
        # 关注我的链接，可设为你的GitHub主页
        follow_link: 'https://github.com/yourname'
        # 个人介绍部件底部图标社交链接
        social_links:
            Github:
                icon: fab fa-github
                url: 'https://github.com/yourname'
            Facebook:
                icon: fab fa-facebook
                url: 'https://facebook.com'
            Twitter:
                icon: fab fa-twitter
                url: 'https://twitter.com/yourname'
            RSS:
                icon: fas fa-rss
                url: /
    -
        # Widget name
        type: toc
        # Where should the widget be placed, left or right
        position: left
    -
        # 分类
        type: category
        # 位置指定
        position: left
    -
        # 标签云
        type: tagcloud
        # 位置
        position: right
    -
        # 近期文章
        type: recent_posts
        # 位置
        position: left
    -
        # 归档
        type: archive
        # Where should the widget be placed, left or right
        position: right
    -
        # 标签
        type: tag
        # Where should the widget be placed, left or right
        position: right
    -
        # 外部链接
        type: links
        # Where should the widget be placed, left or right
        position: left
        # Links to be shown in the links widget
        links:
            Google: 'https://google.com'
            Baidu: 'https://baidu.com'
```
上述设置已经让你的博客稍微有点属于你的样子了，下面来添加一些有意思的元素。

---
### 添加雪花飘落效果
* 在 $\color{DarkTurquoise}{/themes/icarus/sourse/js/src}$目录下新建一个 snow.js 文件(若没有src/文件夹可以自己新建)，复制粘贴以下代码：
** 样式1：六边形雪花 **
```javascript
(function($){
	$.fn.snow = function(options){
	var $flake = $('').css({'position': 'absolute','z-index':'9999', 'top': '-50px'}).html('❄'),
	documentHeight 	= $(document).height(),
	documentWidth	= $(document).width(),
	defaults = {
		minSize		: 10,
		maxSize		: 20,
		newOn		: 1000,
		flakeColor	: "#AFDAEF" /* 此处可以定义雪花颜色，若要白色可以改为#FFFFFF */
	},
	options	= $.extend({}, defaults, options);
	var interval= setInterval( function(){
	var startPositionLeft = Math.random() * documentWidth - 100,
	startOpacity = 0.5 + Math.random(),
	sizeFlake = options.minSize + Math.random() * options.maxSize,
	endPositionTop = documentHeight - 200,
	endPositionLeft = startPositionLeft - 500 + Math.random() * 500,
	durationFall = documentHeight * 10 + Math.random() * 5000;
	$flake.clone().appendTo('body').css({
		left: startPositionLeft,
		opacity: startOpacity,
		'font-size': sizeFlake,
		color: options.flakeColor
	}).animate({
		top: endPositionTop,
		left: endPositionLeft,
		opacity: 0.2
	},durationFall,'linear',function(){
		$(this).remove()
	});
	}, options.newOn);
    };
})(jQuery);
$(function(){
    $.fn.snow({ 
	    minSize: 5, /* 定义雪花最小尺寸 */
	    maxSize: 50,/* 定义雪花最大尺寸 */
	    newOn: 300  /* 定义密集程度，数字越小越密集 */
    });
});

作者：donlex
链接：http://www.imooc.com/article/272005
```
** 样式2：圆点状雪花 **
```javascript
function snowFall(snow) {
    /* 可配置属性 */
    snow = snow || {};
    this.maxFlake = snow.maxFlake || 200;   /* 最多片数 */
    this.flakeSize = snow.flakeSize || 10;  /* 雪花形状 */
    this.fallSpeed = snow.fallSpeed || 1;   /* 坠落速度 */
}
/* 兼容写法 */
requestAnimationFrame = window.requestAnimationFrame ||
    window.mozRequestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.msRequestAnimationFrame ||
    window.oRequestAnimationFrame ||
    function(callback) { setTimeout(callback, 1000 / 60); };

cancelAnimationFrame = window.cancelAnimationFrame ||
    window.mozCancelAnimationFrame ||
    window.webkitCancelAnimationFrame ||
    window.msCancelAnimationFrame ||
	window.oCancelAnimationFrame;
/* 开始下雪 */
snowFall.prototype.start = function(){
    /* 创建画布 */
    snowCanvas.apply(this);
    /* 创建雪花形状 */
    createFlakes.apply(this);
    /* 画雪 */
    drawSnow.apply(this)
}
/* 创建画布 */
function snowCanvas() {
    /* 添加Dom结点 */
    var snowcanvas = document.createElement("canvas");
    snowcanvas.id = "snowfall";
    snowcanvas.width = window.innerWidth;
    snowcanvas.height = document.body.clientHeight;
    snowcanvas.setAttribute("style", "position:absolute; top: 0; left: 0; z-index: 1; pointer-events: none;");
    document.getElementsByTagName("body")[0].appendChild(snowcanvas);
    this.canvas = snowcanvas;
    this.ctx = snowcanvas.getContext("2d");
    /* 窗口大小改变的处理 */
    window.onresize = function() {
        snowcanvas.width = window.innerWidth;
        /* snowcanvas.height = window.innerHeight */
    }
}
/* 雪运动对象 */
function flakeMove(canvasWidth, canvasHeight, flakeSize, fallSpeed) {
    this.x = Math.floor(Math.random() * canvasWidth);   /* x坐标 */
    this.y = Math.floor(Math.random() * canvasHeight);  /* y坐标 */
    this.size = Math.random() * flakeSize + 2;          /* 形状 */
    this.maxSize = flakeSize;                           /* 最大形状 */
    this.speed = Math.random() * 1 + fallSpeed;         /* 坠落速度 */
    this.fallSpeed = fallSpeed;                         /* 坠落速度 */
    this.velY = this.speed;                             /* Y方向速度 */
    this.velX = 0;                                      /* X方向速度 */
    this.stepSize = Math.random() / 30;                 /* 步长 */
    this.step = 0                                       /* 步数 */
}
flakeMove.prototype.update = function() {
    var x = this.x,
        y = this.y;
    /* 左右摆动(余弦) */
    this.velX *= 0.98;
    if (this.velY <= this.speed) {
        this.velY = this.speed
    }
    this.velX += Math.cos(this.step += .05) * this.stepSize;

    this.y += this.velY;
    this.x += this.velX;
    /* 飞出边界的处理 */
    if (this.x >= canvas.width || this.x <= 0 || this.y >= canvas.height || this.y <= 0) {
        this.reset(canvas.width, canvas.height)
    }
};
/* 飞出边界-放置最顶端继续坠落 */
flakeMove.prototype.reset = function(width, height) {
    this.x = Math.floor(Math.random() * width);
    this.y = 0;
    this.size = Math.random() * this.maxSize + 2;
    this.speed = Math.random() * 1 + this.fallSpeed;
    this.velY = this.speed;
    this.velX = 0;
};
// 渲染雪花-随机形状（此处可修改雪花颜色！！！）
flakeMove.prototype.render = function(ctx) {
    var snowFlake = ctx.createRadialGradient(this.x, this.y, 0, this.x, this.y, this.size);
    snowFlake.addColorStop(0, "rgba(255, 255, 255, 0.9)");  /* 此处是雪花颜色，默认是白色 */
    snowFlake.addColorStop(.5, "rgba(255, 255, 255, 0.5)"); /* 若要改为其他颜色，请自行查 */
    snowFlake.addColorStop(1, "rgba(255, 255, 255, 0)");    /* 找16进制的RGB 颜色代码。 */
    ctx.save();
    ctx.fillStyle = snowFlake;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fill();
    ctx.restore();
};
/* 创建雪花-定义形状 */
function createFlakes() {
    var maxFlake = this.maxFlake,
        flakes = this.flakes = [],
        canvas = this.canvas;
    for (var i = 0; i < maxFlake; i++) {
        flakes.push(new flakeMove(canvas.width, canvas.height, this.flakeSize, this.fallSpeed))
    }
}
/* 画雪 */
function drawSnow() {
    var maxFlake = this.maxFlake,
        flakes = this.flakes;
    ctx = this.ctx, canvas = this.canvas, that = this;
    /* 清空雪花 */
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for (var e = 0; e < maxFlake; e++) {
        flakes[e].update();
        flakes[e].render(ctx);
    }
    /*  一帧一帧的画 */
    this.loop = requestAnimationFrame(function() {
        drawSnow.apply(that);
    });
}
/* 调用及控制方法 */
var snow = new snowFall({maxFlake:60});
snow.start();

作者：donlex
链接：http://www.imooc.com/article/272005
```
* 最后在$\color{DarkTurquoise}{/themes/icarus/layout/layout.ejs}$的$body$标签中添加代码：
```html
<!-- 雪花特效 -->
    <script type="text/javascript">
      var windowWidth = $(window).width();
      if (windowWidth > 480) {
        document.write('<script type="text/javascript" src="/js/src/snow.js"><\/script>');
      }
    </script>
```
* 默认雪花为白色，可自行更改颜色，效果可见本站

---

### 网站访问量与访客量统计
* 不蒜子官网：http://busuanzi.ibruce.info/
* 在$\color{DarkTurquoise}{/themes/icarus/layout/common/footer.ejs}$模板文件的中添加如下代码：
```html
<span id="busuanzi_container_site_pv" class="theme-info">
  |  本站总访问量<span id="busuanzi_value_site_pv">span>次
 span>
 <span id="busuanzi_container_site_uv" class="theme-info">
  |  本站访客数<span id="busuanzi_value_site_uv">span>人次
 span>

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">script>
```
* 在$\color{DarkTurquoise}{/themes/icarus/\_config.yml}$中添加：
```yml
busuanzi:
    enable: true
```
* 最终效果：
<div align=center>
![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+icarus主题配置/20190429093801600.png)
</div>
### 网站运行时间统计
* 在$\color{DarkTurquoise}{/themes/icarus/layout/common/footer.ejs}$中添加：
```html
<span id="timeDate">载入天数...</span><span id="times">载入时分秒...</span>
            <script>
                var now = new Date(); 
                function createtime() { 
                    var grt= new Date("12/28/2018 12:49:00");//此处修改你的建站时间或者网站上线时间 
                    now.setTime(now.getTime()+250); 
                    days = (now - grt ) / 1000 / 60 / 60 / 24; dnum = Math.floor(days); 
                    hours = (now - grt ) / 1000 / 60 / 60 - (24 * dnum); hnum = Math.floor(hours); 
                    if(String(hnum).length ==1 ){hnum = "0" + hnum;} minutes = (now - grt ) / 1000 /60 - (24 * 60 * dnum) - (60 * hnum); 
                    mnum = Math.floor(minutes); if(String(mnum).length ==1 ){mnum = "0" + mnum;} 
                    seconds = (now - grt ) / 1000 - (24 * 60 * 60 * dnum) - (60 * 60 * hnum) - (60 * mnum); 
                    snum = Math.round(seconds); if(String(snum).length ==1 ){snum = "0" + snum;} 
                    document.getElementById("timeDate").innerHTML = "本站已安全运行 "+dnum+" 天 "; 
                    document.getElementById("times").innerHTML = hnum + " 小时 " + mnum + " 分 " + snum + " 秒"; 
                } 
            setInterval("createtime()",250);
            </script>
```
* 修改自己的建站时间
* 最终效果：
<div align=center>
![](https://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+icarus主题配置/20190429094726470.png)
</div>

---

### 鼠标点击特效
* 在 $\color{DarkTurquoise}{/themes/icarus/sourse/js/src}$中添加click.js文件，复制以下代码进去：
```js
!function(e,t,a){
    function n(){
        c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),
        o(),
        r()
    }
    function r(){
        for(var e=0;e<d.length;e++)
            d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");
        requestAnimationFrame(r)
    }
    function o(){
        var t="function"==typeof e.onclick&&e.onclick;
        e.onclick=function(e){
            t&&t(),i(e)
        }
    }function i(e){
            var a=t.createElement("div");
            a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)
    }
    function c(e){
        var a=t.createElement("style");a.type="text/css";
        try{
            a.appendChild(t.createTextNode(e))
        }
        catch(t){
            a.styleSheet.cssText=e
        }
        t.getElementsByTagName("head")[0].appendChild(a)
    }
    function s(){
        return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"
    }
    var d=[];
    e.requestAnimationFrame=function(){
        return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){
            setTimeout(e,1e3/60)
        }
    }(),
    n()
}
(window,document);
```
* 最后在$\color{DarkTurquoise}{/themes/icarus/layout/layout.ejs}$文件中的
```html
<!DOCTYPE html>
```
* 的下一行添加：
```html
<script src="/js/src/click.js"></script>
```
* 效果见本站

---

### 看板娘插件
* 在博客主目录下进入点击进入**Git Bash Here**
* 输入命令：
```bash
npm install hexo-helper-live2d --save
```
* 在网站配置文件或主题配置文件$\color{green}{\_config.yml}$中添加：
```yml
live2d:
  enable: true                                   #开启看板娘
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  log: false
  model:
    use: live2d-widget-model-z16     #指定模型任务
  display:
    position: right                              #显示位置
    width: 200                                   #模型宽度
    height: 400                                  #模型高度
  mobile:
    show: true                                  #是否在移动端显示
```
* 效果：见本站

---

### 遇到的坑及解决方法
* ..公式渲染问题
* ..
* ..
<div align=center>
$\color{green}{Waiting....for....update....}$
</div>

---
