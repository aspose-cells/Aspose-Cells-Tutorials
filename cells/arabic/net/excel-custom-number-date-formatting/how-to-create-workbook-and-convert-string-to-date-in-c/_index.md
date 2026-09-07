---
category: general
date: 2026-02-15
description: كيفية إنشاء دفتر عمل، تحويل النص إلى تاريخ، وتنسيق الخلية كتاريخ باستخدام
  Aspose.Cells. تعلم كيفية تعيين تنسيق رقم الخلية وقراءة تاريخ Excel بسهولة.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: ar
og_description: كيفية إنشاء دفتر عمل، تحويل النص إلى تاريخ، وتنسيق الخلية كتاريخ.
  دليل كامل خطوة بخطوة لقراءة تواريخ Excel.
og_title: كيفية إنشاء دفتر عمل وتحويل السلسلة إلى تاريخ في C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية إنشاء دفتر عمل وتحويل السلسلة إلى تاريخ في C#
url: /ar/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء دفتر عمل وتحويل النص إلى تاريخ في C#

هل تساءلت يومًا **كيف تنشئ دفتر عمل** يحول نصًا عاديًا مثل `"R3-04-01"` إلى قيمة `DateTime` حقيقية؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند سحب البيانات من الأنظمة القديمة أو مدخلات المستخدم. الخبر السار؟ ببضع أسطر من C# و Aspose.Cells يمكنك إنجاز ذلك بسرعة، دون الحاجة إلى تحليل يدوي.

في هذا الدرس سنستعرض العملية بالكامل: إنشاء دفتر عمل، إدراج سلسلة تاريخ، تطبيق **تنسيق الخلية ك تاريخ**، إجبار المحرك على **تعيين تنسيق رقم الخلية**، وأخيرًا **قراءة تاريخ Excel** كـ `DateTime`. في النهاية ستحصل على مقتطف قابل للتنفيذ يمكنك وضعه في أي مشروع .NET.

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.7.2+)
- حزمة NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)
- فهم أساسي لصياغة C#
- بيئة تطوير مثل Visual Studio أو VS Code (أيًا كانت)

لا حاجة لأي إعدادات إضافية—Aspose.Cells يتولى كل الأعمال الثقيلة داخليًا.

## الخطوة 1: كيفية إنشاء دفتر عمل – تهيئة ملف Excel

أولاً، نحتاج إلى كائن دفتر عمل جديد. فكر فيه كدفتر ملاحظات فارغ حيث كل ورقة عمل هي صفحة.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*لماذا هذا مهم:* إنشاء دفتر العمل يمنحنا حاوية للخلايا، الأنماط، والصيغ. بدون ذلك لا مكان لوضع سلسلة التاريخ.

## الخطوة 2: تحويل النص إلى تاريخ – إدراج النص الخام

الآن نضع سلسلة التاريخ الخام في الخلية **A1** في أول ورقة عمل. السلسلة تستخدم تنسيقًا مخصصًا (`R3-04-01`) لا يتعرف عليه Excel مباشرة.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*سبب القيام بذلك:* `PutValue` يخزن النص الحرفي. إذا حاولنا تعيين `DateTime` مباشرةً، سيفقد التنسيق المخصص. إبقاء النص كـ string يتيح لنا لاحقًا تطبيق **تعيين تنسيق رقم الخلية** الذي يخبر Excel كيف يفسره.

## الخطوة 3: تنسيق الخلية ك تاريخ – تطبيق النمط رقم 14

النمط المدمج في Excel رقم 14 يطابق `mm-dd-yy`. بتعيين هذا النمط نخبر المحرك: “عامل محتوى هذه الخلية ك تاريخ”.

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*ما يحدث خلف الكواليس:* خاصية `Number` ترتبط بمعرفات تنسيق الأرقام الداخلية في Excel. عندما يعيد دفتر العمل حساباته، سيحاول Excel تحويل النص إلى تاريخ تسلسلي باستخدام التنسيق المحدد.

## الخطوة 4: تعيين تنسيق رقم الخلية – إجبار إعادة الحساب

