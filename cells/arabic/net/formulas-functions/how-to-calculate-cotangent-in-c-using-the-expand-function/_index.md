---
category: general
date: 2026-11-19
description: تعرّف على كيفية حساب الظل المقلوب في C# عن طريق إضافة الصيغ إلى الخلايا،
  واستخدام دالة EXPAND، وتقييم جميع الصيغ باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to calculate cotangent
- how to use expand
- add formula to cell
- evaluate all formulas
- use expand function
language: ar
lastmod: 2026-11-19
og_description: كيف تحسب الظل المقلوب في C#؟ يوضح لك هذا الدرس كيفية إضافة صيغة إلى
  خلية، واستخدام دالة EXPAND، وتقييم جميع الصيغ باستخدام Aspose.Cells.
og_image_alt: C# code snippet adding Excel formulas with Aspose.Cells
og_title: كيفية حساب الظل المقلوب في C# باستخدام EXPAND – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to calculate cotangent in C# by adding formulas to cells,
    using the EXPAND function, and evaluating all formulas with Aspose.Cells.
  headline: How to calculate cotangent in C# using the EXPAND function
  type: TechArticle
- description: Learn how to calculate cotangent in C# by adding formulas to cells,
    using the EXPAND function, and evaluating all formulas with Aspose.Cells.
  name: How to calculate cotangent in C# using the EXPAND function
  steps:
  - name: Creates a workbook and accesses the first worksheet.
    text: Creates a workbook and accesses the first worksheet.
  - name: Writes an `EXPAND` formula that turns a single value into a 5‑row array.
    text: Writes an `EXPAND` formula that turns a single value into a 5‑row array.
  - name: Writes a `COT` formula that **how to calculate cotangent** of π/4.
    text: Writes a `COT` formula that **how to calculate cotangent** of π/4.
  - name: Forces the engine to **evaluate all formulas** so the values are stored
      in the file.
    text: Forces the engine to **evaluate all formulas** so the values are stored
      in the file.
  - name: '**Validate source data** – check that cells referenced by `EXPAND` or `COT`
      contain numbers to avoid `#VALUE!` errors.'
    text: '**Validate source data** – check that cells referenced by `EXPAND` or `COT`
      contain numbers to avoid `#VALUE!` errors.'
  - name: '**Reuse the workbook object** – creating a single `Workbook` instance and
      reusing it for multiple operations reduces memory overhead.'
    text: '**Reuse the workbook object** – creating a single `Workbook` instance and
      reusing it for multiple operations reduces memory overhead.'
  - name: '**Save in the appropriate format** – `.xlsx` retains dynamic‑array formulas;
      `.xls` will downgrade them to static values.'
    text: '**Save in the appropriate format** – `.xlsx` retains dynamic‑array formulas;
      `.xls` will downgrade them to static values.'
  - name: '**Wrap calculations in try/catch** – formula parsing can throw `CellsException`
      if the syntax is invalid.'
    text: '**Wrap calculations in try/catch** – formula parsing can throw `CellsException`
      if the syntax is invalid.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- formulas
title: كيفية حساب قاطع الظل في C# باستخدام دالة EXPAND
url: /ar/net/formulas-functions/how-to-calculate-cotangent-in-c-using-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حساب الظل المقلوب في C# باستخدام دالة EXPAND

إذا كنت بحاجة إلى **كيفية حساب الظل المقلوب** في ملف .xlsx من C#، فإن هذا الدليل يقدم لك حلاً كاملاً وجاهزًا للتنفيذ. ستتعرف على **إضافة صيغة إلى الخلية**، واستخدام دالة **EXPAND** لإنشاء مصفوفات ديناميكية، وأخيرًا **تقييم جميع الصيغ** بحيث يحتوي دفتر العمل على النتائج المحسوبة.

العمل مع Excel برمجيًا يعني غالبًا التعامل مع مراجع الخلايا، وصيغ المصفوفات، والدوال المخصصة. بنهاية هذا الشرح ستحصل على برنامج C# واحد يقوم بـ:

1. إنشاء دفتر عمل والوصول إلى ورقة العمل الأولى.  
2. كتابة صيغة `EXPAND` تحول قيمة واحدة إلى مصفوفة مكوّنة من 5 صفوف.  
3. كتابة صيغة `COT` لحساب **كيفية حساب الظل المقلوب** للزاوية π/4.  
4. إجبار المحرك على **تقييم جميع الصيغ** بحيث تُحفظ القيم في الملف.  

الطريقة تعمل مع أحدث نسخة من Aspose.Cells لـ .NET (v23.12 وقت كتابة هذا الدليل) وتحتاج فقط إلى حزمة NuGet `Aspose.Cells`. لا يلزم تثبيت Excel خارجي.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يُجمّع أيضًا على .NET Framework 4.7.2).  
- Visual Studio 2022 أو أي بيئة تطوير تدعم C#.  
- حزمة NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).  

> **نصيحة احترافية:** إذا كنت تستخدم خط أنابيب CI/CD، أضف إشارة الحزمة إلى ملف المشروع بدلاً من تثبيتها عالميًا. هذا يضمن بناءً قابلًا لإعادة الإنتاج.

