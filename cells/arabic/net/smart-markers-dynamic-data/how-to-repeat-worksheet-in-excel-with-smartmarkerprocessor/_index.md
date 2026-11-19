---
category: general
date: 2026-11-19
description: كيفية تكرار ورقة العمل أثناء تعبئة إكسل ببيانات مصفوفة. تعلم إنشاء عدة
  أوراق عمل وتعبئة ورقة العمل من قائمة في بضع خطوات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: ar
lastmod: 2026-11-19
og_description: كيفية تكرار ورقة العمل باستخدام SmartMarkerProcessor. اتبع هذا الدليل
  لملء Excel ببيانات المصفوفة، وإنشاء عدة أوراق عمل، وملء ورقة العمل من قائمة.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: كيفية تكرار ورقة العمل في إكسل – دليل خطوة بخطوة
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: كيفية تكرار ورقة العمل في إكسل باستخدام SmartMarkerProcessor
url: /ar/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار ورقة العمل في Excel باستخدام SmartMarkerProcessor

إذا كنت بحاجة إلى **how to repeat worksheet** عند إنشاء تقارير Excel، فإن هذا الدليل يوضح لك حلاً كاملاً وقابلاً للتنفيذ. بنهاية البرنامج التعليمي ستتمكن من **populate Excel with array** البيانات، **generate multiple worksheets**، و **populate worksheet from list** باستخدام مكتبة SmartMarkerProcessor.

تكرار ورقة العمل هو طلب شائع عندما تحتاج كل إدارة أو منطقة أو فترة زمنية إلى تبويب خاص بها. المثال أدناه يوضح الخطوات الدقيقة، يشرح لماذا كل إعداد مهم، ويغطي الحالات الحدية مثل القوائم الفارغة أو التسمية المخصصة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث مثبت
- إشارة إلى حزمة NuGet **GroupDocs.Viewer** (أو ما يعادلها) التي تحتوي على `SmartMarkerProcessor`
- مصنف قالب Excel (`.xlsx`) يحتوي على علامة مثل `${repeat:Dept}` موضوعة في الصف الذي تريد تكراره
- إلمام أساسي بـ C# و LINQ (اختياري لكن مفيد)

لا توجد مكتبات طرف ثالث إضافية مطلوبة.

## الخطوة 1: إنشاء كائن SmartMarkerProcessor

المعالج ينسق استبدال العلامات وتكرار ورقة العمل. إنشاءه بدون معلمات يستخدم الخيارات الافتراضية.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

إنشاء المعالج مبكرًا يتيح لك ضبط الخيارات العامة قبل تطبيق أي بيانات. هذا هو الأساس لـ **how to repeat worksheet** بشكل صحيح.

## الخطوة 2: تمكين تكرار ورقة العمل

بشكل افتراضي، يستبدل المعالج العلامات في الورقة الحالية فقط. ضبط `RepeatWorksheet` إلى `true` يخبر المحرك بنسخ الورقة بالكامل لكل عنصر في مجموعة البيانات.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

تمكين هذا الخيار هو المفتاح لـ **generate multiple worksheets**—المعالج سيخلق تبويبًا جديدًا لكل عنصر في مصفوفة `Dept` ويحافظ على التنسيق الأصلي.

## الخطوة 3: تحضير مصدر البيانات كمصفوفة أو قائمة

SmartMarkerProcessor يعمل مع أي مجموعة قابلة للتعداد، لكن استخدام مصفوفة يجعل النية واضحة عندما تريد **populate worksheet from list**. هنا ننشئ كائنًا مجهولًا يحتوي على خاصية `Dept` تحمل مصفوفة من السلاسل.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

إذا كان لديك بالفعل `List<string>` يمكنك تمريره مباشرة؛ المعالج سيتعامل معه بنفس الطريقة. الجزء المهم هو أن اسم الخاصية (`Dept`) يطابق العلامة `${repeat:Dept}` في القالب.

## الخطوة 4: تحميل ورقة العمل القالب

بافتراض أن لديك `ExcelPackage` (من EPPlus) أو كائن `Workbook`، استخرج ورقة العمل التي تريد تكرارها. المتغير `ws` يمثل تلك الورقة.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

إذا كنت تفضل مكتبة مختلفة (مثل ClosedXML)، نفس المبدأ ينطبق: احصل على كائن ورقة عمل يطبق الواجهة المطلوبة.

## الخطوة 5: معالجة ورقة العمل بالبيانات

الآن طبّق البيانات على القالب. المعالج ينسخ ورقة العمل لكل إدارة، يستبدل علامة `${repeat:Dept}` باسم الإدارة الفعلي، ويترك باقي الورقة دون تعديل.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

