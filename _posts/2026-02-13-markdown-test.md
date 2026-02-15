---
layout: post
title: "markdown test"
date: 2026-02-13 00:00 +0000
toc: true
---
# Markdown 格式测试文档

这是一个全面的 Markdown 测试文档，包含了所有常用的格式。

## 一级标题
### 二级标题
#### 三级标题
##### 四级标题
###### 五级标题

---

## 文本格式

这是普通文本。

**这是粗体文本**

*这是斜体文本*

***这是粗斜体文本***

~~这是删除线文本~~

`这是行内代码`

==这是高亮文本==（部分编辑器支持）

## 引用

> 这是一级引用
> 
> > 这是二级嵌套引用
> > 
> > > 这是三级嵌套引用

> 引用可以包含**格式化文本**和`代码`

## 列表

### 无序列表

* 项目 1
* 项目 2
  * 子项目 2.1
  * 子项目 2.2
    * 子子项目 2.2.1
* 项目 3

- 使用减号
- 也可以创建列表

+ 使用加号
+ 同样有效

### 有序列表

1. 第一项
2. 第二项
   1. 子项目 2.1
   2. 子项目 2.2
3. 第三项

### 任务列表

- [x] 已完成任务
- [x] 另一个已完成任务
- [ ] 未完成任务
- [ ] 另一个未完成任务

## 链接

[这是一个链接](https://www.example.com)

[带标题的链接](https://www.example.com "链接标题")

<https://www.example.com>

[引用式链接][ref-link]

[ref-link]: https://www.example.com "引用链接"

## 图片

![替代文本](https://kadefu.com/i/2026/02/15/w1x4qp.png)

![带标题的图片](https://kadefu.com/i/2026/02/15/w2nqep.png "撑阳伞的女人")

## 代码块

### 行内代码

使用 `console.log()` 来输出内容。

### 代码块

```
无语言标记的代码块
可以包含多行
```

```python
# Python 代码
def hello_world():
    print("Hello, World!")
    return True
```

```javascript
// JavaScript 代码
function helloWorld() {
    console.log("Hello, World!");
    return true;
}
```

```html
<!-- HTML 代码 -->
<!DOCTYPE html>
<html>
<head>
    <title>测试页面</title>
</head>
<body>
    <h1>Hello, World!</h1>
</body>
</html>
```

```css
/* CSS 代码 */
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 20px;
}
```

## 表格

### 基本表格

| 表头 1 | 表头 2 | 表头 3 |
|--------|--------|--------|
| 单元格 1 | 单元格 2 | 单元格 3 |
| 单元格 4 | 单元格 5 | 单元格 6 |

### 对齐表格

| 左对齐 | 居中对齐 | 右对齐 |
|:-------|:--------:|-------:|
| 内容   | 内容     | 内容   |
| 长内容 | 长内容   | 长内容 |

### 复杂表格

| 功能 | 支持 | 说明 |
|------|:----:|------|
| **粗体** | ✓ | 使用 `**text**` |
| *斜体* | ✓ | 使用 `*text*` |
| `代码` | ✓ | 使用反引号 |
| [链接](https://example.com) | ✓ | 使用 `[text](url)` |

## 分隔线

---

***

___

- - -

## 转义字符

使用反斜杠转义特殊字符：

\*不是斜体\*

\`不是代码\`

\[不是链接\]

\# 不是标题

## 脚注

这是一个带脚注的文本[^1]。

这是另一个脚注[^2]。

[^1]: 这是第一个脚注的内容。
[^2]: 这是第二个脚注的内容，可以包含**格式化文本**。

## 定义列表

术语 1
: 定义 1a
: 定义 1b

术语 2
: 定义 2

## 缩写

HTML 的全称是 Hypertext Markup Language。

*[HTML]: Hypertext Markup Language

## 数学公式（如果支持 LaTeX）

行内公式：$E = mc^2$

块级公式：

$$
\frac{n!}{k!(n-k)!} = \binom{n}{k}
$$

$$
\int_{a}^{b} f(x)dx
$$

## Emoji 表情（部分编辑器支持）

:smile: :heart: :thumbsup: :rocket: :tada:

😀 😃 😄 😁 🎉 ❤️ 👍

## HTML 标签（部分编辑器支持）

<div style="color: red;">这是红色文字</div>

<details>
<summary>点击展开</summary>
这是隐藏的内容。
</details>

<kbd>Ctrl</kbd> + <kbd>C</kbd>

<mark>高亮文本</mark>

<sub>下标</sub> 和 <sup>上标</sup>

## 特殊块

### 提示块（部分编辑器支持）

> [!NOTE]
> 这是一个提示信息。

> [!TIP]
> 这是一个技巧提示。

> [!IMPORTANT]
> 这是重要信息。

> [!WARNING]
> 这是警告信息。

> [!CAUTION]
> 这是需要注意的信息。

## 混合格式测试

1. **粗体列表项**包含`行内代码`
2. *斜体列表项*包含[链接](https://example.com)
3. 包含引用的列表项：
   > 这是引用内容

表格中的格式：

| 类型 | 示例 | 代码 |
|------|------|------|
| 粗体 | **Bold** | `**Bold**` |
| 斜体 | *Italic* | `*Italic*` |
| 删除线 | ~~Strike~~ | `~~Strike~~` |

---
