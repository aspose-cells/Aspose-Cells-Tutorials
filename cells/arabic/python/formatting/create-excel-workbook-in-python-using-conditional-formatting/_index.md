---
category: general
date: 2026-09-21
description: تعلم كيفية إنشاء مصنف Excel في Python، وتعيين لون خلفية الخلية، وتطبيق
  تنسيق شرطي قائم على التاريخ باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: ar
lastmod: 2026-09-21
og_description: إنشاء مصنف Excel في بايثون، ضبط لون خلفية الخلية، وتطبيق تنسيق شرطي
  يعتمد على التاريخ باستخدام Aspose.Cells. اتبع الدليل خطوة بخطوة.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: إنشاء مصنف إكسل في بايثون مع التنسيق الشرطي
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: إنشاء مصنف إكسل في بايثون باستخدام التنسيق الشرطي
url: /ar/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel في Python باستخدام التنسيق الشرطي

إذا كنت بحاجة إلى سكريبتات **create Excel workbook python** التي تبرز التواريخ تلقائيًا، فإن هذا الدليل يوضح لك بالضبط كيفية ذلك. سترى كيفية **set cell background color**، إضافة قاعدة “Yesterday”، وحفظ الملف — كل ذلك باستخدام Aspose.Cells for Python.

العمل مع ملفات Excel برمجيًا يعني غالبًا تكرار نفس منطق التنسيق عبر العديد من الأوراق. بنهاية هذا الدرس ستحصل على نمط قابل لإعادة الاستخدام لـ **excel conditional formatting python** يمكنك إدراجه في أي مشروع.

## المتطلبات المسبقة

- Python 3.8+ مثبت  
- حزمة `aspose-cells` (`pip install aspose-cells`)  
- إلمام أساسي بدوال Python ووحدة datetime  

لا توجد مكتبات إضافية مطلوبة؛ Aspose.Cells يتعامل مع جميع عمليات Excel.

## الخطوة 1: إنشاء المصنف والوصول إلى ورقة العمل الأولى

الخطوة الأولى هي **create excel workbook python** وإنشاء الكائنات والحصول على ورقة العمل الافتراضية. هذا يمنحك مساحة عمل نظيفة لمزيد من التنسيق.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*لماذا هذا مهم:* `Workbook()` ينشئ ملف Excel في الذاكرة. الوصول إلى `worksheets[0]` يتجنب الترميز الصلب لأسماء الأوراق ويعمل حتى إذا تغير الاسم الافتراضي.

## الخطوة 2: مساعد لإضافة تنسيق شرطي TIME_PERIOD

للحفاظ على نظافة الكود، نغلف إنشاء التنسيق الشرطي في مساعد. يستقبل نطاق خلايا، لون خلفية، والقاعدة الزمنية المطلوبة.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*لماذا هذا مهم:* يساعد المساعد على تجريد الخطوات المتكررة لإنشاء تنسيق شرطي، مما يسهل إعادة استخدامه لقواعد أخرى تعتمد على التاريخ مثل “Today” أو “Last Week”.

## الخطوة 3: تطبيق قاعدة “Yesterday” على نطاق

الآن نستخدم المساعد لتظليل الخلايا التي تحتوي على تاريخ الأمس. النطاق `I19:K20` سيتحول إلى **medium sea green** عندما يتحقق الشرط.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*لماذا هذا مهم:* `TimePeriodType.YESTERDAY` هي جزء من تعداد Aspose.Cells المدمج، لذا لا تحتاج إلى حساب التواريخ يدويًا. المكتبة تقيم القاعدة في كل مرة يفتح فيها المصنف.

## الخطوة 4: ملء النطاق بتواريخ نموذجية

لرؤية القاعدة تعمل، نكتب تاريخين—أحدهما يطابق “Yesterday” والآخر لا. النمط `number` `30` يت对应 إلى تنسيق تاريخ مدمج.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*لماذا هذا مهم:* بإدخال تواريخ محددة يمكنك التحقق من عمل التنسيق الشرطي دون الحاجة لفتح الملف في يوم معين.

## الخطوة 5: إضافة تسمية وصفية وتعديل عرض العمود تلقائيًا

تسمية صغيرة توضح هدف النطاق المنسق، و`auto_fit_column` يجعل الورقة قابلة للقراءة.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## الخطوة 6: حفظ المصنف

أخيرًا، احفظ المصنف على القرص. استدعاء `os.makedirs` يضمن وجود المجلد الهدف.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

عند فتح *TimePeriodDemo.xlsx* ستلاحظ:

- الخلية **I19** مظللة باللون **medium sea green** لأن قيمتها تطابق قاعدة “Yesterday”.  
- الخلية **K20** تحتفظ بالخلفية الافتراضية لأن تاريخها لا يفي بالشرط.  

هذا يوضح **format cells by date** باستخدام سطر واحد من كود Python.

## مثال كامل قابل للتنفيذ

بجمع جميع الأجزاء معًا، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه وتشغيله:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

شغّل السكريبت، افتح الملف الناتج، وسترى التنسيق الشرطي يعمل.

## الاختلافات الشائعة وحالات الحافة

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Highlight “Today”** | استبدل `TimePeriodType.YESTERDAY` بـ `TimePeriodType.TODAY` | لوحات معلومات في الوقت الحقيقي |
| **Multiple ranges** | استدعِ `add_time_period` لكل نطاق، مع تمرير ألوان مختلفة | تقارير معقدة |
| **Dynamic date range** | استخدم `TimePeriodType.LAST_7_DAYS` أو `TimePeriodType.NEXT_MONTH` | تقارير متجددة |
| **Custom color** | استخدم `Color.from_argb(255, r, g, b)` لإنشاء أي درجة لون | تنسيق متسق مع العلامة التجارية |

**نصيحة احترافية:** دائمًا عيّن `condition.style.pattern = BackgroundType.SOLID` عندما تريد تعبئة صلبة؛ وإلا قد يعرض Excel تدرجًا يبدو غير متسق عبر الإصدارات.

## الخلاصة

أنت الآن تعرف كيف تنشئ سكريبتات **create Excel workbook python** التي **set cell background color**، وتطبق **excel conditional formatting python**، وتقوم بـ **format cells by date** باستخدام Aspose.Cells. يغطي المثال سيناريو **date based conditional formatting**، لكن النمط نفسه يعمل مع أي قاعدة زمنية.

بعد ذلك، قد ترغب في استكشاف:

- إضافة أشرطة بيانات أو مجموعات أيقونات (`FormatConditionType.DATA_BAR`)  
- دمج قواعد شرطية متعددة على نفس النطاق  
- تصدير المصنف إلى PDF (`SaveFormat.PDF`) للتقارير  

لا تتردد في تجربة ألوان، نطاقات، وأنواع فترات زمنية مختلفة لتناسب احتياجاتك الخاصة في التقارير. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إتقان تنسيق خلايا Excel وإدارة المصنفات باستخدام Aspose.Cells لـ .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [أتمتة Excel باستخدام Aspose.Cells .NET: إنشاء مصنف وتعيين روابط خارجية](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [كيفية إنشاء نطاقات مسماة محلية للمصنف في Excel باستخدام Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}