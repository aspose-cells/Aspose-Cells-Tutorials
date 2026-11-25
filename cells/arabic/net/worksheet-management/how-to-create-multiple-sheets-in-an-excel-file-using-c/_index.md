---
category: general
date: 2026-11-25
description: تعلم كيفية إنشاء عدة أوراق في ملف Excel باستخدام C#. يغطي هذا الدليل
  حفظ المصنف بصيغة XLSX ومعالجة أسماء الأوراق المكررة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: ar
lastmod: 2026-11-25
og_description: إنشاء عدة أوراق في ملف Excel باستخدام C#. اتبع هذا الدرس الكامل لحفظ
  المصنف كملف XLSX وإدارة أسماء الأوراق المكررة.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: إنشاء أوراق متعددة في ملف Excel باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: كيفية إنشاء عدة أوراق في ملف إكسل باستخدام C#
url: /ar/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء أوراق متعددة في ملف Excel باستخدام C#

إذا كنت بحاجة إلى **إنشاء أوراق متعددة** في مصنف Excel من C#، فإن هذا الدليل يقدّم لك حلاً جاهزًا للتنفيذ. بنهاية الشرح ستحصل على برنامج يولّد ورقة رئيسية، وينشئ أوراق تفصيلية عبر العلامات الذكية، ويحفظ النتيجة كملف **XLSX**—مع معالجة آمنة لأسماء الأوراق **المكررة**.

سترى أيضًا كيفية **إنشاء ملف Excel C#** باستخدام مكتبة Aspose.Cells، وهي خيار شائع لأتمتة الجداول على الخادم.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET)  
* حزمة **Aspose.Cells for .NET** من NuGet (`Aspose.Cells`) – توفر الفئات `Workbook`، `Worksheet`، و `SmartMarkersFactory` المستخدمة في الشيفرة.  

يمكنك إضافة الحزمة بالأمر التالي في سطر الأوامر:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** استخدم مستودع NuGet خاص أو النسخة المجانية للمجتمع إذا كنت تحتاج فقط إلى الميزات الأساسية.

## نظرة عامة على الحل

تتكون المقاربة من أربع خطوات منطقية:

1. **إنشاء مصنف جديد** وتسميته بالورقة الأولى *Master*.  
2. **إدراج علامة ذكية** تخبر Aspose.Cells كيف تُسمّى أوراق التفصيل.  
3. **معالجة العلامة الذكية** بمصدر بيانات قد يحتوي على أسماء مكررة.  
4. **حفظ المصنف** كملف XLSX.

يتم شرح كل خطوة بالتفصيل أدناه، وتُرفق الشيفرة الكاملة في نهاية المقال.

## الخطوة 1: إنشاء مصنف جديد وإضافة ورقة رئيسية

الفئة `Workbook` تمثّل ملف Excel كامل. عند إنشاء كائن منها بدون معاملات، تقوم Aspose.Cells بإنشاء مصنف افتراضي يحتوي على ورقة عمل واحدة. إعادة تسمية هذه الورقة إلى *Master* تجعل هدفها واضحًا.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**لماذا هذا مهم:**  
البدء بمصنف نظيف يجنّب وجود تنسيقات أو أوراق مخفية من تشغيلات سابقة. تسمية الورقة بـ *Master* تساعدك على تحديد موقع العلامة الذكية لاحقًا وتُحافظ على قابلية قراءة الملف للمستخدمين غير التقنيين.

## الخطوة 2: إدراج علامة ذكية تُعرّف أسماء أوراق التفصيل

العلامات الذكية هي نواقل يتم استبدالها بالبيانات في وقت التشغيل بواسطة Aspose.Cells. الصيغة `&=DetailSheetNewName=Detail` تُخبر المحرك بإنشاء ورقة عمل جديدة لكل صف في مصدر البيانات، باستخدام قيمة العمود `Detail` كاسم للورقة.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**لماذا هذا مهم:**  
العلامة الذكية تُزيل الحاجة إلى كتابة حلقة تُضيف الأوراق يدويًا. كما أنها تنسخ تلقائيًا تخطيط الورقة الرئيسية إلى كل ورقة مُولّدة جديدة، مما يضمن تنسيقًا موحدًا.

## الخطوة 3: معالجة العلامة الذكية بمصدر بيانات قد يحتوي على مكررات

