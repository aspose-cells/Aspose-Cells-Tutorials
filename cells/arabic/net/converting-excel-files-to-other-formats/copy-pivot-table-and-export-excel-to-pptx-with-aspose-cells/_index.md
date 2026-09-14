---
category: general
date: 2026-09-11
description: نسخ جدول محوري وتصدير Excel إلى PPTX باستخدام Aspose.Cells. تعلم كيفية
  إنشاء PPTX قابل للتعديل وحفظ المصنف كـ PPTX باستخدام C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: ar
lastmod: 2026-09-11
og_description: نسخ جدول محوري وتصدير Excel إلى PPTX في C# باستخدام Aspose.Cells.
  إنشاء PPTX قابل للتعديل وحفظ المصنف كـ PPTX ببضع أسطر من الشيفرة.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: نسخ جدول محوري وتصدير إكسل إلى PPTX – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: نسخ جدول محوري وتصدير Excel إلى PPTX باستخدام Aspose.Cells
url: /ar/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري وتصدير Excel إلى PPTX باستخدام Aspose.Cells

إذا كنت بحاجة إلى نسخ جدول محوري من ورقة عمل إلى أخرى ثم تصدير ملف Excel إلى عرض تقديمي PowerPoint، يوضح لك هذا الدليل كيفية القيام بذلك. باستخدام Aspose.Cells يمكنك إنشاء PPTX قابل للتحرير وحفظ المصنف كـ PPTX في بضع أسطر فقط من كود C#.

يغطي الدرس كل خطوة مطلوبة لنقل الجدول المحوري، والحفاظ على وظيفته، وإنتاج ملف PPTX حيث يظل المخطط والأشكال قابلة للتحرير. لا تحتاج إلى أدوات خارجية—فقط مكتبة Aspose.Cells وبيئة تطوير .NET.

## ما ستحققه

* **نسخ جدول محوري** من ورقة مصدر إلى ورقة هدف مع الحفاظ على جميع اتصالات البيانات.  
* **تصدير Excel إلى PPTX** بحيث يمكن تعديل الشريحة الناتجة في PowerPoint.  
* **إنشاء PPTX قابل للتحرير** حيث لا يتم تحويل المخططات والجداول والأشكال إلى صور.  
* **حفظ المصنف كـ PPTX** باستخدام نفس استدعاء API الخاص بـ Aspose.Cells.  

### المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.6+).  
* Aspose.Cells for .NET (حزمة NuGet `Aspose.Cells`).  
* فهم أساسي لتطبيقات C# console.  

> **نصيحة احترافية:** قم بتثبيت حزمة NuGet عبر سطر الأوامر لضمان حصولك على أحدث نسخة:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## كيفية نسخ جدول محوري بين أوراق العمل

العملية الأولى هي نقل الجدول المحوري مع الحفاظ على تعريفه. توفر Aspose.Cells طريقة `CopyRange` مع كائن `CopyOptions` يتضمن العلم `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**لماذا يعمل هذا:**  
`CopyRange` ينسخ بيانات الخلايا، التنسيق، وعند كون `CopyPivotTable` صحيحًا، ينسخ ذاكرة التخزين المؤقت للجدول المحوري والبيانات الوصفية. يبدأ النطاق الهدف عند الخلية `A1` (الصف 0، العمود 0) لكن يمكنك تغيير الإزاحات لوضع الجدول المحوري في موقع آخر.

**حالة شائعة:** إذا كانت ورقة الهدف تحتوي بالفعل على جدول محوري بنفس الاسم، سيعيد Aspose.Cells تسمية الجدول الوارد تلقائيًا لتجنب تعارض الأسماء.

## تصدير Excel إلى PPTX وإنشاء PPTX قابل للتحرير

بعد وضع الجدول المحوري في مكانه، يمكنك تصدير المصنف بالكامل إلى ملف PPTX. تسمح لك فئة `ImageOrPrintOptions` بتحديد `ExportImageFormat = ImageFormat.Pptx`، مما يوجه Aspose.Cells لمعالجة المخرجات كعرض تقديمي PowerPoint بدلاً من صورة نقطية.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**لماذا يعمل هذا:**  
عند ضبط `ExportImageFormat` إلى `Pptx`، يحول Aspose.Cells كل ورقة عمل إلى شريحة. تُكتب الأشكال، المخططات، والجداول المحورية ككائنات PowerPoint أصلية، لذا يمكنك النقر المزدوج عليها في PowerPoint وتعديل البيانات الأساسية.

**نصيحة للملفات الكبيرة:** إذا كنت تحتاج فقط إلى مجموعة فرعية من الأوراق، استخدم `workbook.Worksheets.RemoveAt(index)` لإزالة الأوراق التي لا تريد تصديرها قبل استدعاء `Save`. هذا يقلل من حجم ملف PPTX.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يجمع الخطوات السابقة. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج سيظهر:

```
Pivot table copied and workbook exported to PPTX successfully.
```

عند فتح `output.pptx` في Microsoft PowerPoint، ستلاحظ شريحة تحتوي على الجدول المحوري المنسوخ كمخطط قابل للتحرير. النقر المزدوج على المخطط يفتح محرر المخططات في PowerPoint، مما يسمح لك بتعديل السلاسل، المحاور، وعناوين البيانات دون الحاجة للعودة إلى Excel.

## معالجة المشكلات الشائعة

| المشكلة | السبب | الحل |
|-------|-------|-----|
| يظهر الجدول المحوري كصورة ثابتة | تم إهمال علم `CopyPivotTable` أو ضبط `ExportImageFormat` على `Png` | تأكد من `CopyPivotTable = true` و `ExportImageFormat = ImageFormat.Pptx`. |
| تظهر خلايا فارغة في ورقة الهدف | النطاق المصدر لا يغطي كامل مساحة الجدول المحوري | وسّع النطاق (مثال: `"A1:H30"`) لتشمل جميع حقول المحور. |
| حجم ملف PPTX كبير | تم تضمين أوراق عمل غير ضرورية | احذف الأوراق غير المطلوبة قبل استدعاء `Save`. |
| لا يمكن تحرير المخطط في PowerPoint | استخدام نسخة قديمة من Aspose.Cells لا تدعم PPTX | قم بالترقية إلى أحدث نسخة من Aspose.Cells (تحقق من ملاحظات الإصدار). |

## الخطوات التالية والمواضيع ذات الصلة

* **تصدير ورقة Excel إلى PPTX مع تخطيطات شرائح مخصصة** – استكشف `WorksheetToPdfConverter` للتحكم الدقيق في مظهر الشرائح.  
* **تصدير Excel إلى PDF** – استبدل `ImageFormat.Pptx` بـ `ImageFormat.Pdf` لإنشاء ملف PDF بدلاً من ذلك.  
* **تعديل PPTX برمجيًا بعد التصدير** – استخدم مكتبة `Aspose.Slides` لإضافة حركات أو ملاحظات المتحدث.  

من خلال إتقان **نسخ جدول محوري**، **تصدير Excel إلى PPTX**، و**إنشاء PPTX قابل للتحرير**، يمكنك بناء خطوط تقارير شاملة تنقل البيانات من جداول البيانات مباشرة إلى عروض تقديمية دون فقدان القدرة على التحرير.

---


## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}