---
category: general
date: 2026-06-24
description: دمج الخطوط في ملف PDF باستخدام Aspose.Cells في C#. تعلم كيفية حفظ Excel
  كملف PDF، وتصدير Excel إلى HTML، وتحويل xlsx إلى PDF باستخدام Aspose، وتكرار الصفوف
  في Pivot.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: ar
og_description: تضمين الخطوط في PDF باستخدام Aspose.Cells في C#. يوضح هذا البرنامج
  التعليمي خطوة بخطوة كيفية حفظ Excel كملف PDF، وتصدير Excel إلى HTML، والمزيد.
og_title: تضمين الخطوط في PDF باستخدام Aspose.Cells – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: تضمين الخطوط في PDF باستخدام Aspose.Cells – دليل C# الكامل
url: /ar/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إدراج الخطوط في PDF باستخدام Aspose.Cells – دليل C# كامل

هل تساءلت يومًا كيف **embed fonts PDF** عندما تقوم بتحويل دفتر عمل Excel باستخدام Aspose.Cells؟ لست وحدك—العديد من المطورين يواجهون مشكلة عندما يبدو ملف PDF الناتج غير صحيح على الأجهزة التي لا تتوفر فيها الخطوط الأصلية مثبتة.  

في هذا الدليل سنستعرض مثالًا واقعيًا لا يقوم فقط بـ **embed fonts PDF**، بل يوضح لك أيضًا كيفية **save Excel as PDF**، **export Excel to HTML**، تحويل **xlsx to PDF with Aspose**، وحتى **duplicate rows pivot** دون كسر جدول المحور. يبدو ذلك كثيرًا؟ لا تقلق—سنقسمه خطوة بخطوة.

## ما ستتعلمه

- كيفية نسخ الصفوف التي تحتوي على جدول محوري مع الحفاظ على سلامة الجدول المحوري.  
- كيفية إدراج smart‑marker يُعيد تكرار ورقة التفاصيل لكل طلب.  
- الإعدادات الدقيقة التي تحتاجها لـ **embed fonts PDF**، وتصدير المخططات كملفات PPTX قابلة للتحرير، والحفاظ على تجميد الألواح عند **export Excel to HTML**.  
- نصائح لاستكشاف الأخطاء الشائعة مثل الخطوط المفقودة أو كائنات OLE المعطوبة.  

**المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.6+)، Aspose.Cells لـ .NET مثبت، وبيئة تطوير C# أساسية (Visual Studio، Rider، أو VS Code). لا توجد حزم NuGet إضافية بخلاف Aspose.Cells مطلوبة.

---

## إدراج الخطوط في PDF – عملية خطوة بخطوة

فيما يلي الشيفرة الكاملة القابلة للتنفيذ. كل قسم مُعلَّق بحيث يمكنك رؤية السبب الدقيق لما نقوم به.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### لماذا يعمل هذا

- **CopyRows** ينسخ الصفوف التي تحتوي على جدول المحور، بحيث يبقى الجدول الأصلي مرتبطًا ببيانات المصدر. هذا يلبي متطلب **duplicate rows pivot**.  
- **SmartMarkerProcessing** ينشئ ورقة عمل جديدة لكل طلب، مما ي automatisation توليد ورقة التفاصيل.  
- **PdfSaveOptions.EmbedStandardFonts = true** يخبر Aspose.Cells بدمج الخطوط مباشرةً في ملف PDF، وهو المفتاح لـ **embed fonts pdf**. بدون هذا الإعداد سيعود PDF إلى الخطوط النظامية، مما يفسد التخطيط على الأجهزة الأخرى.  
- **HtmlSaveOptions** مع `EmbedAllFonts` و `PreserveFreezePanes` يضمن أنه عند **export Excel to HTML**، تكون الدقة البصرية مطابقة لدفتر العمل الأصلي.  

#### النتيجة المتوقعة

- `result.pdf` – ملف PDF حيث يتم دمج جميع الخطوط المستخدمة؛ افتحه على أي جهاز وستظهر النصوص مطابقة للمصدر.  
- `result.pptx` – ملف PowerPoint يحتوي على مخططات قابلة للتحرير وكائنات OLE.  
- `result.html` – مجلد HTML (`result.html` + `result_files`) يعرض دفتر العمل في المتصفح مع تجميد الألواح محفوظًا.  

---

## حفظ Excel كملف PDF باستخدام Aspose.Cells

إذا كان هدفك الوحيد هو **save Excel as PDF**، يمكنك حذف الخطوات الإضافية والتركيز على خيارات PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**نصيحة احترافية:** عندما تستهدف توافق PDF/A، يقوم Aspose تلقائيًا بدمج جميع الخطوط، مما يمنحك طبقة إضافية من الأمان للتخزين طويل الأمد.

---

## تصدير Excel إلى HTML مع الحفاظ على التخطيط

غالبًا ما يؤدي تصدير إلى HTML إلى فقدان مظهر الورقة الأصلية، خاصةً عندما تكون هناك ألواح مجمدة. المقتطف التالي يوضح الإعدادات الدقيقة التي تحتاجها:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

نظرًا لأننا ضبطنا `EmbedAllFonts`، يحتوي HTML المُولَّد على بيانات الخط مشفرة بصيغة base‑64، مما يلبي متطلب **export excel to html** دون الحاجة إلى ملفات CSS خارجية.

---

## تحويل Xlsx إلى PDF باستخدام Aspose.Cells

أحيانًا تظهر عبارة “**xlsx to pdf aspose**” في عمليات البحث. الشيفرة أدناه توضح خط أنابيب التحويل الدقيق، بما في ذلك بعض التحسينات الإضافية:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**لماذا نهتم بإعداد الصفحة؟** إذا تخطيت ذلك، قد يقطع PDF الافتراضي الأعمدة أو الصفوف. تعديل التخطيط أولاً يضمن أن PDF النهائي يطابق ما تراه في Excel.

---

## نسخ الصفوف مع جدول محوري – الحفاظ على سلامة الجدول المحوري

عقبة شائعة هي محاولة نسخ الصفوف التي تحتوي على جدول محوري؛ غالبًا ما يفقد الجدول المحوري اتصاله بمصدر البيانات. طريقة `CopyRows` التي استخدمناها سابقًا تقوم بالعمل الشاق نيابةً عنك:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – الصف الأول من النطاق الذي تريد نسخه.  
- **destinationRow** – المكان الذي يجب وضع النسخة فيه (نفس الورقة، نفس الفهرس الابتدائي لتكرار فعلي).  
- **totalRows** – عدد الصفوف التي سيتم نسخها.  

نظرًا لأن ذاكرة التخزين المؤقت للجدول المحوري موجودة في ورقة العمل، فإن نسخ الصفوف لا يؤدي إلى كسر الجدول المحوري. هذا يلبي كلمة **duplicate rows pivot** مع الحفاظ على تنظيم دفتر العمل.

---

## ملخص المثال الكامل العامل

بجمع كل شيء معًا، إليك البرنامج الكامل الذي يمكنك وضعه في تطبيق Console وتشغيله فورًا:



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [حفظ دفتر عمل Excel كملف PDF مع خطوط مخصصة باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [كيفية تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [كيفية تصدير مقاطع Excel إلى PDF باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}