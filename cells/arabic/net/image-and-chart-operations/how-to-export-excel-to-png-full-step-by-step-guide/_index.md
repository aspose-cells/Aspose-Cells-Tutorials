---
category: general
date: 2026-08-11
description: كيفية تصدير Excel إلى PNG وحفظ نطاق Excel كصورة باستخدام Aspose.Cells.
  تعلم كيفية حفظ صورة ورقة Excel وتصدير صورة جدول محوري في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel to png
- save excel range as image
- save excel sheet picture
- export pivot table image
language: ar
lastmod: 2026-08-11
og_description: كيفية تصدير Excel إلى PNG بسرعة. يوضح هذا الدرس كيفية حفظ نطاق Excel
  كصورة، حفظ صورة ورقة Excel، وتصدير صورة جدول المحور باستخدام Aspose.Cells.
og_image_alt: Screenshot of C# code exporting an Excel worksheet to a PNG file
og_title: كيفية تصدير Excel إلى PNG – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to export Excel to PNG and save Excel range as image using Aspose.Cells.
    Learn to save Excel sheet picture and export pivot table image in minutes.
  headline: How to export Excel to PNG – full step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Excel automation
- C#
- image export
title: كيفية تصدير إكسل إلى PNG – دليل كامل خطوة بخطوة
url: /ar/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PNG – دليل خطوة بخطوة كامل

إذا كنت بحاجة إلى **كيفية تصدير Excel إلى PNG**، فإن هذا الدليل يشرح لك العملية بالكامل باستخدام Aspose.Cells for .NET. سواء كنت تريد **حفظ نطاق Excel كصورة**، أو تضمين صورة ورقة العمل في تقرير، أو **تصدير صورة جدول محوري** للوحة معلومات، فإن الخطوات أدناه توفر لك حلاً جاهزًا للتنفيذ.

