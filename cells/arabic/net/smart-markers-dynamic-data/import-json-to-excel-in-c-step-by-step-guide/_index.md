---
category: general
date: 2026-08-11
description: استيراد JSON إلى إكسل باستخدام C# و Aspose.Cells. تحميل JSON إلى DataSet،
  معالجة العلامات الذكية، وحفظه كملف xlsx في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: ar
lastmod: 2026-08-11
og_description: استيراد JSON إلى Excel باستخدام C# و Aspose.Cells. يوضح هذا الدليل
  كيفية تحميل JSON إلى DataSet، ومعالجة العلامات الذكية، وحفظ المصنف كملف xlsx، مما
  يتيح تصدير البيانات بسلاسة.
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: استيراد JSON إلى Excel باستخدام C# – دليل خطوة بخطوة كامل
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: استيراد JSON إلى Excel في C# – دليل خطوة بخطوة
url: /ar/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استيراد json إلى Excel في C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى استيراد json إلى Excel باستخدام C#، فإن هذا الدليل يشرح العملية بالكامل. ستتعلم كيفية تحميل JSON إلى DataSet، تطبيق علامة ذكية، وحفظ النتيجة كملف xlsx. نفس النهج يتيح لك أيضًا تحويل json إلى xlsx لسلاسل التقارير أو سكريبتات ترحيل البيانات.

يغطي الدليل كل سطر من الشيفرة المطلوب، يوضح لماذا كل خطوة مهمة، ويسلط الضوء على الأخطاء الشائعة. في النهاية ستتمكن من تصدير بيانات json إلى Excel دون كتابة محولات مخصصة، وستفهم كيفية حفظ المصنف c# بطريقة جاهزة للإنتاج. لا تحتاج إلى أدوات خارجية بخلاف Aspose.Cells.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث مثبت  
- Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET)  
- حزمة NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- ملف قالب Excel يحتوي على علامة ذكية (مثال: `Template.xlsx`)  

يجب أن يحتوي القالب على خلية واحدة تحمل العلامة الذكية `&=Table(Data)` حيث يتطابق `Data` مع اسم DataTable الذي ستمرره.

## استيراد json إلى Excel – إعداد المشروع

أنشئ تطبيق console جديد وأضف مرجع Aspose.Cells:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

إضافة توجيهات `using` في أعلى الملف تسمح للمُترجم بالعثور على `DataSet` و `Workbook` والأنواع المرتبطة. هذه الأساسيات مطلوبة لكل عملية تالية.

## تحويل json إلى xlsx – تحميل JSON إلى DataSet

الخطوة الوظيفية الأولى هي تحويل سلسلة JSON إلى `DataSet`. توفر Aspose.Cells امتدادًا مريحًا `ReadJson` يقوم بتحليل مصفوفة من الكائنات مباشرةً إلى جدول.

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**لماذا هذا مهم:**  
`ReadJson` ينشئ تلقائيًا `DataTable` باسم `Table` (أو اسم العنصر الجذري) ويملأ الأعمدة بناءً على مفاتيح JSON. هذا يلغي الحاجة إلى حلقات يدوية ويضمن استنتاج أنواع البيانات بشكل صحيح. إذا كان JSON يحتوي على كائنات متداخلة، تقوم Aspose.Cells بتسطيحها إلى جداول منفصلة يمكنك الإشارة إليها لاحقًا.

**نصيحة:** إذا كان حجم حمولة JSON كبيرًا، فكر في بثه باستخدام `StringReader` لتجنب تحميل السلسلة بالكامل في الذاكرة.

## تصدير بيانات json إلى Excel – فتح قالب Excel مع علامة ذكية

بعد ذلك، افتح المصنف الذي يحتوي على العلامة الذكية. العلامة الذكية تخبر Aspose.Cells أين تُدرج البيانات من `DataSet`.

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**لماذا هذا مهم:**  
القالب يعزل التنسيق عن الشيفرة. يمكنك تصميم المظهر النهائي في Excel (الخطوط، الحدود، التنسيق الشرطي) وتترك المكتبة تتولى إدراج البيانات. صيغة العلامة الذكية `&=Table(Data)` تُخبر المحرك بكتابة كامل `DataTable` في الخلية التي توجد فيها العلامة.

