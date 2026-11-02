---
category: general
date: 2026-03-21
description: كيفية تصدير بيانات Excel مع أسماء الأعمدة، والحفاظ على تنسيق الأرقام،
  وقراءة صفوف محددة باستخدام Aspose.Cells في C#. تعلم كيفية قراءة ورقة عمل Excel وتصدير
  الصفوف المحددة بكفاءة.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: ar
og_description: كيفية تصدير بيانات Excel مع أسماء الأعمدة، والحفاظ على تنسيق الأرقام،
  وقراءة صفوف محددة باستخدام Aspose.Cells. مثال كامل وقابل للتنفيذ لمطوري C#.
og_title: كيفية تصدير بيانات Excel في C# – دليل برمجي كامل
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: كيفية تصدير بيانات إكسل في C# – دليل خطوة بخطوة
url: /ar/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير بيانات Excel في C# – دليل برمجة كامل

هل تساءلت يومًا **how to export excel** البيانات دون فقدان التنسيق الأصلي؟ ربما جربت النسخ‑اللصق السريع وانتهى بك الأمر بتواريخ تظهر كـ “44728” أو بفقدان رؤوس الأعمدة. هذا محبط، أليس كذلك؟ في هذا الدرس ستتعرف على طريقة نظيفة وشاملة لقراءة ورقة عمل Excel، الحفاظ على تنسيق الأرقام، التصدير مع أسماء الأعمدة، وحتى اختيار الصفوف التي تحتاجها فقط.

سنستخدم مكتبة Aspose.Cells لأنها تمنحك تحكمًا دقيقًا في خيارات التصدير. بنهاية هذا الدليل ستحصل على مقتطف قابل لإعادة الاستخدام يمكن إدراجه في أي مشروع .NET، وستفهم لماذا كل خيار مهم. لا حاجة إلى مستندات خارجية—كل ما تحتاجه موجود هنا.

---

## ما ستتعلمه

- **Read Excel worksheet** إلى الذاكرة باستخدام Aspose.Cells.
- **Export specific rows** (مثلاً الصفوف 0‑49) مع الحفاظ على أسماء الأعمدة.
- **Preserve number format** بحيث تبقى العملات والتواريخ والنسب المئوية كما هي.
- كيفية **export with column names** وتضمين تعليقات الخلايا إذا احتجت إليها.
- مثال كامل وجاهز للتنفيذ بلغة C# بالإضافة إلى نصائح حول المشكلات الشائعة.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).
- Aspose.Cells لـ .NET مثبت عبر NuGet (`Install-Package Aspose.Cells`).
- ملف Excel (`input.xlsx`) موجود في مجلد يمكنك الإشارة إليه.

> **Pro tip:** إذا كنت على خط أنابيب CI، فكر في سحب حزمة NuGet من مصدر خاص لتجنب مفاجآت الترخيص.

---

## الخطوة 1 – تثبيت Aspose.Cells وإضافة المساحات الاسمية

أولاً، تأكد من وجود حزمة Aspose.Cells في مشروعك. افتح وحدة تحكم مدير الحزم Package Manager Console وشغّل:

```powershell
Install-Package Aspose.Cells
```

ثم أضف توجيهات `using` المطلوبة في أعلى ملف C# الخاص بك:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

هذه الاستيرادات تمنحك الوصول إلى `Workbook` و `Worksheet` و `ExportTableOptions` و `DataTable`—وهي المكونات الأساسية لـ **reading an Excel worksheet** وتصدير البيانات.

---

## الخطوة 2 – تحميل المصنف (Read the Excel File)

الآن نقوم فعليًا بـ **read the Excel worksheet**. يأخذ مُنشئ `Workbook` مسار الملف، وستتعامل Aspose.Cells مع كل من صيغ `.xlsx` و `.xls` القديمة.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** تحميل المصنف مرة واحدة وإعادة استخدام كائن `Worksheet` نفسه أكثر كفاءة بكثير من فتح الملف مرارًا، خاصةً مع جداول البيانات الكبيرة.

---

## الخطوة 3 – تكوين خيارات التصدير (Preserve Number Format & Column Names)

هنا نخبر Aspose.Cells *كيف* يتم التصدير. تسمح لنا فئة `ExportTableOptions` بضبط الإخراج بدقة. سنفعّل ثلاث علامات:

1. `ExportAsString = true` – يجبر كل خلية على أن تصبح سلسلة نصية، مما يضمن أن الأرقام تحتفظ بتمثيلها البصري.
2. `IncludeCellComments = true` – ينسخ أي تعليقات مرفقة بالخلايا (مفيد للتوثيق).
3. `PreserveNumberFormat = true` – يحتفظ بالتنسيق الأصلي للرقم (رموز العملة، أنماط التاريخ، إلخ).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** إذا ضبطت `ExportAsString` على `false` لكن لا تزال تريد الحفاظ على تنسيقات الأرقام، قد تحصل على قيم رقمية خام (مثلاً 44728 لتاريخ). إبقاء العلامتين مفعّلتين يتجنب هذه المفاجأة.

---

## الخطوة 4 – الحصول على الورقة الأولى (Read Excel Worksheet)

معظم الملفات البسيطة تحتوي على البيانات التي تحتاجها في الورقة الأولى، لذا سنستخرجها حسب الفهرس. إذا كنت بحاجة إلى ورقة مختلفة، استبدل `0` بالفهرس الصفري المناسب أو استخدم `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** الوصول المباشر إلى كائن الورقة يمنحك تحكمًا كاملاً في مجموعة `Cells` الخاصة به، وهو أمر أساسي لـ **export specific rows** لاحقًا.

---

## الخطوة 5 – تصدير نطاق من الخلايا (Export Specific Rows)

الآن نصل إلى جوهر الدرس: تصدير الصفوف 0‑49 والأعمدة 0‑4 (أي أول 50 صفًا وأول خمسة أعمدة) إلى `DataTable`. سنطلب أيضًا من Aspose.Cells تضمين أسماء الأعمدة كأول صف في `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### ما يفعله هذا

- **`startRow: 0`** – يبدأ من أعلى الورقة.
- **`totalRows: 50`** – يلتقط أول 50 صفًا (أي **export specific rows**).
- **`totalColumns: 5`** – يحدّ التصدير إلى أول خمسة أعمدة.
- **`includeColumnNames: true`** – يضمن أن رؤوس أعمدة `DataTable` تتطابق مع صف رأس Excel، مما يلبي متطلب **export with column names**.
- **`exportOptions`** – يطبق الإعدادات من الخطوة 3، بحيث تبقى القيم الرقمية تظهر كـ “$1,234.56” بدلاً من “1234.56”.

---

## الخطوة 6 – التحقق من التصدير (What the Result Looks Like)

لنطبع أول بضعة صفوف إلى وحدة التحكم حتى تتمكن من رؤية أن التنسيق بقي.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**المخرجات المتوقعة (مثال):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

لاحظ كيف تظهر التواريخ بصيغة `MM/dd/yyyy` والعملات تحتفظ برمز `$`—بفضل **preserve number format**.

---

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| Dates turn into large numbers | `ExportAsString` left `false` | Keep `ExportAsString = true` or convert cells manually |
| Missing column headers | `includeColumnNames` set to `false` | Set it to `true` when you need **export with column names** |
| Comments disappear | `IncludeCellComments` not enabled | Turn on `IncludeCellComments` in `ExportTableOptions` |
| Exporting the wrong sheet | Using `Worksheets[0]` on a multi‑sheet file | Specify the sheet name: `workbook.Worksheets["Data"]` |
| Out‑of‑range exception | `totalRows` exceeds actual rows | Use `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## إضافي: تصدير الورقة بالكامل مع الحفاظ على التنسيقات

إذا قررت لاحقًا أنك بحاجة إلى تصدير الورقة بأكملها، ما عليك سوى استبدال `totalRows` و `totalColumns` بأبعاد الورقة القصوى:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

الآن لديك روتين **read excel worksheet** يعمل لأي حجم، مع الاستمرار في **preserving number format** و **exporting with column names**.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك إدراجه في تطبيق وحدة تحكم. يتضمن جميع الخطوات والاستيرادات وطباعة تحقق بسيطة.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

احفظه كـ `Program.cs`، شغّل `dotnet run`، ويجب أن ترى المعاينة المنسقة في الطرفية.

---

## الخاتمة

لقد استعرضنا للتو **how to export excel** البيانات باستخدام Aspose.Cells، مع تغطية كل شيء من تحميل المصنف إلى الحفاظ على تنسيق الأرقام، التصدير مع أسماء الأعمدة، وتحديد التصدير لصفوف معينة. الكود مستقل، قابل للتنفيذ بالكامل، ويتضمن تدابير واقية عملية لأكثر الحالات الشائعة.

هل أنت مستعد للتحدي التالي؟ جرّب التصدير مباشرة إلى CSV مع الحفاظ على تنسيق الأرقام الأصلي، أو ادفع `DataTable` إلى سياق Entity Framework Core لإدخالات قاعدة بيانات جماعية. كلا السيناريوهين يبنيان على الأساسيات نفسها التي غطيناها هنا.

إذا وجدت هذا الدليل مفيدًا

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}