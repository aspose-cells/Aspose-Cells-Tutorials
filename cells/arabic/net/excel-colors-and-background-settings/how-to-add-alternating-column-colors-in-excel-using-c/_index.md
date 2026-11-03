---
category: general
date: 2026-10-01
description: ألوان أعمدة متناوبة في Excel باستخدام C# – تعلم كيفية إنشاء ملف Excel
  من DataTable، ضبط لون خلفية الخلية في C#، واستيراد DataTable إلى Excel بأعمدة منسقة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: ar
lastmod: 2026-10-01
og_description: تلوين الأعمدة المتناوبة في إكسل بسهولة. اتبع هذا الدليل لإنشاء ملف
  إكسل من DataTable، وتعيين لون خلفية الخلية باستخدام C#، واستيراد DataTable إلى إكسل
  مع أعمدة منسقة.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: إضافة ألوان أعمدة متناوبة في Excel باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: كيفية إضافة ألوان أعمدة متناوبة في Excel باستخدام C#
url: /ar/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة ألوان أعمدة متناوبة في Excel باستخدام C#

إذا كنت بحاجة إلى **alternating column colors excel** في تقرير يتم إنشاؤه من تطبيقك، فإن هذا الدليل يوضح لك حلاً كاملاً. ستتعرف على كيفية إنشاء ملف Excel من `DataTable`، وتعيين لون خلفية الخلية بأسلوب C#، واستيراد datatable إلى excel مع تطبيق نمط مميز لكل عمود.

يغطي الدليل كل ما تحتاجه: حزم NuGet المطلوبة، مثال شفرة كامل قابل للتنفيذ، وتفسيرات لماذا كل خطوة مهمة. في النهاية ستحصل على مصنف منسق يمكن فتحه مباشرة في Microsoft Excel.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) SDK مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير متوافقة مع C#)  
* مكتبة **Aspose.Cells for .NET** – قم بتثبيتها باستخدام  

```bash
dotnet add package Aspose.Cells
```

توفر Aspose.Cells الفئات `Workbook`، `Worksheet`، `Style`، و `BackgroundType` المستخدمة في المثال.

## الخطوة 1: استرجاع البيانات المصدرية كـ `DataTable`

المهمة الأولى هي الحصول على البيانات التي تريد تصديرها. في المشاريع الفعلية قد تقوم بملء `DataTable` من استعلام قاعدة بيانات، أو استدعاء API، أو أي مجموعة في الذاكرة.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**لماذا هذا مهم:**  
`DataTable` هو حاوية عامة تتطابق بسهولة مع ورقة عمل Excel. استخدام `DataTable` يتيح لك **create excel file from datatable c#** دون الحاجة إلى كتابة حلقات مخصصة لكل عمود.

## الخطوة 2: إنشاء مصنف جديد والحصول على ورقة العمل الأولى

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**التفسير:**  
`Workbook` هو الكائن الجذري؛ `Worksheets[0]` يعطيك الورقة الافتراضية التي ستوضع فيها البيانات.

## الخطوة 3: إعداد نمط مميز لكل عمود (ألوان خلفية متناوبة)

لتحقيق **alternating column colors excel**، نقوم بإنشاء `Style` لكل عمود ونعيّن لون خلفية فاتح يتناوب بين درجتين.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**لماذا نستخدم حلقة:**  
تضمن الحلقة أن **set cell background color c#** يُطبق بشكل متسق، حتى إذا تغير عدد الأعمدة أثناء التشغيل. هذا يجعل الحل قويًا للتقارير الديناميكية.

## الخطوة 4: استيراد `DataTable` إلى ورقة العمل، مع تطبيق أنماط الأعمدة

يمكن لـ Aspose.Cells استيراد `DataTable` مباشرة، ويمكننا تمرير مصفوفة الأنماط لتلوين كل عمود.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**ما يحدث خلف الكواليس:**  
`ImportDataTable` يكتب صف العنوان، ثم كل صف بيانات. لأننا قدمنا `columnStyles`، يحصل كل خلية في العمود المعني على النمط المقابل، مما يمنحنا الألوان المتناوبة المطلوبة.

## الخطوة 5: حفظ المصنف المنسق إلى ملف

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

عند فتح *StyledTable.xlsx* في Excel ستلاحظ أن كل عمود مُظلل بشكل متناوب، مما يجعل الجدول أسهل للقراءة.

## مثال كامل قابل للتنفيذ

بجمع كل الأجزاء معًا، إليك برنامج مستقل يمكنك نسخه، لصقه، وتشغيله.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### النتيجة المتوقعة

* ملف باسم **StyledTable.xlsx** موجود في `C:\Temp\`.  
* ورقة العمل تُظهر ثلاثة أعمدة (`Id`, `Name`, `Score`) بألوان خلفية متناوبة: الأعمدة 1 و 3 بلون *LightYellow*، والعمود 2 بلون *LightCyan*.  
* جميع الصفوف من `DataTable` تظهر تحت صف العنوان.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني استخدام ألوان أخرى؟* | نعم. استبدل `System.Drawing.Color.LightYellow` و `LightCyan` بأي قيمة `System.Drawing.Color` تريدها. |
| *ماذا لو كان الـ DataTable يحتوي على أعمدة كثيرة؟* | الحلقة تنشئ نمطًا لكل عمود تلقائيًا، لذا النمط يتوسع دون تعديل الكود. |
| *هل يجب تحرير (dispose) المصنف؟* | Aspose.Cells يطبق `IDisposable`. إذا وضعت `Workbook` داخل كتلة `using`، سيتم تحرير الموارد فورًا. |
| *كيف أطبق نفس الألوان المتناوبة على الصفوف بدلاً من الأعمدة؟* | أنشئ مصفوفة `Style[]` للصفوف واستدعِ `worksheet.Cells.ImportDataTable(..., rowStyles)` – تدعم Aspose.Cells التحميل بأكثر من طريقة. |
| *هل يمكن كتابة الملف مباشرة إلى تدفق (stream) (مثلاً لواجهة ويب API)؟* | نعم. استخدم `workbook.Save(stream, SaveFormat.Xlsx);` بدلاً من مسار الملف. |

## نصائح من الميدان

* **نصيحة احترافية:** احفظ كائنات النمط في ذاكرة مؤقتة إذا كنت تنشئ العديد من أوراق العمل في تشغيل واحد – إنشاء نمط يكلف قليلًا، لكن إعادة استخدامه يقلل من استهلاك الذاكرة.  
* **احذر من:** عند استخدام `System.Drawing.Color` على منصات غير Windows، أضف حزمة NuGet `System.Drawing.Common` وتأكد أن وقت التشغيل يدعم GDI+.

## الخلاصة

الآن تعرف كيف تقوم بـ **alternating column colors excel** بإنشاء ملف Excel من `DataTable` في C#، وتعيين ألوان خلفية الخلايا باستخدام Aspose.Cells، و**import datatable to excel** مع مصفوفة أنماط الأعمدة. هذا النهج سريع، قابل للصيانة، ويعمل مع أي حجم مجموعة بيانات.

### الخطوات التالية

* استكشف **set cell background color c#** لتنسيق شرطي (مثلاً لتسليط الضوء على الدرجات المنخفضة).  
* اجمع هذه التقنية مع **create excel file from datatable c#** لإنشاء تقارير متعددة الأوراق.  
* انظر إلى API الرسم البياني في Aspose.Cells لإضافة ملخصات بصرية إلى نفس المصنف.

لا تتردد في تعديل الألوان، صيغة الملف، أو مصدر البيانات لتتناسب مع احتياجات مشروعك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}