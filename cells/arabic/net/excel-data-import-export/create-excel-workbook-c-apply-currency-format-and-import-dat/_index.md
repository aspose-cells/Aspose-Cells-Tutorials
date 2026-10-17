---
category: general
date: 2026-03-30
description: إنشاء مصنف إكسل باستخدام C# مع تنسيق العملة. تعلّم كيفية استيراد DataTable،
  وإضافة تنسيق الأرقام في إكسل، وتطبيق تنسيق العملة على العمود في دقائق.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: ar
og_description: إنشاء دفتر عمل Excel باستخدام C# وتنسيق الخلايا كعملة على الفور. يوضح
  هذا الدليل خطوة بخطوة كيفية استيراد DataTable إلى Excel وإضافة تنسيق رقم Excel لعمود.
og_title: إنشاء مصنف إكسل C# – دليل تنسيق العملة
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف إكسل C# – تطبيق تنسيق العملة واستيراد جدول البيانات
url: /ar/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel باستخدام C# – تطبيق تنسيق العملة واستيراد DataTable

هل احتجت يوماً إلى **إنشاء مصنف Excel C#** يبدو كأنه تقرير مصقول؟ ربما تقوم بجلب أرقام المبيعات من قاعدة بيانات وتريد أن يظهر عمود السعر بالدولار دون الحاجة إلى تعديل Excel يدوياً. هل هذا مألوف؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما يبدأون بأتمتة تصدير Excel.

في هذا الدليل سنستعرض حلاً كاملاً جاهزاً للتنفيذ **ينشئ مصنف Excel C#**، يستورد `DataTable`، و**يُنسق عمود السعر كعملة**. في النهاية ستحصل على ملف اسمه `StyledTable.xlsx` يمكنك فتحه ورؤية الأرقام مُنسقة بشكل جميل. لا حاجة لمعالجة إضافية بعد ذلك.

> **ما ستتعلمه**
> - كيفية إعداد Aspose.Cells في مشروع .NET  
> - كيفية **استيراد datatable إلى excel** باستخدام مصفوفة الأنماط  
> - كيفية **إضافة تنسيق رقم excel** لعمود محدد  
> - نصائح للتعامل مع أعمدة إضافية أو لغات محلية مختلفة  

> **المتطلبات المسبقة**  
> - .NET 6+ (أو .NET Framework 4.6+) مثبتة  
> - حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
> - إلمام أساسي بـ C# وDataTables  

---

## الخطوة 1: إعداد DataTable (import datatable to excel)

أولاً، نحتاج إلى بعض البيانات التجريبية. في تطبيق حقيقي قد تملأ هذا الجدول من استعلام قاعدة بيانات، لكن المثال المدمج يبقي الأمور بسيطة.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*لماذا هذا مهم*: `DataTable` هو الجسر بين بيانات عملك وملف Excel. يمكن لـ Aspose.Cells استيراده مباشرةً، مع الحفاظ على أسماء الأعمدة وأنواع البيانات.

---

## الخطوة 2: إنشاء مصنف جديد (create excel workbook c#)

الآن ننشئ كائن ملف Excel الفعلي. فكر فيه كقماش فارغ سترسم عليه.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **نصيحة محترف:** إذا كنت بحاجة إلى عدة أوراق، استدعِ `workbook.Worksheets.Add()` وأعط كل واحدة اسمًا ذا معنى.

---

## الخطوة 3: تعريف نمط العملة (format cells currency)

يتيح لك Aspose.Cells إنشاء كائن `Style` يصف مظهر الخلايا. للعملة نستخدم معرف تنسيق الرقم المدمج 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*لماذا لا نكتفي بتعيين سلسلة التنسيق؟* استخدام المعرف المدمج يضمن التوافق عبر إصدارات Excel ويتجنب المشكلات الخاصة باللغات.

---

## الخطوة 4: بناء مصفوفة الأنماط (apply currency format column)

عند استيراد `DataTable`، يمكنك تمرير مصفوفة من كائنات `Style`—واحدة لكل عمود. `null` يعني “استخدام النمط الافتراضي”. هنا نطبق `priceStyle` فقط على العمود الثاني.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

إذا أضفت أعمدة أخرى لاحقًا، ما عليك سوى توسيع المصفوفة وفقًا لذلك. يجب أن يكون طول `columnStyles` مساويًا لعدد الأعمدة التي تستوردها، وإلا سيُطلق Aspose استثناءً.

