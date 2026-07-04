---
category: general
date: 2026-07-03
description: كيفية تصدير ملفات Excel إلى PowerPoint مع مربعات نص قابلة للتحرير باستخدام
  Aspose.Cells – دليل خطوة بخطوة لتحويل XLSX إلى PPTX.
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: ar
og_description: كيفية تصدير Excel إلى PowerPoint مع مربعات نص قابلة للتحرير. تعلم
  تحويل XLSX إلى PPTX باستخدام PresentationExportOptions في C#.
og_title: كيفية تصدير إكسل إلى باوربوينت – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: كيفية تصدير إكسل إلى باوربوينت – دليل شامل
url: /ar/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PowerPoint – دليل شامل

هل تساءلت يومًا **كيف تصدر بيانات Excel** مباشرةً إلى عرض PowerPoint دون فقدان قابلية التعديل؟ لست وحدك. في هذا الدرس سنوضح لك طريقة عملية **لإنشاء PowerPoint من Excel** مع الحفاظ على مربعات النص والأشكال قابلة للتعديل بالكامل.

سنستعرض كل سطر من الشيفرة، نشرح لماذا كل إعداد مهم، وننتهي بملف PowerPoint يمكنك فتحه وتعديله فورًا. في النهاية، ستتمكن من **تحويل XLSX إلى PPTX** في استدعاء طريقة واحد، وستفهم كيف تتحكم **خيارات تصدير العرض التقديمي** في النتيجة.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود التالي:

- **.NET 6.0** (أو أي نسخة حديثة من .NET) مثبتة على جهازك.  
- **رخصة** لـ **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يكفي للاختبار).  
- إلمام أساسي بـ C#—لا شيء معقد، فقط القدرة على إنشاء تطبيق console أو مكتبة صغيرة.  
- ملف Excel (`input.xlsx`) ترغب في تحويله إلى مجموعة شرائح.

هذا كل شيء. لا أدوات إضافية، لا COM interop، مجرد كود مُدار نقي.

