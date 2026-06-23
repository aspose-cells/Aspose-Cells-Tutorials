---
category: general
date: 2026-06-17
description: تضمين الخطوط في XPS باستخدام C# و Aspose.PDF. تعلم XpsSaveOptions وتضمين
  الخطوط وتصدير XPS في دقائق.
draft: false
keywords:
- embed fonts in xps
- XpsSaveOptions
- Aspose.PDF for .NET
- C# XPS export
- font embedding
language: ar
og_description: تضمين الخطوط في XPS باستخدام Aspose.PDF لـ .NET. يوضح هذا البرنامج
  التعليمي كيفية تكوين XpsSaveOptions، وتضمين الخطوط، وإنشاء ملفات XPS بلغة C#.
og_title: دمج الخطوط في XPS باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in XPS using C# and Aspose.PDF. Learn XpsSaveOptions, font
    embedding, and XPS export in minutes.
  headline: Embed Fonts in XPS with C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- XPS
- font embedding
- Aspose.PDF
title: تضمين الخطوط في XPS باستخدام C# – دليل برمجي كامل
url: /ar/net/xps-and-pdf-operations/embed-fonts-in-xps-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إدراج الخطوط في XPS باستخدام C# – دليل برمجة كامل

هل احتجت يومًا إلى **إدراج الخطوط في XPS** لكن لم تكن متأكدًا من أي علامات API يجب تفعيلها؟ لست وحدك—العديد من المطورين يواجهون هذا التحدي عند تصدير ملفات PDF أو مستندات أخرى إلى صيغة XPS. الخبر السار؟ ببضع أسطر من C# والخيارات الصحيحة، يمكنك حزم تلك الخطوط داخل ملف XPS وضمان عرض متسق في أي مكان.

في هذا الدليل سنستعرض الخطوات الدقيقة لتكوين **XpsSaveOptions**، تمكين **إدراج الخطوط**، وحفظ المستند كـ XPS باستخدام **Aspose.PDF for .NET**. في النهاية ستحصل على مقتطف جاهز للتنفيذ يمكنك وضعه في أي مشروع .NET.

## ما ستتعلمه

- لماذا يُعد إدراج الخطوط في XPS مهمًا للحفاظ على الدقة عبر المنصات.  
- كيفية إعداد `XpsSaveOptions` وتفعيل علم `EmbedFonts`.  
- الكود الكامل بلغة C# اللازم لإنشاء ملف XPS مع خطوط مدمجة.  
- المشكلات الشائعة (خطوط مقيدة بالترخيص، حروف مفقودة) وكيفية تجنبها.  

**المتطلبات المسبقة**: .NET 6+ (أو .NET Framework 4.6+)، مرجع إلى حزمة NuGet الخاصة بـ Aspose.PDF for .NET، وفهم أساسي للغة C#. لا تحتاج إلى أدوات خارجية أخرى.

---

## الخطوة 1: تثبيت Aspose.PDF for .NET

قبل كتابة أي كود، تأكد من توفر مكتبة Aspose.PDF في مشروعك.

```bash
dotnet add package Aspose.PDF --version 23.12
```

> **نصيحة محترف:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا الاستفادة من واجهة مدير الحزم NuGet—فقط ابحث عن “Aspose.PDF”.

## الخطوة 2: إنشاء مستند PDF بسيط

سنبدأ بملف PDF صغير يحتوي على سطر نص واحد. سيتم حفظ هذا المستند لاحقًا كـ XPS مع إدراج الخطوط.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a new PDF document
Document pdfDoc = new Document();

// Add a page
Page page = pdfDoc.Pages.Add();

// Add a TextFragment with a custom font (e.g., Arial)
TextFragment tf = new TextFragment("Hello, XPS world!")
{
    // Use a TrueType font that you know is installed
    TextState = { Font = FontRepository.FindFont("Arial") }
};
page.Paragraphs.Add(tf);
```

*لماذا هذا مهم*: استخدام خط TrueType معروف يضمن توفر الحروف للدمج. إذا اخترت خطًا غير مثبت على الجهاز، سيعود Aspose إلى الخط الافتراضي، وقد لا يحتوي XPS على النمط المطلوب.

## الخطوة 3: تكوين XpsSaveOptions لإدراج الخطوط

هنا يكمن جوهر الدرس—كائن `XpsSaveOptions`. ضبط `EmbedFonts = true` يخبر Aspose بحزم كل خط مُشار إليه مباشرة داخل حزمة XPS.

```csharp
using Aspose.Pdf.XpsConversion;

// Configure XPS save options
XpsSaveOptions saveOptions = new XpsSaveOptions
{
    // This flag performs the actual font embedding
    EmbedFonts = true,

    // Optional: compress the XPS for smaller size
    Compression = CompressionType.Zip,

    // Optional: preserve the original PDF's layout
    PreserveFormFields = true
};
```

> **لماذا تمكين الضغط؟** ملف XPS هو في الأساس أرشيف ZIP يحتوي على XML والموارد. تشغيل `Compression` يمكن أن يقلص حجم الملف النهائي حتى 30 % دون التأثير على إدراج الخطوط.

## الخطوة 4: حفظ المستند كـ XPS مع خطوط مدمجة

الآن نجمع كل شيء—نحفظ PDF كـ XPS باستخدام الخيارات التي عرّفناها للتو.

```csharp
// Define the output path (make sure the directory exists)
string outputPath = Path.Combine(Environment.CurrentDirectory, "EmbeddedFontExample.xps");

