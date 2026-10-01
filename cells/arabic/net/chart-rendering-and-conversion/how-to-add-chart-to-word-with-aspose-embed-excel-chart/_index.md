---
category: general
date: 2026-10-01
description: أضف مخططًا إلى Word باستخدام Aspose في دقائق قليلة. تعلم كيفية تضمين
  مخطط Excel في Word، تصدير المخطط من Excel إلى Word، إنشاء مستند Word باستخدام Aspose،
  وحفظ المخطط في مستند Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: ar
lastmod: 2026-10-01
og_description: أضف مخططًا إلى Word باستخدام Aspose في دقائق. يوضح هذا الدليل كيفية
  تضمين مخطط Excel في Word، وتصدير المخطط من Excel إلى Word، وإنشاء مستند Word باستخدام
  Aspose، وحفظ المخطط في مستند Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: إضافة مخطط إلى Word باستخدام Aspose – تضمين مخطط Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: كيفية إضافة مخطط إلى Word باستخدام Aspose – تضمين مخطط Excel
url: /ar/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة مخطط إلى Word باستخدام Aspose – تضمين مخطط Excel

إذا كنت بحاجة إلى **إضافة مخطط إلى Word** بسرعة، فإن هذا الدرس يقدم لك حلاً كاملاً وجاهزًا للتنفيذ. ستتعرف على كيفية تضمين مخطط Excel في ملف Word، وتصدير المخطط من Excel إلى Word، وأخيرًا **حفظ مستند Word بالمخطط** باستخدام بضع أسطر فقط من C#.

تضمين المخططات هو طلب شائع عندما تقوم بإنشاء تقارير أو فواتير أو لوحات معلومات برمجيًا. في نهاية هذا الدليل ستتمكن من **إنشاء مستند Word باستخدام Aspose** يحتوي على أي مخطط من مصنف Excel، دون الحاجة إلى النسخ واللصق اليدوي.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
- حزم NuGet الخاصة بـ Aspose.Cells و Aspose.Words (التثبيت عبر `dotnet add package Aspose.Cells` و `dotnet add package Aspose.Words`)
- ملف Excel موجود (`Chart.xlsx`) يحتوي على مخطط واحد على الأقل
- بيئة تطوير مثل Visual Studio 2022 أو VS Code

## إضافة مخطط إلى Word باستخدام Aspose

فيما يلي البرنامج الكامل المستقل. انسخه في مشروع وحدة تحكم جديد، استعد الحزم، وشغّله. يقوم البرنامج بتحميل مصنف Excel، إنشاء مستند Word، إدراج المخطط الأول، وحفظ النتيجة.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### لماذا كل سطر مهم

1. **تحميل المصنف** – `Workbook` يقوم بتحليل ملف Excel ويمنحك وصولًا برمجيًا إلى أوراق العمل والمخططات.  
2. **إنشاء مستند Word** – `Document` هو نقطة الدخول في Aspose.Words لأي مهمة معالجة Word.  
3. **DocumentBuilder** – هذه الفئة المساعدة تتيح لك إدراج محتوى (نص، صور، مخططات) في موضع المؤشر الحالي.  
4. **InsertChart** – النسخة التي تقبل كائن `Aspose.Cells.Chart` تنسخ بيانات المخطط وتنسيقه وسلسلاته مباشرةً إلى ملف Word. لا يلزم تحويل صورة وسيطة، مما يحافظ على جودة المتجه.  
5. **Save** – `Save` يكتب حزمة .docx إلى القرص، مكملًا خطوة **حفظ مستند Word بالمخطط**.

#### النتيجة المتوقعة

بعد تشغيل البرنامج، افتح `Chart.docx`. سترى المخطط نفسه الذي تم تخزينه في `Chart.xlsx`، موضعًا حيث تم وضع الـ builder (بداية المستند). يظل المخطط قابلاً للتحرير بالكامل داخل Word (يمكنك تغيير حجمه، ألوانه، أو تعديل مصدر البيانات).

## تضمين مخطط Excel في Word

إذا كنت بحاجة إلى تضمين أكثر من مخطط واحد، كرّر استدعاء `InsertChart` لكل كائن مخطط. على سبيل المثال، لتضمين جميع المخططات من ورقة العمل الأولى:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**نصيحة احترافية:** استخدم `builder.Writeln()` لإدراج فاصل فقرة، مما يضمن بدء كل مخطط في سطر جديد.

