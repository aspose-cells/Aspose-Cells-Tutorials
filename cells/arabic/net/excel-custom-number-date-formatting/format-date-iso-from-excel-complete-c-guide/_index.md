---
category: general
date: 2026-03-30
description: تعلم كيفية تنسيق التاريخ بصيغة ISO أثناء قراءة قيم التاريخ والوقت في
  Excel واستخراج بيانات التاريخ والوقت من Excel باستخدام Aspose.Cells في C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: ar
og_description: تنسيق التاريخ بصيغة ISO من بيانات Excel باستخدام Aspose.Cells. يوضح
  هذا الدليل كيفية قراءة تاريخ ووقت Excel، استخراج قيم تاريخ ووقت Excel، وإخراج تواريخ
  ISO.
og_title: تنسيق تاريخ ISO من Excel – دليل C# خطوة بخطوة
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: تنسيق التاريخ بصيغة ISO من Excel – دليل C# الكامل
url: /ar/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنسيق التاريخ بصيغة ISO من Excel – دليل C# الكامل

هل احتجت يومًا إلى **format date iso** عند استخراج التواريخ من ورقة Excel؟ ربما تتعامل مع تواريخ العصور اليابانية، أو تريد فقط سلسلة `yyyy‑MM‑dd` نظيفة لحمولة API. في هذا الدرس ستتعرف بالضبط على كيفية **read Excel datetime** الخلايا، **extract datetime Excel** القيم، وتحويلها إلى صيغة ISO‑8601 — دون أي تخمين.

سنستعرض مثالًا واقعيًا يستخدم Aspose.Cells، يوضح لماذا كل سطر مهم، ويظهر لك النتيجة النهائية التي يمكنك نسخها ولصقها في مشروعك. في النهاية، ستتمكن من التعامل مع سلاسل العصور الغريبة مثل “令和3年5月1日” وإنتاج تاريخ ISO قياسي، جاهز لقواعد البيانات، JSON، أو أي مكان تحتاجه.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Framework أيضًا)
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو مرخصة)
- إلمام أساسي بـ C# ومفاهيم Excel
- Visual Studio أو أي محرر C# تفضله

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells، لذا الإعداد بسيط جدًا.

---

## الخطوة 1: إنشاء Workbook وتحديد الورقة الأولى

أول شيء تقوم به هو إنشاء كائن `Workbook` جديد. هذا يمنحك تمثيلًا في الذاكرة لملف Excel يمكنك بعد ذلك التلاعب به أو القراءة منه.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*لماذا هذا مهم:*  
إنشاء الـ workbook برمجيًا يتيح لك تجنب التعامل مع الملفات الفعلية أثناء الاختبار. كما يضمن أن مرجع الورقة دائمًا صالح — لا مفاجآت مرجع فارغ لاحقًا عندما تحاول **read Excel datetime** القيم.

## الخطوة 2: كتابة سلسلة تاريخ ياباني في خلية

هدفنا هو توضيح كيفية تحليل تاريخ غير غريغوري. سنضع سلسلة العصر مباشرةً في الخلية **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*نصيحة احترافية:* إذا كنت تستخرج البيانات من مصنف موجود، ستتخطى استدعاء `PutValue` وتكتفي بالإشارة إلى الخلية التي تحتوي بالفعل على التاريخ. المفتاح هو أن الخلية تحمل **string** تمثل تاريخًا في التقويم الياباني القمري الشمسي.

## الخطوة 3: تكوين Culture يدعم التقويم الياباني القمري الشمسي

فئة .NET `CultureInfo` تسمح لك بتحديد كيفية تفسير التواريخ. عن طريق استبدال التقويم الغريغوري الافتراضي بـ `JapaneseLunisolarCalendar`، تزود المحلل بالسياق الذي يحتاجه.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*لماذا نفعل ذلك:*  
إذا حاولت تحليل “令和3年5月1日” باستخدام الثقافة الافتراضية، سيتسبب .NET في رمي `FormatException`. استبدال التقويم القمري الشمسي يخبر وقت التشغيل بالضبط كيف يربط “令和3年” (السنة الثالثة من عصر Reiwa) بالسنة الغريغورية 2021.

## الخطوة 4: تحليل قيمة الخلية كـ `DateTime` باستخدام Culture المكوَّن

