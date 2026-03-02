---
category: general
date: 2026-03-01
description: تعلم كيفية تضمين الخطوط في HTML عند تحويل Excel إلى HTML باستخدام Aspose.Cells.
  يوضح هذا الدليل خطوة بخطوة أيضًا كيفية حفظ Excel كملف HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- create html from excel
- save excel as html
language: ar
og_description: كيفية تضمين الخطوط في HTML عند تصدير Excel إلى HTML. اتبع هذا الدليل
  الكامل للحفاظ على الطباعة عبر المتصفحات.
og_title: كيفية تضمين الخطوط في HTML – دليل C# سريع
tags:
- Aspose.Cells
- C#
- HTML export
title: كيفية تضمين الخطوط في HTML – تحويل Excel إلى HTML باستخدام C#
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في HTML – تحويل Excel إلى HTML باستخدام C#

هل تساءلت يومًا **كيف يتم تضمين الخطوط في HTML** بحيث يبدو تحويل Excel إلى HTML مثاليًا من حيث البكسل؟ لست الوحيد. عند تصدير مصنف إلى HTML، السلوك الافتراضي هو الإشارة إلى خطوط النظام، مما قد يسبب كسر التخطيط على الأجهزة التي لا تتوفر فيها تلك الخطوط.  

من خلال تفعيل تضمين الخطوط، تضمن أن الناتج يحافظ على الطباعة الأصلية، بغض النظر عن مكان عرضه. في هذا الدرس سنستعرض الخطوات الدقيقة **لتضمين الخطوط في HTML** باستخدام Aspose.Cells لـ .NET، وسنتطرق أيضًا إلى مهام ذات صلة مثل **تحويل Excel إلى HTML**، **إنشاء HTML من Excel**، و **حفظ Excel كـ HTML**.

## ما ستتعلمه

- لماذا يعتبر تضمين الخطوط مهمًا لتوافق المتصفحات.  
- الكود الدقيق بلغة C# اللازم لتمكين **embed fonts in html** عند حفظ المصنف.  
- كيفية التعامل مع الحالات الخاصة الشائعة مثل ملفات الخط الكبيرة أو قيود الترخيص.  
- خطوات تحقق سريعة للتأكد من أن الخطوط فعلاً مضمّنة.  

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).  
- حزمة NuGet الخاصة بـ Aspose.Cells لـ .NET مثبتة (`Install-Package Aspose.Cells`).  
- فهم أساسي للغة C# وتعامل مع ملفات Excel.  
- وجود خط TrueType/OpenType مخصص واحد على الأقل مستخدم في المصنف.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فعّل “Nullable reference types” لاكتشاف مشكلات null المحتملة مبكرًا.

---

## الخطوة 1: إعداد المشروع وتحميل المصنف

أولاً، أنشئ تطبيق console جديد (أو دمجه في الحل الحالي). ثم أضف مساحة الاسم Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing Excel file that uses custom fonts
        string sourcePath = @"C:\Temp\Report.xlsx";
        Workbook wb = new Workbook(sourcePath);
```

*لماذا هذا مهم:* تحميل المصنف يمنح المكتبة إمكانية الوصول إلى أنماط الخلايا، التي تشمل معلومات الخط التي نرغب في تضمينها لاحقًا.

---

## الخطوة 2: إنشاء **HtmlSaveOptions** وتفعيل تضمين الخطوط

فئة `HtmlSaveOptions` تتحكم في كل جانب من تصدير HTML. ضبط `EmbedFonts = true` يخبر Aspose.Cells بتضمين ملفات الخط المطلوبة مباشرةً في HTML (كروابط بيانات Base64).

```csharp
        // Step 2: Create HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();

        // Enable embedding of fonts in the saved HTML
        htmlOptions.EmbedFonts = true;

        // Optional: Reduce the size of embedded fonts by subsetting
        htmlOptions.SubsetEmbeddedFonts = true;
