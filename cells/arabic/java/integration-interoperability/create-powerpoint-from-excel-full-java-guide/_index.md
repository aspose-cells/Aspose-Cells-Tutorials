---
category: general
date: 2026-06-21
description: إنشاء عرض PowerPoint من Excel بسرعة باستخدام Java. تعلّم كيفية تحويل
  XLSX إلى PPTX باستخدام Aspose.Cells في دليل خطوة بخطوة.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- how to convert xlsx
- how to export excel
- excel workbook to powerpoint
language: ar
og_description: إنشاء PowerPoint من Excel باستخدام Java. يوضح هذا الدرس بالضبط كيفية
  تحويل XLSX إلى PPTX باستخدام Aspose.Cells، مع تغطية الكود، والمشكلات المحتملة، والنصائح.
og_title: إنشاء PowerPoint من Excel – دليل تحويل Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PowerPoint from Excel quickly using Java. Learn how to convert
    XLSX to PPTX with Aspose.Cells in a step‑by‑step tutorial.
  headline: Create PowerPoint from Excel – Full Java Guide
  type: TechArticle
- description: Create PowerPoint from Excel quickly using Java. Learn how to convert
    XLSX to PPTX with Aspose.Cells in a step‑by‑step tutorial.
  name: Create PowerPoint from Excel – Full Java Guide
  steps:
  - name: Expected Output
    text: '- A file named `shapes.pptx` appears in `YOUR_DIRECTORY`. - Opening the
      PPTX in Microsoft PowerPoint shows one slide per worksheet, with all cell formatting,
      charts, and shapes preserved as raster images. - No manual copy‑pasting required—your
      data is now presentation‑ready.'
  - name: 5.1 Large Workbooks or High‑Resolution Slides
    text: 'If your Excel file contains many rows, charts, or high‑resolution graphics,
      the generated PPTX can become bulky. You can reduce file size by:'
  - name: 5.2 Preserving Vector Graphics
    text: If you need vector‑based charts (so they stay crisp when zoomed), Aspose.Cells
      also supports `SaveFormat.SVG` for each slide, then you can assemble an SVG‑based
      PPTX manually. This is more advanced and beyond the scope of this quick guide,
      but worth exploring for design‑heavy decks.
  - name: 5.3 Multiple Worksheets per Slide
    text: Sometimes you want two related worksheets side‑by‑side on a single slide.
      Set `options.setOnePagePerSheet(false);` and use `WorksheetCollection` to control
      the range you render per slide.
  - name: 5.4 Automating Batch Conversions
    text: If you have a folder full of Excel files, wrap the conversion logic inside
      a loop that iterates over `File[] files = new File("YOUR_DIRECTORY").listFiles((dir,
      name) -> name.endsWith(".xlsx"));`. This way you can **convert excel to powerpoint**
      en masse.
  - name: Expected Result Screenshot
    text: '![create powerpoint from excel example](https://example.com/images/create-powerpoint-from-excel.png
      "create powerpoint from excel")'
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells supports both `.xls` and `.xlsx`. Just point
      `Workbook` at the old file; the rest of the code stays identical.
    question: Can I convert an `.xls` (old Excel) file?
  - answer: No. The conversion rasterizes the sheet, so formulas become static values
      on the slide. If you need editable data in PowerPoint, consider exporting to
      CSV and using PowerPoint’s table insertion APIs instead.
    question: Does this method retain formulas?
  - answer: Load the workbook with `loadOptions.setPassword("yourPassword");` before
      creating the `Workbook` object.
    question: What about password‑protected workbooks?
  - answer: 'Not directly via `ImageOrPrintOptions`. You’d need to post‑process the
      generated PPTX with Aspose.Slides for Java, adding notes to each slide programmatically.
      ## Full Working Example – Paste and Run Below is the complete, ready‑to‑run
      program. Copy it into a file named `ExcelToPowerPoint.java`, adj'
    question: Is there a way to add speaker notes automatically?
  type: FAQPage
