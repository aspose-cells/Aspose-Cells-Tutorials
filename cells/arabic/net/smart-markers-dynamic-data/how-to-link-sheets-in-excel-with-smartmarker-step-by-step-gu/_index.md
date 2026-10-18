---
category: general
date: 2026-06-08
description: كيفية ربط الأوراق في Excel باستخدام SmartMarkerProcessor لتقارير الرئيس‑التفاصيل.
  قم بملء ورقة الرئيس وإنشاء تقرير Excel رئيس‑تفاصيل بسهولة.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: ar
og_description: كيفية ربط الأوراق في Excel باستخدام SmartMarkerProcessor. تعلّم تعبئة
  الورقة الرئيسية وإنشاء تقرير رئيسي تفصيلي في دقائق.
og_title: كيفية ربط الأوراق في إكسل باستخدام SmartMarker – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: كيفية ربط الأوراق في إكسل باستخدام SmartMarker – دليل خطوة بخطوة
url: /ar/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ربط الأوراق في Excel باستخدام SmartMarker – دليل خطوة بخطوة

هل تساءلت يومًا **كيف تربط الأوراق** في Excel دون نسخ الصفوف يدويًا أو كتابة حلقات VBA لا نهائية؟ لست وحدك. يواجه معظم المطورين صعوبة عندما يحتاجون إلى تقرير master‑detail نظيف يبقى متزامنًا مع تغير البيانات. الخبر السار؟ يقوم SmartMarkerProcessor بالعمل الشاق نيابةً عنك، محولًا بضع أسطر من C# إلى مصنف master‑detail كامل.

في هذا الدرس سنستعرض الخطوات الدقيقة لـ **ملء ورقة الماستر**، إعداد ورقة التفاصيل، وأخيرًا **إنشاء تقرير master‑detail** يتحدث تلقائيًا. في النهاية ستحصل على نمط قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET.

> **ملاحظة المتطلبات المسبقة:** تحتاج إلى GrapeCity Documents for Excel (GcExcel) الإصدار 2024 أو أحدث، بيئة تطوير .NET (Visual Studio 2022 تعمل بشكل ممتاز)، ومعرفة أساسية بـ C#. لا توجد حزم NuGet إضافية مطلوبة بخلاف GcExcel.

---

## نظرة عامة على الحل

قبل الغوص في الكود، دعنا نفصل ما يعنيه “ربط الأوراق” فعليًا في سياق SmartMarker:

1. **Master sheet** – يحتوي على صف واحد لكل كيان (مثال: قائمة العملاء).
2. **Detail sheet** – يحتوي على الصفوف التي تنتمي إلى صف الماستر (مثال: الطلبات لكل عميل).
3. **SmartMarker syntax** – لغة توصيف صغيرة (`{MasterSheet}#master;{DetailSheet}#detail`) تخبر المعالج كيفية ربط جدولَي البيانات.
4. **Processor options** – تمكين `MasterDetail` يجعل المحرك يكرر صفوف الماستر تلقائيًا ويضمّ صفوف التفاصيل المرتبطة تحتها.

فهم هذه العناصر يساعدك على تعديل النهج لاحقًا — ربما تحتاج إلى تعشيق ثلاثي المستويات أو تنسيق شرطي. احتفظ بهذا النموذج الذهني في متناول يدك أثناء مرورنا على التنفيذ.

---

## الخطوة 1: إعداد البيانات الهرمية لمعالجة Master‑Detail

أول شيء تحتاجه هو مصدر بيانات يعكس علاقة master‑detail. في معظم السيناريوهات الواقعية يأتي هذا من قاعدة بيانات، ولكن للتوضيح سنستخدم كائنًا مجهولًا.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**لماذا هذا مهم:** لا يتخمين SmartMarker العلاقات بشكل سحري؛ إنه يبحث عن أسماء خصائص متطابقة (`MasterId` → `Id`). من خلال هيكلة البيانات بهذه الطريقة نوفر للمعالج خريطة واضحة، وهي الأساس لـ **كيفية ربط الأوراق** بفعالية.

> **نصيحة احترافية:** إذا كانت بياناتك موجودة في كائنات `DataTable`، فقط عرّفها كخصائص بنفس الأسماء — SmartMarker يعمل مع أي مجموعة قابلة للتعداد.

---

## الخطوة 2: إنشاء مصنف وتحميل قالب

يعمل SmartMarker على مصنف Excel موجود مسبقًا، عادةً قالب يحتوي بالفعل على أسماء الأوراق وعلامات العنصر النائب. لننشئ مصنفًا في الذاكرة ونضيف ورقتين فارغتين باسم *MasterSheet* و *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

يمكنك أيضًا تحميل ملف `.xlsx` من القرص (`wb.Open("Template.xlsx")`) إذا كنت تفضّل تصميم التخطيط في Excel أولاً. الجزء المهم هو أن تتطابق أسماء الأوراق مع تلك التي ستشير إليها في سلسلة SmartMarker.

