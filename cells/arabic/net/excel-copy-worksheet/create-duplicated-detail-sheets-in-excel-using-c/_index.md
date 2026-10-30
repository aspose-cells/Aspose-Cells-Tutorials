---
category: general
date: 2026-10-07
description: إنشاء أوراق تفاصيل مكررة في Excel باستخدام C#. تعلّم كيفية إنشاء عدة
  أوراق عمل وبناء تقرير من الجداول في تشغيل واحد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: ar
lastmod: 2026-10-07
og_description: إنشاء أوراق تفاصيل مكررة في Excel باستخدام C#. يوضح هذا الدرس كيفية
  إنشاء عدة أوراق عمل وإنتاج تقرير Excel كامل من الجداول.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: إنشاء أوراق تفاصيل مكررة في إكسل – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: إنشاء أوراق تفاصيل مكررة في Excel باستخدام C#
url: /ar/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء أوراق تفاصيل مكررة في Excel باستخدام C#

إذا كنت بحاجة إلى **إنشاء أوراق تفاصيل مكررة** في مصنف Excel، فإن هذا الدليل يشرح لك العملية بالكامل. ستتعرف على كيفية **إنشاء أوراق عمل متعددة** من مجموعة بيانات رئيسية‑تفصيلية وإنتاج تقرير Excel مصقول مباشرةً من الجداول.

إنشاء تقرير Excel من الجداول هو طلب شائع لأنظمة الفوترة، لوحات معلومات المخزون، أو أي سيناريو يكون فيه سجل رئيسي يحتوي على عدة صفوف تفصيلية مرتبطة. بنهاية هذا البرنامج التعليمي ستحصل على برنامج C# قابل للتنفيذ يقوم بإنشاء مصنف يحتوي على ورقة رئيسية وورقة مسماة بشكل فريد لكل مجموعة تفاصيل.

## المتطلبات الأساسية

قبل أن تبدأ، تأكد من وجود:

* .NET 6.0 (أو أحدث) مثبت  
* Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#  
* حزمة **Aspose.Cells for .NET** NuGet (توفر `SmartMarkerProcessor`)  

يمكنك إضافة الحزمة بالأمر التالي:

```bash
dotnet add package Aspose.Cells
```

## نظرة عامة على الحل

يتبع الحل الخطوات الخمس التالية:

1. **الحصول على مصدر البيانات** الذي يحتوي على جدول رئيسي وجدولين تفصيليين.  
2. **تكوين معالج Smart‑marker** بحيث يحصل كل ورقة تفاصيل مكررة على اسم فريد.  
3. **إنشاء مصنف جديد** ووضع علامة Smart‑marker تشير إلى جدول الـ Master.  
4. **تشغيل المعالج** لإنشاء ورقة الـ Master وجميع أوراق التفاصيل.  
5. **حفظ المصنف** – كل ورقة تفاصيل الآن تحمل اسماً مميزاً.

يتم شرح كل خطوة بالتفصيل أدناه، مع الكود الكامل والتبرير.

## الخطوة 1: الحصول على مصدر البيانات الذي يحتوي على جدول رئيسي وجدولين تفصيليين

المهمة الأولى هي بناء `DataSet` يحاكي البيانات التي ستستخرجها عادةً من قاعدة البيانات. يجب أن يحتوي `DataSet` على جدول اسمه **Master** وجدول أو أكثر اسمه **Detail**. يستخدم محرك Smart‑marker أسماء هذه الجداول كعلامات يمكن استبدالها.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**لماذا هذا مهم:**  
*Smart‑marker* يعمل مع كائنات `DataSet`؛ كل اسم جدول يصبح علامة يمكن للمحرك استبدالها. من خلال هيكلة البيانات بهذه الطريقة يمكنك تمكين المعالج من تكرار ورقة التفاصيل تلقائياً لكل `InvoiceId` مميز.

## الخطوة 2: تكوين معالج Smart‑marker لإعطاء كل ورقة تفاصيل مكررة اسمًا فريدًا

عند مواجهة المعالج لعلامة تفاصيل، ينشئ ورقة عمل جديدة لكل مجموعة صفوف. بشكل افتراضي، تحمل الأوراق الجديدة نفس الاسم، مما يسبب تعارضًا في التسمية. ضبط `DetailSheetNewName` يخبر المحرك كيف يعيد تسمية كل نسخة.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**لماذا هذا مهم:**  
بدون نمط تسمية فريد، سيتسبب المصنف في استثناء عندما يحاول المعالج إضافة ورقة تفاصيل ثانية. العنصر النائب `{0}` يضمن أن كل ورقة تحصل على اسم مميز ومتوقع.

## الخطوة 3: إنشاء مصنف جديد ووضع علامة Smart‑marker تشير إلى جدول الـ Master

الآن تقوم بإنشاء `Workbook` جديد، وتضيف علامة تشير إلى جدول **Master**، ويمكنك تنسيق صف الرأس اختياريًا.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**لماذا هذا مهم:**  
العلامة `{{Master}}` توجه المعالج لتوسيع جدول الـ Master بدءًا من `A1`. الصفوف التالية تصبح صفوف البيانات لكل سجل رئيسي. هذا هو نقطة الانطلاق لـ **generate excel report from tables**.

## الخطوة 4: تشغيل معالج Smart‑marker لإنشاء ورقة الـ Master وأوراق التفاصيل

مع وجود مصدر البيانات، المعالج، والقالب جاهزين، تستدعي `Process`. يقوم المحرك بتوسيع علامة الـ Master، ثم إنشاء ورقة تفاصيل منفصلة لكل `InvoiceId` مميز.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**لماذا هذا مهم:**  
`processor.Process` يقوم بالعمل الشاق: يقرأ صفوف الـ master، ينشئ ورقة تفاصيل لكل مفتاح فريد، ويعيد تسمية تلك الأوراق وفق النمط المحدد مسبقًا. النتيجة هي مصنف يفي بمتطلب **how to generate multiple worksheets**.

## الخطوة 5: حفظ المصنف الناتج – كل ورقة تفاصيل الآن تحمل اسمًا مميزًا

استدعاء `Save` يكتب الملف إلى القرص. عند فتح المصنف، ستلاحظ:

* **Sheet1** – ورقة الـ master التي تحتوي على رؤوس الفواتير.  
* **Detail_1**, **Detail_2**, … – كل ورقة تحتوي على الصفوف من جدول **Detail** التي تخص فاتورة معينة.

فيما يلي نموذج تخطيط المصنف المتوقع (الصورة توضيحية؛ يمكنك استبدالها بلقطة شاشة فعلية إذا رغبت).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### النتيجة المتوقعة

| اسم الورقة | وصف المحتوى |
|------------|----------------------|
| **Sheet1** | صفوف رئيسية: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | صفوف تفاصيل حيث `InvoiceId = 101` |
| **Detail_2** | صفوف تفاصيل حيث `InvoiceId = 102` |

فتح `DuplicatedDetailSheets.xlsx` يجب أن يظهر هذا الهيكل بالضبط.

## الكود الكامل (جاهز للنسخ)



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تسمية الأوراق تلقائيًا – إنشاء أوراق متعددة في C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [كيفية إنشاء أوراق العمل – دليل خطوة بخطوة لإنشاء Excel ديناميكي](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [كيفية إنشاء تقرير Excel في C# – دليل كامل باستخدام SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}