![مخطط كيفية تصدير Excel إلى PowerPoint](https://example.com/placeholder.png "مخطط يوضح تدفق كيفية تصدير بيانات Excel إلى PowerPoint")

## الخطوة 1: تثبيت Aspose.Cells وإعداد المشروع

لـ **كيف تصدر Excel** تحتاج أولاً إلى المكتبة التي تجعل ذلك ممكنًا. افتح الطرفية في مجلد مشروعك وشغّل:

```bash
dotnet add package Aspose.Cells
```

هذا سيجلب أحدث حزمة Aspose.Cells من NuGet. المكتبة تضم كل ما تحتاجه لـ **خيارات تصدير العرض التقديمي**، لذا لن تحتاج إلى الإشارة إلى تجميعات Office Interop.

> **نصيحة محترف:** إذا كنت تستهدف .NET Framework، استخدم نسخة NuGet المناسبة (مثل `Aspose.Cells.NET`) لتجنب مفاجآت التوافق.

## الخطوة 2: تحميل ملف Excel

الآن بعد أن أصبحت المكتبة جاهزة، لنحمّل الملف المصدر. تمثل فئة `Workbook` المستند Excel بالكامل.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*لماذا هذا مهم:* تحميل المصنف هو الخطوة الأولى في أي سير عمل **تحويل XLSX إلى PPTX**. كائن `Workbook` يحتوي على الأوراق، المخططات، وتنسيق الخلايا، وكل ذلك يمكن ربطه بكائنات PowerPoint لاحقًا.

## الخطوة 3: تكوين خيارات تصدير العرض التقديمي (مربعات نص قابلة للتعديل)

هنا يحدث السحر. بشكل افتراضي، تقوم Aspose.Cells بتصدير الأشكال كصور ثابتة. لجعلها **مربعات نص قابلة للتعديل**، يجب تفعيل العلامة الصحيحة.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **لماذا تمكين `ExportEditableObjects`؟**  
> عندما تكون هذه الخاصية `true`، تقوم Aspose.Cells بترجمة كل شكل Excel إلى شكل PowerPoint أصلي. هذا يعني أنه يمكنك فتح ملف `.pptx` الناتج في PowerPoint وتعديل النص، تغيير حجم المربع، أو تعديل الألوان—تمامًا ما تتوقعه عند **إنشاء PowerPoint من Excel**.

## الخطوة 4: تصدير المصنف إلى PowerPoint

مع تحميل المصنف وتكوين الخيارات، السطر النهائي يحفظ الملف كعرض تقديمي PowerPoint.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*ما ستراه:* ملف `output.pptx` سيحتوي على شريحة واحدة لكل ورقة عمل (بشكل افتراضي). كل شريحة تعكس تخطيط الورقة الأصلية، وكل مربع نص وضعته في Excel سيصبح الآن **مربع نص قابل للتعديل** في PowerPoint.

## الخطوة 5: التحقق من النتيجة وإجراء التعديلات إذا لزم الأمر

افتح `output.pptx` في Microsoft PowerPoint:

1. انتقل إلى شريحة نشأت من ورقة عمل.  
2. انقر على مربع نص—لاحظ أنك تستطيع تعديل النص مباشرة.  
3. عدل حجم الشكل أو لونه؛ التغييرات ستظل محفوظة.

إذا بدا شيء غير صحيح، فكر في هذه التعديلات:

- **تصدير أوراق محددة فقط:** استخدم `workbook.Worksheets.RemoveAt(index)` قبل الحفظ.  
- **التحكم في تخطيط الشريحة:** عيّن `exportOptions.ExportAllSheetsAsSlide = false` وأضف الشرائح يدويًا.  
- **الحفاظ على تنسيق المخططات:** تأكد من وضع المخططات على الورقة قبل التصدير؛ ستتحول تلقائيًا إلى مخططات PowerPoint.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| الأشكال تتحول إلى صور | ترك `ExportEditableObjects` على القيمة الافتراضية (`false`) | تعيين `ExportEditableObjects = true` كما هو موضح في الخطوة 3. |
| الأوراق المفقودة | `Save` تم استدعاؤه قبل إزالة الأوراق غير المطلوبة | إزالة أو إخفاء الأوراق التي لا تحتاجها قبل التصدير. |
| حجم الملف كبير | صور عالية الدقة مدمجة إلى جانب الأشكال | استخدام `exportOptions.ImageResolution = 150` لتقليل DPI إذا لزم الأمر. |
| تحذيرات التوافق في PowerPoint | استخدام نسخة قديمة من Aspose.Cells | الترقي إلى أحدث حزمة NuGet (تدعم PPTX 2016+). |

## مثال عملي كامل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في تطبيق console. يتضمن جميع الخطوات، معالجة الأخطاء، وتعليقات توضيحية.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**الناتج المتوقع في الطرفية:**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

افتح ملف `output.pptx` المُنشأ—سترى كل ورقة عمل تتحول إلى شريحة، وكل شكل أضفته في Excel أصبح الآن **مربع نص قابل للتعديل** يمكنك تعديلّه فورًا.

## ملخص: كيفية تصدير Excel بسرعة وبشكل نظيف

غطينا العملية الكاملة لـ **كيف تصدر Excel**—من تثبيت Aspose.Cells، مرورًا بتكوين **خيارات تصدير العرض التقديمي**، وصولًا إلى **تحويل XLSX إلى PPTX** بمحتوى قابل للتعديل بالكامل. النقاط الأساسية هي:

- استخدم `PresentationExportOptions.ExportEditableObjects = true` للحفاظ على الأشكال قابلة للتعديل.  
- طريقة `Workbook.Save` تقوم بالعمل الشاق؛ لا تحتاج إلى أي COM interop.  
- اضبط الإعدادات الاختيارية (دقة الصورة، اختيار الأوراق) لتنعيم النتيجة.

## ما التالي؟

إذا استمتعت بتحويل الجداول إلى شرائح، قد ترغب أيضًا في استكشاف:

- **تضمين المخططات** كمخططات PowerPoint أصلية (`exportOptions.ExportChartAsShape = false`).  
- **تطبيق سلايد ماستر مخصص** بعد التصدير لتتناسب مع هوية الشركة.  
- **أتمتة التحويلات الجماعية** لعشرات الملفات باستخدام حلقة `foreach` بسيطة.  

جميع هذه المواضيع تعتمد على الأساسيات التي غطيناها للتو، لذا أنت الآن على أرضية ثابتة.

---

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، أو مشاركة كيف طورت هذا النمط في مشاريعك الخاصة. برمجة سعيدة، واستمتع بالجسر السلس بين Excel وPowerPoint!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells for .NET: دليل شامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية إضافة والوصول إلى مربعات النص في Excel باستخدام Aspose.Cells .NET | دليل خطوة بخطوة](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [كيفية تصدير ملفات Excel في .NET باستخدام Aspose.Cells: دليل شامل](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}