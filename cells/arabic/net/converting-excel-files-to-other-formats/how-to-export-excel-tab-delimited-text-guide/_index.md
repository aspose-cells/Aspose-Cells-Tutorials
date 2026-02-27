---
category: general
date: 2026-02-26
description: كيفية تصدير إكسل إلى ملف نصي مفصول بعلامات تبويب باستخدام C#. تعلم تصدير
  إكسل كعلامة تبويب، تحويل إكسل إلى نص، وتصدير إكسل باستخدام الفاصل في ثلاث خطوات
  سهلة.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: ar
og_description: كيفية تصدير Excel إلى ملف نصي مفصول بعلامات جدولة باستخدام C#. يوضح
  هذا الدرس كيفية تصدير Excel كجدولة، تحويل Excel إلى txt، وتصدير Excel مع الفاصل.
og_title: كيفية تصدير إكسل – دليل النص المفصول بعلامة التبويب
tags:
- csharp
- excel
- file-conversion
title: كيفية تصدير إكسل – دليل النص المفصول بعلامة التبويب
url: /ar/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير إكسل – دليل C# الكامل

هل تساءلت يومًا **كيفية تصدير إكسل** إلى ملف نصي عادي دون فقدان التنسيق؟ ربما تحتاج إلى TSV (قيم مفصولة بعلامات جدولة) سريع لتدفق بيانات، أو أنك تزود نظامًا قديمًا لا يقرأ سوى `.txt`. في كلتا الحالتين، لست وحدك—المطورون يواجهون هذه المشكلة باستمرار عند نقل البيانات من الجداول.

الخبر السار؟ في ثلاث خطوات بسيطة يمكنك **تصدير إكسل كـ** نص مفصول بـ **tab**، **تحويل إكسل إلى txt**، وحتى اختيار فاصل مخصص إذا غيرت رأيك لاحقًا. أدناه ستجد مثالًا كاملًا قابلًا للتنفيذ بلغة C#، شرحًا لكل سطر، وبعض النصائح لتجنب المشكلات الشائعة.

> **نصيحة احترافية:** هذه الطريقة تعمل مع مكتبة Aspose.Cells الشهيرة، لكن المفاهيم تنطبق على أي واجهة برمجة تطبيقات .NET للـ Excel توفر طريقة من نوع `ExportTable`.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). الكود يُجمّع على أي بيئة تشغيل حديثة.
- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو مرخصة). تثبيت عبر NuGet: `dotnet add package Aspose.Cells`.
- مصنف إدخال يُدعى `input.xlsx` موجود في مجلد يمكنك التحكم فيه.
- قليل من الفضول—لا حاجة لمعرفة داخلية عميقة للـ Excel.

إذا كان لديك كل ذلك، لنبدأ مباشرةً في الحل.

## الخطوة 1 – تحميل المصنف الذي تريد تصديره

أولًا ننشئ كائن `Workbook` يشير إلى ملف المصدر. هذا الكائن يمثل ملف Excel بالكامل، بما في ذلك جميع الأوراق، النطاقات المسماة، والتنسيقات.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*لماذا هذا مهم:*  
تحميل المصنف يمنحك الوصول إلى مجموعة الأوراق (`workbook.Worksheets`). بدون هذا الكائن لا يمكنك الوصول إلى الخلايا أو النطاقات أو إعدادات التصدير.

> **ملاحظة:** إذا كان ملفك موجودًا على مشاركة شبكة، أضف `\\` أو استخدم مسار UNC—Aspose.Cells يتعامل معه بسهولة.

## الخطوة 2 – ضبط خيارات التصدير (قيمة نصية & فاصل Tab)

الآن نخبر المكتبة كيف نريد كتابة البيانات. بتعيين `ExportAsString = true` نجبر كل خلية على أن تُعامل كنص عادي، مما يلغي تنسيقات الأرقام الخاصة باللغات. الجزء `Delimiter = "\t"` هو جوهر **تصدير إكسل كـ tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*لماذا هذا مهم:*  
إذا تخطيت `ExportAsString`، قد تتحول الخلية التي تحتوي `12345` إلى `12,345` في بعض اللغات، مما يكسّر المحللات اللاحقة. يمكن استبدال الفاصل بفواصل، أنابيب، أو أي حرف آخر إذا قررت لاحقًا **تصدير إكسل بفاصل** غير الـ tab.

## الخطوة 3 – تصدير نطاق محدد إلى ملف نصي

