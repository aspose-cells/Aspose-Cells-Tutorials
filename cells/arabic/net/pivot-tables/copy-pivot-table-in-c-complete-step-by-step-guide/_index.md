---
category: general
date: 2026-03-25
description: نسخ جدول محوري باستخدام C# و Aspose.Cells. تعلم كيفية نسخ الجدول المحوري،
  وتصدير ملف جدول محوري، والحفاظ على البيانات في دقائق.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: ar
og_description: نسخ جدول محوري في C# باستخدام Aspose.Cells. يوضح هذا الدليل كيفية
  نسخ الجدول المحوري، وتصدير ملف جدول محوري، والحفاظ على جميع الإعدادات دون تغيير.
og_title: نسخ جدول محوري في C# – دليل برمجة كامل
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: نسخ جدول محوري في C# – دليل كامل خطوة بخطوة
url: /ar/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري في C# – دليل خطوة بخطوة كامل

هل احتجت يومًا إلى **copy pivot table** من دفتر عمل إلى آخر وتساءلت ما إذا كانت منطقية الجدول المحوري ستبقى بعد النقل؟ لست وحدك. في العديد من خطوط تقاريرنا نولد دفتر عمل رئيسي، ثم نرسل نسخة خفيفة الوزن لا تزال تسمح للمستخدمين النهائيين بتقطيع البيانات. الخبر السار؟ ببضع أسطر من C# و Aspose.Cells يمكنك فعل ذلك بالضبط—دون الحاجة إلى أي تعديل يدوي.

في هذا الدرس سنستعرض العملية بالكامل: تحميل الملف المصدر، اختيار النطاق الذي يحتوي على الجدول المحوري، لصقه في دفتر عمل جديد مع الحفاظ على تعريف الجدول المحوري، وأخيرًا **export pivot table file** للاستخدام لاحقًا. بنهاية الدرس ستعرف *how to copy pivot* برمجيًا وستحصل على مثال جاهز للتنفيذ يمكنك إدراجه في مشروعك.

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.6+) مثبت  
- حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- ملف Excel مصدر (`source.xlsx`) يحتوي بالفعل على جدول محوري (أي حجم)  
- معرفة أساسية بـ C#؛ لا تحتاج إلى معرفة عميقة بداخل Excel  

إذا كان أي من هذه غير متوفر لديك، فقط أضف حزمة NuGet وافتح Visual Studio—لا شيء أكثر من ذلك.

## ما يفعله الكود (نظرة عامة)

1. **Load** دفتر العمل الذي يحتوي على الجدول المحوري الأصلي.  
2. **Define** `Range` يغطي كامل الجدول المحوري (بما في ذلك ذاكرة التخزين المؤقت).  
3. **Create** دفتر عمل جديد سيكون هو الوجهة.  
4. **Paste** النطاق مع `CopyPivotTable = true` بحيث يتم نسخ تعريف الجدول المحوري، وليس القيم فقط.  
5. **Save** ملف الوجهة، لتحصل على **export pivot table file** يمكنك مشاركته.

هذه هي سير العمل بالكامل في خمس خطوات مرتبة. لنغوص في كل خطوة.

## Step 1 – Load the Source Workbook that Contains the Pivot Table

أولًا نحتاج إلى جلب الملف المصدر إلى الذاكرة. Aspose.Cells يجعل ذلك سطرًا واحدًا.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Why this matters:* تحميل دفتر العمل يمنحنا الوصول إلى ذاكرة التخزين المؤقت للجدول المحوري. إذا نسخت قيم الخلايا فقط، سيفقد الجدول المحوري قدرته على التقطيع. بالحفاظ على كائن دفتر العمل حيًا، نحافظ على جميع بيانات تعريف الجدول المحوري.

## Step 2 – Define the Range That Includes the Pivot Table

الجدول المحوري ليس مجرد مجموعة خلايا؛ لديه أيضًا بيانات مخفية في الذاكرة المؤقتة. الطريقة الأكثر أمانًا هي اختيار مستطيل يحيط بالكامل بالمنطقة الظاهرة. في معظم الحالات `A1:E20` تعمل، لكن يمكنك اكتشاف الحدود الدقيقة برمجيًا باستخدام خصائص `PivotTable`.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Why we choose a range:* طريقة `Paste` تعمل على كائن `Range`. بتحديد المنطقة الدقيقة، نضمن أن تخطيط الجدول المحوري وذاكرته ينتقلان معًا.

## Step 3 – Create a New Destination Workbook

الآن ننشئ دفتر عمل فارغ سيستقبل النسخة المنقولة من الجدول المحوري. لا شيء معقد، مجرد صفحة نظيفة.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Tip:* إذا كنت بحاجة إلى الحفاظ على أوراق عمل موجودة (مثل قالب)، يمكنك إضافة دفتر العمل الجديد كنسخة من ملف قالب بدلاً من استخدام المُنشئ الفارغ.

## Step 4 – Paste the Range While Preserving the Pivot Table

