---
category: general
date: 2026-03-18
description: نسخ جدول محوري في C# باستخدام Aspose.Cells. تعلم كيفية نسخ نطاق Excel،
  تكرار الجدول المحوري في Excel، نسخ النطاق إلى ورقة جديدة ونسخ الجدول المحوري إلى
  ورقة في دقائق.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: ar
og_description: نسخ جدول محوري في C# باستخدام Aspose.Cells. تعلم كيفية تكرار الجدول
  المحوري في Excel، نسخ نطاق Excel إلى موقع جديد، ونسخ الجدول المحوري إلى ورقة مع
  أمثلة كاملة للكود.
og_title: نسخ جدول محوري في C# – دليل برمجي شامل
tags:
- Aspose.Cells
- C#
- Excel automation
title: نسخ جدول محوري في C# – دليل خطوة بخطوة
url: /ar/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري في C# – دليل برمجة كامل

هل احتجت يومًا إلى **copy pivot table** من جزء من دفتر العمل إلى آخر، لكن لم تكن متأكدًا من كيفية القيام بذلك دون فقدان اتصالات البيانات الأساسية؟ لست وحدك. يواجه العديد من المطورين هذه المشكلة عند أتمتة تقارير Excel، خاصة عندما يكون المحور داخل كتلة بيانات أكبر. الخبر السار؟ باستخدام Aspose.Cells يمكنك نسخ جدول المحور **بالضبط كما هو**، وستتعلم أيضًا كيفية **copy excel range**، **duplicate excel pivot**، وحتى **copy pivot to sheet** ببضع أسطر من C#.

في هذا الدرس سنستعرض سيناريو واقعي: نقل جدول محوري يغطي *A1:J20* إلى منطقة جديدة *M1:V20* في نفس ورقة العمل. بنهاية الدرس ستحصل على برنامج قابل للتنفيذ، وتفهم لماذا كل خطوة مهمة، وتعرف كيف تعدل الكود لنطاقات أخرى أو حتى أوراق عمل منفصلة. لا حاجة لأي مستندات خارجية—كل شيء هنا.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **Aspose.Cells for .NET** (الإصدار 23.9 أو أحدث). يمكنك الحصول عليه عبر NuGet: `Install-Package Aspose.Cells`.
- بيئة تطوير C# أساسية (Visual Studio 2022، Rider، أو VS Code مع امتداد C#).
- ملف Excel (`source.xlsx`) يحتوي على جدول محوري داخل النطاق *A1:J20*.

هذا كل شيء. إذا كنت مرتاحًا لإنشاء تطبيق Console، فأنت جاهز للانطلاق.

---

## كيفية نسخ جدول محوري في Aspose.Cells

جوهر الحل هو استدعاء واحد لـ `Worksheet.Cells.CopyRange`. هذه الطريقة لا تنسخ قيم الخلايا فقط، بل تحافظ أيضًا على الجداول المحورية، المخططات، وغيرها من الكائنات الغنية تلقائيًا. لنفصل الخطوات.

### الخطوة 1: تحميل دفتر العمل المصدر

أولًا نحتاج لجلب دفتر العمل إلى الذاكرة.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **لماذا هذا مهم:** تحميل دفتر العمل يُنشئ تمثيلًا في الذاكرة يمكن لـ Aspose.Cells معالجته دون تشغيل Excel. العملية سريعة، آمنة للخطوط المتعددة، وتعمل على الخوادم.

### الخطوة 2: الحصول على ورقة العمل الأولى

معظم الأمثلة تستخدم الورقة الأولى، لكن يمكنك استهداف أي فهرس أو اسم.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **نصيحة:** إذا كنت بحاجة إلى **copy pivot to sheet** بدلاً من نفس الورقة، فقط غيّر مرجع `worksheet` إلى كائن `Worksheet` آخر.

### الخطوة 3: تعريف النطاقات المصدر والهدف

سنستخدم هياكل `CellArea` لوصف الكتل التي ننقلها.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **شرح:** مؤشرات الصفوف والأعمدة تبدأ من الصفر. العمود 0 = **A**، العمود 12 = **M**، وهكذا. عدّل هذه الأرقام إذا كان المحور موجودًا في مكان آخر.

### الخطوة 4: تنفيذ عملية النسخ

الآن يحدث السحر. ضبط المعامل الأخير من النوع Boolean على `true` يخبر Aspose.Cells بنسخ جميع الكائنات—including the pivot.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **لماذا `true`؟** العلامة تعني “نسخ جميع الكائنات”. إذا ضبطتها على `false`، ستُنقل قيم الخلايا فقط، وسيُفقد الجدول المحوري.

### الخطوة 5: حفظ دفتر العمل

أخيرًا، اكتب دفتر العمل المعدل إلى القرص.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **النتيجة:** الآن يحتوي `copy-pivot.xlsx` على الجدول المحوري الأصلي في *A1:J20* **و** نسخة مطابقة في *M1:V20*. افتح الملف في Excel للتحقق من أن كلا الجدولين يعملان ويحتفظان باتصالات البيانات الخاصة بهما.

---

