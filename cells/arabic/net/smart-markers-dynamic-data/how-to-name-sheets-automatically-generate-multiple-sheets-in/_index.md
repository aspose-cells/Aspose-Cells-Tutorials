---
category: general
date: 2026-02-09
description: كيفية تسمية الأوراق في C# باستخدام SmartMarker – تعلم إنشاء أوراق متعددة
  وتلقائيًا تسمية الأوراق في بضع أسطر من الشيفرة.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: ar
og_description: كيفية تسمية الأوراق في C# باستخدام خيارات SmartMarker. يوضح هذا الدليل
  كيفية إنشاء أوراق متعددة وتسمية الأوراق تلقائيًا بسهولة.
og_title: كيفية تسمية الأوراق تلقائيًا – دليل C# السريع
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية تسمية الأوراق تلقائيًا – إنشاء عدة أوراق في C#
url: /ar/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تسمية الأوراق تلقائيًا – إنشاء أوراق متعددة في C#

هل تساءلت يومًا **كيف تسمية الأوراق** في مصنف Excel دون النقر يدويًا على “Rename” في كل مرة؟ لست وحدك. في العديد من سيناريوهات التقارير تنتهي بك الأمور إلى الحصول على العشرات من أوراق التفاصيل التي تحتاج إلى أسماء منهجية، والقيام بذلك يدويًا كابوس.  

الخبر السار هو أنه ببضع أسطر من C# يمكنك **إنشاء أوراق متعددة** و **أتمتة تسمية الأوراق** بحيث تتبع كل ورقة تفاصيل جديدة نمطًا يمكن التنبؤ به. في هذا الدرس سنستعرض الحل الكامل، نشرح لماذا كل جزء مهم، ونزودك بعينة كود جاهزة للتنفيذ.

## ما يغطيه هذا الدليل

* إعداد مصنف يحتوي على SmartMarkers.
* تهيئة `SmartMarkerOptions` للتحكم في الاسم الأساسي للأوراق التي تم إنشاؤها.
* تشغيل `ProcessSmartMarkers` بحيث تقوم المكتبة بإنشاء `Detail`، `Detail_1`، `Detail_2`، … تلقائيًا.
* نصائح للتعامل مع الحالات الخاصة مثل وجود أسماء أوراق مسبقة أو صيغ تسمية مخصصة.
* مثال كامل قابل للتنفيذ يمكنك لصقه في Visual Studio ورؤية النتيجة فورًا.

لا تحتاج إلى خبرة سابقة مع Aspose.Cells — فقط إعداد أساسي لـ C# وبيئة تطوير متكاملة من اختيارك.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث | ميزات لغة حديثة وتوافق المكتبة |
| Aspose.Cells for .NET (حزمة NuGet) | يوفر معالجة `SmartMarker` وإنشاء الأوراق |
| مشروع وحدة تحكم فارغ (أو أي تطبيق .NET) | يتيح لنا مكانًا لتنفيذ الكود |

Install the library with:

```bash
dotnet add package Aspose.Cells
```

الآن بعد أن غطينا الأساسيات، دعنا نغوص في التنفيذ الفعلي.

## الخطوة 1: إنشاء مصنف يحتوي على SmartMarkers

أولاً نحتاج إلى مصنف يحتوي على عنصر نائب SmartMarker. فكر في SmartMarker كعلامة قالب تخبر المحرك أين يحقن البيانات، وفي حالتنا، متى ينشئ ورقة جديدة.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **نصيحة احترافية:** احرص على أن تكون ورقة القالب خفيفة. يجب أن تحتوي فقط الصفوف التي تحتاج إلى تكرار على SmartMarkers؛ كل ما تبقى يبقى ثابتًا.

## الخطوة 2: تهيئة خيارات SmartMarker – جوهر تسمية الأوراق

الآن يأتي السحر. من خلال ضبط `DetailSheetNewName` نخبر المحرك ما هو الاسم الأساسي الذي سيستخدمه لكل ورقة تم إنشاؤها. ستضيف المكتبة “_1”، “_2”، إلخ، كلما كان الاسم الأساسي موجودًا بالفعل.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

إذا كنت تحتاج يومًا إلى صيغة مختلفة (مثلاً، “Report_2023”)، فقط غيّر السلسلة. يتعامل المحرك مع التصادمات تلقائيًا، وهذا هو السبب في أن هذا النهج **يُؤتمت تسمية الأوراق** دون كود إضافي.

## الخطوة 3: معالجة SmartMarkers وإنشاء الأوراق

