---
category: general
date: 2026-11-22
description: تعلم كيفية تقديم Excel في تطبيق ويب باستخدام Flask. يوضح هذا الدليل كيفية
  تحميل دفتر عمل Excel وعرضه على الويب باستخدام GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: ar
lastmod: 2026-11-22
og_description: كيفية تقديم ملفات Excel باستخدام Flask و GridJs. اتبع هذا الدرس الكامل
  لتحميل دفتر عمل Excel وعرضه على الويب.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: كيفية تقديم ملف Excel باستخدام Flask – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: كيفية تقديم ملفات Excel باستخدام Flask و GridJs
url: /ar/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تقديم ملفات Excel باستخدام Flask و GridJs

إذا كنت بحاجة إلى **how to serve excel** في تطبيق ويب Python، فإن هذا الدرس يوضح حلاً كاملاً. ستتعلم كيفية **load excel workbook** باستخدام مكتبة `cells`، وتعريضها عبر نقطة نهاية Flask، وتمكين المستخدمين من **display excel web** باستخدام GridJs.

سنتنقل عبر كل سطر من الشيفرة، نشرح لماذا كل جزء مهم، ونزودك بمثال جاهز للتنفيذ. بنهاية الدليل يمكنك تضمين أي ملف `.xlsx` في شبكة استجابة على جانب العميل دون كتابة محللات بيانات JavaScript مخصصة.

## المتطلبات المسبقة

- تم تثبيت Python 3.9+  
- حزم `flask` و `cells` (`pip install flask cells`)  
- ملف Excel تجريبي (مثال: `sample.xlsx`) في دليل معروف  

لا يلزم أي إطار عمل للواجهة الأمامية؛ GridJs يتعامل مع واجهة المستخدم تلقائيًا.

## نظرة عامة على الحل

الفكرة الأساسية بسيطة:

1. **Load** ملف Excel على الخادم.  
2. **Create** `GridJsHandler` الذي يترجم بيانات ورقة العمل إلى صيغة JSON التي يتوقعها GridJs.  
3. **Expose** مسار Flask الذي يُعيد عرض JSON ويقبل التعديلات من العميل.  
4. **Run** خادم Flask حتى يتمكن المتصفح من جلب البيانات وعرض الشبكة.  

الآن لنقم بتنفيذ كل خطوة.

## كيفية تقديم Excel باستخدام Flask و GridJs

### الخطوة 1: تحميل ملف Excel

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Why this matters:**  
`cells.Workbook` يحلل ملف `.xlsx` إلى تمثيل في الذاكرة. تحميل ملف العمل مرة واحدة عند بدء التشغيل يحافظ على سرعة الخادم لأن الطلبات اللاحقة تعيد استخدام نفس الكائن بدلاً من الوصول إلى نظام الملفات بشكل متكرر.

### الخطوة 2: إنشاء معالج GridJs على جانب الخادم

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Why this matters:**  
`GridJsHandler` يُجرد عملية التحويل من صفوف/أعمدة Excel إلى مخطط JSON الذي يستهلكه GridJs. كما يتتبع التعديلات على جانب العميل، مما يتيح لك حفظ التغييرات مرة أخرى إلى ملف العمل لاحقًا إذا لزم الأمر.

### الخطوة 3: تمكين الميزات الاختيارية (التحميل الكسول)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Why this matters:**  
عندما تحتوي ورقة العمل على آلاف الصفوف، إرسال مجموعة البيانات بالكامل مرة واحدة قد يثقل المتصفح. التحميل الكسول يبث البيانات صفحة بصفحة، محسنًا الأداء لسيناريو **display excel web**.

### الخطوة 4: إعداد تطبيق Flask بسيط

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Why this matters:**  
Flask يوفر خادم HTTP خفيف الوزن يمكنه تقديم نقاط نهاية JSON والملفات الثابتة. الحفاظ على تطبيق Flask بسيط يقلل من سطح الهجوم ويجعل المثال سهل التكيف.

### الخطوة 5: تعريف نقطة نهاية GridJs

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Why this matters:**  

