---
category: general
date: 2026-06-27
description: كيفية تصدير Excel باستخدام C# — تعلم تحويل Excel إلى PowerPoint، إنشاء
  PowerPoint من Excel، وتحميل ملف Excel باستخدام C# في دقائق.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: ar
og_description: كيفية تصدير Excel باستخدام C# بسيطة. اتبع هذا الدليل خطوة بخطوة لتحويل
  Excel إلى PowerPoint، وإنشاء PowerPoint من Excel، وتحميل مصنف Excel باستخدام C#.
og_title: كيفية تصدير إكسل إلى باوربوينت – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: كيفية تصدير Excel إلى PowerPoint – دليل C# الكامل
url: /ar/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PowerPoint – دليل C# كامل

هل تساءلت يومًا **كيف تصدر بيانات Excel** مباشرةً إلى عرض PowerPoint دون فقدان التنسيق؟ لست وحدك. في العديد من خطوط تقارير البيانات، تكون العقبة هي نقل المخططات والجداول من مصنف Excel إلى مجموعة شرائح أنيقة. الخبر السار؟ ببضع أسطر من C# يمكنك **تحويل Excel إلى PowerPoint**، إنشاء ملف PPTX قابل للتحرير بالكامل، وحتى الحفاظ على دقة المخطط.

في هذا الدرس سنستعرض كيفية تحميل مصنف Excel في C#، تحويل محتواه إلى عرض PowerPoint، وحفظ النتيجة. في النهاية ستتمكن من **إنشاء PowerPoint من Excel** تلقائيًا—بدون الحاجة إلى النسخ واللصق اليدوي. لا تحتاج إلى واجهات مستخدم معقدة، فقط كود نظيف.

> **ما ستحتاجه**  
> * .NET 6+ (أو .NET Framework 4.7.2+)  
> * حزم NuGet الخاصة بـ Aspose.Cells و Aspose.Slides (تقوم بالعمل الشاق)  
> * ملف Excel تجريبي يحتوي على مخطط واحد على الأقل (سنسميه `chartOle.xlsx`)  

