---
category: general
date: 2026-08-07
description: إنشاء ملف إكسل من JSON باستخدام Aspose.Cells Smart Marker – تعلم كيفية
  تعبئة قالب إكسل، وتطبيق تسمية أوراق ديناميكية، وإنشاء عدة أوراق عمل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: ar
lastmod: 2026-08-07
og_description: إنشاء ملف Excel من JSON باستخدام Aspose.Cells Smart Marker لتعبئة
  القوالب بسرعة، واستخدام تسمية أوراق ديناميكية، وإنشاء عدة أوراق عمل.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: إنشاء ملف Excel من JSON – دليل Aspose.Cells Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء ملف إكسل من JSON باستخدام Aspose.Cells Smart Marker
url: /ar/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء Excel من JSON باستخدام Aspose.Cells Smart Marker

إذا كنت بحاجة إلى **إنشاء Excel من JSON**، فإن هذا الدليل يوضح حلاً كاملاً وجاهزًا للإنتاج. سترى كيفية **ملء قالب Excel**، وتكوين **تسمية الأوراق الديناميكية**، و**إنشاء أوراق عمل متعددة** تلقائيًا باستخدام محرك **Aspose.Cells Smart Marker**.

يقودك الدليل عبر كل خطوة مطلوبة، من تعريف كائن المصدر الشبيه بـ JSON إلى حفظ المصنف النهائي. لا تحتاج إلى أي سكريبتات خارجية، ويعمل الكود على .NET 6 أو أحدث.

## ما ستحققه

* تحميل كائن بيانات بنمط JSON إلى الذاكرة.  
* إدراج عنصر نائب Smart Marker في قالب المصنف.  
* تطبيق نمط تسمية بحيث يحصل كل ورقة تفاصيل مكررة على اسم فريد.  
* معالجة القالب لإنشاء ورقة عمل منفصلة لكل طلب في المجموعة.  
* حفظ النتيجة كملف `.xlsx` جاهز للاستخدام اللاحق.

