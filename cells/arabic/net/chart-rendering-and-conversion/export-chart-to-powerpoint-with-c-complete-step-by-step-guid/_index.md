---
category: general
date: 2026-02-26
description: تصدير المخطط إلى PowerPoint من Excel باستخدام C#. تعلم كيفية تحويل Excel
  إلى PowerPoint، حفظ Excel كـ PowerPoint والحفاظ على قابلية تعديل الأشكال.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: ar
og_description: تصدير المخطط إلى PowerPoint من Excel باستخدام C#. يوضح هذا الدليل
  كيفية تحويل Excel إلى PowerPoint، حفظ المصنف كملف PPTX والحفاظ على إمكانية تعديل
  الأشكال.
og_title: تصدير المخطط إلى PowerPoint باستخدام C# – دليل برمجي كامل
tags:
- Aspose.Cells
- C#
- Office Automation
title: تصدير المخطط إلى PowerPoint باستخدام C# – دليل خطوة بخطوة كامل
url: /ar/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

code block placeholders remain.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى PowerPoint – دليل برمجي كامل

هل تساءلت يومًا كيف **تصدير المخطط إلى PowerPoint** دون فقدان قابلية التحرير؟ في العديد من سيناريوهات التقارير تحتاج إلى مخطط حي داخل مجموعة شرائح، ومع ذلك النسخ واللصق يدويًا أمر مؤلم. الخبر السار هو أنك يمكنك القيام بذلك برمجيًا ببضع أسطر من C#.

في هذا الدليل سنستعرض العملية بالكامل: من تحميل دفتر عمل Excel يحتوي على مخطط مع مربع نص، إلى تكوين عملية التصدير بحيث تبقى مربعات النص والأشكال قابلة للتحرير، وأخيرًا حفظ النتيجة كملف **PowerPoint**. في النهاية ستعرف أيضًا كيف **تحول Excel إلى PowerPoint**، **تحفظ Excel كـ PowerPoint**، وحتى تعديل الخيارات لحالات الحافة.

## ما ستحتاجه

- **Aspose.Cells for .NET** (الإصدار 23.10 أو أحدث). إنها المكتبة التي تجعل التحويل سهلًا.
- **.NET 6+** runtime – أي SDK حديث يعمل.
- ملف Excel بسيط (`ChartWithTextbox.xlsx`) يحتوي على مخطط واحد على الأقل ومربع نص.
- Visual Studio أو بيئة التطوير المتكاملة المفضلة لديك.

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells، لكن وجود فهم أساسي لصياغة C# سيساعد بالتأكيد.

## تصدير المخطط إلى PowerPoint – خطوة بخطوة

أدناه نقسم الحل إلى خطوات منفصلة وسهلة المتابعة. كل خطوة تتضمن الشيفرة الدقيقة التي تحتاجها، بالإضافة إلى فقرة قصيرة “لماذا” تشرح السبب وراء ذلك.

### الخطوة 1: تحميل دفتر عمل Excel الذي يحتوي على المخطط

أولًا نحتاج إلى جلب الملف المصدر إلى الذاكرة. استخدام `Workbook` من Aspose.Cells يقرأ كامل جدول البيانات، بما في ذلك المخططات، الصور، والكائنات المدمجة.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*لماذا هذا مهم:* إذا تم فتح دفتر العمل دون تحديد المسار بشكل صحيح، ستحصل على استثناء `FileNotFoundException`. فحص الصحة السريع يمنعك من تصدير شريحة فارغة لاحقًا.

### الخطوة 2: إعداد خيارات العرض للحفاظ على قابلية تحرير الأشكال

تتيح لك Aspose.Cells تحديد ما إذا كانت مربعات النص، الأشكال، وحتى المخطط نفسه ستبقى **قابلة للتحرير** بعد التصدير. ضبط `ExportTextBoxes` و `ExportShapes` إلى `true` يحافظ على تلك الكائنات كعناصر PowerPoint أصلية بدلاً من تحويلها إلى صورة ثابتة.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*لماذا هذا مهم:* إذا تركت هذه العلامات على قيمها الافتراضية (`false`)، ستحتوي الشريحة الناتجة على صورة bitmap للمخطط، مما يجعل من المستحيل تعديل السلاسل أو تغيير العنوان لاحقًا. تمكين الخيارين يمنحك مخطط PowerPoint حقيقي يتصرف تمامًا كما لو رسمته يدويًا.

### الخطوة 3: تحويل Excel إلى PowerPoint وحفظ الملف

الآن نستدعي طريقة `Save`، مع تمرير تعداد `SaveFormat.Pptx` والخيارات التي قمنا بتكوينها للتو. تتولى المكتبة مهمة ترجمة كائن مخطط Excel إلى شكل مخطط PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*لماذا هذا مهم:* استدعاء `Save` يقوم بكل الأعمال الثقيلة—ربط سلاسل Excel بسلاسل PowerPoint، الحفاظ على تنسيق المحاور، ونسخ أي مربعات نص مرتبطة. بعد تنفيذ هذا السطر، ستحصل على ملف `.pptx` قابل للتحرير بالكامل جاهز للفتح في Microsoft PowerPoint.

### التحقق من النتيجة

افتح `Result.pptx` في PowerPoint. يجب أن ترى شريحة تحتوي على:

- المخطط الأصلي، لا يزال مرتبطًا ببياناته (يمكنك النقر المزدوج لتحرير السلاسل).
- أي مربع نص كان في ورقة Excel، الآن كصندوق نص PowerPoint أصلي.
- تخطيط الشريحة يتم اختياره تلقائيًا (عادةً شريحة فارغة).

