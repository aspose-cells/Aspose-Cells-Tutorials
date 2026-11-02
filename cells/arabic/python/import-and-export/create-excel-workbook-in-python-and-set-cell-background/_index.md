---
category: general
date: 2026-10-07
description: إنشاء مصنف Excel في بايثون، ضبط لون خلفية الخلية، ضبط عرض الأعمدة تلقائيًا،
  وتعبئة التواريخ في Excel مع مثال شفرة مختصر.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: ar
lastmod: 2026-10-07
og_description: إنشاء مصنف Excel في بايثون، ثم تعيين لون خلفية الخلية، وضبط عرض الأعمدة
  تلقائيًا، وإدخال التواريخ في Excel. اتبع هذا الدليل خطوة بخطوة لإنشاء ملف TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: إنشاء مصنف إكسل في بايثون – تعيين الخلفية والملاءمة التلقائية
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: إنشاء مصنف إكسل في بايثون وتعيين خلفية الخلية
url: /ar/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel في بايثون وتعيين خلفية الخلية

إنشاء مصنف Excel في بايثون وتطبيق تنسيق شرطي ببضع أسطر من الشيفرة فقط. يوضح لك هذا الدليل **كيفية إنشاء ملفات Excel** برمجياً، وتعيين لون خلفية الخلية، وضبط أعمدة Excel تلقائيًا، وإدخال تواريخ في Excel باستخدام مكتبة Aspose.Cells.

سوف تتعلم كيفية:
* تهيئة مصنف والحصول على ورقة العمل الأولى.  
* تعريف تنسيق شرطي يبرز تواريخ “الأمس”.  
* إدخال تواريخ نموذجية في خلايا محددة.  
* ضبط الأعمدة تلقائيًا بحيث تكون البيانات واضحة الرؤية.  
* حفظ المصنف في مجلد مختار.

المتطلب الوحيد هو وجود بيئة Python 3 تعمل مع حزم `aspose-cells` و `aspose-pydrawing` مثبتة:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## إنشاء مصنف Excel في بايثون – خطوة بخطوة

الأقسام التالية تقسم العملية إلى خطوات يمكن التحكم فيها. كل خطوة تتضمن الشيفرة المطلوبة، شرحًا **لماذا** هي مهمة، ونصيحة لتجنب الأخطاء الشائعة.

### الخطوة 1: استيراد المساحات الاسمية المطلوبة وتعريف دالة مساعدة

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*لماذا هذا مهم*: استيراد الفئات الصحيحة يمنحك القدرة على إنشاء المصنف، وتطبيق التنسيق الشرطي، ومعالجة الألوان.  
**نصيحة احترافية**: احتفظ بالاستيرادات في أعلى الملف؛ يجعل ذلك النص أسهل للقراءة ويمنع أخطاء الاستيراد الدائرية.

### الخطوة 2: إنشاء المصنف والحصول على ورقة العمل الأولى

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

المُنشئ `Workbook()` ينشئ مصنف Excel فارغ في الذاكرة.  
**لماذا**: البدء بمصنف جديد يضمن عدم وجود تنسيقات متبقية من تشغيلات سابقة.

### الخطوة 3: تعيين لون خلفية الخلية باستخدام تنسيق شرطي

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*لماذا*: استخدام شرط **فترة زمنية** يبرز تلقائيًا أي خلية تحتوي على تاريخ الأمس، مما يلغي الحاجة إلى فحص التاريخ يدويًا.  
**نصيحة**: `Color.pink` مجرد مثال؛ يمكنك استخدام أي كائن `Color` (`Color.yellow`, `Color.light_green`, إلخ).

### الخطوة 4: إدخال التواريخ في Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

هنا نقوم **بإدخال تواريخ في خلايا Excel** `I19` و `K20`. التاريخ الأول سيفعل التنسيق الشرطي، بينما الثاني لن يفعل ذلك.  
**لماذا هذا مهم**: إظهار القيم المتطابقة وغير المتطابقة يساعدك على التحقق من أن القاعدة تعمل كما هو متوقع.

### الخطوة 5: ضبط أعمدة Excel تلقائيًا لتحسين الرؤية

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` يضبط عرض العمود بناءً على أطول قيمة خلية.  
**نصيحة**: استدعِ هذا بعد كتابة جميع البيانات؛ وإلا قد يُحسب العرض على محتوى غير مكتمل.

### الخطوة 6: حفظ المصنف

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

حفظ الملف يكتب المصنف الموجود في الذاكرة إلى القرص بصيغة XLSX الحديثة.  

### البرنامج الكامل – تجميع كل الأجزاء معًا

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**الناتج المتوقع**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

افتح الملف المُولد في Excel – الخلايا `I19:K20` ستظهر خلفية وردية للتاريخ الذي يوافق “الأمس”، وستكون العمود L عريضًا بما يكفي لعرض التسمية دون اقتطاع.

---

## لماذا يعمل هذا النهج بأفضل شكل

* **سير عمل خطوة واحدة** – جميع العمليات تتم على نفس كائن `Workbook`، مما يتجنب عمليات الإدخال/الإخراج غير الضرورية.  
* **تنسيق شرطي** – استخدام `FormatConditionType.TIME_PERIOD` يسمح لـ Excel بمعالجة منطق التاريخ، وهو أكثر موثوقية من كتابة فحوصات تاريخ مخصصة في بايثون.  
* **تنسيق صريح** – ضبط `background_color` و `pattern` يضمن النتيجة البصرية عبر إصدارات Excel المختلفة.  
* **ضبط تلقائي بعد إدخال البيانات**  

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}