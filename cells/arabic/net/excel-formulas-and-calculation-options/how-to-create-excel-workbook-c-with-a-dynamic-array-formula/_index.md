---
category: general
date: 2026-10-01
description: إنشاء مصنف Excel باستخدام C# بسرعة وتعلم مثال على صيغة مصفوفة ديناميكية
  لكتابة صيغة Excel بـ C# في Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: ar
lastmod: 2026-10-01
og_description: أنشئ مصنف Excel باستخدام C# بسرعة وشاهد مثالًا على صيغة مصفوفة ديناميكية
  يوضح كيفية كتابة صيغة Excel بـ C# باستخدام Aspose.Cells. اتبع الدليل خطوة بخطوة
  لإنشاء الملف وحسابه وحفظه.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: إنشاء مصنف إكسل C# مع صيغة مصفوفة ديناميكية
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية إنشاء مصنف إكسل باستخدام C# مع صيغة مصفوفة ديناميكية
url: /ar/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مصنف Excel باستخدام C# مع صيغة مصفوفة ديناميكية

إذا كنت بحاجة إلى **إنشاء مصنف Excel C#** برمجيًا، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells. ستحصل أيضًا على **مثال على صيغة مصفوفة ديناميكية** يوضح أفضل طريقة لـ **كتابة صيغة Excel C#** للوظائف الحديثة في Excel مثل `SORT`.

