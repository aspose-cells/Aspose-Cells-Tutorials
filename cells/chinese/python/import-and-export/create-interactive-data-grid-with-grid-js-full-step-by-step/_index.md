---
category: general
date: 2026-06-21
description: 使用 Grid.js 创建交互式数据网格，并学习如何显示带有排序、分页和搜索功能的 JSON 数据表。非常适合网页仪表盘。
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: zh
og_description: 在几分钟内创建交互式数据网格。了解如何使用 Grid.js 显示带分页、排序和搜索功能的 JSON 数据表。
og_title: 使用 Grid.js 创建交互式数据网格 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: 使用 Grid.js 创建交互式数据网格 – 完整分步指南
url: /zh/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Grid.js 创建交互式数据网格 – 完整分步指南

是否曾想过 **创建交互式数据网格**，让用户无需编写后端即可对行进行排序、搜索和分页？你并不孤单。在许多仪表盘中，最大的痛点是把静态的 JSON 转换成一个流畅、可搜索的表格——它的体验像电子表格，却完全在浏览器中运行。

在本教程中，我们将一步步演示 **如何使用 Grid.js** 在普通 HTML 页面上 **显示 JSON 数据表格**。完成后，你将拥有一个可直接放入任何项目的完整示例，并提供自定义工具栏、处理大数据集以及避免常见陷阱的技巧。

## 你将学到的内容

- 如何获取定义列和行的 JSON 文件。
- 如何使用 **Grid.js** 初始化分页、排序、搜索和自定义工具栏。
- 如何将网格渲染到目标容器中。
- 可选的微调：自定义单元格格式、主题切换和错误处理。
- 一个完整的、可直接复制粘贴的代码示例。

### 前置条件

在开始之前，请确保你具备以下条件：

1. 现代浏览器（Chrome、Edge 或 Firefox）——Grid.js 依赖 ES6 特性。  
2. 包含 `grid_data.json` 文件的本地或远程文件夹（我们会展示其格式）。  
3. 基本的 HTML 与 JavaScript 认识——不需要花哨的东西，只要能在浏览器中打开 `.html` 文件即可。

无需构建工具、npm 安装或服务器端代码。这就是 **使用 Grid.js 创建交互式数据网格** 的魅力所在：直接通过 CDN 即可运行。

---

## 第一步：准备定义表格的 JSON

首先，你需要一个 JSON 负载，告诉 Grid.js 存在哪些列以及要显示哪些行。它相当于 **显示 JSON 数据表格** 的蓝图。下面是一个最小示例，可保存为与 HTML 文件同目录下的 `grid_data.json`：

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*为什么采用这种格式？* Grid.js 期望 `columns` 为字符串数组（或用于高级配置的对象），`rows` 为数组的数组，其中每个内部数组的顺序对应列顺序。你当然可以添加更多列或嵌套对象——只要结构对应，Grid.js 都会渲染。

> **专业提示：** 如果你是从 API 获取数据，只需将静态的 `fetch('grid_data.json')` 替换为你的接口 URL，其他代码保持不变。

---

## 第二步：初始化 Grid.js – **how to use gridjs** 的核心

数据源准备好后，我们需要把 Grid.js 引入页面并告诉它如何工作。这一步实现了 **创建交互式数据网格** 的分页、排序和工具栏按钮等功能。

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN 提供最新的稳定版，Meri­maid 主题则开箱即用地提供简洁现代的外观。如果你更喜欢默认样式，可以改为 `gridjs.min.css`。

接下来，在 `<script>` 标签内获取 JSON 并初始化网格：

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### 选项拆解

| 选项 | 功能说明 | 重要性 |
|------|----------|--------|
| `pagination` | 将行拆分为分页（默认每页 10 条） | 在大型表格中保持可用性，避免 UI 被淹没。 |
| `sort` | 可点击的列标题切换升序/降序 | 用户能够快速定位最高值的行。 |
| `search` | 添加即时过滤的文本输入框 | 进行临时查询，无需重新加载数据。 |
| `toolbar` | 在网格上方添加自定义按钮或下拉菜单 | 适用于 “帮助”、 “导出” 或 “刷新” 等操作。 |
| `formatter` | 允许为单元格返回原始 HTML | 示例中将电子邮件字符串转换为可点击的 mailto 链接。 |

> **为何采用此方式？** 通过声明式的网格配置，你可以在不触及核心渲染逻辑的情况下轻松调整行为。这是大多数项目 **how to use Grid.js** 的推荐做法。

---

## 第三步：将网格渲染到页面中

脚本的最后一行 `grid.render(document.getElementById('grid-container'))` 会把完整的表格注入到 HTML body 中你放置的 `<div>`：

```html
<div id="grid-container"></div>
```

就这么简单。页面加载时，浏览器会获取 JSON，构建 Grid.js 实例，并将交互式表格绘制到屏幕上。首次加载后不再需要刷新或额外的服务器请求。

---

## 可选：样式与主题微调

如果默认的 Meri­maid 主题不是你的菜，可以换成任意内置主题（`gridjs.min.css`）或自行编写 CSS。例如，将表头背景设为柔和的灰色：

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

将代码片段放入 `<style>` 标签或外部样式表中即可。Grid.js 支持标准 CSS 选择器，因而你可以完全控制字体、颜色和间距。

---

## 常见陷阱及规避方法

| 陷阱 | 表现 | 解决方案 |
|------|------|----------|
| **跨域错误**（CORS）在从其他域获取 JSON 时出现 | 浏览器控制台显示 “Blocked by CORS policy” | 将 JSON 部署在同源，或在服务器上启用 CORS。 |
| **大数据集导致卡顿** | 滚动不流畅，分页响应慢 | 使用 `server` 分页（`pagination: { server: { url: (prev, page, limit) => … } }`）或懒加载行。 |
| **工具栏按钮未出现** | 即使 `toolbar.enabled: true` 仍看不到按钮 | 确认使用的是 Grid.js 2.0+ 版本；旧版本的工具栏 API 不同。 |
| **邮件链接不可点击** | Formatter 返回纯文本 | 返回 `gridjs.html(...)` 而非普通字符串，示例已演示。 |

提前处理这些问题，可为你节省大量调试时间。

---

## 完整可运行示例（复制粘贴即用）

下面是完整的 HTML 文件，可保存为 `index.html`。在浏览器中打开，即可看到一个完整的 **创建交互式数据网格** 演示，展示 **显示 JSON 数据表格** 的排序、搜索以及帮助按钮功能。



## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [如何使用 Aspose.Cells for Java 创建 Excel 数据验证列表：分步指南](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中创建复选框 | 数据验证教程](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [使用 Aspose.Cells for Java 创建并导入 XML 数据到 Excel](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}