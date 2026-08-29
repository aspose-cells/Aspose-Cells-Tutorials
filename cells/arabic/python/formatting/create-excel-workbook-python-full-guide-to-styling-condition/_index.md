---
category: general
date: 2026-07-06
description: إنشاء مصنف إكسل باستخدام بايثون مع كود لتعيين لون خلفية الخلية، وتعيين
  نمط الخلية برمجيًا، وإضافة تنسيق شرطي بايثون لتسليط الضوء على تاريخ اليوم.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: ar
lastmod: 2026-07-06
og_description: أنشئ دفتر عمل Excel باستخدام Python فورًا. تعلم كيفية تعيين لون خلفية
  الخلية، وتعيين نمط الخلية برمجيًا، وإضافة تنسيق شرطي باستخدام Python لتسليط الضوء
  على تاريخ اليوم.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: إنشاء مصنف إكسل بايثون – تنسيق الخلايا وتحديد اليوم
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: إنشاء مصنف إكسل باستخدام بايثون – دليل شامل للتنسيق والتنسيق الشرطي
url: /ar/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel باستخدام Python – دليل كامل لتنسيق الخلايا والأنماط الشرطية

هل تساءلت يومًا كيف **create Excel workbook Python** من الصفر دون فتح Excel بنفسك؟ لست وحدك. يحتاج العديد من المطورين إلى توليد تقارير، لوحات تحكم، أو حتى سجلات بيانات بسيطة في الوقت الفعلي، والقيام بذلك برمجيًا يوفر ساعات من العمل اليدوي.

في هذا الدرس سنستعرض العملية بالكامل: من إنشاء مصنف جديد، إلى **set cell background color**، إلى **set cell style programmatically**، وأخيرًا إلى **highlight today date excel** باستخدام **add conditional formatting python**. في النهاية ستحصل على سكريبت جاهز للتنفيذ ينتج ملف .xlsx مصقول خلال ثوانٍ.

---

## ما ستبنيه

- ملف Excel جديد مع بعض الخلايا المملوءة.
- خلايا ملونة بخلفية مخصصة.
- قيم رقمية وتواريخ مُنسقة بنمط رقم محدد.
- قاعدة شرطية تُبرز تلقائيًا الخلية التي تحتوي على تاريخ اليوم.

لا حاجة لتثبيت Excel خارجي — Aspose.Cells for Python via .NET يقوم بكل العمل الشاق.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| Python 3.8+ | بناء جملة حديث وتلميحات نوع |
| `aspose-cells` package | المكتبة الأساسية لتعامل مع المصنفات |
| `aspose-pydrawing` (installed with Aspose.Cells) | توفر الفئة `Color` |
| Familiarity أساسية بمفاهيم Excel (الخلايا، النطاقات، التنسيق) | يجعل سير الدرس أكثر سلاسة |

ثبت المكتبة باستخدام:

```bash
pip install aspose-cells
```

---

## الخطوة 1: تهيئة المصنف وورقة العمل

أول شيء تقوم به عندما **create excel workbook python** هو إنشاء كائن `Workbook` والحصول على ورقة العمل الافتراضية. فكر في المصنف كملف Excel كامل، بينما ورقة العمل هي تبويب واحد داخله.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى عدة أوراق، استخدم `book.worksheets.add("MySheet")` لإضافة تبويبات أخرى.

---

## الخطوة 2: فئة المساعدة للتنسيق والأنماط الشرطية

فيما يلي فئة `ConditionalFormatting` مدمجة لكنها كاملة. هي تغلف المهام المتكررة التالية:

1. تحويل نطاق مثل `"A1:C3"` إلى `CellArea`.
2. ملء كل خلية في ذلك النطاق برقم تسلسلي (لأغراض العرض فقط).
3. تطبيق لون خلفية صلب **set cell background color**.
4. إضافة قاعدة شرطية تقوم بـ **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### لماذا فئة مساعدة؟

- **قابلية إعادة الاستخدام:** يمكنك استدعاء `add_time_period_1()` لأي ورقة عمل دون إعادة كتابة المنطق.
- **وضوح:** كل طريقة تقوم بعمل واحد – سمة الكود النظيف.
- **قابلية التوسع:** تريد إضافة قواعد أخرى؟ فقط أضف طريقة أخرى باتباع النمط نفسه.

---

## الخطوة 3: تطبيق التنسيق وحفظ الملف

الآن نجمع كل شيء معًا: ننشئ كائن المساعدة، نشغل روتين التنسيق، وأخيرًا نكتب المصنف إلى القرص.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

عند فتح *styled_workbook.xlsx* يجب أن ترى:

- الخلايا **A1:C3** مرقمة من 0‑8 مع تعبئة بلون أزرق سماوي فاتح.
- الخلية **I1** تعرض تاريخ اليوم بخلفية وردية (بفضل القاعدة الشرطية).
- الخلية **K2** تعرض التاريخ الثابت *2008‑07‑30* للمقارنة.
- الخلية **I2** تحتوي على النص “Today”.

هذه الإشارة البصرية هي بالضبط ما تطلبه متطلبات **highlight today date excel**.

---

## الخطوة 4: تعمق – تخصيص الأنماط

إذا كنت بحاجة إلى تعديل الخطوط، الحدود، أو تنسيقات الأرقام، يمكنك توسيع طريقة `fill_cell` أو إنشاء مساعدة جديدة:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

يمكنك بعد ذلك استدعاء `apply_custom_style(cell, bold=True)` داخل الحلقة لتطبيق **set cell style programmatically** على كل خلية في النطاق.

---

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| الخلايا تبقى بيضاء رغم `Color.light_sky_blue` | لم يتم تطبيق النمط بعد تعيين `foreground_color` | دائمًا استدعِ `cell.set_style(style)` بعد تعديل كائن النمط. |
| القاعدة الشرطية لا تُفعَّل أبدًا | `style.number` غير مُعيَّن لخلايا التاريخ، لذا يتعامل Excel مع القيمة كسلسلة | عيّن `style.number = 30` (أو أي تنسيق تاريخ) قبل `cell.put_value(datetime…)`. |
| المصنف يُحفظ كـ .xls رغم `SaveFormat.XLSX` | إصدار Aspose قديم يفضّل الصيغة القديمة | قم بالترقية إلى أحدث حزمة `aspose-cells`. |
| النطاق مثل `"A1"` يسبب خطأ فهرسة | استخدام `cells.get("A1")` على ورقة لم تُنشأ بعد | تأكد من وجود ورقة العمل (توجد مباشرة بعد `Workbook()`)، أو استخدم `cells.get(row, col)` مع مؤشرات تبدأ من الصفر. |

---

## النص الكامل للنسخ‑واللصق

فيما يلي **entire** السكريبت يمكنك وضعه في ملف اسمه `create_excel.py` وتشغيله فورًا.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [أتمتة Excel باستخدام Aspose.Cells .NET: إنشاء مصنف وتعيين روابط خارجية](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [إتقان تنسيق خلايا Excel وإدارة المصنفات باستخدام Aspose.Cells لـ .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [أتمتة Excel: إنشاء مصنف وإضافة ListBox باستخدام Aspose.Cells لـ .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}