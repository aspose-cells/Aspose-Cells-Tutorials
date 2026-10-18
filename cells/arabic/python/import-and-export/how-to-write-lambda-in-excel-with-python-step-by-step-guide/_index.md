---
category: general
date: 2026-06-21
description: تعلم كيفية كتابة لامدا في إكسل باستخدام بايثون. يغطي هذا الدرس أيضًا
  إنشاء مصنف إكسل باستخدام بايثون وكيفية قراءة الخلايا باستخدام Aspose.Cells.
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: ar
og_description: كيفية كتابة دالة لامدا في إكسل باستخدام بايثون موضحًا. اتبع خطواتنا
  الواضحة لإنشاء دفتر عمل إكسل بايثون، وتطبيق BYROW، وقراءة نتائج الخلايا.
og_title: كيفية كتابة لامدا في إكسل باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: كيفية كتابة لامدا في إكسل باستخدام بايثون – دليل خطوة بخطوة
url: /ar/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية كتابة لامدا في إكسل باستخدام بايثون – دليل خطوة بخطوة

هل تساءلت يومًا **عن كيفية كتابة لامدا** في صيغة إكسل عندما تقوم بأتمتة الجداول من بايثون؟ لست وحدك. يواجه العديد من المطورين صعوبة في دمج قوة وظائف المصفوفات الديناميكية الجديدة في إكسل مع سير عمل مدفوع ببايثون. في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك ذلك بالضبط — وسنلمس أيضًا **إنشاء مصنف إكسل بايثون**، **كيفية قراءة الخلايا**، والنمط المفيد **كيفية الاستخدام BYROW**.

بنهاية هذا الدليل ستحصل على مصنف جديد، وصيغة BYROW تستفيد من لامدا، وطريقة بسيطة لجلب النتائج مرة أخرى إلى سكريبت بايثون الخاص بك. لا حاجة لأي إضافات إكسل إضافية، فقط Aspose.Cells for Python وقليل من الكود.

## المتطلبات المسبقة

قبل أن نغوص في التفاصيل، تأكد من أن لديك:

- Python 3.8 أو أحدث مثبتًا.
- حزمة `aspose-cells` (`pip install aspose-cells`).
- فهم أساسي لقوائم بايثون والدوال.
- (اختياري) بيئة تطوير متكاملة أو محرر نصوص تشعر بالراحة معه.

هذا كل شيء. إذا كان أي من هذه غير مألوف لك، توقف وقم بتثبيت الحزمة أولًا؛ باقي الخطوات ستعمل على أي منصة تدعم بايثون.

## إنشاء مصنف إكسل بايثون

أول شيء نحتاجه هو كائن مصنف نظيف. توفر لنا Aspose.Cells فئة `Workbook` التي تمثل ملف إكسل كامل في الذاكرة.

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

لماذا نبدأ بمصنف جديد؟ لأنه يضمن بيئة حتمية—لا صيغ مخفية، لا تنسيقات عشوائية، مجرد لوحة فارغة. هذا هو الأساس لأي درس **إنشاء مصنف إكسل بايثون**.

## ملء الورقة بالبيانات

بعد ذلك نقوم بملء جدول رقمي 5 × 3 يبدأ من الخلية **A1**. البيانات بسيطة عمدًا لتتمكن من رؤية العملية الحسابية بوضوح.

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

لاحظ كيف نستخدم `put_value` مع قائمة بايثون متداخلة؛ تقوم Aspose.Cells تلقائيًا بربط الصفوف والأعمدة لنا. إذا احتجت يومًا لاستيراد بيانات من ملف CSV أو قاعدة بيانات، ستستبدل `table_data` بذلك المصدر—ولا يتغير شيء آخر.

## كيفية كتابة لامدا في صيغة BYROW (بايثون)

الآن يأتي الجزء الشهي: **كيفية كتابة لامدا** التي سيقوم محرك إكسل بتقييمها. دالة إكسل `BYROW` تكرر كل صف من نطاق ما، وتغذيه إلى `LAMBDA` التي تزودها. في حالتنا نريد متوسط كل صف.

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

لنشرح ذلك:

- `BYROW(A1:C5, …)` يخبر إكسل بالنظر إلى كل صف في النطاق A1:C5.
- `LAMBDA(r, AVERAGE(r))` يعرّف دالة مجهولة (`r` هو مصفوفة الصف) تُعيد متوسط ذلك الصف.
- النتيجة تُسقّط تلقائيًا إلى D1:D5 لأن BYROW تُعيد مصفوفة.

