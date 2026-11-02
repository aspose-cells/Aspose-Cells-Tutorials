---
category: general
date: 2026-03-21
description: تصدير جدول بيانات إكسل إلى DataTable مع رؤوس الأعمدة، تحديد عدد الخانات
  العشرية، وتصدير أول 100 صف باستخدام Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: ar
og_description: تعلم كيفية تصدير جدول بيانات Excel إلى DataTable، مع الحفاظ على العناوين،
  وتحديد عدد المنازل العشرية، واستخراج أول 100 صف في C#.
og_title: تصدير جدول بيانات إكسل في C# – دليل خطوة بخطوة
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: تصدير جدول بيانات إكسل في C# – دليل شامل
url: /ar/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير جدول بيانات Excel – دليل C# كامل

هل تحتاج إلى **export excel data table** من مصنف إلى `DataTable` في .NET؟ أنت في المكان الصحيح—هذا الدليل يوضح لك بالضبط كيفية القيام بذلك، مع الحفاظ على رؤوس الأعمدة، وتحديد عدد المنازل العشرية، واستخراج أول 100 صف فقط.  

إذا سبق لك أن حدقت في جدول بيانات وتساءلت، “كيف يمكنني إدخال هذا إلى تطبيقّي دون فقدان التنسيق؟” فأنت لست وحدك. خلال الدقائق القليلة القادمة سنحوّل هذا “ماذا‑لو” إلى حل ملموس يمكن نسخه ولصقه يعمل مع Aspose.Cells، مكتبة شهيرة لمعالجة Excel.

## ما ستتعلمه

- كيفية **export excel to datatable** باستخدام طريقة `ExportDataTable`.  
- كيفية الحفاظ على أسماء الأعمدة الأصلية (`export excel with headers`).  
- كيفية **limit decimal places excel** القيم عن طريق تكوين `ExportTableOptions`.  
- كيفية استرجاع أول 100 صف بأمان فقط (`export first 100 rows`).  

بدون سكريبتات خارجية، بدون سلاسل سحرية—فقط C# عادي يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 or later (or .NET Framework 4.7+) | يدعم Aspose.Cells كلاهما، لكن أطر التشغيل الأحدث توفر واجهات برمجة تطبيقات جاهزة للـ async. |
| Aspose.Cells for .NET NuGet package | يوفر `Workbook`، `ExportTableOptions`، ومساعد `ExportDataTable`. |
| A sample Excel file (e.g., `Numbers.xlsx`) | مصدر البيانات التي ستقوم بتصديرها. |
| Basic C# knowledge | ستتبع الشيفرات المرفقة، ولا يتطلب الأمر أي شيء معقد. |

إذا كان أي من ذلك غير مألوف لك، احصل على حزمة NuGet باستخدام `dotnet add package Aspose.Cells` وأنشئ ملف Excel صغير يحتوي على بعض الأرقام—بيانات الاختبار الخاصة بك.

![مثال على تصدير جدول بيانات Excel](excel-data-table.png "لقطة شاشة لورقة Excel سيتم تصديرها إلى DataTable")

## الخطوة 1: تحميل المصنف (export excel data table)

أول شيء تحتاجه هو كائن `Workbook` يشير إلى ملف Excel الخاص بك. فكر فيه كفتح كتاب قبل أن تتمكن من قراءة أي فصول.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **لماذا هذا مهم:** تحميل المصنف يمنحك الوصول إلى أوراق العمل، الخلايا، والأنماط. إذا كان مسار الملف خاطئًا، سيطلق Aspose استثناء `FileNotFoundException`، لذا تحقق من الموقع مرة أخرى.

## الخطوة 2: تكوين خيارات التصدير – limit decimal places excel

بشكل افتراضي، يقوم Aspose بتصدير كل قيمة رقمية بدقة كاملة. غالبًا ما تحتاج فقط إلى عدد قليل من الأرقام المهمة، خاصةً عند إدخال البيانات إلى شبكة واجهة مستخدم أو API يتوقع أرقامًا مُقربة.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى استراتيجية تقريب مختلفة (مثلاً، دائمًا تقريب للأعلى)، يمكنك معالجة `DataTable` بعد التصدير. إعداد `SignificantDigits` هو أسرع طريقة لـ **limit decimal places excel** دون كتابة حلقات إضافية.

## الخطوة 3: تصدير النطاق المطلوب (export first 100 rows)

الآن نخبر Aspose أي مجموعة من الخلايا نريد سحبها إلى `DataTable`. في هذا الدرس نأخذ أول 100 صف وأول 10 أعمدة، لكن يمكنك تعديل هذه الأعداد لتناسب حالتك.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **حالة حافة:** إذا كانت الورقة تحتوي على أقل من 100 صف، سيقوم Aspose ببساطة بتصدير ما هو موجود دون إلقاء خطأ. ومع ذلك، قد ترغب في الحماية من نطاق صغير غير متوقع:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## الخطوة 4: التحقق من النتيجة – طباعة سريعة إلى وحدة التحكم

رؤية البيانات في أداة التصحيح أمر جيد، لكن طباعة بعض الصفوف إلى وحدة التحكم يؤكد أن **export excel to datatable** قد نجح فعلاً وأن المنازل العشرية قد تم تقليلها.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### النتيجة المتوقعة

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

لاحظ كيف أن الأعمدة الرقمية الآن تظهر أربعة أرقام مهمة فقط، مطابقة لإعداد `SignificantDigits = 4` الذي طبقناه سابقًا.

## الخطوة 5: تجميع كل شيء – مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق وحدة تحكم. يتضمن معالجة الأخطاء، الحماية الاختيارية لعدد الصفوف، وطريقة المساعدة للطباعة.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

شغّل البرنامج، وسترى أول 100 صف من ورقتك، مُقربة بشكل جميل، مع الحفاظ على أسماء الأعمدة.

## أسئلة شائعة ومشكلات محتملة

| Question | Answer |
|----------|--------|
| **ماذا لو كانت ورقتي تحتوي على خلايا مدمجة؟** | `ExportDataTable` يقوم بتسوية الخلايا المدمجة بأخذ قيمة الخلية العليا‑اليسرى. إذا كنت بحاجة إلى معالجة مخصصة، قم بفك الدمج أولاً أو اقرأ كائنات `Cell` الخام. |
| **هل يمكنني التصدير إلى `DataSet` بدلاً من ذلك؟** | نعم—استخدم `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}