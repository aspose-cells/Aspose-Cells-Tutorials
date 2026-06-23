---
category: general
date: 2026-03-22
description: تعلم كيفية تكرار الجدول المحوري في C# باستخدام Aspose.Cells. يوضح هذا
  الدليل أيضًا كيفية نسخ الصفوف وتحميل دفتر عمل Excel باستخدام C# لتسهيل أتمتة Excel
  السلسة لنسخ الصفوف.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: ar
og_description: كيف تنسخ Pivot في C#؟ اتبع هذا الدليل المختصر لتحميل ملف Excel باستخدام
  C#، نسخ الصفوف، وإتقان أتمتة Excel لنسخ الصفوف.
og_title: كيفية تكرار Pivot في C# – دليل شامل
tags:
- C#
- Excel Automation
- Aspose.Cells
title: كيفية تكرار Pivot في C# – دليل خطوة بخطوة كامل
url: /ar/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار Pivot في C# – دليل خطوة بخطوة كامل

هل تساءلت يومًا **how to duplicate pivot** عن جداول Pivot برمجيًا دون سحبها يدويًا في Excel؟ لست وحدك. في العديد من خطوط تقارير البيانات يُحتاج إلى نفس تخطيط Pivot على مجموعة جديدة من الصفوف، والقيام بذلك يدويًا مضيعة للوقت.  

الأخبار السارة؟ ببضع أسطر من C# يمكنك تحميل مصنف Excel، تعريف المنطقة التي تحتوي على الـ pivot، و **how to copy rows** بحيث يظهر الـ pivot في موقع جديد — كل ذلك في تشغيل آلي واحد. في هذا الدرس سنغطي أيضًا أساسيات **load excel workbook c#** ونقدم لك أساسًا قويًا لمهام **excel automation copy rows**.

> **ما ستخرجه من هذا الدرس**  
> • مثال كامل وقابل للتنفيذ يكرر جدول Pivot.  
> • شرح لماذا كل سطر مهم.  
> • نصائح للتعامل مع الحالات الخاصة مثل أوراق العمل المخفية أو وجود عدة Pivot.

---

## المتطلبات المسبقة

قبل أن نغوص في التفاصيل، تأكد من وجود ما يلي:

- **.NET 6.0** (أو أي نسخة حديثة من .NET) مثبتة.  
- **Aspose.Cells for .NET** – المكتبة التي سنستخدمها للتعامل مع ملفات Excel. يمكنك الحصول عليها عبر NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- مصنف مصدر (`Source.xlsx`) يحتوي بالفعل على جدول Pivot في النطاق **A1:J20** (النطاق الذي سنقوم بتكراره).  
- إلمام أساسي بصياغة C# – لا شيء معقد، فقط عبارات `using` المعتادة وطريقة `Main`.

إذا كان أي من هذه غير مألوف لك، خذ لحظة لتثبيت الحزمة؛ باقي الدليل يفترض أن المكتبة جاهزة للاستخدام.

