---
category: general
date: 2026-07-03
description: تطبيق ألوان الصفوف المتناوبة أثناء استيراد جدول البيانات إلى Excel باستخدام
  C#. تعلم كيفية تصدير جدول البيانات C# إلى Excel، حفظ جدول Excel المُنسق، والحفاظ
  على تنسيق المصنف.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: ar
og_description: تطبيق ألوان الصفوف المتناوبة في Excel باستخدام C#. يوضح هذا الدرس
  كيفية استيراد جدول البيانات إلى Excel، وتصدير جدول البيانات C# إلى Excel، وحفظ المصنف
  مع التنسيق.
og_title: تطبيق ألوان الصفوف المتناوبة في إكسل باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: تطبيق ألوان الصفوف المتناوبة في إكسل باستخدام C# – دليل كامل
url: /ar/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق ألوان الصفوف المتناوبة في Excel باستخدام C# – دليل شامل

هل احتجت يومًا إلى **تطبيق ألوان صفوف متناوبة** عندما تقوم بتصدير `DataTable` من C# إلى Excel؟ لست وحدك—المطورون يطرحون باستمرار سؤالًا حول كيفية جعل تلك الجداول تبدو مصقولة دون الحاجة إلى تعديل Excel يدويًا بعد ذلك. الخبر السار؟ يمكنك القيام بذلك برمجياً في بضع أسطر من الشيفرة فقط.

في هذا الدرس سنستعرض **استيراد datatable إلى excel**، ونوضح لك كيفية **تصدير c# datatable إلى excel** مع جدول منسق، وأخيرًا **حفظ جدول منسق excel** مع الحفاظ على التنسيق. في النهاية ستتمكن من **حفظ المصنف مع التنسيق** الذي يبدو جاهزًا لاجتماع مع عميل.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (العينة تستخدم .NET 6، لكن أي نسخة حديثة تعمل)
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو نسخة مرخصة) – هذه المكتبة تجعل التنسيق سهلًا
- مصدر `DataTable` (يمكن أن يكون من قاعدة بيانات، CSV، أو مجموعة في الذاكرة)

> **نصيحة احترافية:** إذا لم يكن لديك Aspose.Cells بعد، يمكنك الحصول عليه من NuGet باستخدام الأمر `dotnet add package Aspose.Cells`.

## الخطوة 1: إعداد المشروع وتحميل البيانات

