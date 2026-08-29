---
category: general
date: 2026-07-03
description: دورة Aspose Cells GridJs توضح كيفية تصدير بيانات Excel إلى JSON وتصدير
  ورقة العمل إلى JSON بكفاءة باستخدام التحميل الكسول.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: ar
og_description: يشرح برنامج Aspose Cells GridJs كيفية تصدير بيانات Excel إلى JSON
  وتصدير ورقة العمل إلى JSON مع التحميل الكسول للمستندات الكبيرة.
og_title: دليل Aspose Cells GridJs – تصدير بيانات Excel إلى JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: دروس Aspose Cells GridJs – تصدير بيانات Excel إلى JSON مع التحميل الكسول
url: /ar/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل Aspose Cells GridJs – تصدير بيانات Excel بصيغة JSON مع التحميل الكسول

هل تساءلت يوماً كيف **تصدير بيانات Excel بصيغة JSON** من جدول بيانات ضخم دون إبطاء المتصفح؟ في هذا الدليل الخاص بـ Aspose Cells GridJs سنستعرض حلاً كاملاً جاهزاً للتنفيذ يتيح لك **تصدير ورقة العمل إلى JSON** باستخدام التحميل الكسول، بحيث يتم جلب الصفوف التي تحتاجها فقط عند الطلب.

إذا كنت تواجه صعوبة مع ملفات `.xlsx` الضخمة ويتجمد الجانب العميل، فأنت لست وحدك. الخبر السار؟ النهج الذي نطرحه هنا خفيف الوزن وقابل للتوسع، ويمكنك دمجه في أي مشروع Python يستخدم مكتبة Aspose.Cells بالفعل.

## ما يغطيه هذا الدليل

في الدقائق القليلة القادمة ستتعلم كيفية:

1. تحميل مصنف كبير باستخدام Aspose.Cells.
2. تفعيل التحميل الكسول في GridJs بحيث يرسل الخادم الصفوف على شكل قطع.
3. تصدير إعدادات GridJs إلى ملف JSON يمكن للواجهة الأمامية استهلاكه.
4. تعديل حجم القطعة لتحقيق أفضل أداء.
5. التحقق من النتيجة ودمجها مع صفحة HTML بسيطة.

لا توجد خدمات خارجية، ولا سحر مخفي—فقط Python نقي وواجهة Aspose.Cells API. في النهاية ستحصل على **خط أنابيب كامل لتصدير ورقة العمل إلى JSON** يمكنك تكييفه مع لوحات التحكم، أدوات التقارير، أو أي مكوّن شبكة بيانات.

### المتطلبات المسبقة

- Python 3.8+ مثبت محلياً.
- حزمة `asposecells` (يمكنك تنفيذ `pip install aspose-cells`).
- ملف Excel كبير (مثال: `large-data.xlsx`) موجود في دليل معروف.
- إلمام أساسي بـ Python ومفاهيم تطوير الويب.

إذا كان أي من هذه غير مألوف لك، لا تقلق—كل خطوة تتضمن شرحًا مختصرًا للـ “لماذا” لتفهم السبب وراء الكود.

---

## الخطوة 1: تثبيت واستيراد Aspose.Cells

أولاً، نحتاج إلى مكتبة Aspose.Cells. هي منتج تجاري، لكن النسخة التجريبية المجانية تكفي للتطوير.

```bash
pip install aspose-cells
```

الآن استورد الفئات الضرورية في سكريبتك.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **لماذا هذا مهم:** استيراد `Workbook` يمنحك الوصول إلى محرك عالي الأداء يقرأ ملفات Excel مباشرةً إلى الذاكرة، متجاوزاً النهج الأبطأ المستند إلى `openpyxl`.

## الخطوة 2: تحميل المصنف الذي يحتوي على مجموعة البيانات الكبيرة

بعد تجهيز المكتبة، وجهها إلى ملف Excel الخاص بك. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الملف.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **نصيحة احترافية:** إذا كان المصنف أكبر من بضع مئات من الميجابايت، فكر في زيادة حد ذاكرة عملية Python أو استخدام مفسّر 64‑bit لتجنب حدوث `MemoryError`.

## الخطوة 3: تفعيل التحميل الكسول في GridJs

GridJs هو مكوّن شبكة JavaScript من Aspose. التحميل الكسول يُخبر الخادم بإرسال جزء فقط من الصفوف—مثالي للجداول الضخمة.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **لماذا التحميل الكسول؟** بدون ذلك، سيتم تسلسل ورقة العمل بالكامل إلى JSON مرة واحدة، وهو ما قد يتجاوز حدود ذاكرة المتصفح بسهولة. بتعيين `LazyLoadingChunkSize` إلى 500، يحمل كل طلب حمولة يمكن التحكم فيها.

## الخطوة 4: تصدير إعدادات GridJs إلى JSON

