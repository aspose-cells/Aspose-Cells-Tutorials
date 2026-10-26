---
category: general
date: 2026-10-26
description: تعلم كيفية استيراد DataTable إلى ورقة عمل Excel باستخدام C# و Aspose.Cells،
  مع الحفاظ على الأنماط والرؤوس في بضع أسطر من الشيفرة فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: ar
lastmod: 2026-10-26
og_description: كيفية استيراد جدول البيانات إلى ورقة عمل Excel باستخدام C# و Aspose.Cells.
  اتبع هذا الدليل الكامل للحفاظ على الأنماط والرؤوس والتنسيق.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: كيفية استيراد DataTable إلى ورقة عمل Excel – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: كيفية استيراد DataTable إلى ورقة عمل Excel باستخدام C#
url: /ar/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استيراد DataTable إلى ورقة عمل Excel باستخدام C#

إذا كنت تحتاج إلى **كيفية استيراد datatable** إلى ورقة عمل Excel، يوضح هذا الدليل الخطوات الدقيقة في C#. سواء كنت تبني محرك تقارير أو تصدر بيانات شبكة، سترى كيف تحافظ على رؤوس الأعمدة وأنماط الخلايا باستخدام Aspose.Cells. الحل يعمل مع .NET 6+ ويتطلب فقط بضع أسطر من الشيفرة.

