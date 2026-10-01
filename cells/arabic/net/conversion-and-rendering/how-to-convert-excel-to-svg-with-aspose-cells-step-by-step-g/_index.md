---
category: general
date: 2026-10-01
description: تعلم كيفية تحويل Excel إلى SVG وحفظ ملف Excel كـ SVG باستخدام Aspose.Cells.
  اتبع هذا الدليل الكامل لتصدير أوراق Excel كصور SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to svg
- save excel file as svg
- how to export excel to svg
- export excel worksheet as svg
language: ar
lastmod: 2026-10-01
og_description: تحويل Excel إلى SVG باستخدام Aspose.Cells. يشرح هذا الدليل كيفية تصدير
  أوراق عمل Excel كصور SVG، مع تغطية الإعداد، الكود، وحالات الحافة.
og_image_alt: Diagram illustrating the convert excel to svg workflow
og_title: تحويل Excel إلى SVG باستخدام Aspose.Cells – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  headline: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  name: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Exporting multiple worksheets at once
    text: 'When a workbook contains several sheets, you can let Aspose.Cells generate
      a separate SVG for each sheet automatically:'
  - name: Controlling SVG dimensions
    text: 'SVG files are vector‑based, but you can still influence the viewport size:'
  - name: Handling formulas and calculated values
    text: 'By default, Aspose.Cells evaluates formulas before rendering. If you want
      to export raw formulas as text, set:'
  - name: Performance tips
    text: '- **Reuse `ImageOrPrintOptions`**: Create the options once and reuse them
      for multiple workbooks to avoid unnecessary allocations. - **Stream output**:
      If you are building a web API, write the SVG directly to a `MemoryStream` and
      return it as a file result instead of saving to disk.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- SVG export
title: كيفية تحويل Excel إلى SVG باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/net/conversion-and-rendering/how-to-convert-excel-to-svg-with-aspose-cells-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل Excel إلى SVG باستخدام Aspose.Cells – دليل خطوة بخطوة

إذا كنت بحاجة إلى **تحويل Excel إلى SVG**، يوضح لك هذا الدليل بالضبط كيفية تصدير ورقة عمل Excel كصورة SVG باستخدام Aspose.Cells. سترى مثالًا كاملاً قابلاً للتنفيذ يحفظ ملف Excel كـ SVG وتتعرف على سبب أهمية كل إعداد.

تصدير جداول البيانات كرسومات متجهة قابلة للتوسع مفيد عندما تريد عرضًا واضحًا في صفحات الويب أو التقارير أو الوثائق دون فقدان الجودة. تغطي الخطوات أدناه كل شيء من تثبيت المكتبة إلى التعامل مع أوراق عمل متعددة وتفادي المشكلات الشائعة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7.2+)
- ترخيص Aspose.Cells صالح أو مفتاح تقييم مجاني
- مصنف Excel (`input.xlsx`) تريد تحويله
- Visual Studio 2022 أو أي محرر C# تفضله

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Cells`.

## الخطوة 1: تثبيت Aspose.Cells

الطريقة القياسية هي إضافة حزمة Aspose.Cells عبر NuGet. افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.Cells --version 24.10
```

هذا الأمر يقوم بتحميل أحدث نسخة مستقرة (24.10 في وقت كتابة هذا الدليل) وتحديث ملف المشروع. استخدام أحدث نسخة يضمن التوافق مع أحدث ميزات Excel وتحسينات SVG.

## الخطوة 2: تحميل مصنف Excel

