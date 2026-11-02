---
category: general
date: 2026-02-28
description: تعلم كيفية تضمين الخطوط في HTML أثناء تصدير Excel إلى HTML باستخدام Aspose.Cells.
  يتضمن حفظ كـ HTML، وتصدير Excel إلى HTML، ونصائح تحويل جدول البيانات إلى HTML.
draft: false
keywords:
- embed fonts html
- export excel html
- save as html
- save excel html
- convert spreadsheet html
language: ar
og_description: تضمين الخطوط في HTML أمر أساسي لتحويل Excel إلى HTML بشكل مثالي. يوضح
  هذا الدليل كيفية تصدير Excel إلى HTML مع تضمين الخطوط باستخدام Aspose.Cells.
og_title: تضمين الخطوط في HTML عند تصدير Excel – دليل C# الكامل
tags:
- Aspose.Cells
- C#
- HTML export
- Excel automation
title: تضمين الخطوط في HTML عند تصدير Excel – دليل C# الكامل
url: /ar/net/exporting-excel-to-html-with-advanced-options/embed-fonts-html-when-exporting-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تضمين خطوط html عند تصدير Excel – دليل C# الكامل

هل احتجت إلى **embed fonts html** أثناء تحويل دفتر عمل Excel إلى صفحة جاهزة للويب؟ لست وحدك—العديد من المطورين يواجهون مشكلة عندما يبدو HTML المُولد جيدًا على جهازهم لكنه يفقد الخطوط الدقيقة على متصفح آخر. الخبر السار؟ ببضع أسطر من C# و Aspose.Cells يمكنك **export excel html** التي تحمل الخطوط الأصلية داخل الملف.

في هذا الدرس سنستعرض كل خطوة لـ **save as html** مع خطوط مضمَّنة، ونناقش لماذا قد ترغب أيضًا في **save excel html** بدون خطوط، ونظهر طريقة سريعة لـ **convert spreadsheet html** للنشرات البريدية. لا أدوات خارجية، فقط كود نقي يمكنك وضعه في أي مشروع .NET.

## ما ستحتاجه

- **Aspose.Cells for .NET** (أحدث إصدار، 2025‑R2 في وقت كتابة المقال).  
- بيئة تطوير .NET (Visual Studio 2022 أو VS Code تعمل).  
- دفتر عمل Excel تريد تصديره (أي ملف *.xlsx* يكفي).  

هذا كل شيء—لا حزم إضافية، لا حيل JavaScript معقدة. بمجرد إضافة المكتبة إلى المشروع، البقية مباشرة.

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

للبدء، أنشئ تطبيق console جديد (أو دمجه في خدمة موجودة). أضف حزمة NuGet:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة محترف:** إذا كنت تستخدم مصدرًا مؤسسيًا، تأكد من ضبط مصدر الحزمة؛ وإلا سيفشل الأمر بصمت.

الآن أدرج مساحة الاسم في أعلى ملف C# الخاص بك:

```csharp
using Aspose.Cells;
using Aspose.Cells.Saving;
```

هذه الـ `using` تمنحك الوصول إلى الفئة `Workbook` و `HtmlSaveOptions` التي سنحتاجها لاحقًا.

## الخطوة 2: تحميل دفتر عمل Excel الخاص بك

يمكنك تحميل دفتر العمل من القرص، أو من تدفق، أو حتى من مصفوفة بايت. إليك أبسط نسخة تقرأ من ملف:

```csharp
// Load the source Excel file
Workbook wb = new Workbook(@"C:\Files\SampleData.xlsx");

// Optional: adjust settings like calculation mode if needed
wb.CalculateFormula();
```

لماذا نستدعي `CalculateFormula()`؟ إذا كان الورق يحتوي على صيغ، ستقوم المكتبة بحساب قيمها قبل التصدير، مما يضمن أن يظهر HTML نفس الأرقام التي تراها في Excel.

## الخطوة 3: تكوين خيارات حفظ HTML لتضمين الخطوط

هذا هو جوهر الدرس. بشكل افتراضي، تُنشئ Aspose.Cells ملف HTML يربط ملفات CSS وخطوط خارجية. لتضمين الخطوط **embed fonts html**، عكّس العلم `EmbedFonts`:

```csharp
// Step 3: Configure HTML save options to embed fonts in the output
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Embeds all used fonts directly into the HTML as Base64‑encoded data URIs
    EmbedFonts = true,

    // Optional: keep the original cell formatting
    ExportActiveWorksheetOnly = true,

    // Optional: generate a single HTML file (no separate CSS folder)
    ExportToSingleFile = true
};
```

تعيين `EmbedFonts = true` يخبر Aspose.Cells بأخذ كل خط مُشار إليه في دفتر العمل، تحويله إلى سلسلة Base64، وإدراجه داخل وسم `<style>`. هذا يضمن أن أي شخص يفتح `Result.html` سيرى نفس الخطوط تمامًا، بغض النظر عما إذا كان الخط مثبتًا على نظامه.

## الخطوة 4: حفظ دفتر العمل كملف HTML

