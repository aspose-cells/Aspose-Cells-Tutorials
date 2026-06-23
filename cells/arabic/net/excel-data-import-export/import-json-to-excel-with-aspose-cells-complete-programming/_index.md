---
category: general
date: 2026-06-21
description: استورد JSON إلى Excel بسرعة وتعلم كيفية تحويل JSON إلى XLSX، وإنشاء Excel
  من JSON، وتصدير JSON إلى جدول بيانات في بضع خطوات سهلة.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: ar
og_description: استيراد JSON إلى Excel بسهولة. يوضح لك هذا الدليل كيفية تحويل JSON
  إلى XLSX، وإنشاء Excel من JSON، وتصدير JSON إلى جدول بيانات باستخدام C#.
og_title: استيراد JSON إلى Excel باستخدام Aspose.Cells – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: استيراد JSON إلى Excel باستخدام Aspose.Cells – دليل برمجي كامل
url: /ar/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استيراد JSON إلى Excel – دليل برمجة كامل

هل تساءلت يومًا **كيف تستورد JSON إلى Excel** دون كتابة محلل مخصص؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تحويل حمولة JSON إلى جدول بيانات منظم لأغراض التقارير أو تحليلات البيانات. الخبر السار؟ باستخدام Aspose.Cells يمكنك **تحويل JSON إلى XLSX** في بضع أسطر فقط، وتكون العملية بأكملها سريعة وآمنة من حيث النوع.

في هذا الدرس سنستعرض كل خطوة مطلوبة **لإنشاء Excel من JSON**، حفظ النتيجة كملف `.xlsx`، وحتى استكشاف بعض الاختلافات المفيدة—مثل تصدير JSON إلى جدول بيانات يتحدث تلقائيًا عند تغيير البيانات المصدر. في النهاية، ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل على .NET Framework أيضًا)
- ترخيص صالح لـ Aspose.Cells for .NET أو مفتاح تقييم مؤقت
- Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها)
- إلمام أساسي بهياكل JSON وصياغة C#

لا توجد حزم NuGet إضافية بخلاف **Aspose.Cells** مطلوبة، مما يجعل الإعداد خفيفًا.

## الخطوة 1: تثبيت Aspose.Cells وإعداد المشروع

أولًا، أضف مكتبة Aspose.Cells إلى مشروعك. افتح Package Manager Console وشغّل:

```powershell
Install-Package Aspose.Cells
```

إذا كنت تستخدم .NET CLI، فإن الأمر المكافئ هو:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** بعد التثبيت، أضف ملف الترخيص الخاص بك (`Aspose.Cells.lic`) إلى جذر المشروع وحمّله عند بدء التشغيل:

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

الآن أنت جاهز لبدء **استيراد JSON إلى Excel**.

## الخطوة 2: إعداد حمولة JSON

للتوضيح، سنستخدم مصفوفة بسيطة من كائنات الأشخاص. في سيناريو واقعي قد تقرأ هذه السلسلة من ملف، أو استجابة API، أو قاعدة بيانات.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

لاحظ أن JSON هو مصفوفة مسطحة—وهي الشكل المثالي للعمل مع علامات Aspose.Cells الذكية.

## الخطوة 3: تكوين خيارات تحميل JSON

تتيح لك Aspose.Cells معالجة مصفوفة JSON بالكامل كمصدر بيانات *واحد*. هذا أمر حاسم عندما تريد أن تتوسع الصفوف تلقائيًا داخل ورقة العمل.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

ضبط `ArrayAsSingle = true` يخبر المكتبة **بإنشاء علامة ذكية تتكرر لكل عنصر** في المصفوفة، وهو جوهر سير عمل **تحويل JSON إلى XLSX**.

## الخطوة 4: إنشاء دفتر العمل واستيراد JSON

