---
category: general
date: 2026-02-21
description: أنشئ PowerPoint من Excel بسرعة. تعلّم كيفية تصدير Excel إلى PowerPoint
  بنصوص ومخططات قابلة للتحرير باستخدام Aspose.Cells في بضع أسطر فقط من C#.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: ar
og_description: إنشاء عرض PowerPoint من Excel مع نصوص ومخططات قابلة للتحرير. اتبع
  هذا الدليل التفصيلي لتصدير Excel إلى PowerPoint باستخدام Aspose.Cells.
og_title: إنشاء PowerPoint من Excel – دليل C# خطوة بخطوة
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: إنشاء PowerPoint من Excel – الدليل الكامل لـ C#
url: /ar/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

ptx.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PowerPoint من Excel – دليل C# كامل

هل احتجت يوماً إلى **create PowerPoint from Excel** لكن لم تكن متأكدًا أي API تستخدم؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يرغبون في تحويل ورقة عمل غنية بالبيانات إلى مجموعة شرائح مصقولة، خاصةً عندما يحتاجون إلى أن تظل مربعات النص قابلة للتحرير بعد التحويل.  

في هذا الدليل سنوضح لك كيفية **export Excel to PowerPoint** مع الحفاظ على النص القابل للتحرير، ودقة المخططات، والتخطيط—كل ذلك ببضع أسطر من C#. في النهاية ستحصل على ملف PPTX جاهز للاستخدام يمكنك تعديلّه في PowerPoint كما تفعل مع أي شريحة تم إنشاؤها يدويًا.

## ما ستتعلمه

- كيفية تحميل مصنف Excel يحتوي على مخططات وأشكال.  
- كيفية تكوين `PresentationExportOptions` بحيث تبقى مربعات النص قابلة للتحرير (`export editable text`).  
- كيفية **export Excel chart PowerPoint** والحصول على مجموعة شرائح نظيفة.  
- بعض الاختلافات الصغيرة التي يمكنك تطبيقها عندما تحتاج إلى **convert Excel chart PowerPoint** لإعدادات صفحات مختلفة أو أوراق عمل متعددة.  

### المتطلبات المسبقة

- بيئة تطوير .NET (Visual Studio 2022 أو أحدث).  
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو نسخة مرخصة).  
- ملف Excel (`ChartWithShape.xlsx`) يحتوي على مخطط واحد على الأقل وشكل تريد إبقائه قابلاً للتحرير.  

إذا كان لديك كل ذلك، فلنبدأ—بدون إطالة، مجرد حل عملي قابل للتنفيذ.

## إنشاء PowerPoint من Excel – خطوة بخطوة

أسفل كل خطوة سنضع مقتطف كود مختصر، نشرح **لماذا** نقوم به، ونشير إلى الأخطاء الشائعة. لا تتردد في نسخ‑لصق المثال الكامل في أسفل الصفحة.

### الخطوة 1: تحميل مصنف Excel

أولاً نحتاج إلى جلب المصنف المصدر إلى الذاكرة. Aspose.Cells يقرأ الملف ويُنشئ نموذج كائن غني يمكننا التلاعب به.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**لماذا هذا مهم:**  
تحميل المصنف هو الأساس. إذا كان مسار الملف غير صحيح أو كان المصنف تالفًا، ستفشل جميع خطوات `export excel to powerpoint` اللاحقة. فحص الصحة يعطيك ردًا مبكرًا بدلاً من رسالة “الملف غير موجود” غير واضحة لاحقًا.

### الخطوة 2: إعداد خيارات التصدير

Aspose.Cells يزودك بكائن `PresentationExportOptions` يتحكم في مظهر ملف PPTX. هنا تقرر ما إذا كنت تريد أن يبقى النص قابلاً للتحرير.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**لماذا هذا مهم:**  
بدون تكوين `PresentationExportOptions`، تستخدم المكتبة الإعدادات الافتراضية، والتي قد لا تتطابق مع قالب الشرائح الخاص بشركتك. تعديل حجم الشريحة مسبقًا يمنع الحاجة إلى تعديل يدوي لاحقًا.

### الخطوة 3: تمكين مربعات النص القابلة للتحرير

العلمية السحرية `ExportEditableTextBoxes` تخبر Aspose.Cells بالحفاظ على أي شكل نصي كمربعات نص PowerPoint، وليس كصور ثابتة.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**لماذا هذا مهم:**  
إذا تخطيت هذه السطر، سيحتوي PPTX الناتج على نص مُرصَّص—مما يعني أنك لا تستطيع تعديل التسمية أو الشرح في PowerPoint. ضبط `export editable text` هو المفتاح للحصول على مجموعة شرائح قابلة لإعادة الاستخدام فعليًا.

