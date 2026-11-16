---
category: general
date: 2026-11-16
description: إنشاء تنسيق شرطي في Excel باستخدام Python. تعلم كيفية إضافة نطاق تنسيق
  شرطي، تمييز التواريخ، وإنشاء مصنف برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: ar
lastmod: 2026-11-16
og_description: إنشاء تنسيق شرطي في Excel باستخدام Python. يوضح هذا الدرس كيفية إضافة
  نطاق تنسيق شرطي، وتظليل التواريخ، وإنشاء مصنف.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: إنشاء تنسيق شرطي في إكسل باستخدام بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: كيفية إنشاء تنسيق شرطي في إكسل باستخدام بايثون
url: /ar/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء تنسيق شرطي في Excel باستخدام Python

إذا كنت بحاجة إلى **إنشاء تنسيق شرطي** في ملف Excel أثناء العمل بـ Python، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعلم **إنشاء دفتر عمل Excel باستخدام Python**‑style، وتحديد نطاق تنسيق، وتلوين التواريخ دون مغادرة بيئة التطوير المتكاملة.

يتيح لك التنسيق الشرطي تمييز الخلايا بصريًا التي تستوفي معايير محددة—مثالي للوحة التحكم، التقارير، أو أوراق التحقق من البيانات. بنهاية هذا الشرح ستحصل على دفتر عمل كامل الوظائف يلون الخلايا التي تاريخها “Yesterday” بالوردي بينما يبقى باقي النطاق أخضر.

## ما ستحققه

* إنشاء دفتر عمل جديد من الصفر.  
* إضافة مجموعة تنسيق شرطي لكتلة خلايا محددة.  
* تطبيق قاعدة **TIME_PERIOD** التي تبرز التواريخ (سيناريو “كيفية تلوين التواريخ”).  
* حفظ الملف كدفتر عمل XLSX جاهز للمعالجة اللاحقة.

**المتطلبات المسبقة**  
* Python 3.8+  
* حزمة `aspose-cells` للـ Python (`pip install aspose-cells`)  
* إلمام أساسي بوحدة `datetime` في Python  

---

## كيفية إنشاء تنسيق شرطي في Python

الخطوة الأولى هي إعداد دفتر العمل والورقة التي ستستضيف قواعد التنسيق.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**لماذا هذا مهم** – `Workbook` هو نقطة الدخول لجميع عمليات Excel. إنشاء دفتر العمل برمجيًا يستبدل خطوة “File → New” اليدوية، مما يتيح خطوط تقارير مؤتمتة.

---

## إعداد مجموعة التنسيق الشرطي – إضافة نطاق تنسيق شرطي

بعد ذلك نحدد كتلة الخلايا التي ستستقبل القاعدة. في هذا المثال النطاق هو **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**شرح** – `conditional_formattings.add` يسجل مجموعة جديدة مرتبطة بسلسلة العنوان. الشرط الأول (`conds[0]`) يعمل كنمط “افتراضي”؛ القاعدة اللاحقة ستتجاوزها عندما تتحقق معاييرها.

---

## إضافة قاعدة TIME_PERIOD – كيفية تلوين التواريخ

الآن نضيف المنطق الفعلي الذي يحدد تواريخ “Yesterday” ويصبغها بالوردي.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**لماذا نستخدم TIME_PERIOD؟** – توفر Aspose.Cells تعدادًا مدمجًا مثل `YESTERDAY`، `TODAY`، و`LAST_WEEK`. تقوم هذه القيم بتقييم قيمة تاريخ الخلية مقابل تاريخ النظام الحالي، مما يلغي الحاجة إلى صيغ مخصصة.

---

## تعبئة بيانات عينة – توضيح القاعدة

لرؤية التنسيق قيد التنفيذ نُدخل تاريخًا يطابق القاعدة وآخر لا يطابقها.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**ملاحظة حالة الحافة** – قاعدة `TIME_PERIOD` تعمل فقط مع تواريخ *حقيقية*. إذا احتوت الخلية على نص (مثال: “N/A”) يتم تجاهل القاعدة، مما يمنع تغيّر الألوان غير المتوقع.

---

## حفظ دفتر العمل – إضافة تنسيق شرطي python

أخيرًا، نكتب دفتر العمل إلى القرص. يمكن فتح الملف في أي برنامج جداول لتأكيد الألوان.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**النتيجة المتوقعة**  

| I19 (أخضر → وردي) | J19 (أخضر) | K19 (أخضر) |
|--------------------|------------|------------|
| 7/30/2008 (أمس) | – | – |
| **I20**: تسمية “Yesterday” | – | – |
| I21‑K21 (أخضر) | – | – |

تظهر الخلية **I19** بخلفية وردية لأن تاريخها يطابق فترة “Yesterday”، بينما تظل **K20** خضراء.

---

## أسئلة شائعة ونصائح عملية

* **هل يمكنني استخدام نطاق تاريخ مخصص بدلاً من فترة مدمجة؟**  
  نعم. استبدل `condition.time_period` بـ `condition.formula1 = "TODAY()-1"` واضبط `condition.type = FormatConditionType.FORMULA`.

* **ماذا لو كان دفتر العمل يحتوي بالفعل على بيانات؟**  
  استخدم `worksheet.cells.import_data` لتحميل البيانات دفعة واحدة قبل إضافة مجموعة التنسيق الشرطي.

* **الأداء مع الأوراق الكبيرة؟**  
  إضافة العديد من القواعد قد يبطئ عملية العرض. اجمع الخلايا التي تشترك في نفس القاعدة في نطاق واحد (مثال: “A1:C1000”) لتقليل عدد القواعد.

* **التوافق عبر الأنظمة؟**  
  ملف XLSX المُولد يتبع معيار Office Open XML، لذا يعمل على تطبيقات الجداول في Windows وmacOS وLinux.

---

## الخلاصة

أنت الآن تعرف **كيفية إنشاء تنسيق شرطي** في دفتر عمل Excel باستخدام Python. غطى الشرح إنشاء دفتر العمل، تعريف **نطاق إضافة تنسيق شرطي**، تطبيق قاعدة **كيفية تلوين التواريخ**، وحفظ الملف—كل ذلك باستخدام نهج **add conditional formatting python** الذي توفره Aspose.Cells.

من هنا يمكنك:

* توسيع مجموعة القواعد بقيم `TimePeriodType` أخرى (مثل `TODAY`، `LAST_MONTH`).  
* دمج شروط متعددة على نفس النطاق للحصول على مؤشرات بصرية أغنى.  
* دمج هذا التدفق في خطوط تقارير مؤتمتة أو خدمات ويب.

نتمنى لك برمجة سعيدة، ولا تتردد في تجربة ألوان ونطاقات ومنطق تواريخ مختلفة لتناسب احتياجات تقاريرك!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [إنشاء دفتر عمل Excel Python تنسيق شرطي للتاريخ](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [كيفية تطبيق تنسيق شرطي لفترة زمنية في Excel باستخدام Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [إنشاء دفتر عمل Excel Python – دليل كامل للتنسيق الشرطي والتصميم](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}