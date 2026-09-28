---
category: general
date: 2026-03-22
description: كيفية تصدير ملف Excel مع الحفاظ على التنسيق وتنسيق الأرقام. تعلم تحويل
  نطاق Excel، الحصول على نتيجة الصيغة، وتصدير Excel مع التنسيق باستخدام Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: ar
og_description: كيفية تصدير Excel مع التنسيق والحفاظ على تنسيق الأرقام. دليل خطوة
  بخطوة لتحويل نطاق Excel، الحصول على نتيجة الصيغة، وتصدير Excel مع التنسيق في C#.
og_title: كيفية تصدير إكسل مع التنسيق – الحفاظ على تنسيق الأرقام
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية تصدير Excel مع التنسيق – الحفاظ على تنسيق الأرقام
url: /ar/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel مع التنسيق – الحفاظ على تنسيق الأرقام

هل تساءلت يوماً **كيف تصدر Excel** مع الحفاظ على مظهر كل خلية تماماً كما تراه في المصنف؟ ربما تحتاج إلى إرسال تقرير إلى عميل، أو تغذية عنصر شبكة، أو مجرد تخزين القيم في قاعدة بيانات. المشكلة الشائعة هي فقدان تنسيق الأرقام أو تحول الصيغ إلى سلاسل نصية عادية.  

في هذا الدرس سنستعرض مثالاً كاملاً وجاهزاً للتنفيذ بلغة C# **يحافظ على تنسيق الأرقام**، **يحوّل نطاق Excel** إلى `DataTable`، **يحصل على نتيجة الصيغة**، وأخيراً **يصدر Excel مع التنسيق** باستخدام Aspose.Cells. في النهاية ستحصل على طريقة واحدة يمكنك إدراجها في أي مشروع واستدعاؤها بمرجع ورقة العمل.

> **معاينة سريعة:** ينشئ الكود مصنفاً، يكتب قيمة وصيغة، يطلب من Aspose.Cells تصدير الخلايا كسلاسل منسقة، ويطبع `123.456 | 246.912` – تماماً ما تتوقع رؤيته في Excel.

---

## ما ستحتاجه

- **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يكفي للتعلم)
- .NET 6.0 أو أحدث (واجهة برمجة التطبيقات هي نفسها على .NET Framework)
- بيئة تطوير C# أساسية (Visual Studio، VS Code، Rider… اختر ما يناسبك)

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells. إذا لم تقم بتثبيتها بعد، نفّذ:

```bash
dotnet add package Aspose.Cells
```

---

## الخطوة 1 – إنشاء مصنف وكتابة القيم (بما في ذلك صيغة)

أولاً نقوم بإنشاء مصنف جديد ونضع قيمة رقمية في **A1**. ثم نضيف صيغة بسيطة في **B1** تضرب الخلية الأولى في اثنين. هذا يهيئ المشهد لتوضيح **الحصول على نتيجة الصيغة** لاحقاً.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**لماذا هذا مهم:**  
- `PutValue` يخزن الرقم الأصلي، بينما `PutFormula` يخزن العملية الحسابية.  
- Aspose.Cells يبقي الصيغة **نشطة**، لذا عندما نطلب قيمة الخلية لاحقاً ستحصل فعلياً على `246.912`، وليس النص `"=A1*2"`.

---

## الخطوة 2 – إخبار Aspose.Cells بتصدير القيم كسلاسل منسقة

إذا استدعيت `ExportDataTable` بالإعدادات الافتراضية، ستُرجع الخلايا الرقمية قيمها الأساسية من نوع `double`. هذا يزيل أي فواصل آلاف، أو رموز عملة، أو أعداد عشرية مخصصة قد تكون ضبطتها. تسمح لنا فئة `ExportTableOptions` **بالحفاظ على تنسيق الأرقام** و**تصديرها كسلسلة**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**النقطة الأساسية:** `ExportNumberFormat = true` هو المفتاح الذي يجعل **الحفاظ على تنسيق الأرقام** يعمل. بدون هذا الإعداد سترى `"123.456"` و `"246.912"` كأرقام خام، قد تبدو صحيحة في الشيفرة لكن ليست كذلك عندما تلصق البيانات في واجهة تتوقع نفس تنسيق Excel.

---

## الخطوة 3 – طباعة البيانات المصدرة (التحقق)

