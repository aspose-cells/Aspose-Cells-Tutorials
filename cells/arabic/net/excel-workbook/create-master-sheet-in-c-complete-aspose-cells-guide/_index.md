---
category: general
date: 2026-03-30
description: إنشاء ورقة رئيسية باستخدام Aspose.Cells في C#. تعلم كيفية إنشاء دفتر
  عمل Excel في C#، السماح بأسماء الأوراق المكررة وحفظ دفتر العمل كملف XLSX في بضع
  خطوات.
draft: false
keywords:
- create master sheet
- create excel workbook c#
- save workbook as xlsx
- allow duplicate sheet names
language: ar
og_description: إنشاء ورقة رئيسية باستخدام Aspose.Cells في C#. يوضح هذا الدليل كيفية
  إنشاء مصنف Excel في C#، السماح بأسماء أوراق مكررة، وحفظ المصنف بصيغة XLSX.
og_title: إنشاء ورقة رئيسية في C# – دليل Aspose.Cells الكامل
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء ورقة رئيسية في C# – دليل Aspose.Cells الكامل
url: /ar/net/excel-workbook/create-master-sheet-in-c-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ورقة رئيسية في C# – دليل كامل لـ Aspose.Cells

هل احتجت يومًا إلى **create master sheet** في ملف Excel لكنك لم تكن متأكدًا من كيفية التعامل مع مجموعة من أوراق التفاصيل التي تشترك في نفس الاسم الأساسي؟ لست وحدك. في العديد من سيناريوهات التقارير تنتهي بك الأمور إلى وجود عشرات من علامات تبويب التفاصيل، والسلوك الافتراضي لمعظم المكتبات هو إلقاء استثناء عندما ينتهي الأمر بورقتين بنفس الاسم.  

لحسن الحظ، تجعل Aspose.Cells الأمر سهلًا لإنشاء **create master sheet**, وتكوين المحرك للسماح **allow duplicate sheet names**, ثم **save workbook as XLSX**—كل ذلك من كود C# نظيف. في هذا الدرس سنستعرض مثالًا قابلاً للتنفيذ بالكامل، ونشرح لماذا كل سطر مهم، ونقدم لك مجموعة من النصائح التي يمكنك نسخها مباشرةً إلى مشاريعك.

> **ما ستحصل عليه**  
> * كيف **create Excel workbook C#**‑style باستخدام Aspose.Cells.  
> * كيف تضمّن smart‑marker الذي ينشئ ورقة تفاصيل لكل صف بيانات.  
> * كيف تضبط `DetailSheetNewName = DuplicateAllowed` بحيث تقوم المكتبة تلقائيًا بإضافة لاحقة رقمية.  
> * كيف **save workbook as XLSX** على القرص دون أي خطوات إضافية.

