---
category: general
date: 2026-08-04
description: تصدير مخطط Excel إلى PowerPoint باستخدام Aspose.Cells في C#. اتبع دليل
  التحويل خطوة بخطوة من Excel إلى PowerPoint واحفظ الأشكال قابلة للتحرير.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: ar
lastmod: 2026-08-04
og_description: تصدير مخطط Excel إلى PowerPoint باستخدام Aspose.Cells في C#. تعلّم
  كيفية إنشاء ملف PPTX قابل للتعديل، والحفاظ على بيانات المخطط، وأتمتة تحويل Excel
  إلى PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: تصدير مخطط Excel إلى PowerPoint باستخدام C# – دليل كامل لـ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: تصدير مخطط Excel إلى PowerPoint باستخدام C# – دليل Aspose.Cells الكامل
url: /ar/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير مخطط Excel إلى PowerPoint باستخدام C# – دليل كامل لـ Aspose.Cells

إذا كنت بحاجة إلى **تصدير مخطط Excel إلى PowerPoint**، يوضح لك هذا البرنامج التعليمي كيفية القيام بذلك باستخدام Aspose.Cells و Aspose.Slides في C#. ستحصل على ملف PPTX قابل للتحرير بالكامل يحافظ على بيانات المخطط والأشكال، مما يجعل التحويل جاهزًا لمزيد من أعمال التصميم.

تصدير المخططات من Excel إلى PowerPoint هو طلب شائع عند بناء خطوط تقارير آلية، أو عروض مبيعات، أو مواد تدريبية. في هذا الدليل ستتعلم الخطوات الدقيقة لإجراء **تحويل Excel إلى PowerPoint** يحافظ على جميع عناصر المخطط قابلة للتحرير. لا يلزم النسخ‑اللصق اليدوي، ويعمل الكود مع .NET 6+ وكذلك .NET Framework الكلاسيكي.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- ترخيص صالح لـ Aspose.Cells (أو مفتاح تقييم مجاني)  
- إضافة Aspose.Slides for .NET إلى المشروع (المكتبة تتعامل مع إخراج PPTX)  
- تثبيت .NET 6 SDK أو أحدث  
- مصنف Excel يحتوي على مخطط واحد على الأقل (في هذا المثال نستخدم `Shapes.xlsx`)  

يمكنك تثبيت حزم NuGet باستخدام الأوامر التالية:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## الخطوة 1: تحميل مصنف Excel

العملية الأولى هي فتح المصنف الذي يحتوي على المخطط الذي تريد تصديره. تمثل فئة `Workbook` الملف Excel بالكامل.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**لماذا هذا مهم:** تحميل المصنف يمنحك الوصول إلى أوراق العمل، المخططات، والتنسيقات. يقرأ Aspose.Cells الملف دون الحاجة إلى تثبيت Microsoft Office، مما يجعل الحل خفيفًا وصديقًا للخوادم.

## الخطوة 2: اختيار ورقة العمل وتعريف منطقة الطباعة

قد تحتوي ورقة العمل على العديد من المخططات، لكنك عادةً ما تصدر منطقة محددة. ضبط `PrintArea` يخبر Aspose.Cells أي الخلايا (بما فيها المخططات) يجب أن تُعرض.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**لماذا هذا مهم:** بتقييد التصدير إلى منطقة طباعة محددة تتجنب الشرائح الفارغة غير الضرورية وتحافظ على صغر حجم ملف PPTX. يمكن تعديل المنطقة لتطابق النطاق الدقيق لمخططك.

## الخطوة 3: تكوين خيارات التصدير للحصول على PPTX قابل للتحرير

يستخدم Aspose.Cells فئة `ImageOrPrintOptions` للتحكم في تنسيق الإخراج وقابلية التحرير. ضبط `ImageFormat` إلى `ImageFormat.Pptx` يُنشئ ملف PowerPoint، بينما `ExportEditableShapes = true` يحافظ على كائنات المخطط كأشكال قابلة للتحرير.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**لماذا هذا مهم:** علم `ExportEditableShapes` هو المفتاح للحصول على **أشكال قابلة للتحرير في PowerPoint**. بدون هذا الإعداد، سيُحول المخطط إلى صورة نقطية، مما يفقد القدرة على تعديل نقاط البيانات أو التنسيق لاحقًا.

## الخطوة 4: حفظ ورقة العمل كعرض تقديمي PowerPoint

أخيرًا، استدعِ طريقة `Save` على كائن `Workbook`. يحدد تعداد `SaveFormat.Pptx` لـ Aspose.Cells إنتاج ملف PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

