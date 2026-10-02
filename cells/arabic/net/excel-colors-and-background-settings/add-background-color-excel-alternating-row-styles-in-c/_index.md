---
category: general
date: 2026-04-07
description: إضافة لون خلفية لصفوف إكسل باستخدام C#. تعلّم كيفية تطبيق ألوان صفوف
  متناوبة، وضبط أنماط الخلفية الصلبة، واستيراد جدول البيانات إلى إكسل في سير عمل واحد.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: ar
og_description: إضافة لون خلفية لصفوف إكسل باستخدام C#. يوضح هذا الدليل كيفية تطبيق
  ألوان صفوف متناوبة، ضبط خلفية صلبة، واستيراد جدول البيانات إلى إكسل بكفاءة.
og_title: إضافة لون خلفية في إكسل – أنماط الصفوف المتناوبة في C#
tags:
- C#
- Excel
- DataTable
- Styling
title: إضافة لون خلفية في إكسل – أنماط الصفوف المتناوبة في C#
url: /ar/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة لون خلفية إكسل – أنماط الصفوف المتناوبة في C#

هل احتجت يومًا إلى **إضافة لون خلفية إكسل** للصفوف لكنك لم تكن متأكدًا من كيفية القيام بذلك دون كتابة آلاف الأسطر المتشابكة من الشيفرة؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما يحاولون أول مرة جعل جداول البيانات تبدو أكثر من مجرد تجميع خام للبيانات.  

الخبر السار؟ في بضع دقائق فقط يمكنك **تطبيق ألوان صفوف متناوبة**، ضبط **خلفية صلبة**، وحتى **استيراد datatable إلى إكسل** باستخدام نمط نظيف وقابل لإعادة الاستخدام في C#.  

في هذا الدرس سنستعرض العملية بالكامل، من جلب البيانات إلى `DataTable` إلى تنسيق كل صف بنمط خطوط مخططة باللون الأصفر الفاتح والأبيض. لا تحتاج إلى أي مكتبات خارجية بخلاف حزمة معالجة إكسل قوية (مثل **ClosedXML** أو **GemBox.Spreadsheet**)، وسترى لماذا هذا النهج فعال وسهل الصيانة.

## ما ستتعلمه

- كيفية استرجاع البيانات وإدخالها في ورقة عمل إكسل.
- كيفية **تنسيق صفوف إكسل** بألوان خلفية متناوبة.
- آلية **ضبط خلفية صلبة** باستخدام كائن `Style`.
- كيفية **استيراد datatable إلى إكسل** مع الحفاظ على تنسيقات الصفوف.
- نصائح للتعامل مع الحالات الخاصة مثل الجداول الفارغة أو أنظمة الألوان المخصصة.

> **نصيحة احترافية:** إذا كنت تستخدم بالفعل كائن دفتر العمل (`wb`) من مكتبة تدعم إنشاء الأنماط، يمكنك إعادة استخدام نفس كائنات `Style` عبر عدة أوراق عمل—مما يوفر الذاكرة ويحافظ على تنظيم الشيفرة.

## الخطوة 1: استرجاع البيانات – تحضير الـ DataTable

قبل أن يتم أي تنسيق نحتاج إلى مصدر للصفوف. في معظم السيناريوهات الواقعية يأتي ذلك من قاعدة بيانات، أو API، أو ملف CSV. للتوضيح، سنقوم بإنشاء `DataTable` بسيط في الذاكرة.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**لماذا هذا مهم:** استخدام `DataTable` يمنحك حاوية جدولة واعية للمخطط يمكن لمكتبة إكسل استيرادها مباشرة، مما يلغي الحاجة إلى كتابة حلقات خلية بخلية.

## الخطوة 2: إنشاء أنماط الصفوف – **تطبيق ألوان صفوف متناوبة**

الآن سنبني مصفوفة من كائنات `Style`—واحد لكل صف—حتى يتمكن كل صف من الحصول على خلفية خاصة به. النمط الذي سنستخدمه هو الأصفر الفاتح للصفوف الزوجية والأبيض للصفوف الفردية.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**التفسير:**  
- `wb.CreateStyle()` يمنحك كائن نمط نظيف يمكنك تعديلّه دون التأثير على الآخرين.  
- المعامل الثلاثي `(i % 2 == 0)` يحدد ما إذا كان الصف زوجيًا (أصفر فاتح) أو فرديًا (أبيض).  
- ضبط `Pattern = BackgroundType.Solid` هو الخطوة الحاسمة التي **تضبط خلفية صلبة**؛ بدونها سيتجاهل اللون.