أولًا، أنشئ تطبيقًا من نوع console (أو أي مشروع C#) وأضف عبارات `using` اللازمة. ثم احصل على البيانات داخل `DataTable`. للتوضيح سننشئ جدولًا بسيطًا في الوقت الفعلي.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**لماذا هذا مهم:** وجود `DataTable` جاهزة يعني أنه يمكنك **استيراد datatable إلى excel** في استدعاء واحد، مما يلغي الحاجة إلى إدخال الخلايا يدويًا واحدةً تلو الأخرى.

## الخطوة 2: إنشاء مصنف وتحديد أنماط الصفوف المتناوبة

الآن سننشئ كائن `Workbook` جديد. الحيلة لتطبيق **ألوان صفوف متناوبة** تكمن في `ImportTableOptions.StyleArray`. سنستخدم أول نمطين مدمجين (عادةً أبيض ورمادي فاتح) لكن يمكنك تخصيصهما لاحقًا.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**شرح:** `ImportTableOptions` يخبر Aspose.Cells كيف يتعامل مع كل صف أثناء الاستيراد. من خلال تزويده بـ `StyleArray` يحتوي على مدخلين، تقوم المكتبة تلقائيًا بتلوين كل صف فردي بالنمط الأول وكل صف زوجي بالنمط الثاني—وهذا بالضبط ما تحتاجه لتطبيق **ألوان صفوف متناوبة**.

## الخطوة 3: سحب الـ DataTable إلى ورقة العمل (مع العناوين)

مع المصنف والأنماط جاهزة، الآن **نستورد datatable إلى excel**. طريقة `ImportDataTable` تقوم بالعمل الشاق: تكتب عناوين الأعمدة، تحترم مصفوفة الأنماط، وتضع البيانات بدءًا من الخلية A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**لماذا نضع `true` كقيمة للمعامل الثاني:** هذا يخبر الطريقة بكتابة أسماء الأعمدة في الصف الأول، وهو أمر أساسي لتقرير يبدو احترافيًا.

## الخطوة 4: تحسين الجدول (اختياري لكنه مفيد)

إذا أردت أن يضبط الجدول الأعمدة تلقائيًا أو يضيف صفًا للتصفية، بضع أسطر إضافية تجعل المظهر أكثر بريقًا.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

هذه التعديلات لا تؤثر على الألوان المتناوبة لكنها تحسن تجربة المستخدم العامة لملف **حفظ جدول منسق excel**.

## الخطوة 5: حفظ المصنف مع الحفاظ على جميع التنسيقات

أخيرًا، نكتب الملف إلى القرص. طريقة `Save` تحتفظ بكل نمط قمنا بتعيينه، مما يضمن بقاء الصفوف المتناوبة كما هي.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

عند فتح `StyledEmployees.xlsx`، ستلاحظ جدولًا نظيفًا حيث تتناوب الصفوف بين الأبيض والرمادي الفاتح—بالضبط الإشارة البصرية التي يعتمد عليها الكثير من المستخدمين لسهولة القراءة.

### النتيجة المتوقعة

| المعرف | الاسم   | القسم      | تاريخ التوظيف |
|--------|----------|------------|----------------|
| 1      | Alice    | Finance    | 15‑01‑2020 |
| 2      | Bob      | HR         | 23‑06‑2019 |
| 3      | Charlie  | IT         | 10‑03‑2021 |
| 4      | Diana    | Marketing  | 05‑11‑2018 |

- الصف 1، 3 … → خلفية بيضاء  
- الصف 2، 4 … → خلفية رمادية فاتحة  

هذا هو كامل عملية **حفظ المصنف مع التنسيق**.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان الـ DataTable يحتوي على آلاف الصفوف؟

طريقة `ImportDataTable` تنقل البيانات بكفاءة، لكن قد تواجه حدود الذاكرة مع الجداول الكبيرة جدًا. في هذه الحالة، فكر في تقسيم التصدير إلى عدة أوراق عمل أو استخدم نسخة `ImportDataTable` التي تسمح لك بتحديد صف وعمود البداية.

### هل يمكنني استخدام ألوان مخصصة بدلاً من الألوان المدمجة؟

بالطبع. ما عليك سوى استبدال تعيينات `ForegroundColor` في `styleWhite` و `styleGray` بأي `System.Drawing.Color` تفضله—مثل أزرق باهت أو ألوان العلامة التجارية للشركة.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### كيف أضمن أن نمط الصفوف المتناوبة سيستمر عندما يضيف المستخدمون صفوفًا لاحقًا؟

إذا قام المستخدمون بتحرير الملف يدويًا، فإن مصفوفة الأنماط الأصلية لن تمتد تلقائيًا. حل سريع هو تحويل النطاق إلى جدول Excel (`ListObject`) بعد الاستيراد؛ سيتولى Excel تكرار النمط للصفوف الجديدة.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

بهذا سيكتسب أي صف جديد ألوانًا متناوبة تلقائيًا.

## مثال كامل يعمل (جميع الخطوات في مكان واحد)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

شغّل البرنامج، افتح الملف المُنشأ، وسترى فورًا تطبيق الألوان المتناوبة—دون الحاجة لتنسيق يدوي.

## الخلاصة

لقد أوضحنا للتو كيفية **تطبيق ألوان صفوف متناوبة** عندما **نستورد datatable إلى excel** باستخدام C#. تغطي العملية كل ما تحتاجه لت **تصدير c# datatable إلى excel**، **حفظ جدول منسق excel**، و **حفظ المصنف مع التنسيق** الذي يبدو احترافيًا من أول تشغيل.

ما الخطوة التالية؟ جرّب تبديل النمطين للحصول على سمة مخصصة، أو حول النطاق إلى جدول Excel حتى يتمكن المستخدمون من الفرز والتصفية مع الحفاظ على نمط الألوان. يمكنك أيضًا استكشاف التنسيق الشرطي عبر `ConditionalFormattingCollection` للحصول على إشارات بصرية أكثر ديناميكية.

Got a twist


## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}