بعد انتهاء `Process`، يصبح `ws` أول ورقة من عدة أوراق—واحدة لكل إدارة. يُحافظ على اسم الورقة الأصلية، بينما تتلقى النسخ المكررة لاحقات تصاعدية (مثال: “Sheet1 (1)”، “Sheet1 (2)”). يمكنك إعادة تسميتها لاحقًا إذا احتجت إلى نظام تسمية مخصص.

### الناتج المتوقع

عند فتح المصنف الناتج، يجب أن ترى:

- **Sheet1** – القالب الأصلي (غالبًا ما يكون فارغًا أو يُستخدم كقالب رئيسي)
- **Sheet1 (1)** – مُعبأ بـ “HR”
- **Sheet1 (2)** – مُعبأ بـ “IT”
- **Sheet1 (3)** – مُعبأ بـ “Finance”

كل ورقة تحتوي على نفس التخطيط ولكن مع استبدال اسم الإدارة حيث ظهرت `${repeat:Dept}`.

## معالجة الحالات الحدية

### المصفوفات الفارغة أو ذات القيمة null

إذا كان `Dept` null أو فارغًا، لن ينشئ المعالج أي أوراق عمل إضافية. لتجنب مصنف فارغ تمامًا، يمكنك إضافة شرط حماية:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### أسماء أوراق العمل المخصصة

قد لا يناسب نظام التسمية الافتراضي كل متطلبات التقارير. بعد المعالجة، أعد تسمية كل ورقة باستخدام حلقة:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### ملء أعمدة إضافية

إذا كنت بحاجة إلى **populate excel with array** قيم تتجاوز علامة واحدة، وسّع كائن البيانات:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

ثم عدّل علامات القالب إلى `${repeat:Dept.Name}` و `${repeat:Dept.Headcount}`. المعالج سيكرر الصف لكل إدارة ويملأ كلا العمودين.

## مثال كامل يعمل

فيما يلي تطبيق وحدة تحكم مستقل يوضح التدفق الكامل من تحميل القالب إلى حفظ المصنف النهائي.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**شرح الأقسام الرئيسية**

- **Processor creation** – يحدد المحرك الذي سيفسر العلامات.
- **RepeatWorksheet option** – يفعّل الميزة الأساسية التي تجيب على *how to repeat worksheet*.
- **Data source** – يستخدم مصفوفة (`new[]`) لتلبية **populate excel with array**.
- **Template loading** – يوضح طريقة شائعة للحصول على كائن ورقة العمل.
- **Processing** – ينفّذ التكرار وإدخال البيانات في استدعاء واحد.
- **Renaming** – يوضح كيفية تحويل الأسماء العامة “(1)”، “(2)” إلى عناوين ذات معنى، وهو مطلب شائع بعد **generate multiple worksheets**.

تشغيل هذا البرنامج ينتج `Result.xlsx` بثلاث تبويبات خاصة بكل إدارة، كل منها مُعبأ من المصفوفة.

## المشكلات الشائعة والنصائح الاحترافية

- **Marker spelling** – يجب أن تتطابق العلامة مع اسم الخاصية تمامًا (`${repeat:Dept}`). أي خطأ إملائي يمنع التكرار.
- **Worksheet index** – بعد المعالجة، تبقى الورقة الأصلية في الفهرس 0؛ الأوراق المولدة تتبعها تسلسليًا. الخطأ في الفهرسة قد يؤدي إلى إعادة تسمية الورقة الخاطئة.
- **Large data sets** – إنشاء مئات الأوراق قد يزيد حجم الملف بشكل كبير. فكر في تقسيم التقارير أو استخدام ورقة واحدة مع أقسام مجمعة إذا أصبحت الأداء مشكلة.
- **Thread safety** – `SmartMarkerProcessor` غير آمن للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة لكل خيط إذا كنت تعالج عدة مصنفات بالتوازي.

## الخلاصة

أنت الآن تعرف **how to repeat worksheet** في Excel باستخدام SmartMarkerProcessor، وكيفية **populate excel with array** البيانات، وكيفية **generate multiple worksheets**، وكيفية **populate worksheet from list** بفعالية. المثال الكامل يربط جميع المفاهيم معًا، وخطوة إعادة التسمية الاختيارية تتيح لك إنتاج أسماء تبويبات نظيفة وسهلة الاستخدام.

بعد ذلك، قد تستكشف:

- [كيفية تكرار أوراق العمل – دليل كامل لأتمتة Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [إنشاء ورقة عمل لكل عنصر – كيفية تكرار ورقة العمل في C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [كيفية توسيع المصفوفة في Excel وتعبئة قالب](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}