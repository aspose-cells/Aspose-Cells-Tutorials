---
category: general
date: 2026-09-15
description: تعلم كيفية تطبيق تنسيق الشرط للفترات الزمنية وحفظ المصنف كملف XLSX باستخدام
  Aspose.Cells في بايثون. يتضمن كودًا خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: ar
lastmod: 2026-09-15
og_description: تطبيق تنسيق شرطي للفترات الزمنية في Excel باستخدام Python وحفظ المصنف
  كملف XLSX. اتبع هذا الدليل الكامل لـ Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: تطبيق تنسيق شرطي لفترات الزمن في Excel باستخدام Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: كيفية تطبيق تنسيق شرطي للفترات الزمنية في إكسل باستخدام بايثون
url: /ar/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تطبيق تنسيق شرطي لفترة زمنية في Excel باستخدام Python

إذا كنت بحاجة إلى **تنسيق شرطي لفترة زمنية** في ملف Excel، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Python. ستشاهد مثالًا كاملاً وقابلًا للتنفيذ ينشئ مصنفًا، يبرز تواريخ الأمس، و**يحفظ المصنف بصيغة XLSX** في بضع أسطر من الشيفرة فقط.

التنسيق الشرطي طريقة قوية لجذب الانتباه إلى البيانات التي تفي بقاعدة معينة. في هذا الدليل نركز على فترة “Yesterday” (الأمس)، لكن النمط نفسه يعمل مع فترات مدمجة أخرى مثل Today (اليوم)، LastWeek (الأسبوع الماضي)، وNextMonth (الشهر القادم). بنهاية الدليل ستكون قادرًا على **إنشاء سكريبتات python لإنشاء مصنف Excel** جاهزة للإنتاج.

## المتطلبات المسبقة

- تثبيت Python 3.8+  
- حزم `aspose-cells` و `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- إلمام أساسي بصياغة Python  

لا يلزم تثبيت Office إضافي لأن Aspose.Cells يتولى توليد الملف داخليًا.

## تنسيق شرطي لفترة زمنية باستخدام Aspose.Cells في Python

هذا القسم يشرح كل سطر من الشيفرة اللازمة للمهمة الأساسية. كتلة الشيفرة أدناه هي السكريبت الكامل؛ التعليقات توضح هدف كل خطوة.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### لماذا كل خطوة مهمة

1. **إنشاء المصنف** يمنحك ملف Excel في الذاكرة يمكنك التلاعب به دون فتح Excel.  
2. **تحديد النطاق** (`I19:K20`) يخبر Aspose.Cells أين يُطبق القاعدة، مما يبقي المنطق معزولًا.  
3. **إضافة شرط TIME_PERIOD** يستخدم تعداد Aspose المدمج `TimePeriodType.YESTERDAY`. هذا يتجنب حسابات التاريخ اليدوية ويتحدث تلقائيًا عندما يُفتح الملف في يوم مختلف.  
4. **تعيين النمط** (`background_color` و `pattern`) يحدد كيف تظهر الخلايا المظللة. استخدام `Color.pink` يجعل القاعدة سهلة الرؤية.  
5. **كتابة تواريخ تجريبية** مع تنسيق الرقم 30 يضمن أن Excel يعرضها كتاريخ قصير بدلاً من أرقام متسلسلة.  
6. **ضبط عرض العمود تلقائيًا** يحسن قابلية القراءة لأي شخص يفتح الملف لاحقًا.  
7. **الحفظ بصيغة XLSX** ينتج ملفًا متوافقًا على نطاق واسع يمكن فتحه في Excel أو Google Sheets أو أي برنامج جداول حديث.

## كيفية إنشاء مصنف Excel بأسلوب Python باستخدام Aspose.Cells

السكريبت أعلاه يوضح بالفعل الخطوات الدنيا لـ **إنشاء مصنف Excel باستخدام Python**. عمليًا قد ترغب في:

- إضافة أوراق عمل متعددة (`workbook.worksheets.add("Report")`).  
- تعبئة جداول بيانات كبيرة باستخدام حلقات أو pandas DataFrames (`worksheet.cells.import_data_table`).  
- تطبيق تنسيقات إضافية (خطوط، حدود) باستخدام `cell.get_style()`.

جميع هذه الإجراءات تتبع نفس النمط: الحصول على الكائن، تعديل خصائصه، ثم استدعاء `set_style` أو `save`.

## إضافة تنسيق شرطي Python – أنماط مفيدة أخرى

إلى جانب مثال “Yesterday”، يدعم Aspose.Cells عدة أنواع من التنسيق الشرطي:

| FormatConditionType | حالة الاستخدام النموذجية |
|---------------------|--------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | صيغ مخصصة (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | مقارنات بسيطة (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | تدرجات ألوان |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | تمثيل شريط داخل الخلية |

لـ **إضافة تنسيق شرطي python** لحدّ عددي، ستستبدل `FormatConditionType.TIME_PERIOD` بـ `FormatConditionType.CELL_VALUE` وتحدد `condition.operator_type` و `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## حفظ المصنف بصيغة XLSX – أفضل الممارسات

