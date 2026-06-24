---
category: general
date: 2026-06-24
description: إنشاء مصنف جديد في C# ونسخ جدول محوري مع الحفاظ على بياناته. تعلم كيفية
  نسخ الصفوف، وتصدير النطاق المحدد، والحفاظ على الجدول المحوري دون تعديل.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: ar
og_description: إنشاء مصنف جديد في C# ونسخ جدول محوري مع الحفاظ على بياناته. دليل
  خطوة بخطوة يغطي كيفية نسخ الصفوف وتصدير النطاق المحدد.
og_title: إنشاء دفتر عمل جديد في C# – نسخ جدول محوري
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: إنشاء مصنف جديد في C# – نسخ جدول محوري
url: /ar/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف جديد في C# – نسخ جدول محوري

هل احتجت يومًا إلى **إنشاء مصنف جديد** في C# فقط لنقل جزء من البيانات يتضمن جدولًا محوريًا؟ لست وحدك. في العديد من خطوط تقارير البيانات تقوم بأخذ عدد قليل من الصفوف، وربما بعض الأعمدة، وتتوقع أن يبقى الجدول المحوري كما هو تمامًا—بدون مراجع مكسورة، ولا حسابات مفقودة.  

الخبر السار؟ مع بضع أسطر من Aspose.Cells يمكنك **نسخ جدول محوري**، والحفاظ عليه سليمًا، وحتى **تصدير النطاق المحدد** دون كسر أي شيء. أدناه ستشاهد مثالًا كاملًا جاهزًا للتنفيذ يوضح **كيفية نسخ الصفوف**، والحفاظ على الجدول المحوري، وحفظ النتيجة كمصنف جديد تمامًا.

## ما يغطيه هذا الدرس

- إعداد مشروع C# مع Aspose.Cells (المكتبة التي تشغل الكود).  
- تحميل المصنف المصدر الذي يحتوي على الجدول المحوري الأصلي.  
- استخدام طريقتي `CopyRows` و `CopyColumns` في المكتبة لتكرار النطاق الدقيق الذي تحتاجه.  
- حفظ المنطقة المنسوخة في سيناريو **إنشاء مصنف جديد** مع بقاء الجدول المحوري فعالًا.  
- نصائح للحالات الخاصة مثل وجود جداول محورية متعددة، الصفوف المخفية، ومجموعات البيانات الكبيرة.  

بنهاية هذا الدليل ستكون قادرًا على **تصدير النطاق المحدد** من أي ملف Excel، والحفاظ على منطق الجدول المحوري، ووضع الملف الجديد في أي مكان تريد.

> **المتطلبات المسبقة**: Aspose.Cells for .NET (نسخة تجريبية مجانية أو نسخة مرخصة) مثبتة عبر NuGet. إذا لم تقم بإضافتها بعد، نفّذ الأمر `dotnet add package Aspose.Cells` في مجلد المشروع.

---

## إنشاء مصنف جديد ونسخ جدول محوري

فيما يلي جوهر الحل. سنستعرض كل سطر، نشرح لماذا هو مهم، ثم نعرض البرنامج الكامل.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### لماذا يعمل هذا

- **`CopyRows` / `CopyColumns`**: تقوم هذه الطرائق بتكرار بيانات الخلايا الأساسية *وأيضًا* الكائنات المرتبطة (مثل ذاكرة التخزين المؤقت للجدول المحوري). لهذا يبقى الجدول المحوري فعالًا بعد النقل.  
- **مصنف الوجهة المنفصل**: بإنشاء كائن `Workbook` جديد نحصل على **إنشاء مصنف جديد** دون أي تنسيقات متبقية أو أوراق مخفية قد تتداخل.  
- **الفهرسة من الصفر**: Aspose.Cells يستخدم فهارس تبدأ من الصفر، لذا `0` يشير إلى الخلية **A1**. عدّل `startRow`/`startColumn` إذا لم يكن جدولك المحوري في الزاوية العليا اليسرى.  
- **الحفاظ على جدول محوري**: ذاكرة التخزين المؤقت للجدول المحوري تعيش في نفس النطاق، لذا نسخ النطاق ينسخ الذاكرة تلقائيًا. لا حاجة لكود إضافي.

---

## كيفية نسخ الصفوف دون كسر الجدول المحوري

إذا كنت مهتمًا فقط بجزء نسخ الصفوف، يمكنك عزل ذلك:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**نصيحة احترافية**: عند نسخ صفوف تتقاطع مع جدول محوري، احرص دائمًا على نسخ *المنطقة الكاملة* للجدول المحوري (الصفوف + الأعمدة). النسخ الجزئي قد يترك الجدول المحوري بحقول مفقودة، مما يسبب أخطاء `#REF!`.