عند انتهاء الكود، افتح `ShapesExport.pptx` في PowerPoint. سترى شريحة تحتوي على المخطط الأصلي من Excel ككائن مخطط PowerPoint أصلي. انقر مزدوجًا على المخطط لتحرير البيانات، تغيير الألوان، أو إضافة حركات—تمامًا كما لو أنك أنشأت المخطط مباشرة في PowerPoint.

### النتيجة المتوقعة

| اسم الملف                | المحتوى على الشريحة                         |
|--------------------------|---------------------------------------------|
| `ShapesExport.pptx`      | المخطط من `Shapes.xlsx` مُعرض ككائن مخطط PowerPoint قابل للتحرير، مع تسميات المحاور، وسيلة الإيضاح، وسلسلة البيانات intact. |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله. يتضمن جميع توجيهات `using` اللازمة، معالجة الأخطاء، وتعليقات.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**شرح كل جزء**

| الجزء | الغرض |
|-------|-------|
| توجيهات `using` | استدعاء مساحات الأسماء Aspose.Cells و Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | يحمل ملف Excel دون الحاجة إلى تثبيت Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | يحدّ التصدير إلى المنطقة التي تحتوي على المخطط. |
| `ImageOrPrintOptions` | يكوّن إخراج PPTX ويفعل **تصدير Aspose.Cells إلى PPTX** مع أشكال قابلة للتحرير. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | يكتب ملف PowerPoint إلى القرص. |
| `try / catch` | يوفر معالجة أساسية للأخطاء مثل الملفات المفقودة أو مشاكل الترخيص. |

تشغيل هذا البرنامج ينتج شريحة PowerPoint يمكنك فتحها في Microsoft PowerPoint، Google Slides (بعد التحويل)، أو أي عارض متوافق.

## الاختلافات الشائعة والحالات الخاصة

### تصدير عدة أوراق عمل

إذا كنت بحاجة إلى شريحة لكل ورقة عمل، قم بالتكرار عبر `workbook.Worksheets` واستدعِ `Save` مع اسم ملف فريد لكل تكرار.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### التحكم في تخطيط الشريحة

يتيح لك Aspose.Slides إضافة تخطيط شريحة مخصص بعد التصدير. أنشئ عرضًا تقديميًا جديدًا، استورد الشريحة المُولدة، ثم طبّق سمة رئيسية.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### معالجة المخططات ذات مصادر البيانات الخارجية

إذا كان المخطط يشير إلى نطاق بيانات خارج منطقة الطباعة المحددة، قم بتمديد `PrintArea` لتشمل تلك الخلايا. وإلا قد يفقد المخطط سلاسل البيانات أثناء التصدير.

### اعتبارات الترخيص

تعمل مكتبات Aspose في وضع التقييم مع علامة مائية. لإزالة العلامة المائية، اضبط الترخيص قبل أي استدعاء API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

افعل نفس الشيء لـ Aspose.Slides إذا كنت تستخدم ميزاته المتقدمة.

## نصائح احترافية

- **إعادة استخدام خيارات التصدير:** أنشئ مثيلًا واحدًا من `ImageOrPrintOptions` وعيّنها لكل ورقة عمل للحفاظ على مبدأ DRY.  
- **المعالجة الدفعية:** لتقارير على نطاق واسع، اجمع منطق التصدير هذا مع عامل خلفية أو Azure Function لتوليد ملفات PPTX عند الطلب.  
- **الأداء:** إذا كنت تحتاج فقط إلى صورة المخطط (ليس قابلة للتحرير)، اضبط `ExportEditableShapes = false`. هذا يقلل من استهلاك الذاكرة ويسرّع التحويل.  
- **الاختبار:** تحقق من صحة ملف PPTX المُنتج على كل من إصدارات PowerPoint على Windows و macOS، حيث قد تختلف بعض العيوب في العرض بين المنصات.

## الخلاصة

أصبح لديك الآن حل كامل من البداية إلى النهاية لـ **تصدير مخطط Excel إلى PowerPoint** باستخدام C#. غطى الدليل تحميل المصنف، اختيار منطقة الطباعة، تكوين **تصدير Aspose.Cells إلى PPTX** مع **أشكال قابلة للتحرير في PowerPoint**، وحفظ النتيجة كملف PPTX قابل للتحرير بالكامل.  

من هنا يمكنك استكشاف سيناريوهات **تحويل Excel إلى PowerPoint** إضافية مثل التصدير الدفعي، تخطيطات شرائح مخصصة، أو دمج العملية في واجهة برمجة تطبيقات ويب. جرّب أنواع مخططات مختلفة، أضف صورًا، أو اجمع عدة أوراق عمل في عرض تقديمي واحد لتخصيص المخرجات وفق احتياجات عملك.

هل أنت مستعد لأتمتة سير عمل التقارير؟ جرّب استبدال ملف المصدر، ضبط منطقة الطباعة، ودمج الكود في خدمات .NET الحالية لديك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}