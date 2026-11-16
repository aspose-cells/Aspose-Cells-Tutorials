---
category: general
date: 2026-11-16
description: تعرّف على كيفية توسيع المصفوفة في Excel باستخدام Aspose.Cells ودوال المصفوفة
  الديناميكية ومخفض لامدا، ثم كتابة ملف Excel من C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: ar
lastmod: 2026-11-16
og_description: كيفية توسيع المصفوفة في Excel باستخدام Aspose.Cells، ودوال المصفوفة
  الديناميكية، ومخفض لامدا. تابع المثال الكامل بلغة C# لكتابة ملف Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: كيفية توسيع المصفوفة في إكسل باستخدام Aspose.Cells – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية توسيع المصفوفة في إكسل باستخدام Aspose.Cells
url: /ar/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية توسيع المصفوفة في Excel باستخدام Aspose.Cells

إذا كنت بحاجة إلى **كيفية توسيع المصفوفة** في ورقة عمل Excel من C#، فإن هذا الدرس يوضح الخطوات الدقيقة. ستقوم بإنشاء مصنف Excel، واستخدام دوال المصفوفة الديناميكية مثل `EXPAND` و `REDUCE`، وتطبيق **lambda** كمجمع، وأخيرًا **كتابة ملف Excel** إلى القرص. يعمل هذا النهج مع Aspose.Cells 23.10 أو أحدث ولا يتطلب تثبيت Excel يدويًا.

بنهاية هذا الدليل ستحصل على ملف `ExpandReduceDemo.xlsx` يعمل بالكامل ويظهر قوة صيغ المصفوفة الديناميكية في سياق برمجي.

## ما ستحتاجه

- .NET 6.0 (أو أي نسخة .NET يدعمها Aspose.Cells)
- حزمة Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)
- محرر شفرة أو بيئة تطوير (Visual Studio، VS Code، Rider، إلخ)

لا يلزم أي تداخل COM إضافي أو تثبيت Office لأن Aspose.Cells يتعامل مع تنسيق الملف داخليًا.

## الخطوة 1: إنشاء مصنف Excel

المهمة الأولى هي **إنشاء مصنف Excel** في الذاكرة. توفر Aspose.Cells الفئة `Workbook`، التي تمثل ملف XLSX كامل.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **لماذا هذا مهم:** إنشاء كائن `Workbook` يمنحك لوحة رسم نظيفة. ورقة العمل الافتراضية مُعدة مسبقًا، لذا لا تحتاج إلى إضافتها يدويًا ما لم ترغب في وجود أوراق متعددة.

## الخطوة 2: إدراج ثابت مصفوفة عمودي

يمكن لمحرك المصفوفة الديناميكية في Excel العمل مع ثوابت المصفوفة الحرفية. سنضع المصفوفة العمودية `{1;2;3;4;5}` في الخلية **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **نصيحة:** الفاصلة المنقوطة (`;`) تفصل الصفوف في الثابت، بينما الفاصلة (`,`) كانت ستفصل الأعمدة. هذا يعكس صياغة Excel نفسها.

## الخطوة 3: توسيع المصفوفة إلى مصفوفة

الآن نجيب على السؤال الأساسي – **كيفية توسيع المصفوفة** – باستخدام دالة `EXPAND`. الصيغة توسع المصفوفة ذات العمود الواحد إلى مصفوفة 5 صفوف × 2 أعمدة، بدءًا من **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **لماذا EXPAND؟** `EXPAND(source, rows, cols)` يجبر النطاق المصدر على احتلال الحجم المحدد، مع تعبئة الخلايا الفارغة إذا لزم الأمر. إنها الطريقة الأكثر وضوحًا لإنشاء مصفوفة أكبر من مصفوفة واحدة.

## الخطوة 4: تقليل المصفوفة باستخدام جامع lambda

