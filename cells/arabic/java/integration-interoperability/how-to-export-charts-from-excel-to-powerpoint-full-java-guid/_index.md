---
category: general
date: 2026-06-27
description: كيفية تصدير المخططات من Excel إلى PowerPoint باستخدام Java. تعلم تحويل
  جداول البيانات إلى PowerPoint، حفظ ملفات PPTX، وتصدير بيانات Excel إلى PPT بسهولة.
draft: false
keywords:
- how to export charts
- convert spreadsheet to powerpoint
- how to save pptx
- excel to powerpoint slide
- export excel data ppt
language: ar
og_description: كيفية تصدير المخططات من Excel إلى PowerPoint باستخدام Java. يوضح لك
  هذا الدليل خطوة بخطوة كيفية تحويل جدول بيانات إلى PowerPoint، حفظ ملفات PPTX، وتصدير
  بيانات Excel إلى PPT.
og_title: كيفية تصدير المخططات من إكسل إلى باوربوينت – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  headline: How to Export Charts from Excel to PowerPoint – Full Java Guide
  type: TechArticle
- description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  name: How to Export Charts from Excel to PowerPoint – Full Java Guide
  steps:
  - name: '**Load** the workbook you want to transform.'
    text: '**Load** the workbook you want to transform.'
  - name: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
    text: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
  - name: '**Save** the workbook using the `PPTX` format and the options you configured.'
    text: '**Save** the workbook using the `PPTX` format and the options you configured.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
title: كيفية تصدير المخططات من إكسل إلى باوربوينت – دليل جافا الكامل
url: /ar/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير المخططات من Excel إلى PowerPoint – دليل Java كامل

هل تساءلت يومًا **how to export charts** من مصنف Excel مباشرةً إلى شريحة PowerPoint؟ لست وحدك—غالبًا ما يحتاج المطورون إلى تحويل جداول البيانات المعتمدة على البيانات إلى عروض تقديمية جاهزة دون عناء النسخ واللصق اليدوي. في هذا الدرس سنستعرض حلًا برمجيًا نظيفًا يتيح لك **convert spreadsheet to PowerPoint**، حفظ النتيجة كملف PPTX، وحتى ضبط معالجة المخططات أثناء التنفيذ.

ما ستحصل عليه هو مقطع Java جاهز للتنفيذ يأخذ أي مصنف، يستخرج مخططاته (وكيانات OLE إذا رغبت)، ويولد ملف **excel to powerpoint slide** مصقول. لا واجهة مستخدم إضافية، لا VBA معقد، مجرد كود Java يمكنك إدراجه في مشروعك اليوم.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- **Java 17** أو أحدث (تعمل الواجهة البرمجية على أي JDK حديث)
- مكتبة **Aspose.Cells for Java** (يستخدم الكود `PresentationOptions` و `SaveFormat.PPTX`)
- فهم أساسي لإعداد مشروع Java (Maven/Gradle)
- ملف Excel (`.xlsx`) يحتوي على مخطط واحد على الأقل تريد تصديره

إذا كنت تفتقد ملف JAR الخاص بـ Aspose.Cells، أضفه عبر Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

أو قم بتحميل الـ JAR مباشرةً من موقع Aspose وضعه على مسار الـ classpath الخاص بك.

## نظرة عامة على عملية تصدير المخططات

على مستوى عالٍ، العملية هي:

1. **Load** المصنف الذي تريد تحويله.
2. **Configure** كائن `PresentationOptions` لتحديد العناصر (المخططات، كائنات OLE، إلخ) التي يجب أن تُدرج في مجموعة الشرائح.
3. **Save** المصنف باستخدام صيغة `PPTX` والخيارات التي قمت بتكوينها.

هذا كل شيء. تقوم المكتبة بالعمل الشاق—تحويل كل مخطط إلى رسم متجه، الحفاظ على التخطيط، وإنشاء ملف PowerPoint يمكن فتحه دون مشاكل.

فيما يلي سنفصل كل خطوة، نشرح *لماذا* هي مهمة، ونظهر الكود الدقيق الذي تحتاجه.

## الخطوة 1: تحميل المصنف وتكوين خيارات التصدير

أولًا، نحتاج إلى إخبار Aspose بما يجب تضمينه عند بناء ملف PowerPoint. توفر فئة `PresentationOptions` تحكمًا دقيقًا. ضبط `setExportCharts(true)` يضمن أن كل مخطط يصبح عنصرًا في الشريحة، بينما `setExportOleObjects(true)` يضيف أي كائنات مدمجة (مثل جداول Excel) قد تكون لديك.

