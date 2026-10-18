---
category: general
date: 2026-07-13
description: تنسيق عمود التاريخ في Excel أثناء تصدير DataTable من C#. تعلم تصدير DataTable
  إلى Excel باستخدام C# واستيراد DataTable إلى Excel مع التنسيق في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: ar
lastmod: 2026-07-13
og_description: تنسيق عمود التاريخ في إكسل بسهولة. يوضح لك هذا الدليل كيفية تصدير
  جدول البيانات إلى إكسل باستخدام C# واستيراد جدول البيانات إلى إكسل مع أنماط مخصصة.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: تنسيق عمود التاريخ في Excel – دليل تصدير خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: تنسيق عمود التاريخ في إكسل – دليل C# الكامل لتصدير DataTable
url: /ar/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنسيق عمود التاريخ في Excel – دليل C# كامل لتصدير DataTable

هل احتجت يومًا إلى **format date column Excel** عند سحب البيانات من قاعدة بيانات، لكن الخلايا كانت تُظهر الطوابع الزمنية الخام؟ لست وحدك. في العديد من تطبيقات الأعمال، التصدير الافتراضي يُخرج قيمة `DateTime` مثل `2024‑03‑15 00:00:00` ولا أحد يريد هذا الفوضى.  

الخبر السار هو أنه يمكنك التحكم بالمظهر الدقيق لكل عمود مباشرةً من C#. في هذا الدرس سنستعرض حلًا شاملاً يطبق **excel export datatable c#**، يضيف نمط تاريخ للعمود الأول، ونمط عملة للعمود الثاني، وأخيرًا **import datatable to excel** مع تنسيق بلا عناء.

بنهاية الشرح ستحصل على طريقة قابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع .NET، بغض النظر عما إذا كنت تستخدم .NET 6 أو .NET Framework 4.8 أو إصدارًا أحدث.

---

## ما ستحتاجه

- **Aspose.Cells for .NET** (أو أي مكتبة توفر `CreateStyle` و `ImportDataTable`). تستخدم مقتطفات الشيفرة Aspose لأن واجهتها البرمجية (API) نظيفة ومُعتمدة على نطاق واسع.
- **DataTable** التي تقوم بملئها بالفعل من SQL أو CSV أو أي مصدر آخر.
- Visual Studio (أو بيئة التطوير المتكاملة المفضلة لديك).  
- .NET runtime 5.0+ (العينة تستهدف .NET 6، لكن الإطارات الأقدم تعمل بنفس الطريقة).

إذا لم تكن تمتلك Aspose.Cells بعد، احصل على نسخة تجريبية مجانية من الموقع الرسمي—بدون الحاجة لبطاقة ائتمان.

---

## الخطوة 1: استرجاع البيانات المصدر كـ DataTable

أولًا، تحتاج إلى `DataTable`. في السيناريوهات الواقعية عادةً ما يأتي من `SqlDataAdapter.Fill`، لكن لتوضيح الفكرة سنحاكي جدولًا بسيطًا:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **نصيحة احترافية:** عند سحب البيانات مباشرةً من إجراء مخزن، تأكد من أن أنواع الأعمدة تتطابق مع تنسيقات Excel المطلوبة. عمود `datetime` سيكون لاحقًا الهدف لنمط **format date column excel** الخاص بنا.

---

## الخطوة 2: إنشاء مصنف Excel وتعريف أنماط الأعمدة

الآن نقوم بإنشاء مصنف جديد. الحيلة لتطبيق **format date column excel** تكمن في إنشاء كائن `Style`، وضبط خاصية `Number` إلى تنسيق التاريخ المدمج في Excel (الرمز 14)، ثم إسناد هذا النمط إلى فهرس العمود المناسب.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

لماذا `Number = 14`؟ Excel يخزن التواريخ كأرقام تسلسلية؛ التنسيق 14 يُخبر البرنامج بعرض هذه الأرقام باستخدام نمط التاريخ القصير للمنطقة. إذا كنت تحتاج نمطًا مخصصًا (مثل `dd‑MMM‑yyyy`)، يمكنك تعيين `columnStyles[0].Custom = "dd-MMM-yyyy"` بدلاً من ذلك.

---

## الخطوة 3: استيراد DataTable إلى ورقة العمل مع الأنماط

مع جاهزية مصفوفة الأنماط، يصبح استدعاء الاستيراد سطرًا واحدًا. هذا هو جوهر **excel export datatable c#** وأيضًا المكان الذي نقوم فيه بـ **import datatable to excel** مع الحفاظ على تنسيقنا.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

