---
category: general
date: 2026-06-30
description: تحويل Excel إلى PPTX باستخدام Aspose.Cells Java – دليل خطوة بخطوة مع
  أشكال قابلة للتحرير، PptxSaveOptions، وتصدير الكائنات القابلة للتحرير.
draft: false
keywords:
- convert excel to pptx
- aspose.cells
- java excel to powerpoint
- pptxsaveoptions
- export editable objects
language: ar
og_description: تحويل Excel إلى PPTX باستخدام Aspose.Cells Java – تعلم كيفية الحفاظ
  على قابلية تحرير الأشكال باستخدام PptxSaveOptions.
og_title: 'تحويل Excel إلى PPTX: دليل Java الكامل'
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Convert Excel to PPTX using Aspose.Cells Java – step‑by‑step guide
    with editable shapes, PptxSaveOptions, and export editable objects.
  headline: 'Convert Excel to PPTX: Complete Java Guide'
  type: TechArticle
- description: Convert Excel to PPTX using Aspose.Cells Java – step‑by‑step guide
    with editable shapes, PptxSaveOptions, and export editable objects.
  name: 'Convert Excel to PPTX: Complete Java Guide'
  steps:
  - name: Add the Aspose.Cells dependency.
    text: Add the Aspose.Cells dependency.
  - name: Load your Excel workbook.
    text: Load your Excel workbook.
  - name: Enable `exportEditableObjects` on `PptxSaveOptions`.
    text: Enable `exportEditableObjects` on `PptxSaveOptions`.
  - name: Save the workbook as a PPTX file.
    text: Save the workbook as a PPTX file.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
- Automation
title: 'تحويل إكسل إلى PPTX: دليل جافا الكامل'
url: /ar/java/excel-import-export/convert-excel-to-pptx-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PPTX: دليل Java الكامل

هل احتجت يومًا إلى **تحويل Excel إلى PPTX** لكنك لم تكن متأكدًا أي مكتبة ستحافظ على مربعات النص والأشكال قابلة للتحرير؟ لست وحدك. في هذا الدرس سنستعرض حلًا عمليًا باستخدام **Aspose.Cells for Java** لا يقتصر فقط على تحويل المصنف إلى عرض تقديمي PowerPoint بل يحافظ أيضًا على الكائنات القابلة للتحرير لتتمكن من تعديلها لاحقًا.

سنتناول كل شيء بدءًا من إضافة ملف JAR الخاص بـ Aspose.Cells إلى مشروعك، وتكوين `PptxSaveOptions` لتفعيل **export editable objects**، وأخيرًا حفظ الملف. في النهاية ستتمكن من تشغيل طريقة Java واحدة والحصول على PPTX قابل للتحرير بالكامل—دون الحاجة إلى النسخ واللصق يدويًا.

## المتطلبات المسبقة

- **Java Development Kit (JDK) 8+** – تم اختبار الدرس على JDK 11.
- **Maven** أو أي أداة بناء تفضلها (Gradle يعمل أيضًا).
- **رخصة** لـ Aspose.Cells for Java (يمكنك البدء برخصة مؤقتة مجانية للاختبار).
- ملف Excel (`shapes.xlsx`) يحتوي على شكل أو مربع نص واحد على الأقل تريد الاحتفاظ به في PowerPoint.

إذا كان أي من ذلك غير مألوف بالنسبة لك، لا تقلق—إعدادها يستغرق بضع دقائق فقط.

## الخطوة 1: إضافة تبعية Aspose.Cells

أولاً، أضف المكتبة إلى مشروعك. باستخدام Maven، أضف المقتطف التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن المكافئ هو `implementation 'com.aspose:aspose-cells:24.10'`.  
> 
> تذكر تحديث مشروعك بعد تعديل ملف البناء حتى يتم تنزيل ملف JAR.

## الخطوة 2: تحميل مصنف Excel

الآن بعد أن أصبحت المكتبة متاحة، يمكننا فتح ملف المصدر. تقوم فئة `Workbook` بكل الأعمال الثقيلة:

