---
title: HEXO-教程-3|文章小技巧
date: 2026-07-23 22:32:55
tags:
    - hexo
categories:
    - Tutorial
---

{% note info  %}
教你从零开始搭建个人博客
----以HEXO的Particlexf主题为例
`Part III`
{% endnote  %}

本文将要介绍 HEXO 博客的一些文章小技巧，以及 ParticleXF 主题的一些特色功能。

<!-- more -->

# 创建文章

在博客目录下，使用以下命令创建文章：

```bash
$ hexo new "My New Post"
```

当然，你也可以手动创建一个 Markdown 文件，并将其放在 `source/_posts/` 目录下。

{% note info 提示 %}
命令接受的是一个字符串参数，作为文章的标题。你可以使用中文、英文或其他语言的字符。
引号是不必须的，但是当标题中包含空格或特殊字符时，建议加上引号以防止解析错误。
标题如果包含了空格或特殊字符，Hexo 会将其转换为 `-`，作为文章的文件名。
{% endnote %}

此时，`source/_posts/` 目录下会生成一个名为 `my-new-post.md` 的文件。

该文件的 front-matter 中默认包含了文章的标题、创建日期，和一个空的 tags 字段，你可以根据需要进行修改。

```yaml
---
title: My New Post
date: 2026-07-23 22:32:55
tags:
---
```

# Markdown

由于 Markdown 是非常基础的知识，这里不再赘述。你可以上网搜索相关的 Markdown 教程。

{% note tip Tip %}
HEXO 的 Markdown 是支持内嵌 HTML 语法的，这意味着你可以在 Markdown 中直接使用 HTML 标签。
{% endnote  %}

# Tag 与 Category

在文章的 front-matter 中添加 `tags` 和 `categories` 字段，用于设置文章的标签和分类。

其中 `tags` 和 `categories` 字段都可以设置多个值，格式如下：

```yaml
---
tags:
    - hexo
    - tutorial
categories:
    - Tutorial
---
```

# 文章描述/缩略

其实 ParticleXF 主题是没有自动缩略的，也就是说，如果你没有加额外的限制，那么首页的文章列表将会显示整篇文章的内容。

添加描述/缩略有两种方式：

## description 字段

在文章的 front-matter 中添加 `description` 字段，用于设置文章的描述。内容支持 Markdown 格式的内容。

```yaml
---
description: 这是一篇关于 HEXO 博客的一些文章小技巧，以及 ParticleXF 主题的一些特色功能的教程。
---
```

{% note warning 注意 %}
description字段内如果要使用Markdown，有以下注意事项：
1. 不要使用 `---`，否则会被 Hexo 解析为 front-matter 的结束标记
2. 最好不要写多行内容
3. 如果开头是代码块，要在`description:` 后面写 `|`，否则会报错

```yaml
---
description: |
    这是一篇关于 `HEXO` 博客的一些文章小技巧，以及 ParticleXF 主题的一些特色功能的教程。
---
```
{% endnote %}

## more 标签

`<!-- more -->` 可以让文章在首页只显示 `<!-- more -->` 之前的内容，`<!-- more -->` 之后的内容将会在文章详情页显示。

# 评论与TOC

在 ParticleXF 主题中，文章页最右侧有一个目录区域，这就是 `TOC(Table of Contents)`。

{% note tip Tip %}
TOC 底部的 `评论` 按钮在评论未启用时会变成 `底部` 按钮
{% endnote %}

文章的评论和 TOC 是可以单独设置的。

在 `front-matter` 中添加 `toc` 和 `comments` 字段，用于设置文章是否显示目录和评论。

{% note tip Tip %}
`comments` 字段在 about 页面也是可用的。
{% endnote %}

```yaml
---
toc: false
comments: false
---
```

# Note 提示框

Note 提示框是 ParticleXF 主题提供的一个特色功能，可以在文章中添加一些提示信息。

### 写法

```markdown
{% note tip %}
正文，支持 **Markdown**。
{% endnote %}

{% note warning 自定义标题 %}
……
{% endnote %}

{% note danger no-icon %}
不显示图标。
{% endnote %}
```

### 类型一览

{% note note %}
默认 / `note`：一般说明。
{% endnote %}

{% note info %}
`info`：补充信息。
{% endnote %}

{% note tip %}
`tip`：技巧与建议。
{% endnote %}

{% note success %}
`success`：完成、正确路径。
{% endnote %}

{% note warning %}
`warning`：需要注意的点。
{% endnote %}

{% note danger %}
`danger`：风险、错误、破坏性操作。
{% endnote %}

{% note quote %}
`quote`：引用式强调。
{% endnote %}

{% note tip no-icon %}
`no-icon`：不显示左侧图标（任意类型都可加）。
{% endnote %}


上一篇教程：[HEXO-教程-2|主题与页面](/2026/07/23/hexo-tutorial-2/)
下一篇教程：[HEXO-教程-4|部署](/2026/07/25/hexo-tutorial-4/)