فيما يلي نقوم بإنشاء `DataTable` يحاكي مصدر بيانات. لاحظ أن عمود *Detail* يحتوي على قيم مكررة (`"Report"` يظهر مرتين). طريقة `SmartMarkersFactory.Process` تحترم الإعداد `AllowDuplicateSheetNames`، والذي يكون **true** افتراضيًا في هذا المثال.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **مهم:** إذا كنت بحاجة لضمان أسماء أوراق فريدة، عيّن `workbook.Settings.CheckDuplicateSheetNames = true;` قبل المعالجة. السلوك الافتراضي يُنشئ أوراقًا بنفس الاسم، وهو ما يسمح به Excel لكنه قد يسبب ارتباكًا عند التنقل في الملف.

## الخطوة 4: حفظ المصنف كملف XLSX

أخيرًا، احفظ المصنف المُولَّد على القرص. طريقة `Save` تختار تلقائيًا الكاتب المناسب بناءً على امتداد الملف.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**النتيجة المتوقعة**

عند فتح `duplicate_detail_sheets.xlsx` سترى:

| اسم الورقة | المحتوى (الصف الأول) |
|------------|---------------------|
| Master     | عنصر نائب للعلامة الذكية (بدون بيانات) |
| Report     | صف البيانات 1 (`123.45`) |
| Summary    | صف البيانات 2 (`67.89`) |
| Report (2) | صف البيانات 3 (`101.12`) |

يتم إعادة تسمية الورقة الثانية *Report* تلقائيًا إلى *Report (2)* بواسطة Aspose.Cells لتجنب حدوث خطأ صلب مع الحفاظ على نية التكرار الأصلية.

## الشيفرة الكاملة

انسخ الملف التالي إلى مشروع وحدة تحكم (`dotnet new console`) وشغّله. يوضح البرنامج سير العمل الكامل لإنشاء **أوراق متعددة** و**حفظ المصنف xlsx** مع معالجة **أسماء الأوراق المكررة**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

شغّل `dotnet run` من مجلد المشروع. بعد التنفيذ، افتح الملف المُولَّد للتحقق من إنشاء ثلاث أوراق تفصيلية، اثنتان منهما تشتركان في الاسم الأساسي **Report**.

## معالجة الحالات الخاصة وأفضل الممارسات

| الحالة | النهج الموصى به |
|-----------|----------------------|
| **مجموعات بيانات ضخمة** ( > 10 000 صف) | استخدم `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` لتقليل الضغط على الذاكرة. |
| **قواعد تسمية مخصصة للأوراق** | عالج عمود `Detail` مسبقًا لاستبدال الأحرف غير المسموح بها (`/ \ ? * [ ] :`) قبل استدعاء `Process`. |
| **الحاجة إلى أسماء فريدة تمامًا** | عيّن `workbook.Settings.CheckDuplicateSheetNames = true;` ووفّر مخطط تسمية احتياطي (مثلاً إلحاق GUID). |
| **إنشاء ملفات PDF بدلاً من XLSX** | بعد الحفظ، استدعِ `workbook.Save("output.pdf", SaveFormat.Pdf);` – يمكن لـ Aspose.Cells تصدير مباشرة إلى PDF. |
| **التشغيل في خدمة ويب** | اكتب المصنف إلى `MemoryStream` وأعده كملف للتحميل لتجنب عمليات I/O على القرص. |

### نصيحة احترافية: إعادة استخدام نفس كائن `Workbook` لتصديرات متعددة

إذا كان تطبيقك يُنشئ عدة تقارير لكل طلب، احتفظ بكائن `Workbook` واحد في الذاكرة، امسح أوراقه (`workbook.Worksheets.Clear();`) وكرر الخطوات. هذا يُقلل من الحمل الناتج عن تحميل بيئة Aspose.Cells مرارًا.

## الخلاصة

أنت الآن تعرف كيف **تنشئ أوراقًا متعددة** في مصنف Excel باستخدام C#، وكيف **تنشئ ملف Excel C#** باستخدام Aspose.Cells، وكيف تدير **أسماء الأوراق المكررة**، وكيف **تحفظ المصنف xlsx** بشكل موثوق. المثال الكامل يُظهر نمطًا نظيفًا وقابلًا للصيانة يتدرّج من السكريبتات السريعة إلى الخدمات الإنتاجية.

### ما الخطوة التالية؟

* استكشف **التنسيق الشرطي** على الأوراق المُولَّدة لتسليط الضوء على القيم المهمة.  
* استخدم **العلامات الذكية** لملء الجداول، المخططات، أو الجداول المحورية تلقائيًا.  
* دمج الشيفرة في واجهة API بـ ASP.NET Core وإرجاع ملف XLSX كتيار تحميل.

لا تتردد في تجربة مصادر بيانات مختلفة (JSON، XML، أو قاعدة بيانات) وتعديل صيغة العلامة الذكية لتناسب احتياجات تقاريرك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook C# – Step‑by‑Step Guide to Write Dates & Save as XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create excel workbook and save it to file in C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}