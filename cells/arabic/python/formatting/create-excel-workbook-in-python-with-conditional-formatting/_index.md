---
category: general
date: 2026-09-05
description: إنشاء مصنف إكسل في بايثون وإضافة تنسيق شرطي لتظليل خلايا الأمس. تعلّم
  الكود الكامل ولماذا كل خطوة مهمة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: ar
lastmod: 2026-09-05
og_description: إنشاء مصنف Excel في بايثون وإضافة تنسيق شرطي لتسليط الضوء على خلايا
  الأمس. اتبع هذا الدليل خطوة بخطوة للحصول على حل كامل.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: إنشاء مصنف إكسل في بايثون – إضافة تنسيق شرطي
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: إنشاء مصنف إكسل في بايثون مع تنسيق شرطي
url: /ar/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel في Python مع التنسيق الشرطي

إذا كنت بحاجة إلى **create Excel workbook python** لمهمة تقارير، يوضح لك هذا الدليل كيفية إنشاء مصنف وتطبيق قاعدة تنسيق شرطي تُبرز تواريخ الأمس. سترى الشيفرة الدقيقة، سبب وجود كل سطر، وكيفية تعديل الحل لنطاقات تواريخ أخرى.

التنسيق الشرطي هو طريقة قوية لجذب الانتباه إلى البيانات التي تفي بشرط معين. في هذا البرنامج التعليمي نستخدم مكتبة Aspose.Cells للـ Python عبر .NET، التي توفر دعمًا كاملاً لميزات Excel دون الحاجة إلى Microsoft Office. بحلول نهاية الدليل ستحصل على ملف حيث تتحول الخلايا في النطاق *I19:K20* إلى اللون الوردي عندما تحتوي على تاريخ الأمس.

## المتطلبات المسبقة

* تثبيت Python 3.9+  
* حزمة `aspose-cells` (تثبيت باستخدام `pip install aspose-cells`)  
* إلمام أساسي بصياغة Python  
* صلاحية كتابة في الدليل الذي سيُحفظ فيه المصنف

تعمل الشيفرة على Windows و macOS و Linux طالما كان وقت تشغيل .NET متاحًا.

## إنشاء مصنف Excel في Python

الخطوة الأولى هي إنشاء كائن `Workbook` والحصول على ورقة العمل الافتراضية. يمثل هذا الكائن ملف Excel بالكامل في الذاكرة.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*لماذا هذا مهم*: `Workbook()` ينشئ مصنفًا فارغًا بورقة عمل واحدة. الوصول إلى `worksheets[0]` يمنحك مقبضًا لإضافة البيانات والأنماط والتنسيق لاحقًا.

## إضافة نطاق التنسيق الشرطي

بعد ذلك نحدد المنطقة التي سيتم تقييمها بواسطة القاعدة الشرطية. النطاق `I19:K20` يغطي ست خلايا عبر صفين.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*لماذا هذا مهم*: إضافة مجموعة تنسيق شرطي إلى نطاق محدد يعزل القاعدة، مما يمنعها من التأثير على خلايا غير ذات صلة. هذا يحقق متطلب **add conditional formatting range**.

## تعريف القاعدة: تمييز الخلايا بناءً على التاريخ

نقوم الآن بإنشاء شرط من النوع `TIME_PERIOD`. هذا يخبر Excel بمقارنة قيمة كل خلية مع نافذة زمنية محددة مسبقًا.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*لماذا هذا مهم*: `TIME_PERIOD` هو النوع المدمج الوحيد الذي يدعم مباشرةً “Yesterday” و “Today” و “Last Week” وغيرها. بتعيين `condition.time_period` إلى `YESTERDAY`، تقوم القاعدة تلقائيًا بتقييم قيمة تاريخ كل خلية مقابل اليوم السابق للتاريخ الحالي.

## تنسيق الخلايا التي تفي بالشرط

التنسيق الشرطي يحتاج أيضًا إلى نمط بصري. هنا نختار تعبئة صلبة باللون الوردي لجعل الخلايا المطابقة بارزة.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*لماذا هذا مهم*: كائن النمط يحدد كيف سيعرض Excel الخلايا التي تفي بالشرط. استخدام تعبئة صلبة باللون الوردي يحقق متطلب **highlight cells based on date** ويجعل النتيجة سهلة التحقق.

## تعبئة تواريخ نموذجية للتقييم

لرؤية القاعدة تعمل نُدخل تاريخين—أحدهما يطابق تاريخ الأمس والآخر لا. تنسيق `number` `30` يتوافق مع تنسيق التاريخ المدمج `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*لماذا هذا مهم*: توفير تاريخ مطابق وآخر غير مطابق يتيح لك التحقق من أن التنسيق الشرطي يعمل بشكل صحيح. عدل التواريخ لتتناسب مع الشهر الحالي عند تشغيل السكريبت، أو استبدلها بقيم ديناميكية.

## حفظ المصنف

أخيرًا نكتب الملف إلى القرص. ثابت `SaveFormat.XLSX` يضمن أن يكون الناتج ملف Excel حديث.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*لماذا هذا مهم*: حفظ المصنف يتيح لك فتحه في Excel أو LibreOffice أو أي عارض يدعم XLSX. المسار المطبع يؤكد مكان كتابة الملف.

## السكريبت الكامل

بتجميع جميع الأجزاء معًا، يبدو السكريبت الكامل القابل للتنفيذ كالتالي:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### النتيجة المتوقعة

عند فتح `TimePeriodExample.xlsx`:

* الخلية **I19** تظهر بخلفية وردية لأن قيمتها تطابق تاريخ الأمس.
* الخلية **K20** تحتفظ بالخلفية الافتراضية لأن تاريخها خارج الفترة.
* التسمية **“Yesterday”** موجودة في الخلية I20 لتوضيح.

## الاختلافات الشائعة وحالات الحافة

| Situation | Adjustment |
|-----------|------------|
| **تمييز اليوم بدلاً من الأمس** | غيّر `condition.time_period = TimePeriodType.TODAY`. |
| **تطبيق القاعدة على مساحة أكبر** | حدّث سلسلة النطاق في `add("I19:K20")` إلى شيء مثل `"A1:Z100"`. |
| **استخدام لون تعبئة مختلف** | استبدل `DrawingColor.pink` بأي `DrawingColor` آخر (مثال: `DrawingColor.light_green`). |
| **العمل مع تواريخ ديناميكية** | احسب `datetime.now() - timedelta(days=1)` للحصول على تاريخ الأمس واكتب تلك القيمة في الخلايا قبل تطبيق القاعدة. |

**نصيحة احترافية:** عندما تنشئ المصنف برمجيًا للعديد من المستخدمين، احتفظ بتعريف التنسيق الشرطي منفصلًا عن إدخال البيانات. بهذه الطريقة يمكنك إعادة استخدام النمط نفسه عبر عدة أوراق دون تكرار الشيفرة.

## التحقق من النتيجة برمجيًا (اختياري)

إذا كنت ترغب في تأكيد التنسيق دون فتح Excel، يمكنك فحص نمط خلية بعد الحفظ:



## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [أتمتة Excel: إنشاء مصنف وإضافة ListBox باستخدام Aspose.Cells لـ .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [إنشاء مصنف Excel وإضافة تسميات باستخدام Aspose.Cells للـ Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [أتمتة Excel: إنشاء مصنف وإضافة ListBox باستخدام Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}