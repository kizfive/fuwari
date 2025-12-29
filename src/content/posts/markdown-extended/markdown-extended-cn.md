---
title: Markdown 拓展功能111
published: 2024-05-01T00:00:00.000Z
updated: 2025-12-18
description: 在Fuwari中阅读有关Markdown功能的更多信息
image: ""
tags:
  - Markdown
  - 博客
  - 示例
  - 演示
category: 示例
draft: false
lang: zh_CN
en: markdown-extended/markdown-extended/
---

:::note
This is a translated version.
:::

## GitHub 仓库卡片

你可以添加链接创建 GitHub 仓库的动态卡片，页面加载时，仓库信息会通过 GitHub API 拉取。  

::github{repo="Fabrizz/MMM-OnSpotify"}

使用代码 `::github{repo="<owner>/<repo>"}` 创建 GitHub 仓库卡片。

```markdown
::github{repo="saicaca/fuwari"}
```

## GitHub 用户卡片

与仓库卡片相似，你可以通过添加链接创建 GitHub 用户卡片。  

::github{user="torvalds"}

使用代码 `::github{user="username"}` 创建 GitHub 用户卡片。 

```markdown
::github{user="torvalds"}
```

## 警示框（Admonitions）

支持以下类型的警示框：`note`（注意）、`tip`（提示）、`important`（重要）、`warning`（警告）、`caution`（谨慎）  

:::note  
强调用户即使略读也应考虑的信息。  
:::  

:::tip  
帮助用户更成功的可选信息。  
:::  

:::important  
用户成功所需的**关键**信息。  
:::  

:::warning  
因潜在风险需要用户**立即关注**的关键内容。  
:::  

:::caution  
某行为可能导致的**负面潜在后果**。  
:::  


### 基础语法

```markdown
:::note
强调用户即使略读也应考虑的信息。
:::

:::tip
帮助用户更成功的可选信息。
:::
```

### 自定义标题

警示框的标题可以自定义。  

:::note[MY CUSTOM TITLE]  
这是一个带自定义标题的注意框。  
:::

```markdown
:::note[MY CUSTOM TITLE]
这是一个带自定义标题的注意框。
:::
```

### GitHub 语法

> [!TIP]
> [GitHub 语法](https://github.com/orgs/community/discussions/16925) 也受支持。

```
> [!NOTE]
> GitHub 语法也受支持。

> [!TIP]
> GitHub 语法也受支持。
```

### 剧透内容

你可以给文本添加剧透（内容会被隐藏），且文本支持 **Markdown** 语法。

示例内容：剧透里藏着**加粗文字**哦！:spoiler[是隐藏的 **ayyy**]!

```markdown
示例内容：剧透里藏着加粗文字哦！:spoiler[是隐藏的 ayyy]!

```