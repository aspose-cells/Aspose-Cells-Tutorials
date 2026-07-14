---
category: general
date: 2026-07-13
description: كيفية تصدير نطاق الخلايا كجدول باستخدام C# و ExportTableOptions. تعلم
  إعداد المصنف خطوة بخطوة، التنسيق، وتصدير الجدول.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: ar
lastmod: 2026-07-13
og_description: كيفية تصدير نطاق الخلايا كجدول في C# باستخدام ExportTableOptions.
  اتبع هذا الدليل لتنسيق الخلايا، وإنشاء دفتر عمل، وتصدير جدول بسهولة.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: كيفية تصدير نطاق الخلايا كجدول – دليل كامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: كيفية تصدير نطاق الخلايا كجدول – دليل C# الكامل
url: /ar/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير نطاق الخلايا كجدول – دليل C# كامل

هل تساءلت يومًا **كيف تصدر نطاق الخلايا كجدول** دون أن تتعب نفسك بسبب مشاكل التنسيق؟ لست وحدك. سواءً كنت تغذي البيانات إلى خط أنابيب تقارير أو تحتاج فقط إلى تفريغ سريع على نمط CSV، فإن إتقان عملية التصدير يمكن أن يوفر لك ساعات من النسخ واللصق اليدوي.

في هذا البرنامج التعليمي سنستعرض الخطوات الدقيقة لأخذ خلية رقمية، تطبيق الترميز العلمي، وتصديرها كجدول باستخدام **ExportTableOptions**. في النهاية ستحصل على مقتطف شيفرة قابل للتنفيذ، وتفهم *السبب* وراء كل استدعاء، وتعرف كيف تعدل الشيفرة لنطاقات أكبر أو صيغ مختلفة.

## المتطلبات المسبقة

- .NET 6 أو أحدث (تعمل الواجهة البرمجية بنفس الطريقة على .NET Framework 4.7+)
- Aspose.Cells for .NET مثبت (`Install-Package Aspose.Cells`)
- فهم أساسي لصياغة C#؛ لا تحتاج إلى معرفة عميقة بداخل Excel

هل لديك كل ذلك؟ رائع—هيا نبدأ.

## الخطوة 1: إعداد خيارات التصدير – كيفية تصدير نطاق الخلايا كجدول

أول شيء تحتاجه هو كائن **ExportTableOptions** يخبر المكتبة كيف تتعامل مع محتويات الخلية. بدون هذا، سيعتمد التصدير على القيم الرقمية الخام، مما قد يسبب مشاكل للمستهلكين الذين يتوقعون نصًا.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**لماذا هذا مهم:**  
- `ExportAsString = true` يجبر المكتبة على كتابة النص المعروض للخلية، وليس القيمة العشرية الداخلية.  
- `CustomFormat` يتيح لك فرض **تصدير بالترميز العلمي**، وهو مفيد عند التعامل مع أعداد كبيرة جدًا أو صغيرة جدًا.

> **نصيحة احترافية:** إذا كنت بحاجة إلى تنسيق تاريخ أو عملة، استبدل `"0.00E+00"` بـ `"yyyy‑MM‑dd"` أو `"$#,##0.00"` على التوالي.

## الخطوة 2: إنشاء مصنف والحصول على الورقة الأولى – التعامل مع المصنف والورقة

**Workbook** يمثل ملف Excel بالكامل، بينما **Worksheet** هو تبويب واحد. للتصدير البسيط سنكتفي بالورقة الأولى، التي تكون دائمًا موجودة في الفهرس 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**لماذا هذا مهم:**  
إنشاء `Workbook` جديد يضمن لك بيئة نظيفة—لا أنماط مخفية أو بيانات متبقية قد تعيقك. الوصول إلى `Worksheets[0]` هو أسرع طريقة للحصول على مرجع للورقة النشطة دون القلق بشأن أسماء الأوراق.

## الخطوة 3: تعبئة الخلية المستهدفة – تنسيق قيمة الخلية C#

