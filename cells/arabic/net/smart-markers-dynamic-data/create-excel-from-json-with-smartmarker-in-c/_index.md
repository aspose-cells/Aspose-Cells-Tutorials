---
category: general
date: 2026-11-16
description: إنشاء ملف إكسل من JSON باستخدام SmartMarker. تعلّم كيفية تحويل JSON إلى
  إكسل، وإدراج JSON في إكسل، وحفظ ملف العمل بصيغة xlsx في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: ar
lastmod: 2026-11-16
og_description: إنشاء ملف Excel من JSON بسرعة. يوضح هذا الدرس كيفية تحويل JSON إلى
  Excel، وتضمين JSON في Excel، وحفظ ملف العمل بصيغة xlsx باستخدام Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: إنشاء ملف Excel من JSON باستخدام SmartMarker – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: إنشاء ملف إكسل من JSON باستخدام SmartMarker في C#
url: /ar/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء Excel من JSON باستخدام SmartMarker في C#

إذا كنت بحاجة إلى **إنشاء Excel من JSON** في مشروع .NET، يوضح هذا الدليل حلاً كاملاً وقابلاً للتنفيذ. باستخدام معالج Smart Marker الخاص بـ Aspose.Cells يمكنك **تحويل JSON إلى Excel**، وإدراج سلسلة JSON مباشرةً في خلية، و**حفظ المصنف بصيغة xlsx** دون كتابة أي كود تحليل يدوي.

سترى كيفية تسجيل مصدر بيانات JSON، وإدراج Smart Marker يُخرج المصفوفة بالكامل كسلسلة JSON واحدة، ومعالجة ورقة العمل، وأخيرًا كتابة الملف إلى القرص. بنهاية الدليل يمكنك إنشاء ملف Excel يحتوي على حمولة JSON الأصلية في الخلية A1، جاهز للمعالجة اللاحقة أو التقارير.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
- Aspose.Cells for .NET (حزمة NuGet `Aspose.Cells`)
- معرفة أساسية بـ C# وتنسيق JSON
- بيئة تطوير متكاملة مثل Visual Studio أو VS Code

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا جديدًا من نوع console وأضف حزمة Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

