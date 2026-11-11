---
category: general
date: 2026-10-01
description: إنشاء PowerPoint من Excel باستخدام Aspose.Cells في C#. تصدير Excel إلى
  PowerPoint وتحويل XLSX إلى PPTX بسرعة مع مثال كامل للكود.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: ar
lastmod: 2026-10-01
og_description: إنشاء عرض PowerPoint من Excel باستخدام Aspose.Cells في C#. تعلم كيفية
  تصدير Excel إلى PowerPoint وتحويل XLSX إلى PPTX ببضع أسطر من الشيفرة.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: إنشاء PowerPoint من Excel باستخدام Aspose.Cells – دليل سريع
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: إنشاء عرض PowerPoint من Excel باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PowerPoint من Excel باستخدام Aspose.Cells – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إنشاء PowerPoint من Excel**، يوضح لك هذا الدليل كيفية القيام بذلك باستخدام Aspose.Cells for .NET. ستتعلم **تصدير Excel إلى PowerPoint**، تحويل مصنف XLSX إلى عرض تقديمي PPTX، وتخصيص الشرائح الناتجة دون مغادرة مشروع C# الخاص بك.

يغطي الدليل كل ما تحتاجه لتشغيل الكود على .NET 6 أو أحدث، بما في ذلك إعداد المشروع، حزم NuGet المطلوبة، ومثال كامل قابل للتنفيذ. في النهاية، ستحصل على ملف PowerPoint يحتوي على المخطط الأصلي في Excel تمامًا كما يظهر في المصنف.

## ما ستحتاجه

| المتطلبات المسبقة | السبب |
|---|---|
| .NET 6 SDK أو أحدث | يوفر بيئة التشغيل لتطبيق وحدة التحكم C# |
| Visual Studio 2022 (أو أي بيئة تطوير) | يسهّل إنشاء المشروع وتصحيح الأخطاء |
| حزمة Aspose.Cells for .NET عبر NuGet | توفر فئة `Workbook` وواجهات برمجة التطبيقات للتصدير |
| ملف Excel (`.xlsx`) يحتوي على مخطط واحد على الأقل | البيانات المصدر لشريحة PowerPoint |

> **نصيحة محترف:** يعمل Aspose.Cells على Windows وLinux وmacOS، لذا يمكنك تشغيل نفس الكود داخل حاويات Docker أو خطوط أنابيب CI.

## الخطوة 1: إنشاء مشروع وحدة تحكم جديد وإضافة Aspose.Cells

افتح الطرفية (أو وحدة تحكم مدير الحزم في Visual Studio) وشغّل:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

أمر `dotnet add package` يقوم بتنزيل أحدث نسخة مستقرة من **Aspose.Cells**، والتي تتضمن طريقة `ExportPptx` المستخدمة لاحقًا.

## الخطوة 2: إضافة مصنف Excel المصدر

ضع ملف Excel الذي تريد تحويله داخل مجلد المشروع. في هذا الدليل نستخدم `ChartOle.xlsx`، الذي يحتوي على مخطط واحد في ورقة العمل الأولى.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## الخطوة 3: كتابة الكود الذي **ينشئ PowerPoint من Excel**

افتح `Program.cs` واستبدل محتوياته بالكود التالي. يوضح المثال عملية **التصدير الأساسية** ويظهر أيضًا كيفية التعامل مع الحالات الشائعة مثل الملفات المفقودة وأنواع المخططات غير المدعومة.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### لماذا يعمل هذا

* `Workbook` يقرأ ملف Excel بالكامل، بما في ذلك المخططات المدمجة والجداول والتنسيقات.
* `ExportPptx` يحول ورقة العمل النشطة إلى مجموعة شرائح PPTX. تقوم الطريقة تلقائيًا بتحويل مخططات Excel إلى أشكال PowerPoint، مع الحفاظ على الدقة البصرية.
* يحيط الكود العملية بكتلة `try/catch` لتظهر الأخطاء مثل فشل **convert XLSX to PPTX** الناتجة عن ملفات تالفة.

## الخطوة 4: تشغيل البرنامج والتحقق من الناتج

نفّذ التطبيق:

```bash
dotnet run
```

يجب أن ترى رسالة في وحدة التحكم:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

افتح `Exported.pptx` في Microsoft PowerPoint أو أي عارض متوافق. تعرض الشريحة الأولى المخطط تمامًا كما ظهر في `ChartOle.xlsx`. هذا يؤكد أنك نجحت في **إنشاء PowerPoint من Excel**.

## الخطوة 5: متقدم – تصدير عدة أوراق عمل أو تخطيطات شرائح مخصصة

المثال الأساسي يصدر ورقة العمل الأولى فقط. في السيناريوهات الواقعية قد تحتاج إلى:

* **تصدير عدة أوراق عمل** إلى شرائح منفصلة.
* **التحكم في حجم الشريحة** أو إضافة عنصر نائب للعنوان.
* **تضمين أوراق العمل المخفية** في التحويل.

فيما يلي مقتطف مختصر ي iterates عبر جميع أوراق العمل ويضيف كل واحدة كشريحة منفصلة:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **ملاحظة:** يتطلب المقتطف المتقدم مكتبة **Aspose.Slides for .NET**. إذا كنت تحتاج فقط إلى تحويل ورقة واحدة بسيطة، فإن استدعاء `ExportPptx` السابق يكفي.

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|---|---|---|
| شريحة فارغة بعد التصدير | ورقة العمل لا تحتوي على كائنات مرئية | تأكد من وجود مخطط أو جدول أو شكل على الأقل قبل استدعاء `ExportPptx`. |
| فقدان الخطوط في PowerPoint | الخط غير مثبت على الجهاز الذي يُفتح عليه PPTX | دمج الخطوط المطلوبة في مصنف Excel أو تثبيتها على النظام الهدف. |
| مقياس غير متوقع | المخطط كبير يتجاوز أبعاد الشريحة | اضبط خاصية `PageSetup.Zoom` لورقة العمل قبل التصدير. |
| `convert XLSX to PPTX` يطرح `NotSupportedException` | نوع المخطط غير مدعوم من Aspose.Cells (مثل الخرائط ثلاثية الأبعاد) | استبدل المخطط بنوع مدعوم أو صدّر الورقة كصورة أولاً. |

معالجة هذه الحالات الطرفية تضمن سير عمل **تصدير Excel إلى PowerPoint** موثوقًا في بيئات الإنتاج.

## الخلاصة

أنت الآن تعرف كيف **تنشئ PowerPoint من Excel** باستخدام Aspose.Cells for .NET. غطّى الدليل:

* إعداد المشروع وتثبيت حزمة NuGet
* تحميل مصنف Excel واستدعاء `ExportPptx`
* تشغيل الكود وتأكيد إنشاء ملف PPTX
* توسيع الحل للتعامل مع أوراق عمل متعددة وتخطيطات مخصصة
* نصائح عملية لتجنب مشاكل التحويل الشائعة

بهذا المعرفة يمكنك أتمتة إنشاء التقارير، بناء خطوط أنابيب للعرض التقديمي، أو دمج تحويل Excel إلى PowerPoint في أي تطبيق C#. جرّب أنواع مخططات مختلفة، أضف عناوين للشرائح، أو اجمع التصدير مع Aspose.Slides لإنشاء عروض تقديمية متكاملة الميزات.

--- 

*هل ترغب في استكشاف المزيد؟ ألقِ نظرة على المواضيع ذات الصلة مثل **convert Excel to PDF**، **embed Excel data in Word**، أو **use Aspose.Slides to programmatically edit PPTX files**.*

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}