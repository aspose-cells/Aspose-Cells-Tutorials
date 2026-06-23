---
category: general
date: 2026-03-25
description: كيفية تصدير المخططات من Word باستخدام Aspose.Words C# – تعلم كيفية تضمين
  المخططات وتصديرها من Word في دقائق.
draft: false
keywords:
- how to export charts
- how to include charts
- export charts from word
- Aspose.Words export
- C# document automation
language: ar
og_description: كيفية تصدير المخططات من Word باستخدام Aspose.Words C#. يوضح لك هذا
  الدليل كيفية تضمين المخططات وتصديرها من Word بسرعة.
og_title: كيفية تصدير المخططات من Word – دليل C# الكامل
tags:
- C#
- Aspose.Words
- Word Automation
- Charts
title: كيفية تصدير المخططات من Word – دليل C# الكامل
url: /ar/net/chart-rendering-and-conversion/how-to-export-charts-from-word-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير المخططات من Word – دليل C# كامل

هل احتجت يومًا **كيفية تصدير المخططات** من مستند Word لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عند أتمتة التقارير. في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية لا يوضح لك فقط **كيفية تصدير المخططات**، بل يشرح أيضًا **كيفية تضمين المخططات** في الملف المُصدَّر. في النهاية ستتمكن من تصدير المخططات من Word ببضع أسطر من C#.

سنستخدم مكتبة **Aspose.Words for .NET** الشهيرة لأنها تتعامل مع كائنات المخططات بشكل أصلي وتعمل مع .docx و .doc وحتى الصيغ القديمة. لا حاجة للتلاعب بـ Office Interop، ولا كوابيس COM. الخطوات أدناه تفترض أن لديك مشروع C# أساسي وحزمة Aspose.Words NuGet مثبتة. إذا كنت جديدًا على المكتبة، لا تقلق—سنغطي المتطلبات المسبقة بسرعة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- Visual Studio 2022 أو أي بيئة تطوير تفضّلها
- Aspose.Words for .NET (التثبيت عبر `dotnet add package Aspose.Words`)

> **نصيحة احترافية:** حافظ على تحديث نسخة Aspose.Words الخاصة بك؛ الإصدار الأخير (اعتبارًا من مارس 2026) يضيف تحسينات في معالجة المخططات وأداء أفضل.

## الخطوة 1: تحميل مستند Word المصدر

أول شيء تحتاج إلى القيام به هو فتح ملف `.docx` الذي يحتوي على المخططات التي تريد استخراجها. تجعل لك Aspose.Words هذا الأمر سطرًا واحدًا.

```csharp
using Aspose.Words;

// Load the source document (replace with your actual path)
Document document = new Document(@"C:\Docs\input.docx");
```

*لماذا هذا مهم:* تحميل المستند يُنشئ تمثيلًا في الذاكرة لكل عنصر—فقرات، جداول، وبشكل حاسم، كائنات المخططات. بدون هذه الخطوة لا يمكنك الوصول إلى المخططات أو تعديلها.

## الخطوة 2: تكوين خيارات الحفظ للحفاظ على المخططات

بشكل افتراضي، سيحافظ `document.Save("output.docx")` البسيط على كل شيء، ولكن إذا قمت بتغيير `ExportImages` أو علامات مشابهة قد تفقد المخططات المدمجة. لتكون صريحًا—وللإجابة على جزء **كيفية تضمين المخططات** من السؤال—نقوم بتعيين `DocxSaveOptions` مع `ExportCharts = true`.

```csharp
// Create save options that ensure charts are included
DocxSaveOptions saveOptions = new DocxSaveOptions
{
    ExportCharts = true          // Guarantees charts are part of the saved file
};
```

*شرح:* `ExportCharts` يخبر المحرك بترميز كل مخطط كجزء مخطط Office Open XML أصلي. هذا ضروري عندما تفتح الملف لاحقًا في Word أو محررات أخرى؛ تظهر المخططات تمامًا كما كانت في المستند الأصلي.

## الخطوة 3: حفظ المستند باستخدام الخيارات المكوَّنة

الآن نكتب المستند مرة أخرى إلى القرص، باستخدام الخيارات التي عرّفناها للتو. سيحتوي ملف الإخراج على كل المحتوى الأصلي **والمخططات**.

```csharp
// Save the document with charts preserved
document.Save(@"C:\Docs\charts.docx", saveOptions);
```

