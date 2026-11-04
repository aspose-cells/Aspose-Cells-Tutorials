---
category: general
date: 2026-07-16
description: كيفية تصدير ملف pptx من Excel بسرعة. تعلم تعيين منطقة الطباعة، تصدير
  نطاق Excel، وإنشاء عرض PowerPoint قابل للتحرير باستخدام Aspose.Cells و Slides.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export pptx
- set print area
- export excel range
- create editable powerpoint
- export excel chart
language: ar
lastmod: 2026-07-16
og_description: كيفية تصدير ملف pptx من Excel باستخدام Java. إعداد منطقة الطباعة الرئيسية،
  تصدير نطاق، وإنشاء عرض PowerPoint قابل للتحرير باستخدام Aspose.
og_image_alt: Screenshot showing Java code that exports an Excel worksheet as an editable
  PPTX file
og_title: كيفية تصدير PPTX من Excel – دليل Java الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: How to export pptx from Excel quickly. Learn to set print area, export
    excel range, and create editable powerpoint with Aspose.Cells and Slides.
  headline: How to Export PPTX from Excel – Complete Java Guide
  type: TechArticle
- description: How to export pptx from Excel quickly. Learn to set print area, export
    excel range, and create editable powerpoint with Aspose.Cells and Slides.
  name: How to Export PPTX from Excel – Complete Java Guide
  steps:
  - name: '**Load** the Excel workbook with Aspose.Cells.'
    text: '**Load** the Excel workbook with Aspose.Cells.'
  - name: '**Define** the area you want to export using the *print area* feature.'
    text: '**Define** the area you want to export using the *print area* feature.'
  - name: '**Configure** export options to generate a PPTX file.'
    text: '**Configure** export options to generate a PPTX file.'
  - name: '**Save** the result, which will be an editable PowerPoint slide deck.'
    text: '**Save** the result, which will be an editable PowerPoint slide deck.'
  type: HowTo
tags:
- Aspose
- Java
- Excel
- PowerPoint
- Automation
title: كيفية تصدير ملف PPTX من Excel – دليل جافا الكامل
url: /ar/java/excel-import-export/how-to-export-pptx-from-excel-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير PPTX من Excel – دليل Java كامل

هل تساءلت يومًا **كيفية تصدير pptx** مباشرةً من مصنف Excel دون فقدان القدرة على التحرير؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تحويل جداول البيانات إلى شرائح عرض في الوقت الفعلي، خاصةً عندما يجب أن تظل المخططات والأشكال قابلة للتحرير. في هذا الدرس سنستعرض حلًا عمليًا باستخدام Aspose.Cells و Aspose.Slides، موضحين لك بالضبط **كيفية تصدير pptx** مع الحفاظ على التخطيط الأصلي.

سنتناول كل ما تحتاج معرفته: ضبط منطقة الطباعة، تصدير نطاق Excel محدد، إنشاء PowerPoint قابل للتحرير، وحتى التعامل مع كائنات المخططات. في النهاية، ستحصل على برنامج Java جاهز للتنفيذ يحول أي ورقة عمل إلى ملف PPTX قابل للتحرير بالكامل.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك ما يلي:

- **Java Development Kit (JDK) 8 أو أحدث** – أي نسخة حديثة تعمل.
- **Aspose.Cells for Java** و **Aspose.Slides for Java** بصيغة JAR – يمكنك الحصول على نسخ تجريبية أو مرخصة من موقع Aspose.
- **IDE** (IntelliJ IDEA، Eclipse، VS Code، إلخ) – ليس إلزاميًا لكنه مفيد.
- مصنف **Excel** تجريبي (`ShapesWorkbook.xlsx`) يحتوي على الأشكال أو المخططات التي تريد تصديرها.

إذا كان أي من هذه غير مألوف لك، لا تقلق. تثبيت ملفات JAR سهل كإضافتها إلى مسار الفئات (classpath) في مشروعك، والبقية هي أساسيات Java المعتادة.

## نظرة عامة على الحل

الفكرة الأساسية بسيطة:

1. **تحميل** مصنف Excel باستخدام Aspose.Cells.
2. **تحديد** المنطقة التي تريد تصديرها باستخدام خاصية *منطقة الطباعة*.
3. **تكوين** خيارات التصدير لإنشاء ملف PPTX.
4. **حفظ** النتيجة، والتي ستكون مجموعة شرائح PowerPoint قابلة للتحرير.

نظرًا لأن Aspose يحول الأشكال والمخططات تلقائيًا إلى كائنات PowerPoint، يكون ملف الإخراج قابلاً للتحرير بالكامل—دون صور نقطية ثابتة.

