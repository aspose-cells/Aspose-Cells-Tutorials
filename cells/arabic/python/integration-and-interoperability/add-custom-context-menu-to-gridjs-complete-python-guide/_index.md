---
category: general
date: 2026-06-30
description: أضف قائمة سياق مخصصة في GridJs وتعلم كيفية تحميل دفتر عمل Excel، وتحديث
  قيمة الخلية، وتمكين التدقيق الإملائي، وتسجيل أمر مخصص.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: ar
og_description: إضافة قائمة سياق مخصصة في GridJs أثناء تعلم تحميل دفتر عمل Excel،
  وتحديث قيمة الخلية، وتمكين التدقيق الإملائي، وتسجيل أمر مخصص.
og_title: إضافة قائمة سياق مخصصة إلى GridJs – دليل بايثون خطوة بخطوة
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
title: إضافة قائمة سياق مخصصة إلى GridJs – دليل بايثون الكامل
url: /ar/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة قائمة سياق مخصصة إلى GridJs – دليل Python كامل

هل تساءلت يومًا كيف **تضيف عناصر قائمة سياق مخصصة** إلى جدول GridJs مدعوم بملف Excel؟ لست وحدك. في العديد من التطبيقات التي تتعامل مع بيانات ضخمة تحتاج إلى قائمة النقر بزر الفأرة الأيمن لتسمح للمستخدمين بوضع علامة على الصفوف، أو تعليم العناصر كمراجعة، أو بدء إجراء على الخادم—دون مغادرة الشبكة.  

في هذا الدرس سنستعرض خطوة بخطوة كيفية تحميل ملف Excel، ربط عنصر قائمة سياق مخصص، تحديث قيمة خلية، تمكين التدقيق الإملائي، وتسجيل أمر مخصص يحفظ التغييرات مرة أخرى إلى الملف. في النهاية ستحصل على نسخة GridJs تعمل بالكامل وتبدو طبيعية للمستخدمين وتكتب مباشرةً إلى جدول البيانات الأصلي.

## المتطلبات المسبقة

- Python 3.9+ (الكود يستخدم تلميحات الأنواع لكنه يعمل على أي نسخة حديثة)  
- مكتبة `cells` (أو أي غلاف للتعامل مع Excel يوفر كائنات `Workbook` و `Worksheet`)  
- ربط Python لـ `gridjs` (نموذج الكائن يعكس واجهة JavaScript API)  
- فهم أساسي للـ lambdas وهياكل JSON  

إذا كان لديك هذه المتطلبات، لنبدأ.

## الخطوة 1: تحميل ملف Excel واختيار ورقة العمل

أول شيء يجب القيام به هو **تحميل ملف Excel** حتى يتوفر ل‑GridJs البيانات للعرض. فئة `cells.Workbook` تُجرد عمليات الإدخال‑الإخراج للملف وتمنحك وصولًا مباشرًا إلى الصفوف، الأعمدة، والخلايا الفردية.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **لماذا هذا مهم:** تحميل المصنف مسبقًا يعني أن الشبكة يمكنها سحب البيانات عند الطلب، وأي تعديل تجريه لاحقًا (مثل **تحديث قيمة الخلية**) سيُحفظ في نفس الملف.

## الخطوة 2: إنشاء كائن GridJs وربطه بورقة العمل

الآن نقوم بإنشاء كائن `gridjs.GridJs` ونخبره أي ورقة عمل يجب عرضها. فكر في هذا كإعطاء GridJs مصدر بيانات حي يمكنه الاستعلام عنه كلما احتاج إلى رسم صفحة أو جزء محمَّل بشكل كسول.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **نصيحة احترافية:** إذا كنت تتعامل مع عدة أوراق، ما عليك سوى استدعاء `grid.set_worksheet(other_ws)` لاحقًا—دون الحاجة لإعادة إنشاء الشبكة.

## الخطوة 3: تمكين التدقيق الإملائي (وميزات أخرى مفيدة)

معظم تطبيقات الأعمال تسمح للمستخدمين بكتابة ملاحظات حرة. تمكين **التدقيق الإملائي** يقلل الأخطاء المطبعية ويحسن جودة البيانات. GridJs يوفر علمًا بسيطًا لهذا الغرض.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **لماذا نُفعِّل التدقيق الإملائي؟** يعمل على جانب العميل، مما يمنح رد فعل فوري دون استدعاءات إضافية إلى الخادم—مثالي للجداول الكبيرة.

## الخطوة 4: إضافة عنصر قائمة سياق مخصص

هذا هو جوهر الدرس: **إضافة عناصر قائمة سياق مخصصة**. سننشئ خيارًا “Mark as Reviewed” (تمييز كمراجعة) الذي، عند النقر، ينفّذ أمرًا على الخادم سنعرّفه لاحقًا.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **صورة توضيحية**  
> ![Add Custom Context Menu screenshot showing right‑click options](/images/add-custom-context-menu.png "Add Custom Context Menu example")

