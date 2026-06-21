---
category: general
date: 2026-06-21
description: إنشاء دليل Python لملف عمل Excel يوضح كيفية استخدام دالة MAP وlambda
  لتحويل السلسيوس إلى فهرنهايت بسرعة.
draft: false
keywords:
- create excel workbook python
- convert celsius to fahrenheit
- use map function
- how to use map
- how to use lambda
language: ar
og_description: أنشئ دفتر عمل Excel باستخدام Python وتعلم كيفية استخدام دالة MAP مع
  lambda لتحويل السيلسيوس إلى فهرنهايت في دقائق.
og_title: إنشاء دفتر عمل إكسل باستخدام بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  headline: Create Excel Workbook Python – Full Guide
  type: TechArticle
- description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  name: Create Excel Workbook Python – Full Guide
  steps:
  - name: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
    text: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
  - name: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
    text: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
  - name: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
    text: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
  - name: Adding styling (fonts, borders) via Aspose’s rich formatting API.
    text: Adding styling (fonts, borders) via Aspose’s rich formatting API.
  - name: Initialize a workbook.
    text: Initialize a workbook.
  - name: Write raw data.
    text: Write raw data.
  - name: Apply a MAP‑based formula.
    text: Apply a MAP‑based formula.
  - name: Force calculation.
    text: Force calculation.
  - name: Pull the results back into Python.
    text: Pull the results back into Python.
  type: HowTo
- questions:
  - answer: Just extend the range in the `put_value` call and adjust the list comprehension
      range accordingly. The MAP formula will automatically expand if you reference
      a larger range.
    question: What if I have more than four rows?
  - answer: Absolutely. Replace the lambda body with any arithmetic you need, e.g.,
      `LAMBDA(c, c*2)` for a simple doubling operation.
    question: Can I use MAP with other conversions?
  - answer: The library offers a free evaluation mode, but for production use you’ll
      want a proper license to avoid watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: No, MAP is part of the dynamic array functions introduced in Excel 365.
      If you target legacy Excel, you’d fall back to traditional copy‑down formulas.
    question: Is the MAP function available in older Excel versions?
  type: FAQPage
tags:
- python
- excel
- aspose-cells
- data conversion
title: إنشاء دفتر عمل إكسل بايثون – دليل كامل
url: /ar/python/import-and-export/create-excel-workbook-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel باستخدام Python – دليل شامل

هل تساءلت يوماً كيف يمكنك **create Excel workbook python**‑style دون فتح Excel بنفسك؟ ربما تحتاج إلى تحويل قائمة درجات الحرارة من سيلسيوس إلى فهرنهايت في الوقت الفعلي، ولا ترغب في نسخ‑لصق الصيغ يدوياً. في هذا الدرس سنحل هذه المشكلة بالضبط: ستتعلم كيفية إنشاء ملف Excel، وإدخال عمود من بيانات السيلسيوس، ثم **convert celsius to fahrenheit** باستخدام صيغة أنيقة تعتمد على **دالة MAP** و**lambda**.

لماذا هذا مهم؟ أتمتة الجداول توفر الوقت، وتقلل الأخطاء البشرية، وتجعل دمج Excel في خطوط البيانات الكبيرة أمراً بسيطاً. بالإضافة إلى ذلك، مع Aspose.Cells for Python ستحصل على كامل إمكانيات Excel دون الحاجة إلى COM الثقيل. هل أنت مستعد؟ لنبدأ.

## ما ستحتاجه

- Python 3.9+ (أي نسخة حديثة تعمل)
- حزمة `aspose-cells` مثبتة (`pip install aspose-cells`)
- فهم أساسي لقوائم Python والدوال
- لا يلزم أي خبرة سابقة في Excel؛ سنقوم بإنشاء دفتر العمل لك

إذا كان لديك كل ما سبق، فأنت جاهز. وإلا، خذ لحظة لتثبيت المكتبة—ستجد أنها تستحق العناء.

![create excel workbook python example](excel_workbook.png)

*نص بديل للصورة: مثال على إنشاء دفتر عمل Excel باستخدام Python يظهر جدولاً مملوءاً*

## الخطوة 1: إنشاء دفتر عمل Excel في Python

أول شيء يجب القيام به هو **create excel workbook python** باستخدام Aspose.Cells. فكر في دفتر العمل كدفتر ملاحظات جديد حيث كل ورقة عمل هي صفحة يمكنك الكتابة عليها.

```python
import aspose.cells as cells

# Initialize a new workbook – this is our blank Excel file
wb = cells.Workbook()

# Grab the first worksheet (index 0) to start populating data
ws = wb.worksheets[0]
```

*لماذا هذا مهم*: إنشاء كائن `Workbook()` يمنحك تمثيلاً في الذاكرة لملف `.xlsx`. لا توجد عمليات إدخال/إخراج على القرص بعد، مما يبقي الأمور سريعة.

## الخطوة 2: ملء العمود A بدرجات السيلسيوس

الآن بعد أن لدينا ورقة، لنضع بعض قيم السيلسيوس في العمود **A**. سنستخدم طريقة `put_value`، التي تقبل قائمة Python وتكتبها مباشرةً في نطاق الخلايا.

```python
# Write a list of Celsius temperatures into cells A1:A4
ws.cells["A1:A4"].put_value([0, 20, 100, -10])
```

*نصيحة محترف*: سلسلة النطاق `"A1:A4"` مرنة—إذا قمت بتوسيع القائمة لاحقاً، فقط عدل النطاق أو استخدم عنواناً ديناميكياً.

