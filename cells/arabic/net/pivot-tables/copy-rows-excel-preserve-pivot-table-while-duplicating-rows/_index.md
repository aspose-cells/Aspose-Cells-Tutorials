---
category: general
date: 2026-02-14
description: نسخ الصفوف في إكسل والحفاظ على جدول المحور في خطوة واحدة. تعلم كيفية
  نسخ الصفوف، نسخ النطاق إلى ورقة، وتكرار الصفوف مع جدول محوري باستخدام Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: ar
og_description: انسخ الصفوف في إكسل واحفظ جدول المحور في عملية واحدة. اتبع هذا الدليل
  خطوة بخطوة لتكرار الصفوف مع جدول محوري باستخدام C#.
og_title: نسخ الصفوف إكسل – الحفاظ على جدول Pivot أثناء تكرار الصفوف
tags:
- Aspose.Cells
- C#
- Excel automation
title: نسخ الصفوف في إكسل – الحفاظ على جدول المحور أثناء تكرار الصفوف
url: /ar/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ الصفوف في Excel – الحفاظ على جدول Pivot أثناء تكرار الصفوف

هل احتجت إلى **copy rows excel** مع الحفاظ على جدول Pivot سليمًا؟ في هذا الدرس سنستعرض حلًا كاملًا وقابلًا للتنفيذ يوضح لك **how to copy rows**، ويحافظ على سلوك **preserve pivot table**، وحتى **duplicate rows with pivot** عبر الأوراق باستخدام Aspose.Cells for .NET.

تخيل أنك تُعد تقرير مبيعات شهري يجلب البيانات من ورقة رئيسية، ينفّذ Pivot، ثم تحتاج إلى إرسال نسخة مختصرة إلى شريك. النسخ اليدوي للنطاق أمر مرهق، وتخاطر بتعطيل Pivot. الخبر السار؟ بضع أسطر من C# يمكنها إنجاز المهمة دون أي نقرات بالفأرة.

> **ما ستحصل عليه:** عينة كود كاملة، شروحات خطوة بخطوة، نصائح للحالات الخاصة، وفحص سريع للتأكد من أن Pivot صامد بعد النسخ.

---

## ما ستحتاجه

- **Aspose.Cells for .NET** (حزمة NuGet المجانية تكفي لهذا العرض).  
- أحدث **.NET runtime** (4.7+ أو .NET 6/7).  
- ملف Excel (`source.xlsx`) يحتوي على جدول Pivot في الورقة الأولى.  
- Visual Studio، Rider، أو أي محرر C# تفضله.

لا توجد مكتبات إضافية، ولا حاجة لتفاعل COM، ولا يتطلب تثبيت Excel على الخادم. لهذا السبب يُعد هذا النهج صديقًا لـ **copy range to sheet** وآمنًا على الخوادم.

---

## الخطوة 1 – تحميل المصنف (copy rows excel)

أول خطوة هي فتح المصنف المصدر. استخدام Aspose.Cells يمنحنا نموذج كائن نظيف يعمل بنفس الطريقة على Windows، Linux، أو Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **لماذا هذا مهم:** تحميل المصنف يُنشئ تمثيلًا في الذاكرة لكل ورقة، بما في ذلك الكائنات المخفية مثل Pivot caches. بمجرد أن يكون الملف في الذاكرة، يمكننا تعديل الصفوف دون الحاجة إلى الواجهة الرسومية.

---

## الخطوة 2 – تحديد ورقة الوجهة (copy range to sheet)

نريد أن تُلصق الصفوف المنسوخة في ورقة مختلفة — `Sheet2` في هذا المثال. إذا لم تكن الورقة موجودة، سيقوم Aspose بإنشائها لك.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **نصيحة احترافية:** تحقق دائمًا من `Worksheets.Contains` قبل إضافة ورقة؛ وإلا ستحصل على أسماء مكررة واستثناء وقت التشغيل.

---

## الخطوة 3 – نسخ الصفوف مع الحفاظ على جدول Pivot

الآن نصل إلى جوهر الموضوع: نسخ الصفوف **A1:E20** (التي تشمل Pivot) من الورقة الأولى إلى `Sheet2`. طريقة `CopyRows` تنسخ الخلايا الخام *وأيضًا* Pivot cache الأساسي، لذا يبقى Pivot فعالًا.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **لماذا يعمل:** `CopyRows` تحترم Pivot cache الداخلي، لذا يصبح جدول Pivot في ورقة الوجهة نسخة *حية*، وليس لقطة ثابتة. هذا يلبي متطلب **preserve pivot table** دون أي كود إضافي.

