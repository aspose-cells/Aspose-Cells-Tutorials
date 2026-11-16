---
category: general
date: 2026-11-16
description: تعلم كيفية استخدام WRAPCOLS في C# لتقسيم صف إلى أعمدة، وأتمتة مصنف Excel،
  وحساب الصيغ، وحفظ ملف Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: ar
lastmod: 2026-11-16
og_description: كيفية استخدام WRAPCOLS في C# لتقسيم صف إلى أعمدة، أتمتة مصنف Excel،
  تشغيل حساب الصيغ، وحفظ ملف Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: كيفية استخدام WRAPCOLS في C# – تقسيم الصفوف، حساب الصيغ، وحفظ ملفات Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: كيفية استخدام WRAPCOLS لتقسيم صف إلى أعمدة في C#
url: /ar/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS لتقسيم صف إلى أعمدة في C#

إذا كنت بحاجة إلى **how to use WRAPCOLS** في مشروع C#، فإن هذا الدليل يوضح لك حلاً كاملاً وقابلاً للتنفيذ. ستتعرف على كيفية تقسيم صف إلى أعمدة، أتمتة مصنف Excel، تشغيل حساب صيغ Excel، وأخيرًا حفظ ملف Excel بأسلوب C#.

العمل مع Excel برمجيًا يعني غالبًا التعامل مع مجموعات بيانات كبيرة، وتتيح لك دالة `WRAPCOLS` إعادة تشكيل صف واحد إلى مصفوفة دون الحاجة إلى حلقات يدوية. تغطي الخطوات أدناه كل ما تحتاجه—من إنشاء المصنف إلى إخراج الملف النهائي—حتى تتمكن من دمج التقنية في أي تطبيق .NET.

## ما يغطيه هذا الدرس

* إنشاء مصنف جديد والوصول إلى ورقة العمل الأولى.  
* ملء صف بقيم متسلسلة (1‑20).  
* تطبيق صيغة Excel `WRAPCOLS` لتقسيم الصف إلى كتل من 5 أعمدة.  
* تشغيل **excel formula calculation** حتى يصبح الناتج جزءًا من الورقة.  
* استخدام **save excel file c#** لكتابة المصنف إلى القرص.  

لا يتطلب أي إعداد خارجي بخلاف مكتبة Aspose.Cells لـ .NET (أو أي API متوافق يدعم `WRAPCOLS`). في نهاية الدليل ستحصل على ملف باسم `WrapColsDemo.xlsx` يحتوي على أربعة صفوف من خمسة أعمدة لكل منها، مشتقة من البيانات الأصلية ذات الصف الواحد.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Core 3.1 و .NET Framework 4.7+).  
* إشارة إلى **Aspose.Cells** (متاحة عبر NuGet: `Install-Package Aspose.Cells`).  
* إلمام أساسي بصياغة C# وصيغ Excel.  

> **نصيحة احترافية:** إذا كنت تفضل بديلًا مجانيًا، فإن مكتبة EPPlus مفتوحة المصدر تدعم أيضًا الصيغ المخصصة، لكن `WRAPCOLS` مدمجة فقط في المكتبات التي تنفّذ محرك حساب Excel الكامل مثل Aspose.Cells.

## الخطوة 1: إنشاء مصنف جديد والحصول على ورقة العمل الأولى

العملية الأولى هي إنشاء كائن `Workbook` والحصول على ورقة العمل الافتراضية. يمثل هذا الكائن ملف Excel بالكامل في الذاكرة.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

إنشاء المصنف برمجيًا هو الأساس لمهام **automate excel workbook**. تسمح لك إشارة `Worksheet` بالتعامل مع الخلايا مباشرة.

## الخطوة 2: ملء الصف الأول بالقيم 1‑20

بعد ذلك، املأ الخلايا `A1` حتى `T1` بالأرقام من 1 إلى 20. حلقة `for` بسيطة تكتب كل قيمة في الفهرس المناسب للعمود.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

لماذا نكتب القيم برمجيًا؟ يضمن ذلك أن يعمل العرض التوضيحي على أي جهاز دون إدخال بيانات يدوي، وهو أمر أساسي عندما **automate excel workbook** في عمليات الدفعات.

## الخطوة 3: تطبيق دالة WRAPCOLS لتقسيم الصف إلى كتل من 5 أعمدة

الآن نستخدم صيغة Excel `WRAPCOLs`. تأخذ نطاق المصدر وعدد الأعمدة، ثم تُعيد مصفوفة ثنائية الأبعاد "تلف" البيانات المصدر إلى عدد الأعمدة المحدد.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

وضع الصيغة في الخلية `A2` يخبر Excel ببدء الإخراج في الصف الثاني. النتيجة ستكون مصفوفة 4 × 5 لأن 20 عنصرًا مقسومة على 5 أعمدة تُنتج أربعة صفوف.

### كيف تعمل WRAPCOLS

* **نطاق المصدر** – `A1:T1` يحتوي على القيم الـ20 الأصلية.  
* **عدد الأعمدة** – `5` يخبر Excel بإنشاء خمسة أعمدة لكل صف.  
* **النتيجة** – Excel يملأ الخلايا `A2:E5` بالبيانات الملتفة تلقائيًا.