```java
import com.aspose.cells.Workbook;

public class ExcelToPptxConverter {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        // Continue with conversion...
    }
}
```

لماذا نستخدم `Workbook`؟ فهي تج abstracts (نستبدل) الملف Excel بالكامل—الأوراق، الخلايا، المخططات، وبشكل حاسم بالنسبة لنا، **الأشكال القابلة للتحرير**. تحميل المصنف أمر بسيط؛ السحر الحقيقي يحدث عندما نخبر Aspose كيفية تصديره.

## الخطوة 3: تكوين PptxSaveOptions للكائنات القابلة للتحرير

إذا قمت ببساطة باستدعاء `workbook.save("output.pptx")`، سيقوم Aspose بتحويل معظم الأشكال إلى صور ثابتة. للحفاظ عليها قابلة للتحرير، يجب تمكين علم `exportEditableObjects` داخل `PptxSaveOptions`.

```java
import com.aspose.cells.PptxSaveOptions;

        // Step 3: Create PPTX save options and enable editable objects
        PptxSaveOptions pptxOptions = new PptxSaveOptions();
        pptxOptions.setExportEditableObjects(true); // <-- key setting
```

### ماذا يفعل `export editable objects` فعليًا؟

عند ضبطه على `true`، يقوم Aspose بتحويل مربعات النص والأشكال وSmartArt في Excel إلى كائنات PowerPoint الأصلية. هذا يعني أنه بعد التحويل يمكنك فتح ملف PPTX في Microsoft PowerPoint، اختيار شكل، تغيير لونه، أو تحرير النص—كما لو أنك أنشأته مباشرةً في PowerPoint. بدون هذا العلم، تتحول تلك العناصر إلى صور ثابتة، وتفقد تلك المرونة.

## الخطوة 4: حفظ المصنف كملف PPTX

مع تحميل المصنف وإعداد الخيارات، السطر الأخير بسيط:

```java
        // Step 4: Save the workbook as a PPTX file using the configured options
        workbook.save("YOUR_DIRECTORY/shapes.pptx", pptxOptions);
        System.out.println("Conversion complete! Check your PPTX file.");
    }
}
```

شغّل طريقة `main`، وسترى ملف `shapes.pptx` جديد بجوار ملف Excel الخاص بك. افتحه في PowerPoint—ستكون الأشكال ومربعات النص الأصلية قابلة للتحرير بالكامل.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PptxSaveOptions;

public class ExcelToPptxConverter {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook (make sure the path is correct)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // Configure PPTX options to keep shapes editable
        PptxSaveOptions pptxOptions = new PptxSaveOptions();
        pptxOptions.setExportEditableObjects(true); // preserve text boxes & shapes

