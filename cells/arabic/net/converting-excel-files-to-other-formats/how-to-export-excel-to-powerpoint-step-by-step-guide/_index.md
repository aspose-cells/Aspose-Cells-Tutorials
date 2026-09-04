---
category: general
date: 2026-02-21
description: تعلم كيفية تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير. حوّل Excel
  إلى PowerPoint وأنشئ عروض PowerPoint من Excel ببضع أسطر فقط من C#.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- save excel as powerpoint
- how to export charts
language: ar
og_description: كيفية تصدير إكسل إلى باوربوينت مع مخططات قابلة للتحرير. اتبع هذا الدليل
  لتحويل إكسل إلى باوربوينت، وإنشاء باوربوينت من إكسل، وحفظ إكسل كملف باوربوينت بسهولة.
og_title: كيفية تصدير إكسل إلى باوربوينت – دليل كامل
tags:
- C#
- Aspose.Cells
- PowerPoint
title: كيفية تصدير إكسل إلى باوربوينت – دليل خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PowerPoint – دليل كامل

هل تساءلت يومًا **كيف تصدر Excel** إلى PowerPoint دون تحويل المخططات الجميلة إلى صور ثابتة؟ لست وحدك. في العديد من خطوط تقارير البيانات تظهر الحاجة إلى **تحويل Excel إلى PowerPoint** يوميًا، والحيل التقليدية للنسخ‑اللصق إما تكسر التخطيط أو تقفل بيانات المخطط.  

في هذا الدليل سنستعرض حلًا برمجيًا نظيفًا **ينشئ PowerPoint من Excel** مع الحفاظ على قابلية تحرير المخططات. في النهاية ستتمكن من **حفظ Excel كـ PowerPoint** باستدعاء طريقة واحدة وستعرف بالضبط لماذا كل سطر مهم.

## ما ستتعلمه

- الشيفرة C# الدقيقة المطلوبة **لتصدير Excel** إلى ملف PPTX.  
- كيفية إبقاء المخططات قابلة للتحرير باستخدام `PresentationExportOptions`.  
- متى تفضّل هذا النهج على التصدير اليدوي أو المحولات الطرفية.  
- المتطلبات المسبقة، الأخطاء الشائعة، وبعض النصائح الاحترافية لجعل العملية محصنة.

> **نصيحة احترافية:** إذا كنت تستخدم Aspose.Cells بالفعل في مشروعك، فإن هذه الطريقة لا تضيف أي عبء تقريبًا.

### المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث | بيئة تشغيل حديثة، أداء أفضل، ودعم كامل لـ Aspose.Cells. |
| Aspose.Cells for .NET (حزمة NuGet) | توفر الـ `Workbook`، `PresentationExportOptions`، وواجهات `SaveToPptx` التي نعتمد عليها. |
| ملف Excel أساسي يحتوي على مخطط واحد على الأقل | التصدير يعمل فقط عندما يكون هناك كائن مخطط؛ وإلا سيكون ملف PPTX فارغًا. |
| Visual Studio 2022 (أو أي بيئة تطوير تفضّلها) | تسهّل عملية التصحيح وإدارة الحزم. |

إذا كان لديك هذه العناصر جاهزة، فلنبدأ.

## كيفية تصدير Excel إلى PowerPoint مع مخططات قابلة للتحرير

فيما يلي العينة **الكاملة والقابلة للتنفيذ** التي توضح التدفق بالكامل. كل كتلة مشروحة مباشرةً بعدها، بحيث يمكنك النسخ‑اللصق والتعديل دون الحاجة للبحث في الوثائق.

