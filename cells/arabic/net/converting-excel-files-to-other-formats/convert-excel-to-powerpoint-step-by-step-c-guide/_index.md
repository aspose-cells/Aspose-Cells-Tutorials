---
category: general
date: 2026-03-01
description: حوّل Excel إلى PowerPoint بسرعة باستخدام C#. تعلّم كيفية إنشاء PowerPoint
  من مصنف Excel باستخدام Aspose.Cells في بضع أسطر من الشيفرة فقط.
draft: false
keywords:
- convert excel to powerpoint
- generate powerpoint from excel
- convert xlsx to pptx
- how to convert excel
- create pptx from excel
language: ar
og_description: تحويل Excel إلى PowerPoint باستخدام C#. يوضح هذا الدليل كيفية إنشاء
  PowerPoint من ملف Excel باستخدام Aspose.Cells، مع الكود الكامل والنصائح.
og_title: تحويل Excel إلى PowerPoint – دليل C# الكامل
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
title: تحويل Excel إلى PowerPoint – دليل C# خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PowerPoint – دليل خطوة بخطوة بلغة C#

هل احتجت يومًا إلى **تحويل Excel إلى PowerPoint** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—فالعديد من المطورين يواجهون هذه المشكلة عندما يحاولون تحويل جداول البيانات الغنية بالبيانات إلى عروض تقديمية جاهزة.

الأخبار السارة هي أنه ببضع أسطر من C# يمكنك **إنشاء PowerPoint من Excel** تلقائيًا، دون الحاجة إلى النسخ واللصق يدويًا. في هذا الدرس سنستعرض العملية بالكامل، من تحميل ملف `.xlsx` إلى حفظ ملف `.pptx` مصقول يمكنك فتحه في Microsoft PowerPoint أو أي عارض متوافق.

> **ما ستحصل عليه:** برنامج قابل للتنفيذ يقوم بتحميل مصنف Excel، ويضبط خيارات حفظ PowerPoint، ويكتب ملف PowerPoint—كل ذلك باستخدام مكتبة Aspose.Cells.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)  
- **Aspose.Cells for .NET** – يمكنك الحصول عليها من NuGet (`Install-Package Aspose.Cells`)  
- فهم أساسي للغة C# (ليس شيئًا معقدًا، فقط عبارات `using` المعتادة)  
- ملف Excel (`input.xlsx`) ترغب في تحويله إلى مجموعة شرائح  

هذا كل ما تحتاجه. لا أدوات طرف ثالث إضافية، لا تفاعل COM، ولا أتمتة PowerPoint معقدة. لنبدأ.

![مخطط سير تحويل Excel إلى PowerPoint](convert-excel-to-powerpoint.png "تحويل Excel إلى PowerPoint")

*نص بديل: مخطط سير تحويل Excel إلى PowerPoint*

## تحويل Excel إلى PowerPoint باستخدام Aspose.Cells

### الخطوة 1 – تحميل مصنف Excel

أول شيء علينا فعله هو جلب جدول البيانات إلى الذاكرة. تجعل Aspose.Cells ذلك بسيطًا بقدر استدعاء مُنشئ `Workbook` وتمرير مسار الملف.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the Excel workbook
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
```

**لماذا هذا مهم:** تحميل المصنف يمنحنا الوصول إلى كل ورقة عمل، ومخطط، وحتى الصور المدمجة. من هناك يمكننا اتخاذ قرار ما الذي نحتفظ به أو نتخلص منه قبل التحويل.

### الخطوة 2 – إعداد خيارات حفظ العرض التقديمي

تدعم Aspose.Cells صيغ إخراج متعددة، ولـ PowerPoint نستخدم `PresentationSaveOptions`. يتيح لنا هذا الكائن تحديد الهدف `SaveFormat.Pptx` وتعديل بعض الإعدادات المفيدة، مثل ما إذا كنا نريد تضمين الماكرو أو الحفاظ على عرض الأعمدة الأصلي.

```csharp
            // Step 2: Set up presentation save options for PowerPoint format
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                // Optional: keep the original Excel formatting as much as possible
                // (true by default, but we set it explicitly for clarity)
                KeepOriginalFormatting = true
            };
```

**لماذا هذا مهم:** بدون الإعدادات الصحيحة، قد تبدو الشرائح الناتجة مضغوطة أو تفقد التنسيق. من خلال إخبار Aspose.Cells أننا نريد ملف PPTX حقيقي، نضمن أن التحويل يحافظ على تخطيط Excel.

### الخطوة 3 – حفظ المصنف كعرض PowerPoint

الآن يحدث السحر. استدعاء واحد لـ `Save` يكتب ملف `.pptx` يعكس أول ورقة عمل في المصنف (أو جميع الأوراق، حسب نسخة المكتبة). في معظم السيناريوهات تكون الورقة الأولى كافية، لكن يمكنك التجربة لاحقًا.

```csharp
            // Step 3: Save the workbook as a PowerPoint presentation
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"Success! '{outputPath}' has been created.");
        }
    }
}
```

**ما ستراه:** افتح `output.pptx` في PowerPoint وستجد كل ورقة عمل تحولت إلى شريحة. خلايا النص تصبح مربعات نص، والمخططات تصبح مخططات PowerPoint أصلية، وحتى الصور تحتفظ بدقتها الأصلية.

## إنشاء PowerPoint من Excel – نصائح إعداد المشروع

- **تثبيت NuGet:** نفّذ `dotnet add package Aspose.Cells` من مجلد المشروع. سيجلب ذلك أحدث نسخة مستقرة (اعتبارًا من مارس 2026، النسخة 23.10).  
- **منصة الهدف:** إذا كنت تستخدم .NET Core، تأكد من أن ملف `csproj` يحتوي على `<TargetFramework>net6.0</TargetFramework>`.  
- **مسارات الملفات:** استخدم `Path.Combine` لضمان الأمان عبر الأنظمة، خاصة إذا كان الكود يعمل داخل حاويات Linux.  

```csharp
using System.IO;

