---
category: general
date: 2026-05-23
description: كيفية استخدام العلامات مع Aspose.Cells لتحقيق تسمية أوراق ديناميكية في
  أتمتة Excel. تعلم العلامات الذكية وربط بيانات JSON وإنشاء الأوراق في دقائق.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: ar
og_description: كيفية استخدام العلامات في Aspose.Cells لإنشاء ملفات Excel مع تسمية
  أوراق ديناميكية. دليل كامل خطوة بخطوة مع مثال كامل بلغة C#.
og_title: كيفية استخدام العلامات – تسمية الأوراق الديناميكية في إكسل باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية استخدام العلامات في Aspose.Cells لتسمية الأوراق الديناميكية في Excel
url: /ar/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام العلامات في Aspose.Cells لتسمية الأوراق ديناميكياً في Excel

هل تساءلت يوماً **كيف تستخدم العلامات** لتحويل قالب Excel ثابت إلى دفتر عمل شامل بنظام رئيس‑تفصيل؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى إمكانيات *تسمية الأوراق ديناميكياً في Excel*، خاصة عندما يجب أن تعكس أسماء الأوراق قيم البيانات القادمة من JSON أو قاعدة بيانات.  

في هذا الدرس سنستعرض مثالاً كاملاً وجاهزاً للتنفيذ بلغة C# يوضح **كيفية استخدام العلامات** مع **Aspose.Cells** smart markers، ربط بيانات JSON، والسماح للمعالج بإنشاء أوراق تتغير أسماؤها أثناء التشغيل. لا إطالة، فقط الشيفرة الدقيقة التي يمكنك لصقها في Visual Studio ورؤية النتائج فوراً.

## ما ستتعلمه

- مفهوم **smart markers** ولماذا هي مثالية لسيناريوهات الرئيس‑تفصيل.  
- كيفية تضمين وسوم العلامات في دفتر العمل لتُستبدل لاحقاً بأسماء الأوراق الفعلية.  
- إعداد **dynamic sheet naming excel** باستخدام خيار `DetailSheetNewName`.  
- تشغيل `SmartMarkerProcessor` على بيانات JSON لتوليد عدة أوراق تلقائياً.  
- التحقق من النتيجة وبعض النصائح العملية لتجنب المشكلات الشائعة.

> **المتطلبات المسبقة** – تحتاج إلى بيئة تشغيل .NET حديثة (≥ .NET 6)، مكتبة Aspose.Cells for .NET (يمكنك الحصول على نسخة تجريبية مجانية من Aspose)، وإلمام أساسي بلغة C#.  

---

![مثال على كيفية استخدام العلامات في Aspose.Cells](example.png "مثال على كيفية استخدام العلامات في Aspose.Cells")

## كيفية استخدام العلامات لإنشاء تسمية أوراق ديناميكية (الخطوة 1)

الخطوة الأولى هي إنشاء دفتر عمل فارغ سيعمل كقالب لنا. في مشروع حقيقي قد تبدأ من ملف `.xlsx` موجود مسبقاً يحتوي على التخطيط، التنسيق، وخلايا العنصر النائب. لتوضيح الفكرة سننشئ كل شيء برمجياً.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*لماذا هذا مهم*: كائن `Worksheet` هو المكان الذي سنضع فيه وسوم **smart marker**. فكر في الوسوم كعناصر نائبة صغيرة سيستبدلها المعالج لاحقاً بقيم فعلية من JSON.  

## إدراج وسوم Smart Marker (الخطوة 2)

الآن نضع وسوم العلامة مباشرةً في الخلايا. الصيغة `${...}` تخبر Aspose.Cells “هذه علامة”. في مثالنا نحتاج إلى علامتين: واحدة لاسم ورقة الماستر وأخرى لاسم ورقة التفاصيل.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **نصيحة محترف** – احرص على أن تكون أسماء العلامات قصيرة ومعبرة؛ لأنها تصبح المفاتيح التي ستستخدمها في حمولة JSON الخاصة بك.

## إعداد بيانات JSON (الخطوة 3)

