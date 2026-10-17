---
category: general
date: 2026-10-10
description: تحويل Excel إلى PowerPoint وتحديد منطقة الطباعة في C# باستخدام Aspose.Cells
  – تعلم كيفية تصدير Excel، وتحديد منطقة الطباعة، وإنشاء ملف PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: ar
lastmod: 2026-10-10
og_description: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells. يوضح هذا البرنامج
  التعليمي كيفية تعيين منطقة الطباعة، وتصدير Excel، وإنشاء ملف PPTX باستخدام C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: تحويل Excel إلى PowerPoint – دليل كامل لمطوري C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: تحويل Excel إلى PowerPoint وتحديد منطقة الطباعة
url: /ar/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PowerPoint وتحديد منطقة الطباعة

إذا كنت بحاجة إلى **convert Excel to PowerPoint**، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك في C#. من خلال تعريف منطقة طباعة أولاً، يمكنك التحكم في الخلايا التي تظهر على كل شريحة، ويتطابق ملف PPTX النهائي مع توقعات التخطيط الخاصة بك. كما أن الحل يجيب على “how to export Excel” و “how to set print area” باستخدام نفس قاعدة الشيفرة.

في هذا الدرس ستقوم بـ:

* تحميل دفتر عمل موجود.
* تحديد منطقة الطباعة لورقة العمل (خطوة **set print area excel**).
* تهيئة خيارات التحويل لإخراج PowerPoint.
* إنشاء ملف **convert excel to pptx** في استدعاء طريقة واحد.

جميع الشيفرات المطلوبة مضمونة، بحيث يمكنك نسخها، لصقها، وتشغيلها فوراً.

## المتطلبات المسبقة

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | العينة تستهدف .NET 6+، لكن أي نسخة من .NET تدعم C# 10 تعمل. |
| **Aspose.Cells for .NET** | هذه المكتبة توفر `Workbook`، `ImageOrPrintOptions`، وطريقة `ConvertToPdf` (المستخدمة لإنشاء PPTX). قم بتثبيتها عبر NuGet: `dotnet add package Aspose.Cells` |
| **An input Excel file** | الدرس يستخدم `input.xlsx`. ضعها في مجلد يمكنك الإشارة إليه من الشيفرة. |
| **Write permission to the output folder** | البرنامج يكتب `output.pptx`. تأكد من وجود الدليل وأنه قابل للكتابة. |

> **نصيحة احترافية:** إذا كنت تعمل مع عدة أوراق عمل، كرّر خطوة منطقة الطباعة لكل ورقة قبل التحويل.

## الخطوة 1: إنشاء مشروع C# Console جديد

افتح نافذة طرفية أو PowerShell وشغّل:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

هذا ينشئ مشروعًا جديدًا باسم **ExcelToPowerPointDemo** ويضيف حزمة Aspose.Cells، والتي تُعد الاعتماد الأساسي لـ **how to export Excel** إلى صيغ أخرى.

## الخطوة 2: كتابة شيفرة التحويل

استبدل محتوى `Program.cs` بالمثال الكامل أدناه. الشيفرة توضح **convert excel to powerpoint**، وتظهر **how to set print area**، وتنتج ملف **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### لماذا كل جزء مهم

* **Loading the workbook** – هذه هي الخطوة الأولى في أي سيناريو **how to export Excel**. `Workbook` يقرأ الملف إلى الذاكرة، مما يمنحك وصولًا كاملًا إلى الأوراق، الخلايا، والتنسيقات.
* **Setting the print area** – من خلال تعيين `PageSetup.PrintArea`، تخبر Aspose.Cells أي خلايا يجب عرضها. هذا هو جوهر **set print area excel**؛ بدون ذلك، سيتم تصدير الورقة بأكملها، مما قد ينتج شرائح ضخمة وغير قابلة للقراءة.
* **Choosing `SaveFormat.Pptx`** – كائن `ImageOrPrintOptions` يتيح لك تغيير صيغ الإخراج. تعيين `SaveFormat` إلى `Pptx` يطلق عملية **convert excel to pptx**.
* **Calling `ConvertToPdf`** – بالرغم من اسم الطريقة، عندما يكون `SaveFormat` هو `Pptx` تُنتج المكتبة ملف PowerPoint. هذه هي الطريقة الموصى بها لـ **convert excel to powerpoint** في استدعاء واحد.

## الخطوة 3: تشغيل البرنامج

من مجلد المشروع، نفّذ:

```bash
dotnet run
```

إذا تم تكوين كل شيء بشكل صحيح، يجب أن ترى مخرجات وحدة التحكم مشابهة لـ:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

افتح `output.pptx` في Microsoft PowerPoint أو أي عارض متوافق. كل شريحة تتطابق مع الصفحة المطبوعة من ورقة العمل، مقصورة على النطاق الذي حددته.

## معالجة أوراق عمل متعددة

إذا كان دفتر العمل يحتوي على أكثر من ورقة وتريد كل ورقة في مجموعة شرائح منفصلة، قم بالتكرار عبر المجموعة:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

هذا النمط يوضح **how to export Excel** بيانات ورقة‑ورقة مع الاستمرار في **setting print area** بشكل فردي.

## الحالات الخاصة ونصائح الممارسات الأفضل

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | قلل منطقة الطباعة أو زد `HorizontalResolution`/`VerticalResolution` للحفاظ على حجم PPTX قابلًا للإدارة. |
| **Different page orientations** | عيّن `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` قبل التحويل. |
| **Custom slide size** | استخدم `conversionOptions.OnePagePerSheet = false;` واضبط `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | غلف كود التحميل داخل كتلة `try { … } catch (FileNotFoundException)` لتوفير رسالة خطأ واضحة. |
| **Non‑ASCII characters** | تأكد من حفظ دفتر العمل بترميز UTF‑8؛ Aspose.Cells يتعامل مع Unicode تلقائيًا. |

## الشيفرة المصدرية الكاملة للمرجع

فيما يلي البرنامج بالكامل، بما في ذلك توجيهات `using` والتعليقات. احفظه كـ `Program.cs` داخل المشروع الذي تم إنشاؤه في **Step 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## النتيجة المتوقعة

Running the program produces a PowerPoint file (`output.pptx`) that contains:

* شريحة واحدة لكل صفحة مطبوعة من ورقة العمل.
* فقط الخلايا داخل **A1:G30** تكون مرئية في كل شريحة.
* التنسيق محفوظ (الخطوط، الألوان، الحدود) كما هو في Excel.

افتح الملف في PowerPoint للتحقق من أن التخطيط يتطابق مع منطقة الطباعة المحددة.

## الخلاصة

أنت الآن تعرف كيفية **convert Excel to PowerPoint** مع تحديد **set print area excel** بدقة باستخدام Aspose.Cells في C#. غطى الدرس **how to export Excel**، وأظهر **how to set print area**، وعرض **convert excel to pptx** بالكامل.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تعيين منطقة طباعة في Excel باستخدام Aspose.Cells لـ .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [تعيين منطقة طباعة في Excel وتصدير إلى PowerPoint – دليل خطوة بخطوة](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [تعيين منطقة طباعة Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}