tags:
- java
- excel
- powerpoint
- file-conversion
title: إنشاء PowerPoint من Excel – دليل Java الكامل
url: /ar/java/integration-interoperability/create-powerpoint-from-excel-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PowerPoint من Excel – دليل Java كامل

هل تساءلت يومًا كيف **تنشئ PowerPoint من Excel** دون فتح التطبيقات يدويًا؟ لست وحدك. كثير منا يحتاج إلى تحويل جداول البيانات الغنية بالبيانات إلى عروض تقديمية جاهزة، سواءً لمراجعات المبيعات الأسبوعية أو لتحديثات سريعة لأصحاب المصلحة. الخبر السار؟ ببضع أسطر من كود Java يمكنك أتمتة العملية بالكامل—بدون نسخ‑لصق، بدون تنسيق يدوي.

في هذا الدرس سنستعرض تحويل **مصنف Excel إلى PowerPoint** باستخدام Aspose.Cells for Java. في النهاية ستحصل على برنامج قابل للتنفيذ يأخذ ملف `.xlsx` ويُنتج ملف `.pptx` مصقول، جاهز لاجتماعك التالي. سنضيف أيضًا نصائح حول **كيفية تصدير بيانات Excel** بكفاءة، لتتمكن من تعديل الحل وفقًا لمشاريعك الخاصة.

## المتطلبات المسبقة – ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي على جهازك:

- **Java Development Kit (JDK) 8 أو أحدث** – الكود يعمل على أي JDK حديث.
- مكتبة **Aspose.Cells for Java** (الإصدار التجريبي المجاني يكفي للاختبار). يمكنك الحصول عليها من Maven Central أو تحميل ملف JAR مباشرة.
- **مصنف Excel** (`shapes.xlsx` في مثالنا) موجود في دليل يمكنك الإشارة إليه.
- **بيئة تطوير** – IntelliJ IDEA، Eclipse، أو حتى محرر نصوص بسيط مع إمكانية التجميع عبر سطر الأوامر.

هل لديك كل ذلك؟ عظيم، لنبدأ.

## الخطوة 1: إعداد المشروع واستيراد الاعتمادات

أولًا، أنشئ مشروع Maven (أو Gradle) جديد وأضف Aspose.Cells كاعتماد. إذا كنت تفضل طريقة JAR اليدوية، فقط ضع `aspose-cells-xx.x.jar` في مجلد `libs` وأضفه إلى classpath.

```xml
<!-- Maven pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

لماذا هذه الخطوة مهمة: بدون المكتبة، لا تملك Java طريقة أصلية **لتحويل Excel إلى PowerPoint**. Aspose.Cells تقوم بالعمل الشاق، حيث تُترجم كل ورقة عمل إلى صورة شريحة خلف الكواليس.

## الخطوة 2: تحميل مصنف Excel

الآن سنقوم بتحميل المصنف المصدر. هذا يعكس السطر الأول من المقتطف الأصلي، لكننا سنلفه بكتلة try‑catch للمتانة.

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Define paths – adjust as needed
        String inputPath = "YOUR_DIRECTORY/shapes.xlsx";
        String outputPath = "YOUR_DIRECTORY/shapes.pptx";

        try {
            // Step 1: Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);
            System.out.println("Workbook loaded successfully.");
```

لاحظ أننا استخدمنا `Workbook workbook = new Workbook(inputPath);`. هذا السطر هو جوهر **كيفية تحويل xlsx**—يستورد كامل جدول البيانات إلى الذاكرة، جاهزًا للمعالجة اللاحقة.

## الخطوة 3: تكوين ImageOrPrintOptions لإخراج PowerPoint

تتعامل Aspose.Cells مع تحويل PowerPoint كعملية صورة‑أو‑طباعة. ننشئ كائن `ImageOrPrintOptions`، نحدد الصيغة المستهدفة إلى PPTX، ونضبط اختياريًا الدقة أو حجم الشريحة.

```java
            // Step 2: Create options for image/print conversion and set the target format to PPTX
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.PPTX);      // PPTX is the modern PowerPoint format
            options.setOnePagePerSheet(true);           // Each worksheet becomes a separate slide
            options.setImageFormat(ImageFormat.Png);    // Use PNG for crisp slide graphics
            options.setQuality(100);                    // Max quality for clearer images
```

