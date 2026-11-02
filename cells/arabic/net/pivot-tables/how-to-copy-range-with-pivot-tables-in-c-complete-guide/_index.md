---
category: general
date: 2026-03-29
description: تعلم كيفية نسخ النطاق، نسخ الجداول المحورية، وكيفية حفظ المصنف وتحميله
  في C#. انقل الجداول المحورية بسهولة باستخدام كود خطوة بخطوة.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: ar
og_description: كيفية نسخ النطاق، نسخ الجداول المحورية، كيفية حفظ المصنف وكيفية تحميل
  المصنف في C#. نقل الجداول المحورية بسهولة مع كود واضح.
og_title: كيفية نسخ النطاق مع الجداول المحورية في C# – دليل شامل
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية نسخ النطاق مع جداول Pivot في C# – دليل كامل
url: /ar/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ النطاق مع جداول Pivot في C# – دليل شامل

هل تساءلت يومًا **كيفية نسخ النطاق** الذي يحتوي على جدول Pivot دون كسر الرابط إلى بيانات المصدر؟ لست وحدك. في العديد من المشاريع الواقعية صادفت هذه المشكلة بالضبط—تصل ملفات Excel بجداول Pivot متقدمة، والمتطلب هو إعادة وضعها أو تكرار البيانات في مكان آخر.  

الخبر السار؟ الحل بسيط جدًا بمجرد أن تعرف **كيفية تحميل دفتر العمل**، إنشاء نسخة، ثم **كيفية حفظ دفتر العمل** مرة أخرى. في هذا الدرس سنستعرض العملية بالكامل، بما في ذلك كيفية **نسخ جداول Pivot**، وحتى نصيحة سريعة حول **نقل جدول Pivot** إذا كنت تحتاجه في مكان آخر داخل نفس الورقة.

بنهاية هذا الدليل ستحصل على مقطع C# كامل الوظيفة الذي:

1. يقوم بتحميل ملف Excel موجود.  
2. ينسخ نطاقًا (بما في ذلك جدول Pivot) إلى موقع جديد.  
3. يحفظ دفتر العمل المعدل إلى ملف جديد.

بدون سكريبتات خارجية، ولا تعديل يدوي—فقط كود نظيف وقابل لإعادة الاستخدام.

---

## المتطلبات المسبقة

- **.NET 6+** (أي إصدار حديث يعمل).  
- **Aspose.Cells for .NET** – المكتبة التي توفر `Workbook`، `WorksheetCopyOptions`، إلخ. يمكنك تثبيتها عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

- دفتر عمل إدخال (`input.xlsx`) يحتوي بالفعل على جدول Pivot في النطاق `A1:G20`.  
- إلمام أساسي بـ C# و Visual Studio (أو بيئة التطوير المفضلة لديك).

> **نصيحة احترافية:** إذا كنت تستخدم مكتبة Excel مختلفة (مثل EPPlus)، فإن المفاهيم هي نفسها—فقط استبدل استدعاءات الـ API.

## الخطوة 1 – كيفية تحميل دفتر العمل (الإعداد الأساسي)

قبل أن نتمكن من نسخ أي شيء، نحتاج إلى تحميل ملف Excel إلى الذاكرة.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**لماذا هذا مهم:**  
تحميل دفتر العمل يمنحك نموذج كائن يمكنك التلاعب به. بدون `how to load workbook` بشكل صحيح، أي عملية نسخ لاحقة ستؤدي إلى استثناء *FileNotFound* أو *InvalidOperation*.

> **احذر:** إذا كان الملف كبيرًا، فكر في استخدام `LoadOptions` مع `MemorySetting` للتحكم في استهلاك الذاكرة.

## الخطوة 2 – كيفية نسخ النطاق (بما في ذلك الـ Pivot)

الآن يأتي نجمة العرض: نسخ نطاق يحتوي على جدول Pivot. طريقة `CopyRange`، مع `WorksheetCopyOptions`، تقوم بالعمل الشاق.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**لماذا نضبط `CopyPivotTables = true`:**  
بشكل افتراضي، نسخ النطاق ينقل الخلايا الخام فقط. يبقى مخزن الـ Pivot خلفًا، ويصبح الـ Pivot المنسوخ جدولًا ثابتًا. ضبط `CopyPivotTables` يحافظ على الاتصال الحي، بحيث يظل الـ Pivot المنسوخ يحدث عندما تتغير بيانات المصدر.

