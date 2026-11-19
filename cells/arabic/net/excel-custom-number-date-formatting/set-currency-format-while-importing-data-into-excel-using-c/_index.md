---
category: general
date: 2026-11-19
description: تعيين تنسيق العملة في Excel باستخدام C# – تعلّم كيفية تعيين تنسيق الأرقام
  وتنسيق أعمدة Excel أثناء استيراد ورقة عمل Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: ar
lastmod: 2026-11-19
og_description: ضبط تنسيق العملة في Excel باستخدام C# واكتشف كيفية ضبط تنسيق الأرقام،
  وتعيين تنسيق الأرقام، وتنسيق أعمدة Excel أثناء استيراد ورقة عمل Excel.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: ضبط تنسيق العملة في Excel باستخدام C# – دليل خطوة بخطوة كامل
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: تعيين تنسيق العملة أثناء استيراد البيانات إلى Excel باستخدام C#
url: /ar/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تنسيق العملة أثناء استيراد البيانات إلى Excel باستخدام C#

إذا كنت بحاجة إلى **تعيين تنسيق العملة** في ورقة عمل Excel، يوضح لك هذا الدليل كيفية **تعيين تنسيق الأرقام** وتنسيق الأعمدة أثناء تنفيذ **استيراد ورقة عمل Excel**. ستشاهد مثالًا كاملاً قابلاً للتنفيذ يخصص تنسيق الرقم الصحيح لكل عمود من `DataTable` ويستورد البيانات بالتنسيق المطلوب.

العمل مع Excel من C# غالبًا ما يتطلب أكثر من مجرد إلقاء القيم الخام—يجب أيضًا التحكم في كيفية ظهور الأرقام. سواءً كنت تُنشئ فواتير، تقارير مالية، أو لوحات معلومات، فإن تنسيق العملة أو النسب المئوية أو التواريخ بشكل صحيح يجعل المخرجات قابلة للقراءة فورًا.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) مثبت.
* إشارة إلى **Aspose.Cells for .NET** (أو أي مكتبة توفر فئة `Style` مع خاصية `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* إلمام أساسي بـ `DataTable` ومجموعات C#.
* بيئة تطوير متكاملة مثل Visual Studio 2022 أو VS Code.

## الخطوة 1: استرجاع البيانات التي سيتم كتابتها إلى ورقة العمل

أولاً احصل على `DataTable` يحتوي على البيانات الخام التي تريد تصديرها. في المشاريع الحقيقية قد يأتي ذلك من استعلام قاعدة بيانات، أو استدعاء API، أو محلل CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **لماذا هذا مهم:** استيراد `DataTable` مكتمل يتيح لك إبقاء منطق استرجاع البيانات منفصلًا عن منطق إنشاء Excel، مما يحسن من قابلية الاختبار والصيانة.

## الخطوة 2: إنشاء مصفوفة الأنماط – عنصر واحد لكل عمود في DataTable

تتوقع Aspose.Cells مصفوفة `Style[]` يكون طولها مساويًا لعدد الأعمدة التي تخطط لاستيرادها. يمكن لكل عنصر أن يحمل تنسيق رقم محدد.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **نصيحة احترافية:** حتى إذا كنت تحتاج تنسيقًا لجزء فقط من الأعمدة، لا يزال عليك إنشاء كائن `Style` لكل عمود؛ وإلا ستحصل على استثناء `NullReferenceException` أثناء الاستيراد.

## الخطوة 3: تعيين تنسيق الرقم للأعمدة المطلوبة

أرقام الأنماط المدمجة تختلف حسب المكتبة. في Aspose.Cells:

* `0` → عام (عدد صحيح)  
* `2` → عملة (مثال: `$#,##0.00`)  
* `3` → تاريخ، إلخ.

هنا **نُعيّن تنسيق الرقم** لعمودين: العمود الأول (Id) يبقى عددًا صحيحًا، بينما العمود الثاني (Amount) يحصل على تنسيق عملة.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **كيفية تعيين تنسيق الرقم:** استخدام خاصية `Number` هو أسرع طريقة لاختيار تنسيق مدمج. للعملات بحسب الإعدادات الإقليمية، فكر في استخدام سلسلة تنسيق مخصصة تتضمن رمز العملة المناسب.

## الخطوة 4: استيراد DataTable إلى ورقة العمل، وتطبيق أنماط الأعمدة

الآن بعد أن أصبحت مصفوفة الأنماط جاهزة، استورد البيانات. طريقة `ImportDataTable` تحترم الأنماط التي مررت بها.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### النتيجة المتوقعة

عند فتح **FinancialReport.xlsx**، سترى:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*عمود **Amount** يُعرض باستخدام تنسيق العملة الذي قمت بتعيينه، بينما يبقى **Id** عددًا صحيحًا.*

## كيفية تعيين تنسيق الرقم لسيناريوهات إضافية

### تعيين تنسيق الرقم لأعمدة التاريخ

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### استخدام تنسيقات رقم مخصصة للنسب المئوية

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### التنسيق بما يتجاوز تنسيقات الأرقام

يمكنك أيضًا تعيين الخط، لون الخلفية، أو المحاذاة على نفس كائن `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **لماذا يعمل هذا:** كائن `Style` يجمع كل الخصائص البصرية للخلية. عندما تمرر المصفوفة إلى `ImportDataTable`, كل خلية ترث النمط المحدد تلقائيًا.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | العرض | الحل |
|---------|-------|------|
| نسيان إنشاء كل كائن `Style` | `NullReferenceException` عند الاستيراد | قم بالتكرار عبر المصفوفة واستدعِ `CreateStyle()` قبل ضبط الخصائص. |
| استخدام رقم مدمج غير صحيح | تنسيق خاطئ (مثال: تظهر التواريخ كأعداد صحيحة) | راجع وثائق المكتبة للحصول على القيم الثابتة الصحيحة لـ `Number`. |
| عدم حفظ المصنف | لا ملف إخراج أو ملف فارغ | استدعِ `workbook.Save(...)` بعد إكمال الاستيراد. |
| عدم توافق الإعدادات الإقليمية لرمز العملة | يظهر `$` حتى في المناطق غير الأمريكية | استخدم سلسلة تنسيق مخصصة بالرمز المناسب (مثال: `"€#,##0.00"`). |

## مثال كامل قابل للتنفيذ



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}