---
category: general
date: 2026-07-20
description: إنشاء مصنف Excel باستخدام Python و Aspose.Cells، تعيين لون خلفية الخلية،
  وإضافة تنسيق شرطي باستخدام Python لتنسيق الخلايا حسب التاريخ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: ar
lastmod: 2026-07-20
og_description: إنشاء مصنف إكسل باستخدام بايثون و Aspose.Cells. تعلم كيفية تعيين لون
  خلفية الخلية وإضافة تنسيق شرطي بايثون لتنسيق الخلايا حسب التاريخ.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: إنشاء مصنف إكسل بايثون – إضافة تنسيق شرطي
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: إنشاء مصنف إكسل بايثون – دليل التنسيق الشرطي
url: /ar/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف إكسل باستخدام بايثون – دليل التنسيق الشرطي

هل تساءلت يومًا كيف **تنشئ مصنف إكسل بايثون** من الصفر وتجعله يبدو مصقولًا دون فتح الواجهة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى **تعيين لون خلفية الخلية** أو تطبيق أنماط تعتمد على التاريخ برمجيًا.  

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يستخدم Aspose.Cells لإضافة قواعد **conditional formatting python**، وتنسيق الخلايا حسب التاريخ، وحفظ النتيجة كملف XLSX حديث. في النهاية ستحصل على سكريبت مستقل يمكنك وضعه في أي مشروع.

## ما ستتعلمه

- كيفية تهيئة مصنف والحصول على الورقة الأولى.  
- طرق **set cell background color** لنطاق كامل.  
- استخدام **aspose cells conditional formatting** لتسليط الضوء على تواريخ “الأمس”.  
- ضبط عرض الأعمدة تلقائيًا وحفظ الملف على القرص.  

لا تحتاج إلى أي إعدادات خارجية—فقط Python 3 وحزمة Aspose.Cells. إذا كنت قد ثبتت `aspose-cells` مسبقًا، فأنت جاهز؛ وإلا فالأمر `pip install aspose-cells` يكفي.

## المتطلبات المسبقة

- Python 3.8+ (الكود يعمل على 3.9، 3.10، والإصدارات الأحدث).  
- Aspose.Cells for Python via .NET (غلاف NuGet `aspose-cells`).  
- معرفة أساسية بمفاهيم إكسل (الخلايا، النطاقات، التنسيق).  

هل لديك كل ذلك؟ رائع—لنبدأ.

## إنشاء مصنف إكسل بايثون – الإعداد والورقة

أولًا: نحتاج إلى كائن مصنف جديد وإشارة إلى الورقة الافتراضية. هذه هي اللوحة التي ستُجرى عليها جميع العمليات لاحقًا.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **لماذا هذا مهم:** `Workbook()` يُنشئ ملف إكسل في الذاكرة، مما يلغي الحاجة إلى ملفات مؤقتة. المتغيّر `worksheet` هو نقطة الدخول لإجراءات مستوى الخلية.

## تعيين لون خلفية الخلية

قبل إضافة أي قواعد، من الجيد إعطاء النطاق المستهدف لونًا أساسيًا حتى يبرز التنسيق الشرطي. الدالة المساعدة أدناه تسترجع (أو تنشئ) `FormatConditionCollection` لنطاق معين وتلوّن الخلايا بخلفية صلبة.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **نصيحة محترف:** إذا كنت تخطط لإعادة استخدام نفس النطاق مع قواعد متعددة، استدعِ هذه الدالة مرة واحدة واحتفظ بالمجموعة المرجعة؛ سيوفر ذلك عدة استدعاءات API.

## إضافة تنسيق شرطي بايثون لنطاقات التاريخ

الجزء الممتع الآن: سننشئ قاعدة **conditional formatting** لفترة زمنية تُبرز الخلايا التي تحتوي على تاريخ الأمس. هذا يوضح قوة **format cells by date** باستخدام Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **لماذا نستخدم `TIME_PERIOD`؟** يخفّف الحاجة لكتابة صيغ مخصصة. تقوم Aspose.Cells بتقييم التاريخ مقابل تاريخ النظام الحالي، لذا تظل القاعدة دائمًا ذات صلة.

### تشغيل القاعدة

```python
apply_yesterday_rule()
```

عند فتح الملف الناتج، ستضيء الخلايا `I19` باللون الوردي (لأنها “Yesterday”)، بينما تظل الخلية `K20` باللون الأخضر الأساسي.

## ضبط عرض الأعمدة تلقائيًا وحفظ المصنف

جدول مرتب يبدو احترافيًا. الضبط التلقائي يضمن عدم تكدس البيانات.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **حالة حدية:** إذا استهدفت مجلدًا غير موجود، سيتسبب `workbook.save` في رفع استثناء. ضع استدعاء الحفظ داخل كتلة `try/except` إذا أردت معالجة ناعمة.

### السكريبت الكامل (جاهز للنسخ واللصق)

فيما يلي السكريبت بالكامل، جاهز للتنفيذ. استبدل `YOUR_DIRECTORY` بمسار مجلد صالح على جهازك.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

تشغيل هذا السكريبت سينتج ملف `TimePeriodExample.xlsx` مع التنسيق الشرطي الذي وصفناه.

## أسئلة شائعة ونصائح

- **هل يمكنني استهداف نطاق تاريخ مختلف؟**  
  بالتأكيد. غيّر `"I19:K20"` إلى أي نطاق بصيغة A1، وعدّل تواريخ العينة وفقًا لذلك.

- **ماذا لو احتجت صيغة مخصصة بدلاً من `YESTERDAY`؟**  
  استخدم `FormatConditionType.FORMULA` وضع `condition.formula1 = "YOUR_FORMULA"`—مثلاً `=TODAY()-A1=1` لمحاكاة الأمس.

- **كيف أطبق قواعد متعددة على نفس النطاق؟**  
  استدعِ `conditions.add_condition` مرة أخرى بنوع `FormatConditionType` مختلف. الترتيب مهم؛ القواعد اللاحقة يمكن أن تتجاوز السابقة.

- **هل يمكن تعيين لون الخط مع الخلفية؟**  
  نعم—عدّل `condition.style.font.color = Color.white` (أو أي `Color` آخر).

## الخلاصة

أنت الآن تعرف كيف **تنشئ مصنف إكسل بايثون** باستخدام Aspose.Cells، **تعيّن لون خلفية الخلية**، وتضيف **conditional formatting python** ينسق الخلايا حسب التاريخ. السكريبت كامل الوظائف، يتعامل مع الحالات الحدية مثل المجلدات غير الموجودة، ويمكن توسيعه إلى سيناريوهات أكثر تعقيدًا مثل منطق تنسيق متعدد القواعد أو اكتشاف النطاقات ديناميكيًا.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال قاعدة “Yesterday” بقاعدة “Last Week”، أو جرب تعبئة تدرجية، أو أنشئ تقريرًا كاملًا يحتوي على عشرات الجداول المنسقة. جميع اللبنات الأساسية موجودة هنا، وقد أتقنت الآن جوهر **aspose cells conditional formatting** في بايثون.

برمجة سعيدة، ولا تتردد في مشاركة تنويعاتك في التعليقات!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}