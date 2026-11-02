---
category: general
date: 2026-07-14
description: إنشاء كود بايثون لمصنف إكسل يضبط لون خلفية الخلية، يبرز الخلايا بناءً
  على نطاق التاريخ، ويحفظ المصنف بصيغة XLSX في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: ar
lastmod: 2026-07-14
og_description: أنشئ دفتر عمل Excel باستخدام Python فورًا. تعلّم كيفية ضبط لون خلفية
  الخلية، وتظليل الخلايا بناءً على نطاق التاريخ، وحفظ دفتر العمل بصيغة XLSX باستخدام
  Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: إنشاء دفتر عمل إكسل باستخدام بايثون – تنسيق شرطي خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: إنشاء مصنف إكسل بايثون – دليل كامل مع التنسيق الشرطي
url: /ar/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel باستخدام Python – دليل كامل مع التنسيق الشرطي

هل تساءلت يومًا كيف تُنشئ سكريبتات **create excel workbook python** تبدو مصقولة دون الحاجة لفتح Excel يدويًا؟ لست وحدك. في العديد من المشاريع المعتمدة على البيانات نحتاج إلى توليد جداول بيانات، تلوين الخلايا، وحتى وضع علامات على التواريخ التي تقع داخل نطاق معين—كل ذلك من خلال كود Python نقي.

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ **creates an Excel workbook python** باستخدام مكتبة Aspose.Cells، **sets cell background color**، يطبق **conditional formatting based on date**، وأخيرًا **saves workbook as xlsx**. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي خط أنابيب أتمتة.

## ما ستتعلمه

- كيفية تهيئة دفتر عمل والحصول على الورقة الأولى.  
- دالة مساعدة تضيف مجموعة تنسيق شرطي لأي نطاق خلايا.  
- استخدام **conditional formatting based on date** لتسليط الضوء على إدخالات الأمس.  
- ضبط عرض الأعمدة للحصول على تخطيط أنيق.  
- حفظ النتيجة باستخدام **save workbook as xlsx**.  

لا تحتاج إلى تثبيت Excel خارجي—Aspose.Cells يتولى كل شيء في الذاكرة.

## المتطلبات المسبقة

- Python 3.8+ مثبت.  
- حزمة `aspose-cells` (`pip install aspose-cells`).  
- إلمام أساسي بدوال Python وكائنات datetime.  

إذا لم تستخدم Aspose.Cells من قبل، فكر فيها كـ API قوي مكتوب بالكامل بلغة Python يحاكي نموذج كائنات Excel. إنها مثالية للتوليد على الخادم حيث لا يتوفر حزمة Office.

## الخطوة 1: تهيئة دفتر العمل (Create Excel Workbook Python)

أولًا: نحتاج إلى **create excel workbook python**. هذه الخطوة تنشئ كائن دفتر عمل فارغ وتوجهنا إلى الورقة الافتراضية.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **لماذا هذا مهم:** فئة `Workbook` هي نقطة الدخول لكل عملية Excel. بإنشائها برمجيًا نتجنب أي تعامل يدوي مع الملفات.

## الخطوة 2: دالة مساعدة لإضافة مجموعة تنسيق شرطي (Set Cell Background Color)

التنسيق الشرطي يعيش داخل *مجموعة* مرتبطة بنطاق. لنغلف هذا الروتين بدالة مساعدة صغيرة تسمح أيضًا بـ **set cell background color** للنطاق بأكمله.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **نصيحة احترافية:** استخدام دالة مساعدة يبقي تدفق البرنامج الرئيسي نظيفًا ويسهل إعادة استخدام المنطق نفسه لأكثر من نطاق.

## الخطوة 3: تطبيق تنسيق شرطي بناءً على التاريخ (Highlight Cells Based on Date Range)

