---
category: general
date: 2026-06-24
description: إنشاء عدة أوراق باستخدام Aspose.Cells SmartMarker وتعلم كيفية إنشاء أوراق
  ديناميكية بسهولة في C#. دليل خطوة‑بخطوة مع الكود الكامل.
draft: false
keywords:
- generate multiple sheets
- create dynamic sheets
- Aspose.Cells SmartMarker
- C# Excel automation
- dynamic workbook generation
language: ar
og_description: إنشاء عدة أوراق باستخدام Aspose.Cells SmartMarker. تعلم كيفية إنشاء
  أوراق ديناميكية في C# مع مثال كامل قابل للتنفيذ.
og_title: إنشاء عدة أوراق باستخدام SmartMarker – دليل C# كامل
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Generate multiple sheets using Aspose.Cells SmartMarker and learn how
    to create dynamic sheets effortlessly in C#. Step‑by‑step tutorial with full code.
  headline: Generate Multiple Sheets with SmartMarker – Complete C# Guide
  type: TechArticle
- description: Generate multiple sheets using Aspose.Cells SmartMarker and learn how
    to create dynamic sheets effortlessly in C#. Step‑by‑step tutorial with full code.
  name: Generate Multiple Sheets with SmartMarker – Complete C# Guide
  steps:
  - name: Finds every `${}` tag in the worksheet.
    text: Finds every `${}` tag in the worksheet.
  - name: For each element in `data`, it clones the worksheet (or creates a new one)
      and populates the tags.
    text: For each element in `data`, it clones the worksheet (or creates a new one)
      and populates the tags.
  - name: Names the first clone “Detail”, the second “Detail_1”, the third “Detail_2”,
      and so on.
    text: Names the first clone “Detail”, the second “Detail_1”, the third “Detail_2”,
      and so on.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- Automation
title: إنشاء عدة أوراق باستخدام SmartMarker – دليل C# الكامل
url: /ar/net/smart-markers-dynamic-data/generate-multiple-sheets-with-smartmarker-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء أوراق متعددة باستخدام SmartMarker – دليل C# الكامل

هل احتجت يومًا إلى **إنشاء أوراق متعددة** من قالب واحد لكنك لم تكن متأكدًا من كيفية جعل العملية ديناميكية حقًا؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند العمل مع أتمتة Excel. لحسن الحظ، محرك **SmartMarker** في Aspose.Cells يجعل من السهل **إنشاء أوراق ديناميكية** في الوقت الفعلي، دون الحاجة لكتابة أي كود حلقة منخفض المستوى.

في هذا الدرس سنستعرض سيناريو واقعي: بدءًا من مصنف فارغ، إمداد مصدر بيانات صغير، والسماح لـ SmartMarker بإنشاء ورقة “Detail” وأي أوراق إضافية يحتاجها. في النهاية ستحصل على مقتطف جاهز للإنتاج يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

- كيفية إعداد مصدر بيانات بسيط يدفع إنشاء الأوراق  
- أي خصائص في `SmartMarkerOptions` تتحكم في تسمية الأوراق المُنشأة  
- استدعاءات API الدقيقة التي تُطلق **إنشاء أوراق متعددة** تلقائيًا  
- نصائح **لإنشاء أوراق ديناميكية** تتوسع مع نمو البيانات  
- الأخطاء الشائعة (مثل تصادم الأسماء) وكيفية تجنبها  

لا توجد مكتبات خارجية مطلوبة بخلاف Aspose.Cells، والكود يعمل مع .NET 6+ و .NET Framework 4.7.2 على حد سواء.

## المتطلبات المسبقة

- رخصة Aspose.Cells صالحة (أو مفتاح تقييم مؤقت)  
- Visual Studio 2022 أو أي بيئة تطوير C# تفضلها  
- إلمام أساسي بمجموعات C# ومبادئ تهيئة الكائنات  

هل لديك كل ذلك؟ عظيم—لنبدأ.

## الخطوة 1: إعداد مصدر البيانات لـ SmartMarker

SmartMarker يقرأ البيانات من أي كائن قابل للتعداد. لهذا العرض سنستخدم مصفوفة من الأنواع المجهولة، كل عنصر منها يمثل صفًا سيسبب ظهور ورقة جديدة.

```csharp
// Step 1: Prepare the data source for the smart markers
var data = new[]
{
    new { Id = 1 },
    new { Id = 2 }
};
```

