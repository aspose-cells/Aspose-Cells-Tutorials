---
category: general
date: 2026-07-26
description: كيفية تصدير الأشكال من ورقة عمل إكسل إلى باوربوينت في بضع خطوات فقط –
  دليل سريع لتصدير إكسل إلى pptx للمطورين.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: ar
lastmod: 2026-07-26
og_description: كيفية تصدير الأشكال من إكسل إلى باوربوينت خطوة بخطوة. اتبع هذا الدليل
  لتصدير إكسل إلى بي بي تي إكس وشاهد أوراق عملك تتحول إلى شرائح قابلة للتحرير.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: كيفية تصدير الأشكال من إكسل إلى باوربوينت – سريع وسهل
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: كيفية تصدير الأشكال من إكسل إلى باوربوينت – دليل شامل
url: /ar/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير الأشكال من Excel إلى PowerPoint – دليل كامل

هل تساءلت يومًا **how to export shapes** من ملف Excel وكيفية الحفاظ عليها قابلة للتحرير في عرض PowerPoint؟ أنت لست الوحيد. سواء كنت تبني خط أنابيب تقارير أو تحتاج ببساطة إلى طريقة سريعة لتحويل جدول بيانات إلى عرض تقديمي، فإن القدرة على **convert worksheet to PowerPoint** دون فقدان قابلية تحرير الأشكال يمكن أن توفر لك ساعات من العمل اليدوي.

في هذا **excel to powerpoint tutorial** سنستعرض مثالًا كاملًا بلغة C# يقوم بتحميل دفتر عمل، ضبط خيارات التصدير الصحيحة، وكتابة ملف PPTX حيث تظل مربعات النص وغيرها من كائنات الرسم قابلة للتحرير. لا مراجع غامضة—فقط الشيفرة التي يمكنك نسخها ولصقها وتشغيلها اليوم.

## ما ستتعلمه

- الخطوات الدقيقة لـ **export excel to pptx** مع الحفاظ على قابلية تحرير الأشكال.  
- كيف تتحكم مكتبة `Aspose.Cells` وخيارات `PptxSaveOptions` في سلوك التصدير.  
- نصائح للتعامل مع أوراق عمل متعددة، ملفات مفقودة، وإعدادات الأشكال المخصصة.  
- برنامج كامل قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الشيفرة تعمل أيضًا على .NET Framework 4.7+).  
- ترخيص صالح لـ **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يكفي للاختبار).  
- دفتر عمل Excel (مثال: `ShapesDemo.xlsx`) يحتوي على مربع نص أو شكل واحد على الأقل.  
- بيئة تطوير—Visual Studio أو Rider أو VS Code تكفي.

إذا كان لديك كل ذلك، لنبدأ.

## الخطوة 1: تحميل دفتر العمل – نقطة الانطلاق لتصدير الأشكال  

أولًا نحتاج إلى فتح ملف Excel الذي يحتوي على الأشكال التي نريد الحفاظ عليها قابلة للتحرير.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**لماذا هذا مهم:**  
كائن `Workbook` هو البوابة إلى كل خلية، رسم بياني، وكائن رسم داخل الملف. من خلال الحصول على أول ورقة عمل (`Worksheets[0]`) نضمن أننا نعمل على ورقة معروفة، لكن يمكنك استبدال الفهرس باسم (`workbook.Worksheets["Sheet2"]`) إذا كنت تحتاج إلى تبويب محدد.

> **نصيحة احترافية:** غلف استدعاء التحميل داخل كتلة `try / catch` لتقديم رسالة خطأ ودية إذا كان مسار الملف غير صحيح.

## الخطوة 2: ضبط خيارات تصدير PPTX – جوهر تصدير الأشكال  

الآن نخبر Aspose.Cells بالحفاظ على الأشكال قابلة للتحرير في ملف PPTX الناتج.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**لماذا هذه العلامات؟**  
- `ExportEditableTextBoxes` يحول مربعات النص في Excel إلى عناصر نائبة نصية في PowerPoint يمكنك النقر المزدوج عليها وتحريرها.  
- `ExportEditableShapes` يفعل نفس الشيء للأشكال مثل الأسهم، المستطيلات، وSmartArt. بدون هذه العلامات، تتحول الكائنات إلى صور ثابتة، مما يفقد هدف **convert worksheet to powerpoint**.

يمكنك أيضًا تعديل `PptxSaveOptions` للتحكم في حجم الشريحة، السمة، أو ما إذا كان سيتم تضمين الخطوط—مفيد عندما يجب أن يتطابق العرض مع هوية الشركة.

