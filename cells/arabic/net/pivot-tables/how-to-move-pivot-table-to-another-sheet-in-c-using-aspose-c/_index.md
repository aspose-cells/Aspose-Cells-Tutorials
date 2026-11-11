---
category: general
date: 2026-10-26
description: نقل جدول محوري إلى ورقة أخرى في C# مع دليل خطوة بخطوة يوضح أيضًا كيفية
  تحميل مصنف Excel في C# بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- move pivot table to another sheet
- load excel workbook c#
- copy rows with pivot table
- Aspose.Cells pivot table
- C# Excel automation
language: ar
lastmod: 2026-10-26
og_description: نقل جدول محوري إلى ورقة أخرى في C# باستخدام Aspose.Cells. اتبع هذا
  الدرس المختصر لتحميل مصنف Excel في C# ونسخ الجداول المحورية بأمان.
og_image_alt: Screenshot of a pivot table moved to another sheet using C#
og_title: نقل جدول محوري إلى ورقة أخرى في C# – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: move pivot table to another sheet in C# with a step‑by‑step guide that
    also shows how to load Excel workbook C# efficiently
  headline: How to move pivot table to another sheet in C# using Aspose.Cells
  type: TechArticle
- description: move pivot table to another sheet in C# with a step‑by‑step guide that
    also shows how to load Excel workbook C# efficiently
  name: How to move pivot table to another sheet in C# using Aspose.Cells
  steps:
  - name: Expected result
    text: '* The file **CopyPivot.xlsx** contains a new worksheet **PivotCopy**. *
      The pivot table appears exactly as it did on the original sheet, preserving
      filters, row/column fields, and data source connections. * All original data
      remains in the source worksheet, so you have effectively **moved pivot tabl'
  - name: Multiple pivot tables on the same sheet
    text: 'If the source sheet hosts several pivots, repeat steps 3–5 for each `PivotTable`
      object:'
  - name: Copying to an existing sheet with data
    text: 'When the destination sheet already contains data, calculate the next free
      row:'
  - name: Preserving formatting
    text: '`CopyRows` copies cell values, formulas, and formatting by default. If
      you need to exclude formatting, use the overload that accepts a `CopyOptions`
      object and set `CopyOptions.CopyStyle = false`.'
  - name: What to explore next
    text: '* **Load Excel workbook C#** and modify formulas programmatically – see
      the Aspose.Cells documentation on `Formula` objects. * **Export pivot tables
      to PDF** using `Workbook.Save` with `SaveFormat.Pdf`. * **Create pivot tables
      from scratch** with the `PivotTable` API for dynamic report generation.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: كيفية نقل جدول محوري إلى ورقة أخرى في C# باستخدام Aspose.Cells
url: /ar/net/pivot-tables/how-to-move-pivot-table-to-another-sheet-in-c-using-aspose-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نقل جدول محوري إلى ورقة أخرى في C# باستخدام Aspose.Cells

إذا كنت بحاجة إلى **نقل جدول محوري إلى ورقة أخرى** في ملف .xlsx، يوضح لك هذا الدليل الخطوات الدقيقة. ستتعلم أيضًا كيفية **تحميل دفتر عمل Excel C#** باستخدام Aspose.Cells، نسخ الجدول المحوري المرتبط، وحفظ النتيجة دون فقدان أي اتصالات بيانات.

يغطي الدليل كل ما يلزم لتنفيذ جاهز للإنتاج: حزم NuGet المطلوبة، الكود المصدر الكامل، شروحات لماذا كل استدعاء API مهم، ونصائح للتعامل مع الحالات الشائعة مثل وجود جداول محورية متعددة أو أوراق وجهة موجودة بالفعل.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET)  
* حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Aspose.Cells`) – المكتبة التي توفر الفئات `Workbook` و `Worksheet` و `CellArea` المستخدمة في المثال  

ليس عليك تثبيت Microsoft Office؛ Aspose.Cells يعمل مباشرةً مع تنسيق الملف.

## الخطوة 1: تحميل دفتر عمل Excel في C#

العملية الأولى هي قراءة ملف المصدر من القرص. تحميل دفتر العمل ينشئ تمثيلًا في الذاكرة لكل ورقة عمل، خلية، ومخزن محوري.

```csharp
using Aspose.Cells;

namespace PivotTableMover
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            var sourcePath = @"C:\Data\Source.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            // Continue with pivot table handling...
        }
    }
}
```

*لماذا هذه الخطوة مهمة* – `Workbook` يحلل حزمة XLSX، يملأ مجموعة `Worksheets`، ويجهز كائنات مخزن المحور حتى يمكن الإشارة إليها لاحقًا. بدون تحميل دفتر العمل، لا يمكن إجراء أي تعديل آخر.

## الخطوة 2: تحديد ورقة العمل التي تحتوي على الجدول المحوري

عادةً ما تكون أول ورقة عمل هي التي تحتوي على الجدول المحوري، لكن يمكنك البحث بالاسم أو بفحص مجموعة `PivotTables`. للتوضيح، يستخدم هذا المثال الورقة الأولى.

```csharp
// Get the first worksheet that contains the pivot table
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

