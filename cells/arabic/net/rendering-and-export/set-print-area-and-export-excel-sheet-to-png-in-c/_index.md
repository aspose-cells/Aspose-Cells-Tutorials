---
category: general
date: 2026-10-26
description: تحديد منطقة الطباعة وتصدير ورقة Excel إلى PNG باستخدام C#. تعلّم خيارات
  تصدير الصور، كيفية تصدير PNG، والحصول على صورة قابلة للطباعة من المصنف.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: ar
lastmod: 2026-10-26
og_description: تحديد منطقة الطباعة وتصدير ورقة إكسل إلى PNG باستخدام C#. يغطي هذا
  الدليل خطوة بخطوة خيارات تصدير الصور وكيفية تصدير PNG من دفتر العمل.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: تحديد منطقة الطباعة وتصدير ورقة إكسل إلى PNG – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: تحديد منطقة الطباعة وتصدير ورقة Excel إلى PNG في C#
url: /ar/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد منطقة الطباعة وتصدير ورقة Excel إلى PNG باستخدام C#

إذا كنت بحاجة إلى **تحديد منطقة الطباعة** قبل تصدير ورقة Excel إلى PNG، يوضح لك هذا الدليل كيفية القيام بذلك. ستشاهد مثالًا كاملًا بلغة C# يضبط خيارات تصدير الصورة، ويُعدّل منطقة الطباعة في ورقة العمل، ويحفظ النتيجة كصورة.

تصدير ورقة Excel إلى PNG هو طلب شائع عندما تريد تضمين لقطة من ورقة العمل في تقرير أو بريد إلكتروني أو صفحة ويب. يعمل الكود أدناه مع أي مصنف يحتوي على جدول محوري، لكن التقنية تنطبق أيضًا على نطاقات البيانات العادية. لا تحتاج إلى أدوات خارجية—فقط مكتبة Aspose.Cells لـ .NET.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (العينة تستهدف .NET 6، لكن أي نسخة حديثة من .NET تعمل)
- Aspose.Cells لـ .NET (التثبيت عبر NuGet: `Install-Package Aspose.Cells`)
- إلمام أساسي بـ C# ومفاهيم Excel مثل أوراق العمل ومناطق الطباعة

## الخطوة 1: ضبط خيارات تصدير الصورة

أول شيء تقوم به هو إنشاء كائن `ImageOrPrintOptions`. هذا الكائن يخبر Aspose.Cells كيف يُعيد رسم الورقة كصورة.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**لماذا هذا مهم:** `ImageOrPrintOptions` يتحكم في تنسيق الإخراج، الدقة، وتفاصيل الرسم الأخرى. استخدام PNG يضمن جودة غير مضغوطة، وهو مثالي للتقارير التي تتطلب نصًا ورسومات واضحة.

## الخطوة 2: تحميل المصنف والوصول إلى ورقة العمل المستهدفة

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**لماذا هذا مهم:** يجب أن تعمل مع كائن `Worksheet` محدد لأن منطقة الطباعة هي إعداد على مستوى ورقة العمل.

## الخطوة 3: تحديد النطاق الذي تريد طباعته

في كثير من السيناريوهات تكون البيانات التي تهمك داخل جدول محوري. الكود التالي يستخرج نطاق البيانات للجدول المحوري الأول في الورقة.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

إذا لم تحتوي ورقة العمل على جدول محوري، يمكنك استبدال `pivotDataRange` بأي `CellArea` تُنشئه يدويًا، على سبيل المثال:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## الخطوة 4: **تحديد منطقة الطباعة** لتطابق النطاق المختار

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**لماذا هذا مهم:** منطقة الطباعة تخبر Excel (وAspose.Cells) أي الخلايا يجب تضمينها عند رسم الورقة كصورة. من خلال مواءمة منطقة الطباعة مع نطاق بيانات الجدول المحوري، تتجنب الهوامش الفارغة وتضمن أن ملف PNG المُصدَّر يحتوي فقط على البيانات ذات الصلة.

## الخطوة 5: تصدير ورقة العمل إلى صورة PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**لماذا هذا مهم:** `worksheet.ToImage` يحترم منطقة الطباعة التي تم ضبطها مسبقًا، لذا يحتوي ملف PNG على الخلايا التي حددتها بالضبط. إسناد الصورة إلى شكل صورة يسمح لك بإدراجها مرة أخرى في المصنف إذا لزم الأمر، بينما حفظها على القرص يمنحك ملفًا مستقلًا.

## مثال كامل يعمل

جمع جميع الخطوات معًا ينتج برنامجًا مستقلًا يمكنك تشغيله فورًا.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج ينشئ الملف `C:\Temp\WorksheetExport.png`. فتح الملف يُظهر صورة PNG واضحة تحتوي فقط على الخلايا التي تم **تحديد منطقة الطباعة** لها (بيانات الجدول المحوري في هذا المثال). يمكن إدراج الصورة في مستندات Word أو شرائح PowerPoint أو صفحات ويب دون خطوات تحويل إضافية.

## التعامل مع أوراق عمل أو جداول محورية متعددة

- **أوراق عمل متعددة:** كرّر الحلقة عبر `wb.Worksheets` وطبق الخطوات 3‑5 على كل ورقة تحتاج إلى تصديرها.
- **جداول محورية متعددة:** اختر `PivotTables[index]` المناسب أو تكرّر عبر `worksheet.PivotTables` لتصدير كل جدول على حدة.
- **بدون جدول محوري:** أنشئ `CellArea` يدويًا (انظر التعليق في الخطوة 3) وعيّنها إلى `PrintArea`.

## نصائح عملية (E‑E‑A‑T)

- **نصيحة احترافية:** اضبط `HorizontalResolution` و `VerticalResolution` إلى 300 DPI للحصول على PNG جاهز للطباعة؛ القيم الأقل تقلل حجم الملف للاستخدام على الويب.
- **احذر من أشكال الصور الفارغة:** إذا لم تحتوي ورقة العمل على أشكال صور، أضف واحدة قبل إسناد الصورة:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **الأداء:** إعادة استخدام كائن `ImageOrPrintOptions` واحد لعدة أوراق عمل يتجنب عمليات التخصيص غير الضرورية.
- **التوافق:** Aspose.Cells 23.9+ يدعم بالكامل .NET 6 وما بعده؛ الإصدارات الأقدم قد تتطلب تعديل أسماء الـ API.

## الخلاصة

أنت الآن تعرف كيف **تحدد منطقة الطباعة** وتصدّر ورقة Excel إلى صورة PNG.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير Excel إلى PNG – دليل خطوة بخطوة كامل](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [كيفية تصدير نطاق Excel كصورة باستخدام C# و Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [ورقة Excel إلى PNG – تصدير جدول محوري كـ PNG في C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}