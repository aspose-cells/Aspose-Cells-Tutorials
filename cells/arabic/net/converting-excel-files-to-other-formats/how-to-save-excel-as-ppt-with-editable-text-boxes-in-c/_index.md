---
category: general
date: 2026-10-07
description: احفظ ملف Excel كـ PPT باستخدام C# مع الحفاظ على قابلية تحرير مربعات النص
  والأشكال. تعلم خطوة بخطوة كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as ppt
- convert excel to powerpoint
- how to export excel
- how to keep textboxes
- convert spreadsheet to presentation
language: ar
lastmod: 2026-10-07
og_description: احفظ ملف Excel كـ PPT باستخدام C# مع الحفاظ على مربعات النص والأشكال.
  اتبع هذا الدليل الكامل لتحويل Excel إلى PowerPoint مع إمكانية التحرير الكاملة.
og_image_alt: Diagram of Excel workbook being saved as PPT with editable text boxes
og_title: حفظ Excel كـ PPT – دليل التحويل القابل للتعديل
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  headline: How to save Excel as PPT with editable text boxes in C#
  type: TechArticle
- description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  name: How to save Excel as PPT with editable text boxes in C#
  steps:
  - name: Why each line matters
    text: 1. **Loading the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you full access to worksheets, charts, and embedded objects. 2. **Configuring
      `PptxSaveOptions`** – Setting `ExportTextBoxesAsEditable` and `ExportShapesAsEditable`
      tells Aspose.Cells to write those objects as native
  - name: Tips for large files
    text: '- **Memory management:** Call `GC.Collect()` after the conversion if you
      process many files in a batch. - **Image quality:** Use `opts.ImageResolution
      = 300` to increase chart clarity when the source contains high‑resolution graphics.
      - **Performance:** Set `opts.CompressionLevel = CompressionLevel.'
  - name: 'Edge case: Converting a macro‑enabled workbook (`.xlsm`)'
    text: Aspose.Cells can read `.xlsm` files, but macros are **not** transferred
      to the PPTX because PowerPoint does not support VBA macros from Excel. If you
      need the macro logic, consider exporting the relevant data first, then recreating
      the macro in PowerPoint VBA manually.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- document‑conversion
title: كيفية حفظ Excel كـ PPT مع مربعات نص قابلة للتعديل في C#
url: /ar/net/converting-excel-files-to-other-formats/how-to-save-excel-as-ppt-with-editable-text-boxes-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ Excel كـ PPT مع مربعات نص قابلة للتحرير في C#

إذا كنت بحاجة إلى **حفظ Excel كـ PPT** مع الحفاظ على قابلية تحرير كل مربع نص وشكل، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. باستخدام Aspose.Cells for .NET يمكنك **تحويل Excel إلى PowerPoint** ببضع أسطر من الشيفرة، مع الحفاظ على التخطيط الأصلي بحيث يمكن تحرير العرض التقديمي الناتج في PowerPoint دون فقدان أي كائنات.

بالإضافة إلى عملية التحويل نفسها، ستتعلم **كيفية تصدير Excel** مع الحفاظ على مربعات النص، وكيفية إبقاء مربعات النص قابلة للتحرير، وكيفية **تحويل جدول البيانات إلى عرض تقديمي** بطريقة تعمل مع دفاتر عمل كبيرة ومخططات معقدة.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الشيفرة تعمل أيضًا مع .NET Framework 4.6+)
- رخصة Aspose.Cells for .NET (الإصدار التجريبي المجاني مناسب للتقييم)
- Visual Studio 2022 (أو أي بيئة تطوير تدعم C#)
- ملف Excel تجريبي يحتوي على مربعات نص أو أشكال أو مخططات (مثال: `WithTextBoxes.xlsx`)

> **نصيحة احترافية:** إذا كنت تستخدم النسخة التجريبية المجانية، ضع `License.SetLicense("Aspose.Total.lic")` مبكرًا في برنامجك لتجنب علامات التقييم المائية.

## كيفية حفظ Excel كـ PPT مع الحفاظ على مربعات النص

هذا القسم يركز مباشرة على الكلمة المفتاحية الأساسية **save Excel as PPT**. الشيفرة أدناه مثال كامل قابل للتنفيذ يمكنك لصقه في مشروع وحدة تحكم جديد.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Presentation;

class Program
{
    static void Main()
    {
        // Step 1: Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBoxes.xlsx");

        // Step 2: Configure PPTX save options to keep text boxes and shapes editable
        PptxSaveOptions saveOptions = new PptxSaveOptions
        {
            ExportTextBoxesAsEditable = true,   // how to keep textboxes editable
            ExportShapesAsEditable = true       // also keep shapes editable
        };

        // Step 3: Save the workbook as an editable PowerPoint presentation
        workbook.Save("YOUR_DIRECTORY/ExportEditable.pptx", saveOptions);

        Console.WriteLine("Excel file has been successfully saved as PPT.");
    }
}
```

