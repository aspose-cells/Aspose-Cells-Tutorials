---
category: general
date: 2026-02-09
description: إزالة واجهة الفلتر في Excel باستخدام C# بحذف زر AutoFilter. تعلّم كيفية
  إخفاء زر الفلتر، إظهار صف العنوان، والحفاظ على تنظيم أوراقك.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: ar
og_description: واجهة تصفية واضحة في Excel باستخدام C#. يوضح هذا الدليل كيفية إخفاء
  زر التصفية، إظهار صف العنوان، والحفاظ على نظافة أوراق العمل.
og_title: مسح واجهة الفلتر في Excel باستخدام C# – إزالة زر AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: مسح واجهة الفلتر في إكسل باستخدام C# – إزالة زر AutoFilter
url: /ar/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# واجهة تصفية واضحة في Excel باستخدام C# – إزالة زر AutoFilter

هل احتجت يومًا إلى **مسح واجهة التصفية** في ورقة Excel لكنك لم تكن متأكدًا أي سطر من الشيفرة يخفى ذلك السهم الصغير المنسدل؟ لست وحدك. يمكن أن يكون زر التصفية مزعجًا عندما تُرسل تقريرًا إلى المستخدمين النهائيين الذين لا يحتاجون أبدًا لتغيير العرض.  

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ ي **يزيل زر AutoFilter** من جدول، ويتأكد من بقاء صف العنوان مرئيًا، ويتطرق أيضًا إلى كيفية *إخفاء زر التصفية* نهائيًا. في النهاية ستعرف بالضبط **كيفية إزالة AutoFilter** في C# ولماذا كل خطوة مهمة.

## ما ستحتاجه

- .NET 6+ (أو .NET Framework 4.7.2+) – أي بيئة تشغيل حديثة تعمل.
- حزمة **EPPlus** من NuGet (الإصدار 6.x أو أحدث) – توفر لنا `ExcelWorksheet`، `ExcelTable`، إلخ.
- ملف Excel بسيط يحتوي على جدول اسمه **SalesTable** (يمكنك إنشاؤه ببضع نقرات).

هذا كل ما تحتاجه. لا COM interop، لا مكتبات DLL إضافية، فقط عدد قليل من عبارات `using` وبعض الأسطر من الشيفرة.

## مسح واجهة التصفية: إزالة زر AutoFilter

جوهر الحل يكمن في ثلاث عبارات صغيرة. دعنا نفصلها لتفهم *لماذا* هي ضرورية، وليس فقط *ماذا* تفعل.

### الخطوة 1 – الحصول على مرجع للجدول

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

لماذا هذا مهم: EPPlus يعمل مع **الجداول** (`ExcelTable`)، وليس مع النطاقات الخام. من خلال سحب كائن الجدول نحصل على خاصية `AutoFilter`، التي تتحكم في عنصر الواجهة الذي تراه في الورقة. إذا حاولت تعديل ورقة العمل مباشرة، ستؤثر فقط على القيم، وليس على زر التصفية.

### الخطوة 2 – إزالة صف زر AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

تعيين `AutoFilter` إلى `null` يخبر EPPlus بحذف صف التصفية الأساسي. هذه هي عملية **مسح واجهة التصفية** التي يبحث عنها معظم المطورين عندما يسألون “**كيفية إزالة autofilter**”. إنها طريقة نظيفة من سطر واحد تعمل على أي نسخة Excel يدعمها EPPlus.

### الخطوة 3 – الحفاظ على ظهور صف العنوان

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

عند إخفاء واجهة التصفية، قد يقوم Excel أحيانًا بإخفاء صف العنوان إذا كانت علامة `ShowHeader` للجدول غير مفعلة. من خلال تعيينها صراحةً إلى `true` نضمن بقاء عناوين الأعمدة على الشاشة – تفصيل بسيط لكنه مهم لتقرير نهائي مصقول.

### مثال كامل وقابل للتنفيذ

فيما يلي تطبيق console بسيط يفتح مصنفًا موجودًا، ينفذ الخطوات الثلاث، ويحفظ النتيجة. انسخه، اضغط **F5**، وشاهد زر التصفية يختفي.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**النتيجة المتوقعة:** افتح *SalesReport_NoFilter.xlsx* – ستختفي أسهم التصفية، لكن عناوين الأعمدة ستظل موجودة. لا مزيد من الفوضى في واجهة “انقر‑للتصفية”.