لماذا نضبط `OnePagePerSheet`؟ لأن معظم العروض التقديمية تريد **شريحة واحدة لكل ورقة عمل**، مع الحفاظ على التخطيط الذي صممته في Excel. إذا احتجت عدة شرائح لكل ورقة، يمكنك تغيير هذه العلامة لاحقًا.

## الخطوة 4: حفظ المصنف كعرض تقديمي PowerPoint

مع إعداد الخيارات، السطر النهائي يكتب ملف PPTX إلى القرص.

```java
            // Step 3: Save the workbook as a PowerPoint presentation
            workbook.save(outputPath, options);
            System.out.println("Conversion complete! PowerPoint saved at: " + outputPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

هذا كل شيء—**تحويل مصنف Excel إلى PowerPoint** في ثلاث خطوات مختصرة. عند تشغيل البرنامج، تقوم Aspose.Cells برسم كل ورقة كصورة شريحة، وتدمجها في ملف PPTX جديد، وتحفظه في الموقع الذي حددته.

### النتيجة المتوقعة

- يظهر ملف باسم `shapes.pptx` في `YOUR_DIRECTORY`.
- عند فتح PPTX في Microsoft PowerPoint تظهر شريحة واحدة لكل ورقة عمل، مع الحفاظ على جميع تنسيقات الخلايا، المخططات، والأشكال كصور نقطية.
- لا حاجة للنسخ‑اللصق اليدوي—بياناتك الآن جاهزة للعرض.

## الخطوة 5: معالجة السيناريوهات الشائعة وحالات الحافة

على الرغم من أن التحويل الأساسي سهل، إلا أن المشاريع الواقعية غالبًا ما تواجه بعض العقبات. إليك بعض النصائح العملية التي ستوفر عليك عناءً كبيرًا.

### 5.1 مصنفات كبيرة أو شرائح عالية الدقة

إذا كان ملف Excel يحتوي على العديد من الصفوف، المخططات، أو رسومات عالية الدقة، قد يصبح ملف PPTX الناتج ضخمًا. يمكنك تقليل حجم الملف عن طريق:

- خفض `options.setResolution(150);` (الإعداد الافتراضي 220 DPI).
- تغيير `options.setImageFormat(ImageFormat.Jpeg);` وضبط جودة الضغط.
- تقسيم المصنف إلى ملفات أصغر قبل التحويل.

```java
options.setResolution(150);          // Reduce DPI to shrink image size
options.setImageFormat(ImageFormat.Jpeg);
options.setQuality(80);              // JPEG quality (0‑100)
```

### 5.2 الحفاظ على الرسومات المتجهية

إذا كنت تحتاج إلى مخططات متجهية (لتبقى واضحة عند التكبير)، تدعم Aspose.Cells أيضًا `SaveFormat.SVG` لكل شريحة، ثم يمكنك تجميع PPTX قائم على SVG يدويًا. هذا أكثر تقدمًا وخارج نطاق هذا الدليل السريع، لكنه يستحق الاستكشاف للعروض ذات التصميم المكثف.

### 5.3 عدة أوراق عمل في شريحة واحدة

أحيانًا تريد ورقتين عمل مرتبطتين جنبًا إلى جنب في شريحة واحدة. اضبط `options.setOnePagePerSheet(false);` واستخدم `WorksheetCollection` للتحكم في النطاق الذي تُرسمه لكل شريحة.

```java
options.setOnePagePerSheet(false);
Worksheet sheet1 = workbook.getWorksheets().get(0);
Worksheet sheet2 = workbook.getWorksheets().get(1);
// Render both sheets onto a single slide using custom positioning logic.
```

### 5.4 أتمتة التحويل الجماعي

إذا كان لديك مجلد مليء بملفات Excel، ضع منطق التحويل داخل حلقة تتكرر على `File[] files = new File("YOUR_DIRECTORY").listFiles((dir, name) -> name.endsWith(".xlsx"));`. بهذه الطريقة يمكنك **تحويل Excel إلى PowerPoint** على نطاق واسع.

```java
File dir = new File("YOUR_DIRECTORY");
File[] excelFiles = dir.listFiles((d, n) -> n.toLowerCase().endsWith(".xlsx"));
for (File excel : excelFiles) {
    String pptxPath = excel.getAbsolutePath().replace(".xlsx", ".pptx");
    Workbook wb = new Workbook(excel.getAbsolutePath());
    wb.save(pptxPath, options);
    System.out.println("Converted: " + excel.getName());
}
```

## الأسئلة المتكررة (FAQ)

**س: هل يمكنني تحويل ملف `.xls` (Excel قديم)؟**  
ج: بالتأكيد. تدعم Aspose.Cells كلًا من `.xls` و `.xlsx`. ما عليك سوى توجيه `Workbook` إلى الملف القديم؛ يبقى باقي الكود كما هو.

**س: هل تحتفظ هذه الطريقة بالصيغ؟**  
ج: لا. التحويل يُحوّل الورقة إلى صورة نقطية، لذا تصبح الصيغ قيمًا ثابتة على الشريحة. إذا كنت تحتاج إلى بيانات قابلة للتحرير في PowerPoint، ففكر في تصدير إلى CSV واستخدام واجهات برمجة تطبيقات PowerPoint لإدراج الجداول.

**س: ماذا عن المصنفات المحمية بكلمة مرور؟**  
ج: حمّل المصنف باستخدام `loadOptions.setPassword("yourPassword");` قبل إنشاء كائن `Workbook`.

**س: هل هناك طريقة لإضافة ملاحظات المتحدث تلقائيًا؟**  
ج: ليس مباشرة عبر `ImageOrPrintOptions`. ستحتاج إلى معالجة الملف PPTX الناتج باستخدام Aspose.Slides for Java، وإضافة الملاحظات إلى كل شريحة برمجيًا.

## مثال كامل يعمل – انسخه وشغّله

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه في ملف باسم `ExcelToPowerPoint.java`، عدّل المسارات، ثم نفّذ `javac` + `java` أو شغّله من بيئة التطوير الخاصة بك.

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/shapes.xlsx";
        String outputPath = "YOUR_DIRECTORY/shapes.pptx";

        try {
            // Load the workbook (how to export excel)
            Workbook workbook = new Workbook(inputPath);
            System.out.println("Workbook loaded.");

            // Configure conversion options (convert excel to powerpoint)
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.PPTX);
            options.setOnePagePerSheet(true);
            options.setImageFormat(ImageFormat.Png);
            options.setQuality(100);
            options.setResolution(220); // default DPI

            // Perform the conversion
            workbook.save(outputPath, options);
            System.out.println("PowerPoint created at: " + outputPath);
        } catch (Exception e) {
            System.err.println("Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### لقطة شاشة للنتيجة المتوقعة

![إنشاء PowerPoint من مثال Excel](https://example.com/images/create-powerpoint-from-excel.png "إنشاء PowerPoint من مثال Excel")

*(تظهر الصورة شريحة PowerPoint تم إنشاؤها من ورقة Excel، موضحة الحفاظ على حدود الخلايا ومخطط.)*

## الخلاصة

ها أنت ذا—حل شامل من البداية إلى النهاية **لإنشاء PowerPoint من Excel** باستخدام Java. غطينا الكود الأساسي، شرحنا **كيفية تصدير بيانات Excel** كشرائح PPTX، وتناولنا المشكلات الشائعة مثل حجم الملفات الكبير والمعالجة الدفعة. الآن يمكنك أتمتة تحديثات العروض الأسبوعية، توليد عروض جاهزة للعملاء في لحظات، أو دمج هذا التحويل في خط أنابيب تقارير أكبر. تريد التعمق أكثر؟ جرّب إضافة عناوين شرائح مخصصة، دمج روابط تشعبية، أو دمج الناتج مع Aspose.Sl


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Convert Excel Sheets to XPS Format Using Aspose.Cells Java](/cells/english/java/workbook-operations/render-excel-to-xps-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}