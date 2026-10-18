---
category: general
date: 2026-02-28
description: إنشاء تقرير رئيسي وتفصيلي باستخدام C# وتعلم كيفية تعبئة قالب Excel، دمج
  البيانات في Excel، وتحميل ملف Excel باستخدام C# في بضع خطوات فقط.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: ar
og_description: إنشاء تقرير رئيسي وتفصيلي في C# باستخدام Aspose.Cells SmartMarker.
  تعلم كيفية تحميل مصنف Excel في C#، دمج البيانات في Excel، وتعبئة قالب Excel.
og_title: إنشاء تقرير رئيسي‑تفصيلي في C# – تعبئة قالب Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: إنشاء تقرير رئيسي‑تفصيلي في C# – تعبئة قالب Excel باستخدام SmartMarker
url: /ar/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء تقرير رئيس‑تفصيل في C# – تعبئة قالب Excel باستخدام SmartMarker

هل احتجت يوماً **إنشاء تقرير رئيس‑تفصيل** في C# لكنك لم تكن متأكدًا من كيفية جلب البيانات إلى ملف Excel؟ لست وحدك. في هذا الدليل سنستعرض الخطوات الدقيقة **لتعبئة قالب Excel**، **دمج البيانات في Excel**، و**تحميل دفتر عمل Excel C#**‑style بحيث تحصل على تقرير رئيس‑تفصيل مصقول جاهز للتوزيع.

سنستخدم Aspose.Cells SmartMarker، محرك قوي يفهم علاقات الرئيس‑تفصيل مباشرةً. بنهاية البرنامج التعليمي ستحصل على مثال كامل قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET. لا توجد اختصارات “انظر الوثائق” غير واضحة—فقط حل مستقل يمكنك نسخه‑ولصقه وتشغيله.

## ما ستتعلمه

- كيفية **إنشاء بيانات رئيس‑تفصيل** في C# تتطابق مباشرةً مع قالب Excel.
- الطريقة الدقيقة **لتحميل دفتر عمل Excel C#** التي تفتح ملف `.xlsx` يحتوي على وسوم SmartMarker.
- العملية **لتعبئة قالب Excel** عن طريق تشغيل `SmartMarkerProcessor`.
- نصائح للتعامل مع الحالات الخاصة، مثل الوسوم المفقودة أو مجموعات البيانات الكبيرة.
- كيفية التحقق من النتيجة وما يبدو عليه **تقرير الرئيس‑تفصيل** النهائي.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضاً على .NET Framework 4.8).
- Aspose.Cells for .NET (يمكنك الحصول على حزمة تجريبية مجانية عبر NuGet: `Install-Package Aspose.Cells`).
- ملف Excel أساسي (`template.xlsx`) يحتوي على وسوم SmartMarker (سنظهر لك العلامات الدنيا التي تحتاجها).

إذا كان لديك كل ذلك جاهزًا، فلنبدأ.

## الخطوة 1 – إنشاء مصدر بيانات الرئيس‑تفصيل *(how to create master detail)*

أول شيء تحتاجه هو كائن C# يمثل الصفوف الرئيسة (الطلبات) والصفوف الفرعية (عناصر الطلب). سيقرأ SmartMarker هذه الهرمية تلقائيًا عندما يتم تعيين `MasterDetail` إلى `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**لماذا هذا مهم:**  
SmartMarker يبحث عن خاصية تسمى `Orders` (الرئيس) ثم لكل طلب يبحث عن مجموعة تسمى `Items`. بمطابقة هذه الأسماء تحصل تلقائيًا على **تقرير رئيس‑تفصيل** دون كتابة أي حلقات بنفسك.

> **نصيحة احترافية:** اجعل أسماء الخصائص قصيرة ومعبرة؛ فهي تتحول إلى العناصر النائبة في قالب Excel الخاص بك.

## الخطوة 2 – ضبط خيارات SmartMarker لمعالجة الرئيس‑تفصيل

أخبر المحرك أنك تتعامل مع سيناريو رئيس‑تفصيل وامنحه اسم ورقة التفصيل التي ستستقبل الصفوف الفرعية.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**لماذا هذا مهم:**  
إذا حذفت `MasterDetail = true`، سيتعامل SmartMarker مع البيانات كقائمة مسطحة ولن تظهر صفوف التفصيل أبدًا. يجب أن يتطابق `DetailSheetName` مع اسم الورقة التي أنشأتها في القالب (حسّاس لحالة الأحرف).

## الخطوة 3 – تحميل دفتر عمل Excel بنمط C#

