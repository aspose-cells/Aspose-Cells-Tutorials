---
category: general
date: 2026-06-30
description: 向 Python Excel 网格添加自定义上下文菜单，并在保存更新的文件时将值写入 Excel 单元格。学习如何创建右键菜单以及以 Python
  方式更新单元格值。
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: zh
og_description: 在 Python 中添加自定义上下文菜单，以将值写入 Excel 单元格并保存更新后的 Excel 文件。本指南将带您通过 GridJs
  创建右键菜单。
og_title: 在 Python 中添加自定义右键菜单 – 步骤教程
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: 在 Python 中添加自定义上下文菜单 – 完整指南
url: /zh/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中添加自定义上下文菜单 – 完整指南

是否曾想过如何在 Python 提供的电子表格网格中 **添加自定义上下文菜单** 项目？也许你需要一个快速的“Mark as Reviewed”按钮，当用户右键单击单元格时弹出，向 Excel 单元格写入值，然后保存更新后的工作簿——全部在网页 UI 中完成。  

在本教程中，我们将构建正是如此的功能：一个由 GridJs 提供支持的 **custom right‑click menu**，一个在服务器端 **write(s) value to excel cell** 的处理程序，以及一个将更新后的 Excel 文件 **save(s) updated excel file** 到磁盘的最终步骤。完成后，你将拥有一个可在任何 Flask、FastAPI 或 Django 项目中使用的可复用模式。

> **为什么在乎？**  
> 添加自定义上下文菜单可以简化数据审查工作流，减少手动复制粘贴，并为最终用户提供直接在网格内的原生体验。此外，你还将看到如何以 **update cell value python**‑style 的方式更新单元格值，这是一项 Excel 自动化任务的核心技能。

## 前置条件

- Python 3.9+（代码在 3.10 上也可运行）  
- `openpyxl` 用于 Excel 文件处理  
- `gridjs` Python 包装器（或如果你更喜欢前端则使用 JS 库）  
- 基础 Web 框架（示例使用 Flask）  
- 项目文件夹中名为 `sample.xlsx` 的工作簿文件  

如果缺少上述任意项，请运行：

```bash
pip install openpyxl flask gridjs
```

现在让我们开始吧。

---

## 第一步 – 添加自定义上下文菜单：初始化 GridJs 并绑定工作表

你需要做的第一件事是启动一个 `GridJs` 实例并指向你计划使用的工作表。这就是 **add custom context menu** 短语首次出现在代码中的位置，它为后续所有操作奠定基础。

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**发生了什么？**  
`grid.set_worksheet(ws)` 告诉 GridJs 使用 `ws` 的数据作为数据源。从此以后，我们添加的任何 context‑menu 修改都会自动针对同一工作表，保持 UI 与文件同步。

> **专业提示：** 只在读取/写入模式下打开工作簿一次。在请求处理程序中反复打开会导致 Windows 上的文件锁定问题。

## 第二步 – 将值写入 Excel 单元格：为菜单项定义操作

现在网格已就绪，我们需要在用户选择自定义命令时 **write value to excel cell**。我们将添加一个名为 “Mark as Reviewed” 的菜单项，并为其指定标识符 `markReviewed`。该标识符是客户端 JavaScript 将返回给服务器的内容。

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**为什么使用自定义标识符？**  
标识符将 UI 文本与服务器逻辑解耦，使你可以在不修改后端代码的情况下更改标签。它还使 **create right‑click menu** 操作变得明确且可复用。

## 第三步 – 创建右键菜单：注册服务器端处理程序

有了菜单项后，我们需要告诉 GridJs 用户点击时应执行的操作。这就是我们实现 **create right‑click menu** 功能并实际向 Python 发起请求的地方。

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

需要注意的几点：

1. **`ws[cell_address] = "Reviewed"`** 是 **update cell value python** 最直接的方式。底层，`openpyxl` 会将 A1 样式的地址转换为行/列索引。  
2. 处理程序返回一个小的 JSON 负载。GridJs 期待一个状态指示器；如有需要，你可以扩展以包含错误信息。

现在我们将标识符绑定到处理程序：

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**如果单元格为空或受保护怎么办？**  
- 空单元格没有问题——`openpyxl` 会即时创建。  
- 对于受保护的工作表，需要先取消保护 (`ws.protection.sheet = False`) 或捕获 `PermissionError`。

## 第四步 – 更新单元格值（Python）：通过保存工作簿持久化更改

写入值只是故事的一半；你必须 **save updated excel file**，使更改在当前会话之外仍然有效。这就是我们完成从 UI 到磁盘的往返过程的地方。

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**为什么使用单独的文件夹？**  
保存到 `output/` 目录可以保持原始模板不被修改，这对审计追踪很有用。请根据你的部署环境调整路径。

> **注意：** 如果你服务大量并发用户，考虑在 `wb.save()` 周围使用线程安全锁 (`threading.Lock`) 以避免竞争条件。

## 第五步 – 生成客户端配置 JSON 并将所有部分连接起来

最后，我们需要生成前端 GridJs 实例将使用的 JSON。该 JSON 包含工作表数据 **以及** 自定义菜单定义。

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

当你将 `config_json` 嵌入到 HTML 页面时，GridJs 将渲染网格，并在每个单元格上提供可右键点击的 “Mark as Reviewed” 条目。

### 完整 Flask 示例

下面是一个最小的 Flask 应用，将所有部分组合在一起。运行它，打开 `http://localhost:5000`，右键单击任意单元格即可看到自定义菜单的效果。

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**预期结果：**  
- 右键单击任意单元格 → 出现 “Mark as Reviewed”。  
- 点击它 → 单元格内容更改为 “Reviewed”。  
- 工作簿 `output/sample-updated.xlsx` 现在包含了新值。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *如果需要多个自定义操作怎么办？* | 只需向 `grid.settings.context_menu.custom_items` 添加更多对象，并为每个对象注册其自己的标识符。 |
| *我可以向处理程序传递额外数据（例如行 ID）吗？* | 可以。在客户端的 JSON 负载中包含额外的键，然后在 `on_custom_command` 中从 `request` 读取它们。 |
| *这种方法是否兼容异步框架？* | 完全兼容——只需将 `on_custom_command` 定义为 async 函数，并在使用 `aiofiles` 或类似库时使用 `await wb.save(...)`。 |
| *如何为菜单图标设置样式？* | 提供任意 Material‑Icons 名称（如 `"icon": "edit"`）。前端会自动加载图标字体。 |
| *大工作簿怎么办？* | 只加载所需的工作表，并考虑使用 `openpyxl.iter_rows()` 流式读取行，以降低内存使用。 |

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}