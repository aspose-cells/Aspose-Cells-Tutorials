---
category: general
date: 2026-02-09
description: تعلم كيفية تضمين الخطوط في HTML أثناء تصدير Excel إلى HTML باستخدام Aspose.Cells.
  يغطي هذا الدليل خطوة بخطوة أيضًا تحويل Excel إلى HTML وكيفية تصدير Excel مع الخطوط
  المضمنة.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- convert excel to html
- how to export excel
language: ar
og_description: كيفية تضمين الخطوط في HTML عند تصدير Excel. اتبع هذا الدليل الكامل
  لتحويل Excel إلى HTML مع الخطوط المضمنة باستخدام Aspose.Cells.
og_title: كيفية تضمين الخطوط في HTML – دليل تصدير Excel إلى HTML
tags:
- Aspose.Cells
- C#
- Excel
- HTML
title: كيفية تضمين الخطوط في HTML عند تصدير Excel – دليل كامل
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-exporting-excel-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في HTML عند تصدير Excel – دليل كامل

هل تساءلت يومًا **كيفية تضمين الخطوط في HTML** أثناء تحويل مصنف Excel إلى صفحة جاهزة للويب؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يبدو HTML المُولد جيدًا على أجهزتهم لكنه يُظهر خطوطًا بديلة عامة في المتصفح. الخبر السار؟ ببضع أسطر من C# وخيارات الحفظ المناسبة، يمكنك شحن الخطوط الدقيقة التي صممتها في Excel.

في هذا البرنامج التعليمي سنستعرض تصدير ملف Excel إلى HTML **مع خطوط مضمَّنة**، باستخدام Aspose.Cells for .NET. على طول الطريق سنتطرق أيضًا إلى أساسيات *export excel to html*، ونُظهر لك كيفية *convert excel to html* في سيناريوهات مختلفة، ونجيب على الأسئلة المتكررة حول “**how to export excel**” التي تظهر في المنتديات.

## ما ستستفيده

- تطبيق C# كونسول يعمل بالكامل يحفظ مصنف `.xlsx` كملف `embedded.html`.
- شرح لماذا يعتبر تضمين الخطوط مهمًا للحفاظ على التناسق بين المتصفحات.
- نصائح للتعامل مع تراخيص الخطوط، المصنفات الكبيرة، والأداء.
- إرشادات سريعة لطرق بديلة لـ *export excel to html* إذا لم تستخدم Aspose.Cells.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).
- Aspose.Cells for .NET مثبت عبر NuGet (`Install-Package Aspose.Cells`).
- فهم أساسي للغة C# ونموذج كائنات Excel.
- خط TrueType (`.ttf`) أو OpenType (`.otf`) لديك الحق في تضمينه.

لا إعدادات معقدة، لا COM interop، فقط بعض حزم NuGet ومحرر نصوص.

---

## كيفية تضمين الخطوط في HTML – الخطوة 1: إعداد المصنف

قبل أن نخبر Aspose.Cells بتضمين الخطوط، نحتاج إلى مصنف يستخدم فعليًا خطًا مخصصًا. لننشئ مصنفًا صغيرًا في الذاكرة، نطبّق خطًا غير نظامي على خلية، ثم نحفظه.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;   // Needed for HtmlSaveOptions

// Step 1: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

// Step 2: Insert some text and apply a custom font (e.g., "Comic Sans MS")
Style style = workbook.CreateStyle();
style.Font.Name = "Comic Sans MS";   // This font is usually not available on all browsers
style.Font.Size = 14;
style.Font.IsBold = true;

// Apply the style to cell A1
Cell cell = sheet.Cells["A1"];
cell.PutValue("Hello, embedded fonts!");
cell.SetStyle(style);

// Save the workbook as an intermediate .xlsx (optional, just for inspection)
workbook.Save("sample.xlsx");
```

**لماذا هذا مهم:** إذا لم يُشر المصنف إلى خط مخصص، لن يكون هناك شيء لتقوم Aspose.Cells بتضمينه. من خلال تعيين `style.Font.Name` صراحةً، نجبر المصدِّر على البحث عن ملف الخط على النظام وإدراجه في ناتج HTML.

> **نصيحة احترافية:** اختبر دائمًا بخط غير موجود على الأجهزة المستهدفة. الخطوط النظامية مثل Arial لن تُظهر ميزة التضمين.

## كيفية تضمين الخطوط في HTML – الخطوة 2: تكوين خيارات حفظ HTML

الآن يأتي السطر السحري الذي يجيب على السؤال الأساسي: *how to embed fonts in HTML*.

```csharp
// Step 3: Create HtmlSaveOptions and enable font embedding
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Setting this flag tells Aspose.Cells to embed all referenced fonts as base‑64 data URIs
    EmbedFonts = true,

    // Optional: Reduce file size by embedding only the characters actually used
    EmbedFontSubset = true,

    // Optional: Choose a folder for external resources (images, CSS)
    ExportImagesAsBase64 = true
};
```

- `EmbedFonts = true` يقوم بالعمل الرئيسي؛ فهو يمسح المصنف بحثًا عن أي مراجع للخطوط، يحدد ملفات `.ttf`/`.otf` المقابلة، ويحقنها مباشرةً في كتلة `<style>` التي يُنشئها HTML.
- `EmbedFontSubset = true` يُحسّن الأداء—فقط الأحرف التي تُستخدم فعليًا تُضمَّن، مما يبقي HTML النهائي خفيفًا.
- `ExportImagesAsBase64` مفيد عندما يكون لديك مخططات أو صور؛ كل شيء يُدمج في ملف واحد، وهو مثالي للبريد الإلكتروني أو العروض السريعة.

## كيفية تضمين الخطوط في HTML – الخطوة 3: حفظ المصنف

أخيرًا، نستدعي `Save` مع الخيارات التي ضبطناها للتو.

```csharp
// Step 4: Export the workbook to HTML with embedded fonts
string outputPath = "embedded.html";
workbook.Save(outputPath, htmlOptions);

