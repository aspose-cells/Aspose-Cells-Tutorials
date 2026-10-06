---
category: general
date: 2026-03-25
description: تعلم كيفية تصدير Excel إلى DataTable في C# بسرعة. يغطي هذا الدرس تصدير
  Excel مع أسماء الأعمدة وتصدير بيانات Excel كسلسلة نصية للتعامل الموثوق مع البيانات.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: ar
og_description: تصدير Excel إلى DataTable في C# مع أسماء الأعمدة وتحويل السلاسل. اتبع
  هذا الدرس المختصر للحصول على حل جاهز للتنفيذ.
og_title: تصدير Excel إلى DataTable في C# – دليل كامل
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: تصدير إكسل إلى DataTable في C# – دليل خطوة بخطوة
url: /ar/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى DataTable في C# – دليل خطوة بخطوة

هل احتجت يوماً إلى **تصدير Excel إلى DataTable** لكن لم تكن متأكدًا من الإعدادات المطلوبة؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عند محاولتهم أول مرة سحب بيانات جدول البيانات إلى `DataTable`.

الخبر السار؟ في بضع أسطر من الشيفرة يمكنك **تصدير Excel مع أسماء الأعمدة** وحتى **تصدير بيانات Excel كسلسلة نصية** لتجنب مشاكل عدم توافق الأنواع. أدناه ستجد مثالًا كاملاً قابلاً للتنفيذ بالإضافة إلى شرح “السبب” وراء كل إعداد، لتتمكن من تكييفه مع أي مشروع دون تخمين.

## ما يغطيه هذا الدرس

* كيفية إنشاء مصنف في الذاكرة (دون الحاجة إلى ملف فعلي).  
* ملء بعض الصفوف التجريبية لتتمكن من رؤية النتيجة فورًا.  
* ضبط `ExportTableOptions` بحيث يُعامل كل خلية كسلسلة نصية.  
* تصدير نطاق مستطيل إلى `DataTable` مع الحفاظ على الصف الأول كعناوين أعمدة.  
* التحقق من النتيجة وطباعة الصف الأول إلى وحدة التحكم.  

لا توجد روابط توثيقية خارجية مطلوبة—كل ما تحتاجه موجود هنا. إذا كان لديك ملف Excel على القرص، ما عليك سوى استبدال سطر إنشاء المصنف بـ `new Workbook("path/to/file.xlsx")` وستكون جاهزًا.

---

## الخطوة 1: إعداد المشروع وإضافة حزمة Aspose.Cells من NuGet

قبل كتابة أي شيفرة، تأكد من أن مشروعك ي référencé **Aspose.Cells for .NET** (المكتبة التي توفر فئة `Workbook`). يمكنك إضافتها عبر مدير حزم NuGet:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة محترف:** استخدم أحدث نسخة مستقرة (اعتبارًا من مارس 2026، هي 22.12) للحصول على أحدث إصلاحات الأخطاء وتحسينات الأداء.

---

## الخطوة 2: إنشاء مصنف وتعبئته ببيانات تجريبية

سنبدأ بـ `Workbook` جديد تمامًا ونكتب بضع صفوف لتتمكن من رؤية عملية التصدير تعمل. تُظهر هذه الخطوة أيضًا **كيفية تصدير excel إلى datatable** عندما تكون البيانات المصدرية موجودة فقط في الذاكرة.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*لماذا هذا مهم:* بإدراج صف العناوين أولًا (`A1` & `B1`)، يمكننا لاحقًا إخبار المصدّر بأن يعامل الصف الأول كأسماء أعمدة—وهو بالضبط ما يعنيه **export excel with column names**.

---

## الخطوة 3: إخبار Aspose.Cells بمعالجة كل خلية كسلسلة نصية

عند تصدير خلايا رقمية أو تاريخية، يحاول Aspose استنتاج نوع .NET المناسب. قد يسبب ذلك أخطاءً دقيقة إذا كان الكود اللاحق يتوقع سلاسل نصية. علم `ExportTableOptions.ExportAsString` يفرض تحويلًا موحدًا إلى سلاسل نصية.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*لماذا نستخدم هذا؟* تخيل عمودًا يحتوي أحيانًا على أرقام وأحيانًا على نص (مثال: “00123” مقابل “ABC”). بتصدير كل شيء كسلسلة نصية تتجنب فقدان الأصفار البادئة أو حدوث استثناءات تحويل النوع.

