---
category: general
date: 2026-08-11
description: تصدير إكسل إلى txt في C# مع دليل خطوة بخطوة. تعلم كيفية تحويل xlsx إلى
  نص عادي باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: ar
lastmod: 2026-08-11
og_description: تصدير Excel إلى txt في C# بسرعة. يوضح هذا الدليل كيفية تحويل ملفات
  xlsx إلى نص عادي، وتكوين الصيغ، ومعالجة أوراق العمل الكبيرة.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: تصدير إكسل إلى txt في C# – دليل خطوة بخطوة للمطورين
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: تصدير Excel إلى TXT في C# – دليل برمجة كامل
url: /ar/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى TXT في C# – دليل برمجة كامل

إذا كنت بحاجة إلى **تصدير Excel إلى TXT** يمكنك تحقيق النتيجة ببضع أسطر من كود C#. يوضح هذا الدليل كيفية تحويل مصنف `.xlsx` إلى ملف نصي عادي مع الحفاظ على تنسيق البيانات الذي تحدده.

تصدير أوراق العمل كملفات نصية هو طلب شائع عندما تقبل الأنظمة اللاحقة بيانات مفصولة فقط أو عندما تحتاج إلى تدقيق القيم الخام للخلايا. في الأقسام التالية ستتعلم كيفية تكوين تنسيقات التاريخ والرقم، التعامل مع الأوراق الكبيرة، وتجنب المشكلات الشائعة.

## المتطلبات المسبقة لتحويل XLSX إلى نص عادي

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6.0 (أو أحدث) مثبت – الكود يستهدف .NET Standard 2.0، لذا يعمل مع .NET Framework 4.6+ أيضاً.
* ترخيص لـ **Aspose.Cells** (التقييم المجاني يكفي للاختبار).
* بيئة تطوير متكاملة مثل Visual Studio 2022 أو Visual Studio Code.
* ملف Excel اسمه `input.xlsx` موجود في مجلد يمكنك الإشارة إليه من مشروعك.

هذه العناصر هي المتطلبات الخارجية الوحيدة؛ لا يعتمد الدرس على حزم NuGet إضافية.

## كيفية تصدير Excel إلى TXT باستخدام Aspose.Cells

توفر Aspose.Cells الفئة `ExportTableOptions` التي تسمح لك بالتحكم في كيفية تحويل قيم الخلايا إلى سلاسل نصية. بتعيين `ExportAsString` إلى `true` تجبر كل خلية على الكتابة كنص، وهو أمر أساسي عندما تريد مخرجات نصية حتمية.

### الخطوة 1 – تحميل المصنف

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*يقوم مُنشئ `Workbook` بقراءة ملف Excel إلى الذاكرة. إذا لم يكن الملف موجوداً، يتم إلقاء استثناء، لذا قد ترغب في وضع هذا الاستدعاء داخل كتلة try‑catch في الكود الإنتاجي.*

### الخطوة 2 – الحصول على أول ورقة عمل

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*الأوراق ذات فهرس يبدأ من الصفر، لذا الفهرس 0 يشير إلى أول تبويب. يمكنك استبدال الفهرس باسم الورقة (`workbook.Worksheets["Sheet1"]`) عندما تحتاج إلى استهداف تبويب محدد.*

### الخطوة 3 – تعريف خيارات التصدير للتحويل إلى نص

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` يضمن أن كل خلية، بغض النظر عن نوعها الأصلي، تصبح سلسلة نصية في ملف الإخراج. تسمح خصائص `DateTimeFormat` و `NumberFormat` بالتحكم في شكل تواريخ وأرقام، وهو أمر حاسم عندما **تحول XLSX إلى نص عادي** للأنظمة التي تتوقع نمطاً محدداً.*

### الخطوة 4 – تصدير ورقة العمل كملف نصي

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` يكتب محتوى ورقة العمل إلى ملف نصي عادي باستخدام الخيارات التي زودت بها. الفاصل الافتراضي هو حرف الجدولة (`\t`). إذا احتجت فاصلًا مختلفًا، يمكنك استخدام النسخة التي تقبل كائن `ExportTableOptions` وتحديد `ExportTableOptions.Separator`. يمكن فتح الملف الناتج بأي محرر نصوص أو استيراده إلى قاعدة بيانات.*

