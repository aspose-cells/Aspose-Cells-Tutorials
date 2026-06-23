---
category: general
date: 2026-03-22
description: كيفية إنشاء تقرير Excel في C# باستخدام قالب رئيس‑تفصيلي. تعلم كيفية تعبئة
  قالب Excel في C# بسرعة، باستخدام SmartMarker للأوراق القابلة للتكرار.
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: ar
og_description: كيفية إنشاء تقرير إكسل في C# باستخدام قالب قابل لإعادة الاستخدام.
  يوضح لك هذا الدليل خطوة بخطوة كيفية تعبئة قالب إكسل في C# ببيانات رئيسية وتفصيلية.
og_title: كيفية إنشاء تقرير إكسل في C# – دليل SmartMarker الكامل
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: كيفية إنشاء تقرير إكسل في C# – دليل كامل باستخدام SmartMarker
url: /ar/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء تقرير Excel في C# – دليل كامل باستخدام SmartMarker

هل تساءلت يومًا **how to generate Excel report** في C# دون كتابة كود لا نهائي خلية‑ب‑خلية؟ لست وحدك. معظم المطورين يصطدمون بحائط عندما يحتاجون إلى تقرير متعدد الأوراق مصقول يعكس علاقات master‑detail — فكر في الطلبات وبنودها — لكنهم لا يريدون إعادة اختراع العجلة في كل مرة.

الخبر السار؟ باستخدام قالب Excel جاهز ومحرك **SmartMarker** من Aspose.Cells، يمكنك **populate Excel template C#** ببضع أسطر فقط. في هذا الدرس سنستعرض سيناريو واقعي، نشرح لماذا كل خطوة مهمة، ونقدم لك مثالًا كاملاً قابلاً للتنفيذ يمكنك نسخه‑ولصقه اليوم.

> **ما ستحصل عليه:** تقرير Excel master‑detail حيث تنشئ كل طلب ورقة عمل خاصة به، كل ذلك مدفوع بأجسام C# بسيطة. لا حلقات يدوية على الخلايا، لا صيغ هشة — فقط كود نظيف وقابل للصيانة.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6.0** (أو أحدث) مثبت — الكود يستهدف .NET 6 لكنه يعمل أيضًا على .NET Framework 4.7+.
- حزمة NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) — توفر الفئات `Workbook`، `SmartMarkerProcessor`، وغيرها.
- ملف Excel اسمه **MasterDetailTemplate.xlsx** موجود في `YOUR_DIRECTORY`. يجب أن يحتوي على كتلة SmartMarker مثل `{{Orders.OrderId}}` في الورقة الأولى وكتلة متداخلة `{{Orders.Items.Prod}}` لبنود الخط.
- فهم أساسي لأنواع C# المجهولة — سنستخدمها لنمذجة الطلبات والبنود.

إذا كان أي من هذه غير مألوف لك، لا تقلق. سنذكر بدائل (مثل استخدام EPPlus) لاحقًا، لكن المفهوم الأساسي يبقى نفسه.

---

## الخطوة 1: تحميل قالب Excel الذي يحتوي على كتل SmartMarker

