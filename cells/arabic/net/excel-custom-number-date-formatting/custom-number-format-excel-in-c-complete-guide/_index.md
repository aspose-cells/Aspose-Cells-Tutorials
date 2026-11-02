---
category: general
date: 2026-03-22
description: دروس تنسيق الأرقام المخصص في إكسل توضح كيفية استيراد جدول البيانات إلى
  إكسل، وتعيين لون خلفية العمود، وتنسيق العمود كعملة، وحفظ المصنف بصيغة xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: ar
og_description: دليل Excel لتنسيق الأرقام المخصص يشرح لك خطوة بخطوة استيراد DataTable،
  ضبط لون خلفية العمود، تنسيق العمود كعملة، وحفظ المصنف بصيغة xlsx.
og_title: تنسيق الأرقام المخصص في Excel باستخدام C# – دليل خطوة بخطوة
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: تنسيق الأرقام المخصص في إكسل باستخدام C# – دليل كامل
url: /ar/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنسيق الأرقام المخصص في Excel – دليل C# كامل‑المكدس

هل تساءلت يومًا كيف تطبق **custom number format excel** مباشرةً من C#؟ ربما حاولت تصدير DataTable إلى جدول بيانات ورأيت أرقامًا عادية، بدون ألوان، وبدون تنسيق عملة. هذه مشكلة شائعة—خصوصًا عندما تحتاج إلى تقرير مصقول لأصحاب المصلحة.

في هذا الدليل سنحل هذه المشكلة معًا: ستتعلم كيف **import datatable to excel**، **set column background color**، **format column as currency**، وأخيرًا **save workbook as xlsx** باستخدام تنسيق أرقام مخصص يجعل أرقامك بارزة. لا مراجع غامضة، فقط حل كامل قابل للتنفيذ يمكنك نسخه‑ولصقه في مشروعك.

---

## ما ستبنيه

بنهاية هذا البرنامج التعليمي ستحصل على تطبيق Console في C# مستقل يقوم بـ:

1. استرجاع `DataTable` (يمكنك استبدال النموذج بالاستعلام الخاص بك).  
2. إنشاء مصنف Excel جديد باستخدام Aspose.Cells (أو أي مكتبة متوافقة).  
3. تطبيق خط أزرق وعريض على العمود الأول، خلفية أصفر فاتح على العمود الثاني، وتنسيق عملة (`$#,##0.00`) على العمود الثالث.  
4. حفظ الملف باسم `DataTableWithStyleArray.xlsx` في المجلد الذي تختاره.

سترى بالضبط كيف يساهم كل سطر في الملف النهائي، وسنناقش لماذا هذه الاختيارات مهمة من حيث الصيانة والأداء.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).  
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو مرخصة). التثبيت عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

- إلمام أساسي بـ `DataTable` وتطبيقات Console في C#.

---

## الخطوة 1: استرجاع البيانات المصدرية كـ DataTable

أولًا، نحتاج إلى بعض البيانات لتصديرها. في سيناريو واقعي ربما تستدعي مستودعًا أو تنفذ استعلام SQL. للتوضيح سننشئ جدولًا بسيطًا في الذاكرة.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **لماذا هذا مهم:** استخدام `DataTable` يمنحك مصدرًا جدوليًا واعيًا بالمخطط يتطابق بسهولة مع صفوف وأعمدة Excel. كما يتيح لك إعادة استخدام منطق التصدير نفسه لأي مجموعة بيانات دون الحاجة لإعادة كتابة الكود.

---

## الخطوة 2: إنشاء مصنف جديد والحصول على الورقة الأولى

الآن نقوم بإنشاء مصنف Excel. تمثل فئة `Workbook` الملف بالكامل؛ و`Worksheets[0]` هي الورقة الافتراضية التي سنضع فيها بياناتنا.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى أوراق متعددة، ما عليك سوى استدعاء `workbook.Worksheets.Add("SheetName")` وتكرار خطوات التنسيق لكل ورقة.

---

## الخطوة 3: تعريف أنماط الأعمدة – الخط، الخلفية، وتنسيق الرقم

التنسيق في Aspose.Cells يتم عبر كائنات `Style`. سنبني مصفوفة حيث كل عنصر يمثل نمط عمود في الـ DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **لماذا مصفوفة الأنماط؟** تمرير مصفوفة إلى `ImportDataTable` يتيح لك تطبيق نمط مميز لكل عمود في استدعاء واحد، مما يجعل العملية مختصرة وفعّالة. كما يضمن بقاء التنسيق متزامنًا مع ترتيب البيانات.

---

## الخطوة 4: استيراد DataTable مع تطبيق الأنماط