الآن نجمع دفتر العمل مع الخيارات لإنتاج الملف النهائي:

```csharp
// Step 4: Save the document as an HTML file using the configured options
string outputPath = @"C:\Files\Result.html";
wb.Save(outputPath, SaveFormat.Html, htmlOptions);
```

بعد تنفيذ هذا السطر، سيقع `Result.html` جنبًا إلى جنب مع أي موارد داعمة (إذا لم تقم بتمكين `ExportToSingleFile`). افتحه في Chrome أو Edge أو Firefox—ستلاحظ أن الخطوط تبدو مطابقة تمامًا للعرض الأصلي في Excel.

### تحقق سريع

للتأكد من أن الخطوط مضمَّنة فعلاً، افتح ملف HTML في محرر نصوص وابحث عن `@font-face`. يجب أن ترى كتلة مشابهة لـ:

```css
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAA...);
}
```

إذا كان سمة `src` تحتوي على عنوان URL طويل يبدأ بـ `data:`، فقد نجحت العملية.

## الخطوة 5: ماذا لو لا تريد خطوطًا مضمَّنة؟

أحيانًا تفضّل ملف HTML أخف وتقبل أن المتصفح يستخدم الخطوط النظامية كبديل. فقط عكّس العلم:

```csharp
htmlOptions.EmbedFonts = false; // This will generate a normal CSS reference
```

هذا النهج مفيد عندما تُنشئ **export excel html** للوحة تحكم داخلية حيث تتحكم في البيئة، أو عندما تحتاج إلى **convert spreadsheet html** لبريد إلكتروني منخفض النطاق حيث الحجم مهم.

## الخطوة 6: معالجة الحالات الخاصة والمشكلات الشائعة

| الحالة | الحل الموصى به |
|-----------|-----------------|
| **دفاتر عمل كبيرة** ( > 50 MB ) | استخدم `ExportToSingleFile = false` لإبقاء HTML وبيانات الخط منفصلين؛ المتصفحات تتعامل بشكل سيء مع سلاسل Base64 الكبيرة. |
| **الخطوط المخصصة غير مضمَّنة** | تأكد من تثبيت الخط على الجهاز الذي يجري التحويل؛ Aspose.Cells لا يمكنه تضمين الخطوط التي لا يستطيع العثور عليها. |
| **غياب بعض الرموز** | قد تُفقد بعض ميزات OpenType؛ فكر في تحويل الورقة إلى صورة (`SaveFormat.Png`) كحل احتياطي. |
| **القلق بشأن الأداء** | احفظ كائن `HtmlSaveOptions` في الذاكرة إذا كنت تحول ملفات متعددة داخل حلقة؛ تجنّب إنشاءه في كل تكرار. |

## الخطوة 7: مثال كامل يعمل

بجمع كل ما سبق، إليك برنامج مستقل يمكنك نسخه ولصقه وتشغيله:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;

namespace ExcelToHtmlWithEmbeddedFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string sourcePath = @"C:\Files\SampleData.xlsx";
            Workbook wb = new Workbook(sourcePath);
            wb.CalculateFormula(); // Ensure formulas are up‑to‑date

            // 2️⃣ Configure HTML options (embed fonts)
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                ExportActiveWorksheetOnly = true,
                ExportToSingleFile = true,
                // Optional: set a custom CSS class prefix to avoid clashes
                CssClassPrefix = "aspose_"
            };

            // 3️⃣ Save as HTML
            string outputPath = @"C:\Files\Result.html";
            wb.Save(outputPath, SaveFormat.Html, htmlOptions);

            Console.WriteLine($"✅ HTML file with embedded fonts created at: {outputPath}");
        }
    }
}
```

شغّل البرنامج، ثم افتح `Result.html`. يجب أن ترى الورقة معروضة بنفس الخطوط الموجودة في Excel—بدون أحرف مفقودة، دون خطوط بديلة.

---

![embed fonts html example](/images/embed-fonts-html.png){alt="نتيجة embed fonts html تُظهر طباعة دقيقة"}

## الخلاصة

أصبح لديك الآن حل كامل من البداية للنهاية لتضمين **embed fonts html** أثناء تنفيذ عملية **export excel html** باستخدام Aspose.Cells. من خلال تبديل خاصية واحدة يمكنك الانتقال بين ملف HTML ثقيل، مكتمل ذاتيًا، وإصدار أخف يعتمد على خطوط خارجية. هذه المرونة تجعل من السهل **save as html**، **save excel html**، أو حتى **convert spreadsheet html** لمجموعة متنوعة من السيناريوهات—من لوحات التحكم الداخلية إلى النشرات البريدية الجاهزة.

ما الخطوة التالية؟ جرّب تصدير أوراق متعددة إلى صفحة HTML واحدة، استكشف خيارات معالجة الصور المختلفة (`HtmlSaveOptions.ImageFormat`)، أو اجمع ذلك مع تحويل PDF لتقديم صيغ ويب وطباعة معًا. السماء هي الحد، والآن لديك التقنية الأساسية تحت يدك.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي صعوبات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}