---

## الخطوة 5: استيراد DataTable مع الأنماط (import datatable to excel)

الآن يحدث السحر—`DataTable` يهبط في ورقة العمل، وعمود السعر يُظهر فورًا كعملة.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*ماذا لو كان لديك أكثر من عمودين؟* فقط وسّع `columnStyles` بحيث يحصل كل عمود على النمط المناسب (أو `null` للافتراضي). هذه هي الطريقة الأنظف لـ **إضافة تنسيق رقم excel** بشكل انتقائي.

---

## الخطوة 6: حفظ المصنف (create excel workbook c#)

أخيرًا، نكتب الملف إلى القرص. اختر أي مجلد لديك صلاحية كتابة فيه.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

افتح `StyledTable.xlsx` في Excel وسترى:

| المنتج | السعر |
|--------|-------|
| تفاح   | $1.23 |
| موز    | $0.78 |
| كرز    | $2.50 |

عمود **السعر** مُنسق بالفعل كعملة—لا حاجة لأي خطوات إضافية.

---

## الحالات الخاصة والاختلافات

### أعمدة أكثر، تنسيقات مختلفة

إذا كنت بحاجة إلى **تنسيق خلايا العملة** لعدة أعمدة (مثل التكلفة، الضريبة، الإجمالي)، أنشئ `Style` منفصل لكل منها واملأ `columnStyles` وفقًا لذلك:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### عملة خاصة بالمنطقة

لليورو أو الجنيه الإسترليني، استخدم معرفات مدمجة مختلفة (مثلاً 165 لـ `€#,##0.00`). بدلاً من ذلك، عيّن سلسلة تنسيق مخصصة:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### مجموعات بيانات ضخمة

يمكن لـ Aspose.Cells التعامل مع ملايين الصفوف، لكن استهلاك الذاكرة يزداد مع كائنات الأنماط. أعد استخدام كائن `Style` واحد لجميع أعمدة العملة لتقليل البصمة.

### الأنماط المفقودة

إذا كان `columnStyles` أقصر من عدد الأعمدة، سيطبق Aspose النمط الافتراضي على الأعمدة المتبقية. هذا مفيد عندما يهمك تنسيق عدد قليل فقط من الأعمدة.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في تطبيق console. يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى بعض التعليقات المفيدة.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**النتيجة المتوقعة:** فتح `StyledTable.xlsx` يظهر عمود `السعر` مع علامة الدولار ومكانين عشريين، تمامًا كما طلبت تعليمات **تنسيق خلايا العملة**.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع .NET Core؟**  
ج: بالتأكيد. Aspose.Cells متوافق مع .NET‑standard، لذا يمكنك استهداف .NET 5، .NET 6 أو أحدث دون تغييرات.

**س: ماذا لو كان لدي DataTable يحتوي على 10 أعمدة وأريد تنسيق العمود الخامس فقط؟**  
ج: أنشئ `Style[]` بطول 10، املأ المواضع 0‑4 و 6‑9 بـ `null`، وضع نمطك المخصص في الفهرس 4 (صفر‑مبني). سيتبع Aspose كل إدخال.

**س: هل يمكن إخفاء صف العناوين؟**  
ج: بعد الاستيراد، عيّن `worksheet.Cells.Rows[0].Hidden = true;` أو ببساطة مرّر `false` للمعامل `includeColumnNames` في `ImportDataTable`.

---

## الخلاصة

لقد **أنشأنا مصنف Excel باستخدام C#**، استوردنا `DataTable`، و**طبقنا تنسيق عملة على عمود** باستخدام Aspose.Cells. الخطوات الأساسية—تحضير البيانات، تعريف النمط، بناء مصفوفة الأنماط، الاستيراد عبر `ImportDataTable`، والحفظ—تشكل جوهر معظم مهام أتمتة Excel.

من هنا يمكنك استكشاف:

- **إضافة تنسيق رقم excel** للتواريخ أو النسب المئوية  
- تصدير أوراق عمل متعددة في ملف واحد  
- استخدام **تنسيق خلايا العملة** مع رموز خاصة بالمنطقة  
- أتمتة إنشاء المخططات بناءً على نفس البيانات  

جرّب ذلك، وستصبح الشخص المرجعي لتقارير Excel في فريقك. هل لديك تعديل ترغب بمشاركته؟ اترك تعليقًا أدناه—برمجة سعيدة!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}