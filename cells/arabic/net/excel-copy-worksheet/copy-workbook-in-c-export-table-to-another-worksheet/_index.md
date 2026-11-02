---
category: general
date: 2026-06-21
description: نسخ دفتر العمل في C# وتصدير الجدول إلى ورقة عمل أخرى باستخدام Aspose.Cells.
  اتبع هذا الدليل خطوة بخطوة للحصول على حل نظيف وقابل لإعادة الاستخدام.
draft: false
keywords:
- copy workbook in c#
- export table to another worksheet
language: ar
og_description: نسخ دفتر العمل في C# وتصدير الجدول إلى ورقة عمل أخرى مع مثال كامل
  قابل للتنفيذ. تعرّف على سبب فاعلية هذا النهج.
og_title: نسخ دفتر العمل في C# – تصدير الجدول إلى ورقة عمل أخرى
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  headline: Copy Workbook in C# – Export Table to Another Worksheet
  type: TechArticle
- description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  name: Copy Workbook in C# – Export Table to Another Worksheet
  steps:
  - name: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
    text: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
  - name: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
    text: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
  - name: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
    text: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
  type: HowTo
tags:
- csharp
- aspose.cells
- excel automation
title: نسخ دفتر العمل في C# – تصدير الجدول إلى ورقة عمل أخرى
url: /ar/net/excel-copy-worksheet/copy-workbook-in-c-export-table-to-another-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ دفتر العمل في C# – تصدير جدول إلى ورقة عمل أخرى

هل تساءلت يومًا كيف **copy workbook in C#** مع أيضًا نقل نطاق محدد من البيانات إلى ورقة جديدة؟ لست وحدك. يواجه العديد من المطورين هذه المشكلة عند أتمتة التقارير، الفواتير، أو ترحيل البيانات. الخبر السار؟ باستخدام بضع أسطر من كود Aspose.Cells يمكنك كل من تكرار دفتر العمل و **export table to another worksheet** في تدفق عمل واحد ومنظم.

