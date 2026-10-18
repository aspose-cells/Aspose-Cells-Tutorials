---
category: general
date: 2026-06-08
description: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें और ग्रिड को CSV में निर्यात
  करें, साथ ही डाउनलोड CSV फ़ाइल ब्लॉब के साथ। पूरी तरह कार्यशील उदाहरण के लिए इस
  चरण‑दर‑चरण ट्यूटोरियल का पालन करें।
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: hi
og_description: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें और ग्रिड को CSV में एक्सपोर्ट
  करें, डाउनलोड CSV फ़ाइल ब्लॉब के साथ। 10 मिनट से कम समय में पूरी इम्प्लीमेंटेशन
  सीखें।
og_title: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – पूर्ण गाइड
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
title: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – पूर्ण गाइड
url: /hi/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs में कस्टम कॉन्टेक्स्ट मेन्यू जोड़ें – पूर्ण गाइड

क्या आप **GridJs कॉम्पोनेन्ट** में **कस्टम कॉन्टेक्स्ट मेन्यू** जोड़ना चाहते हैं? इस ट्यूटोरियल में हम आपको ठीक‑ठीक वही दिखाएंगे, और यह भी बताएंगे कि **ग्रिड को CSV में एक्सपोर्ट** कैसे किया जाए **download CSV file blob** का उपयोग करके। चाहे आप एक त्वरित एडमिन पैनल बना रहे हों या पूर्ण‑स्तरीय रिपोर्टिंग डैशबोर्ड, एक राइट‑क्लिक मेन्यू जो उपयोगकर्ताओं को डेटा CSV के रूप में निकालने की अनुमति देता है, उत्पादकता में बड़ा इज़ाफ़ा कर सकता है।

हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: Flask के साथ Python साइड, वह JavaScript हैंडलर जो Blob बनाता है, और वह HTML/JS जो GridJs आउटपुट करता है। अंत तक आपके पास एक स्व-समाहित उदाहरण होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

---

## आपको क्या चाहिए

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

- **Python 3.9+** और **Flask** इंस्टॉल हो (`pip install flask`)।
- **gridjs** Python रैपर (या सीधे JavaScript लाइब्रेरी) – इस गाइड में हम मानेंगे कि एक हल्का Python रैपर है जो JavaScript API को मिरर करता है।
- **async JavaScript** (`fetch`, `Promise`) की बुनियादी समझ – लेकिन चिंता न करें, हम हर लाइन को समझाएंगे।
- वह एडिटर जो आपको **पसंद** हो (VS Code, PyCharm, या साधा टेक्स्ट एडिटर भी चलेगा)।

बस इतना ही। कोई अतिरिक्त फ्रंट‑एंड बिल्ड टूल नहीं, कोई Node npm डांस नहीं। सिर्फ़ साधा Flask जो वह HTML सर्व करता है जो GridJs जेनरेट करता है।

---

## GridJs में कस्टम कॉन्टेक्स्ट मेन्यू जोड़ें

सबसे पहले आपको GridJs को बताना होगा कि आप एक कस्टम राइट‑क्लिक मेन्यू चाहते हैं। डिफ़ॉल्ट रूप से GridJs एक न्यूनतम सेट (copy, paste, आदि) के साथ आता है, लेकिन आप इसे पूरी तरह बदल सकते हैं।

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**यह क्यों महत्वपूर्ण है:**  
`CustomContextMenu` सेट करने से डिफ़ॉल्ट सूची को आपके द्वारा प्रदान की गई सूची से बदल दिया जाता है। स्ट्रिंग `"Export CSV"` सिर्फ़ एक लेबल है – असली काम तब होता है जब उपयोगकर्ता इस पर क्लिक करता है, जिसे हम अगले चरण में जोड़ेंगे।

> *Pro tip:* सूची को छोटा रखें। एक भरी‑भरी कॉन्टेक्स्ट मेन्यू तेज़ कार्रवाई के उद्देश्य को बिगाड़ देता है।

---

## Blob डाउनलोड के साथ ग्रिड को CSV में एक्सपोर्ट करें

