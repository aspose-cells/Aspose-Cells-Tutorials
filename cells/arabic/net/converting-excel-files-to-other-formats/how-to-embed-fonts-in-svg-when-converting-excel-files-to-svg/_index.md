---
category: general
date: 2026-09-15
description: تعلم كيفية تضمين الخطوط في SVG وتصدير مخطط Excel إلى PowerPoint، مع تغطية
  تحويل XLSX إلى SVG وتحويل XLSX إلى PPTX مع أمثلة كاملة للكود.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: ar
lastmod: 2026-09-15
og_description: تضمين الخطوط في SVG وتصدير مخطط Excel إلى PowerPoint مع كود C# خطوة
  بخطوة. تحويل XLSX إلى SVG وXLSX إلى PPTX بسرعة وموثوقية.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: تضمين الخطوط في SVG وتصدير مخطط Excel إلى PowerPoint – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية تضمين الخطوط في SVG عند تحويل ملفات Excel إلى SVG و PowerPoint
url: /ar/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في SVG عند تحويل ملفات Excel إلى SVG وPowerPoint  

إذا كنت بحاجة إلى **تضمين الخطوط في SVG** أثناء تحويل مصنف Excel، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعلم أيضًا كيفية **تصدير مخطط Excel إلى PowerPoint**، وكيفية **تحويل XLSX إلى SVG** و **تحويل XLSX إلى PPTX** مع مخططات قابلة للتحرير.  

العمل مع بيانات Excel برمجيًا يعني غالبًا أنك تحتاج إلى نقل المحتوى البصري نفسه بين صيغ ملفات مختلفة. إعادة إنشاء مخطط يدويًا في PowerPoint أو إعادة تطبيق الخطوط في SVG عرضة للأخطاء وتستغرق وقتًا طويلاً. بنهاية هذا البرنامج التعليمي ستحصل على مقطع C# واحد قابل لإعادة الاستخدام يقوم بـ:

* حفظ المصنف كملف SVG مع خطوط مدمجة ومحددات تباين الخط.  
* تصدير نفس المصنف إلى ملف PPTX حيث يبقى المخطط قابلًا للتحرير.  

المتطلب الوحيد هو نسخة حديثة من **Aspose.Cells for .NET** (2024‑x أو أحدث) وبيئة تطوير .NET مثل Visual Studio 2022.

---

## ما ستحتاجه  

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.8).  
* حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* ملف Excel (`input.xlsx`) يحتوي على مخطط واحد على الأقل.  
* صلاحية كتابة إلى دليل الإخراج.  

---

## تضمين الخطوط في SVG أثناء تحويل XLSX إلى SVG  

يضمن تضمين الخطوط أن يتم عرض SVG بشكل صحيح على أي جهاز، حتى إذا كان النظام المستهدف لا يملك الخطوط الأصلية. توفر فئة `SvgSaveOptions` علمين يجعلان ذلك ممكنًا: `EmbedFonts` و `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**لماذا يعمل هذا:**  
* `EmbedFonts = true` ينسخ ملفات الخط إلى قسم `<defs>` في SVG، مما يلغي الاعتماديات الخارجية.  
* `FontVariationSelectors = true` يضيف المحددات اللازمة للخطوط التي تدعم ميزات OpenType، مع الحفاظ على اختلافات الحروف مثل الأحرف المتصلة.  

**النتيجة المتوقعة:** افتح `WithFonts.svg` في أي متصفح حديث؛ سيظهر النص داخل المخطط أو الخلايا بنوع الخط نفسه المستخدم في Excel، حتى على الأجهزة التي لا تملك هذا الخط مثبتًا.

---

## تصدير مخطط Excel إلى PowerPoint مع مخططات قابلة للتحرير  

عندما تحتاج إلى تضمين مخطط في شريحة PowerPoint مع السماح للمستلم بتحرير بيانات المخطط، يوفر `PptxSaveOptions` الخاص بـ Aspose.Cells علم `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**لماذا هذا مهم:**  
تعيين `ExportEditableChart` إلى `true` يخزن المخطط ككائن مخطط Office Open XML بدلاً من صورة ثابتة. عند فتح `EditableChart.pptx` في PowerPoint، يمكنك النقر بزر الماوس الأيمن على المخطط → **Edit Data** وتعديل السلسلة كما في مخطط PowerPoint أصلي.

**خطوات التحقق:**  

1. افتح `EditableChart.pptx` في PowerPoint.  
2. حدد الشريحة التي تحتوي على المخطط.  
3. اختر **Chart Tools → Design → Edit Data**.  
4. تأكد من ظهور شبكة البيانات بنمط Excel وأنه يمكنك تغيير القيم.

