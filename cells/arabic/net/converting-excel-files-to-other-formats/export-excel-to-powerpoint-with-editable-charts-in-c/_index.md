---
category: general
date: 2026-09-21
description: تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير باستخدام Aspose.Cells.
  اتبع هذا الدليل خطوة بخطوة لتحويل ورقة العمل إلى PPTX مع الحفاظ على قابلية تحرير
  المخططات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: ar
lastmod: 2026-09-21
og_description: تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير باستخدام Aspose.Cells.
  تعلّم كيفية تحويل ورقة عمل إلى PPTX مع الحفاظ على إمكانية تحرير المخططات بالكامل.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: تصدير Excel إلى PowerPoint مع مخططات قابلة للتعديل في C#
url: /ar/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير في C#

تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير هو طلب شائع عندما تحتاج إلى إعادة استخدام الرسوم البيانية للجدول في العروض التقديمية. يوضح هذا الدليل كيفية **export Excel to PowerPoint** مع الحفاظ على قابلية تحرير المخطط، باستخدام Aspose.Cells for .NET.

سوف تتعلم كيف:

* تحميل مصنف موجود يحتوي على مخططات ومربعات نصية.  
* تكوين خيارات تصدير PPTX بحيث تظل المخططات والأشكال قابلة للتحرير.  
* تحويل ورقة عمل محددة إلى ملف PowerPoint يمكن فتحه وتحريره في Microsoft PowerPoint.

يفترض الدليل أنك تمتلك معرفة أساسية بـ C# وإصدار حديث من .NET (≥ .NET 6). لا يلزم أي خبرة سابقة مع Aspose.Cells.

---

## تصدير Excel إلى PowerPoint – نظرة عامة

الفكرة الأساسية وراء **export Excel to PowerPoint** هي التعامل مع كل ورقة عمل كمصدر صورة يمكن تحويله إلى شريحة PPTX. عن طريق تبديل العلامات `ExportChartAsEditableText` و `ExportShapeAsEditableText`، تقوم Aspose.Cells بكتابة بيانات المخطط الأساسية ككائنات رسم في PowerPoint بدلاً من صورة ثابتة. هذا يجعل الشريحة الناتجة قابلة للتحرير بالكامل—كما لو كان المخطط قد تم إنشاؤه مباشرة في PowerPoint.

> **لماذا نستخدم المخططات القابلة للتحرير؟**  
> تسمح المخططات القابلة للتحرير للمقدمين بتعديل البيانات أو الألوان أو التسميات دون الرجوع إلى ملف Excel الأصلي، مما يسرّع التغييرات في اللحظة الأخيرة ويحافظ على سلاسة سير العمل في العرض التقديمي.

## تحويل ورقة عمل إلى PowerPoint (worksheet to PowerPoint)

فيما يلي مثال كامل وقابل للتنفيذ يوضح تحويل **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### شرح كل خطوة

| الخطوة | ما يفعله الكود | لماذا يهم **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | يقوم بتحميل `input.xlsx` إلى كائن `Aspose.Cells.Workbook`. | يوفر المصنف إمكانية الوصول إلى المخططات التي تريد تصديرها. |
| 2️⃣   | يضبط `ExportType` إلى `Pptx` ويفعل `ExportChartAsEditableText` و `ExportShapeAsEditableText`. | هذه العلامات هي المفتاح لـ **editable charts pptx** – فهي تخبر المكتبة بكتابة هندسة المخطط ككائنات رسم في PowerPoint بدلاً من صور نقطية. |
| 3️⃣   | يستدعي `ConvertToImage` على ورقة العمل الأولى، منتجًا `Worksheet.pptx`. | الطريقة تنفذ عملية **export excel to powerpoint** وتكتب ملف PPTX يمكن فتحه مباشرة في PowerPoint. |

> **نصيحة احترافية:** إذا كنت بحاجة إلى تصدير *عدة* أوراق عمل، قم بالتكرار عبر `workbook.Worksheets` واستدعِ `ConvertToImage` لكل واحدة، مع تسمية ملفات الإخراج اختياريًا بـ `Sheet1.pptx`، `Sheet2.pptx`، إلخ.

## تمكين المخططات القابلة للتحرير في PPTX (export excel chart pptx)

