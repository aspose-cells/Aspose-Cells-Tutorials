---
category: general
date: 2026-11-19
description: كيفية تضمين الخطوط عند تصدير Excel إلى PDF باستخدام C#. تعلم كيفية حفظ
  المصنف كملف PDF مع تضمين الخطوط لمشاركة المستندات بشكل موثوق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel to pdf
- save workbook as pdf
- save excel as pdf
- pdf export embedded fonts
language: ar
lastmod: 2026-11-19
og_description: كيفية تضمين الخطوط أثناء تصدير Excel إلى PDF باستخدام C#. يوضح هذا
  الدليل كيفية حفظ المصنف كملف PDF مع خطوط مدمجة لضمان عرض ثابت.
og_image_alt: Screenshot illustrating how to embed fonts during Excel to PDF export
og_title: كيفية تضمين الخطوط عند تصدير Excel إلى PDF باستخدام C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to embed fonts while exporting Excel to PDF using C#. Learn to
    save workbook as PDF with embedded fonts for reliable document sharing.
  headline: How to embed fonts when exporting Excel to PDF with C#
  type: TechArticle
- description: How to embed fonts while exporting Excel to PDF using C#. Learn to
    save workbook as PDF with embedded fonts for reliable document sharing.
  name: How to embed fonts when exporting Excel to PDF with C#
  steps:
  - name: Install the Aspose.Cells NuGet package
    text: 'Open a terminal in your project folder and run:'
  - name: Load the workbook you want to export
    text: '```csharp using Aspose.Cells;'
  - name: Configure PDF save options to embed standard fonts
    text: '```csharp // Create PDF save options PdfSaveOptions pdfOptions = new PdfSaveOptions
      { // When true, standard fonts (Arial, Times New Roman, etc.) are embedded in
      the PDF. EmbedStandardFonts = true,'
  - name: Save the workbook as a PDF using the configured options
    text: '```csharp // Export the workbook to PDF with embedded fonts workbook.Save(@"C:\Data\output.pdf",
      pdfOptions); ```'
  - name: Expected output
    text: Open `output.pdf` in any PDF viewer. The document should display the same
      typefaces as the original Excel file, even on a machine that lacks those fonts.
      You can verify font embedding by opening the PDF in Adobe Acrobat and checking
      **File → Properties → Fonts** – the list will show each font with t
  - name: Conclusion
    text: You now know **how to embed fonts** when you **export Excel to PDF** using
      C#. By configuring `PdfSaveOptions.EmbedStandardFonts` and saving the workbook
      with `Save`, you achieve a reliable **save workbook as pdf** operation that
      preserves typography across all viewers. Apply the checklist, avoid th
  type: HowTo
tags:
- C#
- Aspose.Cells
- PDF
- Excel automation
title: كيفية تضمين الخطوط عند تصدير Excel إلى PDF باستخدام C#
url: /ar/net/conversion-to-pdf/how-to-embed-fonts-when-exporting-excel-to-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط عند تصدير Excel إلى PDF باستخدام C#

إذا كنت بحاجة إلى **كيفية تضمين الخطوط** أثناء تصدير مصنف Excel إلى PDF، فإن هذا الدليل يوضح العملية بالكامل. ستتعلم **تصدير Excel إلى PDF** مع تضمين الخطوط بحيث يتم عرض الملف الناتج بشكل صحيح على أي جهاز.

يُزيل تضمين الخطوط مشكلة “الخط المفقود” التي تظهر غالبًا عندما يُفتح ملف PDF على جهاز لا يحتوي على الخطوط الأصلية. يغطي الدليل أيضًا **save workbook as PDF**، **save Excel as PDF**، وغيرها من السيناريوهات ذات الصلة.

## ما ستحققه

* تحميل ملف `.xlsx` موجود في C#.
* تهيئة تصدير PDF لتضمين الخطوط القياسية.
* حفظ المصنف كملف PDF يحافظ على الطباعة الأصلية.
* التحقق من أن PDF يحتوي على الخطوط المضمنة.

تحتاج إلى .NET 6 أو أحدث وإشارة إلى مكتبة **Aspose.Cells**، التي توفر `Workbook` و `PdfSaveOptions`. لا توجد أدوات طرف ثالث إضافية مطلوبة.

## كيفية تضمين الخطوط عند تصدير Excel إلى PDF

### الخطوة 1: تثبيت حزمة Aspose.Cells عبر NuGet

افتح طرفية في مجلد المشروع الخاص بك وشغّل:

```bash
dotnet add package Aspose.Cells
```

تضيف الحزمة مساحة الأسماء `Aspose.Cells`، التي تحتوي على الفئة `Workbook` لقراءة ملفات Excel وفئة `PdfSaveOptions` للتحكم في إخراج PDF.

### الخطوة 2: تحميل المصنف الذي تريد تصديره

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

`Workbook` يحلل ملف Excel ويُنشئ تمثيلًا في الذاكرة لجميع الأوراق، الأنماط، والكائنات المدمجة. يجب تحميل الملف أولاً قبل تطبيق أي خيارات تصدير.

### الخطوة 3: تهيئة خيارات حفظ PDF لتضمين الخطوط القياسية

```csharp
// Create PDF save options
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    // When true, standard fonts (Arial, Times New Roman, etc.) are embedded in the PDF.
    EmbedStandardFonts = true,

    // Optional: set the compliance level if you need PDF/A‑1b for archiving.
    Compliance = PdfCompliance.PdfA1b
};
```

ضبط `EmbedStandardFonts` إلى **true** يجبر المصدّر على تضمين الخطوط المستخدمة في المصنف. هذا يلبي مباشرةً متطلبات **pdf export embedded fonts** ويضمن أن يظهر PDF متطابقًا على جميع المنصات.

### الخطوة 4: حفظ المصنف كملف PDF باستخدام الخيارات المكوّنة

```csharp
// Export the workbook to PDF with embedded fonts
workbook.Save(@"C:\Data\output.pdf", pdfOptions);
```

طريقة `Save` تكتب ملف PDF إلى المسار المحدد. نظرًا لأن `pdfOptions` يحتوي على `EmbedStandardFonts` مفعّلًا، فإن الملف الناتج يحتوي على بيانات الخط.

> **نصيحة احترافية:** إذا كان المصنف يستخدم خطوطًا مخصصة غير مثبتة على الخادم، عيّن `PdfSaveOptions.CustomFontsFolder` إلى المجلد الذي يحتوي على تلك الخطوط قبل استدعاء `Save`.

### النتيجة المتوقعة

افتح `output.pdf` في أي عارض PDF. يجب أن يعرض المستند نفس الخطوط كما في ملف Excel الأصلي، حتى على جهاز لا يملك تلك الخطوط. يمكنك التحقق من تضمين الخطوط بفتح PDF في Adobe Acrobat وفحص **File → Properties → Fonts** – ستظهر القائمة كل خط مع كلمة “Embedded”.

![كيفية تضمين الخطوط أثناء تصدير Excel إلى PDF](/images/excel-pdf-embed-fonts.png){: .center alt="لقطة شاشة توضح كيفية تضمين الخطوط أثناء تصدير Excel إلى PDF"}

## تصدير Excel إلى PDF مع خطوط مضمّنة – مكتبات بديلة

إذا لم تتمكن من استخدام Aspose.Cells، فإن مكتبة COM **Microsoft.Office.Interop.Excel** تدعم أيضًا تصدير PDF، لكنها **لا** توفر علامة مدمجة لتضمين الخطوط. في هذه الحالة يجب عليك:

1. تصدير المصنف إلى PDF.
2. تشغيل خطوة معالجة لاحقة باستخدام مكتبة PDF مثل **iTextSharp** لتضمين الخطوط المفقودة.

نظرًا لأن هذا النهج يضيف تعقيدًا ويتطلب بيئة Windows، يظل Aspose.Cells هو الحل الموصى به لتصدير **export excel to pdf** موثوق مع خطوط مضمّنة.

## حفظ المصنف كملف PDF – قائمة التحقق

بعد انتهاء التصدير، مرّ بهذه القائمة:

| ✅ | عنصر القائمة |
|---|---|
| 1 | يفتح ملف PDF دون تحذيرات استبدال الخط. |
| 2 | `PdfSaveOptions.EmbedStandardFonts` مضبوط على `true`. |
| 3 | الخطوط المخصصة (إن وجدت) موجودة في المجلد المشار إليه بـ `CustomFontsFolder`. |
| 4 | يتوافق PDF مع معيار PDF/A المطلوب، إذا لزم الأمر. |

إذا فشل أي عنصر، أعد مراجعة الإعدادات في **Step 3** وتأكد من أن ملفات الخطوط متاحة للعملية.

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|---|---|---|
| ظهور الخطوط كبدائل | `EmbedStandardFonts` ترك على القيمة الافتراضية `false`. | تفعيل `EmbedStandardFonts = true`. |
| حجم PDF كبير (> 10 MB) | تضمين العديد من خطوط TrueType الكبيرة يزيد الحجم. | قصر التضمين على الخطوط المستخدمة فقط، أو ضغط PDF باستخدام `PdfSaveOptions.Compress = true`. |
| فشل التصدير على خادم بدون واجهة (headless) | الخادم يفتقر إلى الخطوط المطلوبة. | تثبيت الخطوط اللازمة على الخادم أو توجيه `CustomFontsFolder` إلى مجموعة خطوط مدمجة. |

## حفظ Excel كملف PDF – الخطوات التالية

الآن بعد أن يمكنك **save excel as pdf** مع خطوط مضمّنة، فكر في توسيع سير العمل:

* **Batch processing** – التكرار عبر مجلد من ملفات Excel وتصدير كل ملف باستخدام نفس `PdfSaveOptions`.
* **Password protection** – استخدم `PdfSaveOptions.Password` لحماية PDF بكلمة مرور.
* **Watermarking** – أضف علامة مائية نصية أو صورة عبر `PdfSaveOptions.Watermark` قبل الحفظ.

هذه التحسينات تبني على الأساس نفسه الذي أنشأته للتو.

---

### الخلاصة

أنت الآن تعرف **كيفية تضمين الخطوط** عندما **تصدّر Excel إلى PDF** باستخدام C#. من خلال تهيئة `PdfSaveOptions.EmbedStandardFonts` وحفظ المصنف باستخدام `Save`، تحصل على عملية **save workbook as pdf** موثوقة تحافظ على الطباعة عبر جميع العارضات. طبّق قائمة التحقق، تجنّب المشكلات المذكورة، واستكشف الخطوات التالية المقترحة لأتمتة إنشاء PDF في تطبيقاتك.

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تضمين الخطوط عند تحويل Excel إلى PDF – دليل كامل](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)
- [كيفية تضمين الخطوط عند تحويل Excel إلى PDF – دليل خطوة بخطوة](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)
- [كيفية تصدير PDF من Excel – دليل كامل لحفظ المصنف كملف PDF](/cells/english/net/conversion-to-pdf/how-to-export-pdf-from-excel-complete-guide-to-save-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}