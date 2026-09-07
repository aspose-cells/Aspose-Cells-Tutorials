---
category: general
date: 2026-02-28
description: تعلم كيفية تعيين تنسيق التاريخ في Excel، قراءة تاريخ ووقت Excel، استخراج
  التاريخ من Excel وحساب صيغ المصنف باستخدام Aspose.Cells في C#. مثال كامل قابل للتنفيذ.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: ar
og_description: إتقان ضبط تنسيق التاريخ في إكسل، قراءة تاريخ ووقت إكسل، استخراج التواريخ،
  وحساب صيغ المصنف مع مثال كامل بلغة C#.
og_title: ضبط تنسيق التاريخ في Excel باستخدام C# – دليل خطوة بخطوة كامل
tags:
- Aspose.Cells
- C#
- Excel automation
title: ضبط تنسيق التاريخ في إكسل باستخدام C# – دليل كامل خطوة بخطوة
url: /ar/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تنسيق تاريخ Excel – دليل C# الكامل

هل واجهت صعوبة في **تعيين تنسيق تاريخ Excel** أثناء إنشاء جداول البيانات في الوقت الفعلي؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما تظهر الخلية كسلسلة نصية خام بدلاً من تاريخ صحيح، خاصةً مع تواريخ العصور اليابانية أو سلاسل اللغة المخصصة.  

في هذا الدرس سنستعرض مثالًا واقعيًا **يُعيّن تنسيق تاريخ Excel**، ثم **يقرأ تاريخ ووقت Excel**، **يستخرج التاريخ من Excel**، وحتى **يحسب صيغ المصنف** حتى تتمكن أخيرًا من **الحصول على قيمة خلية تاريخ ووقت** ككائنات .NET `DateTime` أصلية. لا مراجع خارجية، مجرد مقتطف مستقل قابل للتنفيذ يمكنك لصقه في Visual Studio ورؤيته يعمل فورًا.

## ما ستحتاجه

- **Aspose.Cells for .NET** (أي إصدار حديث؛ الـ API المستخدم هنا يعمل مع 23.x وما فوق)  
- .NET 6 أو أحدث (الكود يُجمّع أيضًا مع .NET Framework 4.6+)  
- فهم أساسي لصياغة C# – إذا كنت تستطيع كتابة `Console.WriteLine` فأنت جاهز.

هذا كل شيء. لا حزم NuGet إضافية بخلاف Aspose.Cells، ولا حاجة لتثبيت Excel.

## كيفية تعيين تنسيق تاريخ Excel في C#  

أول ما نقوم به هو إخبار Excel أن الخلية تحتوي على تاريخ، وليس مجرد نص. توفر Aspose.Cells معرف تنسيق رقم مدمج (`14`) يتطابق مع نمط التاريخ القصير للغة الحالية.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **نصيحة احترافية:** استدعاء `CalculateFormula()` أمر حاسم. بدون ذلك، تظل الخلية تحتفظ بالسلسلة الخام، وستُطلق `GetDateTime()` استثناءً. هذا السطر يجبر Aspose.Cells على تشغيل المحلل الداخلي الخاص به، وبالتالي **حساب صيغ المصنف** لنا.

الناتج الذي ستراه عند تشغيل البرنامج هو:

```
Parsed DateTime: 2020-04-01
```

هذا يؤكد أننا نجحنا في **تعيين تنسيق تاريخ Excel**، وتمكنا من **الحصول على خلية تاريخ ووقت** ككائن `DateTime` صحيح.

## قراءة قيم تاريخ ووقت Excel  

الآن بعد أن تم تخزين التاريخ بشكل صحيح، قد تتساءل كيف تستعيده لاحقًا، ربما من ملف موجود. طريقة `GetDateTime()` نفسها تعمل على أي خلية تحمل بالفعل تنسيق تاريخ.

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

إذا لم تكن الخلية مُنسقة كتاريخ، تُعيد `GetDateTime()` القيمة `DateTime.MinValue`. لهذا السبب نحتاج دائمًا إلى **تعيين تنسيق تاريخ Excel** أولًا.

## استخراج التاريخ من خلايا Excel  