استيراد DataTable هو مهمة شائعة عند العمل مع جداول البيانات، لكن المطورين غالبًا ما ينسون تمكين نقل النمط أو تمرير علم العنوان بشكل صحيح. في هذا الدرس ستتعلم كيفية تكوين **ImportTableOptions**، تشغيل **ImportDataTableStyle**، واستدعاء `ImportDataTable` بأمان. في النهاية ستحصل على طريقة جاهزة للتنفيذ يمكنك وضعها في أي مشروع C#.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6 SDK أو أحدث مثبت.
* نسخة مرخصة من **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يعمل للاختبار).
* إلمام أساسي بـ `DataTable` ومفاهيم Excel.
* بيئة تطوير متكاملة مثل Visual Studio 2022 (أي محرر يدعم C# يعمل).

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Cells`.

## الخطوة 1: استرجاع البيانات المصدر إلى DataTable

أول شيء تقوم به عندما تجيب على **كيفية استيراد datatable** هو أن تكون البيانات جاهزة. في معظم السيناريوهات الواقعية يأتي `DataTable` من استعلام قاعدة بيانات، أو محلل CSV، أو مجموعة في الذاكرة. إليك مثالًا بسيطًا ينشئ جدولًا ببضع صفوف:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*لماذا هذا مهم*: من خلال إنشاء `DataTable` أولاً، تتحكم في ترتيب الأعمدة، أنواع البيانات، وأسماء العناوين—كل ذلك يُحافظ عليه عند استيراد الجدول لاحقًا إلى ورقة عمل Excel.

## الخطوة 2: إنشاء `ImportTableOptions` وتفعيل استيراد النمط

عند الإجابة على **كيفية استيراد datatable**، القرار التالي هو ما إذا كنت تريد النمط البصري (الخطوط، الألوان، الحدود) الذي قد يكون معرفًا مسبقًا على `DataTable` المصدر. توفر Aspose.Cells الفئة `ImportTableOptions` للتحكم الدقيق. ضبط `ImportDataTableStyle = true` ينسخ معلومات النمط إلى ورقة العمل الهدف.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*لماذا هذا مهم*: بدون تفعيل `ImportDataTableStyle`، ستستخدم الخلايا المستوردة النمط الافتراضي للورقة، مما يفقد أي تنسيق مخصص قد تكون قد طبّقته على `DataTable`. هذه العلامة أساسية لتصدير مصقول.

## الخطوة 3: استيراد DataTable إلى ورقة العمل، بما في ذلك العناوين

الآن لديك كل ما تحتاجه للإجابة على **كيفية استيراد datatable** إلى ملف Excel. تنشئ مصنفًا، تختار ورقة عمل، وتستدعي `ImportDataTable`. الوسيط الثاني للطريقة (`true`) يخبر Aspose.Cells بكتابة رؤوس الأعمدة كصف أول.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

تشغيل `ExportDataTableToExcel("Employees.xlsx")` ينتج ملف `Employees.xlsx` حيث يحتوي الصف الأول على **Id**، **Name**، و**Department**، وتحتفظ كل خلية بالنمط المعرف في `DataTable` الأصلي.

### مثال كامل قابل للتنفيذ

فيما يلي برنامج وحدة تحكم كامل، مستقل، يوضح **كيفية استيراد datatable** ويحفظ النتيجة في الدليل الحالي. انسخه والصقه في مشروع وحدة تحكم جديد وشغّله.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**الناتج المتوقع**  
عند فتح `Employees.xlsx`، سترى:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

جميع الخلايا تحتفظ بالنمط الافتراضي للـ DataTable (الخط، المحاذاة). إذا طبّقت أنماطًا مخصصة على `DataTable` قبل الاستيراد، فإن تلك الأنماط تظهر بنفس الشكل في ورقة العمل لأن `ImportDataTableStyle` مضبوط على `true`.

## المشكلات الشائعة ونصائح أفضل الممارسات

| المشكلة | سبب حدوثها | كيفية تجنبها |
|---------|------------|--------------|
| **العناوين مفقودة** | تمرير `false` كوسيط ثانٍ إلى `ImportDataTable` يتخطى أسماء الأعمدة. | استخدم دائمًا `true` عندما تحتاج إلى العناوين، أو اكتبها يدويًا قبل الاستيراد. |
| **النمط غير منقول** | نسيان تفعيل `ImportDataTableStyle`. | عيّن `ImportDataTableStyle = true` في `ImportTableOptions`. |
| **الجداول الكبيرة تسبب بطء الأداء** | استيراد ملايين الصفوف دون تقسيم. | استورد على دفعات أو استخدم نسخة `ImportDataTable` مع معامل `startRow` لتدفق البيانات. |
| **مرجع ورقة العمل غير صحيح** | استخدام `workbook.Worksheets[1]` عندما توجد ورقة واحدة فقط. | استخدم `workbook.Worksheets[0]` أو أنشئ ورقة جديدة بـ `workbook.Worksheets.Add()`. |
| **انتهاء صلاحية الترخيص** | إصدار تجريبي من Aspose.Cells يعرض علامة مائية بعد 30 يومًا. | طبق ترخيصًا صالحًا بـ `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**نصيحة احترافية**: إذا كنت بحاجة لتطبيق سمة مخصصة بعد الاستيراد، استدعِ `ws.Cells.ApplyStyle(style)` حيث `style` هو كائن `Style` تُكوّنه مرة واحدة وتعيد استخدامه عبر الصفوف.

## توسيع الحل

الآن بعد أن عرفت **كيفية استيراد datatable**، يمكنك استكشاف السيناريوهات المرتبطة:

* **استيراد جداول متعددة** – كرّر عملية الاستيراد على أوراق عمل مختلفة.  
* **التنسيق الشرطي** – بعد الاستيراد، أضف قواعد باستخدام `ws.Cells.ApplyConditionalFormatting`.  
* **التصدير إلى CSV** – استخدم `workbook.Save("file.csv", SaveFormat.Csv)` إذا كان التنسيق النصي البسيط مطلوبًا.  
* **قراءة البيانات مرة أخرى إلى DataTable** – استخدم `ws.Cells.ExportDataTable` للتحقق من سلامة النقل ذهابًا وإيابًا.  

جميع هذه الإضافات تبني على النمط الأساسي الموضح أعلاه: استرجاع البيانات، تكوين خيارات الاستيراد، واستدعاء طريقة واحدة من Aspose.Cells.

## الخلاصة

أصبح لديك الآن إجابة كاملة وجاهزة للإنتاج حول **كيفية استيراد datatable** إلى ورقة عمل Excel باستخدام C#. غطى الدرس استرجاع البيانات المصدر، تكوين `ImportTableOptions` مع `ImportDataTableStyle`، وأداء الاستيراد باستخدام `ImportDataTable`. باتباع عينة الشيفرة ستحافظ على العناوين والأنماط تلقائيًا، ويمكنك تعديل النمط لمجموعات بيانات أكبر، أوراق متعددة، أو احتياجات تنسيق إضافية.

هل أنت مستعد لأتمتة سير عمل التقارير الخاص بك؟ جرّب استبدال `DataTable` النموذجية باستعلام قاعدة بيانات حقيقي، جرب أنماط خلايا مخصصة، ودمج الطريقة في طبقة الخدمة الحالية. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استيراد المصفوفات إلى Excel باستخدام Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [كيفية استيراد بيانات XML إلى Excel باستخدام Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [كيفية استيراد DataTables بتنسيق HTML إلى Excel باستخدام Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}