## تصدير بيانات json إلى Excel – معالجة العلامة الذكية

الآن عالج العلامة الذكية، مع تمرير `DataTable` التي تم إنشاؤها من JSON.

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**لماذا هذا مهم:**  
`ProcessSmartMarkers` يقرأ العلامة، يوسع الجدول عموديًا، ويحافظ على تنسيق الخلية الأصلي. الطريقة أيضًا تحترم عرض الأعمدة وتطبق تنسيقات الأرقام تلقائيًا بناءً على أنواع .NET الأساسية.

**حالة حافة:** إذا كانت الخلية المستهدفة تحتوي بالفعل على بيانات، فإن الطريقة ستستبدلها. للحفاظ على المحتوى الموجود، ضع العلامة في منطقة مخصصة من القالب.

## حفظ المصنف c# – كتابة الملف النهائي

أخيرًا، احفظ المصنف كملف `.xlsx`. يمكنك اختيار أي موقع يمكن لتطبيقك الكتابة إليه.

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**لماذا هذا مهم:**  
تحديد `SaveFormat.Xlsx` يضمن أن الناتج يتوافق مع معيار Open XML، مما يجعله قابلًا للقراءة بواسطة تطبيقات الجداول الحديثة. إذا كنت بحاجة إلى ملف `.xls` قديم، استبدل `SaveFormat.Xlsx` بـ `SaveFormat.Excel97To2003`.

**نصيحة احترافية:** استخدم `SaveOptions` للتحكم في مستوى الضغط للملفات الكبيرة، مثال: `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## الشيفرة المصدرية الكاملة

جمع جميع الخطوات معًا ينتج برنامجًا قابلاً للتنفيذ:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**الناتج المتوقع:**  
تشغيل البرنامج ينشئ `JsonSingleCell.xlsx`. عند فتح الملف ستظهر الصفوفين (`John`, `30` و `Anna`, `25`) مُعبأة تحت خلية العلامة الذكية، مع الحفاظ على أي تنسيق رأس قمت بتعريفه في `Template.xlsx`.

![مثال على كود استيراد json إلى Excel](image.png "مثال على كود استيراد json إلى Excel")

## أسئلة شائعة وكيفية التعامل معها

- **ماذا لو كانت مصفوفة JSON فارغة؟**  
  `ReadJson` لا يزال ينشئ `DataTable` فارغًا. العلامة الذكية ستنتج صف الرأس فقط، وهو غالبًا ما يكون النتيجة المطلوبة للقوالب التقاريرية.

- **هل يمكنني استيراد عدة مصفوفات JSON إلى أوراق مختلفة؟**  
  نعم. حمّل كل مصفوفة في `DataTable` خاص بها داخل نفس `DataSet`، ثم استدعِ `ProcessSmartMarkers` على كل ورقة عمل، مع الإشارة إلى اسم الجدول المناسب في العلامة (مثال: `&=Table(Orders)`).

- **كيف أتحكم في ترتيب الأعمدة؟**  
  بعد `ReadJson`، أعد ترتيب الأعمدة عن طريق تعديل `dataSet.Tables[0].Columns` قبل معالجة العلامة الذكية.

- **هل يمكن كتابة JSON مباشرةً إلى خلية واحدة كسلسلة نصية؟**  
  إذا كنت بحاجة إلى وضع سلسلة JSON الخام في خلية، تخطّ خطوة `DataSet` وعيّنها مباشرةً: `worksheet.Cells["A1"].PutValue(jsonData);`

## الخلاصة

أنت الآن تعرف كيف تستورد json إلى Excel في C# باستخدام Aspose.Cells، من تحميل JSON إلى DataSet إلى معالجة العلامة الذكية وحفظ المصنف c#. هذا الحل المتكامل يتيح لك تحويل json إلى xlsx بسرعة، وتصدير بيانات json.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استيراد JSON إلى Excel بسهولة باستخدام Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [استيراد بيانات JSON إلى Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [استيراد JSON إلى Excel بفعالية باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}