أول شيء نفعله هو فتح ملف القالب. فكر في القالب كهيكل عظمي؛ سيقوم SmartMarker لاحقًا بملئه بالبيانات الحقيقية.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**لماذا هذا مهم:** بفصل التخطيط (القالب) عن البيانات (كائنات C#)، تبقي المصممين سعداء والمطورين سعداء. يمكن للمصممين تعديل الخطوط، الألوان، أو الصيغ دون لمس الكود.

---

## الخطوة 2: بناء مصدر البيانات Master‑Detail

بعد ذلك، ننشئ البيانات التي ستملى القالب. لتقرير طلبات نموذجي، لديك مجموعة من الطلبات، كل طلب يحتوي على مجموعة من البنود.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **نصيحة احترافية:** استخدم فئات ذات نوع قوي بدلاً من الأنواع المجهولة إذا كنت تحتاج لإعادة الاستخدام عبر تقارير متعددة. النهج المجهول يبقي المثال مختصرًا.

**لماذا هذا مهم:** يعمل SmartMarker عن طريق مطابقة أسماء الخصائص (`Orders`, `OrderId`, `Items`, `Prod`, `Qty`) مع العلامات النائبة في القالب. يجب أن يتطابق الهيكل تمامًا، وإلا سيتخطى المحرك تلك الأقسام.

---

## الخطوة 3: إخبار SmartMarker بإنشاء ورقة جديدة لكل سجل رئيسي

بشكل افتراضي، يكتب SmartMarker جميع الصفوف في ورقة واحدة. نريد كل طلب في ورقة عمل خاصة به، وهو مثالي للطباعة أو إرسال ملفات PDF لكل طلب لاحقًا.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**لماذا هذا مهم:** `EnableRepeatingSheet` يلغي الحاجة إلى استنساخ الورقة يدويًا. يقوم المحرك بنسخ الورقة الأصلية، يحقن بيانات الطلب، ويعيد تسمية الورقة تلقائيًا (عادةً باستخدام قيمة العمود الأول).

---

## الخطوة 4: معالجة القالب ببياناتك

الآن نربط كل شيء معًا. `SmartMarkerProcessor` يتجول في المصنف، يستبدل العلامات، وينشئ أوراقًا جديدة حسب التعليمات.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**لماذا هذا مهم:** هذا السطر الواحد يقوم بالعمل الشاق — تحليل القالب، التكرار عبر المجموعات، ومعالجة الجداول المتداخلة. إنه قلب عملية **populate Excel template C#** بدون أي حلقات يدوية.

---

## الخطوة 5: حفظ التقرير النهائي

أخيرًا، اكتب المصنف المملوء إلى القرص. يمكنك أيضًا بثه مباشرةً إلى استجابة HTTP لتطبيقات الويب.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**لماذا هذا مهم:** حفظ الملف يمنحك قطعة ملموسة يمكنك فتحها في Excel، مشاركتها مع أصحاب المصلحة، أو تمريرها إلى عمليات لاحقة مثل تحويل PDF.

---

## مثال كامل يعمل (جاهز للنسخ‑اللصق)

فيما يلي البرنامج الكامل، بما في ذلك توجيهات `using` وطريقة `Main`. ضعها في تطبيق Console، عدل مسارات الملفات، وشغّلها.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### النتيجة المتوقعة

عند فتح `MasterDetailResult.xlsx` ستلاحظ:

- **ورقة “Order_1”** — تحتوي على رأس الطلب 1 وصفين للمنتجين A و B.
- **ورقة “Order_2”** — تحتوي على رأس الطلب 2 وصف واحد للمنتج C.
- جميع الصيغ، التنسيقات، والرسوم البيانية من القالب الأصلي محفوظة.

![تقرير Excel مع أوراق منفصلة لكل طلب – مثال على مصنف مكتمل](/images/excel-report-example.png "تقرير Excel مولد ببيانات master‑detail")

*نص بديل للصورة: تقرير Excel مولد ببيانات master‑detail مع أوراق منفصلة لكل طلب، يوضح كيفية إنشاء تقرير Excel باستخدام C# و SmartMarker.*

---

## أسئلة شائعة وحالات خاصة

### ماذا لو أحتاج إلى ورقة ثابتة (مثل ملخص) إلى جانب الأوراق المتكررة؟

قم بتعيين `EnableRepeatingSheet = true` **فقط** على الورقة التي تحتوي على كتلة الـ master. الأوراق الأخرى ستبقى دون تعديل، لذا يمكنك الاحتفاظ بصفحة ملخص في القالب الأصلي.

### هل يمكنني استخدام DataTable بدلاً من الكائنات المجهولة؟

بالتأكيد. يعمل SmartMarker مع أي كائن يطبق `IEnumerable`. فقط استبدل النوع المجهول بـ `DataTable` وتأكد من أن أسماء الأعمدة تتطابق مع العلامات.

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### كيف أغيّر نمط تسمية الأوراق التي تم إنشاؤها؟

نفّذ واجهة `ISmartMarkerSheetNaming` مخصصة (أو عدل `workbook.Worksheets` بعد المعالجة). معظم المطورين يعيدون تسمية الأوراق بناءً على قيمة خلية:

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### ماذا لو كان القالب يستخدم صيغة عنصر نائب مختلفة؟

يسمح SmartMarker بتخصيص الفواصل عبر `SmartMarkerOptions`. على سبيل المثال، لاستخدام `<< >>` بدلاً من `{{ }}`:

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

---

## نصائح لتوسيع هذا النهج

- **قم بتخزين القالب في الذاكرة** إذا كنت تولد تقارير كثيرة لكل طلب؛ التحميل من القرص في كل مرة يضيف زمن استجابة.
- **اجمعه مع تحويل PDF** (`workbook.Save("report.pdf", SaveFormat.Pdf)`) للحصول على مخرجات صديقة للبريد الإلكتروني.
- **اجعل مسارات الملفات قابلة للمعايرة** باستخدام ملفات إعداد أو متغيرات بيئية لجعل الحل قابلًا للنقل بين بيئات التطوير، الاختبار، والإنتاج.
- **اختبر طبقة البيانات** بشكل منفصل؛ SmartMarker نفسه حتمي، لذا تحتاج فقط إلى التحقق من أن البيانات التي تزودها تتطابق مع المخطط المتوقع.

---

## الخلاصة

لقد غطينا **how to generate Excel report** في C# من البداية إلى النهاية، بدءًا من تحميل قالب SmartMarker إلى حفظ مصنف متعدد الأوراق يعكس علاقات master‑detail. عبر **populate Excel template C#** ببضع أسطر من الكود، تتجنب المنطق الهش الخلية‑ب‑خلية وتمنح المصممين حرية تشكيل المظهر النهائي.

الخطوات التالية قد تشمل:

- استخدام **populate Excel template C#** مع رسوم بيانية تتحدث تلقائيًا لكل ورقة.
- دمج **excel smartmarker c#** مع ASP.NET Core لبث التقارير مباشرةً إلى المتصفحات.
- أتمتة خطوط **c# excel automation** التي تسحب البيانات من APIs أو قواعد البيانات.

جرّبها، عدّل القالب، وشاهد كيف يمكنك تحويل البيانات الخام إلى تقرير Excel مصقول بسرعة. هل لديك أسئلة أو حالة استخدام مميزة؟ اترك تعليقًا أدناه — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}