ثم قم بتضمين المساحات الاسمية المطلوبة في أعلى ملف `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**لماذا؟**  
`Aspose.Cells` يوفر نموذج المصنف، بينما `Aspose.Cells.SmartMarkers` يحتوي على الفئة `SmartMarkerProcessor` التي تفسر العلامات `&=` في ورقة العمل.

## الخطوة 2: تعريف مصدر بيانات JSON

ضع سلسلة JSON في متغيّر. في هذا المثال لدينا مصفوفة من الطلبات:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**لماذا؟**  
يعمل Smart Marker مع أي JSON مُشكل بشكل صحيح. حفظ JSON كسلسلة يتيح لك تسجيله مباشرةً دون الحاجة إلى ملف على القرص.

## الخطوة 3: تسجيل بيانات JSON مع SmartMarkerProcessor

أنشئ كائنًا من `SmartMarkerProcessor` واربط سلسلة JSON باسم ستستخدمه لاحقًا في ورقة العمل:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**لماذا؟**  
`RegisterJsonDataSource` يقوم بتحليل JSON ويجعل هيكله متاحًا لـ Smart Markers. يصبح الاسم `"OrdersJson"` هو الكائن الجذري في تعبيرات العلامات.

## الخطوة 4: إنشاء مصنف وإدراج Smart Marker

أنشئ مصنفًا جديدًا، احصل على ورقة العمل الأولى، واكتب Smart Marker في الخلية A1 سيُخرج المصفوفة الكاملة `Orders` كسلسلة JSON واحدة:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**لماذا؟**  
التعبير `OrdersJson.Orders.ArrayAsSingle` يخبر Smart Marker بأخذ مصفوفة `Orders` وتحويلها مرة أخرى إلى JSON، ووضع النتيجة في الخلية المستهدفة. هذه هي أبسط طريقة **لإدراج JSON في Excel**.

## الخطوة 5: معالجة ورقة العمل

شغّل المعالج ليستبدل العلامة بسلسلة JSON الفعلية:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**لماذا؟**  
تقوم المعالجة بفحص كل خلية بحثًا عن علامات `&=`، وتقييمها مقابل مصادر البيانات المسجلة، ثم كتابة القيمة المُقيمة مرة أخرى في ورقة العمل.

## الخطوة 6: حفظ المصنف كملف .xlsx

أخيرًا، احفظ المصنف إلى القرص. عدّل المسار إلى مجلد لديك صلاحية كتابة فيه:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**لماذا؟**  
`SaveFormat.Xlsx` يضمن تخزين الملف بصيغة Office Open XML الحديثة، مما يلبي متطلبات **حفظ المصنف xlsx**.

## الكود الكامل

بجمع جميع الأجزاء معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### النتيجة المتوقعة في Excel

افتح `JsonArraySingleCell.xlsx`. ستحتوي الخلية A1 على:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

سلسلة JSON هي تمثيل مضغوط للمصفوفة الأصلية `Orders`، مما يجعل من السهل نقلها أو استهلاكها في سير عمل مبني على Excel لاحقًا.

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل |
|-----------|------------|
| **كائنات JSON متعددة** | سجّل كل كائن باسم مميز (مثال: `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) واستخدمه مع علامات منفصلة. |
| **JSON منسق بشكل جميل في خلية** | استخدم خيار `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **حمولات JSON الكبيرة** | فكّر في كتابة JSON إلى ورقة مخفية أو استخدام تحويل `DataTable` لأداء أفضل. |
| **إدراج JSON في خلايا متعددة** | ضع علامات مختلفة في خلايا أخرى، مثل `&=OrdersJson.Orders[0].Id` لاستخراج حقول فردية. |

**نصيحة احترافية:** عند التعامل مع JSON كبير جدًا، قم بزيادة مخزن الذاكرة للمصنف (`WorkbookSettings.MemorySetting`) لتجنب `OutOfMemoryException`.

## اختبار الحل

1. ابنِ وشغّل تطبيق الـ console (`dotnet run`).  
2. تحقق من أن الـ console يطبع المسار الكامل للملف المُنشأ.  
3. افتح الملف في Excel أو أي عارض جداول.  
4. تأكد من أن الخلية A1 تحتوي على سلسلة JSON للمصفوفة تمامًا كما هو موضح أعلاه.

إذا احتوت الخلية على نص العلامة (`&=OrdersJson...`) بدلًا من JSON، فتأكد من أن المعالج تم استدعاؤه **بعد** وضع العلامة وأن سلسلة JSON صالحة.

## الخلاصة

أنت الآن تعرف كيف **تنشئ Excel من JSON** باستخدام Aspose.Cells Smart Markers، وكيف **تحول JSON إلى Excel**، وتدرج حمولة JSON مباشرةً في خلية، و**تحفظ المصنف بصيغة xlsx** بسطر واحد من الكود. هذه الطريقة تلغي التحليل اليدوي، وتعمل مع أي بنية JSON، وتنتج ملف Excel نظيف ومتوافق مع المعايير.

### الخطوات التالية

- استكشف **حلقات Smart Marker** (`&=OrdersJson.Orders`) لإنشاء صف لكل طلب بدلاً من سلسلة JSON واحدة.  
- اجمع هذه التقنية مع **صيغ Excel** لحساب الإجماليات من البيانات المدمجة.  
- انظر إلى **قراءة JSON من Excel** باستخدام `Workbook.Load` و `SmartMarkerProcessor` بالعكس.

لا تتردد في تجربة أشكال JSON مختلفة، أوراق عمل متعددة، أو تصدير إلى صيغ أخرى مثل CSV أو PDF. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء Excel من JSON باستخدام Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [إنشاء مصنف Excel من JSON – دليل Aspose.Cells الكامل](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [حفظ مصنف Excel من JSON – دليل كامل](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}