## الخطوة 3: تطبيق MAP مع LAMBDA لتحويل كل قيمة سيلسيوس إلى فهرنهايت

هنا يحدث السحر. **دالة MAP** (الجديدة في Excel 365) تتيح لك تطبيق **lambda** على كل عنصر في مصفوفة. في حالتنا، المصفوفة هي `A1:A4`، والـ lambda تقوم بالتحويل الكلاسيكي `c * 9/5 + 32`.

```python
# Set the formula in B1 that maps each Celsius value to Fahrenheit
ws.cells["B1"].formula = "=MAP(A1:A4, LAMBDA(c, c*9/5 + 32))"
```

*كيف تعمل*:  
- `MAP(array, LAMBDA(parameter, expression))` تتكرر على `array`.  
- `c` هو المتغير المؤقت لكل قيمة سيلسيوس.  
- التعبير `c*9/5 + 32` يُعيد ما يعادلها بالفهرنهايت.

إذا كنت جديداً على **how to use map** في Excel، فكر فيها كدالة `map()` المدمجة في Python ولكن على شكل صيغة ورقة عمل. إنها تلغي الحاجة لسحب الصيغ يدوياً.

## الخطوة 4: حساب الصيغة لتصبح النتائج ملموسة

Aspose.Cells لا يقوم بتقييم الصيغ تلقائياً إلا إذا طلبت ذلك. استدعاء `calculate_formula()` يجبر المحرك على حساب نتيجة MAP وتخزين القيم في العمود **B**.

```python
# Force calculation – this writes the computed Fahrenheit values into the cells
wb.calculate_formula()
```

*حالة حافة*: إذا قمت بتعديل عمود السيلسيوس لاحقاً، ستحتاج إلى تشغيل `calculate_formula()` مرة أخرى، أو ضبط `calc_mode` للدفتر إلى الوضع التلقائي.

## الخطوة 5: استرجاع وعرض قيم الفهرنهايت من العمود B

أخيراً، لنستخرج الأرقام المحسوبة إلى Python ونطبعها. هذا يوضح **how to use lambda** برمجياً.

```python
# Extract the Fahrenheit values from B1:B4 into a Python list
fahrenheit = [ws.cells[f"B{i}"].value for i in range(1, 5)]
print(fahrenheit)
```

**الناتج المتوقع**

```
[32.0, 68.0, 212.0, 14.0]
```

إذا رأيت هذه الأرقام، تهانينا—لقد نجحت في **create excel workbook python**‑style، ملأته، واستخدمت **use map function** مع **lambda** لتقوم بـ **convert celsius to fahrenheit**.

## أسئلة شائعة ومشكلات محتملة

- **ماذا لو كان لدي أكثر من أربعة صفوف؟**  
  فقط قم بتمديد النطاق في استدعاء `put_value` واضبط نطاق الفهم القائم على القائمة وفقاً. صيغة MAP ستمتد تلقائياً إذا أشرت إلى نطاق أكبر.

- **هل يمكنني استخدام MAP لتحويلات أخرى؟**  
  بالتأكيد. استبدل جسم الـ lambda بأي عملية حسابية تحتاجها، مثلاً `LAMBDA(c, c*2)` لتضاعف القيمة ببساطة.

- **هل أحتاج إلى رخصة لـ Aspose.Cells؟**  
  المكتبة توفر وضع تقييم مجاني، لكن للاستخدام الإنتاجي ستحتاج إلى رخصة صحيحة لتجنب العلامات المائية.

- **هل دالة MAP متوفرة في إصدارات Excel القديمة؟**  
  لا، MAP جزء من الدوال الديناميكية التي تم تقديمها في Excel 365. إذا كنت تستهدف إصدارات Excel القديمة، ستحتاج إلى الاعتماد على صيغ النسخ التقليدية.

## توسيع المثال – الخطوات التالية

الآن بعد أن وضّحنا سير العمل الأساسي، يمكنك تجربة ما يلي:

1. **how to use map** لتحويلات متعددة الأعمدة، مثل تحويل درجات الحرارة وتطبيق التقريب في خطوة واحدة.  
2. **how to use lambda** لإدراج منطق شرطي: `LAMBDA(c, IF(c<0, "below freezing", c*9/5+32))`.  
3. حفظ دفتر العمل على القرص: `wb.save("temperatures.xlsx")`.  
4. إضافة تنسيق (خطوط، حدود) عبر واجهة التنسيق الغنية في Aspose.  

كل من هذه الأفكار يبنى على الأساس نفسه الذي وضعناه، مما يبقي الكود مختصراً مع فتح إمكانيات أتمتة قوية للجداول.

## الخلاصة

استعرضنا العملية الكاملة لـ **create excel workbook python** من الصفر، ملأناها ببيانات السيلسيوس، ثم **convert celsius to fahrenheit** باستخدام **دالة MAP** وتعبير **lambda**. الخطوات كانت:

1. تهيئة دفتر العمل.  
2. كتابة البيانات الخام.  
3. تطبيق صيغة تعتمد على MAP.  
4. إجبار الحساب.  
5. سحب النتائج إلى Python.

مع هذه الوصفة في صندوق أدواتك، يصبح أتمتة خطوط البيانات المرتكزة على Excel أمراً بسيطاً. لا تتردد في تعديل الـ lambda، ربط عدة استدعاءات MAP، أو حتى دمج دفتر العمل في خدمة ويب. السماء هي الحد.

هل لديك تحويل آخر في ذهنك؟ اترك تعليقاً، ولنستكشف معاً. Happy coding!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}