![Diagram showing how to export Excel to PowerPoint using C#](https://example.com/images/export-excel-to-pptx.png "How to Export Excel to PowerPoint diagram")

## كيفية تصدير Excel إلى PowerPoint باستخدام C# – نظرة عامة

قبل أن نبدأ بالبرمجة، من المفيد فهم تدفق العملية المكوّن من ثلاث خطوات:

1. **Load Excel workbook** – نقرأ ملف `.xlsx` إلى الذاكرة.  
2. **Convert workbook to a PowerPoint presentation** – تقوم Aspose بتحويل كل ورقة عمل (أو المخطط المحدد) إلى شريحة.  
3. **Save the generated presentation** – يمكن فتح ملف PPTX النهائي في PowerPoint، تحريره، أو إرساله إلى أصحاب المصلحة.

كل خطوة معزولة عمدًا حتى تتمكن من استبدالها بمنطق مخصص لاحقًا (مثل اختيار أوراق معينة، تطبيق سمات الشرائح، إلخ). الآن لنفصل التفاصيل.

## الخطوة 1 – تحميل مصنف Excel بأسلوب C#

أول شيء يجب عليك القيام به هو جلب ملف Excel إلى تطبيقك. باستخدام Aspose.Cells يكون الكود بسيطًا:

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**لماذا هذا مهم:**  
`Workbook` يختصر كل المصنف، ويمنحك الوصول إلى أوراق العمل، الخلايا،—والأهم—المخططات المدمجة. إذا تخطيت فحص وجود الملف ستحصل على استثناء `FileNotFoundException` غير واضح لاحقًا، وهو ما قد يتحول إلى كابوس تصحيح في بيئة الإنتاج.

**نصيحة احترافية:** إذا كنت تحتاج فقط إلى ورقة معينة، يمكنك تمرير كائن `LoadOptions` لتقليل استهلاك الذاكرة:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

هذا التعديل الصغير يسرّع معالجة المصنفات الكبيرة بشكل ملحوظ.

## الخطوة 2 – تحويل Excel إلى PowerPoint (Export Excel Chart PowerPoint)

الآن يأتي السحر: تحويل المصنف إلى ملف PPTX. توفر Aspose.Slides طريقة واحدة تقوم بالعمل الشاق:

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**ما الذي يحدث خلف الكواليس؟**  
`SaveToPresentation` يتنقل عبر كل ورقة عمل، يستخرج أي كائنات مخطط، ويخلق شريحة لكل مخطط. الطريقة تحافظ على تنسيق المخطط الأصلي، لذا تبقى الألوان، الخطوط، وعناوين البيانات كما هي. إذا كان المصنف يحتوي على جداول عادية، فستُعرض كصناديق نصية على الشريحة.

**حالة حافة – مخططات متعددة:**  
إذا كانت ورقة العمل تحتوي على أكثر من مخطط واحد، تقوم Aspose بترتيبها عموديًا على نفس الشريحة. لتضع كل مخطط على شريحة منفصلة يمكنك تكرار المخططات يدويًا:

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

هذا المقتطف يمنحك تحكمًا دقيقًا—مثالي لإنشاء عرض متقن.

## الخطوة 3 – حفظ العرض المُولَّد (Create PowerPoint from Excel)

الخطوة الأخيرة هي حفظ ملف PPTX على القرص. الأمر بسيط كما يلي:

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**لماذا يجب عليك التحقق من النتيجة:**  
بعد الحفظ، افتح `editable.pptx` في PowerPoint. يجب أن ترى شريحة واحدة لكل مخطط، كلُّها قابلة للتحرير بالكامل (يمكنك تغيير الألوان، نقل الكائنات، إلخ). إذا ظهر مخطط غير صحيح، تحقق من أن المخطط الأصلي في Excel يستخدم خطوطًا قياسية—بعض الخطوط المخصصة قد لا تُضمّن بشكل صحيح.

**مشكلة شائعة:**  
حفظ الملف على مشاركة شبكة دون أذونات مناسبة يسبب استثناء `UnauthorizedAccessException`. تأكد من أن الحساب الذي يشغل البرنامج يملك صلاحية كتابة إلى `YOUR_DIRECTORY`.

## مثال كامل يعمل – جميع الخطوات معًا

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في مشروع تطبيق Console جديد، استعد حزم NuGet، واضغط **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**الناتج المتوقع (في وحدة التحكم):**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

افتح `editable.pptx` وسترى شريحة لكل مخطط، جاهزة لمزيد من التعديل.

## الأسئلة المتكررة (FAQs)

**س: هل يمكنني تصدير ورقة عمل واحدة فقط بدلاً من المصنف بالكامل؟**  
ج: نعم. استخدم `Workbook.Worksheets["Sheet1"]` لعزل ورقة معينة، ثم استدعِ `SaveToPresentation` على تلك الورقة فقط.

**س: ماذا عن الحفاظ على الماكرو؟**  
ج: لا يتم نقل الماكرو إلى PowerPoint—فقط الكائنات البصرية (المخططات، الجداول) تُصدّر. إذا كنت بحاجة إلى وظائف الماكرو، ففكر في إنشاء الشرائح أولاً، ثم إضافة VBA يدويًا.

**س: هل يعمل هذا مع ملفات `.xls`؟**  
ج: بالتأكيد. تدعم Aspose.Cells الصيغ القديمة؛ فقط غيّر امتداد الملف في `excelPath`.

**س: كيف أغيّر حجم الشريحة إلى وضعية الشاشة العريضة (16:9)؟**  
ج: بعد إنشاء كائن `Presentation`، عيّن:

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**س: هل هناك بديل مجاني؟**  
ج: المكتبات المفتوحة المصدر مثل EPPlus يمكنها قراءة Excel، لكنها لا توفر تحويلًا مباشرًا من Excel إلى PowerPoint. سيتوجب عليك تحويل المخططات إلى صور وإدراجها يدويًا، مما يتطلب كودًا أكثر بكثير.

## نصائح وأفضل الممارسات

- **Batch processing:** إذا كان لديك عشرات المصنفات، غلف عملية التحويل داخل حلقة `Parallel.ForEach`—لكن احرص على التعامل مع كائنات Aspose غير الآمنة للمتعدد الخيوط.  
- **Memory management:** استدعِ `presentation.Dispose()` و `workbook.Dispose()` عند التعامل مع ملفات كبيرة لتحرير الموارد الأصلية بسرعة.  
- **Styling slides:** بعد التحويل، يمكنك تطبيق سمة شريحة رئيسية باستخدام `presentation.SlideMaster` لتمنح جميع الشرائح مظهرًا موحدًا.  
- **Testing:** أتمت اختبار وحدة بسيط يقوم بتحميل مصنف معروف، تشغيل التحويل، والتحقق من أن ملف PPTX الناتج يحتوي على عدد الشرائح المتوقع.

## الخلاصة

لقد أظهرنا لك **كيفية تصدير بيانات Excel** إلى مجموعة شرائح PowerPoint باستخدام C#. من خلال تحميل المصنف، تحويله باستخدام Aspose، وحفظ ملف PPTX، أصبح لديك طريقة قابلة للتكرار وبرمجية لـ **تحويل Excel إلى PowerPoint**، **إنشاء PowerPoint من Excel**، و**تحميل مصنف Excel بأسلوب C#** دون جهد يدوي. الكود مستقل، يعمل مع أي بيئة .NET حديثة، ويمكن توسيعه ليتناسب مع خطوط تقارير معقدة.

هل أنت مستعد للتحدي التالي؟ جرّب دمج عدة مخططات في شريحة واحدة، تطبيق تخطيطات شرائح مخصصة، أو حتى إنشاء ملاحظات المتحدث تلقائيًا. السماء هي الحد عندما تجمع بين أتمتة Excel وإنشاء PowerPoint.

هل لديك أسئلة أو حالة استخدام مميزة؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## ما الذي ينبغي أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells لـ .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [كيفية تصدير Excel إلى HTML مع خطوط الشبكة باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}