أحيانًا تحتوي الخلية على طابع زمني كامل (تاريخ + وقت) لكنك تحتاج فقط إلى جزء التاريخ. يمكنك قطع مكون الوقت باستخدام `.Date` على الـ `DateTime` المُعاد.

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

هذا النهج يعمل بغض النظر عن تنسيق الرقم الأساسي في Excel، طالما تم التعرف على الخلية ك تاريخ.

## حساب صيغ المصنف  

ماذا لو كان التاريخ نتيجة صيغة، مثل `=TODAY()` أو `=DATE(2022,5,10)`؟ ستقوم Aspose.Cells بتقييم الصيغة عندما تستدعي `CalculateFormula()`. بعد ذلك، تتصرف الخلية تمامًا كما لو تم إدخال تاريخ يدويًا.

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

لاحظ أننا لم نحتاج إلى تغيير نمط الخلية؛ Excel بالفعل يعامل نتائج الصيغ كتواريخ عندما تُعيد الصيغة رقمًا تسلسليًا يُطابق تاريخًا.

## الحصول على خلية تاريخ ووقت من مصنف موجود  

بدمج كل ما سبق، إليك روتينًا مختصرًا يمكنك إدراجه في أي مشروع لفتح ملف Excel، وضمان تفسير جميع خلايا التاريخ بشكل صحيح، وإرجاع قائمة من كائنات `DateTime`.

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

تشغيل `ExtractAllDates("Sample.xlsx")` سيعطيك كل تاريخ تم **تعيين تنسيق تاريخ Excel** له بشكل صحيح في الورقة الأولى.

## المشكلات الشائعة وكيفية تجنبها  

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| `GetDateTime()` يُطلق `ArgumentException` | الخلية غير مُعترف بها ك تاريخ (يفتقر إلى تنسيق رقم) | تطبيق `Style.Number = 14` **قبل** استدعاء `CalculateFormula()` |
| يظهر التاريخ كـ `1900‑01‑00` | يُفسّر الرقم التسلسلي 0 في Excel كالعصر الأساسي | تأكد من أن الخلية تحتوي فعليًا على رقم تسلسلي صالح (>0) |
| سلاسل العصور اليابانية لا تُ解析 | Aspose.Cells لا يُ解析 سلاسل العصور إلا بعد `CalculateFormula()` | احتفظ بالسلسلة الخام، عيّن تنسيق تاريخ، ثم استدعِ `CalculateFormula()` |
| تحولات المنطقة الزمنية | يتم تخزين `DateTime` بدون معلومات المنطقة، لكن تطبيقك قد يعرضه ب locale مختلف | استخدم `DateTimeKind.Utc` أو قم بالتحويل صراحةً إذا لزم الأمر |

## صورة – ملخص بصري  

![مثال على تعيين تنسيق تاريخ Excel](excel-date-format.png "مثال على تعيين تنسيق تاريخ Excel")

الرسم يوضح التدفق: **كتابة السلسلة → تطبيق تنسيق الرقم → إعادة حساب → استرجاع DateTime**.

## الخلاصة  

غطينا كل ما تحتاجه لت **تعيين تنسيق تاريخ Excel**، **قراءة تاريخ ووقت Excel**، **استخراج التاريخ من Excel**، **حساب صيغ المصنف**، وأخيرًا **الحصول على قيم خلية تاريخ ووقت** ككائنات .NET أصلية. الكود الكامل القابل للتنفيذ جاهز للنسخ واللصق، والشروحات توضح لك "السبب" وراء كل خطوة، لتتمكن من تعديل النمط لسيناريوهات أكثر تعقيدًا.

### ما التالي؟

- **استيراد/تصدير جماعي:** استخدم المساعد `ExtractAllDates` لمعالجة تقارير كبيرة دفعةً.  
- **تنسيقات تاريخ مخصصة:** استبدل `Style.Number = 14` بـ `Style.Custom = "yyyy/mm/dd"` للحصول على تنسيق مستقل عن اللغة.  
- **تواريخ مع مراعاة المنطقة الزمنية:** اجمع بين `DateTimeOffset` وأرقام Excel التسلسلية للتطبيقات العالمية.

لا تتردد في التجربة، إضافة تنسيق شرطي، أو دفع التواريخ إلى قاعدة بيانات. إذا واجهت أي صعوبات، اترك تعليقًا—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}