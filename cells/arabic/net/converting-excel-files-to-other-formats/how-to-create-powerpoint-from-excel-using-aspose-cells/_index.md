---
category: general
date: 2026-09-18
description: إنشاء عرض PowerPoint من Excel باستخدام Aspose.Cells – نسخ جداول Pivot،
  تصدير النطاقات، وحفظها كملف PPTX ببضع أسطر من كود C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: ar
lastmod: 2026-09-18
og_description: إنشاء PowerPoint من Excel بسرعة. تعلّم كيفية نسخ جداول Pivot وتصدير
  النطاقات وحفظ المصنف كملف PPTX باستخدام Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: إنشاء PowerPoint من Excel باستخدام Aspose.Cells – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: كيفية إنشاء PowerPoint من Excel باستخدام Aspose.Cells
url: /ar/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء PowerPoint من Excel باستخدام Aspose.Cells

إذا كنت بحاجة إلى إنشاء PowerPoint من Excel، يوضح لك هذا الدليل حلاً مختصرًا وشاملًا. سترى كيفية نسخ جدول محوري، وتصدير نطاق مختار، وحفظ النتيجة كملف PPTX ببضع أسطر فقط من C#.

إنشاء مجموعة شرائح مباشرةً من بيانات جدول البيانات يزيل خطوة النسخ‑اللصق اليدوية التي تبطئ سير عمل التقارير. يغطي الدليل كل ما تحتاجه، من إعداد المشروع إلى ملف PPTX النهائي، وهو يعمل مع أحدث نسخة من Aspose.Cells for .NET.

## المتطلبات المسبقة

* **Aspose.Cells for .NET** (الإصدار 23.12 أو أحدث). قم بتثبيته عبر NuGet: `Install-Package Aspose.Cells`.
* بيئة تطوير **.NET 6+** (Visual Studio 2022 أو VS Code).
* مصنف Excel (`Source.xlsx`) يحتوي على البيانات والجدول المحوري الذي تريد إعادة استخدامه.
* صلاحية كتابة إلى مجلد الإخراج.

لا توجد مكتبات طرف ثالث إضافية مطلوبة.

## إنشاء PowerPoint من Excel – خطوة بخطوة

تتكون العملية من أربع خطوات منطقية تتطابق مباشرةً مع مثال الشيفرة الذي ستراه لاحقًا.

### الخطوة 1: تحميل مصنف المصدر وتحديد النطاق

يجب تحميل المصنف الذي يحتوي على البيانات المصدر والجدول المحوري. اختيار نطاق دقيق يضمن نقل الخلايا المطلوبة فقط، مما يحافظ على خفة الشريحة الناتجة.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**لماذا هذا مهم:**  
`CreateRange` ينشئ كائن `Range` يمكن نسخه ككل. بتحديد النطاق إلى `A1:G20`، تتجنب سحب خلايا غير ذات صلة، والتي قد تزيد حجم ملف PowerPoint.

### الخطوة 2: إعداد مصنف الوجهة

تتعامل Aspose.Cells مع شريحة PowerPoint كمصنف عندما تقوم بحفظها بصيغة PPTX. إنشاء مصنف جديد يمنحك لوحة رسم نظيفة للنطاق المنسوخ.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**نصيحة:** إذا كنت بحاجة إلى عدة شرائح، يمكنك إضافة أوراق عمل إضافية وحفظ كل منها لاحقًا كملف PPTX منفصل.

### الخطوة 3: نسخ النطاق مع الحفاظ على الجدول المحوري

طريقة `CopyRange` تقبل كائن `PasteOptions`. ضبط `CopyPivotTables = true` يخبر Aspose.Cells بالحفاظ على بنية الجدول المحوري دون تعديل، وليس فقط القيم المعروضة.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**كيف يعمل:**  
عند كون `CopyPivotTables` صحيحًا، تستقبل ورقة الوجهة كلًا من البيانات المصدر وذاكرة التخزين المؤقت للجدول المحوري. هذا يعني أن الجدول المحوري يظل فعالًا بالكامل ويمكن تحديثه لاحقًا إذا تغيرت البيانات المصدر.

