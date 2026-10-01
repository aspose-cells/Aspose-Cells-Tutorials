---
category: general
date: 2026-10-01
description: تعلم كيفية تضمين الخطوط في HTML أثناء تحويل Excel إلى HTML باستخدام Aspose.Cells.
  صدّر ملف Excel كـ HTML مع الخطوط المضمنة في بضع خطوات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: ar
lastmod: 2026-10-01
og_description: كيفية تضمين الخطوط في HTML عند تصدير ملفات Excel. اتبع هذا الدليل
  خطوة بخطوة لتحويل Excel إلى HTML مع الخطوط المضمنة.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: كيفية تضمين الخطوط في HTML من Excel – دليل Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: كيفية تضمين الخطوط عند تحويل Excel إلى HTML باستخدام Aspose.Cells
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط عند تحويل Excel إلى HTML باستخدام Aspose.Cells

تضمين الخطوط في ملف HTML عند تحويل مصنف Excel أمر أساسي للحفاظ على المظهر الأصلي عبر المتصفحات. إذا كنت بحاجة إلى تحويل Excel إلى HTML مع الحفاظ على الخطوط المخصصة، يوضح هذا الدليل العملية بالكامل. ستتعرف أيضًا على كيفية تصدير Excel كـ HTML ولماذا يعتبر تضمين الخطوط في HTML مهمًا للحصول على عرض متسق.

يغطي هذا البرنامج التعليمي كل ما تحتاجه: المكتبات المطلوبة، تكوين الكود، والتحقق من ملف HTML المُنشأ. في النهاية، ستتمكن من تصدير Excel كـ HTML مع خطوط مدمجة ببضع أسطر من C# فقط.

## ما ستحتاجه

قبل أن تبدأ، تأكد من وجود ما يلي:

* **.NET 6.0 أو أحدث** – يستهدف الكود .NET 6، لكن أي نسخة من .NET تدعم Aspose.Cells ستعمل.
* **Aspose.Cells for .NET** – احصل على ترخيص أو استخدم نسخة التقييم المجانية من موقع Aspose.
* بيئة تطوير **C#** (Visual Studio، Rider، أو VS Code) – أي IDE يمكنه تجميع مشاريع .NET.
* مصنف Excel (`Styled.xlsx`) يستخدم خطوطًا مخصصة تريد الحفاظ عليها.

## الخطوة 1: إعداد Aspose.Cells في مشروع .NET الخاص بك

أولاً، أضف حزمة NuGet الخاصة بـ Aspose.Cells إلى مشروعك:

```bash
dotnet add package Aspose.Cells
```

ثم استورد مساحة الاسم في أعلى ملف C# الخاص بك:

```csharp
using Aspose.Cells;
```

إضافة الحزمة تجعل الفئات `Workbook`، `HtmlSaveOptions`، والفئات المرتبطة متاحة للاستخدام.

## الخطوة 2: تحميل مصنف Excel

تحميل المصنف هو الخطوة الأولى الملموسة في **كيفية تصدير بيانات Excel**. يقوم مُنشئ `Workbook` بقراءة الملف من القرص:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*لماذا هذا مهم:* تقوم Aspose.Cells بتحليل المصنف، بما في ذلك أنماط الخلايا، الصيغ، ومعلومات الخط. إذا تعذر العثور على الملف، سيتم رمي استثناء، لذا تأكد من صحة المسار.

## الخطوة 3: تكوين خيارات حفظ HTML لتضمين الخطوط

جوهر **تضمين الخطوط في html** هو فئة `HtmlSaveOptions`. اضبط `EmbedFonts` على `true` حتى يتم كتابة كل خط مستخدم في المصنف داخل مخرجات HTML كقاعدة `@font-face` مشفرة بـ Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*لماذا هذا مهم:* بشكل افتراضي، تشير Aspose.Cells إلى ملفات خطوط خارجية قد لا تكون متوفرة على جهاز العميل. تمكين `EmbedFonts` يضمن أن HTML المعروض يبدو مطابقًا لورقة Excel الأصلية، بغض النظر عن الخطوط المثبتة لدى المشاهد.

