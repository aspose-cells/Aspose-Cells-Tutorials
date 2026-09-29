---
category: general
date: 2026-02-23
description: تحديث جدول محوري في Excel باستخدام C# وتصديره كصورة PNG. تعلم كيفية تحميل
  ملف Excel في C#، تحديث الجدول المحوري، وحفظ النتيجة.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: ar
og_description: تحديث جدول Pivot في Excel باستخدام C# وتصديره كصورة PNG. دليل خطوة
  بخطوة مع الكود الكامل ونصائح عملية.
og_title: تحديث جدول Pivot في Excel باستخدام C# – تصدير كصورة PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: تحديث جدول محوري في Excel باستخدام C# – تصدير كصورة PNG
url: /ar/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديث جدول محوري في Excel باستخدام C# – تصدير كصورة PNG

هل احتجت يومًا إلى **تحديث جدول محوري في Excel** من تطبيق C# ثم تحويله إلى صورة؟ لست الوحيد الذي يحاول حل ذلك. في هذا الدرس سنستعرض خطوة بخطوة كيفية **refresh Excel pivot table**، **load Excel workbook C#**، وأخيرًا **export pivot as image** — كل ذلك في مقتطف نظيف وقابل للتنفيذ.

ما ستحصل عليه في النهاية هو ملف PNG يبدو تمامًا كالجدول المحوري الذي تراه في Excel، جاهز لتضمينه في التقارير أو الرسائل الإلكترونية أو لوحات المعلومات. لا نسخ‑لصق يدوي، ولا تعقيدات COM interop، فقط كود .NET بسيط.

## المتطلبات المسبقة

- .NET 6+ (or .NET Framework 4.7+)
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو نسخة مرخصة) – يمكنك الحصول عليها من NuGet باستخدام `Install-Package Aspose.Cells`.
- ملف `input.xlsx` موجود يحتوي على جدول محوري واحد على الأقل.
- مجلد لديك صلاحية كتابة فيه لصورة الإخراج.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فعّل **nullable reference types** (`<Nullable>enable</Nullable>`) لاكتشاف الأخطاء المتعلقة بـ null مبكرًا.

---

## الخطوة 1: تحميل مصنف Excel في C#

أول شيء نحتاجه هو كائن `Workbook` يشير إلى ملف المصدر الخاص بنا. فكر في ذلك كفتح ملف Excel برمجيًا.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**لماذا هذا مهم:** تحميل المصنف يمنحنا الوصول إلى الأوراق، الخلايا، والأهم من ذلك الجداول المحورية التي أنشأتها. إذا لم يُعثر على الملف، تقوم Aspose بإلقاء استثناء `FileNotFoundException` واضح، يمكنك التقاطه لتوفير معالجة سلسة.

---

## الخطوة 2: تكوين خيارات تصدير الصورة (تصدير الجدول المحوري كصورة)

تتيح لك Aspose.Cells تحديد كيفية عرض الجدول المحوري. هنا نطلب PNG لأنه بدون فقدان الجودة ومدعوم على نطاق واسع.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**لماذا PNG؟** على عكس JPEG، يحافظ PNG على خطوط الشبكة الواضحة وتظليل النص الذي تعتمد عليه الجداول المحورية. إذا كنت بحاجة إلى ملف أصغر، يمكنك التحويل إلى `ImageFormat.Jpeg` وضبط الجودة، لكنك ستفقد بعض الوضوح.

---

## الخطوة 3: تحديث الجدول المحوري

قبل أن نلتقط الصورة، يجب أن نتأكد من أن الجدول المحوري يعكس أحدث البيانات. هذا هو جوهر **refresh excel pivot table**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**ما الذي يحدث خلف الكواليس؟** `Refresh()` يعيد حساب الجدول المحوري بناءً على النطاق المصدر. إذا أضفت صفوفًا إلى البيانات المصدر بعد حفظ المصنف، فإن هذه الدالة ستجلبها. تخطي هذه الخطوة ينتج صورة قديمة لا تتطابق مع البيانات الحالية.

---

## الخطوة 4: تحويل الجدول المحوري إلى PNG (تصدير صورة جدول محوري Excel)

