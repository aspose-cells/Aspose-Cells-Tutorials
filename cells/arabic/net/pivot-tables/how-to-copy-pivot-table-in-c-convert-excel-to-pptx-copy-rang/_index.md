---
category: general
date: 2026-01-14
description: كيفية نسخ جدول محوري باستخدام Aspose.Cells وتعلم تحويل Excel إلى PPTX،
  ونسخ نطاق إلى مصنف آخر، وجعل مربع النص قابل للتحرير في PPTX في دليل واحد.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: ar
og_description: كيفية نسخ جدول محوري ثم تحويل Excel إلى PPTX، نسخ نطاق إلى مصنف آخر،
  وجعل مربع النص قابل للتحرير في PPTX — كل ذلك باستخدام Aspose.Cells.
og_title: كيفية نسخ جدول محوري في C# – دليل كامل لتحويل Excel إلى PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: كيفية نسخ جدول Pivot في C# – تحويل Excel إلى PPTX، نسخ النطاق وجعل مربع النص
  قابلاً للتحرير
url: /ar/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في C# – دليل كامل لتحويل Excel إلى PPTX

كيفية نسخ جدول محوري من مصنف إلى آخر هو سؤال شائع عندما تقوم بأتمتة التقارير المستندة إلى Excel. في هذا الدرس سنستعرض ثلاث سيناريوهات واقعية باستخدام **Aspose.Cells for .NET**: نسخ نطاق جدول محوري، تصدير ورقة عمل إلى ملف PPTX مع مربع نص قابل للتحرير، وتعبئة خلية واحدة بمصفوفة JSON عبر Smart Markers.

سترى أيضًا كيفية **تحويل Excel إلى PPTX**، **نسخ نطاق إلى مصنف آخر**، و **جعل مربع النص قابل للتحرير في PPTX** دون كسر أي تنسيق. في النهاية ستحصل على قاعدة شفرة جاهزة للتنفيذ يمكنك إدراجها في أي مشروع .NET.

> **نصيحة احترافية:** جميع الأمثلة تستهدف Aspose.Cells 23.12، لكن نفس المفاهيم تنطبق على الإصدارات السابقة مع تعديلات بسيطة في API.

![مخطط يوضح كيفية نسخ جدول محوري، وتصدير ورقة عمل إلى PPTX، وإدراج مصفوفة JSON – سير عمل نسخ جدول محوري](how-to-copy-pivot-table-diagram.png)

---

## ما ستحتاجه

