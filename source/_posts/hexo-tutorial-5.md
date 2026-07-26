---
title: HEXO-教程-5|定制化
date: 2026-07-25 13:22:09
tags:
    - hexo
categories:
    - Tutorial
pinned: 1
---

{% note info  %}
教你从零开始搭建个人博客
----以HEXO的Particlexf主题为例
`Part V`
{% endnote  %}

本文将要介绍如何简单定制 ParticleXF 主题，主要讲 `EJS`、如何添加自己的 `JS` 和 `CSS`、如何修改模板。

<!-- more -->

# 先认识主题结构

ParticleXF 的主要文件结构大致如下：

- `layout/`：页面模板，主要是 EJS 文件
- `source/js/`：前端脚本，生成后会输出到站点的 `/js/`
- `source/css/`：样式文件，生成后会输出到站点的 `/css/`
- `scripts/`：Hexo 运行时脚本

如果只是做小范围定制，通常不需要重写整个主题，只要改模板、加一份自己的 JS 或 CSS 就够了。

# EJS 是什么

ParticleXF 的模板大多是 EJS 文件，比如 `themes/particlexf/layout/layout.ejs`、`menu.ejs`、`post.ejs` 这些。

EJS 可以理解成“带有 JavaScript 逻辑的 HTML 模板”。常见写法有三种：

```ejs
<%= title %>
<%- partial("menu") %>
<% if (theme.preview.enable) { %>
    <script src="<%- url_for("/js/lib/preview.js") %>"></script>
<% } %>
```

它们分别表示：

- `<%= ... %>`：输出变量内容，会自动转义
- `<%- ... %>`：输出原始内容，不做转义
- `<% ... %>`：只执行逻辑，不直接输出

{% note tip %}
如果你只是想把变量显示到页面上，优先用 `<%= ... %>`。只有在你明确知道内容安全、并且确实需要输出 HTML 时，才考虑 `<%- ... %>`。
{% endnote %}

# 添加自己的 JS

最简单的方式是把自己的脚本放到主题的 `source/js/` 目录下。

比如你新建一个 `themes/particlexf/source/js/custom.js`，Hexo 生成后它会出现在站点的 `/js/custom.js`。

## 写自己的脚本

例如你可以先写一个最简单的测试脚本：

```javascript
window.addEventListener("DOMContentLoaded", () => {
    console.log("Custom script loaded");
});
```

## 在模板里引入

如果你希望它在所有页面都生效，可以在 `themes/particlexf/layout/layout.ejs` 里加一行：

```ejs
<script src="<%- url_for("/js/custom.js") %>"></script>
```

通常可以放在现有的 `main.js` 和 `theme.js` 后面。

## 只在特定页面加载

你也可以在 EJS 中写条件判断，只让脚本在某些页面加载：

```ejs
<% if (is_post()) { %>
<script src="<%- url_for("/js/custom-post.js") %>"></script>
<% } %>
```

这样就不会在首页、分类页也加载同一个脚本。

# 添加自己的 CSS

ParticleXF 的主样式文件在 `themes/particlexf/source/css/main.css`。

如果你只是想改几个颜色、间距、字体，直接往这里加样式就可以。

## 直接写样式

例如你想让文章标题更明显，可以加一段类似这样的规则：

```css
.article h1,
.article h2,
.article h3 {
    letter-spacing: 0.02em;
}
```

## 新建独立样式文件

如果你不想把所有自定义内容都塞进 `main.css`，也可以新建一个 `custom.css`。

然后在 `layout.ejs` 或 `import.ejs` 里引用它：

```ejs
<link rel="stylesheet" href="<%- url_for("/css/custom.css") %>" />
```

这种方式更适合长期维护，因为你自己的样式和主题原样式分开了。

## 常见做法

通常建议这样处理：

- 小改动：直接写进 `main.css`
- 大改动：单独建 `custom.css`
- 调试时：先在浏览器开发者工具里确认选择器是否生效

# 修改模板

如果你要改页面结构，比如加按钮、换布局、插入自定义模块，就需要改 EJS 模板。

ParticleXF 的模板都在 `themes/particlexf/layout/` 下。

## 找到对应模板

常见的模板文件有：

- `layout.ejs`：整体页面骨架
- `menu.ejs`：顶部菜单
- `post.ejs`：文章页
- `footer.ejs`：底部区域
- `index.ejs`：首页

比如你想在每个页面底部加一段提示，可以先看 `footer.ejs`。

## 使用 partial 拆分模板

ParticleXF 已经把很多区域拆成了 partial，比如：

```ejs
<%- partial("menu") %>
<%- partial("footer") %>
```

如果你要加自己的模块，也可以新建一个模板片段，再用 partial 引入，这样会更清晰。

## 一个简单示例

假设你想在文章页标题下方显示一段自定义提示，可以在对应模板里写：

```ejs
<% if (is_post()) { %>
    <div class="post-tip">这是一段自定义提示</div>
<% } %>
```

然后在 CSS 里补样式：

```css
.post-tip {
    margin: 20px 0;
    padding: 12px 16px;
    border-left: 4px solid var(--accent);
    background: var(--bg-surface-elevated);
}
```

# 推荐的修改顺序

如果你刚开始改主题，我建议按这个顺序来：

1. 先用 EJS 找到你要改的页面结构
2. 再加 JS 处理交互
3. 最后补 CSS 调整外观

这样最不容易改乱，也方便你回头定位问题。

{% note warning %}
如果你直接改主题源码，更新主题时可能会被覆盖。比较稳妥的做法是先备份自己的修改，或者把常用自定义内容单独抽出来管理。
{% endnote %}

上一篇教程：[HEXO-教程-4|部署](/2026/07/25/hexo-tutorial-4/)