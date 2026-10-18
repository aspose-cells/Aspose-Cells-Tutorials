---
category: general
date: 2026-10-10
description: تحويل JSON إلى XLSX في C# باستخدام SmartMarker – تعلم كيفية استيراد JSON
  إلى Excel وتعبئة مصنف برمجياً.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: ar
lastmod: 2026-10-10
og_description: تحويل JSON إلى XLSX في C# باستخدام SmartMarker. اتبع هذا الدليل لاستيراد
  JSON إلى Excel، وإنشاء مصنف Excel باستخدام C#، وتعبئة Excel من JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: تحويل JSON إلى XLSX في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: تحويل JSON إلى XLSX في C# باستخدام SmartMarker
url: /ar/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل JSON إلى XLSX في C# باستخدام SmartMarker

إذا كنت بحاجة إلى **تحويل JSON إلى XLSX في C#**، فإن هذا الدليل يوضح لك كيفية **استيراد JSON إلى Excel** و**ملء Excel من JSON** باستخدام بضع أسطر من الشيفرة فقط. سترى كيفية **إنشاء دفتر عمل Excel في C#**، وتكوين معالج SmartMarker، وأخيرًا **استيراد JSON إلى خلايا ورقة العمل**.

> **ما ستحصل عليه** – مثال قابل للتنفيذ بالكامل يقرأ مصفوفة JSON، يتعامل معها كسجل واحد، ويكتب البيانات إلى ملف `.xlsx` جاهز للتقارير أو التحليل اللاحق.

## تحويل JSON إلى XLSX – نظرة عامة

SmartMarker هو جزء من مكتبة Aspose.Cells ويسمح لك بربط JSON أو XML أو أي كائن .NET مباشرةً بقالب Excel. في هذا الدليل سنقوم بـ:

1. **إنشاء دفتر عمل Excel** في الذاكرة.
2. **تحميل بيانات JSON** التي تمثل قائمة بسيطة من الأشخاص.
3. **تكوين SmartMarker** لجعل مصفوفة JSON تُعامل كسجل واحد (`ArrayAsSingle = true`).
4. **معالجة ورقة العمل**، مما يسمح لـ SmartMarker باستبدال العلامات بقيم JSON.
5. **حفظ دفتر العمل** كملف `.xlsx`.

يعمل كامل التدفق على .NET 6+ ويتطلب فقط حزمة NuGet `Aspose.Cells`.

## الخطوة 1: إنشاء دفتر عمل Excel في C#

أولاً، أضف حزمة Aspose.Cells إلى مشروعك:

```bash
dotnet add package Aspose.Cells
```

الآن يمكنك إنشاء كائن `Workbook` جديد. يبدأ دفتر العمل فارغًا، لكن يمكنك إضافة ورقة عمل ووضع علامات SmartMarker حيث يجب أن تظهر بيانات JSON.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **لماذا ننشئ دفتر العمل أولاً** – يعمل SmartMarker على كائن `Worksheet` موجود مسبقًا؛ حيث يوفر دفتر العمل الحاوية لجميع العمليات اللاحقة.

## الخطوة 2: تعريف بيانات JSON وتكوين SmartMarker

سوف نستخدم حمولة JSON صغيرة تُدرج شخصين. خيار `ArrayAsSingle` يخبر SmartMarker بمعاملة المصفوفة بأكملها كسجل منطقي واحد، وهو مثالي عندما تريد جدولًا بسيطًا بدون حلقات متداخلة.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **نصيحة:** إذا حذفت `ArrayAsSingle`، سيحاول SmartMarker إنشاء سجل منفصل لكل عنصر في المصفوفة، مما قد يؤدي إلى تكرار الصفوف أو تخطيط غير متوقع.

## الخطوة 3: إدراج علامات SmartMarker في ورقة العمل

