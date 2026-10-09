---
category: general
date: 2026-03-18
description: تعلم كيفية إنشاء ملف Excel من JSON باستخدام C#، السماح بأسماء أوراق مكررة،
  إنشاء ورقة تفاصيل، وحفظ المصنف بـ C# في دقائق.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: ar
og_description: إنشاء ملف Excel من JSON باستخدام C#. يوضح هذا الدليل كيفية السماح
  بأسماء أوراق مكررة، وإنشاء ورقة تفاصيل، وحفظ المصنف باستخدام C# مع Aspose.Cells.
og_title: إنشاء ملف إكسل من JSON في C# – دليل كامل
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: إنشاء إكسل من JSON في C# – دليل خطوة بخطوة
url: /ar/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف Excel من JSON في C# – دليل خطوة بخطوة

هل احتجت يوماً إلى **إنشاء Excel من JSON** لكن لم تكن متأكدًا من المكتبة التي يمكنها إنجاز المهمة؟ لست وحدك. في العديد من تطبيقات المؤسسات نستقبل البيانات على شكل JSON ويجب نقلها إلى جداول إكسل منسقة—مثل تقارير المبيعات، تصدير المخزون، أو سجلات التدقيق. الخبر السار؟ باستخدام محرك SmartMarker في Aspose.Cells يمكنك تحويل سلسلة JSON إلى ملف Excel كامل في بضع أسطر فقط.

في هذا الدرس سنستعرض العملية بالكامل: من إعداد حمولة JSON، إلى تكوين SmartMarker للسماح بأسماء أوراق مكررة، وإنشاء **ورقة تفاصيل**، وأخيرًا **حفظ المصنف** بأسلوب C#. في النهاية ستحصل على مقطع شفرة يمكن إدراجه في أي مشروع .NET.

> **ملخص سريع:**  
> • الهدف الأساسي – إنشاء Excel من JSON.  
> • الأهداف الثانوية – السماح بأسماء أوراق مكررة، إنشاء ورقة تفاصيل، حفظ المصنف بـ C#.  

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK (أو أي نسخة حديثة من .NET).  
- Visual Studio 2022 أو VS Code مع امتداد C#.  
- ترخيص فعال أو نسخة تجريبية مجانية من **Aspose.Cells for .NET** (حزمة NuGet هي `Aspose.Cells`).  
- ملف قالب Excel (`template.xlsx`) يحتوي مسبقًا على علامات SmartMarker مثل `&=Name` ومكان لحجز جدول التفاصيل.

إذا كان أي من ذلك غير مألوف لك، لا تقلق—تثبيت حزمة NuGet يتم بأمر واحد، ويمكن أن يكون القالب مجرد مصنف عادي يحتوي على بعض الخلايا النائبة.

## نظرة عامة على الحل

على مستوى عالٍ سنقوم بـ:

1. تعريف سلسلة JSON تعكس البيانات التي نريدها في الورقة.  
2. إعداد `SmartMarkerOptions` للسماح بأسماء أوراق مكررة وتحديد اسم **ورقة التفاصيل** بشكل متوقع.  
3. تحميل قالب Excel الذي يحتوي على علامات SmartMarker.  
4. تشغيل معالج SmartMarker لدمج بيانات JSON في المصنف.  
5. حفظ الملف النهائي باستخدام `workbook.Save(...)`.

كل خطوة موضحة أدناه، مع مقاطع شفرة كاملة وشرح لماذا هذه الخطوة مهمة.

---

## الخطوة 1 – إعداد حمولة JSON التي ستدمجها

أول شيء تحتاجه هو مستند JSON يتطابق مع علامات SmartMarker داخل القالب. فكر في JSON كمصدر الحقيقة؛ كل مفتاح يصبح نائبا في ملف Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**لماذا هذا مهم:**  
SmartMarker يقرأ هيكلية JSON ويوسع الجداول تلقائيًا للمجموعات مثل `Orders`. إذا لم يتطابق هيكل JSON مع العلامات، سيؤدي الدمج إلى إنتاج صفوف فارغة—وهو خطأ شائع.

---

## الخطوة 2 – تكوين SmartMarker للسماح بأسماء أوراق مكررة وتسمية ورقة التفاصيل

بشكل افتراضي، يمنع Aspose.Cells وجود أسماء أوراق مكررة، مما قد يعيقك عند إنشاء ورقة تفاصيل لكل سجل رئيسي. تسمح لك فئة `SmartMarkerOptions` بتخفيف هذا القيد وتحديد نمط تسمية للأوراق التفصيلية الجديدة.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**لماذا هذا مهم:**  
إذا كنت تتكرر عبر عدة عملاء وكل تكرار ينشئ ورقة جديدة، فإن المحرك عادةً ما يرمي استثناءً. ضبط `AllowDuplicateSheetNames` إلى `true` يخبر Aspose.Cells بإضافة لاحقة رقمية تلقائيًا، مما يبقي العملية سلسة.

---

## الخطوة 3 – تحميل قالب Excel الذي يحتوي على علامات SmartMarker

قالبك هو القماش الذي سيُرسم عليه SmartMarker البيانات. يمكن أن يحتوي على أي تنسيق—ألوان، صيغ، مخططات—حتى لا تحتاج إلى إعادة إنشاء هذه المنطق برمجيًا.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**نصيحة:**  
احتفظ بالقالب في مجلد جزء من مخرجات مشروعك (مثلاً `Content\Templates`). بهذه الطريقة يمكنك الإشارة إليه بمسار نسبي وتجنب كتابة مسارات مطلقة صلبة.

