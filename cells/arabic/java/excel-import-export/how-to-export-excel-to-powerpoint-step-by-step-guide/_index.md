---
category: general
date: 2026-08-04
description: كيفية تصدير Excel إلى PowerPoint بسرعة. تعلم تحويل Excel إلى PPTX، وتحديد
  منطقة الطباعة، وإنشاء شرائح قابلة للتحرير باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- set print area excel
- create powerpoint from excel
- convert spreadsheet to ppt
language: ar
lastmod: 2026-08-04
og_description: كيفية تصدير Excel إلى PowerPoint بسرعة. يوضح هذا الدرس كيفية تحويل
  Excel إلى PPTX، وتحديد منطقة الطباعة، وإنشاء ملف PowerPoint قابل للتحرير باستخدام
  Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet being transformed into a PowerPoint
  slide with editable shapes
og_title: كيفية تصدير إكسل إلى باوربوينت – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to export Excel to PowerPoint quickly. Learn to convert Excel to
    PPTX, set print area, and create editable slides with Aspose.Cells.
  headline: How to export Excel to PowerPoint – step‑by‑step guide
  type: TechArticle
- description: How to export Excel to PowerPoint quickly. Learn to convert Excel to
    PPTX, set print area, and create editable slides with Aspose.Cells.
  name: How to export Excel to PowerPoint – step‑by‑step guide
  steps:
  - name: Load the workbook containing the data to export
    text: You must open the Excel file before any export options can be applied. Loading
      the workbook also validates that the file exists and is readable.
  - name: Set the print area in Excel before export
    text: Defining a print area tells Aspose.Cells which cells should appear on the
      slide. If you skip this, the entire worksheet may be rendered, leading to oversized
      slides.
  - name: Configure export options for PPTX
    text: Export options allow you to specify the target format and control how the
      sheet is translated into a slide. Here we request PPTX, which creates an editable
      PowerPoint file.
  - name: Save the first worksheet as an editable PowerPoint presentation
    text: Finally, invoke `save` with the PPTX format. The resulting file contains
      a single slide that mirrors the defined print area, and all shapes remain editable.
  type: HowTo
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
- Export
title: كيفية تصدير Excel إلى PowerPoint – دليل خطوة بخطوة
url: /ar/java/excel-import-export/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PowerPoint – دليل خطوة بخطوة

إذا كنت بحاجة إلى **how to export Excel** إلى عرض تقديمي PowerPoint قابل للتحرير، فإن هذا الدليل يقدم الحل الكامل. ستتعرف على كيفية تحويل Excel إلى PPTX، وتحديد منطقة الطباعة، وإنشاء مجموعة شرائح يمكنك تعديلها مباشرةً في PowerPoint.

غالبًا ما ينتهي تصدير البيانات من جدول بيانات بصور ثابتة، ولكن مع Aspose.Cells يمكنك الاحتفاظ بالأشكال والجداول وتنسيق النص. في نهاية هذا الدرس ستحصل على ملف `.pptx` يتصرف كشريحة PowerPoint أصلية، جاهز لمزيد من أعمال التصميم.

## المتطلبات المسبقة