ذلك السطر الواحد هو الجواب على **كيفية كتابة لامدا** للحسابات على مستوى الصفوف. يمكنك استبدال `AVERAGE` بـ `SUM` أو `MAX` أو أي تجميع آخر—فقط غيّر جسم اللامدا.

## إجبار حساب الصيغة

Aspose.Cells لا تُقيم الصيغ تلقائيًا عند تعيينها، لذا علينا أن نطلب منها إعادة الحساب.

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

إذا تخطيت هذه الخطوة، ستظل الخلايا في العمود D تحتوي على نص الصيغة، وليس على الأرقام المحسوبة. هذا هو الفخ الشائع عندما يستخدم الناس **كيفية الاستخدام BYROW** دون تفعيل عملية حساب.

## كيفية قراءة الخلايا بعد الحساب

أخيرًا، لنسترجع النتائج إلى بايثون. هذا يوضح **كيفية قراءة الخلايا** بطريقة تعمل مع أي ناتج صيغة.

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

قائمة استيعاب سريعة (list‑comprehension) تتنقل عبر الصفوف الخمسة، تأخذ قيمة كل خلية عبر `.value`، وتخزنها في `row_averages`. القائمة المطبوعة تؤكد أن لامدانا عملت كما هو متوقع.

### نصيحة احترافية
إذا احتجت لقراءة كتلة كبيرة من النتائج، استخدم `worksheet.cells.get_range("D1:D5").value` لجلب المصفوفة بالكامل في استدعاء واحد—أسرع بكثير للأوراق الكبيرة.

## استخدام دالة لامدا في إكسل لحساب متوسطات الصفوف (السكريبت الكامل)

بجمع كل ما سبق، إليك السكريبت الكامل الجاهز للتنفيذ:

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

عند تشغيل هذا السكريبت سيطبع:

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

هذا هو دورة الحياة الكاملة: **إنشاء مصنف إكسل بايثون**، ملء البيانات، **كيفية الاستخدام BYROW**، **كيفية كتابة لامدا**، وأخيرًا **كيفية قراءة الخلايا**.

## الحالات الحدية والأسئلة الشائعة

- **ماذا لو لم تكن بياناتي متصلة؟**  
  BYROW يعمل على أي نطاق مستطيل. إذا كان هناك فراغات، ما عليك سوى الإشارة إلى نطاق أكبر ودع اللامدا تتجاهل الخلايا الفارغة (`AVERAGEIF(r, "<>")`).

- **هل يمكنني تمرير أكثر من وسيط واحد إلى اللامدا؟**  
  نعم. الوسيط الأول هو دائمًا الصف (أو العمود لـ `BYCOL`). يمكن تمرير وسائط إضافية بعد النطاق، مثل `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`.

- **هل هذا متوافق مع إصدارات إكسل القديمة؟**  
  BYROW و LAMBDA متاحان بدءًا من Excel 365 (المصفوفات الديناميكية). إذا كنت تحتاج دعمًا للنسخ القديمة، سيتعين عليك محاكاة المنطق باستخدام VBA أو أعمدة مساعدة متعددة.

- **هل يجب حفظ المصنف على القرص؟**  
  ليس لهذا العرض التجريبي، لكن يمكنك استدعاء `workbook.save("output.xlsx")` إذا أردت ملفًا فعليًا.

## الخلاصة

غطينا **كيفية كتابة لامدا** في صيغة إكسل BYROW من بايثون، وعرضنا سير عمل كامل **إنشاء مصنف إكسل بايثون**، وأظهرنا أبسط طريقة لـ **كيفية قراءة الخلايا** بعد الحساب. باستخدام Aspose.Cells تتجنب أي مشاكل COM interop، والنمط نفسه يمكن توسيعه لآلاف الصفوف مع تغييرات قليلة في الكود.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال `AVERAGE` بـ `MEDIAN`، أضف منطقًا شرطيًا داخل اللامدا، أو أنشئ مجموعة تقارير كاملة تلقائيًا. الجمع بين بايثون ودالات إكسل الحديثة يفتح عالمًا من إمكانيات الأتمتة المدفوعة بالبيانات.

هل لديك أسئلة أو تريد مشاركة حيل لامدا الخاصة بك؟ اترك تعليقًا أدناه، وبرمجة سعيدة!  

![how to write lambda in Excel using Python](image.png){alt="كيفية كتابة لامدا في إكسل باستخدام بايثون"}

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Load an Excel Workbook Without Defined Names Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}