الآن يأتي جوهر العملية — تحويل سلسلة العصر إلى كائن `DateTime` صحيح. توفر Aspose.Cells overload مريح لـ `GetDateTime` يقبل `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*ما يحدث في الخلفية:*  
`GetDateTime` يقرأ السلسلة الخام، يطبق قواعد التقويم الخاصة بالثقافة المقدمة، ويعيد `DateTime` يمثل نفس اللحظة في التقويم الغريغوري. هذه هي اللحظة التي تقوم فيها بـ **extract datetime Excel** البيانات بصيغة يمكنك العمل بها في .NET.

## الخطوة 5: إخراج التاريخ المُحلل بصيغة ISO 8601

أخيرًا، نقوم بتنسيق الـ `DateTime` كسلسلة ISO — `yyyy‑MM‑dd` — والتي تُقبل عالميًا من قبل APIs، قواعد البيانات، وإطارات العمل الأمامية.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*لماذا ISO؟*  
ISO 8601 يزيل الغموض. “05/01/2021” قد تكون 1 مايو أو 5 يناير حسب الإعداد المحلي. `2021-05-01` واضح تمامًا، وهذا هو السبب في أننا نستخدم **format date iso** في معظم سيناريوهات التكامل.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه في مشروع تطبيق Console، أضف مرجع Aspose.Cells، واضغط **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**الناتج المتوقع**

```
2021-05-01
```

شغّله مرة واحدة، وسترى التاريخ بصيغة ISO يُطبع في وحدة التحكم. هذه هي السلسلة الكاملة من **read Excel datetime** إلى **format date iso**.

## التعامل مع الحالات الشائعة

### 1. خلايا تحتوي على أرقام تواريخ Excel حقيقية

أحيانًا يخزن Excel التواريخ كأرقام تسلسلية (مثال: `44204`). في هذه الحالة، لا تحتاج إلى Culture؛ فقط استدعِ `GetDateTime()` بدون معاملات:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. خلايا فارغة أو غير صالحة

إذا كانت الخلية فارغة أو تحتوي على سلسلة لا يمكن تحليلها، سيتسبب `GetDateTime` في رمي استثناء. غلف الاستدعاء بـ `try/catch` أو تحقق من `IsDateTime` أولًا:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. صيغ عصور مختلفة

العصور اليابانية الأخرى (Heisei، Showa) تتبع نفس النمط. `JapaneseLunisolarCalendar` سيتعامل معها تلقائيًا، لذا لا تحتاج إلى منطق إضافي — فقط زوّد السلسلة.

## نصائح احترافية وملاحظات

- **Performance:** عند معالجة جداول بيانات كبيرة، أعد استخدام نسخة واحدة من `CultureInfo` بدلاً من إنشاء نسخة جديدة داخل حلقة.
- **Thread Safety:** كائنات `CultureInfo` تصبح للقراءة فقط بعد ضبط التقويم، لذا هي آمنة للمشاركة بين الخيوط.
- **Aspose.Cells Licensing:** إذا كنت تستخدم النسخة التجريبية المجانية، تذكر أن بعض الميزات قد تكون محدودة بعد انتهاء فترة التجربة. تحليل التاريخ المعروض هنا يعمل جيدًا في كل من الوضع التجريبي والمرخص.
- **Time Zones:** الـ `DateTime` الذي تحصل عليه هو **unspecified** (بدون منطقة زمنية). إذا كنت تحتاج إلى UTC، استدعِ `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` أو حوِّل باستخدام `TimeZoneInfo`.

## الخلاصة

غطّينا كل ما تحتاجه لتطبيق **format date iso** من مصنف Excel باستخدام C#. بدءًا من سلسلة عصر ياباني خام، قمنا بـ **read Excel datetime**، إعداد Culture المناسب، **extract datetime Excel**، وأخيرًا إخراج سلسلة ISO‑8601 نظيفة. النهج يعمل مع أي تمثيل تاريخ قد يقدمه Excel، سواء كان رقمًا تسلسليًا، سلسلة محلية، أو صيغة عصر تقليدية.

ما الخطوة التالية؟ جرّب التكرار على عمود كامل من التواريخ، اكتب نتائج ISO في ورقة جديدة، أو أدخلها مباشرةً في حمولة JSON لخدمة ويب. إذا كنت مهتمًا بأنظمة تقويم أخرى (Hebrew، Islamic)، فإن Aspose.Cells و `CultureInfo` في .NET تجعل هذه التجارب سهلة بنفس القدر.

هل لديك أسئلة أو صيغة تاريخ معقدة لا تستطيع حلها؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}