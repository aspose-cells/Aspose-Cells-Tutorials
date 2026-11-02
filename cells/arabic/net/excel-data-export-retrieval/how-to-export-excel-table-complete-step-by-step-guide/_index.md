---
category: general
date: 2026-07-03
description: تعلم كيفية تصدير جدول Excel إلى ملف .txt وحفظ جدول Excel كملف .txt باستخدام
  C#. تصدير بيانات Excel كنص عادي مع مثال كامل للكود.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: ar
og_description: كيفية تصدير جدول Excel كنص عادي. يوضح لك هذا الدليل كيفية تصدير بيانات
  Excel كنص عادي وحفظ جدول Excel في ملف .txt باستخدام Aspose.Cells.
og_title: كيفية تصدير جدول إكسل – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: كيفية تصدير جدول إكسل – دليل كامل خطوة بخطوة
url: /ar/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير جدول Excel – دليل خطوة بخطوة كامل

هل تساءلت يومًا **كيف تصدر جدول Excel** دون سحب كامل المصنف إلى الذاكرة؟ لست الوحيد. في العديد من وظائف الأتمتة النظام المتلقي يقبل فقط ملف `.txt` بسيط، لذا تحتاج إلى **حفظ جدول Excel إلى ملف .txt** بسرعة وبشكل موثوق.  

في هذا الدرس سنستعرض حل C# نظيف ي **يصدر بيانات Excel كنص عادي** باستخدام Aspose.Cells. في النهاية ستحصل على برنامج جاهز للتنفيذ، وتفهم لماذا كل سطر مهم، وترى كيف تعدل عملية التصدير لتناسب حالاتك الخاصة.

## ما ستحتاجه

- **Aspose.Cells for .NET** (أي نسخة حديثة، مثل 23.12).  
- .NET 6 SDK أو أحدث – الكود يُترجم مع .NET Core أيضًا.  
- ملف `input.xlsx` تجريبي يحتوي على جدول Excel واحد على الأقل.  
- محرر نصوص أو بيئة تطوير (Visual Studio، VS Code، Rider… حسب اختيارك).

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells، ويمكن تشغيل كل ذلك على Windows أو Linux أو macOS.

## الخطوة 1: إعداد المشروع والاستيرادات

أولاً، أنشئ تطبيق console وأدرج المساحات الاسمية اللازمة.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **نصيحة احترافية:** إذا كنت تستخدم .NET CLI، نفّذ `dotnet new console -n ExcelTableExport` ثم `dotnet add package Aspose.Cells` قبل لصق الكود أعلاه.

## الخطوة 2: تحميل المصنف والحصول على الورقة الأولى

كائن workbook يمثل ملف Excel بالكامل. تحميله مرة واحدة يقلل من استهلاك الذاكرة.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

لماذا نختار الورقة الأولى؟ في العديد من التقارير المولدة تكون البيانات في الورقة الأولى، لكن يمكنك تغيير الفهرس أو استخدام `wb.Worksheets["SheetName"]` لورقة مسماة.

## الخطوة 3: استرجاع أول جدول معرف في الورقة

جداول Excel (ListObjects) توفر لنا بيانات منظمة، مما يجعل عملية التصدير متوقعة.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

إذا كان المصنف يحتوي على جداول متعددة، يمكنك ببساطة التكرار عبر `ws.Tables` أو الاختيار بواسطة `tbl.Name`.

## الخطوة 4: تكوين خيارات التصدير – تصدير كل خلية كسلسلة

تتيح لك Aspose.Cells التحكم في تنسيق كل خلية أثناء التصدير. ضبط `ExportAsString` يضمن تحويل الأرقام والتواريخ والصيغ إلى نص عادي.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### إضافة إجراء تصدير مخصص لإزالة المسافات الفارغة

غالبًا ما تحتوي البيانات المصدرية على مسافات بادئة أو لاحقة. إزالة هذه المسافات تجعل ملف `.txt` النهائي أنظف.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

