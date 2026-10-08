---
category: general
date: 2026-06-08
description: كيفية تضمين الخطوط عند تحويل Excel إلى PDF باستخدام Aspose.Cells. تعلّم
  تحويل Excel إلى PDF، حفظ المصنف كملف PDF، وتصدير XLSX إلى PDF مع عرض الخطوط بشكل
  مثالي.
draft: false
keywords:
- how to embed fonts
- convert excel to pdf
- save workbook as pdf
- export xlsx to pdf
- save excel as pdf
language: ar
og_description: كيفية تضمين الخطوط عند تحويل Excel إلى PDF يضمن أن تبدو مستنداتك دقيقة
  تمامًا. اتبع هذا الدليل لتحويل Excel إلى PDF، حفظ المصنف كملف PDF، وتصدير XLSX إلى
  PDF مع تضمين الخطوط.
og_title: كيفية تضمين الخطوط عند تحويل Excel إلى PDF – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to embed fonts when converting Excel to PDF using Aspose.Cells.
    Learn to convert Excel to PDF, save workbook as PDF, and export XLSX to PDF with
    perfect font rendering.
  headline: How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide
  type: TechArticle
- description: How to embed fonts when converting Excel to PDF using Aspose.Cells.
    Learn to convert Excel to PDF, save workbook as PDF, and export XLSX to PDF with
    perfect font rendering.
  name: How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide
  steps:
  - name: Why `EmbedStandardFonts = true` matters
    text: When you **save workbook as PDF**, the default behavior is to reference
      system fonts. If the recipient’s computer lacks those fonts, the PDF viewer
      substitutes them, often resulting in garbled text or shifted layouts. By enabling
      `EmbedStandardFonts`, Aspose.Cells copies the font outlines into the P
  - name: Common pitfall
    text: 'If the file is password‑protected, you’ll need to supply the password:'
  - name: 'Edge case: PDFs larger than 10 MB'
    text: 'Some email systems reject attachments over a certain size. If you hit that
      limit, consider:'
  - name: Verifying the embedded fonts
    text: Open the resulting PDF in Adobe Acrobat Reader, go to **File → Properties
      → Fonts**. You should see entries like “Arial (Embedded Subset)”. If the fonts
      are listed as “Not Embedded”, double‑check that `EmbedStandardFonts` is set
      to `true`.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells auto‑detects the format. Just change the input
      file extension, and the same code applies.
    question: Does this work with older versions of Excel (e.g., .xls)?
  - answer: Aspose.Cells is cross‑platform. Ensure the required fonts are installed
      on the Linux machine (e.g., `msttcorefonts` package) so the library can locate
      them before embedding.
    question: What if I’m using .NET Core on Linux?
  - answer: 'Yes. Use `pdfOptions.FontEmbeddingMode = FontEmbeddingMode.Custom` and
      provide a list of font names to embed. --- ## Wrapping Up We’ve covered **how
      to embed fonts when converting Excel to PDF** from start to finish: loading
      the workbook, tweaking `PdfSaveOptions`, saving the file, and verifying the'
    question: Can I embed only specific fonts?
  type: FAQPage
tags:
- Aspose.Cells
- Excel
- PDF conversion
title: كيفية تضمين الخطوط عند تحويل Excel إلى PDF – دليل خطوة بخطوة
url: /ar/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط عند تحويل Excel إلى PDF – دليل كامل

هل تساءلت يومًا **كيفية تضمين الخطوط عند تحويل Excel إلى PDF** بحيث يبدو الناتج مطابقًا تمامًا للجدول الأصلي؟ لست وحدك—فغياب الخطوط أو استبدالها مشكلة شائعة، خاصةً عندما تشارك ملفات PDF مع زملاء لا يمتلكون نفس الخطوط المثبتة. في هذا الدليل سنستعرض حلًا مختصرًا وعملًا بالكامل لا يقتصر فقط على **تحويل Excel إلى PDF** بل يضمن أيضًا أن الخطوط تُحمل مع الملف.

سنستخدم Aspose.Cells (مكتبة .NET شهيرة) لـ **حفظ المصنف كملف PDF**، لكن المفاهيم تنطبق على أي أداة تسمح لك بتعديل خيارات حفظ PDF. بنهاية هذا الدليل ستتمكن من **تصدير XLSX إلى PDF** مع تضمين الخطوط، وستفهم لماذا هذا مهم لتبادل المستندات بشكل موثوق.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). أي بيئة تشغيل حديثة تعمل.
- **Aspose.Cells for .NET** (حزمة NuGet `Aspose.Cells`). مجانية للتجربة وتوفر جميع المميزات.
- ملف Excel (`input.xlsx`) ترغب في تحويله.
- قليل من معرفة C#—ليس كثيرًا، فقط ما يكفي للصق الكود.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، أضف حزمة NuGet عبر `Install-Package Aspose.Cells` في وحدة التحكم الخاصة بمدير الحزم.

