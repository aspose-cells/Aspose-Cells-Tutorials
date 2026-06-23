---
category: general
date: 2026-03-30
description: أنشئ عرض PowerPoint من Excel بسرعة باستخدام Aspose.Cells و Aspose.Slides.
  تعلّم كيفية تصدير ورقة العمل كصورة وحفظ العرض التقديمي كملف PPTX باستخدام C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: ar
og_description: إنشاء عرض PowerPoint من Excel باستخدام C# و Aspose. تصدير ورقة العمل
  كصورة، مع الحفاظ على الأشكال قابلة للتحرير، وحفظ النتيجة كملف PPTX.
og_title: إنشاء عرض PowerPoint من Excel – دليل C# الكامل
tags:
- Aspose
- C#
- Office Automation
title: إنشاء PowerPoint من Excel – دليل C# خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PowerPoint من Excel – دليل C# كامل

هل احتجت يوماً إلى **إنشاء PowerPoint من Excel** لكن لم تكن متأكدًا أي مكتبة يمكنها الحفاظ على قابلية تحرير المخططات؟ لست وحدك. في العديد من سيناريوهات التقارير تريد تحويل جدول بيانات إلى مجموعة شرائح دون فقدان القدرة على تعديل مربعات النص لاحقًا. يوضح لك هذا الدليل بالضبط كيفية **تحويل Excel إلى PowerPoint** باستخدام Aspose.Cells و Aspose.Slides، بالإضافة إلى شرح كيفية **تصدير ورقة العمل كصورة** وأخيرًا **حفظ العرض التقديمي كملف PPTX**.

سنستعرض كل سطر من الشيفرة، نشرح *لماذا* كل إعداد مهم، ونناقش أيضًا ما يجب فعله إذا كان دفتر العمل يحتوي على مخططات معقدة تفضل تصديرها كصورة. في النهاية ستحصل على تطبيق C# Console جاهز للتشغيل يأخذ `ShapesDemo.xlsx` وينتج `Result.pptx` – كل ذلك مع مربعات نص قابلة للتحرير وصور واضحة.

## ما ستحتاجه

- .NET 6.0 أو أحدث (تعمل الواجهة البرمجية مع .NET Framework أيضًا، لكن .NET 6 هو الخيار المثالي).  
- **Aspose.Cells** و **Aspose.Slides** حزم NuGet (تعمل تراخيص التجربة المجانية للاختبار).  
- إلمام أساسي بصياغة C# – إذا كنت تستطيع كتابة `Console.WriteLine`، فأنت جاهز.  

لا تحتاج إلى COM interop إضافي، ولا إلى تثبيت Office على الخادم، ولا إلى نسخ‑لصق يدوي للصور. كل شيء يتم معالجته برمجيًا.

---

## إنشاء PowerPoint من Excel – تحميل دفتر العمل وتعيين خيارات التصدير

أول شيء نقوم به هو فتح ملف Excel وإخبار Aspose.Cells كيف نريد عرض الورقة. كائن `ImageOrPrintOptions` هو المكان الذي يحدث فيه السحر: نقوم بتمكين `ExportShapes` و `ExportEditableTextBoxes` بحيث تصبح أي أشكال (بما في ذلك المخططات) جزءًا من الشريحة **و** تظل قابلة للتحرير بعد التحويل.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**لماذا هذه العلامات؟**  
- `OnePagePerSheet` يمنع تقسيم الورقة عبر عدة شرائح – ستحصل على صورة واحدة بحجم كامل.  
- `ExportShapes` يخبر Aspose.Cells ب rasterize المخططات *و* الأشكال المتجهية، مع الحفاظ على مظهرها.  
- `ExportEditableTextBoxes` هو السر الذي يتيح لك النقر المزدوج على مربع نص في PowerPoint وتعديل النص دون الحاجة لفتح Excel مرة أخرى.

> **نصيحة احترافية:** إذا كنت بحاجة فقط إلى صورة ثابتة لمخطط، اضبط `ExportShapes = false` واستخدم طريقة `ExportExcelChartAsPicture` لاحقًا (انظر القسم النهائي).

---

## تحويل Excel إلى PowerPoint – إنشاء صورة من ورقة العمل

مع إعداد الخيارات، نقوم الآن بتحويل ورقة العمل إلى `System.Drawing.Image`. يقوم `WorksheetToImageConverter` بالعمل الشاق، مطبقًا الإعدادات التي عرفناها للتو.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

المعامل `0` يشير إلى الصفحة الأولى (لدينا صفحة واحدة فقط بسبب `OnePagePerSheet`). الصورة الناتجة `sheetImage` تحتفظ بدقة DPI الأصلية، لذا لن تبدو شريحتك متقطعة حتى على الشاشات عالية الدقة.

---

