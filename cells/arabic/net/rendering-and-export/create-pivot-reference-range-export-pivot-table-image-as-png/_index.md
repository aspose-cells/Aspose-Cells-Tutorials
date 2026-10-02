---
category: general
date: 2026-02-09
description: إنشاء نطاق مرجعي محوري في C# وتصدير صورة جدول محوري. تعلم كيفية حفظ نطاق
  Excel كملف PNG باستخدام Aspose.Cells – دليل سريع وكامل.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: ar
og_description: إنشاء نطاق مرجعي للجدول المحوري في C# وتصدير صورة الجدول المحوري إلى
  PNG. دليل كامل خطوة بخطوة لحفظ نطاق Excel كملف PNG.
og_title: إنشاء نطاق مرجع Pivot – تصدير صورة جدول Pivot كملف PNG
tags:
- Aspose.Cells
- C#
- Excel
title: إنشاء نطاق مرجع محوري – تصدير صورة الجدول المحوري بصيغة PNG
url: /ar/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء نطاق مرجع لل Pivot – تصدير صورة جدول Pivot كملف PNG

هل تحتاج إلى **إنشاء نطاق مرجع لل Pivot** في مصنف Excel باستخدام C#؟ يمكنك أيضًا **تصدير صورة جدول Pivot** و **حفظ نطاق Excel كملف png** ببضع أسطر من الشيفرة فقط. في تجربتي، تحويل Pivot حي إلى صورة ثابتة طريقة مفيدة لتضمين التحليلات في التقارير أو الرسائل الإلكترونية أو لوحات التحكم دون الحاجة لسحب المصنف بالكامل.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: المكتبات المطلوبة، الشيفرة الدقيقة، لماذا كل استدعاء مهم، وبعض المشكلات التي قد تواجهها. بنهاية الدرس ستتمكن من إنشاء ملف PNG لأي جدول Pivot بثقة، وستفهم كيف تُكيّف النمط لعدة أوراق عمل أو صيغ صور مخصصة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يكفي للاختبار).  
- **.NET 6.0** أو أحدث – الـ API الذي نستخدمه متوافق تمامًا مع .NET Standard 2.0+، لذا الإطارات الأقدم ستُترجم أيضًا.  
- مشروع C# أساسي (تطبيق Console، WinForms، أو ASP.NET – أي شيء يمكنه الإشارة إلى حزمة NuGet).  

إذا لم تقم بتثبيت Aspose.Cells بعد، نفّذ:

```bash
dotnet add package Aspose.Cells
```

هذا كل ما تحتاجه – لا COM interop، ولا Excel مثبت على الخادم.

## الخطوة 1: فتح المصنف والوصول إلى الورقة الأولى

أول ما تقوم به هو تحميل ملف المصنف والحصول على الورقة التي تحتوي على جدول Pivot. نختار **الورقة الأولى** (`Worksheets[0]`) عمدًا لأن معظم ملفات العرض توضع فيها الـ Pivot، لكن يمكنك استبدال الفهرس باسم إذا رغبت.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*لماذا هذا مهم:* `Worksheet` هي نقطة الدخول لأي عملية تعتمد على النطاق. إذا أشرت إلى الورقة الخطأ، فإن استدعاء `PivotTables[0]` التالي سيثير استثناء `IndexOutOfRangeException`.

## الخطوة 2: إنشاء نطاق مرجع لل Pivot

الآن نطلب من جدول Pivot نفسه أن يعطينا **نطاق مرجع**. هذا النطاق يمثل الخلايا الدقيقة التي تُكوّن الـ Pivot – العناوين، صفوف البيانات، والمجاميع. الطريقة `CreateReferenceRange()` تقوم بالعمل الشاق داخليًا، مع معالجة الخلايا المدمجة والصفوف المخفية لك.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **نصيحة احترافية:** إذا كان المصنف يحتوي على عدة Pivot، قم بالتكرار عبر `worksheet.PivotTables` واختر ما تحتاجه عبر خاصية `Name`.

## الخطوة 3: تحويل نطاق المرجع إلى صورة