هذا هو جوهر العملية: نمرر `DataTable` إلى الورقة، نخبر Aspose بتضمين صف العنوان، ونعطيه مصفوفة `columnStyles` الخاصة بنا.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **ماذا يحدث خلف الكواليس؟** يقوم Aspose بالتكرار عبر كل عمود، يكتب عنوان العمود، ثم يكتب قيم كل صف. أثناء ذلك يطبق النمط المقابل من المصفوفة، لذا ستحصل على عنوان أزرق لـ “Product”، خلفية صفراء لـ “Quantity”، وعمود “Revenue” بتنسيق عملة جميل.

---

## الخطوة 5: حفظ المصنف كملف XLSX

أخيرًا، نقوم بحفظ المصنف على القرص. تختار طريقة `Save` تنسيق XLSX تلقائيًا بناءً على امتداد الملف.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **نصيحة:** إذا كنت بحاجة إلى بث الملف (مثلاً في API ويب)، استخدم `workbook.Save(stream, SaveFormat.Xlsx)` بدلاً من مسار الملف.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع Console جديد. يترجم ويعمل مباشرةً، وينتج ملف Excel منسق.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### النتيجة المتوقعة

عند فتح `DataTableWithStyleArray.xlsx` ستظهر لك:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

التنسيق **custom number format excel** الذي حددته (`$#,##0.00`) يضمن أن كل خلية إيرادات تعرض علامة الدولار، فاصل الآلاف، واثنين من الأرقام العشرية—تمامًا ما تتوقعه الفرق المالية.

---

## الأسئلة المتكررة والحالات الخاصة

### هل يمكنني استخدام هذا مع مكتبة Excel مختلفة؟

بالتأكيد. الفكرة—إنشاء نمط لكل عمود وتطبيقه أثناء الاستيراد—قابلة للتحويل إلى EPPlus أو ClosedXML أو NPOI. تختلف استدعاءات الـ API، لكن النمط يبقى نفسه.

### ماذا لو كان لدى DataTable أعمدة أكثر من الأنماط؟

سيطبق Aspose النمط الافتراضي على أي عمود لا يملك مدخلًا مطابقًا في مصفوفة `columnStyles`. لتجنب المفاجآت، إما احرص على أن يكون حجم المصفوفة مساويًا لـ `dataTable.Columns.Count` أو أنشئ الأنماط ديناميكيًا داخل حلقة.

### كيف أضبط تنسيق رقم مخصص للتواريخ؟

ما عليك سوى تعيين `style.Custom = "dd‑mm‑yyyy"` (أو أي سلسلة تنسيق Excel صالحة). نفس النهج القائم على المصفوفة يعمل مع التواريخ، النسب المئوية، أو الصيغة العلمية.

### هل هناك طريقة لضبط عرض الأعمدة تلقائيًا بعد الاستيراد؟

نعم—استدعِ `worksheet.AutoFitColumns();` بعد عملية الاستيراد. يقوم بحساب العرض المناسب بناءً على محتوى الخلايا.

### ماذا عن مجموعات البيانات الكبيرة (100k+ صف)?

`ImportDataTable` مُحسّن للعمليات الضخمة، لكن قد تواجه حدود الذاكرة. في هذه الحالة، فكر في تدفق الصفوف يدويًا باستخدام `Cells[i, j].PutValue(...)` وإعادة استخدام كائن `Style` واحد لتقليل الحمل.

---

## نصائح احترافية ومخاطر شائعة

- **تجنب كتابة المسارات صراحةً** في الكود الإنتاجي؛ استخدم `Environment.GetFolderPath` أو إعدادات التكوين.  
- **حرّر المصنف** إذا كان التطبيق يعمل لفترة طويلة—ضعه داخل كتلة `using` لتحرير الموارد الأصلية.  
- **انتبه للفواصل الخاصة بالثقافات**. التنسيق المخصص `$#,##0.00` يفرض نقطة كفاصل عشري بغض النظر عن إعدادات نظام التشغيل، وهذا عادة ما يكون مطلوبًا للتقارير المالية.  
- **تأكد من الإشارة إلى System.Drawing** (أو `System.Drawing.Common` على .NET Core) لاستخدام هياكل اللون في التنسيق.  
- **اختبر الناتج على إصدارات Excel مختلفة**؛ قد تفسر الإصدارات القديمة بعض التنسيقات المخصصة بشكل مختلف قليلًا.

---

## الخلاصة

لقد غطينا كل ما تحتاجه لتطبيق **custom number format excel** من خلال C#: استخراج البيانات من `DataTable`، **import datatable to excel**، تطبيق **set column background color**، استخدام **format column as currency**، وأخيرًا **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}