الآن نفتح القالب الذي يحتوي على وسوم SmartMarker. هذه هي خطوة **load Excel workbook C#** التي يخطئ فيها كثير من المطورين لأنهم ينسون استخدام مسار الملف الصحيح أو إغلاق دفتر العمل بشكل سليم.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**لماذا هذا مهم:**  
Aspose.Cells يقرأ كامل دفتر العمل إلى الذاكرة، لذا يمكن أن يكون الملف على القرص، مضمّنًا كمورد، أو حتى يُستَـ streaming من خدمة ويب. فقط تأكد أن المسار يشير إلى ملف `.xlsx` صالح يحتوي على الوسوم التي سنناقشها لاحقًا.

## الخطوة 4 – إدراج وسوم SmartMarker في القالب (populate Excel template)

إذا فتحت `template.xlsx` الآن، ستجد ورقتين:

- **Orders** – ورقة الرئيس مع صف مثل `&=Orders.Id`.
- **OrderDetail** – ورقة التفصيل مع صفوف مثل `&=Items.Sku` و `&=Items.Qty`.

إليك عرضًا بسيطًا للعلامات:

| الورقة | الخلية A1 | الخلية B1 |
|-------|----------|----------|
| Orders | `&=Orders.Id` | *(فارغ)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

لا تحتاج إلى كتابة أي كود للوسوم—فهي موجودة في ملف Excel. خطوة **populate Excel template** هي ببساطة استدعاء المعالج:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**لماذا هذا مهم:**  
المعالج يفحص كل ورقة، يستبدل العناصر النائبة `&=` بالقيم الفعلية، ويوسّع الصفوف لكل سجل رئيس وتفصيل. لأن `MasterDetail` مفعّل، يتم إنشاء صف جديد تلقائيًا لكل عنصر تحت الطلب المناسب.

## الخطوة 5 – حفظ تقرير الرئيس‑تفصيل

أخيرًا، اكتب دفتر العمل المعبأ إلى القرص. هذه هي اللحظة التي تحصل فيها على **تقرير رئيس‑تفصيل** جاهز للمشاركة.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**الناتج المتوقع:**  

- ورقة **Orders** تعرض صفين: `1` و `2` (معرفات الطلبات).  
- ورقة **OrderDetail** تعرض ثلاثة صفوف:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

هذا هو **إنشاء تقرير رئيس‑تفصيل** كامل الوظائف يمكنك إرساله بالبريد، طباعته، أو إرساله إلى نظام آخر.

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان القالب يفتقد وسمًا؟
SmartMarker يتجاهل الوسوم غير المعروفة بصمت، لكن ستحصل على خلايا فارغة. تحقق من تهجئة الوسم وتأكد أن أسماء الخصائص في كائن C# تتطابق تمامًا.

### كيف يتعامل مع مجموعات بيانات كبيرة؟
المعالج يبث الصفوف، لذا حتى آلاف سجلات التفصيل لن تستهلك الذاكرة بشكل مفرط. مع ذلك، للملفات الضخمة جدًا قد ترغب في زيادة `MemorySetting` في `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### هل يمكنني استخدام اسم ورقة مختلف للماستر؟
نعم—فقط أعد تسمية الورقة في القالب واضبط `DetailSheetName` إذا كان لديك ورقة تفصيل. اسم ورقة الماستر يُستنتج من العنصر النائب (`&=Orders.Id`).

### ماذا لو احتجت لإضافة صف إجمالي؟
أضف صيغة Excel عادية في القالب (مثلاً `=SUM(B2:B{#})`). سيحافظ SmartMarker على الصيغة بعد إدخال البيانات.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق Console. يتضمن جميع توجيهات `using`، نموذج البيانات، الخيارات، وتعامل الملفات.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح `output.xlsx`، وسترى بيانات الرئيس‑تفصيل مُعبأة بشكل جميل.

## مرجع بصري

![إنشاء تقرير رئيس‑تفصيل - لقطة شاشة للنتيجة](https://example.com/images/master-detail-report.png "مثال على إنشاء تقرير رئيس‑تفصيل")

*تُظهر الصورة ورقة Orders مع المعرفات 1 و 2، وورقة OrderDetail مع صفوف SKU‑Qty الثلاثة.*

## الخلاصة

أنت الآن تعرف **كيفية إنشاء تقرير رئيس‑تفصيل** في C# باستخدام Aspose.Cells SmartMarker، من بناء مصدر البيانات إلى **loading Excel workbook C#**، **populating Excel template**، وأخيرًا.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}