إذا لاحظت أي عناصر مفقودة، تحقق مرة أخرى من أن دفتر العمل المصدر يحتوي فعليًا على كائنات مرئية وأن `ExportTextBoxes` / `ExportShapes` تم ضبطهما على `true`.

### تحويل Excel إلى PowerPoint: معالجة أوراق العمل المتعددة

غالبًا ما يحتوي دفتر العمل على أكثر من ورقة، كل واحدة منها تحمل مخططًا خاصًا بها. بشكل افتراضي، سيقوم Aspose.Cells بتصدير **جميع** المخططات من **جميع** الأوراق إلى شرائح منفصلة. إذا كنت تحتاج فقط إلى مجموعة فرعية، يمكنك تصفية المخططات قبل الحفظ:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*نصيحة احترافية:* ضبط `chart.IsVisible = false` أرخص من إزالة المخطط بالكامل، ويسمح لك بتبديل الإدراج دون تعديل الملف المصدر.

### حفظ Excel كـ PowerPoint – تخصيص حجم الشريحة

يستخدم PowerPoint حجم شريحة افتراضي 10 بوصة × 5.63 بوصة. إذا كان المخطط يبدو مكتظًا، يمكنك تغيير أبعاد الشريحة عبر كائن `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

الآن سيحصل المخطط المصدر على مساحة أكبر للتنفس، وستحتفظ أي مربعات نص بتخطيطها الأصلي.

### كيفية تحويل Excel إلى PPT: التعامل مع الكائنات المخفية

قد تتسلل الصفوف أو الأعمدة أو الأشكال المخفية إلى عملية التصدير. لإزالتها، قم بإجراء تنظيف سريع قبل الحفظ:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

هذه الخطوة ليست دائمًا ضرورية، لكنها تمنع الفجوات غير المتوقعة في مجموعة الشرائح النهائية.

### حفظ دفتر العمل كـ PPTX – مثال عملي كامل

بجمع كل ما سبق، إليك برنامج وحدة تحكم جاهز للتنفيذ يوضح التدفق الكامل:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

تشغيل هذا البرنامج سيُنشئ `Result.pptx` مع مخطط ومربع نص قابلين للتحرير، تمامًا ما تتوقعه عندما **تحفظ دفتر العمل كـ pptx** يدويًا.

![مثال على تصدير المخطط إلى PowerPoint](/images/export-chart-to-powerpoint.png "تصدير المخطط إلى PowerPoint – شريحة قابلة للتحرير")

## أسئلة شائعة وحالات خاصة

**ماذا لو كان ملف Excel يحتوي على مخطط مرتبط بمصدر بيانات خارجي؟**  
يقوم Aspose.Cells بنسخ القيم *الحالية* للبيانات إلى مخطط PowerPoint. لا يحافظ على الرابط الخارجي، لأن PowerPoint لا يمكنه الإشارة إلى اتصال بيانات Excel بنفس الطريقة. إذا كنت تحتاج إلى تحديثات حية، فكر في تضمين ملف Excel الأصلي داخل PPTX ككائن OLE بدلاً من ذلك.

**هل يمكنني تصدير مخطط يستخدم سمة مخصصة؟**  
نعم. تحاول المكتبة مطابقة ألوان سمة Excel مع فتحات سمة PowerPoint. بالنسبة للأنماط المخصصة جدًا قد تحتاج إلى تعديل الألوان بعد التصدير باستخدام API الخاص بـ PowerPoint (مثل Aspose.Slides).

**هل هناك حد لعدد المخططات؟**  
عمليًا لا يوجد حد—Aspose.Cells يبث البيانات، لذا حتى دفتر عمل يحتوي على عشرات المخططات سيُصدّر، رغم أن حجم ملف PPTX الناتج سيزداد بصورة خطية.

**هل أحتاج إلى ترخيص لـ Aspose.Cells؟**  
التقييم المجاني يعمل، لكنه يضيف علامة مائية على الشريحة الأولى. للاستخدام الإنتاجي، احصل على ترخيص مناسب لإزالة العلامة المائية وإطلاق الأداء الكامل.

## ملخص

غطّينا كيفية **تصدير المخطط إلى PowerPoint** باستخدام C#، وعرضنا الشيفرة الدقيقة لتحميل دفتر عمل Excel، وتكوين `PresentationOptions` للحفاظ على مربعات النص والأشكال قابلة للتحرير، وأخيرًا حفظ النتيجة كملف `.pptx`. كما تعلمت كيف **تحول Excel إلى PowerPoint**، **تحفظ Excel كـ PowerPoint**، وأجبت على سؤال “**كيفية تحويل Excel إلى ppt**” بمثال كامل قابل للتنفيذ.

## ما التالي؟

- **احفظ دفتر العمل كـ PPTX** مع شرائح متعددة: كرّر عبر كل ورقة عمل واستدعِ `Save` مع `PresentationOptions` لكل منها.
- استكشف **Aspose.Slides** إذا كنت بحاجة إلى تعديل PPTX المُنشأ برمجيًا (إضافة انتقالات، ملاحظات المتحدث، إلخ).
- جرّب تصدير **مخططات المحور** أو **المخططات ثلاثية الأبعاد**—تنطبق نفس الخيارات، لكن قد تحتاج إلى تعديل تنسيق المحاور بعد ذلك.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع الوثائق الرسمية لـ Aspose.Cells لأحدث تغييرات API. برمجة سعيدة، واستمتع بتحويل تلك المخططات من Excel إلى عروض PowerPoint مصقولة ببضع أسطر من C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}