علامات SmartMarker هي نواقل نصية عادية محاطة بـ `&`. ضعها في الخلايا التي تريد ظهور قيم JSON فيها. في هذا المثال نكتب العلامات مباشرة عبر الشيفرة، لكن يمكنك أيضًا تصميم قالب في Excel أولاً.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **شرح:** `&=Name&` يخبر SmartMarker باستبدال الخلية بحقل `Name` من كائن JSON، بينما `&=Age&` يفعل نفس الشيء لحقل `Age`.

## الخطوة 4: معالجة ورقة العمل – ملء Excel من JSON

الآن دع SmartMarker يقرأ سلسلة JSON ويملأ النواقل.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

خلف الكواليس، يقوم SmartMarker بتحليل `jsonData`، ويربط كل خاصية من خصائص الكائن بالعلامة المقابلة، ويوسع الصفوف تلقائيًا لأن `ArrayAsSingle` يساوي `true`. بعد المعالجة، تبدو ورقة العمل هكذا:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

## الخطوة 5: حفظ ملف XLSX

أخيرًا، احفظ دفتر العمل المملوء إلى القرص.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

تشغيل البرنامج ينشئ `SmartMarkerJson.xlsx` على سطح المكتب الخاص بك. فتح الملف في Excel يُظهر جدولًا نظيفًا مع بيانات JSON المستوردة بشكل صحيح.

## المشكلات الشائعة عند استيراد JSON إلى ورقة العمل

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **علامات SmartMarker المفقودة** | SmartMarker يستبدل فقط الخلايا التي تحتوي على `&=...&`. | تحقق مرة أخرى من تهجئة العلامة الدقيقة وحساسيتها لحالة الأحرف. |
| **تنسيق JSON غير صحيح** | علامات الاقتباس المفردة (`'`) ليست صالحة كـ JSON للمحلل المدمج. | استخدم علامات اقتباس مزدوجة (`\"`) أو دع Aspose.Cells يتعامل مع الصيغة المرنة كما هو موضح. |
| **معاملة المصفوفة كسجلات متعددة** | القيمة الافتراضية لـ `ArrayAsSingle` هي `false`. | عيّن `processor.Options.ArrayAsSingle = true` عندما تريد جدولًا مسطحًا. |
| **الحفظ إلى مجلد للقراءة فقط** | `workbook.Save` يُطلق استثناء. | اختر دليلًا قابلًا للكتابة (مثل سطح المكتب أو مجلد مؤقت). |

## توسيع الحل

- **Multiple worksheets:** إنشاء أوراق إضافية واستدعاء `processor.Process` على كل واحدة مع مصادر JSON مختلفة.
- **Styling:** بعد المعالجة، تطبيق أنماط الخلايا (الخطوط، الحدود) كما هو الحال في أي عملية عادية في Aspose.Cells.
- **Large datasets:** بالنسبة لآلاف الصفوف، فكر في تدفق دفتر العمل لتقليل استهلاك الذاكرة (`WorkbookDesigner` أو `SaveOptions` مع `EnableMemoryOptimization`).

## الخلاصة

أنت الآن تعرف كيف **تحويل JSON إلى XLSX في C#** باستخدام Aspose.Cells SmartMarker. سير العمل الكامل — **إنشاء دفتر عمل Excel في C#**، إضافة علامات SmartMarker، تكوين المعالج، **ملء Excel من JSON**، وحفظ الملف — يتيح لك **استيراد JSON إلى ورقة العمل** بخلايا قليلة من الشيفرة.  

لا تتردد في تجربة هياكل JSON أكثر تعقيدًا، إضافة صيغ، أو إنشاء مخططات مباشرةً من البيانات المملوءة. إذا أعجبك هذا الدليل، جرب الدرس التالي حول **كيفية استيراد JSON إلى Excel** لإنشاء مخططات أو حول **إنشاء دفتر عمل Excel في C#** مع تنسيق متقدم.

---

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [تحويل JSON إلى Excel باستخدام C# – دليل خطوة بخطوة](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [كيفية إدراج JSON في قالب Excel – خطوة بخطوة](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [إنشاء دفتر عمل Excel C# – إدراج JSON وحفظ كملف XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}