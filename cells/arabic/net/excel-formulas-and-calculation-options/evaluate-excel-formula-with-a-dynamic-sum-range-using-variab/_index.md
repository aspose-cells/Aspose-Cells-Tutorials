---
category: general
date: 2026-11-19
description: قيّم صيغة إكسل بشكل ديناميكي باستخدام المتغيرات لإنشاء نطاق جمع مرن.
  تعلم كيفية أتمتة صيغة الجمع في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- evaluate excel formula
- dynamic sum range
- automate sum formula
- use variables formula
- create dynamic range sum
language: ar
lastmod: 2026-11-19
og_description: قيّم صيغة إكسل باستخدام المتغيرات لتلقائيًا إنشاء صيغة الجمع. اتبع
  هذا الدليل خطوة بخطوة لحسابات إكسل مرنة.
og_image_alt: Screenshot of an Excel worksheet showing a SUM formula with placeholders
  replaced by actual range
og_title: تقييم صيغة إكسل – دليل النطاق الديناميكي للجمع
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Evaluate Excel formula dynamically by using variables to create a flexible
    sum range. Learn how to automate sum formula in minutes.
  headline: Evaluate Excel formula with a dynamic sum range using variables
  type: TechArticle
- description: Evaluate Excel formula dynamically by using variables to create a flexible
    sum range. Learn how to automate sum formula in minutes.
  name: Evaluate Excel formula with a dynamic sum range using variables
  steps:
  - name: Why use a dynamic sum range?
    text: '* **Flexibility** – The same code works for any number of rows. * **Maintainability**
      – Change the range in one place instead of updating many formulas. * **Automation**
      – Perfect for generating reports where the data size is not known ahead of time.'
  - name: Defining the variables
    text: '```csharp // 5️⃣ Create a MacroProcessor instance (no macro file needed
      for simple substitution) MacroProcessor macroProcessor = new MacroProcessor();'
  - name: Quick verification in Excel
    text: 'Open `DynamicSum_Evaluated.xlsx` in Excel. You should see:'
  - name: Typical mistakes and how to avoid them
    text: '| Symptom | Cause | Fix | |--------------------------------------|--------------------------------------------|-----|
      | `#NAME?` error in A1 | Variable name typo (`Startrow` vs `StartRow`) | Ensure
      the dictionary keys match the placeholder names exactly, case‑sensitive. | |
      Formula not recalculated '
  type: HowTo
tags:
- Excel
- C#
- MacroProcessor
title: تقييم صيغة إكسل بنطاق جمع ديناميكي باستخدام المتغيرات
url: /ar/net/excel-formulas-and-calculation-options/evaluate-excel-formula-with-a-dynamic-sum-range-using-variab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تقييم صيغة Excel بنطاق جمع ديناميكي باستخدام المتغيرات

إذا كنت بحاجة إلى **evaluate Excel formula** التي تتكيف مع البيانات المتغيرة، يوضح لك هذا الدليل كيفية القيام بذلك باستخدام **dynamic sum range**. باستخدام **variables in the formula** يمكنك **automate sum formula** دون ترميز عناوين الخلايا يدويًا، مما يجعل جداولك أكثر قابلية للصيانة وكودك أكثر قابلية لإعادة الاستخدام.

في هذا الدرس ستقوم بـ:

* إعداد ورقة عمل بأرقام نموذجية.
* كتابة صيغة تحتوي على نواقل للصفوف البداية والنهاية.
* تعريف تلك النواقل باستخدام ميزة **use variables formula**.
* معالجة ورقة العمل بحيث يتم استبدال النواقل وتعيد خطوة **evaluate Excel formula** المجموع الصحيح.
* التحقق من النتيجة ورؤية كيفية **create dynamic range sum** للمنطق في سيناريوهات العالم الحقيقي.

> **المتطلبات المسبقة** – تحتاج إلى بيئة تطوير .NET (Visual Studio 2022 أو أحدث) ومكتبة Aspose.Cells for .NET، التي توفر الفئة `MacroProcessor` المستخدمة في الأمثلة.