إذا كان دفتر العمل يحتوي على عدة أوراق بها جداول محورية، قم بالتكرار عبر `sourceWorkbook.Worksheets` وتفقد `sheet.PivotTables.Count` لاختيار الورقة الصحيحة.

## الخطوة 3: تعريف نطاق الخلايا الذي يحيط بالجدول المحوري

يتطلب Aspose.Cells بنية `CellArea` لتحديد المربع المستطيل الذي تريد نسخه. يجب أن يشمل النطاق كامل الجدول المحوري، بما في ذلك صفوف العناوين وأي أعمدة محسوبة.

```csharp
// Define the area covering the pivot table (adjust rows/columns as needed)
CellArea pivotRange = new CellArea
{
    StartRow = 0,          // zero‑based index, first row of the pivot
    StartColumn = 0,       // first column of the pivot
    EndRow = 30,           // last row of the pivot (inclusive)
    EndColumn = 10         // last column of the pivot (inclusive)
};
```

*لماذا هذه الخطوة مهمة* – طريقة `CopyRows` تعمل على نطاق صفوف، ولكن بتمرير `CellArea` تضمن أن جميع الخلايا التابعة للجدول المحوري مشمولة. إذا كان النطاق صغيرًا جدًا، سيفقد الجدول المحوري بيانات المصدر؛ إذا كان كبيرًا جدًا، سيتم نسخ خلايا غير ضرورية.

## الخطوة 4: إنشاء (أو اختيار) ورقة العمل الوجهة

يمكنك نقل الجدول المحوري إلى ورقة موجودة أو إنشاء ورقة جديدة. المثال ينشئ ورقة جديدة باسم **"PivotCopy"** ويضع الصفوف المنسوخة بدءًا من الصف 0.

```csharp
// Create a new worksheet for the copied pivot table
Worksheet destSheet = sourceWorkbook.Worksheets[sourceWorkbook.Worksheets.Add()];
destSheet.Name = "PivotCopy";
```

إذا كنت تفضل نقل الجدول المحوري إلى ورقة موجودة، استبدل كود الإنشاء بإشارة إلى تلك الورقة:

```csharp
// Worksheet destSheet = sourceWorkbook.Worksheets["ExistingSheetName"];
```

## الخطوة 5: نسخ الصفوف — بما في ذلك الجدول المحوري المرتبط — إلى ورقة الوجهة

طريقة `CopyRows` تقبل علامة (`true`) تخبر Aspose.Cells بنسخ أي جداول محورية مرتبطة بالصفوف. هذه العلامة أساسية؛ بدونها سيفقد تعريف الجدول المحوري.

```csharp
// Copy rows from sourceSheet to destSheet, preserving pivot tables
sourceSheet.CopyRows(
    sourceRowIndex: 0,          // start row in source sheet
    totalRows: 40,              // number of rows to copy (covers the pivot range)
    sourceArea: pivotRange,     // the cell area that defines the pivot
    copyAssociatedPivotTables: true, // preserve pivot tables
    destinationSheet: destSheet,
    destinationRowIndex: 0);    // start row in the destination sheet
```

*لماذا هذه الخطوة مهمة* – معامل `copyAssociatedPivotTables` يضمن أن مخزن المحور وإعدادات الحقول تنتقل مع الصفوف المنسوخة. ورقة الوجهة تستقبل جدولًا محوريًا كامل الوظائف يشير إلى نفس مصدر البيانات كما الأصل.

## الخطوة 6: حفظ دفتر العمل المعدل

بعد عملية النسخ، احفظ دفتر العمل إلى ملف جديد. الحفاظ على الملف الأصلي دون تعديل يجعل العملية آمنة للأنابيب الآلية.

```csharp
// Save the workbook with the moved pivot table
var outputPath = @"C:\Data\CopyPivot.xlsx";
sourceWorkbook.Save(outputPath);
```

عند فتح **CopyPivot.xlsx**، سترى ورقة "PivotCopy" التي تحتوي على نسخة مطابقة تمامًا من الجدول المحوري الأصلي، جاهزة للمزيد من التحليل أو التوزيع.

## مثال عملي كامل

دمج جميع الخطوات معًا ينتج تطبيقًا مكتبيًا مستقلًا:

```csharp
using Aspose.Cells;

namespace PivotTableMover
{
    class Program
    {
        static void Main()
        {
            // 1. Load the source workbook
            var sourcePath = @"C:\Data\Source.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);

            // 2. Locate the worksheet with the pivot table
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

            // 3. Define the range that includes the pivot table
            CellArea pivotRange = new CellArea
            {
                StartRow = 0,
                StartColumn = 0,
                EndRow = 30,
                EndColumn = 10
            };

            // 4. Create a destination worksheet
            Worksheet destSheet = sourceWorkbook.Worksheets[sourceWorkbook.Worksheets.Add()];
            destSheet.Name = "PivotCopy";

            // 5. Copy rows and associated pivot tables
            sourceSheet.CopyRows(
                sourceRowIndex: 0,
                totalRows: 40,
                sourceArea: pivotRange,
                copyAssociatedPivotTables: true,
                destinationSheet: destSheet,
                destinationRowIndex: 0);

            // 6. Save the result
            var outputPath = @"C:\Data\CopyPivot.xlsx";
            sourceWorkbook.Save(outputPath);
        }
    }
}
```

### النتيجة المتوقعة

* الملف **CopyPivot.xlsx** يحتوي على ورقة عمل جديدة **PivotCopy**.  
* يظهر الجدول المحوري تمامًا كما كان في الورقة الأصلية، مع الحفاظ على الفلاتر، حقول الصف/العمود، واتصالات مصدر البيانات.  
* جميع البيانات الأصلية تبقى في ورقة المصدر، لذا فقد قمت فعليًا **نقل جدول محوري إلى ورقة أخرى** دون فقدان أي وظيفة.

## التعامل مع التغييرات الشائعة

### جداول محورية متعددة في نفس الورقة

إذا كانت ورقة المصدر تستضيف عدة جداول محورية، كرر الخطوات 3–5 لكل كائن `PivotTable`:

```csharp
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Determine the exact area of each pivot table
    CellArea ptArea = pt.TableRange;
    // Copy each pivot individually
    sourceSheet.CopyRows(0, ptArea.EndRow - ptArea.StartRow + 1,
        ptArea, true, destSheet, destSheet.Cells.MaxDataRow + 1);
}
```

### النسخ إلى ورقة موجودة تحتوي على بيانات

عندما تكون ورقة الوجهة تحتوي بالفعل على بيانات، احسب الصف الحر التالي:

```csharp
int destStartRow = destSheet.Cells.MaxDataRow + 1;
sourceSheet.CopyRows(0, 40, pivotRange, true, destSheet, destStartRow);
```

### الحفاظ على التنسيق

`CopyRows` ينسخ قيم الخلايا، الصيغ، والتنسيق بشكل افتراضي. إذا كنت بحاجة لاستبعاد التنسيق، استخدم النسخة التي تقبل كائن `CopyOptions` واضبط `CopyOptions.CopyStyle = false`.

## نصائح احترافية

* **تحقق من نطاق الجدول المحوري** – قبل النسخ، تأكد من أن `pivotRange.EndRow` و `EndColumn` يطابقان `pt.TableRange`. النطاقات غير المتطابقة قد تقص الجدول المحوري أو تكرر صفوفًا إضافية.  
* **تحديث مخزن المحور** بعد نقل الجدول إذا تغيرت بيانات المصدر. استدعِ `pt.RefreshData()` على الجدول المحوري في الوجهة لضمان أن الحسابات محدثة.  
* **تجنب المسارات الصريحة** في الكود الإنتاجي. استخدم `Path.Combine` وملفات الإعداد لجعل الحل قابلًا للنقل عبر البيئات.

## الخلاصة

أصبح لديك الآن طريقة كاملة وجاهزة للإنتاج **لنقل جدول محوري إلى ورقة أخرى** في C#. عرض الدليل كيفية **تحميل دفتر عمل Excel C#**، تعريف النطاق الدقيق للجدول المحوري، نسخ الصفوف مع الحفاظ على تعريف الجدول، وحفظ الملف المحدث. باستخدام هذه اللبنات يمكنك أتمتة مهام تقارير Excel المعقدة، دمج معالجة الجداول المحورية في خدمات الويب، أو بناء خطوط أنابيب تحليل بيانات مخصصة.

### ما الذي يمكنك استكشافه لاحقًا

* **تحميل دفتر عمل Excel C#** وتعديل الصيغ برمجيًا – راجع وثائق Aspose.Cells حول كائنات `Formula`.  
* **تصدير الجداول المحورية إلى PDF** باستخدام `Workbook.Save` مع `SaveFormat.Pdf`.  
* **إنشاء جداول محورية من الصفر** باستخدام API `PivotTable` لتوليد تقارير ديناميكية.  

لا تتردد في تجربة ملفات مصدر مختلفة، جداول محورية متعددة، أو تخطيطات وجهة مخصصة. النمط نفسه ينطبق بغض النظر عن حجم دفتر العمل أو تعقيده. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [نسخ جدول محوري إلى ورقة أخرى – دليل C# كامل](/cells/english/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/)
- [كيفية نسخ جدول محوري في Excel باستخدام C# و Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [إنشاء جدول محوري في Excel باستخدام Aspose.Cells لـ .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}