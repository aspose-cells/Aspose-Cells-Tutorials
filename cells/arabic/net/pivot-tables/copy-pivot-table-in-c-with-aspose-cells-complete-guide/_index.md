---
category: general
date: 2026-08-11
description: نسخ جدول محوري باستخدام C# و Aspose.Cells. تعلّم كيفية تحميل مصنف Excel،
  تكرار جدول محوري، والحفاظ على تنسيقه بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: ar
lastmod: 2026-08-11
og_description: نسخ جدول محوري في C# باستخدام Aspose.Cells. يوضح لك هذا الدليل كيفية
  تحميل مصنف Excel، وتكرار جدول محوري، والحفاظ على جميع التنسيقات دون تغيير.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: نسخ جدول محوري في C# – دليل Aspose.Cells خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: نسخ جدول محوري في C# باستخدام Aspose.Cells – دليل كامل
url: /ar/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري في C# باستخدام Aspose.Cells – دليل كامل

إذا كنت بحاجة إلى **copy pivot table** من موقع إلى آخر في مصنف Excel باستخدام C#، فإن هذا الدرس يوضح لك كيفية ذلك. سترى حلاً مختصرًا وشاملًا يقوم بتحميل المصنف، نسخ الجدول المحوري، والحفاظ على كل تفاصيل التنسيق.

العمل مع Excel برمجيًا يعني غالبًا التعامل مع كائنات معقدة مثل الجداول المحورية. في هذا الدليل ستتعلم كيفية **duplicate pivot table excel** دون فقدان الفلاتر أو الحقول المحسوبة أو التنسيق. المتطلب الوحيد هو الإشارة إلى مكتبة Aspose.Cells، التي تمنحك التحكم الكامل في ملفات Excel من .NET.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
* رخصة صالحة لـ Aspose.Cells for .NET (يمكنك استخدام نسخة التقييم المجانية للاختبار)
* ملف Excel (`Source.xlsx`) يحتوي على جدول محوري تريد نسخه
* بيئة تطوير مثل Visual Studio 2022

## كيفية نسخ جدول محوري باستخدام Aspose.Cells

الخطوات الأساسية هي:

1. **Load Excel workbook C#** – افتح ملف المصدر.
2. **Select the range that contains the pivot table** – تضمّن كامل منطقة الجدول المحوري.
3. **Copy the range to a new location** – يبقى الجدول المحوري كما هو.
4. **Save the workbook** – الملف الجديد يحتوي على الجدول المحوري المكرر.

كل خطوة مشروحة أدناه مع الكود الكامل.

### الخطوة 1: Load Excel workbook C#

تحميل المصنف هو الإجراء الأول عندما تقوم بـ **load excel workbook c#**. تقوم Aspose.Cells بقراءة الملف إلى الذاكرة، مما يمنحك الوصول إلى أوراق العمل، الخلايا، والجداول المحورية.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **لماذا هذا مهم:** تحميل المصنف ينشئ كائن `Workbook` يمثل ملف Excel بالكامل. جميع العمليات اللاحقة تعمل على هذا التمثيل في الذاكرة، وهو أسرع من الوصول المتكرر إلى نظام الملفات.

### الخطوة 2: Identify and copy the pivot table range

الجدول المحوري يقع داخل نطاق خلايا مستطيل. لكي تقوم بـ **move pivot table cell** بأمان، يجب نسخ النطاق بالكامل، وليس الخلايا الفردية فقط.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **لماذا هذا يعمل:** `Range.Copy` ينسخ ليس فقط قيم الخلايا بل أيضًا ذاكرة التخزين المؤقت للجدول المحوري والتنسيق. هذه هي الطريقة الموصى بها لـ **duplicate pivot table excel** دون إعادة بناء الجدول يدويًا.

### الخطوة 3: Save the workbook with the copied pivot table

