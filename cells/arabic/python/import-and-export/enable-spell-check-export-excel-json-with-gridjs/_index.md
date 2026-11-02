---
category: general
date: 2026-06-21
description: فعّل تدقيق الإملاء أثناء تصدير JSON من Excel باستخدام GridJs. تعلّم تحويل
  ملفات xlsx إلى JSON، وضبط التحميل الكسول، وتحميل دفتر عمل Excel بكفاءة.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: ar
og_description: تمكين التدقيق الإملائي أثناء تصدير JSON من Excel باستخدام GridJs.
  يوضح هذا الدليل كيفية تحويل ملف xlsx إلى JSON، وتكوين التحميل الكسول، وتحميل دفتر
  عمل Excel.
og_title: تمكين التدقيق الإملائي وتصدير Excel JSON باستخدام GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: تفعيل التدقيق الإملائي وتصدير Excel JSON باستخدام GridJs
url: /ar/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تمكين تدقيق الإملاء وتصدير Excel JSON باستخدام GridJs

هل احتجت يومًا إلى **تمكين تدقيق الإملاء** في واجهة جدول بيانات ويب وتساءلت كيف تحصل على البيانات بصيغة JSON في الوقت نفسه؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عندما يحاولون **تصدير Excel JSON** من مصنف مع الحفاظ على ميزات متقدمة مثل التحقق من الصيغ.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلاً للتنفيذ يوضح لك كيفية **تحميل مصنف Excel**، تحويله إلى حمولة JSON باستخدام GridJs، **تكوين التحميل الكسول**، وبالطبع **تمكين تدقيق الإملاء**. بنهاية الدرس ستتمكن من **تحويل xlsx إلى JSON** ببضع أسطر فقط—بدون غموض ولا قطع مفقودة.

> **ما ستحصل عليه**  
> * سكريبت بايثون يقرأ ملف `.xlsx`، ينشئ كائن خادم GridJs، ويكتب `grid_data.json`.  
> * فهم لماذا كل خيار مهم (تدقيق الإملاء، تدقيق الصيغ، التحميل الكسول).  
> * نصائح لتوسيع الحل إلى مصنفات أكبر.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.9+ | مطلوب لحزمة `cells` المستخدمة أدناه. |
| مكتبة `cells` (`pip install cells`) | توفر فئتي `Workbook` و `GridJs`. |
| ملف Excel تجريبي (`sample.xlsx`) | هذا هو المصدر الذي سنـ **نحمّل منه مصنف Excel**. |
| صلاحية كتابة إلى مجلد الإخراج | ضروري لخطوة `grid.save()`. |

إذا كان أي من هذه غير مألوف لك، توقف وقم بتثبيتها أولًا—وإلا سيثير السكريبت خطأ استيراد.

---

## الخطوة 1: تحميل مصنف Excel

أول شيء تقوم به عندما تريد **تحويل xlsx إلى json** هو فتح المصنف. فكر فيها كفتح الباب قبل أن تتمكن من تزيين الغرفة.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **نصيحة احترافية:** إذا كان ملفك ضخمًا، فكر في استخدام `cells.Workbook(..., read_only=True)` لتقليل استهلاك الذاكرة.

---

## الخطوة 2: إنشاء كائن خادم GridJs

الآن بعد أن أصبح المصنف في الذاكرة، نحتاج إلى كائن **GridJs** سيترجم الأوراق إلى JSON يمكن لواجهة العميل استهلاكها.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

متغيّر `grid` هو في الأساس غلاف رقيق حول المصنف يعرف كيف يَسلسل الخلايا، الصيغ، وحتى معلومات التنسيق.

---

## الخطوة 3: تمكين تدقيق الإملاء (وتدقيق الصيغ)

هنا يبرز الكلمة المفتاحية الأساسية. عبر تبديل علم `enableSpellCheck`، تمنح المستخدمين النهائيين شبكة أمان ضد الأخطاء المطبعية—تمامًا كما في Excel لسطح المكتب.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

لماذا تمكين كلاهما؟ تدقيق الإملاء يلتقط الأخطاء النصية، بينما تدقيق الصيغ يحمي من الحسابات المكسورة. معًا يجعل واجهة الويب تبدو مصقولة كالتجربة الأصلية في Excel.

---

## الخطوة 4: تكوين التحميل الكسول

إذا كنت تتعامل مع آلاف الصفوف، فإن إرسال مجموعة البيانات بالكامل في حمولة واحدة سيُثقل المتصفح. **قم بتكوين التحميل الكسول** لإرسال البيانات على دفعات صغيرة (500 صف لكل طلب في مثالنا).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

يمكنك تعديل `pageSize` بناءً على ظروف الشبكة. الصفحات الأصغر تعني المزيد من الطلبات ولكن واجهة أكثر سلاسة؛ الصفحات الأكبر تقلل عدد الطلبات لكن قد تتسبب في تأخير.

