---
category: general
date: 2026-08-17
description: حفظ Excel كملف DOCX باستخدام Aspose.Cells – تحويل سريع لدفتر عمل Excel
  أو مخطط إلى مستند Word قابل للتحرير (DOCX) ببضع أسطر من كود C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as docx
- convert excel to word
- convert spreadsheet to word document
- export chart from excel to word
- save excel file as word document
language: ar
lastmod: 2026-08-17
og_description: احفظ ملف Excel كـ docx باستخدام Aspose.Cells في C#. يوضح لك هذا الدليل
  خطوة بخطوة كيفية تحويل مصنف Excel، بما في ذلك المخططات المدمجة، إلى مستند Word قابل
  للتحرير.
og_image_alt: Screenshot of C# code converting an Excel file with a chart into a Word
  DOCX file
og_title: حفظ ملف Excel كـ DOCX – دليل C# الكامل باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: save excel as docx using Aspose.Cells – quickly convert an Excel workbook
    or chart to an editable Word document (DOCX) with a few lines of C# code.
  headline: How to save Excel as DOCX with Aspose.Cells in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to Word
- DOCX conversion
title: كيفية حفظ ملف Excel كـ DOCX باستخدام Aspose.Cells في C#
url: /ar/java/integration-interoperability/how-to-save-excel-as-docx-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ Excel كملف DOCX باستخدام Aspose.Cells في C#

إذا كنت بحاجة إلى **حفظ Excel كملف DOCX**، فإن هذا الدليل يشرح لك الخطوات الدقيقة المطلوبة في C#. سواء كنت تريد **تحويل Excel إلى Word** للتحرير اللاحق أو تضمين مخطط Excel داخل تقرير Word، فإن الحل أدناه يتعامل مع كلا السيناريوهين بأقل قدر من الشيفرة.

في هذا البرنامج التعليمي ستتعلم كيفية:

* تحميل مصنف `.xlsx` موجود يحتوي على بيانات ومخططات.  
* تصدير المصنف (أو مجرد مخطط) إلى ملف Word قابل للتحرير بامتداد `.docx`.  
* التعامل مع الحالات الشائعة مثل وجود أوراق عمل متعددة وتكبير المخطط.

