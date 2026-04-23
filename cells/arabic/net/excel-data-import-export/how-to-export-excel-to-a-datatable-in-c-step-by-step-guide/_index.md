---
category: general
date: 2026-03-18
description: كيفية تصدير بيانات Excel إلى DataTable في C# باستخدام كود يتعامل مع خلايا
  محددة، يحول Excel إلى DataTable، ويُنسق الأرقام. تعلّم تصدير الخلايا المحددة والمزيد.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: ar
og_description: كيفية تصدير بيانات Excel إلى DataTable في C#. يوضح هذا الدرس كيفية
  تصدير خلايا محددة، تحويل Excel إلى DataTable، وتنسيق الأرقام بسهولة.
og_title: كيفية تصدير Excel إلى DataTable في C# – دليل شامل
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: كيفية تصدير Excel إلى DataTable في C# – دليل خطوة بخطوة
url: /ar/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى DataTable في C# – دليل خطوة بخطوة

هل تساءلت يومًا **كيف تصدر بيانات Excel** إلى `DataTable` دون فقدان التنسيق؟ لست وحدك—المطورون يحتاجون باستمرار إلى استخراج جزء من جدول البيانات إلى الذاكرة للتقارير، والتحقق، أو عمليات الإدخال الجماعي. الخبر السار؟ ببضع أسطر من C# يمكنك تصدير نطاق محدد (مثلاً *A1:F11*), وإجبار كل خلية على أن تُعامل كسلسلة نصية، وحتى تطبيق تنسيق رقم مخصص.

في هذا البرنامج التعليمي سنغطي كل ما تحتاج إلى معرفته: من تحميل المصنف، تكوين **تصدير خلايا محددة**، تحويل النطاق إلى `DataTable`، ومعالجة الحالات الحدية مثل الصفوف الفارغة أو الأرقام المعتمدة على الإعدادات المحلية. بنهاية الدليل ستحصل على طريقة قابلة لإعادة الاستخدام تعمل مع سيناريوهات **excel to datatable c#** في الكود الإنتاجي.

> **المتطلبات المسبقة** – ستحتاج إلى مكتبة Aspose.Cells for .NET (أو أي API مشابه يقدم `ExportDataTable`). المثال يفترض .NET 6+، لكن المفاهيم تنطبق على الإصدارات الأقدم أيضًا.

---

## ما ستتعلمه

- كيفية **تحويل Excel إلى DataTable** باستخدام Aspose.Cells.
- تصدير نطاق مخصص (`excel range to datatable`) مع معالجة جميع القيم كسلاسل نصية.
- تطبيق تنسيق رقم ذو منزلتين عشريتين (`#,#00.00`) أثناء التصدير.
- المشكلات الشائعة (صفوف فارغة، أعمدة مخفية) وكيفية تجنبها.
- عينة كود جاهزة للنسخ، قابلة للتنفيذ بالكامل.

## المتطلبات الأولية والإعداد

قبل أن نغوص في الكود، تأكد من أنك تمتلك:

1. **Aspose.Cells for .NET** مثبتًا عبر NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. ملف Excel (`input.xlsx`) موجود في مجلد يمكنك الإشارة إليه، مثال: `YOUR_DIRECTORY/input.xlsx`.
3. مشروع يستهدف .NET 6 أو أحدث (عبارات `using` الموضحة أدناه تعمل مباشرة).

> **نصيحة محترف:** إذا كنت تستخدم مكتبة مختلفة (مثل EPPlus أو ClosedXML)، فإن الفكرة تبقى نفسها—حمّل المصنف، اختر نطاقًا، واستدعِ طريقة تُعيد `DataTable`.

## الخطوة 1: تحميل المصنف والحصول على الورقة الأولى

الشيء الأول الذي تحتاجه هو كائن `Workbook` يمثل ملف Excel الخاص بك. بمجرد حصولك عليه، يمكنك الوصول إلى أي ورقة عمل عبر الفهرس أو الاسم.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**لماذا هذا مهم:** تحميل المصنف مبكرًا يتيح لك فحص هيكله (الأوراق المخفية، الحماية) قبل أن تقرر أي خلايا تريد تصديرها. إذا كان الملف كبيرًا، فكر في استخدام `LoadOptions` لتدفق الأجزاء المطلوبة فقط.

## الخطوة 2: تكوين خيارات التصدير – معالجة جميع القيم كسلاسل نصية

عند تصدير البيانات للمعالجة اللاحقة (مثل الإدخال الجماعي إلى SQL)، غالبًا ما تريد **تمثيل نصي متسق**. هذا يتجنب أخطاء عدم توافق الأنواع لاحقًا.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**شرح:**  
- `ExportAsString = true` يخبر Aspose.Cells بتجاهل نوع الخلية الأصلي وإرجاع النص المُنسق.  
- `NumberFormat = "#,##0.00"` يضمن أن الأرقام مثل `1234.5` تصبح `"1,234.50"`—مفيد للتقارير المالية.