سوف نقسم هذا سير العمل إلى خطوات صغيرة، كل خطوة في عنوان H2 واضح. الكلمة المفتاحية الأساسية **how to export pptx** تظهر في العنوان الأول، لتلبية متطلبات تحسين محركات البحث.

---

## الخطوة 1: تحميل المصنف – نقطة الانطلاق لـ كيفية تصدير PPTX

الأول الذي تحتاجه هو كائن `Workbook` يشير إلى ملف Excel المصدر. يمنحك هذا الكائن إمكانية الوصول إلى أوراق العمل، الخلايا، المخططات—وبشكل حاسم—إعدادات تخطيط الصفحة التي تسمح لنا بتعيين *منطقة الطباعة*.

```java
import com.aspose.cells.*;

public class ExportShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the shapes or charts you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesWorkbook.xlsx");
```

> **لماذا هذا مهم:** تحميل المصنف هو الأساس لأي عملية تصدير. بدون ذلك لا يمكنك فحص أو تعديل البيانات التي تنوي تحويلها إلى شرائح.

---

## الخطوة 2: ضبط منطقة الطباعة – التحكم في نطاق تصدير Excel

تحترم Aspose.Cells **منطقة الطباعة** في ورقة العمل عند التحويل إلى PPTX. من خلال تعريف منطقة طباعة، تخبر المكتبة فعليًا *أي خلايا* (أو كائنات مخطط) يجب تضمينها في الشريحة. هذه هي الطريقة الأكثر موثوقية لـ **ضبط منطقة الطباعة** للحصول على تصدير نظيف.

```java
        // Choose the first worksheet (index 0) and set its print area to A1:H30
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");
```

> **نصيحة:** إذا كنت بحاجة لتصدير منطقة مختلفة، ما عليك سوى تغيير سلسلة النطاق (`"A1:H30"`). يمكنك أيضًا تعيين نطاقات غير متصلة متعددة باستخدام قائمة مفصولة بفواصل منقوطة، مثل `"A1:D10;F1:H10"`.

---

## الخطوة 3: تكوين خيارات التصدير – التحضير لتصدير نطاق Excel كـ PPTX

توفر Aspose الفئة `ImageOrPrintOptions` لضبط عملية التصدير بدقة. تعيين `ExportType` إلى `PPTX` يخبر المحرك بإنشاء ملف PowerPoint بدلاً من صورة ثابتة.

```java
        // Create export options and specify PPTX as the target format
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setExportType(ImageExportType.PPTX);
```

> **لماذا هذه الخطوة أساسية:** علم `ExportType` يحدد صيغة الإخراج. استخدام `PPTX` يضمن تحويل الأشكال، مربعات النص، والمخططات إلى كائنات PowerPoint أصلية، مع الحفاظ على إمكانية التحرير.

---

## الخطوة 4: حفظ كـ PowerPoint قابل للتحرير – القطعة النهائية لـ كيفية تصدير PPTX

الآن بعد أن تم إعداد كل شيء، نستدعي `Workbook.save`. الطريقة تستخدم تلقائيًا الخيارات التي عرّفناها مسبقًا، وتنتج ملف `.pptx` يمكن تحرير كل عنصر فيه عبر Microsoft PowerPoint أو أي عارض متوافق.

```java
        // Save the first worksheet as an editable PPTX file
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);
    }
}
```

**الناتج المتوقع:** افتح `EditableShapes.pptx` في PowerPoint، وسترى شريحة تعكس النطاق المحدد من Excel. تتحول الأشكال إلى أشكال PowerPoint، وتصبح المخططات كائنات مخطط قابلة للتحرير، والنص يبقى قابلاً للتحرير بالكامل.

---

## الخطوة 5: تصدير أوراق عمل متعددة أو مخططات محددة – توسيع تصدير مخطط Excel

أحيانًا لا تكون ورقة عمل واحدة كافية. ربما لديك عدة أوراق، كل واحدة تحتوي على مخطط خاص، وتريد أن تتحول كل ورقة إلى شريحة منفصلة. إليك نمطًا سريعًا يمكنك اتباعه:

