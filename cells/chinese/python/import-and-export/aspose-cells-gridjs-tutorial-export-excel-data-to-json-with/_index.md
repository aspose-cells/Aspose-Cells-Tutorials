---
category: general
date: 2026-07-03
description: Aspose Cells GridJs 教程，展示如何使用惰性加载高效地将 Excel 数据导出为 JSON，以及将工作表导出为 JSON。
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: zh
og_description: Aspose Cells GridJs 教程说明了如何将 Excel 数据导出为 JSON，以及如何在大型电子表格中使用惰性加载将工作表导出为
  JSON。
og_title: Aspose Cells GridJs 教程 – 将 Excel 数据导出为 JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Aspose Cells GridJs 教程 – 使用惰性加载将 Excel 数据导出为 JSON
url: /zh/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs 教程 – 使用惰性加载导出 Excel 数据 JSON

是否曾想过如何在不让浏览器卡死的情况下，从庞大的电子表格 **导出 Excel 数据 JSON**？在本 Aspose Cells GridJs 教程中，我们将一步步演示一个完整、可直接运行的方案，使用惰性加载 **导出工作表为 JSON**，仅在需要时按需获取所需的行。

如果你一直在与巨大的 `.xlsx` 文件作斗争，且客户端经常卡顿，你并不孤单。好消息是？我们在这里介绍的方法既轻量又可扩展，且可以直接放入任何已经使用 Aspose.Cells 库的 Python 项目中。

## 本指南涵盖内容

在接下来的几分钟里，你将学习如何：

1. 使用 Aspose.Cells 加载大型工作簿。
2. 开启 GridJs 惰性加载，使服务器分块流式传输行数据。
3. 将 GridJs 配置导出为前端可消费的 JSON 文件。
4. 调整块大小以获得最佳性能。
5. 验证输出并将其集成到一个简单的 HTML 页面中。

无需外部服务，也没有隐藏的魔法——仅使用纯 Python 和 Aspose.Cells API。完成后，你将拥有一个 **完整的导出工作表为 JSON** 流程，可用于仪表盘、报表工具或任何数据网格组件。

### 前置条件

- 本地已安装 Python 3.8+。
- `asposecells` 包（可通过 `pip install aspose-cells` 安装）。
- 一个较大的 Excel 文件（例如 `large-data.xlsx`），放置在已知目录下。
- 对 Python 和 Web 开发概念有基本了解。

如果上述任意一点你不熟悉，请不要慌——每一步都包含简短的 “为什么” 说明，帮助你理解代码背后的原理。

---

## 第 1 步：安装并导入 Aspose.Cells

首先，需要 Aspose.Cells 库。它是商业产品，但免费试用版足以用于开发。

```bash
pip install aspose-cells
```

现在在脚本中导入所需的类。

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **为什么这很重要：** 导入 `Workbook` 可让你使用高性能引擎直接将 Excel 文件读取到内存中，绕过更慢的 `openpyxl` 方式。

## 第 2 步：加载包含大数据集的工作簿

库准备就绪后，指向你的 Excel 文件。路径可以是绝对路径也可以是相对路径，只要确保文件存在即可。

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **专业提示：** 如果工作簿大小超过几百兆，考虑增大 Python 进程的内存限制或使用 64 位解释器，以避免 `MemoryError`。

## 第 3 步：启用 GridJs 惰性加载

GridJs 是 Aspose 的 JavaScript 网格组件。惰性加载指示服务器只发送部分行——这对超大表格尤为适用。

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **为什么使用惰性加载？** 如果不使用，它会一次性将整个工作表序列化为 JSON，极易超出浏览器内存限制。将 `LazyLoadingChunkSize` 设置为 500 后，每次请求只携带可管理的负载。

## 第 4 步：将 GridJs 配置导出为 JSON

现在让 Aspose 生成前端 GridJs 组件所需的 JSON。这是 **导出 Excel 数据 JSON** 操作的核心。

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

`ExportGridJsJson` 方法返回一个 `bytes` 对象，包含工作表的 JSON 表示，可直接保存或流式传输。

## 第 5 步：将 JSON 写入文件（或流式输出）

为了快速测试，先把 JSON 写入磁盘。在生产环境的 API 中，你可以直接从 Flask/Django 端点返回它。

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **你将看到：** 打开 `lazygrid.json` 后会看到包含 `columns`、`rows` 和分页元数据的结构。`rows` 数组最初为空；页面加载时 GridJs 会请求第一块数据。

## 第 6 步：将 JSON 接入简易 HTML 页面（可选）

如果想看到网格实际运行效果，创建一个小 HTML 文件，从 CDN 加载 GridJs 并指向生成的 JSON。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **为什么要加入这一步？** 它演示了完整的往返过程：Python 生成 JSON，浏览器获取并由 GridJs 按块渲染数据。你现在可以尝试不同的 `LazyLoadingChunkSize` 值，以找到网络环境的最佳平衡点。

## 第 7 步：验证并排查问题

运行 Python 脚本：

```bash
python export_lazy_grid.py
```

你应该会看到成功提示以及 `lazygrid.json` 文件。用浏览器打开 HTML 文件，网格应立即显示前 500 行，并提供分页控件以加载更多。

如果网格为空：

- **检查 JSON 文件大小** —— 零字节文件通常意味着工作簿路径错误。
- **确认已启用惰性加载** —— `LazyLoading` 标志必须为 `True`。
- **检查浏览器控制台** —— 任何 CORS 或 404 错误表明 JSON 未被正确提供。

---

## 常见变体与边缘情况

### 导出指定工作表

上例始终使用第一个工作表 (`Worksheets[0]`)。若要导出其他工作表，只需更改索引或使用工作表名称：

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### 为超大文件调整块大小

对于拥有数百万行的文件，500 的块大小可能仍然偏小，会导致大量往返请求。你可以将其提升至 2000 或更高，但要记住更大的块会在每次请求中消耗更多带宽。

```python
grid_options.LazyLoadingChunkSize = 2000
```

### 导出到流而非文件

如果你的 API 直接返回 JSON，则无需写入磁盘：

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### 处理公式和格式

默认情况下，`ExportGridJsJson` 包含公式的计算值。如果需要原始公式，请设置：

```python
grid_options.ExportFormulas = True
```

---

## 结论

在本 **Aspose Cells GridJs 教程** 中，我们涵盖了使用惰性加载 **导出 Excel 数据 JSON** 以及 **导出工作表为 JSON** 的全部步骤。从安装 Aspose.Cells、启用惰性加载、生成 JSON，到使用简易 HTML 页面进行展示，你现在拥有一个能够优雅扩展到超大电子表格的全栈模式。

动手试一试——调整块大小、指向不同工作表，或将端点集成到 Flask 或 Django 应用中。可能性无限，性能提升立竿见影。

准备好迈出下一步了吗？尝试添加列排序、自定义单元格渲染器，甚至服务器端过滤，让你的 GridJs 网格真正交互式。如果遇到问题，欢迎在下方留言；祝编码愉快！


## 接下来你应该学习什么？

以下教程与本指南紧密相关，基于本篇演示的技术进一步展开。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}