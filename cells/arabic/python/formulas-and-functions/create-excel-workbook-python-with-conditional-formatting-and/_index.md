---
category: general
date: 2026-10-04
description: إنشاء دفتر عمل Excel باستخدام بايثون و Aspose.Cells. تعلم تنسيق الخلايا
  الشرطي في Excel باستخدام بايثون، لون خلفية الخلية باستخدام بايثون، وتنسيق تاريخ
  الخلايا باستخدام بايثون في مثال كامل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: ar
lastmod: 2026-10-04
og_description: إنشاء ملف عمل Excel باستخدام بايثون مع Aspose.Cells. يوضح هذا الدليل
  تنسيق الخلايا الشرطي في Excel باستخدام بايثون، وتغيير لون خلفية الخلية باستخدام
  بايثون، وتنسيق تاريخ الخلايا باستخدام بايثون خطوة بخطوة.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: إنشاء ملف عمل Excel باستخدام بايثون – دليل كامل مع التنسيق الشرطي
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: إنشاء دفتر عمل إكسل باستخدام بايثون مع التنسيق الشرطي ولون خلفية الخلية
url: /ar/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel باستخدام Python مع التنسيق الشرطي ولون خلفية الخلية

إذا كنت بحاجة إلى **create Excel workbook python** بسرعة، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. سترى مثالًا كاملاً قابلاً للتنفيذ يضيف **excel conditional formatting python**، ويغيّر **cell background color python**، و**format cells date python** لتسليط الضوء على “Yesterday”.

في العديد من سيناريوهات التقارير، يُعد الإشارة البصرية للخلية الملونة وسيلة تجعل البيانات مفهومة على الفور. يمرّك هذا الشرح عبر كل سطر من الشيفرة، يوضح لماذا كل خطوة مهمة، ويعطيك برنامجًا جاهزًا للتنفيذ يمكنك تكييفه مع مشاريعك الخاصة.

## ما ستحققه

بنهاية هذه المقالة ستكون قادرًا على:

1. **create Excel workbook python** باستخدام مكتبة Aspose.Cells.  
2. تطبيق **excel conditional formatting python** الذي يبرز تلقائيًا التواريخ التي تقع على “Yesterday”.  
3. ضبط **cell background color python** إلى اللون الوردي (أو أي لون تفضله).  
4. **format cells date python** بحيث تظهر التواريخ بنمط التاريخ القياسي في Excel.  

لا تحتاج إلى خبرة سابقة مع Aspose.Cells—فقط بيئة Python 3 تعمل وإمكانية الوصول إلى pip.

## المتطلبات المسبقة

- تثبيت Python 3.8 أو أحدث.  
- تثبيت الحزم `aspose-cells` و `aspose-pydrawing` عبر `pip install aspose-cells aspose-pydrawing`.  
- إلمام أساسي بصياغة Python ومفاهيم Excel (المصنفات، الأوراق، الخلايا).  

> **نصيحة احترافية:** إذا شغّلت البرنامج في بيئة افتراضية، فإنك تتجنب تعارض الإصدارات مع مشاريع أخرى.

## الخطوة 1: إعداد المشروع واستيراد الفئات المطلوبة

الخطوة الأولى عندما تقوم بـ **create Excel workbook python** هي استيراد فئات Aspose.Cells التي ستحتاجها. هذه الفئات تمنحك وصولًا مباشرًا إلى إنشاء المصنف، التنسيق الشرطي، وتنسيق الأنماط.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*لماذا هذا مهم:* استيراد الرموز المطلوبة فقط يبقي مساحة الأسماء نظيفة ويسهّل قراءة البرنامج. `Workbook` هو نقطة الدخول لـ **create Excel workbook python**، بينما `FormatConditionType` و `TimePeriodType` أساسيان لـ **excel conditional formatting python**.

## الخطوة 2: إنشاء مصنف جديد والحصول على الورقة الأولى

الآن نقوم فعليًا بـ **create Excel workbook python**. يُنشئ المُنشئ `Workbook()` ملف Excel فارغ مع ورقة عمل افتراضية.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*شرح:* كل ملف Excel يبدأ بورقة عمل واحدة على الأقل. بشكل افتراضي تُسمّي Aspose.Cells هذه الورقة “Sheet1”. يمكنك إضافة أوراق أخرى لاحقًا، لكن لهذا العرض توجيه مثالنا إلى ورقة واحدة لتبقى الفكرة مركزة.

## الخطوة 3: تحديد النطاق المستهدف للتنسيق الشرطي

