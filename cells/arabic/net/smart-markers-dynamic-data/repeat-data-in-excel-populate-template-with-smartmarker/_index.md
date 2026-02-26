---
category: general
date: 2026-02-21
description: كرر البيانات في إكسل بسرعة باستخدام SmartMarker — تعلم كيفية تعبئة قالب
  إكسل وتكرار الصفوف بسهولة.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: ar
og_description: تكرار البيانات في إكسل باستخدام SmartMarker. تعلم كيفية تعبئة قالب
  إكسل، وتكرار الصفوف، وأتمتة جداول البيانات الخاصة بك.
og_title: تكرار البيانات في إكسل – تعبئة القالب باستخدام SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: تكرار البيانات في إكسل – تعبئة القالب باستخدام SmartMarker
url: /ar/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تكرار البيانات في Excel – تعبئة القالب باستخدام SmartMarker

هل احتجت يومًا إلى **repeat data in Excel** لكنك لم تكن متأكدًا من كيفية تجنّب النسخ واللصق اليدوي؟ لست وحدك. في العديد من سيناريوهات التقارير لديك قائمة من العناصر التي يجب أن تتوسع إلى صفوف تلقائيًا، والقيام بذلك يدويًا هو وصفة للأخطاء.

الأمر هو أن استخدام SmartMarkerProcessor من مكتبة **GemBox.Spreadsheet** يتيح لك **populate an Excel template** بسطر واحد من C# وجعل الصفوف تتكرر لكل عنصر في مجموعتك. في هذا الدليل سنستعرض الخطوات الدقيقة، نعرض لك الشيفرة الكاملة، ونشرح لماذا كل جزء مهم، حتى تتمكن من تكرار الصفوف في Excel بثقة دون عناء.

## ما ستتعلمه

* كيفية تعريف بنية البيانات التي تدفع عملية التكرار.  
* كيفية ربط `SmartMarkerProcessor` بملف عمل يحتوي على ورقة قالب مخفية.  
* كيف يتوسع العلامة `${Repeat:Item}` إلى عدة صفوف تلقائيًا.  
* نصائح للتعامل مع الحالات الحدية مثل المجموعات الفارغة أو التنسيق المخصص.  

بنهاية هذا الدرس ستكون قادرًا على **populate excel from data** بطريقة قابلة للتوسع، وسهلة الصيانة، وتعمل مع أي مشروع .NET.

---

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الشيفرة تستخدم ميزات C# الحديثة).  
* حزمة NuGet **GemBox.Spreadsheet** (الإصدار المجاني يعمل حتى 150 صفًا).  
* ملف قالب Excel أساسي (`Template.xlsx`) يحتوي على ورقة مخفية باسم `HiddenTemplate`.  
* الإلمام بكائنات C# و LINQ مفيد لكنه غير مطلوب.

---

## الخطوة 1 – تعريف بنية البيانات المتكررة

أولاً، تحتاج إلى مصدر بيانات يمكن لمحرك SmartMarker التكرار عليه. في معظم التطبيقات الواقعية سيأتي هذا من قاعدة بيانات أو API أو ملف CSV. لتوضيح الفكرة سنستخدم نوعًا مجهولًا بخصية واحدة تسمى `Item` تحتوي على مصفوفة من السلاسل.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **لماذا هذا مهم:** العلامة `${Repeat:Item}` داخل قالب Excel تبحث عن خاصية باسم `Item`. إذا قمت بإعادة تسمية الخاصية، يجب تحديث العلامة وفقًا لذلك. هذا الارتباط الوثيق يضمن بقاء القالب متزامنًا مع الشيفرة، مما يجعل من السهل **populate excel template** دون التخمين بشأن أسماء الأعمدة.

### تنوعات شائعة

* **Complex objects:** بدلاً من مصفوفة سلاسل بسيطة يمكنك توفير قائمة من الكائنات (`new[] { new { Name = "A", Qty = 10 } }`). ستقوم العلامة بتكرار الصفوف ويمكنك الإشارة إلى `${Item.Name}` و `${Item.Qty}` في الورقة.  
* **Empty collections:** إذا كانت `Item` فارغة، سيقوم SmartMarker ببساطة بإزالة كتلة التكرار، تاركًا القالب دون تعديل—مفيد للأقسام الاختيارية.

---

## الخطوة 2 – إنشاء SmartMarkerProcessor لورقة القالب المخفية

بعد ذلك، حمّل ملف العمل الخاص بك وأنشئ كائن `SmartMarkerProcessor`. وجهه إلى ملف العمل الذي يحتوي على ورقة القالب المخفية؛ سيقوم SmartMarker بنسخ تلك الورقة إلى ورقة مرئية وتوسيع علامات التكرار.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **نصيحة احترافية:** إذا كان لديك عدة قوالب في نفس الملف، يمكنك تحديد اسم ورقة المصدر عند استدعاء `processor.Process`. هذا يساعد عندما تحتاج إلى **repeat rows in excel** لأقسام مختلفة من التقرير.

