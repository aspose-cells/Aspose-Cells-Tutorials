---
category: general
date: 2026-11-16
description: تعلم كيفية حفظ Excel كـ PowerPoint وتحويل Excel إلى PowerPoint برمجياً.
  يغطي هذا الدليل خطوة بخطوة أيضًا تصدير Excel إلى PPTX وحفظ المصنف كـ PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: ar
lastmod: 2026-11-16
og_description: احفظ ملف Excel كـ PowerPoint باستخدام Aspose.Cells. اتبع هذا الدليل
  لتحويل Excel إلى PowerPoint، وتصدير Excel إلى PPTX، وحفظ المصنف كـ PPTX في دقائق.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: حفظ إكسل كـ باوربوينت – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: كيفية حفظ ملف Excel كـ PowerPoint باستخدام Aspose.Cells في C#
url: /ar/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ Excel كـ PowerPoint باستخدام Aspose.Cells في C#

إذا كنت بحاجة إلى **حفظ Excel كـ PowerPoint** برمجيًا، فإن هذا الدليل يقدم لك حلاً كاملاً وجاهزًا للتنفيذ. سواءً كنت تبني محرك تقارير أو مولد شرائح تلقائي، فإن الخطوات أدناه تسمح لك بتحويل ورقة عمل Excel إلى شريحة PPTX قابلة للتحرير ببضع أسطر من الشيفرة فقط.