---

## الخطوة 3: إنشاء SmartMarkerProcessor وتمكين وضع Master‑Detail

الآن نستدعي المحرك الذي سيقرأ العلامات ويلصق البيانات. يأخذ `SmartMarkerProcessor` المصنف كمعامل في المُنشئ، وعلم `Options.MasterDetail` يُخبره بمعاملة علامات `#master` و `#detail` كزوج مرتبط.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**لماذا تمكين `MasterDetail`؟** بدون هذا العلم، سيتعامل المعالج مع `{MasterSheet}#master` و `{DetailSheet}#detail` كعمليات مستقلة، مما يفقد العلاقة الحيوية بين الصفوف. ضبط العلم هو السطر الوحيد الذي يجعل **كيفية ربط الأوراق** تعمل فعليًا.

---

## الخطوة 4: تعريف سلسلة SmartMarker وتشغيل المعالج

سلسلة العلامة تخبر SmartMarker أي ورقة هي الماستر وأيها هي التفصيل. الصياغة بسيطة: `{SheetName}#master;{SheetName}#detail`. يمكنك أيضًا إضافة علامات إضافية (مثل `#header`) لكنها غير ضرورية لتقرير أساسي.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

عند تشغيل `Process`، يقوم المحرك بـ:

1. كتابة كل صف ماستر في *MasterSheet* بدءًا من أول صف فارغ بعد العنوان.
2. لكل صف ماستر، يفحص مجموعة `Details`، يختار الصفوف التي يتطابق فيها `MasterId` مع `Id` الخاص بالماستر، ويكتبها في *DetailSheet* مباشرةً تحت الإدخال الماستر المقابل.

---

## الخطوة 5: حفظ أو تصدير المصنف الناتج

في هذه المرحلة لديك مصنف مكتمل التعبئة. يمكنك حفظه على القرص، بثه مرة أخرى إلى عميل ويب، أو حتى تحويله إلى PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

افتح الملف وسترى ورقتين: *MasterSheet* تُظهر `A` و `B`، بينما *DetailSheet* تُظهر `Item1` تحت الماستر `1` و `Item2` تحت الماستر `2`. هذا هو جوهر **ملء ورقة الماستر** و **إنشاء تقرير master‑detail** في خطوة واحدة.

---

## نظرة بصرية عامة

![مخطط يوضح كيفية ربط الأوراق في Excel باستخدام SmartMarkerProcessor](https://example.com/diagram.png "مخطط ربط الأوراق")

المخطط (نص alt يتضمن الكلمة المفتاحية الأساسية) يُظهر تدفق البيانات من كائنات C# → SmartMarkerProcessor → أوراق Excel المرتبطة.

---

## معالجة الحالات الشائعة

### عدة صفوف تفصيلية لكل ماستر

إذا كان لصف ماستر عدة تفاصيل مرتبطة، يكرر SmartMarker صف الماستر مرة واحدة ثم يكتب *جميع* صفوف التفاصيل المتطابقة تحته. لا حاجة إلى كود إضافي — فقط تأكد من أن مجموعة `Details` تحتوي على كل صف.

### تفاصيل مفقودة

عندما لا يحتوي إدخال ماستر على صفوف تفاصيل متطابقة، تتخطى ورقة التفاصيل هذا القسم ببساطة. إذا كنت بحاجة إلى عنصر نائب (مثال: “No items”)، يمكنك إضافة عمود محسوب في القالب يستخدم صيغة Excel مثل `=IF(COUNTA(A2:B2)=0,\"No items\",\"\")`.

### مجموعات بيانات كبيرة

معالجة عشرات الآلاف من الصفوف قد تكون مستهلكة للذاكرة. للحفاظ على أداء سريع:

- استخدم `processor.Options.EnableStreaming = true` (متاح في GcExcel 2025+).
- قسّم البيانات إلى أجزاء وعالج كل جزء على حدة، ثم دمج المصنفات.

### تعيين أعمدة مخصص

إذا لم تتطابق أسماء الخصائص الخاصة بك (`MasterKey` مقابل `Id`)، يمكنك استخدام طريقة `SmartMarkerProcessor.Map` لإنشاء اسم مستعار قبل المعالجة.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## مثال عملي كامل

بجمع كل شيء معًا، إليك برنامجًا كاملًا جاهزًا للنسخ واللصق يمكنك تشغيله فورًا.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [معادلات الروابط الخارجية للماستر في Excel باستخدام Aspose.Cells للـ Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [أوراق Excel ديناميكية للماستر في Java باستخدام Aspose.Cells: دليل شامل](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [تقارير Excel ديناميكية للماستر باستخدام Aspose.Cells Java: نطاقات مسماة وصيغ معقدة](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}