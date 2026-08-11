---
category: general
date: 2026-08-11
description: إنشاء ورقة إكسل من DataTable في C# وتصدير DataTable إلى إكسل مع تسمية
  ورقة تلقائية. تعلم كيفية إضافة صفوف إلى DataTable وحفظ المصنف بصيغة xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: ar
lastmod: 2026-08-11
og_description: إنشاء ورقة إكسل من DataTable في C#. يوضح هذا الدرس كيفية تصدير DataTable
  إلى إكسل، إضافة صفوف إلى DataTable، إنشاء عدة أوراق إكسل وحفظ المصنف بصيغة xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: إنشاء ورقة إكسل من DataTable في C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: إنشاء ورقة إكسل من DataTable في C# – دليل خطوة بخطوة
url: /ar/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ورقة إكسل من DataTable في C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إنشاء ورقة إكسل** من `DataTable` في C#، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعرف على كيفية **تصدير DataTable إلى إكسل**، إضافة الصفوف، التعامل مع أسماء الأوراق المكررة، وأخيرًا **حفظ المصنف كملف xlsx**.

يستخدم المثال Aspose.Cells، مكتبة .NET شائعة الاستخدام لأتمتة إكسل. تنطبق نفس المفاهيم على المكتبات الأخرى التي تدعم المعالجة بنمط SmartMarker، لكن الشيفرة أدناه تعمل مباشرةً مع Aspose.Cells 22.12 أو أحدث.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث مثبت  
* إشارة إلى حزمة NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* إلمام أساسي بـ `DataTable` وتطبيقات C# console  

هذه المتطلبات تجعل الدرس مستقلًا وتجنب الحاجة إلى أدوات خارجية.

## الخطوة 1: إنشاء DataTable سيتم تصديره إلى إكسل

الخطوة الأولى هي بناء `DataTable` يعكس البيانات التي تريدها في ورقة العمل. هنا نقوم بإنشاء جدول باسم **Sheet1**، نضيف عمود `Id`، ونُدرج صفين.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**لماذا هذا مهم:**  
`DataTable` هو تمثيل مريح للبيانات الجدولية في الذاكرة. تسمية الجدول بـ `"Sheet1"` تخبر Aspose.Cells أي ورقة تستهدف عند معالجة SmartMarkers.

## الخطوة 2: إضافة صفوف إلى DataTable (توسيع اختياري)

إذا كانت بيانات المصدر ديناميكية، ستحتاج غالبًا إلى إضافة صفوف داخل حلقة. المقتطف التالي يوضح نمطًا شائعًا:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**نصيحة:** عند إضافة عدد كبير من الصفوف، فكر في تعطيل القيود (`dataTable.Constraints.Clear()`) لتحسين الأداء.

## الخطوة 3: تكوين خيارات SmartMarker لإنشاء أوراق إكسل متعددة تلقائيًا

تتيح لك خيارات SmartMarker التحكم في كيفية معالجة أسماء الأوراق المكررة. ضبط `DetailSheetNewName` إلى `"Sheet1_{0}"` يخبر Aspose.Cells بإعادة تسمية الأوراق اللاحقة إلى `Sheet1_1`، `Sheet1_2`، وهكذا.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**لماذا هذا مهم:**  
عند معالجة عدة كائنات `DataTable` تشترك في نفس الاسم، عادةً ما يطرح إكسل خطأً لأن أسماء الأوراق يجب أن تكون فريدة. نمط `DetailSheetNewName` يزيل هذا التعارض تلقائيًا.

## الخطوة 4: معالجة SmartMarkers وتصدير DataTable إلى إكسل

