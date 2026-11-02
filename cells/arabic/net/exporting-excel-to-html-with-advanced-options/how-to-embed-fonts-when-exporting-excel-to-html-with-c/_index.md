---
category: general
date: 2026-10-10
description: تعلم كيفية تضمين الخطوط أثناء تصدير Excel إلى HTML باستخدام C#. يغطي
  هذا الدليل تصدير Excel إلى HTML، تحويل Excel إلى HTML، وكيفية حفظ Excel مع الخطوط
  المضمنة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel html
- convert excel html
- how to save excel
- embed fonts html
language: ar
lastmod: 2026-10-10
og_description: كيفية تضمين الخطوط أثناء تصدير Excel إلى HTML في C#. اتبع هذا الدرس
  الكامل لتصدير Excel إلى HTML، وتحويل Excel إلى HTML، وتعلم كيفية حفظ Excel مع الخطوط
  المضمنة.
og_image_alt: Screenshot showing exported HTML file that demonstrates how to embed
  fonts from Excel
og_title: كيفية تضمين الخطوط عند تصدير Excel إلى HTML – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to embed fonts while exporting Excel to HTML in C#. This
    guide covers export excel html, convert excel html, and how to save Excel with
    embedded fonts.
  headline: How to embed fonts when exporting Excel to HTML with C#
  type: TechArticle
tags:
- Excel
- HTML export
- Font embedding
- C#
title: كيفية تضمين الخطوط عند تصدير Excel إلى HTML باستخدام C#
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط عند تصدير Excel إلى HTML باستخدام C#

إذا كنت بحاجة إلى **how to embed fonts** في ملف HTML تم إنشاؤه من مصنف Excel، فإن هذا البرنامج التعليمي يوضح الخطوات الدقيقة. غالبًا ما يزيل تصدير Excel إلى HTML الخطوط المخصصة، مما يفسد الدقة البصرية للجدول الأصلي. من خلال تكوين الخيارات الصحيحة يمكنك الحفاظ على كل نوع خط مباشرةً في مخرجات HTML.

في هذا الدليل ستتعلم كيفية **export excel html**، **convert excel html**، و**how to save Excel** مع تضمين الخطوط، باستخدام مكتبة Aspose.Cells لـ .NET. الحل يعمل مع .NET 6+ ويتطلب فقط بضع أسطر من كود C#.

## ما ستحقه

- برنامج C# كامل وقابل للتنفيذ يقوم بتحميل ملف `.xlsx` موجود.
- مخرجات HTML حيث يتم تضمين جميع الخطوط المستخدمة كقواعد `@font-face` مشفرة بـ Base64.
- ثقة بأن HTML المُصدّر يبدو مطابقًا تمامًا لملف المصنف الأصلي على أي متصفح.

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6 SDK أو أحدث | يوفر بيئة التشغيل لمشروع C#. |
| Visual Studio 2022 (أو أي بيئة تطوير متكاملة) | يسهل إنشاء وتشغيل تطبيق الكونسول. |
| Aspose.Cells لـ .NET (حزمة NuGet `Aspose.Cells`) | توفر الفئة `HtmlSaveOptions` وميزة `EmbedFonts`. |
| ملف Excel (`sample.xlsx`) يستخدم خطًا مخصصًا (مثل *Calibri* أو خط TrueType تم تنزيله) | يوضح تأثير تضمين الخطوط. |

> **نصيحة احترافية:** إذا كنت تعمل خلف بروكسي مؤسسي، قم بتكوين NuGet لاستخدام البروكسي قبل تثبيت الحزمة.

## الخطوة 1: تثبيت Aspose.Cells

افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.Cells
```

يضيف الأمر أحدث نسخة مستقرة من Aspose.Cells إلى مشروعك، مما يجعل الفئات `Workbook` و `HtmlSaveOptions` متاحة.

## الخطوة 2: تحميل مصنف Excel

أنشئ تطبيق كونسول جديد (`dotnet new console`) وأضف الشيفرة التالية إلى `Program.cs`:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing workbook. Replace the path with your actual file location.
        Workbook wb = new Workbook("sample.xlsx");
        // Continue with HTML export...
    }
}
```

**لماذا هذه الخطوة مهمة:**  
تحميل المصنف يمنحك الوصول إلى أوراق العمل، الأنماط، والخطوط المخصصة المشار إليها داخل الملف. بدون وجود كائن `Workbook` محمَّل لا يمكنك تكوين خيارات التصدير.

## الخطوة 3: تكوين خيارات حفظ HTML لتضمين الخطوط

تتحكم الفئة `HtmlSaveOptions` في كل جانب من جوانب تصدير HTML. ضبط `EmbedFonts = true` يخبر Aspose.Cells بتضمين كل خط مستخدم في المصنف مباشرةً في ملف HTML المُولد.

```csharp
// Configure HTML save options to embed fonts
HtmlSaveOptions opts = new HtmlSaveOptions
{
    // When true, the exporter creates @font-face rules with Base64 data.
    EmbedFonts = true,

    // Optional: keep the original folder structure for images.
    ExportImagesAsBase64 = true,

    // Optional: generate a single HTML file (no external CSS folder).
    ExportActiveWorksheetOnly = false
};
```

**شرح:**  
- `EmbedFonts` هو العلامة الأساسية التي تحقق متطلبات **how to embed fonts**.  
- `ExportImagesAsBase64` يضمن أن تصبح أي صور أيضًا جزءًا من ملف HTML الواحد، مما يبسط النشر.  
- `ExportActiveWorksheetOnly` مضبوطة على `false` تضمن تضمين جميع أوراق العمل، وهو مفيد عندما يمتد المصنف على عدة أوراق.

