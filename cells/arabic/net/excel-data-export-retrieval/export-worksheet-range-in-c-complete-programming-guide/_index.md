---
category: general
date: 2026-05-04
description: تصدير نطاق ورقة العمل باستخدام C# مع تنسيق مخصص. تعلم كيفية تصدير نطاق
  إكسل وكيفية تخصيص تصدير الخلايا في بضع خطوات سهلة.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: ar
og_description: تصدير نطاق ورقة العمل باستخدام C#. يوضح هذا الدليل كيفية تصدير نطاق
  إكسل وتخصيص تصدير الخلايا بسرعة وموثوقية.
og_title: تصدير نطاق ورقة العمل في C# – دليل البرمجة الكامل
tags:
- C#
- Excel
- Data Export
title: تصدير نطاق ورقة العمل في C# – دليل برمجي شامل
url: /ar/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير نطاق ورقة العمل في C# – دليل برمجة كامل

هل احتجت يومًا إلى **تصدير نطاق ورقة العمل** لكن الناتج الافتراضي لم يكن كما تريد؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون استخراج مجموعة من الخلايا إلى ملف CSV أو JSON. الخبر السار؟ ببضع أسطر من C# يمكنك ليس فقط **تصدير نطاق إكسل** بل أيضًا **تخصيص تصدير الخلايا** ليتطابق مع أي تنسيق لاحق.

في هذا الدرس سنستعرض سيناريو واقعي: أخذ الخلايا *A1:D10* من مصنف إكسل، تحويل كل قيمة إلى سلسلة محاطة بأقواس، وكتابة النتيجة إلى ملف. بنهاية الدرس ستعرف بالضبط **كيفية تصدير نطاق ورقة العمل** مع تحكم كامل في تمثيل كل خلية، بالإضافة إلى مجموعة من النصائح للحالات الخاصة التي قد تواجهها لاحقًا.

## ما ستحتاجه

- .NET 6 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)  
- حزمة NuGet **GemBox.Spreadsheet** (أو أي مكتبة توفر `ExportTableOptions`؛ الـ API المعروض من GemBox)  
- فهم أساسي لصياغة C# – لا شيء معقد، مجرد عبارات `using` العادية وإنشاء الكائنات  

إذا كان لديك هذه المتطلبات، فأنت جاهز للبدء.

## الخطوة 1: إعداد خيارات التصدير – نقطة التحكم الأساسية  

أول ما تفعله هو إنشاء كائن `ExportTableOptions` وإخبارها بمعاملة كل خلية كسلسلة نصية. هذا هو الأساس لـ **كيفية تصدير نطاق إكسل** مع الحفاظ على نوع البيانات ثابتًا.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*لماذا نجبر التصدير كسلسلة نصية؟*  
عندما تقوم لاحقًا بتخصيص كل خلية، ستضيف أقواس وربما رموز أخرى. الحفاظ على كل شيء كسلسلة يمنع مفاجآت تحويل النوع (مثل تحويل التواريخ إلى أرقام تسلسلية).

## الخطوة 2: ربط حدث CellExport – تخصيص كل خلية  

الآن يأتي الجزء الممتع: **كيفية تخصيص تصدير الخلية**. تقوم GemBox بإطلاق حدث `CellExport` لكل خلية على وشك الكتابة. من خلال معالجته يمكنك إحاطة القيمة بأقواس، إضافة بادئة، أو حتى تخطي خلية بالكامل.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*نصيحة احترافية:* إذا كنت تريد تعديل الخلايا الرقمية فقط، تحقق من `e.Value.GetType()` قبل إضافة الأقواس. هذه الحراسة الصغيرة قد تنقذك من تعديل نص العناوين عن غير قصد.

## الخطوة 3: تصدير النطاق المطلوب – الإجراء الأساسي  

بعد إعداد الخيارات، تستدعي `ExportTable`. تأخذ الطريقة المصنف الذي حمّلته، عنوان النطاق الذي تريد، والخيارات التي ضبطتها للتو.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

التحميل الزائد الذي استخدمناه يكتب مباشرة إلى ملف (CSV بشكل افتراضي). إذا كنت تفضّل الحصول على سلسلة في الذاكرة، استبدل الوسيط الأخير بـ `StringWriter` وقرأ النتيجة بعد ذلك.

### مثال كامل يعمل

فيما يلي تطبيق console مكتمل يمكنك لصقه في مشروع جديد وتشغيله فورًا (فقط استبدل مسارات الملفات).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**الناتج المتوقع (مقتطف CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

كل خلية من *A1* إلى *D10* الآن محاطة بأقواس مربعة، تمامًا كما عرّفنا في معالج `CellExport`.

## معالجة الحالات الشائعة  

### 1. الخلايا الفارغة  
إذا كانت الخلية فارغة، سيكون `e.Value` مساويًا لـ `null`. محاولة تنسيقها باستخدام الاستبدال النصي ستؤدي إلى استثناء. احمِ نفسك من ذلك:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. النطاقات الكبيرة  
تصدير ملايين الصفوف قد يستهلك الذاكرة. في هذه الحالة، قم ببث الناتج بدلاً من تحميل المصنف بالكامل في الذاكرة:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. الفواصل المختلفة  
CSV ليس التنسيق الوحيد الذي قد تحتاجه. غيّر الفاصل بضبط `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## الأسئلة المتكررة  

**س: هل يعمل هذا مع ملفات .xlsx التي أنشأتها Excel 365؟**  
بالطبع. GemBox تقرأ صيغة OpenXML الحديثة دون أي إعداد إضافي.

**س: هل يمكنني تصدير عدة نطاقات غير متصلة في آن واحد؟**  
ليس مباشرة عبر استدعاء `ExportTable` واحد. قم بالتكرار على كل سلسلة نطاق (`"A1:D10"`، `"F1:H5"` إلخ) وادمج النتائج بنفسك.

**س: ماذا لو احتجت لتطبيق تنسيق مختلف لكل عمود؟**  
داخل معالج `CellExport` لديك الوصول إلى `e.ColumnIndex`. استخدم عبارة `switch` لتطبيق منطق خاص بالعمود.

## الخلاصة  

غطّينا **كيفية تصدير نطاق ورقة العمل** مع تحكم كامل في مظهر كل خلية، وأظهرنا **كيفية تصدير نطاق إكسل** باستخدام `ExportTableOptions`، ووضحنا **كيفية تخصيص تصدير الخلية** عبر حدث `CellExport`. الحل الكامل يقتصر على بضعة عشرات سطرًا من C#، لكنه مرن بما يكفي للسيناريوهات الإنتاجية.

ما الخطوة التالية؟ جرّب استبدال تغليف الأقواس بتنسيق صديق لـ JSON، أو جرب منطقًا شرطيًا يتخطى الصفوف المخفية. يمكنك أيضًا استكشاف التصدير مباشرة إلى `MemoryStream` لاستجابات الويب‑API—دون الحاجة إلى ملفات مؤقتة.

إذا تابعت معنا، فأنت الآن تملك نمطًا قويًا وقابلًا لإعادة الاستخدام لتصدير أي نطاق ورقة عمل بالطريقة التي تحتاجها. Happy coding، ولا تتردد في ترك تعليق إذا واجهت أي صعوبة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}