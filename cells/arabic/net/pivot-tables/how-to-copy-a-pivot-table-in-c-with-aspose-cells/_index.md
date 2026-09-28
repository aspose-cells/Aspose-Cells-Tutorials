---
category: general
date: 2026-09-27
description: تعلم كيفية نسخ جدول محوري في C# باستخدام Aspose.Cells. يتضمن نسخ الصفوف
  مع التنسيق، نسخ الجدول المحوري إلى ورقة أخرى، وتصدير الجدول المحوري إلى مصنف جديد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: ar
lastmod: 2026-09-27
og_description: كيفية نسخ جدول محوري في C# باستخدام Aspose.Cells. اتبع الدليل خطوة
  بخطوة لنسخ الصفوف مع التنسيق، نقل الجدول المحوري إلى ورقة أخرى، وتصديره إلى مصنف
  جديد.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: كيفية نسخ جدول محوري في C# – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: كيفية نسخ جدول محوري في C# باستخدام Aspose.Cells
url: /ar/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في C# باستخدام Aspose.Cells

إذا كنت بحاجة إلى **نسخ جدول محوري** من ورقة عمل إلى أخرى، فإن تعلم **كيفية نسخ جدول محوري** في C# باستخدام Aspose.Cells يمكن أن يوفر لك ساعات من العمل اليدوي. تتيح لك الطريقة أيضًا **نسخ الصفوف مع التنسيق**، والحفاظ على ذاكرة التخزين المؤقت للجدول المحوري، وحتى **تصدير الجدول المحوري إلى مصنف جديد** عندما تحتاج إلى ملف مستقل.

هذا الدليل يشرح لك سير العمل الكامل:

* إنشاء مصنف،  
* نسخ نطاق الجدول المحوري مع الحفاظ على التنسيق،  
* وضع البيانات المنسوخة في ورقة جديدة، و  
* حفظ النتيجة كملف منفصل.

سترى لماذا تُعد طريقة `CopyRows` المدمجة هي الأكثر موثوقية لـ **نسخ جدول محوري إلى ورقة أخرى**، وستحصل على نصائح للتعامل مع الحالات الخاصة مثل الصفوف المخفية أو مصادر البيانات الخارجية.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