## الخطوة 1: إنشاء دفتر عمل والوصول إلى ورقة العمل الأولى

كائن دفتر العمل هو نقطة الدخول لجميع عمليات الجداول. إن إنشاؤه في الذاكرة يجنب أي تأثيرات جانبية على نظام الملفات حتى تقوم بحفظه صراحةً.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1 – instantiate a new workbook and get the first worksheet
        Workbook wb = new Workbook();               // empty workbook with one sheet
        Worksheet ws = wb.Worksheets[0];            // reference to Sheet1
```

**لماذا هذا مهم:**  
Aspose.Cells ينشئ ورقة عمل افتراضية (`Sheet1`) تلقائيًا. الوصول إليها عبر `Worksheets[0]` يضمن أنك تكتب في موقع معروف، مما يُزيل أخطاء “الورقة غير موجودة” لاحقًا.

## الخطوة 2: إضافة قيمة بسيطة ستقرأها دالة EXPAND

دالة `EXPAND` تحتاج إلى خلية مصدر. هنا نضع قيمة رقمية في **B1** ستُوسّع إلى مصفوفة عمودية.

```csharp
        // Step 2 – write a source value in B1
        ws.Cells["B1"].PutValue(42);   // any numeric value works
```

**حالة حافة:** إذا كانت `B1` فارغة، تُعيد `EXPAND` خطأ `#VALUE!`. تأكد دائمًا من أن الخلية المصدر تحتوي على رقم صالح أو صيغة تُعيد رقمًا.

## الخطوة 3: استخدام دالة EXPAND لإنشاء مصفوفة مكوّنة من 5 صفوف

الآن نكتب صيغة إلى **A1** تُوسّع القيمة من **B1** إلى نطاق مكوّن من 5 صفوف وعمود واحد. هذا يوضح **كيفية استخدام EXPAND** ويُظهر أيضًا **استخدام دالة EXPAND**.

```csharp
        // Step 3 – write the EXPAND formula in A1
        // =EXPAND(B1,5,1) creates a vertical array of 5 rows based on B1
        ws.Cells["A1"].Formula = "=EXPAND(B1,5,1)";
```

**لماذا EXPAND؟**  
`EXPAND` هي دالة مصفوفة ديناميكية تم تقديمها في Excel 365. تُزيل الحاجة إلى صيغ المصفوفة القديمة `Ctrl+Shift+Enter` وتُسقِط النتائج تلقائيًا إلى الخلايا المجاورة. في هذا المثال سيشغل النتيجة النطاق **A1:A5**، حيث تُظهر كل خلية القيمة `42`.

## الخطوة 4: كتابة الصيغة التي **كيفية حساب الظل المقلوب**

الظل المقلوب لزاوية θ هو `1 / tan(θ)`. يوفر Excel دالة مدمجة `COT`، لذا يمكننا حساب `cot(π/4)` مباشرة. يجب أن تكون النتيجة `1`.

```csharp
        // Step 4 – calculate cotangent of π/4 in A2
        ws.Cells["A2"].Formula = "=COT(PI()/4)";
```

**شرح:**  
- `PI()` تُعيد الثابت الرياضي π.  
- `PI()/4` تُقيم إلى π/4 (45 درجة).  
- `COT` تُعيد الظل المقلوب لتلك الزاوية، وهو `1`.  

إذا احتجت يومًا إلى الظل المقلوب لزاوية متغيرة مخزنة في خلية (مثل `B2`)، استبدل القيمة الثابتة بالإشارة: `=COT(B2)`.

## الخطوة 5: إجبار دفتر العمل على **تقييم جميع الصيغ**

بشكل افتراضي، يكتب Aspose.Cells الصيغ إلى الملف دون حساب نتائجها. لتخزين القيم المحسوبة، استدعِ `CalculateFormula()`.

```csharp
        // Step 5 – evaluate every formula in the workbook
        wb.CalculateFormula();
```

**ماذا يحدث تحت الغطاء؟**  
Aspose.Cells يحلل كل صيغة، يبني شجرة تنفيذ، ويحساب القيم باستخدام محرك حسابه الخاص. هذا يُحاكي سلوك Excel، مما يضمن أن الملف المحفوظ يحتوي على النتائج بدلاً من الصيغ فقط.

## الخطوة 6: حفظ دفتر العمل والتحقق من المخرجات

أخيرًا، احفظ دفتر العمل على القرص وربما اطبع القيم المحسوبة إلى وحدة التحكم للتحقق السريع.

