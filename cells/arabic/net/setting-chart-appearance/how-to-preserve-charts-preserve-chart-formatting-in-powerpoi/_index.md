---
category: general
date: 2026-07-03
description: كيفية الحفاظ على المخططات مع الحفاظ على تنسيق المخطط باستخدام Aspose.Slides
  في C#. اتبع هذا الدليل خطوة بخطوة.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: ar
og_description: كيفية حفظ المخططات والحفاظ على تنسيق المخطط باستخدام Aspose.Slides
  في C#. دليل كامل مع الكود.
og_title: كيفية الحفاظ على المخططات – الحفاظ على تنسيق المخططات في PowerPoint (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: كيفية الحفاظ على المخططات – الحفاظ على تنسيق المخطط في PowerPoint باستخدام
  C#
url: /ar/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية الحفاظ على المخططات – الحفاظ على تنسيق المخطط في PowerPoint C#

هل تساءلت يومًا **how to preserve charts** عندما تحتاج إلى تصدير أو تعديل ملف PowerPoint برمجيًا؟ ربما جربت حفظًا سريعًا وتحول المخطط إلى صورة ثابتة، مما كسر القدرة على التحرير التي كنت تعتمد عليها.  

في هذا البرنامج التعليمي سنوضح لك **how to preserve charts** **و** نحافظ على **preserve chart formatting** الخاص بها باستخدام Aspose.Slides for .NET. في النهاية ستحصل على مقطع C# جاهز للتنفيذ ينتج ملف PPTX حيث يبقى كل مخطط ككائن OOXML قابل للتحرير — لا مزيد من الصور المسطحة.

## ما ستتعلمه

- الخطوات الدقيقة لتحميل عرض تقديمي، تكوين خيارات التصدير، وحفظه مع **preserving chart formatting**.  
- لماذا علم `ExportEditableObjects` مهم وكيف يمنع تحويل المخططات إلى صورة نقطية.  
- المشكلات الشائعة (مثل صيغ PPT القديمة، الخطوط المفقودة) والحلول السريعة.  

لا يتطلب أي خبرة سابقة في Aspose؛ فقط إعداد أساسي لـ C# وملف PowerPoint تريد الحفاظ على صداقة المخططات فيه.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).  
- حزمة NuGet لـ Aspose.Slides for .NET (`Install-Package Aspose.Slides.NET`).  
- ملف عينة `input.pptx` يحتوي على مخطط واحد على الأقل.  
- Visual Studio، Rider، أو أي محرر تفضله.

---

## الخطوة 1: تثبيت Aspose.Slides وإنشاء مشروع وحدة تحكم جديد

للبدء، أنشئ تطبيق وحدة تحكم جديدًا وجلب المكتبة:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Pro tip:** إذا كنت خلف بروكسي مؤسسي، أضف العلامة `--no-restore` واستعد لاحقًا باستخدام إعدادات البروكسي الخاصة بك.

## الخطوة 2: تحميل العرض التقديمي المصدر – أول مكان لتطبيق **how to preserve charts**

افتح ملف PPTX الخاص بك باستخدام الفئة `Presentation`. هنا يبدأ المسار إلى **how to preserve charts** فعليًا.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

لاحظ أننا لم نتعامل مع أي كائنات مخطط بعد—هذا مقصود. تحميل الملف كما هو يضمن الحفاظ على بنية XML الأصلية، وهو أمر حاسم لـ **preserve chart formatting** لاحقًا.

## الخطوة 3: تكوين خيارات التصدير – جوهر **how to preserve charts**

توفر Aspose.Slides فئة `PresentationExportOptions`. ضبط `ExportEditableObjects` إلى `true` يخبر المحرك بالحفاظ على المخططات والجداول وSmartArt كأجزاء OOXML أصلية بدلاً من تسطيحها.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

لماذا يعمل هذا؟ عندما تكون `ExportEditableObjects` `false` (الإعداد الافتراضي)، تقوم المكتبة بتحويل الكائنات المعقدة إلى صور نقطية للتوافق، مما يدمر **preserve chart formatting**. تشغيله يحافظ على XML المخطط الأصلي، مما يسمح للمستخدمين بفتح PPTX ولا يزال بإمكانهم تعديل بيانات المخطط.

## الخطوة 4: حفظ العرض التقديمي باستخدام الخيارات المكوّنة

الآن نكتب ملف الإخراج. نفس الدالة `Save` التي تقبل `SaveFormat` و `exportOptions` تضمن بقاء المخطط قابلًا للتحرير.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

تشغيل هذا البرنامج ينتج `EditableCharts.pptx`. افتحه في PowerPoint، انقر بزر الماوس الأيمن على مخطط، وسترى خيار “Edit Data” المعتاد—دليل على أننا نجحنا في إتقان **how to preserve charts** و **preserve chart formatting**.

## الخطوة 5: التحقق من النتيجة وحل المشكلات الشائعة

### التحقق

1. افتح `EditableCharts.pptx` في PowerPoint.  
2. انقر على أي مخطط → “Edit Data”.  
3. يجب أن تظهر ورقة بيانات شبيهة بـ Excel، مما يتيح لك تعديل قيم السلاسل.

إذا رأيت صورة ثابتة فقط، تحقق مرة أخرى من أن:

- أنت تستخدم نسخة حديثة من Aspose.Slides (الإصدارات القديمة كان بها أخطاء في `ExportEditableObjects`).  
- ملف PPTX المصدر يحتوي فعليًا على كائنات مخطط (وليس صورًا للمخططات).  
- لا يوجد سمة مخصصة أو استبدال خطوط يسبب عرض المخطط كصورة.

### حالات خاصة

- **Older PPT (binary) files:** حوّلها إلى PPTX أولاً (`pres.Save("temp.pptx", SaveFormat.Pptx)`) قبل تطبيق خيارات التصدير.  
- **Large presentations:** قد يزداد استهلاك الذاكرة؛ فكر في نمط `Dispose` الخاص بـ `Presentation` أو واجهات برمجة التطبيقات المتدفقة للملفات الضخمة.  
- **Embedded fonts:** إذا كان بيئة الهدف تفتقر إلى الخطوط الأصلية، قد يلجأ PowerPoint إلى عرض المخطط كصورة. قم بدمج الخطوط في الملف المصدر أو وزعها مع تطبيقك.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PowerPoint 2003 (PPT)؟**  
ج: لا مباشرةً—`ExportEditableObjects` ينطبق فقط على صيغة PPTX. حوّل أولاً، ثم صدّر.

**س: هل يمكنني الحفاظ على كائنات أخرى مثل SmartArt؟**  
ج: بالتأكيد. علم `ExportEditableObjects` نفسه يحافظ على SmartArt والجداول والرسوم البيانية قابلة للتحرير.

**س: ماذا لو احتجت للحفاظ على حجم الشريحة الأصلي؟**  
ج: حجم الشريحة مخزن في بيانات تعريف العرض التقديمي ولا يتأثر بهذه الخيارات. لا حاجة لكود إضافي.

## الخطوات التالية – استمر في الزخم

الآن بعد أن أتقنت **how to preserve charts**، جرّب استكشاف:

- **preserve chart formatting** لأنواع مخططات محددة (مثل الشريط المكدس مقابل الرادار).  
- استخدام واجهة برمجة تطبيقات `Chart` لتعديل البيانات برمجيًا قبل الحفظ.  
- التصدير إلى صيغ أخرى (PDF، HTML) مع الحفاظ على قابلية تحرير المخططات في PPTX المصدر.  

كل من هذه يبني على نفس المبدأ: الحفاظ على OOXML الأساسي دون تغيير.

## الخلاصة

لقد استعرضنا **how to preserve charts** في ملف PowerPoint باستخدام Aspose.Slides for .NET، ووضحنا الخطوات الدقيقة لـ **preserve chart formatting** اللازمة للحفاظ على هذه المخططات قابلة للتحرير بالكامل. المقتطف الكامل للكود أعلاه جاهز للإدراج في أي مشروع C#، وتغطي الشروحات *السبب* وراء كل سطر—لذا لن تقوم فقط بالنسخ واللصق، بل ستفهم.

جرّبه، عدّل خيارات التصدير، وسرعان ما ستتمكن من أتمتة تحديثات العروض التقديمية دون فقدان القدرة على تعديل بيانات المخطط بدقة. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [كيفية تحويل مخططات Excel إلى SVG باستخدام Aspose.Cells for .NET (دليل خطوة بخطوة)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [كيفية إنشاء مخططات في Excel باستخدام Aspose.Cells for .NET: دليل المطور](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}