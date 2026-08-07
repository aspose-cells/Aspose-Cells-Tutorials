---
category: general
date: 2026-06-30
description: أضف قائمة سياق مخصصة إلى شبكة إكسل في بايثون واكتب قيمةً في خلية إكسل
  أثناء حفظ الملف المحدث. تعلّم كيفية إنشاء قائمة النقر بزر الفأرة الأيمن وتحديث قيمة
  الخلية بأسلوب بايثون.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: ar
og_description: إضافة قائمة سياق مخصصة في بايثون لكتابة قيمة في خلية إكسل وحفظ ملف
  الإكسل المحدث. يشرح هذا الدليل كيفية إنشاء قائمة النقر بزر الفأرة الأيمن باستخدام
  GridJs.
og_title: إضافة قائمة سياق مخصصة في بايثون – دليل خطوة بخطوة
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
title: إضافة قائمة سياق مخصصة في بايثون – دليل كامل
url: /ar/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة قائمة سياق مخصصة في Python – دليل كامل

هل تساءلت يومًا كيف **add custom context menu** عناصر إلى شبكة جدول بيانات تقوم بخدمتها من Python؟ ربما تحتاج إلى زر سريع “Mark as Reviewed” يظهر عندما ينقر المستخدم بزر الفأرة الأيمن على خلية، يكتب قيمة في خلية Excel، ثم يحفظ المصنف المحدث — كل ذلك دون مغادرة واجهة الويب.  

في هذا الدرس سنبني ذلك بالضبط: **custom right‑click menu** مدعوم من GridJs، معالج من جانب الخادم **write(s) value to excel cell**، وخطوة أخيرة **save(s) updated excel file** على القرص. في النهاية ستحصل على نمط قابل لإعادة الاستخدام يمكنك دمجه في أي مشروع Flask أو FastAPI أو Django.

> **لماذا يهم؟**  
> إضافة قائمة سياق مخصصة تُبسّط سير عمل مراجعة البيانات، وتقلل من النسخ واللصق اليدوي، وتمنح المستخدمين تجربة طبيعية داخل الشبكة. بالإضافة إلى ذلك، سترى كيفية **update cell value python**‑style، وهي مهارة أساسية لأي مهمة أتمتة Excel.

## المتطلبات المسبقة

- Python 3.9+ (الكود يعمل على 3.10 أيضًا)  
- `openpyxl` لمعالجة ملفات Excel  
- `gridjs` غلاف Python (أو مكتبة JS إذا كنت تفضّل الواجهة الأمامية)  
- إطار ويب أساسي (مثال Flask موضح)  
- ملف مصنف باسم `sample.xlsx` في مجلد المشروع الخاص بك  

إذا كنت تفتقد أيًا من هذه، نفّذ:

```bash
pip install openpyxl flask gridjs
```

## الخطوة 1 – إضافة قائمة سياق مخصصة: تهيئة GridJs وربط ورقة العمل

أول شيء تحتاج إلى القيام به هو إنشاء مثيل `GridJs` وتوجيهه إلى ورقة العمل التي تخطط للعمل معها. هنا تظهر عبارة **add custom context menu** لأول مرة في كودنا، وتُهيئ الساحة لكل شيء آخر.

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

**ما الذي يحدث؟**  
`grid.set_worksheet(ws)` يخبر GridJs باستخدام البيانات من `ws` كمصدر بياناته. من الآن فصاعدًا، أي تعديل في قائمة السياق نضيفه سيستهدف تلقائيًا نفس ورقة العمل، مما يحافظ على تزامن الواجهة والملف.

> **Pro tip:** حافظ على فتح المصنف في وضع القراءة/الكتابة مرة واحدة فقط. فتحه بشكل متكرر داخل معالج الطلب قد يسبب مشاكل قفل الملفات على Windows.

## الخطوة 2 – كتابة قيمة إلى خلية Excel: تعريف الإجراء لعنصر القائمة

الآن بعد أن أصبحت الشبكة جاهزة، نحتاج إلى **write value to excel cell** عندما يختار المستخدم الأمر المخصص لدينا. سنضيف إدخال قائمة يُسمّى “Mark as Reviewed” ونمنحه معرفًا `markReviewed`. المعرف هو ما سيرسله JavaScript على جانب العميل إلى الخادم.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**لماذا نستخدم معرفًا مخصصًا؟**  
المعرف يفصل نص الواجهة عن منطق الخادم، مما يسمح لك بتغيير التسمية دون تعديل كود الخلفية. كما يجعل عملية **create right‑click menu** واضحة وقابلة لإعادة الاستخدام.

## الخطوة 3 – إنشاء قائمة النقر الأيمن: تسجيل معالج الخادم