## الخطوة 3: الحصول على ورقة العمل المستهدفة

معظم المكتبات تعرض مجموعة أوراق العمل. سنعمل مع الأولى، لكن يمكنك استهداف أي فهرس أو اسم تفضله.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

إذا كان دفتر العمل جديدًا تمامًا، عادةً ما تنشئ المكتبة ورقة افتراضية لك. وإلا، يمكنك إضافة واحدة صراحةً:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

## الخطوة 4: استيراد الـ DataTable مع أنماط الصفوف – **استيراد datatable إلى إكسل**

مع جاهزية الأنماط، الخطوة الأخيرة هي إدخال `DataTable` إلى الورقة مع تطبيق النمط المقابل على كل صف.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**ما الذي يحدث خلف الكواليس؟**  
- `true` يخبر الطريقة بكتابة رؤوس الأعمدة كأول صف.  
- `0, 0` يحدد الزاوية العليا اليسرى (A1) كنقطة الإدراج.  
- `rowStyles` يطابق كل `Style` مع صف البيانات المقابل، مما يمنحنا الألوان المتناوبة التي أعددناها مسبقًا.

## الخطوة 5: حفظ دفتر العمل

الجزء الأخير من اللغز هو حفظ دفتر العمل إلى ملف حتى تتمكن من فتحه في إكسل ورؤية النتيجة.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

افتح الملف وسترى ورقة منسقة بشكل أنيق:

- صف الرأس بخط عريض (تنسيق المكتبة الافتراضي).  
- الصف 1، 3، 5… بخلفية بيضاء نظيفة.  
- الصف 2، 4، 6… بملء أصفر فاتح خفيف، مما يسهل القراءة.

### لقطة النتيجة المتوقعة

| المعرف | الاسم      | النتيجة |
|----|-----------|-------|
| 1  | طالب 1 | 78.45 |
| 2  | طالب 2 | 62.13 |
| 3  | طالب 3 | 91.27 |
| …  | …         | …     |

الصفوف 2، 4، 6، … تظهر بخلفية أصفر فاتح—وهو بالضبط تأثير **تطبيق ألوان صفوف متناوبة** الذي استهدفناه.

![مثال إضافة لون خلفية إكسل](https://example.com/excel-background.png "مثال إضافة لون خلفية إكسل")

*(يتضمن نص البديل الكلمة المفتاحية الأساسية لتحسين محركات البحث.)*

## معالجة الحالات الخاصة والاختلافات

### DataTable فارغ

إذا كان `dataTable.Rows.Count` صفرًا، ستكون مصفوفة `rowStyles` فارغة وستظل `ImportDataTable` تكتب صف الرأس (إذا كان `includeHeaders` يساوي `true`). لا يتم إلقاء استثناء، لكن قد ترغب في الحماية من إنشاء ملف شبه فارغ:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### أنظمة ألوان مخصصة

هل تريد خطوطًا باللون الأزرق/الرمادي بدلاً من الأصفر/الأبيض؟ فقط استبدل قيم `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

لا تتردد في سحب الألوان من ملف إعدادات حتى يتمكن غير المطورين من تعديل اللوحة دون لمس الشيفرة.

### إعادة استخدام الأنماط عبر عدة أوراق عمل

إذا كنت تصدر عدة جداول إلى نفس دفتر العمل، يمكنك إنشاء مصفوفة الأنماط مرة واحدة وإعادة استخدامها:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

فقط احرص على أن يكون عدد الصفوف في كلا الجدولين متساويًا، أو أنشئ مصفوفة جديدة لكل ورقة.

## مثال كامل يعمل

بوضع كل شيء معًا، إليك برنامج مستقل يمكنك نسخه ولصقه في تطبيق كونسول.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

شغّل البرنامج، افتح `Report.xlsx`، وسترى الخلفية المتناوبة بالضبط كما هو موضح.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}