دالة `REDUCE` تتكرر على نطاق وتجمع القيم باستخدام تعبير **lambda**. هنا نجمع كل قيمة عمود في عمود واحد، ونضع النتيجة في **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **كيفية استخدام lambda:** `LAMBDA(acc, val, acc+val)` تستقبل المجمع الحالي (`acc`) والقيمة التالية للخلية (`val`). تُعيد المجمع الجديد، مما يؤدي إلى حساب مجموع متراكم. هذا يوضح **كيفية استخدام lambda** في صيغ Excel من الكود.

## الخطوة 5: حساب الصيغ لتظهر النتائج

Aspose.Cells لا يقوم تلقائيًا بتقييم الصيغ عند تعيينها. استدعاء `CalculateFormula` يجبر المحرك على حساب كل صيغة في المصنف.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **ملاحظة:** إذا فتحت الملف المُولد في Excel، فستكون القيم مرئية بالفعل لأنها تم حسابها مسبقًا.

## الخطوة 6: كتابة ملف Excel إلى القرص

أخيرًا، **اكتب ملف Excel** باستخدام طريقة `Save`. اختر مجلدًا لديك صلاحية كتابة فيه.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### النتيجة المتوقعة

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **العمود B** و **C** يحتويان على مصفوفة 5 × 2 التي أنشأتها `EXPAND`.
- **الخلية D1** تُظهر `15`، مجموع جميع الأرقام، محسوبًا بواسطة صيغة `REDUCE` + **lambda**.

## الأسئلة الشائعة والحالات الخاصة

- **هل يمكنني توسيع إلى أعمدة أكثر مما يوفره المصدر؟**  
  نعم. `EXPAND` يملأ الأعمدة المفقودة بخلايا فارغة. نفس الأمر ينطبق على الصفوف.

- **ماذا لو كانت المصفوفة المصدر أفقية (`{1,2,3,4,5}`)؟**  
  `EXPAND` سيعامل المصدر كصف واحد؛ لا يزال بإمكانك تحديد عدد الصفوف والأعمدة لإعادة تشكيله.

- **هل يعمل `REDUCE` مع بيانات غير رقمية؟**  
  يجب أن تُعيد الدالة lambda قيمة متوافقة مع نوع المجمع. للدمج النصي يمكنك استخدام `LAMBDA(acc, val, acc & val)`.

- **هل أحتاج إلى استدعاء `CalculateFormula` لكل تعديل؟**  
  فقط عندما تحتاج القيم المحسوبة قبل الحفظ. سيعيد Excel حساب الصيغ عند الفتح إذا تخطيت ذلك.

## نصائح احترافية

- **الأداء:** للمصنفات الكبيرة، استدعِ `workbook.CalculateFormula` مرة واحدة بعد ضبط جميع الصيغ، بدلاً من استدعائه بعد كل خلية.
- **سلامة الإصدارات:** `EXPAND` و `REDUCE` متوفران في Excel 365 وما بعده. Aspose.Cells يطبقهما بغض النظر عن نسخة Excel المستهدفة لأن محرك الحساب مدمج.
- **تصحيح الصيغ:** استخدم `sheet.Cells["B1"].Formula` لقراءة السلسلة الدقيقة التي ضبطتها؛ يساعد ذلك عند بناء الصيغ ديناميكيًا.

## الخلاصة

أنت الآن تعرف **كيفية توسيع المصفوفة** في Excel باستخدام Aspose.Cells، وتستفيد من **دوال المصفوفة الديناميكية**، وتطبق **lambda** مع `REDUCE`، وت **تكتب ملف Excel** من C#. يمكن تعديل هذا المثال من البداية إلى النهاية لتناسب تحويلات بيانات أكثر تعقيدًا، مثل تحويل المصفوفات، المجاميع التراكمية، أو التجميعات المخصصة.

---

*الخطوات التالية:*  
- استكشف دوال ديناميكية أخرى مثل `FILTER`، `SORT`، و `UNIQUE`.  
- اجمع عدة تعبيرات `LAMBDA` لبناء دوال معرفة من قبل المستخدم قابلة لإعادة الاستخدام.  
- دمج توليد المصنف في واجهات برمجة تطبيقات ASP.NET Core لإنشاء تقارير في الوقت الفعلي.

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}