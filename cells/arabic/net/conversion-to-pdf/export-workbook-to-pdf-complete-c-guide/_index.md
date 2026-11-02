---
category: general
date: 2026-02-26
description: تصدير المصنف إلى PDF مع تضمين الخطوط وأيضًا تصدير المخططات إلى PowerPoint
  باستخدام C#. تعلم كيفية نسخ ورقة جدول محوري وحفظ المصنف كملف PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: ar
og_description: تصدير المصنف إلى PDF مع تضمين الخطوط وأيضًا تصدير المخططات إلى PowerPoint
  باستخدام C#. اتبع الدليل خطوة بخطوة لنسخ جداول Pivot وحفظها كملف PPTX.
og_title: تصدير دفتر العمل إلى PDF – دليل C# الكامل
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: تصدير المصنف إلى PDF – دليل C# الكامل
url: /ar/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير دفتر العمل إلى PDF – دليل C# الكامل

تصدير دفتر العمل إلى PDF هو طلب شائع عندما تحتاج إلى مشاركة التقارير مع أصحاب المصلحة الذين قد لا يكون لديهم Excel مثبت. في هذا الدرس سنظهر لك أيضًا كيفية **تصدير المخططات إلى PowerPoint**، نسخ **ورقة عمل Pivot Table**، وتضمين الخطوط بحيث يبدو ملف PDF مطابقًا تمامًا لتصميمك على الشاشة.  

هل تساءلت يومًا لماذا تفقد بعض ملفات PDF التخطيط الأصلي أو لماذا تنتهي شرائح PowerPoint بأشكال مفقودة؟ الجواب عادةً يكمن في خيارات مفقودة أثناء عملية التصدير. بحلول نهاية هذا الدليل ستحصل على طريقة C# واحدة قابلة لإعادة الاستخدام تعالج كل هذه المشكلات—لا مزيد من النسخ واللصق اليدوي أو العبث بإعدادات التصدير.

## ما ستتعلمه

- كيفية إنشاء دفتر عمل، إضافة تعبيرات Smart Marker، ومعالجتها.  
- كيفية **نسخ ورقة عمل Pivot Table** دون كسر مصدر البيانات.  
- كيفية **تصدير المخططات، الأشكال، ومربعات النص** إلى عرض PowerPoint مع الحفاظ على إمكانية التعديل.  
- كيفية **تضمين الخطوط القياسية** أثناء تصدير PDF لضمان عرض متسق على أي جهاز.  
- كيفية **حفظ دفتر العمل كـ PPTX** باستخدام نهج `save workbook as pptx`.  

كل هذا يعمل مع أحدث مكتبات Aspose.Cells و Aspose.Slides .NET (الإصدار 23.11 وقت كتابة هذا الدرس). لا أدوات خارجية، لا سكريبتات ما بعد المعالجة—فقط C# نقي.

> **نصيحة محترف:** إذا كنت تستخدم Aspose بالفعل في مشروعك، يمكنك إدراج مقتطفات الشيفرة كما هي؛ وإلا، أضف حزم NuGet `Aspose.Cells` و `Aspose.Slides` أولاً.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الشيفرة تعمل أيضًا على .NET Framework 4.7.2).  
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها).  
- Aspose.Cells .NET و Aspose.Slides .NET مثبتتان عبر NuGet.  
- إلمام أساسي بـ C# ومفاهيم Excel مثل Smart Markers و PivotTables.

---

![مخطط تصدير دفتر العمل إلى PDF](export-workbook-to-pdf.png "تدفق عمل تصدير دفتر العمل إلى PDF يظهر مخرجات PDF و PPTX")

## تصدير دفتر العمل إلى PDF – تنفيذ خطوة بخطوة

فيما يلي المثال الكامل الجاهز للتنفيذ. يقوم بإنشاء دفتر عمل، إدخال تعبيرات Smart Marker، معالجتها، نسخ نطاق Pivot Table، وأخيرًا حفظ كل من ملف PDF وملف PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### لماذا يعمل هذا

1. **معالجة Smart Marker** تتيح لك تعبئة دفتر العمل من أي مصدر بيانات (JSON، DataTables، إلخ) دون كتابة حلقات.  
2. **DetailSheetNewName** ينشئ ورقة منفصلة لكل قسم، مما يمنحك تبويبًا نظيفًا لكل قسم.  
3. **نسخ النطاق** (`sourceRange.Copy`) يكرر Pivot Table *بما في ذلك* ذاكرته المؤقتة، لذا فإن الورقة المنسوخة تتصرف تمامًا كالأصل.  
4. **PresentationOptions** مع `ExportCharts`، `ExportShapes`، و `ExportTextBoxes` تخبر Aspose بأن تُظهر تلك الكائنات كعناصر PowerPoint أصلية، مع الحفاظ على إمكانية التعديل.  
5. **PdfSaveOptions.EmbedStandardFonts** يضمن أن يبدو PDF مطابقًا على الأجهزة التي لا تملك الخطوط الأصلية مثبتة.

