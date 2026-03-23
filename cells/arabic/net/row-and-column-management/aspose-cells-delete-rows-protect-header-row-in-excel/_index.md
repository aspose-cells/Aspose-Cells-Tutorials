---
category: general
date: 2026-03-22
description: Aspose Cells حذف الصفوف مع حماية صف العنوان. تعلم كيفية استرجاع الجدول
  الأول وحذف صفوف جدول Excel بأمان باستخدام C#.
draft: false
keywords:
- aspose cells delete rows
- protect header row
- delete excel table rows
- retrieve first table
language: ar
og_description: حذف الصفوف باستخدام Aspose Cells مع حماية صف الرأس. تعلّم كيفية استرجاع
  الجدول الأول وحذف صفوف جدول Excel بأمان في C#.
og_title: Aspose Cells حذف الصفوف – حماية صف العنوان في Excel
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose Cells حذف الصفوف – حماية صف العنوان في Excel
url: /ar/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Delete Rows – حماية صف العنوان في Excel

هل سبق لك أن حاولت **aspose cells delete rows** من جدول واكتشفت أن العنوان اختفى؟ هذا هو الخطأ الشائع عند التعامل مع أوراق Excel برمجياً. في هذا الدليل سنستعرض حلاً كاملاً قابلاً للتنفيذ **يحمي صف العنوان**، يوضح لك كيفية **retrieve first table**، ويحذف **Excel table rows** بأمان دون كسر البنية.

سنغطي كل شيء من تحميل المصنف إلى التعامل مع الاستثناء الذي ترميه Aspose عندما تحاول ترك العنوان معزولاً. في النهاية ستحصل على نمط ثابت يمكنك إدراجه في أي مشروع .NET يستخدم Aspose.Cells.

---

## ما الذي ستحتاجه

- **Aspose.Cells for .NET** (الإصدار 23.12 أو أحدث) – المكتبة التي تتيح لك العمل مع ملفات Excel دون الحاجة إلى تثبيت Office.  
- بيئة تطوير C# أساسية (Visual Studio، Rider، أو سطر أوامر `dotnet`).  
- ملف Excel (`TableWithHeader.xlsx`) يحتوي على جدول **ListObject** واحد على الأقل مع صف عنوان في الصف الأول.

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells.

---

## الخطوة 1: تحميل المصنف واسترجاع أول جدول  

أول شيء عليك فعله هو فتح المصنف والحصول على الجدول الذي تريد تعديلّه. هنا يأتي دور الكلمة المفتاحية الثانوية **retrieve first table**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains a table with a header row
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Access the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.ListObjects[0];

        // Continue with row deletion...
        DeleteRowsSafely(table);
    }
}
```

**لماذا هذا مهم:**  
- `Workbook` يقرأ الملف دون الحاجة إلى وجود Excel.  
- `worksheet.ListObjects[0]` هي أبسط طريقة لـ **retrieve first table**؛ إذا كان لديك جداول متعددة يمكنك التكرار أو استخدام اسم الجدول.

> **نصيحة محترف:** إذا لم تكن متأكدًا ما إذا كانت ورقة العمل تحتوي فعلاً على جدول، تحقق أولاً من `worksheet.ListObjects.Count` لتجنب استثناء `IndexOutOfRangeException`.

---

## الخطوة 2: حماية صف العنوان أثناء حذف الصفوف  

الآن يأتي جوهر الموضوع: **aspose cells delete rows** دون مسح العنوان. طريقة `DeleteRows` في Aspose تأخذ فهرسًا يبدأ من الصفر وعددًا. محاولة حذف العنوان (الصف 0) تُحدث استثناءً، وهذا ما نريد تجنبه.

```csharp
static void DeleteRowsSafely(ListObject table)
{
    try
    {
        // Attempt to delete rows 2‑3 (the header is row 1 in Excel, index 0 in code)
        // Here we start at index 1 (second row) and delete 2 rows.
        table.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted successfully.");
    }
    catch (Exception ex)
    {
        // The API throws an exception because the header would be removed
        Console.WriteLine("Operation blocked: " + ex.Message);
    }

    // Save the workbook to verify the result
    table.Worksheet.Workbook.Save(@"YOUR_DIRECTORY\Result.xlsx");
}
```

**شرح المنطق:**  

| الخطوة | السبب |
|--------|-------|
| `table.DeleteRows(1, 2);` | الفهرس 1 يشير إلى **الصف الثاني** (أول صف بيانات). حذف صفين يزيل الصفوف 2‑3 وفقًا لتسمية Excel، مع ترك العنوان (الصف 1) دون تغيير. |
| `catch (Exception ex)` | Aspose يرمي استثناءً **فقط** عندما تكون العملية ستحيد العنوان. التقاطه يتيح لك تسجيل رسالة ودية بدلاً من تعطل التطبيق. |
| `Save` | حفظ التغييرات يتيح لك فتح `Result.xlsx` ورؤية أن العنوان لا يزال موجودًا. |

> **ماذا لو كنت بحاجة فعلًا لحذف العنوان؟**  
> استخدم `table.ShowHeaders = false;` قبل الحذف، أو احذف الجدول بالكامل وأعد إنشائه. لكن في معظم السيناريوهات التجارية ستحرص على **protect header row**.

---

## الخطوة 3: التحقق من النتيجة – المخرجات المتوقعة  

بعد تشغيل البرنامج، افتح `Result.xlsx`. يجب أن ترى:

- الصف الأول لا يزال يحتوي على عناوين الأعمدة الأصلية.  
- الصفوف 2‑3 (التي استهدفناها) اختفت، وتم تحريك البيانات المتبقية للأعلى.  

ستظهر الرسالة في وحدة التحكم:

```
Rows deleted successfully.
```

إذا حاولت حذف العنوان عن طريق الخطأ (مثلاً `table.DeleteRows(0, 1);`)، ستكون النتيجة:

```
Operation blocked: Cannot delete header row of the table.
```

تؤكد هذه الرسالة أن الحماية المدمجة في Aspose تقوم بعملها.

---

## الخطوة 4: طرق بديلة لـ **Delete Excel Table Rows**  

أحيانًا تحتاج إلى تحكم أكبر—مثل حذف الصفوف بناءً على شرط، أو إزالة صفوف غير متجاورة. إليك نمطين سريعين يحافظان على سلامة العنوان.

### 4.1 حذف الصفوف عبر تصفية البيانات  

```csharp
static void DeleteRowsByCondition(ListObject table, string columnName, string valueToRemove)
{
    // Find the column index by name
    int colIndex = table.ListColumns[columnName].Index;

    // Iterate backwards to avoid messing up row indices
    for (int i = table.DataRange.RowCount - 1; i >= 0; i--)
    {
        var cell = table.DataRange[i, colIndex];
        if (cell.StringValue.Equals(valueToRemove, StringComparison.OrdinalIgnoreCase))
        {
            // Delete the row (add 1 because DataRange is zero‑based inside the table)
            table.DeleteRows(i + 1, 1);
        }
    }
}
```

### 4.2 حذف جماعي باستخدام نطاق  

```csharp
// Delete rows 5‑10 (still preserving the header)
table.DeleteRows(4, 6);   // 4 = 5th row in Excel, 6 = number of rows to delete
```

كلا المقتطفين يحترمان قاعدة **protect header row** لأن الفهرس الابتدائي لا ينزل أبداً إلى أقل من 1.

---

## الخطوة 5: الأخطاء الشائعة وكيفية تجنّبها  

| المشكلة | السبب | الحل |
|----------|-------|------|
| حذف العنوان عن طريق الخطأ | استخدام `0` كفهرس بداية | ابدأ دائمًا بـ `1` للصفوف البيانات، أو تحقق من `table.ShowHeaders` أولاً. |
| `IndexOutOfRangeException` عندما لا تحتوي الورقة على جداول | افتراض وجود جدول | تحقق من `worksheet.ListObjects.Count > 0` قبل الوصول إلى `[0]`. |
| عدم حفظ التغييرات | نسيان استدعاء `Save` | استدعِ `workbook.Save` بعد التعديلات. |
| حذف الصفوف في الوسط يغيّر الفهارس، مما يسبب تخطي بعض الصفوف | التكرار من الأمام أثناء الحذف | تكرّر **عكسيًا** أو اجمع الصفوف للحذف أولاً. |

---

## الخطوة 6: جمع كل شيء معًا – مثال كامل يعمل  

```csharp
using System;
using Aspose.Cells;