بعد النسخ، تقوم ببساطة بحفظ المصنف. سيحتوي الملف الجديد على كل من الجدول الأصلي والجدول المحوري المكرر.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **لماذا يجب الحفاظ على التنسيق:** تم تلبية متطلب `preserve pivot formatting` تلقائيًا لأن Aspose.Cells تحتفظ بمعلومات النمط أثناء عملية النسخ. لا حاجة إلى أي كود تنسيق إضافي.

### مثال كامل يعمل

جمع الخطوات الثلاث يعطيك برنامجًا كاملاً قابلاً للتنفيذ:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**النتيجة المتوقعة:**  
افتح `CopyPivot.xlsx` في Excel. سترى الجدول المحوري الأصلي بدون تغيير وجدولًا محوريًا ثانيًا متطابقًا يبدأ من الخلية `I1`. جميع الفلاتر والحقول المحسوبة والأنماط البصرية تتطابق مع المصدر.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية التعامل |
|-----------|------------------|
| **Pivot table spans a dynamic range** | استخدم `PivotTable.PivotTableRange` للحصول على العنوان الدقيق في وقت التشغيل بدلاً من كتابة `"A1:G20"` يدويًا. |
| **You need to move the pivot table to another worksheet** | استدعِ `sourceRange.Copy(otherWorksheet.Cells, "A1")` بعد إنشاء `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Preserving only formatting, not data** | بعد النسخ، قم بمسح قيم البيانات باستخدام `targetRange.Clear(ClearOptions.Contents)` مع ترك الأنماط دون تعديل. |
| **Large workbooks cause memory pressure** | استخدم `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` للسماح لـ Aspose.Cells ببث البيانات. |
| **You want to rename the duplicated pivot table** | احصل على الجدول المحوري الجديد عبر `sheet.PivotTables[sheet.PivotTables.Count - 1]` واضبط خاصية `Name`. |

هذه النصائح تساعدك على **move pivot table cell** المواقع، **duplicate pivot table excel** الملفات، والحفاظ على متطلب **preserve pivot formatting**.

## نصائح احترافية للنسخ الموثوق

* **نصيحة احترافية:** تحقق دائمًا من أن النطاق المصدر يشمل كامل ذاكرة التخزين المؤقت للجدول المحوري. فقدان عمود قد يتسبب في تعطل النسخة المنسوخة.
* **احذر من الخلايا المدمجة** داخل النطاق؛ قد تتسبب في حدوث استثناء عند `Copy`. قم بإلغاء الدمج قبل النسخ أو عدل النطاق.
* **نصيحة أداء:** إذا كنت تحتاج فقط إلى نسخ تعريف الجدول المحوري (بدون بيانات)، استخدم `PivotTable.Clone` بدلاً من نسخ النطاق بالكامل.

## الخلاصة

أنت الآن تعرف كيفية **copy pivot table** برمجيًا في C# باستخدام Aspose.Cells مع الحفاظ على **preserve pivot formatting**، **load excel workbook c#**، وحتى **move pivot table cell** عبر أوراق العمل. الحل الكامل يحمل المصنف، ينسخ نطاق الجدول المحوري، ويحفظ ملفًا جديدًا يحتوي على كلا الجدولين.

بعد ذلك، قد تستكشف سيناريوهات **duplicate pivot table excel** مثل النسخ بين مصنفات مختلفة، أو أتمتة إنشاء التقارير باستخدام جداول محورية متعددة. للحصول على تخصيص أعمق، اطلع على PivotTable API الخاصة بـ Aspose.Cells لتعديل الفلاتر، الحقول المحسوبة، أو ارتباطات المخططات.

Happy coding, and feel free to experiment with the code to fit your specific Excel automation needs!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف Excel جديد – نسخ وتكرار جدول محوري](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [إنشاء جدول محوري في Excel باستخدام Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [تغيير تخطيطات جدول محوري في Excel بكفاءة باستخدام Aspose.Cells for .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}