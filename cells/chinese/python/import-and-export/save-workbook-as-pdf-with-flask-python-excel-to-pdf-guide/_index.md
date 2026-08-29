---
category: general
date: 2026-06-21
description: 使用 Flask 和 Aspose.Cells 在 Python 中将工作簿保存为 PDF——学习如何将 XLSX 转换为 PDF、自动调整
  Excel 列宽，并使用 Flask 的 send_file 返回 PDF 文件。
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: zh
og_description: 使用 Flask 在 Python 中将工作簿保存为 PDF。本分步教程展示了如何将 XLSX 转换为 PDF、自动适配 Excel
  列宽，并使用 Flask 的 send_file 发送 PDF 文件。
og_title: 使用 Flask 将工作簿保存为 PDF – 完整 Python 指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  headline: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  type: TechArticle
- description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn
    how to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask
    send_file pdf.
  name: Save Workbook as PDF with Flask – Python Excel to PDF Guide
  steps:
  - name: Why Each Piece Matters
    text: '- **`request.files.get("file")`** – Safely fetches the uploaded file; using
      `.get` avoids a `KeyError` if the field is missing. - **`io.BytesIO`** – Keeps
      everything in RAM, so we never write temporary files to disk. This is crucial
      for scalability. - **`auto_fit_columns()`** – Without this, column '
  - name: Manual Test with cURL
    text: '```bash curl -X POST http://localhost:5000/convert  -F "file=@sample.xlsx"  -o
      result.pdf ```'
  - name: Automated Test with Python’s `requests`
    text: '```python import requests'
  type: HowTo
tags:
- flask
- python
- excel
- pdf
- aspose-cells
title: 使用 Flask 将工作簿保存为 PDF – Python Excel 转 PDF 指南
url: /zh/python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Flask 将工作簿保存为 PDF – Python Excel 转 PDF 指南

需要 **将工作簿保存为 PDF** 并通过 Web 服务提供吗？你并不是唯一一个想把上传的 Excel 文件即时转换为精美 PDF 的人。在本指南中，我们将演示如何使用 Flask 和 Aspose.Cells 将工作簿保存为 PDF，同时涵盖 **将 XLSX 转换为 PDF**、自动适配 Excel 列宽，最终使用 `flask send_file pdf` 将结果返回。

我们将从一个全新的 Flask 项目开始，加入一些最佳实践技巧，最终得到一个任何客户端都可以调用的完整端点。完成后，你只需几行 Python 代码即可将任意电子表格转换为 PDF。

## 你需要准备的环境

- **Python 3.8+**（代码在 3.9、3.10 以及更高版本均可运行）
- **Flask**（`pip install flask`）– 为我们的 API 提供轻量级的 Web 框架
- **Aspose.Cells for Python via .NET**（`pip install aspose-cells`）– 实际读取 XLSX 并写入 PDF 的库
- 对 HTTP `POST` 请求的基本了解（不需要高级技巧）

如果你已经具备以上条件，太好了——直接进入下一步。如果没有，“安装依赖”步骤会帮你完成准备工作。

## 第一步 – 创建 Flask 项目

首先，为项目创建一个新文件夹并启动虚拟环境。这样可以保持依赖整洁。

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

随后创建一个名为 `app.py` 的文件。该文件将承载完整的 **save workbook as pdf** 逻辑。

## 第二步 – 初始化 Flask 应用

我们先导入所需模块并创建 Flask 应用对象。请注意导入块保持简洁——没有未使用的模块，这有助于降低启动时间。

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **小技巧：** 将 `app = Flask(__name__)` 放在文件顶部；这样在使用 `pytest-flask` 等工具进行后续测试时会更加方便。

## 第三步 – 构建转换端点（convert xlsx to pdf）

下面是本教程的核心：一个接受 `POST` 上传的电子表格、将其加载到 Aspose.Cells 工作簿并准备导出为 PDF 的端点。

```python
@app.route("/convert", methods=["POST"])
def convert():
    # 1️⃣ Grab the uploaded file from the request
    uploaded = request.files.get("file")
    if not uploaded:
        return {"error": "No file provided"}, 400

    # 2️⃣ Read the file into memory (binary)
    file_bytes = uploaded.read()

    # 3️⃣ Load the spreadsheet into a workbook object
    workbook = cells.Workbook(io.BytesIO(file_bytes))

    # 4️⃣ Auto‑fit all columns in the first sheet (auto fit excel columns)
    workbook.worksheets[0].auto_fit_columns()

    # 5️⃣ Save the workbook as PDF into an in‑memory stream
    pdf_stream = io.BytesIO()
    workbook.save(pdf_stream, cells.SaveFormat.PDF)
    pdf_stream.seek(0)

    # 6️⃣ Return the PDF using flask send_file pdf
    return send_file(
        pdf_stream,
        mimetype="application/pdf",
        as_attachment=True,
        download_name="output.pdf"
    )
```

