---
category: general
date: 2026-11-16
description: كيفية نسخ جدول محوري من ملف Excel إلى مصنف جديد باستخدام C#. تعلم تحميل
  المصنف، نسخ النطاق، والحفاظ على الجداول المحورية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: ar
lastmod: 2026-11-16
og_description: كيفية نسخ جدول محوري من مصنف موجود إلى مصنف جديد باستخدام C#. اتبع
  هذا الدليل الكامل لتحميل مصنف Excel، نسخ النطاق، والحفاظ على الجدول المحوري دون
  تغيير.
og_image_alt: how to copy pivot table example in C#
og_title: كيفية نسخ جدول محوري إلى مصنف جديد في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: كيفية نسخ جدول محوري إلى مصنف جديد في C#
url: /ar/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري إلى مصنف جديد في C#

إذا كنت بحاجة إلى **how to copy pivot table** من ملف Excel إلى مصنف جديد، فإن هذا الدليل يوضح لك الخطوات الدقيقة. ستتعلم كيفية **load excel workbook c#**، تعريف نطاق المصدر، و**copy range to new workbook** مع الحفاظ على الجدول المحوري دون تغيير.

نسخ جدول محوري هو طلب شائع عندما تريد إعادة استخدام قالب تقرير، نقل البيانات بين المشاريع، أو إنشاء ملف خفيف الوزن للتوزيع. يستخدم مثال الشيفرة أدناه Aspose.Cells، مكتبة .NET مُدارة بالكامل تعمل دون الحاجة إلى تثبيت Microsoft Office. بنهاية هذا الدرس ستحصل على برنامج قابل للتنفيذ ينشئ مصنفًا جديدًا يحتوي على الجدول المحوري الأصلي، جاهز للمعالجة الإضافية أو المشاركة.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث (المثال يعمل مع .NET Core و .NET Framework)  
* Visual Studio 2022 أو أي محرر C# تفضله  
* رخصة Aspose.Cells for .NET (الإصدار التجريبي المجاني يعمل للتقييم)  
* ملف Excel المصدر (`Source.xlsx`) الذي يحتوي على جدول محوري واحد على الأقل  

> **نصيحة احترافية:** إذا كنت تستخدم النسخة التجريبية المجانية، قم بتعيين الرخصة في الشيفرة لتجنب العلامات المائية للتقييم.

## الخطوة 1: تحميل المصنف المصدر (load excel workbook c#)

الإجراء الأول هو فتح المصنف الذي يحتوي على الجدول المحوري. تقوم Aspose.Cells بقراءة الملف إلى الذاكرة، مما يمنحك وصولًا كاملاً إلى أوراق العمل، الخلايا، وكائنات الجداول المحورية.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*لماذا هذا مهم*: تحميل المصنف هو الأساس لأي أتمتة Excel. بدون كائن `Workbook` صالح لا يمكنك فحص الجدول المحوري أو نسخ بياناته.

## الخطوة 2: تحديد مساحة الخلايا التي تحيط بالجدول المحوري (copy range to new workbook)

يعيش الجدول المحوري داخل كتلة مستطيلة من الخلايا. يجب عليك تحديد تلك الكتلة حتى يعرف عملية النسخ ما الذي يجب نقله. يستخدم مُنشئ `CellArea` فهارس تبدأ من الصفر: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*لماذا هذا مهم*: من خلال تحديد النطاق صراحةً تتجنب نسخ البيانات غير المرتبطة وتضمن تضمين ذاكرة التخزين المؤقت للجدول المحوري. يمكن حساب النطاق ديناميًا إذا كنت بحاجة إلى التعامل مع أحجام جداول محورية مختلفة.

## الخطوة 3: إنشاء مصنف جديد والحصول على ورقة العمل الأولى

الآن أنشئ المصنف الوجهة الذي سيستقبل الصفوف المنسوخة. تقوم Aspose.Cells تلقائيًا بإضافة ورقة عمل افتراضية، والتي سنستخدمها كهدف.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*لماذا هذا مهم*: البدء بمصنف نظيف يضمن أن الجدول المحوري فقط (وصفوفه الداعمة) سيظهر في الملف، مما يحافظ على خفة الناتج.

## الخطوة 4: نسخ الصفوف من النطاق المصدر إلى ورقة الوجهة (how to copy pivot table)

طريقة `CopyRows` تنسخ الصفوف بالكامل، مع الحفاظ على الصيغ، التنسيق، وبشكل حاسم—الجداول المحورية. معلمات الطريقة هي: صف البداية، صف النهاية، مجموعة خلايا الهدف، ومؤشر الصف في الهدف حيث يبدأ النسخ (هنا `0` للبدء من الصف الأول).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*لماذا هذا مهم*: استخدام `CopyRows` بدلاً من نسخ الخلايا الفردية يضمن بقاء ذاكرة التخزين المؤقت للجدول المحوري مرتبطة بالبيانات المنسوخة. تتعامل Aspose.Cells مع هياكل XML الأساسية، لذا لا تحتاج إلى إعادة بناء الجدول المحوري يدويًا.

