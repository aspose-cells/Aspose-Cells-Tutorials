---
category: general
date: 2026-08-07
description: حذف الصفوف من جدول Excel باستخدام C#. تعلم كيفية إزالة صفوف البيانات
  في Excel بأمان مع حماية صف العنوان في Excel في بضع خطوات فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: ar
lastmod: 2026-08-07
og_description: احذف الصفوف من جدول إكسل برمجيًا. يوضح لك هذا الدليل كيفية إزالة صفوف
  البيانات بأمان وحماية صف الرأس في إكسل باستخدام Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: حذف الصفوف من جدول Excel – حل سريع بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: حذف الصفوف من جدول إكسل – دليل C# الكامل
url: /ar/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف الصفوف من جدول Excel – دليل كامل C# 

إذا كنت بحاجة إلى **delete rows from Excel table** في مشروع .NET، فإن هذا الدرس يوضح لك طريقة موثوقة للقيام بذلك. سواءً كنت تقوم بتنظيف البيانات المستوردة أو تقليص تقرير، سترى كيف تُزيل **remove data rows excel** بينما يقوم الـ API تلقائيًا **protect header row excel** من الحذف العرضي.

في الخطوات أدناه ستتعلم كيفية تحميل دفتر العمل، حذف الصفوف بأمان، وأخيرًا حفظ التغييرات. يغطي الدليل أيضًا الخطأ الشائع المتمثل في محاولة حذف صف الرأس ويشرح لماذا تمنع المكتبة ذلك. في النهاية ستكون قادرًا على **remove data rows excel** بثقة في أي حل يعتمد على Aspose.Cells‑based solution.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث مثبت.
- حزمة **Aspose.Cells for .NET** من NuGet (الإصدار 23.10 أو أحدث). قم بتثبيتها باستخدام:

  ```bash
  dotnet add package Aspose.Cells
  ```

- ملف Excel (`TableWithHeader.xlsx`) يحتوي على جدول منظم مع صف رأس في ورقة العمل الأولى.
- إلمام أساسي بـ C# و Visual Studio (أو أي بيئة تطوير تفضلها).

## الخطوة 1: تحميل دفتر العمل الذي يحتوي على جدول مع صف رأس

العملية الأولى هي فتح دفتر العمل الذي يحتوي على الجدول الذي تريد تعديله. تقوم Aspose.Cells بقراءة الملف إلى الذاكرة دون الحاجة إلى تثبيت Excel.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**لماذا هذا مهم:** تحميل دفتر العمل ينشئ كائن `Workbook` يمنحك الوصول إلى أوراق العمل والجداول والخلايا. بدون هذا الكائن لا يمكنك تعديل بنية Excel.

## الخطوة 2: الوصول إلى ورقة العمل الأولى والجدول الأول فيها

في معظم الأمثلة البسيطة يتم الاحتفاظ بالجدول في ورقة العمل الأولى وعلى الفهرس 0، لكن يمكنك تعديل الفهارس وفقًا لسيناريوك.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**لماذا هذا مهم:** `ListObject` يمثل جدول Excel، والذي يتضمن صف الرأس، صفوف البيانات، وأي تنسيق. العمل مع كائن الجدول يضمن احترامك لسمات جدول Excel، مثل حماية صف الرأس.

## الخطوة 3: محاولة حذف صف الرأس (لإظهار الحماية)

تقوم Aspose.Cells بإلقاء استثناء إذا حاولت حذف صف الرأس لأن الـ API **protect header row excel** مصمم لذلك. إظهار هذا السلوك يساعدك على فهم لماذا فشل الحذف المباشر.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**المخرجات المتوقعة**

```
Deletion prevented: Cannot delete the header row of a table.
```

**شرح:** طريقة `DeleteRows` تستقبل فهرس بداية يبدأ من الصفر وعدد. الفهرس 0 يشير إلى صف الرأس، والذي تحميه المكتبة للحفاظ على بنية الجدول سليمة.

## الخطوة 4: حذف صفوف البيانات فقط – الطريقة الصحيحة لـ **remove data rows excel**