```java
import com.aspose.cells.*;

public class ExcelToPowerPointExporter {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source Excel workbook
        // -------------------------------------------------
        String srcPath = "C:/data/sourceWorkbook.xlsx";
        Workbook workbook = new Workbook(srcPath);

        // -------------------------------------------------
        // 2️⃣ Configure presentation export options
        // -------------------------------------------------
        PresentationOptions presentationOptions = new PresentationOptions();
        presentationOptions.setExportCharts(true);          // <-- how to export charts
        presentationOptions.setExportOleObjects(true);     // include embedded OLE objects

        // The next lines are optional but often useful:
        presentationOptions.setExportFormulas(false);      // skip raw formulas if you only need visuals
        presentationOptions.setExportImages(true);         // grab any pictures as well
```

**لماذا هذه الخطوة مهمة:**  
إذا تخطيت `setExportCharts(true)`، سيتعامل Aspose مع المخططات كخلايا عادية، ويضع بياناتها في الشريحة بدلاً من مخطط بصري. وهذا يُفقد الهدف من العرض التقديمي. بالمثل، يتيح تشغيل تصدير OLE الاحتفاظ بالكائنات المعقدة (مثل جداول Pivot) دون كتابة كود إضافي.

> **نصيحة احترافية:** عند التعامل مع مصنفات ضخمة، فكر في إيقاف `setExportFormulas` لتسريع عملية التحويل. يظل المظهر البصري كما هو، لكن العملية تصبح أخف على الذاكرة.

## الخطوة 2: حفظ المصنف كملف PowerPoint

بعد إعداد الخيارات، يصبح التحويل سطرًا واحدًا: استدعِ `workbook.save(...)` مع تعداد `SaveFormat.PPTX`. هذا هو الجزء الذي نجيب فيه على سؤال **how to save pptx** في Java.

```java
        // -------------------------------------------------
        // 3️⃣ Save the workbook as a PowerPoint file
        // -------------------------------------------------
        String outPath = "C:/output/slide.pptx";
        workbook.save(outPath, SaveFormat.PPTX, presentationOptions);

        System.out.println("✅ Conversion complete! Check " + outPath);
    }
}
```

**ما الذي يحدث خلف الكواليس؟**  
يقوم Aspose بالتنقل عبر كل ورقة عمل، استخراج كل مخطط، تحويله إلى شكل PowerPoint (عادةً رسم متجه EMF)، ووضعه على شريحة جديدة. إذا كان لديك عدة أوراق عمل، يحصل كل منها على شريحة خاصة به افتراضيًا. يمكنك لاحقًا إعادة ترتيب الشرائح باستخدام Apache POI أو PowerPoint نفسه.

### النتيجة المتوقعة

افتح `slide.pptx` في Microsoft PowerPoint، وسترى:

- شريحة واحدة لكل ورقة عمل (أو لكل مخطط، حسب مصدر البيانات)
- المخططات معروضة بوضوح، مع الحفاظ على الألوان وعناوين البيانات
- أي كائنات OLE (مثل جداول Excel المدمجة) تظهر ككائنات قابلة للتحرير

إذا لم تظهر أي مخططات، تأكد من أن المصنف المصدر يحتوي فعلاً على كائن مخطط وأن `setExportCharts(true)` لم يتم استبداله في مكان آخر.

## بديل: تصدير مخطط واحد إلى PPTX مستقل

أحيانًا تحتاج فقط إلى **excel to powerpoint slide** لمخطط محدد، وليس للمصنف بأكمله. يمكنك تحقيق ذلك بإنشاء مصنف مؤقت يحتوي فقط على المخطط المطلوب.

```java
        // -------------------------------------------------
        // 4️⃣ Export a single chart (optional)
        // -------------------------------------------------
        // Assume the chart is on the first worksheet, first chart
        Worksheet sheet = workbook.getWorksheets().get(0);
        int chartIndex = 0; // change if you have multiple charts
        Chart chart = sheet.getCharts().get(chartIndex);

        // Clone the chart into a new workbook
        Workbook singleChartWb = new Workbook();
        Worksheet newSheet = singleChartWb.getWorksheets().get(0);
        newSheet.getCharts().addCopy(chart);

        // Use the same PresentationOptions
        singleChartWb.save("C:/output/singleChart.pptx", SaveFormat.PPTX, presentationOptions);
```