لا حاجة إلى وثائق خارجية—كل ما تحتاجه موجود هنا.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أنك تمتلك:

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث (أو .NET Framework 4.7+) | Aspose.Cells 23.x+ تستهدف هذه البيئات. |
| Visual Studio 2022 (أو أي بيئة تطوير C#) | لتسهيل إنشاء المشروع وتصحيح الأخطاء. |
| Aspose.Cells for .NET حزمة NuGet (`Install-Package Aspose.Cells`) | المكتبة التي تشغّل كل سحر الـ smart‑marker. |
| معرفة أساسية بـ C# | ستفهم الصياغة دون الحاجة إلى دورة سريعة. |

إذا كنت تفتقد أيًا منها، أضفها الآن—ليس هناك فائدة من المتابعة ببيئة غير مكتملة.

## الخطوة 1: إنشاء ورقة رئيسية باستخدام Aspose.Cells

أول شيء نفعله هو **create Excel workbook C#**‑style عن طريق إنشاء كائن `Workbook`. هذا الكائن يحتوي بالفعل على ورقة عمل افتراضية، سنعيد تسميتها إلى “Master” ونتعامل معها كقالب لجميع صفحات التفاصيل.

```csharp
using Aspose.Cells;

// Step 1: Initialise a new workbook – this automatically gives us one sheet
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet that comes with a fresh workbook
Worksheet masterSheet = workbook.Worksheets[0];

// Give it a meaningful name – this will be our master sheet
masterSheet.Name = "Master";
```

*لماذا إعادة تسمية الورقة؟*  
اسم افتراضي مثل “Sheet1” لا يعكس الغرض، ولاحقًا عندما تفحص الملف ستريد أن تكون علامة التبويب الرئيسية معروفة على الفور. التسمية أيضًا تمنع التصادمات العرضية عندما تضيف أوراقًا أخرى لاحقًا.

## الخطوة 2: إعداد الـ smart‑marker الذي سيولد أوراق تفاصيل

الـ smart‑markers هي نواقل مكانية تستبدلها Aspose.Cells بالبيانات أثناء التشغيل. بوضع `{{#detail:DataSheetName}}` في الخلية **A1**، نخبر المحرك: “لكل سجل في مصدر البيانات، أنشئ ورقة جديدة يُستمد اسمها من الحقل `DataSheetName`.”

```csharp
// Step 2: Insert a smart‑marker into cell A1.
// The marker #detail tells Aspose.Cells to generate a new sheet per data row.
masterSheet.Cells["A1"].PutValue("{{#detail:DataSheetName}}");
```

فكر في العلامة كبطاقة تعليمات صغيرة ملصقة على ورقة العمل. عندما يعمل المعالج، يقرأ البطاقة، يجلب القيمة المناسبة من مصدر البيانات، ثم ينسخ ورقة الـ master إلى علامة تبويب جديدة.

## الخطوة 3: بناء مصدر البيانات – أسماء أوراق مكررة عن قصد

في الواقع قد تجلب هذا من قاعدة بيانات، لكن للعرض سنستخدم مصفوفة في الذاكرة من كائنات مجهولة. لاحظ أن العنصرين يستخدمان نفس الاسم الأساسي `"Detail"`؛ هذا هو السيناريو الذي يصبح فيه **allow duplicate sheet names** أمرًا حاسمًا.

```csharp
// Step 3: Create a data source with two items that share the same base sheet name.
var dataSource = new[]
{
    new { DataSheetName = "Detail" },
    new { DataSheetName = "Detail" }
};
```

إذا جربت ذلك دون أي خيارات خاصة، ستطلق Aspose.Cells استثناءً في التكرار الثاني لأن ورقة باسم “Detail” موجودة بالفعل. لهذا السبب الخطوة التالية مهمة.

## الخطوة 4: تمكين أسماء الأوراق المكررة

Aspose.Cells تعرض `SmartMarkerOptions.DetailSheetNewName`. ضبطه إلى `DetailSheetNewName.DuplicateAllowed` يخبر المحرك بإضافة لاحقة رقمية تلقائيًا (مثال: “Detail_1”) كلما حدث تعارض في الاسم.

```csharp
// Step 4: Configure SmartMarker options to permit duplicate sheet names.
var smartMarkerOptions = new SmartMarkerOptions
{
    // This makes the library rename clashes to "Detail_1", "Detail_2", etc.
    DetailSheetNewName = DetailSheetNewName.DuplicateAllowed
};
```

*لماذا لا نعطي كل صف اسمًا فريدًا يدويًا؟*  
لأن البيانات المصدرية غالبًا لا تضمن التفرد، خاصةً عندما يُدخل المستخدمون نصًا حرًا. السماح للمكتبة بالتعامل مع اللاحقة يزيل فئة كاملة من الأخطاء.

## الخطوة 5: معالجة الـ smart‑markers وإنشاء أوراق التفاصيل

الآن نستدعي `SmartMarkers.Process`، مع تمرير كل من مصدر البيانات والخيارات التي قمنا بتكوينها. الطريقة تمر عبر كل عنصر، تنسخ ورقة الـ master، وتعيد تسمية النسخة وفقًا لحقل `DataSheetName` (مع إضافة لاحقة إذا لزم الأمر).

```csharp
// Step 5: Run the smart‑marker processor – this creates the detail sheets.
masterSheet.SmartMarkers.Process(dataSource, smartMarkerOptions);
```

بعد تنفيذ هذا السطر ستحصل على ثلاث علامات تبويب في المصنف:

1. **Master** – القالب الأصلي.  
2. **Detail** – أول ورقة تم إنشاؤها (لا حاجة لللاحقة).  
3. **Detail_1** – الورقة الثانية (تمت إضافة اللاحقة تلقائيًا).

يمكنك التحقق من ذلك بفتح الملف في Excel؛ سترى ورقتي التفاصيل جنبًا إلى جنب.

## الخطوة 6: حفظ المصنف كملف XLSX

أخيرًا، نقوم بحفظ الملف على القرص. طريقة `Save` تختار تلقائيًا تنسيق XLSX عندما تعطيها امتداد `.xlsx`.

```csharp
// Step 6: Persist the workbook – this is the moment we finally “save workbook as XLSX”.
string outputPath = @"C:\Temp\DuplicateDetailSheets.xlsx";
workbook.Save(outputPath);
```

**نصيحة احترافية:** إذا كنت بحاجة إلى بث الملف مباشرةً إلى استجابة ويب (مثل ASP.NET Core)، استخدم `workbook.Save(stream, SaveFormat.Xlsx)` بدلاً من مسار ملف.

## مثال كامل يعمل

أدناه البرنامج الكامل الجاهز للتنفيذ. انسخه إلى تطبيق Console، اضغط F5، وافتح الملف الناتج لرؤية النتيجة.

```csharp
using System;
using Aspose.Cells;

namespace MasterSheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and rename the default sheet to "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // 2️⃣ Insert a smart‑marker that will generate a detail sheet per data row
            masterSheet.Cells["A1"].PutValue("{{#detail:DataSheetName}}");

            // 3️⃣ Prepare a data source where two rows share the same sheet name
            var dataSource = new[]
            {
                new { DataSheetName = "Detail" },
                new { DataSheetName = "Detail" }
            };

            // 4️⃣ Allow duplicate sheet names – the library will add "_1", "_2", …
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = DetailSheetNewName.DuplicateAllowed
            };

            // 5️⃣ Process the smart‑markers; this creates the detail sheets
            masterSheet.SmartMarkers.Process(dataSource, smartMarkerOptions);

            // 6️⃣ Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\DuplicateDetailSheets.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**النتيجة المتوقعة:** افتح `DuplicateDetailSheets.xlsx` وسترى ثلاث أوراق عمل—`Master`، `Detail`، و`Detail_1`. كل ورقة تفاصيل هي نسخة مطابقة من الـ master، جاهزة لتملأها ببيانات الصفوف لاحقًا.

## أسئلة شائعة وحالات حافة

### ماذا لو احتجت إلى أكثر من ورقتين مكررتين؟

لا مشكلة. الإعداد `DuplicateAllowed` نفسه سيستمر في إضافة أرقام تزايدية (`Detail_2`, `Detail_3`, …) حتى يحصل كل صف على علامة تبويب خاصة به.

### هل يمكنني تخصيص تنسيق اللاحقة؟

بشكل افتراضي، تستخدم Aspose.Cells شرطة سفلية تليها رقم. إذا كنت تحتاج نمطًا مختلفًا (مثال: “Detail‑A”، “Detail‑B”)، سيتعين عليك معالجة المصنف بعد تشغيل `Process`، بالت iterating على `workbook.Worksheets` وإعادة التسمية حسب ما تراه مناسبًا.

### هل يعمل هذا النهج مع مجموعات بيانات كبيرة (مئات الصفوف)؟

نعم، لكن راقب استهلاك الذاكرة. كل ورقة مُولدة هي نسخة كاملة من الـ master، لذا عدد كبير من الصفوف قد يزيد حجم الملف بسرعة. إذا كنت تحتاج فقط إلى عدد قليل من الصفوف لكل ورقة، فكر في استخدام `SmartMarkerOptions.RemoveEmptyRows = true` لتقليل الخلايا الزائدة.

### هل الملف المُولد فعلاً ملف XLSX؟

بالتأكيد. طريقة `Save` تكتب حزمة Open XML التي يتوقعها Excel. يمكنك حتى فتح الملف باستخدام LibreOffice أو Google Sheets دون أي تحويل.

## نصائح لكود جاهز للإنتاج

| نصيحة | لماذا يهم |
|-----|----------------|
| **Dispose `Workbook

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}