// Example of safe path building
string baseDir = AppDomain.CurrentDomain.BaseDirectory;
string inputPath = Path.Combine(baseDir, "input.xlsx");
string outputPath = Path.Combine(baseDir, "output.pptx");
```

## تحويل Xlsx إلى Pptx – معالجة أوراق عمل متعددة

بشكل افتراضي تقوم Aspose.Cells بتحويل **ورقة العمل النشطة فقط**. إذا كنت تحتاج شريحة لكل ورقة، يمكنك التكرار عبر المجموعة وحفظ كل واحدة على حدة:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet sheet = workbook.Worksheets[i];
    sheet.IsSelected = true; // Make this sheet the active one
    string slidePath = Path.Combine(baseDir, $"Slide_{i + 1}.pptx");
    workbook.Save(slidePath, saveOptions);
}
```

**نصيحة احترافية:** بعد كل تكرار، استدعِ `workbook.Worksheets[i].IsSelected = false` إذا كنت تخطط لإعادة استخدام نفس كائن `Workbook` لعمليات أخرى.

## كيفية تحويل Excel – التعامل مع الملفات الكبيرة

المصنفات الكبيرة (مئات الميغابايت) قد تجهد الذاكرة. بعض الحيل تحافظ على سلاسة العملية:

1. **تمكين البث:** `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` يجبر Aspose.Cells على استخدام ملفات مؤقتة بدلاً من تحميل كل شيء في الذاكرة.  
2. **تخطي الصفوف/الأعمدة الفارغة:** اضبط `saveOptions.IgnoreEmptyRows = true` لتقليل الفوضى في الشرائح.  
3. **تغيير حجم الصور:** إذا كان Excel يحتوي على صور عالية الدقة، يمكنك تقليل حجمها قبل التحويل باستخدام `ImageResizeOptions`.  

```csharp
workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;
saveOptions.IgnoreEmptyRows = true;
saveOptions.ImageResizeOptions = new ImageResizeOptions
{
    Width = 1024,
    Height = 768,
    ResizeMode = ResizeMode.Proportional
};
```

## إنشاء Pptx من Excel – التحقق من النتيجة

بعد انتهاء استدعاء `Save`، ستحتاج إلى التأكد من أن الملف قابل للاستخدام:

```csharp
if (File.Exists(outputPath))
{
    var fileInfo = new FileInfo(outputPath);
    Console.WriteLine($"File size: {fileInfo.Length / 1024} KB");
    // Optionally launch PowerPoint automatically (Windows only)
    System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
    {
        FileName = outputPath,
        UseShellExecute = true
    });
}
else
{
    Console.Error.WriteLine("Something went wrong – the PPTX was not created.");
}
```

فتح الملف يجب أن يظهر مجموعة شرائح تعكس تخطيط جدول البيانات الأصلي، مع المخططات والجداول وأي صور مدمجة.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني الحفاظ على ماكرو Excel؟* | لا. لا يدعم PowerPoint ماكرو VBA من Excel. سيتعين عليك إعادة إنشاء أي أتمتة داخل PowerPoint نفسه. |
| *ماذا عن تعليقات الخلايا؟* | تتحول إلى مربعات نص منفصلة على الشريحة، لكن يمكنك إخفاؤها بتعيين `saveOptions.IncludeCellComments = false`. |
| *هل يتم تقييم الصيغ؟* | نعم—تقوم Aspose.Cells بتقييم الصيغ قبل التحويل، لذا تعرض الشريحة القيم المحسوبة وليس الصيغ نفسها. |
| *هل هناك طريقة لتخصيص تصميم الشريحة؟* | يمكنك تطبيق قالب PowerPoint بعد التحويل باستخدام فئة `Presentation` من Aspose.Slides، ثم نسخ الشرائح المولدة إليه. |

## مثال كامل يعمل (كل الكود في مكان واحد)

```csharp
using Aspose.Cells;
using System;
using System.IO;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build safe file paths
            string baseDir = AppDomain.CurrentDomain.BaseDirectory;
            string inputPath = Path.Combine(baseDir, "input.xlsx");
            string outputPath = Path.Combine(baseDir, "output.pptx");

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Optional: improve memory usage for huge files
            workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;

            // Configure PowerPoint save options
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                KeepOriginalFormatting = true,
                IgnoreEmptyRows = true,
                ImageResizeOptions = new ImageResizeOptions
                {
                    Width = 1024,
                    Height = 768,
                    ResizeMode = ResizeMode.Proportional
                }
            };

            // Save as PowerPoint
            workbook.Save(outputPath, saveOptions);

            // Verify the result
            if (File.Exists(outputPath))
            {
                Console.WriteLine($"Success! '{outputPath}' created ({new FileInfo(outputPath).Length / 1024} KB).");
                // Open the file automatically (Windows only)
                System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            else
            {
                Console.Error.WriteLine("Failed to create the PowerPoint file.");
            }
        }
    }
}
```

شغّل البرنامج، وستحصل على ملف `.pptx` جديد جاهز لاجتماع العميل التالي، أو عرض مجلس الإدارة، أو ملخص داخلي.

## الخلاصة

أنت الآن تعرف **كيفية تحويل Excel إلى PowerPoint** باستخدام C# و Aspose.Cells. الخطوات الأساسية—تحميل المصنف، ضبط `PresentationSaveOptions`، واستدعاء `Save`—بسطة، ومع ذلك يغطي الدرس أيضًا تفاصيل **إنشاء PowerPoint من Excel** مثل التعامل مع الذاكرة،

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}