سوف تتعلم كيف **تحول Excel إلى PowerPoint**، وتصدّر الورقة إلى ملف PPTX، وتحافظ على قابلية تحرير مربعات النص والأشكال – كل ذلك دون مغادرة بيئة .NET.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7.2+)
* رخصة Aspose.Cells صالحة (الإصدار التجريبي المجاني يعمل للتقييم)
* Visual Studio 2022 (أو أي بيئة تطوير C#)
* مصنف Excel يحتوي على البيانات والأشكال التي تريد تصديرها

## الخطوة 1: تثبيت Aspose.Cells

أضف حزمة Aspose.Cells NuGet إلى مشروعك:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** استخدم العلامة `-v` لتحديد نسخة معينة، مثل `Aspose.Cells.24.5`.

## الخطوة 2: تحميل المصنف الذي تريد تصديره

العملية الأولى في سير عمل **حفظ Excel كـ PowerPoint** هي تحميل المصنف المصدر.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*لماذا هذا مهم:* تحميل المصنف يمنحك الوصول إلى أوراق العمل، إعدادات الصفحة، وكائنات الرسم التي ستتحول إلى أشكال PowerPoint قابلة للتحرير.

## الخطوة 3: تكوين خيارات التصدير لشريحة PPTX قابلة للتحرير

لـ **تحويل Excel إلى PowerPoint** مع الحفاظ على قابلية التحرير، يجب ضبط بعض الخصائص على `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*شرح:*  
* `SaveFormat = SaveFormat.Pptx` يخبر Aspose.Cells بإنشاء ملف PowerPoint.  
* `ExportEditableText` و `ExportEditableShapes` يضمنان أن الشريحة الناتجة تتصرف كشرائح PowerPoint الأصلية — يمكنك النقر على مربع نص أو شكل وتحريره مباشرة في PowerPoint.

## الخطوة 4: تحديد منطقة التصدير وتكييفها لتظهر في شريحة واحدة

عند **تصدير Excel إلى PPTX**، عادةً ما تريد نطاقًا محددًا يظهر على الشريحة. ضبط منطقة الطباعة وخيارات التكييف يضمن مخرجات نظيفة وشريحة واحدة.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*لماذا هذا مهم:* `PrintArea` يحدّد التصدير إلى الخلايا من A1 إلى G30، بينما `FitToPagesTall` و `FitToPagesWide` يضغطان كل شيء في شريحة واحدة، مما يمنع الصفحات الإضافية غير المرغوبة.

## الخطوة 5: حفظ ورقة العمل كملف PPTX قابل للتحرير

الآن يمكنك أخيرًا **حفظ المصنف كـ PPTX** وإكمال عملية **حفظ Excel كـ PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

بعد تشغيل البرنامج، افتح `EditableShapes.pptx` في Microsoft PowerPoint. سترى شريحة تعكس النطاق المحدد من Excel، وجميع مربعات النص والأشكال قابلة للتحرير بالكامل.

### النتيجة المتوقعة

* ملف باسم `EditableShapes.pptx` موجود في `C:\Output\`.
* شريحة PowerPoint واحدة تحتوي على النطاق A1:G30.
* مربعات نص، مخططات، وأشكال يمكنك النقر المزدوج عليها وتحريرها مباشرة في PowerPoint.

## الكود الكامل (جاهز للنسخ)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## الأسئلة الشائعة ومعالجة الحالات الخاصة

| السؤال | الإجابة |
|----------|--------|
| **ماذا لو كان لدي عدة أوراق عمل؟** | قم بالتكرار عبر `workbook.Worksheets` وكرر الخطوات 3‑5 لكل ورقة، مع تغيير اسم ملف الإخراج (مثال: `Sheet1.pptx`, `Sheet2.pptx`). |
| **هل يمكنني تصدير المصنف بالكامل إلى مجموعة شرائح PowerPoint واحدة؟** | نعم. اضبط `ExportAllSheets = true` على `ImageOrPrintOptions`. كل ورقة عمل تتحول إلى شريحة منفصلة. |
| **الأشكال تظهر كصور، وليس ككائنات قابلة للتحرير.** | تأكد من أن `ExportEditableShapes = true` وأنك تستخدم Aspose.Cells 24.5+ (الإصدارات السابقة تفتقر إلى هذه الميزة). |
| **ملف PPTX المُنتج كبير جدًا.** | قلل من منطقة الطباعة، أو خفّض دقة الصورة عبر `exportOptions.ImageResolution`. |
| **هل أحتاج إلى رخصة للاستخدام في الإنتاج؟** | الرخصة المدفوعة تزيل علامة التقييم وتفتح الأداء الكامل. النسخة التجريبية المجانية تعمل للاختبار. |

## نصائح لكتابة كود إنتاج قوي

* **تحقق من صحة مسارات الملفات** قبل استدعاء `Workbook` أو `Save` لتجنب `FileNotFoundException`.  
* **غلف عملية التصدير بكتلة try/catch** للتعامل مع أخطاء الترخيص (`Aspose.Cells.LicenseException`).  
* **قم بتحرير المصنف** (`workbook.Dispose()`) عند الانتهاء لتحرير الموارد غير المدارة.  
* **استخدم I/O غير متزامن** (`FileStream` مع `await`) إذا كنت تصدر العديد من الأوراق الكبيرة في خدمة ويب.

## الخطوات التالية

الآن بعد أن عرفت كيفية **حفظ Excel كـ PowerPoint**، يمكنك استكشاف المواضيع ذات الصلة:

* **تصدير Excel إلى PPTX مع تخطيطات شرائح مخصصة** – ضبط `SlideSize` وإضافة شريحة رئيسية.  
* **تحويل شريحة Excel إلى PDF** – استخدم `SaveFormat.Pdf` للحصول على نسخة قابلة للطباعة.  
* **تحويل مجموعة من المصنفات دفعة واحدة** – دمج الحلقة الموضحة أعلاه مع `Directory.GetFiles`.  

جرّب مناطق طباعة مختلفة، خيارات التحجيم، وسمات PowerPoint لتخصيص المخرجات وفقًا لهوية مؤسستك.

---

*برمجة سعيدة! إذا ساعدك هذا الدليل في **تحويل Excel إلى PowerPoint**، لا تتردد في مشاركته مع زملائك أو فتح قضية في مستودع Aspose.Cells على GitHub للحصول على مزيد من المساعدة.*

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حفظ Excel كـ PowerPoint باستخدام C# و Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [كيفية حفظ PPTX من Excel – دليل كامل لتصدير ورقة Excel إلى PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [تحويل Excel إلى PowerPoint – دليل كامل خطوة بخطوة](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}