### الخطوة 4: تصدير ورقة العمل إلى PPTX

الآن نكتب فعليًا ملف PPTX. يمكنك اختيار أي ورقة عمل؛ هنا نستخدم الأولى (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**لماذا هذا مهم:**  
`SaveToPptx` يحترم إعدادات الصفحة (الهوامش، الاتجاه) التي حددتها في Excel، لذا تعكس الشريحة التخطيط الذي صممته مسبقًا. هذا هو جوهر **export excel chart powerpoint**.

### الخطوة 5: التحقق من النتيجة (اختياري لكن موصى به)

بعد التحويل، افتح ملف `Result.pptx` في PowerPoint وتحقق من:

1. ظهور المخططات بوضوح واحتفاظها بسلاسل البيانات.  
2. إمكانية اختيار وتحرير مربعات النص.  
3. تطابق حجم الشريحة مع توقعاتك.

إذا لاحظت أي شيء غير صحيح، راجع `exportOptions`—على سبيل المثال، قد تحتاج إلى ضبط `exportOptions.IncludePrintArea = true` للاعتراف بمنطقة الطباعة المسماة.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### الخطوة 6: تنويعات متقدمة (تصدير أوراق متعددة)

غالبًا ما تريد **convert excel chart powerpoint** لعدة أوراق عمل مرة واحدة. قم بالتكرار عبر المجموعة وأعط كل شريحة اسمًا فريدًا:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**نصيحة احترافية:** إذا كنت بحاجة إلى جميع الأوراق في *ملف PPTX واحد*، أنشئ كائن `Presentation` جديد، استورد كل شريحة، ثم احفظ مرة واحدة. هذا أكثر تعقيدًا قليلاً لكنه يوفر عليك التعامل مع ملفات متعددة.

## مثال كامل يعمل

إليك البرنامج بالكامل لتلصقه في تطبيق Console وتشغيله فورًا.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**النتيجة المتوقعة:**  
عند فتح `Result.pptx`، سترى شريحة تعكس تخطيط ورقة Excel. أي مخطط وضعته في Excel يظهر كمخطط PowerPoint أصلي، والشرح الذي أضفته كشكل يصبح الآن مربع نص قابل للتحرير بالكامل.

## أسئلة شائعة وحالات خاصة

- **هل يعمل مع المصنفات المُمكَّنة للماكرو (`.xlsm` )؟**  
  نعم. Aspose.Cells يقرأ الماكرو لكنه لا ينفذه. عملية التحويل تتجاهل VBA، لذا ستحصل على المحتوى المرئي فقط.

- **ماذا لو احتوت ورقة العمل على مخططات متعددة؟**  
  جميع المخططات الظاهرة تُنقل إلى الشريحة نفسها. إذا أردت كل مخطط في شريحة منفصلة، قسّم ورقة العمل أو استخدم الحلقة الموضحة في الخطوة 6.

- **هل يمكنني الحفاظ على سمات PowerPoint مخصصة؟**  
  ليس مباشرة أثناء التصدير. بعد التحويل يمكنك تطبيق سمة في PowerPoint أو برمجيًا عبر Aspose.Slides.

- **هل هناك طريقة لتصدير نطاق مختار فقط؟**  
  حدد منطقة طباعة مسماة في Excel (`Page Layout → Print Area`) وفعل `exportOptions.IncludePrintArea = true`.

## الخلاصة

أنت الآن تعرف كيف **create PowerPoint from Excel** باستخدام Aspose.Cells، مع تحكم كامل في النص القابل للتحرير، ودقة المخططات، وحجم الشرائح. المقتطف القصير الذي شاركناه يغطي السيناريو الأكثر شيوعًا، والنصائح الإضافية تمنحك مرونة عندما تحتاج إلى **export excel to powerpoint** لعدة أوراق أو تخطيطات مخصصة.  

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذا النهج مع **Aspose.Slides** لإضافة انتقالات، ملاحظات المتحدث، أو حتى دمج الشرائح المُولدة في عرض تقديمي أكبر. أو جرب تحويل مصنف كامل إلى مجموعة شرائح متعددة—مثالي لأنابيب التقارير الآلية.

هل لديك أسئلة، أو اكتشفت تعديلًا ذكيًا؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}