---
category: general
date: 2026-02-09
description: إنشاء PowerPoint من Excel في دقائق – تعلم كيفية تحويل Excel إلى PowerPoint
  وتصدير Excel إلى PPT باستخدام مثال بسيط لكود C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: ar
og_description: أنشئ عرض PowerPoint من Excel بسرعة. يوضح هذا الدليل كيفية تحويل Excel
  إلى PowerPoint، وتصدير Excel إلى PPT، وإنشاء PPT من Excel باستخدام C#.
og_title: إنشاء PowerPoint من Excel – دليل البرمجة الكامل
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: إنشاء عرض بوربوينت من إكسل – دليل خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PowerPoint من Excel – دليل برمجة كامل

هل احتجت يومًا إلى **إنشاء PowerPoint من Excel** لكن لم تكن متأكدًا أي API تستدعي؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يرغبون في تحويل جداول البيانات إلى عروض شرائح دون النسخ واللصق اليدوي.  

خبر سار: ببضع أسطر من C# يمكنك **تحويل Excel إلى PowerPoint**، تصدير أشكال الورقة، والحصول على ملف PPTX جاهز للعرض. في هذا الدرس سنستعرض العملية بالكامل، نشرح لماذا كل خطوة مهمة، ونظهر لك كيفية التعامل مع أكثر المشكلات شيوعًا.

## ما ستتعلمه

- كيفية تحميل مصنف Excel يحتوي على مخططات أو صور أو SmartArt.  
- النداء الدقيق الذي **يصدر Excel إلى PPT** باستخدام مكتبة Aspose.Cells.  
- كيفية حفظ العرض التقديمي المُنشأ والتحقق من النتيجة.  
- نصائح للتعامل مع المصنفات بدون أشكال، تعديل حجم الشريحة، وحل مشكلات عدم توافق الإصدارات.

بدون أدوات خارجية، بدون COM interop، مجرد كود .NET نقي يعمل في أي مكان يدعم .NET Core أو .NET 5+.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. **Aspose.Cells for .NET** (المكتبة التي توفر `SaveToPresentation`). يمكنك الحصول عليها من NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. SDK .NET حديث (يفضل 6.0 أو أحدث).  
3. ملف Excel (`shapes.xlsx`) يحتوي على شكل واحد على الأقل، مخطط أو صورة تريد ظهورها في شريحة.

هذا كل شيء—بدون تثبيت Office، بدون مشاكل الترخيص لهذا الغرض (التقييم المجاني يعمل بشكل جيد).

---

## الخطوة 1: تحميل مصنف Excel (إنشاء PowerPoint من Excel)

أول شيء نحتاجه هو كائن `Workbook` يشير إلى ملف المصدر. هذا الكائن يمثل مستند Excel بالكامل، بما في ذلك جميع الأوراق، المخططات، والكائنات المدمجة.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **نصيحة احترافية:** إذا لم تكن متأكدًا ما إذا كان الملف موجودًا، غلف المُنشئ بـ `try/catch` وقدم رسالة خطأ مفيدة. سيوفر عليك مواجهة `FileNotFoundException` غامضة لاحقًا.

---

## الخطوة 2: تحويل المصنف إلى عرض PowerPoint (تصدير Excel إلى PPT)

تأتي Aspose.Cells مع مُصدّر مدمج يحول المصنف بالكامل — أو أوراق مختارة فقط — إلى عرض PowerPoint. طريقة `SaveToPresentation` تقوم بالعمل الشاق.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

إذا كنت تحتاج فقط إلى **إنشاء ppt من excel** لمجموعة فرعية من الأوراق، يمكنك استخدام النسخة التي تقبل مجموعة `SheetOptions`. في معظم الحالات تكون التحويل الافتراضي كافيًا.

---

## الخطوة 3: حفظ العرض المُنشأ (كيفية تحويل Excel إلى PPTX)

الآن بعد أن لدينا كائن `Presentation`، حفظه على القرص أمر بسيط. سيكون الناتج ملف `.pptx` قياسي يمكن لأي نسخة حديثة من PowerPoint فتحه.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **ماذا لو كان المصنف لا يحتوي على أشكال؟**  
> سيستمر المُصدّر في إنشاء شرائح، لكنها ستكون فارغة. يمكنك التحقق من `workbook.Worksheets[i].Shapes.Count` قبل التحويل وتقرر ما إذا كنت ستتخطى تلك الورقة.

---

## اختياري: تحسين المخرجات (تصدير Excel إلى PPT متقدم)

أحيانًا يكون حجم الشريحة الافتراضي (4:3) غير مثالي للعروض العريضة. يمكنك تعديل أبعاد الشريحة قبل الحفظ:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

هذه التعديلات توضح **كيفية تحويل Excel إلى PowerPoint** بمظهر احترافي، وليس مجرد تصدير بيانات خام.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى تطبيق Console، عدل مسارات الملفات، واضغط **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**النتيجة المتوقعة:** افتح `shapes.pptx` في PowerPoint. سترى شريحة واحدة لكل ورقة عمل، كل منها يحتفظ بالمخططات الأصلية، الصور، والأشكال الأخرى. تظهر شريحة العنوان الاختيارية في البداية، مما يمنح المجموعة مقدمة مصقولة.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو احتجت ورقة واحدة فقط؟* | استخدم `Workbook.Worksheets[0]` واستدعِ `SaveToPresentation` على تلك الورقة عبر `SheetOptions`. |
| *هل يمكنني الحفاظ على صيغ Excel؟* | لا—الصيغ تُعرض كقيم ثابتة في الشريحة. إذا كنت تحتاج إلى بيانات حية، فكر في ربط PPTX بملف Excel لاحقًا. |
| *هل يعمل هذا على Linux/macOS؟* | نعم. Aspose.Cells مستقل عن النظام؛ فقط قم بتثبيت بيئة تشغيل .NET وستكون جاهزًا. |
| *ماذا عن المصنفات المحمية بكلمة مرور؟* | حمّلها باستخدام `LoadOptions` التي تتضمن كلمة المرور قبل استدعاء `SaveToPresentation`. |
| *لماذا أحصل على شرائح فارغة؟* | تحقق من أن المصنف يحتوي فعلاً على أشكال (`Shapes.Count > 0`). تُنشأ الشرائح الفارغة للأوراق الخالية. |

---

## الخلاصة

أصبح لديك الآن حل واضح وشامل لـ **إنشاء PowerPoint من Excel** باستخدام C#. من خلال تحميل المصنف، استدعاء `SaveToPresentation`، وحفظ النتيجة، يمكنك **تحويل Excel إلى PowerPoint**، **تصدير Excel إلى PPT**، و**إنشاء PPT من Excel** ببضع أسطر فقط.  

من هنا قد تستكشف:

- إضافة حركات إلى الشرائح المُنشأة باستخدام Aspose.Slides.  
- أتمتة العملية بالكامل (مثلاً، قراءة الملفات من مجلد، تحويلها دفعة واحدة).  
- دمج الكود في API ASP.NET Core بحيث يمكن للمستخدمين رفع ملف Excel والحصول على PPTX فورًا.

جرّبه، عدّل حجم الشريحة، أضف عنوانًا مخصصًا—هناك مساحة كبيرة لتخصيص المخرجات كما تريد. هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا أدناه، وتمنياتنا بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}