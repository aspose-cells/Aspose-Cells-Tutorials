---
category: general
date: 2026-05-23
description: تعلم كيفية تصدير جدول محوري كصورة وحفظ الجدول المحوري كصورة باستخدام
  Aspose.Cells في C#. كود خطوة بخطوة ونصائح.
draft: false
keywords:
- export pivot table as image
- save pivot table as picture
language: ar
og_description: تصدير جدول محوري كصورة وحفظ جدول محوري كصورة باستخدام Aspose.Cells.
  الكود الكامل، الشرح، وأفضل الممارسات.
og_title: تصدير جدول محوري كصورة باستخدام C# – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  headline: Export Pivot Table as Image with C# – Complete Guide
  type: TechArticle
- description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  name: Export Pivot Table as Image with C# – Complete Guide
  steps:
  - name: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
    text: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
  - name: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
    text: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
  - name: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
    text: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
  - name: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
    text: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
  - name: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
    text: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
  - name: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
    text: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
  - name: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
    text: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel automation
- PivotTable
- Image export
title: تصدير جدول محوري كصورة باستخدام C# – دليل كامل
url: /ar/net/pivot-tables/export-pivot-table-as-image-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير جدول محوري كصورة باستخدام C# – دليل شامل

هل تساءلت يومًا كيف **export pivot table as image** مباشرةً من ملف Excel دون أخذ لقطة شاشة؟ لست وحدك. في العديد من سيناريوهات التقارير—مثل لوحات التحكم الآلية أو مرفقات البريد الإلكتروني—وجود صورة واضحة لجدول محوري أسهل بكثير من ملف `.xlsx` خام.  

في هذا الدرس سنستعرض الخطوات الدقيقة لـ **export pivot table as image** وكذلك نغطي فن **save pivot table as picture** باستخدام مكتبة Aspose.Cells القوية. في النهاية ستحصل على برنامج C# مستقل يمكن تشغيله ينتج ملف PNG في المكان الذي تحتاجه.

## ما يغطيه هذا الدليل

- إعداد مشروع .NET مع Aspose.Cells  
- تحميل ملف عمل موجود وتحديد جدول المحوري المطلوب  
- تكوين خيارات تصدير الصورة (الدقة، الصيغة، إلخ)  
- تصدير جدول المحوري كملف صورة PNG فعليًا  
- المشكلات الشائعة—مثل التعامل مع أوراق العمل المخفية أو وجود جداول محورية متعددة—وكيفية تجنبها  

بدون سكربتات خارجية، بدون تعديل يدوي، مجرد كود يمكنك نسخه‑ولصقه وتشغيله.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. **.NET 6+** (أو .NET Framework 4.6+ إذا تفضل الكلاسيكي) مثبت.  
2. **رخصة** لـ Aspose.Cells — النسخة التجريبية المجانية تكفي للاختبار، لكن الرخصة تزيل علامة التقييم.  
3. ملف Excel (`Sample.xlsx`) يحتوي على جدول محوري واحد على ورقة تسمى *Sheet1* (يمكنك إعادة تسميتها لاحقًا).  

إذا كان أي من هذه غير متوفر، احصل على أحدث حزمة NuGet لـ Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

الآن بعد أن أصبح كل شيء جاهز، لنبدأ.

## الخطوة 1: تحميل ملف العمل والحصول على ورقة العمل

أولًا: نحتاج إلى فتح ملف العمل وتحديد الورقة التي تستضيف الجدول المحوري. هذه الخطوة هي الأساس لـ **export pivot table as image** لأنه بدون كائن `Worksheet` صالح لا يمكن للمكتبة العثور على الجدول.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // Path to the Excel file containing the pivot table
        string workbookPath = @"C:\Data\Sample.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(workbookPath);

        // Obtain the worksheet that contains the pivot table
        // Replace "Sheet1" with your actual sheet name if different
        Worksheet ws = workbook.Worksheets["Sheet1"];
```

> **لماذا هذا مهم:** تقوم Aspose.Cells بقراءة ملف العمل بالكامل في الذاكرة، لذا أي خطأ إملائي في اسم الورقة يسبب `ArgumentException`. تأكد دائمًا من وجود الورقة قبل المتابعة.

## الخطوة 2: الوصول إلى الجدول المحوري المطلوب

يمكن لملف العمل أن يحتوي على جداول محورية متعددة، لكن في معظم السيناريوهات البسيطة نحتاج فقط إلى الأول. إذا كان لديك عدة جداول، يمكنك التكرار عبر `ws.PivotTables` واختيار الجدول بالاسم.

```csharp
        // Access the first pivot table in the worksheet
        // If you know the pivot's name, you can use ws.PivotTables["MyPivot"]
        PivotTable pivot = ws.PivotTables[0];
```

> **نصيحة احترافية:** عندما يكون لديك أكثر من جدول محوري، استخدم `ws.PivotTables["PivotName"]` لتجنب تصدير الجدول الخطأ عن طريق الصدفة.

## الخطوة 3: تكوين خيارات تصدير الصورة

توفر Aspose.Cells تحكمًا دقيقًا في مخرجات الصورة. هنا سنضبط الصيغة إلى PNG، لكن يمكنك التبديل إلى JPEG أو BMP بتغيير `ImageFormat`. يمكنك أيضًا تعديل DPI، التحجيم، وما إذا كنت تريد تضمين خطوط الشبكة.

```csharp
        // Set up image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: increase resolution for sharper output
            // HorizontalResolution = 300,
            // VerticalResolution = 300,
            // Transparent = true   // if you need a transparent background
        };
