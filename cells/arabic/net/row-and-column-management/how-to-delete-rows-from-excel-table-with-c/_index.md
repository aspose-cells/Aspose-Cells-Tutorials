---
category: general
date: 2026-11-25
description: تعلم كيفية حذف الصفوف من جدول Excel باستخدام C# وكذلك حذف عدة صفوف من
  ورقة Excel بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: ar
lastmod: 2026-11-25
og_description: احذف الصفوف من جدول Excel باستخدام C# وتعلم كيفية حذف عدة صفوف من
  ورقة Excel بكود نظيف.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: حذف الصفوف من جدول Excel في C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: كيفية حذف الصفوف من جدول Excel باستخدام C#
url: /ar/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حذف الصفوف من جدول Excel باستخدام C#

إذا كنت بحاجة إلى حذف صفوف من جدول Excel باستخدام C#، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعرف أيضًا على كيفية حذف عدة صفوف من ورقة Excel دون التأثير على البيانات الأخرى.

العمل مع Excel برمجيًا غالبًا ما يتطلب إزالة السجلات القديمة أو غير الصالحة. حذف الصفوف مباشرةً في ورقة العمل يمكن أن يكون محفوفًا بالمخاطر لأن صف الرأس لجدول منظم يجب أن يبقى سليمًا. يشرح هذا البرنامج التعليمي نهجًا آمنًا يحافظ على رأس الجدول ويسمح لك بحذف أي عدد من صفوف البيانات في استدعاء واحد.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6.0 أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير متكاملة متوافقة)  
* حزمة **Aspose.Cells** من NuGet (الإصدار 23.10 أو أحدث) – هذه المكتبة توفر الفئات `Workbook`، `Worksheet`، و `ListObject` المستخدمة في الأمثلة  

لا تحتاج إلى تثبيت Microsoft Office على جهاز التطوير لأن Aspose.Cells يعمل مباشرةً مع تنسيق الملف.

## حذف الصفوف من جدول Excel – خطوة بخطوة

الأقسام التالية تصف كل خطوة مطلوبة لحذف الصفوف من جدول Excel بأمان. الكلمة المفتاحية الأساسية تظهر في هذا العنوان لتلبية متطلبات تحسين محركات البحث.

### الخطوة 1: إضافة Aspose.Cells إلى مشروعك

افتح **Package Manager Console** وشغّل:

```powershell
Install-Package Aspose.Cells
```

تضيف الحزمة التجميعات اللازمة وتُعرّف الأنواع `Workbook`، `Worksheet`، و `ListObject`.

### الخطوة 2: تحميل المصنف وتحديد موقع الجدول

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*لماذا هذا مهم*: تمثل `ListObject` جدول Excel حقيقي، يحتفظ بصف الرأس الخاص به. من خلال العمل مع `ListObject`، تتجنب إزالة الرأس عن طريق الخطأ.

### الخطوة 3: حذف صفوف البيانات المطلوبة

طريقة `DeleteRows` تتوقع فهرس صف **صفر‑مبني** بالنسبة للجدول، **بما في ذلك** صف الرأس. لأن الرأس لا يمكن إزالته، يجب أن تبدأ من الفهرس 1 للصف الأول من البيانات.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

إذا حاولت `table.DeleteRows(0, 2)`، ستطلق Aspose.Cells استثناءً لأن صف الرأس (الفهرس 0) محمي. البدء من الفهرس 1 يضمن حذف صفوف البيانات فقط.

### الخطوة 4: حفظ المصنف المعدل

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

تشغيل البرنامج يزيل الصفين الموجودين مباشرةً أسفل الرأس مع الحفاظ على بنية الجدول سليمة.

### مثال كامل يعمل

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**الناتج المتوقع**: الملف `table_with_header_modified.xlsx` يحتوي على رأس الجدول الأصلي، يليه جميع الصفوف ما عدا الصفين الذين تم إزالتهما. لا يتم تعديل أي أوراق عمل أخرى.

## حذف عدة صفوف من ورقة Excel