```csharp
        // Step 6 – save the workbook
        string outPath = "CotangentAndExpandDemo.xlsx";
        wb.Save(outPath);

        // Optional: display calculated values in the console
        Console.WriteLine("A1–A5 (EXPAND result):");
        for (int row = 0; row < 5; row++)
        {
            Console.WriteLine($"A{row + 1} = {ws.Cells[row, 0].StringValue}");
        }
        Console.WriteLine($"A2 (COT result) = {ws.Cells["A2"].StringValue}");
        Console.WriteLine($"Workbook saved to {outPath}");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، تُظهر وحدة التحكم:

```
A1–A5 (EXPAND result):
A1 = 42
A2 = 42
A3 = 42
A4 = 42
A5 = 42
A2 (COT result) = 1
Workbook saved to CotangentAndExpandDemo.xlsx
```

فتح *CotangentAndExpandDemo.xlsx* في Excel يُؤكد:

- الخلايا **A1:A5** تحتوي على `42` (المصفوفة الموسعة).  
- الخلية **A2** تُظهر `1` (الظل المقلوب للزاوية π/4).  

جميع الصيغ استُبدلت بالقيم المُقيمة لأننا استدعينا `wb.CalculateFormula()`.

## الأسئلة الشائعة واستكشاف الأخطاء وإصلاحها

| السؤال | الإجابة |
|----------|--------|
| **ماذا لو احتجت إلى مصفوفة أفقية؟** | استخدم `=EXPAND(B1,1,5)` – يصبح الوسيط الثاني (`rows`) 1 والثالث (`columns`) 5، مما يُسقِط النتائج إلى **A1:E1**. |
| **هل يمكنني توسيع نطاق بدلاً من خلية واحدة؟** | نعم. `=EXPAND(B1:B3,5,1)` سيُعيد تكرار المصدر المكوّن من ثلاثة صفوف لملء نتيجة مكوّنة من 5 صفوف، مع القص أو الحشو حسب الحاجة. |
| **لماذا تُعيد `COT` الخطأ `#DIV/0!` لبعض الزوايا؟** | `COT(θ) = 1 / tan(θ)`. إذا كان `tan(θ)` صفرًا (مثل θ = 0، π، 2π)، تكون النتيجة غير معرفة، مما يؤدي إلى خطأ قسمة على صفر. |
| **هل أحتاج إلى تمكين أي خيارات حساب؟** | لا. Aspose.Cells يُفعِّل وضع الحساب الكامل تلقائيًا عند استدعاء `CalculateFormula()`. |
| **هل تُدعم دالة EXPAND في إصدارات Excel القديمة؟** | `EXPAND` تتطلب Excel 365 أو أحدث. إذا كنت تستهدف إصدارات أقدم، فكر في استخدام صيغ المصفوفة القديمة أو ملء الخلايا يدويًا عبر الكود. |

## أفضل الممارسات عند العمل مع الصيغ في Aspose.Cells

1. **التحقق من صحة البيانات المصدر** – تأكد من أن الخلايا التي تُشير إليها `EXPAND` أو `COT` تحتوي على أرقام لتجنب أخطاء `#VALUE!`.  
2. **إعادة استخدام كائن دفتر العمل** – إنشاء نسخة واحدة من `Workbook` وإعادة استخدامها للعمليات المتعددة يقلل من استهلاك الذاكرة.  
3. **الحفظ بالصيغ المناسبة** – `.xlsx` يحتفظ بصيغ المصفوفات الديناميكية؛ `.xls` سيُحوِّلها إلى قيم ثابتة.  
4. **إحاطة الحسابات بكتل try/catch** – قد تُطلق عملية تحليل الصيغ استثناء `CellsException` إذا كان التركيب غير صالح.  

## الخلاصة

أنت الآن تعرف **كيفية حساب الظل المقلوب** في C# عبر **إضافة صيغة إلى خلية**، واستخدام دالة **EXPAND** لإنشاء مصفوفات ديناميكية، و**تقييم جميع الصيغ** باستخدام Aspose.Cells. يُظهر المثال الكامل سير عمل نظيف من إنشاء دفتر العمل إلى التحقق من النتائج، جاهزًا للتكامل في تقارير أو خطوط معالجة بيانات أكبر.

الخطوات التالية التي قد تستكشفها:

- **كيفية استخدام EXPAND** مع مصفوفات متعددة الأعمدة للبيانات على نمط المصفوفات.  
- **إضافة صيغة إلى خلية** بشكل ديناميكي بناءً على إدخال المستخدم أو ملفات الإعداد.  
- **تقييم جميع الصيغ** في دفتر عمل متعدد الأوراق مع إعدادات حساب مخصصة (مثل الحسابات التكرارية).  

لا تتردد في تجربة دوال رياضية أخرى (`SIN`, `COS`, `TAN`, `COT`) ودمجها مع `EXPAND` لبناء حاسبات قوية مدفوعة بالجداول مباشرةً من C#. استمتع

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروح خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية حساب الظل المقلوب في Excel باستخدام C# – دليل خطوة‑بخطوة](/cells/english/net/excel-formulas-and-calculation-options/how-to-calculate-cotangent-in-excel-with-c-step-by-step-guid/)
- [كيفية تقييم الصيغ في C# – دليل Aspose.Cells الكامل](/cells/english/net/calculation-engine/how-to-evaluate-formulas-in-c-complete-aspose-cells-guide/)
- [كيفية توسيع المصفوفة في C# باستخدام Aspose.Cells – دليل خطوة‑بخطوة](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}