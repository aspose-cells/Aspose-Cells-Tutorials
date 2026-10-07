---
category: general
date: 2026-02-09
description: كيفية إنشاء دفتر عمل وتحميل JSON إلى Excel بسرعة. تعلم كيفية إدراج JSON،
  تحميل JSON إلى Excel، وتعبئة Excel من JSON باستخدام مثال بسيط بلغة C#.
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: ar
og_description: كيفية إنشاء دفتر عمل وتحميل JSON إلى Excel في دقائق. اتبع هذا الدليل
  خطوة بخطوة لإدراج JSON، وتحميل JSON إلى Excel، وتعبئة Excel من JSON.
og_title: كيفية إنشاء دفتر عمل وإدراج JSON في إكسل
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية إنشاء مصنف وإدراج JSON في إكسل
url: /ar/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء دفتر عمل وإدراج JSON في Excel

هل تساءلت يومًا **كيف تنشئ دفتر عمل** يحتوي بالفعل على البيانات التي تحتاجها، دون الحاجة إلى نسخ‑لصق الصفوف يدويًا؟ ربما لديك حمولة JSON تأتي من خدمة ويب وتريد رؤيتها داخل ورقة Excel فورًا. في هذا الدرس سنستعرض ذلك بالضبط — **كيف تنشئ دفتر عمل**، تحميل JSON إلى Excel، وحتى تعديل خيارات SmartMarker بحيث تتعامل المصفوفات بالطريقة التي تتوقعها.

سنستخدم مكتبة Aspose.Cells for .NET لأنها توفر واجهة برمجة تطبيقات نظيفة لا تحتاج إلى تثبيت Excel. بنهاية الدليل ستتمكن من **load json into excel**، **insert json into excel**، و**populate excel from json** ببضع أسطر فقط.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- فهم أساسي لصياغة C# (لا شيء معقد)
- بيئة تطوير من اختيارك — Visual Studio، Rider، أو VS Code تكفي

> **نصيحة احترافية:** إذا لم تكن لديك رخصة بعد، تقدم Aspose وضع تقييم مجاني مثالي لتجربة الشيفرات أدناه.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

قبل أن نتمكن من الإجابة على **how to create workbook**، نحتاج إلى تطبيق console بلغة C# (أو أي مشروع .NET) مع توجيهات `using` الصحيحة.

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **لماذا هذا مهم:** `Workbook` موجود في `Aspose.Cells`، بينما `SmartMarkerOptions` ينتمي إلى مساحة الاسم `SmartMarkers`. نسيان أيٍ من الاستيرادين سيسبب خطأً أثناء التجميع.

## الخطوة 2: إنشاء نسخة جديدة من Workbook

الآن نصل إلى جوهر الموضوع — **how to create workbook**. الأمر بسيط كما استدعاء المُنشئ.

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

هذا السطر يمنحك ملف Excel فارغ في الذاكرة، جاهز لتعبئته بالبيانات. فكر فيه كقماش فارغ؛ يمكنك لاحقًا حفظه على القرص، بثه إلى متصفح، أو إرفاقه برسالة بريد إلكتروني.

## الخطوة 3: إدراج JSON في الخلية A1

السؤال المنطقي التالي هو **how to insert json** في خلية محددة. هنا سنضع سلسلة JSON صغيرة تحتوي على مصفوفة من الأسماء.

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **ما الذي يحدث؟**  
> - `Worksheets[0]` يشير إلى الورقة الأولى (والوحيدة) في دفتر العمل الجديد.  
> - `Cells["A1"]` يختار الخلية العليا‑اليسرى.  
> - `PutValue` يكتب نص JSON الأصلي، محافظًا على التنسيق الدقيق.

إذا شغلت البرنامج وفتحت الملف الناتج، سترى سلسلة JSON مرتبة في A1 — مثالية للمعالجة اللاحقة.

## الخطوة 4: ضبط خيارات SmartMarker (Array‑as‑Single)

SmartMarkers هي طريقة Aspose لتحويل العناصر النائبة إلى بيانات حقيقية. بشكل افتراضي، تُعامل المصفوفة كمجموعة من الصفوف، لكن أحيانًا تريد المصفوفة بأكملها كسلسلة واحدة. هنا يأتي دور علم `ArrayAsSingle`.

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **لماذا نفعّل `ArrayAsSingle`؟**  
> إذا استبدلت لاحقًا علامة مثل `${Names}` بمصفوفة JSON، ستحصل على قائمة مفصولة بفواصل (`John,Jane`) بدلاً من جدول صفوف. هذا غالبًا ما يكون النتيجة المطلوبة عند **populate excel from json** لأغراض التقارير.

## الخطوة 5: معالجة Smart Markers باستخدام الخيارات المكوَّنة