تحميل المصنف هو أول عملية ملموسة في خط أنابيب **convert excel to svg**. تمثل فئة `Workbook` الملف Excel بالكامل وتمنحك الوصول إلى أوراق العمل، الصيغ، والتنسيقات.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the source workbook
var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Optional: verify that the workbook loaded correctly
Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");
```

**لماذا هذا مهم:**  
إذا تعذر فتح الملف (مثلاً مسار غير صحيح أو تنسيق غير مدعوم)، تقوم Aspose.Cells برمي استثناء توضيحي يمكنك التقاطه وتسجيله. التحقق من عدد أوراق العمل مبكرًا يساعدك على اتخاذ قرار ما إذا كنت ستصدر ورقة واحدة أو المصنف بأكمله.

## الخطوة 3: تكوين خيارات تصيير SVG

لـ **save excel file as svg**، يجب إنشاء كائن `ImageOrPrintOptions` وتعيين خاصية `SaveFormat` إلى `SaveFormat.Svg`. يمكنك أيضًا ضبط جودة الصورة، التحجيم، وما إذا كنت تريد تضمين الخطوط.

```csharp
// Set up rendering options for SVG output
var imageOptions = new ImageOrPrintOptions
{
    // Export format must be SVG
    SaveFormat = SaveFormat.Svg,

    // Preserve the original aspect ratio
    OnePagePerSheet = true,

    // Optional: increase resolution for sharper vectors
    // (SVG is resolution‑independent, but this affects rasterized elements)
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**شرح:**  
`OnePagePerSheet = true` يجبر كل ورقة عمل على صفحة SVG واحدة، وهو ما تريده عادةً لتضمينه في الويب. تغيير الدقة يؤثر على كيفية تصيير الصور النقطية المضمنة (مثل الصور داخل الخلايا) داخل ملف SVG.

## الخطوة 4: حفظ المصنف كصورة SVG

الآن يمكنك **export excel worksheet as svg** عن طريق استدعاء `Workbook.Save` مع مسار الهدف والخيارات التي قمت بتكوينها للتو.

```csharp
// Define the output path
string outputPath = @"YOUR_DIRECTORY\output.svg";

// Save the workbook (or a specific worksheet) as SVG
workbook.Save(outputPath, imageOptions);

Console.WriteLine($"Workbook exported to SVG at: {outputPath}");
```

إذا كنت تحتاج إلى تصدير ورقة واحدة فقط بدلاً من المصنف بالكامل، استخرج الورقة واستخدم `SheetRender`:

```csharp
// Export only the first worksheet
var sheet = workbook.Worksheets[0];
var sheetRender = new SheetRender(sheet, imageOptions);
sheetRender.ToImage(0, outputPath); // 0 = first page
```

**لماذا هذا يعمل:**  
`Workbook.Save` يتكرر على جميع أوراق العمل عندما تكون `OnePagePerSheet` مفعلة، مما يولد ملف SVG واحد لكل ورقة إذا كان مسار الإخراج يحتوي على عنصر نائب (مثل `output_{0}.svg`). استخدام `SheetRender` يمنحك تحكمًا دقيقًا في الأوراق التي تريد تصديرها.

## الخطوة 5: التحقق من ناتج SVG

بعد انتهاء التحويل، افتح ملف `.svg` الناتج في متصفح أو محرر SVG (مثل Inkscape). يجب أن ترى النص، حدود الخلايا، وأي صور مدمجة تُعرض كمتجهات قابلة للتوسع.

```bash
# On macOS or Linux you can open the file directly:
open YOUR_DIRECTORY/output.svg
```

إذا ظهر ملف SVG فارغًا أو يفتقد التنسيق، تحقق من التالي:

1. أن المصنف يحتوي فعليًا على بيانات في الورقة المستهدفة.  
2. عدم وجود صفوف/أعمدة مخفية تحجب المحتوى (استخدم `sheet.IsVisible`).  
3. الخطوط المستخدمة في المصنف مثبتة على الجهاز؛ وإلا ستستبدلها Aspose.Cells بخطوط أخرى قد تؤثر على المظهر.

## اعتبارات متقدمة

### تصدير أوراق عمل متعددة مرة واحدة

عندما يحتوي المصنف على عدة أوراق، يمكنك السماح لـ Aspose.Cells بإنشاء ملف SVG منفصل لكل ورقة تلقائيًا:

```csharp
// Use a placeholder {0} for sheet index
string multiOutput = @"YOUR_DIRECTORY\output_{0}.svg";
workbook.Save(multiOutput, imageOptions);
```

المكتبة تستبدل `{0}` برقم الفهرس الخاص بالورقة (يبدأ من 0). هذا مفيد لمعالجة دفعات تقارير كبيرة.

### التحكم بأبعاد SVG

ملفات SVG تعتمد على المتجهات، لكن لا يزال بإمكانك التأثير على حجم نافذة العرض:

```csharp
imageOptions.PageWidth = 800;   // width in pixels (converted to SVG points)
imageOptions.PageHeight = 600;  // height in pixels
```

تحديد أبعاد صريحة يضمن تخطيطًا ثابتًا عند تضمين SVG داخل حاويات HTML.

### معالجة الصيغ والقيم المحسوبة

بشكل افتراضي، تقوم Aspose.Cells بتقييم الصيغ قبل التصيير. إذا رغبت في تصدير الصيغ كنصوص، اضبط:

```csharp
imageOptions.ExportFormulasAsString = true;
```

هذا الخيار مفيد للوثائق التي تحتاج إلى إظهار الصيغة الفعلية في Excel بدلاً من نتيجتها المحسوبة.

### نصائح الأداء

- **إعادة استخدام `ImageOrPrintOptions`**: أنشئ الخيارات مرة واحدة وأعد استخدامها لعدة مصنفات لتجنب عمليات التخصيص غير الضرورية.  
- **تدفق الإخراج**: إذا كنت تبني واجهة برمجة تطبيقات ويب، اكتب SVG مباشرة إلى `MemoryStream` وأرجعه كملف بدلاً من حفظه على القرص.

```csharp
using (var stream = new MemoryStream())
{
    workbook.Save(stream, imageOptions);
    // Reset position before reading
    stream.Position = 0;
    // Return stream to caller (e.g., ASP.NET Core FileResult)
}
```

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب | الحل |
|--------|-------|-----|
| ملف SVG فارغ | المصنف يحتوي على صفوف/أعمدة مخفية أو ورقة ذات حجم صفر | إظهار الصفوف/الأعمدة أو تعيين `sheet.IsVisible = true` |
| فقدان الخطوط | الخط غير مثبت على الخادم | تثبيت الخط المطلوب أو تضمينه باستخدام `imageOptions.EmbeddedFonts = true` |
| ملفات SVG متعددة بأسماء غير متوقعة | مسار الإخراج يفتقر إلى عنصر `{0}` | استخدم `output_{0}.svg` لإنشاء ملفات لكل ورقة |
| بطء التحويل للمصنفات الكبيرة | تصيير كل ورقة على حدة دون `OnePagePerSheet` | فعّل `OnePagePerSheet` أو عالج الأوراق بالتوازي باستخدام `Task.Run` |

## مثال كامل قابل للتنفيذ

فيما يلي تطبيق console مكتمل يوضح **how to export Excel to SVG** من البداية حتى النهاية. استبدل `YOUR_DIRECTORY` بمسار فعلي على جهازك.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToSvgDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
            var workbook = new Workbook(workbookPath);
            Console.WriteLine($"Loaded {workbook.Worksheets.Count} worksheet(s).");

            // 2️⃣ Configure SVG options
            var svgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Svg,
                OnePagePerSheet = true,
                HorizontalResolution = 300,
                VerticalResolution = 300,
                // Optional: set explicit dimensions
                // PageWidth = 800,
                // PageHeight = 600
            };

            // 3️⃣ Export each sheet as a separate SVG file
            string outputPattern = @"YOUR_DIRECTORY\output_{0}.svg";
            workbook.Save(outputPattern, svgOptions);
            Console.WriteLine("Export completed. SVG files created:");

            for (int i = 0; i < workbook.Worksheets.Count; i++)
            {
                Console.WriteLine($"\t{string.Format(outputPattern, i)}");
            }
        }
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
Loaded 2 worksheet(s).
Export completed. SVG files created:
    YOUR_DIRECTORY\output_0.svg
    YOUR_DIRECTORY\output_1.svg