أخيرًا، نختار النطاق الذي نهتم به (`A1:D10` في هذا المثال) ونكتب النتيجة إلى `out.txt`. الطريقة `ExportTable` تقوم بكل العمل الشاق: تقرأ الخلايا، تطبق الخيارات، وتدفق النتيجة إلى القرص.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

بعد تشغيل هذا، ستجد `out.txt` يحتوي على محتوى يشبه:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

كل عمود مفصول بـ **tab**، مما يجعله جاهزًا لـ `awk`، `PowerShell`، أو أي أداة متوافقة مع CSV تحترم الفواصل.

### التحقق السريع

افتح الملف المُولد في محرر نصوص عادي (Notepad، VS Code) وتأكد من:

1. أن الأعمدة مصطفة عندما تُفعّل “إظهار المسافات البيضاء”.
2. عدم ظهور علامات اقتباس أو فواصل إضافية.
3. أن جميع الخلايا الرقمية تظهر بالضبط كما في Excel (بفضل `ExportAsString`).

إذا لاحظت أي شيء غير صحيح، تحقق من أن المصنف الأصلي لا يخفي صفوفًا/أعمدة، وتأكد من أنك أشرت إلى فهرس الورقة الصحيح.

## تنوعات شائعة وحالات حافة

### تصدير ورقة عمل كاملة

إذا أردت **تصدير نطاق إكسل** يغطي الورقة بأكملها، يمكنك استخدام `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### استخدام فاصل مختلف

التبديل من tab إلى أنبوب (`|`) سهل كغيّر سطر واحد:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

هذا يلبي سيناريو **تصدير إكسل بفاصل** دون تعديل أي كود آخر.

### التعامل مع ملفات ضخمة (> 100 ميغابايت)

للمصنفات الكبيرة، قم بتدفق التصدير لتجنب تحميل كل شيء في الذاكرة:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### تحويل عدة أوراق في تمريرة واحدة

إذا كنت بحاجة إلى **تحويل إكسل إلى txt** لعدة أوراق، قم بالتكرار عليها:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

كل ورقة تحصل على ملف TSV خاص بها—مفيد للمهام الدفعية.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل، جاهزًا للترجمة. فقط استبدل مسارات الملفات بما يناسبك.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**الناتج المتوقع:** ملف اسمه `out.txt` حيث كل عمود مفصول بحرف tab، وتظهر قيمة كل خلية تمامًا كما هي في Excel.

## الأسئلة الشائعة

- **هل يعمل هذا مع ملفات .xls؟**  
  نعم. Aspose.Cells يكتشف الصيغة تلقائيًا، لذا يمكنك توجيه `Workbook` إلى ملف `.xls` قديم وتطبيق نفس الكود.

- **ماذا لو احتوت بياناتي على علامات tab؟**  
  ستُحافظ علامات tab داخل الخلية، ما قد يكسر محللات TSV. في هذه الحالة، فكر في التحويل إلى فاصل أنبوب (`|`) عبر تعديل `exportOptions.Delimiter`.

- **هل يمكنني تصدير الصيغ بدل القيم؟**  
  عيّن `exportOptions.ExportAsString = false` واستخدم نسخة `ExportTableOptions` التي تشمل `ExportFormula = true`. سيحتوي الناتج على نص الصيغة الأصلي.

- **هل هناك طريقة لتخطي الصفوف المخفية؟**  
  نعم. عيّن `exportOptions.ExportHiddenRows = false` (القيمة الافتراضية `true`). الصفوف المخفية ستُستبعد من الملف النصي النهائي.

## الخلاصة

أصبح لديك الآن وصفة جاهزة للإنتاج **كيفية تصدير إكسل** كملف نصي مفصول بـ tab، وكيفية **تصدير إكسل كـ tab**، وكيفية **تحويل إكسل إلى txt** مع تحكم كامل في الفواصل واختيار النطاق. باستخدام طريقة `ExportTable` في Aspose.Cells تتجنب بناء CSV يدويًا، تحافظ على دقة البيانات، وتبقي قاعدة الشيفرة نظيفة.

مستعد للتحدي التالي؟ جرّب:

- التصدير مباشرة إلى `MemoryStream` لواجهات برمجة التطبيقات الويب.  
- إضافة صف رأس ديناميكي بناءً على محتوى الصف الأول.  
- دمج هذه العملية في Azure Function تراقب حاوية تخزين لملفات Excel جديدة.

جرّبه، عدّل الفاصل، ودع البيانات تتدفق إلى أي مكان تحتاجه. برمجة سعيدة!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}