إذا كنت بحاجة إلى الأنواع الأصلية للبيانات، ما عليك سوى ضبط `ExportAsString` إلى `false` ومعالجة التحويل بنفسك.

## الخطوة 3: تصدير نطاق محدد (A1:F11) إلى DataTable

الآن يأتي جوهر **تصدير خلايا محددة**. طريقة `ExportDataTable` تأخذ مؤشرات الصف/العمود للبداية والنهاية (صفرية) بالإضافة إلى علم لتضمين العنوان.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**ما ستحصل عليه:** `DataTable` يحتوي على 11 صفًا (بما في ذلك العنوان) و6 أعمدة (`A`‑`F`). جميع القيم هي سلاسل نصية مُنسقة وفقًا لـ `exportOptions`.

## الخطوة 4: التحقق من النتيجة – طباعة إلى وحدة التحكم

من الجيد دائمًا فحص صحة المخرجات قبل تمرير الجدول إلى مكوّن آخر.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

يجب أن ترى شيئًا مثل:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

لاحظ كيف تُظهر الأعمدة الرقمية منزلتين عشريتين، تمامًا كما حددنا.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يربط كل شيء معًا. ضعّه في مشروع وحدة تحكم جديد، عدّل مسار الملف، وشغّله—لا حاجة لأي إعداد إضافي.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**النقاط الرئيسية المستفادة من الكود:**

- كائن `ExportTableOptions` قابل لإعادة الاستخدام؛ يمكنك تمريره إلى عدة استدعاءات `ExportDataTable` إذا احتجت لتصدير عدة نطاقات.  
- الفهرسة تبدأ من **0**، لذا `A1` يطابق `(0,0)`.  
- ضبط `includeColumnNames` إلى `true` يستخدم الصف الأول تلقائيًا كعناوين أعمدة—مفيد لعمليات `DataTable` اللاحقة.

## معالجة الحالات الحدية والأسئلة الشائعة

### ماذا لو كان للورقة صفوف أو أعمدة مخفية؟

Aspose.Cells يحترم الرؤية بشكل افتراضي. إذا كنت بحاجة لتصدير البيانات المخفية، اضبط `exportOptions.ExportHiddenRows = true` و `ExportHiddenColumns = true`.

### ملف Excel الخاص بي يحتوي على صيغ—هل سأتلقى القيم المحسوبة؟

نعم. بشكل افتراضي تُعيد `ExportDataTable` **القيمة المعروضة** (نتيجة الصيغة). إذا أردت نص الصيغة الأصلي، اضبط `exportOptions.ExportFormulas = true`.

### كيف يمكنني تخطي الصفوف الفارغة تمامًا؟

بعد التصدير، يمكنك تنقية `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### هل يمكنني تصدير نطاق غير متصل (مثلاً A1:B5 و D1:E5)؟

Aspose.Cells لا يدعم النطاقات المتقطعة في استدعاء واحد. بدلاً من ذلك، صدّر كل كتلة على حدة ثم ادمج `DataTable`s الناتجة يدويًا.

## نصائح الأداء

- **إعادة استخدام `ExportTableOptions`** لتصديرات متعددة؛ إنشاء نسخة جديدة في كل مرة يضيف حملاً ضئيلًا لكنه ي clutter الكود.  
- **تدفق الملفات الكبيرة** باستخدام `LoadOptions` لتجنب تحميل المصنف بالكامل في الذاكرة.  
- **تجنب `DataTable`** إذا كنت تحتاج فقط لتصدير CSV سريع—`ExportDataTable` مريح لكنه ليس الأكثر كفاءة للذاكرة مع الأوراق الضخمة.

## الخلاصة

لقد استعرضنا **كيفية تصدير بيانات Excel** إلى `DataTable` مع التحكم في التنسيق، معالجة نطاقات خلايا محددة، وضمان أن كل قيمة تصل كسلسلة نصية. المثال الكامل يُظهر نهجًا نظيفًا وجاهزًا للإنتاج يمكنك تكييفه لـ **convert excel to datatable**، **export specific cells**، أو أي سيناريو **excel range to datatable** تواجهه.

لا تتردد في التجربة: غير النطاق، بدّل `ExportAsString`، أو مرّر `DataTable` مباشرة إلى Entity Framework للإدخالات الجماعية. السماء هي الحد بمجرد أن تكون لديك هذه الأساس الصلب.

### الخطوات التالية والمواضيع ذات الصلة

- **استيراد DataTable مرة أخرى إلى Excel** – تعلم العملية العكسية باستخدام `ImportDataTable`.  
- **الإدخال الجماعي لـ DataTable إلى SQL Server** – استخدم `SqlBulkCopy` لتحميل فائق السرعة.  
- **العمل مع EPPlus أو ClosedXML** – شاهد كيف يبدو نفس المهمة مع مكتبات بديلة.  
- **تنسيق الخلايا عند التصدير** – استكشف `ExportTableOptions` أكثر لتنسيقات التاريخ، إعدادات الثقافة المخصصة، وأكثر.

هل لديك أسئلة أو حالة استخدام مختلفة؟ اترك تعليقًا، ولنستمر في النقاش. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}