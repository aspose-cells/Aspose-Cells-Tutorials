---
category: general
date: 2026-02-28
description: حذف صفوف جدول إكسل في C# بسرعة. تعلم كيفية إضافة نطاق مسمى في إكسل، الوصول
  إلى ورقة العمل بالاسم، وتجنب أخطاء تكرار الاسم.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: ar
og_description: حذف صفوف جدول إكسل باستخدام C#. يوضح هذا الدرس أيضًا كيفية إضافة نطاق
  مسمى في إكسل والوصول إلى ورقة العمل بالاسم.
og_title: حذف الصفوف من جدول إكسل باستخدام C# – دليل شامل
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: حذف صفوف جدول إكسل باستخدام C# – دليل خطوة بخطوة
url: /ar/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف صفوف جدول Excel باستخدام C# – دليل برمجة كامل

هل احتجت يومًا إلى **delete rows excel table** من مصنف ولكنك لم تكن متأكدًا من أي استدعاء API تستخدم؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عندما يحاولون أول مرة تقليل حجم جدول برمجيًا.  

في هذا الدليل سنستعرض مثالًا كاملاً وقابلًا للتنفيذ لا يقتصر فقط على إزالة الصفوف من جدول Excel، بل يُظهر أيضًا **how to add defined name** (المعروفة باسم *named range*)، وكيفية **access worksheet by name**، ولماذا يؤدي إضافة اسم مكرر في ورقة أخرى إلى رمي استثناء `InvalidOperationException`.  

بنهاية المقال ستكون قادرًا على:

* الحصول على ورقة عمل باستخدام اسم تبويبها.  
* حذف صفوف البيانات بأمان من أول جدول في تلك الورقة.  
* إنشاء نطاق مسمى يشير إلى عنوان محدد.  
* فهم مشاكل الأسماء المكررة عبر الأوراق.

لا حاجة إلى وثائق خارجية—كل ما تحتاجه موجود هنا.

---

## ما ستحتاجه

* **DevExpress Spreadsheet** (أو أي مكتبة تُظهر كائنات `Workbook` و `Worksheet` و `ListObject` و `Names`).  
* مشروع .NET يستهدف **.NET 6** أو أحدث (الكود يُترجم مع .NET Framework 4.8 أيضًا).  
* إلمام أساسي بـ C#—إذا كنت تستطيع كتابة حلقة `foreach`، فأنت جاهز.

> **نصيحة احترافية:** إذا كنت تستخدم نسخة Community المجانية من DevExpress، فإن الـ APIs المستخدمة أدناه هي نفسها في النسخة التجارية.

## الخطوة 1 – الوصول إلى ورقة العمل بالاسم

أول شيء عليك فعله هو تحديد الورقة التي تحتوي على الجدول الذي تريد تعديله.  
معظم المطورين يستخدمون `Worksheets[0]` من باب العادة، لكن ذلك يربط كودك بترتيب الأوراق ويتعطل بمجرد أن يقوم أحدهم بإعادة تسمية تبويب.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*لماذا هذا مهم:* باستخدام **name** للورقة بدلاً من فهرستها تتجنب التعديلات غير المقصودة على الورقة الخاطئة عندما يتغير المصنف.

إذا كان الاسم الذي قدمته غير موجود، فإن المكتبة ترمي استثناء `KeyNotFoundException`، والذي يمكنك التقاطه لعرض رسالة خطأ ودية.

---

## الخطوة 2 – حذف صفوف جدول Excel (الطريقة الآمنة)

الآن بعد أن حصلت على ورقة العمل الصحيحة، لنقم بإزالة صفوف البيانات من أول جدول.  
خطأ شائع هو استدعاء `DeleteRows(1, rowCount‑1)`. منذ **DevExpress 22.2** هذا التحميل محظور **prohibited** ويرمي استثناء `InvalidOperationException`. المكتبة تتوقع منك حذف الصفوف **داخل نطاق بيانات الجدول**، وليس صف الرأس.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **ماذا لو كان الجدول فارغًا؟** شرط الـ `if` يمنع استدعاء مع `rowCount = 0`، والذي كان سيثير استثناءً.

### نظرة بصرية  

![مثال حذف صفوف جدول excel](image.png "لقطة شاشة تُظهر حذف الصفوف من جدول Excel")  

