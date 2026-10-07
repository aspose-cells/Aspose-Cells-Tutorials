---
category: general
date: 2026-10-07
description: تعلم كيفية تعيين اسم لجدول Excel مع معالجة مشكلات التسمية وكيفية تعريف
  نطاق مسمى عند إضافة الجدول إلى ورقة العمل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- assign name to excel table
- how to define named range
- add table to worksheet
language: ar
lastmod: 2026-10-07
og_description: قم بتعيين اسم لجدول Excel بأمان وتعلم كيفية تعريف نطاق مسمى عند إضافة
  الجدول إلى ورقة العمل في C#.
og_image_alt: Screenshot showing Excel table with a custom name assigned
og_title: تعيين اسم لجدول إكسل – دليل كامل لمطوري C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to assign name to Excel table while handling naming issues
    and how to define named range when you add table to worksheet.
  headline: Assign name to Excel table and avoid naming conflicts
  type: TechArticle
tags:
- Excel automation
- Aspose.Cells
- C#
title: تعيين اسم لجدول إكسل وتجنب تعارض الأسماء
url: /ar/net/excel-advanced-named-ranges/assign-name-to-excel-table-and-avoid-naming-conflicts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين اسم لجدول Excel وتجنب تعارض الأسماء

إذا كنت بحاجة إلى **تعيين اسم لجدول Excel** في مشروع C#، يوضح لك هذا الدليل الخطوات الدقيقة. ستتعرف أيضًا على **كيفية تعريف نطاق مسمى** بشكل صحيح وتفهم التأثير عند **إضافة جدول إلى ورقة العمل**.

العمل مع Excel برمجيًا يعني غالبًا التعامل مع النطاقات المسماة وكائنات الجداول. تسمية جدول بمعرف مكرر تُحدث استثناءً، مما قد يعرقل خطوط الأتمتة. يوجهك هذا البرنامج التعليمي إلى حل قوي يمنع الخطأ ويحافظ على تنظيم المصنف.

ستتعلم كيفية:

* إنشاء مصنف (workbook) وورقة عمل (worksheet).
* تعريف نطاق مسمى باستخدام الـ API الموصى به.
* إضافة جدول إلى ورقة العمل.
* تعيين اسم للجدول بأمان، مع معالجة الأسماء الموجودة بلطف.

لا حاجة إلى وثائق خارجية—كل ما تحتاجه موجود في مقتطفات الشيفرة والتفسيرات أدناه.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث.
* Aspose.Cells for .NET (نسخة تجريبية مجانية أو نسخة مرخصة).
* إلمام أساسي بصياغة C#.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

ابدأ بإنشاء تطبيق console وإضافة حزمة NuGet الخاصة بـ Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

namespace ExcelTableNamingDemo
{
    class Program
    {
        static void Main()
        {
            // All subsequent steps are performed inside this method.
        }
    }
}
```

*لماذا هذه الخطوة مهمة*: استيراد `Aspose.Cells` يمنحك الوصول إلى الفئات `Workbook`، `Worksheet`، `ListObject`، و `Name` التي تدير هياكل Excel.

## الخطوة 2: إنشاء مصنف جديد والحصول على أول ورقة عمل

```csharp
// Step 2: Create a new workbook and obtain the default worksheet.
Workbook workbook = new Workbook();               // Initializes an empty workbook.
Worksheet worksheet = workbook.Worksheets[0];    // Retrieves the first (default) sheet.
```

يبدأ المصنف بورقة واحدة تسمى “Sheet1”. بالإشارة إلى `Worksheets[0]` تضمن أنك دائمًا تعمل مع الورقة النشطة، وهو أمر أساسي عندما تقوم لاحقًا **بإضافة جدول إلى ورقة العمل**.

## الخطوة 3: تعريف نطاق مسمى – الطريقة الصحيحة

المقتطف الأصلي استخدم `workbook.Workbooks[0].Names`، وهو غير موجود في Aspose.Cells ويسبب ارتباكًا. المجموعة الصحيحة هي `workbook.Names`.

```csharp
// Step 3: Define a named range "MyRange" that refers to cells A1:A5 on Sheet1.
Name range = workbook.Names.Add("MyRange", "Sheet1!$A$1:$A$5");

// Populate the range with sample data for demonstration.
for (int i = 0; i < 5; i++)
{
    worksheet.Cells[i, 0].PutValue($"Item {i + 1}");
}
```

*لماذا هذه الخطوة مهمة*: `how to define named range` سؤال شائع عند أتمتة Excel. إضافة الاسم عبر `workbook.Names` يسجّله على مستوى المصنف، مما يجعله مرئيًا للمعادلات والكائنات الأخرى.

## الخطوة 4: إضافة جدول إلى ورقة العمل يغطي A1:B5

```csharp
// Step 4: Add a table that spans A1:B5. The last argument (true) indicates that the first row contains headers.
int firstRow = 0;   // Row index for A1
int firstCol = 0;   // Column index for A1
int totalRows = 4;  // 0‑based index for row 5 (A5)
int totalCols = 1;  // 0‑based index for column B (second column)

ListObject table = worksheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true);

// Give the header cells a label.
worksheet.Cells[0, 0].PutValue("Product");
worksheet.Cells[0, 1].PutValue("Quantity");