**حالة حافة:** إذا كان النطاق الوجهة يتداخل مع المصدر، سيُصدر Aspose.Cells استثناء `ArgumentException`. اختر دائمًا هدفًا غير متداخل، أو أنشئ ورقة عمل جديدة أولاً.

## الخطوة 3 – كيفية حفظ دفتر العمل (حفظ التغييرات)

بعد النسخ، سترغب في كتابة التغييرات مرة أخرى إلى القرص. هنا يأتي دور **كيفية حفظ دفتر العمل**.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**ما يحدث خلف الكواليس:**  
`Save` يُسلسل دفتر العمل الموجود في الذاكرة، بما في ذلك جدول الـ Pivot المنسوخ حديثًا، إلى حزمة `.xlsx` قياسية. إذا كنت تحتاج إلى تنسيق مختلف (CSV، PDF، إلخ)، فقط غير امتداد الملف أو استخدم الدالة المتعددة التي تقبل `SaveFormat`.

> **نصيحة:** استخدم `Workbook.Save(string, SaveOptions)` إذا كنت بحاجة لحماية الملف بكلمة مرور أو ضبط خيارات تصدير أخرى.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**النتيجة المتوقعة:**  
افتح `output.xlsx`. سترى جدول الـ Pivot الأصلي لا يزال في `A1:G20`، ونسخة مطابقة بالكامل تعمل بدءًا من `A25`. كلا الـ Pivot يشيران إلى نفس بيانات المصدر، لذا تحديث أحدهما يحدّث الآخر.

## الأسئلة المتكررة والاختلافات

### هل يمكنني **نقل جدول Pivot** بدلاً من نسخه؟

بالتأكيد. بعد النسخ، قم ببساطة بمسح النطاق الأصلي (أو استخدم `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) ثم أعد تسمية نطاق الوجهة إذا لزم الأمر. هذا ينقل الـ Pivot فعليًا.

### ماذا لو كان الـ Pivot يستخدم مصدر بيانات خارجي؟

`CopyPivotTables = true` ينسخ فقط تعريف الـ Pivot، وليس الاتصال الخارجي نفسه. تأكد من أن دفتر العمل الهدف لديه إمكانية الوصول إلى نفس مصدر البيانات، أو أعد إنشاء الاتصال بعد النسخ.

### كيف يمكنني النسخ إلى **ورقة عمل مختلفة**؟

فقط مرّر كائن ورقة العمل الوجهة بدلاً من `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### هل هناك طريقة لنسخ **نطاقات متعددة** مرة واحدة؟

يمكنك استدعاء `CopyRange` بشكل متكرر أو استخدام `CopyRows`/`CopyColumns` للكتل الأكبر. التكرار على قائمة من سلاسل العناوين هو نهج نظيف.

## الأخطاء الشائعة والنصائح الاحترافية

- **حجم مخزن الـ Pivot:** مخازن الـ Pivot الكبيرة يمكن أن تزيد حجم دفتر العمل بشكل كبير. إذا كنت تحتاج فقط إلى البيانات المعروضة، فكر في ضبط `CopyPivotTables = false` ثم استخدم `PivotTable.RefreshData()` على الوجهة.  
- **مسارات الملفات:** استخدم `Path.Combine` لتجنب الفواصل المكتوبة صراحةً، خاصةً في .NET متعدد المنصات.  
- **الأداء:** بالنسبة لدفاتر العمل الضخمة، غلف عملية النسخ داخل `using (var stream = new MemoryStream())` واحفظ إلى الذاكرة أولاً، ثم اكتب إلى القرص. هذا يقلل من عبء الإدخال/الإخراج.

## الخلاصة

أنت الآن تعرف **كيفية نسخ النطاق** الذي يحتوي على جدول Pivot، وكيفية **نسخ جداول Pivot**، والخطوات الدقيقة لـ **كيفية تحميل دفتر العمل** و**كيفية حفظ دفتر العمل** بعد العملية. سواء كنت تحتاج إلى **نقل جدول Pivot** داخل نفس الورقة أو إلى ورقة عمل أخرى، يبقى النمط نفسه—تحميل، نسخ مع الخيارات الصحيحة، ثم حفظ.

جرّبه مع ملفاتك الخاصة، عدّل عنوان الوجهة، وجرب تكوينات Pivot مختلفة. كلما لعبت أكثر، كلما زادت ثقتك في أتمتة مهام Excel باستخدام C#.

![مخطط يوضح نسخ النطاق المصدر A1:G20 إلى A25 في نفس ورقة العمل – كيفية نسخ النطاق مع جداول Pivot](/images/how-to-copy-range-diagram.png "كيفية نسخ النطاق مع جداول Pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}