---

## تقييم صيغة Excel بنطاق جمع ديناميكي

الفكرة الأساسية هي كتابة تعبير Excel `SUM` عادي، ولكن استبدال مراجع الخلايا بمتغيرات تقوم بتحديدها أثناء التشغيل. عندما يعمل المعالج الماكرو، يستبدل المتغيرات، يُدخل نطاقًا محددًا، ثم **evaluates Excel formula** كما يفعل Excel.

### لماذا استخدام نطاق جمع ديناميكي؟

* **Flexibility** – يعمل نفس الكود لأي عدد من الصفوف.
* **Maintainability** – غيّر النطاق في مكان واحد بدلاً من تحديث العديد من الصيغ.
* **Automation** – مثالي لإنشاء تقارير حيث لا يُعرف حجم البيانات مسبقًا.

---

## إعداد ورقة العمل والبيانات النموذجية

أولاً أنشئ مصنفًا جديدًا واملأ عمودًا بالأرقام. الكود التالي ينشئ مصنفًا، يضيف قيمًا إلى الخلايا **B2‑B10**، ويحفظه باسم `DynamicSum.xlsx` للفحص.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Macros;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Name = "Data";

        // 2️⃣ Populate column B with sample numbers (2‑10)
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"B{i}"].PutValue(i); // B2 = 2, B3 = 3, … B10 = 10
        }

        // 3️⃣ Save the initial file so you can see the raw data
        workbook.Save("DynamicSum.xlsx");
        Console.WriteLine("Worksheet with sample data created.");
    }
}
```

**شرح**

* `Workbook` هو نقطة الدخول لجميع عمليات Excel.
* `worksheet.Cells[$"B{i}"].PutValue(i)` يكتب قيمة رقمية في كل خلية في العمود **B**.
* حفظ الملف يتيح لك فتحه في Excel وتأكيد البيانات قبل تطبيق الصيغة.

## استخدام صيغة المتغيرات لتحديد النطاق

الآن نضيف صيغة تشير إلى نواقل `${var:StartRow}` و `${var:EndRow}`. سيتم استبدال هذه النواقل لاحقًا بعناوين خلايا فعلية.

```csharp
// 4️⃣ Assign a formula that uses variable placeholders for the start and end rows
worksheet.Cells["A1"].Formula = "=SUM(${var:StartRow}:${var:EndRow})";
```

في هذه المرحلة تحتوي الخلية **A1** على النص الحرفي `=SUM(${var:StartRow}:${var:EndRow})`. لن يفهم Excel ذلك، لكن **MacroProcessor** سيستبدل المتغيرات قبل التقييم.

### تعريف المتغيرات

```csharp
// 5️⃣ Create a MacroProcessor instance (no macro file needed for simple substitution)
MacroProcessor macroProcessor = new MacroProcessor();

// 6️⃣ Define the actual rows that the placeholders should represent
macroProcessor.Options.Variables["StartRow"] = "B2";
macroProcessor.Options.Variables["EndRow"]   = "B10";
```

**لماذا هذا يعمل**

* `MacroProcessor.Options.Variables` هو قاموس حيث كل مفتاح هو اسم المتغير (بدون الغلاف `${var:}`) والقيمة هي السلسلة التي ستحل محل الناقل.
* بتعيين `StartRow` إلى `"B2"` و `EndRow` إلى `"B10"` نخبر المعالج بإنشاء النطاق `B2:B10`.

## معالجة وتقييم الصيغة

بعد تعريف المتغيرات، استدعِ `Process` لاستبدال النواقل والسماح لـ Excel بإعادة حساب الخلية.

```csharp
// 7️⃣ Process the worksheet so the placeholders are replaced and the formula is evaluated
macroProcessor.Process(worksheet, null);

// 8️⃣ Save the workbook with the evaluated result
workbook.Save("DynamicSum_Evaluated.xlsx");