الآن بعد أن حصلنا على `DataTable` مليء بسلاسل منسقة، لنقم بطباعة محتوياته إلى وحدة التحكم. هذا يوضح أيضاً أننا نجحنا في **الحصول على نتيجة الصيغة** دون الحاجة لتقييم الصيغة يدوياً.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

تشغيل البرنامج يطبع:

```
123.456 | 246.912
```

لاحظ كيف أن العمود الثاني يعرض **نتيجة الصيغة**، وليس نص الصيغة. هذا بالضبط ما تحتاجه عندما **تصدّر Excel مع التنسيق** للمعالجة اللاحقة.

---

## الخطوة 4 – تحويل نطاقات Excel أكبر (اختياري)

المثال أعلاه يتعامل مع شريحة صغيرة `A1:B1`، لكن السيناريوهات الواقعية غالباً ما تتطلب تصدير جداول كاملة. الطريقة نفسها تعمل لأي كتلة مستطيلة – فقط عدّل قيم `firstRow`، `firstColumn`، `totalRows`، و `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**نصيحة احترافية:** إذا كان ورقك يحتوي بالفعل على صف عنوان، اضبط `includeColumnNames` إلى `true`. سيستخدم Aspose.Cells الصف الأول من النطاق كأسماء أعمدة، وهو مفيد عندما تربط الـ `DataTable` بشبكة واجهة المستخدم لاحقاً.

---

## الخطوة 5 – المشكلات الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **الأرقام تفقد الفواصل أو رموز العملة** | `ExportAsString` = `false` أو تم إغفال `ExportNumberFormat` | اضبط كلا الخيارين `ExportAsString = true` **و** `ExportNumberFormat = true`. |
| **خلايا الصيغ تُعيد نص الصيغة** | لم تقم باستدعاء `CalculateFormula` قبل التصدير (مطلوب فقط إذا لم يكن المصنف مضبوطاً على الحساب التلقائي) | إما فعّل الحساب التلقائي (`workbook.CalculateFormula()`) أو اعتمد على `ExportAsString` الذي يجبر التقييم. |
| **العناوين تظهر كصفوف بيانات** | `includeColumnNames` = `false` بينما النطاق يحتوي على صف عنوان | اضبط `includeColumnNames = true` لتعامل الصف الأول كأسماء أعمدة. |
| **النطاقات الكبيرة تسبب ضغطاً على الذاكرة** | تصدير الورقة بالكامل مرة واحدة يحمل كل شيء في الذاكرة | صدّر على دفعات (مثلاً 500 صف في كل مرة) وادمج الـ `DataTable`s إذا لزم الأمر. |

---

## الخطوة 6 – مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج بالكامل، من عبارات `using` إلى `Main`. الصقه في تطبيق Console واضغط **F5** – ستظهر النتيجة المنسقة فوراً.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**الناتج المتوقع**

```
123.456 | 246.912

Press any key to exit...
```

هذا هو سير عمل **كيفية تصدير Excel** بالكامل، مع الحفاظ على التنسيق، وتقييم نتائج الصيغ، و`DataTable` نظيفة جاهزة لأي مستهلك .NET.

---

## الخلاصة

غطّينا كل ما تحتاج معرفته حول **كيفية تصدير Excel** مع **الحفاظ على تنسيق الأرقام**، **تحويل نطاق Excel** إلى `DataTable`، و**الحصول على نتائج الصيغ** دون أي تحليل إضافي. المفتاح هو تكوين `ExportTableOptions` – بمجرد ضبط `ExportAsString` و `ExportNumberFormat` إلى `true`، سيتولى Aspose.Cells كل العمل الشاق.

من هنا يمكنك:

- ربط الـ `DataTable` بـ WPF `DataGrid` أو عرض ASP.NET MVC.  
- كتابة الجدول إلى ملف CSV مع الحفاظ على التمثيل البصري الدقيق.  
- توسيع النهج إلى عدة أوراق أو نطاقات ديناميكية.

لا تتردد في تجربة تنسيقات مختلفة (عملة، نسب مئوية) ومجموعات بيانات أكبر. إذا صادفت أي شذوذ، ارجع إلى جدول **المشكلات الشائعة** – فهو يغطي أكثر العقبات التي قد تواجهك عند **تصدير Excel مع التنسيق**.

برمجة سعيدة، ولتظل جداولك المصدرة دائماً متقنة كما الأصلية!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}