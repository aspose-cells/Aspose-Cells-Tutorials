---
category: general
date: 2026-10-01
description: نسخ جدول محوري في C# باستخدام Aspose.Cells. تعلم كيفية تحميل مصنف Excel،
  تعريف النطاقات، ونسخ النطاق إلى ورقة العمل مع الحفاظ على الجدول المحوري.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- load excel workbook c#
- copy range to worksheet
language: ar
lastmod: 2026-10-01
og_description: نسخ جدول محوري في C# باستخدام Aspose.Cells. يوضح هذا البرنامج التعليمي
  كيفية تحميل مصنف Excel، نسخ النطاق إلى ورقة العمل، والاحتفاظ بالجدول المحوري.
og_image_alt: Screenshot of C# code copying a pivot table between worksheets
og_title: نسخ جدول محوري في C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Copy pivot table in C# using Aspose.Cells. Learn how to load Excel
    workbook, define ranges, and copy range to worksheet while preserving the pivot.
  headline: Copy pivot table between worksheets in C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: نسخ جدول محوري بين أوراق العمل في C# – دليل خطوة بخطوة
url: /ar/net/pivot-tables/copy-pivot-table-between-worksheets-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري بين أوراق العمل في C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **نسخ جدول محوري** من ورقة إلى أخرى في ملف .xlsx، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام C#. ستتعلم كيفية **تحميل مصنف Excel C#**، تعريف النطاقات المتطابقة، و**نسخ النطاق إلى ورقة العمل** مع الحفاظ على الجدول المحوري. يعمل الحل مع Aspose.Cells .NET، وهي مكتبة تحافظ على تعريفات الجداول المحورية أثناء عمليات النسخ.

## تحميل مصنف Excel في C#

قبل أن تتمكن من معالجة أي بيانات، يجب تحميل مصنف المصدر إلى الذاكرة. توفر Aspose.Cells فئة `Workbook` التي تقرأ الملف وتبني نموذج كائن يمثل أوراق العمل، الخلايا، والجداول المحورية.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Path to the source workbook that contains the original pivot table
        const string sourcePath = @"YOUR_DIRECTORY\Input.xlsx";

        // Load the workbook – this is the step that answers “load excel workbook c#”
        Workbook workbook = new Workbook(sourcePath);
        // The workbook now holds all worksheets, including any pivot tables.
```

**لماذا هذا مهم:** تحميل المصنف مرة واحدة يمنحك مصدرًا موحدًا للبيانات. جميع العمليات اللاحقة تعمل على هذا النموذج في الذاكرة، مما يكون أسرع من فتح الملف مرارًا وتكرارًا.

## تعريف نطاقات المصدر والوجهة

يعيش الجدول المحوري داخل كتلة مستطيلة من الخلايا. لنسخه، تقوم بإنشاء كائن `Range` يضم الكتلة بالكامل. يجب أن تكون الأبعاد نفسها موجودة في ورقة الهدف؛ وإلا سيؤدي النسخ إلى قطع البيانات.

```csharp
        // Step 2: Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.Worksheets[0];

        // Step 3: Define the exact range that includes the pivot table.
        // Adjust "A1:G20" to match the actual size of your pivot.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

> **نصيحة:** إذا لم تكن متأكدًا من النطاق، استخدم `sourceSheet.PivotTables[0].DataRange.FirstCell.Name` و `LastCell.Name` لإنشاء العنوان برمجيًا.

## إضافة ورقة عمل جديدة وتحضير نطاق الوجهة

الآن أنشئ ورقة عمل جديدة ستستضيف النسخة المنسوخة من الجدول المحوري. يجب أن يكون نطاق الوجهة له نفس العنوان مثل نطاق المصدر.

```csharp
        // Step 4: Add a new worksheet for the copy
        Worksheet destinationSheet = workbook.Worksheets.Add();

        // Create a matching range on the new sheet
        Range destinationRange = destinationSheet.Cells.CreateRange("A1:G20");
```

**لماذا هذه الخطوة ضرورية:** الجداول المحورية مرتبطة بسياق ورقة العمل. نسخ النطاق بدون ورقة هدف سيؤدي إلى استثناء لأن الخلايا المستهدفة غير موجودة.

## نسخ النطاق إلى ورقة العمل مع الحفاظ على الجدول المحوري

طريقة `Range.Copy` في Aspose.Cells لا تنسخ القيم الخام فقط، بل تنسخ أيضًا الكائنات الأساسية مثل الجداول المحورية، المخططات، والنطاقات المسماة. هذا هو جوهر **كيفية نسخ جدول محوري** دون فقدان تعريفه.

```csharp
        // Step 5: Perform the copy – the pivot table definition travels with the cells
        sourceRange.Copy(destinationRange);
```

