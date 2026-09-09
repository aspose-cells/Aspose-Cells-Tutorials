---
category: general
date: 2026-03-01
description: استيراد البيانات مع التنسيق إلى Excel باستخدام C#. تعلم كيفية استيراد
  DataTable إلى Excel وإضافة لون خلفية إلى الخلايا في بضع خطوات فقط.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: ar
og_description: استيراد البيانات مع التنسيق إلى Excel باستخدام C#. دليل خطوة بخطوة
  يوضح كيفية استيراد DataTable وإضافة لون خلفية للخلايا.
og_title: استيراد البيانات مع التنسيق إلى إكسل – دليل C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: استيراد البيانات مع التنسيق إلى إكسل باستخدام C#
url: /ar/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استيراد البيانات مع التنسيق إلى Excel باستخدام C#

هل احتجت يومًا إلى **استيراد البيانات مع التنسيق** إلى مصنف Excel لكنك تحصل دائمًا على ورقة عادية ومملة؟ لست وحدك. يواجه معظم المطورين هذا الجدار عندما يكتشفون أن الاستيراد الافتراضي يزيل جميع الألوان والأنماط التي قاموا بإعدادها بعناية في بيانات المصدر.

في هذا الدرس سنستعرض حلًا كاملًا وجاهزًا للتنفيذ **يستورد DataTable إلى Excel** و**يضيف لون خلفية إلى خلايا Excel** في الوقت نفسه. لا تحتاج إلى أي معالجة لاحقة—ستظهر جدول البيانات بالضبط كما تريد مباشرةً.

## ما ستتعلمه

- كيفية استرجاع البيانات إلى `DataTable`.
- كيفية تعريف مصفوفة من كائنات `Style` التي تحمل ألوان الخلفية.
- كيفية استدعاء `ImportDataTable` مع تلك الأنماط بحيث يحافظ الاستيراد على التنسيق.
- مثال كامل قابل للتنفيذ يمكنك إدراجه في تطبيق console ورؤية النتيجة فورًا.
- نصائح، ومخاطر محتملة، وتنوعات للمشاريع الواقعية.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).
- مكتبة **GemBox.Spreadsheet** (الإصدار المجاني يكفي للعرض).
- إلمام أساسي بـ C# ومفاهيم Excel.

إذا كنت تتساءل *لماذا GemBox؟* لأنها توفر طريقة سطر واحد `ImportDataTable` تقبل مصفوفات الأنماط—وهو بالضبط ما نحتاجه **لاستيراد البيانات مع التنسيق** دون كتابة حلقة.

---

## الخطوة 1: إعداد المشروع وإضافة GemBox.Spreadsheet

لبدء العمل، أنشئ تطبيق console جديد:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **نصيحة احترافية:** الإصدار المجاني يحد من عدد الخلايا إلى 150 ألف خلية، وهو كافٍ للعرض. إذا وصلت إلى الحد، قم بالترقية أو التحول إلى EPPlus، لكن الواجهة البرمجية ستختلف قليلًا.

## الخطوة 2: استرجاع بيانات المصدر كـ `DataTable`

أول شيء نحتاجه هو `DataTable` يحاكي البيانات التي عادةً ما تجلبها من قاعدة بيانات. إليك أداة مساعدة صغيرة تنشئ واحدة في الذاكرة:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**لماذا هذا مهم:** بفصل استرجاع البيانات في طريقة منفصلة، يمكنك استبدال أي مصدر—SQL، CSV، خدمة ويب—دون لمس منطق الاستيراد. هذا يبقي الكود نظيفًا ويجعل الدرس **كيفية استيراد datatable إلى excel** قابلًا لإعادة الاستخدام.

## الخطوة 3: تعريف الأنماط التي تريد تطبيقها

الآن يأتي الجزء الممتع: سننشئ مصفوفة من كائنات `Style`، كل منها يحمل `ForegroundColor` مميز. تسمح لك GemBox بتعيين `BackgroundPatternColor` (لون تعبئة الخلية) و`ForegroundColor` (لون النص). في هذا العرض سنلون العمودين الأولين بألوان مختلفة.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**شرح:**  
- كائنات `Style` خفيفة الوزن؛ لا تحتاج لإنشاء كائن جديد لكل خلية.  
- بمواءمة ترتيب المصفوفة مع ترتيب الأعمدة، تقوم GemBox تلقائيًا بتطبيق النمط المطابق أثناء الاستيراد.  
- هذا هو المفتاح لـ **استيراد البيانات مع التنسيق**—التنسيق ينتقل مع البيانات، لا بعد ذلك.