> **نصيحة محترف:** إذا كان لديك **جداول متعددة** وتريد إخفاء زر التصفية للجميع، قم بالتكرار عبر `worksheet.Tables` وطبق نفس الثلاث أسطر داخل الحلقة.

## كيفية إزالة AutoFilter في Excel باستخدام C# – نظرة أعمق

قد تتساءل، “ماذا لو كان المصنف يحتوي بالفعل على تصفية مفعلة؟ هل يؤدي تعيين `AutoFilter = null` إلى مسح الصفوف المصفاة أيضًا؟” الجواب **نعم**. EPPlus يمسح كلًا من الواجهة ومعايير التصفية الأساسية، ويعيد البيانات إلى ترتيبها الأصلي.  

إذا كنت تريد فقط *إخفاء* الزر مع إبقاء التصفية نشطة، يمكنك بدلاً من ذلك تعيين خاصية `AutoFilter` إلى **مرشح فارغ جديد**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

هذا الاختلاف مفيد عندما تريد *إخفاء زر التصفية* للحصول على مظهر مصقول لكن لا تزال تسمح للمستخدمين المتقدمين بتفعيل التصفية عبر VBA أو الشريط.

### حالة خاصة: جداول بدون صف عنوان

بعض التقارير القديمة تستخدم نطاقات عادية بدلاً من الجداول. في هذه الحالة، لن يعرض EPPlus كائن `ExcelTable`، لذا سيتسبب الكود أعلاه في استثناء. الحل هو **تحويل النطاق إلى جدول** أولًا:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

بهذا تكون قد *أزلت واجهة autofilter excel* حتى على نطاق لم يبدأ كجدول رسمي.

## إظهار صف العنوان بعد إخفاء زر التصفية – لماذا يهم

الشكوى الشائعة هي أن صف العنوان يختفي أحيانًا بعد إخفاء واجهة التصفية، خاصةً إذا تم إنشاء المصنف أصلاً مع تشغيل خيار “إخفاء العنوان”. من خلال تعيين `salesTable.ShowHeader = true;` صراحةً نتجنب هذه المفاجأة.  

إذا احتجت يومًا إلى **إخفاء زر التصفية** مع إبقاء العنوان مخفيًا (ربما لتوليد تفريغ بيانات خام)، ما عليك سوى تعيين `salesTable.ShowHeader = false;` بعد مسح التصفية. الشيفرة متماثلة، مما يجعل من السهل التبديل بناءً على علم التكوين.

## إخفاء زر التصفية – نصائح عملية ومخاطر

- **توافق الإصدارات:** EPPlus 6+ يعمل مع ملفات `.xlsx` فقط. إذا كنت تتعامل مع صيغة `.xls` القديمة، ستحتاج إلى مكتبة مختلفة (مثل NPOI) لأن واجهة **مسح واجهة التصفية** غير متوفرة.
- **الأداء:** تحميل مصنف ضخم فقط لإخفاء زر واحد قد يكون بطيئًا. فكر في استخدام `ExcelPackage.Load(stream, true)` للفتح في وضع **قراءة‑فقط**، ثم تطبيق التغيير، ثم الحفظ.
- **الاختبار:** تحقق دائمًا من الملف الناتج يدويًا في المرة الأولى. يمكن لاختبارات UI الآلية التحقق من اختفاء أسهم التصفية فعليًا (`worksheet.Tables[0].AutoFilter == null`).
- **الترخيص:** EPPlus انتقل إلى ترخيص مزدوج في الإصدار 5. للمشاريع التجارية ستحتاج إلى ترخيص مدفوع أو الانتقال إلى مكتبة بديلة.

## الملف الكامل للنسخ‑واللصق

فيما يلي الملف الدقيق الذي يمكنك وضعه في مشروع console جديد. لا توجد تبعيات مخفية، كل شيء مستقل.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

شغّل `dotnet add package EPPlus --version 6.0.8` (أو أحدث) قبل البناء، وستحصل على ورقة نظيفة جاهزة للتوزيع.

## الخلاصة

لقد أظهرنا لك **كيفية إزالة AutoFilter** و**مسح واجهة التصفية** في مصنف Excel باستخدام C#. النواة المكوّنة من ثلاث أسطر (`AutoFilter = null;`، `ShowHeader = true;`) تقوم بالعمل الأساسي، بينما يضيف الكود المحيط القليل من الإعدادات لتكملة الحل.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}