المعالج يعمل مع أي مصدر بيانات يمكن تمثيله كـ JSON، أو `DataSet`، أو حتى كائن عادي. إليك سلسلة JSON بسيطة تحتوي على مجموعة رئيس‑تفصيل. لاحظ أن كل طلب يحمل كل من `MasterSheetName` و `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*لماذا JSON؟* إنه خفيف الوزن، قابل للقراءة البشرية، ويتكامل بشكل ممتاز مع واجهات برمجة التطبيقات الويب. يمكنك أيضاً سحب هذه البيانات من استعلام SQL وتحويلها إلى JSON باستخدام `Newtonsoft.Json`.

## تهيئة SmartMarkerProcessor (الخطوة 4)

`SmartMarkerProcessor` هو المحرك الذي يمسح دفتر العمل، يجد العلامات، ويقوم بربط البيانات. إنشاءه سطر واحد فقط.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## تعريف تسمية أوراق ديناميكية (الخطوة 5)

هنا يتألق مفهوم **dynamic sheet naming excel** حقاً. عبر ضبط `DetailSheetNewName`، نخبر المعالج بإنشاء ورقة تفاصيل جديدة لكل طلب وتسميتها بناءً على `OrderId`. المتغير `${OrderId}` يُستبدل بالقيمة الحالية أثناء المعالجة.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **احذر** – إذا نسيت تضمين صيغة `${}`، ستصبح اسم الورقة حرفياً “Detail_${OrderId}” بدلاً من “Detail_1”، “Detail_2”، إلخ.

## تطبيق JSON وتوليد الأوراق (الخطوة 6)

الآن نترك المعالج يقوم بالعمل الشاق. سيقرأ JSON، يستبدل العلامات، ويخلق أوراق عمل جديدة حسب الحاجة.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### ما الذي يحدث خلف الكواليس؟

1. يقرأ المعالج مصفوفة `Orders`.  
2. لكل طلب ينشئ **ورقة ماستر** (باستخدام `${Orders.MasterSheetName}`) و**ورقة تفاصيل** (باستخدام نمط `DetailSheetNewName`).  
3. تُستبدل قيم الخلايا بالحقول المقابلة من JSON، لذا فإن الخلية الأولى في ورقة الماستر ستحتوي على “Master_1”، “Master_2”، إلخ.  

## حفظ النتيجة والتحقق منها (اختياري)

أخيراً، احفظ دفتر العمل على القرص. افتح الملف في Excel ويجب أن ترى ورقتين ماستر (`Master_1`, `Master_2`) وورقتين تفاصيل مسماة ديناميكياً (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**الناتج المتوقع** – بعد فتح `output.xlsx` ستظهر:

- ورقة **Master_1** مع الخلية A1 = “Master_1”.  
- ورقة **Detail_1** مع الخلية A1 = “Detail_1”.  
- ورقة **Master_2** مع الخلية A1 = “Master_2”.  
- ورقة **Detail_2** مع الخلية A1 = “Detail_2”.  

هذا هو الدورة الكاملة **كيفية استخدام العلامات** لتحقيق **dynamic sheet naming excel** باستخدام **Aspose.Cells smart markers**.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى أكثر من مستويين من التسلسل الهرمي؟

يمكنك تعشيق العلامات داخل أوراق التفاصيل التي تم إنشاؤها حديثاً. ما عليك سوى وضع وسوم `${...}` إضافية في ورقة القالب قبل المعالجة. سيقوم المعالج بالتدرج عبر كل مستوى تلقائياً.

### هل يمكنني استخدام DataTable بدلاً من JSON؟

بالتأكيد. يحتوي `SmartMarkerProcessor` على إصدارات متجاوزة لـ `DataSet`، `DataTable`، وحتى الكائنات المخصصة. التغيير الوحيد هو استدعاء `ApplyJson` → ستستخدم `ApplyDataSet(myDataSet)` بدلاً منه.

### كيف أتحكم في ترتيب إنشاء الأوراق؟

الترتيب يتبع تسلسل مجموعة المصدر. إذا احتجت إلى ترتيب مخصص، قم بفرز مصفوفة JSON (أو DataTable) قبل تمريرها إلى المعالج.

### هل هناك طريقة لإخفاء ورقة القالب بعد المعالجة؟

نعم. اضبط `sm.Options.RemoveTemplateSheets = true;` قبل استدعاء `ApplyJson`. سيتم إزالة الورقة الأصلية (الفهرس 0) من دفتر العمل النهائي.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في مشروع C# جديد من نوع Console. تأكد من إضافة حزمة NuGet الخاصة بـ `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

شغّل البرنامج، افتح `output.xlsx` وسترى الأوراق الديناميكية تماماً كما تم وصفه سابقاً.

---

## الخلاصة

لقد استعرضنا **كيفية استخدام العلامات** في Aspose.Cells لتحويل دفتر عمل بسيط إلى حل رئيس‑تفصيل مع **dynamic sheet naming excel**. النقاط الأساسية هي:

1. ضع وسوم `${...}` حيث تريد ظهور البيانات.  
2. زوّد `SmartMarkerProcessor` ببيانات JSON (أو أي مصدر مدعوم).  
3. استخدم `DetailSheetNewName` لتسمية الأوراق الجديدة تلقائياً أثناء المعالجة.  

من هنا يمكنك استكشاف سيناريوهات أكثر تقدماً—إضافة جداول، تنسيق خلايا، أو حتى تضمين مخططات—كل ذلك مدفوعاً بالبيانات.

## دروس ذات صلة

- [How to Implement Aspose.Cells Smart Markers in C# for Dynamic Excel Reporting](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Mastering Aspose.Cells .NET: Implement Smart Markers and Custom Labels for Dynamic Excel Reports](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}