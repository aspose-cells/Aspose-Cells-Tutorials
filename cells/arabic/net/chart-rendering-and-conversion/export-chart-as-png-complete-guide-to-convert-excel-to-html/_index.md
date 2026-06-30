---
category: general
date: 2026-06-30
description: صدّر المخطط بصيغة PNG أثناء تحويل Excel إلى HTML باستخدام Aspose.Cells.
  تعلّم كيفية تضمين الصور بصيغة Base64 وحفظ المصنف كملف HTML في دقائق.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: ar
og_description: تصدير المخطط كملف PNG وتضمين الصور بصيغة Base64 أثناء تحويل Excel
  إلى HTML. اتبع هذا الدرس خطوة بخطوة بلغة C# لحفظ المصنف كملف HTML بسهولة.
og_title: تصدير المخطط كملف PNG – تحويل Excel إلى HTML باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: تصدير المخطط بصيغة PNG – دليل شامل لتحويل Excel إلى HTML باستخدام Aspose.Cells
url: /ar/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط كـ PNG – دليل كامل لتحويل Excel إلى HTML باستخدام Aspose.Cells

هل تساءلت يومًا كيف يمكنك **تصدير المخطط كـ PNG** مباشرةً من مصنف Excel مع تحويل الورقة بأكملها إلى HTML نظيف ومتجاوب؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تقرير جاهز للويب يعرض المخططات دون الحاجة إلى التعامل مع ملفات صور منفصلة. الخبر السار هو أن Aspose.Cells يجعل هذا الأمر سهلًا للغاية.

في هذا البرنامج التعليمي سنستعرض الخطوات الدقيقة لـ **تحويل Excel إلى HTML**، **تضمين الصور كـ Base64**، وأخيرًا **حفظ المصنف كـ HTML**—كل ذلك مع ضمان حفظ كل مخطط كصورة PNG. في النهاية ستحصل على ملف HTML واحد يمكنك وضعه في أي صفحة ويب، وستظهر جميع المخططات فورًا دون الحاجة إلى أصول إضافية.

## ما ستتعلمه

- كيفية تحميل مصنف موجود يحتوي بالفعل على مخططات.  
- أي علامات `HtmlSaveOptions` تتحكم في تصدير الصور، تنسيق المخطط، والاستجابة.  
- الكود الدقيق المطلوب **لتصدير المخطط كـ PNG** وتضمين تلك PNGs كسلاسل Base64.  
- كيفية **حفظ المصنف كـ HTML** باستدعاء طريقة واحدة.  
- نصائح لتصحيح الأخطاء الشائعة، مثل فقدان صور المخططات أو سلاسل Base64 الضخمة.  

**المتطلبات المسبقة:**  
- .NET 6+ (أو .NET Framework 4.6+) مثبتة.  
- رخصة Aspose.Cells صالحة (أو مفتاح تقييم مؤقت).  
- إلمام أساسي بـ C# و Visual Studio (أو بيئة التطوير المفضلة لديك).  

إذا كان أي من هذه غير مألوف لك، توقف لحظة وقم بإعداده؛ باقي الدليل يفترض أنها جاهزة.

---

## الخطوة 1: إعداد المشروع وتثبيت Aspose.Cells

قبل أن نتمكن من **تصدير المخطط كـ PNG**، نحتاج إلى مشروع C# ي引用 مكتبة Aspose.Cells.

1. افتح Visual Studio وأنشئ تطبيق **Console App** جديد (`dotnet new console`).  
2. أضف حزمة NuGet الخاصة بـ Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (اختياري) إذا كان لديك ملف ترخيص، ضعّه في جذر المشروع وفعل الترخيص أثناء التشغيل:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **نصيحة احترافية:** احفظ ملف الترخيص خارج نظام التحكم في المصدر. استخدم متغيرات البيئة أو مخازن الأسرار الآمنة للإنتاج.

---

## الخطوة 2: تحميل المصنف الذي يحتوي على المخطط

الآن سنقوم بتحميل ملف Excel الذي يحتوي بالفعل على المخطط الذي نريد **تصديره كـ PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **لماذا هذا مهم:** تحميل المصنف مبكرًا يمنحنا الوصول إلى جميع الأوراق، المخططات، والكائنات المضمنة. إذا فشل تحميل المصنف، لن يتم تشغيل خطوة **تصدير المخطط إلى PNG** لاحقًا.

---

## الخطوة 3: تكوين خيارات حفظ HTML

قلب الحل يكمن في `HtmlSaveOptions`. من خلال تعديل بعض الخصائص يمكننا:

- **ExportChartImageFormat = ImageFormat.Png** → يضمن أن يصبح كل مخطط بصيغة PNG.  
- **ExportImagesAsBase64 = true** → يضمّن بيانات PNG مباشرةً في HTML، مما يلغي الحاجة إلى ملفات خارجية.  
- **IsResponsive = true** → يجعل الجداول المولدة تتكيف مع شاشات الهواتف المحمولة.  
- **ExportPrintingHeadersFooters = false** → يزيل البيانات الوصفية غير الضرورية للطباعة.  

إليك التكوين الكامل:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### لماذا هذه الإعدادات؟

- **ExportChartImageFormat = ImageFormat.Png** هو الطريقة الوحيدة لضمان صورة مخطط خالية من الفقدان وآمنة للويب.  
- **ExportImagesAsBase64 = true** يعني أنه يمكنك **تضمين الصور كـ Base64**، وهو مثالي لتقارير البريد الإلكتروني أو النشر بملف واحد.  
- **IsResponsive = true** يحل مشكلة شائعة: جداول تتجاوز عرض الشاشة على الهواتف الذكية.  
- **ExportPrintingHeadersFooters = false** يحافظ على خفة وزن HTML—بدون معلومات طباعة مخفية لا تُستَخدم على الويب.  

