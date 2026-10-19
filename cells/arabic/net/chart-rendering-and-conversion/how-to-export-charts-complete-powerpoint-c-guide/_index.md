---
category: general
date: 2026-06-05
description: كيفية تصدير المخططات من PowerPoint باستخدام C#. يتضمن تصدير كائنات OLE
  وجعل المخططات قابلة للتحرير في ملف PPTX الناتج – خطوة بخطوة.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: ar
og_description: كيفية تصدير المخططات من PowerPoint باستخدام C#. تعلم تصدير كائنات
  OLE وجعل المخططات قابلة للتعديل في ملف PPTX المحفوظ – خطوة بخطوة.
og_title: كيفية تصدير المخططات – دليل PowerPoint الكامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: كيفية تصدير المخططات – دليل PowerPoint الكامل بلغة C#
url: /ar/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير المخططات – دليل PowerPoint كامل بلغة C#

هل تساءلت يومًا **كيفية تصدير المخططات** من عرض PowerPoint دون فقدان القدرة على تعديلها لاحقًا؟ لست وحدك. في العديد من خطوط تقارير البيانات، تعيش بيانات المخطط داخل ملف PPTX، وبمجرد أن تسلم الملف، غالبًا ما يحتاج المستلم إلى تعديل قيمة أو تغيير تسمية. الخبر السار هو أنه ببضع أسطر من C# يمكنك الحفاظ على قابلية التحرير، ويمكنك أيضًا تصدير كائنات OLE المضمنة في نفس الوقت.

في هذا الدرس سنستعرض مثالًا عمليًا وجاهزًا للتنفيذ يوضح **كيفية تصدير المخططات**، وكيفية **تصدير كائنات OLE**، وكيفية **جعل المخططات قابلة للتحرير** في ملف الإخراج. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET يستخدم مكتبة Aspose.Slides.

> **نصيحة احترافية:** إذا كنت جديدًا على Aspose.Slides، تأكد من إضافة حزمة NuGet `Aspose.Slides.NET` إلى مشروعك—وإلا لن يتم تجميع الكود.

## ما ستحتاجه

| المتطلبات | لماذا يهم |
|-------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | أوقات تشغيل حديثة توفر أداءً أفضل وإدارة حزم أسهل. |
| Aspose.Slides for .NET (latest version) | هذه المكتبة توفر الفئات `Presentation` و `PptxSaveOptions` التي سنستخدمها. |
| ملف PowerPoint تجريبي يحتوي على مخطط واحد على الأقل | العرض التجريبي يعمل على أي ملف `.pptx` يحتوي على مخطط؛ ستلاحظ قابلية التحرير بعد التصدير. |
| بيئة تطوير متكاملة (Visual Studio، Rider، أو VS Code) | مفيد للتصحيح السريع ورؤية الملف المُولَّد. |

لا توجد أدوات طرف ثالث إضافية مطلوبة—كل شيء يتم التعامل معه عبر Aspose API.

## الخطوة 1 – تحميل العرض المصدر

أولاً نحتاج إلى جلب ملف PPTX الأصلي إلى الذاكرة. فكر في ذلك كفتح مستند في Word قبل البدء في التحرير.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **لماذا هذا مهم:** كائن `Presentation` هو نقطة الدخول لجميع العمليات اللاحقة. فهو يحلل الملف، يبني نموذج كائن للشرائح، الأشكال، المخططات، وكائنات OLE، ويحافظ على كل شيء في حالة قابلة للتعديل.

## الخطوة 2 – إنشاء خيارات الحفظ وتمكين المخططات القابلة للتحرير

بشكل افتراضي، عند استدعاء `Save` تقوم المكتبة بتحويل المخططات إلى صور ثابتة. للحفاظ على قابليتها للتحرير يجب تفعيل علم `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **كيف يعمل:** عندما تكون `ExportEditableCharts` مساوية لـ `true`، تقوم المكتبة بكتابة تعريف XML للمخطط (`chart.xml`) داخل ملف PPTX بدلاً من تحويله إلى صورة نقطية. ثم يقرأ PowerPoint هذا الـ XML ويسمح للمستخدم بفتح محرر المخطط.

## الخطوة 3 – تفعيل تصدير كائنات OLE المضمنة

العديد من العروض التقديمية تدمج جداول Excel، رسومات Visio، أو حتى ملفات PDF ككائنات OLE. إذا كنت تريد أن تبقى هذه الكائنات صالحة بعد عملية التصدير، فعّل `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **ما يعنيه فعليًا “تصدير كائنات OLE”:** حزمة OLE تُخزن ككتلة ثنائية داخل ملف PPTX. ضبط هذا العلم يحافظ على الثنائي الأصلي، مما يسمح للمستلم بالنقر المزدوج على الكائن وفتحه في تطبيقه الأصلي (مثل Excel). بدون هذا، سيُحذف كائن OLE، مما يؤدي إلى كسر الروابط وفقدان البيانات.

## الخطوة 4 – حفظ العرض باستخدام الخيارات المُكوَّنة

الآن بعد أن أعددنا الخيارات، نخبر Aspose ببساطة بكتابة الملف.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **النتيجة:** يحتوي `editable.pptx` على نفس الشرائح الموجودة في `input.pptx`، ولكن يمكن تحرير أي مخطط مباشرةً في PowerPoint، وتبقى جميع كائنات OLE المضمنة سليمة.

