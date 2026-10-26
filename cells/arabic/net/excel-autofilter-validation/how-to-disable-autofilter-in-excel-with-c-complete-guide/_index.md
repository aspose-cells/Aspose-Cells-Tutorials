---
category: general
date: 2026-10-26
description: تعطيل الفلتر التلقائي في إكسل باستخدام C#. يوضح هذا الدرس كيفية إزالة
  الفلتر التلقائي من جدول إكسل برمجياً ويتضمن مثالًا عمليًا كاملًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: ar
lastmod: 2026-10-26
og_description: قم بإلغاء تمكين الفلتر التلقائي في Excel بسرعة. اتبع هذا الدليل لإزالة
  الفلتر التلقائي من جدول Excel باستخدام C# و Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: تعطيل الفلتر التلقائي في إكسل باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية تعطيل الفلتر التلقائي في إكسل باستخدام C# – دليل كامل
url: /ar/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعطيل الفلتر التلقائي في Excel باستخدام C# – دليل كامل

إذا كنت بحاجة إلى **تعطيل الفلتر التلقائي في Excel**، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام C#. سواءً كنت تقوم بتنظيف تقرير قبل النشر أو أتمتة خط أنابيب تصدير البيانات، فإن إزالة الفلتر تضمن أن تعرض ورقة العمل كل الصفوف. ستتعلم أيضًا كيفية **إزالة الفلتر التلقائي من جدول Excel** في استدعاء واحد موثوق.

سنستخدم مكتبة **Aspose.Cells for .NET** الشهيرة لأنها تعمل دون الحاجة إلى تثبيت Excel على الخادم. بحلول نهاية هذا الدرس ستحصل على تطبيق وحدة تحكم مستقل يقوم بتحميل مصنف، العثور على أول جدول، وتعطيل الفلتر التلقائي الخاص به. الحل يعمل مع ملفات .xlsx التي تم إنشاؤها بواسطة Excel 2007 أو أحدث.

## ما ستحتاجه