## الخطوة 5: حفظ المصنف الناتج (copy range to new workbook)

أخيرًا، احفظ الملف الجديد على القرص. الآن يحتوي مصنف الوجهة على جدول محوري مطابق يعمل بشكل مستقل عن ملف المصدر.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج ينتج `CopyWithPivot.xlsx`. فتح الملف في Excel يظهر:

* نفس تخطيط الجدول المحوري كما في `Source.xlsx`
* جميع صفوف البيانات المصدر التي كانت جزءًا من ذاكرة التخزين المؤقت للجدول المحوري
* لا توجد مراجع إلى المصنف الأصلي (الجدول المحوري يعمل دون اتصال)

## التعامل مع التغييرات الشائعة

### نسخ جداول محورية متعددة

إذا كانت ورقة المصدر تحتوي على عدة جداول محورية، قم بتوسيع `CellArea` لتغطية اتحاد جميع النطاقات، أو كرر خطوة النسخ لكل منطقة مميزة.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### الحفاظ على الأنماط والتنسيق الشرطي

`CopyRows` ينسخ أنماط الخلايا تلقائيًا. إذا كنت بحاجة إلى الحفاظ على الأنماط المسماة على مستوى المصنف أو تنسيقات الأرقام المخصصة، استدعِ `destWorkbook.Worksheets[0].CopyStyle` قبل الحفظ.

### العمل مع مصنفات كبيرة

للملفات التي يزيد حجمها عن 100 ميغابايت، فكر في استخدام `Workbook.LoadOptions` مع ضبط `MemorySetting` إلى `MemorySetting.MemoryPreference` لتقليل الضغط على الذاكرة.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## الشيفرة المصدرية الكاملة (جاهزة للتنفيذ)

فيما يلي البرنامج الكامل، بما في ذلك توجيهات `using` والتعليقات. انسخه إلى مشروع وحدة تحكم جديد واستبدل `YOUR_DIRECTORY` بمسار المجلد الفعلي.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

شغّل البرنامج (`dotnet run` أو `Ctrl+F5` في Visual Studio). بعد التنفيذ، افتح `CopyWithPivot.xlsx` للتحقق من أن الجدول المحوري يعمل تمامًا كما الأصلي.

## الأسئلة المتكررة

**س: هل يعمل هذا مع الماكرو أو المصنفات المفعلة بـ VBA؟**  
ج: يمكن لـ Aspose.Cells قراءة الملفات المفعلة بالماكرو (`.xlsm`)، لكن كود الماكرو لا يُنسخ. يتم الحفاظ على الجدول المحوري نفسه لأنه جزء من XML ورقة العمل.

**س: ماذا لو كان الجدول المحوري يستخدم مصدر بيانات خارجي؟**  
ج: عملية النسخ تشمل البيانات المخزنة مؤقتًا فقط. إذا كان المصنف الوجهة يحتاج إلى تحديث من المصدر الأصلي، سيتعين عليك إعادة تكوين اتصال البيانات يدويًا.

**س: هل يمكنني نسخ الجدول المحوري دون صفوف البيانات الأساسية؟**  
ج: لا. يحتاج الجدول المحوري إلى ذاكرة التخزين المؤقت الخاصة به. الطريقة الأكثر موثوقية هي نسخ الصفوف التي تحتوي على الذاكرة المؤقتة، كما هو موضح. يمكنك لاحقًا إخفاء تلك الصفوف إذا لم ترغب في ظهورها.

## الخلاصة

أنت الآن تعرف **how to copy pivot table** من ملف Excel إلى آخر باستخدام C#. غطى الدرس **load excel workbook c#**، تعريف **copy range to new workbook**، واستخدم طريقة `CopyRows` في Aspose.Cells للحفاظ على الجدول المحوري دون تغيير. مع المثال الكامل القابل للتنفيذ يمكنك دمج هذا النمط في خطوط تقارير، أدوات تصدير آلية، أو أي سيناريو يحتاج إلى نقل جدول محوري بين المصنفات.

### الخطوات التالية

- استكشف ميزات **Aspose.Cells** مثل تحديث الجداول المحورية برمجيًا.  
- اجمع هذا النهج مع **ExcelPackage** (EPPlus) إذا كنت تحتاج إلى بديل مفتوح المصدر.  
- قم بأتمتة النسخ عبر عدة أوراق عن طريق التكرار عبر `srcWorkbook.Worksheets`.  

لا تتردد في تجربة نطاقات مختلفة، إضافة تنسيقات مخصصة، أو تضمين المنطق في خدمة معالجة بيانات أكبر. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف جديد في C# – نسخ جدول محوري](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [كيفية نسخ جدول محوري في Excel باستخدام C# و Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [نسخ جدول محوري إلى مصنف جديد، تصدير الشكل إلى PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}