---
category: general
date: 2026-08-01
description: إنشاء مصنف إكسل باستخدام بايثون و Aspose.Cells – تعلم ضبط عرض الأعمدة
  تلقائيًا، تنسيق الخلايا حسب التاريخ، تعيين تنسيق تاريخ الخلية وتطبيق التنسيق الشرطي.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: ar
lastmod: 2026-08-01
og_description: إنشاء دفتر عمل Excel باستخدام Python على الفور. اتبع هذا الدليل لتعديل
  عرض الأعمدة تلقائيًا في Excel، وتنسيق الخلايا حسب التاريخ، وتعيين تنسيق تاريخ الخلية،
  وإتقان تنسيق الخلايا الشرطي باستخدام Aspose Cells.
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: إنشاء مصنف إكسل بايثون – خطوة بخطوة مع Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: إنشاء مصنف إكسل باستخدام بايثون – دليل كامل مع Aspose.Cells
url: /ar/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel باستخدام Python – دليل كامل مع Aspose.Cells

هل تساءلت يومًا كيف تنشئ سكريبتات **create Excel workbook python** تبدو مصقولة دون فتح Excel يدويًا؟ لست وحدك. سواء كنت تبني لوحة تقارير أو تقوم بأتمتة تصدير البيانات اليومية، فإن القدرة على إنشاء ملف Excel من Python تُغيّر قواعد اللعبة.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ لا يقتصر فقط على إنشاء دفتر عمل بل يوضح أيضًا **auto fit excel column**، **format cells by date**، **set cell date format**، وتطبيق **aspose cells conditional formatting**. في النهاية ستحصل على سكريبت مستقل يمكنك إدراجه في أي مشروع.

> **نصيحة احترافية:** Aspose.Cells for Python via .NET يتيح لك العمل مع ملفات Excel دون الاعتماد على COM، مما يجعله مثاليًا لحاويات Linux أو خطوط أنابيب CI.

## ما ستحتاجه

- **Python 3.8+** (الكود يعمل على أي نسخة حديثة)  
- **Aspose.Cells for Python via .NET** – تثبيت باستخدام `pip install aspose-cells`  
- مجلد يمكنك الكتابة فيه (سنسميه `YOUR_DIRECTORY`)  
- فهم أساسي لدوال وكائنات Python (لا تحتاج إلى معرفة عميقة بـ Excel)  

إذا كان لديك هذه المتطلبات بالفعل، عظيم—لنبدأ.

## الخطوة 1: إنشاء دفتر عمل Excel باستخدام Python – تهيئة دفتر العمل

أول شيء نقوم به هو إنشاء كائن دفتر عمل جديد. فكر فيه كقماش فارغ حيث يرسم كل عملية لاحقة عنصرًا جديدًا.

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **لماذا هذا مهم:** `Workbook()` ينشئ تمثيلًا في الذاكرة لملف `.xlsx`. من خلال الوصول إلى `worksheets[0]` نحصل على الورقة الافتراضية، جاهزة للبيانات والتنسيق.

## الخطوة 2: تحديد النطاق المستهدف واللون الأساسي – التحضير للتنسيق الشرطي

قبل إضافة أي منطق شرطي، نحتاج إلى نطاق سيستضيف القاعدة. النطاق `I19:K20` اختياري لكنه كبير بما يكفي لعرض عدة خلايا.

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

طريقة `add` تنشئ كائن التنسيق وتمنحه خلفية افتراضية، مما يجعل القاعدة اللاحقة بارزة.

## الخطوة 3: تنسيق شرطي باستخدام Aspose Cells – تطبيق قاعدة TIME_PERIOD لليوم السابق

الآن نصل إلى جوهر العرض: شرط **TIME_PERIOD** يبرز الخلايا التي تحتوي على تاريخ الأمس.

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **شرح:** `FormatConditionType.TIME_PERIOD` يخبر Aspose أننا نتعامل مع قاعدة تعتمد على التاريخ. بتعيين `time_period` إلى `YESTERDAY`، يقوم المحرك تلقائيًا بتقييم قيمة كل خلية مقابل اليوم السابق في التقويم.

## الخطوة 4: ملء تواريخ عينة – تعيين تنسيق تاريخ الخلية والتحقق من القاعدة

لرؤية القاعدة تعمل نحتاج إلى تواريخ فعلية. سنقوم أيضًا **set cell date format** حتى تظهر القيم كتواريخ قابلة للقراءة.

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