في هذه المرحلة لديك ملف Word جديد (`charts.docx`) هو نسخة مطابقة للأصل، مكتمل بكل رسومات المخططات. افتحه في Microsoft Word للتحقق—يجب أن تكون المخططات قابلة للتعديل بالكامل، وتعمل بشكل كامل، وتظهر كما كانت من قبل.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى تطبيق كونسول، عدّل المسارات، واضغط **F5**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document containing charts
            string inputPath = @"C:\Docs\input.docx";
            Document document = new Document(inputPath);
            Console.WriteLine($"Loaded document: {inputPath}");

            // 2️⃣ Set save options to explicitly include charts
            DocxSaveOptions saveOptions = new DocxSaveOptions
            {
                ExportCharts = true   // This ensures charts are not stripped out
            };
            Console.WriteLine("Configured DocxSaveOptions to export charts.");

            // 3️⃣ Save the new file
            string outputPath = @"C:\Docs\charts.docx";
            document.Save(outputPath, saveOptions);
            Console.WriteLine($"Document saved with charts at: {outputPath}");

            // Verification hint
            Console.WriteLine("Open the output file in Word to confirm charts are present.");
        }
    }
}
```

**النتيجة المتوقعة:** عند فتح `charts.docx` في Microsoft Word، يظهر كل مخطط من `input.docx` دون تغيير. لا صور مفقودة، ولا مراجع مكسورة.

## معالجة الحالات الشائعة

| Situation | What to Watch For | Recommended Fix |
|-----------|-------------------|-----------------|
| **المستند يحتوي على أوراق Excel مدمجة** | قد تكون المخططات مرتبطة ببيانات Excel خارجية. | استخدم `DocxSaveOptions.ExportEmbeddedExcelData = true` (متاح في الإصدارات الأحدث) للحفاظ على البيانات كما هي. |
| **مستندات كبيرة (> 100 ميغابايت)** | استخدام الذاكرة يرتفع أثناء التحميل. | فعّل `LoadOptions.LoadFormat = LoadFormat.Docx` وفكّر في البث باستخدام `DocumentBuilder` للمعالجة التدريجية. |
| **تحتاج فقط إلى مخططات محددة** | تصدير الملف بالكامل يُعد مبالغة. | قم بالتكرار على `document.GetChildNodes(NodeType.Shape, true)` وصفيه بـ `Shape.IsChart`. ثم استنسخ تلك الأشكال إلى `Document` جديد قبل الحفظ. |
| **الصيغة المستهدفة هي PDF** | قد تُظهر المخططات بشكل مختلف. | استخدم `PdfSaveOptions` مع `ExportCharts = true` (العلم يعمل مع PDF أيضًا). |

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات `.doc` القديمة؟**  
ج: نعم. تقوم Aspose.Words تلقائيًا بتحويل الصيغة الثنائية القديمة إلى بنية Open XML الحديثة في الذاكرة، لذا لا يزال `ExportCharts` ساريًا.

**س: ماذا لو أردت فقط تصدير صور المخططات، وليس المستند بالكامل؟**  
ج: يمكنك استخراج كل مخطط كصورة باستخدام `ChartRenderer`. مثال: `chartRenderer.Save("chart.png", ImageFormat.Png);` هذا يلبي الحاجة المحددة لـ **كيفية تصدير المخططات**.

**س: هل هناك قلق بشأن الترخيص؟**  
ج: Aspose.Words هي مكتبة تجارية. للتقييم يمكنك استخدام ترخيص مؤقت؛ للإنتاج ستحتاج إلى ترخيص صالح لتجنب علامة التقييم المائية.

## نظرة بصرية

فيما يلي مخطط سريع للتدفق—لاحظ الكلمة المفتاحية الأساسية في نص alt.

![مثال على تصدير المخططات – مخطط يوضح خطوات التحميل → التكوين → الحفظ](https://example.com/images/export-charts-diagram.png)

*نص alt:* **مخطط يوضح تصدير المخططات مع توضيح خطوات التحميل، التكوين، والحفظ**

## الخلاصة

لقد غطينا للتو **كيفية تصدير المخططات** من مستند Word باستخدام Aspose.Words، وأظهرنا **كيفية تضمين المخططات** عند الحفظ، وتطرقنا إلى عدة سيناريوهات لـ **تصدير المخططات من Word** بصيغ مختلفة. نمط الخطوات الثلاث — التحميل، التكوين، الحفظ — بسيط، موثوق، ويتوسع من التقارير الصغيرة إلى المستندات المؤسسية الضخمة.

ما التالي؟ جرّب استخراج المخططات المحددة فقط، تحويلها إلى PNG للاستخدام على الويب، أو أتمتة عملية دفعة تمر عبر مجلد من ملفات Word وتصدّر مخططاتها دفعة واحدة. كل من هذه الإضافات يبني على التقنية الأساسية التي إتقنتها الآن.

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، أو مشاركة كيفية تعديلك لهذا النمط في مشاريعك الخاصة. برمجة سعيدة، ولتظهر مخططاتك دائمًا بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}