مع وجود المصنف والبيانات والخيارات جاهزة، مكالمة طريقة واحدة تقوم بالعمل الشاق.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### النتيجة المتوقعة

عند فتح *GeneratedSheets.xlsx* سترى:

| اسم الورقة | المحتوى |
|------------|---------|
| Template   | تخطيط العلامة الأصلي (محفوظ للمرجعية) |
| Detail     | المجموعة الأولى من الصفوف (Apple, Banana, Cherry) |
| Detail_1   | النسخة الثانية – بيانات مطابقة (مفيدة عندما يكون لديك مجموعات متعددة) |
| Detail_2   | … وهكذا، حسب عدد مجموعات SmartMarker المتميزة التي لديك |

نمط التسمية (`Detail`، `Detail_1`، `Detail_2`) يوضح **كيفية تسمية الأوراق** برمجيًا بالإضافة إلى **إنشاء أوراق متعددة** حسب الحاجة.

## الحالات الخاصة والاختلافات

### 1. أسماء الأوراق الموجودة

إذا كان المصنف يحتوي بالفعل على ورقة باسم “Detail”، سيبدأ المحرك بـ “Detail_1”. هذا يمنع الكتابة فوق غير مقصودة.

### 2. صيغ الزيادة المخصصة

هل تريد “Detail‑A”، “Detail‑B” بدلاً من اللاحقات الرقمية؟ يمكنك معالجة الأسماء بعد `ProcessSmartMarkers`:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. مجموعات SmartMarker متعددة

إذا كان المصنف يحتوي على أكثر من مجموعة SmartMarker واحدة (مثلاً، `{{invoice}}` و `{{detail}}`)، ستولد كل مجموعة مجموعتها الخاصة من الأوراق بناءً على نفس `DetailSheetNewName`. لإعطاء كل مجموعة بادئة مميزة، أنشئ كائنات `SmartMarkerOptions` منفصلة واستدعِ `ProcessSmartMarkers` لكل مجموعة.

## نصائح عملية من الميدان

* **نصيحة احترافية:** قم بإيقاف `AllowDuplicateNames` في `WorkbookSettings` إذا كنت تريد أن ترمي المكتبة استثناءً بدلاً من إعادة تسمية الأوراق بصمت. هذا يساعد على اكتشاف أخطاء منطق التسمية مبكرًا.
* **احذر من:** الأسماء الأساسية الطويلة جدًا. يحد Excel أسماء الأوراق إلى 31 حرفًا؛ المكتبة تقص تلقائيًا، لكن قد ينتهي بك الأمر بأسماء غامضة.
* **ملاحظة أداء:** إنشاء مئات الأوراق قد يستهلك الذاكرة. حرّر المصنف (`wb.Dispose()`) فور الانتهاء إذا كنت تشغل البرنامج داخل خدمة طويلة الأمد.

## نظرة بصرية

![مخطط كيفية تسمية الأوراق](image.png "مخطط يوضح التدفق من قالب SmartMarker إلى الأوراق المُنشأة – كيفية تسمية الأوراق")

*يتضمن النص البديل الكلمة الرئيسية لتلبية تحسين محركات البحث.*

## الكود الكامل (جاهز للنسخ واللصق)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

شغّل البرنامج، افتح الملف المُولد، وسترى الأوراق مُسمّاة تلقائيًا وفقًا للنمط الذي حددناه.

## الخلاصة

أنت الآن تعرف **كيفية تسمية الأوراق** في مصنف C#، وكيفية **إنشاء أوراق متعددة** باستخدام SmartMarker، وكيفية **أتمتة تسمية الأوراق** بحيث لا تحتاج أبدًا إلى إعادة تسمية أي شيء يدويًا مرة أخرى. هذا النهج يتوسع من عدد قليل من صفحات التفاصيل إلى مئات، والنمط نفسه يعمل مع أي مجموعة تُمرّرها إلى `ProcessSmartMarkers`.

ما التالي؟ جرّب استبدال مصدر البيانات باستعلام قاعدة بيانات، جرب صيغ اللاحقة المخصصة، أو ربط مجموعات SmartMarker متعددة لإنشاء محرك تقارير كامل. السماء هي الحد عندما تدع المكتبة تتولى عمل التسمية المتكررة.

إذا وجدت هذا الدليل مفيدًا، أعطه نجمة على GitHub، شاركه مع زملائك، أو اترك تعليقًا أدناه بأفكارك الخاصة لتسمية الأوراق. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}