### الخطوة 4: حفظ المصنف كملف PowerPoint

أخيرًا، قم بتصدير المصنف إلى صيغة PPTX. علم `SaveFormat.Pptx` يخبر Aspose.Cells بكتابة ورقة العمل كشريحة PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**النتيجة:**  
`CopyWithPivot.pptx` يفتح في Microsoft PowerPoint (أو أي عارض متوافق) بشريحة واحدة تعرض النطاق المنسوخ، بما في ذلك جدول محوري حي يمكن التفاعل معه في PowerPoint.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع وحدة تحكم جديد وتشغيله فورًا.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**المخرجات المتوقعة:**  
تشغيل البرنامج يطبع “PowerPoint file created successfully.” وينتج ملفًا باسم `CopyWithPivot.pptx`. فتح الملف في PowerPoint يظهر شريحة واحدة حيث يظهر النطاق المنسوخ من Excel بالضبط كما كان في ورقة المصدر، مع جدول محوري نشط يمكن تحديثه من داخل PowerPoint.

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **جداول محورية متعددة** | حدد كائنات `Range` منفصلة لكل جدول واستدعِ `CopyRange` لكل منها، أو انسخ الورقة بالكامل إذا كانت تشترك في نفس مصدر البيانات. |
| **مجموعات بيانات كبيرة** | قم بزيادة النطاق (مثال: `"A1:Z5000"`). فكر في تمكين `PasteOptions.CompressData = true` لتقليل حجم PPTX. |
| **تخطيطات شرائح مختلفة** | بعد الحفظ بصيغة PPTX، افتح الملف في PowerPoint وطبق تخطيطًا أو سمة مخصصة؛ تظل البيانات قابلة للتحرير. |
| **الحفظ إلى تدفق** | استخدم `destinationWorkbook.Save(stream, SaveFormat.Pptx)` عندما تحتاج لإرجاع PPTX عبر واجهة برمجة تطبيقات ويب. |
| **الحفاظ على تنسيق الخلايا** | اضبط `PasteOptions.PasteType = PasteType.All` للحفاظ على الخطوط والألوان والحدود. |

**نصيحة احترافية:** تأكد دائمًا من وجود مجلد الوجهة قبل استدعاء `Save`. إذا كان المجلد غير موجود، سيُطلق `Save` استثناء `DirectoryNotFoundException`.

## الخلاصة

أنت الآن تعرف كيفية إنشاء PowerPoint من Excel، نسخ جدول محوري، وتصدير النتيجة كملف PPTX باستخدام Aspose.Cells. الخطوات—تحميل مصنف المصدر، تحديد نطاق، النسخ باستخدام `CopyPivotTables`، والحفظ كـ PPTX—تغطي سير العمل بالكامل بطريقة موثوقة وجاهزة للإنتاج.

بعد ذلك، استكشف **كيفية تصدير Excel إلى PPTX** لعدة أوراق عمل، أو تعلم **كيفية نسخ نطاق بين المصنفات** عندما تحتاج إلى دمج بيانات من عدة مصادر قبل إنشاء مجموعة الشرائح. كلا الموضوعين يبنيان على نفس واجهة API ويمكن دمجهما لأتمتة خطوط تقارير معقدة.

برمجة سعيدة، واستمتع بتحويل جداول البيانات الخاصة بك إلى عروض تقديمية مصقولة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية نسخ جدول محوري في C# – تحويل Excel إلى PPTX، نسخ نطاق وإنشاء مربع نص](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [إنشاء مصنف جديد – كيفية نسخ ورقة عمل مع جدول محوري](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [كيفية إنشاء وحفظ ملفات Excel باستخدام Aspose.Cells for .NET: دليل كامل](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}