Excel لن يحول النص تلقائيًا حتى نطلب منه تقييم الصيغ (أو في هذه الحالة، إعادة تفسير الخلية). استدعاء `CalculateFormula` يُطلق هذا التحويل.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*نصيحة:* إذا كنت تتعامل مع العديد من الخلايا، يمكنك استدعاء `CalculateFormula` مرة واحدة بعد الانتهاء من جميع التنسيقات—هذا يوفر بضع مليثواني.

## الخطوة 5: قراءة تاريخ Excel – الحصول على قيمة DateTime

أخيرًا، نستخرج تمثيل `DateTime` من الخلية. Aspose.Cells يوفّره عبر `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**الناتج المتوقع (مع افتراض التقويم الميلادي الافتراضي):**

```
2023-04-01 00:00:00
```

لاحظ كيف تم تجاهل البادئة `"R3-"` لأن محلل تواريخ Excel يركز على الجزء الرقمي عندما يكون النمط تاريخًا. إذا احتوت سلاسل النص على بادئات أخرى، قد تحتاج إلى معالجتها مسبقًا، لكن بالنسبة للعديد من التنسيقات القديمة يعمل هذا الأسلوب بشكل مثالي.

## مثال كامل يعمل

بدمج كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

احفظه باسم `Program.cs`، استعد حزمة Aspose.Cells، ثم نفّذ `dotnet run`. يجب أن ترى الـ `DateTime` المنسق يُطبع في وحدة التحكم.

## الاختلافات الشائعة وحالات الحافة

### سلاسل تواريخ مختلفة

إذا كانت بيانات المصدر لديك على شكل `"2023/04/01"` أو `"01‑Apr‑2023"`، يمكنك ما زال الاعتماد على نفس سير العمل—فقط غيّر خاصية **Number** لتتناسب مع النمط (مثلاً `Number = 15` لـ `d-mmm-yy`).  

### تنسيقات خاصة بالمنطقة

Excel يحترم إعدادات المنطقة لدفتر العمل. لإجبار التحليل بنمط أمريكي، عيّن ثقافة دفتر العمل:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### عندما لا يتعرف Excel على السلسلة

أحيانًا لا يستطيع Excel استنتاج تاريخ (مثل `"R3-13-40"`). في هذه الحالات، عالج السلسلة مسبقًا:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

ثم طبّق نفس تنسيق الرقم.

## نصائح احترافية ومخاطر محتملة

- **نصيحة احترافية:** استخدم `StyleFlag` لتعديل تنسيق الرقم فقط، مع ترك باقي خصائص النمط دون تغيير.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **احذر من:** الكتابة فوق الأنماط الموجودة في خلية لديها حدود أو خطوط. نهج `StyleFlag` يمنع ذلك.
- **ملاحظة أداء:** إذا كنت تعالج آلاف الصفوف، اجمع استدعاءات `CalculateFormula` بعد إكمال جميع التحديثات؛ استدعاؤها لكل صف يضيف عبئًا غير ضروري.

## الخلاصة

أنت الآن تعرف **كيفية إنشاء دفتر عمل**، **تحويل النص إلى تاريخ**، **تنسيق الخلية ك تاريخ**، **تعيين تنسيق رقم الخلية**، وأخيرًا **قراءة تاريخ Excel** كـ `DateTime`. النمط بسيط: أدخل النص الخام، طبّق نمط تاريخ، إجبر على إعادة الحساب، ثم اقرأ القيمة.  

من هنا يمكنك توسيع المنطق إلى أعمدة كاملة، استيراد بيانات CSV، أو حتى إنشاء تقارير تحول سلاسل التاريخ القديمة تلقائيًا إلى تواريخ Excel صحيحة.  

هل أنت مستعد للارتقاء؟ جرّب تطبيق تنسيق رقم مخصص (`Number = 22`) لعرض التواريخ كـ `yyyy-mm-dd`، أو استكشف أدوات `DateTimeConversion` في Aspose.Cells لمواقف أكثر تعقيدًا.

برمجة سعيدة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}