الآن سنقوم فعليًا بـ **highlight cells based on date range**. يركز المثال على “الأمس” لكن يمكنك استبدال `TimePeriodType.YESTERDAY` بـ `TODAY` أو `LAST_WEEK` وغيرها.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **ما الذي يحدث؟**  
> 1. نُعطي النطاق كله خلفية خضراء محايدة.  
> 2. ثم نضيف شرط `TIME_PERIOD` يغيّر التعبئة إلى اللون الوردي **فقط** عندما يساوي تاريخ الخلية تاريخ الأمس.  
> 3. تعداد `TimePeriodType` يختصر حساب التاريخ، لذا لا تحتاج إلى كتابة منطق مخصص.

## الخطوة 4: ملء تواريخ تجريبية (So the Rule Can Be Evaluated)

لرؤية القاعدة تعمل، سنضع بعض التواريخ في الورقة. أحدها يقع داخل نافذة “الأمس”، والآخر لا.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **ملاحظة حالة حافة:** إذا كان دفتر العمل سيفتح في إعدادات إقليمية مختلفة، فكر في استخدام `date_style.custom = "dd‑mm‑yyyy"` لضمان عرض موحد.

## الخطوة 5: ترتيب التخطيط (Auto‑Fit Columns)

جدول مضغوط يبدو غير مهني. لنـ **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **لماذا auto‑fit؟** يضمن أن أي تسميات أو تواريخ طويلة تكون مرئية بالكامل، وهو أمر مهم خاصةً عند مشاركة الملف مع أصحاب المصلحة غير التقنيين.

## الخطوة 6: حفظ دفتر العمل (Save Workbook As XLSX)

أخيرًا، نـ **save workbook as xlsx** إلى الموقع الذي تختاره. ثابت `SaveFormat.XLSX` يخبر Aspose.Cells بكتابة الصيغة الحديثة OpenXML.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **النتيجة المتوقعة:**  
> - الخلايا I19 و K20 تحتوي على تواريخ.  
> - I19 (الأمس) مميزة بالوردي، بينما K20 تبقى خضراء.  
> - العمود L يتوسع تلقائيًا ليتسع للتسمية “Yesterday”.  

إذا فتحت `TimePeriodDemo.xlsx` في Excel، سيظهر التنسيق الشرطي مُطبقًا بالفعل—دون الحاجة إلى خطوات إضافية.

---

![ورقة Excel تُظهر تاريخ الأمس المميز باللون الوردي](https://example.com/images/excel-demo.png "لقطة شاشة للملف Excel المُولد مع الخلايا المميزة")

*الصورة أعلاه توضح دفتر العمل النهائي؛ لاحظ التمييز الوردي للخلية التي تحتوي على تاريخ الأمس.*

## ملخص: ما أنجزناه

- **Created an Excel workbook python** من الصفر باستخدام Aspose.Cells.  
- **Set cell background color** لنطاق كامل لإعطاء الورقة إشارة بصرية.  
- تطبيق **conditional formatting based on date** لتعليم إدخالات الأمس تلقائيًا.  
- **Saved workbook as xlsx**، جاهز للتوزيع أو المعالجة الإضافية.  

تم إنجاز كل ذلك في أقل من 60 سطرًا من Python، والكود يعمل على أي منصة تدعم بيئة تشغيل Aspose.Cells.

## الخطوات التالية والمواضيع ذات الصلة

إذا وجدت هذا مفيدًا، قد ترغب أيضًا في استكشاف:

- **set cell background color** للصفوف بالكامل بناءً على قيم الحالة (مثل “Completed”، “Pending”).  
- استخدام **highlight cells based on date range** لإنشاء نوافذ متحركة (آخر 7 أيام، الشهر الحالي).  
- التصدير إلى صيغ أخرى مثل **CSV** أو **PDF** باستخدام `SaveFormat.CSV` أو `SaveFormat.PDF`.  
- إضافة **charts** برمجيًا لتصوير البيانات التي قمت بتنسيقها.  

لا تتردد في تعديل منطق التاريخ، تغيير لوحة الألوان، أو توسيع النطاق ليشمل أعمدة كاملة. النمط يبقى نفسه: إنشاء دفتر عمل، إرفاق مجموعة تنسيق شرطي، تعريف القاعدة، ثم الحفظ.

هل لديك أسئلة حول حالة استخدام محددة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}