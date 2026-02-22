---
category: general
date: 2026-02-21
description: تصدير البيانات إلى Excel عن طريق تحميل قالب Excel واستخدام Smart Markers
  لإنشاء تقرير Excel من مصفوفة. تعلم كيفية تعبئة قالب Excel بسرعة.
draft: false
keywords:
- export data to excel
- populate excel template
- load excel template
- generate excel report
- create excel from array
language: ar
og_description: تصدير البيانات إلى Excel باستخدام قالب SmartMarker. يوضح هذا الدليل
  كيفية تحميل قالب Excel، وإنشاء ملف Excel من مصفوفة، وتوليد تقرير Excel.
og_title: تصدير البيانات إلى إكسل – ملء قالب من مصفوفة
tags:
- C#
- Excel Automation
- Smart Markers
title: 'تصدير البيانات إلى إكسل: تعبئة قالب من مصفوفة في C#'
url: /ar/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير البيانات إلى Excel: ملء قالب من مصفوفة في C#

هل احتجت يومًا إلى **تصدير البيانات إلى Excel** لكنك لم تكن متأكدًا من كيفية تحويل مصفوفة عادية إلى مصنف منسق بشكل جميل؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما يحاولون مشاركة البيانات مع أصحاب المصلحة غير التقنيين لأول مرة. الخبر السار هو أنه ببضع أسطر من C# يمكنك **تحميل قالب Excel**، إضافة بياناتك، وتوليد **تقرير Excel** يبدو احترافيًا على الفور.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ يستخدم **Aspose.Cells Smart Markers** لملء قالب Excel. في النهاية ستتمكن من **إنشاء Excel من مصفوفة**، حفظ النتيجة، وفتح الملف لرؤية الصفوف المملوءة. لا أجزاء مفقودة، مجرد حل متكامل يمكنك نسخه ولصقه في مشروعك.

## ما ستتعلمه

- كيفية **تحميل قالب Excel** الذي يحتوي بالفعل على عناصر نائبة Smart Marker مثل `${OrderId}` و `${OrderItems:ItemName}`.  
- كيفية هيكلة مصدر البيانات بحيث يستطيع `SmartMarkerProcessor` التكرار على المجموعات.  
- كيفية **ملء قالب Excel** بمصفوفة متداخلة وإنتاج ملف **تقرير Excel** نهائي.  
- نصائح للتعامل مع الحالات الخاصة مثل المجموعات الفارغة أو مجموعات البيانات الكبيرة.  

**المتطلبات المسبقة**: .NET 6+ (أو .NET Framework 4.6+) وحزمة NuGet الخاصة بـ Aspose.Cells for .NET. إذا كنت تستخدم Visual Studio، فقط أضف الحزمة عبر مدير NuGet—لا حاجة لإعدادات إضافية.