```

افتح أي من ملفات `.svg` المولدة في متصفح للتحقق من نجاح التحويل.

## الخلاصة

أنت الآن تعرف **كيفية تحويل Excel إلى SVG** باستخدام Aspose.Cells، من تثبيت المكتبة إلى معالجة أوراق عمل متعددة وضبط خيارات التصيير. غطى الدليل سير العمل الكامل لـ **save excel file as svg**، وشرح لماذا كل إعداد مهم، وأبرز الحالات الخاصة مثل الصفوف المخفية، تضمين الخطوط، واعتبارات الأداء.

بعد ذلك، قد ترغب في استكشاف:

- **كيفية تصدير Excel إلى SVG** في واجهة برمجة تطبيقات ويب (بث الـ SVG مباشرة إلى العميل)  
- تحويل Excel إلى صيغ متجهة أخرى مثل PDF أو EMF  
- استخدام Aspose.Slides لتضمين SVG المولد في عروض PowerPoint

لا تتردد في تجربة التحجيم، الأنماط المخصصة، أو دمج ناتج SVG مع HTML/CSS لتقارير تفاعلية. برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحويل أوراق Excel إلى SVG باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/workbook-operations/convert-excel-to-svg-aspose-cells-java/)
- [تحويل Excel إلى SVG باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/convert-excel-to-svg-aspose-cells-net/)
- [كيفية تحويل مخططات Excel إلى SVG باستخدام Aspose.Cells في Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}