## حفظ العرض التقديمي كـ PPTX – إدراج الصورة في شريحة

الآن نقوم بإنشاء ملف PowerPoint جديد، نضيف شريحة، ونضع الصورة النقطية (bitmap) عليها. يتعامل Aspose.Slides مع الصورة ككائن *إطار صورة* (picture frame)، يمكنك لاحقًا تغيير حجمه أو تحريكه مثل أي كائن PowerPoint أصلي.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **ماذا لو كانت الصورة أكبر من حجم الشريحة؟**  
> سيقوم PowerPoint تلقائيًا بقطع أي شيء يتجاوز أبعاد الشريحة. حل سريع هو تعديل حجم الصورة قبل إدراجها:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

يمكنك بعد ذلك تمرير `newWidth` و `newHeight` إلى `AddPictureFrame`.

---

## تصدير ورقة العمل كصورة – حفظ ملف PPTX

أخيرًا نقوم بحفظ العرض التقديمي على القرص. علم `SaveFormat.Pptx` يضمن تنسيق OpenXML الحديث، والذي يعمل عبر جميع إصدارات PowerPoint الحديثة.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

عند فتح `Result.pptx` سترى شريحة واحدة تبدو تمامًا مثل ورقة Excel الخاصة بك، لكن لا يزال بإمكانك النقر على أي مربع نص وتعديل محتواه مباشرة في PowerPoint.

---

## تصدير مخطط Excel كصورة – عندما تُفضَّل الصور النقطية

أحيانًا لا تحتاج إلى أشكال قابلة للتحرير؛ صورة PNG عالية الجودة لمخطط تكفي. يمكن لـ Aspose.Cells تصدير مخطط محدد إلى صورة دون تحويل الورقة بأكملها:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

يمكنك بعد ذلك تضمين `chart.png` في شريحة بنفس الطريقة التي أضفنا بها `sheetImage`. يقلل هذا النهج من حجم ملف PPTX ويكون مفيدًا عندما لا تكون البيانات المحيطة مطلوبة على الشريحة.

---

## المشكلات الشائعة وكيفية تجنّبها

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **النص يبدو غير واضح** | تم التصدير بدقة DPI منخفضة (الافتراضية 96). | اضبط `imageOptions.Dpi = 300;` قبل التحويل. |
| **الأشكال تختفي** | `ExportShapes` تركت `false`. | تأكد من أن `ExportShapes = true` عندما تحتاج إلى رسومات قابلة للتحرير. |
| **عدم توافق حجم الشريحة** | الصورة أكبر من أبعاد الشريحة. | قم بتغيير حجم الصورة (انظر مقتطف الشيفرة) أو غيّر حجم الشريحة عبر `presentation.SlideSize`. |
| **استثناء الترخيص** | استخدام نسخة تجريبية دون تفعيل صحيح. | استدعِ `License license = new License(); license.SetLicense("Aspose.Total.lic");` مبكرًا في `Main`. |

---

## مثال كامل يعمل (جاهز للنسخ‑اللصق)

فيما يلي البرنامج بالكامل، جاهز للإدراج في مشروع Console جديد. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف Excel الخاص بك.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**المخرجات المتوقعة:**  
تشغيل البرنامج يطبع `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. فتح ملف PPTX يظهر شريحة واحدة تعكس ورقة Excel الأصلية، مع مربعات نص قابلة للتحرير.

---

## ملخص وخطوات مستقبلية

أنت الآن تعرف كيف **إنشاء PowerPoint من Excel** باستخدام واجهات برمجة التطبيقات القوية من Aspose، وكيف **تصدير ورقة العمل كصورة**، وكيف **حفظ العرض التقديمي كـ PPTX** مع الحفاظ على إمكانية التحرير. نفس النمط يعمل مع دفاتر عمل متعددة الأوراق—فقط قم بالتكرار عبر `workbook.Worksheets` وأضف شريحة جديدة لكل واحدة.

- **تحويل دفعة:** التكرار عبر مجلد من ملفات Excel وإنشاء مجموعة شرائح لكل ملف.  
- **تخطيطات ديناميكية:** استخدم `slide.LayoutSlide` لتطبيق قوالب PowerPoint المصممة مسبقًا.  
- **تصدير المخطط فقط:** دمج مقتطف “Export Excel chart as picture” مع نواقل الشرائح للحصول على مجموعة شرائح أصغر.  
- **تنسيق متقدم:** تطبيق خلفيات شرائح مخصصة، انتقالات، أو رسوم متحركة عبر Aspose.Slides.

لا تتردد في التجربة—غيّر DPI، استبدل `ShapeType.Ellipse` بإطار صورة دائري، أو حتى قم بتضمين صور متعددة في شريحة واحدة. السماء هي الحد عندما تكون لديك سيطرة برمجية على

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}