| المتطلبات | لماذا يهم |
|--------------|----------------|
| .NET 6.0 أو أحدث | يوفر بيئة التشغيل لكود C#. |
| Aspose.Cells for .NET (حزمة NuGet `Aspose.Cells`) | يمنح الوصول البرمجي إلى أوراق العمل والجداول والفلترات التلقائية. |
| ملف Excel تجريبي (`Sample.xlsx`) يحتوي على جدول واحد على الأقل مع تطبيق الفلتر التلقائي | يقوم الكود بالعمل على أول جدول؛ وجود جدول يتيح لنا توضيح كيفية تعطيل الفلتر. |
| Visual Studio 2022 (أو أي بيئة تطوير C#) | يسهل بناء وتصحيح تطبيق وحدة التحكم. |

> **نصيحة احترافية:** إذا كنت تفضل بديلاً مجانيًا، يمكنك تعديل الكود لاستخدام **ClosedXML** أو **EPPlus**؛ الفكرة الأساسية—تعيين خاصية `AutoFilter` للجدول إلى `null`—تبقى كما هي.

## الخطوة 1: إنشاء مشروع وحدة تحكم جديد

افتح الطرفية أو موجه أوامر Visual Studio وشغّل الأمر التالي:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

هذا ينشئ مشروعًا جديدًا باسم `ExcelFilterDemo` ويضيف مكتبة Aspose.Cells.

## الخطوة 2: تحميل المصنف وتحديد ورقة العمل الأولى

العملية المنطقية الأولى هي فتح ملف المصنف. تقوم Aspose.Cells بقراءة الملف إلى كائن `Workbook` يمنحك وصولًا مباشرًا إلى أوراق العمل والجداول.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **لماذا هذه الخطوة؟** تحميل المصنف ضروري قبل أن تتمكن من تعديل أي كائنات Excel. استخدام ورقة العمل الأولى (`Worksheets[0]`) يعكس السيناريو الشائع حيث توجد البيانات الأساسية في الورقة الأولى.

## الخطوة 3: استرجاع أول جدول معرف في ورقة العمل

جداول Excel (المعروفة أيضًا باسم ListObjects) هي الحاويات التي تحتفظ بالبيانات المهيكلة. يمكن لكل جدول أن يحتوي على فلتر تلقائي خاص به. لإزالة الفلتر نحتاج أولاً إلى مرجع إلى كائن الجدول.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **حالة حافة:** إذا كان المصنف قد يحتوي على أوراق عمل بدون جداول، غلف الوصول بعبارة `if (worksheet.Tables.Count > 0)` للتحقق. هذا يمنع أخطاء وقت التشغيل ويجعل الحل قويًا.

## الخطوة 4: تعطيل الفلتر التلقائي للجدول

التعطيل الفعلي يتم بسطر واحد: تعيين `null` لخاصية `AutoFilter` لكائن `Table`. هذا يمسح أي معايير للفلتر ويزيل أسهم القوائم المنسدلة من صف الرأس.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

بعد تنفيذ هذا السطر، يتصرف الجدول كنطاق عادي بدون واجهة فلتر.

## الخطوة 5: حفظ المصنف المعدل

أخيرًا، اكتب التغييرات مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد للحفاظ على المصدر.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### الكود الكامل

بجمع جميع الأجزاء معًا، يبدو البرنامج الكامل هكذا:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. بعد التنفيذ، افتح `Sample_NoFilter.xlsx` في Excel؛ ستلاحظ أن أسهم الفلتر اختفت وأن جميع الصفوف مرئية.

## التحقق من أن الفلتر التلقائي قد اختفى فعلاً

1. افتح الملف المحفوظ (`Sample_NoFilter.xlsx`) في Microsoft Excel.  
2. انقر على أي رأس عمود – يجب ألا ترى سهم الفلتر المنسدِل.  
3. إذا ما زلت ترى الأسهم، تحقق مرة أخرى أن الجدول الذي استهدفته هو بالفعل الجدول الذي يحتوي على الفلتر. يمكنك سرد جميع الجداول باستخدام:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

يجب أن يُظهر إخراج وحدة التحكم `Has AutoFilter: False` للجدول الذي قمت بتعديله.

## الأخطاء الشائعة وكيفية تجنّبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | ورقة العمل لا تحتوي على جداول. | أضف شرطًا `if (worksheet.Tables.Count == 0)` قبل الوصول. |
| الملف المحفوظ لا يزال يظهر الفلاتر | قمت بتحرير ورقة العمل أو الجدول الخطأ. | استخدم `wb.Worksheets["SheetName"]` أو تكرار عبر `wb.Worksheets` لتحديد الجدول الصحيح. |
| البرنامج يتعطل على إصدارات .NET القديمة | Aspose.Cells يتطلب .NET 6.0+ للحزمة الأخيرة. | قم بترقية إطار العمل المستهدف في ملف `.csproj`. |
| NullReferenceException عندما يكون `table.AutoFilter` بالفعل null | قمت باستدعاء الكود مرتين على نفس الملف دون إعادة التحميل. | أعد تحميل المصنف أو تحقق `if (table.AutoFilter != null)` قبل التعيين. |

## توسيع الحل

الآن بعد أن عرفت كيفية **تعطيل الفلتر التلقائي في Excel**، قد ترغب في:

* **إزالة الفلتر التلقائي من جدول Excel** فقط عندما يتحقق شرط معين (مثلاً عندما يتم تعيين علم للمستخدم). أضف عبارة `if` حول `table.AutoFilter = null;`.
* **تطبيق فلتر جديد** برمجيًا بعد مسح القديم، باستخدام `table.AutoFilter.Range` و `table.AutoFilter.AddFilterColumn(...)`.
* **معالجة جداول متعددة** في نفس المصنف عن طريق التكرار عبر `worksheet.Tables` وتعطيل كل فلتر.

تتبع هذه الإضافات نفس النمط الموضح أعلاه وتبقي قاعدة الشيفرة نظيفة.

## الخلاصة

أصبح لديك الآن طريقة مختصرة وجاهزة للإنتاج **لتعطيل الفلتر التلقائي في Excel** باستخدام C#. من خلال تحميل المصنف، الوصول إلى أول جدول، وتعيين `table.AutoFilter = null`، تقوم فعليًا **بإزالة الفلتر التلقائي من جدول Excel** دون تفاعل يدوي. المثال الكامل يُترجم، يُنفّذ، وينتج ملفًا نظيفًا جاهزًا لمزيد من الأتمتة أو التوزيع.

لا تتردد في تجربة جداول إضافية، منطق شرطي، أو مكتبات بديلة. إذا صادفت أي حالات حافة، ارجع إلى قسم استكشاف الأخطاء أو استكشف وثائق Aspose.Cells الواسعة لمعالجة الفلاتر المتقدمة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إزالة الفلتر التلقائي من جداول Excel باستخدام C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [مسح واجهة الفلتر في Excel باستخدام C# – إزالة زر AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [كيفية استخدام AutoFilter في أتمتة Excel باستخدام C# – دليل كامل خطوة بخطوة](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}