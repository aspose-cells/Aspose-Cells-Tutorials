---
category: general
date: 2026-10-26
description: خيارات ExportTableOptions المخصصة عند ExportAsStrin تتيح لك تصدير بيانات
  Excel كسلاسل نصية في C#. اتبع الدليل خطوة بخطوة لتكوين وتشغيل التصدير.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: ar
lastmod: 2026-10-26
og_description: خيارات ExportTable المخصصة عندما يتيح ExportAsStrin تصدير Excel بنص
  فقط. تعلّم الخطوات الدقيقة لتكوين وتشغيل التصدير في C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: خيارات تصدير الجدول المخصصة عند ExportAsString – تصدير Excel كسلسلة في C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: خيارات تصدير الجدول المخصصة عند ExportAsStrin لبرنامج Excel
url: /ar/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تخصيص ExportTableOptions عند ExportAsStrin – تصدير Excel كسلسلة نصية في C#

إذا كنت تحتاج إلى **Custom ExportTableOptions when ExportAsStrin** للحصول على قيمة كل خلية كنص عادي، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. سواءً كنت تبني خط أنابيب لاستيراد البيانات أو تحتاج إلى تفريغ جاهز لـ CSV، سترى لماذا يؤدي تكوين الخيارات بهذه الطريقة إلى تجنب مفاجآت تحويل الأنواع.

في هذا البرنامج التعليمي ستتعلم **how to export excel as string** باستخدام مكتبة Aspose.Cells، وسترى الشيفرة الكاملة القابلة للتنفيذ، وتفهم السبب وراء كل إعداد. لا حاجة إلى أي وثائق خارجية – كل ما تحتاجه موجود هنا.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET)  
* حزمة Aspose.Cells for .NET (تثبيت عبر NuGet: `Install-Package Aspose.Cells`)  
* ملف Excel (`sample.xlsx`) موجود في مجلد الجذر للمشروع  

هذه العناصر هي الاعتمادات الوحيدة؛ الشيفرة تعمل على Windows أو Linux أو macOS دون الحاجة إلى مكتبات إضافية.

## الخطوة 1: تحميل المصنف الذي تريد تصديره

أول شيء تقوم به عند استخدام **Custom ExportTableOptions when ExportAsStrin** هو الحصول على كائن `Worksheet` من مصنف تم تحميله. هذا الكائن يمنحك الوصول إلى الصفوف والأعمدة وواجهة برمجة تطبيقات التصدير.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*لماذا هذا مهم:*  
`Workbook` يقرأ الملف مرة واحدة ويحافظ على جميع معلومات التنسيق في الذاكرة. باختيار `Worksheet` محدد، تقوم بتحديد نطاق التصدير وتجنب معالجة غير ضرورية للأوراق المخفية.

## الخطوة 2: تكوين ExportTableOptions مع ExportAsString = true

جوهر **Custom ExportTableOptions when ExportAsStrin** هو كائن `ExportTableOptions`. ضبط `ExportAsString` يجبر المصدّر على معاملة كل خلية كنص، بغض النظر عن نوع البيانات الأصلي (تاريخ، رقم، منطقية، إلخ). تمكين `PreserveFormatting` يحافظ على النمط البصري (مثل رموز العملة) في النص الناتج.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*لماذا هذا مهم:*  
عند استدعاء `ExportDataTable` لاحقًا، تحاول المكتبة عادةً استنتاج نوع .NET لكل عمود. مع `ExportAsString = true`، يتم تخطي خطوة الاستنتاج هذه، مما يمنع التحويلات غير المتوقعة إلى `DateTime` أو `double` التي قد تتسبب في تعطل محللات CSV اللاحقة.

## الخطوة 3: تصدير نطاق إلى DataTable باستخدام الخيارات المخصصة

الآن يمكنك تصدير نطاق مستطيل (الصفوف 0‑9، الأعمدة 0‑4) من ورقة العمل. تُعيد الطريقة `DataTable` حيث كل حقل هو `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*لماذا هذا مهم:*  
`ExportDataTable` هي الطريقة الأكثر ملاءمة لنقل بيانات Excel إلى بنية علاقية many .NET APIs already understand (مثل Entity Framework، Dapper). بتمرير **Custom ExportTableOptions when ExportAsStrin**، تضمن أن كل `DataColumn.DataType` سيكون `typeof(string)`.

## الخطوة 4: التحقق من النتيجة – جميع القيم نصوص

من الممارسات الجيدة التأكد من أن عملية التصدير سارت كما هو متوقع. الحلقة التالية تطبع كل خلية ونوعها في وقت التشغيل.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**الناتج المتوقع**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

كل خلية تُظهر `String` كنوعها، مما يؤكد أن **Custom ExportTableOptions when ExportAsStrin** عملت بشكل صحيح.

## الخطوة 5: اختياري – كتابة DataTable إلى CSV

إذا كان هدفك النهائي هو ملف نصي عادي، يمكنك بسهولة تسلسل `DataTable` إلى CSV:



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة قابلة للتنفيذ مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [تصدير سلاسل HTML من Excel إلى DataTable باستخدام Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [تصدير الخصائص المخصصة Excel PDF Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java فلاتر التحميل المخصصة تصدير Excel](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}