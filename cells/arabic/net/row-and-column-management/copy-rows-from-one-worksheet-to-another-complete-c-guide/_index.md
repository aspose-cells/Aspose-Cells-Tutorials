---
category: general
date: 2026-07-29
description: انسخ الصفوف من ورقة عمل إلى أخرى وتعلم كيفية تحميل مصنف Excel برمجيًا
  باستخدام Aspose.Cells في دليل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: ar
lastmod: 2026-07-29
og_description: نسخ الصفوف من ورقة عمل إلى أخرى باستخدام Aspose.Cells. تعلم كيفية
  تحميل دفتر Excel برمجيًا والحفاظ على جداول Pivot في بضع أسطر فقط من C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: نسخ الصفوف من ورقة عمل إلى أخرى – دليل أتمتة Excel باستخدام C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: نسخ الصفوف من ورقة عمل إلى أخرى – دليل C# الكامل
url: /ar/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ الصفوف من ورقة عمل إلى أخرى – دليل C# الكامل

هل احتجت يومًا إلى **نسخ الصفوف من ورقة عمل إلى أخرى** لكن لم تكن متأكدًا من كيفية الحفاظ على الصيغ وجداول المحور دون تغيير؟ لست وحدك. في العديد من خطوط تقارير البيانات نحتاج إلى استخراج جزء من البيانات من ورقة رئيسية ووضعه في مصنف جديد للمعالجة اللاحقة. الخبر السار؟ باستخدام Aspose.Cells يمكنك القيام بذلك برمجيًا، وتستغرق العملية بأكملها بضع أسطر فقط.

في هذا الدرس سنستعرض تحميل مصنف Excel برمجيًا، تحديد نطاق، ثم نسخ تلك الصفوف إلى مصنف جديد تمامًا مع الحفاظ على أي جداول محور مدمجة. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#—بدون الحاجة إلى النسخ واللصق اليدوي.

## ما ستحققه

- **تحميل مصنف Excel برمجيًا** باستخدام فئة `Workbook` من Aspose.Cells.  
- تحديد **منطقة الخلايا** التي تحتوي على الصفوف التي تريد نقلها.  
- **نسخ الصفوف من ورقة عمل إلى أخرى** باستخدام استدعاء طريقة واحد يحافظ على جداول المحور.  
- حفظ النتيجة في ملف جديد جاهز للتوزيع أو المعالجة الإضافية.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل على .NET Core و .NET Framework على حد سواء).  
- رخصة Aspose.Cells صالحة (أو مفتاح تقييم مؤقت).  
- مجلدان على القرص: أحدهما لملف المصنف المصدر (`Source.xlsx`) والآخر للوجهة (`Destination.xlsx`).  

إذا كان لديك كل ذلك، لنبدأ.

## الخطوة 1: تحميل مصنف Excel برمجيًا

أولًا وقبل كل شيء—قبل أن تتمكن من نسخ أي شيء تحتاج إلى جلب ملف المصدر إلى الذاكرة. Aspose.Cells يجعل ذلك سهلًا:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **لماذا هذا مهم:** تحميل المصنف برمجيًا يمنحك التحكم الكامل في محتويات الملف دون الحاجة إلى فتح Excel على الخادم. كما أنه يتجنب مشاكل التفاعل مع COM ويعمل في بيئات بدون واجهة رسومية مثل خطوط أنابيب CI.

## الخطوة 2: تحديد نطاق المصدر الذي يحتوي على الصفوف

بعد ذلك، حدد بالضبط أي صفوف تريد نقلها. كائن `CellArea` يتيح لك تحديد كتلة مستطيلة باستخدام عناوين الخلية العليا‑اليسرى والسفلى‑اليمنى:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **نصيحة احترافية:** إذا كان حجم بياناتك يتغير ديناميكيًا، يمكنك حساب `EndRow` باستخدام `sourceWorksheet.Cells.MaxDataRow` لالتقاط الجدول بالكامل دائمًا.

## الخطوة 3: إنشاء مصنف جديد للوجهة

الآن أنشئ مصنفًا فارغًا سيتلقى الصفوف المنسوخة. هذا المصنف يبدأ بورقة عمل واحدة افتراضيًا:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **لماذا مصنف جديد؟** البدء بنظافة يضمن أنك لا تكتب فوق بيانات موجودة عن طريق الخطأ ويمنحك بيئة اختبار متوقعة.

## الخطوة 4: نسخ الصفوف من ورقة عمل إلى أخرى (مع الحفاظ على جداول المحور)

هذا هو جوهر الدرس. طريقة `CopyRows` تنسخ الصفوف المحددة، وعند تمرير `true` كمعامل أخير، تنسخ أيضًا أي جداول محور موجودة داخل النطاق:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### ما الذي يحدث خلف الكواليس؟

