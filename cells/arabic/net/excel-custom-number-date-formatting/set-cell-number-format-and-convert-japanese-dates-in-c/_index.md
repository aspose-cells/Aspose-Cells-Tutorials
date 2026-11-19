---
category: general
date: 2026-11-19
description: تعيين تنسيق رقم الخلية في C# وتعلم كيفية تطبيق تنسيق تاريخ Excel لتواريخ
  العصور اليابانية، مما يتيح تحويل تاريخ Excel موثوق به في C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: ar
lastmod: 2026-11-19
og_description: تعيين تنسيق رقم الخلية في C# وتطبيق تنسيق تاريخ Excel على تواريخ العصور
  اليابانية. اتبع هذا الدليل الكامل للحصول على تحويل دقيق لتواريخ Excel في C#.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: تعيين تنسيق أرقام الخلايا وتحويل التواريخ اليابانية في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: تعيين تنسيق رقم الخلية وتحويل التواريخ اليابانية في C#
url: /ar/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تنسيق رقم الخلية وتحويل التواريخ اليابانية في C#

إذا كنت بحاجة إلى **تعيين تنسيق رقم الخلية** في مشروع أتمتة Excel باستخدام C#، فإن هذا الدليل يوضح لك كيفية **تطبيق تنسيق تاريخ Excel** وإجراء **تحويل تاريخ Excel في C#** لتواريخ العصور اليابانية. ستحصل على مثال كامل قابل للتنفيذ يحول سلسلة عصر ريوا (مثال: `R3/04/01`) إلى التاريخ الميلادي `2021‑04‑01`.

## ما ستتعلمه

* كيفية إنشاء مصنف والوصول إلى ورقة العمل الأولى.  
* كيفية **تعيين تنسيق رقم الخلية** بحيث يتعامل Excel مع القيمة ك تاريخ.  
* كيفية **تطبيق تنسيق تاريخ Excel** الذي يتعرف على سلاسل العصر الياباني.  
* كيفية تشغيل **تحويل تاريخ Excel في C#** عن طريق إعادة حساب الصيغ.  
* النتيجة المتوقعة ونصائح استكشاف الأخطاء في الحالات الخاصة.

**المتطلبات المسبقة**

* .NET 6 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.6+).  
* Aspose.Cells for .NET 2024 أو أحدث – تثبيت عبر NuGet: `dotnet add package Aspose.Cells`.  
* إلمام أساسي بـ C# ومعالجة تواريخ Excel.

> **Pro tip:** Aspose.Cells يعمل دون الحاجة لتثبيت Microsoft Office، مما يجعله مثالياً لأتمتة الخادم.

## تعيين تنسيق رقم الخلية باستخدام Aspose.Cells في C#

الخطوة الأولى هي إخبار Excel أن الخلية تحتوي على تاريخ. يخزن Excel التواريخ كأرقام متسلسلة، لذا نحتاج إلى تطبيق تنسيق رقم تاريخ مدمج (ID 14) على الخلية المستهدفة.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### لماذا يعمل هذا

* `Style.Number = 14` يطابق تنسيق *التاريخ القصير* في Excel (`mm/dd/yyyy` افتراضياً).  
* عندما تحتوي الخلية على سلسلة عصر ياباني مثل `R3/04/01`، يقوم محلل Aspose.Cells الداخلي بالتعرف على العصر ويحولها إلى الرقم المتسلسل الميلادي المقابل أثناء `CalculateFormula()`.  
* بعد الحساب، تُعيد `StringValue` التاريخ الميلادي المنسق.

## تطبيق تنسيق تاريخ Excel لتواريخ العصر الياباني

