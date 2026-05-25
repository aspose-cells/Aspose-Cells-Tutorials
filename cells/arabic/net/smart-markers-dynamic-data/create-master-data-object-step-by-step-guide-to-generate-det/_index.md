---
category: general
date: 2026-02-14
description: إنشاء كائن بيانات رئيسية في C# وتوليد ورقة تفاصيل بسهولة. تعلّم سير عمل
  SmartMarker الكامل مع أمثلة عملية على الشيفرة.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: ar
og_description: أنشئ كائن البيانات الرئيسي في C# وقم بإنشاء ورقة تفاصيل باستخدام SmartMarker.
  اتبع دليلنا التفصيلي للحصول على حل جاهز للتنفيذ.
og_title: إنشاء كائن البيانات الرئيسي – دليل كامل
tags:
- C#
- SmartMarker
- Excel Automation
title: إنشاء كائن البيانات الرئيسي – دليل خطوة بخطوة لإنشاء ورقة التفاصيل
url: /ar/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء كائن بيانات رئيسية – دليل كامل

هل احتجت يوماً إلى **إنشاء كائن بيانات رئيسية** لورقة عمل Excel لكنك لم تكن متأكدًا من كيفية ربطه بصفحة تفاصيل SmartMarker؟ لست وحدك. في العديد من سيناريوهات التقارير، يقوم الكائن الرئيسي بتشغيل صفحة تفاصيل ديناميكية، وقد يشعر ضبط التوصيلات بشكل صحيح كأنك تُجمع لغزًا بدون صورة.  

في هذا الدليل سنستعرض العملية بالكامل—بناء كائن البيانات الرئيسي، تكوين خيارات SmartMarker لت **توليد ورقة تفاصيل**، وأخيرًا تشغيل المعالج. في النهاية ستحصل على مقطع شفرة قابل للتنفيذ يمكنك لصقه في أي مشروع .NET يستخدم مكتبة GrapeCity Documents for Excel (GcExcel).

## ما ستحتاجه

- .NET 6+ (أو .NET Framework 4.7.2) مع إشارة إلى `GcExcel.dll`
- إلمام أساسي بـ C# (المتغيرات، الأنواع المجهولة، مُبادئ تهيئة الكائن)
- مصنف Excel يحتوي بالفعل على وسوم SmartMarker مثل `{{OrderId}}` وجدول لعنصر السطر
- Visual Studio، Rider، أو أي محرر تفضله

هذا كل ما تحتاجه—لا حزم NuGet إضافية بخلاف توزيع GcExcel الأساسي.

## الخطوة 1: إنشاء كائن البيانات الرئيسي

أول شيء يجب عليك فعله هو **إنشاء كائن بيانات رئيسية** يعكس البنية المتوقعة من وسوم SmartMarker. فكر فيه كأنه نموذج تقرير صغير في الذاكرة.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

لماذا نستخدم نوعًا مجهولًا هنا؟ لأنه يتيح لك تعريف حاوية خفيفة الوزن دون إعلان فئة كاملة—مثالي للعرض السريع أو عندما لا يتوقع أن يتغير الشكل. إذا احتجت نموذجًا قابلاً لإعادة الاستخدام لاحقًا، ما عليك سوى استبدال `var` بـ POCO مناسب.

> **نصيحة احترافية:** حافظ على أن تكون أسماء الخصائص (`OrderId`, `Product`, `Quantity`) مطابقة تمامًا للمتغيّرات في ورقة العمل؛ SmartMarker يطابقها بغض النظر عن حالة الأحرف.

## الخطوة 2: تكوين خيارات SmartMarker لتوليد ورقة تفاصيل

الآن نخبر SmartMarker أننا نريد ورقة عمل منفصلة لجدول عناصر السطر. هنا يأتي دور كلمة **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

نمط `DetailSheetNewName` يستخدم وسوم بين أقواس معقوفة يتم استبدالها وقت التشغيل. في مثالنا ستُسمى الورقة `Order_1`. إذا قمت لاحقًا بالتكرار عبر عدة طلبات، سيحصل كل طلب على تبويب خاص به—تمامًا ما يتوقعه معظم المحاسبين.