---

## الخطوة 4: حفظ المصنف كـ HTML

مع ضبط الخيارات، السطر الأخير هو استدعاء واحد يقوم بـ **تحويل Excel إلى HTML** و**تصدير المخطط كـ PNG** خلف الكواليس.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

عند انتهاء هذا السطر، ستحصل على ملف اسمه `Report.html`. افتحه في أي متصفح، وسترى:

- كل بيانات الورقة تُعرض كجداول HTML نظيفة.  
- كل مخطط يُعرض كصورة PNG مضمنة (بفضل تضمين Base64).  
- لا توجد ملفات صور إضافية بجوار ملف HTML.  

### النتيجة المتوقعة

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

لاحظ السمة `src="data:image/png;base64,..."`—هذا هو سحر **تضمين الصور كـ Base64** في العمل. لا يتم إنشاء ملفات `.png` منفصلة على القرص.

---

## الخطوة 5: التحقق من تصدير PNG وتعديل الإعدادات إذا لزم الأمر

أحيانًا قد يبدو المخطط غير واضح بعد التحويل، خاصةً إذا كان يستخدم خطوطًا مخصصة أو تدرجات معقدة. إليك كيفية التحقق المزدوج:

1. افتح ملف HTML المُولَّد في Chrome. انقر بزر الماوس الأيمن على صورة المخطط واختر **Open image in new tab**. سيظل العنوان يبدأ بـ `data:image/png;base64,`.  
2. إذا ظهرت الصورة غير واضحة، فكر في زيادة دقة المخطط قبل الحفظ:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. بالنسبة للمخططات التي تعتمد على مصادر بيانات خارجية، تأكد من أن المصنف تم تحديثه بالكامل قبل الحفظ:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

هذه التعديلات تضمن أن خطوة **تصدير مخطط Excel إلى PNG** تنتج رسومات حادة وجاهزة للإنتاج.

---

## الخطوة 6: نشر ملف HTML في أي مكان

نظرًا لأن جميع الصور مضمَّنة، يمكنك الآن:

- إرسال ملف HTML كمرفق واحد عبر البريد الإلكتروني.  
- لصق HTML في نظام إدارة محتوى يقبل الكود الخام.  
- استضافته على موقع ثابت دون القلق من فقدان ملفات PNG.  

إذا احتجت يومًا إلى ملفات PNG كأصول منفصلة (ربما لإنشاء PDF لاحقًا)، يمكنك تغيير `ExportImagesAsBase64` إلى `false` وتوجيه `HtmlSaveOptions` إلى مجلد إخراج للصور.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

الآن سيشير HTML إلى ملفات PNG خارجية، مع الحفاظ على **تصدير المخطط كـ PNG** وتوفير ملفات صور فردية لاستخدامات أخرى.

---

## المشكلات الشائعة وكيفية تجنّبها

| العرض | السبب المحتمل | الحل |
|---------|--------------|-----|
| المخطط غير موجود في HTML | ترك `ExportChartImageFormat` على القيمة الافتراضية (`Jpeg`) والمتصفح يحظر المحتوى المختلط. | اضبط `ExportChartImageFormat = ImageFormat.Png`. |
| ملف HTML كبير (عدة ميغابايت) | مخططات كبيرة أو العديد من الصور عالية الدقة المضمَّنة كـ Base64. | قلل `htmlOptions.ImageResolution` أو اضغط المخطط في Excel قبل التحويل. |
| الجداول تتجاوز العرض على الهواتف | عدم تفعيل `IsResponsive`. | تأكد من ضبط `IsResponsive = true` في `HtmlSaveOptions`. |
| سلاسل Base64 تحتوي على أحرف سطر جديد | إصدارات .NET القديمة قد تقسم السلاسل الطويلة. | حدّث إلى .NET 6+ أو اضبط `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## إضاقة: تغليف كل شيء في طريقة قابلة لإعادة الاستخدام

إذا كنت ستقوم بهذا التحويل بشكل متكرر، قم بلف المنطق في طريقة واحدة:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

الآن يمكنك استدعاء `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` من أي مكان في قاعدة الكود الخاصة بك.

---

## الخلاصة

لقد أتقنت الآن كيفية **تصدير المخطط كـ PNG** أثناء **تحويل Excel إلى HTML**، **تضمين الصور كـ Base64**، و**حفظ المصنف كـ HTML** باستخدام Aspose.Cells. الفكرة الأساسية هي أن مجموعة مختارة من إعدادات `HtmlSaveOptions` تمنحك ملف HTML واحد مكتمل يحتوي على كل شيء ويعمل على أي جهاز—بدون ملفات PNG إضافية، دون مجلدات فوضوية.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذا النهج مع **تصدير مخطط Excel إلى PNG** لإنشاء PDF، أو جرب CSS مخصص لتنسيق الجداول أكثر. السماء هي الحد عندما تتحكم في البيانات والعرض برمجيًا.

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، أو شارك كيف طبّقت هذا النمط في مشاريعك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [تصدير Excel إلى HTML باستخدام Aspose.Cells لـ .NET: دليل كامل](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [تصدير Excel إلى HTML بدون سكريبتات الإطار باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [كيفية تصدير ورقة عمل Excel إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}