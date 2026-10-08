---
title: ParticleXF 更新：聊天记录、首页卡片与国际化
date: 2026-10-08
tags:
  - ParticleXF
  - hexo
  - update
categories:
  - Tutorial
description: 这次更新加入可折叠的模拟聊天记录、首页文章卡片样式自定义，并让主题界面与外挂标签的默认文案支持中英文切换。
---

从 `2c8e193` 之后到 `d235dfe`，ParticleXF 主题共完成了五次提交。最直观的变化是新加入的聊天记录标签；写文章时还可以单独调整首页卡片样式，主题界面的默认文案也开始跟随站点语言设置。

<!-- more -->

## 首页文章卡片可以单独定制

以前首页文章卡片统一使用主题样式。现在可以在单篇文章的 Front Matter 中设置卡片容器、标题、摘要和按钮的行内 CSS：

```yaml
---
title: 一篇示例文章
card_style: "border-color: #7eb89a;"
card_title_style: "color: #7eb89a;"
card_description_style: "font-size: 0.95rem;"
card_button_style: "background: #345f48; border-radius: 4px;"
---
```

这四个字段只作用于当前文章的首页卡片，不改变文章正文。标题还支持旧字段 `title_style`，摘要支持 `description_style`，按钮支持 `button_style` 和 `go_post_style`。主题会对这些字段做 HTML 属性转义，但行内 CSS 仍应由可信的文章作者维护。

## 主题文案支持中英文

在站点根目录的 `_config.yml` 中设置语言：

```yaml
language: zh-CN
```

目前提供 `zh-CN` 和 `en`。首页“阅读全文”、加载提示、归档搜索、文章加密输入框、目录控件、页脚备案文字，以及代码块的展开、收起和复制提示，都会使用对应语言文件。Note 的默认标题、Tabs 自动生成的标签名，以及 Chat 的默认标题、空记录提示和图片替代文字也一并接入了这套机制。

语言文件位于主题的 `languages/zh-CN.yml` 和 `languages/default.yml`。文章作者在标签中明确写出的标题、发言内容不会自动翻译。

## 用 Chat 标签写模拟聊天记录

新增的 `{% chat %}` 支持 `wechat`、`qq` 和 `telegram` 三种外观。每行消息使用 `角色|时间|内容`，时间可以省略。`me`、`self`、`我`、`right` 会显示在右侧，其余角色默认显示在左侧。

下面是一段实际渲染的示例：

{% chat wechat title="项目群" subtitle="发布讨论"%}
me:Florance,/images/avatar.jpg
A|10:24|这次更新的聊天标签可以显示图片吗？
me|10:25|可以，还能点击顶部折叠聊天记录。
me|10:26|[image:/images/background.jpg background]
{% endchat %}

发言人通过 `A:John,/images/avatar.jpg` 定义一次，后面的消息直接写 `A` 即可复用姓名和头像。头像及消息图片都支持本地路径，也支持完整的图片 URL。图片消息可写为 `[image:地址 说明]`，或使用 Markdown 图片语法。

顶部图标默认使用平台 Logo；添加 `logo="/images/ParticleXF.png"` 可以改用图片。聊天记录默认展开，设置 `expanded=false` 或添加 `collapsed` 即可默认收起，读者仍可点击顶部栏切换。聊天背景、文字和气泡会跟随主题的亮暗模式变化。

## 资源与代码整理

页面加载遮罩改在 `DOMContentLoaded` 后关闭，减少等待其他外部资源时的停留。`chat.js`、`note.js`、`tabs.js`、`video.js` 的代码格式和顶部说明也已统一，并补齐了中英文 README 中的配置示例。