अब जब मेन्यू आइटम मौजूद है, हमें एक JavaScript हैंडलर चाहिए जो सर्वर से बात करे, CSV फ़ेच करे, उसे **Blob** में बदल दे, और डाउनलोड को फोर्स करे। यही वह जगह है जहाँ **download CSV file blob** वाक्यांश आता है।

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

### हैंडलर का विवरण

| लाइन | क्या करता है |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Flask रूट (`/export/csv`) को कॉल करता है और शीट नाम को क्वेरी स्ट्रिंग के रूप में भेजता है। |
| `.then(r => r.blob())` | HTTP रिस्पॉन्स को **Blob** में बदलता है – मूलतः CSV डेटा के लिए एक बाइनरी कंटेनर। |
| `URL.createObjectURL(b)` | एक अस्थायी URL बनाता है जिसे ब्राउज़र फ़ाइल की तरह ट्रीट कर सकता है। |
| `a.download = cell.sheetName + ".csv"` | फ़ाइलनाम सेट करता है जो उपयोगकर्ता को डाउनलोड डायलॉग में दिखेगा। |
| `a.click()` | छिपे हुए एंकर को प्रोग्रामेटिकली क्लिक करता है, जिससे ब्राउज़र Blob को डाउनलोड करता है। |

> **Blob क्यों उपयोग करें?**  
> ब्राउज़र सीधे `fetch` से लौटे कच्चे टेक्स्ट को फ़ाइल‑जैसा नहीं डाउनलोड कर सकता जब तक कि उसे Blob में न बदला जाए। Blob‑URL ट्रिक सबसे भरोसेमंद, क्रॉस‑ब्राउज़र तरीका है **download CSV file blob** को ट्रिगर करने का, बिना पेज रिफ्रेश किए।

---

## Flask बैकएंड सेट अप करें

फ़्रंट‑एंड हैंडलर को `/export/csv` पर एक एंडपॉइंट चाहिए। यहाँ एक न्यूनतम Flask व्यू है जो शीट नाम लेता है, वर्कबुक से डेटा निकालता है, और CSV को स्ट्रीम करता है।

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

### मुख्य बिंदु

- **`io.StringIO`** हमें फ़ाइल सिस्टम को छुए बिना मेमोरी में CSV बनाने देता है।
- **`Content‑Disposition`** ब्राउज़र को बताता है कि फ़ाइल एक अटैचमेंट है और फ़ाइलनाम सुझाता है। जबकि फ्रंट‑एंड भी `a.download` सेट करता है, सर्वर‑साइड पर यह सेटिंग नॉन‑JS क्लाइंट्स के लिए फ़ॉलबैक प्रदान करती है।
- रूट जानबूझकर सरल रखा गया है; बाद में आप ऑथेंटिकेशन, परमिशन चेक्स, या बड़े डेटा सेट्स के लिए स्ट्रीमिंग जोड़ सकते हैं।

---

## क्लाइंट पर ग्रिड रेंडर करना

कस्टम कॉन्टेक्स्ट मेन्यू और बैकएंड तैयार होने के बाद, अंतिम कदम है GridJs कॉम्पोनेन्ट को रेंडर करना और HTML/JS को ब्राउज़र तक पहुंचाना।

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Flask व्यू में आमतौर पर आप इस तरह करेंगे:

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

जब पेज लोड होता है, GridJs टेबल बनाता है, कस्टम कॉन्टेक्स्ट मेन्यू इन्जेक्ट करता है, और वह JavaScript हैंडलर जो हमने पहले परिभाषित किया था, तैयार रहता है। किसी भी सेल पर राइट‑क्लिक करें, **Export CSV** चुनें, और देखें कि ब्राउज़र शीट के नाम पर फ़ाइल डाउनलोड करता है।

---

## पूर्ण कार्यशील उदाहरण (सभी फ़ाइलें)

नीचे पूरा, चलाने योग्य कोड दिया गया है जिसे आप नई फ़ोल्डर में कॉपी‑पेस्ट कर सकते हैं। Flask इंस्टॉल करें (`pip install flask`) और `python app.py` चलाएँ।

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
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


## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}