![مخطط عملية تصدير البيانات إلى Excel](https://example.com/export-data-diagram.png "سير عمل تصدير البيانات إلى Excel")

## تصدير البيانات إلى Excel باستخدام قالب SmartMarker

أول شيء نحتاجه هو مصنف يعمل كهيكل لتقريرنا. فكر فيه كوثيقة Word تحتوي على حقول دمج، إلا أنه ملف Excel والحقول تُسمى **Smart Markers**.  

```csharp
// Step 1: Load the Excel template that contains Smart Markers (${OrderId}, ${OrderItems:ItemName})
var workbook = new Aspose.Cells.Workbook("YOUR_DIRECTORY/template.xlsx");
```

لماذا نحمّل قالبًا أصلاً؟ لأن التخطيط—عرض الأعمدة، أنماط العناوين، الصيغ—لا يحتاج إلى إعادة بناء في الكود. تصممه مرة واحدة في Excel، تضع العلامات، وتدع المكتبة تتولى الجزء الصعب.

## تحميل قالب Excel وإعداد البيئة

قبل أن نتمكن من معالجة أي شيء، يجب استيراد مساحة الأسماء `Aspose.Cells` والتأكد من وجود ملف القالب.  

```csharp
using Aspose.Cells;

// Verify template existence (optional but helpful)
if (!System.IO.File.Exists("YOUR_DIRECTORY/template.xlsx"))
{
    throw new System.IO.FileNotFoundException("Template file not found. Ensure the path is correct.");
}
```

> **نصيحة محترف:** احفظ القالب في مجلد `Resources` واضبط خاصية *Copy to Output Directory* للملف على *Copy always*؛ بهذه الطريقة يعمل المسار سواءً في بيئة التطوير أو بعد النشر.

## إعداد مصدر البيانات الخاص بك (إنشاء Excel من مصفوفة)

الآن يأتي الجزء الذي **ننشئ فيه Excel من مصفوفة**. يتوقع `SmartMarkerProcessor` كائنًا قابلًا للتعداد، لذا فإن النوع المجهول البسيط يعمل جيدًا.  

```csharp
// Step 2: Prepare the data source – an array of orders, each with an ID and a list of item names
var orderData = new[]
{
    new
    {
        OrderId = 1,
        OrderItems = new[]
        {
            new { ItemName = "Pen" },
            new { ItemName = "Paper" }
        }
    },
    new
    {
        OrderId = 2,
        OrderItems = new[]
        {
            new { ItemName = "Notebook" },
            new { ItemName = "Marker" },
            new { ItemName = "Eraser" }
        }
    }
};
```

لاحظ مصفوفة `OrderItems` المتداخلة—هذا يعكس العلامة `${OrderItems:ItemName}` في القالب. سيعيد المعالج تكرار الصف لكل عنصر، مملئًا عمود `ItemName` تلقائيًا.

إذا كان لديك بالفعل `List<Order>` أو `DataTable`، فقط مرّرها إلى المعالج؛ المفتاح هو أن تتطابق أسماء الخصائص مع العلامات.

## معالجة القالب لملء Excel

مع وجود المصنف والبيانات جاهزين، نقوم بإنشاء كائن `SmartMarkerProcessor` وندعّه يدمج البيانات.  

```csharp
// Step 3: Create a SmartMarkerProcessor for the loaded workbook
var processor = new Aspose.Cells.SmartMarkerProcessor(workbook);

// Step 4: Populate the template by processing the Smart Markers with the data source
processor.Process(orderData);
```

لماذا نستخدم `SmartMarkerProcessor`؟ لأنه أسرع من الكتابة اليدوية للخلية بخلية ويحافظ على ميزات Excel مثل الصيغ، الخلايا المدمجة، والتنسيق الشرطي. بالإضافة إلى ذلك، يوسّع الصفوف تلقائيًا للمجموعات—مثالي لسيناريوهات **ملء قالب Excel**.

## حفظ تقرير Excel المُولد

أخيرًا، نكتب المصنف المملوء إلى القرص.  

```csharp
// Step 5: Save the populated workbook to a new file
string outputPath = "YOUR_DIRECTORY/output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Excel report generated at: {outputPath}");
```

بعد تشغيل البرنامج، افتح `output.xlsx`. يجب أن ترى شيئًا مشابهًا لـ:

| OrderId | ItemName |
|---------|----------|
| 1       | Pen      |
| 1       | Paper    |
| 2       | Notebook |
| 2       | Marker   |
| 2       | Eraser   |

هذا هو **تقرير Excel مُولد** بالكامل من مصفوفة في الذاكرة، دون كتابة أي منطق حلقة يدويًا.

## التعامل مع الحالات الخاصة والمشكلات الشائعة

- **المجموعات الفارغة** – إذا كانت `OrderItems` فارغة لأحد الطلبات، سيتخطى Smart Markers الصف ببساطة. إذا كنت بحاجة إلى صف بديل، أضف علامة شرطية مثل `${OrderItems?ItemName:"(no items)"}`.  
- **مجموعات البيانات الكبيرة** – لآلاف الصفوف، فكر في تدفق الإخراج (`workbook.Save(outputPath, SaveFormat.Xlsx)` مُحسّن بالفعل، لكن يمكنك أيضًا تمكين `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference`.  
- **تحديث القالب** – عندما تغير أسماء العلامات، حدّث أسماء خصائص النوع المجهول وفقًا لذلك؛ وإلا سيتجاهل المعالج الحقول غير المتطابقة بصمت.  
- **تنسيق التاريخ/الرقم** – تنسيق الخلية في القالب هو السائد. إذا كنت تحتاج إلى تنسيق خاص بالثقافة، اضبط `NumberFormat` للخلية قبل المعالجة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق Console. يتضمن جميع بيانات `using`، معالجة الأخطاء، وتعليقات.  

```csharp
using System;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load the Excel template that contains Smart Markers
            // -------------------------------------------------
            string templatePath = "YOUR_DIRECTORY/template.xlsx";
            if (!System.IO.File.Exists(templatePath))
            {
                Console.WriteLine("Template not found. Please place template.xlsx in the specified folder.");
                return;
            }

            var workbook = new Workbook(templatePath);

            // -------------------------------------------------
            // 2️⃣ Prepare the data source – create excel from array
            // -------------------------------------------------
            var orderData = new[]
            {
                new
                {
                    OrderId = 1,
                    OrderItems = new[]
                    {
                        new { ItemName = "Pen" },
                        new { ItemName = "Paper" }
                    }
                },
                new
                {
                    OrderId = 2,
                    OrderItems = new[]
                    {
                        new { ItemName = "Notebook" },
                        new { ItemName = "Marker" },
                        new { ItemName = "Eraser" }
                    }
                }
            };

            // -------------------------------------------------
            // 3️⃣ Process the template – populate excel template
            // -------------------------------------------------
            var processor = new SmartMarkerProcessor(workbook);
            processor.Process(orderData);

            // -------------------------------------------------
            // 4️⃣ Save the generated Excel report
            // -------------------------------------------------
            string outputPath = "YOUR_DIRECTORY/output.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Export data to Excel completed. File saved at: {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح `output.xlsx`، وسترى البيانات مُعبأة بشكل أنيق. هذا كل شيء—عملك **تصدير البيانات إلى Excel** الآن مؤتمت بالكامل.

## الخلاصة

لقد استعرضنا حلًا كاملاً لـ **تصدير البيانات إلى Excel** باستخدام قالب مُصمم مسبقًا، ومصفوفة بسيطة كمصدر للبيانات، وAspose.Cells Smart Markers ل**ملء قالب Excel** تلقائيًا. في بضع خطوات فقط يمكنك **تحميل قالب Excel**، تحويل أي مجموعة إلى **تقرير Excel** مصقول، و**إنشاء Excel من مصفوفة** دون كتابة أي كود خلية منخفض المستوى.

ما الخطوة التالية؟ جرّب استبدال النوع المجهول بفئة `Order` حقيقية، أضف علامات أكثر تعقيدًا مثل `${OrderDate:MM/dd/yyyy}`، أو دمج هذه المنطق في Web API يُعيد الملف عند الطلب. النمط نفسه يعمل للفواتير، جداول المخزون، أو أي مخرجات جدولة تحتاج لمشاركتها.

هل لديك أسئلة أو سيناريو صعب؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}