مع وجود عنصر القائمة، نحتاج إلى إخبار GridJs بما يجب فعله عندما ينقر المستخدم عليه. هنا نُطبق وظيفة **create right‑click menu** التي تُرسل طلبًا فعليًا إلى Python.

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

بعض النقاط التي يجب ملاحظتها:

1. **`ws[cell_address] = "Reviewed"`** هي أبسط طريقة لـ **update cell value python**. تحت الغطاء، `openpyxl` يترجم عنوان النمط A1 إلى مؤشرات الصف/العمود.
2. المعالج يُعيد حمولة JSON صغيرة. GridJs يتوقع مؤشر حالة؛ يمكنك توسيعه لتضمين رسائل خطأ إذا لزم الأمر.

نربط الآن المعرف بالمعالج:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**ماذا لو كانت الخلية فارغة أو محمية؟**  
- الخلايا الفارغة لا مشكلة—`openpyxl` سيُنشئها تلقائيًا.  
- بالنسبة للأوراق المحمية، ستحتاج إلى إلغاء الحماية أولاً (`ws.protection.sheet = False`) أو التقاط `PermissionError`.

## الخطوة 4 – تحديث قيمة الخلية في Python: حفظ التغيير عن طريق حفظ المصنف

كتابة القيمة هي نصف القصة فقط؛ يجب عليك **save updated excel file** حتى يبقى التغيير بعد انتهاء الجلسة الحالية. هنا نُكمل الرحلة من الواجهة إلى القرص.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**لماذا مجلد منفصل؟**  
الحفظ في دليل `output/` يحافظ على القالب الأصلي دون تعديل، وهو مفيد لتتبع التدقيق. عدّل المسار ليتناسب مع بيئة النشر الخاصة بك.

> **Watch out:** إذا كنت تخدم العديد من المستخدمين المتزامنين، فكر في استخدام قفل آمن للثريد (`threading.Lock`) حول `wb.save()` لتجنب حالات السباق.

## الخطوة 5 – إنشاء JSON لتكوين العميل وربط كل شيء معًا

أخيرًا، نحتاج إلى إنتاج JSON الذي سيستهلكه مثال GridJs على الواجهة الأمامية. يحتوي هذا الـ JSON على بيانات ورقة العمل **و** تعريف القائمة المخصصة.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

عند تضمين `config_json` في صفحة HTML الخاصة بك، سيقوم GridJs بعرض الشبكة مع إدخال “Mark as Reviewed” القابل للنقر بزر الفأرة الأيمن على كل خلية.

### مثال كامل باستخدام Flask

فيما يلي تطبيق Flask بسيط يجمع جميع الأجزاء معًا. شغّله، افتح `http://localhost:5000` وانقر بزر الفأرة الأيمن على أي خلية لرؤية القائمة المخصصة تعمل.

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

**النتيجة المتوقعة:**  
- انقر بزر الفأرة الأيمن على أي خلية → يظهر “Mark as Reviewed”.  
- انقر عليه → يتغير محتوى الخلية إلى “Reviewed”.  
- المصنف `output/sample-updated.xlsx` الآن يحتوي على القيمة الجديدة.

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو احتجت إلى إجراءات مخصصة متعددة؟* | فقط أضف المزيد من الكائنات إلى `grid.settings.context_menu.custom_items` وسجّل كل واحد بمعرفه الخاص. |
| *هل يمكنني تمرير بيانات إضافية (مثل معرف الصف) إلى المعالج؟* | نعم. أدرج مفاتيح إضافية في حمولة JSON على جانب العميل، ثم اقرأها من `request` في `on_custom_command`. |
| *هل هذا النهج متوافق مع أطر العمل غير المتزامنة؟* | بالتأكيد — فقط اجعل `on_custom_command` دالة async واستخدم `await wb.save(...)` إذا انتقلت إلى `aiofiles` أو ما شابه. |
| *كيف يمكنني تنسيق أيقونة القائمة؟* | قدّم أي اسم من Material‑Icons (`"icon": "edit"`). الواجهة الأمامية تقوم بتحميل خط الأيقونة تلقائيًا. |
| *ماذا عن المصنفات الكبيرة؟* | حمّل فقط الورقة المطلوبة، وفكّر في تدفق الصفوف باستخدام `openpyxl.iter_rows()` للحفاظ على استهلاك الذاكرة. |

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [الحفاظ على بادئة الاقتباس المفرد لقيمة الخلية أو النطاق في Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [الحفاظ على بادئة الاقتباس المفرد لقيمة الخلية أو النطاق في Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [الحفاظ على بادئة الاقتباس المفرد لقيمة الخلية أو النطاق في Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}