---

## الخطوة 5: تصدير Excel JSON

كل الأعمال الثقيلة الآن خلف الكواليس. الخطوة الأخيرة هي **تصدير excel json** إلى ملف يمكن للواجهة الأمامية طلبه.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

عند انتهاء طريقة `save`، ستحصل على ملف `grid_data.json` منظم يحتوي على:

* أسماء الأوراق ومعرفاتها  
* بيانات الصفوف (القيم، الصيغ، والتنسيق)  
* بيانات التعريف حول الميزات المفعلة (تدقيق الإملاء، التحميل الكسول، إلخ)

يمكنك التحقق من المخرجات بفتح الملف في محرر نصوص أو بتحميله في وحدة تحكم المتصفح:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

هذا هو **حل كامل ومستقل** لتحويل ملف Excel إلى حمولة JSON مع الحفاظ على تدقيق الإملاء فعالًا.

---

## البرنامج الكامل – جمع كل الأجزاء معًا

فيما يلي البرنامج الكامل الذي يمكنك نسخه، تعديل المسارات، وتشغيله. لا خطوات مخفية، لا سكريبتات خارجية—ملف واحد فقط.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

احفظه باسم `export_gridjs.py` وشغّله:

```bash
python export_gridjs.py
```

سترى سلسلة من رسائل `[✓]` تؤكد نجاح كل خطوة.

---

## أسئلة شائعة وحالات حافة

**ماذا لو كان مصنف Excel يحتوي على عدة أوراق؟**  
يقوم GridJs تلقائيًا بالتكرار على كل ورقة، لذا سيحتوي الـ JSON الناتج على مصفوفة `sheets`. يمكنك التصفية على جانب العميل إذا كنت تحتاج فقط إلى جزء منها.

**هل يمكنني تعطيل تدقيق الإملاء لورقة معينة؟**  
قاموس `options` يُطبق عالميًا. لتبديل الإعداد لورقة محددة تحتاج إلى إنشاء كائنات `GridJs` منفصلة أو معالجة الـ JSON بعد الإنشاء.

**ملفي أكبر من 10 ميغابايت—هل سيظل التحميل الكسول مفيدًا؟**  
بالتأكيد. يعمل التحميل الكسول على مستوى الـ API؛ الخادم يبث فقط الصفحة المطلوبة. ومع ذلك، قد ترغب في زيادة `pageSize` إلى 1000 إذا كانت زمنية استجابة الشبكة منخفضة.

**هل يجب أن أقلق بشأن أحرف Unicode؟**  
تتعامل مكتبة `cells` مع UTF‑8 مباشرة، لذا الأحرف مثل الإيموجي أو النصوص غير اللاتينية تمر عبر العملية دون مشاكل.

---

## نصائح احترافية للإنتاج

* **قم بتخزين الـ JSON مؤقتًا** – إذا كان المصنف نادرًا ما يتغير، خزن `grid_data.json` في CDN لتحميل فائق السرعة.  
* **الأمان** – لا تكشف أبدًا عن ملف Excel الأصلي؛ قدم فقط الـ JSON المُولد.  
* **الإصدار** – أدرج رقم إصدار في اسم ملف الـ JSON (مثال: `grid_data_v2.json`) لتجنب البيانات القديمة بعد التحديثات.  
* **الاختبار** – اكتب اختبار وحدة صغير يحمل الـ JSON ويتحقق من أن `enableSpellCheck` هو `true`. يلتقط الانحدارات مبكرًا.

---

## الخلاصة

أصبح لديك الآن وصفة شاملة من البداية إلى النهاية **لتمكين تدقيق الإملاء** أثناء **تصدير Excel JSON** باستخدام GridJs. من **تحميل مصنف Excel** إلى **تكوين التحميل الكسول** وأخيرًا **تحويل xlsx إلى json**، العملية واضحة وجاهزة للإنتاج.  

ما الخطوات التالية؟ جرّب ربط `grid_data.json` المُولد بصفحة HTML بسيطة تستخدم مكتبة عميل GridJs، جرب مُعالج خلايا مخصص، أو أضف مصادقة حول نقطة النهاية التي تُعيد الـ JSON. السماء هي الحد عندما تجمع بين تدقيق الإملاء، التحميل الكسول، والتحويل السلس من Excel إلى JSON.

هل لديك أسئلة إضافية أو مصنف معقد تحاول التعامل معه؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!  

---

![تمكين تدقيق الإملاء في GridJs](/images/enable-spell-check-gridjs.png "لقطة شاشة تُظهر تمكين تدقيق الإملاء في واجهة GridJs UI")


## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [تصدير Excel إلى JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [استيراد بيانات JSON إلى Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [كيفية تصفية البيانات بفعالية أثناء تحميل مصنفات Excel باستخدام Aspose.Cells في Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}