### لماذا كل سطر مهم

1. **Loading the workbook** – `Workbook` يقرأ ملف `.xlsx` إلى الذاكرة، مما يمنحك وصولًا كاملًا إلى أوراق العمل، المخططات، والكائنات المدمجة.  
2. **Configuring `PptxSaveOptions`** – ضبط `ExportTextBoxesAsEditable` و `ExportShapesAsEditable` يخبر Aspose.Cells بكتابة تلك الكائنات كأشكال PowerPoint أصلية بدلاً من صور مسطحة. هذا هو المفتاح لـ **how to keep textboxes** قابلة للتحرير بعد التحويل.  
3. **Saving as PPTX** – طريقة `Save` مع كائن `PptxSaveOptions` تقوم بعملية **convert Excel to PowerPoint** الفعلية. الملف الناتج (`ExportEditable.pptx`) يمكن فتحه في Microsoft PowerPoint وتعديله كما أي عرض تقديمي أصلي.

> **ملاحظة:** الناتج يحافظ على عرض الأعمدة الأصلي، ارتفاع الصفوف، وتنسيق الخلايا، لذا يبقى التخطيط البصري مطابقًا لورقة Excel المصدر.

![لقطة شاشة لمخرجات وحدة التحكم تؤكد نجاح التحويل](/images/save-excel-as-ppt-console.png "مخرجات وحدة التحكم بعد حفظ Excel كـ PPT")

*نص بديل للصورة: نافذة وحدة التحكم تظهر “تم حفظ ملف Excel بنجاح كـ PPT.”*

## تحويل Excel إلى PowerPoint – التعامل مع دفاتر العمل الكبيرة

عند **convert spreadsheet to presentation** يحتوي على العديد من أوراق العمل، قد ترغب في أن يصبح كل ورقة شريحة منفصلة. Aspose.Cells يقوم بذلك تلقائيًا، لكن يمكنك ضبط السلوك حسب الحاجة:

```csharp
// Create save options with a custom slide layout
PptxSaveOptions opts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Each worksheet becomes a new slide (default behavior)
    // You can also set opts.OnePagePerSheet = false to merge sheets
};
workbook.Save("LargeExport.pptx", opts);
```

### نصائح للملفات الكبيرة

- **إدارة الذاكرة:** استدعِ `GC.Collect()` بعد التحويل إذا كنت تعالج العديد من الملفات دفعة واحدة.  
- **جودة الصورة:** استخدم `opts.ImageResolution = 300` لزيادة وضوح المخططات عندما يحتوي المصدر على رسومات عالية الدقة.  
- **الأداء:** اضبط `opts.CompressionLevel = CompressionLevel.Maximum` لتقليل حجم ملف PPTX دون التأثير على قابلية التحرير.

## كيفية تصدير Excel مع الحفاظ على الصيغ والمخططات

إذا كان دفتر العمل يحتوي على صيغ، يتم تقييمها أثناء التحويل، وتظهر القيم الناتجة على الشرائح. الصيغ الأصلية **غير** منقولة لأن PowerPoint لا يدعم صيغ Excel أصلاً. ومع ذلك، يمكنك ربط دفتر العمل المصدر بالعرض التقديمي:

```csharp
PptxSaveOptions linkedOpts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Keep a link to the original Excel file for future updates
    LinkToSource = true
};
workbook.Save("LinkedExport.pptx", linkedOpts);
```

عند فتح المستخدم للملف PPTX في PowerPoint، تظهر نافذة تطلب ما إذا كان يجب تحديث البيانات المرتبطة. هذا يلبي المتطلب **how to export Excel** مع السماح بالتعديلات لاحقًا.

## المشكلات الشائعة وكيفية الحفاظ على مربعات النص سليمة