هنا تكمن جوهر العملية. ضبط `CopyPivotTable = true` يخبر Aspose.Cells بنقل تعريف الجدول المحوري، وليس القيم المعروضة فقط.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*What happens under the hood?* Aspose.Cells يعيد إنشاء ذاكرة التخزين المؤقت للجدول المحوري في دفتر العمل الوجهة، ويعيد ربط مصدر بيانات الجدول، ويحافظ على المقاطع، والفلاتر، والحقول المحسوبة. النتيجة هي جدول محوري تفاعلي بالكامل—تمامًا كما تتوقع إذا قمت بنسخ الورقة يدويًا في Excel.

## Step 5 – Save the Resulting Workbook (Export Pivot Table File)

أخيرًا نكتب دفتر العمل الوجهة إلى القرص. الملف الذي ستحصل عليه هو **export pivot table file** جاهز للتوزيع.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

افتح `copy-pivot.xlsx` في Excel، وسترى الجدول المحوري كاملًا، جاهزًا للتحديث أو التقطيع.

## Full Working Example (All Steps Combined)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console. يتضمن معالجة الأخطاء وتعليقات لتوضيح الفكرة.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Expected outcome:** عند فتح `copy-pivot.xlsx`، سيظهر الجدول المحوري تمامًا كما هو في `source.xlsx`. يمكنك تحديثه، تغيير الفلاتر، أو حتى إضافة مصادر بيانات جديدة دون فقدان الوظائف.

## Common Questions & Edge Cases

### What if the source workbook has multiple pivots?

قم بالتكرار عبر `sourceSheet.PivotTables` وكرر عملية النسخ‑اللصق لكل منها. فقط تأكد أن نطاق كل وجهة لا يتداخل مع الآخر.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Does this work with external data sources (e.g., SQL)?

إذا كان الجدول المحوري الأصلي يجلب البيانات من اتصال خارجي، يتم نسخ سلسلة الاتصال أيضًا. ومع ذلك، يجب أن يكون لدى دفتر العمل الوجهة القدرة على الوصول إلى نفس مصدر البيانات. قد تحتاج إلى تعديل بيانات الاعتماد أو استخدام `WorkbookSettings` للسماح بالاتصالات الخارجية.

### Can I copy only the pivot layout (no data)?

اضبط `PasteOptions.PasteType = PasteType.Formulas` واحتفظ بـ `CopyPivotTable = true`. هذا ينسخ الهيكل فقط بينما يترك ذاكرة التخزين المؤقت للبيانات فارغة، مما يجبر على تحديث الجدول عند الفتح الأول.

### What about protecting the sheet?

إذا كانت الورقة المصدر محمية، قم بإلغاء الحماية قبل النسخ، أو مرّر كلمة المرور المناسبة إلى `Worksheet.Unprotect`. بعد اللصق، يمكنك إعادة تطبيق الحماية على الورقة الوجهة.

## Pro Tips & Pitfalls

- **Pro tip:** استخدم دائمًا أحدث إصدار من Aspose.Cells؛ الإصدارات القديمة كان فيها خلل يجعل `CopyPivotTable` يتجاهل المقاطع.  
- **Watch out for:** ذاكرات التخزين المؤقت الكبيرة للجداول المحورية قد تزداد حجم ملف الوجهة. إذا كان الحجم مهمًا، فكر في مسح الحقول غير المستخدمة قبل النسخ.  
- **Performance tip:** عند نسخ العديد من أوراق العمل، عطل مؤقتًا `WorkbookSettings.EnableThreadedCalculation` لتسريع العملية.  
- **Naming clash:** إذا كان دفتر العمل الوجهة يحتوي بالفعل على جدول محوري بنفس الاسم، سيعيد Aspose تسمية الجدول القادم (`PivotTable1_1`). أعد التسمية يدويًا إذا كنت تحتاج إلى معرف محدد.

## Visual Summary

![نسخ جدول محوري في C# – مخطط يوضح دفتر العمل المصدر → اختيار النطاق → اللصق مع الحفاظ على الجدول المحوري → ملف الوجهة](copy-pivot-diagram.png "توضيح سير عمل نسخ الجدول المحوري")

*Alt text:* **Copy pivot table** مخطط يوضح سير العمل بين المصدر، النطاق، خيارات اللصق، والملف المُصدَّر.

## Conclusion

لقد غطينا كل ما تحتاجه لتتمكن من **copy pivot table** باستخدام C# و Aspose.Cells: تحميل المصدر، اختيار النطاق الصحيح، الحفاظ على تعريف الجدول المحوري أثناء اللصق، وأخيرًا تصدير النتيجة كملف مستقل. المقتطف أعلاه جاهز للإنتاج؛ فقط ضع مساراتك وستكون جاهزًا للانطلاق.

الآن بعد أن عرفت *how to copy pivot* برمجيًا، يمكنك أتمتة توزيع التقارير، بناء مولدات قوالب، أو دمج تحليلات Excel في خدمات .NET الأكبر. قد ترغب في استكشاف **export pivot table file** إلى صيغ أخرى (PDF, CSV) أو تضمين دفتر العمل في واجهة ويب API للتحليلات الفورية.

هل لديك تعديل ترغب في مشاركته—ربما نسخ الجداول المحورية عبر إصدارات Excel مختلفة أو التعامل مع نماذج PowerPivot؟ اترك تعليقًا، ولنستمر في النقاش. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}