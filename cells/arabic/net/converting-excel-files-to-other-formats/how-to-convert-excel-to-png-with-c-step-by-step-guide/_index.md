---
category: general
date: 2026-10-10
description: تحويل Excel إلى PNG بسرعة باستخدام Aspose.Cells في C#. تعلم كيفية تصدير
  نطاق Excel، حفظ Excel كملف PNG، وتحويل ورقة العمل إلى صورة في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: ar
lastmod: 2026-10-10
og_description: حوّل Excel إلى PNG فورًا باستخدام Aspose.Cells. يوضح هذا البرنامج
  التعليمي كيفية تصدير نطاق Excel، حفظ Excel كملف PNG، وتحويل ورقة العمل إلى صورة.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: تحويل Excel إلى PNG باستخدام C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: كيفية تحويل Excel إلى PNG باستخدام C# – دليل خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل Excel إلى PNG باستخدام C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **تحويل Excel إلى PNG** برمجيًا، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for .NET. سواء كنت تبني خدمة تقارير أو لوحة تحكم آلية، ستتعلم كيفية تصدير نطاق Excel، وحفظ النتيجة كملف PNG، ومعالجة الحالات الخاصة الشائعة.

ستمر بجميع الخطوات المطلوبة—من إضافة حزمة NuGet إلى عرض منطقة ورقة عمل محددة—حتى تتمكن من دمج الحل في أي مشروع C# دون الحاجة للبحث عن موارد إضافية.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
* Visual Studio 2022 (أو أي بيئة تطوير تدعم C#)
* ترخيص صالح لـ Aspose.Cells for .NET (الإصدار التجريبي المجاني يعمل للتقييم)
* ملف Excel باسم **Pivot.xlsx** موجود في مجلد يمكنك الإشارة إليه (يستخدم الدليل `YOUR_DIRECTORY` كعنصر نائب)

> **نصيحة احترافية:** قم بتثبيت حزمة Aspose.Cells عبر وحدة تحكم مدير حزم NuGet:  
> `Install-Package Aspose.Cells`

## تحويل Excel إلى PNG – استعراض كامل للكود

البرنامج الكامل التالي يقوم بتحميل مصنف، وتكوين خيارات الصورة، وعرض نطاق خلايا محدد إلى ملف PNG. جميع توجيهات `using` المطلوبة مضمونة، بحيث يمكنك نسخ الكود إلى مشروع وحدة تحكم جديد وتشغيله فورًا.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### كيف يعمل الكود

* **تحميل المصنف** – `Workbook` يقرأ ملف `.xlsx` إلى الذاكرة، مما يمنحك الوصول إلى جميع أوراق العمل.
* **ImageOrPrintOptions** – هذا الكائن يخبر Aspose.Cells بإنتاج PNG (`ImageFormat.Png`). يمكنك أيضًا تعديل DPI أو التكبير/التصغير أو لون الخلفية إذا لزم الأمر.
* **RenderRangeToImage** – الطريقة `RenderRangeToImage` تأخذ ثلاثة معطيات: نطاق الخلايا (`"A1:H30"`)، مسار الملف الوجهة، وخيارات الصورة. هذه هي العملية الأساسية التي **تصدّر نطاق Excel** إلى صورة PNG.
* **النتيجة** – بعد التنفيذ، ستجد `Pivot.png` في المجلد المحدد، يحتوي على تمثيل بصري دقيق للخلايا المختارة.

## تصدير نطاق Excel إلى PNG – تخصيص المخرجات

إذا كنت بحاجة إلى **تصدير نطاق Excel** غير `A1:H30`، ما عليك سوى تغيير المتغير `range`. الطريقة تقبل أي عنوان بنمط Excel، بما في ذلك النطاقات المسماة:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

يمكنك أيضًا تصدير ورقة العمل بالكامل باستخدام `"A1:Z1000"` (أو عنوان أكبر) أو عن طريق استدعاء `RenderToImage` دون معلمة نطاق.

## حفظ Excel كـ PNG مع إعدادات إضافية

أحيانًا تريد أن يتطابق PNG مع دقة محددة للطباعة أو الاستخدام على الويب. اضبط `ImageOrPrintOptions` كما يلي:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

هذه الإعدادات توضح كيفية **حفظ Excel كـ PNG** مع DPI مخصص وشفافية، مما يمنحك سيطرة كاملة على جودة الصورة النهائية.

## كيفية تصدير Excel – معالجة أوراق العمل المتعددة

المثال يستهدف أول ورقة عمل (`Worksheets[0]`). لتحويل ورقة عمل مختلفة إلى صورة (**convert worksheet to image**)، قم بالإشارة إليها بالترتيب أو بالاسم:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

معالجة كل ورقة في حلقة أمر بسيط:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## الحالات الخاصة واستكشاف الأخطاء

| الموقف | النهج الموصى به |
|-----------|----------------------|
| **نطاق كبير جدًا** (مثلاً كامل المصنف) | زيادة `HorizontalResolution`/`VerticalResolution` تدريجيًا لتجنب `OutOfMemoryException`. ضع في اعتبارك تصدير كل ورقة على حدة. |
| **الخلايا المدمجة** | Aspose.Cells يحافظ على مظهر الخلايا المدمجة تلقائيًا، لكن تحقق من النتيجة إذا كنت تعتمد على عرض الأعمدة الدقيق. |
| **الصيغ التي تشير إلى ملفات خارجية** | تأكد من أن تلك الملفات متاحة قبل تحميل المصنف؛ وإلا قد تظهر القيم القديمة في الصورة المصدرة. |
| **غياب الترخيص** | الإصدار التجريبي يضيف علامة مائية. قم بتطبيق ترخيص صالح (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) قبل العرض لإنتاج PNG نظيف. |

## مثال عملي كامل

فيما يلي البرنامج المستقل الذي يمكنك تجميعه وتشغيله. استبدل `YOUR_DIRECTORY` بمسار مجلد فعلي على جهازك.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**الناتج المتوقع**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

افتح `Pivot.png` بأي عارض صور—سترى التخطيط البصري الدقيق للخلايا A1 إلى H30، بما في ذلك التنسيق والألوان والحدود.

## الخلاصة

أصبح لديك الآن طريقة موثوقة لـ **تحويل Excel إلى PNG** باستخدام C#. يغطي الدليل كيفية **تصدير نطاق Excel**، **حفظ Excel كـ PNG**، و**تحويل ورقة العمل إلى صورة** مع خيارات قابلة للتخصيص ونصائح أفضل الممارسات.  

من هنا يمكنك:

* دمج الكود في واجهة برمجة تطبيقات ويب لتوليد الصور عند الطلب.  
* دمج مخرجات PNG مع إنشاء PDF لتقارير متعددة الصيغ.  
* استكشاف صيغ صور أخرى (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) عن طريق تعديل خاصية `ImageFormat`.

لا تتردد في تجربة نطاقات مختلفة، ودقات مختلفة، واختيارات أوراق عمل لتتناسب مع سيناريو الأتمتة الخاص بك.

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [تحويل Excel إلى PNG، TIFF، وPDF في Java باستخدام Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [إتقان Aspose.Cells Java: تحويل Excel إلى PNG مع موفر تدفق مخصص](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}