### مثال كامل يعمل

فيما يلي البرنامج الكامل المستقل الذي يمكنك تجميعه وتشغيله. يتضمن عبارات `using`، وإدارة صحيحة للموارد، وتعليقات تشرح كل سطر.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**الناتج المتوقع:** بعد تشغيل البرنامج، افتح `editable.pptx` في PowerPoint. انقر بزر الماوس الأيمن على أي مخطط → *Edit Data* → يفتح محرر المخطط، مما يؤكد نجاح **جعل المخططات قابلة للتحرير**. انقر مزدوجًا على ورقة Excel المضمنة، وستفتح في Excel، مما يثبت أن **تصدير كائنات OLE** قد نجح.

![مخطط كيفية تصدير المخططات](https://example.com/images/export-charts.png "كيفية تصدير المخططات – PowerPoint بعد التصدير")

*(نص بديل: كيفية تصدير المخططات – لقطة شاشة لبرنامج PowerPoint مع مخطط قابل للتحرير وكائن OLE)*

## أسئلة شائعة وحالات حافة

### ماذا لو كان الملف المصدر لا يحتوي على مخططات؟

سيستمر تشغيل الكود؛ `ExportEditableCharts` ببساطة لا يؤثر لأنه لا يوجد شيء للتحويل. لا يتم إلقاء أي خطأ.

### هل يمكنني تصدير مخططات محددة فقط؟

نعم. بدلاً من استخدام العلم العام `ExportEditableCharts`، يمكنك التجول عبر `presentation.Slides` وتعيين `Chart.IsEditable = true` على كائنات المخطط الفردية قبل الحفظ. هذا يمنحك تحكمًا دقيقًا.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### هل يؤدي تمكين تصدير OLE إلى زيادة حجم الملف؟

قليلًا. يتم تخزين تدفقات OLE الثنائية كما هي، لذا قد يكون ملف PPTX الناتج أكبر ببضع كيلوبايت. في معظم سيناريوهات الأعمال، هذه المقايضة تستحق لأنها تحافظ على قابلية التحرير الكاملة.

### أي إصدارات PowerPoint يمكنها فتح الملف الناتج؟

أي إصدار يدعم معيار OOXML (PowerPoint 2007 وما بعده). تعتمد ميزة المخطط القابل للتحرير على محرر المخططات الأصلي الذي تم تقديمه في Office 2007، لذا فإن الإصدارات القديمة مثل `.ppt` لن تستفيد.

## نصائح لكود جاهز للإنتاج

| النصيحة | السبب |
|-----|--------|
| استخدم كتل `using` (كما هو موضح) لتفريغ كائنات `Presentation`. | يمنع تسرب الذاكرة، خاصةً عند معالجة العديد من الملفات دفعة واحدة. |
| تحقق من صحة مسارات الملفات قبل التحميل. | يتجنب `FileNotFoundException` الذي قد يتسبب في تعطل خدمة الخلفية. |
| سجّل إعدادات `ExportEditableCharts` و `ExportOLEObjects`. | مفيد لتشخيص المشكلات عندما يبلغ المستخدم عن مخططات غير قابلة للتحرير. |
| امسك `Aspose.Slides.Exception` بشكل منفصل. | يوفر رسائل خطأ أوضح من المكتبة (مثل أنواع المخططات غير المدعومة). |
| ضع في الاعتبار `PptxCompressionLevel` إذا كان حجم الملف مهمًا. | يمكنك ضغط الناتج مع الحفاظ على قابلية التحرير. |

## ملخص – ما أنجزناه

بدأنا بسؤال واضح: **كيفية تصدير المخططات** من ملف PowerPoint مع الحفاظ على قابليتها للتحرير وحفظ كائنات OLE المضمنة. من خلال تحميل العرض، وتكوين `PptxSaveOptions` (`ExportEditableCharts = true` و `ExportOLEObjects = true`)، وحفظ الملف، لدينا الآن ملف PPTX يلبي المتطلبين. يمكن إعادة استخدام نفس النمط لتحويل دفعات، خطوط CI، أو أي أداة تقارير آلية.

## ما الذي يمكنك استكشافه لاحقًا؟

- **تصدير المخططات كصور** للتقارير الثابتة (`saveOptions.ExportEditableCharts = false`).  
- **تحويل PPTX إلى PDF** مع الحفاظ على الرسومات المتجهية (`PdfSaveOptions`).  
- **معالجة بيانات المخطط برمجيًا** (مثل تحديث قيم السلسلة قبل التصدير).  
- **دمج مع Azure Functions** لتوفير واجهة برمجة تطبيقات تصدير المخططات عند الطلب.

لا تتردد في التجربة، وأخبرنا بأي حالات حافة تواجهها. برمجة سعيدة، ونتمنى أن تظل جميع مخططاتك قابلة للتحرير!

## ما الذي ينبغي أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [كيفية تحويل مخططات Excel إلى SVG باستخدام Aspose.Cells لـ .NET (دليل خطوة بخطوة)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [كيفية تطبيق السمات على مخططات Excel باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}