الآن نقوم بإنشاء كائن `Workbook` جديد ونستورد JSON باستخدام علامة ذكية باسم `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

في الخلفية، تقوم Aspose.Cells بتحليل JSON، وربط كل خاصية (`Name`, `Age`) بعمود، وتجهز عنصرًا نائبًا سيتوسع لاحقًا إلى صفوف.

## الخطوة 5: وضع العلامة الذكية في ورقة العمل

العلامة الذكية تبدو هكذا `{{People}}`. عند حفظ دفتر العمل، تقوم Aspose.Cells باستبدال هذه العلامة بجدول يحتوي على جميع البيانات من مصفوفة JSON.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

يمكنك نقل العلامة إلى أي مكان—الزاوية العليا اليسرى خيار شائع لأنها تمنح الجدول مساحة للنمو إلى الأسفل وإلى اليمين.

## الخطوة 6: حفظ دفتر العمل كملف XLSX

أخيرًا، اكتب دفتر العمل إلى القرص. هنا نقوم **بحفظ JSON كـ Excel** ونحصل على ملف `.xlsx` حقيقي يمكنك فتحه في Excel أو Google Sheets أو أي تطبيق جدول بيانات آخر.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

عند فتح `JsonSingleCell.xlsx`، سترى شيئًا مثل:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

هذا هو نتيجة **إنشاء Excel من JSON** عمليًا.

## مثال كامل يعمل

بجمع كل ذلك، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

فتح الملف يظهر جدولًا من صفين مع رؤوس **Name** و **Age**، مطابقة تمامًا لمصفوفة JSON الأصلية.

## تنويعات متقدمة

### 1. استيراد مصفوفات JSON متعددة إلى أوراق مختلفة

إذا كان لديك عدة مصفوفات—مثل `"Employees"` و `"Departments"`—يمكنك استيراد كل واحدة إلى ورقة عمل خاصة بها:

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

الآن لقد **قمت بتصدير JSON إلى جدول بيانات** مع علامات تبويب متعددة، كل واحدة تعكس مجموعة بيانات مميزة.

### 2. تنسيق الجدول المُنشأ

يمكنك تطبيق نمط بعد توسيع البيانات:

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

هذه اللمسة الصغيرة تجعل صف العنوان يبرز، وهو مفيد للوحات تقارير.

### 3. استخدام ملف JSON بدلاً من سلسلة نصية

إذا كان JSON موجودًا على القرص، فقط اقرأه أولًا:

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

بقية الخطوات تبقى كما هي تمامًا، لذا يمكنك **حفظ JSON كـ Excel** من أي مصدر.

## الأخطاء الشائعة وكيفية تجنبها

- **Missing `ArrayAsSingle`** – نسيان هذا العلم سيجعل كل كائن يُعامل كمصدر بيانات منفصل، مما يؤدي إلى خلايا فارغة. احرص دائمًا على ضبطه عندما يكون JSON مصفوفة على المستوى الأعلى.
- **Incorrect Smart Marker Name** – يجب أن يتطابق الاسم (`{{People}}`) مع `DataSourceName` الذي مررته (`"People"`). أي خطأ إملائي سيترك العنصر النائب دون استبدال.
- **License Not Loaded** – في وضع التقييم، يحتوي ملف الإخراج على علامة مائية. حمّل الترخيص مبكرًا للحفاظ على دفتر العمل نظيفًا.
- **File Path Permissions** – محاولة الحفظ في مجلد محمي تُسبب استثناء. استخدم `Environment.CurrentDirectory` أو مسار يمكن للمستخدم الكتابة فيه.

## اختبار النتيجة برمجيًا

إذا أردت التحقق من نجاح التصدير دون فتح Excel، يمكنك قراءة الخلية الأولى مرة أخرى:

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

فحص سريع في وحدة التحكم مثل هذا يؤكد أن **تحويل JSON إلى XLSX** عمل كما هو متوقع.

## الخلاصة

لقد غطينا الآن كل ما تحتاجه **لاستيراد JSON إلى Excel** باستخدام Aspose.Cells: من تثبيت المكتبة، إعداد JSON، تكوين العلامات الذكية، وحتى **حفظ JSON كـ Excel**. سواء كنت تحتاج إلى **تحويل JSON إلى XLSX**، **إنشاء Excel من JSON**، أو **تصدير JSON إلى جدول بيانات** للتحليلات، يبقى النمط هو نفسه—العلامات الذكية تقوم بالعمل الشاق.

لا تتردد في تجربة التنسيق، أو عدة أوراق، أو حتى التحديثات الديناميكية بإعادة استيراد JSON أثناء التشغيل. الخطوة المنطقية التالية هي دمج هذا الكود في واجهة ويب API تقدم تقارير Excel عند الطلب—فقط استبدل سطر حفظ الملف بتدفق يُرجع إلى العميل.

هل لديك أسئلة حول حالات خاصة، مثل كائنات JSON المتداخلة أو مجموعات بيانات كبيرة؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استيراد JSON إلى Excel بكفاءة باستخدام Aspose.Cells للـ Java: دليل شامل](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [استيراد بيانات JSON إلى Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [استيراد JSON إلى Excel بسهولة باستخدام Aspose.Cells للـ .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}