## الخطوة 4: حفظ المصنف كملف HTML مع خطوط مضمَّنة

الآن استدعِ طريقة `Save`، مع تمرير مسار الإخراج المطلوب والخيارات التي قمت بتكوينها للتو:

```csharp
// Save the workbook as an HTML file with embedded fonts
wb.Save("Embedded.html", opts);
```

يحتوي ملف `Embedded.html` الناتج على:

- علامات HTML قياسية لبيانات الجدول.
- كتلة أو أكثر `<style>` تحتوي على قواعد `@font-face` التي تُضمّن الخطوط المخصصة كسلاسل Base64.
- جميع الصور مشفرة مباشرةً في HTML (إن وجدت).

## الخطوة 5: التحقق من أن الخطوط مضمَّنة فعليًا

افتح `Embedded.html` في متصفح (Chrome, Edge, Firefox). يجب أن تُظهر الصفحة تمامًا كما هو المصنف الأصلي في Excel، حتى إذا لم يكن الجهاز المستهدف يحتوي على الخطوط المخصصة مثبتة.

للتحقق المزدوج من التضمين:

1. افتح مصدر الصفحة (`Ctrl+U` في معظم المتصفحات).  
2. ابحث عن `@font-face`. سترى كتلة مشابهة لـ:

```css
@font-face {
    font-family: 'Calibri';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1Mv...') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

إذا كان attribute `src` يحتوي على عنوان URL من نوع `data:`، فإن الخط مضمَّن بنجاح.

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل المقترح |
|-----------|----------------------|
| **مصنف كبير يحتوي على العديد من الخطوط المخصصة** | زيادة `MaxFontEmbeddingSize` (إن كان متاحًا) أو تقسيم التصدير إلى ملفات HTML متعددة لتجنب تجاوز حدود حجم المتصفح. |
| **تحتاج فقط إلى ورقة عمل واحدة** | ضبط `opts.ExportActiveWorksheetOnly = true` وتفعيل الورقة المطلوبة قبل الحفظ (`wb.Worksheets[0].Activate();`). |
| **تضمين الخطوط غير مسموح به وفقًا لسياسة الشركة** | ضبط `opts.EmbedFonts = false` والاعتماد على الخطوط الآمنة للويب أو توفير ملفات الخط بجانب ملف HTML. |
| **استهداف متصفحات قديمة لا تدعم خطوط Base64** | استخدام `opts.FontEmbeddingMode = FontEmbeddingMode.FontFile;` (إذا كان إصدار المكتبة يدعم ذلك) لإنشاء ملفات `.ttf` منفصلة والإشارة إليها عبر عناوين URL عادية. |

## مثال كامل وقابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في `Program.cs`. يتضمن جميع توجيهات `using` الضرورية ومعالجة الأخطاء لسكريبت جاهز للإنتاج.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the workbook (replace with your file path)
            Workbook wb = new Workbook("sample.xlsx");

            // 2️⃣ Configure HTML export options to embed fonts
            HtmlSaveOptions opts = new HtmlSaveOptions
            {
                EmbedFonts = true,               // ✅ Core requirement: how to embed fonts
                ExportImagesAsBase64 = true,     // Keep everything in one file
                ExportActiveWorksheetOnly = false
            };

            // 3️⃣ Save as HTML with embedded fonts
            string outputPath = "Embedded.html";
            wb.Save(outputPath, opts);

            Console.WriteLine($"HTML file with embedded fonts saved to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**المخرجات المتوقعة:**  
تشغيل البرنامج يطبع سطر التأكيد وينشئ `Embedded.html`. فتح الملف في أي متصفح حديث يظهر الجدول مع جميع الخطوط الأصلية محفوظة، محققًا هدف **how to embed fonts**.

## الخلاصة

أنت الآن تعرف **كيفية تضمين الخطوط** أثناء تنفيذ عملية **export excel html**، وكيفية **convert excel html** دون فقدان الخطوط، والخطوات الدقيقة **how to save excel** كملف HTML مع خطوط مضمَّنة. باستخدام `HtmlSaveOptions.EmbedFonts = true`، يصبح HTML المُولد مستقلًا، قابلًا للنقل، ومطابقًا بصريًا للمصنف الأصلي.

### ما التالي؟

- استكشف خصائص `HtmlSaveOptions` للتحكم في CSS، معالجة الصور، واختيار أوراق العمل.  
- اجمع هذه التقنية مع الأتمتة على جانب الخادم لإنشاء تقارير HTML في الوقت الفعلي.  
- اطلع على **embed fonts html** لتنسيقات مستندات أخرى (مثل PDF) باستخدام واجهات برمجة تطبيقات Aspose المماثلة.

لا تتردد في تجربة خطوط مختلفة، أحجام مصنفات مختلفة، وبيئات المتصفحات. إذا واجهت أي مشاكل، راجع جدول الحالات الخاصة أعلاه أو استشر وثائق Aspose.Cells لسيناريوهات متقدمة لتضمين الخطوط. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير Excel إلى HTML – دليل برمجة كامل](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-complete-programming-guide/)
- [كيفية تصدير Excel إلى HTML – دليل خطوة بخطوة](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [كيفية تضمين الخطوط عند تحويل Excel إلى PDF – دليل كامل](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}