        // Save as PPTX
        workbook.save("YOUR_DIRECTORY/shapes.pptx", pptxOptions);
        System.out.println("Conversion complete! Check your PPTX file.");
    }
}
```

### النتيجة المتوقعة

```
Conversion complete! Check your PPTX file.
```

افتح `shapes.pptx` → اختر أي شكل → حرّر نصه أو لونه أو حجمه. إذا رأيت تلك التغييرات تنعكس، فقد نجحت في **تحويل Excel إلى PPTX** مع الحفاظ على الكائنات القابلة للتحرير.

## معالجة الحالات الخاصة الشائعة

| الحالة | ما يجب مراقبته | الحل الموصى به |
|-----------|-------------------|-----------------|
| **مصنف كبير ( > 200 ميغابايت )** | قد يزداد استهلاك الذاكرة بشكل كبير أثناء التحويل. | زيادة حجم heap للـ JVM (`-Xmx2g`) أو تقسيم المصنف إلى أجزاء أصغر قبل التحويل. |
| **أنواع المخططات غير المدعومة** | بعض ميزات مخططات Excel (مثل الخرائط ثلاثية الأبعاد) لا تتحول بشكل مثالي إلى PowerPoint. | تحويل تلك المخططات إلى صور يدويًا باستخدام `Chart.toImage()` قبل الحفظ. |
| **رخصة مفقودة** | سيضيف Aspose.Cells علامة مائية إلى ملف PPTX الناتج. | تطبيق رخصة مجانية مؤقتة (`License.setLicense("Aspose.Total.lic")`) للاختبار؛ الحصول على رخصة كاملة للإنتاج. |
| **المسار يحتوي على مسافات** | قد تتسبب المسارات في Windows التي تحتوي على مسافات في حدوث `FileNotFoundException`. | استخدام شرطات مائلة معقّدة (`C:\\My Documents\\shapes.xlsx`) أو واجهة برمجة تطبيقات Java `Path`. |

## إضافي: تحويل أوراق متعددة إلى شرائح منفصلة

إذا كنت تريد أن تتحول كل ورقة عمل إلى شريحة خاصة بها، يمكنك التكرار عبر أوراق المصنف وحفظ كل واحدة على حدة:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.PptxSaveOptions;

Workbook wb = new Workbook("YOUR_DIRECTORY/multiSheet.xlsx");
PptxSaveOptions opts = new PptxSaveOptions();
opts.setExportEditableObjects(true);

int sheetCount = wb.getWorksheets().getCount();
for (int i = 0; i < sheetCount; i++) {
    Worksheet sheet = wb.getWorksheets().get(i);
    // Create a temporary workbook containing only this sheet
    Workbook temp = new Workbook();
    temp.getWorksheets().addCopy(sheet);
    temp.getWorksheets().removeAt(0); // remove the default empty sheet
    String outPath = String.format("YOUR_DIRECTORY/slide_%d.pptx", i + 1);
    temp.save(outPath, opts);
    System.out.println("Saved slide: " + outPath);
}
```

كل تكرار ينتج ملف PPTX منفصل يحتوي على شريحة واحدة قابلة للتحرير—مثالي لإنشاء مجموعات شرائح برمجيًا.

## نظرة بصرية

![مخطط يوضح تدفق التحويل من Excel إلى PPTX – تحميل المصنف، تكوين PptxSaveOptions، وحفظه كـ PowerPoint قابل للتحرير](https://example.com/convert-excel-to-pptx-diagram.png "مخطط تدفق تحويل excel إلى pptx")

*نص بديل للصورة*: **مخطط يوضح تدفق التحويل من Excel إلى PPTX** – هذا يفي بمتطلبات النص البديل للصورة بينما يعزز الكلمة المفتاحية الأساسية.

## ملخص

لقد غطينا كيفية **تحويل Excel إلى PPTX** باستخدام Aspose.Cells for Java، مع التركيز على الحفاظ على **الأشكال القابلة للتحرير** عبر `PptxSaveOptions`. الخطوات هي:

1. إضافة تبعية Aspose.Cells.
2. تحميل مصنف Excel الخاص بك.
3. تمكين `exportEditableObjects` على `PptxSaveOptions`.
4. حفظ المصنف كملف PPTX.

الآن لديك مقطع شفرة قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع Java—دون نسخ‑لصق يدوي، ودون فقدان التنسيق.

## ما التالي؟

- **تنسيق الشرائح**: استخدم واجهات برمجة تطبيقات `Presentation` (مثل Aspose.Slides) لإضافة شرائح رئيسية أو سمات مخصصة بعد التحويل.
- **المعالجة الدفعية**: دمج حلقة الأوراق المتعددة مع خدمة مراقبة ملفات لتحويل تقارير Excel الواردة تلقائيًا.
- **النشر السحابي**: غلف الشفرة في نقطة نهاية REST باستخدام Spring Boot حتى تتمكن الخدمات الأخرى من طلب تحويل فوري.

لا تتردد في تجربة إعدادات `PptxSaveOptions` المختلفة—هناك أيضًا `setSlideSize` و `setPreserveFormulas` إذا كنت بحاجة إلى مزيد من التحكم. هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PDF في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [تحويل Excel إلى HTML باستخدام Aspose.Cells Java: دليل خطوة بخطوة](/cells/english/java/workbook-operations/excel-to-html-aspose-cells-java/)
- [تحويل ورقة عمل Excel إلى JPEG في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-worksheet-jpeg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}