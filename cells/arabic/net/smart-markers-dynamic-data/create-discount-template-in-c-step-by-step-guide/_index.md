---
category: general
date: 2026-02-14
description: أنشئ قالب خصم بسرعة وتعلم كيفية تطبيق الخصم في جدول البيانات، وإدخال
  البيانات في القالب، وتعريف بادئة المتغيّر للعلامات الذكية.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: ar
og_description: إنشاء قالب خصم باستخدام C#. تعلم كيفية تطبيق الخصم في جدول البيانات،
  حقن البيانات في القالب، وتعريف بادئة متغيرة للعلامات الذكية.
og_title: إنشاء قالب خصم – شرح كامل بلغة C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: إنشاء قالب خصم في C# – دليل خطوة بخطوة
url: /ar/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

.

Proceed to produce Arabic translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء قالب خصم – دليل كامل بلغة C#

هل احتجت يومًا إلى **إنشاء قالب خصم** لتقرير مبيعات لكنك لم تكن متأكدًا من كيفية إدخال الأرقام إلى جدول البيانات تلقائيًا؟ لست وحدك. في هذا الدرس سنوضح لك بالضبط كيف **تنشئ قالب خصم**، ثم **تطبق الخصم في خلايا جدول البيانات**، **تُدخل البيانات في القالب**، وحتى **تحدد بادئة المتغير** للعلامات الذكية—كل ذلك باستخدام كود C# نظيف.

سنبدأ بتحديد المشكلة، ثم نتجه مباشرة إلى حل عملي يمكنك نسخه ولصقه. في النهاية ستحصل على نمط قابل لإعادة الاستخدام يعمل سواءً كنت تُنشئ فواتير، قوائم أسعار، أو أي جدول بيانات يحتاج إلى خصومات ديناميكية.

---

## ما ستتعلمه

- كيفية تصميم قالب جدول بيانات يدعم الخصم.
- كيفية تكوين `VariablePrefix` / `VariableSuffix` مخصص بحيث تكون العلامات سهلة الرؤية.
- كيفية تمرير كائن مجهول (`discountData`) إلى `SmartMarkerProcessor`.
- كيف أن الصيغة الناتجة (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) تحسب السعر النهائي تلقائيًا.
- نصائح للتعامل مع الحالات الحدية مثل الصفوف ذات الخصم صفر أو مستويات خصم متعددة.

**المتطلبات المسبقة** – بيئة تشغيل .NET حديثة (≥ .NET 6)، مرجع إلى مكتبة `Aspose.Cells` (أو ما شابه) التي توفر `SmartMarkerProcessor`، وفهم أساسي لصياغة C#. لا شيء معقد.

---

## الخطوة 1: إنشاء قالب خصم في جدول البيانات الخاص بك

ابدأ بفتح مصنف جديد (أو استخدم مصنفًا موجودًا) وضع عنصر نائب حيث سيُطبق الخصم. فكر في القالب كملف Excel عادي يحتوي على “علامات ذكية” سيستبدلها المعالج.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**لماذا هذا مهم:** من خلال تضمين `#Discount#` داخل الصيغة نخبر المعالج بالضبط مكان قيمة الخصم. سيستبدل `SmartMarkerProcessor` `#Discount#` بالرقم الذي ستقدمه لاحقًا، مع ترك باقي الصيغة دون تعديل.

---

## الخطوة 2: تعريف بادئة المتغير للعلامات الذكية

بشكل افتراضي، تبحث العديد من المكتبات عن `${Variable}` أو `{{Variable}}`. في حالتنا نريد علامة نظيفة وقابلة للقراءة البشرية، لذا **نعرّف بادئة المتغير** واللاحقة صراحةً.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**نصيحة احترافية:** استخدام `#` يجعل العلامات قصيرة وسهلة الرؤية في شريط صيغ Excel. إذا احتجت لتجنب التعارض مع الدوال المدمجة في Excel، اختر زوجًا مختلفًا (مثال: `[[` و `]]`).

---

## الخطوة 3: إدخال البيانات في القالب باستخدام SmartMarkerProcessor

الآن نُدخل قيمة الخصم الفعلية. سيقوم المعالج بفحص ورقة العمل، العثور على كل `#Discount#`، واستبداله بالقيمة من الكائن المجهول الذي نمرره.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

بعد هذا الاستدعاء، تصبح الصيغة في الخلية `B2` كالتالي:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

عند حساب المصنف، تُظهر الخلية `B2` **90**، أي خصم 10 % تم تطبيقه على السعر الأصلي 100.

**لماذا يعمل ذلك:** `StartSmartMarkerProcessing` يتجول في كل خلية، يبحث عن الرمز `#Discount#`، ويستبدله بالقيمة الرقمية. وبما أن الرمز موجود داخل جملة `IF`، فإن جدول البيانات لا يزال يتعامل مع الحالات التي قد يكون فيها الخصم صفرًا.

---

## الخطوة 4: تطبيق الخصم في جدول البيانات – التحقق من النتيجة

لنُطلق عملية الحساب ونطبع السعر النهائي على وحدة التحكم. تُظهر هذه الخطوة أن سير عمل **تطبيق الخصم في جدول البيانات** قد نجح.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**الناتج المتوقع**

```
Original: 100
Discounted (10%): 90
```

إذا غيرت `discountData.Discount` إلى `0.25` وأعدت تشغيل المعالج، سيعكس الناتج تلقائيًا خصمًا بنسبة 25 %—دون الحاجة إلى أي كود إضافي.

---

## الخطوة 5: التعامل مع الحالات الحدية والخصومات المتعددة

### صفوف الخصم صفر

أحيانًا لا يكون المنتج معروضًا بخصم. للحفاظ على صلابة الصيغة، يغطي الـ `IF` الذي وضعته مسبقًا هذا السيناريو: عندما يكون `#Discount#` يساوي `0`، يمر السعر الأصلي دون تعديل.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### أعمدة خصم متعددة

إذا احتجت إلى خصومات منفصلة لكل صف، أعط كل صف علامته الخاصة، مثل `#Discount1#`، `#Discount2#`، ومرّر مجموعة:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

يتطابق المعالج مع العلامات بالتسلسل، لذا يحصل كل صف على القيمة الصحيحة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ الذي يدمج جميع الخطوات السابقة. احفظه باسم `Program.cs`، أضف مرجعًا إلى `Aspose.Cells`، ثم شغّله.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

عند تشغيله سيطبع الأرقام المتوقعة وينتج ملف `DiscountedPricing.xlsx` يمكنك فتحه في Excel لرؤية الصيغة مُحلَّة بالفعل.

---

## الخلاصة

الآن تعرف كيف **تنشئ قالب خصم**، **تطبق الخصم في جدول البيانات**، **تُدخل البيانات في القالب**، و**تحدد بادئة المتغير** للعلامات الذكية—كل ذلك بضع أسطر مختصرة من C#. النمط قابل للتوسيع—فقط غير الكائن المجهول أو مرّر مجموعة لتحديثات جماعية، وسيعالج القالب نفسه أي سيناريو خصم تطرحه.

هل أنت مستعد للمرحلة التالية؟ جرّب:

- إضافة حسابات الضرائب إلى جانب الخصومات.
- سحب نسب الخصم من قاعدة بيانات بدلاً من تعيينها يدويًا.
- استخدام التنسيق الشرطي لتظليل الصفوف ذات الخصومات العالية.

هذه الإضافات تحافظ على الفكرة الأساسية مع توسيع فائدة قالب الخصم الخاص بك.

لديك أسئلة أو حالة استخدام مميزة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}