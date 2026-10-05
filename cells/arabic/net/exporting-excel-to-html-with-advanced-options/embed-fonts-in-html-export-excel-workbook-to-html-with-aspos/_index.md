---
category: general
date: 2026-06-17
description: تضمين الخطوط في HTML عند حفظ المصنف كملف HTML. تعلّم كيفية تحويل المصنف
  إلى HTML وتصدير HTML من Excel مع الخطوط المدمجة في بضع خطوات.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: ar
og_description: تضمين الخطوط في HTML عند حفظ المصنف كملف HTML. اتبع هذا الدليل لتحويل
  المصنف إلى HTML وتعلم كيفية تصدير Excel HTML بدعم كامل للخطوط.
og_title: تضمين الخطوط في HTML – تصدير مصنف Excel إلى HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: تضمين الخطوط في HTML – تصدير مصنف Excel إلى HTML باستخدام Aspose.Cells
url: /ar/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تضمين الخطوط في HTML – تصدير مصنف Excel إلى HTML باستخدام Aspose.Cells

هل تساءلت يومًا كيف **تضمين الخطوط في HTML** عند تصدير ورقة Excel؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يظهر HTML المُولد بخط عام sans‑serif بدلاً من تنسيق Excel الأصلي. الخبر السار؟ ببضع أسطر من الشيفرة يمكنك **حفظ المصنف كـ HTML** والحفاظ على كل الخطوط كما هي.

في هذا الدرس سنستعرض العملية الكاملة لـ **تحويل المصنف إلى HTML** باستخدام Aspose.Cells for .NET، نشرح لماذا يعتبر تضمين الخطوط مهمًا، ونظهر لك بالضبط **كيفية تصدير Excel إلى HTML** بحيث يكون الناتج مشابهًا تمامًا لورقة العمل الأصلية. لا أدوات خارجية، لا معالجة يدوية بعد‑الإنشاء—فقط كود C# نظيف وقابل للتنفيذ.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (المثال يعمل على .NET Core، .NET Framework، و .NET 5+)
- حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- فهم أساسي للغة C# وتعامل مع ملفات Excel
- اختياريًا: ملف خط TrueType مخصص تريد تضمينه (مثال: `MyFont.ttf`)

هل لديك كل ذلك؟ عظيم—لنبدأ.

## الخطوة 1: إعداد المشروع وتحميل مصنف Excel

أولاً نحتاج إلى كائن مصنف. يمكنك إنشاء واحد من الصفر أو تحميل ملف `.xlsx` موجود. إليك إعدادًا بسيطًا يضيف أيضًا خطًا مخصصًا إلى مجموعة أنماط المصنف.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*لماذا هذه الخطوة؟* بتحميل المصنف أولًا نعطي Aspose.Cells فرصة لفحص جميع أنماط الخلايا. تسجيل خط مخصص يضمن العثور على الخط عندما نقوم لاحقًا بتضمينه في ملف HTML.

## الخطوة 2: تكوين خيارات حفظ HTML لت **تضمين الخطوط في HTML**

السحر يكمن في `HtmlSaveOptions`. ضبط `EmbedFonts = true` يخبر المكتبة بتضمين كل خط مستخدم كقاعدة `@font-face` مشفرة بـ Base64 داخل ملف HTML المُولد.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*لماذا تمكين `EmbedFonts`؟* بدون ذلك، يشير HTML الناتج إلى خطوط النظام، وأي شخص يفتح الملف على جهاز لا يحتوي على تلك الخطوط سيظهر بديلًا. التضمين يضمن الحفاظ على المظهر البصري عبر المتصفحات والأجهزة.

## الخطوة 3: **حفظ المصنف كـ HTML** باستخدام الخيارات المكوَّنة

الآن نكتب الملف أخيرًا. طريقة `Save` تأخذ ثلاثة معطيات: مسار الهدف، الصيغة (`SaveFormat.Html`)، والخيارات التي قمنا بتكوينها للتو.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

إذا سارت الأمور بسلاسة، ستحصل على ملف `with-fonts.html` واحد يحتوي على تخطيط الورقة بالكامل *ومع* بيانات الخط المشفرة مباشرة في العلامات.

## النتيجة المتوقعة

افتح `with-fonts.html` في أي متصفح حديث (Chrome، Edge، Firefox). يجب أن ترى:

- نفس قيم الخلايا، الألوان، والحدود كما في ملف Excel الأصلي.
- النص يُعرض بالخط الدقيق الذي استخدمته في Excel، حتى وإن لم يكن الخط مثبتًا على جهازك.
- لا ملفات `.css` أو صور خارجية—كل شيء داخل ملف HTML.

فيما يلي مقتطف صغير من كتلة `<style>` التي قد يولدها البرنامج (تم تقصير سلسلة Base64 للاختصار):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## الخطوة 4: المشكلات الشائعة وكيفية إصلاحها

| المشكلة | لماذا يحدث | الحل |
|------|----------------|-----|
| **فقدان الخط في HTML** | لم يتم تسجيل ملف الخط مع `FontConfigs` قبل الحفظ. | استدعِ `FontConfigs.AddFontFile` *قبل* إنشاء `HtmlSaveOptions`. |
| **حجم ملف HTML كبير** | تضمين العديد من الخطوط الكبيرة قد ي inflate الملف. | قم بتضمين الخطوط التي تحتاجها فقط؛ استخدم `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset` لتضمين الأحرف المستخدمة فقط (متاح في إصدارات Aspose الأحدث). |
| **حروف غير صحيحة (مثل الأحرف الآسيوية)** | الخط لا يحتوي على نطاقات Unicode المطلوبة. | تأكد من أن الخط المصدر يدعم هذه الأحرف، أو قم بتضمين خط احتياطي إضافي. |
| **تباطؤ الأداء مع المصنفات الكبيرة** | تضمين الخطوط يضيف عبء معالجة. | صدّر فقط الورقة النشطة (`ExportActiveWorksheetOnly = true`) أو قسّم المصنف إلى أجزاء أصغر. |

## الخطوة 5: توسيع الحل – تصدير أوراق عمل متعددة

إذا كنت بحاجة إلى **تحويل المصنف إلى HTML** لجميع الأوراق، ما عليك سوى إيقاف `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

ستظهر كل ورقة عمل كـ `<div>` منفصل داخل نفس ملف HTML، مع الحفاظ على الخطوط المضمنة.

## نصيحة احترافية: الجمع مع تخصيص CSS

أحيانًا تريد تحكمًا أدق في العلامات المُولدة. توفر `HtmlSaveOptions` الخاصية `CssClassPrefix` لتجنب تصادم أسماء الفئات عند دمج تصديرات HTML متعددة:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

الآن كل فئة CSS مُولدة ستبدأ بـ `myExcel_`، مما يسهل تطبيق ورقة الأنماط الخاصة بك لاحقًا.

## ملخص

- **تضمين الخطوط في HTML** عبر ضبط `HtmlSaveOptions.EmbedFonts = true`.
- استخدم **حفظ المصنف كـ HTML** (`wb.Save(..., SaveFormat.Html, ...)`) لإنتاج ملف واحد مكتمل.
- هذه الطريقة **تحول المصنف إلى HTML** مع الحفاظ على كل التفاصيل البصرية، وتجيب على السؤال الشائع **كيفية تصدير Excel إلى HTML** بجودة عالية.
- سجِّل الخطوط المخصصة باستخدام `FontConfigs.AddFontFile` لضمان توفرها للتضمين.
- عدِّل الخيارات مثل `ExportImagesAsBase64` و `ExportActiveWorksheetOnly` لتتناسب مع احتياجات مشروعك.

## ما التالي؟

- جرّب التصدير إلى **MHTML** (`SaveFormat.Mhtml`) للحصول على حزمة أكثر قابلية للنقل.
- استكشف **تحويل PDF** (`SaveFormat.Pdf`) إذا كنت تحتاج إلى صيغة جاهزة للطباعة.
- دمج تصدير HTML في واجهة برمجة تطبيقات ويب ليتمكن المستخدمون من تنزيل جداول مصممة على الفور.

لا تتردد في التجربة—غيّر الخطوط، غير اختيار الأوراق، أو اجمع بين صيغ تصدير متعددة. مرونة Aspose.Cells تتيح لك تخصيص الناتج لأي سيناريو، من لوحات تقارير آلية إلى مقتطفات HTML جاهزة للبريد الإلكتروني.

برمجة سعيدة، ولتظل صفحات HTML دائمًا مطابقة تمامًا لورقة Excel الأصلية!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [تعيين الخط الافتراضي في تحويل Excel إلى HTML باستخدام Aspose.Cells for .NET | دليل عمليات المصنف](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [كيفية تصدير Excel إلى HTML مع خطوط الشبكة باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}