```

*لماذا نفعّل `SubsetEmbeddedFonts`*: يزيل الأحرف غير المستخدمة، مما يقلص حجم ملف HTML النهائي—مفيد خصوصًا عند التعامل مع عائلات خطوط كبيرة.

---

## الخطوة 3: اختيار مجلد الإخراج وحفظ HTML

الآن حدد أين سيُحفظ ملف HTML. ستقوم Aspose.Cells أيضًا بإنشاء مجلد للملفات الداعمة (الصور، CSS، إلخ).  

```csharp
        // Define output location
        string outputFolder = @"C:\Temp\ExportedHtml";
        string outputFile = System.IO.Path.Combine(outputFolder, "Report.html");

        // Ensure the folder exists
        System.IO.Directory.CreateDirectory(outputFolder);

        // Step 3: Save the workbook as HTML with the configured options
        wb.Save(outputFile, htmlOptions);

        Console.WriteLine($"HTML file with embedded fonts saved to: {outputFile}");
    }
}
```

*ما ستلاحظه:* افتح ملف `Report.html` الناتج في أي متصفح. يجب أن تُعرض الخطوط المخصصة بشكل صحيح حتى وإن لم يكن الخط مثبتًا على الجهاز.

---

## الخطوة 4: التحقق من أن الخطوط مضمّنة فعلاً

طريقة سريعة لتأكيد التضمين هي فحص ملف HTML المُولد. ابحث عن كتل `<style>` التي تحتوي على قواعد `@font-face` مع `src: url(data:font/ttf;base64,…)`.  

```html
/* Example snippet from the output */
@font-face {
    font-family: 'MyCustomFont';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
    font-weight: normal;
    font-style: normal;
}
```

إذا رأيت URI من نوع `data:`، فهذا يعني أن الخط مضمّن. لا ينبغي الإشارة إلى ملفات `.ttf` أو `.woff` خارجية.

---

## الأسئلة الشائعة والحالات الخاصة

| Question | Answer |
|----------|--------|
| **ماذا لو كان المصنف يستخدم خطوطًا مختلفة كثيرة؟** | تضمين جميعها قد يثقل حجم HTML. استخدم `htmlOptions.SubsetEmbeddedFonts = true` للاحتفاظ فقط بالحروف المطلوبة، أو حدّد يدويًا الخطوط التي تريد تضمينها عبر `htmlOptions.FontsToEmbed`. |
| **هل يجب أن أقلق بشأن ترخيص الخطوط؟** | بالتأكيد. تضمين الخط في ملف HTML يُنشئ نسخة تُوزّع مع المحتوى الخاص بك. تأكد من أن لديك الحق في إعادة توزيع الخط (مثل الخطوط المفتوحة المصدر مثل Google Fonts فهي آمنة). |
| **هل سيعمل هذا في المتصفحات القديمة مثل IE9؟** | طريقة URI المشفر Base64 مدعومة حتى IE8، لكن هناك حد للحجم (~32 KB). بالنسبة للخطوط الكبيرة جدًا، فكر في الرجوع إلى ملفات خطوط خارجية وتقديمها عبر HTTP. |
| **هل يمكنني تضمين الخطوط عند تحويل Excel إلى PDF بدلاً من HTML؟** | نعم—Aspose.Cells يدعم أيضًا `PdfSaveOptions.EmbedStandardFonts` و `PdfSaveOptions.FontEmbeddingMode`. الفكرة نفسها، فقط API مختلف. |
| **ماذا لو احتجت إلى **إنشاء HTML من Excel** على خادم بدون واجهة مستخدم؟** | نفس الكود يعمل في ASP.NET Core، Azure Functions، أو أي بيئة بدون واجهة—فقط تأكد من أن العملية لديها صلاحية قراءة ملفات الخطوط. |

---

## نصائح الأداء

1. **قم بتخزين HTML مؤقتًا** إذا كنت تصدر نفس المصنف بشكل متكرر؛ خطوة التضمين قد تكون مستهلكة للمعالج.  
2. **ضغط مجلد الإخراج** (قم بضغطه بصيغة zip) قبل إرساله عبر الشبكة؛ الخطوط المضمّنة مُشفّرة بالفعل بـ Base64، لذا سيقلل الضغط بعض الكيلوبايت.  
3. **تجنب تضمين خطوط النظام** (Arial, Times New Roman) ما لم تكن بحاجة إلى نسخة مخصصة؛ المتصفحات لديها هذه الخطوط بالفعل.  

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using Aspose.Cells;

class EmbedFontsDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook (your Excel file must contain custom fonts)
        string excelPath = @"C:\Temp\Sample.xlsx";
        Workbook workbook = new Workbook(excelPath);

        // 2️⃣ Prepare HTML options with font embedding enabled
        HtmlSaveOptions options = new HtmlSaveOptions
        {
            EmbedFonts = true,               // ✅ This is the key line for embedding fonts
            SubsetEmbeddedFonts = true,      // ✅ Reduces file size by keeping only used glyphs
            ExportActiveWorksheetOnly = true // Optional: export just the active sheet
        };

        // 3️⃣ Define where the HTML will be saved
        string outputDir = @"C:\Temp\HtmlExport";
        System.IO.Directory.CreateDirectory(outputDir);
        string htmlPath = System.IO.Path.Combine(outputDir, "Sample.html");

        // 4️⃣ Save the workbook as HTML
        workbook.Save(htmlPath, options);

        Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
    }
}
```

تشغيل هذا البرنامج ينتج ملف `Sample.html` الذي **embed fonts in html** ويمكن فتحه على أي جهاز دون فقدان المظهر الأصلي.

---

## الخلاصة

لقد غطينا **كيفية تضمين الخطوط في HTML** عندما **تحول Excel إلى HTML**، مما يضمن أن الدقة البصرية لمصنفك تبقى محفوظة خلال الانتقال إلى الويب. من خلال تفعيل `HtmlSaveOptions.EmbedFonts` (وباختياري `SubsetEmbeddedFonts`) ستحصل على ملف HTML مستقل يعمل عبر المتصفحات، حتى على الأجهزة التي لا تتوفر فيها الخطوط الأصلية.  

بعد ذلك، قد تستكشف **إنشاء HTML من Excel** لأوراق عمل متعددة، أو تغوص في **حفظ Excel كـ HTML** مع سمات CSS مخصصة. كلا السيناريوهين يستخدمان نفس كائن `HtmlSaveOptions`—فقط عدّل الخصائص مثل `ExportActiveWorksheetOnly` أو `CssStyleSheetType`.  

جرّبه، عدّل الخيارات، ودع الخطوط المضمّنة تقوم بالعمل الشاق. إذا واجهت أي مشاكل، اترك تعليقًا—برمجة سعيدة!  

![مثال على كيفية تضمين الخطوط في HTML](https://example.com/images/embed-fonts.png "كيفية تضمين الخطوط في HTML")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}