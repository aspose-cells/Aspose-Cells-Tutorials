---
category: general
date: 2026-09-24
description: إنشاء دفتر عمل Excel برمجياً وتعلم كيفية إنشاء عدة أوراق تفصيلية، ثم
  حفظ دفتر العمل كملف xlsx مع مثال واضح بلغة C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: ar
lastmod: 2026-09-24
og_description: إنشاء مصنف إكسل برمجياً، شاهد كيفية إنشاء أوراق تفصيلية متعددة وحفظ
  المصنف كملف xlsx في مثال واحد قابل للتنفيذ.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: إنشاء دفتر عمل إكسل برمجيًا – دليل كامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: إنشاء مصنف إكسل برمجيًا باستخدام العلامات الذكية
url: /ar/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel برمجيًا باستخدام Smart Markers

إذا كنت بحاجة إلى **إنشاء مصنف Excel برمجيًا**، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Aspose.Cells .NET. ستكتشف أيضًا **كيفية إنشاء عدة أوراق تفصيلية** من مصدر بيانات واحد وأخيرًا **حفظ المصنف كملف xlsx** دون أي خطوات يدوية.  

الحل مكتمل ذاتيًا: نستعرض كل سطر من الكود، نشرح لماذا كل إعداد مهم، ونغطي المشكلات الشائعة مثل تكرار أسماء الأوراق. في النهاية ستحصل على تطبيق وحدة تحكم جاهز للتنفيذ ينتج مصنفًا يحتوي على ورقة رئيسية ومجموعة من الأوراق التفصيلية.

## ما ستحتاجه

| المتطلبات المسبقة | السبب |
|------------------|--------|
| .NET 6.0 SDK or later | يوفر بيئة التشغيل لتطبيق وحدة التحكم C# |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | يوفر الفئات `Workbook` و `SmartMarkerProcessor` و `SmartMarkerOptions` |
| A simple data source (e.g., `DataTable` or a list of objects) | مصدر بيانات بسيط (مثل `DataTable` أو قائمة من الكائنات) |
| Visual Studio 2022 or any editor that supports .NET | يجعل من السهل تجميع وتشغيل الكود |

> **نصيحة احترافية:** قم بتثبيت حزمة Aspose.Cells عبر سطر الأوامر قبل البدء:  
> `dotnet add package Aspose.Cells`

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ مشروع وحدة تحكم جديد واستورد المساحات الاسمية المطلوبة.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*لماذا هذا مهم*: `Aspose.Cells` يتعامل مع دورة حياة المصنف، بينما `Aspose.Cells.SmartMarkers` يزودك بمحرك Smart Marker القوي الذي يمكنه إنشاء العديد من الأوراق من قالب واحد.

## الخطوة 2: إنشاء مصنف Excel برمجيًا

الإجراء الأول هو إنشاء كائن `Workbook`. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

إذا كنت تفضل البدء من قالب يحتوي بالفعل على صفوف رأس أو تنسيق، استبدل `new Workbook()` بـ `new Workbook("Template.xlsx")`. باقي العملية يعمل بنفس الطريقة.

## الخطوة 3: إعداد قالب Smart Marker

يعمل Smart Markers على محتويات الخلايا التي تحتوي على نواقل مثل `&=Employees.Name`. في هذا الشرح سنضيف قالبًا بسيطًا مباشرة عبر الكود، ولكن يمكنك أيضًا تعديل الورقة يدويًا في Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*لماذا هذا مهم*: الناقل `&=Employees.Name` يخبر معالج Smart Marker بالتكرار عبر مجموعة `Employees`. كل تكرار سينتج ورقة عمل جديدة لأننا سنقوم بتكوين المعالج لإنشاء **ورقة تفصيلية** لكل صف.

## الخطوة 4: بناء مصدر بيانات يحتوي على عدة صفوف

سنستخدم `DataTable` كطريقة سريعة لمحاكاة مجموعة من سجلات الموظفين.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

يمكنك استبدال ذلك بأي `IEnumerable` (مثل `List<Employee>`) – يقبل Smart Markers أي مصدر بيانات ينفذ `IEnumerable`.

## الخطوة 5: تكوين خيارات Smart Marker – كيفية إنشاء عدة أوراق تفصيلية

بشكل افتراضي، يكتب Smart Markers البيانات مرة أخرى إلى نفس الورقة. لإنشاء **عدة أوراق تفصيلية**، يجب تعيين خاصية `DetailSheetNewName`. هذا يوضح أيضًا **كيفية إنشاء عدة أوراق تفصيلية** دون تعارضات في الأسماء.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

