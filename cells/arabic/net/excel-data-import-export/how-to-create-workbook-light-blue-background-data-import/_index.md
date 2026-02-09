---
category: general
date: 2026-02-09
description: كيفية إنشاء دفتر عمل في C# بخلفية زرقاء فاتحة واستيراد البيانات مع العناوين.
  تعلم إضافة خلفية زرقاء فاتحة، واستخدام النمط الافتراضي لبرنامج Excel، واستيراد جدول
  البيانات.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: ar
og_description: كيفية إنشاء دفتر عمل في C# بخلفية زرقاء فاتحة، استيراد البيانات مع
  العناوين، وتطبيق النمط الافتراضي لبرنامج Excel—كل ذلك في دليل مختصر واحد.
og_title: كيفية إنشاء دفتر عمل – خلفية زرقاء فاتحة، استيراد البيانات
tags:
- C#
- Excel
- Aspose.Cells
title: كيفية إنشاء دفتر عمل – خلفية زرقاء فاتحة، استيراد البيانات
url: /ar/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء دفتر عمل – خلفية زرقاء فاتحة، استيراد البيانات

هل تساءلت يومًا **how to create workbook** في C# التي تبدو أكثر جاذبية مباشرةً من الصندوق؟ ربما سحبّت `DataTable` من قاعدة بيانات وتعبت من الخلايا البيضاء الافتراضية المملة. في هذا الدرس سنستعرض إنشاء دفتر عمل جديد، إضافة خلفية زرقاء فاتحة إلى عمود، واستيراد البيانات مع العناوين — كل ذلك باستخدام النمط الافتراضي الذي توفره Excel.

سنضيف أيضًا بعض سيناريوهات “ماذا لو”، مثل التعامل مع القيم الفارغة أو تخصيص أكثر من عمود واحد. في النهاية، ستحصل على ملف Excel مُنسق بالكامل يمكنك إرساله إلى أصحاب المصلحة دون أي معالجة لاحقة.

## المتطلبات المسبقة

* **.NET 6+** (الكود يعمل على .NET Framework 4.6+ أيضًا)  
* **Aspose.Cells for .NET** – المكتبة التي تدعم استدعاءات `Workbook` و `Style` و `ImportDataTable`. قم بتثبيتها عبر NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* مصدر `DataTable` – سنقوم بإنشاء واحد تجريبي في المثال، لكن يمكنك استبداله بأي استعلام ADO.NET.

هل لديك هذه المتطلبات؟ رائع، لنبدأ.

## الخطوة 1: تهيئة دفتر عمل جديد (الكلمة المفتاحية الأساسية)

أول شيء تحتاج إلى القيام به هو **how to create workbook** – حرفيًا. تمثل فئة `Workbook` ملف Excel بالكامل، ومُنشئها يمنحك صفحة فارغة.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **لماذا هذا مهم:** بدءًا بـ `Workbook` جديد يضمن لك التحكم في كل نمط من البداية. إذا فتحت ملفًا موجودًا، فستورث أي أنماط تركها المؤلف الأصلي، مما قد يؤدي إلى تنسيق غير متسق.

## الخطوة 2: إعداد الـ DataTable الذي ستستورده

لأغراض التوضيح، لننشئ `DataTable` بسيطًا. في السيناريوهات الواقعية ربما ستستدعي إجراء مخزن أو طريقة ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **نصيحة:** إذا كنت بحاجة للحفاظ على ترتيب الأعمدة تمامًا كما هو في قاعدة البيانات، اضبط معامل `importColumnNames` في `ImportDataTable` إلى `true`. هذا يخبر Aspose.Cells بكتابة عناوين الأعمدة لك.

## الخطوة 3: تعريف أنماط الأعمدة – الافتراضي + خلفية زرقاء فاتحة

الآن نجيب على جزء **add light blue background** من اللغز. تسمح لك Aspose.Cells بتمرير مصفوفة من كائنات `Style` التي تتطابق مع كل عمود تقوم باستيراده. الإدخال الأول هو النمط للعمود 0، والثاني للعمود 1، وهكذا. إذا كان لديك عدد أنماط أقل من عدد الأعمدة، فإن الأعمدة المتبقية ستعود إلى النمط الافتراضي.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **لماذا نمطين فقط؟** في مثالنا لدينا أربعة أعمدة، لكننا نريد فقط أن يبرز العمود الثاني (Name). لا يلزم أن يطابق طول المصفوفة عدد الأعمدة؛ أي مدخلات مفقودة ستورث تلقائيًا النمط الافتراضي للدفتر.

## الخطوة 4: استيراد الـ DataTable مع العناوين والأنماط

هنا نجمع بين **excel import datatable c#** و **import data with headers**. تقوم طريقة `ImportDataTable` بالعمل الشاق: تكتب أسماء الأعمدة، الصفوف، وتطبق مصفوفة الأنماط التي أنشأناها للتو.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### النتيجة المتوقعة

بعد تشغيل البرنامج، سيحتوي `workbook` على ورقة عمل واحدة تبدو هكذا:

| **ID** | **Name** (أزرق فاتح) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* عمود **Name** يحتوي على خلفية زرقاء فاتحة، مما يثبت أن مصفوفة الأنماط تعمل.  
* عناوين الأعمدة تُولد تلقائيًا لأننا مررنا `true` للمعامل `importColumnNames`.  
* القيم الفارغة تظهر كخلايا فارغة، وهذا هو السلوك الافتراضي لـ Aspose.Cells.

## الخطوة 5: حفظ دفتر العمل (اختياري لكن مفيد)

من المحتمل أنك تريد كتابة الملف إلى القرص أو بثه مرة أخرى إلى عميل ويب. الحفظ سهل ومباشر:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **نصيحة احترافية:** إذا كنت تستهدف إصدارات Excel القديمة، غيّر `SaveFormat.Xlsx` إلى `SaveFormat.Xls`. يتولى الـ API التحويل لك.

## حالات خاصة وتنوعات

### أعمدة متعددة مُنسقة

إذا كنت بحاجة إلى أكثر من عمود مُنسق، ببساطة قم بتوسيع مصفوفة `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

الآن سيصبح كل من **Name** و **Salary** باللون الأزرق الفاتح.

### تنسيق شرطي بدلاً من الأنماط الثابتة

أحيانًا تريد أن يتحول عمود إلى اللون الأحمر عندما تتجاوز القيمة عتبة معينة. هنا يأتي دور **use default style excel** مع التنسيق الشرطي:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### الاستيراد بدون عناوين

إذا كان نظامك اللاحق يوفر عناوينه الخاصة بالفعل، فقط مرّر `false` للمعامل `importColumnNames`. سيبدأ البيانات عند `A1` ويمكنك كتابة عناوين مخصصة لاحقًا.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## مثال كامل يعمل (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}