---
title: 【教程】Hexo+Github博客搭建
date: 2018-12-26 10:20:24
tags: Blog
categories: 教程
toc: true
thumbnail: 'https://qcloud.coding.net/u/vincentqin/p/blogResource/git/raw/master/build-a-website-using-hexo/hexo-cover.png'
comments: true
---
## 开始
<!-- more -->
---
> 对于萌新来说，Hexo是一个非常容易上手的轻量级博客平台，只需简单的配置便可以打造令人满意的博客页面，下面是我自己搭建博课的流程，在此记录以备后续的需要。


---

## Step1:
**前期准备:**
- [ ] 安装Node.js : [Download](https://nodejs.org/zh-cn/)
- [ ] 安装git for win: [Download](https://git-scm.com/downloads)
- [ ] 注册GitHub账号: [Github.com](https://github.com/)

---

## Step2:
- [ ] 在GitHub中新建（New）一个库（Repositories），用来存放网站内容：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128105238488.png)
---
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128105923772.png)

---
## Step3:
**连接git与GitHub账户：**
* 在桌面点击鼠标右键，选择Git Bash Here 会跳出终端窗口输入命令并回车：
> ssh-keygen
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128111826521.png)
* 根据路径找到密钥文件并打开：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128112227406.png)
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128112429949.png)
* 打开你的GitHub账户点击右上角的头像选择setting --> SSH and GPG keys:
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128112644863.png)
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128113042424.png)
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128113504140.png)
> 至此，成功连接GIt与GitHub账户。



---
## Step4:
**安装Hexo：*
* 在桌面打开Git Bash Here终端输入命令：
> npm install -g hexo-cli

![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128114514842.png)

> 如果许久后未能安装，说明网络太慢，可更换安装源
> Ctrl+C，在终端输入：
> npm config set registry http://registry.cnpmjs.org

---
* 安装成功后，在电脑的任意磁盘内建立文件夹以存放Hexo网站：
* 这是我创建的路径：blog文件夹将被用于博客
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128115144081.png)
* 进入blog文件夹点击鼠标右键进入Git Bash Here终端，依次执行命令：
> hexo init  //初始化文件夹为博客根目录
> hexo install //安装必要依赖文件

* 安装hexo-deployer-git插件：
> npm install hexo-deployer-git --save

* 到此，还记得之前创建的GitHub库吗？ 打开该仓库复制仓库的SSH地址：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128120739091.png)
* 进入网站根目录/blog,用编辑器（vs code)打开 _config.yml 网站配置文件：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128121123562.png)

* 修改_config.yml 配置文件保存并退出：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128121726691.png)

* 回到Git终端，执行命令：
> hexo g -d //将网站部署到GitHub上

![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128122048305.png)

* 至此，可在浏览器内输入你的博客地址查看是否成功：
![](http://hexoblog-1257022783.cos.ap-chengdu.myqcloud.com/Hexo+Github博客搭建简明教程（Windows）/20190128122615866.png)
---

## Step5:
**如何写作：**
* 回到blog文件夹内，/source/_post/ 文件夹内的Markdown文件就是你的博文存放处
* 你可以新建md文档写作并用hexo g -d 命令将更新的博文部署到网站上
* 也可以利用HexoEdit编辑器写作并上传，详情可见我的另一篇博文[HesoEditor教程](https://ccyh.xyz/2019/01/27/HexoEditor/)
* 关于Markdown语法网上有许多教程可供学习[Markdown中文文档](https://markdown-zh.readthedocs.io/en/latest/)
---
> 关于Hexo主题更换配置我会在以后的文章中介绍，若有错误请指明，不甚感激。
> Thanks for your watching !!!!!!