## الخطوة 3: تشغيل معالج SmartMarker

مع وجود البيانات والخيارات جاهزة، الخطوة الأخيرة هي استدعاء المعالج على ورقة العمل المستهدفة.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

في الخلفية، يقوم SmartMarker بمسح ورقة العمل بحثًا عن الوسوم، يحقن قيم `orderData`، وبما أن `DetailSheet` يساوي `true`، فإنه ينسخ القالب إلى ورقة جديدة تُسمى `Order_1`. تظهر جميع عناصر السطر في منطقة التفاصيل، مع الحفاظ على أي تنسيق قمت بتطبيقه في القالب.

### مثال عملي كامل

فيما يلي برنامج وحدة تحكم مستقل يفتح مصنف القالب (`Template.xlsx`)، ينفذ الخطوات الثلاث، ويحفظ النتيجة كـ `Result.xlsx`. يمكنك نسخ‑لصق هذا في مشروع وحدة تحكم جديد والضغط على **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### النتيجة المتوقعة

- **Result.xlsx** يحتوي على ورقة تسمى `Order_1`.
- الخلية `A1` (أو أي مكان وضعت فيه `{{OrderId}}`) الآن تُظهر `1`.
- جدول يبدأ من كتلة SmartMarker يُظهر صفين:
  | المنتج | الكمية |
  |--------|--------|
  | A      | 2      |
  | B      | 5      |

إذا فتحت الملف، ستلاحظ أن التنسيق من القالب محفوظ—الحدود، الخطوط، التنسيق الشرطي—كلها لا تزال كما هي.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان لدي عدة طلبات؟

قم بلف كائن البيانات الرئيسي في مجموعة ودع SmartMarker يتكرر تلقائيًا:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

كل طلب يولد ورقة خاصة به (`Order_1`, `Order_2`, …). يعامل المعالج المصفوفة الخارجية كمجموعة رئيسية.

### كيف أتحكم في موضع الورقة؟

عيّن `smartMarkerOptions.DetailSheetInsertIndex = 2;` لوضع الورقة الجديدة بعد التبويب الثاني، أو استخدم `DetailSheetInsertAfter = "Summary"` للإدراج بعد ورقة مسماة.

### هل يمكن تعطيل ورقة التفاصيل لتشغيل معين؟

ما عليك سوى تبديل `DetailSheet = false;`. سيكتب SmartMarker عندها عناصر السطر في نفس الورقة التي توجد فيها وسوم البيانات الرئيسية.

### ماذا عن مجموعات البيانات الكبيرة؟

SmartMarker يبث البيانات بكفاءة، لكن إذا تجاوزت بضع مئات آلاف صفًا قد تصادف حد 1,048,576 صفًا في Excel. في هذه الحالة قسّم البيانات إلى عدة سجلات رئيسية أو فكر في التصدير إلى CSV.

## نظرة بصرية

![مخطط يوضح كيفية إنشاء كائن بيانات رئيسية وتوليد ورقة تفاصيل باستخدام SmartMarker](/images/smartmarker-flow.png)

*التوضيح يُظهر التدفق من كائن البيانات الرئيسي في C# → خيارات SmartMarker → معالجة ورقة العمل → ورقة تفاصيل جديدة.*

## الخلاصة

أنت الآن تعرف كيف **تنشئ كائن بيانات رئيسية** في C# وتُكوّن SmartMarker لت **توليد ورقة تفاصيل** تلقائيًا. نمط الثلاث خطوات—البيانات، الخيارات، المعالج—يغطي معظم سيناريوهات أتمتة Excel باستخدام GcExcel.  

من هنا قد ترغب في استكشاف:

- إضافة بيانات رأس/تذييل إلى كل ورقة تفاصيل
- استخدام التنسيق الشرطي بناءً على حالة الطلب
- تصدير المصنف المُنتج إلى PDF باستخدام `workbook.SaveAsPdf(...)`

لا تتردد في التجربة، وكسر الأشياء، ثم إعادتها معًا. هذه أسرع طريقة لإتقان أتمتة أوراق العمل. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}