إذا احتجت يومًا إلى **split row into columns** بحجم كتلة مختلف، ما عليك سوى تغيير الوسيط الثاني. على سبيل المثال، `WRAPCOLS(A1:T1,4)` سيُنتج خمسة صفوف من أربعة أعمدة لكل منها.

## الخطوة 4: حساب الصيغ حتى يتم تجسيد نتيجة WRAPCOLS

تظل الصيغة المضافة حديثًا غير مُقيمة حتى يتم تشغيل محرك الحساب. باستدعاء `CalculateFormula()`، تضمن أن خطوة **excel formula calculation** تكتب القيم الفعلية في ورقة العمل.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

تشغيل الحساب أمر حاسم عندما تقوم لاحقًا بـ **save excel file c#** لأن الملف المحفوظ يجب أن يحتوي على القيم المحسوبة، وليس مجرد نص الصيغة. بدون هذه الخطوة، سيظهر في المصنف المحفوظ `#N/A` أو الصيغة الخام بدلاً من الأرقام المتوقعة.

## الخطوة 5: حفظ المصنف إلى القرص

أخيرًا، احفظ المصنف باستخدام طريقة `Save`. يمكنك تحديد أي مسار ملف صالح؛ المثال يستخدم دليلًا نائبًا يجب استبداله بالمسار الخاص بك.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

استدعاء `Save` يوضح **save excel file c#** بأبسط صوره. تختار Aspose.Cells تلقائيًا تنسيق XLSX بناءً على امتداد الملف. إذا كنت تحتاج ملفًا أقدم بامتداد `.xls`، غير الامتداد وفقًا لذلك.

### النتيجة المتوقعة

افتح `WrapColsDemo.xlsx` وسترى:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

تم **split row into columns** للصف الأصلي عبر أربعة صفوف، كل منها يحتوي على خمسة أعمدة.

## الكود الكامل

جمع جميع الخطوات معًا ينتج برنامجًا صغيرًا ومتكاملًا:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

انسخ الكود إلى مشروع وحدة تحكم جديد، استعد حزمة NuGet الخاصة بـ Aspose.Cells، وشغّله. سيُنشئ البرنامج ملف Excel على سطح المكتب في ثوانٍ.

## الاختلافات الشائعة والحالات الحدية

| الحالة | التعديل |
|-----------|------------|
| **حجم كتلة مختلف** | غير `WRAPCOLS(A1:T1,5)` إلى `WRAPCOLS(A1:T1, n)` حيث `n` هو عدد الأعمدة المطلوب. |
| **عدة صفوف مصدر** | استخدم `WRAPCOLS(A1:A10,5)` لتلف نطاق عمودي إلى مصفوفة من 5 أعمدة. |
| **نطاق مصدر ديناميكي** | كوّن سلسلة العنوان في C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) قبل تعيين الصيغة. |
| **أوراق عمل كبيرة** | استدعِ `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` لتجاوز الخلايا التي تسبب أخطاء وتحسين الأداء. |
| **حفظ كـ CSV** | استبدل `workbook.Save(outputPath)` بـ `workbook.Save(outputPath, SaveFormat.Csv)`. |

تظهر هذه الاختلافات أن نمط **how to use wrapcols** يمكن تكييفه للعديد من سيناريوهات إعادة تشكيل البيانات.

## نصائح استكشاف الأخطاء وإصلاحها

* **الصيغة غير مُقيمة** – تأكد من استدعاء `workbook.CalculateFormula()` *بعد* تعيين الصيغة. تخطي هذه الخطوة يترك الخلية بنص `WRAPCOLS` الخام.  
* **رفض الوصول إلى الملف** – تحقق من وجود الدليل الهدف وأن العملية لديها صلاحيات كتابة. استخدام `Environment.SpecialFolder.Desktop` يجنب معظم مشاكل الصلاحيات.  
* **عدد الصفوف غير صحيح** – أعد فحص الوسيط الثاني لـ `WRAPCOLS`. هو يحدد عدد الأعمدة، وليس عدد الصفوف؛ فالصفوف تُستنتج من إجمالي خلايا المصدر مقسومة على عدد الأعمدة.

## الخلاصة

أنت الآن تعرف **how to use WRAPCOLS** في C# لتقوم بـ **split row into columns**، وتُنشئ **automate excel workbook** بالكامل، وتُجري **excel formula calculation**، وتُنفّذ **save excel file c#** بكود واحد نظيف. تُزيل هذه التقنية عمليات النسخ‑اللصق اليدوية وتُوسّع بسهولة لخطوط أنابيب تحويل البيانات الكبيرة.

### الخطوات التالية

* استكشف وظائف المصفوفات الديناميكية الأخرى مثل `SEQUENCE` و `FILTER` و `UNIQUE` لتثري مجموعة أدوات أتمتة Excel الخاصة بك.  
* اجمع بين `WRAPCOLS` وواجهات برمجة تطبيقات إنشاء المخططات لإنتاج تقارير جاهزة للنشر.  
* دمج الكود في خدمة خلفية تعالج تحميلات CSV وتُخرج ملفات Excel مُعاد تشكيلها للتحليلات اللاحقة.

لا تتردد في تجربة نطاقات مصدر مختلفة وعدد أعمدة مختلف—عدّل الصيغة، أعد تشغيل الحساب، وشاهد المصنف يتحدّث فورًا. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}