### حالة حافة: الخطوط غير المدعومة

إذا كان المصنف يستخدم خطًا غير مثبت على الخادم، فإن Aspose.Cells ستعود إلى خط نظام افتراضي. لتجنب ذلك، قم بتثبيت الخطوط المطلوبة على الخادم أو قم بتضمينها يدويًا بعد التصدير.

## الخطوة 4: حفظ المصنف كـ HTML باستخدام الخيارات المكوَّنة

الآن يمكنك كتابة ملف HTML. طريقة `Save` تأخذ مسار الإخراج وكائن `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

بعد التنفيذ، يحتوي `Styled.html` على بيانات الجدول وكتلة `<style>` مع تعريفات `@font-face` المشفرة بـ Base64 لكل خط مخصص.

## الخطوة 5: التحقق من الخطوط المدمجة

افتح `Styled.html` في متصفح. افحص قسم `<head>`؛ يجب أن ترى شيئًا مشابهًا لـ:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

إذا ظهرت الخطوط بشكل صحيح في الجدول المعروض، فإن عملية التضمين نجحت. إذا لاحظت فقدان رموز، فتأكد من تثبيت ملفات الخط المصدر على الجهاز الذي يجري التحويل.

## الاختلافات الشائعة والخيارات الإضافية

### تحويل أوراق عمل متعددة

إذا كنت بحاجة إلى **تحويل Excel إلى HTML** لجميع أوراق العمل، اضبط `ExportActiveWorksheetOnly = false` (الإعداد الافتراضي). ستقوم Aspose.Cells بإنشاء ملف HTML منفصل لكل ورقة.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### التحكم في مخرجات CSS

يمكنك تقليل حجم HTML بتعطيل CSS المضمن داخل العناصر:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### استخدام Stream بدلاً من ملف

عند دمج العملية في واجهة ويب API، اكتب HTML إلى `MemoryStream` وأعده مباشرة:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## نصيحة احترافية: رخصة المنتج لإزالة علامات التقييم

إذا كنت تستخدم نسخة التقييم، قد يحتوي HTML المُولد على تعليق علامة مائية. قم بتطبيق ترخيص Aspose.Cells قبل تحميل المصنف للحصول على مخرجات نظيفة:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## مثال كامل يعمل

فيما يلي برنامج كامل قابل للتنفيذ يوضح **كيفية تضمين الخطوط**، **تحويل Excel إلى HTML**، و**تصدير Excel كـ HTML** في خطوة واحدة:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**الناتج المتوقع:** بعد تشغيل البرنامج، سيظهر `Styled.html` في `YOUR_DIRECTORY`. فتح الملف في أي متصفح حديث يعرض الجدول بنفس الخطوط الموجودة في ملف Excel الأصلي، حتى على الأجهزة التي لا تملك تلك الخطوط.

## الخلاصة

أنت الآن تعرف **كيفية تضمين الخطوط** عندما **تحول Excel إلى HTML** باستخدام Aspose.Cells، وقد رأيت التدفق الكامل من تحميل المصنف إلى التحقق من الخطوط المدمجة. يضمن هذا النهج الحفاظ على الدقة البصرية لملفات Excel في HTML المُولد، مما يجعله مثاليًا للتقارير على الويب، النشرات البريدية، أو أي سيناريو يتطلب **تصدير Excel كـ HTML** مع طباعة مخصصة.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **تصدير Excel كـ PDF**، **تنسيق مخرجات HTML بـ CSS مخصص**، أو **معالجة دفعات متعددة من المصنفات**. جميعها تعتمد على نمط `HtmlSaveOptions` نفسه، لذا يمكنك تعديل الكود بتغييرات قليلة فقط.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}