المتطلبات المسبقة: Visual Studio 2022 (أو أي بيئة تطوير C#)، .NET 6+، وحزمة **Aspose.Cells** من NuGet. المثال يستخدم C#؛ نفس المفاهيم تنطبق على VB.NET أو لغات .NET الأخرى.

## إنشاء Excel من JSON – سير العمل العام

تقسم الأقسام التالية سير العمل إلى خمس خطوات منطقية. كل خطوة تتضمن الكود الدقيق الذي تحتاجه، شرحًا لأهميته، ونصائح لتوسيع الحل.

### الخطوة 1: تعريف بيانات المصدر المتوافقة مع JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**لماذا هذا مهم** – كائن `ordersData` يعكس البنية التي ستحصل عليها من واجهة برمجة تطبيقات JSON حقيقية. Aspose.Cells Smart Marker يقرأ الخصائص العامة، لذا فإن النوع المجهول يعمل طالما أن أسماء الخصائص تتطابق مع وسوم العلامة (`{{Orders}}`). عندما تستبدل لاحقًا النوع المجهول بكائن JSON مُفكك، لا يلزم تعديل الكود.

### الخطوة 2: إعداد قالب المصنف وإدراج Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**لماذا هذا مهم** – علامة `{{Orders}}` تخبر المعالج بالتكرار عبر مجموعة `Orders`. وضع العلامة في الخلية `A1` في الورقة الأولى يجعل تلك الورقة هي الورقة *الرئيسية*. سيقوم المعالج بنسخ هذه الورقة لكل طلب، مع الحفاظ على أي تنسيق تضيفه لاحقًا.

> **نصيحة:** إذا كان لديك قالب مُصمم مسبقًا (مثلًا مع رؤوس، صيغ، أو تنسيق)، قم بتحميله باستخدام `new Workbook("Template.xlsx")` بدلاً من إنشاء مصنف فارغ.

### الخطوة 3: تكوين تسمية الأوراق الديناميكية

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**لماذا هذا مهم** – بشكل افتراضي، تقوم Aspose.Cells بتسمية الأوراق المكررة بـ `Sheet1`، `Sheet2`، إلخ. نمط `DetailSheetNewName` يدرج فهرسًا تزايديًا (`{0}`) بحيث يحصل كل ورقة على اسم ذو معنى. يمكنك تضمين وسوم إضافية (مثل `{Id}`) لتضمين بيانات السجل الحالي.

> **نصيحة احترافية:** استخدم `DetailSheetNewName = "Order_{Id}"` لتسمية الأوراق بناءً على معرف الطلب، مما يجعل التنقل أسهل في المصنفات الكبيرة.

### الخطوة 4: معالجة القالب بالبيانات وخيارات التسمية

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**لماذا هذا مهم** – يقوم `SmartMarkerProcessor` بدمج `ordersData` في المصنف، وإنشاء ورقة جديدة لكل عنصر في `Orders`، وتطبيق نمط التسمية المحدد مسبقًا. كما يقوم المعالج بتوسيع أي مجموعات متداخلة (مثل `Items`) إذا أضفت وسومًا إضافية داخل ورقة التفاصيل.

### الخطوة 5: حفظ المصنف الناتج

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**لماذا هذا مهم** – طريقة `Save` تكتب المصنف المكتمل إلى القرص. يحتوي الملف الآن على ورقة رئيسية (يمكن إخفاؤها أو حذفها) وسلسلة من أوراق التفاصيل المسماة `DetailSheet_1`، `DetailSheet_2`، …، كل واحدة تحمل بيانات طلب واحد.

#### النتيجة المتوقعة

| اسم الورقة | المحتوى (مبسط) |
|------------|----------------|
| DetailSheet_1 | Order Id = 1, Items: Apple, Banana |
| DetailSheet_2 | Order Id = 2, Items: Orange |

جميع الأوراق تحتفظ بأي تنسيق قمت بتطبيقه على الورقة الرئيسية قبل المعالجة.

## تنويعات متقدمة

### ملء قالب Excel بحقول إضافية

إذا كان JSON الخاص بك يحتوي على مزيد من الخصائص (مثل `CustomerName`، `TotalAmount`)، أضف وسومًا مطابقة إلى القالب:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

سيستبدل المعالج كل علامة بقيمة الخاصية المطابقة.

### إنشاء أوراق عمل متعددة من مجموعات متداخلة

يمكنك إنشاء مستوى ثاني من التكرار بوضع علامة داخل ورقة التفاصيل تشير إلى مجموعة متداخلة، مثل `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

أثناء المعالجة، تقوم Aspose.Cells بإنشاء صف لكل عنصر في مصفوفة `Items`، مما يتيح لك إنشاء قوائم مفصلة لكل طلب.

### تسمية مخصصة باستخدام بيانات السجل

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

الآن تُسمى الأوراق `Order_1`، `Order_2`، مما يطابق اسم الورقة مع معرف العمل.

## الأخطاء الشائعة وكيفية تجنبها

| الخطأ | الحل |
|-------|------|
| نص العلامة لا يتطابق مع اسم الخاصية (حسّاس لحالة الأحرف) | تأكد من أن العلامة (`{{Orders}}`) تتطابق مع الخاصية تمامًا، بما في ذلك حالة الأحرف. |
| القالب يحتوي على خلايا مدمجة تمتد عبر منطقة العلامة | قم بفك دمج الخلايا أو ضع العلامة في خلية واحدة غير مدمجة لتجنب تغييرات غير متوقعة في التخطيط. |
| مجموعات JSON الكبيرة تسبب ضغطًا على الذاكرة | قم بمعالجة البيانات على دفعات أو بث JSON إلى `DataTable` واستخدم `SmartMarkerProcessor` مع `DataSource`. |
| مسار الملف المحفوظ غير صالح | استخدم `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` أو تحقق من أذونات الكتابة. |

## مثال كامل يعمل

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

تشغيل البرنامج يولد ملف Excel على سطح المكتب يحتوي على ورقتين تفصيليتين (`DetailSheet_1` و `DetailSheet_2`). كل ورقة تعكس سجل الطلب المقابل.

## الخلاصة

أنت الآن تعرف كيفية **إنشاء Excel من JSON** باستخدام **Aspose.Cells Smart Marker**، وكيفية **ملء قالب Excel**، وتطبيق **تسمية الأوراق الديناميكية**، و**إنشاء أوراق عمل متعددة** تلقائيًا. نفس النمط يمكن توسيعه إلى العشرات أو الآلاف من السجلات، يدعم المجموعات المتداخلة، ويتكامل بسلاسة مع أي مكتبة تفكيك JSON في .NET.

### الخطوات التالية

* استكشف **التنسيق الشرطي** داخل ورقة التفاصيل لتسليط الضوء على الطلبات ذات القيمة العالية.  
* استبدل الكائن المجهول بنموذج قوي النوع يتم تفكيكه عبر `System.Text.Json`.  
* اجمع بين Smart Markers و**PivotTable** لإنشاء تقارير متقدمة.  

جرّب نمط التسمية، أضف المزيد من العلامات، ودمج هذا سير العمل في خطوط تصدير البيانات الحالية لديك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}