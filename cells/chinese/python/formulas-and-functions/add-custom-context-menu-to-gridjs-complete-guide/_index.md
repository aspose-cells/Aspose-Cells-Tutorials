---
category: general
date: 2026-06-08
description: 为 GridJs 添加自定义右键菜单，并将网格导出为 CSV（使用下载 CSV 文件的 Blob）。请按照此分步教程获取完整可运行的示例。
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: zh
og_description: 为 GridJs 添加自定义右键菜单，并使用下载 CSV 文件 Blob 将网格导出为 CSV。了解完整实现，耗时不到 10 分钟。
og_title: 为 GridJs 添加自定义右键菜单 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: 为 GridJs 添加自定义右键菜单 – 完整指南
url: /zh/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 GridJs 添加自定义右键菜单 – 完整指南

想要 **为 GridJs 组件添加自定义右键菜单** 吗？在本教程中我们将一步步演示如何实现，并展示如何使用 **download CSV file blob** 将 **grid 导出为 CSV**。无论你是在构建快速的管理面板还是完整的报表仪表盘，一个右键菜单让用户能够将数据导出为 CSV，都能显著提升工作效率。

我们将覆盖所有必要内容：使用 Flask 的 Python 后端、创建 Blob 的 JavaScript 处理函数，以及 GridJs 生成的 HTML/JS。完成后，你将拥有一个可直接嵌入任意项目的完整示例。

---

## 你需要准备的环境

在深入之前，请确保你已经具备：

- 已安装 **Python 3.9+** 和 **Flask**（`pip install flask`）。
- **gridjs** 的 Python 包装器（或直接使用 JavaScript 库）——本指南假设使用一个轻量的 Python 包装器，功能与 JavaScript API 相同。
- 对 **async JavaScript**（`fetch`、`Promise`）有基本了解——别担心，我们会逐行解释。
- 你喜欢的编辑器（VS Code、PyCharm，甚至是普通的文本编辑器都可以）。

就这些。无需额外的前端构建工具，也不需要 Node/npm。只需使用普通的 Flask 来提供 GridJs 生成的 HTML 即可。

---

## 为 GridJs 添加自定义右键菜单

首先需要告诉 GridJs 你想使用自定义的右键菜单。默认情况下，GridJs 只提供一套最小的菜单（复制、粘贴等），但你可以完全替换它。

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**为什么这很重要：**  
设置 `CustomContextMenu` 会用你提供的列表替换默认菜单。字符串 `"Export CSV"` 仅作为标签——真正的工作在用户点击时触发，我们将在下一步完成绑定。

> *小技巧：* 保持列表简短。杂乱的右键菜单会削弱快速操作的意义。

---

## 使用 Blob 下载将 Grid 导出为 CSV

有了菜单项后，我们需要一个 JavaScript 处理函数与服务器通信，获取 CSV，将其转换为 **Blob**，并强制下载。这正是 **download CSV file blob** 所指的场景。

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### 逐行解析处理函数

| 行号 | 作用说明 |
|------|----------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | 调用 Flask 路由 (`/export/csv`)，并通过查询字符串传递工作表名称。 |
| `.then(r => r.blob())` | 将 HTTP 响应转换为 **Blob** —— 实际上是 CSV 数据的二进制容器。 |
| `URL.createObjectURL(b)` | 生成一个临时 URL，浏览器可以将其视作文件。 |
| `a.download = cell.sheetName + ".csv"` | 设置下载对话框中显示的文件名。 |
| `a.click()` | 以编程方式点击隐藏的锚点，触发浏览器下载 Blob。 |

> **为什么使用 Blob？**  
> 浏览器无法直接下载 `fetch` 返回的原始文本，除非将其转换为类似文件的对象。Blob‑URL 技巧是最可靠、跨浏览器的方式，在不刷新页面的情况下触发 **download CSV file blob**。

---

## 配置 Flask 后端

前端处理函数需要访问 `/export/csv` 端点。下面是一个最小化的 Flask 视图函数，它接收工作表名称，从工作簿中获取数据，并以流的方式返回 CSV。

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### 关键要点

- **`io.StringIO`** 让我们在内存中构建 CSV，而无需操作文件系统。
- **`Content‑Disposition`** 告诉浏览器该文件是附件并建议文件名。虽然前端也设置了 `a.download`，但在服务器端提供此头部可以为非 JS 客户端提供回退。
- 该路由故意保持简洁；后续可以加入身份验证、权限检查或针对大数据集的流式传输。

---

## 在客户端渲染 Grid

在自定义右键菜单和后端准备就绪后，最后一步是渲染 GridJs 组件并将 HTML/JS 发送到浏览器。

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

在 Flask 视图中通常这样写：

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

页面加载后，GridJs 会构建表格，注入自定义右键菜单，之前定义的 JavaScript 处理函数也已准备就绪。右键任意单元格，选择 **Export CSV**，即可看到浏览器下载一个以工作表名称命名的文件。

---

## 完整可运行示例（所有文件）

下面是完整的可运行代码，你可以直接复制到新文件夹中。安装 Flask（`pip install flask`）并运行 `python app.py`。

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术进行扩展。每篇资源都提供完整的代码示例和逐步说明，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [加载 CSV 文件的自定义解析器（Aspose Cells Java）](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [CSV 导出 Java 代码](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [导出 Excel CSV 空行（Aspose Cells .NET）](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}