---
category: general
date: 2026-11-19
description: تعلم كيفية حذف جدول من Excel باستخدام C#. يوضح هذا الدرس أيضًا كيفية
  قراءة ملف Excel باستخدام C# وتحميل دفتر عمل Excel باستخدام C# مع مثال كامل للكود.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete table from excel
- read excel file c#
- how to remove table excel
- load excel workbook c#
- how to delete excel table
language: ar
lastmod: 2026-11-19
og_description: احذف جدولًا من Excel باستخدام C# بسرعة. اتبع هذا الدليل لقراءة ملف
  Excel بـ C# وتحميل دفتر عمل Excel بـ C# مع مثال عملي.
og_image_alt: Screenshot of C# code that deletes a table from an Excel worksheet
og_title: حذف جدول من Excel باستخدام C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to delete table from Excel in C#. This tutorial also shows
    how to read Excel file C# and load Excel workbook C# with a complete code example.
  headline: How to delete table from Excel using C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: كيفية حذف جدول من Excel باستخدام C# – دليل خطوة بخطوة
url: /ar/net/tables-and-lists/how-to-delete-table-from-excel-using-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حذف جدول من Excel باستخدام C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **حذف جدول من Excel** برمجيًا، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام C#. سترى مثالًا كاملًا قابلًا للتنفيذ يقوم بتحميل مصنف Excel، وإزالة الجدول الأول، وحفظ النتيجة. النمط نفسه يغطي أيضًا **read excel file c#** و **load excel workbook c#**، بحيث يمكنك تكييفه مع أي سيناريو أتمتة.

العمل مع ملفات Excel في .NET غالبًا ما يتطلب مكتبة موثوقة. في هذا الدرس نستخدم **Aspose.Cells**، وهو API مُدار بالكامل يدعم الجداول، الصيغ، والتنسيق الغني دون الحاجة إلى Microsoft Office على الخادم. الخطوات قصيرة، والكود مستقل بذاته، وستفهم لماذا كل سطر مهم.

## ما ستحققه

* تحميل ملف `.xlsx` موجود إلى الذاكرة.
* تحديد موقع جدول وحذفه (المعروف أيضًا باسم ListObject) من ورقة العمل.
* حفظ المصنف المعدل إلى ملف جديد.
* توسيع النهج للتعامل مع جداول متعددة أو حالات عدم وجود جدول.

لا يلزم وجود خبرة سابقة مع Aspose.Cells—فقط معرفة أساسية بـ C#.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Core 3.1 و .NET Framework 4.6+).
* Visual Studio 2022 (أو أي محرر يدعم مشاريع .NET).
* حزمة **Aspose.Cells** على NuGet. قم بتثبيتها باستخدام:

```bash
dotnet add package Aspose.Cells
```

* ملف Excel (`input.xlsx`) يحتوي على جدول واحد على الأقل. إذا لم يكن لديك واحد، أنشئ جدولًا بسيطًا في Excel واحفظه في نفس مجلد المشروع.

---

## الخطوة 1: تحميل مصنف Excel في C#

المهمة الأولى هي قراءة المصنف من القرص. هذا هو جوهر **load excel workbook c#**.

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Define file paths
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Step 1: Load the workbook
        Workbook workbook = new Workbook(inputPath);
```

**لماذا هذا مهم:**  
`Workbook` يمثل ملف Excel بالكامل في الذاكرة. تحميله مرة واحدة يتيح لك تنفيذ عمليات متعددة—قراءة الخلايا، تعديل الجداول، أو تغيير التنسيق—دون فتح الملف مرارًا وتكرارًا.

---

## الخطوة 2: الوصول إلى ورقة العمل الأولى (read excel file c#)

بعد تحميل المصنف، تحتاج إلى مرجع لورقة العمل التي تحتوي على الجدول.

```csharp
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

**شرح:**  
`Worksheets` هي مجموعة ذات فهرس يبدأ من الصفر، لذا `[0]` يُعيد الورقة الأولى. إذا كان ملفك يحتوي على تخطيط مختلف، استبدل الفهرس أو استخدم `workbook.Worksheets["SheetName"]`.

---

## الخطوة 3: حذف الجدول من ورقة العمل

الآن نقوم بتنفيذ العملية الأساسية **delete table from excel**. المثال يزيل الجدول الأول، لكن نفس المنطق ينطبق على أي فهرس جدول.

```csharp
        // Step 3: Delete the first table in the worksheet
        if (worksheet.Tables.Count > 0)
        {
            // Table[0] is the first ListObject on the sheet
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }
```

**لماذا هذا يعمل:**  
`Tables` هي مجموعة من كائنات `ListObject`. استدعاء `Delete()` يزيل تعريف الجدول *و* نطاق البيانات الأساسي، تاركًا خلايا عادية خلفه. شرط `if` يطبق **how to remove table excel** بأمان، مما يمنع حدوث استثناء عندما لا تحتوي الورقة على جداول.

