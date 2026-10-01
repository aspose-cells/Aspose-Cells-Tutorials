---
category: general
date: 2026-10-01
description: تعلم كيفية حذف الصفوف من جدول Excel وتغيير اسم جدول Excel باستخدام C#.
  دليل خطوة بخطوة مع الكود الكامل وأفضل الممارسات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: ar
lastmod: 2026-10-01
og_description: احذف الصفوف من جدول Excel وغير اسم جدول Excel في C#. اتبع هذا الدليل
  الكامل لتحميل المصنف، تعديل الجدول، وحفظ النتيجة.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: حذف الصفوف من جدول إكسل وتغيير اسمه في C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية حذف الصفوف من جدول Excel وتغيير اسمه في C#
url: /ar/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حذف الصفوف من جدول Excel وتغيير اسمه في C#

إذا كنت بحاجة إلى **حذف الصفوف من جدول Excel** أثناء العمل باستخدام C#، فإن هذا الدليل يوضح الخطوات الدقيقة المطلوبة. ستتعرف على كيفية **تحميل مصنف Excel في C#**، وإزالة صفوف محددة من جدول، ثم **تحديث اسم جدول Excel** بحيث يبقى الملف متسقًا.

يغطي الدليل كل ما تحتاج معرفته: حزم NuGet المطلوبة، كود كامل قابل للتنفيذ، ومشكلات شائعة مثل انتهاكات بنية الجدول. بنهاية المقال يمكنك تعديل أي جدول Excel برمجيًا دون تدخل يدوي.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث مثبت.
* Visual Studio 2022 (أو أي بيئة تطوير C#) مُكوَّنة لتطوير .NET.
* مكتبة **Aspose.Cells for .NET** مضافة عبر NuGet (`Install-Package Aspose.Cells`).
* مصنف Excel موجود (`Table.xlsx`) يحتوي على ورقة عمل واحدة على الأقل بها جدول.

توفر هذه العناصر البيئة اللازمة لـ **load Excel workbook c#** code وتنفيذ العمليات بثقة.

## الخطوة 1: تحميل المصنف الذي يحتوي على الجدول

العملية الأولى هي فتح ملف المصنف. تقوم Aspose.Cells بقراءة المصنف بالكامل إلى الذاكرة، مما يمنحك تحكمًا كاملاً في أوراق العمل والجداول وبيانات الخلايا.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*لماذا هذا مهم*: تحميل المصنف هو الأساس لأي تعديل لاحق على الجدول. كائن `Workbook` يُظهر مجموعة `Worksheets`، والتي ستستخدمها لتحديد موقع الجدول المستهدف.

## الخطوة 2: الوصول إلى أول ورقة عمل وأول جدول لها

تخزن معظم ملفات Excel الجداول في أول ورقة عمل، لكن يمكنك تعديل الفهرس إذا لزم الأمر. الكود التالي يسترجع أول كائن `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

إذا لم تحتوي ورقة العمل على جدول، فإن `sheet.Tables.Count` سيكون صفرًا ويجب معالجة هذه الحالة. محاولة الوصول إلى `sheet.Tables[0]` عندما لا توجد جداول ستؤدي إلى استثناء، لذا يُنصح باستخدام شرط حماية في كود الإنتاج.

## الخطوة 3: حذف الصفوف من جدول Excel

لـ **إزالة الصفوف من جدول Excel**، استدعِ `DeleteRows(startRow, totalRows)`. المعامل `startRow` يبدأ من الصفر بالنسبة لأول صف بيانات في الجدول (الصف بعد العنوان).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### لماذا نستخدم `DeleteRows` بدلاً من حذف صفوف ورقة العمل؟

`DeleteRows` يقوم بتحديث النطاق الداخلي للجدول، مع الحفاظ على الصيغ والأنماط والأسماء المعرفة التي تخص الجدول. حذف صفوف ورقة العمل مباشرة قد يكسر بنية الجدول ويسبب استثناء.

**حالة حافة**: إذا كان الحذف سيترك الجدول بدون صفوف بيانات، فإن Aspose.Cells يطرح استثناء `ArgumentException`. احمِ نفسك من ذلك بفحص `table.RowCount` قبل الحذف.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## الخطوة 4: تغيير اسم جدول Excel

بعد إزالة الصفوف، قد ترغب في إعطاء الجدول معرفًا أكثر وصفًا. الخاصية `Name` تحدد الاسم المعرف للجدول، والذي يُستخدم في الصيغ وVBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*لماذا إعادة التسمية؟* اسم جدول واضح يحسن قابلية القراءة في الصيغ (`=SUM(SalesData2026[Amount])`) ويتجنب تصادم الأسماء عندما تكون هناك جداول متعددة تشترك في أغراض مشابهة.

## الخطوة 5: حفظ المصنف المعدل (اختياري)

احفظ التغييرات عن طريق حفظها في ملف جديد أو استبدال الملف الأصلي. الحفظ في موقع جديد يكون أكثر أمانًا أثناء التطوير.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

طريقة `Save` تكتب المصنف المحدث، بما في ذلك نطاق الجدول المتغير والاسم الجديد للجدول، إلى القرص.

## مثال كامل يعمل

جمع جميع الخطوات معًا ينتج برنامجًا مستقلًا يمكنك تشغيله فورًا.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**الناتج المتوقع** (بافتراض وجود الملف والجدول):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

تشغيل البرنامج يحدّث ملف Excel تمامًا كما هو موضح: تُحذف الصفوف، يتغير اسم الجدول، ويتم حفظ النتيجة دون تعديل يدوي.

## أسئلة شائعة وحلول المشكلات

| السؤال | الإجابة |
|----------|--------|
| *ماذا يحدث إذا كان الجدول يمتد عبر خلايا مدمجة؟* | `DeleteRows` يحترم النطاقات المدمجة. إذا كانت خلية مدمجة تعبر حدود الحذف، فإن Aspose.Cells يضبط الدمج تلقائيًا. تحقق من النتيجة بصريًا إذا كنت تعتمد على دمجات معقدة. |
| *هل يمكنني حذف صفوف من جدول هو جزء من مخزن Pivot؟* | حذف الصفوف من جدول المصدر الذي يغذي جدول Pivot **لا** يحدّث مخزن Pivot تلقائيًا. استدعِ `pivotTable.RefreshData()` بعد تعديل جدول المصدر. |
| *هل من الممكن حذف صفوف بناءً على شرط (مثلاً القيمة < 0)؟* | نعم. قم بالتكرار عبر `table.ListObjects` أو `table.Rows` لتحديد الصفوف المطابقة، ثم جمع مؤشراتهم واستدعِ `DeleteRows` لكل نطاق. |
| *هل يجب إتلاف كائن `Workbook`؟* | `Workbook` يطبق `IDisposable`. ضعّه داخل كتلة `using` لتحرير الموارد بشكل حتمي، خاصةً عند معالجة ملفات كبيرة. |
| *كيف يختلف هذا عن استخدام EPPlus؟* | EPPlus يدعم أيضًا تعديل الجداول لكنه يستخدم API مختلف (`ExcelTable`). مفاهيم تحميل المصنف، حذف الصفوف، وإعادة تسمية الجدول مماثلة. اختر المكتبة التي تتوافق مع متطلبات الترخيص الخاصة بك. |

## أفضل الممارسات عند تعديل جداول Excel في C#

* **تحقق من الفهارس** – فهارس صفوف الجدول تبدأ من الصفر؛ أخطاء الإزاحة بمقدار واحد قد تتسبب في حذف غير متوقع.
* **تحقق من تصادم الأسماء** – Excel لا يسمح بأسماء معرفة مكررة؛ تحقق دائمًا من التفرد قبل تعيين اسم جديد.
* **احفظ نسخة احتياطية من الملفات الأصلية** – السكريبتات الآلية قد تفسد البيانات؛ احتفظ بنسخة من المصنف الأصلي.
* **استخدم عبارات `using`** – يضمن تحرير مقبض الملف بسرعة:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **اختبر مع حالات الحافة** – يجب التحقق من الجداول التي تحتوي على صف بيانات واحد، الجداول التي تمتد عبر كامل ورقة العمل، والجداول المرتبطة بالمخططات بعد التغييرات.

## الخلاصة

أنت الآن تعرف كيفية **حذف الصفوف من جدول Excel** و**تغيير اسم جدول Excel** باستخدام C#. الحل الكامل يقوم بتحميل المصنف، الوصول إلى الجدول المستهدف، إزالة الصفوف المطلوبة، إعادة تسمية الجدول، وحفظ النتيجة. استخدم هذه التقنيات لأتمتة إنشاء التقارير، تنظيف البيانات، أو أي سير عمل يتطلب إدارة جداول Excel برمجيًا.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **تحديث قيم الخلايا في جدول Excel**، **إضافة صفوف جديدة برمجيًا**، و**تصدير بيانات الجدول إلى CSV**. إتقان هذه العمليات سيمنحك تحكمًا كاملاً في ملفات Excel من داخل تطبيقات C# الخاصة بك.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إعادة تسمية جدول في Excel باستخدام C# – دليل خطوة بخطوة](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [إنشاء جدول Excel في C# – دليل خطوة بخطوة](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [الحصول على أول جدول من مصنف Excel في C# – دليل كامل](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}