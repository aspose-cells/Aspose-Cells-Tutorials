---
category: general
date: 2026-08-11
description: كيفية إعادة تسمية جدول في Excel باستخدام C# و Aspose.Cells. تعلم إنشاء
  مصنف Excel، إضافة نطاق مسمى، وتجنب تعارضات إعادة التسمية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: ar
lastmod: 2026-08-11
og_description: كيفية إعادة تسمية جدول في Excel باستخدام C# و Aspose.Cells. يوضح هذا
  الدليل كيفية إنشاء مصنف Excel، إضافة نطاق مسمى، وإعادة تسمية جدول Excel بأمان.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: كيفية إعادة تسمية جدول في Excel باستخدام C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: كيفية إعادة تسمية جدول في Excel باستخدام C# – دليل خطوة بخطوة
url: /ar/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إعادة تسمية جدول في Excel باستخدام C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **كيفية إعادة تسمية جدول** في ملف Excel برمجياً، فإن هذا الدليل يوضح لك النهج الدقيق باستخدام Aspose.Cells for .NET. سترى كيف **تنشئ دفتر عمل Excel**، وتعرّف **نطاقًا مسمىً**، وتعيد تسمية جدول Excel موجود دون التسبب في تعارض أسماء.

يعمل الحل مع أي مشروع .NET يستهدف .NET 6 أو أحدث ويتطلب فقط حزمة Aspose.Cells NuGet. بحلول نهاية الدليل يمكنك إعادة تسمية جدول Excel بأمان وفهم سبب حدوث تعارض عندما يتطابق اسم الجدول مع نطاق معرف.

## المتطلبات المسبقة

- .NET 6 SDK أو أحدث مثبت  
- Visual Studio 2022 (أو أي بيئة تطوير C#)  
- حزمة Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)  

لا توجد حاجة إلى أي تجميعات interop إضافية لـ Excel لأن Aspose.Cells يعمل بالكامل في الذاكرة.

## نظرة عامة على الحل

1. **Create Excel workbook** – إنشاء كائن `Workbook` وإضافة بعض البيانات التجريبية.  
2. **Add a named range** – استخدم `Worksheets.Names.Add` لإنشاء نطاق باسم `MyRange`.  
3. **Create an Excel table (ListObject)** – تحويل البيانات إلى جدول حتى يكون لدينا ما نعيد تسميته.  
4. **Rename the table** – محاولة تعيين خاصية `Name` للجدول إلى نفس المعرف كما في النطاق المسمى.  
5. **Handle name conflicts** – التقاط الاستثناء، شرح سبب حدوثه، وعرض استراتيجية إعادة تسمية آمنة.  

يتم شرح كل خطوة بالتفصيل أدناه.

## الخطوة 1: كيفية إنشاء دفتر عمل Excel وتعبئة البيانات

إنشاء دفتر عمل هو الأساس لأي مهمة أتمتة Excel. تمثل فئة `Workbook` الملف بالكامل في الذاكرة.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**لماذا هذا مهم:** يجب أن يحتوي دفتر العمل على بيانات قبل أن تتمكن من إنشاء جدول. تقوم Aspose.Cells بتخزين البيانات في مجموعة ذات فهرس يبدأ من الصفر، لذا `Worksheets[0]` يشير دائمًا إلى الورقة الأولى.

## الخطوة 2: كيفية إضافة نطاق مسمى إلى ورقة العمل

يتيح لك **النطاق المسمى** الإشارة إلى خلية أو نطاق محدد بمعرف سهل. إضافة نطاق أمر بسيط:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**لماذا هذا مهم:** يتم تخزين النطاقات المسمية في مجموعة الأسماء العامة لدفتر العمل. إذا حصل جدول لاحقًا على نفس الاسم، تقوم Aspose.Cells بإلقاء استثناء `CellException` لأن Excel لا يسمح بأسماء مكررة.

## الخطوة 3: كيفية إضافة جدول Excel (ListObject)