كان إنشاء ملف Excel من C# يتطلب في السابق استخدام COM interop أو توليد XML يدويًا، وكلاهما كان هشًا وصعب الصيانة. بنهاية هذا البرنامج التعليمي ستحصل على مصنف كامل الوظائف يحسب مصفوفة ديناميكية تلقائيًا، وستفهم لماذا يُعَد هذا النهج موثوقًا لأتمتة مستوى الإنتاج.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث مثبت (الكود يعمل مع .NET Core و .NET Framework أيضًا)
- رخصة Aspose.Cells صالحة أو مفتاح تقييم مجاني
- Visual Studio 2022 (أو أي بيئة تطوير تدعم C#)
- إلمام أساسي بصياغة C# وصيغ Excel

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Cells`، والتي يمكنك إضافتها باستخدام:

```bash
dotnet add package Aspose.Cells
```

## الخطوة 1: إعداد مشروع C# وإضافة مرجع Aspose.Cells

أنشئ تطبيقًا جديدًا من نوع console وأضف مرجع Aspose.Cells. هذه الخطوة أساسية لأن المكتبة توفر الكائنات `Workbook` و `Worksheet` ومحرك الحساب الذي تحتاجه لـ **كتابة صيغة Excel C#**.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **لماذا هذا مهم:** تقوم Aspose.Cells بتجريد تفاصيل OpenXML منخفضة المستوى، مما يتيح لك التركيز على منطق الأعمال بدلاً من تفاصيل تنسيق الملف.

## الخطوة 2: إنشاء مصنف Excel والحصول على الورقة الأولى

الآن **ننشئ مصنف Excel C#** عن طريق إنشاء كائن `Workbook`. يحتوي المصنف الافتراضي على ورقة عمل واحدة، نقوم باسترجاعها لمزيد من العمليات.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى عدة أوراق، استدعِ `workbook.Worksheets.Add()` قبل الوصول إليها.

## الخطوة 3: تعبئة البيانات المصدر للمصفوفة الديناميكية

تتطلب وظائف المصفوفة الديناميكية مثل `SORT` نطاقًا مصدرًا. لنملأ الخلايا *A2:A10* بأرقام غير مرتبة حتى تتمكن صيغة `SORT` من إظهار سلوكها.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **سبب القيام بذلك:** توفير بيانات ملموسة يتيح لك رؤية **مثال صيغة المصفوفة الديناميكية** قيد التنفيذ دون الحاجة إلى ملفات إدخال خارجية.

## الخطوة 4: كتابة صيغة المصفوفة الديناميكية في الخلية A1

هذا هو جوهر جزء **كتابة صيغة Excel C#**. نُعيّن صيغة `SORT` إلى الخلية *A1*. لأن `SORT` هي دالة مصفوفة ديناميكية، سيقوم Excel تلقائيًا بتمديد النتائج المرتبة إلى الخلايا الأسفل.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **شرح:**  
> - `worksheet.Cells[0, 0]` يستهدف الخلية **A1** (الصف 0، العمود 0).  
> - السلسلة `=SORT(A2:A10)` هي صيغة Excel قياسية. تقوم Aspose.Cells بتحليلها بنفس طريقة Excel، مما يتيح دعمًا كاملاً لوظائف المصفوفة الديناميكية الحديثة.

## الخطوة 5: إعادة حساب المصنف حتى تُملأ الصيغة تلقائيًا

لا تقوم Aspose.Cells بإعادة حساب الصيغ تلقائيًا عند الكتابة. يجب عليك تشغيل الحساب صراحةً لرؤية النتائج الممتدة.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

بعد هذا الاستدعاء، ستحتوي الخلايا **A1:A9** على القائمة المرتبة: 5, 7, 8, 14, 19, 21, 27, 33, 42.

### التحقق من النتيجة (المخرجات المتوقعة)

يمكنك طباعة القيم الممتدة إلى وحدة التحكم لتأكيد نجاح الحساب:

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**المخرجات المتوقعة في وحدة التحكم**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **ملاحظة حول الحالات الحدية:** إذا كان النطاق المصدر يحتوي على بيانات غير رقمية، فإن `SORT` ستقوم بالترتيب أبجديًا. تأكد دائمًا من صحة نوع البيانات قبل تطبيق الدوال التي تتعامل مع الأرقام فقط.

## الخطوة 6: حفظ المصنف على القرص (اختياري)

حفظ الملف يتيح لك فتحه في Excel ورؤية المصفوفة الديناميكية بصريًا. هذه الخطوة ليست ضرورية للحساب نفسه، لكنها مفيدة للتصحيح والتوزيع.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

عند فتح *SortedNumbers.xlsx* في Excel 365 أو أحدث، سترى القائمة المرتبة تمتد تلقائيًا من **A1** إلى الأسفل—تمامًا ما أنتجه **مثال صيغة المصفوفة الديناميكية** من C#.

## مثال كامل يعمل

بجمع كل الأجزاء معًا، إليك البرنامج الكامل القابل للتنفيذ:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

شغّل البرنامج (`dotnet run`) وسترى الأرقام المرتبة مطبوعة، يليها تأكيد بأن الملف تم حفظه.

## أسئلة شائعة وتنوعات

### ماذا لو أردت استخدام دالة مصفوفة ديناميكية مختلفة؟

استبدل سلسلة الصيغة بأي دالة مصفوفة ديناميكية أخرى، مثل `=FILTER(A2:A10, B2:B10>10)` أو `=UNIQUE(A2:A10)`. نمط **كتابة صيغة Excel C#** يبقى نفسه:

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### كيف أتعامل مع صيغ تشير إلى أوراق عمل أخرى؟

أشر إلى ورقة أخرى باسمها:

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

تقوم Aspose.Cells بحل مراجع الأوراق المتقاطعة تلقائيًا أثناء `workbook.Calculate()`.

### هل يمكنني إيقاف الحساب التلقائي وإجراء الحساب لاحقًا؟

نعم. اضبط وضع حساب المصنف إلى يدوي:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

هذا يحسن الأداء عندما تقوم بتحديث آلاف الخلايا قبل إجراء الحساب النهائي.

## الخلاصة

أنت الآن تعرف كيفية **إنشاء مصنف Excel C#** باستخدام Aspose.Cells، وإدراج **مثال على صيغة مصفوفة ديناميكية**، و**كتابة صيغة Excel C#** التي تمتد تلقائيًا. يغطي الحل الكامل إعداد المشروع، تحضير البيانات، إدراج الصيغة، إجبار الحساب، التحقق، وحفظ الملف اختياريًا.

من هنا يمكنك استكشاف سيناريوهات أكثر تقدمًا: ربط عدة دالات مصفوفة ديناميكية، تطبيق تنسيقات رقمية مخصصة، أو دمج توليد المصنف في واجهة برمجة تطبيقات ويب. تذكر دائمًا التحقق من صحة البيانات المدخلة قبل تطبيق الصيغ، واستفد من محرك الحساب القوي في Aspose.Cells لمعالجة Excel على الخادم بشكل موثوق. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel Automation with Aspose.Cells .NET: Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Create Excel Workbook C# – Complete Guide with Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}