### الخطوة 1: تثبيت Aspose.Cells

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.Cells
```

سيتم جلب أحدث نسخة مستقرة (حالياً 24.9) وإضافة المراجع اللازمة إلى ملف `.csproj` الخاص بك.

### الخطوة 2: تحميل دفتر عمل Excel

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

> **لماذا يهم هذا:** `Workbook` هو نقطة الدخول لأي تعديل على Excel. بتحميل الملف أولاً، نضمن أن التصدير اللاحق يعمل على البيانات والتنسيق نفسه الذي تراه في Excel.

### الخطوة 3: تكوين خيارات تصدير PPTX للحفاظ على قابلية تحرير المخططات

```csharp
// Step 3: Configure PPTX export options to keep charts editable
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableCharts = true   // This flag ensures charts stay editable in PowerPoint
};
```

إذا تركت `ExportEditableCharts` بدون تفعيل، سيقوم Aspose بتحويل المخططات إلى صور مسطحة. وهذا يتعارض مع هدف **كيفية تصدير المخططات** بصيغة قابلة للتحرير.

### الخطوة 4: حفظ الورقة الأولى كملف PPTX

```csharp
// Step 4: Export the first worksheet as a PPTX file using the options
workbook.Worksheets[0].PageSetup.SaveToPptx(@"YOUR_DIRECTORY\Editable.pptx", exportOptions);
```

طريقة `SaveToPptx` تكتب ملف PowerPoint حيث يتحول كل خلية Excel إلى مربع نص، وكل مخطط إلى كائن مخطط PowerPoint أصلي. الآن يمكنك فتح `Editable.pptx` في PowerPoint والنقر مزدوجًا على أي مخطط لتعديل السلاسل أو المحاور أو النمط.

### الخطوة 5: التحقق من النتيجة

1. افتح `Editable.pptx` في Microsoft PowerPoint.  
2. ابحث عن الشريحة التي تت对应 للورقة المصدرة.  
3. انقر على مخطط → اختر **Edit Data** → يجب أن ترى شبكة البيانات بنمط Excel.

إذا ظل المخطط صورة، فتأكد من أن `ExportEditableCharts` مضبوط على `true` وأن الورقة المصدر تحتوي فعليًا على كائن مخطط.

![مخطط يوضح التدفق من Excel إلى PowerPoint – كيفية تصدير Excel](/images/excel-to-pptx-flow.png "مثال على كيفية تصدير Excel")

## تحويل Excel إلى PowerPoint – الأخطاء الشائعة والنصائح

حتى مع الشيفرة الصحيحة، قد يواجه المطورون بعض العقبات. إليك أكثر المشكلات شيوعًا وكيفية تجنبها.

| المشكلة | الشرح | الحل |
|-------|-------------|-----|
| **عدم ظهور المخططات** | قد لا يحتوي دفتر العمل على أي كائنات مخطط، أو قد تكون مخفية. | تأكد من أن المخطط مرئي وليس على ورقة مخفية. |
| **تحول المخططات إلى صور** | ترك `ExportEditableCharts` على القيمة الافتراضية `false`. | اضبط `ExportEditableCharts = true` كما هو موضح في الخطوة 3. |
| **أخطاء مسار الملف** | استخدام مسارات نسبية دون `Path.Combine` المناسب. | يفضَّل `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`. |
| **ملفات كبيرة تسبب OutOfMemory** | تصدير دفتر عمل يحتوي على آلاف الصفوف والعديد من المخططات يستهلك الذاكرة. | استخدم `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` قبل التحميل. |
| **عدم توافق الإصدارات** | استخدام نسخة قديمة من Aspose.Cells لا تدعم `PresentationExportOptions`. | حدّث إلى أحدث حزمة NuGet. |

### إضافية: تصدير عدة أوراق عمل

إذا كنت بحاجة إلى **إنشاء PowerPoint من Excel** لأكثر من ورقة، يمكنك تكرار المجموعة:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string pptxPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(pptxPath, exportOptions);
}
```

كل ورقة عمل تتحول إلى ملف PPTX خاص بها، مع الحفاظ على قابلية تحرير المخططات في جميعها.

## حفظ Excel كـ PowerPoint – سيناريوهات متقدمة

### دمج الصور بجانب المخططات

أحيانًا يخلط التقرير بين المخططات وشعارات الشركة. Aspose يتعامل مع الصور كأي شكل آخر، لذا ستظهر في PPTX تلقائيًا. إذا أردت التحكم في الترتيب، عدّل قيمة Z‑index عبر خصائص `Shape` قبل التصدير.

### تخطيطات شرائح مخصصة

يدعم PowerPoint الشرائح الرئيسية (master slides). بينما `SaveToPptx` ينشئ تخطيطًا افتراضيًا، يمكنك لاحقًا تطبيق قالب رئيسي:

```csharp
using Aspose.Slides;

// Load the generated PPTX
Presentation pres = new Presentation(@"YOUR_DIRECTORY\Editable.pptx");

// Apply a master template (must be a .pptx file)
pres.Masters.AddFromFile(@"TEMPLATES\CorporateTemplate.pptx");

// Save the final version
pres.Save(@"YOUR_DIRECTORY\FinalPresentation.pptx", SaveFormat.Pptx);
```

هذه الخطوة تسمح لك **بتحويل Excel إلى PowerPoint** مع الحفاظ على هوية العلامة التجارية الخاصة بشركتك.

### التعامل مع أنواع المخططات المختلفة

معظم أنواع المخططات الشائعة (Bar, Column, Line, Pie) تُصدَّر بشكل مثالي. ومع ذلك، **كيفية تصدير المخططات** مثل Radar أو Stock قد تتطلب تنسيقًا إضافيًا بعد الاستيراد. في هذه الحالات يمكنك:

1. التصدير كما هو موضح.  
2. فتح ملف PPTX برمجيًا باستخدام Aspose.Slides.  
3. تعديل خصائص المخطط (مثلاً `Chart.Type = ChartType.Radar`).  

## ملخص وخطوات تالية

غطّينا كل ما تحتاج معرفته حول **كيفية تصدير Excel** إلى مجموعة شرائح PowerPoint مع الحفاظ على قابلية تحرير المخططات. الخطوات الأساسية—تثبيت Aspose.Cells، تحميل دفتر العمل، تكوين `PresentationExportOptions`، واستدعاء `SaveToPptx`—هي بضع أسطر من كود C#، لكنها تستبدل سير عمل يدوي كامل.

### ما الذي يمكنك تجربته لاحقًا

- **تحويل Excel إلى PowerPoint** لكامل دفتر العمل باستخدام مثال الحلقة.  
- تجربة **إنشاء PowerPoint من Excel** لتقارير لوحة تحكم ديناميكية تُحدَّث كل ليلة.  
- دمج هذا التصدير مع **Aspose.Slides** لتطبيق قوالب شرائح رئيسية وتلقيم العلامة التجارية.  
- استكشاف طريقة `ExportAllSheetsAsPptx` إذا رغبت في ملف PPTX واحد يحتوي على عدة أوراق عمل.

لا تتردد في تعديل المسارات، ضبط خيارات التصدير، أو دمج المنطق في خدمة تقارير أكبر. الحد الوحيد هو إبداعك في تصور البيانات.

---

*برمجة سعيدة! إذا واجهت أي صعوبات أثناء محاولة **حفظ Excel كـ PowerPoint**، اترك تعليقًا أدناه أو راجع وثائق Aspose.Cells لأحدث التحديثات.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}