الآن نطلب من Aspose إنتاج الـ JSON الذي يتوقعه مكوّن GridJs في الواجهة الأمامية. هذه هي جوهر عملية **export excel data json**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

طريقة `ExportGridJsJson` تُعيد كائن `bytes` يحتوي على تمثيل JSON لورقة العمل، جاهز للحفظ أو البث.

## الخطوة 5: كتابة الـ JSON إلى ملف (أو بثه)

لإجراء اختبار سريع، اكتب الـ JSON إلى القرص. في واجهة برمجة تطبيقات إنتاجية ستعيده مباشرةً من نقطة نهاية Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **ما ستراه:** فتح `lazygrid.json` سيظهر بنية تحتوي على `columns`، `rows`، وبيانات الترقيم. مصفوفة `rows` ستكون فارغة في البداية؛ سيطلب GridJs القطعة الأولى عند تحميل الصفحة.

## الخطوة 6: ربط الـ JSON بصفحة HTML بسيطة (اختياري)

إذا أردت رؤية الشبكة تعمل، أنشئ ملف HTML صغير يحمل GridJs من CDN ويشير إلى الـ JSON المُولد.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **لماذا نضيف هذا؟** يوضح الرحلة الكاملة: Python يُنشئ الـ JSON، المتصفح يجلبه، وGridJs يعرض البيانات قطعةً بقطعة. يمكنك الآن تجربة قيم مختلفة لـ `LazyLoadingChunkSize` للعثور على الإعداد المثالي لشبكتك.

## الخطوة 7: التحقق من النتيجة وحل المشكلات

شغّل سكريبت Python:

```bash
python export_lazy_grid.py
```

يجب أن تظهر رسالة النجاح وملف `lazygrid.json`. افتح ملف HTML في المتصفح؛ يجب أن تعرض الشبكة أول 500 صف فوراً، مع أدوات ترقيم لتحميل المزيد.

إذا ظهرت الشبكة فارغة:

- **تحقق من حجم ملف JSON** – ملف بحجم صفر بايت عادةً يعني أن مسار المصنف غير صحيح.
- **تأكد من تفعيل التحميل الكسول** – يجب أن تكون قيمة العلم `LazyLoading` هي `True`.
- **افحص وحدة تحكم المتصفح** – أي أخطاء CORS أو 404 تشير إلى أن الـ JSON لا يُقدَّم بشكل صحيح.

---

## تنويعات شائعة وحالات حافة

### تصدير ورقة عمل محددة

المثال أعلاه يستخدم دائمًا أول ورقة عمل (`Worksheets[0]`). لتصدير ورقة مختلفة، غير الفهرس أو استخدم اسم الورقة:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### تغيير حجم القطعة للملفات الضخمة

للملفات التي تحتوي على ملايين الصفوف، قد يكون حجم القطعة 500 لا يزال صغيرًا، مما يسبب العديد من الطلبات. يمكنك زيادته إلى 2000 أو أكثر، لكن تذكر أن القطع الأكبر تستهلك عرض نطاق أكبر لكل طلب.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### تصدير إلى تدفق بدلاً من ملف

إذا كانت واجهة برمجة التطبيقات تُعيد الـ JSON مباشرةً، فلا تحتاج إلى الكتابة على القرص:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### التعامل مع الصيغ والتنسيق

بشكل افتراضي، تشمل `ExportGridJsJson` القيم المحسوبة للصيغ. إذا كنت تحتاج الصيغ الأصلية، عيّن:

```python
grid_options.ExportFormulas = True
```

---

## الخلاصة

في هذا **دليل Aspose Cells GridJs** غطينا كل ما تحتاجه لتقوم بـ **export excel data json** و**export worksheet to JSON** باستخدام التحميل الكسول. من تثبيت Aspose.Cells، تفعيل التحميل الكسول، توليد الـ JSON، إلى ربطه بصفحة HTML بسيطة، لديك الآن نمط كامل يُمكنه التوسع بسلاسة مع جداول بيانات ضخمة.

جرّبه—عدّل حجم القطعة، جرّب أوراق عمل مختلفة، أو دمج النقطة النهاية في تطبيق Flask أو Django. الاحتمالات لا حصر لها، وفوائد الأداء فورية.

هل أنت مستعد للخطوة التالية؟ حاول إضافة فرز الأعمدة، مُعالج خلايا مخصص، أو حتى تصفية على مستوى الخادم لجعل شبكة GridJs تفاعلية حقًا. إذا واجهت أي صعوبة، اترك تعليقًا أدناه؛ برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استيراد بيانات JSON إلى Excel باستخدام Aspose.Cells Java&#58; دليل شامل](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [تحميل CSV وتصديره إلى JSON باستخدام Aspose.Cells لـ .NET&#58; دليل شامل](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [تصدير بيانات Excel باستخدام Aspose.Cells .NET&#58; دليل كامل لتصدير البيانات بسلاسة](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}