---
category: general
date: 2026-03-22
description: كيفية استخدام اللامبدا في C# للعمل مع صيغ Excel. تعلم كتابة الصيغة في
  الخلية، تحويل النطاق إلى مصفوفة، عرض المصفوفة في وحدة التحكم، وحساب القاطع في Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: ar
og_description: كيفية استخدام اللامدا في C# للتعامل مع صيغ Excel، وتحويل النطاق إلى
  مصفوفة، وكتابة الصيغة إلى خلية، وعرض المصفوفة في وحدة التحكم، وحساب القاطع الزاوي
  في Excel.
og_title: كيفية استخدام لامدا في C# مع صيغ Excel – خطوة بخطوة
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: كيفية استخدام لامدا في C# مع صيغ إكسل – دليل كامل
url: /ar/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Lambda في C# مع صيغ Excel – دليل شامل

هل تساءلت يومًا **كيف تستخدم lambda** عندما تقوم بأتمتة Excel من C#؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى دمج قوة الدالات الديناميكية الجديدة في Excel مع قدرة C# على `LAMBDA`. الخبر السار؟ الأمر بسيط إلى حد ما بمجرد أن ترى كيف تتكامل الأجزاء معًا.

في هذا البرنامج التعليمي سنستعرض **كتابة صيغة في خلية**، **تحويل نطاق إلى مصفوفة**، **عرض تلك المصفوفة في وحدة التحكم**، وحتى **حساب الظل المقلوب (cotangent) في Excel**—كل ذلك مع إظهار **كيفية استخدام lambda** داخل استدعاء `REDUCE`. في النهاية ستحصل على مقتطف قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET ي引用 Aspose.Cells (أو مكتبة مشابهة).

---

## ما ستتعلمه

- كيفية **كتابة صيغة في خلية** باستخدام C#.
- كيفية **تحويل النطاق إلى مصفوفة** باستخدام دالة `EXPAND`.
- كيفية **عرض المصفوفة في وحدة التحكم** بعد الحساب.
- كيفية **حساب الظل المقلوب في Excel** باستخدام `COT` و `COTH`.
- الصياغة الدقيقة **لكيفية استخدام lambda** داخل دالة `REDUCE` في Excel من C#.

> **المتطلبات المسبقة:** تحتاج إلى نسخة حديثة من .NET (Core 6+ أو .NET Framework 4.7+) ومكتبة Aspose.Cells for .NET المثبتة عبر NuGet.

---

## الخطوة 1: إعداد المصنف وكتابة الصيغة في الخلية

أول ما نقوم به هو إنشاء مصنف جديد والحصول على أول ورقة عمل. ثم **نكتب صيغة في خلية** – في هذه الحالة ستحتوي الخلية `A1` على نتيجة استدعاء `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**لماذا هذا مهم:** كتابة الصيغة مباشرة من الكود تتيح لك إنشاء جداول بيانات معقدة في الوقت الفعلي دون الحاجة لفتح Excel. كما أنها تمهد للخطوة التالية حيث **نحوّل النطاق إلى مصفوفة**.

---

## الخطوة 2: تحويل النطاق إلى مصفوفة باستخدام EXPAND

`EXPAND` هي طريقة Excel لتحويل نطاق صغير إلى مصفوفة أكبر. بوضع الصيغة في `A1`، سيقوم Excel بإنشاء كتلة 4 × 5 تبدأ من تلك الخلية. من C#، لا نحتاج إلى نسخ القيم يدويًا – المكتبة ستقوم بالعمل عندما نستدعي `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**كيفية استخدام lambda:** لم نصل إليها بعد، لكن ترقب. أولًا نحتاج البيانات في الورقة، ثم سنقلصها باستخدام lambda.

---

## الخطوة 3: استخدام LAMBDA داخل REDUCE – جوهر “كيفية استخدام Lambda”

أدخلت Excel 365 دالة `REDUCE`، التي تقبل **قيمة ابتدائية**، **نطاق**، و**LAMBDA** يحدد كيفية دمج كل عنصر. من C# نُعيّن مجرد سلسلة الصيغة؛ الـ lambda يعيش داخل صيغة Excel، وليس في كود C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**شرح:**  
- `0` هو المجمّع الابتدائي (`acc`).  
- `A1:D4` هو النطاق الذي نريد معالجته (الأعمدة الأربعة الأولى من الانسكاب).  
- `LAMBDA(acc, x, acc + x)` يخبر Excel أن يضيف كل خلية (`x`) إلى المجمّع.

هذا هو جوهر **كيفية استخدام lambda** للتجميع في سياق جداول البيانات.

---

## الخطوة 4: حساب الظل المقلوب في Excel – من الدرجات إلى الدوال الزائدية

إذا كنت تحتاج إلى نتائج مثلثية، فإن دالتي `COT` و `COTH` في Excel سهلتا الأمر. سنضعهما في `G1` و `G2` على التوالي.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**لماذا هذا مفيد:** معرفة **كيفية حساب الظل المقلوب في Excel** يمكن أن توفر عليك كتابة كود رياضي مخصص، خاصةً عندما يُشارك المصنف مع غير المطورين.

---

## الخطوة 5: إجبار الحساب واسترجاع المصفوفة الموسعة

الآن نطلب من المصنف تقييم كل الصيغ، ثم نستخرج المصفوفة المنسكبة من `A1`. هنا نُظهر **عرض المصفوفة في وحدة التحكم**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**ما ستراه:**  
- مصفوفة 4 × 5 منسقة بشكل جميل تُطبع سطرًا بسطر.  
- المجموع المحسوب بواسطة lambda في `REDUCE`.  
- القيمتين للظل المقلوب.

بهذا نكون قد أكملنا السلسلة من **كتابة صيغة في خلية** حتى **عرض المصفوفة في وحدة التحكم**.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق console. تذكر إضافة حزمة NuGet `Aspose.Cells` أولًا (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**الناتج المتوقع في وحدة التحكم (القيم قد تختلف بناءً على محتويات B1:C2 الافتراضية، والتي تكون 0 عادةً):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

لا تتردد في ملء `B1:C2` بأرقامك الخاصة قبل التشغيل – ستنعكس هذه القيم في المصفوفة.

---

## نصائح احترافية ومخاطر شائعة

- **نصيحة احترافية:** إذا أردت أن يبدأ النطاق المنسكب من خلية أخرى، فقط غير الخلية المستهدفة (`A1`). دالة `EXPAND` تحترم نقطة الارتكاز.
- **احذر من:** الخلايا الفارغة في النطاق الأصلي تتحول إلى `0` في المصفوفة المنسكبة، ما قد يؤثر على مجموع `REDUCE`.
- **حالة حافة:** عندما يحتوي المصنف على صيغ تعتمد على دوال متقلبة (مثل `NOW()`)، استدعِ `workbook.Calculate()` بعد ضبط جميع الصيغ لضمان تحديث كل شيء.
- **ملاحظة الأداء:** بالنسبة للانسكابات الكبيرة، فكر في تحديد الحجم في استدعاء `EXPAND`؛ وإلا قد تُخصص ذاكرة أكثر من اللازم.
- **التوافق:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}