- **GET** – المتصفح يجلب عرض ورقة العمل الأولي.  
- **POST** – عندما يقوم المستخدم بتحرير خلية، يرسل GridJs حمولة JSON؛ `apply_changes` يدمج تلك التعديلات مرة أخرى في الحالة الداخلية للمعالج.  

إرجاع `grid_handler.get_view()` يضمن أن العميل يتلقى دائمًا أحدث البيانات، وهو أمر أساسي لتجربة **display excel web** سلسة.

### الخطوة 6: تشغيل خادم Flask

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Why this matters:**  
تشغيل على المنفذ 5000 هو الإعداد الافتراضي لـ Flask، مما يجعل الاختبار محليًا سهلًا (`http://localhost:5000/gridjs`). في بيئة الإنتاج ستضع Flask خلف خادم WSGI (مثل Gunicorn) وربما تفعيل HTTPS.

## النتيجة المتوقعة بصيغة JSON

عند الانتقال إلى `http://localhost:5000/gridjs` باستخدام طلب GET، يكون الرد كما يلي:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs يستهلك هذه الحزمة تلقائيًا، ويعرض جدولًا قابلًا للبحث والفرز في المتصفح.

## مثال كامل قابل للتنفيذ

فيما يلي السكريبت الكامل الذي يمكنك نسخه إلى `app.py` وتنفيذه:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

شغّل السكريبت باستخدام:

```bash
python app.py
```

افتح المتصفح ووجهه إلى صفحة HTML بسيطة تقوم بتحميل GridJs (انظر وثائق GridJs للحصول على وسم `<script>`). ستعرض الشبكة محتوى Excel فورًا.

## التغييرات الشائعة والحالات الخاصة

| الحالة | كيفية التكيف |
|-----------|--------------|
| **Multiple worksheets** | إنشاء `GridJsHandler` منفصل لكل ورقة وتعريض نقاط نهاية مميزة (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **Large files (>10 MB)** | زيادة حد حجم طلب Flask (`app.config['MAX_CONTENT_LENGTH']`) وإبقاء `lazy_load` مفعلاً. |
| **Persisting edits back to the file** | بعد `apply_changes`، استدعِ `workbook.save("output.xlsx")` لكتابة التغييرات إلى القرص. |
| **Authentication** | غلف نقطة النهاية بـ Flask‑Login أو فحص رمز API قبل إرجاع البيانات. |
| **CORS for external front‑ends** | أضف `from flask_cors import CORS; CORS(app)` للسماح بطلبات عبر الأصل. |

هذه التعديلات تتيح لك توسيع عملية **load excel workbook** لتناسب أحمال الإنتاج.

## نصائح احترافية

- **Cache the JSON view** إذا كان ملف العمل نادرًا ما يتغير؛ استخدم `functools.lru_cache` حول `grid_handler.get_view()` لتقليل عبء التسلسل.  
- **Validate incoming edits** (`request.json`) لمنع البيانات غير الصالحة من إفساد ملف العمل.  
- عند الخدمة عبر HTTPS، اضبط `app.run(ssl_context=('cert.pem', 'key.pem'))` لتشفير المرور.

## الخلاصة

أنت الآن تعرف **how to serve excel** ملفات باستخدام Flask و GridJs، من تحميل ملف العمل إلى إرجاع عرض JSON يمكن للمتصفح عرضه. يغطي المثال دورة الحياة الكاملة: **load excel workbook**، تمكين التحميل الكسول، تعريض نقطة نهاية REST، وتشغيل خادم جاهز للإنتاج.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **display excel web** في واجهة React، أو قم بتمديد المعالج لـ **load excel workbook** من تخزين سحابي (مثل AWS S3). جرّب تنسيق أعمدة GridJs، إضافة ترقيم الصفحات، أو حفظ تعديلات المستخدمين مرة أخرى إلى جدول البيانات الأصلي.

برمجة سعيدة، واستمتع بتحويل ملفات Excel الثابتة إلى جداول ويب تفاعلية!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}