#### النتيجة المتوقعة

افترض أن `input.xlsx` يحتوي على:

| A            | B       | C            |
|--------------|---------|--------------|
| 2023‑05‑01   | 1234.5  | نص تجريبي   |

مع الخيارات أعلاه سيحتوي ملف `Exported.txt` على:

```
2023-05-01	1,234.50	Sample text
```

كل عمود مفصول بعلامة جدولة، والتواريخ تتبع الصيغة `yyyy‑MM‑dd`، والأرقام تستخدم الفاصلة كفاصل آلاف وتحتوي على منزلتين عشريتين.

## المشكلات الشائعة عند تصدير ورقة العمل كملف نصي

| المشكلة | لماذا يحدث | كيفية تجنبه |
|---------|------------|--------------|
| تنسيق الأرقام يعتمد على الإعدادات المحلية | الصيغة الافتراضية تحترم ثقافة نظام التشغيل، مما قد ينتج فواصل أو نقاط بشكل غير متسق. | عيّن `NumberFormat` صراحةً في `ExportTableOptions`. |
| ظهور الصفوف أو الأعمدة المخفية في الإخراج | Aspose.Cells تصدر النطاق المستخدم بالكامل، بما في ذلك الصفوف المخفية. | عيّن `ExportTableOptions.ExportHiddenRows = false` و `ExportHiddenColumns = false` إذا رغبت في تخطيها. |
| أوراق العمل الكبيرة تستهلك الذاكرة | يتم تحميل المصنف بالكامل في الذاكرة قبل التصدير. | استخدم `Workbook.LoadOptions` مع `LoadDataOnly = true` لتقليل استهلاك الذاكرة، أو عالج الملف على دفعات. |
| خلايا التاريخ مخزنة كنص في الملف الأصلي | إذا كانت الخلية تحتوي بالفعل على سلسلة منسقة، يتعامل المُصدر معها كنص ويتجاهل `DateTimeFormat`. | تأكد من أن المصنف الأصلي يخزن التواريخ كأنواع تاريخ Excel صحيحة. |

معالجة هذه القضايا تجعل عملية **كيفية تصدير ورقة عمل Excel كنص** موثوقة عبر بيئات مختلفة.

## توسيع الحل – فواصل مخصصة وتصدير تدفقي

إذا كنت بحاجة إلى ملف قيم مفصولة بفواصل (CSV) بدلاً من ملف مفصول بعلامة جدولة، عدل الخيارات:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

للملفات التي يزيد حجمها عن 500 ميغابايت، يمنع التصدير التدفقي استنزاف الذاكرة:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

النسخة التي تقبل `Stream` تكتب الصفوف تدريجياً، وهو مثالي للوظائف الدفعية أو خدمات الويب التي تُعيد الملف النصي مباشرةً إلى العميل.

## التحقق من النتيجة برمجياً

بعد انتهاء التصدير يمكنك قراءة السطر الأول مرة أخرى إلى الذاكرة لتأكيد التنسيق:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

تشغيل هذا المقتطف يجب أن يطبع نفس السطر المعروض في قسم *النتيجة المتوقعة*، مما يمنحك الثقة بأن التحويل نجح.

## ملخص الكود الكامل

جمع جميع الأجزاء معاً ينتج برنامجًا مستقلاً يمكنك نسخه إلى تطبيق Console:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

قم بتجميع البرنامج وتشغيله؛ سيظهر ملف `Exported.txt` في نفس الدليل الذي يحتوي على المصنف الأصلي.

## الخطوات التالية والمواضيع ذات الصلة

* **تصدير ورقة العمل كملف نصي** – جرّب فواصل مختلفة، ترميزات (UTF‑8 مقابل ASCII)، وأنماط إنهاء السطر لتوافق متعدد المنصات.
* **تحويل جماعي** – كرّر عبر `workbook.Worksheets` لإنشاء ملف نصي منفصل لكل تبويب.
* **التكامل مع قواعد البيانات** – مرّر النص المُولد مباشرةً إلى عملية إدخال جماعي لـ SQL Server أو PostgreSQL.
* 

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}