**لماذا هذا مهم:** خاصية `Id` هي الحقل الوحيد الذي يحتاجه القالب، لكن يمكنك توسيع الكائن بعشرات الأعمدة. كل عنصر في المصفوفة يُطلق تكرار *detail*، والذي يترجمه SmartMarker إلى ورقة عمل منفصلة عندما تضبط الخيارات بشكل صحيح.

## الخطوة 2: ضبط خيارات SmartMarker – تسمية ورقة Detail

فئة `SmartMarkerOptions` تتيح لك تحديد كيفية تسمية المحرك للأوراق التي ينشئها. تعيين `DetailSheetNewName` إلى `"Detail"` يخبر SmartMarker بالبدء بهذا الاسم وإضافة فهرس تلقائيًا للأوراق اللاحقة.

```csharp
// Step 2: Set up SmartMarker options (e.g., name for the first detail sheet)
var options = new SmartMarkerOptions
{
    // The base name for the first generated sheet.
    DetailSheetNewName = "Detail"
};
```

**نصيحة محترف:** إذا تركت هذه الخاصية، سيعيد SmartMarker استخدام اسم ورقة العمل الأصلي، ولن ترى تأثير **إنشاء أوراق متعددة**. تسمية الورقة الأساسية تساعد أيضًا الكود اللاحق على العثور على الألسنة التي تم إنشاؤها حديثًا.

## الخطوة 3: إنشاء مصنف جديد لاستضافة الناتج

يمكنك البدء من ملف قالب أو من مصنف جديد تمامًا. هنا ننشئ مصنفًا فارغًا، يحتوي بالفعل على ورقة عمل افتراضية واحدة (الفهرس 0). ستعمل هذه الورقة كـ *الماستر* حيث توجد علامات SmartMarker.

```csharp
// Step 3: Create a new workbook that will receive the generated sheets
var workbook = new Workbook(); // starts with one blank sheet named "Sheet1"
```

إذا كان لديك قالب مُصمم مسبقًا (مثلاً يحتوي على رؤوس، صيغ، أو تنسيقات)، فقط حمّله باستخدام `new Workbook("Template.xlsx")` بدلاً من ذلك. باقي العملية يبقى كما هو.

## الخطوة 4: تشغيل معالجة SmartMarker على الورقة الأولى

الآن يأتي السطر السحري الذي يخبر Aspose.Cells بفحص الورقة بحثًا عن علامات SmartMarker، استبدالها بالبيانات، و**إنشاء أوراق متعددة** حسب الحاجة.

```csharp
// Step 4: Run SmartMarker processing on the first worksheet using the data and options
workbook.Worksheets[0].SmartMarkerProcessing(data, options);
```

ما يحدث في الخلفية:

1. يجد كل علامة `${}` في الورقة.  
2. لكل عنصر في `data`، ينسخ الورقة (أو ينشئ ورقة جديدة) ويملأ العلامات.  
3. يطلق على النسخة الأولى اسم “Detail”، والثانية “Detail_1”، والثالثة “Detail_2”، وهكذا.

### التحقق من النتيجة

بعد الاستدعاء، يمكنك فحص المصنف برمجيًا أو حفظه على القرص:

```csharp
// Save to verify the generated sheets
workbook.Save("GeneratedMultipleSheets.xlsx", SaveFormat.Xlsx);

// Optional: List sheet names to the console for quick debugging
foreach (var sheet in workbook.Worksheets)
{
    Console.WriteLine(sheet.Name);
}
```

تشغيل المقتطف يطبع:

```
Detail
Detail_1
```

… وملف Excel يحتوي على ورقتين منسقتين تمامًا—كل واحدة تمثل عنصرًا في مصفوفة `data`.

## الخطوة 5: توسيع المثال – بيانات وقوالب أكثر تعقيدًا

النمط الأساسي يتوسع بسهولة. افترض أنك تحتاج لإضافة عمود ثانٍ، `Name`، وصف صف رأس يظهر في كل ورقة. فقط أغنِ مصدر البيانات وعدّل القالب:

```csharp
var data = new[]
{
    new { Id = 1, Name = "Alice" },
    new { Id = 2, Name = "Bob" },
    new { Id = 3, Name = "Charlie" }
};
```

في ورقة القالب، ضع علامات SmartMarker مثل `${Name}` و `${Id}` في أي موضع تريد ظهور القيم فيه. سيستمر SmartMarker في **إنشاء أوراق ديناميكية** لكل إدخال، مسميًا إياها `Detail`, `Detail_1`, `Detail_2`, إلخ.

