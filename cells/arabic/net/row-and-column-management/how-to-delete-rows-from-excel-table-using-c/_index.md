---
category: general
date: 2026-09-27
description: تعلم كيفية حذف الصفوف من جدول Excel في C# من خلال دليل خطوة بخطوة يوضح
  أيضًا كيفية تحميل ملف Excel في C# بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: ar
lastmod: 2026-09-27
og_description: حذف الصفوف من جدول Excel في C# مع مثال واضح. يغطي هذا الدرس أيضًا
  كيفية تحميل دفتر عمل Excel في C# ومعالجة الحالات الخاصة الشائعة.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: حذف الصفوف من جدول Excel في C# – دليل كامل للكود
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: كيفية حذف الصفوف من جدول Excel باستخدام C#
url: /ar/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف الصفوف من جدول Excel في C# – دليل برمجي كامل

إذا كنت بحاجة إلى **حذف الصفوف من جدول Excel** في ملف .xlsx، فإن هذا الدرس يوضح لك بالضبط كيفية القيام بذلك باستخدام C#. سترى مثالًا مختصرًا وقابلًا للتنفيذ يقوم بتحميل مصنف Excel، وإزالة صفوف محددة من الجدول الأول، وحفظ النتيجة. يعمل النهج مع مكتبة Aspose.Cells الشهيرة ويمكن تكييفه مع مكتبات Excel الأخرى في .NET.

إزالة الصفوف من جدول هو مهمة شائعة عند تنظيف البيانات المستوردة، أو تقليم أقسام التقارير، أو أتمتة تحديثات جداول البيانات. بنهاية هذا الدليل ستكون قادرًا على **تحميل مصنف Excel C#**، وتحديد موقع جدول (ListObject)، وحذف أي صفوف تريدها، وكتابة الملف المعدل مرة أخرى إلى القرص.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث مثبت (الكود يعمل أيضًا مع .NET Framework 4.7+).
* مرجع إلى حزمة **Aspose.Cells** على NuGet (أو أي مكتبة متوافقة تُظهر أنواع `Workbook` و `Worksheet` و `ListObject`).
* ملف إدخال اسمه `input.xlsx` موجود في مجلد يمكنك الإشارة إليه من مشروعك.
* إلمام أساسي بصياغة C# و Visual Studio (أو بيئة التطوير المفضلة لديك).

> **نصيحة احترافية:** إذا كنت تفضل بديلًا مفتوح المصدر، يمكن تطبيق نفس المنطق باستخدام **ClosedXML** – فقط استبدل الفئات الخاصة بـ Aspose بـ `XLWorkbook` و `IXLWorksheet` و `IXLTable`.

## الخطوة 1: تحميل مصنف Excel في C#

العملية الأولى هي قراءة ملف المصدر إلى الذاكرة. تحميل المصنف أمر سريع بالنسبة لأحجام جداول البيانات النموذجية ويمنحك وصولًا كاملاً إلى أوراق العمل، والجداول، وقيم الخلايا.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*لماذا هذا مهم:* `Workbook` يحلل بنية Open XML لملف .xlsx، مكشفًا عن مجموعة من كائنات `Worksheet`. إذا لم يتم العثور على الملف، فإن Aspose يرمي استثناء `FileNotFoundException`، لذا تأكد من صحة المسار.

## الخطوة 2: الوصول إلى ورقة العمل المستهدفة

معظم جداول البيانات تحتوي على عدة أوراق؛ تحتاج إلى اختيار الورقة التي تحتوي على الجدول الذي تريد تعديله. هنا نستخدم الورقة الأولى (`Worksheets[0]`)، وهي قيمة افتراضية آمنة للملفات البسيطة.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*لماذا هذا مهم:* `Worksheet` هو الحاوية للجداول (`ListObjects`). الوصول إلى الورقة الصحيحة يمنع التغييرات غير المقصودة على البيانات غير المرتبطة.

## الخطوة 3: حذف الصفوف من جدول Excel

جداول Excel تمثل بواسطة كائنات `ListObject`. الجدول الأول في الورقة هو `ListObjects[0]`. طريقة `DeleteRows(startIndex, rowCount)` تزيل الصفوف **نسبةً إلى منطقة بيانات الجدول**، وليس أرقام الصفوف المطلقة في ورقة العمل.  

