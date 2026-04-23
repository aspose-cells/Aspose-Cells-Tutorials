---
category: general
date: 2026-03-30
description: إنشاء مصنف Excel باستخدام C# و Aspose.Cells. تعلم تطبيق دالة lambda في
  Excel، ودالة sequence في Excel، وتوسيع المصفوفة في Excel، وحفظ المصنف بصيغة xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: ar
og_description: إنشاء دفتر عمل Excel باستخدام C# بسرعة. يوضح هذا الدليل كيفية استخدام
  دالة لامدا في Excel، ودالة التسلسل في Excel، وتوسيع المصفوفة في Excel، وحفظ دفتر
  العمل كملف xlsx.
og_title: إنشاء مصنف إكسل C# – دليل Lambda و SEQUENCE و EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف إكسل C# – دليل Lambda و SEQUENCE و EXPAND
url: /ar/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel باستخدام C# – دليل Lambda و SEQUENCE و EXPAND

هل احتجت يومًا إلى **إنشاء دفتر عمل Excel باستخدام C#** لتقرير آلي، لكنك لم تكن متأكدًا من أي استدعاءات API تستخدم؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يغوصون لأول مرة في إنشاء Excel برمجيًا. في هذا الدليل ستشاهد مثالًا كاملاً قابلاً للتنفيذ يغطي كل شيء من **دالة SEQUENCE في Excel** إلى **دالة LAMBDA القوية في Excel**، وحتى كيفية **توسيع مصفوفة Excel**.

سنوضح لك أيضًا الخطوات الدقيقة لـ **حفظ دفتر العمل كملف xlsx** حتى تتمكن من تسليم الملف لأي شخص يستخدم Excel. بنهاية هذا الشرح ستحصل على مقتطف ثابت وجاهز للإنتاج يمكنك إدراجه في أي مشروع .NET. لا روابط غامضة مثل “انظر الوثائق”—فقط كود يعمل الآن.

## ما ستحتاجه

- **.NET 6.0 أو أحدث** – المثال يستهدف .NET 6، لكن أي نسخة حديثة تعمل.  
- **Aspose.Cells for .NET** – تثبيت عبر NuGet (`Install-Package Aspose.Cells`).  
- فهم أساسي لسينتاكس C# (المتغيرات، الكائنات، وتعبيرات lambda).  
- بيئة تطوير متكاملة (IDE) مريحة لك (Visual Studio، Rider، أو VS Code).  

هذا كل شيء. لا حاجة إلى COM interop إضافي، ولا يتطلب تثبيت Office على الخادم—Aspose.Cells يتعامل مع كل شيء في الذاكرة.

## إنشاء دفتر عمل Excel باستخدام C# – تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى خطوات صغيرة. كل خطوة لها عنوان واضح، مقتطف شفرة قصير، وتفسير **لماذا** نقوم بذلك. لا تتردد في نسخ الكتلة الكاملة في النهاية وتشغيلها كتطبيق كونسول.

### الخطوة 1 – تهيئة دفتر عمل جديد

أولًا: نحتاج إلى كائن دفتر عمل فارغ يمثل ملف Excel في الذاكرة.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*لماذا هذا مهم:* `Workbook` هو نقطة الدخول لجميع عمليات Aspose.Cells. بالحصول على أول `Worksheet` نحصل على مساحة يمكننا كتابة الصيغ، القيم، أو التنسيق فيها.

> **نصيحة احترافية:** إذا احتجت إلى عدة أوراق، ما عليك سوى استدعاء `workbook.Worksheets.Add()` والاحتفاظ بإشارة إلى كل واحدة.

### الخطوة 2 – استخدام دالة SEQUENCE في Excel لتوليد البيانات

تُنشئ **دالة SEQUENCE في Excel** مصفوفة ديناميكية من الأرقام دون أي VBA. سنضعها في الخلية `A1` وسنترك Excel يوسّعها تلقائيًا.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*لماذا هذا مهم:* `SEQUENCE(3)` تُعيد `[1,2,3]`. تغليفها بـ `EXPAND` يجبر النتيجة على أن تكون نطاقًا من 5 صفوف، مع ملء الصفوف الإضافية بالفراغات. هذا يوضح كلًا من **دالة SEQUENCE في Excel** و **توسيع مصفوفة Excel** في خطوة واحدة.