class AsposeDeleteRowsDemo
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Ensure a table exists
        if (sheet.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // 3️⃣ Retrieve the first table (retrieve first table)
        ListObject table = sheet.ListObjects[0];

        // 4️⃣ Delete rows safely (aspose cells delete rows while protecting header row)
        DeleteRowsSafely(table);

        // 5️⃣ (Optional) Delete rows by condition
        // DeleteRowsByCondition(table, "Status", "Closed");

        // 6️⃣ Save the result
        workbook.Save(@"YOUR_DIRECTORY\Result.xlsx");
        Console.WriteLine("Workbook saved as Result.xlsx");
    }

    static void DeleteRowsSafely(ListObject table)
    {
        try
        {
            // Delete rows 2‑3 (header stays intact)
            table.DeleteRows(1, 2);
            Console.WriteLine("Rows deleted successfully.");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Operation blocked: " + ex.Message);
        }
    }

    // Uncomment if you need conditional deletion
    /*
    static void DeleteRowsByCondition(ListObject table, string columnName, string valueToRemove)
    {
        int colIdx = table.ListColumns[columnName].Index;
        for (int i = table.DataRange.RowCount - 1; i >= 0; i--)
        {
            var cell = table.DataRange[i, colIdx];
            if (cell.StringValue.Equals(valueToRemove, StringComparison.OrdinalIgnoreCase))
            {
                table.DeleteRows(i + 1, 1);
            }
        }
    }
    */
}
```

شغّل هذا البرنامج، افتح `Result.xlsx` وسترى أن العنوان لم يتأثر بينما تم حذف الصفوف المحددة. هذا هو **الحل الكامل المتكامل** لـ **aspose cells delete rows** دون التضحية بالعنوان.

---

## الخلاصة  

لقد أوضحنا كيف **aspose cells delete rows** مع **protect header row**، وكيف **retrieve first table**، وعدة طرق لحذف **excel table rows** بأمان. النقاط الأساسية هي:

- ابدأ دائمًا الحذف من الفهرس 1 للحفاظ على العنوان.  
- استخدم `try/catch` للتعامل مع استثناء الحماية المدمج في Aspose.  
- تحقق من وجود الجدول قبل التنفيذ، وتكرّر عكسيًا عند حذف الصفوف شرطياً.

هل أنت مستعد للارتقاء؟ جرّب دمج هذا النهج مع واجهات **Aspose Cells** لتنسيق الصفوف المحذوفة قبل إزالتها، أو أتمتة العملية عبر عدة أوراق عمل. الاحتمالات لا حصر لها، والآن لديك نمط موثوق لتبنيه.

إذا وجدت هذا الدرس مفيدًا، اضغط إعجاب، شاركه مع زملائك، أو اترك تعليقًا بحلولك الخاصة للحالات الخاصة. Happy coding!  

---

![Aspose Cells Delete Rows Example – Header Row Protected](https://example.com/images/aspose-delete-rows.png "aspose cells delete rows")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}