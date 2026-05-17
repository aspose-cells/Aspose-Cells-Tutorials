---
category: general
date: 2026-03-22
description: تحديد منطقة الطباعة في إكسل وتحويل إكسل إلى باوربوينت بأشكال قابلة للتعديل.
  تعلم كيفية تكرار صف العنوان، إنشاء باوربوينت من إكسل وتصدير إكسل إلى ملف pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: ar
og_description: حدد منطقة الطباعة في Excel وحوّلها إلى شريحة PowerPoint بأشكال قابلة
  للتحرير. اتبع هذا الدليل الكامل لتكرار صف العنوان وتصدير Excel إلى pptx.
og_title: تحديد منطقة الطباعة في إكسل – دليل تصدير إلى باوربوينت
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: تحديد منطقة الطباعة في إكسل وتصديرها إلى باوربوينت – دليل خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين منطقة الطباعة في Excel وتصديرها إلى PowerPoint – دليل برمجة كامل

هل احتجت يومًا إلى **set print area** في ورقة عمل Excel ثم تحويل تلك القطعة إلى شريحة PowerPoint؟ لست وحدك. في العديد من خطوط تقارير البيانات، نفس البيانات التي تُطبع بشكل جيد تحتاج أيضًا إلى الظهور في عرض تقديمي، غالبًا مع تكرار الصف الأول كعنوان. الخبر السار؟ ببضع أسطر من C# يمكنك **convert excel to powerpoint**، الحفاظ على قابلية تحرير جميع مربعات النص، وحتى **repeat title row** تلقائيًا.

في هذا الدليل سنستعرض كل ما تحتاج معرفته: من تكوين منطقة الطباعة إلى إنشاء ملف PPTX يمكنك تحريره مباشرة في PowerPoint. في النهاية ستتمكن من **create powerpoint from excel**، تصدير النتيجة كـ **export excel to pptx**، وإعادة استخدام نفس الكود في أي مشروع .NET. لا سحر، فقط خطوات واضحة ومثال كامل قابل للتنفيذ.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (واجهة برمجة التطبيقات تعمل مع .NET Framework أيضًا)
- **Aspose.Cells for .NET** (المكتبة التي توفر `Workbook`، `ImageOrPrintOptions`، إلخ)
- بيئة تطوير C# أساسية (Visual Studio، Rider، أو VS Code مع امتداد C#)
- ملف Excel (`input.xlsx`) يحتوي على البيانات التي تريد تصديرها

هذا كل شيء—لا توجد حزم NuGet إضافية بخلاف Aspose.Cells. إذا لم تقم بإضافة المكتبة بعد، نفّذ:

```bash
dotnet add package Aspose.Cells
```

الآن نحن جاهزون للبدء.

## الخطوة 1: تحميل الـ Workbook – نقطة البداية للتصدير

أول شيء عليك القيام به هو تحميل الـ workbook الذي يحتوي على الورقة التي تريد تحويلها إلى شريحة. فكر في الـ workbook كمستند المصدر؛ بدونها لا شيء آخر يهم.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**لماذا هذا مهم:** تحميل الـ workbook يمنحك الوصول إلى مجموعة الأوراق، خيارات إعداد الصفحة، ومحرك التصدير. إذا تخطيت هذه الخطوة لن تتمكن من تعيين **print area** أو تكرار أي صفوف.

> **نصيحة احترافية:** استخدم مسارًا مطلقًا أثناء الاختبار، ثم انتقل إلى مسار نسبي أو مسار يعتمد على الإعدادات للإنتاج.

## الخطوة 2: تكوين خيارات التصدير – الحفاظ على قابلية تحرير مربعات النص والأشكال

عند تصديرك إلى PowerPoint ربما تريد أن تكون الشريحة الناتجة قابلة للتحرير. يتيح لك Aspose.Cells التحكم في ذلك باستخدام `ImageOrPrintOptions`. ضبط `ExportTextBoxes` و `ExportShapeObjects` إلى `true` يخبر المكتبة بالحفاظ على تلك الكائنات كعناصر PowerPoint أصلية بدلاً من تحويلها إلى صورة.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**لماذا هذا مهم:** إذا احتجت يومًا إلى **convert excel to powerpoint** ثم تعديل الشريحة يدويًا، فإن هذا الإعداد يوفر عليك إعادة إنشاء مربعات النص من الصفر. كما يضمن بقاء أي أشكال (مثل الأسهم أو المخططات) ككائنات متجهة يمكنك تغيير حجمها.

## الخطوة 3: تعيين منطقة الطباعة وتكرار صف العنوان