// 9️⃣ Read back the calculated value for verification
double result = worksheet.Cells["A1"].DoubleValue;
Console.WriteLine($"The dynamic sum of B2:B10 is {result}");
```

**ما يحدث داخليًا**

1. `MacroProcessor.Process` يفحص كل صيغة في ورقة العمل.
2. يجد `${var:StartRow}` و `${var:EndRow}` ويستبدلهما بـ `"B2"` و `"B10"`.
3. تصبح الصيغة `=SUM(B2:B10)`.
4. Aspose.Cells يعيد حساب الورقة، لذا فإن `A1` الآن يحتوي على النتيجة الرقمية للمجموع.

**الناتج المتوقع**

```
The dynamic sum of B2:B10 is 54
```

لأن 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10 = 54، فإن خطوة **evaluate Excel formula** تنجح.

## التحقق من النتيجة ومشكلات شائعة

### تحقق سريع في Excel

افتح `DynamicSum_Evaluated.xlsx` في Excel. يجب أن ترى:

* العمود **B** مملوء بالأرقام 2‑10.
* الخلية **A1** تُظهر **54** (مجموع النطاق).
* شريط الصيغة للخلية **A1** يعرض `=SUM(B2:B10)` – النواقل اختفت.

### أخطاء شائعة وكيفية تجنبها

| Symptom                              | Cause                                      | Fix |
|--------------------------------------|--------------------------------------------|-----|
| `#NAME?` error in A1                 | خطأ إملائي في اسم المتغير (`Startrow` بدلاً من `StartRow`) | تأكد من أن مفاتيح القاموس تطابق أسماء النواقل تمامًا، مع مراعاة حساسية الحالة. |
| Formula not recalculated             | `MacroProcessor.Process` تم استدعاؤه مع `CalculationOptions` غير فارغ يعطل الحساب التلقائي | مرّر `null` أو `CalculationOptions` مع `CalculateOnOpen = true`. |
| Unexpected range (e.g., `B2:B9`)    | قيمة المتغير تفتقد رقم الصف النهائي | تحقق مرة أخرى من القيمة المعينة لـ `EndRow`. |
| Performance slowdown on large sheets| إعادة معالجة المصنف بالكامل لخلية واحدة | استخدم `macroProcessor.Process(worksheet, new string[] { "A1" })` لتحديد معالجة خلايا معينة. |

## إنشاء جمع نطاق ديناميكي في المشاريع الحقيقية

الآن بعد أن فهمت الآلية، يمكنك توسيع النمط:

* **Dynamic columns** – استخدم `${var:Column}` مع متغيرات الصفوف لجمع عبر الأعمدة.
* **Multiple ranges** – دمج النطاقات بفواصل: `=SUM(${var:Range1},${var:Range2})`.
* **User‑driven ranges** – عَبِّئ المتغيرات من مدخلات واجهة المستخدم، أو معلمات API، أو ملفات التكوين.

**نصيحة احترافية:** احفظ قاموس المتغيرات في فئة تكوين منفصلة حتى تتمكن من إعادة استخدامه عبر عدة أوراق عمل أو مصنفات.

## الخاتمة

لقد تعلمت كيفية **evaluate Excel formula** عن طريق **إنشاء نطاق جمع ديناميكي** باستخدام تقنية **use variables formula** وكيفية **automate sum formula** في C#. يوضح المثال الكامل إعداد البيانات النموذجية، تعريف النواقل، معالجة ورقة العمل، والتحقق من النتيجة، مما يمنحك أساسًا قويًا لـ **create dynamic range sum** لأي مهمة تقارير أو تحليل بيانات.

لا تتردد في التجربة:

* غيّر `StartRow` و `EndRow` إلى

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء ملف Excel Java – دليل صيغة SUM في Excel](/cells/english/java/basic-excel-functions/excel-sum-formula-guide/)
- [كيفية إنشاء مصنف Excel C# بصيغة مصفوفة ديناميكية](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [إنشاء مصنف Excel مع صيغة EXPAND – دليل كامل](/cells/english/net/formulas-functions/create-excel-workbook-with-expand-formula-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}