## نسخ نطاق Excel إلى موقع جديد – تعديل سريع

أحيانًا تحتاج فقط إلى **copy excel range** دون القلق بشأن الجداول المحورية. نفس طريقة `CopyRange` تقوم بالمهمة؛ فقط اضبط المعامل الأخير على `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **متى تستخدم:** إذا كنت تنقل بيانات خام إلى ورقة حساب مؤقتة، فإن إلغاء نسخ الكائنات يوفر الذاكرة ويسرّع العملية.

---

## تكرار جدول محوري عبر عدة أوراق

ماذا لو أردت **duplicate excel pivot** في ورقة عمل مختلفة؟ النمط يبقى نفسه؛ فقط اشِر إلى `Worksheet` آخر كوجهة.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **حالة خاصة:** إذا كان الجدول المحوري المصدر يستخدم جدولًا موجودًا على الورقة الأصلية، سيقوم Aspose.Cells أيضًا بنسخ تعريف الجدول الأساسي، مما يضمن أن الجدول الجديد يعمل مباشرةً.

---

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا تحدث | الحل |
|---------|------------|------|
| **يفقد الجدول المحوري ذاكرته المؤقتة** | استخدام `CopyRange` مع `false` أو روتين نسخ مخصص يتجاهل الكائنات. | احرص دائمًا على تمرير `true` عندما تحتاج إلى الجدول نفسه. |
| **الخلايا الهدف تحتوي بالفعل على بيانات** | يتم الكتابة فوقها بصمت، مما قد يفسد الصيغ الموجودة. | امسح المنطقة الهدف أولًا: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **النطاق المصدر لا يشمل كامل الجدول المحوري** | الجداول المحورية قد تمتد إلى صفوف/أعمدة أكثر مما تتوقع (مثل الصفوف المخفية). | استخدم `worksheet.PivotTables[0].DataRange` للحصول على الحدود الدقيقة برمجيًا. |
| **النسخ بين دفاتر العمل** | `CopyRange` يعمل فقط داخل نفس دفتر العمل. | استخدم `sourceWorksheet.Cells.CopyRange` إلى نطاق مؤقت، ثم `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## النتيجة المتوقعة والتحقق

بعد تشغيل البرنامج:

1. افتح `copy-pivot.xlsx`.
2. سترى جدولين محوريين متطابقين—واحد في **A1:J20** وآخر في **M1:V20**.
3. قم بتحديث أي جدول محوري؛ يجب أن يعكس كلاهما نفس البيانات الأساسية.
4. إذا قمت بالتكرار إلى ورقة أخرى، ستجد النسخة الوظيفية هناك أيضًا.

طريقة سريعة للتحقق عبر الكود:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## نصيحة احترافية: اكتشاف النطاق تلقائيًا

تحديد `CellArea` يدويًا يناسب التقارير الثابتة، لكن في بيئات الإنتاج غالبًا ما تحتاج إلى تحديد موقع الجدول المحوري ديناميكيًا.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **لماذا ذلك؟** يجعل حلك مرنًا أمام تغيّر التخطيط—لا مزيد من الأخطاء “أوه، الجدول انتقل إلى B2”.

---

![copy pivot table example](copy-pivot.png){alt="مثال على نسخ جدول محوري"}

*تُظهر الصورة (نموذجية) الجدول المحوري الأصلي على اليسار والنسخة المكررة على اليمين.*

---

## ملخص

لقد غطينا كيفية **copy pivot table** في C# باستخدام Aspose.Cells، واستكشفنا طرقًا لـ **copy excel range**، **duplicate excel pivot**، وحتى **copy pivot to sheet** عبر أوراق العمل. النقاط الرئيسية هي:

- استخدم `Worksheet.Cells.CopyRange` مع العلامة `true` للحفاظ على الكائنات الغنية.
- عرّف كائنات `CellArea` المصدر والهدف باستخدام مؤشرات صفرية.
- غيّر ورقة العمل الوجهة إذا احتجت إلى **copy pivot to sheet**.
- انتبه لحالات الحافة مثل وجود بيانات مسبقة، الصفوف المخفية، والنسخ بين دفاتر العمل.

---

## ما التالي؟

- **اكتشاف الجداول المحورية ديناميكيًا**: أنشئ أداة تفحص دفتر العمل وتكرر جميع الجداول تلقائيًا.
- **التصدير إلى PDF/HTML**: بعد النسخ، قد ترغب في تحويل الورقة إلى تقرير—Aspose.Cells يدعم ذلك أيضًا.
- **تحسين الأداء**: للدفاتر الضخمة، فكر في إيقاف الحساب قبل النسخ وإعادة تفعيله بعد الانتهاء.

لا تتردد في التجربة: غيّر إحداثيات الهدف، انسخ إلى دفتر عمل جديد، أو كرّر العملية عبر عدة أوراق لإنشاء تقرير موحد. الإمكانيات لا حصر لها، ومع الأساس الذي اكتسبته الآن ستتمكن من تعديل الكود لأي مهمة أتمتة Excel.

برمجة سعيدة، ولتظل جداولك المحورية دائمًا متزامنة تمامًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}