الإصدار الزائد من `ImportDataTable` الذي نستخدمه يقبل مصفوفة الأنماط، ويطبق كل نمط على العمود المطابق أثناء كتابة البيانات. لا حاجة إلى حلقة معالجة لاحقة—عمود التاريخ الخاص بك مُنسق بالفعل بشكل جميل.

---

## الخطوة 4: حفظ المصنف (أو بثه مباشرةً إلى المتصفح)

اعتمادًا على السيناريو قد تحتاج إلى حفظ الملف على القرص، أو إلى تدفق ذاكرة، أو إرجاع الملف كاستجابة HTTP. إليك ثلاثة أنماط شائعة:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **احذر من:** إذا كنت تستخدم `FileResult` في ASP.NET Core، تأكد من ضبط `Response.Headers["Cache-Control"] = "no-cache"` عندما يتم إنشاء الملف في الوقت الفعلي. هذا يمنع المتصفح من تقديم نسخة قديمة.

---

## الخطوة 5: التحقق من النتيجة – شكل ورقة Excel

بعد تشغيل الشيفرة، افتح `ExportedReport.xlsx`. يجب أن ترى:

| تاريخ الطلب (منسق) | المبلغ الإجمالي (عملة) | العميل |
|-------------------|------------------------|--------|
| 03/13/2024        | $1,245.67              | Acme Corp|
| 03/14/2024        | $980.00                | Beta Ltd |
| 03/15/2024        | $1,500.25              | Gamma Inc|

لاحظ كيف أن **format date column excel** يعرض تاريخًا قصيرًا نظيفًا، بينما عمود العملة ينسق تلقائيًا وفقًا لإعدادات المنطقة الخاصة بك. لا حاجة لتنسيق يدوي خلية بخلية.

![format date column excel example](/images/format-date-column-excel.png)

*نص بديل للصورة: format date column excel – لقطة شاشة لورقة Excel مع عمود تاريخ منسق بشكل صحيح.*

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان لدى DataTable أكثر من ثلاثة أعمدة؟

فقط قم بتمديد مصفوفة `columnStyles`. لأي عمود لا تقوم بتنسيقه صراحةً، اترك القيمة `null`؛ سيطبق Excel التنسيق العام الافتراضي.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### كيف تطبق تنسيق تاريخ مخصص (مثال: “dd‑MMM‑yyyy”)؟

استبدل الرقم المدمج بسلسلة مخصصة:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### هل يمكنني استخدام هذا النهج مع EPPlus أو ClosedXML؟

نعم، المفهوم هو نفسه: إنشاء كائن نمط، إسناده إلى عمود، ثم تحميل `DataTable`. تختلف الواجهة البرمجية (API)، لكن نمط **excel export datatable c#** يبقى كما هو.

### ماذا عن مجموعات البيانات الكبيرة (أكثر من 100k صفًا)؟

`ImportDataTable` مُحسّن للكتابات الضخمة، لكن قد تواجه حدود الذاكرة. في هذه الحالة، فكر في بث الصفوف باستخدام `Cells.ImportDataTable` على دفعات، أو استخدم `Worksheet.Cells["A1"].PutValue` داخل حلقة مع إعادة استخدام كائنات النمط.

---

## مثال كامل يعمل (جميع الخطوات في طريقة واحدة)

فيما يلي طريقة مستقلة يمكنك نسخها ولصقها في أي تطبيق كونسول أو وحدة تحكم ASP.NET. تُظهر التدفق الكامل — من استرجاع البيانات إلى تصدير Excel المنسق.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

شغّل البرنامج، افتح `StyledExport.xlsx`، وسترى أن **format date column excel** تم تطبيقه بشكل مثالي.

---

## ملخص وخطوات قادمة

لقد غطينا للتو كيفية **format date column excel** عند إجراء **excel export datatable c#**، وكيفية **import datatable to excel** مع تنسيق كل عمود في استدعاء واحد. النقاط الرئيسية:

1. إنشاء كائن `Style` لكل عمود تريد تنسيقه.  
2. استخدام `Number = 14` للتواريخ، `Number = 2` للعملة، أو أي تنسيق مخصص تحتاجه.  
3. تمرير مصفوفة الأنماط إلى `ImportDataTable` — المكتبة تقوم بالعمل الشاق.

ماذا يمكنك استكشافه بعد ذلك؟

- **Conditional formatting** لتسليط الضوء على التواريخ المتأخرة.  
- **

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استيراد DataTable إلى Excel باستخدام Aspose.Cells for .NET (دليل خطوة بخطوة)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [تصدير بيانات Excel إلى DataTable باستخدام Aspose.Cells for .NET: دليل كامل](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [تصدير سلاسل HTML من Excel إلى DataTable باستخدام Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}