- Java 17 أو أحدث (الكود يستخدم Java API الخاص بـ Aspose.Cells)
- Aspose.Cells for Java 23.9 أو أحدث (قم بالتنزيل من [Aspose website](https://products.aspose.com/cells/java/))
- مصنف باسم `PresentationDemo.xlsx` موجود في دليل معروف
- إلمام أساسي بتطوير Java (أي بيئة تطوير متكاملة تعمل)

## كيفية تصدير Excel – شرح كامل للكود

الأقسام التالية تقسم العملية إلى خطوات واضحة وقابلة لإعادة الاستخدام. كل خطوة تشرح **why** أهميتها، وليس فقط **what** ما يجب كتابته.

### الخطوة 1: تحميل المصنف الذي يحتوي على البيانات المراد تصديرها

يجب فتح ملف Excel قبل تطبيق أي خيارات تصدير. تحميل المصنف يتحقق أيضًا من وجود الملف وإمكانية قراءته.

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PresentationDemo.xlsx");
        // Proceed with export configuration...
```

*لماذا هذه الخطوة؟*  
`Workbook` هو نقطة الدخول لجميع عمليات Aspose.Cells. بدونها لا يمكنك الوصول إلى أوراق العمل، إعدادات الصفحة، أو وظائف التصدير.

### الخطوة 2: تحديد منطقة الطباعة في Excel قبل التصدير

تحديد منطقة الطباعة يخبر Aspose.Cells أي الخلايا يجب أن تظهر على الشريحة. إذا تخطيت هذه الخطوة، قد يتم عرض كامل ورقة العمل، مما يؤدي إلى شرائح ذات حجم كبير.

```java
        // Define the printable range (A1 to H30)
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");
```

*لماذا هذه الخطوة؟*  
`setPrintArea` يعكس ميزة **set print area excel** في Excel، مما يضمن أن الخلايا المحددة فقط تظهر في شريحة PowerPoint. هذا يقلل من حجم الملف ويحافظ على ترتيب التخطيط.

### الخطوة 3: تكوين خيارات التصدير لـ PPTX

خيارات التصدير تسمح لك بتحديد الصيغة المستهدفة والتحكم في كيفية تحويل الورقة إلى شريحة. هنا نطلب PPTX، الذي ينشئ ملف PowerPoint قابل للتحرير.

```java
        // Configure export options to generate a PPTX file
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*لماذا هذه الخطوة؟*  
`ImageOrPrintOptions` يجمع إعدادات مثل جودة الصورة، مقياس الصفحة، وتوجيه **convert excel to pptx**. ضبط `SaveFormat.PPTX` يضمن أن الناتج هو مجموعة شرائح PowerPoint بدلاً من صورة ثابتة.

### الخطوة 4: حفظ ورقة العمل الأولى كعرض PowerPoint قابل للتحرير

أخيرًا، استدعِ `save` بصيغة PPTX. الملف الناتج يحتوي على شريحة واحدة تعكس منطقة الطباعة المحددة، وجميع الأشكال تظل قابلة للتحرير.

```java
        // Export the first worksheet to an editable PowerPoint file
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);
    }
}
```

*لماذا هذه الخطوة؟*  
`workbook.save` يقوم بالتحويل الفعلي. لأننا حددنا مسبقًا منطقة الطباعة وخيارات التصدير، فإن الشريحة المولدة تحترم التخطيط الذي صممته في Excel. يمكن فتح ملف الإخراج في Microsoft PowerPoint، حيث يمكنك نقل الأشكال، تغيير حجمها، أو تغيير لونها—مما يلبي متطلب **create powerpoint from excel**.

#### النتيجة المتوقعة

- ملف باسم `EditableShapes.pptx` يظهر في `YOUR_DIRECTORY`.
- فتح الملف في PowerPoint يظهر شريحة واحدة تحتوي على النطاق `A1:H30` من المصنف الأصلي.
- جميع مربعات النص، المخططات، والأشكال قابلة للتحرير بالكامل، مثل كائنات PowerPoint الأصلية.

## تحويل Excel إلى PPTX – التعامل مع أوراق عمل متعددة

إذا كنت بحاجة إلى **convert spreadsheet to ppt** لأكثر من ورقة عمل واحدة، كرّر خطوة التصدير لكل ورقة واختياريًا دمج الشرائح في عرض تقديمي واحد.

```java
        // Loop through all worksheets and add each as a separate slide
        for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
            Worksheet sheet = workbook.getWorksheets().get(i);
            sheet.getPageSetup().setPrintArea("A1:H30"); // adjust per sheet if needed
            // Save each sheet as an individual PPTX (or merge later)
            sheet.getPageSetup().setPrintArea("A1:H30");
            workbook.save("YOUR_DIRECTORY/Slide_" + (i + 1) + ".pptx", SaveFormat.PPTX);
        }
```

*نصيحة:* استخدم كائنات `Presentation` من Aspose.Slides إذا رغبت في دمج الشرائح المولدة في مجموعة واحدة برمجيًا.

## تحديد منطقة الطباعة في Excel – أفضل الممارسات

- اختر منطقة طباعة تتطابق مع التخطيط البصري الذي تريده على الشريحة.
- تجنب الخلايا المدمجة التي تمتد خارج النطاق المحدد؛ قد تتسبب في تحجيم غير متوقع.
- اختبر منطقة الطباعة عن طريق الطباعة إلى PDF أولاً؛ عرض PDF يعكس ناتج PowerPoint.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|---------|-------|------|
| شريحة فارغة | لم يتم تحديد منطقة الطباعة أو تم تحديد نطاق فارغ | تحقق من أن `setPrintArea` يشير إلى خلايا تحتوي على بيانات |
| تشوه الأشكال | مستوى تكبير ورقة العمل > 100% | أعد ضبط التكبير إلى 100% قبل التصدير |
| خطوط مفقودة | الخطوط غير مثبتة على الخادم | تضمين الخطوط المطلوبة أو استخدام بدائل متوفرة في النظام |
| حجم ملف كبير | تصدير كامل الورقة | قلل النطاق باستخدام **set print area excel** أو قسم إلى شرائح متعددة |

## تحويل Excel إلى PPTX – نهج بديل باستخدام Aspose.Slides

إذا كنت تستخدم بالفعل Aspose.Slides، يمكنك استيراد ملف PPTX الذي تم إنشاؤه بواسطة Aspose.Cells ثم إثرائه بالحركات، الانتقالات، أو شرائح إضافية. هذا يوضح مرونة سير عمل **convert spreadsheet to ppt**.

```java
import com.aspose.slides.*;

Presentation pres = new Presentation("YOUR_DIRECTORY/EditableShapes.pptx");
// Add a title slide
ISlide titleSlide = pres.getSlides().addEmptySlide(pres.getSlideSize().getSize());
// Save the enhanced deck
pres.save("YOUR_DIRECTORY/FinalPresentation.pptx", SaveFormat.Pptx);
```

## الخاتمة

أنت الآن تعرف **how to export Excel** إلى مجموعة شرائح PowerPoint قابلة للتحرير بالكامل باستخدام Aspose.Cells for Java. يغطي الدرس عملية **convert excel to pptx**، ويظهر كيفية **set print area excel** للتحكم الدقيق، ويظهر طريقة سريعة لـ **create powerpoint from excel**. باتباع هذه الخطوات يمكنك أتمتة إنشاء التقارير، بناء لوحات معلومات تعتمد على الشرائح، أو تبسيط العروض التقديمية المدفوعة بالبيانات.

**الخطوات التالية**

- استكشف **convert spreadsheet to ppt** مع أوراق عمل متعددة لإنشاء مجموعات شرائح متعددة.  
- أضف مخططات، جداول، أو صور إلى مصدر Excel ولاحظ كيف تظهر في PowerPoint.  
- استخدم Aspose.Slides لإضافة حركات، انتقالات شرائح، أو ملاحظات المتحدث برمجيًا.

لا تتردد في تجربة مناطق طباعة مختلفة، اتجاهات الصفحات، وخيارات التصدير لتخصيص الناتج وفقًا لاحتياجاتك الدقيقة في التقارير. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تحديد منطقة طباعة في Excel باستخدام Aspose.Cells لـ .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells لـ .NET&#58; دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية نسخ جدول Pivot في C# – تحويل Excel إلى PPTX، نسخ النطاق وإنشاء مربع نص](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}