---

## تصدير النطاق المحدد – سيناريو واقعي

تخيل أن لديك مصنف مبيعات ضخم، لكن عميلك يريد فقط ملخص الربع الأول، والذي يقع في الصفوف 1‑20 والأعمدة A‑D. المقتطف أعلاه بالفعل **تصدير النطاق المحدد** لك. فقط غيّر المتغيرين `totalRows` و `totalColumns` لتطابق طلب العميل، وستكون العملية جاهزة.

### التعامل مع الصفوف المخفية أو الفلاتر

إذا كان ورق العمل المصدر يحتوي على صفوف مخفية (ربما تم تصفيتها)، قد ترغب في نسخ الصفوف *المرئية* فقط. Aspose.Cells يقدم إصدارات م overload من `CopyRows` تحترم الرؤية:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

ضع القيمة الأخيرة `true` لنسخ الصفوف المرئية فقط—مثالي لـ “تصدير النطاق المحدد” عندما يكون المستخدم قد طبّق فلاتر.

---

## الحفاظ على جدول محوري – الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| **لم يتم نسخ ذاكرة التخزين المؤقت للجدول المحوري** | استخدام `Range.Copy` العادي بدلاً من `Cells.CopyRows/CopyColumns`. | الالتزام بطرق `Cells` كما هو موضح. |
| **ورقة الوجهة تحتوي على جدول محوري موجود مسبقًا** | حفظ فوق مصنف يحتوي بالفعل على جدول محوري بنفس الاسم. | ابدأ بـ `Workbook()` جديد (كما فعلنا). |
| **انكسار النطاقات المسماة** | الجدول المحوري المصدر يشير إلى نطاق مسمى غير موجود في الملف الجديد. | انسخ النطاق المسمى أيضًا: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **تغيّر مسار مصدر البيانات** | الجدول المحوري يشير إلى مصدر بيانات خارجي غير متوفر. | استخدم `PivotTable.RefreshData()` بعد النسخ إذا لزم الأمر. |

---

## مثال كامل من البداية إلى النهاية (جاهز للتنفيذ)

فيما يلي البرنامج الكامل، بما في ذلك توجيهات `using` وواجهة سطر أوامر بسيطة. انسخه‑الصقه في مشروع تطبيق Console جديد واضغط **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**الناتج المتوقع** (في سطر الأوامر):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

افتح `copy-pivot.xlsx` وسترى نفس جدول المحوري الموجود في `source.xlsx`، يعمل بالكامل ويشير إلى نطاق البيانات المنسوخ.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع جداول محورية متعددة في نفس الورقة؟**  
ج: نعم، طالما أن المستطيل المنسوخ يضم كل جدول محوري تحتاجه. إذا أردت جدولًا واحدًا فقط، عدّل `rows`/`cols` لعزل ذلك.

**س: ماذا لو كان المصنف المصدر يستخدم اتصالات بيانات خارجية؟**  
ج: ستظل ذاكرة التخزين المؤقت للجدول المحوري تشير إلى الاتصال الأصلي. استدعِ `pivotTable.RefreshData()` بعد تحميل الوجهة إذا رغبت في إعادة استعلام المصدر.

**س: هل يمكنني نسخ الجدول المحوري إلى ورقة مختلفة داخل نفس المصنف؟**  
ج: بالتأكيد. استبدل `destinationWorkbook` بـ `sourceWorkbook` واختر فهرس ورقة عمل آخر.

**س: هل هناك طريقة لنسخ التنسيق فقط؟**  
ج: استخدم إصدارات `CopyRows`/`CopyColumns` التي تقبل كائن `CopyOptions`—حدد `CopyOptions.CopyType = CopyType.ValuesOnly` أو `CopyType.All` حسب احتياجاتك.

---

## الخلاصة

لقد استعرضنا سيناريو **إنشاء مصنف جديد** يضم **نسخ جدول محوري**، **الحفاظ على جدول محوري**، و**تصدير النطاق المحدد**—كل ذلك باستخدام C# النقي.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء جدول محوري جديد برمجيًا في .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [كيفية تغيير مصدر بيانات الجدول المحوري باستخدام Aspose.Cells for .NET | دليل تحليل البيانات](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [كيفية إدارة توافق جداول محورية Excel مع Aspose.Cells for .NET | دليل تحليل البيانات](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}