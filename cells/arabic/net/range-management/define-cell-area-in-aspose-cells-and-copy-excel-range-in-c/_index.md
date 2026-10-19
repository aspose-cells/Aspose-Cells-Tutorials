---
category: general
date: 2026-08-04
description: حدد نطاق الخلية في Aspose.Cells وتعلم كيفية نسخ جداول المحور، ونسخ نطاق
  Excel باستخدام C#، ونسخ النطاق في نفس الورقة بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: ar
lastmod: 2026-08-04
og_description: حدد نطاق الخلايا في Aspose.Cells وانسخ نطاق Excel في C# مع الحفاظ
  على جداول Pivot. اتبع هذا الدليل خطوة بخطوة للحصول على نتائج موثوقة.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: تحديد نطاق الخلية في Aspose.Cells – نسخ نطاق Excel في C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: تحديد نطاق الخلية في Aspose.Cells ونسخ نطاق Excel في C#
url: /ar/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد مساحة الخلية في Aspose.Cells ونسخ نطاق Excel باستخدام C#

إذا كنت بحاجة إلى **تحديد مساحة الخلية** لنطاق ثم نسخ ذلك النطاق في نفس ورقة العمل، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells لـ .NET. سواء كنت تنقل تقريرًا يعتمد على Pivot أو تكرر كتلة بيانات، ستتعلم العملية الكاملة في بضع خطوات فقط.

ستكتشف أيضًا **كيفية نسخ Pivot** دون فقدان اتصالاته، وسترى مثالًا واضحًا على **copy excel range c#** الذي يعمل في سيناريو **copy range same sheet**. لا تحتاج إلى أدوات خارجية—فقط Aspose.Cells وبعض أسطر C#.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
- Aspose.Cells لـ .NET (حزمة NuGet `Aspose.Cells`)
- مصنف Excel (`input.xlsx`) يحتوي على جدول Pivot في النطاق A1:J50
- بيئة تطوير مثل Visual Studio 2022

## الخطوة 1: تحديد مساحة الخلية للنطاق المصدر

المهمة الأولى هي **تحديد مساحة الخلية** التي تمثل الكتلة التي تريد نسخها. يستخدم Aspose.Cells البنية `CellArea`، التي تخزن مؤشرات الصف والعمود بدءًا من الصفر.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**لماذا هذا مهم:** يحدد `CellArea` لـ Aspose.Cells بالضبط الخلايا التي يجب التعامل معها. استخدام مؤشرات بدءًا من الصفر يجنب الأخطاء الشائعة من نوع off‑by‑one عند تحويل ترميز Excel A1 إلى كود.

## الخطوة 2: تحديد مساحة الخلية الوجهة في نفس ورقة العمل

لـ **copy range same sheet**، يجب أيضًا تحديد مكان وصول البيانات. يمكن أن يبدأ الوجهة في أي صف؛ هنا نبدأ من الصف 61 (مؤشر صفر‑مبني 60) لترك مساحة فارغة.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**لماذا هذا مهم:** من خلال مطابقة أبعاد المصدر، تضمن أن الكتلة المنسوخة تتناسب تمامًا دون اقتطاع.

## الخطوة 3: نسخ النطاق مع الحفاظ على جداول Pivot

الآن يمكنك **كيفية نسخ Pivot** بأمان. تتضمن فئة `CopyOptions` علمًا `CopyPivotTables` الذي يحتفظ بتعريف الـ Pivot، مصدر البيانات، والتنسيق.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**لماذا هذا مهم:** بدون تعيين `CopyPivotTables = true`، سيصبح الـ Pivot لقطة ثابتة، مما يفقد التفاعلية. هذا الخيار ينسخ الذاكرة المؤقتة والاتصالات الأساسية، لذا يعمل الـ Pivot الجديد تمامًا مثل الأصلي.

## الخطوة 4: حفظ المصنف

أخيرًا، احفظ التغييرات إلى القرص. يُظهر ملف الإخراج أن جدول الـ Pivot تم تكراره في نفس الورقة.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**نصيحة احترافية:** استخدم `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` إذا كنت بحاجة إلى فرض تنسيق معين، خاصةً عند العمل مع إصدارات Excel القديمة.

## الخطوة 5: التحقق من جدول Pivot المنسوخ

افتح `CopyWithPivot.xlsx` في Excel وتحقق من التالي:

1. النطاق A61:J110 يحتوي على نسخة من البيانات الأصلية.
2. يظهر جدول Pivot جديد في أعلى النطاق المنسوخ.
3. تحديث الـ Pivot يعكس التغييرات في البيانات المصدر، مؤكدًا أن **how to copy pivot** نجح.

إذا لم يتم تحديث الـ Pivot، تأكد من أن نطاق البيانات المصدر في تعريف الـ Pivot لا يزال يشير إلى منطقة المصنف الأصلية. يقوم Aspose.Cells تلقائيًا بتحديث مرجع المصدر عندما تكون `CopyPivotTables` true.

## الحالات الخاصة والاختلافات

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **Copy to a different worksheet** | استبدل `srcWorkbook.Worksheets[0]` بفهرس أو اسم ورقة العمل الهدف، وقم بضبط `destinationRange` وفقًا لذلك. |
| **Copy a merged cell block** | عيّن `CopyOptions.PasteType = PasteType.All` للحفاظ على الخلايا المدمجة والتنسيق. |
| **Copy only values, not formulas** | استخدم `CopyOptions.PasteType = PasteType.Values` لتجنب نقل الصيغ التي تشير إلى الورقة الأصلية. |
| **Large ranges ( > 10,000 rows )** | فكر في استخدام `Workbook.Copy` لنسخ أوراق العمل بالكامل لتحسين الأداء، ثم احذف الصفوف غير المطلوبة. |

تظهر هذه الاختلافات أن منطق **aspose.cells copy range** نفسه يمكن تكييفه مع العديد من السيناريوهات الواقعية.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. استبدل `YOUR_DIRECTORY` بمسار مجلد فعلي على جهازك.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**الناتج المتوقع:** بعد تشغيل البرنامج، يحتوي `CopyWithPivot.xlsx` على البيانات الأصلية بالإضافة إلى كتلة مطابقة تبدأ من الصف 61، مع جدول Pivot فعال.

## الخلاصة

أنت الآن تعرف كيف **تحدد مساحة الخلية** في Aspose.Cells، **copy excel range c#**، و **copy range same sheet** مع الحفاظ على جميع وظائف الـ Pivot. تُزيل هذه التقنية أخطاء النسخ واللصق اليدوية وتعمل بكفاءة مع المصنفات الكبيرة.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **how to copy pivot** عبر عدة أوراق عمل، أو استخدم **aspose.cells copy range** لتكرار أوراق كاملة مع التنسيق. جرّب إعدادات `CopyOptions` المختلفة لتخصيص سلوك النسخ وفقًا لاحتياجات مشروعك.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم عرضها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}