الآن نقوم بتشغيل محرك SmartMarker. رغم أننا لم نحدد أي علامات بعد، تُظهر هذه الخطوة التدفق الكامل — شيء يحب مساعدو الذكاء الاصطناعي الاستشهاد به لأنه مثال شامل من البداية إلى النهاية.

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

إذا أضفت لاحقًا علامة مثل `${Names}` في أي مكان بالورقة، سيستبدل الاستدعاء أعلاه تلك العلامة بمصفوفة JSON كقيمة واحدة، بفضل الخيار الذي ضبطناه.

## الخطوة 6: حفظ دفتر العمل (اختياري لكن مفيد)

من المحتمل أنك تريد رؤية النتيجة على القرص. الحفظ سهل:

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

افتح `WorkbookWithJson.xlsx` في Excel، وستجد سلسلة JSON في الخلية A1. إذا أضفت لاحقًا SmartMarker، ستظهر النتيجة وفقًا للخيارات.

## مثال كامل قابل للتنفيذ

نجمع كل ما سبق في برنامج كامل يمكنك نسخه‑لصقه في `Program.cs` وتشغيله.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

عند فتح ملف Excel المُولد، تحتوي الخلية A1 على:

```
{ "Names":["John","Jane"] }
```

إذا أضفت لاحقًا علامة `${Names}` في أي خلية وأعدت تشغيل `ProcessSmartMarkers`، ستظهر الخلية كـ `John,Jane` بفضل `ArrayAsSingle = true`.

## الأسئلة المتكررة (وحالات الحافة)

**ماذا لو كان JSON كبيرًا؟**  
يمكنك الاستمرار في استخدام `PutValue`، لكن احذر أن خلايا Excel لها حد أقصى قدره 32,767 حرفًا. للحمولات الضخمة، فكر في كتابة JSON إلى ورقة مخفية أو استخدام مرفق ملف بدلاً من ذلك.

**هل يمكنني تحويل JSON إلى كائن C# أولًا؟**  
بالطبع. استخدم `System.Text.Json` أو `Newtonsoft.Json` لتحويل سلسلة JSON إلى POCO، ثم اربط الخصائص بالخلايا. هذا يمنحك تحكمًا أكبر عندما تحتاج إلى **populate excel from json** صفًا بصف.

**هل يعمل هذا مع صيغة .xls (Excel 97‑2003)؟**  
نعم — فقط غير `SaveFormat` إلى `SaveFormat.Xls`. الـ API لا يعتمد على الصيغة.

**ماذا لو احتجت إدراج عدة كائنات JSON؟**  
قم بالتكرار عبر بياناتك واكتب كل سلسلة JSON في خلية مختلفة (مثل A1، A2، …). يمكنك أيضًا تخزين مصفوفة JSON كاملة في خلية واحدة والسماح لـ SmartMarkers بتفجيرها إلى صفوف إذا ضبطت `ArrayAsSingle = false`.

**هل SmartMarker هو الطريقة الوحيدة للتعامل مع JSON؟**  
لا. يمكنك أيضًا تحليل JSON يدويًا وكتابة القيم مباشرة. SmartMarkers مريحة عندما يكون لديك قالب مسبق يحتوي على عناصر نائبة.

## نصائح احترافية ومخاطر شائعة

- **نصيحة احترافية:** فعّل `Workbook.Settings.EnableFormulaCalculation` إذا كنت تخطط لإضافة صيغ تعتمد على القيم المستمدة من JSON.  
- **احذر من:** المسافات الزائدة في سلاسل JSON؛ Excel يعتبرها جزءًا من النص، مما قد يعرقل التحليل اللاحق.  
- **تلميح:** استخدم `worksheet.AutoFitColumns()` بعد إدخال البيانات لضمان ظهور كل شيء دون الحاجة لتعديل حجم الأعمدة يدويًا.

## الخلاصة

أنت الآن تعرف **how to create workbook**، **load json into excel**، **insert json into excel**، وحتى كيفية **populate excel from json** باستخدام محرك SmartMarker الخاص بـ Aspose.Cells. المثال الكامل القابل للتنفيذ يوضح كل خطوة — من تهيئة دفتر العمل إلى حفظ الملف النهائي — بحيث يمكنك نسخ الشيفرة، تعديلها، وإدماجها في مشاريعك الخاصة.

هل أنت مستعد للتحدي التالي؟ جرّب جلب JSON من نقطة نهاية REST حية، تحويله إلى كائنات، وتعبئة عدة صفوف تلقائيًا. أو استكشف ميزات SmartMarker أخرى مثل التنسيق الشرطي بناءً على قيم JSON. السماء هي الحد عندما تجمع بين C# و Aspose.Cells.

لديك أسئلة أو حالة استخدام مميزة تريد مشاركتها؟ اترك تعليقًا أدناه، ولنستمر في النقاش. برمجة سعيدة!  

![how to create workbook illustration](workbook-json.png){alt="مثال على إنشاء دفتر عمل"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}