### 每个部分为何重要

- **`request.files.get("file")`** – 安全获取上传的文件；使用 `.get` 可以避免字段缺失时抛出 `KeyError`。
- **`io.BytesIO`** – 将所有内容保存在内存中，永不写入临时磁盘文件。这对可扩展性至关重要。
- **`auto_fit_columns()`** – 若不调用此方法，PDF 中的列宽常常显得过窄。该方法会根据最长单元格自动扩展列宽，呈现专业外观。
- **`workbook.save(..., cells.SaveFormat.PDF)`** – 这一步完成了 XLSX 到 PDF 的核心转换。Aspose.Cells 能处理公式、图表乃至合并单元格。
- **`flask send_file pdf`** – 使用适当的响应头将 PDF 发送回客户端，并提示下载文件名为 `output.pdf`。

## 第四步 – 运行 Flask 服务器

在 `app.py` 底部添加常规的 “run guard”，使脚本可以直接执行。

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

运行 `python app.py` 将在 `http://localhost:5000` 启动服务器。`debug=True` 在开发阶段非常便利；上线前记得关闭。

## 第五步 – 测试端点（手动 & 自动化）

### 使用 cURL 手动测试

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

如果一切顺利，`result.pdf` 将包含 `sample.xlsx` 的精美格式化版本，且所有列已自动适配。

### 使用 Python `requests` 自动化测试

```python
import requests

with open("sample.xlsx", "rb") as f:
    response = requests.post(
        "http://localhost:5000/convert",
        files={"file": f}
    )
    response.raise_for_status()
    with open("downloaded.pdf", "wb") as out:
        out.write(response.content)

print("PDF saved as downloaded.pdf")
```

这两种方式都展示了完整的 **python excel to pdf** 工作流——从上传到下载，整个过程无需在服务器端触及文件系统。

## 第六步 – 边缘情况与常见陷阱

| 场景 | 需要注意的点 | 解决方案 |
|-----------|-------------------|-----|
| 大型 XLSX 文件（> 50 MB） | 服务器内存压力 | 将上传流式写入临时文件，并使用 `Workbook(file_path)` 替代 `BytesIO`。 |
| 受密码保护的工作簿 | `Workbook` 抛出异常 | 在 `Workbook` 构造函数中传入密码：`Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`。 |
| 未调用 `auto_fit_columns()` | PDF 列被截断 | 必须在 `save()` **之前** 调用 `auto_fit_columns()`。 |
| 客户端期望 JSON 错误信息 | Flask 返回 HTML 错误页 | 按端点示例返回 JSON 字典并设置正确的状态码（如 `return {"error": "No file provided"}, 400`）。 |

提前考虑这些情况，可让你的 API 更加健壮且友好。

## 第七步 – 部署到生产环境

准备上线时，请考虑以下生产级别的调整：

- **使用 WSGI 服务器** 如 `gunicorn`（`gunicorn -w 4 app:app`）替代 Flask 内置服务器。
- **通过反向代理（NGINX）启用 HTTPS**，保护文件上传过程。
- **设置请求大小限制**（`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`），防止拒绝服务攻击。
- **使用结构化日志记录器**（如 `structlog`）记录错误，便于追踪转换失败原因。

上述步骤均保持核心 **save workbook as pdf** 逻辑不变，只是让服务更适合生产环境。

## 预期输出

当你使用有效的 XLSX 文件调用 `/convert` 端点时，响应将：

1. 包含 `Content-Type: application/pdf` 头部。
2. 促使浏览器（或客户端）下载名为 `output.pdf` 的文件。
3. 通过 `auto fit excel columns` 调用，使每列宽度自动适配内容，呈现完整可见的列、已计算的公式以及保留的嵌入图片。

打开下载的 PDF，你应当看到每列全部可见、公式已求值、图片完整保留。

## 结论

现在，你已经拥有一个完整的、可投入生产的示例，使用 Flask、Aspose.Cells 与纯 Python 实现 **save workbook as pdf**。本教程涵盖了从环境搭建、**convert xlsx to pdf**、自动适配列宽，到使用 `flask send_file pdf` 返回结果的全部步骤。

接下来，你可以尝试添加 **自定义样式**、合并单元格，甚至将多个工作表合并为单个多页 PDF。同样的模式也适用于其他文件类型——只需更换 `SaveFormat` 枚举即可。

对边缘情况或部署有疑问？欢迎在下方留言，祝编码愉快！

## 接下来你可以学习什么？

以下教程与本指南紧密相关，帮助你进一步深化所学技术。每篇资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并在项目中探索替代实现方案。

- [How to Save Specific Pages of an Excel File as PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Save Excel Workbook as PDF with Custom Fonts using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Convert Excel to PDF with Fit Columns in Java using Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}