### معالجة الحالات الحدية

* **Missing template sheet:** غلف عملية التحميل بكتلة try/catch وسجّل خطأ واضح—هذا يمنع الفشل الصامت عندما يكون مسار الملف غير صحيح.  
* **Large data sets:** بالنسبة لآلاف الصفوف، فكر في تدفق الناتج إلى ملف (`processor.Save`) بدلاً من الاحتفاظ بكل شيء في الذاكرة.

---

## الخطوة 3 – تطبيق البيانات وتوسيع العلامة `${Repeat:Item}`

الآن يأتي السطر السحري الذي يكرر الصفوف فعليًا. مرّر الكائن الذي أنشأته في الخطوة 1 إلى `processor.Process`. سيقوم SmartMarker بالعثور على كل علامة `${Repeat:Item}`، يكرر الصف لكل عنصر، ويستبدل العناصر النائبة بالقيم الفعلية.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### ما يجب أن تراه

عند فتح `Result.xlsx`، تم نسخ ورقة القالب المخفية إلى ورقة مرئية جديدة (تسمى افتراضيًا `Sheet1`). الصف الذي يحتوي على `${Repeat:Item}` يظهر الآن ثلاث مرات، مع إظهار الخلايا **A**، **B**، و **C** على التوالي.

| Item |
|------|
| A    |
| B    |
| C    |

إذا أضفت أعمدة إضافية مثل `${Item.Price}`، فسيتم ملؤها تلقائيًا من مصدر البيانات.

---

## كيفية تكرار الصفوف في Excel بدون SmartMarker (مقارنة سريعة)

| النهج                | تعقيد الكود | الصيانة | الأداء |
|----------------------|------------|----------|--------|
| نسخ‑لصق يدوي         | عالي       | منخفض   | ضعيف   |
| ماكرو VBA            | متوسط      | متوسط   | جيد    |
| **SmartMarkerProcessor**| منخفض   | عالي    | ممتاز  |

كما ترى، استخدام SmartMarker لت **repeat data in excel** يمنحك أنقى فصل بين تصميم القالب ومنطق الأعمال. كما أنه مستقل عن اللغة—مفاهيم مشابهة موجودة في مكتبات Java و Python و JavaScript.

---

## نصائح متقدمة & مشكلات شائعة

### 1. تنسيق الصفوف المتكررة

يقوم SmartMarker بنسخ الصف بالكامل—بما في ذلك أنماط الخلايا والحدود والتنسيق الشرطي. إذا كنت بحاجة إلى نمط مختلف للصف الأول أو الأخير، أضف علامات إضافية مثل `${If:Item.IsFirst}` واستخدم صيغًا شرطية داخل Excel.

### 2. التعامل مع مجموعات البيانات الكبيرة

عند العمل بأكثر من > 10 000 صف، قم بتعطيل الحساب التلقائي في Excel قبل المعالجة:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

أعد تمكينه بعد الحفظ للحفاظ على سرعة الأداء.

### 3. تعبئة Excel من البيانات في قاعدة بيانات حقيقية

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

ثم استخدم `${Repeat:Order}` في القالب لسرد كل طلب. يُظهر هذا النمط مدى سهولة **populate excel from data** مباشرةً من Entity Framework.

### 4. استخدام كتل تكرار متعددة

يمكنك وجود عدة علامات `${Repeat:...}` على نفس الورقة أو على أوراق مختلفة. يقوم SmartMarker بمعالجتها تسلسليًا، لذا فإن الترتيب مهم فقط إذا كان أحد الكتل يعتمد على ناتج آخر.

---

## مثال كامل قابل للتنفيذ

فيما يلي تطبيق console مستقل يمكنك لصقه في Visual Studio وتشغيله فورًا. يوضح جميع الخطوات الثلاث بالإضافة إلى حفظ الملف.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**الناتج المتوقع:** يحتوي `Result.xlsx` على ورقة حيث يظهر الصف الذي يحتوي على `${Repeat:Item}` ثلاث مرات، مع عرض A و B و C. لا حاجة لأي تعديلات يدوية.

---

## الخلاصة

أنت الآن تعرف كيف **repeat data in excel** بفعالية باستخدام SmartMarkerProcessor. من خلال تعريف كائن بيانات بسيط، تحميل قالب ملف العمل، واستدعاء `Process`، يمكنك **populate excel template**، **repeat rows in excel**، وعامةً **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}