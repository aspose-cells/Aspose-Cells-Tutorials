---
category: general
date: 2026-06-30
description: 如何轻松创建 gridjs，提供完整的 JavaScript 示例，涵盖 gridjs 配置、容器设置和渲染过程。
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: zh
og_description: 如何轻松创建 gridjs，提供完整的 JavaScript 示例，涵盖 gridjs 配置、容器设置和渲染过程。
og_title: 如何创建 Gridjs – 完整的 JavaScript 网格指南
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: 如何创建 Gridjs —— 完整的 JavaScript 网格指南
url: /zh/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何创建 Gridjs – 完整的 JavaScript 网格指南

有没有想过 **如何创建 gridjs** 并立即在页面上看到一个炫酷的数据表格？你并不是唯一的。许多开发者在首次尝试接入 Gridjs 时会卡在配置对象和渲染调用上。好消息是？只要掌握正确的步骤，这其实非常简单。

在本教程中，我们将通过一个真实案例演示 **如何从零创建 gridjs**、如何编写合适的 **gridjs 配置**、如何将网格绑定到 **gridjs 容器**，以及最后如何触发 **gridjs 渲染**。完成后，你将拥有一个可以直接放入任何项目的完整功能网格——没有神秘，只是清晰的代码。

## 你将学到

- 搭建一个最小化的 HTML 页面以使用 Gridjs。
- 编写 **gridjs 配置** 对象，定义列、数据和选项。
- 将 Gridjs 实例附加到 **gridjs 容器** 元素。
- 调用 **gridjs render** 来显示表格。
- 调整常用设置（分页、排序、样式）并避免典型陷阱。

无需任何外部构建工具；所有内容都在浏览器中通过单个 script 标签运行。让我们开始吧。

## 前置条件

在深入之前，请确保你拥有：

1. 现代浏览器（Chrome、Edge、Firefox、Safari）——支持 ES6。
2. 基本的 HTML 与 JavaScript 知识——不需要框架。
3. 可访问的 Gridjs 库——我们将从 CDN 引入，无需 npm 安装。

就这些。如果你已经有页面想要增强，只需把代码片段粘进去即可。

## 步骤 1：向页面添加 Gridjs 资源

首先，需要加载 Gridjs 的 CSS 与 JavaScript 文件。CDN 版本轻量且非常适合快速演示。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **专业提示：**Mermaid 主题为表格提供了简洁、现代的外观，无需额外 CSS。如果你更喜欢其他风格，可将其替换为 `classic.min.css`。

## 步骤 2：定义 **gridjs 容器**

**gridjs 容器** 只是一个普通的 `<div>`，用于承载渲染后的表格。在上面的标记中我们已经创建了 `<div id="grid"></div>`。`id` 属性至关重要，因为后面会用它来绑定 Gridjs 实例。

如果需要在同一页面上放置多个网格，请为每个容器分配唯一的 ID（`grid1`、`grid2` …），并为每个容器重复绑定逻辑。

## 步骤 3：编写 **gridjs 配置** 对象

下面就是 **如何创建 gridjs** 的核心——配置对象。这个普通的 JavaScript 对象告诉 Gridjs 要显示哪些列、填充哪些数据以及启用哪些功能。

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### 为什么这个配置很重要

- **Columns** – 定义表头文字及可选宽度。若不指定，Gridjs 会从第一行数据推断列名，往往不够友好。
- **Data** – 行数组，每行是一个单元格值数组。你也可以提供返回 Promise 的异步函数，库会自动处理。
- **Pagination** – 限制每页行数，防止巨表淹没 UI。
- **Search & Sort** – 只需一个布尔值即可开启交互式搜索与排序，省去自定义处理器。
- **Language** – 自定义 UI 文本，适用于本地化或品牌化。

后续如果想把静态数据数组换成 `fetch` 调用，其他步骤保持不变。

## 步骤 4：实例化 Gridjs 并绑定到 **gridjs 容器**

配置准备好后，创建一个新的 `GridJs.Grid`（在 UMD 构建中类名为 `gridjs.Grid`），并指向我们的容器元素。

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

注意我们使用了 `document.getElementById('grid')`——这就是前面定义的 **gridjs 容器**。如果有多个容器，只需使用相应的 ID 重复此行代码。

## 步骤 5：触发 **gridjs render** 调用

最后一步是调用 **gridjs render** 方法。它会使用前面传入的配置，在容器中注入一个完整样式的 `<table>`。

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

就这样！在浏览器中打开页面后，你会看到一个可搜索、分页的表格，包含我们定义的四行数据。搜索框会自动出现在顶部，分页控件位于底部。

### 预期输出

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

在搜索框输入内容或点击列标题进行排序时，UI 会相应更新。

## 常见变体与边缘情况

### 异步加载数据

如果数据存放在服务器上，使用返回 Promise 的函数替代静态 `data` 数组：

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs 会在 Promise 未完成时显示加载旋转图标，完成后自动渲染表格。

### 自定义单元格渲染

有时需要在单元格中放置图标、按钮或格式化日期。可以在列上使用 `formatter` 属性：

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

`gridjs.h` 辅助函数可以在不引入 React 的情况下创建虚拟 DOM 元素。

### 单页多个网格

只需使用不同的容器 ID 重复步骤 2‑5：

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

每个网格相互独立，你可以混合使用不同的分页限制、列集合甚至主题。

## 专业技巧与常见坑点

- **别忘了 CSS** —— 没有样式表，表格只会呈现为普通的 HTML 表格，失去所有美化和分页控件。
- **避免重复 ID** —— 每个 **gridjs 容器** 必须拥有唯一 ID，否则 Gridjs 会覆盖第一个实例。
- **注意数据结构** —— 列数必须与每行的单元格数匹配；不匹配会导致布局异常且不报错。
- **使用 `gridjs.h` 渲染复杂单元格** —— 直接注入原始 HTML 字符串可能破坏虚拟 DOM 的 diff 算法。
- **留意版本** —— 上面的 CDN 链接指向 2026 年 6 月的最新 5.x 版本。如果锁定旧版本，某些选项（如 `language`）可能不存在。

## 完整工作示例（复制‑粘贴）

下面是完整的 HTML 文件，可保存为 `gridjs-demo.html` 并直接在浏览器中打开。



## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在掌握本教程技术的基础上进一步扩展 API 功能并探索替代实现方式。

- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}