> **نصيحة احترافية:** بعد النسخ، يمكنك التحقق من ظهور الجدول المحوري في `destinationSheet.PivotTables`. طريقة `Copy` تحتفظ بمصدر بيانات الجدول المحوري الأصلي، الفلاتر، والتخطيط.

## حفظ المصنف مع الجدول المحوري المنسوخ

أخيرًا، اكتب المصنف المعدل إلى ملف جديد. يحتوي الملف الناتج على الورقة الأصلية بالإضافة إلى ورقة مكررة تحمل جدولًا محوريًا مطابقًا.

```csharp
        // Step 6: Save the workbook under a new name
        const string outputPath = @"YOUR_DIRECTORY\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        // Optional: Inform the user
        System.Console.WriteLine($"Pivot table copied successfully to {outputPath}");
    }
}
```

عند فتح `CopyWithPivot.xlsx` في Excel، ستظهر ورقتان: الأصلية والجديدة، كل منهما تعرض نفس الجدول المحوري مع نفس الفلاتر والحقول المحسوبة.

## المشكلات الشائعة وأفضل الممارسات

| المشكلة | لماذا يحدث | كيفية تجنبه |
|-------|----------------|-----------------|
| **النطاق لا يغطي كامل الجدول المحوري** | قد يمتد مصدر بيانات الجدول المحوري إلى ما وراء الخلايا المحددة، مما يسبب فقدان حقول. | استخدم خاصية `DataRange` للجدول المحوري لتوليد العنوان تلقائيًا. |
| **ورقة الوجهة تحتوي بالفعل على جدول محوري بنفس الاسم** | Aspose.Cells يطرح تعارضًا في التسمية. | أعد تسمية الجدول المحوري في الوجهة بعد النسخ: `destinationSheet.PivotTables[0].Name = "PivotCopy";` |
| **المصنفات الكبيرة تسبب ضغطًا على الذاكرة** | تحميل المصنف بالكامل إلى الذاكرة قد يكون ثقيلًا. | استخدم `LoadOptions` لتحميل أوراق العمل المطلوبة فقط إذا لم تكن بحاجة إلى الملف بأكمله. |
| **النسخ عبر إصدارات Excel مختلفة** | بعض الإصدارات القديمة لا تدعم بعض ميزات الجداول المحورية. | احفظ النتيجة كملف `.xlsx` (Office Open XML) لضمان التوافق. |

## توسيع الحل

بمجرد أن تحصل على روتين **نسخ جدول محوري** موثوق، يمكنك بناء تدفقات عمل أكثر تعقيدًا:

* **نسخ دفعي:** تكرار عبر جميع أوراق العمل التي تحتوي على جداول محورية وتكرارها في مصنف ملخص.
* **اكتشاف النطاق الديناميكي:** استبدال `"A1:G20"` الصريح بكود يكتشف أبعاد الجدول المحوري تلقائيًا.
* **تحديث الجدول المحوري:** بعد النسخ، استدعِ `destinationSheet.PivotTables[0].RefreshData();` لضمان أن الجدول المحوري يعكس أي تغييرات في مصدر البيانات الأساسي.

## النتيجة المتوقعة

تشغيل البرنامج مع ملف `Input.xlsx` صالح ينتج `CopyWithPivot.xlsx`. عند فتح الملف يظهر:

```
Sheet1 (original)          Sheet2 (copy)
+----------------------+   +----------------------+
| Pivot Table: Sales   |   | Pivot Table: Sales   |
| – Region, Product    |   | – Region, Product    |
| – Sum of Amount      |   | – Sum of Amount      |
+----------------------+   +----------------------+
```

كلا الورقتين تعرض تخطيطات جدول محوري متطابقة، فلاتر، وحقول محسوبة.

## الخلاصة

أنت الآن تعرف كيف **تنسخ جدول محوري** بين أوراق العمل في C# باستخدام Aspose.Cells. غطى الدرس تحميل المصنف، تعريف النطاقات المتطابقة، تنفيذ النسخ، وحفظ النتيجة — كل ذلك مع الحفاظ على التعريف الكامل للجدول المحوري. استخدم نفس النمط لأتمتة التقارير، إنشاء أوراق قالب، أو بناء أدوات ترحيل البيانات.

**الخطوات التالية:**  
* استكشف تنويعات **كيفية نسخ جدول محوري** لعدة جداول في ورقة واحدة.  
* دمج هذه التقنية مع سكريبتات **تحميل مصنف Excel C#** لمعالجة دفعات من الملفات.  
* جرب طريقة **نسخ النطاق إلى ورقة العمل** على المخططات، الجداول، والتنسيقات الشرطية للحصول على حل استنساخ مصنف كامل.  

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}