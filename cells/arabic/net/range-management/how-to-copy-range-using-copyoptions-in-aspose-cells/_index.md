---
category: general
date: 2026-11-19
description: تعلم كيفية نسخ النطاق باستخدام CopyOptions في Aspose.Cells، مع الحفاظ
  على التنسيق وجداول المحور أثناء نسخ نطاق Excel مع التنسيق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: ar
lastmod: 2026-11-19
og_description: يسمح لك نسخ النطاق باستخدام CopyOptions في Aspose.Cells بتكرار بيانات
  Excel مع الحفاظ على التنسيق الكامل وجداول Pivot، مما يتيح معالجة موثوقة لدفتر العمل.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: نسخ النطاق باستخدام CopyOptions في Aspose.Cells – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية نسخ النطاق باستخدام CopyOptions في Aspose.Cells
url: /ar/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ النطاق باستخدام CopyOptions في Aspose.Cells

إذا كنت بحاجة إلى **copy range using CopyOptions** في Aspose.Cells، فإن هذا الدليل يوضح لك بالضبط كيفية تكرار مجموعة من الخلايا مع الحفاظ على جميع التنسيقات والجداول المحورية المدمجة دون تغيير. يواجه العديد من المطورين صعوبة في الحفاظ على النمط عند نقل البيانات بين أوراق العمل، وتقوم فئة `CopyOptions` بحل هذه المشكلة دون خطوات يدوية إضافية.

في هذا البرنامج التعليمي ستتعلم:

* تحديد مناطق المصدر والوجهة في مصنف Excel.  
* استخدام `CopyOptions` للاحتفاظ بتنسيق الخلايا وعرض الأعمدة والجداول المحورية.  
* حفظ النتيجة في ملف جديد جاهز للمعالجة اللاحقة.

يعمل المثال مع أي ملف `.xlsx` ويتطلب فقط مكتبة Aspose.Cells for .NET.

## المتطلبات المسبقة

قبل البدء، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت.  
* ترخيص صالح لـ Aspose.Cells for .NET (أو مفتاح تقييم مجاني).  
* Visual Studio 2022 أو أي بيئة تطوير C# تفضلها.  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Cells`.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيق console جديد وأضف مرجع Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

تُتيح لك توجيهة `using Aspose.Cells;` الوصول إلى `Workbook` و `CellArea` و `CopyOptions`.

## الخطوة 2: تحميل المصنف الذي تريد تعديله

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` يمثل ملف Excel بالكامل. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف المصدر الخاص بك.

## الخطوة 3: تعريف نطاقات المصدر والوجهة

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` يبني مساحة مستطيلة بناءً على عناوين الخلية العليا‑اليسرى والسفلى‑اليمنى. يمكنك تعديل الإحداثيات لتتناسب مع حجم الكتلة التي تحتاج إلى نسخها.

## الخطوة 4: نسخ النطاق مع الحفاظ على التنسيق والجداول المحورية

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

كائن `CopyOptions` يخبر Aspose.Cells بالضبط ما يجب الاحتفاظ به. تعيين `CopyPivotTables = true` هو المفتاح لـ **copy range using CopyOptions** عندما يتضمن المصدر جداول محورية. العلامات الأخرى تضمن أن **copy excel range with formatting** يتحقق تلقائيًا—لا يلزم أي كود إضافي لإعادة تطبيق الأنماط بعد النسخ.

### لماذا `CopyOptions` مهم

* **Performance** – المكتبة تنفذ عملية داخلية واحدة بدلاً من نسخ الخلايا واحدة‑بواحدة.  
* **Accuracy** – جميع الجوانب البصرية (الخطوط، الألوان، الحدود) تبقى بعد النقل، مما يلغي الانحراف البصري في التقارير المولدة.  
* **Reliability** – الجداول المحورية تظل فعّالة لأن الذاكرة المؤقتة ومراجع المصدر تُنسخ.

## الخطوة 5: حفظ المصنف المعدل

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

بعد استدعاء `Save`، يحتوي الملف `output.xlsx` على البيانات الأصلية بالإضافة إلى الكتلة المكررة في موقع الوجهة، مع كامل التنسيق والجداول المحورية.

## الكود الكامل للمرجع

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

تشغيل هذا البرنامج يطبع:

```
Range copied successfully. Output saved to output.xlsx
```

افتح `output.xlsx` في Excel – ستلاحظ أن الكتلة A1:H30 تم تكرارها في A35:H64، مع جميع ألوان الخلايا، الحدود، تنسيقات الأرقام، وأي جداول محورية لا تزال سليمة.

## الأسئلة الشائعة ومعالجة الحالات الخاصة

### ماذا لو كان نطاق الوجهة يتداخل مع المصدر؟

Aspose.Cells يطرح استثناء `ArgumentException`. لتجنب ذلك، احسب وجهة لا تتقاطع مع المصدر، أو انسخ إلى ورقة عمل مختلفة:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### كيف تنسخ بين مصنفات مختلفة؟

أنشئ نسخة ثانية من `Workbook` للملف الهدف واستخدم نفس كائن `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### هل يقوم `CopyOptions` أيضًا بنسخ الخلايا المدمجة؟

نعم. علم `CopyStyle` يتضمن معلومات الخلايا المدمجة. إذا كنت بحاجة إلى تحكم أدق، عيّن `options.CopyMergedCells = true` (متوفر في الإصدارات الأحدث).

### ماذا عن النطاقات الكبيرة (آلاف الصفوف)؟

العملية فعّالة من حيث الذاكرة، لكن قد ترغب في زيادة `WorkbookSettings` `MemorySetting` إلى `MemorySetting.MemoryPreference` للملفات الكبيرة جدًا.

## نصائح احترافية

* **Reuse the same `CopyOptions`** instance for multiple copy operations – it reduces object allocation overhead.  
* **Validate ranges** before copying: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` helps catch typo‑related errors early.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) while copying large data sets to speed up the process, then call `workbook.CalculateFormula()` after the copy if you need updated results.

## الخلاصة

أنت الآن تعرف كيف تقوم بـ **copy range using CopyOptions** في Aspose.Cells، محققًا **copy excel range with formatting** بالكامل مع الحفاظ على الجداول المحورية والميزات المتقدمة الأخرى. يزيل هذا النهج الحاجة إلى إعادة تطبيق الأنماط يدويًا ويضمن أن تكون أتمتة Excel الخاصة بك قوية وقابلة للصيانة.

الخطوات التالية التي قد تستكشفها:

* استخدم `CopyOptions` لتكرار أوراق العمل بالكامل.  
* اجمع عملية النسخ مع `WorksheetCollection.AddCopy` لإنشاء تقارير مبنية على القوالب.  
* دمج الكود في API ASP.NET Core لتوفير تحويلات Excel في الوقت الفعلي.

لا تتردد في تجربة إحداثيات مصدر/وجهة مختلفة، ومشاركة نتائجك في التعليقات!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}