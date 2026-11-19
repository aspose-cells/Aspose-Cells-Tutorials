---
category: general
date: 2026-11-19
description: كيفية تصدير مخطط Excel كصورة PNG باستخدام Aspose.Cells. تعلم حفظ صورة
  مخطط Excel وتعيين تنسيق الصورة PNG في بضع خطوات فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: ar
lastmod: 2026-11-19
og_description: كيفية تصدير مخطط Excel كصورة PNG باستخدام Aspose.Cells. اتبع هذا الدليل
  خطوة بخطوة لحفظ صورة مخطط Excel وتعيين تنسيق الصورة PNG بكفاءة.
og_image_alt: How to export Excel chart as a PNG image
og_title: كيفية تصدير مخطط Excel كصورة PNG – دليل سريع بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: كيفية تصدير مخطط إكسل كصورة PNG باستخدام C#
url: /ar/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير مخطط Excel كصورة PNG باستخدام C#

إذا كنت بحاجة إلى **how to export Excel chart** إلى صورة محمولة، يوضح هذا الدليل حلاً كاملاً وجاهزًا للتنفيذ. باستخدام Aspose.Cells يمكنك **save Excel chart image** بتنسيق PNG باستخدام ثلاث أسطر من الشيفرة فقط، كما يشرح الدليل أيضًا كيفية **set image format png** و **save Excel picture file** بأمان.

ستنتهي من هذه المقالة ببرنامج قابل للتنفيذ يقوم بتحميل دفتر عمل، ويُظهر المخطط الأول، ويكتب ملف `pivot.png` إلى القرص. لا أدوات إضافية، ولا نسخ‑لصق يدوي—فقط شفرة C# نظيفة يمكنك إدراجها في أي مشروع .NET.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6.0 SDK أو أحدث (الشيفرة تعمل أيضًا مع .NET Framework 4.6+)
* Visual Studio 2022 أو أي محرر C#
* رخصة Aspose.Cells for .NET (أو مفتاح تقييم مؤقت)
* ملف Excel (`pivot.xlsx`) يحتوي على مخطط واحد على الأقل في ورقة العمل الأولى

هذه العناصر هي الاعتمادات الخارجية الوحيدة؛ الدليل لا يتطلب تثبيت Office على الجهاز.

## الخطوة 1: تثبيت Aspose.Cells

افتح الطرفية في مجلد المشروع الخاص بك وشغّل:

```bash
dotnet add package Aspose.Cells
```

الحزمة تضيف مساحة الأسماء `Aspose.Cells`، التي توفر الفئات `Workbook` و `ImageOrPrintOptions` وغيرها المطلوبة لـ **save Excel chart image**.

## الخطوة 2: إنشاء برنامج وحدة تحكم بسيط

أنشئ تطبيق وحدة تحكم جديد (`dotnet new console -n ExportChartDemo`) واستبدل ملف `Program.cs` الذي تم إنشاؤه تلقائيًا بالكود التالي. البرنامج يوضح **how to export Excel chart** ويتضمن تعليقات تشرح كل قرار.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### لماذا كل جزء مهم

* **Loading the workbook** – `Workbook` يقوم بتحليل ملف `.xlsx` دون الحاجة إلى تثبيت Microsoft Excel.
* **ImageOrPrintOptions** – هذا الكائن يتحكم في تنسيق الإخراج. تعيين `ImageFormat = ImageFormat.Png` **sets image format png**, وهو تنسيق غير فقدان البيانات ومدعوم على نطاق واسع.
* **RenderToImage** – طريقة `RenderToImage` تحوّل المخطط (كائن `Picture`) إلى ملف صورة. الطريقة تتعامل أيضًا مع التحجيم، DPI، والشفافية تلقائيًا.
* **Error handling** – الفحص `sheet.Pictures.Count == 0` يمنع استثناء وقت التشغيل إذا لم تحتوي ورقة العمل على مخططات، وهو حالة شائعة عندما يشير المستخدم إلى الورقة الخاطئة.

## الخطوة 3: تشغيل البرنامج والتحقق من النتيجة

1. بناء المشروع: `dotnet build`.
2. تشغيله: `dotnet run --project ExportChartDemo`.

إذا تم تكوين كل شيء بشكل صحيح، سترى:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

افتح `pivot.png` باستخدام أي عارض صور. يجب أن ترى التمثيل البصري الدقيق لمخطط Excel، مما يؤكد أنك نجحت في **save Excel picture file**.

### النتيجة المتوقعة

فيما يلي مثال لما قد يبدو عليه ملف PNG المصدر (المخطط الفعلي يعتمد على ملف المصدر الخاص بك).

![Exported Excel chart saved as PNG image](images/exported-chart.png){: .center alt="كيفية تصدير مخطط Excel كصورة PNG"}

## الخطوة 4: خيارات متقدمة – تصدير مخططات متعددة

إذا كان دفتر العمل يحتوي على أكثر من مخطط واحد، يمكنك التكرار عبر مجموعة `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

هذا النمط يتيح لك **save Excel chart image** لكل مخطط في الورقة، وهو مفيد لأنابيب التقارير.

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `ArgumentOutOfRangeException` on `Pictures[0]` | ورقة العمل لا تحتوي على مخطط أو المخطط موجود في ورقة مختلفة. | تحقق من فهرس الورقة (`Worksheets[0]`) وتأكد من وجود المخطط. استخدم `Worksheets["SheetName"]` إذا لزم الأمر. |
| Exported image is blurry | تم ضبط DPI منخفض جدًا (الافتراضي 96). | قم بزيادة `HorizontalResolution` و `VerticalResolution` في `ImageOrPrintOptions`. |
| PNG file is empty or corrupted | عدم وجود رخصة مما يسبب قيود التقييم. | طبق رخصة Aspose.Cells صالحة قبل تحميل دفتر العمل (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| File path errors (`FileNotFoundException`) | عنصر نائب `YOUR_DIRECTORY` غير صحيح. | استخدم مسارات مطلقة أو `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

معالجة هذه المشكلات تضمن تجربة سلسة لـ **save excel picture file**.

## نصيحة احترافية: التصدير مباشرة إلى تدفق الذاكرة

أحيانًا تحتاج الصورة في الذاكرة (مثلاً، للرفع إلى واجهة ويب API) بدلاً من كتابتها إلى القرص:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

منطق **set image format png** نفسه ينطبق؛ فقط استبدل مسار الملف بتدفق.

## الخلاصة

أنت الآن تعرف **how to export Excel chart** كملف PNG باستخدام Aspose.Cells for .NET. شمل الدليل:

* تثبيت المكتبة
* تحميل دفتر عمل
* **Setting image format png**
* **Saving Excel chart image** إلى القرص
* معالجة مخططات متعددة والأخطاء الشائعة

مع هذا الأساس يمكنك دمج تصدير المخططات في تقارير آلية، خدمات ويب، أو أدوات سطح مكتب. بعد ذلك، استكشف المواضيع ذات الصلة مثل **save excel picture file** كـ JPEG (`ImageFormat.Jpeg`) أو تحويل المخططات إلى PDF لتقارير قابلة للطباعة.

برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحويل مخطط Excel الدائري إلى صورة باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [تصدير المخطط كـ PNG – دليل كامل لتحويل Excel إلى HTML باستخدام Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [تصدير خلايا Excel إلى صورة باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}