يوفر الجدول معالجة بيانات منظمة، وتصفية، وتنسيق. في Aspose.Cells يُطلق عليه **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**لماذا هذا مهم:** الآن الجدول موجود بالاسم `InitialTable`. إعادة تسميته توضح عملية **كيفية إعادة تسمية جدول**.

## الخطوة 4: كيفية إعادة تسمية جدول Excel ومعالجة التعارضات

محاولة إعادة تسمية الجدول إلى `MyRange` ستتعارض مع النطاق المسمى الذي أنشأناه سابقًا. يُظهر الشيفرة التالية النمط الصحيح لاكتشاف وحل التعارض.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### ما يفعله الكود

| الخطوة | الإجراء | السبب |
|------|--------|--------|
| **محاولة إعادة تسمية** | `table.Name = "MyRange"` | يوضح سيناريو التعارض. |
| **التقاط الاستثناء** | Prints the conflict message. | يوفر لك ملاحظات فورية حول المشكلة. |
| **إنشاء اسم آمن** | `GetUniqueTableName` adds a numeric suffix until the name is free. | يضمن أن اسم الجدول الجديد **لا** يتصادم مع أي نطاق مسمى أو جدول موجود. |
| **حفظ دفتر العمل** | `workbook.Save("RenamedTable.xlsx")` | يحفظ التغييرات حتى تتمكن من فتح الملف في Excel والتحقق من النتيجة. |

**الناتج المتوقع** عند تشغيل البرنامج:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

فتح `RenamedTable.xlsx` يظهر جدولًا باسم `MyRange_1` ونطاقًا مسمىً منفصلًا `MyRange` يشير إلى الخلية A1.

## لماذا يحدث التعارض وأفضل الممارسات لإعادة تسمية جدول Excel

- Excel يخزن **النطاقات المسمية** و **أسماء الجداول** في نفس مساحة الاسم.  
- عندما تحاول تعيين اسم جدول موجود بالفعل كنطاق، تقوم Aspose.Cells بإلقاء استثناء `CellException`.  
- النهج الموصى به هو **التحقق من الأسماء الموجودة أولاً** (كما هو موضح في `NameExists`) أو استخدام نمط تسمية يضمن التفرد (مثلاً، إضافة بادئة `tbl_` للجداول).  

تطبيق هذا النمط يمنع أخطاء وقت التشغيل ويجعل أتمتتك أكثر قوة.

## نصائح إضافية للعمل مع Aspose.Cells

- **نصيحة احترافية:** استخدم `Workbook.Worksheets.Names.Remove("MyRange")` إذا كنت ترغب عمدًا في استبدال النطاق باسم جدول.  
- **احذر حساسية الأحرف:** Excel يتعامل مع الأسماء دون حساسية لحالة الأحرف؛ تستخدم طرق المساعدة `OrdinalIgnoreCase` لمحاكاة سلوك Excel.  
- **الأداء:** إذا كنت تعالج العديد من أوراق العمل، قم بتخزين مجموعة الأسماء في الذاكرة المؤقتة بدلاً من التكرار المتكرر.

## مثال كامل في كتلة واحدة

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم. يتضمن جميع الخطوات من إنشاء دفتر العمل إلى إعادة تسمية الجدول بأمان.

```csharp
using System;
using Aspose.Cells;

class RenameTableDemo
{
    static void Main()
    {
        // Create workbook and populate data
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);

        // Add named range "MyRange" pointing to A1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");

        // Convert the data range into a table named "InitialTable"
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(0, 0, 4, 3, true)];
        table.Name = "InitialTable";

        // Attempt to rename the table to "MyRange" – this will conflict
        try
        {
            table.Name = "MyRange";
            Console


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء نطاقات مسماة على مستوى دفتر العمل في Excel باستخدام Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [كيفية تنفيذ صيغ النطاق المسمى في .NET باستخدام Aspose.Cells لأتمتة Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [كيفية إضافة مقاطع إلى جداول Excel باستخدام Aspose.Cells for .NET: دليل شامل](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}