- Visual Studio 2022 (أو أي بيئة تطوير C#)  
- .NET 6.0 أو إصدار أحدث  
- حزمة Aspose.Cells for .NET عبر NuGet  
  ```bash
  dotnet add package Aspose.Cells
  ```
- ملفّان Excel تجريبيان (`source.xlsx`, `chartWithTextbox.xlsx`) موجودان في مجلد تتحكم فيه (استبدل `YOUR_DIRECTORY` بالمسار الفعلي الخاص بك).

لا توجد مكتبات إضافية مطلوبة؛ فإن تجميع `Aspose.Cells` نفسه يتعامل مع Excel و PPTX و Smart Markers.

---

## كيفية نسخ جدول محوري والحفاظ على بياناته

عند نسخ نطاق يحتوي على جدول محوري، السلوك الافتراضي هو لصق **القيم** فقط. للحفاظ على تعريف الجدول المحوري دون تغيير يجب تمكين العلم `CopyPivotTable`.

### خطوة بخطوة

1. **تحميل المصنف المصدر** الذي يحتوي على الجدول المحوري.  
2. **إنشاء مصنف هدف فارغ** – سيستقبل النطاق المنسوخ.  
3. **استخدام `CopyRange` مع `CopyPivotTable = true`** بحيث ينتقل تعريف الجدول المحوري مع البيانات.  
4. **حفظ ملف الهدف** في أي مكان تحتاجه.

#### مثال كامل للكود

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**لماذا يعمل هذا:**  
`CopyOptions.CopyPivotTable` يخبر Aspose.Cells بنسخ كائن `PivotTable` الأساسي بدلاً من قيمه المعروضة فقط. الآن يحتوي المصنف الهدف على جدول محوري كامل الوظائف يمكنك تحديثه أو تعديله برمجيًا.

**حالة خاصة:** إذا كان المصنف المصدر يستخدم مصادر بيانات خارجية، قد تحتاج إلى تضمين البيانات أو تعديل سلاسل الاتصال بعد النسخ، وإلا سيظهر الجدول المحوري “#REF!”.

---

## تحويل Excel إلى PPTX وجعل مربع النص قابل للتحرير

تصدير ورقة عمل إلى PowerPoint مفيد لإنشاء عروض شرائح مباشرة من البيانات. بشكل افتراضي يصبح مربع النص المُصدّر شكلًا ثابتًا، لكن ضبط `IsTextBoxEditable` يغيّر هذا السلوك.

### خطوة بخطوة

1. **فتح المصنف** الذي يحتوي على المخطط ومربع النص الذي تريد تصديره.  
2. **تهيئة `ImageOrPrintOptions`** مع `SaveFormat = SaveFormat.Pptx`.  
3. **تحديد منطقة الطباعة** التي تشمل مربع النص.  
4. **تمكين `IsTextBoxEditable`** بحيث يمكن تحرير النص بعد فتح ملف PPTX.  
5. **حفظ ملف PPTX**.

#### مثال كامل للكود

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**النتيجة:** افتح `result.pptx` في PowerPoint – سيصبح مربع النص الذي وضعته في Excel الآن مربع نص عادي يمكنك الكتابة فيه. لا حاجة لإعادة إنشائه يدويًا.

**مشكلة شائعة:** إذا كانت ورقة العمل تحتوي على خلايا مدمجة تتقاطع مع منطقة الطباعة، قد يتحرك الشريحة الناتجة. قم بضبط منطقة الطباعة أو فك دمج الخلايا قبل التصدير.

---

## نسخ نطاق إلى مصنف آخر باستخدام Smart Markers (JSON → خلية واحدة)

أحيانًا تحتاج إلى تضمين مصفوفة JSON في خلية Excel واحدة، على سبيل المثال عند تمرير البيانات إلى أنظمة لاحقة تتوقع سلسلة JSON. يمكن لـ Smart Markers في Aspose.Cells تسلسل مصفوفة كخلية واحدة عندما تضبط `ArrayAsSingle = true`.

### خطوة بخطوة

1. **تحميل مصنف قالب** يحتوي على عنصر نائب Smart Marker (مثل `&=Items.Name`).  
2. **تحضير كائن البيانات** – نوع مجهول يحتوي على مصفوفة `Items`.  
3. **إنشاء `SmartMarkerProcessor`** وتطبيق البيانات مع `ArrayAsSingle`.  
4. **حفظ المصنف المملوء**.

#### مثال كامل للكود

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**شرح:**  
عندما تكون `ArrayAsSingle` true، يقوم Aspose.Cells بدمج كل عنصر من `Items.Name` في سلسلة على نمط JSON (`["A","B"]`) ويكتبها في الخلية التي احتوت Smart Marker. هذا يتجنب إنشاء صف منفصل لكل عنصر من المصفوفة.

**متى يُستخدم:** مثالي لتصدير جداول الإعدادات، حمولات API، أو أي سيناريو يتوقع فيه المستهلك سلسلة JSON مضغوطة بدلاً من تخطيط جدولي.

---

## نصائح إضافية ومعالجة الحالات الخاصة

| السيناريو | ما يجب مراقبته | الحل المقترح |
|----------|-------------------|---------------|
| **جداول محورية كبيرة** | ارتفاع استهلاك الذاكرة عند نسخ مخازن الجداول المحورية الضخمة. | استخدم `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` قبل التحميل. |
| **تصدير إلى PPTX مع الصور** | قد يتم تحويل الصور إلى نقطية بدقة DPI منخفضة. | اضبط `pptxOptions.ImageResolution = 300` للحصول على شرائح أكثر وضوحًا. |
| **تنسيق JSON في Smart Marker** | الأحرف الخاصة (`"` , `\`) تكسر JSON. | قم بتهريبها يدويًا أو استخدم `JsonSerializer` لتسلسلها مسبقًا قبل تمريرها إلى Smart Markers. |
| **نسخ نطاق عبر إصدارات Excel مختلفة** | قد تفقد ملفات `.xls` القديمة التنسيق. | احفظ الهدف كملف `.xlsx` للحفاظ على الميزات الحديثة. |

---

## ملخص – كيفية نسخ جدول محوري والقيام بالمزيد

بدأنا بالإجابة على **كيفية نسخ جدول محوري** مع الحفاظ على وظيفته، ثم أظهرنا لك كيفية **تحويل Excel إلى PPTX**، **جعل مربع النص قابل للتحرير في PPTX**، وأخيرًا كيفية **نسخ نطاق إلى مصنف آخر** باستخدام Smart Markers لتضمين مصفوفة JSON كخلية واحدة.

جميع المقاطع الثلاثة مستقلة؛ يمكنك لصقها في تطبيق Console جديد، تعديل مسارات الملفات، وتشغيلها اليوم.

---

## ما التالي؟

- **استكشاف صيغ تصدير أخرى** – Aspose.Cells يدعم أيضًا PDF و XPS و HTML.  
- **تحديث الجداول المحورية برمجيًا** باستخدام `PivotTable.RefreshData()` بعد النسخ.  
- **دمج Smart Markers مع المخططات** لإنشاء لوحات معلومات ديناميكية تتحدث تلقائيًا.  

إذا كنت مهتمًا **بحفظ المصنف كـ PPTX** مع تخطيطات شرائح مخصصة، اطلع على وثائق Aspose.Cells حول `SlideOptions`.

لا تتردد في التجربة—بدل منطقة الطباعة، جرّب `CopyOptions` مختلفة، أو قدم حمولة JSON أكثر تعقيدًا. الـ API مرن بما يكفي لمعظم خطوط تقارير البيانات.

---

### الأسئلة المتكررة

**س: هل `CopyPivotTable` ينسخ أيضًا مقاطع التصفية؟**  
ج: ليس مباشرة. مقاطع التصفية هي كائنات منفصلة؛ بعد النسخ ستحتاج إلى إعادة إنشائها أو نسخها عبر مجموعة `Worksheet.Shapes`.

**س: هل يمكنني تصدير عدة أوراق عمل إلى مجموعة PPTX واحدة؟**  
ج: نعم. قم بالتكرار عبر كل ورقة عمل، استدعِ `Save` بنفس `ImageOrPrintOptions` واضبط `pptxOptions.StartSlideNumber` لاستمرار الترقيم.

**س: ماذا لو احتوت مصفوفة JSON الخاصة بي على كائنات متداخلة؟**  
ج: اضبط `ArrayAsSingle = false` واستخدم قالبًا مخصصًا يتكرر على

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}