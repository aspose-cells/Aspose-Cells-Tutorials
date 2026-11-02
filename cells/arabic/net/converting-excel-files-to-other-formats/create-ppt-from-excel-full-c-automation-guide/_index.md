---
category: general
date: 2026-03-18
description: أنشئ عرض PowerPoint من Excel باستخدام C# بسرعة. تعلّم كيفية تحويل Excel
  إلى PPT، وأتمتة Excel إلى PPT، وتعامل مع تحويل ملفات xls إلى pptx في دقائق.
draft: false
keywords:
- create ppt from excel
- convert excel to ppt
- excel to ppt conversion
- convert xls to pptx
- automate excel to ppt
language: ar
og_description: إنشاء عرض PPT من Excel باستخدام C# بسرعة. اتبع هذا الدليل خطوة بخطوة
  لتحويل Excel إلى PPT، وأتمتة Excel إلى PPT، وإدارة تحويل xls إلى pptx.
og_title: إنشاء PPT من Excel – دليل كامل لأتمتة C#
tags:
- C#
- Aspose
- Presentation Automation
title: إنشاء عرض PPT من Excel – دليل كامل لأتمتة C#
url: /ar/net/converting-excel-files-to-other-formats/create-ppt-from-excel-full-c-automation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PPT من Excel – دليل الأتمتة الكامل بلغة C#

هل تساءلت يومًا كيف **إنشاء PPT من Excel** دون فتح PowerPoint يدويًا؟ لست وحدك. يحتاج العديد من المطورين إلى تحويل جداول البيانات إلى عروض شرائح بسرعة، سواء لتقارير أسبوعية، أو لوحات معلومات المبيعات، أو النشرات البريدية الآلية. الخبر السار؟ ببضع أسطر من C# يمكنك **تحويل Excel إلى PPT**، وحتى **أتمتة Excel إلى PPT** كجزء من سير عمل أكبر.

في هذا الدليل سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يقوم بتحميل دفتر عمل `.xls`، وتحويله إلى ملف `.pptx`، وحفظ النتيجة. سنناقش أيضًا لماذا كل خطوة مهمة، وما هي الفخاخ التي يجب الانتباه إليها، وكيف يمكنك توسيع الحل لتغطية كامل نطاق **تحويل Excel إلى PPT**.

## ما ستحتاجه

قبل أن نبدأ، تأكد من تثبيت المتطلبات المسبقة التالية على جهازك:

| المتطلب | السبب |
|--------------|--------|
| **.NET 6+ SDK** | ميزات لغة حديثة وأداء أفضل. |
| **Aspose.Cells for .NET** | توفر الفئة `Workbook` المستخدمة لقراءة ملفات Excel. |
| **Aspose.Slides for .NET** | تمكن الفئة `Presentation` من إنشاء ملفات PowerPoint. |
| **Visual Studio 2022** (or any IDE you prefer) | يسهل عملية تصحيح الأخطاء وإدارة حزم NuGet دون عناء. |

يمكنك جلب مكتبات Aspose من NuGet باستخدام:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

> **نصيحة احترافية:** إذا كنت تستخدم خط أنابيب CI/CD، قم بتثبيت الإصدارات في ملف `csproj` لتجنب التغييرات المكسرة غير المتوقعة.

## نظرة عامة على العملية

على مستوى عالٍ، **إنشاء PPT من Excel** يتبع ثلاث خطوات بسيطة:

1. تحميل دفتر عمل Excel الذي يحتوي على الأشكال أو الجداول أو المخططات التي تريد إعادة استخدامها.
2. استدعاء روتين التحويل المدمج الذي يحول دفتر العمل إلى عرض تقديمي PowerPoint.
3. حفظ العرض التقديمي المُولد على القرص، جاهز للفتح أو الإرسال عبر البريد الإلكتروني.

فيما يلي سنفصل كل خطوة، نشرح الآليات الأساسية، ونظهر لك الشيفرة الدقيقة التي تحتاجها.