الآن نقوم بإنشاء `Workbook` جديد، تشغيل `ProcessSmartMarkers`، والسماح لـ Aspose.Cells بملء ورقة (أوراق) العمل بناءً على `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**شرح:**  
`ProcessSmartMarkers` يفحص المصنف بحثًا عن علامات مثل `&=Sheet1!A1` (غير معروضة هنا) ويستبدلها بالبيانات من `dataTable`. لأننا بدأنا بمصنف فارغ، تقوم Aspose.Cells بإنشاء ورقة جديدة تتطابق مع اسم الجدول وتملأها بالصفوف التي أضفناها.

## الخطوة 5: حفظ المصنف كملف xlsx

أخيرًا، احفظ المصنف على القرص بصيغة OpenXML الحديثة (`.xlsx`). يمكنك تعديل المسار ليتناسب مع بيئتك.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**النتيجة:**  
تشغيل البرنامج ينتج ملف إكسل يحتوي على:

| اسم الورقة | الصفوف |
|------------|--------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (إذا تم معالجة DataTable آخر بنفس الاسم) |

منطق إعادة تسمية الأوراق يضمن **إنشاء أوراق إكسل متعددة** دون الحاجة لإدارة الأسماء يدويًا.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية التعامل |
|-----------|------------------|
| **جداول كبيرة جدًا** (≥ 100 000 صف) | استخدم `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` قبل المعالجة للحفاظ على استهلاك الذاكرة منخفضًا. |
| **ترتيب الأعمدة المخصص** | أعد ترتيب كائنات `DataColumn` في `DataTable` قبل استدعاء `ProcessSmartMarkers`. |
| **عدة DataTables بأسماء مختلفة** | استدعِ `ProcessSmartMarkers` لكل جدول؛ سيقوم Aspose.Cells بإنشاء ورقة منفصلة لكل اسم تلقائيًا. |
| **الحاجة إلى صف رأس مع تنسيق** | بعد المعالجة، احصل على `Worksheet.Cells["A1"]` وطبق خصائص `Style` (الخط، الخلفية). |
| **الحفظ إلى تدفق بدلاً من ملف** | استبدل `workbook.Save(outputPath, SaveFormat.Xlsx)` بـ `workbook.Save(stream, SaveFormat.Xlsx)`. |

**نصيحة احترافية:** احرص دائمًا على تغليف عمليات نظام الملفات داخل كتل `try…catch` للكشف عن مشاكل الأذونات مبكرًا.

## الشيفرة المصدرية الكاملة (جاهزة للنسخ)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### النتيجة المتوقعة

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

فتح `DuplicateSheets.xlsx` يُظهر ورقة باسم **Sheet1** تحتوي على عمود `Id` بالقيم `1, 2, 3, 4, 5`. إذا قمت لاحقًا بمعالجة `DataTable` آخر باسم `"Sheet1"` في نفس المصنف، سيقوم Aspose.Cells بإنشاء **Sheet1_1**، **Sheet1_2**، إلخ، تلقائيًا.

## الخلاصة

أنت الآن تعرف كيف **تنشئ ورقة إكسل** من `DataTable` في C#، **تصدّر DataTable إلى إكسل**، **تضيف صفوفًا إلى DataTable**، تُولّد **إنشاء أوراق إكسل متعددة** مع تسمية تلقائية، و**تحفظ المصنف كملف xlsx**. المثال الكامل القابل للتنفيذ يوضح سير العمل من البداية إلى النهاية ويقدم نصائح عملية لمجموعات البيانات الكبيرة والتنسيق المخصص.

### ما التالي؟

* استكشف **تنسيق الخلايا** (الخطوط، الألوان، الحدود) عبر الوصول إلى `Worksheet.Cells` بعد `ProcessSmartMarkers`.  
* استخدم **حلقات SmartMarker** لإنشاء تقارير رئيس‑تفصيل في مصنف واحد.  
* انتقل إلى **تصدير CSV** بتغيير `SaveFormat.Csv` إذا كنت بحاجة إلى تمثيل نصي بسيط.  

لا تتردد في تعديل الشيفرة لتتناسب مع مصادر بياناتك الخاصة—سواء كانت استعلام قاعدة بيانات، استجابة API، أو مجموعة في الذاكرة. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء وحفظ مصنف إكسل بصيغة ODS باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [كيفية إنشاء وحفظ مصنف إكسل بصيغة SVG باستخدام Aspose.Cells لـ Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [كيفية إنشاء وتصدير إكسل إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}