![Illustration of how to duplicate pivot in C# using Aspose.Cells](https://example.com/duplicate-pivot.png "how to duplicate pivot in C# illustration")

*نص بديل للصورة: "how to duplicate pivot in C# example showing source and duplicated pivot rows".*

## الخطوة 1: Load Excel Workbook C# – فتح الملف

أول شيء تحتاج إلى القيام به عندما تريد **load excel workbook c#** هو إنشاء كائن `Workbook` يشير إلى ملفك. هذا الكائن يمنحك الوصول إلى كل ورقة عمل، خلية، وPivot داخل الملف.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**لماذا هذا مهم:**  
`Workbook` يُجسد ملف Excel بالكامل كنموذج في الذاكرة. بدون تحميله أولًا لا يمكنك فحص موقع الـ Pivot أو نسخ الصفوف. بالإضافة إلى ذلك، المُنشئ يكتشف تنسيق الملف تلقائيًا (XLS, XLSX, CSV، إلخ)، لذا لا تحتاج إلى كود إضافي لاكتشاف التنسيق.

## الخطوة 2: How to Copy Rows – تعريف منطقة Pivot

الآن بعد أن أصبح المصنف في الذاكرة، نحتاج إلى إخبار Aspose.Cells أي صفوف تحتوي على الـ Pivot. في مثالنا الـ Pivot موجود في **A1:J20**، ما يترجم إلى الصفوف **0‑19** (فهرسة صفرية). سنغلف ذلك في هيكل `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**لماذا نستخدم `CellArea`:**  
إنه طريقة خفيفة لوصف كتلة مستطيلة. عندما تستدعي لاحقًا `CopyRows`، يقرأ الطريقة هذا الكائن لتعرف بالضبط أي صفوف يجب تكرارها. إذا احتجت لتعديل النطاق (مثلاً إذا نما الـ Pivot إلى العمود K)، ما عليك سوى تغيير قيمة `endColumn`.

## الخطوة 3: الوصول إلى ورقة العمل الهدف

معظم المصنفات تحتوي على ورقة واحدة، لكن الـ API يعمل بنفس الطريقة مع عدة أوراق. احصل على الورقة الأولى (الفهرس 0) – حيث يعيش الـ Pivot الأصلي.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**نصيحة احترافية:**  
إذا كان لديك أوراق مسماة، يمكنك أيضًا استرجاعها بالاسم: `workbook.Worksheets["Sheet1"]`. هذا يساعد على تجنب الترميز الصلب للفهارس عندما يتغير هيكل المصنف.

## الخطوة 4: How to Copy Rows – تكرار جدول Pivot

هذا هو جوهر **how to duplicate pivot**: ننسخ الصفوف التي تحتوي على الـ Pivot إلى موقع جديد. في حالتنا نبدأ عند الصف 31 (فهرس صفرية 30). طريقة `CopyRows` تنسخ *كلا* البيانات وذاكرة التخزين المؤقت للـ Pivot، لذا تتصرف الصفوف الجديدة تمامًا مثل الأصل.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**ما يحدث خلف الكواليس؟**  
`CopyRows` تستنسخ كل صف، مع الحفاظ على الصيغ، الأنماط، وتعريفات الـ Pivot. لأن ذاكرة الـ Pivot تُخزن على مستوى المصنف، فإن الـ Pivot المكرر يشير تلقائيًا إلى نفس مصدر البيانات – لا حاجة لتكوين إضافي.

**حالة خاصة – الصفوف المخفية:**  
إذا كان أي من الصفوف في النطاق المصدر مخفيًا، سيظل مخفيًا بعد النسخ. إذا رغبت في إظهاره، استدعِ `worksheet.Rows[destRow].IsHidden = false` بعد عملية النسخ.

## الخطوة 5: حفظ المصنف – التحقق من النسخة المكررة

أخيرًا، اكتب التغييرات إلى القرص. يمكنك استبدال الملف الأصلي أو، للأمان، حفظه باسم جديد لتتمكن من مقارنة قبل/بعد.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**النتيجة التي يجب أن تراها:**  
افتح `CopyWithPivot.xlsx`. ستجد الـ Pivot الأصلي في **A1:J20** ونسخة مطابقة تبدأ من **A31:J50**. يمكن تحديث كلا الـ Pivot بشكل مستقل، وأي مقاطع (slicers) مرتبطة بالأصل ستظل تعمل مع النسخة لأنها تشترك في نفس الذاكرة المؤقتة.

## أسئلة شائعة وتنوعات

### هل يمكنني تكرار عدة Pivot في آن واحد؟

بالطبع. يمكنك التكرار عبر جميع جداول الـ Pivot (`worksheet.PivotTables`) ونسخ نطاق كل منها إلى وجهة مختلفة. فقط تأكد من أن النطاقات الوجهة لا تتداخل.

### ماذا لو كان المصنف المصدر محميًا بكلمة مرور؟

Aspose.Cells يتيح لك فتح ملف محمي بتمرير كلمة المرور إلى مُنشئ `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### كيف أُنسخ الصفوف دون التأثير على الصيغ؟

إذا كنت تحتاج فقط إلى *القيم* (بدون صيغ)، استخدم `CopyRows` مع علم `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### هل هناك طريقة لنسخ الصفوف إلى مصنف *مختلف*؟

نعم. بعد نسخ الصفوف في الورقة المصدر، يمكنك استنساخ الورقة إلى كائن `Workbook` آخر عبر `targetWorkbook.Worksheets.AddCopy(worksheet)`.

## نصائح احترافية لأتمتة Excel موثوقة Copy Rows

- **تحقق من النطاق** قبل النسخ. شرط سريع `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` يمنع الأخطاء الناتجة عن الخروج عن النطاق.  
- **أوقف الحساب** أثناء نسخ النطاقات الكبيرة: `workbook.Settings.CalcMode = CalcMode.Manual;` – هذا يسرّع العملية بشكل ملحوظ.  
- **حرّر الكائنات** (`workbook.Dispose()`) إذا كنت تعالج العديد من الملفات في حلقة لتفريغ الموارد الأصلية.  
- **سجّل العملية** – خاصة في خطوط الإنتاج – لتتمكن من تتبع الملفات التي تم معالجتها واكتشاف الأخطاء مبكرًا.

## الخاتمة

الآن تعرف **how to duplicate pivot** في C# باستخدام Aspose.Cells، ورأيت سير العمل الكامل من **load excel workbook c#** إلى **excel automation copy rows** وأخيرًا حفظ النتيجة. المثال مستقل، يعمل مباشرة، ويمكن توسيعه للتعامل مع عدة Pivot، ملفات محمية، أو نسخ عبر مصنفات مختلفة.

الخطوات التالية؟ جرّب تعديل السكريبت لتقوم بـ:

- تحديث الـ Pivot المكرر برمجيًا (`pivotTable.RefreshData();`).  
- تصدير المنطقة المكررة إلى CSV للمعالجة اللاحقة.  
- دمج الكود في API مبني على ASP.NET Core بحيث يمكن للمستخدمين رفع ملف والحصول فورًا على نسخة مكررة من الـ Pivot.

برمجة سعيدة، ولتكن أتمتة Excel لديك سلسة دائمًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}