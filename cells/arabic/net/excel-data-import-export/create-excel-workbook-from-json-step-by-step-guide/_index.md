---
category: general
date: 2026-03-25
description: إنشاء مصنف إكسل من JSON وحفظ المصنف بصيغة xlsx. تعلّم كيفية تصدير JSON
  إلى xlsx، إنشاء إكسل من JSON، وتعبئة إكسل من JSON في دقائق.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: ar
og_description: إنشاء مصنف إكسل من JSON فورًا. يوضح هذا الدليل كيفية تصدير JSON إلى
  XLSX، وإنشاء إكسل من JSON، وتعبئة إكسل من JSON باستخدام Aspose.Cells.
og_title: إنشاء دفتر عمل Excel من JSON – دليل C# الكامل
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: إنشاء دفتر عمل إكسل من JSON – دليل خطوة بخطوة
url: /ar/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel من JSON – دليل C# كامل

هل احتجت يومًا إلى **إنشاء مصنف Excel** من حمولة JSON لكنك لم تكن متأكدًا من أين تبدأ؟ أنت لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عندما يحاولون تحويل بيانات API إلى جدول بيانات مرتب. الأخبار السارة؟ باستخدام بضع أسطر من C# و Aspose.Cells يمكنك **export json to xlsx**، **generate excel from json**، و **populate excel from json** دون الحاجة إلى محولات من طرف ثالث.

في هذا الدليل سنستعرض العملية بالكامل—بدءًا من سلسلة JSON خام، وإدراجها في SmartMarker، وأخيرًا **save workbook as xlsx** على القرص. في النهاية ستحصل على ملف Excel جاهز للاستخدام يبدو هكذا:

| الاسم | النتيجة |
|------|-------|
| John | 90    |
| Anna | 85    |

> **نصيحة احترافية:** إذا كنت تستخدم Aspose.Cells بالفعل في مكان آخر في مشروعك، يمكنك إعادة استخدام نفس كائن `Workbook` لاستيراد JSON متعدد—مفيد للمعالجة الدفعية.

## ما ستحتاجه

