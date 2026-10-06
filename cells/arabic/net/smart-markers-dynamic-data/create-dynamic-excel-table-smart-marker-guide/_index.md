---
category: general
date: 2026-05-23
description: إنشاء جدول إكسل ديناميكي باستخدام قالب وبيانات JSON. تعلم كيفية تحميل
  قالب إكسل، أتمتة تقرير إكسل، وتعبئة إكسل من JSON بسرعة.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: ar
og_description: أنشئ جدول إكسل ديناميكي في دقائق باستخدام قالب وJSON. يوضح هذا الدرس
  كيفية تحميل قالب إكسل، أتمتة تقرير إكسل، وتعبئة إكسل من JSON.
og_title: إنشاء جدول إكسل ديناميكي – دليل العلامة الذكية
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: إنشاء جدول إكسل ديناميكي – دليل العلامة الذكية
url: /ar/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء جدول Excel ديناميكي – دليل Smart Marker

هل احتجت يومًا إلى **إنشاء جدول Excel ديناميكي** يتوسع تلقائيًا لكل سجل في مجموعة البيانات الخاصة بك؟ لست وحدك. سواء كنت تبني لوحة تحكم مبيعات شهرية أو حزمة فواتير حسب العملاء، فإن القدرة على **ملء Excel من JSON** دون كتابة حلقات لا نهائية يمكن أن توفر ساعات.

في هذا الدرس سنستعرض حلًا كاملاً وتطبيقيًا يوضح لك كيفية **تحميل قالب Excel**، وإدراج Smart Marker، وتغذيته ببيانات JSON، وأخيرًا **أتمتة إنشاء تقرير Excel**. في النهاية ستحصل على مشروع .NET جاهز للتشغيل ينتج مصنف Excel مصقولًا من حمولة JSON واحدة.

---

## ما ستحتاجه

