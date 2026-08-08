---
category: general
date: 2026-08-08
description: إنشاء مصنف Excel باستخدام بايثون وإضافة تنسيق شرطي بناءً على التاريخ.
  دليل خطوة بخطوة باستخدام Aspose.Cells لتسليط الضوء على خلايا الأمس.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: ar
lastmod: 2026-08-08
og_description: إنشاء مصنف Excel باستخدام بايثون مع Aspose.Cells وتطبيق تنسيق شرطي
  بناءً على التاريخ لجداول البيانات الديناميكية.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: إنشاء ملف عمل Excel باستخدام Python – تنسيق شرطي للتواريخ
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: إنشاء مصنف إكسل لتنسيق شرطي لتاريخ بايثون
url: /ar/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel باستخدام Python وتنسيق شرطي حسب التاريخ

إذا كنت بحاجة إلى **create Excel workbook Python** وتريد تمييز الخلايا التي تطابق تاريخًا محددًا تلقائيًا، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعلم تطبيق **conditional formatting based on date** بحيث تُظهر تواريخ الأمس باللون الوردي، باستخدام مكتبة Aspose.Cells.

الدليل يمر بكل خطوة — من تثبيت SDK إلى حفظ ملف .xlsx النهائي — حتى تتمكن من نسخ‑لصق مثال عملي في مشروعك الخاص. لا حاجة إلى وثائق خارجية؛ جميع الشيفرات والتفسيرات مكتوبة ضمن الدليل نفسه.

## المتطلبات المسبقة

* Python 3.8 أو أحدث مثبت.
* `aspose-cells` package (الواجهة البرمجية لـ Python لمكتبة Aspose.Cells). قم بتثبيتها باستخدام:
  ```bash
  pip install aspose-cells
  ```
* إلمام أساسي بـ Python ومفاهيم Excel مثل أوراق العمل وأنماط الخلايا.

> **نصيحة احترافية:** تعمل Aspose.Cells بدون الحاجة لتثبيت Microsoft Excel، مما يجعلها مثالية لأتمتة الخوادم.

## الخطوة 1: إنشاء مصنف Excel في Python

المهمة الأولى هي إنشاء كائن مصنف جديد والحصول على ورقة العمل الافتراضية. هذا الكائن يمثل ملف Excel بالكامل ويوفر الوصول إلى الصفوف والأعمدة وواجهات برمجة التطبيقات الخاصة بالتنسيق.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

إنشاء المصنف هو الأساس لأي تعديل لاحق، سواءً كنت تضيف بيانات أو صيغ أو قواعد تنسيق.

## الخطوة 2: تعريف تنسيق شرطي يعتمد على التاريخ

الآن نضيف **conditional formatting based on date**. يتيح لنا تعداد `FormatConditionType.TIME_PERIOD` تحديد فترات زمنية مدمجة مثل Yesterday أو Today أو LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

سبب أهمية هذه الخطوة: يقوم Excel بتقييم الشرط لكل خلية في النطاق. عندما تكون قيمة الخلية ضمن الفترة المحددة (الأمس)، يتم تطبيق النمط الذي حددناه تلقائيًا.

## الخطوة 3: ملء النطاق بتواريخ تجريبية

لرؤية القاعدة تعمل، نكتب عددًا من كائنات `datetime` في الخلايا المستهدفة. أحدها مُحدد عمدًا ليكون تاريخ الأمس وفقًا لنظام التاريخ الداخلي للمصنف.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

السطر `number = 30` يخبر Excel بعرض القيمة باستخدام تنسيق التاريخ القصير القياسي. يمكنك تغيير هذا الفهرس إلى أي تنسيق رقم مدمج إذا كنت تفضل عرضًا مختلفًا.

## الخطوة 4: ضبط عرض العمود لسهولة القراءة

تعديل عرض العمود الذي يحتوي على التواريخ تلقائيًا يجعل المخرجات أسهل للقراءة، خاصةً عند فتح المصنف في Excel أو عارض.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## الخطوة 5: حفظ المصنف على القرص

أخيرًا، احفظ المصنف كملف .xlsx. استبدل `"YOUR_DIRECTORY"` بمسار حقيقي على جهازك.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

عند فتح `TimePeriodDemo.out.xlsx` في Excel، ستظهر الخلية **I19** بخلفية وردية لأن قيمتها تطابق قاعدة “Yesterday”، بينما تظل **K20** دون تغيير.

### النتيجة المتوقعة

| I19 (التاريخ) | I20 (التسمية) | J19 | J20 | K19 | K20 (التاريخ) |
|---------------|---------------|-----|-----|-----|----------------|
| *2008‑07‑30* (خلفية وردية) | Yesterday | – | – | – | *2008‑08‑03* (بدون تنسيق) |

التظليل الوردي يؤكد أن **conditional formatting based on date** يعمل كما هو مقصود.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية تعديل الشيفرة |
|--------|--------------------|
| **تمييز “Today” بدلاً من “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **تطبيق القاعدة على عمود كامل** | Use `worksheet.get_range("A:A").format_conditions` |
| **استخدام نطاق تاريخ مخصص (مثلاً آخر 7 أيام)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **ألوان خلفية مختلفة** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **التشغيل على Linux بدون شاشة** | Aspose.Cells تعمل بالكامل بدون واجهة رسومية؛ لا حاجة إلى أي إعداد إضافي. |

## مثال كامل قابل للتنفيذ

فيما يلي السكريبت الكامل الذي يمكنك تشغيله كما هو (بعد تحديث مسار المخرجات). جميع الاستيرادات، التعليقات، وأساسيات معالجة الأخطاء مضمونة.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

تشغيل السكريبت ينتج ملف Excel حيث يتم تمييز خلية “Yesterday” تلقائيًا، مما يوضح **create Excel workbook Python** مع **conditional formatting based on date**.

## الخلاصة

أنت الآن تعرف كيفية **create Excel workbook Python**، وتعريف **date‑based conditional formatting

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف Excel باستخدام Aspose.Cells في Java: دليل خطوة بخطوة](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [إنشاء مصنف Excel مع مخططات باستخدام Aspose.Cells .NET | دليل خطوة بخطوة](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [أتمتة Excel: إنشاء مصنف وإضافة ListBox باستخدام Aspose.Cells لـ .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}