إذا أردت أن تعرض الخلية العصر الياباني بدلاً من التاريخ الميلادي، يمكنك استخدام تنسيق رقم مخصص يتضمن رمز العصر. هذا يوضح قدرة **تطبيق تنسيق تاريخ Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` يفرض اللغة اليابانية.  
* `ggg` يمثل اسم العصر (مثال: `R` لعصر ريوا).  
* إضافة الأحرف الحرفية (`年`, `月`, `日`) تُنشئ تخطيط تاريخ ياباني مألوف.

### متى تستخدم تنسيقاً مخصصاً

* التقارير الموجهة للجمهور الياباني.  
* عندما تحتاج إلى الحفاظ على معلومات العصر الأصلية للوثائق القانونية.  
* في لوحات المعلومات حيث يُعرض كل من التاريخ الميلادي وتاريخ العصر جنباً إلى جنب.

## تحويل تاريخ Excel في C# – معالجة العصور اليابانية

يمكن تقسيم عملية **c# excel date conversion** إلى ثلاثة أجزاء منطقية:

1. **تحليل سلسلة العصر** – Aspose.Cells يتعرف تلقائياً على `R` (ريوا)، `H` (هييسي)، `S` (شووا)، إلخ.  
2. **التحويل إلى رقم متسلسل** – Excel يخزن التواريخ كأيام منذ 1899‑12‑30.  
3. **تنسيق الرقم المتسلسل** – إما باستخدام تنسيق مدمج (ID 14) أو تنسيق ياباني مخصص.

### مثال كامل من البداية إلى النهاية

فيما يلي برنامج مستقل يوضح كل من المخرجات الميلادية ومخرجات العصر في تشغيل واحد.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### الحالات الخاصة ومصائد الأخطاء الشائعة

| الحالة                                 | ما يجب مراقبته                                          | الحل / التوصية                                            |
|----------------------------------------|--------------------------------------------------------|-----------------------------------------------------------|
| سلسلة عصر فارغة أو غير صحيحة          | `PutValue` يخزن النص الحرفي؛ فشل التحويل               | تحقق من صحة الإدخال باستخدام تعبير منتظم قبل كتابة الخلية. |
| عدم تطابق اللغة                        | التنسيق المخصص يعرض أرقاماً غربية بدلاً من الأحرف اليابانية | تأكد من أن التنسيق `Custom` يتضمن `[$-ja-JP]` أو اضبط `Workbook.Settings.CultureInfo` إلى `ja-JP`. |
| وجود صيغ في المصنف تشير إلى خلية التاريخ | قد يكتب إعادة الحساب فوق نتائج الصيغ                   | استدعِ `CalculateFormula` **بعد** جميع خطوات التنسيق، أو استخدم `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` إذا رغبت بتجاوز الأخطاء. |
| استخدام إصدارات قديمة من Aspose.Cells   | دعم العصور اليابانية أضيف في 2022 Q3                    | حدّث إلى أحدث حزمة NuGet.                                 |

## اختبار الحل

1. **شغّل البرنامج** من Visual Studio أو `dotnet run`.  
2. تحقق من أن وحدة التحكم تطبع التاريخ الميلادي `2021‑04‑01` وسلسلة العصر `R3年04月01日`.  
3. افتح المصنف المُنشأ (إذا أضفت `wb.Save("Demo.xlsx");`) في Microsoft Excel لترى نفس التنسيق المطبق على الخلايا.

### نصيحة أتمتة

إذا كنت بحاجة إلى معالجة نطاق كبير من تواريخ العصور (مثال: العمود A يحتوي على العديد من التواريخ اليابانية)، غلف منطق التحويل داخل حلقة:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

هذا النهج يحافظ على عملية **تعيين تنسيق رقم الخلية** سريعة وفعّالة من حيث الذاكرة.

## الخلاصة

أنت الآن تعرف كيف **تعيّن تنسيق رقم الخلية** في C# باستخدام Aspose.Cells، وكيف **تطبق تنسيق تاريخ Excel** لسلاسل العصر الياباني، وكيف تُجري **تحويل تاريخ Excel في C#** موثوق من العصر إلى التاريخ الميلادي. يوضح الكود الكامل القابل للتنفيذ كلا المخرجات ويبرز الحالات الخاصة الشائعة.

**الخطوات التالية**

* استكشاف تنسيقات مدمجة أخرى (format IDs)  

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [set excel date format in C# – Complete Step‑by‑Step Guide](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [How to apply a custom number format excel in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}