في هذا الدرس سنستعرض العملية بالكامل — من تحميل ملف المصدر، استنساخه، وتصدير نطاق كسلسلة نصية، إلى لصق تلك السلسلة في ورقة الوجهة. بنهاية الدرس ستحصل على مقطع شفرة مستقل وجاهز للإنتاج يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- **Aspose.Cells for .NET** (الإصدار 23.12 أو أحدث). إنها مكتبة قوية تتعامل مع ملفات Excel دون الحاجة إلى تثبيت Office.
- بيئة تطوير .NET (Visual Studio، Rider، أو VS Code مع إضافة C#).
- دفتر عمل تجريبي اسمه `Formatted.xlsx` موجود في دليل معروف (سنشير إليه كـ `YOUR_DIRECTORY/Formatted.xlsx`).

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells، ويعمل الكود على .NET 6+، .NET Framework 4.7+، أو .NET Core.

## تنفيذ خطوة بخطوة

فيما يلي البرنامج الكامل القابل للتنفيذ. لا تتردد في نسخه‑ولصقه في مشروع تطبيق كونسول واضغط **F5**.

```csharp
using System;
using Aspose.Cells;

namespace WorkbookCopyExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load the source workbook
            // -------------------------------------------------
            // Adjust the path to point at your actual file location.
            string sourcePath = @"YOUR_DIRECTORY/Formatted.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            Console.WriteLine("Source workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Set up export options – we want the range as a string
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true   // This forces the export to return CSV‑style text.
            };
            Console.WriteLine("Export options configured (ExportAsString = true).");

            // -------------------------------------------------
            // Step 3: Copy workbook in C# – creates an isolated clone
            // -------------------------------------------------
            // Using the Copy method ensures the original stays untouched.
            Workbook destinationWorkbook = sourceWorkbook.Copy();
            Console.WriteLine("Destination workbook created as a copy of the source.");

            // -------------------------------------------------
            // Step 4: Export the specified range (B2:B10) from the source sheet
            // -------------------------------------------------
            // The range is taken from the first worksheet (index 0).
            // ExportTable returns a string that can be written directly.
            string exportedTable = sourceWorkbook.Worksheets[0]
                .Cells.ExportTable(sourceWorkbook.Worksheets[0].Cells["B2:B10"],
                                   exportOptions);
            Console.WriteLine("Range B2:B10 exported as string:");
            Console.WriteLine(exportedTable);

            // -------------------------------------------------
            // Step 5: Paste the exported string into the destination sheet
            // -------------------------------------------------
            // We start at cell A1 of the first worksheet in the destination.
            destinationWorkbook.Worksheets[0].Cells["A1"]
                .PutValue(exportedTable);
            Console.WriteLine("Exported data placed at A1 in the destination workbook.");

            // -------------------------------------------------
            // Step 6: Save the result so you can verify it
            // -------------------------------------------------
            string resultPath = @"YOUR_DIRECTORY/Copy_With_ExportedTable.xlsx";
            destinationWorkbook.Save(resultPath);
            Console.WriteLine($"Result saved to {resultPath}");
        }
    }
}
```

### لماذا يعمل هذا النهج

1. **`Workbook.Copy()`** يقوم بإنشاء نسخة عميقة من كل ورقة عمل، نمط، وصيغة. إنها الطريقة الأنظف لـ **copy workbook in C#** دون الحاجة إلى التكرار اليدوي عبر الأوراق.  
2. **`ExportTableOptions.ExportAsString = true`** يخبر Aspose.Cells أن يعطينا سلسلة بنمط CSV بدلاً من كتلة ثنائية. هذا يجعل من السهل إدراج البيانات في أي خلية باستخدام `PutValue`.  
3. من خلال التصدير من **source workbook** وإدراجه في **destination workbook**، نحافظ على استقلالية الملفين تمامًا—دون تلوث غير مقصود للمرجعيات.

## الحالات الخاصة والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الإصلاح / التوصية |
|-----------|-------------------|-----------------------|
| **Different worksheet indexes** | إذا كان دفتر العمل المصدر أو الوجهة يحتوي على عدة أوراق، قد يؤدي الترميز الصلب للفهارس `0` إلى استهداف الورقة الخاطئة. | استخدم `Worksheets["SheetName"]` أو قم بالتكرار عبر `Worksheets` لتحديد الورقة المطلوبة. |
| **Large ranges** | تصدير نطاق ضخم كسلسلة قد يتجاوز حدود الذاكرة. | فكر في التصدير على دفعات أو استخدم `ExportTable` مع `ExportAsString = false` وتعامل مع التدفقات الثنائية. |
| **Formatting loss** | `ExportAsString` يزيل جميع التنسيقات؛ تُحفظ القيم الخام فقط. | إذا كنت تحتاج إلى الأنماط، صدّر كـ `IEnumerable<CellArea>` وانسخ الخلايا بشكل فردي. |
| **File path issues** | قد تتعطل المسارات النسبية عندما يعمل التطبيق من دليل عمل مختلف. | استخدم `Path.Combine(Environment.CurrentDirectory, "Formatted.xlsx")` أو خزن المسارات في الإعدادات. |

### نصيحة احترافية

إذا كنت تخطط لإعادة استخدام البيانات المصدرة عبر عدة دفاتر عمل، قم بلف منطق التصدير‑واللصق في طريقة مساعدة:

```csharp
static void ExportRangeToWorkbook(Workbook src, string range, Workbook dest, string destCell)
{
    var opts = new ExportTableOptions { ExportAsString = true };
    string data = src.Worksheets[0].Cells.ExportTable(src.Worksheets[0].Cells[range], opts);
    dest.Worksheets[0].Cells[destCell].PutValue(data);
}
```

الآن يمكنك استدعاء `ExportRangeToWorkbook(sourceWorkbook, "B2:B10", destinationWorkbook, "A1");` أينما احتجت.

## التحقق من النتيجة

افتح `Copy_With_ExportedTable.xlsx` في Excel أو أي عارض جداول:

- يجب أن تكون ورقة العمل الأولى مطابقة تمامًا لـ `Formatted.xlsx` **باستثناء** كتلة البيانات الجديدة التي تبدأ من **A1**.  
- الخلايا من A1 إلى A9 (أو عدد الصفوف التي يغطيها النطاق B2:B10) ستحتوي على القيم المصدرة، كل منها مفصول بالفاصل الافتراضي (الفاصلة للـ CSV). إذا كنت تحتاج إلى فاصل مختلف، اضبط `exportOptions.Separator` قبل التصدير.

هذا الفحص البصري يؤكد نجاح كل من عملية **copy workbook in C#** و **export table to another worksheet**.

## الخلاصة

لقد عرضنا للتو نمطًا نظيفًا وقابلًا للتكرار لـ **copy workbook in C#** مع تصدير جدول إلى ورقة عمل أخرى في آنٍ واحد. النقاط الرئيسية هي:

- استخدم `Workbook.Copy()` للحصول على نسخة آمنة وعميقة.  
- استفد من `ExportTableOptions.ExportAsString` لتحويل نطاق إلى سلسلة قابلة للنقل.  
- أدخل السلسلة أينما احتجت باستخدام `PutValue`.

من هنا قد ترغب في استكشاف:

- تصدير نطاقات متعددة غير متصلة.  
- تحويل السلسلة إلى مصفوفة ثنائية الأبعاد لمزيد من معالجة البيانات.  
- أتمتة العملية عبر مجلد من دفاتر العمل (معالجة دفعات).

جرّبه، عدّل النطاق، وشاهد كيف تُبسّط هذه التقنية خطوط أتمتة Excel الخاصة بك. إذا واجهت أي مشاكل أو كان لديك أفكار لتوسعات، لا تتردد في ترك تعليق أدناه. برمجة سعيدة!

![Copy workbook in C# example diagram](https://example.com/images/copy-workbook-diagram.png "Copy workbook in C# example showing source, export, and destination steps")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [نسخ ورقة عمل من دفتر عمل إلى آخر باستخدام Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [نسخ الأوراق داخل دفتر العمل باستخدام Aspose.Cells for .NET - دليل خطوة بخطوة](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [نسخ البيانات داخل دفتر العمل باستخدام Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-data-within-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}