**لماذا قد تحتاج هذا:**  
إذا كنت تُنشئ مجموعة شرائح في الوقت الفعلي (مثل خدمة تقارير تُرسل مخططًا واحدًا لكل بريد إلكتروني)، فإن إنشاء مصنف صغير يقلل من استهلاك الذاكرة ويسرّع العملية.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | العَرَض | الحل |
|-------|---------|-----|
| اختفاء المخططات | الشرائح فارغة أو تحتوي فقط على جداول بيانات | تأكد من استدعاء `presentationOptions.setExportCharts(true)` **قبل** `workbook.save`. |
| حجم الملف كبير | PPTX > 30 MB لعدد قليل من المخططات | أوقف تصدير الصور (`setExportImages(false)`) أو اضغط الصور في PowerPoint بعد الإنشاء. |
| فقدان كائنات OLE | جداول Excel المدمجة تتحول إلى صور ثابتة | اضبط `setExportOleObjects(true)`؛ وتأكد من أن كائنات OLE المصدر غير محمية. |
| خطأ توافق | PowerPoint يُظهر أن الملف تالف | استخدم أحدث نسخة من Aspose.Cells؛ قد تحتوي الإصدارات القديمة على أخطاء في إنشاء PPTX. |

## كيفية تصدير المخططات في خط أنابيب CI/CD

إذا كنت تُؤتمت توليد التقارير كجزء من عملية البناء، يمكنك دمج الكود أعلاه في مكوّن Maven أو مهمة Gradle. فقط تأكد من أن JVM لديها مساحة كافية للذاكرة (مثلاً `-Xmx2g`) عند معالجة مصنفات ضخمة.

```groovy
task exportCharts(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = 'com.example.ExcelToPowerPointExporter'
    args = []
    jvmArgs = ['-Xmx2g']
}
```

تشغيل `./gradlew exportCharts` سيولد ملف PPTX دون أي تدخل يدوي—مثالي للوظائف الليلية للتقارير.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي الفئة الكاملة في Java التي يمكنك وضعها في أي بيئة تطوير. تشمل جميع الاستيرادات، معالجة الأخطاء، وتعليقات توضح كل سطر.

```java
// FullExample.java
import com.aspose.cells.*;

public class FullExample {
    public static void main(String[] args) {
        try {
            // 👉 1️⃣ Load the Excel workbook you want to convert
            String srcFile = "C:/data/analysis.xlsx";
            Workbook wb = new Workbook(srcFile);

            // 👉 2️⃣ Set up export options – this is the core of how to export charts
            PresentationOptions opts = new PresentationOptions();
            opts.setExportCharts(true);          // include every chart
            opts.setExportOleObjects(true);     // keep OLE objects (tables, etc.)
            opts.setExportImages(true);         // optionally keep pictures
            opts.setExportFormulas(false);      // skip formulas for speed

            // 👉 3️⃣ Choose where the PPTX will be saved – answer to how to save pptx
            String outFile = "C:/output/analysis.pptx";

            // 👉 4️⃣ Perform the conversion
            wb.save(outFile, SaveFormat.PPTX, opts);

            System.out.println("✅ Excel file converted to PowerPoint successfully!");
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

شغّل الفئة، افتح `analysis.pptx`، وسترى كل مخطط من مصنفك الأصلي يعيش الآن داخل مجموعة شرائح PowerPoint. هذه هي جوهرية **export excel data ppt**—بدون خطوات يدوية، بدون أخطاء نسخ‑لصق.

## ملخص بصري

![مخطط يوضح كيفية تصدير المخططات من Excel إلى PowerPoint باستخدام Aspose.Cells](/images/export-charts-diagram.png "How to export charts from Excel to PowerPoint")

*التوضيح أعلاه يربط التدفق من مصنف Excel → PresentationOptions → ملف PPTX.*

## الخاتمة

غطّينا **how to export charts** من Excel إلى PowerPoint باستخدام Java، عرضنا الكود الدقيق الذي تحتاجه **convert spreadsheet to PowerPoint**، وشرحنا **how to save pptx** بشكل موثوق. من خلال تعديل `PresentationOptions` يمكنك التحكم في كل شيء—from تضمين المخططات إلى معالجة كائنات OLE—مما يمنحك جسرًا مرنًا بين تحليل البيانات وطبقة العرض.

الخطوة التالية؟ جرّب دمج هذا التحويل مع **Apache POI** لإعادة ترتيب الشرائح برمجيًا، أو أدمجه في خدمة Spring Boot تُقدّم تقارير PPTX عند الطلب. يمكنك أيضًا استكشاف تصدير إلى **PDF** أو **HTML** باستخدام نفس المكتبة—Aspose.Cells يجعل ذلك سهلًا.

هل لديك أسئلة حول حالات خاصة،

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات التي تم استعراضها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create and Export Charts in Java Using Aspose.Cells&#58; A Complete Guide](/cells/english/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java&#58; Custom Page Sizes Guide](/cells/english/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}