- **ورقة العمل المصدر**: `sourceWorkbook.Worksheets[0]` تشير إلى الورقة الأولى في ملف المصدر.  
- **فهارس الصفوف**: Aspose.Cells يستخدم فهرسة تبدأ من الصفر، لذا `StartRow` و `EndRow` تتطابقان مع الصفوف التي حددتها في `sourceRange`.  
- **صف البداية في الوجهة**: نبدأ من الصف 0 في الورقة الجديدة، مما يضع الكتلة المنسوخة في الأعلى تمامًا.  
- علامة `true`: هذه هي المفتاح السحري الذي يخبر Aspose.Cells بنسخ أي جداول محور موجودة داخل الصفوف المنسوخة، مع الحفاظ على ذاكرة التخزين المؤقت والاتصالات الخاصة بها.

> **تحذير حالة حافة:** إذا كان نطاق المصدر يحتوي على خلايا مدمجة تمتد خارج المنطقة المحددة، فسيتم قطع تلك الدمج. للحفاظ عليها، قم بتوسيع النطاق ليغطي بالكامل المنطقة المدمجة.

## الخطوة 5: حفظ مصنف الوجهة

أخيرًا، اكتب الملف الجديد إلى القرص. يمكنك اختيار أي مجلد تفضله؛ فقط تأكد من أن العملية لديها صلاحيات كتابة:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

عند فتح `Destination.xlsx` سترى الصفوف A1‑H20 مكررة، مع أي جداول محور كانت مدمجة أصلاً. باقي المصنف يبقى فارغًا، جاهزًا لإضافة أوراق أو بيانات أخرى لاحقًا.

## مثال كامل يعمل

بوضع كل الأجزاء معًا، إليك البرنامج الكامل القابل للتنفيذ:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

افتح ملف الوجهة وتحقق من أن البيانات، التنسيق، وجداول المحور تبدو تمامًا كما كانت في المصدر. إذا لاحظت أي بيانات مفقودة، تحقق مرة أخرى من أن `sourceRange` يغطي بالكامل الصفوف ذات الصلة.

## أسئلة شائعة ونصائح

- **هل يمكنني النسخ إلى ورقة عمل محددة بدلاً من الأولى؟**  
  بالتأكيد. استبدل `destinationWorkbook.Worksheets[0]` بـ `destinationWorkbook.Worksheets["TargetSheet"]` (أنشئ الورقة أولاً إذا لم تكن موجودة).

- **ماذا لو أردت نسخ القيم فقط دون الصيغ؟**  
  استخدم `CopyRows` مع التحميل الزائد الذي يقبل كائن `CopyRowsOptions` واضبط `PasteType` إلى `PasteType.Values`.

- **كيف أتعامل مع ملفات كبيرة دون استهلاك الذاكرة؟**  
  Aspose.Cells يدعم **البث** عبر `LoadOptions` مع `MemorySetting.MemoryPreference`. حمّل مصنف المصدر بأثر ذاكرة أقل وستظل عملية النسخ فعّالة.

- **هل تظل جداول المحور مرتبطة بمصدر البيانات الأصلي؟**  
  عند ضبط علامة `true`، يتم تكرار ذاكرة التخزين المؤقت للجداول، لذا تشير جداول المحور في المصنف الجديد إلى البيانات المنسوخة، وليس إلى الملف الأصلي.

## الخاتمة

أنت الآن تعرف كيفية **نسخ الصفوف من ورقة عمل إلى أخرى** مع الحفاظ على أي جداول محور، ورأيت كيف **تحمل مصنف Excel برمجيًا** باستخدام Aspose.Cells. هذا النمط يُعد أساسًا قويًا لبناء خطوط تقارير آلية، سكريبتات ترحيل بيانات، أو أي سيناريو يتطلب دمج بيانات Excel في الوقت الفعلي.

ما التالي؟ جرّب توسيع المقطع إلى:

- تكرار عبر نطاقات مصدر متعددة وتجميعها في ملف وجهة واحد.  
- تطبيق التنسيق الشرطي بعد النسخ لتسليط الضوء على المقاييس الرئيسية.  
- تصدير المصنف النهائي إلى PDF أو CSV للاستخدام اللاحق.

لا تتردد في التجربة، وإذا واجهت أي مشكلة، اترك تعليقًا أدناه. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية نسخ الصفوف في Excel باستخدام Aspose.Cells لـ .NET: دليل C#](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [نسخ ورقة عمل من مصنف إلى آخر باستخدام Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [كيفية تصدير الصفوف المرئية في Excel باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}