## تصدير مخطط Excel إلى Word – التعامل مع أوراق عمل متعددة

عندما تكون المخططات موزعة عبر عدة أوراق عمل، قم بالتكرار عبر مجموعة `Worksheets` في المصنف:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

هذا النهج **يصدّر مخطط Excel إلى Word** لأي تخطيط مصنف، مما يجعل الحل قويًا للتقارير المعقدة.

## إنشاء مستند Word باستخدام Aspose – تخصيص المظهر

يمكنك التحكم في حجم وموقع كل مخطط مُدرج عن طريق تعديل الـ `Shape` الذي تُعيده `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

ضبط `WrapType` إلى `Inline` يضمن أن يتصرف المخطط كفقرة عادية، وهو ما يكون غالبًا مرغوبًا في توليد المستندات تلقائيًا.

## حفظ مستند Word بالمخطط – أفضل الممارسات

- **استخدم اسم ملف وصفي** (`Report_Q1_2026.docx`) لتسهيل إدارة الإصدارات.  
- **تخلص من الكائنات** عندما تنتهي، خاصةً في عمليات الدُفعات الكبيرة:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **تحقق من النتيجة** برمجيًا إذا كنت تُنشئ العديد من الملفات:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إدراج مخطط ليس هو الأول في الورقة؟* | نعم. يمكن الوصول إليه عبر الفهرس: `sheet.Charts[2]` للمخطط الثالث. |
| *ماذا لو كان مخطط Excel يستخدم مصدر بيانات غير موجود في المصنف؟* | Aspose.Cells يدمج البيانات مباشرةً في كائن المخطط، لذا يظل المخطط فعالًا حتى إذا تم إزالة نطاق المصدر. |
| *هل أحتاج إلى ترخيص لـ Aspose؟* | التقييم المجاني يعمل، لكن النسخة المرخصة تزيل علامة التقييم وتفتح جميع الميزات. |
| *هل سيكون المخطط قابلًا للتحرير في Word بعد الإدراج؟* | يتم إدراج المخطط كمخطط Word أصلي، لذا يمكن للمستخدمين تحرير السلاسل والعناوين والأنماط باستخدام واجهة Word. |
| *كيف يمكن إدراج مخطط كصورة بدلاً من مخطط أصلي؟* | استخدم `builder.InsertImage(chart.ToImage())` لتضمين صورة نقطية. هذا مفيد عندما تريد الحفاظ على العرض البصري الدقيق دون إمكانية تحرير المخطط على مستوى Word. |

## مثال كامل يعمل (نسخ‑لصق)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

تشغيل الكود ينتج ملف Word (`ReportWithCharts.docx`) يحتوي على نتائج **إضافة مخطط إلى Word** لكل مخطط في المصنف المصدر.

## الخلاصة

أنت الآن تعرف كيف **تضيف مخططًا إلى Word** باستخدام Aspose.Cells و Aspose.Words، وكيف **تضمّن مخطط Excel في Word**، **تصدّر مخطط Excel إلى Word**، **تنشئ مستند Word باستخدام Aspose**، وأخيرًا **تحفظ مستند Word بالمخطط**. يعمل هذا النهج في حالات المخطط الواحد وكذلك في المصنفات المعقدة التي تحتوي على العديد من المخططات عبر أوراق عمل متعددة.

الخطوات التالية التي قد تستكشفها:

- تطبيق تنسيق مخصص على المخططات المُدرجة (الألوان، الخطوط) عبر واجهة برمجة `Chart`.  
- دمج إدراج المخطط مع توليد النص لإنتاج تقارير مؤتمتة بالكامل.  
- استخدم Aspose.Slides إذا كنت بحاجة إلى  

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حفظ DOCX من Excel – دليل كامل لتصدير المخططات إلى Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [إنشاء مصنف Excel مع مخطط دائري باستخدام Aspose.Cells .NET - دليل شامل](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [إنشاء مخطط فقاعة في Excel باستخدام Aspose.Cells .NET&#58; دليل خطوة بخطوة](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}