---

## الخطوة 4: تصدير النطاق المطلوب إلى DataTable

الآن نقوم فعليًا بـ **export excel to datatable**. طريقة `ExportDataTable` تأخذ صف البداية/عمود البداية، عدد الصفوف/الأعمدة، علم لاستخراج أسماء الأعمدة، والإعدادات التي أنشأناها للتو.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*ما الذي يحدث في الخلفية؟*  
- `startRow: 0` يشير إلى الصف الأول في Excel (صف العناوين).  
- `exportColumnNames: true` يخبر Aspose بنقل “Name” و “Age” إلى مجموعة أعمدة `DataTable`.  
- `totalRows`/`totalColumns` يمكن أن تكون أكبر من البيانات الفعلية؛ الخلايا الزائدة تصبح سلاسل نصية فارغة بفضل `ExportAsString`.

---

## الخطوة 5: التحقق من النتيجة – طباعة الصف الأول

طباعة سريعة إلى وحدة التحكم تثبت أن التحويل نجح وأن أسماء الأعمدة لا تزال موجودة.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**الناتج المتوقع**

```
First row: Alice, 30
```

إذا غيرت البيانات التجريبية، سيعكس وحدة التحكم تلك التغييرات تلقائيًا—دون الحاجة إلى أي شيفرة إضافية.

---

## الأسئلة المتكررة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تصدير ورقة موجودة بالفعل على القرص؟** | نعم—استبدل `new Workbook()` بـ `new Workbook("myFile.xlsx")`. تبقى باقي الخطوات كما هي. |
| **ماذا لو كان ملف Excel يحتوي على خلايا مدمجة؟** | يتم فك الدمج؛ تُستخدم قيمة الخلية العليا اليسرى لكامل النطاق المدمج. |
| **هل يجب أن أقلق بشأن تنسيقات الأرقام الخاصة بالثقافة؟** | لا عندما يكون `ExportAsString = true`؛ كل شيء يُستقبل كسلسلة نصية كما هو معروض في Excel. |
| **كم عدد الصفوف التي يمكنني تصديرها مرة واحدة؟** | يمكن لـ Aspose.Cells معالجة ملايين الصفوف، لكن استهلاك الذاكرة يزداد مع حجم `DataTable`. فكر في التجزئة إذا وصلت إلى حدود الذاكرة. |
| **ماذا عن الأعمدة المخفية؟** | تُصدر الأعمدة المخفية ما لم تقم بتعيين `ExportHiddenColumns = false` في `ExportTableOptions`. |

---

## إضافي: تصدير إلى CSV بدلاً من DataTable

أحيانًا قد تفضل ملفًا مسطحًا. يمكن إعادة استخدام نفس `ExportTableOptions` مع `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

هذا السطر الواحد يمنحك ملف CSV جاهز للاستيراد مع الاستمرار في **exporting excel data as string**.

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

شغّل البرنامج (`dotnet run`) وسترى نتيجة **export excel to datatable** مطبوعة في وحدة التحكم. استبدل البيانات التجريبية، غير `totalRows`/`totalColumns`، أو وجه المصنف إلى ملف حقيقي—كل شيء يتوسع بسهولة.

---

## الخلاصة

أصبح لديك الآن **حل كامل ومستقل لتصدير Excel إلى DataTable** في C#. من خلال ضبط `ExportTableOptions.ExportAsString` تضمن **export excel data as string**، ومن خلال تعيين `exportColumnNames: true` تحصل على رؤوس الأعمدة المعتادة عند **export excel with column names**.

من هنا يمكنك:

* تمرير `DataTable` إلى Entity Framework أو Dapper لإدخالات جماعية.  
* إرساله إلى محرك تقارير مثل **FastReport** أو **RDLC**.  
* تحويله إلى JSON لاستجابة API (`JsonConvert.SerializeObject(table)`).

لا تتردد في التجربة—ربما تحاول تصدير ورقة أكبر، أو دمج هذا مع **how to export excel to datatable** من مشاركة شبكة. النمط يبقى نفسه، والشيفرة جاهزة للإنتاج.

---

![مخطط تحويل Excel → DataTable – تصدير excel إلى datatable](https://example.com/placeholder.png "مخطط تصدير excel إلى datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}