الآن نصل إلى جوهر الدرس: **set print area** وجعل الصف الأول يتكرر في كل صفحة مطبوعة (أو، في حالتنا، في الشريحة المصدرة). منطقة الطباعة تخبر Excel أي خلايا يجب اعتبارها للطباعة—أو التصدير في سيناريونا.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**لماذا هذا مهم:** بتحديد التصدير إلى `A1:G20` تتجنب سحب نطاقات فارغة ضخمة، مما يسرّع التحويل ويحافظ على نظافة الشريحة. سطر `PrintTitleRows` يجعل الصف الأول يعمل كعنوان—بالضبط ما تحتاجه عندما **repeat title row** في عرض تقديمي.

> **حالة خاصة:** إذا بدأت بياناتك من الصف 2، عدّل النطاق وفقًا لذلك (مثال: `PrintTitleRows = "$2:$2"`).

## الخطوة 4: حفظ الورقة كملف PowerPoint

أخيرًا، نكتب الشريحة إلى القرص. طريقة `Save` تأخذ اسم الملف الهدف والخيارات التي قمنا بتكوينها سابقًا. النتيجة هي ملف PPTX يحتوي على مربعات نص وأشكال قابلة للتحرير، جاهز للفتح في PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**ما ستراه:** افتح `SheetWithEditableShapes.pptx` في PowerPoint. يظهر الصف الأول كعنوان، جميع الخلايا من `A1:G20` تُعرض، وأي أشكال أضفتها في Excel لا تزال قابلة للتحريك والتحرير. لا صور نقطية—فقط كائنات PowerPoint أصلية.

## مثال عملي كامل – جميع الخطوات مجتمعة

فيما يلي البرنامج الكامل، جاهز للنسخ واللصق. شغّله كتطبيق كونسول أو دمجه في أي حل أكبر.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**المخرجات المتوقعة:** بعد تشغيل البرنامج، يطبع الكونسول رسالة النجاح، ويظهر ملف PPTX في الموقع المحدد. فتح الملف يظهر شريحة واحدة بالنطاق المحدد، مربعات نص قابلة للتحرير، وأي أشكال أصلية.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **هل يعمل هذا مع عدة أوراق عمل؟** | نعم. قم بالتكرار عبر `workbook.Worksheets` وكرر نفس الخطوات لكل ورقة، مع تغيير اسم ملف الإخراج في كل مرة. |
| **ماذا لو احتجت لتصدير أكثر من شريحة واحدة؟** | استدعِ `workbook.Save` عدة مرات مع كائنات `ImageOrPrintOptions` مختلفة، كل واحدة مكوّنة بإعداد `PageSetup` مختلف إذا لزم الأمر. |
| **هل يمكنني تغيير حجم الشريحة؟** | استخدم `exportOptions.ImageFormat` لتحديد DPI، أو عدّل `sheet.PageSetup.PaperSize` قبل الحفظ. |
| **هل Aspose.Cells مجاني؟** | يوفر نسخة تجريبية مجانية مع علامات مائية. للإنتاج، يلزم الحصول على ترخيص. |
| **ماذا عن صيغ Excel؟** | القيم المصدرة هي **النتائج المحسوبة** في وقت التصدير. إذا كنت بحاجة إلى صيغ حية في PowerPoint، فستحتاج إلى نهج مختلف. |

## نصائح لسير العمل بسلاسة

- **نصيحة احترافية:** اضبط `Workbook.Settings.CalcMode = CalculationModeType.Automatic` قبل التصدير لضمان تحديث جميع الصيغ.
- **احذر من:** النطاقات الكبيرة جدًا قد تسبب ضغطًا على الذاكرة. قلل منطقة الطباعة إلى أصغر نطاق ضروري.
- **نصيحة أداء:** أعد استخدام نسخة واحدة من `ImageOrPrintOptions` إذا كنت تصدر عدة أوراق؛ إنشاء نسخة جديدة في كل مرة يضيف عبئًا.
- **ملاحظة الإصدار:** الكود أعلاه يستهدف Aspose.Cells 23.10 (الصادر في نوفمبر 2023). الإصدارات اللاحقة تحتفظ بنفس الـ API، لكن تحقق دائمًا من ملاحظات الإصدار لأي تغييرات كسرية.

## الخلاصة

لقد غطينا كيفية **set print area** في ورقة عمل Excel، تكرار الصف الأول كعنوان، ثم **export excel to pptx** مع الحفاظ على مربعات النص والأشكال القابلة للتحرير. باختصار، الآن تعرف طريقة موثوقة لـ **convert excel to powerpoint**، **repeat title row**، و **create powerpoint from excel** ببضع أسطر من C#.

هل أنت مستعد للخطوة التالية؟ جرّب أتمتة تحويل دفعي لعشرات التقارير، أو أضف تخطيطات شرائح مخصصة باستخدام PowerPoint SDK بعد التصدير. السماء هي الحد—جرب، واختبر، واستمتع بقوة توليد المستندات برمجيًا.

إذا وجدت هذا الدرس مفيدًا، شاركه، اترك تعليقًا بتعديلاتك الخاصة، أو استكشف أدلتنا الأخرى حول **export excel to pptx** ومواضيع الأتمتة ذات الصلة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}