## الخطوة 4: استيراد `DataTable` إلى ورقة العمل مع الأنماط

مع البيانات والأنماط جاهزة، يمكننا الآن إنشاء مصنف، اختيار أول ورقة عمل، واستدعاء `ImportDataTable`. توقيع الطريقة يبدو هكذا:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

إليك كيفية استخدامها:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**ما الذي يحدث في الخلفية؟**  
- `true` يخبر GemBox بكتابة أسماء الأعمدة في الصف الأول.  
- `0, 0` يضع الاستيراد في الخلية A1.  
- `importStyles` يربط كل عمود بالألوان التي عرّفناها مسبقًا.  

عند فتح *Report.xlsx*، ستلاحظ أن عمود **ID** مظلل باللون الأزرق الفاتح، وعمود **Name** مظلل باللون الأخضر الفاتح، وعمود **Score** يبقى بدون تعديل. هذا هو **استيراد البيانات مع التنسيق** في استدعاء واحد.

## الخطوة 5: التحقق من النتيجة (الناتج المتوقع)

افتح ملف `Report.xlsx` المُنشأ. يجب أن ترى شيئًا مشابهًا لهذا:

| المعرف (أزرق فاتح) | الاسم (أخضر فاتح) | النتيجة |
|--------------------|-------------------|----------|
| 1                  | Alice             | 93.5     |
| 2                  | Bob               | 78.0     |
| 3                  | Charlie           | 85.2     |
| 4                  | Diana             | 91.3     |
| 5                  | Ethan             | 67.8     |

- خلايا عمود **المعرف** لها خلفية زرقاء فاتحة.  
- خلايا عمود **الاسم** لها خلفية خضراء فاتحة.  
- عمود **النتيجة** يبقى بخلفية بيضاء افتراضية.

هذا التلميح البصري يجعل التقرير سهل القراءة فورًا—لمسة صغيرة يمكنها تحسين تجربة المستخدم بشكل كبير.

![صورة لورقة Excel تُظهر استيراد البيانات مع التنسيق – عمود المعرف أزرق فاتح، عمود الاسم أخضر فاتح](excel-screenshot.png "مثال على استيراد البيانات مع التنسيق")

*يتضمن نص الصورة الكلمة المفتاحية الأساسية لتحسين محركات البحث.*

---

## أسئلة شائعة وحالات خاصة

### هل يمكنني تطبيق أكثر من مجرد ألوان الخلفية؟

بالطبع. تسمح لك `Style` بتعيين الخطوط، الحدود، تنسيقات الأرقام، وحتى التنسيق الشرطي. على سبيل المثال، لجعل الدرجات فوق 90 غامقة وحمراء:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### ماذا لو كان لدي DataTable يحتوي على أعمدة أكثر من الأنماط؟

ستطبق GemBox الأنماط فقط على الأعمدة التي لها إدخال مطابق في المصفوفة. الأعمدة الزائدة تعود إلى النمط الافتراضي—بدون أي خطأ.

### هل يعمل هذا مع مجموعات بيانات كبيرة؟

نعم، لكن راقب حد الخلايا في الإصدار المجاني (150 ألف خلية). للتقارير الضخمة، فكر في الترخيص المدفوع أو بث البيانات صفًا بصف مع `worksheet.Cells[row, col].Value = …`—مع ذلك ستفقد راحة الاستدعاء في سطر واحد.

### كيف يمكنني استيراد البيانات مع التنسيق من قالب Excel موجود؟

يمكنك تحميل قالب المصنف أولًا:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

هذا يتيح لك الحفاظ على شعارات الرأس، التذييلات، وأي أنماط موجودة مسبقًا مع الاستمرار في **استيراد البيانات مع التنسيق** للجزء الديناميكي.

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

شغّل البرنامج (`dotnet run`) وافتح ملف *Report.xlsx* المُنشأ لترى الألوان مطبقة فورًا.

---

## الخلاصة

أصبح لديك الآن حلًا قويًا، النهاية

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}