---
title: HEXO-教程-2|主题与页面
date: 2026-07-23 21:29:49
tags:
    - hexo
categories:
    - Tutorial
---

{% note info  %}
教你从零开始搭建个人博客
----以HEXO的Particlexf主题为例
`Part II`
{% endnote  %}

本文将要介绍如何安装主题、进行一些基本的配置和创建页面。

<!-- more -->

# 安装 ParticleXF 主题

你可以到[Hexo主题网站](https://hexo.io/themes/)浏览和选择你喜欢的主题。以 ParticleXF 主题为例，你可以通过以下命令来安装它：

## 方式一：克隆到主题目录


```bash
cd your-hexo-site
git clone https://github.com/FloranceYeh/hexo-theme-particlexf themes/particlexf
```

{% note warning 注意 %}
这个办法在某些部署环境下可能会引发子模块问题，解决方法有两种：
1. 将 `themes/particlexf` 目录下的隐藏的 `.git` 文件夹删除。
2. 使用方式二安装主题。
{% endnote  %}

## 方式二：作为子模块（推荐）

```bash
cd your-hexo-site
git submodule add https://github.com/FloranceYeh/hexo-theme-particlexf themes/particlexf
```

## 方式三：下载压缩包

到项目的Github仓库 [hexo-theme-particlexf](https://github.com/FloranceYeh/hexo-theme-particlexf) 下载源代码，这里直接贴出文件地址：[ParticleXF-main.zip](https://github.com/FloranceYeh/hexo-theme-particlexf/archive/refs/heads/main.zip)

下载完成后，将压缩包解压并解压到主题目录 `themes/particlexf`。

安装完成后，在站点根目录的 `_config.yml` 中启用主题：

```yaml
theme: particlexf
```

{% note info %}
这里的 `theme` 字段实际上是主题目录的名称，而不是主题的名称。
所以当你发现主题没启用时，请检查主题目录名和 `_config.yml` 文件中的配置是否一致。
{% endnote  %}

# 主题配置

安装好主题后记得查看主题提供的 `README.md` 文件，里面有详细的配置说明，也有一些注意事项。

{% note tip 复制一份主题配置 %}
将主题的 `_config.yml` 文件复制到站点根目录下，并改名为 `_config.<themename>.yml`
\<themename\> 是你的主题目录名称
{% endnote  %}

## ParticleXF 主题配置

### 关闭 Hexo 自带的代码高亮和归档页

对于 ParticleXF 主题，要注意的是 Hexo 自带的代码高亮和归档页功能可能会和主题自带的功能冲突，所以建议关闭它们。

把 `_config.yml` 中的 `syntax_highlighter` 配置改为空值即可。

```yaml
syntax_highlighter:
```

### 配置`_config.particlexf.yml`

在`_config.particlexf.yml`里，大部分字段都给了注释，建议你根据自己的需求进行配置。

# 创建页面

在 Hexo 中，内置了一些特殊的页面类型，比如 `about`、`archives`、`tags`、`categories` 等。

## `Archives` 页面

Archives 页面是 Hexo 自带的归档页，它会自动生成，可在 `_config.yml` 中配置是否启用。

```yaml
archive_generator:
  enabled: true
```

## 创建 `about` 页面

```bash
hexo new page about
```

## 创建 `categories` 页面

```bash
hexo new page categories
```

然后在 `source/categories/index.md` 中被 `---` 包裹的头部，（称作`front-matter`）添加以下内容：

```yaml
---
···
type: categories
···
---
```

## 创建 `tags` 页面

```bash
hexo new page tags
```

然后也要在 `source/tags/index.md` 的 `front-matter` 中添加以下内容：

```yaml
---
···
type: tags
···
---
```

## 创建 `links` 页面（ParticleXF 的实现）

### 创建页面

```bash
hexo new page links
```

不用修改 `source/links/index.md` 的 `front-matter`。

`source/links/index.md` 中如果写了内容，将在页面最底部渲染。

### 添加数据

创建 `source/_data/links.yml` 文件，并在其中添加链接数据，格式如下：

```yaml
字段1:
    字段1.1:
        name: Friend
        url: https://friend.com
        ava: https://friend.com/images/avatar.jpg
        des: A friend website.
    字段1.2:
        name: Another Friend
        url: https://anotherfriend.com
        ava: https://anotherfriend.com/images/avatar.jpg
        des: Another friend website.
字段2:
    字段2.1:
        name: Yet Another Friend
        url: https://yetanotherfriend.com
        ava: https://yetanotherfriend.com/images/avatar.jpg
        des: Yet another friend website.
```

{% note info %}
links.yml中的字段是可嵌套的，`字段1`、`字段1.1` 都可以自定义，且这些是不显示在页面上的。
只有`name`、`url`、`ava`、`des`是固定的。
{% endnote  %}

# 主页配置

在 `_config.yml` 中，你可以配置主页每页显示的文章数量和排序方式：

```yaml
index_generator:
  path: ''
  per_page: 10
  order_by: -date
```

## ParticleXF 主题的主页配置

在 ParticleXF 主题中，你还可以通过修改 `_config.particlexf.yml` 文件来进一步配置主页的显示效果。

ParticleXF 使用的图标库是 [Font Awesome](https://fontawesome.com/)。

图标使用一般包含两个字段：`name` 和 `theme`，使用前记得查看 [Font Awesome 图标库](https://fontawesome.com/icons) 以获取图标名称和主题。

### 顶栏

顶栏菜单的配置在 `_config.particlexf.yml` 中的 `menu` 字段中，你可以添加、删除或修改菜单项。

其中二级字段名（如 `Home`、`About` 等）是菜单的显示名称，`name` 是图标名称，`theme` 是图标主题，`link` 是菜单链接。


```yaml
menu:
    Home:
        name: house
        theme: solid
        link: /
    About:
        name: id-card
        theme: solid
        link: /about
    Archives:
        name: box-archive
        theme: solid
        link: /archives
    Categories:
        name: bookmark
        theme: solid
        link: /categories
    Tags:
        name: tags
        theme: solid
        link: /tags
    Links:
        name: link
        theme: solid
        link: /links
```

### 卡片

卡片的配置在 `_config.particlexf.yml` 中的 `card` 字段中，你可以根据需要进行配置。

```yaml
card:
    enable: true
    description: |
        DEMO for ParticleXF
        Tutorial for Hexo
    iconLinks:
        Github:
            name: github
            theme: brands
            link: https://github.com/FloranceYeh/hexo-theme-particlexf
        Email:
            name: envelope
            theme: solid
            link: mailto:Florance_Sunrise@outlook.com
    friendLinks:
        Home: /
        About: /about
```

上一篇教程：[HEXO-教程-1|安装与使用](/2026/07/23/hexo-tutorial-1/)
下一篇教程：[HEXO-教程-3|文章小技巧](/2026/07/23/hexo-tutorial-3/)