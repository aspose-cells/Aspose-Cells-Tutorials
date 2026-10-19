---
category: general
date: 2026-06-27
description: كيفية استخدام wrapcols و wrap rows في Excel باستخدام C#. تعلم إنشاء مصنف
  Excel باستخدام C# وإعادة حساب صيغ Excel مع مثال خطوة بخطوة.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: ar
og_description: كيفية استخدام wrapcols و wrap rows في Excel باستخدام C#. يوضح هذا
  الدليل كيفية إنشاء مصنف Excel باستخدام C# وإعادة حساب صيغ Excel في دقائق.
og_title: كيفية استخدام wrapcols في C# – دليل شامل لتغليف Excel
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية استخدام wrapcols في C# – دليل كامل مع Excel WRAPROWS وإعادة حساب الصيغ
url: /ar/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام wrapcols في C# – دليل كامل مع Excel WRAPROWS وإعادة حساب الصيغ

هل تساءلت يومًا **how to use wrapcols** عندما تحتاج إلى إعادة تشكيل قائمة طويلة إلى شبكة مرتبة؟ ربما جربت حيلة النسخ‑اللصق اليدوية، لكنها بطيئة وعرضة للأخطاء، وبصراحة، مزعجة. الخبر السار؟ يمكن لـ `WRAPCOLS` في Excel (وأخيه `WRAPROWS`) القيام بالعمل الشاق نيابةً عنك—*ويمكنك* تشغيلهما من كود C#.

في هذا الدرس سنستعرض إنشاء مصنف Excel في C#، وتطبيق `WRAPCOLS` و `WRAPROWS`، وأخيرًا **recalculate excel formulas** حتى تظهر البيانات المغلفة فورًا. في النهاية ستحصل على مقطع جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

- كيفية **create excel workbook c#** باستخدام مكتبة Aspose.Cells (بدون الحاجة إلى COM interop).
- الصياغة الدقيقة لدالة `WRAPCOLS` وكيف تختلف عن `WRAPROWS`.
- لماذا يجب عليك **recalculate excel formulas** بعد إدراج الدوال، وكيفية القيام بذلك بكفاءة.
- مثال كامل قابل للتنفيذ يمكنك نسخه‑ولصقه ورؤية النتيجة في ملف `.xlsx`.

**المتطلبات المسبقة** – تحتاج إلى .NET 6+ (أو .NET Framework 4.7+)، Visual Studio 2022 أو أي بيئة تطوير تفضلها، وحزمة NuGet الخاصة بـ Aspose.Cells for .NET. إذا كنت جديدًا على Aspose.Cells، لا تقلق؛ الخطوات واضحة ومشروحة بالكامل.

---

## الخطوة 1: إعداد المشروع وتثبيت Aspose.Cells

To start, create a new console project:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فقط انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن **Aspose.Cells** وقم بتثبيتها.

المكتبة تزودنا بفئات `Workbook` و `Worksheet` و `Cell` التي سنحتاجها لبقية الدرس.

## الخطوة 2: إنشاء مصنف Excel وتعبئة بيانات عينة

Now we’ll spin up a workbook, grab the first worksheet, and fill column **A** and **B** with sample numbers. This data will later be wrapped into columns and rows.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **لماذا هذا مهم:** وجود بيانات حتمية يتيح لك التحقق من أن `WRAPCOLS` و `WRAPROWS` تقومان بما تتوقعه بالضبط.

## الخطوة 3: تطبيق دالة `WRAPCOLS` – **how to use wrapcols**

`WRAPCOLS` تأخذ نطاقًا أحادي الأبعاد وتوزعه عبر عدد محدد من الأعمدة، مع إضافة صفوف جديدة تلقائيًا حسب الحاجة. إليك الصيغة الدقيقة التي سنُدخلها في الخلية **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **شرح:** الوسيط الثاني (`3`) يخبر Excel بإنشاء ثلاثة أعمدة لكل صف. لذا القيم الثلاث الأولى (1, 2, 3) تُوضع في A1:C1، الثلاث التالية (4, 5, 6) تُوضع في A2:C2، والقيم المتبقية تُملأ الصف التالي.

## الخطوة 4: تطبيق دالة `WRAPROWS` – wrap rows excel

`WRAPROWS` تقوم بالعكس: تأخذ نطاقًا عموديًا وترتبه إلى عدد محدد من الصفوف لكل عمود. سنضع هذه الصيغة في **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **شرح:** مع `2` صفوف لكل عمود، القيم “A, B” تُوضع في B1:B2، “C, D” في C1:C2، وهكذا. الدالة توسع الورقة أفقيًا تلقائيًا.

