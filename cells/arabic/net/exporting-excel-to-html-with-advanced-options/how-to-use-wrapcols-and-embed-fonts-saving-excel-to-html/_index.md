---
category: general
date: 2026-10-20
description: تعلم كيفية استخدام wrapcols في Aspose.Cells، وإدراج الخطوط في HTML، وحفظ
  ملف Excel كـ HTML مع مثال كامل بلغة C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: ar
lastmod: 2026-10-20
og_description: كيفية استخدام wrapcols في Aspose.Cells، وتضمين الخطوط في HTML، وتحويل
  دفتر العمل إلى HTML مع دليل واضح بلغة C# للمطورين.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: كيفية استخدام wrapcols وتضمين الخطوط عند تصدير Excel إلى HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: كيفية استخدام wrapcols وتضمين الخطوط عند حفظ Excel إلى HTML
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام wrapcols وتضمين الخطوط وحفظ Excel كـ HTML

إذا كنت بحاجة إلى **كيفية استخدام wrapcols** في صيغة Aspose.Cells، يوضح لك هذا الدليل الخطوات الدقيقة. ستتعلم أيضًا **كيفية تضمين الخطوط في HTML** و**حفظ Excel كـ HTML** بحيث يبدو الناتج متطابقًا عبر المتصفحات.  

يغطي الدرس ثلاثة سيناريوهات عملية: استخدام دالة `WRAPCOLS`، تصدير دفتر عمل مع خطوط مضمَّنة، وإنشاء تقرير رئيس‑تفصيل باستخدام Smart Markers. في النهاية ستحصل على برنامج C# واحد قابل للتنفيذ يوضح كل هذه الميزات.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) مثبت.
* Aspose.Cells for .NET مضاف إلى مشروعك (`dotnet add package Aspose.Cells`).
* إلمام أساسي بـ C# وصيغ Excel.

لا توجد مكتبات طرف ثالث إضافية مطلوبة؛ فـ Aspose.Cells يتعامل مع تحويل HTML وتضمين الخطوط داخليًا.

## الخطوة 1: إظهار وظيفة **كيفية استخدام wrapcols** في صيغة

دالة `WRAPCOLS` تقسم نطاقًا أحادي الأبعاد إلى مصفوفة ثنائية الأبعاد، مع تعبئة الأعمدة أولاً. هذا مفيد عندما تحتاج إلى إعادة تشكيل البيانات للتقارير أو الرسوم البيانية.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**لماذا يعمل هذا:**  
تأخذ `WRAPCOLS` معاملين – النطاق المصدر وعدد الأعمدة. تقوم الدالة بتعبئة المصفوفة عموديًا، متجاهلة أي قيم زائدة (الـ `3` في المثال). تظهر النتيجة في الخلية العليا اليسرى للنطاق الهدف (`B1`)، ويمكنك توسيع النطاق يدويًا إذا كنت بحاجة إلى المصفوفة الكاملة.

> **نصيحة احترافية:** بعد تعيين الصيغة، استدعِ `workbook.CalculateFormula()` لضمان أن النتيجة محدثة قبل قراءة قيم الخلايا.

## الخطوة 2: **تحويل دفتر العمل إلى HTML** و**تضمين الخطوط في html**

عند تصدير ملف Excel إلى HTML، غالبًا ما تستبدل المتصفحات الخطوط بخطوطها الافتراضية، مما قد يفسد التخطيط البصري. يتيح لك Aspose.Cells تضمين الخطوط الدقيقة المستخدمة في دفتر العمل مباشرةً داخل ملف HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**لماذا يعتبر تضمين الخطوط مهمًا:**  
عند ضبط `EmbedFonts` على `true`، يقوم Aspose.Cells بتحويل كل خط TrueType/OpenType مستخدم إلى قاعدة `@font-face` مشفّرة بـ Base64 داخل HTML المُولَّد. هذا يلغي الحاجة إلى تثبيت الخطوط نفسها على جهاز العميل، مما يضمن عرضًا بكسلًا مثاليًا.

> **حالة خاصة:** إذا كان دفتر العمل المصدر يشير إلى خط غير مثبت على الخادم، سيعود Aspose.Cells إلى خط افتراضي ويصدر تحذيرًا. تأكد من توفر الخطوط المطلوبة


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Embed Fonts in HTML – Convert Excel to HTML with C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [How to Convert Excel Files to HTML Using Aspose.Cells for .NET: Hiding Overlaid Content](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}