### الخطوة 3 – تجميع الأرقام باستخدام دالة LAMBDA في Excel

الآن لنستعرض قدرة **دالة LAMBDA في Excel**. سنجمع الأرقام من 1 إلى 5 باستخدام الدالة الجديدة `REDUCE`، التي تعتمد داخليًا على lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*لماذا هذا مهم:* `REDUCE` تُكرر على المصفوفة التي تنتجها `SEQUENCE(5)`، وتُمرّر كل عنصر (`b`) إلى lambda جنبًا إلى جنب مع المتراكم (`a`). الـ lambda `a+b` يجمعهم، فينتج `15` في `B1`. هذه طريقة نظيفة تعتمد على الصيغ فقط لإجراء التجميع دون حلقات في C#.

### الخطوة 4 – تطبيق الدوال المثلثية مباشرةً في الخلايا

الدوال الرياضية المدمجة في Excel مفيدة للحسابات السريعة. سنضع دالة الظل المقلوب (cotangent) ودالة الظل المقلوب الزائد (hyperbolic cotangent) في خلايا متجاورة.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*لماذا هذا مهم:* يوضح أنه يمكنك دمج الدوال الرياضية الكلاسيكية مع صيغ المصفوفة الديناميكية الحديثة. لا حاجة لحساب هذه القيم في C# إلا إذا كان لديك سبب أداء محدد.

### الخطوة 5 – حساب جميع الصيغ

Aspose.Cells لا يقوم بتقييم الصيغ تلقائيًا عند تعيينها. عليك أن تطلب منه حسابها.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*لماذا هذا مهم:* بعد هذا الاستدعاء، تحتوي خاصية `Value` لكل خلية على النتيجة المُقيمة، جاهزة للحفظ أو القراءة مرة أخرى.

### الخطوة 6 – حفظ دفتر العمل كملف Xlsx

أخيرًا، نقوم بحفظ دفتر العمل على القرص باستخدام نمط **حفظ دفتر العمل كملف xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*لماذا هذا مهم:* طريقة `Save` تكتشف امتداد الملف تلقائيًا. باستخدام “.xlsx” نضمن أن الملف متوافق مع إصدارات Excel الحديثة. المسار يشير إلى سطح المكتب لتسهيل الوصول أثناء الاختبار.

### مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع كونسول جديد. يتضمن جميع الخطوات السابقة، بالإضافة إلى كتلة تحقق صغيرة تطبع القيم المحسوبة إلى الكونسول.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**الناتج المتوقع في الكونسول**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

وعند فتح *NewFunctions.xlsx* سترى نفس الأرقام موزعة في الأعمدة الأربعة الأولى.

![لقطة شاشة لإنشاء دفتر عمل Excel باستخدام C# للجدول الناتج](/images/create-excel-workbook-csharp.png)

## الحالات الخاصة، النصائح، والأسئلة الشائعة

- **ماذا لو احتجت إلى أكثر من ورقة واحدة؟**  
  ما عليك سوى استدعاء `workbook.Worksheets.Add()` وتكرار تعيين الصيغ على كل كائن `Worksheet` جديد.  

- **هل يمكنني استخدام إصدارات Excel أقدم؟**  
  تتطلب دوال المصفوفة الديناميكية (`SEQUENCE`, `EXPAND`, `REDUCE`) Excel 365 أو Excel 2021+. إذا كنت تستهدف إصدارات أقدم، التزم بالصيغ الكلاسيكية أو احسب القيم في C# قبل كتابتها.  

- **هل هناك مخاوف بشأن الأداء؟**  
  بالنسبة لآلاف الصفوف، تعيين الصيغ على نطاق ثم استدعاء `CalculateFormula` عادةً ما يكون أسرع من التكرار وتعيين القيم واحدًا تلو الآخر.  

- **حفظ إلى تدفق بدلاً من ملف؟**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}