---
title: Hexo用MathJax渲染数学公式
date: 2019-04-30 17:24:31
tags: Hexo
categories: 教程 
thumbnail: false
comments: true
toc: true
disqusId: ccyhweb
---

## 更改默认Markdown渲染引擎

<!-- more -->

Hexo的默认Markdown渲染引擎为hexo-renderer-marked，将其替换为hexo-renderer-kramed,对于这一步，网上的大部分教程是这么干的：
```bash
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-kramed --save
```
也就是先卸载掉默认引擎，再安装新引擎。但是我的npm出了问题，而且我个人觉得npm实在是不好用，因此我下载了yarn，并执行：
```bash
yarn remove hexo-renderer-marked
yarn add hexo-renderer-kramed
```
但当我执行hexo clean时却出现了类似下面的错误：
```bash
Error: hexo-renderer-marked is not installed , please install ....
```
所以一直无法成功。
后来我想干脆不卸载marked渲染引擎，直接安装kramed：
```bash
yarn add hexo-renderer-kramed
```
---

## 安装MathJax
卸载hexo-math：
```bash
yarn remove hexo-math
```
再安装hexo-renderer-mathjax：
```bash
yarn add hexo-renderer-mathjax -S
```
---

## 解决行内公式语义冲突

在博客的根目录下找到$\color{red}{node\_modules/kramed/lib/rules/inline.js}$
做如下两处更改：
```js
var inline = {
  //escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,   第一处
  escape: /^\\([`*\[\]()#$+\-.!_>])/,
  autolink: /^<([^ >]+(@|:\/)[^ >]+)>/,
  url: noop,
  html: /^<!--[\s\S]*?-->|^<(\w+(?!:\/|[^\w\s@]*@)\b)*?(?:"[^"]*"|'[^']*'|[^'">])*?>([\s\S]*?)?<\/\1>|^<(\w+(?!:\/|[^\w\s@]*@)\b)(?:"[^"]*"|'[^']*'|[^'">])*?>/,
  link: /^!?\[(inside)\]\(href\)/,
  reflink: /^!?\[(inside)\]\s*\[([^\]]*)\]/,
  nolink: /^!?\[((?:\[[^\]]*\]|[^\[\]])*)\]/,
  reffn: /^!?\[\^(inside)\]/,
  strong: /^__([\s\S]+?)__(?!_)|^\*\*([\s\S]+?)\*\*(?!\*)/,
  //em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,  第二处
  em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
  code: /^(`+)\s*([\s\S]*?[^`])\s*\1(?!`)/,
  br: /^ {2,}\n(?!\s*$)/,
  del: noop,
  text: /^[\s\S]+?(?=[\\<!\[_*`$]| {2,}\n|$)/,
  math: /^\$\$\s*([\s\S]*?[^\$])\s*\$\$(?!\$)/,
};
```
## 更改Mathjax加载脚本
找到$\color{red}{node-modules/hexo-renderer-mathjax/mathjax.html}$将最后一句改为：
```html
<script src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>
```

---

## 大功告成

```bash
hexo g -d
```
将改动部署到博客

---
