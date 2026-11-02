---
category: general
date: 2026-06-08
description: تصدير نطاق Excel كصورة باستخدام C# و Aspose.Cells. تعلّم كيفية حفظ ورقة
  عمل Excel كصورة في بضع خطوات بسيطة فقط.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: ar
og_description: تصدير نطاق Excel كصورة باستخدام C#. يوضح لك هذا الدليل كيفية حفظ ورقة
  عمل Excel كصورة بسرعة وبشكل موثوق.
og_title: تصدير نطاق إكسل كصورة – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: تصدير نطاق إكسل كصورة – دليل C# الكامل
url: /ar/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير نطاق إكسل كصورة – دليل C# كامل

هل احتجت يومًا إلى **export Excel range as image** لكن لم تكن متأكدًا من أي استدعاء API تستخدمه؟ لست وحدك. سواء كنت تبني لوحة تقارير أو تحتاج إلى لقطة من جدول محوري لعرض PowerPoint، تحويل مجموعة خلايا إلى PNG هو حيلة مفيدة.

في هذا الدليل سنستعرض مثالًا مستقلًا لا يقتصر فقط على **export excel range as image** بل يُظهر لك أيضًا كيفية **save excel worksheet as image** للورقة بأكملها. لا سكريبتات خارجية، فقط C# صافية و Aspose.Cells، بحيث يمكنك نسخ‑لصق الشيفرة ومشاهدة النتيجة فورًا.

## ما ستتعلمه

- تحميل مصنف موجود وتحديد نطاق معين (جدول محوري أو أي مجموعة خلايا).  
- ضبط خيارات تصدير الصورة مثل الصيغة، الدقة، والتحجيم.  
- تصدير نطاق واحد إلى PNG أو JPEG أو BMP.  
- توسيع نفس المنطق لـ **save excel worksheet as image** في سطر واحد.  
- نصائح للتعامل مع جداول محورية متعددة، نطاقات كبيرة، ومشكلات شائعة.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- Aspose.Cells for .NET ≥ 23.9 (يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose).  
- فهم أساسي للغة C# وإدخال/إخراج الملفات.  

إذا كان لديك ذلك، فلنبدأ.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ تطبيق console جديد (أو دمج الشيفرة في أي مشروع موجود). أضف حزمة Aspose.Cells عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

بعد ذلك استورد المساحات الاسمية المطلوبة:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **نصيحة احترافية:** احتفظ بعبارات `using` في أعلى الملف؛ فهذا يجعل الشيفرة أسهل للقراءة—خصوصًا عندما تضيف ميزات Aspose لاحقًا.

## الخطوة 2: تحميل المصنف الذي يحتوي على النطاق المستهدف

تحتاج إلى مصنف موجود على القرص. استبدل `YOUR_DIRECTORY/input.xlsx` بالمسار الفعلي لملفك.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

لماذا هذه الخطوة مهمة: كائن `Workbook` هو نقطة الدخول لكل عملية في Aspose.Cells. بدون ذلك لا يمكنك الإشارة إلى أوراق العمل أو النطاقات أو الجداول المحورية.

## الخطوة 3: تحديد النطاق المراد تصديره

لديك سيناريوهين شائعين:

1. **جدول محوري محدد** – الكود الذي قدمته يستخدم `PivotTables[0].PivotTableRange`.  
2. **مجموعة خلايا عشوائية** – يمكنك استخدام `worksheet.Cells.CreateRange("B2:D10")`.

في الأسفل نتعامل مع كلا الحالتين، لتختار ما يناسب حالتك.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **لماذا نتحقق من الجداول المحورية أولاً:** العديد من ملفات التقارير تعتمد على بيانات محورية ديناميكية. إذا لم توجد، يضمن fallback أن الدرس سيعمل على أي حال.

## الخطوة 4: ضبط خيارات تصدير الصورة

توفر لك Aspose.Cells تحكمًا دقيقًا في صورة الإخراج. أكثر الإعدادات شيوعًا هي الصيغة، الدقة (DPI)، وما إذا كنت تريد تضمين خطوط الشبكة.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

يمكنك تغيير `ImageFormat.Jpeg` أو `ImageFormat.Bmp` إذا كان نظامك المستقبلي يفضّل هذه الأنواع. إعداد DPI مهم عندما تدمج الصورة في ملفات PDF أو عروض شرائح عالية الدقة.

## الخطوة 5: تصدير النطاق (أو ورقة العمل بالكامل) كصورة

الآن يحدث السحر. طريقة `ToImage` تكتب التمثيل البصري للنطاق مباشرةً إلى القرص.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### ما يفعله الكود

- `exportRange.ToImage` يلتقط فقط الخلايا داخل النطاق (الجدول المحوري أو المجموعة المخصصة).  
- `worksheet.ToImage` يلتقط *المنطقة المرئية بالكامل* للورقة، وبالتالي **save excel worksheet as image**.  

كلا الاستدعائين يحترمان الخيارات التي ضبطتها مسبقًا—وبالتالي ستحصل على ملفات PNG بدقة 300 DPI.

## معالجة الحالات الخاصة والأسئلة الشائعة

### جداول محورية متعددة

إذا كان المصنف يحتوي على أكثر من جدول محوري، يمكنك التكرار عبرهم:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### نطاقات كبيرة جدًا

تصدير نطاق ضخم (مثلاً آلاف الصفوف) قد يستهلك الكثير من الذاكرة. خفّف ذلك عبر:

- تقليل `HorizontalResolution` / `VerticalResolution`.  
- التصدير على أجزاء (تقسيم النطاق إلى كتل أصغر).  

### خلفيات شفافة

إذا كنت تحتاج خلفية شفافة (مفيدة لتراكبها على صفحات الويب)، اضبط لون الخلفية إلى `Color.Transparent` قبل التصدير:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### أذونات الملفات

تأكد من وجود المجلد المستهدف وأن عمليتك لديها صلاحية كتابة. وإلا سيُطلق `ToImage` استثناء `IOException`.

## مثال كامل يعمل

بجمع كل ذلك، إليك برنامج console جاهز للتنفيذ:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**الناتج المتوقع** (console):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

افتح ملفات PNG المُولدة وسترى لقطة دقيقة للبيكسل للنطاق المحدد والورقة بالكامل على التوالي.

## الخلاصة

لقد غطينا الآن كل ما تحتاجه لـ **export excel range as image** وكذلك كيفية **save excel worksheet as image** باستخدام Aspose.Cells و C#. من تحميل المصنف إلى ضبط خيارات الصورة ومعالجة الجداول المحورية المتعددة، الخطوات بسيطة وقابلة للتكرار بالكامل.

بعد ذلك، قد ترغب في:

- تجربة قيم `ImageFormat` مختلفة (JPEG، BMP).  
- دمج الصورة مع PDF باستخدام فئة `Document` لتوليد التقارير.  
- أتمتة العملية لمجموعة من الملفات في مجلد.

لا تتردد في تعديل المقتطف ليتناسب مع سير عملك—سواء كنت تُرسل الصور إلى API ويب، أو تُدمجها في رسائل البريد الإلكتروني، أو تُنشئ تقارير قابلة للطباعة. برمجة سعيدة، ودع الصور تتحدث عن بيانات إكسل الخاصة بك!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تصدير خلايا إكسل إلى صورة باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [تصدير مصنف إكسل كصورة باستخدام Aspose.Cells للـ Java: دليل خطوة بخطوة](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [تصدير مصنف إكسل كصورة باستخدام Aspose Cells للـ Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}