*نص بديل: مثال حذف صفوف جدول excel في كود C#*

## الخطوة 3 – كيفية إضافة اسم معرف (إنشاء نطاق مسمى)

بعد تنظيف الجدول قد ترغب في الإشارة إلى نطاق محدد لاحقًا—مثلًا لرسمة بيانية أو قائمة تحقق من البيانات. هنا يأتي دور **add named range excel**.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

طريقة `Names.Add` تأخذ معاملين: المعرف والعنوان بنمط A1.  
نظرًا لأننا استخدمنا **access worksheet by name** سابقًا، يمكن لسلسلة العنوان الإشارة بأمان إلى أي ورقة دون القلق بشأن تغيّر الفهرس.

## الخطوة 4 – النطاق المسمى في ورقة أخرى – تجنب أخطاء الأسماء المكررة

قد تعتقد أنه يمكنك إعادة استخدام نفس المعرف في ورقة مختلفة، مثل هذا:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

للأسف، نطاق تسمية Excel هو **workbook‑wide**، وليس لكل ورقة. الاستدعاء أعلاه يطلق استثناء `InvalidOperationException` بالرسالة *“A name with the same identifier already exists.”*

### كيفية التحايل على ذلك

1. **اختر اسمًا فريدًا** (`MyTable_Sheet2`).  
2. **احذف الاسم الموجود** قبل إعادة إضافته (فقط إذا كنت تريد استبداله فعلاً).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

## مثال كامل وقابل للتنفيذ

بجمع كل شيء معًا، إليك تطبيق console مستقل يمكنك وضعه في Visual Studio وتشغيله على ملف `sample.xlsx` تجريبي.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**النتيجة المتوقعة**

* جميع صفوف البيانات من أول جدول في **Sheet1** تختفي، تاركةً صف الرأس فقط.  
* الاسم **MyTable** الآن يشير إلى `Sheet1!$A$1:$C$5`.  
* اسم ثاني **MyTable_Sheet2** يشير بأمان إلى نطاق في **Sheet2** دون رمي استثناء.

## أسئلة شائعة وحالات حافة

| السؤال | الإجابة |
|----------|--------|
| *ماذا لو كان المصنف يحتوي على جداول متعددة؟* | احصل على `ListObject` الصحيح حسب الفهرس (`worksheet.ListObjects[1]`) أو حسب الاسم (`worksheet.ListObjects["MyTable"]`). |
| *هل يمكنني حذف صفوف من جدول يمتد عبر أوراق عمل متعددة؟* | لا—الجداول محصورة في ورقة واحدة. يجب تكرار منطق الحذف لكل ورقة. |
| *هل هناك طريقة لحذف جزء فقط من الصفوف؟* | نعم—استخدم `table.DeleteRows(startRow, count)` حيث `startRow` يبدأ من الصفر داخل نطاق بيانات الجدول. |
| *هل تستمر النطاقات المسمية بعد الحفظ؟* | بالطبع. بمجرد استدعاء `SaveDocument`، تصبح الأسماء جزءًا من XML المصنف. |
| *كيف يمكنني سرد جميع الأسماء المعرفة في المصنف؟* | استخدم حلقة `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

## الخلاصة

لقد غطينا **delete rows excel table** باستخدام C#، وأظهرنا **add named range excel**، وأوضحنا الطريقة الصحيحة لـ **access worksheet by name** مع تجنب استثناء الاسم المكرر المخيف.  

الحل الكامل موجود في المقتطف البرمجي أعلاه—انسخه، الصقه، وشغله على ملفاتك الخاصة. من هنا يمكنك توسيع المنطق للتعامل مع جداول متعددة، حسابات نطاق ديناميكية، أو حتى دمجه مع واجهة مستخدم.

**الخطوات التالية** التي قد تستكشفها:

* استخدم **named range on another sheet** لتغذية سلاسل الرسوم البيانية.  
* اجمع منطق الحذف مع **ExcelDataReader** لاستيراد البيانات قبل تنظيفها.  
* قم بأتمتة التحديثات الجماعية عبر العشرات من المصنفات باستخدام حلقة `foreach (var file in Directory.GetFiles(...))` بسيطة.

هل لديك المزيد من الأسئلة حول أتمتة Excel في C#؟ اترك تعليقًا، ولنستمر في النقاش. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}