المتطلب الوحيد هو مكتبة Aspose.Cells for .NET، التي توفر overload لـ `Workbook.save` الذي يكتب مباشرةً إلى صيغة Word.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث | يوفر ميزات لغة حديثة ودعم طويل الأمد. |
| Visual Studio 2022 (أو أي بيئة تطوير C#) | يجعل عملية التصحيح وإدارة المشروع أسهل. |
| **Aspose.Cells for .NET** حزمة NuGet | تزودك بطريقة `Workbook.save(..., SaveFormat.DOCX)` المستخدمة **لحفظ ملف Excel كمستند Word**. |

قم بتثبيت الحزمة باستخدام .NET CLI:

```bash
dotnet add package Aspose.Cells
```

## الخطوة 1: إنشاء مشروع وحدة تحكم C#

افتح الطرفية واكتب:

```bash
dotnet new console -n ExcelToWordDemo
cd ExcelToWordDemo
```

هذا ينشئ مشروعًا بسيطًا يمكنك لصق كود التحويل فيه.

## الخطوة 2: تحميل مصنف Excel الذي يحتوي على المخطط

العملية الأولى هي قراءة ملف `.xlsx` المصدر. تدعم Aspose.Cells كلًا من المسارات المحلية والتدفقات، لذا يمكنك تحميل المصنفات من القرص، أو التخزين السحابي، أو مصفوفة بايت.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source Excel file that contains data and optionally a chart.
        const string sourcePath = @"YOUR_DIRECTORY\chart.xlsx";

        // Load the workbook. The constructor automatically detects the format.
        Workbook workbook = new Workbook(sourcePath);

        Console.WriteLine($"Workbook loaded. Worksheets count: {workbook.Worksheets.Count}");
```

**لماذا هذه الخطوة مهمة:** تحميل المصنف يتحقق من وجود الملف وأن Aspose.Cells يمكنه تحليل البنى الداخلية (الخلايا، الجداول، المخططات). إذا كان الملف تالفًا، سيتم رمي استثناء هنا، مما يتيح لك معالجة الخطأ قبل محاولة التحويل.

## الخطوة 3: (اختياري) تصدير مخطط واحد بدلاً من المصنف بالكامل

إذا كان هدفك هو **تصدير المخطط من Excel إلى Word** بدلاً من كامل الجدول، يمكنك استخراج المخطط كصورة وإدراجه في مستند Word جديد يدويًا. المقتطف التالي يوضح كلا النهجين.

```csharp
        // ------------------------------------------------------------
        // Option A: Convert the entire workbook (including all charts)
        // ------------------------------------------------------------
        // The SaveFormat.DOCX overload writes the full workbook to a
        // Word document where each worksheet becomes a separate table.
        // This is the simplest way to **convert spreadsheet to Word document**.
        const string docxPathFull = @"YOUR_DIRECTORY\chart_editable.docx";
        workbook.Save(docxPathFull, SaveFormat.DOCX);
        Console.WriteLine($"Full workbook saved as DOCX at: {docxPathFull}");

        // ------------------------------------------------------------
        // Option B: Export only the first chart as a picture
        // ------------------------------------------------------------
        // Some scenarios require only the visual chart without the data grid.
        // The code below extracts the first chart from the first worksheet.
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Charts.Count > 0)
        {
            // Render the chart to an image (PNG by default).
            var chart = sheet.Charts[0];
            using var chartImage = chart.ToImage();

            // Save the image temporarily.
            string tempImagePath = @"YOUR_DIRECTORY\temp_chart.png";
            chartImage.Save(tempImagePath, System.Drawing.Imaging.ImageFormat.Png);
            Console.WriteLine($"Chart extracted to image: {tempImagePath}");

            // Create a new empty workbook that will be saved as DOCX.
            Workbook chartOnlyWorkbook = new Workbook();
            Worksheet chartSheet = chartOnlyWorkbook.Worksheets[0];
            // Insert the picture into the worksheet; when saved as DOCX,
            // the picture appears in the Word document.
            int pictureIndex = chartSheet.Pictures.Add(0, 0, tempImagePath);
            chartSheet.Pictures[pictureIndex].Placement = PlacementType.FreeFloating;
            const string docxPathChartOnly = @"YOUR_DIRECTORY\chart_only.docx";
            chartOnlyWorkbook.Save(docxPathChartOnly, SaveFormat.DOCX);
            Console.WriteLine($"Chart-only DOCX created at: {docxPathChartOnly}");
        }
        else
        {
            Console.WriteLine("No charts found in the workbook – only the full conversion was performed.");
        }
    }
}
```

### شرح الكود

* **الخيار A** يستخدم `Workbook.Save(..., SaveFormat.DOCX)` الذي يقوم مباشرةً **بحفظ Excel كملف DOCX**. يتم تحويل كل ورقة عمل إلى جدول Word، وأي مخططات مدمجة تصبح كائنات Word قابلة للتحرير.
* **الخيار B** يوضح نهجًا أكثر تفصيلًا لمتطلب **تصدير المخطط من Excel إلى Word**. يقوم بـ:
  1. جلب أول مخطط عبر `sheet.Charts[0]`.
  2. تحويل المخطط إلى صورة PNG (`chart.ToImage()`).
  3. إدراج الصورة في مصنف جديد.
  4. حفظ ذلك المصنف كملف DOCX، مما ينتج ملف Word يحتوي فقط على صورة المخطط.

كلا المسارين يضمنان أن ملف `.docx` الناتج قابل للتحرير بالكامل في Microsoft Word.

## الخطوة 4: التحقق من النتيجة

افتح الملفات التي تم إنشاؤها (`chart_editable.docx` و/أو `chart_only.docx`) في Microsoft Word:

* **التحويل الكامل** – يجب أن ترى كل ورقة Excel كجدول منفصل. تظهر المخططات ككائنات مخطط Word قابلة للتحرير يمكنك تعديل حجمها أو تنسيقها.
* **تحويل المخطط فقط** – سترى صورة واحدة تمثل المخطط الأصلي في Excel.

إذا لم يفتح مستند Word، تحقق مرة أخرى من أن ملف Excel المصدر غير محمي بكلمة مرور وأن ترخيص Aspose.Cells (إن كان لديك) تم تطبيقه بشكل صحيح.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|-------|-----|
| ملف Word تالف | نسخة Aspose.Cells مفقودة أو غير متطابقة | استخدم نفس نسخة Aspose.Cells في بيئة التطوير والإنتاج. |
| المخطط يبدو ضبابيًا | تم حفظ PNG بدقة DPI منخفضة | استدعِ `chart.ToImage(300, 300)` لزيادة الدقة قبل الحفظ. |
| تم حفظ ورقة العمل الأولى فقط | تم استدعاء `Workbook.Save` على مصنف يحتوي على أوراق مخفية | عيّن `workbook.Worksheets[i].IsVisible = true` لكل ورقة تريد تضمينها. |
| تحذير الترخيص في وحدة التحكم | نسخة تجريبية من Aspose.Cells | طبّق ترخيصًا صالحًا عبر `License license = new License(); license.SetLicense("Aspose.Cells.lic");` قبل تحميل المصنف. |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه إلى `Program.cs`. استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي حيث يوجد ملف Excel الخاص بك.

```csharp
using System;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1. Load the Excel workbook containing data and charts
        // ------------------------------------------------------------
        const string sourcePath = @"YOUR_DIRECTORY\chart.xlsx";
        Workbook workbook = new Workbook(sourcePath);
        Console.WriteLine($"Workbook loaded. Worksheets: {workbook.Worksheets.Count}");

        // ------------------------------------------------------------
        // 2. Convert the entire workbook to an editable Word document
        // ------------------------------------------------------------
        const string docxPathFull = @"YOUR_DIRECTORY\chart_editable.docx";
        workbook.Save(docxPathFull, SaveFormat.DOCX);
        Console.WriteLine($"Full workbook saved as DOCX: {docxPathFull}");

        // ------------------------------------------------------------
        // 3. (Optional) Export only the first chart as a picture in Word
        // ------------------------------------------------------------
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Charts.Count > 0)
        {
            // Render chart to high‑resolution PNG (300 DPI)
            var chart = sheet.Charts[0];
            using var chartImage = chart.ToImage(300, 300);
            string tempImagePath = @"YOUR_DIRECTORY\temp_chart.png";
            chartImage.Save(tempImagePath, ImageFormat.Png);
            Console.WriteLine($"Chart image saved: {tempImagePath}");

            // Create a new workbook that will become the chart‑only DOCX
            Workbook chartOnlyWb = new Workbook();
            Worksheet chartSheet = chartOnlyWb.Worksheets[0];
            int picIdx = chartSheet.Pictures.Add(0, 0, tempImagePath);
            chartSheet.Pictures[picIdx].Placement = PlacementType.FreeFloating;

            const string docxPathChartOnly = @"YOUR_DIRECTORY\chart_only.docx";
            chartOnlyWb.Save(docxPathChartOnly, SaveFormat.DOCX);
            Console.WriteLine($"Chart‑only DOCX created: {docxPathChartOnly}");
        }
        else
        {
            Console.WriteLine("No charts detected – only full workbook conversion performed.");
        }
    }
}
```

### ناتج وحدة التحكم المتوقع



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تحويل ملفات Excel إلى DOCX باستخدام Aspose.Cells for .NET في C#](/cells/english/net/workbook-operations/convert-excel-to-docx-aspose-csharp/)
- [إنشاء وحفظ مصنف Excel كملف PDF في ASP.NET باستخدام Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [كيفية إنشاء وحفظ مصنف Excel كملف ODS باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}