## الخطوة 5: إعادة حساب جميع الصيغ – **recalculate excel formulas**

عند تعيين صيغة برمجيًا، لن يقوم Excel بحساب النتيجة حتى يتم فتح المصنف أو تقوم بإبلاغ المكتبة صراحةً بتقييمها. هنا يأتي دور **recalculate excel formulas**:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **لماذا تحتاج هذا:** بدون استدعاء `CalculateFormula()`, ستظهر الخلايا النص الخام `=WRAPCOLS(...)` عند فتح الملف، مما يُفقد الدرس هدفه.

## الخطوة 6: حفظ المصنف والتحقق من النتيجة

Finally, write the workbook to disk. You can open the resulting file in Excel to see the wrapped layout.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### النتيجة المتوقعة

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **الأعمدة A‑C** تم تعبئتها بواسطة استدعاء `WRAPCOLS` (ثلاثة أعمدة لكل صف).  
- **الصفوف B‑I** تم تعبئتها بواسطة استدعاء `WRAPROWS` (صفين لكل عمود).  

افتح `output.xlsx` وسترى التخطيط الدقيق المعروض أعلاه. إذا لم تتطابق الأرقام، تحقق مرة أخرى من سلاسل الصيغ وتأكد من استدعاء `CalculateFormula()`.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان النطاق المصدر فارغًا؟
كلا من `WRAPCOLS` و `WRAPROWS` سيعيدان ببساطة مصفوفة فارغة، مما ينتج عنه خلية فارغة. من الآمن استدعاء الدوال حتى عندما لا تكون متأكدًا من وجود البيانات.

### هل يمكنني تغليف أكثر من نطاق في آن واحد؟
نعم—ما عليك سوى وضع صيغ إضافية في خلايا أخرى. كل صيغة تعمل بشكل مستقل، لذا يمكنك وضع `WRAPCOLS` في D1، `WRAPROWS` في E1، إلخ.

### كيف يختلف هذا عن النسخ‑اللصق البسيط للترانسبوز؟
`WRAPCOLS`/`WRAPROWS` يتعاملان مع *التقسيم إلى صفحات* تلقائيًا. إذا كان لديك 20 عنصرًا وطلبت 3 أعمدة، فإن الدالة تنشئ عدد الصفوف اللازم (7 في هذه الحالة) دون الحاجة لحساب الأبعاد يدويًا.

### هل تدعم المكتبة صيغ المصفوفة الديناميكية (Excel 365)؟
Aspose.Cells يدعم بالكامل صيغ المصفوفة الديناميكية، بما في ذلك `WRAPCOLS` و `WRAPROWS`. محرك الحساب سيفرغ النتائج كما في Excel الأصلي.

### ماذا عن الأداء مع مجموعات البيانات الكبيرة؟
للملايين من الصفوف، فكر في تجميع الحساب (`workbook.CalculateFormula(FormulaCalculationOptions)`) أو تعطيل الحساب التلقائي أثناء إدراج الصيغ، ثم إعادة تمكينه قبل الحفظ.

---

## الكود الكامل (جاهز للتنفيذ)

Below is the complete program—copy it into `Program.cs` and hit **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## الخلاصة

أنت الآن تعرف **how to use wrapcols** (وزميله `WRAPROWS`) من C# لإعادة تشكيل البيانات في ورقة Excel، وتفهم لماذا **recalculate excel formulas** خطوة ضرورية. هذا النمط—*create excel workbook c# → insert WRAP functions → recalculate*—هو أساس قوي لأي مهمة تقارير أو عرض بيانات تتطلب تخطيطات أعمدة أو صفوف ديناميكية.

ما التالي؟ جرّب التجربة مع:

- عدد أعمدة/صفوف مختلف (`WRAPCOLS(..., 5)` أو `WRAPROWS(..., 4)`).
- دمج `WRAPCOLS` مع صيغ مصفوفة ديناميكية أخرى مثل `FILTER` أو `SORT`.
- تصدير المصنف إلى PDF باستخدام `workbook.Save("report.pdf", SaveFormat.Pdf)`.

لا تتردد في تعديل العينة، إضافة تنسيق، أو دمجها في خط أنابيب أتمتة أكبر. إذا واجهت أي مشاكل، اترك تعليقًا أدناه—برمجة سعيدة!

![Diagram showing how wrapcols and wraprows transform a single column into a grid – how to use wrapcols example](wrapcols-wraprows-diagram.png "how to use wrapcols example")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Hide Rows and Columns in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}