- **.NET 6+** (أو أي إطار .NET حديث يدعم C# 10)
- **Aspose.Cells for .NET** – تثبيت عبر NuGet: `dotnet add package Aspose.Cells`
- فهم أساسي لصياغة C# (لا يتطلب معرفة عميقة بـ Excel)

هذا كل شيء. لا خدمات خارجية، لا تفاعل COM، مجرد كود مُدار نقي.

## الخطوة 1: تهيئة مصنف Excel جديد

الأول الذي نفعله هو إنشاء كائن مصنف جديد. فكر فيه كفتح ملف Excel فارغ حيث سنضع بياناتنا لاحقًا.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

لماذا نبدأ بمصنف جديد؟ يضمن لك لوحة نظيفة، يمنع بقاء الأنماط من تشغيلات سابقة، ويحافظ على حجم الملف بأقل قدر—مثالي لأنابيب العمل الآلية.

## الخطوة 2: إعداد بيانات JSON التي تريد استيرادها

للتوضيح سنستخدم مصفوفة JSON صغيرة، لكن يمكنك استبدالها بأي JSON صالح تحصل عليه من خدمة ويب، ملف، أو استعلام قاعدة بيانات.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

لاحظ علامات الاقتباس المزدوجة المت_ESCAPE (`\"`)—هذا مجرد صياغة سلسلة نصية في C#. في سيناريو واقعي ربما تقرأ هذا من ملف:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## الخطوة 3: إخبار SmartMarker بمعالجة المصفوفة بالكامل كسجل واحد

محرك SmartMarker في Aspose.Cells يمكنه التكرار على المجموعات تلقائيًا. بتمكين **ArrayAsSingle**، نتعامل مع مصفوفة JSON بالكامل كسجل واحد، وهذا بالضبط ما نحتاجه لجدول مسطح.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

إذا نسيت هذا العلم، سيحاول SmartMarker إنشاء ورقة منفصلة لكل عنصر—وهذا بالتأكيد ليس ما تريد عند إنشاء جدول بسيط.

## الخطوة 4: وضع رمز SmartMarker في ورقة العمل

رموز SmartMarker تبدو هكذا `${jsonArray}`. عندما يعمل المعالج، يستبدل الرمز بالبيانات من مصدر JSON. سنضع الرمز في الخلية **A1** بحيث يبدأ الإخراج من الزاوية العليا اليسرى.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

يمكنك أيضًا تنسيق صف العنوان مسبقًا قبل المعالجة. على سبيل المثال، اجعل الخط عريضًا في الصف الأول:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## الخطوة 5: تشغيل معالج SmartMarker

الآن يحدث السحر. يقرأ المعالج JSON، يطابق كل خاصية بعمود، ويكتب الصفوف تحت الرمز.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

خلف الكواليس، تقوم Aspose.Cells بـ:

1. تحليل JSON إلى كائن .NET.
2. مطابقة أسماء الخصائص (`Name`, `Score`) مع عناوين الأعمدة.
3. كتابة كل عنصر من المصفوفة كصف جديد.

إذا كان JSON الخاص بك يحتوي على كائنات متداخلة، يمكنك الإشارة إليها باستخدام تدوين النقطة (`${parent.child}`) – ميزة مفيدة لتقارير أكثر تعقيدًا.

## الخطوة 6: حفظ المصنف كملف XLSX

أخيرًا، احفظ المصنف على القرص. امتداد الملف `.xlsx` يخبر Excel (ومعظم تطبيقات الجداول الأخرى) أن هذا مصنف OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

بالطبع يمكنك بث المصنف مباشرةً إلى استجابة HTTP إذا كنت تبني واجهة برمجة تطبيقات ويب:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يدمج كل خطوة سابقة. انسخه إلى مشروع وحدة تحكم جديد واضغط **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**النتيجة المتوقعة:** فتح `json-single.xlsx` يظهر صفين تحت العنوان العريض—`John` بنتيجة `90` و`Anna` بـ `85`. يتم استنتاج أسماء الأعمدة تلقائيًا من أسماء خصائص JSON.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت مفاتيح JSON تحتوي على مسافات أو أحرف خاصة؟

SmartMarker يتوقع أسماء معرفات صالحة. استبدل المسافات بشرطات سفلية أو استخدم تعيينًا مخصصًا:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### كيف يمكنني تصدير مصفوفة JSON كبيرة (آلاف الصفوف)؟

المعالج يبث البيانات داخليًا، لذا يبقى استهلاك الذاكرة معتدلًا. ومع ذلك قد ترغب في:

- زيادة حد `MaxRows` للورقة (`worksheet.Cells.MaxRow = 1_048_576;` – الحد الأقصى في Excel).
- إيقاف خطوط الشبكة للأداء (`worksheet.IsGridlinesVisible = false;`).

### هل يمكنني إضافة جداول JSON متعددة إلى نفس المصنف؟

بالتأكيد. ضع رموز SmartMarker مختلفة في نطاقات منفصلة (مثال، `${orders}` في `A10`، `${customers}` في `D1`) واستدعِ `Process` مرة لكل رمز أو مرة واحدة مع كائن JSON مركب يحتوي على كلا المصفوفتين.

## مكافأة: إضافة مخطط بسيط (اختياري)

إذا أردت تصور النتائج، أضف مخطط عمودي سريع بعد ملء البيانات:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

سوف يشير المخطط تلقائيًا إلى الصفوف المضافة حديثًا، مما يمنحك تقريرًا مصقولًا في خطوة واحدة.

## الخلاصة

أنت الآن تعرف **how to create excel workbook** من سلسلة JSON، **export json to xlsx**، **generate excel from json**، و**populate excel from json** باستخدام ميزة SmartMarker في Aspose.Cells. الحل الكامل—تهيئة المصنف، ضبط SmartMarker، معالجة JSON، وحفظ الملف—يُكتب في بضع أسطر فقط، لكنه يتوسع ليعالج مجموعات بيانات ضخمة.

ما الخطوات التالية؟ جرّب استبدال JSON الثابت بنداء API، أضف تنسيقًا شرطيًا بناءً على النتائج، أو أنشئ أوراقًا متعددة لمجالات بيانات مختلفة. النمط نفسه يعمل مع CSV، XML، أو حتى نتائج قاعدة البيانات—فقط غير سلسلة المصدر واضبط رمز SmartMarker.

برمجة سعيدة، ولتظل جداولك دائمًا مرتبة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}