الآن بعد أن كل شيء محدث، يمكننا تحويل الجدول المحوري مباشرةً إلى ملف صورة.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**النتيجة:** افتح `pivot.png` وسترى لقطة دقيقة للجدول المحوري المحدث. يمكن إرفاق هذا الملف برسالة بريد إلكتروني، أو تضمينه في صفحة ويب، أو إدخاله في محرك تقارير.

### النتيجة المتوقعة

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

إذا كنت تتصفح المجلد، يجب أن يعرض PNG نفس الصفوف والأعمدة والفلاتر التي تراها في Excel.

---

## معالجة الحالات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **Multiple pivot tables** | Loop through `worksheet.PivotTables` and call `Refresh()` / `RenderToImage()` for each. |
| **Dynamic sheet names** | Use `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` or search by `worksheet.Name`. |
| **Large datasets** | Increase `imgOptions.OnePagePerSheet = false` and set `imgOptions.PageWidth`/`PageHeight` to control paging. |
| **Missing Aspose.Cells license** | The free trial adds a watermark. Acquire a license and call `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` before loading the workbook. |
| **File‑path issues** | Use `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` to avoid hard‑coded separators. |

---

## نصائح احترافية وأفضل الممارسات

- **Dispose properly** – غلف `Workbook` داخل كتلة `using` أو استدعِ `wb.Dispose()` عند الانتهاء لتحرير الموارد الأصلية.
- **Cache rendered images** – إذا كنت تحتاج إلى نفس صورة الجدول المحوري بشكل متكرر، احفظ PNG على القرص واستخدمه مرة أخرى بدلاً من إعادة تصييره في كل مرة.
- **Thread safety** – يجب على كل خيط (thread) العمل مع نسخة `Workbook` خاصة به؛ كائنات Aspose.Cells غير آمنة للاستخدام المتعدد الخيوط.
- **Performance** – قد يكون تصيير الجداول المحورية الكبيرة مستهلكًا للذاكرة. اضبط `imgOptions.ImageFormat` إلى `Bmp` للحصول على سرعة أكبر لكن ملفات أكبر، أو قلل الـ DPI لتسريع التصيير.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

شغّل البرنامج، افتح `pivot.png`، وسترى جدولًا محوريًا محدثًا تمامًا كما يظهر في Excel.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات .xlsx التي تم إنشاؤها بواسطة LibreOffice؟**  
ج: نعم. تقوم Aspose.Cells بقراءة تنسيق Open XML بغض النظر عن التطبيق الأصلي، لذا يمكنك **load excel workbook c#** من LibreOffice أو تصدير Google Sheets أو أي مصدر آخر.

**س: هل يمكنني تصدير عدة أوراق عمل في آن واحد؟**  
ج: بالتأكيد. قم بالتكرار عبر `wb.Worksheets` وطبق نفس منطق `RenderToImage` لكل ورقة. فقط تذكر إعطاء كل مخرج اسم ملف فريد.

**س: ماذا لو كان الجدول المحوري يستخدم مصدر بيانات خارجي؟**  
ج: يمكن لـ Aspose.Cells تحديث الاتصالات الخارجية إذا كانت مدمجة في الملف، لكن سيتعين عليك توفير سلسلة الاتصال والبيانات الاعتمادية برمجيًا. راجع وثائق Aspose لـ `DataSourceOptions`.

---

## الخلاصة

أصبح لديك الآن حل شامل من البداية للنهاية لـ **refresh excel pivot table** من C# و **export excel pivot image** كملف PNG. يوضح الكود كيفية **load excel workbook c#**، تكوين إعدادات الصورة، التأكد من أن الجدول المحوري يعكس أحدث البيانات، وأخيرًا تصييره إلى ملف.

بعد ذلك، قد ترغب في استكشاف **export pivot as image** بصيغ أخرى (PDF، SVG) أو أتمتة العملية لعدة مصنفات في مهمة دفعة. هل تريد تضمين PNG في تقرير Word؟ ففئة `ImageOrPrintOptions` نفسها تعمل مع Aspose.Words.

لا تتردد في التجربة، واكتشاف الأخطاء، وطرح الأسئلة في التعليقات — برمجة سعيدة! 

![Refresh Excel pivot table screenshot](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}