```

> **لماذا نختار PNG:** يحافظ PNG على وضوح النص ويدعم الشفافية، مما يجعله مثاليًا للتضمين في التقارير أو صفحات الويب.

## الخطوة 4: تصدير جدول المحوري كملف صورة

الآن يحدث السحر. طريقة `ToImage` تكتب جدول المحوري إلى القرص بالصيغ التي ضبطناها. هذا هو جوهر **save pivot table as picture**.

```csharp
        // Define the output path – make sure the directory exists
        string outputPath = @"C:\Exports\pivot.png";

        // Export the pivot table as an image file
        pivot.ToImage(outputPath, imageOptions);

        System.Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

> **حالة حافة:** إذا لم يكن دليل الهدف موجودًا، فإن `ToImage` يطرح `DirectoryNotFoundException`. أنشئ المجلد أولًا أو استخدم `Directory.CreateDirectory(Path.GetDirectoryName(outputPath))`.

## الخطوة 5: التحقق من النتيجة

شغّل البرنامج (F5 في Visual Studio أو `dotnet run` من سطر الأوامر). انتقل إلى `C:\Exports\pivot.png` وسترى لقطة واضحة لجدولك المحوري، مطابقة تمامًا لما تراه داخل Excel.

![export pivot table as image example](https://example.com/images/pivot-export.png "export pivot table as image example")

*نص بديل للصورة: مثال على تصدير جدول محوري كصورة*

إذا بدت الصورة مقصوصة، عدّل خصائص `ImageOrPrintOptions` مثل `HorizontalResolution`، `VerticalResolution`، أو `OnePagePerSheet`. هذه التعديلات تسمح لك بـ **save pivot table as picture** بالأبعاد الدقيقة التي تحتاجها.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تصدير عدة جداول محورية مرة واحدة؟** | قم بالتكرار عبر `ws.PivotTables` واستدعِ `ToImage` لكل جدول، مع تغيير اسم ملف الإخراج في كل مرة. |
| **ماذا لو كان الجدول يحتوي على مخططات؟** | المخططات ليست جزءًا من منطقة بيانات الجدول المحوري، لذا لن تظهر. صَدِّر المخطط منفصلًا باستخدام `Chart.ToImage`. |
| **هل يعمل هذا مع ملفات عمل محمية بكلمة مرور؟** | نعم—حمّل ملف العمل باستخدام `Workbook(workbookPath, new LoadOptions { Password = "secret" })`. |
| **كيف أغيّر لون الخلفية؟** | اضبط `imageOptions.BackgroundColor = Color.White;` (أو أي لون من `System.Drawing.Color`). |
| **هل هناك طريقة للتصدير إلى JPEG لتقليل حجم الملف؟** | غيّر `ImageFormat = ImageFormat.Jpeg` ويمكنك أيضًا ضبط `imageOptions.JpegQuality = 80`. |

## نصائح احترافية لتصدير جاهز للإنتاج

1. **تحرير الموارد:** ضع `Workbook` داخل كتلة `using` أو استدعِ `workbook.Dispose()` لتحرير الذاكرة، خاصةً عند معالجة ملفات كبيرة.  
2. **سلامة الخيوط:** يجب أن يمتلك كل خيط نسخة `Workbook` خاصة به؛ كائنات Aspose.Cells غير آمنة للاستخدام المتعدد الخيوط.  
3. **التسجيل (Logging):** سجّل مسار التصدير وأي استثناءات في ملف سجل مركزي لتسهيل تتبع الأخطاء.  
4. **المعالجة الدفعية:** إذا كنت بحاجة لإنشاء صور لعشرات ملفات العمل، فكر في نظام طابور (مثل Azure Queue) لتوزيع الحمل.  

## مثال كامل يعمل

إليك البرنامج الكامل مرة أخرى، جاهز للنسخ‑واللصق:

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;
using System.IO;

class ExportPivotImage
{
    static void Main()
    {
        // 1️⃣ Load workbook
        string workbookPath = @"C:\Data\Sample.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // 2️⃣ Get worksheet containing the pivot
        Worksheet ws = workbook.Worksheets["Sheet1"]; // adjust if needed

        // 3️⃣ Grab the first pivot table
        if (ws.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found on the sheet.");
            return;
        }
        PivotTable pivot = ws.PivotTables[0];

        // 4️⃣ Set image export options (PNG is default)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Uncomment to increase DPI for sharper images
            // HorizontalResolution = 300,
            // VerticalResolution = 300
        };

        // 5️⃣ Ensure output directory exists
        string outputDir = @"C:\Exports";
        Directory.CreateDirectory(outputDir);
        string outputPath = Path.Combine(outputDir, "pivot.png");

        // 6️⃣ Export pivot table as image
        pivot.ToImage(outputPath, imageOptions);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

تشغيل هذا الكود سينتج ملف PNG باسم `pivot.png` في `C:\Exports`. افتحه بأي عارض صور وسترى نسخة بصرية مطابقة تمامًا لجدولك المحوري—مثالي للتقارير، الرسائل الإلكترونية، أو صفحات الويب.

## الخلاصة

لقد غطينا كل ما تحتاجه لـ **export pivot table as image** و **save pivot table as picture** باستخدام C# و Aspose.Cells. من تحميل ملف العمل إلى ضبط خيارات الصورة، العملية مباشرة وقابلة للبرمجة بالكامل.  

ما الخطوة التالية؟ جرّب صيغًا أخرى (JPEG، BMP)، زد الـ DPI للحصول على رسومات بجودة طباعة، أو عالج مجموعة من ملفات العمل دفعةً. يمكنك أيضًا استكشاف تصدير الورقة بالكامل كصورة إذا كنت تحتاج إلى السياق المحيط.  

هل لديك أسئلة إضافية أو سيناريو معقد؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## دروس ذات صلة

- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Master Pivot Table Formatting in .NET Using Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}