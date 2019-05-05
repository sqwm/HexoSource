---
title: Hexo-icarus修改文章详情页
date: 2019-05-01 18:46:04
tags: Hexo
categories: 教程 
thumbnail: 'https://camo.githubusercontent.com/10c034a879aaaa88ea3669f0992cd28743d8ca07/687474703a2f2f70706f66666963652e6769746875622e696f2f6865786f2d7468656d652d6963617275732f67616c6c6572792f707265766965772e706e673f31'
comments: true
toc: true
disqusId: ccyhweb
---



## 为什么修改？
<!-- more -->
由于Hexo-icarus主题的文章详情页默认与主页布局一致，皆为三栏布局。但是三栏布局限制了文章内容的展示，因此试图将其改为两栏布局。

---

## 通过修改源代码来达成目标
打开/themes/icarus/layout/layout.ejs文件，添加col()函数到文件中：
```js
<% function col(){
    if(!is_post()){
        return main_column_class();
        }
    else{
        return 'is-6-tablet is-6-desktop is-9-widescreen';
        } 
    } %>
```
再section标签中做如下改动：
```html
<section class="section">
        <div class="container">
            <div class="columns">
                <!-- 将main_column_class() 改为 col() -->
                <div class="column <%= col() %> has-order-2 column-main"><%- body %></div>
                <%- partial('common/widget', { position: 'left' }) %>
                <%- partial('common/widget', { position: 'right' }) %>
            </div>
        </div>
    </section>
```
不难看出，上述改动的目的是将显示逻辑改为：若当前页面不是文章页面则直接采用原始设置，否则将文章栏放大。
通过上面的修改，hexo server查看效果，发现文章详情页的文章栏确实放大了，但是右侧的部件栏并未消失，而是被挤出了屏幕外一部分，极不美观。

为了解决上述问题，还需修改/themes/icarus/layout/common/widget.ejs文件。
将代码全选复制，再粘贴于末尾，做如下修改3处代码：
```js
<% if (get_widgets(position).length && !is_post()) { %>        <!-- 修改 -->
<% function side_column_class() {
    switch (column_count()) {
        case 2:
            return 'is-4-tablet is-4-desktop is-4-widescreen';
        case 3:
            return 'is-4-tablet is-4-desktop is-3-widescreen';
    }
    return '';
} %>
<% function visibility_class() {
    if (column_count() === 3 && position === 'right') {
        return 'is-hidden-touch is-hidden-desktop-only';
    }
    return '';
} %>
<% function order_class() {
    return position === 'left' ? 'has-order-1' : 'has-order-3';
} %>
<% function sticky_class(position) {
    return get_config('sidebar.' + position + '.sticky', false) ? 'is-sticky' : '';
} %>
<div class="column <%= side_column_class() %> <%= visibility_class() %> <%= order_class() %> column-<%= position %> <%= sticky_class(position) %>">
    <% get_widgets(position).forEach(widget => {%>
        <%- partial('widget/' + widget.type, { widget, post: page }) %>
    <% }) %>
    <% if (position === 'left') { %>
        <div class="column-right-shadow is-hidden-widescreen <%= sticky_class('right') %>">
        <% get_widgets('right').forEach(widget => {%>
            <%- partial('widget/' + widget.type, { widget, post: page }) %>
        <% }) %>
        </div>
    <% } %>
</div>
<% } %>

<!-- 粘贴的部分 -->
<% if (position === 'left' && is_post()) { %>                          <!-- 修改，可选保留的栏 -->
<% function side_column_class() {
    switch (column_count()) {
        case 2:
            return 'is-4-tablet is-4-desktop is-4-widescreen';
        case 3:
            return 'is-4-tablet is-4-desktop is-3-widescreen';
    }
    return '';
} %>
<% function visibility_class() {
    if (column_count() === 3 && position === 'right') {
        return 'is-hidden-touch is-hidden-desktop-only';
    }
    return '';
} %>
<% function order_class() {
    return position === 'left' ? 'has-order-3' : 'has-order-1';       <!-- 修改 -->
} %>
<% function sticky_class(position) {
    return get_config('sidebar.' + position + '.sticky', false) ? 'is-sticky' : '';
} %>
<div class="column <%= side_column_class() %> <%= visibility_class() %> <%= order_class() %> column-<%= position %> <%= sticky_class(position) %>">
    <% get_widgets(position).forEach(widget => {%>
        <%- partial('widget/' + widget.type, { widget, post: page }) %>
    <% }) %>
    <% if (position === 'left') { %>
        <div class="column-right-shadow is-hidden-widescreen <%= sticky_class('right') %>">
        <% get_widgets('right').forEach(widget => {%>
            <%- partial('widget/' + widget.type, { widget, post: page }) %>
        <% }) %>
        </div>
    <% } %>
</div>
<% } %>
```
---


## 大功告成
我这里保存的是左边栏，若要保存右边栏可以在 widget.ejs 文件中更改（已标识）。

## 效果
见本站！
