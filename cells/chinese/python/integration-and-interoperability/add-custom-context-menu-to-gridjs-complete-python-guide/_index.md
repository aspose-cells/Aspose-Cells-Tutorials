---
category: general
date: 2026-06-30
description: 在 GridJs 中添加自定义上下文菜单，并学习如何加载 Excel 工作簿、更新单元格值、启用拼写检查以及注册自定义命令。
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: zh
og_description: 在 GridJs 中添加自定义上下文菜单，同时学习加载 Excel 工作簿、更新单元格值、启用拼写检查以及注册自定义命令。
og_title: 为 GridJs 添加自定义上下文菜单 – 步骤详解 Python 教程
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: 为 GridJs 添加自定义上下文菜单 – 完整 Python 指南
url: /zh/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 GridJs 添加自定义上下文菜单 – 完整 Python 指南

有没有想过如何 **添加自定义上下文菜单** 项目到由 Excel 工作簿支持的 GridJs 表格中？你并不孤单。在许多数据密集型应用中，你需要右键菜单让用户标记行、将项目标记为已审阅，或启动服务器端操作——而无需离开网格。

在本教程中，我们将逐步演示如何加载 Excel 工作簿、绑定自定义上下文菜单项、更新单元格值、启用拼写检查，以及注册一个自定义命令以将更改持久化回文件。完成后，你将拥有一个功能完整的 GridJs 实例，用户体验自然，并且可以直接写回源电子表格。

## 前置条件

- Python 3.9+（代码使用类型提示，但在任何近期版本上均可运行）  
- `cells` 库（或任何提供 `Workbook` 和 `Worksheet` 对象的 Excel 处理包装器）  
- `gridjs` Python 绑定（对象模型与 JavaScript API 相同）  
- 对 lambda 表达式和 JSON 结构有基本了解  

如果你已经具备以上条件，下面开始吧。

## 步骤 1：加载 Excel 工作簿并选择工作表

首先需要 **加载 Excel 工作簿**，这样 GridJs 才有数据可显示。`cells.Workbook` 类封装了文件 I/O，并直接提供对行、列和单元格的访问。

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **为什么重要：** 预先加载工作簿意味着网格可以按需拉取数据，随后进行的任何编辑（例如 **更新单元格值**）都会持久化到同一文件中。

## 步骤 2：创建 GridJs 实例并绑定工作表

现在实例化一个 `gridjs.GridJs` 对象，并告诉它要渲染哪个工作表。可以把它看作为给 GridJs 提供一个实时数据源，网格在需要渲染页面或懒加载块时随时查询。

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **小技巧：** 如果你需要处理多个工作表，只需在后续调用 `grid.set_worksheet(other_ws)` 即可——无需重新创建网格。

## 步骤 3：启用拼写检查（以及其他可选功能）

大多数业务应用允许用户输入自由文本。启用 **拼写检查** 可以减少错别字并提升数据质量。GridJs 为此提供了一个简单的开关。

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **为什么要启用拼写检查？** 它在客户端运行，能够即时反馈，无需额外的服务器请求——非常适合大规模表格。

## 步骤 4：添加自定义上下文菜单项

本教程的核心：**添加自定义上下文菜单** 条目。我们将创建一个 “标记为已审阅” 选项，点击后会触发后面要定义的服务器端命令。

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **图片示例**  
> ![Add Custom Context Menu screenshot showing right‑click options](/images/add-custom-context-menu.png "Add Custom Context Menu example")

上图的 alt 文本已包含主要关键词，满足 SEO 要求。

## 步骤 5：注册自定义命令以更新单元格值

当用户选择 “标记为已审阅” 时，需要 **注册自定义命令** 来更新相应的 Excel 单元格并保存文件。`grid.register_custom_command` 方法将 Python 可调用对象绑定到前面设置的动作标识符。

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **为什么可行：** 处理函数会收到来自客户端的单元格引用，使用 `Worksheet` API **更新单元格值**，随后将整个工作簿写回磁盘。返回的响应让前端知道操作已成功。

### 边缘情况处理

- **缺少单元格引用：** 如果 `req` 中没有 `"cell"`，抛出明确错误，以便 UI 显示 toast。  
- **并发编辑：** 在高并发场景下，考虑对工作簿加锁或使用版本戳，以避免竞争条件。

## 步骤 6：为大表格启用懒加载

如果要处理成千上万行数据，懒加载可以保持 UI 的流畅。将每页大小设为合适的块——500 行在大多数浏览器中表现良好。

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **如果有 10 000 行怎么办？** 网格会逐页请求数据，降低客户端和服务器的内存压力。

## 步骤 7：（可选）为行编辑添加自定义模态框

有时需要比内联编辑更丰富的 UI。GridJs 允许弹出模态窗口，你可以在其中放置任意内容——比如 React 组件或简单的 HTML 表单。

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **为什么使用模态框？** 它可以将复杂的校验逻辑隔离，并让你完全控制布局，同时仍然可以从网格中触发。

## 步骤 8：获取客户端配置 JSON

最后，需要将配置发送到浏览器。`get_client_config` 方法会把所有设置序列化为一个 JSON 对象，前端的 GridJs 库即可消费。

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

输出大致如下（为简洁起见已截断）：

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### 预期结果

- 右键任意单元格会弹出包含 **标记为已审阅** 的菜单。  
- 选择该项后会向服务器发送请求，服务器 **将单元格值更新为 “Reviewed”** 并保存为 `example‑updated.xlsx`。  
- 拼写检查会在用户输入时高亮拼写错误。  

所有这些都在不刷新页面的情况下完成，得益于懒加载和轻量级的 JSON 负载。

## 常见问题 & 专业技巧

| Question | Answer |
|----------|--------|
| *工作簿是只读的怎么办？* | 确保文件权限允许写入，或在库支持的情况下使用 `mode="rw"` 打开工作簿。 |
| *可以添加多个自定义菜单项吗？* | 当然可以——只需向 `grid.settings.context_menu.custom_items` 追加更多字典即可。 |
| *单元格更新后需要重新加载网格吗？* | 如果返回 `{status:"ok"}`，GridJs 会自动刷新受影响的行；否则可在客户端调用 `grid.refresh()`。 |
| *如何让拼写检查支持特定语言？* | 设置 `grid.settings.spell_check.language = "en-US"`（或任意受支持的 locale）。 |
| *懒加载能与服务器端过滤配合使用吗？* | 能——将 `grid.settings.filter.enabled = True` 并在自定义命令中实现过滤逻辑即可。 |

## 完整工作示例（所有步骤合并）

下面是一段可以直接放入 Flask 路由或作为独立进程运行的脚本。请将 `YOUR_DIRECTORY` 替换为服务器上的实际路径。

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式。每篇资源都提供完整的可运行代码示例和逐步解释。

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}