سوف تتعلم كيفية تحميل دفتر عمل، وتحديث جدول محوري، وتكوين خيارات الصورة، وأخيرًا كتابة ملف PNG يحافظ على مظهر البيانات المصدر مع التنسيق. لا تحتاج إلى أدوات خارجية أو لقطات شاشة يدوية.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير C#)  
* ترخيص Aspose.Cells for .NET أو نسخة تقييم مجانية – قم بتنزيلها من [موقع Aspose.Cells](https://products.aspose.com/cells/net)  
* ملف Excel تجريبي (`PivotTable.xlsx`) يحتوي على جدول محوري واحد على الأقل  

يعمل الكود على Windows و macOS و Linux لأن Aspose.Cells مستقل عن المنصة.

## الخطوة 1: تثبيت Aspose.Cells عبر NuGet

افتح مجلد المشروع في الطرفية وشغّل الأمر التالي:

```bash
dotnet add package Aspose.Cells
```

يضيف هذا أحدث نسخة مستقرة من **Aspose.Cells** إلى ملف `.csproj` الخاص بك. المكتبة توفر الفئات `Workbook` و `Worksheet` و `ImageOrPrintOptions` وغيرها التي سنستخدمها لـ **حفظ صورة ورقة Excel**.

## الخطوة 2: تحميل دفتر العمل الذي يحتوي على الجدول المحوري

```csharp
using Aspose.Cells;
using System;

// Load the Excel file – replace the path with your actual location
string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*لماذا هذا مهم:*  
تحميل دفتر العمل يمنحك الوصول إلى جميع أوراق العمل والخلايا والكائنات المضمنة. فئة `Workbook` تُجرد تنسيق الملف، بحيث يمكنك العمل مع `.xlsx` أو `.xls` أو حتى `.csv` دون الحاجة إلى كود تحليل إضافي.

## الخطوة 3: اختيار ورقة العمل وتحديث الجدول المحوري

```csharp
// Get the first worksheet where the pivot table resides
Worksheet sheet = workbook.Worksheets[0];

// Refresh the pivot table so it reflects the latest source data
if (sheet.PivotTables.Count > 0)
{
    sheet.PivotTables[0].Refresh();
}
else
{
    Console.WriteLine("No pivot tables found on the selected worksheet.");
}
```

*لماذا هذا مهم:*  
جداول البيانات المحورية تحتفظ بذاكرة مؤقتة لبيانات المصدر. استدعاء `Refresh()` يضمن أن التمثيل البصري يطابق أي تغييرات حديثة، وهو أمر حاسم عندما تقوم لاحقًا بـ **تصدير صورة الجدول المحوري**.

## الخطوة 4: تكوين خيارات تصدير الصورة (صيغة PNG، الحفاظ على النمط)

```csharp
// Set up export options – PNG keeps lossless quality and supports transparency
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Png,
    // Preserve the pivot table’s style (fonts, colors, borders)
    CalculatePivotTableStyle = true,
    // Optional: set image resolution (DPI) for higher quality
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

*لماذا هذا مهم:*  
`CalculatePivotTableStyle = true` يخبر Aspose.Cells بأن يرسم الجدول المحوري تمامًا كما يظهر في Excel، بما في ذلك التنسيق الشرطي. تعديل DPI يمكن أن يكون مفيدًا للطباعة أو الشاشات عالية الدقة.

## الخطوة 5: التقاط النطاق المستخدم (بما في ذلك الجدول المحوري) كصورة

```csharp
// Determine the range that contains data – MaxDisplayRange covers the whole used area
CellArea usedRange = sheet.Cells.MaxDisplayRange;

// Add a picture of the used range to the worksheet (position 0,0) and save it
Picture pic = sheet.Pictures.Add(0, 0, usedRange);
pic.Save(@"YOUR_DIRECTORY\PivotImage.png", imgOptions);
```

*لماذا هذا مهم:*  
`MaxDisplayRange` يتوسع تلقائيًا إلى أبعد خلية تحتوي على بيانات أو صيغ أو تنسيق، مما يضمن تضمين الجدول المحوري بالكامل والخلايا المحيطة. طريقة `Pictures.Add` تنشئ صورة في الذاكرة نكتبها فورًا إلى القرص كملف PNG.

## مثال كامل قابل للتنفيذ

بجمع كل ذلك معًا، إليك برنامج وحدة تحكم مستقل يمكنك نسخه ولصقه وتشغيله:

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPngExport
{
    class Program
    {
        static void Main()
        {
            // ---------- 1. Load workbook ----------
            string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // ---------- 2. Get first worksheet ----------
            Worksheet sheet = workbook.Worksheets[0];

            // ---------- 3. Refresh pivot table ----------
            if (sheet.PivotTables.Count > 0)
            {
                sheet.PivotTables[0].Refresh();
            }
            else
            {
                Console.WriteLine("No pivot tables found on the selected worksheet.");
                return;
            }

            // ---------- 4. Set image export options ----------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Png,
                CalculatePivotTableStyle = true,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // ---------- 5. Export used range as PNG ----------
            CellArea usedRange = sheet.Cells.MaxDisplayRange;
            Picture pic = sheet.Pictures.Add(0, 0, usedRange);
            string outputPath = @"YOUR_DIRECTORY\PivotImage.png";
            pic.Save(outputPath, imgOptions);

            Console.WriteLine($"Pivot table image saved to: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، ستطبع وحدة التحكم:

```
Pivot table image saved to: YOUR_DIRECTORY\PivotImage.png
```

وسيظهر الملف `PivotImage.png` في المجلد الهدف. افتحه بأي عارض صور—سترى التمثيل البصري الدقيق لورقة Excel، بما في ذلك الجدول المحوري المنسق، وعناوين الأعمدة، وأي بيانات محيطة.

## الاختلافات الشائعة وحالات الحافة

| السيناريو | التعديل |
|----------|------------|
| **تصدير نطاق خلايا محدد فقط** (مثال: `A1:D20`) | استبدل `sheet.Cells.MaxDisplayRange` بـ `new CellArea { StartRow = 0, StartColumn = 0, EndRow = 19, EndColumn = 3 }`. |
| **عدة أوراق عمل** | قم بالتكرار عبر `workbook.Worksheets` وكرر الخطوات 3‑5 لكل ورقة تريد تصديرها. |
| **تنسيق صورة مختلف** (JPEG, BMP) | غيّر `SaveFormat = SaveFormat.Jpeg` (أو `Bmp`). يُنصح باستخدام PNG لجودة غير مضغوطة. |
| **أوراق عمل كبيرة** تسبب ضغطًا على الذاكرة | استخدم `sheet.Pictures.Add` مع `CellArea` أصغر أو قسّم التصدير إلى عدة صور. |
| **عدم وجود جدول محوري** | احمِ الكود باستخدام `if (sheet.PivotTables.Count == 0)` كما هو موضح؛ يمكنك لا يزال تصدير النطاق العادي. |

## نصائح احترافية

* **تسجيل الترخيص مبكرًا** – سجّل ترخيص Aspose.Cells قبل تحميل دفتر العمل لتجنب علامة التقييم.  
  ```csharp
  var license = new License();
  license.SetLicense(@"YOUR_DIRECTORY\Aspose.Total.NET.lic");
  ```
* **تصدير دفعي** – في خطوط تقارير، غلف منطق التصدير في طريقة تُعيد `byte[]`. هذا يتيح لك إرسال PNG مباشرة إلى واجهة ويب API دون الحاجة إلى نظام الملفات.  
* **خلفية شفافة** – PNG يدعم الشفافية بالفعل. إذا أردت خلفية بيضاء، اضبط `imgOptions.Transparent = false;`.  

## الخلاصة

أنت الآن تعرف **كيفية تصدير Excel إلى PNG** باستخدام Aspose.Cells، مع تغطية سير العمل الكامل من تحميل دفتر العمل إلى **حفظ نطاق Excel كصورة**، **حفظ صورة ورقة Excel**، و **تصدير صورة الجدول المحوري**. الكود المقدم كامل، قابل للتنفيذ، وقابل للتكييف مع سيناريوهات العالم الحقيقي مثل التقارير الآلية أو إنشاء اللوحات.

هل أنت مستعد للخطوة التالية؟ استكشف كيفية **تحويل PNG إلى PDF** لتقارير قابلة للطباعة، أو دمج الصورة في خدمة ويب تقدم تصورات Excel مباشرة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [تصدير دفتر عمل Excel كصورة باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [كيفية تصدير خلايا Excel كصور باستخدام Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}