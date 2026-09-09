---
category: general
date: 2026-03-01
description: إنشاء مصنف جديد ونسخ ورقة العمل إلى مصنف يحتوي على جدول محوري. تعلم كيفية
  تصدير الجدول المحوري، نسخ الورقة، ونسخ الجدول المحوري في C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: ar
og_description: إنشاء مصنف جديد في C# ونسخ ورقة العمل إلى المصنف مع الحفاظ على جدول
  المحور. دليل خطوة بخطوة مع الكود الكامل.
og_title: إنشاء دفتر عمل جديد – نسخ ورقة العمل وجداول المحور في C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: إنشاء مصنف جديد – كيفية نسخ ورقة عمل تحتوي على جدول محوري
url: /ar/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل جديد – نسخ ورقة العمل وجدول محوري في C#

هل احتجت يومًا إلى **create new workbook** يحتوي على جدول محوري جاهز دون الحاجة لإعادة بنائه من الصفر؟ لست وحدك. في العديد من سيناريوهات التقارير لديك ملف رئيسي (`src.xlsx`) يحتوي على جدول محوري معقد، وتريد إرسال نسخة نظيفة (`dest.xlsx`) إلى عميل أو نظام آخر. الخبر السار؟ يمكنك القيام بذلك في سطرين فقط من C#—وهذا الدليل سيظهر لك بالضبط كيف.

سنستعرض العملية بالكامل: تحميل دفتر العمل المصدر، نسخ أول ورقة عمل (التي تحتوي على الجدول المحوري)، وحفظها كدفتر عمل جديد تمامًا. في النهاية ستعرف **how to copy sheet** التي تحتوي على جدول محوري، وكيفية **export pivot table** إذا احتجت ذلك، وحتى بعض الحيل للحالات الخاصة مثل النسخ إلى ملف موجود.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (أي نسخة حديثة تعمل)
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو مرخصة) – هذه المكتبة توفر الفئة `Workbook` المستخدمة أدناه.
- ملف Excel المصدر (`src.xlsx`) الذي يحتوي بالفعل على جدول محوري في ورقة العمل الأولى.

إذا لم يكن لديك Aspose.Cells بعد، أضفه عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

هذا كل شيء—بدون أي COM interop إضافي، ولا حاجة لتثبيت Excel على الخادم.

## ما يغطيه هذا الدرس

- **Create new workbook** من ورقة عمل موجودة تحتوي على جدول محوري.
- **Copy worksheet to workbook** مع الحفاظ على جميع تعريفات الجدول المحوري.
- **Export pivot table** البيانات إلى DataTable (اختياري).
- المشكلات الشائعة عند استخدام **how to copy pivot** في بيئات مختلفة.
- مثال كامل قابل للتنفيذ يمكنك وضعه في تطبيق Console.

---

## الخطوة 1: تحميل دفتر العمل المصدر (How to Copy Sheet)

الخطوة الأولى هي فتح دفتر العمل الذي يحتوي على الجدول المحوري. استخدام Aspose.Cells يجعل ذلك سهلًا لأنه يقرأ الملف إلى الذاكرة دون تشغيل Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **لماذا هذا مهم:** تحميل الملف يتحقق من وجود الجدول المحوري ويمنحك الوصول إلى مجموعة أوراق العمل. إذا كان الملف تالفًا، فإن `Workbook` يرمي استثناء واضح، مما يحفظك من مخرجات غامضة لاحقًا.

## الخطوة 2: نسخ ورقة العمل إلى دفتر عمل جديد (Copy Worksheet to Workbook)

الآن نقوم فعليًا بـ **copy worksheet to workbook**. طريقة `CopyTo` في Aspose.Cells تستنسخ الورقة بالكامل—بما في ذلك الصيغ، التنسيق، وذاكرة التخزين المؤقت للجدول المحوري—إلى ملف جديد.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **نصيحة احترافية:** `CopyTo` ينشئ دفتر عمل جديد خلف الكواليس، لذا لا تحتاج إلى إنشاء كائن `Workbook` آخر. هذا يحافظ على استهلاك الذاكرة منخفضًا ويضمن بقاء تعريف الجدول المحوري سليمًا.