عند ضبط `ExportChartAsEditableText` على `true`، تقوم Aspose.Cells بكتابة كل مخطط كمجموعة من عناصر `<a:graphic>` داخل XML الخاص بـ PPTX. ثم يتعامل PowerPoint مع هذه العناصر ككائنات مخطط أصلية، ويمكنك النقر المزدوج لفتح محرر المخطط.

**المشكلات الشائعة**

* **Missing Aspose.Cells license** – بدون ترخيص تضيف المكتبة علامة مائية إلى الناتج. سجِّل ترخيصًا مبكرًا في برنامجك (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Unsupported chart types** – بينما معظم المخططات الثنائية الأبعاد (عمود، خط، دائري) قابلة للتحرير بالكامل، قد تعود بعض المخططات الثلاثية الأبعاد أو المركبة إلى صور. اختبر أنواع المخططات الخاصة بك إذا كنت تعتمد على القابلية الكاملة للتحرير.  
* **Large worksheets** – تصدير أوراق عمل كبيرة جدًا قد يستهلك ذاكرة كبيرة. فكر في استخدام `ExportMaxRows` أو `ExportMaxColumns` في `ImageOrPrintOptions` لتحديد المنطقة التي يتم تحويلها.

## نصائح للحفاظ على المخططات قابلة للتحرير (editable charts pptx)

1. **Preserve chart data ranges** – تأكد من أن مصدر بيانات المخطط يقع في نفس ورقة العمل التي تقوم بتصديرها. يتم تحويل المراجع عبر الأوراق إلى قيم ثابتة في PPTX.  
2. **Use the latest Aspose.Cells version** – الإصدارات الجديدة تحسن الدعم للميزات الإضافية للمخططات وتصلح الأخطاء النادرة المتعلقة بتصدير PPTX.  
3. **Validate the output** – بعد التحويل، افتح ملف PPTX المُولد في PowerPoint وتحقق من إمكانية تحرير عنوان المخطط، السلاسل، وتسميات المحاور. إذا ظهر أي عنصر كصورة، تحقق مرة أخرى من تمكين `ExportChartAsEditableText` ومن أن نوع المخطط مدعوم.  
4. **Batch processing** – لسيناريوهات الأتمتة (مثلاً، إنشاء مجموعة شرائح من تقارير Excel متعددة)، احزم منطق التحويل في طريقة تقبل `Workbook`، `int worksheetIndex`، و `string outputPath`. هذا يعزل سير عمل **export excel to powerpoint** ويجعله قابلًا لإعادة الاستخدام.

## ملخص المثال الكامل العامل

بجمع كل شيء معًا، إليك البرنامج البسيط الذي يمكنك نسخه‑لصقه في مشروع .NET Console جديد:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**النتيجة المتوقعة**

* ملف باسم `Worksheet.pptx` يظهر في `YOUR_DIRECTORY`.  
* فتح الملف في Microsoft PowerPoint يعرض شريحة تحتوي على المخطط الأصلي وأي مربعات نصية.  
* النقر المزدوج على المخطط يفتح محرر المخططات في PowerPoint، مما يسمح لك بتغيير قيم السلاسل، الألوان، أو عناوين المحاور—مؤكدًا أن ميزة **editable charts pptx** تعمل كما هو مقصود.

## الخلاصة

أصبح لديك الآن حل كامل لـ **export Excel to PowerPoint** يحافظ على قابلية تحرير المخططات. من خلال تكوين `ImageOrPrintOptions` مع `ExportChartAsEditableText` و `ExportShapeAsEditableText`، ينتج عملية التحويل ملف PPTX أصلي حيث تتصرف المخططات كما لو تم إنشاؤها مباشرة في PowerPoint.

من هنا يمكنك:

* توسيع الكود للتعامل مع عدة أوراق عمل (**worksheet to PowerPoint** لكل منها).  
* دمج التصدير مع ميزات أخرى في Aspose.Cells، مثل إضافة عناوين شرائح أو إدراج صور.  
* استكشاف المواضيع ذات الصلة مثل **export Excel chart PPTX** مع سمات مخصصة أو أتمتة خط أنابيب إنشاء مجموعة الشرائح بالكامل.

لا تتردد في تجربة أنواع مخططات مختلفة، إضافة تسميات بيانات، أو دمج هذا التدفق في نظام تقارير أكبر. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells لـ .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}