| العَرَض | السبب | الحل |
|---------|-------|-----|
| تظهر مربعات النص كصور | `ExportTextBoxesAsEditable` تركت على القيمة الافتراضية `false` | اضبط `ExportTextBoxesAsEditable = true` |
| لا يمكن تحريك الأشكال في PowerPoint | `ExportShapesAsEditable` غير مفعلة | فعّل `ExportShapesAsEditable = true` |
| فقدان وسوم المخططات | المخطط يستخدم سمة مخصصة غير مدعومة من قبل المحول | استخدم سمة قياسية قبل التحويل |
| العرض التقديمي فارغ | مسار دفتر العمل غير صحيح أو الملف مقفل | تحقق من المسار وتأكد من أن الملف غير مفتوح في مكان آخر |

### حالة خاصة: تحويل دفتر عمل يدعم الماكرو (`.xlsm`)

Aspose.Cells يمكنه قراءة ملفات `.xlsm`، لكن الماكرو **غير** منقولة إلى PPTX لأن PowerPoint لا يدعم ماكرو VBA من Excel. إذا كنت بحاجة إلى منطق الماكرو، فكر في تصدير البيانات ذات الصلة أولاً، ثم إعادة إنشاء الماكرو في VBA الخاص بـ PowerPoint يدويًا.

## التحقق من النتيجة – تحويل جدول البيانات إلى عرض تقديمي بشكل صحيح

بعد تشغيل الشيفرة، افتح `ExportEditable.pptx` في PowerPoint:

1. **اختر مربع نص** – يجب أن ترى مقابض التحجيم المعتادة، مما يؤكد أن الكائن قابل للتحرير.  
2. **انقر بزر الفأرة الأيمن على شكل** – ستظهر قائمة السياق خيارات شكل PowerPoint (تعبئة، خط، إلخ).  
3. **تحقق من ترتيب الشرائح** – يجب أن يتطابق كل ورقة عمل مع شريحة، مع الحفاظ على ترتيب التبويبات الأصلي.

إذا كان أي كائن غير قابل للتحرير، أعد فحص أعلام `PptxSaveOptions`. القيم الافتراضية (`false`) تجعل المحول يرسم الكائنات كصور، لذا فإن ضبطها إلى `true` ضروري لتلبية متطلب **how to keep textboxes**.

## أفضل الممارسات للاستخدام في الإنتاج

- **تفعيل الرخصة مبكرًا:** `License license = new License(); license.SetLicense("Aspose.Total.lic");`  
- **معالجة الاستثناءات:** غلف عملية التحويل داخل كتلة `try/catch` لتظهر أخطاء الوصول إلى الملفات.  
- **التسجيل:** احفظ مسارات المصدر والوجهة مع الطوابع الزمنية لسجلات التدقيق.  
- **اختبار الوحدات:** استخدم دفتر عمل صغير يحتوي على كائنات معروفة لتتحقق من أن PPTX الناتج يحتوي على العدد المتوقع من الأشكال القابلة للتحرير.

```csharp
try
{
    // Conversion code from earlier sections
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Conversion failed: {ex.Message}");
    // Optionally rethrow or handle according to your error policy
}
```

## الخلاصة

أصبح لديك الآن حل كامل وجاهز للإنتاج **لحفظ Excel كـ PPT** مع الحفاظ على مربعات النص، الأشكال، والتخطيط العام. من خلال ضبط `PptxSaveOptions` يمكنك التحكم في **how to keep textboxes** قابلة للتحرير، مما يتيح تعديلًا سلسًا في PowerPoint بعد التحويل. نفس النهج يتيح لك **convert Excel to PowerPoint**، **export Excel**، و**convert spreadsheet to presentation** لأي حجم دفتر عمل.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **تصدير مخططات Excel كصور عالية الدقة**، **تحويل دفاتر عمل متعددة دفعةً**، أو **دمج PPTX المُولد في تطبيق ويب**. كل من هذه يوسع الأساسيات التي تم تغطيتها هنا ويعزز قوة Aspose.Cells في سيناريوهات أتمتة المستندات الواقعية. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells for .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية إضافة والوصول إلى مربعات النص في Excel باستخدام Aspose.Cells .NET | دليل خطوة بخطوة](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [كيفية تحويل أوراق Excel إلى صور باستخدام Aspose.Cells .NET (دليل خطوة بخطوة)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}