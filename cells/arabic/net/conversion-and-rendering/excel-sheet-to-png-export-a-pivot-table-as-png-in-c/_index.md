---
category: general
date: 2026-03-18
description: دليل تحويل ورقة إكسل إلى PNG يوضح كيفية تصدير Pivot، وتحديد منطقة الطباعة
  للـ Pivot، وتصدير صورة نطاق إكسل باستخدام Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: ar
og_description: دليل تحويل ورقة إكسل إلى PNG يشرح لك كيفية تصدير جداول المحور، وتعيين
  منطقة الطباعة للمحور، وتصدير صورة نطاق إكسل باستخدام C#.
og_title: تحويل ورقة إكسل إلى PNG – الدليل الكامل لتصدير الجداول المحورية
tags:
- Aspose.Cells
- C#
- Excel automation
title: تحويل ورقة إكسل إلى PNG – تصدير جدول محوري كصورة PNG في C#
url: /ar/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – تصدير جدول محوري كصورة PNG في C#

هل احتجت يوماً إلى تحويل **excel sheet to png** لكن لم تكن متأكدًا من كيفية التقاط الجدول المحوري فقط؟ لست وحدك. في العديد من خطوط التقارير يكون تصور الجدول المحوري هو النجم، وتصديره كصورة PNG يتيح لك تضمينه في رسائل البريد الإلكتروني، لوحات التحكم، أو الوثائق دون الحاجة لسحب كامل المصنف.

في هذا الدليل سنوضح لك **how to export pivot** data، **set print area pivot**، وأخيرًا **export excel range image** حتى تحصل على ملف **export worksheet to image** نظيف. لا روابط غامضة إلى مستندات خارجية—فقط مقتطف كامل قابل للتنفيذ وتفسير لكل سطر.

## ما ستحتاجه

- **Aspose.Cells for .NET** (حزمة NuGet `Aspose.Cells` – الإصدار 23.12 أو أحدث).  
- بيئة تطوير .NET (Visual Studio، Rider، أو `dotnet` CLI).  
- ملف Excel (`input.xlsx`) يحتوي على جدول محوري واحد على الأقل.

هذا كل شيء. إذا كان لديك هذه المتطلبات، هيا نبدأ.

## الخطوة 1 – تحميل المصنف والحصول على الورقة الأولى

قبل أن نتعامل مع الجدول المحوري، نحتاج إلى تحميل المصنف في الذاكرة.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*لماذا هذا مهم:* تحميل الملف يمنحنا الوصول إلى جميع الكائنات (الجداول، المخططات، الجداول المحورية). استخدام الورقة الأولى هو الافتراضي البسيط؛ يمكنك استبدال `0` برقم الفهرس الفعلي للورقة أو اسمها إذا لزم الأمر.

## الخطوة 2 – استرجاع نطاق الجدول المحوري

الجدول المحوري موجود داخل كتلة خلايا. نحتاج إلى تلك الكتلة لنخبر Excel ما الذي يجب طباعته.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*لماذا نفعل ذلك:* `PivotTableRange` يحدد لنا الصفوف والأعمدة البداية والنهاية بدقة. بدون ذلك، سيشمل التصدير كامل الورقة، مما يفسد هدف **set print area pivot**.

## الخطوة 3 – تحديد منطقة الطباعة بحيث يتم عرض الجدول المحوري فقط

محرك الطباعة في Excel يحترم خاصية `PrintArea`. بتضييقها إلى الجدول المحوري، نتجنب البيانات العشوائية أو الخلايا الفارغة.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*نصيحة احترافية:* إذا كان لديك عدة جداول محورية في نفس الورقة، يمكنك دمج نطاقاتها باستخدام قائمة مفصولة بفواصل (`"0,0:10,5,12,0:22,5"`). هذه هي تقنية **export excel range image** لعدة كتل.

## الخطوة 4 – إعداد خيارات تصدير الصورة (صيغة PNG)

تتيح لك Aspose.Cells ضبط المخرجات بدقة. PNG صيغة غير مضغوطة، مثالية للصور الواضحة للجدول المحوري.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*لماذا PNG؟* على عكس JPEG، يحافظ PNG على وضوح النص وخلفيات شفافة، مما يجعله الخيار المفضل لسيناريوهات **excel sheet to png**.

## الخطوة 5 – تصدير الورقة (منطقة الجدول المحوري) إلى ملف PNG

الآن يحدث السحر—تحويل منطقة الطباعة المحددة إلى صورة.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*ما ستراه:* ملف `pivot.png` يحتوي فقط على الجدول المحوري، دون صفوف أو أعمدة إضافية. افتحه بأي عارض صور وستحصل على تصور جاهز للمشاركة.

---

## الأسئلة المتكررة وحالات الحافة

### ماذا لو كان المصنف يحتوي على **multiple pivot tables**؟

احصل على `PivotTableRange` لكل جدول محوري، دمج النطاقات، وتعيين السلسلة المدمجة إلى `PrintArea`. مثال:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### هل يمكنني التصدير إلى **other image formats**؟

بالطبع. غيّر `imgOptions.ImageFormat = ImageFormat.Jpeg;` (أو `Bmp`، `Gif`، `Tiff`). فقط تذكر أن JPEG يضيف تشوهات ضغط—عادةً غير مثالي للجداول المحورية التي تحتوي على نصوص كثيرة.

### كيف أتعامل مع **large pivots** التي تمتد على عدة صفحات؟

اضبط `imgOptions.OnePagePerSheet = false;` للسماح بالعرض متعدد الصفحات، ثم كرر عبر الصفحات:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### ماذا عن **hidden rows/columns**؟

تحترم Aspose إعدادات إظهار/إخفاء الورقة. إذا كنت بحاجة لتجاهل العناصر المخفية، قم بإظهارها مؤقتًا قبل التصدير أو عدل `PrintArea` يدويًا.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

شغّل البرنامج، وستجد `pivot.png` في المكان الذي حددته. افتح الملف—سترى عرضًا واضحًا للجدول المحوري فقط، ولا شيء آخر.

## الخلاصة

أصبحت الآن تمتلك **حلًا كاملاً من البداية إلى النهاية** لتحويل **excel sheet to png** مع التركيز حصريًا على جدول محوري. من خلال **setting the print area pivot**، وضبط **image export options**، واستخدام طريقة `ToImage` في Aspose.Cells، يمكنك أتمتة إنشاء التقارير، تضمين التصورات في صفحات الويب، أو ببساطة أرشفة لقطات التحليل.

ما الخطوة التالية؟ جرّب استبدال PNG بملف PDF عالي الدقة (`ImageFormat.Pdf`)، جرب عدة جداول محورية في ورقة واحدة، أو دمج هذه الطريقة مع تصدير المخططات للحصول على خط أنابيب تصدير لوحة تحكم متكاملة.

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا، أو تابع الدرس التالي حيث سنستكشف **export worksheet to image** لالتقاط صور كاملة للورقة، بما في ذلك المخططات والتنسيق الشرطي. برمجة سعيدة!  

<img src="pivot.png" alt="مثال على تحويل excel sheet to png لتصدير جدول محوري">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}