النص البديل أعلاه يحتوي على الكلمة المفتاحية الأساسية، لتلبية متطلبات تحسين محركات البحث.

## الخطوة 5: تسجيل أمر مخصص لتحديث قيمة الخلية

عند اختيار المستخدم “Mark as Reviewed”، نحتاج إلى **تسجيل أمر مخصص** يُحدّث خلية Excel الأساسية ويحفظ الملف. طريقة `grid.register_custom_command` تربط دالة Python بالمعرف الذي حددناه مسبقًا.

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

> **لماذا يعمل هذا:** المتعامل يستقبل مرجع الخلية من العميل، يستخدم واجهة `Worksheet` **لتحديث قيمة الخلية**، ثم يكتب المصنف بالكامل إلى القرص. الاستجابة تُخبر الواجهة الأمامية بأن العملية نجحت.

### معالجة الحالات الطرفية

- **غياب مرجع الخلية:** إذا كان `req` لا يحتوي على `"cell"`، ارفع خطأ واضح حتى يتمكن الواجهة من عرض إشعار.  
- **التعديلات المتزامنة:** في سيناريوهات الزيارات العالية، فكر في قفل المصنف أو استخدام طابع نسخة لتجنب ظروف السباق.

## الخطوة 6: تمكين التحميل الكسول للأوراق الكبيرة

إذا كنت تتعامل مع آلاف الصفوف، فإن التحميل الكسول يحافظ على استجابة الواجهة. عيّن حجم الصفحة إلى جزء معقول—500 صف يعمل جيدًا لمعظم المتصفحات.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **ماذا لو كان لديك 10 000 صف؟** ستطلب الشبكة البيانات صفحةً بصفحة، مما يقلل الضغط على الذاكرة في كل من العميل والخادم.

## الخطوة 7: (اختياري) إضافة نافذة منبثقة مخصصة لتحرير الصفوف

أحيانًا تحتاج إلى واجهة أغنى من المحرر المدمج. GridJs يتيح لك فتح نافذة منبثقة يمكنك استضافتها في أي مكان—ربما مكوّن React أو نموذج HTML بسيط.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **لماذا نستخدم نافذة منبثقة؟** تعزل منطق التحقق المعقّد وتمنحك تحكمًا كاملاً في التخطيط، مع إمكانية استدعائها من الشبكة.

## الخطوة 8: استرجاع تكوين JSON للعميل

أخيرًا، تحتاج إلى إرسال التكوين إلى المتصفح. طريقة `get_client_config` تسلسل كل شيء إلى كائن JSON يمكن لمكتبة GridJs على الواجهة الأمامية استهلاكه.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

الناتج يبدو تقريبًا هكذا (مقتطع للوضوح):

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

### النتيجة المتوقعة

- النقر بزر الفأرة الأيمن على أي خلية يفتح قائمة بها **Mark as Reviewed**.  
- اختيارها يرسل طلبًا إلى الخادم، الذي **يحدّث قيمة الخلية** إلى “Reviewed” ويحفظ `example‑updated.xlsx`.  
- التدقيق الإملائي يبرز الكلمات غير الصحيحة أثناء الكتابة.  

كل هذا يحدث دون تحديث كامل للصفحة، بفضل التحميل الكسول وحمولة JSON الخفيفة.

## أسئلة شائعة ونصائح احترافية

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان المصنف للقراءة فقط؟* | تأكد من أن أذونات الملف تسمح بالكتابة، أو افتح المصنف بـ `mode="rw"` إذا كانت المكتبة تدعم ذلك. |
| *هل يمكن إضافة أكثر من عنصر قائمة مخصص؟* | بالتأكيد—فقط أضف قواميس إضافية إلى `grid.settings.context_menu.custom_items`. |
| *هل أحتاج إلى إعادة تحميل الشبكة بعد تحديث خلية؟* | GridJs يحدّث الصف المتأثر تلقائيًا إذا أرجعت `{status:"ok"}`؛ وإلا استدعِ `grid.refresh()` من العميل. |
| *كيف أجعل التدقيق الإملائي مخصصًا للغة؟* | عيّن `grid.settings.spell_check.language = "en-US"` (أو أي لغة مدعومة). |
| *هل التحميل الكسول متوافق مع التصفية على الخادم؟* | نعم—اجمع `grid.settings.filter.enabled = True` ونفّذ منطق التصفية في الأمر المخصص الخاص بك. |

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي سكريبت واحد يمكنك وضعه في مسار Flask أو تشغيله كعملية مستقلة. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على خادمك.

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


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}