## الخطوة 3: التحقق من النسخة المنسوخة من الجدول المحوري (How to Copy Pivot)

بعد انتهاء النسخ، من الجيد فتح الملف الجديد والتأكد من أن الجدول المحوري لا يزال يعمل. يمكنك القيام بذلك برمجياً أو مجرد فتحه في Excel.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

تشغيل البرنامج يطبع شيئًا مشابهًا لـ:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

إذا رأيت تلك القيم، فإن خطوة **how to copy pivot** نجحت.

## الخطوة 4: (اختياري) تصدير بيانات جدول محوري إلى DataTable

أحيانًا تحتاج إلى الأرقام الخام من الجدول المحوري دون فتح Excel. Aspose.Cells يتيح لك سحب بيانات الجدول المحوري إلى `DataTable`—مثالي للمعالجة الإضافية أو استجابات API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **لماذا قد تحتاج هذا:** التصدير يتيح لك **export pivot table** إلى قاعدة بيانات، حمولة JSON، أو أي تنسيق آخر دون الحاجة إلى النسخ واللصق يدويًا.

## الخطوة 5: الحالات الخاصة والمشكلات الشائعة

### النسخ إلى دفتر عمل موجود

إذا كنت بحاجة إلى **copy worksheet to workbook** يحتوي بالفعل على أوراق أخرى، استخدم النسخة التي تستقبل كائن `Workbook` هدف:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### الحفاظ على مصادر البيانات الخارجية

الجداول المحورية التي تجلب البيانات من اتصالات خارجية (مثل Power Query) قد تفقد الرابط بعد النسخ. في هذه الحالات، عيّن `pivot.RefreshDataOnOpen = true` قبل الحفظ:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### الملفات الكبيرة والأداء

للملفات التي يزيد حجمها عن 50 ميغابايت، فكر في تفعيل `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` لتقليل الضغط على الذاكرة.

---

![إنشاء دفتر عمل جديد – نسخ ورقة عمل مع جدول محوري](https://example.com/images/create-new-workbook.png "إنشاء دفتر عمل جديد")

*نص بديل للصورة: إنشاء دفتر عمل جديد – نسخ ورقة عمل مع جدول محوري*

---

## مثال عملي كامل (جميع الخطوات مجمعة)

فيما يلي التطبيق الكامل القابل للتنفيذ. انسخه إلى مشروع `.csproj` جديد واضغط **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### النتيجة المتوقعة

- `dest.xlsx` يظهر في `YOUR_DIRECTORY`.
- الورقة الأولى تبدو تمامًا مثل الأصل، مع جدول محوري كامل.
- تشغيل الـ console يطبع بيانات تعريف الجدول المحوري ومعاينة صغيرة للبيانات، مما يؤكد نجاح النسخ.

---

## الخلاصة

أنت الآن تعرف كيف **create new workbook** بنسخ ورقة عمل تحتوي على جدول محوري، وكيف **copy worksheet to workbook**، وحتى كيفية **export pivot table** للمعالجة اللاحقة. سواء كنت تبني خدمة تقارير، أو تُ automatisé توزيع Excel، أو تحتاج فقط إلى طريقة سريعة لتكرار جدول محوري، فإن الخطوات أعلاه توفر لك حلًا موثوقًا وجاهزًا للإنتاج.

**الخطوات التالية** التي قد تستكشفها:

- دمج عدة أوراق (استخدم `CopyTo` بشكل متكرر) – مثالي لتجميع تقرير كامل.
- ضبط إعدادات تحديث ذاكرة التخزين المؤقت للجدول المحوري عندما تتغير بيانات المصدر.
- استخدام تقنيات **how to copy sheet** لتكرار المخططات، الصور، أو وحدات VBA.
- الاطلاع على `WorkbookDesigner` في Aspose.Cells لإنشاء تقارير مبنية على القوالب.

جرّبها، عدّل المسارات، وسترى مدى سهولة شحن دفاتر عمل نظيفة وجاهزة للجدول المحوري. هل لديك أسئلة حول الحالات الخاصة أو الترخيص؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}