---
category: general
date: 2026-03-25
description: تعلم كيفية تضمين الخطوط في HTML عند تصدير Excel إلى HTML. يوضح لك هذا
  الدليل خطوة بخطوة كيفية تضمين الخطوط في HTML وحفظ المصنف كملف HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- how to export excel
- save workbook as html
language: ar
og_description: كيف يتم تضمين الخطوط في HTML عند تصدير Excel؟ اتبع هذا الدليل لتضمين
  الخطوط في HTML، وتصدير Excel إلى HTML، وحفظ المصنف كملف HTML باستخدام Aspose.Cells.
og_title: كيفية تضمين الخطوط في HTML من Excel – دليل كامل
tags:
- Aspose.Cells
- C#
- HTML export
- Font embedding
title: كيفية تضمين الخطوط في HTML من Excel – دليل كامل
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-from-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في HTML من Excel – دليل كامل

هل تساءلت يومًا **عن كيفية تضمين الخطوط** في ملف HTML يتم إنشاؤه من مصنف Excel؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يبدو HTML المُصدَّر جيدًا على جهازهم لكنه يفقد الخطوط الأصلية على جهاز آخر. الخبر السار؟ الحل بسيط جدًا مع Aspose.Cells، ويمكنك تضمين الخطوط مباشرةً داخل مخرجات HTML.

في هذا الدرس سنستعرض الخطوات الدقيقة **لتضمين الخطوط في html**، ونوضح لك **كيفية تصدير Excel إلى html**، وأخيرًا نُظهر لك **كيفية حفظ المصنف كـ html** مع جميع الإعدادات اللازمة. في النهاية ستحصل على ملف HTML جاهز للإدراج يعرض المحتوى تمامًا كما في جدول البيانات الأصلي—بدون حروف مفقودة، ولا خطوط بديلة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework)
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو مرخصة)
- ملف Excel تجريبي (`sample.xlsx`) يستخدم على الأقل خطًا مخصصًا واحدًا
- Visual Studio 2022 أو أي محرر C# تفضله

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells.

## الخطوة 1: إعداد المشروع وتحميل المصنف

أولًا، أنشئ تطبيق console جديد وأضف مرجع Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load an existing Excel workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // We'll configure the export options in the next step
        }
    }
}
```

**Why this matters:** تحميل المصنف هو الأساس. إذا لم يتم تحميل المصنف بشكل صحيح، فلن يكون لأي من إعدادات تضمين الخطوط اللاحقة أي تأثير. أيضًا، لاحظ أن Aspose.Cells يقرأ تلقائيًا معلومات الخط المخزنة في الملف، لذا لا تحتاج إلى تحديد أسماء الخطوط يدويًا.

## الخطوة 2: إنشاء HtmlSaveOptions وتفعيل تضمين الخطوط

الآن نقوم بإنشاء كائن `HtmlSaveOptions` ونفعل علم `EmbedAllFonts`. هذا يخبر Aspose.Cells بتضمين كل خط يُشار إليه في المصنف مباشرةً داخل HTML المُولد.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions();

// Enable embedding of all fonts in the output HTML
htmlSaveOptions.EmbedAllFonts = true;

// Optional: Reduce the size of the generated HTML by using base64 encoding
htmlSaveOptions.ExportEmbeddedImages = true;
```

**Why we enable `EmbedAllFonts`:** عندما تصدر Excel إلى HTML بدون هذا العلم، سيشير HTML إلى الخطوط بالاسم فقط. إذا لم يكن لدى نظام المشاهد تلك الخطوط مثبتة، سيتراجع المتصفح إلى عائلة خطوط عامة، مما يفسد التخطيط. التضمين يضمن أن الأحرف الدقيقة تنتقل مع ملف HTML.

**Pro tip:** إذا كنت تحتاج فقط إلى مجموعة فرعية من الخطوط (مثلاً، تعرف أن المصنف يستخدم فقط *Calibri* و *Arial*)، يمكنك تعيين `htmlSaveOptions.FontsList` إلى مجموعة مخصصة. هذا يمكن أن يقلص حجم الملف النهائي بشكل كبير.

## الخطوة 3: حفظ المصنف كـ HTML مع الخطوط المضمنة

أخيرًا، استدعِ `Save` على كائن `Workbook`، مع تمرير المسار والإعدادات التي قمنا بتكوينها.

```csharp
// Step 3: Save the workbook as an HTML file with embedded fonts
string htmlPath = @"C:\Temp\embedded.html";
workbook.Save(htmlPath, htmlSaveOptions);

Console.WriteLine($"HTML file with embedded fonts saved to: {htmlPath}");
```

هذا كل شيء—ملف `embedded.html` الآن يحتوي على كتل `<style>` مع تعريفات `@font-face` وبيانات الخط المشفرة بصيغة base64. افتحه في أي متصفح حديث وسترى نفس الخطوط تمامًا كما في `sample.xlsx`.

### النتيجة المتوقعة

عند فتح `embedded.html`:

- يظهر الخط المخصص بالضبط كما هو في Excel.
- لا يتم طلب أي ملفات خطوط خارجية (تحقق من علامة Network في أدوات المطور—يجب ألا يُحمَّل شيء).
- قد يكون حجم الصفحة أكبر من تصدير HTML بسيط، لكن الدقة البصرية تكون مثالية.

## تصدير Excel إلى HTML – مثال كامل