```java
        // Loop through all worksheets and export each as a separate slide
        for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
            Worksheet sheet = workbook.getWorksheets().get(i);
            // Optional: set a distinct print area per sheet
            sheet.getPageSetup().setPrintArea("A1:G20");

            // Save each sheet as an individual PPTX (you could also merge later)
            String outPath = "YOUR_DIRECTORY/Slide_" + (i + 1) + ".pptx";
            workbook.save(outPath, SaveFormat.PPTX);
        }
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى جميع الأوراق في عرض تقديمي واحد، فكر في استخدام Aspose.Slides لدمج ملفات PPTX المُولدة في مجموعة واحدة. تجعل API العملية سهلة لإضافة شرائح من عروض تقديمية متعددة.

---

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|----------|
| **شرائح فارغة** | لم يتم تعيين منطقة الطباعة أو تم تعيينها لنطاق فارغ. | تحقق مرة أخرى من قيم `setPrintArea`؛ استخدم `worksheet.getPageSetup().getPrintArea()` للتصحيح. |
| **المخططات تظهر كصور** | استخدام نسخة قديمة من Aspose.Cells لا تدعم تحويل المخططات. | قم بترقية إلى أحدث نسخة من Aspose.Cells for Java (≥23.9). |
| **حجم الملف كبير** | تصدير المصنف بالكامل عندما يكون النطاق المطلوب صغيرًا. | قصر منطقة الطباعة أو تصدير `Worksheet` محدد بدلاً من `Workbook` كامل. |
| **خطوط مفقودة** | لا يستطيع PowerPoint العثور على الخط المستخدم في Excel. | تضمين الخطوط في PPTX عبر `exportOptions.setEmbedFonts(true);` (يتطلب نسخة مرخصة). |

معالجة هذه المشكلات مبكرًا توفر عليك جلسات تصحيح محبطة لاحقًا.

---

## متقدم: تصدير نطاق Excel محدد كشريحة تحتوي على مخطط فقط

إذا كان هدفك هو **تصدير مخطط Excel** بدلاً من الورقة بأكملها، يمكنك عزل كائن المخطط وتصديره مباشرة:

```java
        // Assume the first chart in the first worksheet
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

        // Convert the chart to a PPTX slide
        ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
        chartOptions.setExportType(ImageExportType.PPTX);
        chartOptions.setOnePagePerSheet(true); // ensures one slide per chart

        // Save the chart as PPTX
        chart.save("YOUR_DIRECTORY/ChartOnly.pptx", chartOptions);
```

> **ما ستحصل عليه:** شريحة PowerPoint تحتوي على المخطط فقط، قابلة للتحرير بالكامل—مثالية للوحة معلومات أو ملخصات تنفيذية.

---

## مثال عملي كامل – جميع الخطوات مجمعة

فيما يلي البرنامج الكامل الجاهز للتنفيذ بلغة Java والذي يجمع كل ما ناقشنا. انسخه إلى IDE الخاص بك، عدل مسارات الملفات، ثم شغّله.

```java
import com.aspose.cells.*;
import com.aspose.slides.*;

public class ExportShapesToPptx {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing shapes/charts
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesWorkbook.xlsx");

        // 2️⃣ Define the printable area (export excel range)
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // 3️⃣ Set up export options for PPTX (creates editable PowerPoint)
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setExportType(ImageExportType.PPTX);
        // Optional: embed fonts to avoid missing‑font issues
        // exportOptions.setEmbedFonts(true);

        // 4️⃣ Save the worksheet as an editable PPTX file
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        // 🎉 Done! Open EditableShapes.pptx in PowerPoint to see editable shapes and charts.
    }
}
```

**تشغيل البرنامج** سيولد `EditableShapes.pptx` في الدليل المحدد. افتحه، وسترى أن كل شكل ومخطط من النطاق المحدد أصبح الآن كائن PowerPoint أصلي يمكنك تحريكه، تغيير حجمه، أو تعديل لونه.

---

## ملخص – ما تعلمناه حول كيفية تصدير PPTX

- **كيفية تصدير pptx** من Excel باستخدام Aspose.Cells و Aspose.Slides.
- كيفية **ضبط منطقة الطباعة** للتحكم في **نطاق تصدير Excel**.
- طرق **إنشاء PowerPoint قابل للتحرير** يحافظ على الأشكال والمخططات.
- تقنيات **تصدير مخطط Excel** كشريحة مستقلة.
- نصائح للتعامل مع أوراق عمل متعددة والأخطاء الشائعة.

كل هذا يمكن تحقيقه ببضع أسطر من Java، دون نسخ يدوي، وتظل النتيجة قابلة للتحرير بالكامل—ما يلبي تمامًا ما تتطلبه معظم سيناريوهات أتمتة الأعمال.

## الخطوات التالية والمواضيع ذات الصلة

إذا كنت تتطلع للمزيد، فاستكشف هذه المواضيع المجاورة (كل منها يحتوي على إحدى كلماتنا المفتاحية الثانوية):

- [تصدير نطاق Excel إلى HTML باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [كيفية إنشاء مخطط Excel مع خط الاتجاه وتصديره كصورة باستخدام Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}