في هذا المثال نحذف الصف الثاني والثالث من الجدول (الرأس هو الصف 0، لذا نبدأ من الفهرس 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### ماذا لو كان للجدول اسم أو موقع مختلف؟

* **جدول مسمى:** استخدم `ws.ListObjects["MyTableName"]` بدلاً من الفهرس.
* **جداول متعددة:** قم بالتكرار عبر `ws.ListObjects` واختر الجدول الذي يطابق شرطًا (مثل أسماء رؤوس الأعمدة).
* **عدد صفوف ديناميكي:** يمكنك حساب `rowCount` في وقت التشغيل عن طريق فحص `ws.ListObjects[0].DataRange.RowCount`.

### معالجة الحالات الطرفية

| الحالة | التغيير الموصى به في الكود |
|---|---|
| الجدول فارغ أو يحتوي على عدد صفوف أقل | تحقق من `ws.ListObjects[0].DataRange.RowCount` قبل الحذف. |
| عدد الصفوف المراد حذفها يتجاوز حجم الجدول | قلّ `rowCount` إلى `DataRange.RowCount - startIndex`. |
| الحاجة لحذف الصفوف بناءً على شرط (مثلاً قيمة في العمود C) | قم بالتكرار عبر `DataRange.Rows` وجمع الفهارس المطابقة، ثم احذف بترتيب عكسي للحفاظ على استقرار الفهارس. |

## الخطوة 4: حفظ المصنف المعدل

بعد الحذف، اكتب المصنف مرة أخرى إلى ملف جديد (أو استبدل الأصلي إذا كنت تفضل). الحفظ ينشئ ملف .xlsx جديد يعكس الجدول المحدث.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*لماذا هذا مهم:* `Save` يقوم بتسلسل التمثيل الموجود في الذاكرة إلى القرص. إذا كنت بحاجة إلى الحفاظ على الملف الأصلي، فاحرص دائمًا على الكتابة إلى مسار مختلف.

## مثال كامل وقابل للتنفيذ

جمع جميع الخطوات معًا يمنحك برنامجًا مستقلًا يمكنك نسخه، لصقه، وتشغيله.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**الناتج المتوقع** (وحدة التحكم):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

افتح `output.xlsx` – الجدول الأول الآن يفتقد الصفوف التي حذفتها، بينما يظل صف الرأس سليمًا.

## أسئلة شائعة وتنوعات

### كيف أحذف الصفوف من **جميع** الجداول في مصنف؟

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### هل يمكنني حذف الصفوف بناءً على **قيمة خلية**؟

نعم. افحص `DataRange` للعثور على الخلايا المطابقة، اجمع فهارسها الصفرية، ثم احذفها بترتيب تنازلي:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### ماذا لو احتجت إلى **الحفاظ على التنسيق**؟

`DeleteRows` يزيل الصف بالكامل من الجدول لكنه يحتفظ بنمط الجدول للصفوف المتبقية. إذا كنت بحاجة إلى الحفاظ على تنسيق معين لصف تقوم بحذفه، انسخ النمط إلى صف آخر قبل الحذف.

### هل يعمل هذا مع ملفات **.xls** (Excel 97‑2003)؟

نعم. Aspose.Cells يكتشف تنسيق الملف تلقائيًا، لذا يعمل نفس الكود مع `.xls`. فقط غيّر امتداد الملف في مُنشئ `Workbook`.

## نصائح الأداء

* **حذف دفعي:** حذف العديد من الصفوف صفًا بصف قد يكون أبطأ. استخدم استدعاء واحد `DeleteRows(start, count)` عندما يكون ذلك ممكنًا.
* **تجنب حجز خيط واجهة المستخدم:** إذا دمجت هذا في تطبيق سطح مكتب، شغّل معالجة المصنف على خيط خلفي للحفاظ على استجابة الواجهة.
* **تحرير الموارد بشكل صحيح:** رغم أن Aspose.Cells يستخدم الذاكرة المُدارة، غلف `Workbook` داخل كتلة `using` إذا كنت تتعامل مع ملفات كبيرة لتحرير الموارد بسرعة.

## الخلاصة

لديك الآن مثال كامل وجاهز للإنتاج ي **يحذف الصفوف من جدول Excel** باستخدام C#. يغطي الدليل كيفية **تحميل مصنف Excel C#**، وتحديد `ListObject` المطلوب، وإزالة الصفوف بأمان، وحفظ الملف المحدث. مع معالجة الحالات الطرفية ونصائح الأداء المضمنة، يمكنك تكييف هذا النمط مع سيناريوهات أكثر تعقيدًا مثل الحذف الشرطي، الجداول المتعددة، أو مكتبات Excel البديلة في .NET.

### الخطوات التالية

* استكشف **ClosedXML** أو **EPPlus** إذا كنت تفضل مجموعة أدوات مفتوحة المصدر بالكامل.
* اجمع بين حذف الصفوف و **التحقق من صحة البيانات** لتنظيف جداول البيانات قبل استيرادها إلى قاعدة بيانات.
* أتمتة العملية لمجلد من المصنفات باستخدام `Directory.GetFiles` وحلقة تكرار.

لا تتردد في تجربة نطاقات صفوف مختلفة، أسماء جداول، ومنطق شرطي. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحميل ملف Excel C# – كيفية حذف الصفوف وإزالة صفوف محددة](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [كيفية إدراج وحذف الصفوف في Excel باستخدام Aspose.Cells لـ .NET: دليل شامل](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [كيفية حذف الصفوف الفارغة في Excel باستخدام Aspose.Cells .NET لتنظيف البيانات](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}