// Save the PDF as XPS, embedding all fonts
pdfDoc.Save(outputPath, SaveFormat.Xps, saveOptions);

Console.WriteLine($"XPS file saved to: {outputPath}");
```

عند فتح `EmbeddedFontExample.xps` في Windows XPS Viewer، يجب أن ترى النص معروضًا تمامًا كما ظهر في PDF، بغض النظر عما إذا كان نظام المشاهد يحتوي على خط Arial أم لا.

## الخطوة 5: التحقق من إدراج الخطوط (اختياري لكن موصى به)

إذا رغبت في التأكد من أن الخطوط مدمجة فعلاً، يمكنك فك ضغط ملف XPS (إنه مجرد أرشيف ZIP) وتفقد مجلد `Resources/Fonts`.

```powershell
# PowerShell one‑liner to list embedded fonts
Expand-Archive -Path .\EmbeddedFontExample.xps -DestinationPath .\tempXps
Get-ChildItem .\tempXps\Resources\Fonts
```

يجب أن ترى ملفات `.ttf` أو `.otf` تتطابق مع الخطوط التي استخدمتها. إذا كان المجلد فارغًا، راجع `saveOptions.EmbedFonts` وتأكد من أن الخط المصدر غير مقيد بالترخيص.

## حالات الحافة الشائعة وكيفية التعامل معها

| الحالة | ما يحدث | الحل |
|-----------|--------------|-----|
| **الخط مرخص بـ “no‑embed”** | يقوم Aspose باستبدال الخط صامتًا، مما يؤدي إلى حروف مفقودة. | استخدم خطًا آخر أو احصل على ترخيص يسمح بالإدراج. |
| **ملف الخط المخصص غير مثبت** | `FontRepository.FindFont` يعيد `null` → استثناء وقت التشغيل. | حمّل الخط يدويًا: `FontRepository.AddFont("path/to/font.ttf");` قبل إنشاء `TextFragment`. |
| **ملفات XPS الكبيرة** | إدراج العديد من الخطوط قد يثقل حجم الملف. | فعّل `Compression = CompressionType.Zip` أو قلّص الخطوط عبر `saveOptions.SubsetFonts = true`. |
| **عدم عرض الأحرف Unicode** | حروف مفقودة لبعض السكريبتات. | تأكد من أن الخط المختار يدعم النطاق Unicode المطلوب، أو أدرج خطوطًا احتياطية متعددة. |

---

## مثال كامل جاهز للتنفيذ (انسخه‑ألصقه)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.XpsConversion;

class EmbedFontsInXpsDemo
{
    static void Main()
    {
        // 1️⃣ Create a simple PDF with custom text
        Document pdfDoc = new Document();
        Page page = pdfDoc.Pages.Add();

        // Load a TrueType font (Arial) – replace with your font if needed
        FontRepository.AddFont(@"C:\Windows\Fonts\arial.ttf");
        TextFragment tf = new TextFragment("Hello, XPS world!")
        {
            TextState = { Font = FontRepository.FindFont("Arial") }
        };
        page.Paragraphs.Add(tf);

        // 2️⃣ Set up XpsSaveOptions to embed fonts
        XpsSaveOptions saveOptions = new XpsSaveOptions
        {
            EmbedFonts = true,
            Compression = CompressionType.Zip,
            PreserveFormFields = true
        };

        // 3️⃣ Save as XPS
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "EmbeddedFontExample.xps");

        pdfDoc.Save(outputPath, SaveFormat.Xps, saveOptions);

        Console.WriteLine($"✅ XPS saved with embedded fonts at: {outputPath}");
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
✅ XPS saved with embedded fonts at: C:\YourProject\EmbeddedFontExample.xps
```

افتح ملف XPS المُولد؛ يجب أن يظهر النص بنفس النمط، حتى على جهاز لا يحتوي على Arial.

---

## الخلاصة

لقد استعرضنا كيفية **إدراج الخطوط في XPS** باستخدام C# و **Aspose.PDF for .NET**. من خلال تكوين `XpsSaveOptions` مع `EmbedFonts = true`، تضمن أن كل حرف ينتقل مع حزمة XPS، مما يلغي المفاجآت غير السارة على أجهزة العملاء.  

من إعداد المشروع إلى التحقق من الموارد المدمجة، لديك الآن حل كامل وجاهز للنسخ. الآن جرّب استبدال الخطوط، إضافة صور، أو إنشاء مستندات XPS متعددة الصفحات—كل ذلك سيستفيد من استراتيجية الإدراج نفسها.

هل لديك أسئلة حول الترخيص، تقليل حجم الخطوط، أو الأداء؟ اترك تعليقًا، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [Export Excel to XPS with Aspose.Cells .NET](/cells/english/net/workbook-operations/export-excel-xps-aspose-cells-net/)
- [How to Extract Fonts from Excel Files Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [Render Excel to PNG, TIFF, PDF with Custom Fonts in .NET Using Aspose.Cells](/cells/english/net/workbook-operations/render-excel-custom-fonts-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}