تستقبل الدالة اللامبدا كائن `Cell` و`TextWriter`. يمكنك أيضًا إضافة منطق شرطي هنا—مثلاً استبدال الفواصل بفواصل منقوطة لإخراج بنمط CSV.

## الخطوة 5: تصدير الجدول بدءًا من الخلية A1 إلى ملف نصي

الآن نكتب الجدول فعليًا إلى القرص. طريقة `ExportTable` تتنقل عبر الجدول صفًا بصف، وتطبق الخيارات التي حددناها للتو.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**ما ستراه:** كل صف من جدول Excel يتحول إلى سطر في `Table.txt`. الأعمدة مفصولة بحرف تبويب (`\t`) افتراضيًا—مثالي للتحليل اللاحق.

### مثال على المخرجات المتوقعة

بافتراض أن `input.xlsx` يحتوي على جدول بثلاثة أعمدة (`ID`, `Name`, `Score`) وصفين من البيانات، سيظهر `Table.txt` كالتالي:

```
1    Alice    85
2    Bob      92
```

لاحظ أن المسافات تم إزالتها، وكل شيء نص عادي—تمامًا ما تتطلبه الحاجة إلى **export excel data as plain text**.

## معالجة الحالات الخاصة الشائعة

| الحالة | ما الذي يجب فعله | السبب |
|-----------|------------|-----|
| **الجدول يحتوي على خلايا فارغة** | الدالة اللامبدا تكتب `cell.StringValue.Trim()` التي تُرجع سلسلة فارغة للخلايا الفارغة. | يحافظ على محاذاة الأعمدة دون إضافة أحرف غير مرغوبة. |
| **تحتاج إلى فاصل مخصص** | استبدل `writer.Write(cell.StringValue.Trim());` بـ `writer.Write($"{cell.StringValue.Trim()},");` ثم احذف الفاصل الزائد في نهاية كل صف. | بعض الأنظمة تفضّل الفواصل أو الأنابيب بدلاً من علامات التبويب. |
| **أوراق عمل كبيرة ( > 100 k صف) ** | استخدم `ExportTableOptions` مع `ExportAsString = true` وقم ببث الملف كما هو موضح؛ Aspose.Cells يعالج الصفوف بطريقة تدفقية، مما يتجنب أخطاء نفاد الذاكرة. | يضمن القابلية للتوسع. |
| **جداول متعددة في ورقة واحدة** | قم بالتكرار عبر `ws.Tables` واستدعِ `ExportTable` لكل منها، ويمكن إضافة سطر فاصل بين عمليات التصدير إذا رغبت. | يتيح لك **save Excel table to .txt file** لكل جدول. |

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs`. استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي موجود على جهازك.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم الإعداد بشكل صحيح، سترى رسالة التأكيد وملف `Table.txt` الذي تم إنشاؤه حديثًا يحتوي على **export excel data as plain text**.

## إضافي: تأكيد بصري (اختياري)

إذا رغبت في رؤية لقطة سريعة للملف الناتج، يمكنك فتحه في أي محرر نصوص. أدناه صورة placeholder تُظهر التخطيط المتوقع.

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*نص بديل:* **how to export excel table** – يُظهر ناتج نصي لجدول Excel تم تصديره.

## ملخص وخطوات قادمة

لقد غطينا كل ما تحتاج معرفته حول **how to export Excel table** باستخدام Aspose.Cells، من تحميل المصنف إلى تقليم قيم الخلايا وأخيرًا كتابة ملف `.txt` نظيف.  

- الآن تفهم **save Excel table to .txt file** باستخدام منطق مخصص.  
- يمكنك تعديل الدالة اللامبدا للتعامل مع التواريخ أو الأرقام أو الفواصل المخصصة.  
- للمشاريع الأكبر، فكر في تغليف المنطق في طريقة أو فئة قابلة لإعادة الاستخدام.

**ما التالي؟** جرّب تصدير جداول متعددة، أو غيّر تنسيق الإخراج إلى CSV بتغيير الفاصل. يمكنك أيضًا استكشاف **export excel data as plain text** مباشرةً إلى تدفق شبكة للتكاملات الفورية.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}