النتيجة ملفان—`FinalReport.pdf` و `FinalPresentation.pptx`—يمكن إرسالهما بالبريد الإلكتروني، أرشفتهما، أو عرضهما في أي عارض دون فقدان الدقة.

## تصدير المخططات إلى PowerPoint (حفظ دفتر العمل كـ PPTX)

إذا كان تقريرك يحتوي على مخططات، فغالبًا ما تريد أن تكون قابلة للتعديل في PowerPoint. فئة `PresentationOptions` هي المفتاح. إليك مقتطفًا مركزًا يُظهر فقط جزء تصدير المخطط:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**ماذا يحدث خلف الكواليس؟** تقوم Aspose بترجمة كل مخطط Excel إلى مخطط PowerPoint أصلي، مع الحفاظ على السلاسل، عناوين المحاور، والتنسيق. هذا أفضل بكثير من تصدير المخطط كصورة ثابتة، لأن جمهورك يمكنه تعديل نقاط البيانات لاحقًا.

## نسخ ورقة عمل Pivot Table دون فقدان البيانات

غالبًا ما تكون جداول Pivot هي الجزء الأصعب في عملية التصدير لأنها تعتمد على ذاكرة مخبأة مخفية. طريقة `Copy` البسيطة تعمل لأن Aspose ينسخ كلًا من النطاق المرئي **والكائن المخفي للذاكرة المؤقتة**.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **ملاحظة:** إذا كنت تحتاج فقط إلى Pivot Table على ورقة جديدة داخل نفس دفتر العمل، فإن نهج `sourceRange.Copy` السابق أخف وزنًا ويتجنب إنشاء دفتر عمل جديد بالكامل.

## تضمين الخطوط لتصدير PDF – لماذا هذا مهم

عند فتح PDF على جهاز لا يملك الخطوط الأصلية، قد يتحرك النص، تتغير فواصل الأسطر، أو تختفي الأحرف. ضبط `EmbedStandardFonts = true` يخبر Aspose بتضمين أكثر الخطوط شيوعًا (Arial، Times New Roman، إلخ) مباشرةً في تدفق PDF.

إذا كنت تستخدم خطوطًا مخصصة، انتقل إلى `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. إليك مثالًا:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

الآن كل متلقي يرى التخطيط نفسه الذي صممته—دون مفاجآت.

## ملخص المثال الكامل العامل

بجمع كل ما سبق، البرنامج الكامل (الموضح سابقًا) يقوم بما يلي:

1. **ينشئ** دفتر عمل يحتوي على عناصر نائب Smart Marker.  
2. **يعالج** العلامات، مُولّدًا ورقة تفصيلية باسم القسم.  
3. **ينسخ** نطاقًا يحتوي على Pivot Table إلى ورقة عمل جديدة، محافظًا على وظيفتها.  
4. **يصدر** دفتر العمل إلى PowerPoint، مع الحفاظ على المخططات، الأشكال، ومربعات النص قابلة للتعديل.  
5. **يصدر** نفس دفتر العمل إلى PDF مع تضمين الخطوط القياسية لضمان عرض موثوق.

شغّل البرنامج، افتح الملفات المُولدة، وسترى:

- **PDF**: جداول واضحة، خطوط مضمّنة، ونفس النمط البصري لمصدر Excel.  
- **PowerPoint**: مخططات قابلة للتعديل يمكنك النقر بزر الفأرة الأيمن → *Edit Data* في PowerPoint، وأشكال لا تزال قابلة للتلاعب بالكامل.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع .NET Core؟**  
نعم—Aspose.Cells و Aspose.Slides متعددان المنصات. فقط استهدف .NET 6 أو أحدث وسيعمل نفس الكود على Windows أو Linux أو macOS.

**س: ماذا لو أردت تصدير مجموعة فرعية فقط من الأوراق؟**  
استخدم `Workbook.Save` مع `SaveOptions` التي تسمح لك بتحديد `SheetNames`. مثال: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**س: هل يمكنني تشفير ملف PDF؟**  
بالطبع. اضبط `PdfSaveOptions.EncryptionDetails` مع كلمة مرور قبل استدعاء `Save`.

**س: جدول Pivot الخاص بي يستخدم مصدر بيانات خارجي—هل سيكسر النسخ الرابط؟**  
عملية النسخ تشمل الذاكرة المؤقتة، وليس الاتصال الخارجي. سيظل Pivot يعمل دون اتصال، لكنه لن يتجدد ضد المصدر الأصلي. إذا كنت تحتاج إلى تجديد مباشر، صدّر بيانات المصدر مع دفتر العمل.

## الخطوات التالية والمواضيع ذات الصلة

- **Dynamic Data Sources** – تعلم كيفية تغذية JSON أو DataTable إلى Smart Markers لتقارير في الوقت الحقيقي.  
- **Advanced PDF Styling** – استكشف `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}