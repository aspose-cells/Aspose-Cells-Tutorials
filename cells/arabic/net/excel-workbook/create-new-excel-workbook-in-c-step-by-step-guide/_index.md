---
category: general
date: 2026-02-15
description: إنشاء مصنف Excel جديد وتعلم كيفية استخدام EXPAND، توسيع تسلسل، وحساب
  قاطع الظل. كما يمكنك معرفة كيفية حفظ المصنف إلى ملف.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: ar
og_description: إنشاء مصنف Excel جديد باستخدام C#. تعلّم كيفية استخدام EXPAND، توسيع
  تسلسل، حساب الظل المقلوب، وحفظ المصنف إلى ملف.
og_title: إنشاء مصنف Excel جديد في C# – دليل برمجة شامل
tags:
- C#
- Aspose.Cells
- Excel automation
title: إنشاء مصنف Excel جديد في C# – دليل خطوة بخطوة
url: /ar/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel جديد في C# – دليل برمجة كامل

هل احتجت يوماً إلى **إنشاء مصنف Excel جديد** من الشيفرة ولم تعرف من أين تبدأ؟ لست وحدك؛ كثير من المطورين يواجهون هذه المشكلة عند أتمتة التقارير أو بناء خطوط البيانات. في هذا الدرس سنوضح لك بالضبط كيفية إنشاء مصنف Excel جديد، كتابة بعض الصيغ الرائعة، ثم **حفظ المصنف إلى ملف** لفحصه لاحقاً.

سنغوص أيضاً في تفاصيل دالة `EXPAND`، نُظهر **كيفية استخدام EXPAND** لتحويل تسلسل صغير إلى كتلة كبيرة، نشرح **كيفية توسيع التسلسل** عملياً، وأخيراً نكشف **كيفية حساب القاطع** مباشرة داخل Excel. في النهاية ستحصل على برنامج C# قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما الذي ستحتاجه

- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو نسخة مرخصة) – المكتبة التي تسمح لنا بالتعامل مع Excel دون الحاجة لتثبيت Office.  
- **.NET 6+** (أو .NET Framework 4.6+).  
- بيئة تطوير متوسطة مثل Visual Studio 2022 أو VS Code أو Rider.  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Cells`. إذا لم تكن لديك بعد، نفّذ:

```bash
dotnet add package Aspose.Cells
```

هذا كل ما تحتاجه—لا شيء آخر لإعداده.

## الخطوة 1: إنشاء مصنف Excel جديد

أول شيء نفعله هو إنشاء كائن `Workbook`. فكر فيه كقماش فارغ حيث ستعيش جميع الأوراق والخلايا والصيغ.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **لماذا هذا مهم:** إنشاء المصنف في الذاكرة يعني أننا لا نتعامل مع القرص حتى نقرر صراحةً **حفظ المصنف إلى ملف**. هذا يجعل العملية سريعة ويسمح لك بسلسلة تعديلات إضافية دون عبء I/O.

## الخطوة 2: كيفية استخدام EXPAND لتوسيع تسلسل

`EXPAND` هي دالة Excel حديثة تأخذ مصفوفة أصغر وتمددها إلى حجم محدد. في مثالنا نبدأ بتسلسل عمودي من ثلاثة صفوف ونحوّله إلى كتلة 5 × 5.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **شرح:** `SEQUENCE(3)` ينتج `{1;2;3}` (مصفوفة عمودية). `EXPAND(...,5,5)` يخبر Excel بتكرار تلك المصفوفة حتى تملأ مستطيلًا من 5 صفوف × 5 أعمدة، بدءًا من A1. النتيجة هي مصفوفة حيث يتكرر كل عمود الأرقام الثلاثة الأصلية، والصفّان الأخيران فارغان لأن المصدر يحتوي فقط على ثلاثة صفوف.

### النتيجة المتوقعة

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

سترى النمط نفسه ينتشر عبر النطاق بمجرد فتح المصنف في Excel.

## الخطوة 3: كيفية حساب القاطع في Excel

معظم الناس يعرفون `SIN` و `COS` و `TAN`، لكن `COT` اختصار مفيد للمقلوب (العكس) للظل. إليك كيفية الحصول على قاطع 45° (الذي يساوي 1) باستخدام الراديان.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **لماذا نستخدم COT؟** استدعاء `COT` مباشرةً يتجنب القسمة الإضافية التي تحتاجها مع `1/TAN(...)`، مما يجعل الصيغة أوضح وأسرع قليلاً في الأوراق الكبيرة.

## الخطوة 4: تقييم جميع الصيغ

Aspose.Cells لا يحسب الصيغ تلقائيًا إلا إذا طلبت ذلك. طريقة `CalculateFormula` تجبر على تقييم كامل بحيث تُخزن القيم الناتجة في الخلايا.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **نصيحة:** إذا كان لديك العديد من الصيغ المكلفة، يمكنك تمرير كائن `CalculationOptions` لضبط الأداء (مثل تمكين المعالجة المتعددة الخيوط).

## الخطوة 5: حفظ المصنف إلى ملف

الآن بعد أن أصبح كل شيء جاهزًا، نُجري أخيرًا **حفظ المصنف إلى ملف**. اختر مجلدًا لديك صلاحية كتابة فيه، وأعطِ الملف اسمًا ذا معنى.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **ماذا يحدث على القرص؟** استدعاء `Save` يكتب حزمة `.xlsx` مكتملة، تشمل المصفوفة المتوسعة من `EXPAND` والقيمة المحسوبة للقاطع. افتح الملف في Excel وسترى كتلة 5 × 5 تبدأ من A1 والرقم `1` في B1.

![مخرجات Excel تُظهر التسلسل الموسع وقيمة القاطع](excel-output.png "مخرجات مثال إنشاء مصنف Excel جديد")

*نص بديل للصورة: مخرجات مثال إنشاء مصنف Excel جديد*

### تحقق سريع

1. افتح `output.xlsx`.  
2. تأكد من أن الخلايا **A1:E5** تحتوي على نمط 1‑2‑3 المتكرر.  
3. انظر إلى **B1** – يجب أن تُظهر `1`.  

إذا كان كل شيء مطابقًا، تهانينا—لقد نجحت في أتمتة Excel!

## كيفية توسيع التسلسل في سيناريوهات أخرى

بينما يستخدم المثال أعلاه `SEQUENCE(3)` ثابتًا، يمكنك بسهولة استبداله بنطاق ديناميكي أو صيغة أخرى:

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**متى تستخدمه؟**  
- إنشاء جداول نائبة للقوالب.  
- تكرار صف رأس بسرعة عبر العديد من الأعمدة.  
- بناء شبكات خريطة الحرارة دون نسخ‑لصق يدوي.

## الأخطاء الشائعة وكيفية تجنّبها

| الخطأ | السبب | الحل |
|---------|----------------|-----|
| `#VALUE!` بعد `EXPAND` | المصفوفة المصدر ليست نطاقًا صحيحًا (مثلاً تحتوي على أخطاء) | نظّف البيانات المصدر أو غلفها بـ `IFERROR`. |
| القاطع يُعيد `#DIV/0!` للزاوية 0° | `COT(0)` لا نهائي رياضيًا | احمِ الصيغة بـ `IF(PI()/4=0,0,COT(...))`. |
| المصنف غير محفوظ | المسار غير صالح أو لا توجد صلاحية كتابة | استخدم `Path.GetFullPath` وتأكد من وجود المجلد. |
| الصيغ غير محسوبة | إغفال `CalculateFormula` | استدعِها دائمًا قبل `Save`. |

## إضافة تنسيق (اختياري)

إذا أردت أن يبدو المخرجات أجمل، يمكنك تطبيق نمط بسيط بعد الحسابات:

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

هذا المقتطف اختياري، لكنه يوضح كيف يمكنك دمج منطق **إنشاء مصنف Excel جديد** مع التنسيق في خطوة واحدة.

## ملخص

استعرضنا العملية بالكامل:

1. **إنشاء مصنف Excel جديد** باستخدام Aspose.Cells.  
2. استخدام **كيفية استخدام EXPAND** لتحويل `SEQUENCE` صغير إلى مصفوفة 5 × 5.  
3. إظهار **كيفية حساب القاطع** مباشرةً في خلية.  
4. إجبار الحساب عبر `CalculateFormula`.  
5. **حفظ المصنف إلى ملف** والتحقق من النتيجة.

كل هذا مستقل، يعمل على أي بيئة تشغيل .NET حديثة، ويتطلب حزمة NuGet واحدة فقط.

## ما التالي؟

- **مصادر بيانات ديناميكية:** سحب البيانات من قاعدة بيانات وإدخالها في `EXPAND`.  
- **أوراق عمل متعددة:** حلقة عبر مجموعة من الأوراق لتوليد كتاب تقرير كامل.  
- **صيغ متقدمة:** استكشاف `LET` و `LAMBDA` أو المنطق الشرطي القائم على المصفوفات لجداول أكثر ذكاءً.  

لا تتردد في التجربة—غيّر معامل `SEQUENCE`، جرّب زوايا مختلفة لـ `COT`، أو أدمج توليد المخططات. السماء هي الحد عندما يمكنك **إنشاء مصنف Excel جديد** برمجيًا.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راسلني على Twitter @YourHandle. سأكون سعيدًا بالمساعدة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}