أحيانًا تحتاج إلى حذف صفوف **ليست** جزءًا من جدول منظم. الكلمة المفتاحية الثانوية تظهر في هذا العنوان. يختلف النهج قليلًا لأنك تتعامل مع مجموعة `Rows` في الورقة بدلاً من `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**لماذا يعمل هذا**: `Rows.RemoveAt(startIndex, count)` يزيل كتلة متصلة من الصفوف مباشرةً من الورقة. لا توجد حماية للرأس، لذا يمكنك البدء من أي فهرس. الطريقة فعّالة لأنها تُحدّث هياكل البيانات الداخلية في عملية واحدة، وهو مثالي عندما تحتاج إلى حذف عدة صفوف من ورقة Excel.

### الحالات الخاصة وأفضل الممارسات

| الحالة                                 | المعالجة الموصى بها |
|----------------------------------------|----------------------|
| حذف صفوف تتجاوز آخر صف موجود           | تحقق من `worksheet.Rows.Count` قبل استدعاء `RemoveAt`. |
| إزالة جميع الصفوف ما عدا الرأس        | احذف صفوف البيانات داخل حلقة أو استخدم `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| الحفاظ على تنسيق الخلايا               | الحذف عبر `ListObject` ينقل التنسيق تلقائيًا؛ بالنسبة للأوراق العادية، انسخ التنسيق قبل الإزالة إذا لزم الأمر. |
| أوراق عمل كبيرة (> 10 000 صف)          | نفّذ عمليات الحذف بترتيب تنازلي لتجنب تغيير الفهارس، أو استخدم `DeleteRows` على الجدول إذا كان ذلك ممكنًا. |

**نصيحة احترافية**: عندما تحتاج إلى حذف صفوف بناءً على شرط (مثل الصفوف التي تكون قيمة عمودها فارغة)، قم بالتكرار عبر `DataRange` للجدول من الخلف إلى الأمام واستدعِ `DeleteRows` لكل صف يطابق الشرط. الحذف من الخلف يمنع اختلال الفهارس.

## أسئلة شائعة

*هل يعمل هذا مع ملفات .xlsx التي تم إنشاؤها بواسطة Excel 365؟*  
نعم. تدعم Aspose.Cells مواصفة Office Open XML بالكامل، لذا يعمل نفس الكود مع أي ملف `.xlsx` حديث.

*ماذا لو كان المصنف يحتوي على جداول متعددة؟*  
استرجع الجدول المطلوب بالاسم: `var table = worksheet.ListObjects["MyTable"];` ثم طبّق `DeleteRows` كما هو موضح.

*هل يمكنني حذف الصفوف دون استخدام مكتبة طرف ثالث؟*  
يمكنك استخدام Microsoft.Office.Interop.Excel عبر COM interop، لكن ذلك يتطلب تثبيت Excel على الخادم ويضيف عبئًا متعلقًا بـ COM. توفر Aspose.Cells بديلاً خفيفًا وآمنًا للخوادم.

## الخلاصة

أنت الآن تعرف كيفية حذف صفوف من جدول Excel بأمان وكيفية حذف عدة صفوف من ورقة Excel باستخدام C#. التقنية الأساسية تعتمد على طريقة `ListObject.DeleteRows` التي تحافظ على رأس الجدول، بينما التقنية الثانوية تستخدم `Rows.RemoveAt` للأوراق العادية. طبّق هذه الأنماط لتنظيف البيانات، أتمتة إنشاء التقارير، أو تنفيذ ميزات تعديل جماعي في تطبيقاتك.

**الخطوات التالية**

* استكشف ميزات Aspose.Cells الأخرى مثل إدراج الصفوف، نسخ الأنماط، أو تصفية البيانات.  
* جرّب نفس العمليات باستخدام **ClosedXML** إذا كنت تفضّل مكتبة مفتوحة المصدر؛ الـ API مشابه لكنه يستخدم `IXLTable` و `IXLRows`.  
* اجمع منطق حذف الصفوف مع استعلامات LINQ لبناء خطوط أنابيب تنظيف بيانات أكثر تعقيدًا.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية حذف الصفوف في Excel باستخدام C# – حماية رأس الجدول](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [كيفية استخدام Aspose.Cells لحذف الصفوف في جدول Excel مع الحفاظ على](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [تحميل ملف Excel C# – كيفية حذف الصفوف وإزالة صفوف محددة](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}