---

## تحويل XLSX إلى SVG – ملخص سير العمل الكامل  

فيما يلي نسخة مختصرة تجمع بين التحميل، ومعالجة البيانات الاختيارية، والحفظ كـ SVG. استخدمها عندما تحتاج فقط إلى إخراج SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

استدعِ الطريقة هكذا:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**نصيحة للحالات الخاصة:** إذا كان المصنف يحتوي على خطوط مخصصة غير مثبتة على الخادم، قم بتضمينها يدويًا قبل استدعاء `Save`. استخدم `FontInfoCollection` لإضافة ملفات الخط إلى `SvgSaveOptions` عبر الخاصية `CustomFonts` (متوفرة في إصدارات Aspose.Cells الأحدث).

---

## تحويل XLSX إلى PPTX – الحفاظ على قابلية تحرير المخطط  

توضح الطريقة المساعدة التالية مسار **تحويل XLSX إلى PPTX** مع ضمان بقاء المخطط قابلًا للتحرير.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

الاستخدام:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**سؤال شائع:** *ماذا لو كان لدي مصنف يحتوي على عدة أوراق عمل بها مخططات؟*  
**الإجابة:** يقوم Aspose.Cells بتصدير الورقة الأولى افتراضيًا. لتضمين أوراق إضافية، قم بالتكرار عبر `workbook.Worksheets`، وانسخ كل مخطط إلى شريحة جديدة، واحفظ كل شريحة على حدة باستخدام كائنات `Presentation` من Aspose.Slides. هذا السيناريو المتقدم يتجاوز تدفق “حفظ المصنف كـ SVG” و “تصدير مخطط Excel إلى PowerPoint”، لكن العلامات الأساسية تظل هي نفسها.

---

## نصائح عملية ومخاطر محتملة  

* **الأداء:** يزيد تضمين الخطوط من حجم ملف SVG. إذا كان الحجم مصدر قلق، عيّن `EmbedFonts = false` واعتمد على الخطوط الآمنة للويب.  
* **ترخيص الخطوط:** تأكد من أن لديك الحق في تضمين الخطوط التي تستخدمها؛ بعض الخطوط التجارية تقيد التضمين.  
* **توافق المخططات:** تُحفظ المخططات القابلة للتحرير كأجزاء `chart.xml` داخل PPTX. قد تفقد المخططات المعقدة جدًا (مثل المخططات ثلاثية الأبعاد أو المخططات المختلطة) بعض التنسيقات عند تحريرها في PowerPoint. اختبر أكثر أنواع المخططات شيوعًا التي تحتاجها.  
* **تعارض الإصدارات:** علم `ExportEditableChart` يتطلب Aspose.Cells 20.10 أو أحدث. استخدام نسخة أقدم سيؤدي إلى التحويل الصامت إلى صورة نقطية.  
* **سلامة الخيوط:** كائنات Workbook غير آمنة للاستخدام عبر الخيوط. أنشئ نسخة جديدة من `Workbook` لكل طلب في سيناريو خدمة ويب.  

---

## مثال كامل من البداية إلى النهاية  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

تشغيل هذا البرنامج ينتج ملفين:

* **WithFonts.svg** – ملف SVG يعرض تمامًا كما في عرض Excel، مع تضمين الخطوط.  
* **EditableChart.pptx** – عرض PowerPoint يمكن تحرير المخطط فيه مباشرة.

---

## الخلاصة  

أصبحت الآن تعرف كيف **تضمّن الخطوط في SVG** عندما **تحول XLSX إلى SVG**، وكيف **تصدّر مخطط Excel إلى PowerPoint** مع الحفاظ على قابلية تحرير المخطط. يوضح الكود نفسه طريقة نظيفة لـ **حفظ المصنف كـ SVG** و **تحويل XLSX إلى PPTX** بأقل جهد.  

من هنا يمكنك استكشاف مواضيع إضافية مثل:

* إضافة خطوط مخصصة برمجيًا (`svgOptions.CustomFonts`).  
* معالجة دفعات من المصنفات المتعددة في خدمة خلفية.  
* استخدام Aspose.Slides لإنشاء ملفات PPTX متعددة الشرائح تجمع عدة مخططات Excel.  

جرّب الخيارات، عدّل المقاطع لتناسب مشروعك، واستمتع بتحويلات Excel إلى SVG/PPTX موثوقة دون معالجة يدوية لاحقة. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}