إذا كان مصدر البيانات يحتوي على أسماء مكررة، يضيف المعالج تلقائيًا لاحقة رقمية (مثل `Detail_1`، `Detail_2`). هذا يمنع أخطاء وقت التشغيل ويضمن حفظ جميع الأوراق التفصيلية.

## الخطوة 6: معالجة Smart Markers

الآن نستدعي المعالج، مع تمرير مصدر البيانات والخيارات التي عرّفناها للتو.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*لماذا هذا مهم*: يقرأ المعالج الناقل `&=Employees.Name`، يتكرر على كل صف من `employees`، ينشئ ورقة جديدة تسمى “Detail”، ويكتب بيانات الصف في تلك الورقة. تظل الورقة الأصلية كملخص أو ورقة رئيسية.

## الخطوة 7: حفظ المصنف كملف xlsx

أخيرًا، احفظ المصنف على القرص باستخدام نمط **حفظ المصنف كملف xlsx**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

تضمن قيمة التعداد `SaveFormat.Xlsx` أن يتم تخزين الملف بصيغة Office Open XML الحديثة، والتي تتوافق مع Excel 2007+ ومعظم الخدمات السحابية.

## مثال كامل قابل للتنفيذ

انسخ الشيفرة التالية إلى `Program.cs` في مشروع وحدة تحكم .NET وشغّله. سيولد البرنامج ملف `detail.xlsx` في مجلد `output`، يحتوي على ورقة رئيسية واحدة وثلاث أوراق تفصيلية (واحدة لكل موظف).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**المخرجات المتوقعة**

- `output/detail.xlsx` يحتوي على:
  - **Sheet1** – القالب الأصلي مع العنوان “Employee Report”.
  - **Detail** – أول ورقة تفصيلية مع سجل Alice.
  - **Detail_1** – ورقة تفصيلية ثانية مع سجل Bob.
  - **Detail_2** – ورقة تفصيلية ثالثة مع سجل Carol.

افتح الملف في Excel وسترى كل موظف في ورقة خاصة به، مما يثبت أننا نجحنا في **إنشاء عدة أوراق تفصيلية** و**حفظ المصنف كملف xlsx**.

## أسئلة شائعة ومعالجة الحالات الخاصة

| السؤال | الإجابة |
|--------|----------|
| *ماذا لو احتجت إلى اسم مخصص لكل ورقة تفصيلية؟* | قم بتعيين `DetailSheetNewName = "Employee_"` وأدرج عمودًا باسم `SheetName` في مصدر البيانات. سيضيف المعالج قيمة `SheetName` إلى الاسم الأساسي. |
| *هل يمكنني الاحتفاظ بالورقة الأصلية كملخص لجميع التفاصيل؟* | نعم. تظل الورقة الرئيسية دون تعديل؛ يمكنك إضافة صيغ تشير إلى الأوراق التفصيلية التي تم إنشاؤها. |
| *ماذا يحدث عندما يكون مصدر البيانات فارغًا؟* | لن يتم إنشاء أي أوراق تفصيلية، لكن المصنف لا يزال يُحفظ. فكر في التحقق من `employees.Rows.Count` قبل المعالجة إذا كنت بحاجة إلى معالجة خاصة. |
| *هل يمكن استخدام ملف قالب موجود؟* | استبدل `new Workbook()` بـ `new Workbook("Template.xlsx")`. جميع منطق Smart Marker يعمل بنفس الطريقة. |

## الخلاصة

أنت الآن تعرف **كيفية إنشاء مصنف Excel برمجيًا**، وكيفية **إنشاء عدة أوراق تفصيلية** باستخدام Smart Markers، وكيفية **حفظ المصنف كملف xlsx** باستخدام Aspose.Cells. يمكن تعديل المثال الكامل للفواتير أو التقارير أو أي سيناريو يتطلب مخرجات Excel بنظام رئيس‑تفصيل.

### الخطوات التالية

- استكشف ميزات Smart Marker الأخرى مثل **group markers** و **conditional formatting**.  
- استبدل `DataTable` باستعلام قاعدة بيانات حقيقي لتوليد تقارير على نطاق واسع.  
- استخدم `Workbook.Save("output.pdf", SaveFormat.Pdf)` لتصدير نفس البيانات إلى PDF للتوزيع.

لا تتردد في تجربة أنماط تسمية مختلفة أو تنسيق أو أوراق عمل إضافية—مهاراتك الجديدة في إنشاء Excel برمجيًا جاهزة للاستخدام في الإنتاج. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف Excel C# – إضافة تعليق وحفظ كـ XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [إنشاء مصنف جديد في C# – إضافة صيغة وحفظ ملف Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [إنشاء مصنف Excel C# – إدراج JSON وحفظ كـ XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}