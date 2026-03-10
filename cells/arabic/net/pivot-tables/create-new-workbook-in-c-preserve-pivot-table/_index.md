---
category: general
date: 2026-02-15
description: إنشاء مصنف جديد في C# ونسخ جدول محوري دون فقدان تعريفه. تعلم كيفية نسخ
  الصفوف، الحفاظ على الجدول المحوري، وتكرار الجدول المحوري بسهولة.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: ar
og_description: إنشاء دفتر عمل جديد في C# ونسخ جدول محوري مع الحفاظ على تعريفه. دليل
  خطوة بخطوة للمطورين.
og_title: إنشاء دفتر عمل جديد في C# – الحفاظ على الجدول المحوري
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف جديد في C# – الحفاظ على جدول المحوري
url: /ar/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

code blocks: placeholders only.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل جديد في C# – الحفاظ على جدول Pivot

هل احتجت يومًا إلى **إنشاء دفتر عمل جديد** في C# يحتوي على نسخة مطابقة تمامًا من جدول Pivot من ملف آخر؟ لست وحدك. في العديد من خطوط تقارير البيانات يكون جدول Pivot هو قلب التحليل، وفقدان تعريفه عند نقل البيانات كابوس.

الأخبار السارة؟ مع بضع أسطر من كود Aspose.Cells يمكنك نسخ الصفوف—بما في ذلك جدول Pivot—إلى دفتر عمل جديد والحفاظ على كل شيء كما هو. فيما يلي سترى **كيفية نسخ الصفوف**، **إعدادات الحفاظ على جدول Pivot**، وحتى **تكرار جدول Pivot** عبر الملفات دون كسر الصيغ أو الذاكرة المؤقتة.

## ما يغطيه هذا البرنامج التعليمي

1. تحميل دفتر العمل المصدر الذي يحتوي بالفعل على جدول Pivot.  
2. **إنشاء دفتر عمل جديد** كائنات للوجهة.  
3. استخدام `CopyRows` لنقل النطاق الذي يحتوي على جدول Pivot.  
4. حفظ النتيجة مع التأكد من بقاء جدول Pivot فعالًا.  

لا حاجة إلى وثائق خارجية—فقط الكود، والسبب، وبعض النصائح العملية التي يمكنك لصقها مباشرةً في مشروعك.

> **نصيحة احترافية:** Aspose.Cells يعمل مع .NET Core، .NET Framework، وحتى Xamarin، لذا فإن المقتطف نفسه يعمل أينما احتجت إليه.

![إنشاء دفتر عمل جديد مع جدول Pivot المنسوخ](/images/create-new-workbook-pivot.png "إنشاء دفتر عمل جديد مع جدول Pivot المنسوخ")

## الخطوة 1 – إنشاء دفتر عمل جديد وتحميل ملف المصدر

أول شيء نقوم به هو كائنات **إنشاء دفتر عمل جديد**. أحدها يحتفظ بالبيانات الأصلية، والآخر سيستقبل النطاق المنسوخ.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*لماذا هذا مهم:*  
`Workbook` هو نقطة الدخول لأي تعديل على Excel في Aspose.Cells. من خلال إنشاء دفتر عمل جديد نضمن صفحة نظيفة—بدون أنماط مخفية أو أوراق عمل شاردة قد تتداخل لاحقًا.

## الخطوة 2 – كيفية نسخ الصفوف بما في ذلك جدول Pivot

الآن يأتي جوهر المشكلة: **كيفية نسخ الصفوف** التي تحتوي على جدول Pivot دون تسطيحه. طريقة `CopyRows` تفعل ذلك بالضبط.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

بعض الأمور التي يجب ملاحظتها:

* `startRow` و `totalRows` يحددان الكتلة التي تحتوي على جدول Pivot.  
* الطريقة تنسخ **كلا** من البيانات الخام وذاكرة التخزين المؤقتة للـ Pivot، لذا يعرف دفتر العمل الوجهة كيفية إعادة بناء جدول Pivot مباشرةً.  
* إذا كان جدول Pivot يبدأ أعمق في الورقة، فقط غيّر الفهارس—لا حاجة لاستدعاء API مختلف.  