**تحذير حالة حافة:** إذا كان لديك أكثر من 255 ورقة، سيُطلق Excel استثناءً. في مثل هذه السيناريوهات، فكر في تجميع البيانات إلى دفعات أو استخدام ورقة واحدة مع جدول بدلاً من أوراق منفصلة.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **تكرار أسماء الأوراق** | نسيان ضبط `DetailSheetNewName` أو إعادة استخدام اسم موجود | احرص دائمًا على ضبط اسم أساسي فريد أو تحقق من وجود الاسم باستخدام `workbook.Worksheets.Exists(name)` قبل المعالجة |
| **غياب علامات SmartMarker** | القالب لا يحتوي على أي عناصر `${}`، لذا لا شيء يُستبدل | أدرج على الأقل علامة واحدة؛ حتى `${Id}` تجري عملية إنشاء الورقة |
| **تباطؤ الأداء مع مجموعات بيانات ضخمة** | كل صف بيانات يُنشئ ورقة عمل جديدة، ما يستهلك الذاكرة | عالج البيانات على دفعات، أو اكتب إلى ورقة واحدة باستخدام جدول إذا تجاوزت بضع مئات صفوف |
| **انتهاء صلاحية الرخصة** | وضع التقييم يضيف علامة مائية على الملفات المُولدة | طبّق رخصة Aspose.Cells صالحة مبكرًا في تطبيقك (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) |

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare data source
        var data = new[]
        {
            new { Id = 1 },
            new { Id = 2 }
        };

        // 2️⃣ Configure SmartMarker options – this is what makes us **generate multiple sheets**
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 3️⃣ Create a fresh workbook (or load a template)
        var workbook = new Workbook(); // starts with a default sheet named "Sheet1"

        // 4️⃣ Insert a simple SmartMarker tag into the first worksheet for demo purposes
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Record ID: ${Id}");

        // 5️⃣ Run SmartMarker processing – the engine will **create dynamic sheets** automatically
        sheet.SmartMarkerProcessing(data, options);

        // 6️⃣ Save the result so you can open it in Excel
        workbook.Save("GenerateMultipleSheetsDemo.xlsx", SaveFormat.Xlsx);

        // 7️⃣ Quick verification output
        Console.WriteLine("Generated sheets:");
        foreach (var ws in workbook.Worksheets)
            Console.WriteLine($"- {ws.Name}");
    }
}
```

**الناتج المتوقع** عند فتح `GenerateMultipleSheetsDemo.xlsx`:

- الورقة **Detail** تحتوي على “Record ID: 1” في الخلية A1.  
- الورقة **Detail_1** تحتوي على “Record ID: 2” في الخلية A1.

سيسرد الطرفية:

```
Generated sheets:
- Detail
- Detail_1
```

هذا هو سير العمل الكامل **لإنشاء أوراق متعددة** و**إنشاء أوراق ديناميكية** باستخدام SmartMarker.

## الخلاصة

غطينا كل ما تحتاجه **لإنشاء أوراق متعددة** باستخدام Aspose.Cells SmartMarker، من إعداد البيانات إلى قواعد التسمية والتحقق النهائي. الفكرة الأساسية بسيطة: أعطِ SmartMarker مجموعة، حدّد الاسم الأساسي الذي تريده، ودع المحرك يتولى الباقي. لا نسخ يدوي، لا استدعاءات `Copy` معقدة—فقط كود نظيف وقابل للصيانة.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة مخططات، تنسيقات شرطية، أو حتى تضمين صور في كل ورقة تم إنشاؤها ديناميكيًا. أو استكشف مجموعة ميزات Aspose.Cells الأوسع مثل **التصفية التلقائية**، **جداول المحور**، و**تصدير PDF**—جميعها يعمل بانسجام مع الأوراق التي أنشأتها للتو.

إذا واجهت أي صعوبة، اترك تعليقًا أدناه أو راجع الوثائق الرسمية لـ Aspose.Cells لتفاصيل أعمق حول `SmartMarkerOptions`. برمجة سعيدة، ولتظل مصنفاتك دائمًا منظمة! 

![مخطط يوضح التدفق من مصفوفة البيانات → معالجة SmartMarker → أوراق عمل متعددة](/images/generate-multiple-sheets-diagram.png "إنشاء أوراق متعددة باستخدام SmartMarker")


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية دمج وإعادة تسمية أوراق Excel باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [كيفية دمج أوراق Excel في ملف نصي واحد باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)
- [تحويل أوراق Excel إلى ملفات PDF باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/convert-excel-sheets-to-pdfs-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}