---

## ![How to embed fonts when converting Excel to PDF](image.png){alt="كيفية تضمين الخطوط عند تحويل Excel إلى PDF"}

---

## كيفية تضمين الخطوط عند تحويل Excel إلى PDF

البرنامج التالي كامل وجاهز للتنفيذ. يوضح كل خطوة من تحميل المصنف إلى تكوين خيارات PDF التي **تضمن الخطوط القياسية**، وأخيرًا حفظ النتيجة.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.PdfSaveOptions;   // Namespace for PdfSaveOptions (if needed)

class ExcelToPdfWithEmbeddedFonts
{
    static void Main()
    {
        // Step 1: Load or create the workbook
        // Replace YOUR_DIRECTORY with the actual folder path on your machine.
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Configure PDF save options to embed standard fonts
        PdfSaveOptions pdfOptions = new PdfSaveOptions
        {
            // This flag forces the PDF writer to embed the fonts used in the workbook.
            EmbedStandardFonts = true,

            // Optional: you can also embed all custom fonts by setting this to true.
            // EmbedAllFonts = true
        };

        // Step 3: Save the workbook as a PDF using the configured options
        string outputPath = @"YOUR_DIRECTORY\VarSelector.pdf";
        workbook.Save(outputPath, SaveFormat.Pdf, pdfOptions);

        Console.WriteLine($"PDF created at: {outputPath}");
        Console.WriteLine("Fonts are now embedded – open the file to verify.");
    }
}
```

### لماذا `EmbedStandardFonts = true` مهم

عند **حفظ المصنف كملف PDF**، السلوك الافتراضي هو الإشارة إلى خطوط النظام. إذا كان جهاز المستلم لا يحتوي على تلك الخطوط، يقوم عارض PDF باستبدالها، مما يؤدي غالبًا إلى نص مشوش أو تخطيطات متغيرة. بتمكين `EmbedStandardFonts`، تقوم Aspose.Cells بنسخ مخططات الخطوط داخل ملف PDF، مما يجعل المستند مستقلًا. هذا هو الأساس لتضمين الخطوط بفعالية.

---

## الخطوة 1: تحميل مصنف Excel

قبل أن يحدث أي تحويل، تحتاج إلى كائن `Workbook` يمثل ملف `.xlsx` المصدر. القالب يقبل مسار ملف، أو تدفق، أو حتى `DataTable`. إذا لم يكن لديك ملف موجود، يمكنك أيضًا إنشاء مصنف جديد من الصفر:

```csharp
Workbook workbook = new Workbook(); // creates a blank workbook
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].PutValue("Hello, world!");
```

تحميل ملف حقيقي هو السيناريو الأكثر شيوعًا عندما تريد **تحويل Excel إلى PDF**.

### خطأ شائع

إذا كان الملف محميًا بكلمة مرور، ستحتاج إلى توفير كلمة المرور:

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx);
loadOptions.Password = "mySecret";
Workbook workbook = new Workbook("protected.xlsx", loadOptions);
```

---

## الخطوة 2: تكوين خيارات حفظ PDF (قلب عملية تضمين الخطوط)

فئة `PdfSaveOptions` تقدم مجموعة من المفاتيح التي تؤثر على ملف PDF النهائي. بالنسبة لنا الخاصية الأساسية هي `EmbedStandardFonts`. ضبطها على `true` يخبر Aspose.Cells بتضمين الخطوط المدمجة مثل Arial و Times New Roman و Courier.

إذا كان لديك خطوط مخصصة (مثل خطوط العلامة التجارية للشركة) يمكنك أيضًا تضمينها:

```csharp
pdfOptions.EmbedAllFonts = true; // embeds every font used in the workbook
```

كن على علم أن تضمين جميع الخطوط قد يزيد حجم الملف بضع مئات من الكيلوبايت—عادةً ما يكون ذلك مستحقًا من أجل الاتساق.

### حالة خاصة: ملفات PDF أكبر من 10 ميغابايت

بعض أنظمة البريد الإلكتروني ترفض المرفقات التي تتجاوز حجمًا معينًا. إذا وصلت إلى هذا الحد، فكر في:

- تقليل الخطوط (`pdfOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`).
- خفض دقة الصورة (`pdfOptions.DefaultFontResolution = 72` DPI).
- ضغط ملف PDF (`pdfOptions.Compression = CompressionLevel.Best`).

---

## الخطوة 3: حفظ المصنف كملف PDF

استدعاء `workbook.Save` مع ثلاثة معاملات—مسار الإخراج، `SaveFormat.Pdf`، وخيارات `pdfOptions` المُكوَّنة—ينتج المستند النهائي. الطريقة متزامنة وتطرح استثناءً إذا حدث خطأ (مثل عدم وجود صلاحيات كتابة). احرص على وضعها داخل كتلة try‑catch في الكود الإنتاجي.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Pdf, pdfOptions);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to create PDF: {ex.Message}");
}
```

### التحقق من الخطوط المضمنة

افتح ملف PDF الناتج في Adobe Acrobat Reader، ثم انتقل إلى **File → Properties → Fonts**. يجب أن ترى مدخلات مثل “Arial (Embedded Subset)”. إذا ظهرت الخطوط كـ “Not Embedded”، تحقق مرة أخرى من ضبط `EmbedStandardFonts` على `true`.

---

## الخطوة 4: نصائح إضافية لتدفق عمل **تحويل Excel إلى PDF** بلا عيوب

| الحالة | الإعداد الموصى به | لماذا يساعد |
|-----------|--------------------|--------------|
| جداول بيانات كبيرة تحتوي على العديد من الصور | `pdfOptions.JpegQuality = 80` | يقلل حجم الملف دون فقدان ملحوظ في الجودة |
| الحاجة إلى نص قابل للبحث في ملفات PDF | Ensure `pdfOptions.TextCompression = TextCompressionMode.Flate` | يحافظ على إمكانية تحديد النص والبحث فيه |
| رغبة في حماية ملف PDF | `pdfOptions.Password = "secret"` | يضيف طبقة كلمة مرور، مع الحفاظ على تضمين الخطوط |

---

## النتيجة المتوقعة

تشغيل البرنامج مع ملف `input.xlsx` بسيط يحتوي على النص “Hello, world!” سيولد `VarSelector.pdf`. عند فتحه:

- يظهر النص بنفس الخط الموجود في Excel (مثلاً Calibri).
- تبويب **Fonts** في خصائص PDF يسرد كل خط مستخدم مع “Embedded Subset”.
- لا توجد تغييرات في التخطيط أو أحرف مفقودة.

هذا هو الهدف المثالي لـ **حفظ المصنف كملف PDF** مع تضمين الخطوط.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع إصدارات Excel القديمة (مثل .xls)؟**  
ج: بالتأكيد. Aspose.Cells يكتشف الصيغة تلقائيًا. فقط غيّر امتداد ملف الإدخال، ويظل الكود نفسه صالحًا.

**س: ماذا لو كنت أستخدم .NET Core على Linux؟**  
ج: Aspose.Cells متعدد المنصات. تأكد من تثبيت الخطوط المطلوبة على جهاز Linux (مثل حزمة `msttcorefonts`) حتى يتمكن المكتبة من العثور عليها قبل التضمين.

**س: هل يمكنني تضمين خطوط محددة فقط؟**  
ج: نعم. استخدم `pdfOptions.FontEmbeddingMode = FontEmbeddingMode.Custom` وقدم قائمة بأسماء الخطوط التي تريد تضمينها.

---

## الخلاصة

غطينا **كيفية تضمين الخطوط عند تحويل Excel إلى PDF** من البداية إلى النهاية: تحميل المصنف، تعديل `PdfSaveOptions`, حفظ الملف، والتحقق من النتيجة. باتباع هذه الخطوات ستتمكن من **تحويل Excel إلى PDF**، **حفظ المصنف كملف PDF**، و**تصدير XLSX إلى PDF** دون معاناة “استبدال الخطوط”.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة رؤوس/تذييلات، إدراج صور، أو إنشاء ملفات PDF متعددة الأوراق—كل هذه السيناريوهات تستفيد من نفس تقنية تضمين الخطوط.

إذا وجدت هذا الدليل مفيدًا، شاركه، اترك تعليقًا، أو استكشف أدلتنا الأخرى حول معالجة PDF وأتمتة Excel. برمجة سعيدة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [حفظ مصنف Excel كملف PDF مع خطوط مخصصة باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [حفظ مصنف Excel PDF خطوط مخصصة Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [حفظ مصنف Excel PDF خطوط مخصصة Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}