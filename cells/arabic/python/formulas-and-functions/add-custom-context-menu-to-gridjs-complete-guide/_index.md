---
category: general
date: 2026-06-08
description: أضف قائمة سياق مخصصة إلى GridJs وقم بتصدير الشبكة إلى CSV باستخدام ملف
  Blob للتحميل. اتبع هذا الدليل خطوة بخطوة للحصول على مثال يعمل بالكامل.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: ar
og_description: أضف قائمة سياق مخصصة إلى GridJs وصدر الشبكة إلى CSV باستخدام ملف Blob
  للتحميل. تعلّم التنفيذ الكامل في أقل من 10 دقائق.
og_title: إضافة قائمة سياق مخصصة إلى GridJs – دليل كامل
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
title: إضافة قائمة سياق مخصصة إلى GridJs – دليل كامل
url: /ar/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة قائمة سياق مخصصة إلى GridJs – دليل كامل

هل تريد **إضافة قائمة سياق مخصصة** إلى مكوّن GridJs؟ في هذا الدرس سنرشدك خطوة بخطوة إلى ذلك، وسنوضح لك كيفية **تصدير الشبكة إلى CSV** باستخدام **download CSV file blob**. سواءً كنت تبني لوحة تحكم إدارية سريعة أو لوحة تقارير متكاملة، فإن قائمة النقر بزر الفأرة الأيمن التي تسمح للمستخدمين باستخراج البيانات كملف CSV يمكن أن تكون دفعة حقيقية للإنتاجية.

سنغطي كل ما تحتاجه: الجانب الخاص بـ Python مع Flask، ومعالج JavaScript الذي ينشئ الـ Blob، وHTML/JS الذي يولده GridJs. في النهاية ستحصل على مثال مستقل يمكنك إدراجه في أي مشروع.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- **Python 3.9+** و **Flask** مثبتين (`pip install flask`).
- غلاف **gridjs** للـ Python (أو المكتبة JavaScript مباشرة) – في هذا الدليل سنفترض وجود غلاف Python خفيف يعكس واجهة برمجة التطبيقات JavaScript.
- فهم أساسي لـ **async JavaScript** (`fetch`, `Promise`) – لكن لا تقلق، سنشرح كل سطر.
- محرر تحبه (VS Code، PyCharm، أو حتى محرر نصوص بسيط).

هذا كل شيء. لا أدوات بناء front‑end إضافية، لا رقص Node npm. مجرد Flask بسيط يقدم الـ HTML الذي يولده GridJs.

---

## إضافة قائمة سياق مخصصة إلى GridJs

أول شيء عليك فعله هو إخبار GridJs أنك تريد قائمة سياق مخصصة عند النقر بزر الفأرة الأيمن. بشكل افتراضي، يأتي GridJs بمجموعة بسيطة (نسخ، لصق، إلخ)، لكن يمكنك استبدالها بالكامل.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**لماذا هذا مهم:**  
ضبط `CustomContextMenu` يستبدل القائمة الافتراضية بالقائمة التي تقدمها. النص `"Export CSV"` هو مجرد تسمية – العمل الحقيقي يحدث عندما ينقر المستخدم عليها، وسنربط ذلك في الخطوة التالية.

> *نصيحة محترف:* حافظ على القائمة قصيرة. القائمة المزدحمة تُفقد الغرض من الإجراءات السريعة.

---

## تصدير الشبكة إلى CSV باستخدام تحميل Blob

الآن بعد أن عنصر القائمة موجود، نحتاج إلى معالج JavaScript يتواصل مع الخادم، يجلب ملف CSV، يحوله إلى **Blob**، ويجبر المتصفح على التحميل. هنا يأتي مصطلح **download CSV file blob**.

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

### شرح المعالج

| السطر | ما يفعله |
|------|----------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | يستدعي مسار Flask (`/export/csv`) مع تمرير اسم الورقة كسلسلة استعلام. |
| `.then(r => r.blob())` | يحول استجابة HTTP إلى **Blob** – حاوية ثنائية للبيانات CSV. |
| `URL.createObjectURL(b)` | يولد عنوان URL مؤقت يمكن للمتصفح التعامل معه كملف. |
| `a.download = cell.sheetName + ".csv"` | يحدد اسم الملف الذي سيظهر للمستخدم في نافذة التحميل. |
| `a.click()` | ينقر برمجيًا على العنصر المخفي `<a>`، مما يدفع المتصفح لتحميل الـ Blob. |

> **لماذا نستخدم Blob؟**  
> لا يمكن للمتصفحات تحميل نص خام يُرجع من `fetch` مباشرةً دون تحويله إلى شيء يشبه الملف. حيلة الـ Blob‑URL هي الطريقة الأكثر موثوقية ومتوافقة عبر المتصفحات لتفعيل **download CSV file blob** دون تحديث الصفحة.

---

## إعداد خلفية Flask

معالج الواجهة الأمامية يتوقع نقطة وصول عند `/export/csv`. إليك عرض Flask بسيط يأخذ اسم الورقة، يجلب البيانات من المصنف، ويرسل CSV كاستجابة.

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

### نقاط رئيسية

- **`io.StringIO`** يتيح لنا بناء CSV في الذاكرة دون الحاجة إلى نظام الملفات.
- **`Content‑Disposition`** يخبر المتصفح أن الملف مرفق ويقترح اسمًا للملف. رغم أن الواجهة الأمامية تحدد `a.download`، فإن وجوده على الخادم يوفر بديلًا للعملاء غير المدعومين للـ JavaScript.
- المسار بسيط عمدًا؛ يمكنك إضافة المصادقة، فحوصات الصلاحية، أو البث للبيانات الضخمة لاحقًا.

---

## عرض الشبكة على العميل

مع قائمة السياق والخلفية جاهزة، الجزء الأخير هو عرض مكوّن GridJs وإرسال HTML/JS إلى المتصفح.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

في عرض Flask عادةً ما تقوم بـ:

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

عند تحميل الصفحة، يبني GridJs الجدول، يدمج قائمة السياق المخصصة، ويصبح معالج JavaScript الذي عرفناه جاهزًا للتنفيذ. انقر بزر الفأرة الأيمن على أي خلية، اختر **Export CSV**، وسترى المتصفح يحمل ملفًا يحمل اسم الورقة.

---

## مثال كامل يعمل (جميع الملفات)

فيما يلي الكود الكامل القابل للتنفيذ يمكنك نسخه‑لصقه في مجلد جديد. ثبّت Flask (`pip install flask`) وشغّل `python app.py`.

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


## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}