لاحظ كيف نستخدم نفس رقم **format cells by date** (`30`) لكلا الخليتين. هذا يضمن عرض التواريخ بشكل متسق، بغض النظر عن إعدادات اللغة للنظام.

## الخطوة 5: إضافة تسمية وصفية – جعل الورقة ذات شرح ذاتي

تسمية صغيرة تساعد أي شخص يفتح الملف على فهم ما تمثله الخلايا الملونة.

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## الخطوة 6: Auto Fit Excel Column – ضبط عرض الأعمدة تلقائيًا

عند توليد البيانات برمجيًا، غالبًا ما تبقى أعرض الأعمدة بالحجم الضيق الافتراضي. طريقة **auto fit excel column** توسعها بما يكفي لعرض المحتوى.

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **لماذا العمود 12؟** في الفهرسة التي تبدأ من الصفر، العمود `12` يطابق عمود Excel `L`. عدل الفهرس إذا غيرت التخطيط.

## الخطوة 7: حفظ دفتر العمل – تصديره إلى ملف حقيقي

أخيرًا، نحفظ كل شيء على القرص. علم `SaveFormat.XLSX` يضمن دفتر عمل حديث مبني على صيغة zip.

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### النتيجة المتوقعة

افتح `TimePeriodDemo.out.xlsx` في Excel (أو أي عارض) وسترى:

- الخلية **I19** مميزة باللون **الوردي** لأن تاريخها يطابق “الأمس”.  
- الخلية **K20** بدون تغيير، مما يوضح أن القاعدة الشرطية تجاهلت التواريخ خارج الفترة بشكل صحيح.  
- العمود **L** تم ضبط عرضه تلقائيًا بحيث لا يتم قطع تسمية “Yesterday”.

![مثال إنشاء دفتر عمل Excel باستخدام Python](/images/create_excel_workbook_python.png){: .center-image alt="مثال إنشاء دفتر عمل Excel باستخدام Python يظهر التنسيق الشرطي لتاريخ الأمس"}

## الاختلافات الشائعة وحالات الحافة

| الموقف | كيفية التعديل |
|-----------|---------------|
| **نطاق تاريخ مختلف** | Change `condition.time_period` to `TimePeriodType.TODAY`, `TimePeriodType.LAST_7_DAYS`, etc. |
| **شروط متعددة** | Call `conds.add_condition()` again and configure a new `FormatConditionType` (e.g., `FORMAT_CONDITION_TYPE.EXPRESSION`). |
| **تنسيق تاريخ مخصص** | Use `style_i19.number = 14` for `mm-dd-yy` or assign a custom format string via `style_i19.custom = "dd-mmm-yyyy"`. |
| **أوراق عمل كبيرة** | Wrap the `auto_fit_column` call in a try/except block to avoid performance hits on massive files. |
| **التشغيل في بيئة CI بدون واجهة** | No UI is needed; Aspose works entirely in memory, so you can generate the file in a Docker container without Excel installed. |

## ملخص – ما تم تغطيته

- **Create Excel workbook python** من الصفر باستخدام Aspose.Cells.  
- **Auto fit excel column** للحفاظ على مخرجاتك مرتبة.  
- **Format cells by date** و **set cell date format** لعرض متسق.  
- تطبيق **aspose cells conditional formatting** باستخدام النوع `TIME_PERIOD`.

## الخطوات التالية

إذا أتقنت الأساسيات، فكر في استكشاف:

- **Data bars, color scales, and icon sets** للحصول على تنسيق شرطي أكثر غنى.  
- **PivotTable generation** عبر `worksheet.pivot_tables.add()`.  
- **Exporting to PDF** باستخدام `workbook.save("report.pdf", SaveFormat.PDF)`.  

كل من هذه المواضيع يبني على المفاهيم الأساسية التي استخدمناها هنا، لذا ستشعر بالراحة.

---

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع توثيق Aspose.Cells for Python للمزيد من التفاصيل.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تعديل تلقائي للصفوف والأعمدة في Excel باستخدام Aspose.Cells Java لإدارة دفتر عمل سلس](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [إنشاء دفتر عمل Excel باستخدام Aspose.Cells في Java: دليل خطوة بخطوة](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [أتمتة عرض أعمدة Excel: تعديل تلقائي للأعمدة باستخدام Aspose.Cells for .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}