![مخطط إنشاء PPT من Excel](https://example.com/create-ppt-from-excel.png "سير عمل إنشاء PPT من Excel")

*نص بديل للصورة: مخطط يوضح كيفية إنشاء PPT من Excel باستخدام C# ومكتبات Aspose.*

## الخطوة 1: تحميل دفتر عمل Excel الذي يحتوي على الأشكال

أول شيء عليك فعله هو إخبار Aspose.Cells بمكان ملف المصدر. يقبل مُنشئ `Workbook` مسارًا إلى ملف `.xls` أو `.xlsx` ويقوم بتحليله إلى نموذج كائنات في الذاكرة.

```csharp
using Aspose.Cells;
using Aspose.Slides;
using System;

namespace ExcelToPptDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Load the Excel workbook containing shapes
            string inputPath = @"YOUR_DIRECTORY/input.xls";
            Workbook workbook = new Workbook(inputPath);
```

**لماذا هذا مهم:**  
تحميل دفتر العمل هو أكثر من مجرد قراءة ملف. تقوم Aspose.Cells بإنشاء رسم بياني كامل للكائنات يتضمن أوراق العمل، الخلايا، المخططات، وحتى الأشكال المدمجة. إذا تخطيت هذه الخطوة، فإن **تحويل Excel إلى PPT** لاحقًا لن يكون لديه أي بيانات مصدر للعمل معها.

### حالات الحافة الشائعة

- **File not found** – لفّ المُنشئ داخل `try/catch` وعرض خطأ واضح.
- **Password‑protected files** – استخدم `LoadOptions` لتزويد كلمة المرور.
- **Large workbooks** – فكّر في ضبط `LoadOptions.MemorySetting = MemorySetting.MemoryPreferTempFile` لتجنب استثناءات نفاد الذاكرة.

## الخطوة 2: تحويل دفتر العمل إلى عرض تقديمي PowerPoint

تأتي Aspose.Slides مع طريقة توسيع مفيدة `SaveAsPresentation()` التي تقوم بالعمل الشاق نيابةً عنك. في الخلفية، تقوم بالتكرار على كل ورقة عمل، استخراج المخططات والأشكال، وربطها بكائنات الشرائح.

```csharp
            // 👉 Step 2: Convert the workbook to a PowerPoint presentation (default PPTX format)
            Presentation presentation = workbook.SaveAsPresentation();
```

**لماذا هذا مهم:**  
هذا السطر هو جوهر عملية **تحويل Excel إلى PPT**. تتعامل المكتبة مع قرارات التخطيط (مثل ورقة عمل واحدة لكل شريحة) وتحافظ على الدقة البصرية، لذا لا تحتاج إلى إعادة إنشاء المخططات يدويًا في PowerPoint.

### تعديل التحويل (اختياري)

إذا كنت بحاجة إلى مزيد من التحكم — على سبيل المثال تريد أوراقًا محددة فقط أو تريد تغيير حجم الشريحة — يمكنك استخدام النسخة التي تقبل `PresentationOptions`:

```csharp
            var options = new PresentationOptions
            {
                SlidesLayout = SlidesLayout.OneSlidePerWorksheet,
                SlideSize = new SizeF(960, 540) // 16:9 widescreen
            };
            Presentation customPresentation = workbook.SaveAsPresentation(options);
```

## الخطوة 3: حفظ العرض التقديمي المُولد إلى ملف

بمجرد أن يصبح كائن `Presentation` جاهزًا، يصبح حفظه أمرًا بسيطًا. تقوم طريقة `Save` بكتابة ملف PPTX الثنائي إلى القرص.

```csharp
            // 👉 Step 3: Save the generated presentation to a file
            string outputPath = @"YOUR_DIRECTORY/output.pptx";
            presentation.Save(outputPath, SaveFormat.Pptx);

            Console.WriteLine($"✅ Success! PPT created at {outputPath}");
        }
    }
}
```

**لماذا هذا مهم:**  
حفظ الملف يُكمل **تحويل Excel إلى PPT** ويجعله متاحًا للعمليات اللاحقة — مرفقات البريد الإلكتروني، تحميلات SharePoint، أو تخصيصات إضافية للشرائح.

### التحقق من النتيجة

بعد تشغيل البرنامج، افتح `output.pptx` في PowerPoint. يجب أن ترى شريحة واحدة لكل ورقة عمل، مع المخططات والأشكال المعروضة تمامًا كما ظهرت في Excel. إذا كان هناك شيء غير صحيح، تحقق مرة أخرى من أن دفتر العمل المصدر يحتوي فعليًا على العناصر البصرية التي تتوقعها.

## مثال كامل يعمل (جميع الخطوات معًا)

فيما يلي الشيفرة الكاملة الجاهزة للنسخ واللصق والتي يمكنك تشغيلها فورًا بعد تثبيت حزم NuGet.

```csharp
// Full example: create PPT from Excel in C#
using Aspose.Cells;
using Aspose.Slides;
using System;

namespace ExcelToPptDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Load the Excel workbook containing shapes
            string inputPath = @"YOUR_DIRECTORY/input.xls";
            Workbook workbook;
            try
            {
                workbook = new Workbook(inputPath);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to load workbook: {ex.Message}");
                return;
            }

            // 👉 Step 2: Convert the workbook to a PowerPoint presentation (default PPTX format)
            Presentation presentation;
            try
            {
                presentation = workbook.SaveAsPresentation();
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Conversion error: {ex.Message}");
                return;
            }

            // 👉 Step 3: Save the generated presentation to a file
            string outputPath = @"YOUR_DIRECTORY/output.pptx";
            try
            {
                presentation.Save(outputPath, SaveFormat.Pptx);
                Console.WriteLine($"✅ Success! PPT created at {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to save PPT: {ex.Message}");
            }
        }
    }
}
```

شغّل البرنامج (`dotnet run`) وشاهد وحدة التحكم تؤكد إنشاء `output.pptx`. هذا كل شيء — لقد **أتمتت Excel إلى PPT** بأقل من 30 سطرًا من الشيفرة.

## توسيع الحل: سيناريوهات واقعية

الآن بعد أن عرفت كيفية **إنشاء PPT من Excel**، قد تتساءل كيف تعدله لخطوط أنابيب أكثر تعقيدًا.

### 1. تحويل XLS إلى PPTX بالجملة

إذا كان لديك مجلد مليء بملفات `.xls` القديمة، قم بالتكرار عليها وتطبيق نفس منطق التحويل:

```csharp
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY", "*.xls"))
{
    Workbook wb = new Workbook(file);
    Presentation ppt = wb.SaveAsPresentation();
    string outFile = Path.ChangeExtension(file, ".pptx");
    ppt.Save(outFile, SaveFormat.Pptx);
}
```

يُعالج هذا المقتطف حالة الاستخدام **تحويل xls إلى pptx** بأقل جهد.

### 2. إضافة شريحة عنوان مخصصة

أحيانًا تحتاج إلى شريحة تمهيدية لا تستند إلى Excel. يمكنك إضافة شريحة في البداية قبل الحفظ:

```csharp
Slide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.AddAutoShape(ShapeType.Rectangle, 50, 50, 860, 120)
          .TextFrame.Text = "Quarterly Sales Report";
```

الآن يبدأ العرض النهائي بشريحة عنوان مصقولة، تليها المحتويات المُولدة تلقائيًا.

### 3. تضمين شعار على كل شريحة

متطلب شائع للعلامة التجارية هو وضع شعار على كل شريحة. استخدم مجموعة `Slide` للتكرار وإضافة صورة:

```csharp
foreach (var slide in presentation.Slides)
{
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 850, 500, 80, 80, "logo.png");
}
```

### 4. معالجة الملفات الكبيرة بكفاءة

عند التعامل مع دفاتر عمل أكبر من 100 ميغابايت، فعّل البث:

```csharp
var loadOptions = new LoadOptions { MemorySetting = MemorySetting.MemoryPreferTempFile };
Workbook largeWb = new Workbook(inputPath, loadOptions);
Presentation largePpt = largeWb.SaveAsPresentation();
largePpt.Save(outputPath, SaveFormat.Pptx);
```

هذه التعديلات تجعل **تحويل Excel إلى PPT** قويًا بما يكفي لبيئات الإنتاج.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات `.xlsx`؟**  
ج: بالتأكيد. يقبل نفس مُنشئ `Workbook` كلًا من ملفات `.xls` القديمة و `.xlsx` الحديثة. لا حاجة لتغيير الشيفرة.

**س: ماذا لو كان دفتر العمل يحتوي على ماكرو؟**  
ج: تقوم Aspose.Cells بقراءة البيانات والمخططات الظاهرة ولكنها تتجاهل ماكرو VBA. إذا كنت بحاجة إلى الحفاظ على الماكرو، سيتعين عليك التعامل معه بشكل منفصل.

**س: هل يمكنني استهداف PowerPoint 97‑2003 (`.ppt`) بدلاً من `.pptx`؟**  
ج: نعم — فقط غيّر قيمة تعداد `SaveFormat`: `presentation.Save(output

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}