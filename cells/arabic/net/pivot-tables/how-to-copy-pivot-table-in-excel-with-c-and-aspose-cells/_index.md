---
category: general
date: 2026-10-04
description: تعلم كيفية نسخ جدول محوري من مصنف إلى آخر باستخدام C#. يغطي هذا الدليل
  أيضًا كيفية نسخ الصفوف، وتكرار الجدول المحوري، ونسخ نطاق Excel بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: ar
lastmod: 2026-10-04
og_description: نسخ جدول محوري في Excel باستخدام C#. اتبع هذا الدليل الكامل لتكرار
  الجداول المحورية، نسخ الصفوف، ونسخ نطاق Excel باستخدام Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: نسخ جدول محوري في إكسل باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية نسخ جدول محوري في Excel باستخدام C# و Aspose.Cells
url: /ar/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في Excel باستخدام C# و Aspose.Cells

إذا كنت بحاجة إلى **نسخ جدول محوري** من مصنف إلى آخر، يوضح لك هذا الدرس حلاً كاملاً قابلاً للتنفيذ. ستشاهد بالضبط كيفية تحميل ملف المصدر، تعريف النطاق الذي يحتوي على الجدول المحوري، نسخ الصفوف (بما في ذلك تعريف الجدول المحوري)، وحفظ النتيجة. سواءً كنت تقوم بأتمتة خط أنابيب تقارير أو بناء أداة ترحيل، فإن الخطوات أدناه تتيح لك تكرار جدول محوري ببضع أسطر من C# فقط.