**نصيحة احترافية:**  
إذا كنت بحاجة إلى حذف جدول بالاسم بدلاً من الموقع، استخدم `worksheet.Tables["TableName"].Delete();`. هذا مفيد عندما يحتوي المصنف على عدة جداول وتريد استهداف جدول معين فقط.

---

## الخطوة 4: حفظ المصنف المعدل (how to delete excel table)

أخيرًا، اكتب التغييرات مرة أخرى إلى القرص. هذا يكمل سير عمل **how to delete excel table**.

```csharp
        // Step 4: Save the modified workbook
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**ما يحدث في الخلفية:**  
`Save` ينشئ ملف `.xlsx` جديد يعكس جميع التغييرات في الذاكرة. يبقى الملف الأصلي `input.xlsx` دون تعديل، وهو ممارسة آمنة للسكريبتات الإنتاجية.

---

## مثال كامل قابل للتنفيذ

بجمع جميع الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله:

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Load the workbook (load excel workbook c#)
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet (read excel file c#)
        Worksheet worksheet = workbook.Worksheets[0];

        // Delete the first table (delete table from excel)
        if (worksheet.Tables.Count > 0)
        {
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }

        // Save the changes (how to delete excel table)
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**الناتج المتوقع**

```
Table deleted successfully.
Modified workbook saved to YOUR_DIRECTORY\output.xlsx
```

افتح `output.xlsx` في Excel؛ سيظهر الجدول الذي حذفته الآن كخلايا عادية تحتوي على البيانات الأصلية.

---

## معالجة الحالات الشائعة

| Situation | Recommended approach |
|-----------|----------------------|
| **جداول متعددة** | التكرار عبر `worksheet.Tables` وحذف كل واحد، أو الحذف بالاسم باستخدام `worksheet.Tables["MyTable"].Delete();`. |
| **الجدول غير موجود** | شرط `if (worksheet.Tables.Count > 0)` يمنع بالفعل حدوث `NullReferenceException`. يمكنك أيضًا تسجيل تحذير للمراجعة. |
| **ملفات كبيرة** | استخدم `Workbook.LoadOptions` لفتح الملف في وضع **memory‑efficient** (مثال: `LoadOptions { MemorySetting = MemorySetting.MemoryPreference };`). |
| **الحفاظ على التنسيق** | حذف جدول يزيل نمطه. إذا كنت بحاجة إلى الحفاظ على النمط البصري، انسخ النمط إلى النطاق المستهدف قبل استدعاء `Delete()`. |

---

## نصيحة أداء: عمليات الدفعة

إذا كنت بحاجة إلى حذف العديد من الجداول عبر عدة أوراق عمل، غلف التغييرات في نسخة `Workbook` واحدة واستدعِ `workbook.CalculateFormula()` مرة واحدة فقط بعد جميع عمليات الحذف. هذا يقلل من استهلاك المعالج مقارنةً بإعادة الحساب بعد كل حذف جدول.

---

## الخطوات التالية

الآن بعد أن عرفت **how to remove table excel** و **delete table from excel**، قد ترغب في:

* **Read Excel file C#** لاستخراج البيانات بعد إزالة الجدول. مجموعة `Cells` تتيح لك التجول عبر الصفوف والأعمدة.
* إنشاء جداول جديدة برمجيًا باستخدام `worksheet.Tables.Add()`—مفيد لسيناريوهات التقارير.
* استكشاف ميزات أخرى في Aspose.Cells مثل تعديل المخططات، الجداول المحورية، أو التنسيق الشرطي.

كل من هذه المواضيع يبني على نفس كائنات `Workbook` و `Worksheet` التي استخدمتها للتو، لذا فإن تعديل الكود يكون بسيطًا.

---

## الخلاصة

لقد تعلمت كيفية **delete table from Excel** باستخدام C#. يغطي الدليل تحميل المصنف، الوصول إلى ورقة العمل، حذف الجدول بأمان، وحفظ الملف المحدث—كل ذلك مع مثال كامل قابل للتنفيذ. مع هذه الأساسيات يمكنك أتمتة أي سير عمل يعتمد على Excel، سواء كنت تحتاج إلى **read excel file c#**، **load excel workbook c#**، أو **how to delete excel table** في سيناريوهات أكثر تعقيدًا.

لا تتردد في تجربة جداول متعددة، أوراق عمل مختلفة، أو مكتبات بديلة مثل EPPlus إذا كنت تفضل حلاً مفتوح المصدر. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [قراءة ملف Excel C# – كيفية تحميل مصنف Excel C# بكفاءة](/cells/english/net/loading-and-saving-excel-files-with-options/read-excel-file-c-how-to-load-excel-workbook-c-efficiently/)
- [كيفية حذف الصفوف من جدول Excel وتغيير اسمه في C#](/cells/english/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/)
- [كيفية إعادة تسمية جدول في Excel باستخدام C# – دليل خطوة بخطوة](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}