- **Aspose.Cells for .NET** (أو أي مكتبة تدعم Smart Markers). يستخدم المثال الإصدار 24.5، لكن أي إصدار حديث يعمل.
- Visual Studio 2022 (أو بيئة التطوير المفضلة لديك لـ C#).
- ملف قالب Excel بسيط (`template.xlsx`) موجود في مجلد تملكه.
- سلسلة JSON تحتوي على مجموعة تسمى `Customers`.

هذا كل شيء—لا خدمات إضافية، لا اتصالات بقاعدة بيانات، فقط شفرة صافية.

## الخطوة 1: إنشاء مصنف قالب – تحميل قالب Excel

أول شيء نقوم به هو **تحميل قالب Excel** إلى الذاكرة. فكر في القالب كقماش حيث يُخبر العنصر النائب الخاص مكان تكرار الصفوف المعالج.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **لماذا هذا مهم:** تحميل القالب مرة واحدة يقلل من عمليات الإدخال/الإخراج للملف ويسمح لك بإعادة استخدام نفس التخطيط للعديد من التقارير. كما أنه يعزل منطق Smart Marker عن باقي الشفرة، مما يوفر فصلًا نظيفًا للمسؤوليات.

## الخطوة 2: إدراج Smart Marker – إنشاء جدول Excel ديناميكي

الآن نقوم بإدراج **Smart Marker** سيكرر جدولًا لكل إدخال في مجموعة `Customers`. الصيغة `${Customers.RepeatWorksheet}` تخبر Aspose.Cells بنسخ الورقة بالكامل لكل عميل.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **نصيحة احترافية:** إذا كنت تحتاج فقط إلى تكرار الصفوف بدلاً من الأوراق بالكامل، استخدم `${Customers.Repeat}` في الصف الأول من الجدول. التكرار على مستوى الورقة مفيد عندما يحصل كل عميل على تبويب خاص به.

## الخطوة 3: إعداد SmartMarkerProcessor – أتمتة تقرير Excel

مع وجود العلامة، نقوم بإنشاء `SmartMarkerProcessor`. هذا الكائن يدير ربط البيانات بين JSON وقالب Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

المعالج خفيف الوزن؛ يمكنك إعادة استخدامه لعدة حمولات JSON إذا رغبت.

## الخطوة 4: تغذية بيانات JSON – ملء Excel من JSON

هنا يحدث السحر. نقوم بتغذية سلسلة JSON تحتوي على مصفوفة من العملاء. يمكن لكل عميل أن يحتوي على حقول مثل `Name`، `Email`، و `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **لماذا JSON؟** JSON مستقل عن اللغة وسهل الإنشاء من واجهات برمجة التطبيقات، قواعد البيانات، أو حتى الإدخال اليدوي. استخدام `ApplyJson` يعني أنك لا تحتاج إلى ربط الكائنات يدويًا؛ المعالج يقوم بالعمل الشاق.

## الخطوة 5: حفظ النتيجة – إنشاء تقرير Excel من JSON

أخيرًا، نكتب المصنف المملوء إلى القرص. الآن يحتوي ملف الإخراج على ورقة منفصلة لكل عميل، كل واحدة مملوءة بالبيانات من JSON الخاص بنا.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### النتيجة المتوقعة

- **output.xlsx** سيحتوي على ثلاث أوراق عمل مسماة `Sheet1`، `Sheet2`، `Sheet3` (أو أي تسمية يستخدمها القالب الخاص بك).
- كل ورقة ستعرض قيم `Name`، `Email`، و `Total` لعميل واحد.
- التخطيط الذي صممته في `template.xlsx` (العناوين، التنسيق، الصيغ) يُحافظ عليه عبر جميع الأوراق المُنشأة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتشغيل. انسخه والصقه في تطبيق Console، عدل مسارات الملفات، واضغط **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح `output.xlsx`، وسترى **إنشاء جدول Excel ديناميكي** قيد التنفيذ—كل عميل يحصل على ورقته الخاصة، مُنسقة بالكامل كما صممت.

## أسئلة شائعة وحالات خاصة

| Question | Answer |
|----------|--------|
| *ماذا لو كان JSON الخاص بي يحتوي على كائنات متداخلة؟* | تدعم Smart Markers تدوين النقاط (`${Customers.Address.City}`) طالما أن هيكلية JSON متطابقة. |
| *هل يمكنني تسمية أوراق العمل المُنشأة باسم العميل؟* | نعم—أضف علامة مثل `${Customers.Name}` في خلية اسم ورقة العمل أو استخدم `processor.ApplyJson(customersJson, \"Customers\")` مع نمط تسمية. |
| *ماذا عن مجموعات البيانات الكبيرة (أكثر من 10 ألف صف)؟* | المعالج يبث البيانات بكفاءة، لكن راقب استهلاك الذاكرة. فكر في تقسيم التقرير إلى ملفات متعددة إذا وصلت إلى حدود الأداء. |
| *هل أحتاج إلى ترخيص لـ Aspose.Cells؟* | التقييم المجاني يكفي للاختبار، لكن النسخة المرخصة تزيل العلامات المائية وتوفر جميع الميزات. |
| *هل يمكنني استخدام هذا النهج مع .NET Core؟* | بالطبع—Aspose.Cells يدعم .NET 6/7/8. فقط أضف حزمة NuGet ويظل الكود كما هو. |

## نصائح للتطبيقات الجاهزة للإنتاج

- **تحقق من صحة JSON** قبل تغذيته إلى `ApplyJson`. سيؤدي حمولة غير صحيحة إلى رمي `JsonParseException`.
- **قم بتخزين القالب مؤقتًا** إذا كنت تولد تقارير متعددة في وقت قصير؛ تحميله من القرص بشكل متكرر غير ضروري.
- **قفل المصنف** أثناء المعالجة إذا كنت تشغله في خدمة ويب متعددة الخيوط لتجنب حالات السباق.
- **أضف معالجة أخطاء** حول `workbook.Save` للتعامل بلطف مع مشاكل الأذونات أو الملفات المقفلة.
- **خصّص التنسيق** في القالب (التنسيق الشرطي، الصيغ) لتسمح للأوراق المُنشأة بالحفاظ على منطق الأعمال دون شفرة إضافية.

## الخلاصة

أصبح لديك الآن نمط قوي وشامل لكيفية **إنشاء جدول Excel ديناميكي** باستخدام قالب، Smart Markers، وبيانات JSON. من خلال **تحميل قالب Excel**، وإدراج علامة تكرار، و**ملء Excel من JSON**، يمكنك **أتمتة إنشاء تقرير Excel** ببضع أسطر من C# فقط.

ما الخطوات التالية؟ جرّب إضافة مخططات تشير إلى الجداول الديناميكية، أو صدّر نفس JSON إلى PDF باستخدام Aspose.Words. يمكنك أيضًا تجربة **إنشاء تقرير Excel من JSON** من استعلام قاعدة بيانات لإغلاق الحلقة.

## دروس ذات صلة

- [إنشاء جدول محوري في Excel باستخدام Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [إنشاء مخططات خطية ديناميكية في Excel باستخدام Aspose.Cells for .NET&#58; دليل خطوة بخطوة](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [كيفية إنشاء مربعات اختيار في Excel باستخدام Aspose.Cells for .NET | درس التحقق من البيانات](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}