نسخ جدول محوري هو أكثر من مجرد نسخ قيم الخلايا؛ يجب أن تنتقل الذاكرة المؤقتة الأساسية وإعدادات الحقول معًا. يستخدم المثال مكتبة **Aspose.Cells** لأنها تتعامل مع بيانات تعريف الجدول المحوري تلقائيًا، لذا لا تحتاج إلى إعادة بناء الذاكرة المؤقتة يدويًا. بنهاية هذا الدليل ستتمكن من **كيفية نسخ جدول محوري**، **نسخ نطاق Excel**، و**كيفية نسخ الصفوف** بأمان.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث مثبت (الكود يعمل أيضًا مع .NET Framework 4.7+).
- ترخيص صالح لـ Aspose.Cells for .NET أو ترخيص تجريبي مؤقت.
- ملفي Excel: `Source.xlsx` يحتوي على الجدول المحوري الذي تريد نسخه، ومجلد فارغ حيث سيتم كتابة `CopyWithPivot.xlsx`.
- Visual Studio 2022 (أو أي بيئة تطوير تدعم C#).

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

أنشئ مشروع console جديد وأضف حزمة NuGet الخاصة بـ Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

توفر الحزمة الفئات `Workbook` و `Worksheet` و `CellArea` المستخدمة في الشيفرة أدناه.

## الخطوة 2: تحميل مصنف المصدر الذي يحتوي على الجدول المحوري

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **لماذا هذا مهم:** تحميل المصنف يُنشئ تمثيلًا في الذاكرة لجميع الأوراق، بما في ذلك أي ذاكرة مؤقتة مخفية للجدول المحوري. بدون تحميل الملف، لا يمكنك الإشارة إلى نطاق الجدول المحوري.

## الخطوة 3: تعريف مساحة الخلايا التي تغطي الجدول المحوري

يجب إخبار Aspose.Cells أي صفوف وأعمدة تنتمي إلى الجدول المحوري. تسمح لك بنية `CellArea` بتحديد كتلة مستطيلة.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **نصيحة:** إذا لم تكن متأكدًا من الحجم الدقيق، افتح ملف المصدر في Excel، حدد الجدول المحوري، ولاحظ النطاق المعروض في مربع الاسم (مثال: `A1:K31`). حوّل إحداثيات Excel إلى فهارس صفرية لاستخدامها في الشيفرة.

## الخطوة 4: إنشاء مصنف وجهة جديد والحصول على أول ورقة عمل له

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **لماذا هذه الخطوة مطلوبة:** يجب أن يكون مصنف الوجهة موجودًا قبل أن تتمكن من نسخ الصفوف. تقوم Aspose.Cells بإنشاء ورقة عمل افتراضية تلقائيًا، وسنستخدمها كهدف.

## الخطوة 5: نسخ الصفوف (بما في ذلك الجدول المحوري) من المصدر إلى الوجهة

طريقة `CopyRows` تنسخ كلًا من قيم الخلايا والذاكرة المؤقتة للجدول المحوري.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **كيف يعمل ذلك:**  
> - تأخذ `CopyRows` ورقة العمل المصدر، رقم الصف الابتدائي، وعدد الصفوف المراد نسخها.  
> - كما تستقبل ورقة العمل الوجهة والصف الذي يجب أن يبدأ النسخ عنده.  
> - لأن النطاق المصدر يتضمن الجدول المحوري، تقوم الطريقة بنقل ذاكرة الجدول المحوري، قائمة الحقول، وتخطيطه دون تعديل. هذا هو جوهر **كيفية نسخ جدول محوري** دون فقدان الوظائف.

### حالة خاصة: نسخ جدول محوري يمتد عبر أوراق عمل متعددة

إذا كانت بيانات المصدر للجدول المحوري موجودة في ورقة مختلفة عن الورقة التي يحتويها الجدول نفسه، فإن الذاكرة المؤقتة لا تزال تُنسخ لأن Aspose.Cells تخزن الذاكرة في المصنف وليس في الورقة. ومع ذلك، يجب التأكد من أن مصنف الوجهة يحتوي على نفس نطاق بيانات المصدر؛ وإلا سيظهر للجدول محوري أخطاء `#REF!`. في مثل هذه الحالات، قم أولًا بنسخ نطاق بيانات المصدر، ثم صفوف الجدول المحوري.

## الخطوة 6: حفظ المصنف الذي يحتوي الآن على الجدول المحوري المنسوخ

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

تشغيل البرنامج ينتج ملف `CopyWithPivot.xlsx` يحتوي على نسخة مطابقة تمامًا للجدول المحوري الأصلي، بما في ذلك جميع المقاطع، الفلاتر، والحقول المحسوبة.

### النتيجة المتوقعة

عند فتح `CopyWithPivot.xlsx`:

- يظهر الجدول المحوري في نفس الموضع (مثال: A1:K31) كما هو في `Source.xlsx`.
- تُحافظ جميع تسميات الصفوف والأعمدة، الإجماليات، والتنسيقات.
- تحديث الجدول المحوري يُظهر نفس البيانات الموجودة في المصدر، مما يؤكد أن الذاكرة المؤقتة تم نسخها بشكل صحيح.

## كيفية نسخ الصفوف بدون جدول محوري (نسخ نطاق Excel)

إذا كنت تحتاج فقط إلى **نسخ نطاق Excel** دون أي بيانات جدول محوري، يمكنك استخدام نفس طريقة `CopyRows` ولكن الإشارة إلى نطاق لا يحتوي على جدول محوري. مثال:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

هذا يوضح **كيفية نسخ الصفوف** للبيانات العامة، مما يعزز مرونة نفس الـ API.

## تكرار جدول محوري في نفس المصنف (نهج بديل)

أحيانًا تريد **تكرار جدول محوري** داخل نفس المصنف بدلاً من إنشاء ملف جديد. يمكنك تحقيق ذلك بنسخ الصفوف إلى موقع مختلف:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

بعد الحفظ، سيحتوي المصنف على جدولين محوريين متطابقين—مفيد للمقارنة جنبًا إلى جنب أو لإنشاء نسخ احتياطية.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|---------|-------|------|
| يظهر الجدول المحوري `#REF!` بعد النسخ | نطاق بيانات المصدر غير موجود في مصنف الوجهة | نسخ نطاق بيانات المصدر أولًا، أو استخدم `CopyRows` على ورقة بيانات المصدر قبل نسخ الجدول المحوري |
| فقدان التنسيق | تم نسخ القيم فقط (مثال: باستخدام `Copy` بدلاً من `CopyRows`) | استخدم دائمًا `CopyRows` التي تحافظ على النمط، التنسيق، وبيانات تعريف الجدول المحوري |
| إزاحة الصفوف غير متوقعة | عدم تطابق صف البداية في الوجهة مع صف البداية في المصدر | تحقق من أن صف البداية في `destWorksheet.Cells` يطابق الموقع المقصود |
| ضغط الذاكرة في المصنفات الكبيرة | `CopyRows` يحمل كامل الأوراق في الذاكرة | نفّذ النسخ على دفعات أو استخدم واجهات البث إذا كان عدد الصفوف > 100,000 |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك لصقه في `Program.cs` وتشغيله فورًا (استبدل `YOUR_DIRECTORY` بمسار فعلي على جهازك).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. بعد التنفيذ، افتح `CopyWithPivot.xlsx` للتحقق من أن الجدول المحوري يظهر تمامًا كما هو في ملف المصدر.

## الخلاصة

أنت الآن تعرف **كيفية نسخ جدول محوري** من مصنف Excel إلى آخر باستخدام C# و Aspose.Cells. غطى الدليل سير العمل الكامل—من تحميل ملف المصدر، تعريف مساحة خلايا الجدول المحوري، نسخ الصفوف، وحفظ مصنف الوجهة. كما تعلمت **كيفية نسخ الصفوف**، **نسخ نطاق Excel**، و**تكرار جدول محوري** داخل نفس الملف، بالإضافة إلى الأخطاء الشائعة ونصائح أفضل الممارسات.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة كود لتحديث الجدول المحوري المنسوخ برمجيًا، أو استكشف تصدير الجدول المحوري إلى PDF باستخدام Aspose.Cells. جرب نطاقات مصدر مختلفة، وستتقن أتمتة Excel في .NET بسرعة.

---


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}