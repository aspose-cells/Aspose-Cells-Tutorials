---
category: general
date: 2026-10-26
description: تعلم كيفية تصدير مخططات Excel إلى PowerPoint باستخدام C#. احفظ قابلية
  تعديل الأشكال واحفظ كملف PPTX ببضع أسطر من الشيفرة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: ar
lastmod: 2026-10-26
og_description: تصدير مخططات Excel إلى PowerPoint باستخدام C#. يوضح لك هذا الدليل
  كيفية الحفاظ على الأشكال قابلة للتحرير وحفظها كملف PPTX باستخدام Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: تصدير مخططات Excel إلى PowerPoint باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: كيفية تصدير مخططات إكسل إلى باوربوينت باستخدام C#
url: /ar/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير مخططات Excel إلى PowerPoint باستخدام C#

إذا كنت بحاجة إلى **تصدير مخططات Excel إلى PowerPoint**، فإن هذا الدليل يشرح لك حلاً كاملاً جاهزًا للتنفيذ. سواءً كنت تبني لوحة تقارير أو تقوم بأتمتة عروض الشرائح، سترى كيف أن بضع أسطر من كود C# تحافظ على قابلية تحرير أشكال المخطط بالكامل بعد التحويل.

في هذا الدرس ستتعلم كيفية:

* تحميل ملف Excel موجود يحتوي على مخططات.  
* (اختياريًا) تعديل إعدادات المصنف قبل التحويل.  
* حفظ المصنف كملف PowerPoint مع الحفاظ على قابلية تحرير الشكل.  

كل ذلك يتم باستخدام **Aspose.Cells for .NET**، وهي مكتبة تتعامل مع تحويل Excel إلى PowerPoint دون الحاجة إلى Microsoft Office على الخادم.

## ما ستحتاجه

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 أو أحدث | بيئة تشغيل حديثة مع جميع ميزات اللغة |
| Visual Studio 2022 (أو أي بيئة تطوير متكاملة) | محرر ومصحح أخطاء مريح |
| **Aspose.Cells for .NET** حزمة NuGet | توفر فئة `Workbook` ودعم `SaveFormat.Pptx` |
| ملف Excel (`ChartAndShapes.xlsx`) يحتوي على مخطط واحد على الأقل | مصدر المخططات التي تريد تصديرها |

> **نصيحة احترافية:** استخدم النسخة المجانية **Aspose.Cells Evaluation** لاختبار الكود؛ مفتاح الترخيص يزيل علامة التقييم.

```bash
dotnet add package Aspose.Cells
```

## تصدير مخططات Excel إلى PowerPoint – سير العمل الكامل

فيما يلي الكود الشامل الذي ينجز عملية التصدير مع **الحفاظ على قابلية تحرير الشكل**. يتم شرح كل خطوة بالتفصيل.

### الخطوة 1: تحميل ملف Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

تمثل فئة `Workbook` ملف Excel بالكامل. تحميل الملف يقرأ جميع أوراق العمل والمخططات والأشكال إلى الذاكرة، وهو ما يلزم لأي تعديل لاحق.

### الخطوة 2: (اختياري) تعديل إعدادات المصنف

في معظم الحالات تكون الإعدادات الافتراضية كافية لتصدير نظيف. ومع ذلك، إذا كنت بحاجة لتغيير وضع الحساب، إعداد الصفحة، أو إخفاء بعض الأوراق، يمكنك القيام بذلك هنا.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **لماذا هذا مهم:** تعديل الإعدادات قبل التحويل يضمن أن الشرائح المولدة تعكس الحالة الدقيقة التي تريدها، خاصةً عندما يمكن للمعادلات أو الأوراق المخفية أن تؤثر على بيانات المخطط.

### الخطوة 3: حفظ المصنف كملف PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

