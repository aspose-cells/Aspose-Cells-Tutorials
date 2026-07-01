---
category: general
date: 2026-06-30
description: Create GridJs instance in Python with custom modal settings. Learn how
  to bind a worksheet, configure the modal, and output client JSON.
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: en
og_description: Create GridJs instance in Python with custom modal settings. Step‑by‑step
  instructions for worksheet integration and client configuration.
og_title: Create GridJs Instance – Complete Python Guide
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: Create GridJs Instance – Complete Python Guide
url: /python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create GridJs Instance – Complete Python Guide

Ever wondered how to **create gridjs instance** from Python without pulling your hair out? You're not the only one. Whether you're building an admin dashboard, a product catalog, or a quick‑look spreadsheet, getting GridJs up and running is the first hurdle.  

In this tutorial we’ll walk through a real‑world example: binding a worksheet, turning on a custom modal that pops up on double‑click, and finally pulling the client‑side configuration JSON so you can feed it to the front‑end. By the end you’ll have a working GridJs setup you can drop into any Flask or Django project.

## Prerequisites

- Python 3.8+ installed locally  
- Basic familiarity with OOP in Python  
- A minimal `Worksheet` class (we’ll mock one for the demo)  

No external GridJs package exists for Python, so we’ll simulate the API that mirrors the JavaScript library. The concepts translate directly to the real GridJs JavaScript usage.

## Step 1: Define a Mock GridJs Class (GridJs Python API)

Before we can **create gridjs instance**, we need a thin wrapper that mimics the real library. This keeps the example runnable and focuses on the configuration flow.

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **Pro tip:** Keep the Python wrapper thin—just enough to generate the JSON you’ll hand off to the JavaScript side. Over‑engineering the bridge adds maintenance overhead.

## Step 2: Create a Simple Worksheet Object (GridJs Worksheet Integration)

Our **gridjs worksheet integration** can be as simple as a class with a `name` attribute. In a real app you’d pull data from a database or a CSV file.

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

Now you have a placeholder you can pass into the grid.

## Step 3: Assemble the Grid – The Core “Create GridJs Instance” Logic

With the mock classes ready, we can finally **create gridjs instance** and configure it step‑by‑step.

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### Expected Output (GridJs Client Configuration)

Running `python main.py` yields a nicely formatted JSON blob:

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

That JSON is exactly what you’d feed to the front‑end GridJs constructor:

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## Step 4: Hook the JSON into a Front‑End Page (Putting It All Together)

The **gridjs client configuration** you just printed can be embedded in a Flask route:

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **Why this works:** The back‑end supplies a JSON payload that mirrors the settings you defined in Python. The front‑end reads the same payload, ensuring the **gridjs custom modal** behaves exactly as you configured.

## Common Pitfalls and Edge Cases (GridJs Custom Modal)

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Modal never opens on double‑click | `custom_modal.enabled` left `False` | Ensure you set `grid.settings.custom_modal.enabled = True` |
| Modal dimensions look odd on mobile | Fixed pixel values (`600px`) don’t scale | Use CSS‑relative units (`80%`, `vh`) or media queries |
| URL returns 404 | The path `/product-editor.html` isn’t served | Add a static route in Flask/Django or host the file on a CDN |
| Worksheet name missing in JSON | `Worksheet` object lacks `name` attribute | Provide a meaningful `name` or extend the mock to include metadata |

Addressing these early saves you hours of debugging later.

## Extending the Example (Next Steps)

- **Load real data**: Replace the mock `Worksheet` with a pandas DataFrame and serialize rows to JSON.  
- **Secure the modal**: Add authentication checks before serving `/product-editor.html`.  
- **Dynamic column mapping**: Pull column headers from the worksheet schema instead of hard‑coding them.  
- **Internationalization**: Store modal titles in a language file and inject them via the JSON payload.

All these enhancements build on the same **create gridjs instance** foundation you just mastered.

## Conclusion

We’ve covered everything you need to **create gridjs instance** in Python, from wiring up a worksheet to turning on a custom modal and finally exposing a clean client‑side configuration JSON. The pattern is simple, reusable, and fits neatly into any modern web framework.

Give it a spin, tweak the modal dimensions, swap the worksheet for a real database query, and you’ll have a production‑ready GridJs integration in no time. Got questions? Drop a comment, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create a Custom Size Chart PDF with Aspose.Cells .NET: Step‑by‑Step Guide](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [How to Create a Custom Static Value Function in Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}