الآن نُدخل قيمة رقمية في الخلية **A1** (الصف 0، العمود 0). القيمة التي نختارها طويلة عشريًا عمدًا حتى تتمكن من رؤية الترميز العلمي يعمل.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**لماذا هذا مهم:**  
استدعاء `PutValue` يحدد نوع البيانات للخلية تلقائيًا. لأننا سنصدر كنص، سيتم تحويل القيمة العشرية الخام باستخدام الصيغة التي حددناها مسبقًا، لتظهر لنا النتيجة المرتبة `"1.23E+04"`.

## الخطوة 4: تصدير نطاق الخلية المحدد كجدول – تصدير نطاق الخلية كجدول

مع الخيارات والبيانات جاهزة، الخطوة الأخيرة هي إخبار Aspose.Cells بكتابة النطاق. طريقة `ExportTable` تتطلب صف/عمود البداية، حجم النطاق، وكائن الخيارات الذي أنشأناه.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**لماذا هذا مهم:**  
- `totalRows = 1` و `totalColumns = 1` يحدّان التصدير إلى خلية واحدة، لكن يمكنك توسيع هذين الرقمين لتغطية كتل أكبر (مثلاً `5, 3` لنطاق 5 صفوف × 3 أعمدة).  
- الطريقة تكتب البيانات إلى بنية جدول داخلية يمكن حفظها كـ CSV أو HTML أو حتى بثها مباشرة إلى عميل.

### حفظ النتيجة (اختياري)

إذا رغبت في حفظ الجدول المُصدَّر على القرص، يمكنك كتابته إلى ملف CSV:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

تشغيل ما سبق سيولد ملفًا يحتوي على:

```
1.23E+04
```

## حالات الحافة والاختلافات الشائعة

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|--------|
| **تصدير عدة صفوف** | تعديل `totalRows` واستخدام حلقة لتكرار الصفوف إذا لزم الأمر | يتيح تصدير دفعات دون استدعاء `ExportTable` متكررًا |
| **الحفاظ على الصيغ** | ضبط `ExportAsString = false` | يبقي الصيغة الأصلية بدلاً من القيمة المعروضة |
| **فواصل مختلفة** | استخدام overload `ExportTableToCSV(..., ',', ...)` | يتحول من القيم المفصولة بفواصل إلى قيم مفصولة بعلامات تبويب أو أنابيب |
| **مصنفات كبيرة** | بث التصدير لتجنب `OutOfMemoryException` | يناسب أكثر من 10 000 صف |

## مثال كامل يعمل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. يمكن تجميعه مع أي مشروع .NET Console يملك مرجعًا إلى Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**الناتج المتوقع:**  
ملف باسم `ExportedTable.csv` يحتوي على سطر واحد:

```
1.23E+04
```

إذا فتحت ملف CSV في محرر نصوص، سترى الترميز العلمي مطبقًا كما عُرِّف.

## الخلاصة

غطّينا **كيفية تصدير نطاق الخلايا كجدول** من البداية إلى النهاية: إعداد `ExportTableOptions`، إنشاء `Workbook`، إدخال البيانات، وأخيرًا استدعاء `ExportTable`. بفهم كل جزء، يمكنك الآن توسيع النهج إلى نطاقات أكبر، صيغ مختلفة، أو حتى دمجه في واجهة ويب API تُقدِّم بيانات مستخرجة من Excel مباشرة.

في المستقبل، قد ترغب في استكشاف:

- **ExportTableToHTML** للمعاينات الجاهزة للويب  
- **ExportTableToDataTable** لتغذية خطوط أنابيب ADO.NET مباشرة  
- صيغ **مخصصة متقدمة** للتواريخ، العملات، أو النسب المئوية  

جرّب ذلك، وستحوِّل تصدير خلية بسيطة إلى محرك توصيل بيانات مرن. لديك أسئلة أو حالة استخدام غريبة؟ اترك تعليقًا أدناه—برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}