الثابت `SaveFormat.Pptx` يخبر Aspose.Cells بإنشاء عرض تقديمي PowerPoint. داخليًا، تقوم المكتبة بتحويل كل مخطط Excel إلى شكل PowerPoint يبقى قابلًا للتحرير بالكامل في Microsoft PowerPoint.

### الخطوة 4: التحقق من النتيجة

Open `Shapes.pptx` in PowerPoint and:

1. اختر مخططًا في أي شريحة.  
2. انقر بزر الماوس الأيمن → **Edit Data**.  
3. تأكد من ظهور جدول بيانات المخطط ويمكنك تعديل القيم.

إذا فتح المخطط لوحة **Edit Data**، فإن التحويل نجح وتم الحفاظ على **قابلية تحرير الشكل**.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="مثال على تصدير مخططات Excel إلى PowerPoint"}

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|-------|-----|
| المخططات تظهر كصور ثابتة | استخدام نسخة أقدم من Aspose.Cells لا تدعم تصدير PPTX | الترقي إلى أحدث نسخة Aspose.Cells 23.x أو أحدث |
| بيانات مفقودة في مخطط PowerPoint | المصنف غير محسوب بالكامل قبل التصدير | استدعاء `workbook.CalculateFormula()` قبل `Save` |
| الأشكال غير قابلة للتحرير | الحفظ باستخدام `SaveFormat.Xlsx` بدلاً من `SaveFormat.Pptx` | تأكد من تمرير `SaveFormat.Pptx` إلى `Workbook.Save` |
| استثناء الترخيص أثناء التشغيل | نسخة التقييم بدون ترخيص مسجل | تسجيل الترخيص باستخدام `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### حالة خاصة: تصدير عدة أوراق عمل مع مخططات منفصلة

إذا كان ملف Excel يحتوي على عدة أوراق عمل، كل منها يحتوي على مخطط خاص به، فإن Aspose.Cells ينشئ شريحة منفصلة لكل مخطط تلقائيًا. يمكنك التحكم في ترتيب الشرائح بإعادة ترتيب أوراق العمل قبل عملية الحفظ.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### نصيحة أداء: بث الإخراج بدلاً من الكتابة إلى القرص

عند إنشاء ملفات PowerPoint في واجهة برمجة تطبيقات ويب، تجنب الملفات المؤقتة عن طريق الكتابة إلى `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## مثال كامل قابل للتنفيذ

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**الناتج المتوقع:** يطبع الطرفية رسالة التأكيد، ويفتح `Shapes.pptx` في PowerPoint مع ظهور كل مخطط Excel على شريحة منفصلة. اختيار مخطط يتيح لك تحرير بياناته، مما يؤكد أن **قابلية تحرير الشكل** محفوظة.

## ملخص وخطوات مستقبلية

أنت الآن تعرف كيف **تصدّر مخططات Excel إلى PowerPoint** باستخدام C# مع الحفاظ على قابلية تحرير المخططات بالكامل. جوهر الحل هو طريقة `Workbook.Save` مع `SaveFormat.Pptx`، وهي ميزة من **Aspose.Cells export** التي تُبسط التعامل مع Open XML المعقد.

من هنا يمكنك استكشاف:

* إضافة عناوين شرائح مخصصة أو ملاحظات باستخدام واجهة برمجة تطبيقات **Aspose.Slides**.  
* تحويل كائنات Excel أخرى (جداول، صور) إلى جانب المخططات.  
* أتمتة معالجة دفعات متعددة من المصنفات في خدمة خلفية.

لا تتردد في تجربة الإعدادات الاختيارية المذكورة أعلاه، ودمج هذا النمط في خطوط تقاريرك للحصول على توليد PowerPoint سريع وموثوق.

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تصدير مخطط Excel إلى PowerPoint باستخدام C# – دليل كامل لـ Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [كيفية تصدير Excel إلى PowerPoint باستخدام C# – دليل كامل](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [كيفية تصدير الأشكال من Excel إلى PowerPoint – دليل كامل](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}