يعمل التنسيق الشرطي على نطاق مستطيل. هنا نختار النطاق `I19:K20`، الذي يوفّر ثلاثة أعمدة وصفين للعبث بهما.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*سبب القيام بذلك:* طريقة `get` تُعيد كائن `ConditionalFormatting` مرتبط بالنطاق المحدد. إذا لم يكن للنطاق أي تنسيق بعد، تُنشئ Aspose.Cells مجموعة جديدة تلقائيًا.

## الخطوة 4: إضافة شرط TIME_PERIOD وتعيين لون الخلفية

هذا هو جوهر **excel conditional formatting python**. نضيف قاعدة `TIME_PERIOD` التي تُبرز الخلايا التي تحتوي تواريخها على “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*تفصيل عميق:*  
- `FormatConditionType.TIME_PERIOD` يُخبر Excel بتقييم التواريخ نسبةً إلى التاريخ الحالي.  
- `TimePeriodType.YESTERDAY` هو تعداد مدمج يُحدّث نفسه تلقائيًا كل يوم، بحيث يظل المصنف يبرز دائمًا “Yesterday” الأخير.  
- بتعيين `background_color` إلى `Color.pink` والنمط إلى `SOLID`، نحصل على تأثير **cell background color python** دون الحاجة إلى كود VBA إضافي.

## الخطوة 5: ملء النطاق بتواريخ تجريبية وتطبيق تنسيق التاريخ

لرؤية التنسيق الشرطي يعمل، نحتاج إلى قيم تاريخية حقيقية. كما نحتاج إلى **format cells date python** حتى يتعامل Excel مع القيم كتاريخ وليس كأرقام عادية.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*شرح:*  
- السطر `style.number = 30` هو خطوة **format cells date python**. رمز التنسيق 30 يُطابق نمط التاريخ القصير (`m/d/yy`).  
- استخدام دالة مساعدة يُبقي الشيفرة DRY (Don’t Repeat Yourself) ويسهّل إضافة تواريخ أخرى لاحقًا.

## الخطوة 6: إضافة تسمية وصفية

تساعد تسمية صغيرة أي شخص يفتح المصنف على فهم سبب تلوين الخلايا.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## الخطوة 7: حفظ المصنف على القرص

أخيرًا، نقوم بـ **create Excel workbook python** على القرص عبر استدعاء `save`. يضمن ثابت `SaveFormat.XLSX` أن الملف يكون بصيغة Office Open XML الحديثة.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

عند فتح `TimePeriodDemo.xlsx` في Excel، ستلاحظ:

- الخلايا `I19` و `K20` تحتوي على تواريخ.  
- الخلية التي تطابق “Yesterday” (في هذا المثال الثابت، `I19`) مُظللة بالوردي.  
- التسمية “Yesterday” تظهر في `I20`.  

> **نصيحة:** إذا شغّلت البرنامج في يوم مختلف، سيظل التنسيق الشرطي يبرز الخلية التي تاريخها يساوي اليوم السابق لتاريخ النظام—بدون الحاجة لتعديل الشيفرة.

## البرنامج الكامل – جاهز للنسخ والتنفيذ

فيما يلي البرنامج المتكامل، المستقل، الذي يجمع جميع الخطوات السابقة. انسخه إلى ملف باسم `conditional_format_demo.py`، عدّل `YOUR_DIRECTORY`، ثم نفّذه باستخدام `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع سطر تأكيد:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

فتح الملف المُنشأ يُظهر الخلفية الوردية على الخلية التي تطابق قاعدة “Yesterday”، مما يؤكد أن **excel conditional formatting python** و **cell background color python** يعملان معًا.

## الاختلافات الشائعة والحالات الحدية

| الحالة | كيفية تعديل الشيفرة |
|-----------|-----------------------|
| **لون تمييز مختلف** | غيّر `Color.pink` إلى أي ثابت `Color` آخر، مثل `Color.light_green`. |
| **تمييز “Today” بدلاً من “Yesterday”** | عيّن `condition.time_period = TimePeriodType.TODAY`. |
| **تطبيق التنسيق على عمود كامل** | استخدم نطاقًا مثل `"A:A"` وعدّل المتغيّر `target_range` وفقًا لذلك. |
| **استخدام تنسيق تاريخ مخصص** | استبدل `style.number = 30` بـ `style.custom = "dd-mmm-yyyy"` للحصول على تنسيق أكثر قابلية للقراءة. |
| **شروط متعددة على نفس النطاق** |  |

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}