عند **حفظ المصنف بصيغة xlsx**، ضع في الاعتبار:

- **تحديد `SaveFormat` الصحيح** (`SaveFormat.XLSX`) لتجنب الصيغ القديمة.  
- **استخدام اسم ملف حتمي** إذا كان السكريبت يُنفّذ في حلقة (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **إغلاق الموارد** (`workbook.dispose()`) في الخدمات طويلة التشغيل لتحرير الذاكرة الأصلية.

المثال يستخدم بالفعل `SaveFormat.XLSX`، مما ينتج مصنفًا حديثًا مضغوطًا يحتفظ بجميع قواعد التنسيق الشرطي.

## إبراز الأمس في Excel – خطوات التحقق

بعد تشغيل السكريبت، افتح `TimePeriodExample.xlsx`:

1. الخلايا `I19` و `K20` تحتوي على التواريخ `30‑07‑2008` و `03‑08‑2008`.  
2. الخلية `I20` تُظهر النص “Yesterday”.  
3. إذا غيرت تاريخ النظام إلى **30 يوليو 2008** وأعدت فتح الملف، ستُملأ الخلايا ذات التواريخ المطابقة باللون الوردي تلقائيًا.  
4. تغيير تاريخ النظام إلى أي يوم آخر يزيل التعبئة الورديّة، مؤكدًا أن القاعدة تتفاعل مع منطق **التنسيق الشرطي لفترة زمنية**.

## الأخطاء الشائعة وكيفية تجنّبها

- **غياب `aspose-pydrawing`** – فئة `Color` موجودة في هذه الحزمة؛ نسيان تثبيتها يسبب `ImportError`.  
- **تنسيق رقم غير صحيح** – استخدام التنسيق العام الافتراضي يُظهر أرقامًا متسلسلة (مثال: 39822). دائمًا عيّن `style.number = 30` للتواريخ القصيرة.  
- **عدم توافق النطاق** – يجب أن يشمل نطاق التنسيق الشرطي الخلايا التي تريد تظليلها؛ وإلا لن يكون للقاعدة أي تأثير.

## نصيحة احترافية: إعادة استخدام روتين التنسيق

إذا كنت تحتاج إلى قاعدة “Yesterday” نفسها في مصنفات متعددة، غلف المنطق في دالة مساعدة:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

استدعِ `apply_yesterday_highlight(worksheet, "A1:A10")` أينما احتجت.

## الخلاصة

أظهر لك هذا الدليل كيفية تنفيذ **تنسيق شرطي لفترة زمنية** في Excel باستخدام Python، وكيفية **حفظ المصنف بصيغة XLSX**، وكيفية **إبراز الأمس في Excel** باستخدام سكريبت واحد قابل لإعادة الاستخدام. الآن لديك أساس قوي لإضافة كود **add conditional formatting python** إلى أي مشروع أتمتة، سواءً كنت تُولّد تقارير يومية، تبني لوحات معلومات، أو تُعدّ تصديرات بيانات.

**الخطوات التالية**

- استكشف قيم `TimePeriodType` أخرى مثل `TODAY` أو `LAST_WEEK`.  
- اجمع بين قواعد شرطية متعددة على نفس النطاق للحصول على مؤشرات بصرية أغنى.  
- دمج توليد المصنف في خدمة ويب أو مهمة مجدولة.

برمجة سعيدة، واستمتع بالوضوح البصري الذي يضيفه التنسيق الشرطي إلى أتمتة Excel الخاصة بك!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}