// Fill the second column with numbers.
for (int i = 1; i <= 5; i++)
{
    worksheet.Cells[i, 1].PutValue(i * 10);
}
```

الفئة `ListObject` تمثل جدول Excel. إضافة الجدول هي جوهر عملية **إضافة جدول إلى ورقة العمل**. العلامة `true` تخبر Aspose.Cells بمعاملة الصف الأول كصف رأس، وهو ما يتطابق مع الاستخدام المعتاد في Excel.

## الخطوة 5: تعيين اسم للجدول بأمان

محاولة إعادة استخدام اسم موجود يسبب استثناءً. لتجنب ذلك، تحقق مما إذا كان الاسم موجودًا بالفعل قبل تعيينه.

```csharp
// Step 5: Assign a unique name to the table, handling duplicates gracefully.
string desiredTableName = "MyRange";   // Intentional conflict with the named range.

bool nameExists = workbook.Names.Exists(desiredTableName) ||
                  worksheet.ListObjects.Exists(desiredTableName);

if (nameExists)
{
    // Resolve the conflict by appending a suffix.
    int suffix = 1;
    string newName;
    do
    {
        newName = $"{desiredTableName}_{suffix}";
        suffix++;
    } while (workbook.Names.Exists(newName) || worksheet.ListObjects.Exists(newName));

    table.Name = newName;
    Console.WriteLine($"Table name '{desiredTableName}' was taken; assigned '{newName}' instead.");
}
else
{
    table.Name = desiredTableName;
    Console.WriteLine($"Table successfully assigned name '{desiredTableName}'.");
}
```

*لماذا هذه الخطوة مهمة*: يوضح هذا الشيفرة **كيفية تعريف نطاق مسمى**‑aware عندما **تقوم بتعيين اسم لجدول Excel**. يمنع الاستثناء الذي كان سيتولد في المقتطف الأصلي.

## الخطوة 6: حفظ المصنف والتحقق من النتائج

```csharp
// Step 6: Save the workbook to disk.
string outputPath = "NamedTableDemo.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to '{outputPath}'.");
```

افتح الملف `NamedTableDemo.xlsx` الذي تم إنشاؤه في Excel:

* يظهر النطاق المسمى “MyRange” تحت الصيغ → مدير الأسماء ويشير إلى `Sheet1!$A$1:$A$5`.
* يظهر الجدول بالاسم الذي عينته (إما “MyRange” أو “MyRange_1” الذي تم توليده تلقائيًا).
* العمود B يحتوي على القيم الرقمية التي أدخلتها.

مخرجات وحدة التحكم تؤكد أي اسم تم استخدامه في النهاية.

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | الشرح | الحل |
|---------|-------|------|
| استخدام `workbook.Workbooks[0].Names` | هذه الخاصية غير موجودة؛ الشيفرة تُترجم لكن تُحدث استثناءً وقت التشغيل. | استخدم `workbook.Names` مباشرة. |
| تجاهل الأسماء الموجودة | محاولة تعيين `table.Name` إلى معرف مستخدم مسبقًا يرفع استثناءً. | تحقق من كل من `workbook.Names` و `worksheet.ListObjects` قبل التعيين. |
| عدم تخصيص الصف الأول للرؤوس | إضافة جدول بدون رؤوس قد يسبب تنسيقًا غير متوقع. | مرّر `true` إلى طريقة `Add` أو عيّن قيم الرؤوس يدويًا. |
| نسيان حفظ المصنف | التغييرات تبقى في الذاكرة وتفقد عند انتهاء البرنامج. | استدعِ `workbook.Save` مع مسار ملف صحيح. |

## توسيع الحل

إذا كنت بحاجة إلى **إضافة جدول إلى ورقة عمل** في عدة أوراق، غلف منطق التسمية في طريقة قابلة لإعادة الاستخدام:

```csharp
static void AddTableWithUniqueName(Worksheet ws, string baseName, int rows, int cols)
{
    ListObject tbl = ws.ListObjects.Add(0, 0, rows - 1, cols - 1, true);
    string uniqueName = baseName;
    int i = 1;
    while (ws.Workbook.Names.Exists(uniqueName) || ws.ListObjects.Exists(uniqueName))
    {
        uniqueName = $"{baseName}_{i}";
        i++;
    }
    tbl.Name = uniqueName;
}
```

يمكنك الآن استدعاء `AddTableWithUniqueName(worksheet, "SalesData", 10, 3);` لكل ورقة دون القلق من تصادم الأسماء.

## الخلاصة

أصبحت الآن تعرف كيف **تُعيّن اسمًا لجدول Excel** بأمان، وكيف تُعرّف **نطاقًا مسمى** بشكل صحيح، والخطوات اللازمة لـ **إضافة جدول إلى ورقة العمل** باستخدام Aspose.Cells for .NET. من خلال فحص الأسماء الموجودة قبل التعيين، تمنع الاستثناءات وتبقي مصنفك منظمًا.

جرّب مخططات تسمية مختلفة، أوراق عمل متعددة، أو نطاقات ديناميكية. الأنماط المعروضة هنا قابلة للتوسع إلى مشاريع أتمتة أكبر، مما يضمن أن كل جدول ونطاق يحمل معرفًا فريدًا ومعبّرًا.

--- 

*هل ترغب في أتمتة المزيد من مهام Excel؟ استكشف المواضيع ذات الصلة مثل “working with charts in Aspose.Cells”، “exporting workbook to PDF”، و “using formulas programmatically”.*


## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Convert Table to Range in Excel](/cells/english/net/tables-and-lists/converting-table-to-range/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}