Console.WriteLine($"Workbook exported with embedded fonts to: {outputPath}");
```

بعد انتهاء التنفيذ، افتح `embedded.html` في أي متصفح حديث. يجب أن ترى النص يُعرض بـ *Comic Sans MS* حتى وإن لم يكن الخط مثبتًا محليًا. المتصفح يقرأ كتلة `<style>` التي تحتوي على قاعدة `@font-face` مع حمولة `data:font/ttf;base64,...`—تمامًا ما أردنا.

![مخرجات HTML مع الخطوط المضمنة](embed-fonts-html.png "لقطة شاشة توضح كيفية تضمين الخطوط في HTML")

*نص بديل للصورة:* **كيفية تضمين الخطوط في HTML** – لقطة شاشة للصفحة المُولدة مع تطبيق الخط المخصص.

---

## تصدير Excel إلى HTML – طرق بديلة

إذا لم تكن مقيدًا بـ Aspose.Cells، فهناك طرق أخرى لـ *export excel to html*:

| المكتبة / الأداة | دعم تضمين الخطوط | ملاحظة سريعة |
|----------------|-----------------------|------------|
| **ClosedXML** | لا يدعم تضمين الخطوط مدمجًا | يولد HTML عادي؛ يجب عليك إضافة `@font-face` يدويًا. |
| **EPPlus**    | لا يدعم تضمين الخطوط | جيد للجداول البيانية، لكنه يفقد التنسيق. |
| **Office Interop** | يمكنه تضمين الخطوط عبر `SaveAs` مع `xlHtmlStatic` | يتطلب تثبيت Excel على الخادم—عادةً غير مستحسن. |
| **LibreOffice CLI** | يمكنه تضمين الخطوط باستخدام علامة `--embed-fonts` | يعمل عبر الأنظمة لكن يضيف تبعية ثقيلة. |

عندما تحتاج إلى حل موثوق من جانب الخادم دون تثبيت Office، يبقى Aspose.Cells هو المسار الأكثر بساطة لـ *convert excel to html* مع خطوط مضمَّنة.

## كيفية تصدير Excel – المشكلات الشائعة وكيفية حلها

1. **ملفات الخطوط مفقودة** – إذا لم يكن الخط المستهدف موجودًا على الجهاز الذي يشغّل الكود، سيتخطى Aspose.Cells التضمين صامتًا، ويعود HTML إلى خط عام.  
   *الحل:* ثبّت الخط على الخادم أو انسخ ملفات `.ttf`/`.otf` بجوار ملف التنفيذ واضبط `FontSources` يدويًا:

   ```csharp
   FontSources.AddFolder(@"C:\MyFonts");
   ```

2. **قيود الترخيص** – بعض الخطوط التجارية تحظر التضمين.  
   *الحل:* راجع اتفاقية ترخيص الخط (EULA). إذا كان التضمين ممنوعًا، اختر خطًا آخر أو استضف ملف الخط بنفسك مع الترخيص المناسب.

3. **مصنفات كبيرة** – تضمين العديد من الخطوط قد يضاعف حجم HTML.  
   *الحل:* استخدم `EmbedFontSubset = true` (كما هو موضح أعلاه) أو قلل المصنف إلى الأوراق التي تحتاجها فقط قبل التصدير.

4. **توافق المتصفحات** – المتصفحات القديمة (IE 8 وما أدنى) لا تفهم `@font-face` المشفر بـ base‑64.  
   *الحل:* قدّم قاعدة CSS احتياطية تشير إلى نسخة `.woff` من الخط يمكن الوصول إليها عبر الويب.

---

## تحويل Excel إلى HTML – التحقق من النتيجة

بعد تشغيل العينة، افتح `embedded.html` وابحث عن كتلة `<style>` تبدأ هكذا:

```html
<style type="text/css">
@font-face {
    font-family: 'Comic Sans MS';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1MvMg8S...') format('truetype');
}
...
</style>
```

إذا رأيت عنوان URL من نوع `data:`، فقد نجح التضمين. سيحتوي جسم الصفحة على شيء مشابه لـ:

```html
<div class="c0">Hello, embedded fonts!</div>
```

يجب أن يُعرض النص تمامًا كما كان في Excel، بغض النظر عن الخطوط المثبتة لدى العميل.

---

## الأسئلة المتكررة (FAQs)

**س: هل يعمل هذا مع صيغ Excel؟**  
ج: بالتأكيد. تُقيم الصيغ قبل توليد HTML، لذا القيم المعروضة هي سلاسل ثابتة—تمامًا مثل أي تصدير عادي.

**س: هل يمكنني تضمين الخطوط عند التصدير إلى حزمة ZIP بدلاً من ملف HTML واحد؟**  
ج: نعم. اضبط `htmlOptions.ExportToSingleFile = false` وسينشئ Aspose.Cells مجلدًا يحتوي على ملفات CSS وملفات الخطوط منفصلة، وهو ما يفضله بعض الفرق لإدارة الإصدارات.

**س: ماذا لو كنت بحاجة إلى تضمين

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}