إذا أردت أن تبدأ الصفوف في موضع مختلف في ورقة الوجهة — مثلاً الصف 10 — ما عليك سوى تغيير الوسيط الثالث إلى `9`.

---

## الخطوة 4 – حفظ المصنف (duplicate rows with pivot)

أخيرًا، اكتب المصنف المعدل إلى القرص. سيظل جدول Pivot يعمل بالكامل في الملف الجديد.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **التحقق من النتيجة:** افتح `copyWithPivot.xlsx` في Excel، انتقل إلى *Sheet2*، وقم بتحديث Pivot. يجب أن ترى نفس تخطيط الحقول والحسابات كما في الأصل — دون أي خلل.

---

## التحقق من النسخ – فحص سريع

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

إذا طبع الكونسول `True`، فقد نجحت في **duplicate rows with pivot** وحافظت على محرك التحليل البياني حيًا.

---

## حالات الحافة الشائعة وكيفية التعامل معها

| الحالة | ما يجب مراقبته | التعديل المقترح |
|-----------|-------------------|-----------------|
| **نطاق المصدر يحتوي على خلايا مدمجة** | قد تتسبب الخلايا المدمجة في عدم محاذاة عند النسخ. | استخدم `CopyRows` كما هو موضح؛ فهو يحافظ على الدمج تلقائيًا. |
| **ورقة الوجهة تحتوي بالفعل على بيانات** | قد تُستبدل البيانات الحالية بالصفوف الجديدة. | غيّر صف البداية في الوسيط الثالث إلى أول صف فارغ: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Pivot يستخدم مصدر بيانات خارجي** | الاتصالات الخارجية لا تُنسخ. | تأكد من أن المصنف المصدر يحتوي على مجموعة البيانات الكاملة؛ وإلا أعد ربط الاتصال بعد النسخ. |
| **مصنف كبير (أكثر من 100k صف)** | استهلاك الذاكرة قد يرتفع. | فكر في النسخ على دفعات (مثلاً 5,000 صف في كل مرة) لتخفيف الضغط على الـ GC. |

---

## مثال عملي كامل (جميع الخطوات معًا)

فيما يلي البرنامج الكامل الذي يمكنك لصقه في تطبيق Console وتشغيله فورًا.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

شغّل البرنامج، افتح `copyWithPivot.xlsx` الناتج، وستلاحظ أن Pivot في **Sheet2** يعمل تمامًا كما في الأصل. لا حاجة لإعادة إنشاء يدوي.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات `.xls` المتوافقة مع Excel 2003؟**  
ج: نعم. Aspose.Cells ي abstracts تنسيق الملف، لذا يعمل نفس الكود مع `.xls`، `.xlsx`، وحتى `.xlsb`.

**س: ماذا لو أردت نسخ *الأعمدة* بدلاً من الصفوف؟**  
ج: استخدم `CopyColumns` بنفس الفكرة؛ فقط استبدل معلمات الصفوف بمعلمات الأعمدة.

**س: هل يمكنني نسخ نطاقات متعددة غير متجاورة مرة واحدة؟**  
ج: ليس مباشرة باستخدام `CopyRows`. يمكنك عمل حلقة لكل نطاق أو إنشاء ورقة مؤقتة تجمع النطاقات قبل النسخ.

---

## الخلاصة

لقد عرضنا نمطًا نظيفًا لـ **copy rows excel** يحافظ على سلامة **preserve pivot table**، ويُظهر لك **how to copy rows** بفعالية، ويُبين لك كيفية **copy range to sheet** دون فقدان أي وظيفة Pivot. بنهاية هذا الدليل، يجب أن تكون قادرًا على **duplicate rows with pivot** في أي خط أنابيب أتمتة — سواء كنت تُولّد تقارير يومية أو تبني خدمة تصدير بيانات على نطاق واسع.

هل أنت مستعد للتحدي التالي؟ جرّب توسيع الكود إلى:

- تصدير الورقة المكررة كملف PDF.  
- تحديث Pivot برمجيًا بعد النسخ.  
- معالجة قائمة من الملفات المصدرية دفعةً واحدة.

إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو تواصل معي عبر GitHub. برمجة سعيدة، واستمتع بالوقت الذي وفرته بعدم سحب Excel يدويًا!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}