> **سؤال شائع:** *هل سيفقد الـ Pivot المنسوخ مرجع بيانات المصدر؟*  
> لا. Aspose.Cells يدمج الذاكرة المؤقتة مباشرةً في ورقة العمل، لذا يصبح الـ Pivot مستقلًا في الملف الجديد.

## الخطوة 3 – الحفاظ على جدول Pivot عند حفظ الوجهة

بعد نسخ الصفوف، يعيش جدول Pivot في دفتر العمل الوجهة تمامًا كما كان في المصدر. حفظ الملف سهل.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

عند فتح `destination.xlsx` في Excel، سترى جدول Pivot جاهزًا للتحديث. سلوك **preserve pivot table** يحدث تلقائيًا لأن الذاكرة المؤقتة سافرت مع الصفوف.

### التحقق من النتيجة

افتح الملف و:

1. انقر على جدول Pivot.  
2. لاحظ ظهور قائمة الحقول—هذا يعني أن الذاكرة المؤقتة سليمة.  
3. جرّب التحديث؛ البيانات تُحدَّث دون أخطاء.

إذا واجهت خطأ *#REF!*، تحقق مرة أخرى من أن النطاق المنسوخ يشمل الصفوف المخفية للذاكرة المؤقتة (عادةً بعد البيانات الظاهرة).

## الخطوة 4 – تكرار جدول Pivot إلى عدة دفاتر عمل (اختياري)

أحيانًا تحتاج إلى نفس جدول Pivot في عدة تقارير. النمط الذي استخدمناه يتوسع بسهولة—فقط كرّر النسخ لكل دفتر عمل جديد.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

هذا المقتطف **duplicates pivot table** ثلاث مرات باستخدام حلقة واحدة. عدّل مصفوفة `targets` لتتناسب مع جدول تقاريرك.

### الحالات الحدية التي يجب مراعاتها

| الحالة | ما يجب مراقبته | الحل |
|-----------|-------------------|-----|
| استخدام جدول Pivot لمصدر بيانات خارجي | قد تشير الذاكرة المؤقتة إلى اتصال غير موجود على الجهاز الجديد | دمج مصدر البيانات أو إعادة إنشاء الاتصال في دفتر العمل الوجهة |
| جدول Pivot كبير جدًا ( > 100 k صف) | `CopyRows` قد يستهلك الكثير من الذاكرة | استخدم `CopyRows` على دفعات أو فكر في `Copy` مع `PasteOptions` لتقليل استهلاك الذاكرة |
| ورقة العمل تحتوي على صفوف/أعمدة مخفية | قد يتم تخطي صفوف الذاكرة المخفية إذا قمت بنسخ الصفوف الظاهرة فقط | دائمًا انسخ النطاق الدقيق للصفوف الذي يحتوي على الذاكرة، وليس المنطقة الظاهرة فقط |

## مثال عملي كامل

نجمع كل ذلك معًا، إليك برنامج مستقل يمكنك وضعه في تطبيق كونسول.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

شغّل البرنامج، افتح `destination.xlsx`، وسترى نفس جدول Pivot جاهزًا لتقطيع وتحليل بياناتك. لا حاجة لإعادة إنشائه يدويًا.

---

## الخلاصة

لقد أظهرنا للتو كيفية **create new workbook** في C# و**copy pivot table** مع الحفاظ على جميع الإعدادات حية. باستخدام `CopyRows` تحصل على طريقة موثوقة لـ **preserve pivot table**، والإجابة على سؤال “**how to copy rows**” القديم، وحتى **duplicate pivot table** عبر تقارير متعددة بأقل قدر من الكود.

الخطوات التالية؟ جرّب تعديل النطاق المنسوخ ليشمل المخططات التي تشير إلى نفس جدول Pivot، أو جرب `PasteOptions` للحفاظ على التنسيق بدقة. النمط نفسه يعمل مع كائنات Aspose.Cells الأخرى مثل الجداول والنطاقات المسماة، لذا لا تتردد في توسيعه.

هل تواجه تحديًا—ربما جدول Pivot يجلب بيانات من قاعدة بيانات خارجية، أو دفتر عمل موجود في السحابة؟ اترك تعليقًا أدناه، وسنواجهه معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}