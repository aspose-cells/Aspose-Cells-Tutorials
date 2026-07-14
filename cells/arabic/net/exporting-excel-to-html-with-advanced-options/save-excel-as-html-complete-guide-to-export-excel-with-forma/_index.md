---
category: general
date: 2026-07-14
description: احفظ ملف Excel كـ HTML بسرعة وتعلم كيفية تحويل Excel إلى HTML مع الحفاظ
  على التنسيق الكامل. صدّر ملف Excel مع التنسيق باستخدام Aspose.Cells في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: ar
lastmod: 2026-07-14
og_description: احفظ ملف Excel كـ HTML فورًا. يوضح هذا الدليل كيفية تحويل Excel إلى
  HTML مع الحفاظ على الأنماط وتمكين تنسيق الأرقام في Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: حفظ إكسل كـ HTML – تصدير خطوة بخطوة مع تنسيق كامل
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: حفظ إكسل كـ HTML – دليل كامل لتصدير إكسل مع التنسيق
url: /ar/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ Excel كـ HTML – دليل كامل لتصدير Excel مع التنسيق

هل تساءلت يوماً كيف **تحفظ Excel كـ HTML** دون فقدان الألوان أو الحدود أو تنسيقات الأرقام؟ لست وحدك. في العديد من سيناريوهات التقارير تحتاج إلى عرض جاهز للويب لدفتر عمل، وأسرع طريقة هي تصدير الملف مباشرةً إلى HTML.  

في هذا الدليل سنستعرض الخطوات الدقيقة **لتحويل Excel إلى HTML** باستخدام Aspose.Cells، وتمكين تنسيق الأرقام في Grid.js، والتأكد من أن النتيجة تبدو تماماً مثل جدول البيانات الأصلي. في النهاية ستحصل على ملف HTML جاهز للإدراج يمكنك خدمته من أي خادم ويب.

## ما ستتعلمه

- المتطلبات المسبقة وتثبيت الحزمة  
- تحميل دفتر عمل موجود (أو إنشاء واحد في الوقت الفعلي)  
- تكوين `HtmlSaveOptions` للحصول على تمثيل بصري مثالي  
- تمكين `GridJsOptions.EnableNumberFormat` للحفاظ على تنسيق الأرقام  
- حفظ الملف والتحقق من النتيجة  

إذا جربت يوماً **تصدير Excel مع التنسيق** باستخدام تصدير CSV عام، فأنت تعرف مدى الإحباط عندما تتحول الأرقام إلى نص عادي. هذا الدليل يتجنب تلك المشكلة.

---

## المتطلبات المسبقة – إعداد بيئة التطوير

قبل الغوص في الكود، تأكد من وجود ما يلي:

| المتطلبات | سبب الأهمية |
|-------------|----------------|
| .NET 6.0 أو أحدث (الدليل يستخدم .NET 6) | واجهات برمجة تطبيقات حديثة وأداء أفضل |
| Visual Studio 2022 (أو VS Code مع امتداد C#) | تحرير وتصحيح مريح |
| حزمة NuGet Aspose.Cells لـ .NET | المكتبة التي تدعم `HtmlSaveOptions` و `GridJsOptions` |
| ملف Excel تجريبي (`sample.xlsx`) أو دفتر عمل تنشئه برمجياً | المصدر الذي ستقوم بتحويله |

ثبت Aspose.Cells بالأمر التالي في نافذة Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

> **نصيحة احترافية:** إذا كنت تستخدم خط أنابيب CI، أضف سطر `dotnet add package` نفسه إلى سكريبت البناء حتى تكون الاعتمادية موجودة دائماً.

---

## الخطوة 1: تحميل أو إنشاء دفتر عمل

يمكنك إما تحميل ملف موجود أو بناء واحد برمجياً. إليك مثالًا بسيطًا ينشئ دفتر عمل يحتوي على بعض الخلايا المنسقة لتتمكن من رؤية التنسيق يبقى بعد التصدير.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **لماذا هذا مهم:** من خلال تعيين تنسيقات الأرقام صراحةً، ستلاحظ لاحقًا أن `GridJsOptions.EnableNumberFormat` يحافظ على تلك التنسيقات في مخرجات HTML.

---

## الخطوة 2: تكوين خيارات حفظ HTML

الآن ننشئ كائن `HtmlSaveOptions`. هذا الكائن يخبر Aspose.Cells بالضبط كيف تريد أن يتم عرض HTML.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### تمكين تنسيق الأرقام في Grid.js

إذا كنت تخطط لتضمين HTML داخل صفحة تستخدم **Grid.js** للجداول التفاعلية، فستحتاج إلى إبقاء الأرقام منسقة (مثل رموز العملات، فواصل الآلاف). السطر التالي يفعل ذلك تمامًا:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **ما الذي يحدث في الخلفية؟** `EnableNumberFormat` يضيف مقتطف JavaScript صغير يخبر Grid.js بتفسير خاصية `data-format` للخلية، مما يحافظ على تنسيق Excel داخل المتصفح.

---

## الخطوة 3: حفظ دفتر العمل كملف HTML

مع دفتر العمل جاهزًا والخيارات مضبوطة، السطر الأخير يكتب ملف HTML إلى القرص.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

تشغيل البرنامج ينتج ملف `gridjs.html` يبدو هكذا (عرض مبسط):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

افتح الملف في أي متصفح وسترى جدولًا منسقًا بشكل جميل، مع خلفية رأسية رمادية فاتحة وتنسيق عملة. إذا أدرجت الصفحة في موقع يحمل Grid.js مسبقًا، ستُظهر الأرقام تلقائيًا الفواصل والرموز الصحيحة.

---

## الأخطاء الشائعة عند **تحويل Excel إلى HTML**

| المشكلة | سبب حدوثها | كيفية تجنبه |
|-------|---------------|-----------------|
| **فقدان الصيغ** | HTML ثابت؛ الصيغ تتحول إلى قيم نصية. | إذا كنت بحاجة إلى حسابات حية، احتفظ بدفتر العمل على الخادم واستخدم مكتبات JavaScript مثل SheetJS. |
| **فقدان الصور** | الصور تُخزن كموارد منفصلة. | قم بتعيين `HtmlSaveOptions.ExportImagesAsBase64 = true` لتضمينها مباشرة. |
| **ملفات ضخمة** | دفاتر العمل الكبيرة تولد HTML + JS ضخمة. | استخدم `ExportOnlyVisibleSheets` أو قسّم إلى صفحات متعددة عبر `HtmlSaveOptions.OnePagePerSheet`. |
| **إعدادات لغة رقمية غير صحيحة** | Excel يخزن الأرقام بثقافة ثابتة، وقد تطبق المتصفحات إعدادات محلية. | قم بتعيين `htmlOptions.Encoding = Encoding.UTF8` واستخدم `GridJsOptions.EnableNumberFormat` صراحةً. |

---

## متقدم: تصدير أوراق متعددة مع مثيلات Grid.js منفصلة

إذا كان دفتر العمل يحتوي على عدة أوراق وتريد أن يصبح كل منها جدول Grid.js مستقل، يمكنك التكرار عبر أوراق العمل وحفظ كل واحدة على حدة:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

كل ملف سيحتوي على عنصر `<table class="gridjs-table">` خاص به، جاهز للتعامل المستقل.

---

## التحقق من النتيجة – قائمة مراجعة سريعة

1. **هل تم الحفاظ على التنسيق؟** قارن ألوان خلفية الخلايا والحدود مع عرض Excel الأصلي.  
2. **هل تم الحفاظ على تنسيقات الأرقام؟** ابحث عن خاصية `data-format` داخل عناصر `<td>`.  
3. **هل تم عرض الصور؟** إذا صدرت الصور كـ Base64، يجب أن تظهر مدمجة داخل الصفحة.  
4. **هل وحدة التحكم في المتصفح نظيفة؟** لا أخطاء JavaScript متعلقة بـ Grid.js.  

إذا فشل أي من هذه الفحوصات، راجع الخاصية المقابلة في `HtmlSaveOptions`—معظم المشكلات تنبع من إغفال علم معين.

---

## الخلاصة

أصبح لديك الآن طريقة جاهزة للإنتاج **لحفظ Excel كـ HTML** مع الحفاظ على كل نمط، حد، وتمثيل رقمي. من خلال تكوين `HtmlSaveOptions` وتفعيل `GridJsOptions.EnableNumberFormat`، حولنا جدول بيانات ثابت إلى جدول ويب صديق للمتصفح يعمل بسلاسة مع Grid.js.

باختصار، يوضح لك هذا الدليل كيفية **تحويل Excel إلى HTML** و**تصدير Excel مع التنسيق** باستخدام Aspose.Cells. لا تتردد في التجربة: جرّب سمات مختلفة، أدمج مخططات، أو حتى قدّم HTML عبر نقطة نهاية ASP.NET للتحويل الفوري.

---

## ما التالي؟

- **استكشاف صيغ تصدير أخرى**: PDF، PNG، أو CSV عبر `Workbook.Save`.  
- **دمج مع ASP.NET Core**: إرجاع سلسلة HTML مباشرةً من إجراء تحكم.  
- **الدمج مع SheetJS**: تحميل HTML المُولد مرة أخرى إلى دفتر عمل JavaScript للتحرير من جانب العميل.  

إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راجع وثائق Aspose.Cells للحصول على خيارات تكوين أعمق. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [كيفية تصدير Excel إلى HTML مع خطوط الشبكة باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [تصدير Excel إلى HTML مع الحفاظ على أنماط الحدود باستخدام Aspose.Cells لـ Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [تحويل HTML إلى Excel باستخدام Aspose.Cells .NET: دليل شامل](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}