يمكن لـ Aspose.Cells تحويل أي `Range` إلى صورة. الكائن المرتجع يدعم صيغ raster (PNG, JPEG) و vector (SVG). هنا نطلب الصورة raster الافتراضية، وهي كائن متوافق مع `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*ما الذي يحدث في الخلفية؟* الـ API يلتقط لقطة مرئية لتخطيط النطاق، مع احترام أنماط الخلايا، الخطوط، والتنسيق الشرطي. إنه في الأساس نفس أخذ لقطة شاشة، لكن برمجيًا وبدون واجهة مستخدم.

## الخطوة 4: حفظ الصورة المولدة إلى ملف

أخيرًا، نقوم بحفظ الصورة. طريقة `Save` تختار PNG تلقائيًا عندما تُعطيها امتداد “.png”. يمكنك أيضًا تمرير كائن `SaveOptions` إذا احتجت للتحكم في DPI أو صيغة مختلفة.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

بعد تنفيذ هذا السطر، افتح `pivot.png` وسترى لقطة بكسلية دقيقة لجدول الـ Pivot، جاهزة للتضمين في أي مكان.

## مثال كامل يعمل

لنجمع كل ما سبق، إليك برنامج Console مستقل يمكنك نسخه ولصقه وتشغيله:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**الناتج المتوقع:** ملف اسمه `pivot.png` موجود في `YOUR_DIRECTORY`. افتحه بأي عارض صور – يجب أن ترى التخطيط الدقيق للـ Pivot الأصلي، بما في ذلك عناوين الأعمدة، صفوف البيانات، والمجاميع الكلية.

## تصدير صورة جدول Pivot – تخصيص الحجم والدقة (DPI)

أحيانًا تكون الصورة الافتراضية صغيرة جدًا للعرض في شريحة عرض. يمكنك التحكم في الدقة بتمرير كائن `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*لماذا نضبط DPI؟* DPI أعلى ينتج حواف أكثر وضوحًا، خاصةً عندما يتم تكبير PNG في PowerPoint أو PDF.

## حفظ نطاق Excel كملف PNG – التعامل مع أوراق عمل متعددة

إذا كنت بحاجة لتصدير Pivot من عدة أوراق، قم بالتكرار عبر `Workbook.Worksheets` وكرر الخطوات. إليك مقتطفًا مختصرًا:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

هذا النمط **export pivot table image** لكل Pivot في المصنف، ويُسمّى كل ملف باسم ورقته وPivot الخاص به – مثالي للمعالجة الدفعية.

## المشكلات الشائعة وكيفية تجنبها

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | Worksheet has no pivot tables. | Check `worksheet.PivotTables.Count` before accessing. |
| Blank image output | Pivot is filtered to hide all rows. | Ensure the pivot has visible data, or call `pivot.RefreshData();` before creating the range. |
| Low‑resolution PNG | Default DPI is 96. | Use `ImageOrVectorSaveOptions.Resolution` as shown above. |
| File‑path errors | Invalid characters in `YOUR_DIRECTORY`. | Use `Path.Combine` and `Path.GetInvalidPathChars()` to sanitize. |

## التحقق – اختبار سريع

بعد تشغيل المثال الكامل:

1. افتح `pivot.png` في Windows Photo Viewer.  
2. تحقق من أن عناوين الأعمدة، صفوف البيانات، وصفوف الإجمال تتطابق مع عرض Excel.  
3. إذا لاحظت فقدان صفوف، أعد التحقق من أن طريقة **RefreshData** للـ Pivot تم استدعاؤها قبل `CreateReferenceRange()`.

## مكافأة: تضمين PNG في مستند Word

نظرًا لأن الصورة بالفعل بصيغة PNG، يمكنك تمريرها مباشرة إلى Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

الآن لديك تقرير Word يحتوي على اللقطة الدقيقة للـ Pivot – دون الحاجة لنسخ‑لصق يدوي.

## الخلاصة

لقد تعلمت الآن كيفية **إنشاء نطاق مرجع لل Pivot**، **تصدير صورة جدول Pivot**، و **حفظ نطاق Excel كملف png** باستخدام Aspose.Cells في C#. النقاط الأساسية هي:

- استخدم `PivotTable.CreateReferenceRange()` لعزل المنطقة البصرية للـ Pivot.  
- حوّل ذلك النطاق إلى صورة عبر `Range.ToImage()`.  
- احفظ الصورة كـ PNG، مع إمكانية تعديل DPI لجودة الطباعة.  

من هنا يمكنك استكشاف تصدير دفعي، صيغ صور مختلفة (SVG, JPEG)، أو حتى تضمين PNG في ملفات PDF أو Word. السماء هي الحد عندما تمتلك الـ Pivot كرسمة ثابتة.

هل لديك أسئلة أو سيناريو صعب؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}