لنجمع كل شيء معًا، إليك البرنامج الكامل القابل للتنفيذ:

```csharp
using System;
using Aspose.Cells;

namespace ExcelToHtmlWithFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\Temp\sample.xlsx";
            Workbook workbook = new Workbook(excelPath);
            
            // 2️⃣ Configure HTML export options
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedAllFonts = true,          // ✅ Embed every used font
                ExportEmbeddedImages = true,   // ✅ Include images as base64
                ExportChartImageFormat = ImageFormat.Png,
                ExportImagesAsBase64 = true    // ✅ Keep everything in one file
            };
            
            // 3️⃣ Save as HTML
            string htmlPath = @"C:\Temp\embedded.html";
            workbook.Save(htmlPath, htmlOptions);
            
            Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
        }
    }
}
```

**Why this works:** كائن `HtmlSaveOptions` هو حاوية قوية. بتفعيل `EmbedAllFonts`، تُخبر Aspose.Cells بفحص مجموعة الأنماط في المصنف، سحب ملفات الخط من نظام التشغيل، وتضمينها. علما `ExportEmbeddedImages` و `ExportImagesAsBase64` يحافظان على أن يكون HTML مكتملًا ذاتيًا، وهو أمر مفيد عندما تحتاج لإرسال الملف عبر البريد الإلكتروني أو تخزينه في قاعدة بيانات.

## المشكلات الشائعة عند تضمين الخطوط في HTML

حتى مع الكود الصحيح، قد تواجه بعض العقبات. دعنا نتعامل معها قبل أن تتحول إلى صداع.

| المشكلة | لماذا يحدث | كيفية الإصلاح |
|-------|----------------|------------|
| **فقدان الخط على الخادم** | قد لا يحتوي الخادم الذي يُشغَّل عليه الكود على الخط المخصص المثبت. | قم بتثبيت الخطوط المطلوبة على الخادم أو انسخ ملفات `.ttf/.otf` إلى مجلد معروف واضبط `htmlSaveOptions.FontsLocation` إلى ذلك المسار. |
| **ملف HTML كبير** | تضمين العديد من الخطوط الثقيلة قد يثقل حجم HTML (أحيانًا >5 MB). | استخدم `htmlSaveOptions.FontsList` لتضمين الخطوط الضرورية فقط، أو فكر في تقليل حجم الخطوط باستخدام أداة مثل FontForge قبل التضمين. |
| **قيود الترخيص** | بعض الخطوط التجارية تحظر التضمين. | تحقق من اتفاقية ترخيص الخط (EULA). إذا كان التضمين غير مسموح، استخدم بديلًا ويب‑آمنًا أو حوِّل الورقة إلى PDF بدلاً من ذلك. |
| **توافق المتصفح** | المتصفحات القديمة جدًا (IE 8) قد تتجاهل `@font-face` مع بيانات base64. | قدم قاعدة CSS احتياطية أو قدِّم ملف CSS منفصل للمتصفحات القديمة. |
| **نطاق Unicode غير صحيح** | قد لا يحتوي الخط المضمن على جميع الأحرف المستخدمة (مثل الحروف الآسيوية). | تأكد من أن الخط المصدر يدعم نطاقات Unicode المطلوبة، أو قم بتضمين خط ثانوي يغطي النطاق المفقود. |

## متقدم: تضمين خطوط مختارة فقط

إذا كنت تعرف أن المصنف يستخدم فقط *Calibri* و *Times New Roman*، يمكنك حصر التضمين كما يلي:

```csharp
htmlSaveOptions.FontsList = new string[] { "Calibri", "Times New Roman" };
```

هذا يقلص حجم HTML بشكل كبير مع الحفاظ على المظهر والملمس.

## اختبار المخرجات

بعد توليد `embedded.html`، نفّذ الفحوص السريعة التالية:

1. افتح الملف في Chrome/Edge/Firefox.  
2. افتح أدوات المطور → Network → صَفِّ حسب **font**. يجب ألا ترى أي طلبات خارجية.  
3. افحص كتلة `<style>`؛ ستجد قواعد `@font-face` مع `src: url(data:font/ttf;base64,…)`.  
4. قارن النص المعروض مع عرض Excel الأصلي—التطابق البكسلي يعني أنك نجحت.

## الخلاصة

في هذا الدليل غطينا **كيفية تضمين الخطوط** في HTML عند **تصدير Excel إلى HTML** باستخدام Aspose.Cells. بإنشاء كائن `HtmlSaveOptions`، وضبط `EmbedAllFonts = true`، واستدعاء `Workbook.Save`، ستحصل على ملف HTML ذاتي الاكتمال يعيد بدقة الخطوط الأصلية للجدول. كما استعرضنا المشكلات الشائعة، حيل الأداء، وطريقة سريعة لتضمين الخطوط التي تحتاجها فعلاً.

---

### ما التالي؟

- **تصدير Excel إلى PDF مع خطوط مضمَّنة** – مثالي للمستندات الجاهزة للطباعة.  
- **تحويل عدة أوراق عمل إلى ملف HTML واحد** – تعلّم عن `HtmlSaveOptions.OnePagePerSheet`.  
- **إنشاء HTML ديناميكي في ASP.NET Core** – بث الـ HTML مباشرةً إلى المتصفح دون الحاجة إلى نظام ملفات.

لا تتردد في تجربة الخيارات، اترك تعليقًا إذا واجهت أي صعوبة، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}