الآن بعد أن علمت أن صف الرأس محمي، احذف فقط صفوف البيانات التي تبدأ بعد صف الرأس. في معظم الجداول يكون أول صف بيانات على الفهرس 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**لماذا هذا يعمل:** بالبدء من الفهرس 1 تتخطى صف الرأس، لذا العملية تتوافق مع قاعدة **protect header row excel**. تقوم طريقة `DeleteRows` بتحديث النطاق الداخلي للجدول تلقائيًا.

## الخطوة 5: حفظ دفتر العمل المعدل

احفظ التغييرات في ملف جديد لتبقي النسخة الأصلية سليمة.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**النتيجة:** بعد تشغيل البرنامج، يحتوي `TableHeaderProtected.xlsx` على نفس صف الرأس، لكن صفوف البيانات المحددة قد اختفت. فتح الملف في Excel يظهر جدولًا نظيفًا بدون الصفوف المحذوفة.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| محاولة حذف صف الرأس | Aspose.Cells يفرض سلامة الجدول | ابدأ دائمًا الحذف من الفهرس 1 أو أعلى |
| حذف عدد صفوف أكثر مما هو موجود | `DeleteRows` يطرح `ArgumentOutOfRangeException` | تحقق من `table.DataRange.RowCount` قبل استدعاء `DeleteRows` |
| العمل مع نطاق غير جدول | طرق `ListObject` تنطبق فقط على الجداول المنظمة | حوّل النطاق إلى جدول أولًا (`worksheet.Tables.Add`) إذا لزم الأمر |

**نصيحة احترافية:** إذا كنت بحاجة إلى مسح الجدول بالكامل مع الحفاظ على الصف الرأس، استخدم `table.DeleteRows(1, table.DataRange.RowCount - 1);`. هذا يزيل كل صف بيانات بغض النظر عن عدد الصفوف الحالية في الجدول.

## بديل: حذف الصفوف بواسطة عنوان الخلية

أحيانًا قد تعرف عنوان الخلية الدقيق بدلاً من فهرس الصف. يمكنك تحويل العنوان إلى فهرس صف باستخدام مجموعة `Cells`:

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

هذا النهج مفيد عندما يتم تحديد الصفوف المراد إزالتها بناءً على المحتوى بدلاً من عدد ثابت.

## اختبار تنفيذك

1. شغّل البرنامج باستخدام دفتر عمل تجريبي يحتوي على ما لا يقل عن خمسة صفوف بيانات.  
2. تحقق من أن وحدة التحكم تطبع “Rows deleted and workbook saved successfully.”  
3. افتح `TableHeaderProtected.xlsx` في Excel وتأكد من:
   - أن صف الرأس لا يزال موجودًا.
   - أن الصفوف البيانات المطلوبة فقط هي المفقودة.

إذا اختفى صف الرأس، فمن المحتمل أنك بدأت الحذف من الفهرس 0—راجع **Step 4**.

## الخلاصة

أنت الآن تعرف كيفية **delete rows from Excel table** بأمان باستخدام C#. غطى الدليل تحميل دفتر العمل، الوصول إلى الجدول، احترام قاعدة **protect header row excel**، حذف **remove data rows excel** بشكل صحيح، وحفظ النتيجة. باتباع هذه الخطوات تتجنب الأخطاء الشائعة وتحافظ على بنية جداول Excel منظمة.

### الخطوات التالية

- استكشف ميزات **Aspose.Cells** مثل إدراج الصفوف، تطبيق الأنماط، أو تصفية البيانات.  
- اجمع حذف الصفوف مع **Excel formulas** لأتمتة التنظيف بناءً على نتائج الحساب.  
- اطلع على المواضيع ذات الصلة مثل **exporting Excel to CSV** أو **reading large workbooks efficiently**.

لا تتردد في تجربة عدد صفوف مختلف، جداول متعددة، أو حذف شرطي. إذا واجهت حالات حافة، ارجع إلى معالجة الأخطاء الموضحة في **Step 3**—ستحمي المكتبة دائمًا صف الرأس لك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [حذف عدة صفوف في Excel باستخدام Aspose.Cells .NET: دليل شامل لتعامل البيانات](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [كيفية إدراج وحذف الصفوف في Excel باستخدام Aspose.Cells for .NET: دليل شامل](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [كيفية حذف الصفوف الفارغة في Excel باستخدام Aspose.Cells .NET لتنظيف البيانات](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}