| المتطلبات | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث | يدعم Aspose.Cells .NET 6+ ويعطي أفضل أداء. |
| Visual Studio 2022 (أو أي بيئة تطوير C#) | تحتاج إلى محرر يمكنه استعادة حزم NuGet. |
| Aspose.Cells for .NET (حزمة NuGet `Aspose.Cells`) | هذه المكتبة توفر API `CopyRows` المستخدمة في المثال. |
| ملف Excel مصدر (`source.xlsx`) يحتوي على جدول محوري في النطاق `A1:G20` | يقوم الكود بنسخ هذا النطاق المحدد؛ عدل النطاق إذا كان جدولك المحوري أكبر. |

قم بتثبيت المكتبة عبر NuGet CLI أو Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## الخطوة 1: تحميل المصنف الذي يحتوي على الجدول المحوري

السطر الأول ينشئ كائن `Workbook` يمثل ملف Excel بالكامل. تحميل الملف مرة واحدة يمنحك صلاحية القراءة/الكتابة على كل ورقة عمل.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **لماذا هذه الخطوة مهمة** – بدون تحميل المصنف، لا يمكن لأي من استدعاءات `CopyRows` اللاحقة الإشارة إلى البيانات المصدر أو ذاكرة التخزين المؤقت للجدول المحوري.

## الخطوة 2: إعداد أوراق العمل المصدر والوجهة

تحتاج إلى ورقة وجهة حيث سيُحفظ الجدول المحوري المنسوخ. الكود أدناه يجلب الورقة الأولى (حيث يقع الجدول المحوري الأصلي) ويضيف ورقة جديدة باسم **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **نصيحة احترافية:** إذا كانت ورقة الوجهة موجودة مسبقًا، استدعِ `Worksheets.RemoveAt(index)` أولاً لتجنب تكرار الأسماء.

## الخطوة 3: تعريف مساحة الخلايا التي تحيط بالجدول المحوري

كائن `CellArea` يصف الخلية العلوية اليسرى والسفلية اليمنى للنطاق الذي تريد نقله. في هذا المثال يشغل الجدول المحوري النطاق `A1:G20`. عدل الإحداثيات للجداول الأكبر.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## الخطوة 4: نسخ الصفوف مع التنسيق والحفاظ على ذاكرة التخزين المؤقت للجدول المحوري

طريقة `CopyRows` تنسخ **الصفوف** من ورقة المصدر إلى ورقة الوجهة. بتمرير `CopyOptions.CopyAll` تضمن نقل القيم، التنسيق، المخططات، والكائنات المدمجة—وكل ما هو جزء من الجدول المحوري.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### لماذا `CopyRows` يعمل أفضل من `Copy` للجداول المحورية

* `CopyRows` يحترم ذاكرة التخزين المؤقت الداخلية للجدول المحوري، لذا يظل الجدول المنسوخ فعالًا.
* يحافظ على **نسخ الصفوف مع التنسيق** تمامًا كما تظهر في الورقة الأصلية.
* على عكس `Copy` البسيط لنطاق، فإنه ينقل أيضًا الصفوف المخفية وأي مقاطع (slicers) مرتبطة.

## الخطوة 5: حفظ المصنف مع الجدول المحوري المنسوخ

أخيرًا، اكتب المصنف المعدل إلى القرص. الملف الجديد يحتوي على الورقة الأصلية بالإضافة إلى ورقة **Copy** التي تحمل نسخة كاملة الوظيفة من الجدول المحوري الأصلي.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### النتيجة المتوقعة

عند فتح `pivot_copied.xlsx`:

* الورقة **Sheet1** لا تزال تحتوي على البيانات والجدول المحوري الأصلي.
* الورقة **Copy** تعرض جدولًا محوريًا مطابقًا مع نفس التخطيط، الفلاتر، والتنسيق.
* جميع الصيغ واتصالات البيانات تبقى سليمة لأن ذاكرة التخزين المؤقت للجدول المحوري تم نسخها مع الصفوف.

## كيفية نسخ جدول محوري إلى ورقة أخرى في نفس المصنف

إذا كنت تحتاج فقط إلى الجدول المحوري في ورقة موجودة مسبقًا (مثلاً “Report”)، استبدل خطوة إنشاء الوجهة بإشارة إلى الورقة المستهدفة:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

هذا المقتطف يوضح **نسخ جدول محوري إلى ورقة أخرى** دون إنشاء ورقة عمل جديدة.

## تصدير الجدول المحوري إلى مصنف جديد

أحيانًا تريد الجدول المحوري في ملف منفصل تمامًا. بعد عملية النسخ، يمكنك حذف جميع الأوراق ما عدا تلك التي تحمل الجدول المحوري المنسوخ ثم حفظ الملف:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

الآن يحتوي `pivot_only.xlsx` على ورقة واحدة فقط بها الجدول المحوري المكرر، مما يلبي متطلبات **تصدير جدول محوري إلى مصنف جديد**.

## كيفية نسخ صفوف Excel دون فقدان التنسيق

نفس استدعاء `CopyRows` يعمل لأي نطاق، ليس فقط للجداول المحورية. إذا كنت تحتاج إلى **نسخ صفوف Excel** التي تشمل تنسيقًا شرطيًا، تحقق من صحة البيانات، أو خلايا مدمجة، استخدم نفس الطريقة:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

نظرًا لأن `CopyOptions.CopyAll` ينقل كل شيء، فإن الصفوف في الوجهة تبدو تمامًا كالصفوف في المصدر.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | العَرَض | الحل |
|---------|---------|-----|
| النطاق المصدر لا يشمل كامل الجدول المحوري | يظهر الجدول المحوري المنسوخ مقطوعًا. | تأكد من أن `CellArea` يغطي جميع الصفوف/الأعمدة للجدول المحوري. |
| ورقة الوجهة تحتوي بالفعل على بيانات | الصفوف المكتوبة فوقها تتسبب في فقدان البيانات. | اختر ورقة جديدة أو ابدأ النسخ من صف أعلى. |
| الجدول المحوري يستخدم مصدر بيانات خارجي | يفقد النسخ ارتباطه. | بعد النسخ، استدعِ `pivotTable.RefreshData()` لإعادة إنشاء الرابط. |
| الصفوف المخفية تُهمل | بعض الصفوف تختفي في النسخة. | `CopyRows` ينسخ الصفوف المخفية تلقائيًا؛ تأكد من عدم استخدام `CopyOptions.CopyValuesOnly`. |

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مستقل يمكنك لصقه في مشروع وحدة تحكم جديد. يوضح كل خطوة تم مناقشتها أعلاه.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**تشغيل البرنامج** ينشئ `pivot_copied.xlsx` مع نسخة مكررة من الجدول المحوري الأصلي على ورقة جديدة باسم **Copy**.

## الخلاصة

أنت الآن تعرف **كيفية نسخ جدول محوري** في C# باستخدام 

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}