## الخطوة 3: حفظ الورقة كملف PPTX – القطعة النهائية لتصدير Excel Workbook إلى PowerPoint  

مع ضبط الخيارات، يصبح الحفظ بسيطًا.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**ماذا يحدث خلف الكواليس؟**  
تقوم Aspose.Cells بالتكرار عبر كل كائن رسم على الورقة، وتطابقه مع فئة الشكل المقابلة في PowerPoint، وتكتب XML الذي يقرأه PowerPoint. لأننا فعلنا العلامات القابلة للتحرير، فإن XML يحدد كل شكل كـ `Shape` بدلاً من `Picture`، لذا يتعامل PowerPoint معه ككائن حي.

## الخطوة 4: تأكيد التصدير – رد فعل سريع للمستخدم  

رسالة صغيرة في وحدة التحكم تخبرك بأن العملية نجحت.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

إذا شغلت البرنامج ورأيت الرسالة، افتح `ShapesEditable.pptx` في PowerPoint. انقر على أي مربع نص—يجب أن تكون قادرًا على تحرير النص مباشرة، وسحب الشكل يجب أن يحركه كما لو كان كائن PowerPoint أصلي.

## الخطوة 5: معالجة سيناريوهات العالم الحقيقي  

فيما يلي بعض الاختلافات الشائعة التي قد تواجهها أثناء العمل على **excel to powerpoint tutorial**.

### أوراق عمل متعددة

إذا كنت بحاجة لتصدير عدة أوراق إلى ملف PPTX واحد، قم بالتكرار عبر `workbook.Worksheets` واستدعِ `worksheet.Save` باستخدام نفس `pptxOptions`. ستضيف Aspose.Cells شريحة جديدة تلقائيًا لكل ورقة.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### تخطيطات شرائح مخصصة

يمكنك تحديد `pptxOptions.SlideSize` (مثال: `SlideSizeType.Widescreen`) لتتناسب مع أبعاد عرض الشركة.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### ملفات مفقودة أو أذونات

غلف طريقة `Main` بالكامل داخل كتلة `try`:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

هذا يجعل عملية **export excel workbook powerpoint** قوية للخطوط الإنتاجية.

## مثال كامل يعمل

إليك البرنامج الكامل الذي يمكنك تجميعه الآن. احفظه باسم `ExportEditableShapes.cs`، عدل مسارات الملفات، وشغّله باستخدام `dotnet run`.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**المخرجات المتوقعة** عند تشغيل البرنامج:

```
Exported worksheet with editable shapes.
```

افتح ملف `ShapesEditable.pptx` الناتج وسترى كل شكل من Excel ككائن PowerPoint قابل للتحرير بالكامل—بالضبط ما طلبته عندما بحثت عن **how to export shapes**.

## الأسئلة المتكررة

- **هل يعمل هذا مع صيغ Excel القديمة (.xls)؟**  
  نعم. يمكن لـ `Workbook` فتح `.xls` و`.xlsx` وحتى ملفات CSV. يعمل تصدير الأشكال بنفس الطريقة.

- **ماذا لو أردت الحفاظ على المخططات قابلة للتحرير؟**  
  المخططات تُصدر بالفعل كمخططات PowerPoint أصلية؛ لا تحتاج إلى علامات إضافية.

- **هل يمكنني التصدير إلى PDF بدلاً من PPTX؟**  
  بالطبع—استبدل `SaveFormat.Pptx` بـ `SaveFormat.Pdf` وتخلص من `PptxSaveOptions`.

## الخلاصة

أصبح لديك الآن حل شامل من البداية إلى النهاية لـ **how to export shapes** من Excel إلى عرض PowerPoint قابل للتحرير. من خلال الاستفادة من `Aspose.Cells` وخيارات `PptxSaveOptions`، تحتفظ بكل مربع نص وكائن رسم، محولًا جدول بيانات ثابت إلى عرض تقديمي ديناميكي بأقل جهد ممكن.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة قوالب شرائح مخصصة، إدراج صور برمجيًا، أو ربط هذا التصدير بأنابيب CI/CD التي تُنشئ عروض مبيعات أسبوعية تلقائيًا. عالم **export excel workbook powerpoint** مفتوح على مصراعيه—اكتشفه!

*إذا وجدت هذا **excel to powerpoint tutorial** مفيدًا، أعطه نجمة على GitHub أو شاركه مع زميل لا يزال ينسخ‑يلصق جداول البيانات إلى الشرائح. برمجة سعيدة!*

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [كيفية تصدير خلايا Excel كصور باستخدام Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [كيفية تصدير مخططات Excel كـ SVG باستخدام Aspose.Cells Java للرسومات المتجهة القابلة للتوسيع](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}