---

## الخطوة 4 – تشغيل معالج SmartMarker مع JSON والخيارات

الآن يحدث السحر. يقرأ `SmartMarkerProcessor` الـ JSON، يطبق الخيارات التي ضبطتها، ويملأ المصنف وفقًا لذلك.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**ما الذي يحدث خلف الكواليس؟**  
- يقوم المعالج بمسح كل خلية بحثًا عن علامات مثل `&=Name` أو `&=Orders.Item`.  
- يستبدل العلامات البسيطة بقيم عددية (`Name`, `Date`).  
- للمجموعات (`Orders`)، ينشئ ورقة تفاصيل جديدة (اسمها “Detail”) ويملأ صفًا في الجدول لكل عنصر.  
- لأننا سمحنا بأسماء أوراق مكررة، إذا كان القالب يحتوي بالفعل على ورقة باسم “Detail”، سيخلق المحرك ورقة “Detail (2)”.

---

## الخطوة 5 – حفظ المصنف المدمج إلى القرص

أخيرًا، اكتب المصنف المملوء إلى ملف. يمكنك اختيار أي تنسيق يدعمه Aspose.Cells—XLSX، CSV، PDF، إلخ. هنا سنبقى مع XLSX الحديث.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**لماذا هذا مهم:**  
الحفظ هو المكان الذي تقوم فيه فعليًا **بحفظ المصنف بأسلوب C#**. إذا احتجت إلى بث الملف إلى عميل ويب، يمكنك استخدام `workbook.Save(Stream, SaveFormat.Xlsx)` بدلاً من ذلك.

---

## مثال كامل يعمل

بجمع كل شيء معًا، إليك تطبيق console كامل جاهز للتنفيذ. تأكد من تثبيت حزمة NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) قبل التجميع.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

- **الورقة 1** (الورقة الرئيسية) ستظهر “John” في خلية `Name` و “2023‑01‑01” في خلية `Date`.  
- ستظهر ورقة **Detail** جديدة، تحتوي على جدول بصفين: أحدهما لأمر Laptop والآخر لأمر Mouse.  
- إذا كان القالب يحتوي بالفعل على ورقة باسم “Detail”، ستُسمى الورقة الجديدة “Detail (2)”، بفضل علم `AllowDuplicateSheetNames`.

![Excel output showing master sheet with name and date, plus a Detail sheet with order rows](excel-output.png "generate excel from json result")

*نص بديل للصورة:* **إنشاء Excel من JSON – مثال لمصنف يحتوي على ورقة رئيسية وتفصيلية**

---

## أسئلة شائعة وحالات حافة

### ماذا لو كان JSON يحتوي على مجموعات متداخلة؟

يمكن لـ SmartMarker التعامل مع المصفوفات المتداخلة، لكن سيتعين عليك إضافة أوراق تفاصيل إضافية أو استخدام علامات هرمية. على سبيل المثال، `&=Orders.SubItems.Product` سيولد ورقة من المستوى الثالث تلقائيًا.

### كيف أُخصص نمط تسمية الأوراق المكررة؟

بدلاً من `DetailSheetNewName` ثابت، يمكنك تعيين رد نداء عبر `smartMarkerOptions.DetailSheetNameGenerator`. يتيح لك ذلك دمج طوابع زمنية أو معرفات فريدة في اسم الورقة.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### هل يمكنني إنشاء CSV بدلاً من XLSX؟

بالطبع. استبدل استدعاء `Save` النهائي بـ:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

يبقى باقي الخطوات كما هي.

### هل يعمل هذا في ASP.NET Core؟

نعم. يمكن تشغيل نفس الشفرة داخل إجراء تحكم (controller). ما عليك سوى بث المصنف إلى الاستجابة:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## نصائح احترافية ومخاطر محتملة

- **نصيحة احترافية:** احتفظ بعلامات SmartMarker في ورقة “Template” منفصلة. بهذه الطريقة يمكنك حماية الورقة من التعديلات العرضية مع السماح للمعالج بقراءتها.  
- **احذر من:** مفاتيح JSON التي تحتوي على مسافات أو أحرف خاصة. يتوقع Aspose.Cells معرفات JavaScript صالحة؛ أعد تسميتها أو استخدم سمة `JsonProperty` إذا كنت تقوم بإلغاء تسلسلها من POCO.  
- **نصيحة أداء:** إذا كنت تعالج آلاف الصفوف، اضبط `smartMarkerOptions.EnableCache = true` لإعادة استخدام العلامات المترجمة.  
- **تحقق من الإصدار:** الشفرة أعلاه تستهدف Aspose.Cells 23.9+. الإصدارات الأقدم قد لا تدعم `AllowDuplicateSheetNames`.

---

## الخلاصة

أصبح لديك الآن وصفة كاملة من البداية إلى النهاية **لإنشاء Excel من JSON** في C#. من خلال تكوين `SmartMarkerOptions` أظهرنا كيفية **السماح بأسماء أوراق مكررة**، والتحكم في تسمية **ورقة التفاصيل**، وأخيرًا **حفظ المصنف بأسلوب C#**. النهج مكتمل ذاتيًا—لا خدمات خارجية، مجرد حزمة NuGet واحدة.

ما الخطوة التالية؟ جرّب استبدال مصدر JSON بواجهة برمجة تطبيقات حقيقية.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}