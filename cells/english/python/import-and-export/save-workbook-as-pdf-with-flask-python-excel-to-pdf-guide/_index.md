---
category: general
date: 2026-06-21
description: Save workbook as PDF using Flask and Aspose.Cells in Python – learn how
  to convert XLSX to PDF, auto‑fit Excel columns, and return the file with flask send_file
  pdf.
draft: false
keywords:
- save workbook as pdf
- convert xlsx to pdf
- python excel to pdf
- auto fit excel columns
- flask send_file pdf
language: en
og_description: Save workbook as PDF in Python using Flask. This step‑by‑step tutorial
  shows how to convert XLSX to PDF, auto‑fit Excel columns, and serve the result with
  flask send_file pdf.
og_title: Save Workbook as PDF with Flask – Complete Python Guide
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
title: Save Workbook as PDF with Flask – Python Excel to PDF Guide
url: /python/import-and-export/save-workbook-as-pdf-with-flask-python-excel-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Workbook as PDF with Flask – Python Excel to PDF Guide

Need to **save workbook as PDF** from a web service? You’re not the only one wondering how to turn an uploaded Excel file into a sleek PDF on the fly. In this guide we’ll walk through saving a workbook as PDF using Flask and Aspose.Cells, while also covering how to **convert XLSX to PDF**, auto‑fit Excel columns, and finally deliver the result with `flask send_file pdf`.

We'll start with a fresh Flask project, sprinkle in a few best‑practice tips, and end up with a fully functional endpoint that any client can call. By the time you finish, you’ll be able to turn any spreadsheet into a PDF in just a few lines of Python code.

## What You’ll Need

- **Python 3.8+** (the code works on 3.9, 3.10, and newer)
- **Flask** (`pip install flask`) – the lightweight web framework that powers our API
- **Aspose.Cells for Python via .NET** (`pip install aspose-cells`) – the library that actually reads XLSX and writes PDF
- A basic understanding of HTTP `POST` requests (nothing fancy)

If you already have these pieces, great—let’s dive in. If not, the “Install Dependencies” step will get you set up.

## Step 1 – Set Up the Flask Project

First, create a new folder for the project and spin up a virtual environment. This keeps our dependencies tidy.

```bash
mkdir flask_excel_pdf && cd flask_excel_pdf
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install flask aspose-cells
```

Now create a file called `app.py`. This will hold the entire **save workbook as pdf** logic.

## Step 2 – Initialize the Flask Application

We start by importing the pieces we need and creating the Flask app object. Notice how concise the import block is—no unused modules, which keeps the startup time low.

```python
# app.py
from flask import Flask, request, send_file
import aspose.cells as cells
import io

app = Flask(__name__)
```

> **Pro tip:** Keep `app = Flask(__name__)` at the top of the file; it makes later testing with tools like `pytest-flask` a breeze.

## Step 3 – Build the Conversion Endpoint (convert xlsx to pdf)

Here’s the heart of the tutorial: an endpoint that accepts a spreadsheet via `POST`, loads it into an Aspose.Cells workbook, and prepares it for PDF export.

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

### Why Each Piece Matters

- **`request.files.get("file")`** – Safely fetches the uploaded file; using `.get` avoids a `KeyError` if the field is missing.
- **`io.BytesIO`** – Keeps everything in RAM, so we never write temporary files to disk. This is crucial for scalability.
- **`auto_fit_columns()`** – Without this, column widths often appear cramped in the PDF. The method expands each column to fit its longest cell, giving a professional look.
- **`workbook.save(..., cells.SaveFormat.PDF)`** – This single call does the heavy lifting of converting XLSX to PDF. Aspose.Cells handles formulas, charts, and even merged cells.
- **`flask send_file pdf`** – Sends the PDF back to the client with appropriate headers, prompting a download named `output.pdf`.

## Step 4 – Run the Flask Server

Add the typical “run guard” at the bottom of `app.py` so the script can be executed directly.

```python
if __name__ == "__main__":
    # Listening on all interfaces makes testing from Docker or another machine easy
    app.run(host="0.0.0.0", port=5000, debug=True)
```

Running `python app.py` will start the server on `http://localhost:5000`. The `debug=True` flag is handy during development; remember to turn it off in production.

## Step 5 – Test the Endpoint (Manual & Automated)

### Manual Test with cURL

```bash
curl -X POST http://localhost:5000/convert \
  -F "file=@sample.xlsx" \
  -o result.pdf
```

If everything went well, `result.pdf` will contain a nicely formatted version of `sample.xlsx`, with all columns auto‑fitted.

### Automated Test with Python’s `requests`

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

Both approaches demonstrate the full **python excel to pdf** workflow—from upload to download—without ever touching the filesystem on the server side.

## Step 6 – Edge Cases & Common Pitfalls

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Large XLSX files ( > 50 MB ) | Memory pressure on the server | Stream the upload to a temporary file and use `Workbook(file_path)` instead of `BytesIO`. |
| Password‑protected workbook | `Workbook` throws an exception | Pass the password to `Workbook` constructor: `Workbook(io.BytesIO(file_bytes), cells.LoadOptions(password="secret"))`. |
| Missing `auto_fit_columns()` | PDF columns appear truncated | Always call `auto_fit_columns()` **before** `save()`. |
| Client expects a JSON error | Flask returns HTML error page | Return a JSON dict with proper status code as shown in the endpoint (line `return {"error": "No file provided"}, 400`). |

By anticipating these scenarios, your API stays robust and user‑friendly.

## Step 7 – Deploying to Production

When you’re ready to go live, consider these production‑grade adjustments:

- **Use a WSGI server** like `gunicorn` (`gunicorn -w 4 app:app`) instead of Flask’s built‑in server.
- **Enable HTTPS** via a reverse proxy (NGINX) to protect file uploads.
- **Set a request size limit** (`app.config["MAX_CONTENT_LENGTH"] = 20 * 1024 * 1024`) to avoid denial‑of‑service attacks.
- **Log errors** with a structured logger (e.g., `structlog`) so you can trace conversion failures.

All of these steps preserve the core **save workbook as pdf** logic while making the service production‑ready.

## Expected Output

When you hit the `/convert` endpoint with a valid XLSX file, the response will:

1. Have a `Content-Type: application/pdf` header.
2. Prompt the browser (or client) to download a file named `output.pdf`.
3. Render the spreadsheet with columns automatically sized to their content, thanks to the `auto fit excel columns` call.

Open the downloaded PDF—you should see each column fully visible, formulas evaluated, and any embedded images preserved.

## Conclusion

You now have a complete, production‑ready example that **save workbook as pdf** using Flask, Aspose.Cells, and pure Python. The tutorial covered everything from setting up the environment, **convert xlsx to pdf**, auto‑fitting columns, and finally delivering the result with `flask send_file pdf`. 

Next, you might explore adding **custom styling**, merging cells, or even converting multiple worksheets into a single multi‑page PDF. The same pattern works for other file types—just swap the `SaveFormat` enum.

Got questions about edge cases or deployment? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save Specific Pages of an Excel File as PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Save Excel Workbook as PDF with Custom Fonts using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Convert Excel to PDF with Fit Columns in Java using Aspose.Cells](/cells/english/java/workbook-operations/convert-excel-to-pdf-fit-columns-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}