---
category: general
date: 2026-06-08
description: تعلم كيفية تحويل ملفات XLSX إلى PPTX مع الحفاظ على إمكانية تعديل الأشكال
  باستخدام Aspose. يوضح كود Java خطوة بخطوة كيفية تصدير الأشكال دون فقدان إمكانية
  التعديل.
draft: false
keywords:
- convert xlsx to pptx
- how to export shapes
- how to keep shapes
- aspose export pptx
language: ar
og_description: تحويل XLSX إلى PPTX مع الحفاظ على قابلية تعديل الأشكال. يوضح هذا الدليل
  شفرة Java ويشرح كيفية الحفاظ على الأشكال باستخدام Aspose.
og_title: تحويل XLSX إلى PPTX – تصدير الأشكال القابلة للتحرير باستخدام Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  headline: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  type: TechArticle
- description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  name: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  steps:
  - name: Expected Output
    text: '- A PowerPoint file named `editable.pptx` located in the directory you
      specified. - Each worksheet appears as a separate slide. - All shapes (text
      boxes, arrows, charts) remain fully editable, just as they were in Excel.'
  - name: 1. Shapes Turn Into Images
    text: '> **Symptom:** After conversion, clicking a shape shows no resize handles.'
  - name: 2. Missing Slides for Some Worksheets
    text: '> **Symptom:** Only the first sheet appears in the PPTX.'
  - name: 3. File Not Found Exceptions
    text: '> **Symptom:** Java throws `FileNotFoundException` for the source Excel.'
  - name: Wrap‑Up
    text: We’ve walked through the entire process of **convert xlsx to pptx**, showing
      exactly **how to export shapes** and **how to keep shapes** editable using the
      Aspose API. The complete Java program is ready to drop into any Maven project,
      and the optional tweaks let you tailor the conversion to your exa
  type: HowTo
- questions:
  - answer: Yes, you could use OpenXML SDK, but you’d lose the high‑level shape preservation
      that Aspose handles automatically.
    question: Can I convert XLSX to PPTX without Aspose?
  - answer: The conversion strips out VBA; only visual elements are transferred. If
      you need macro logic in PowerPoint, you’ll have to recreate it manually.
    question: Does this work with macros or VBA code inside the workbook?
  - answer: Aspose processes them efficiently, but memory usage can spike. Consider
      converting sheet‑by‑sheet or increasing the JVM heap (`-Xmx2g`).
    question: What about large workbooks with hundreds of shapes?
  type: FAQPage
tags:
- Aspose.Cells
- Aspose.Slides
- Java
- File Conversion
title: تحويل XLSX إلى PPTX – دليل شامل لتصدير الأشكال القابلة للتحرير
url: /ar/java/excel-import-export/convert-xlsx-to-pptx-complete-guide-to-export-editable-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل XLSX إلى PPTX – دليل كامل لتصدير الأشكال القابلة للتعديل

هل تساءلت يومًا كيف **تحول XLSX إلى PPTX** دون تحويل المخططات والرسوم البيانية الجميلة إلى صور ثابتة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى عرض PowerPoint يظل يسمح للمستلم بتعديل الأشكال، تغيير حجم مربعات النص، أو تعديل الموصلات. الخبر السار؟ Aspose يجعل ذلك سهلًا، وفي هذا الدرس سنظهر لك بالضبط **كيفية تصدير الأشكال** و**كيفية الحفاظ على قابلية تعديل الأشكال** أثناء التحويل.

سنستعرض مثالًا عمليًا بلغة Java يقوم بتحميل مصنف Excel، يفعّل الخيار الصحيح، ويكتب ملف PPTX يمكنك فتحه في PowerPoint وتعديله فورًا. في النهاية ستعرف ليس فقط *ما* تستدعيه، بل *لماذا* كل إعداد مهم، بالإضافة إلى مجموعة من النصائح لتجنب المشكلات الشائعة.

## المتطلبات المسبقة – ما تحتاجه قبل البدء

قبل الغوص في الكود، تأكد من وجود ما يلي على جهازك:

- **Java Development Kit (JDK) 8 أو أحدث** – الكود يتوافق مع أي JDK حديث.
- **Aspose.Cells for Java** و **Aspose.Slides for Java** بصيغة JAR – يمكنك الحصول عليها من مستودع Maven الخاص بـ Aspose أو تنزيل أحدث نسخة من موقع Aspose.
- ملف **Excel (`shapes.xlsx`)** يحتوي على الأشكال التي تريد الحفاظ عليها. مصنف بسيط به بعض الكائنات المرسومة يكفي للاختبار.
- بيئة التطوير المفضلة لديك (IntelliJ IDEA، Eclipse، VS Code…) أو مجرد محرر نصوص عادي وواجهة سطر أوامر.

إذا كان أي من هذه غير مألوف لك، لا تقلق. تثبيت ملفات JAR سهل كإضافة تبعيتين إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-slides</artifactId>
    <version>23.12</version>
</dependency>
```

الآن بعد أن غطينا الأساسيات، لنبدأ العمل.

## الخطوة 1: تحميل مصنف Excel الذي يحتوي على الأشكال

أول شيء عليك فعله هو قراءة ملف `.xlsx` الذي يحتوي على الكائنات المتجهية. Aspose.Cells يخفّف عنك تفاصيل OpenXML منخفضة المستوى، لذا كل ما عليك هو إنشاء كائن `Workbook`.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the source workbook – replace the path with your actual file location
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        // From here on we can manipulate the workbook or pass it straight to Slides
```

> **لماذا هذا مهم:** تحميل المصنف بشكل صحيح يضمن أن أي كائنات رسم مدمجة (مخططات، SmartArt، أشكال حرة) تُحفظ في الذاكرة ككائنات Aspose أصلية. إذا تخطيت هذه الخطوة أو استخدمت تدفق ملف عام، قد يتعامل محرك التحويل مع الورقة كصورة ثابتة، مما يفقد القابلية للتعديل.

## الخطوة 2: إخبار Aspose بالحفاظ على الأشكال قابلة للتعديل

Aspose.Slides يوفر علمًا يُدعى `setSaveEditableShape`. عندما يُضبط على `true`، تحتفظ المكتبة ببيانات الشكل الأصلية بدلاً من تحويلها إلى صورة نقطية. هذا هو الجزء المتعلق بـ **كيفية الحفاظ على الأشكال** في دليلنا.

```java
        // Create save options for PPTX output
        ImageOrPrintOptions pptxSaveOptions = new ImageOrPrintOptions();

        // Enable editable shape preservation – this is the key switch
        pptxSaveOptions.setSaveEditableShape(true);
```

> **نصيحة محترف:** القيمة الافتراضية لـ `SaveEditableShape` هي `false`. نسيان تفعيل هذا العلم هو السبب الأكثر شيوعًا لتلقي مطوري PPTX مليء بالصور الثابتة. تأكد من هذه السطر إذا كان الناتج يبدو "معلقًا".

## الخطوة 3: التحويل وحفظ المصنف كملف PPTX

الآن نستدعي طريقة `save`، مع تمرير تعداد `SaveFormat.PPTX` وخياراتنا المخصصة. هذا هو جوهر **تحويل xlsx إلى pptx**.

```java
        // Save the workbook as a PPTX file with editable shapes preserved
        workbook.save("YOUR_DIRECTORY/editable.pptx", SaveFormat.PPTX, pptxSaveOptions);
    }
}
```

عند تشغيل البرنامج، يقرأ Aspose ورقة Excel، يترجم كل ورقة عمل إلى شريحة، ويكتب الملف إلى `editable.pptx`. افتح هذا الملف في PowerPoint وسترى الأشكال الأصلية محفوظة—جاهزة للنقل، إعادة اللون، أو تغيير الحجم.

### النتيجة المتوقعة

- ملف PowerPoint باسم `editable.pptx` موجود في الدليل الذي حددته.
- كل ورقة عمل تظهر كشريحة منفصلة.
- جميع الأشكال (مربعات النص، الأسهم، المخططات) تظل قابلة للتعديل بالكامل، تمامًا كما كانت في Excel.

إذا فتحت PPTX وحاولت تعديل شكل، يجب أن ترى نفس المقابض التي تظهر عند إنشاء شكل من الصفر في PowerPoint.

## المشكلات الشائعة وكيفية تجنبها

### 1. تتحول الأشكال إلى صور

> **العَرَض:** بعد التحويل، النقر على شكل لا يظهر مقبض تعديل.

**السبب:** `setSaveEditableShape(false)` (الإعداد الافتراضي) أو استخدام نسخة قديمة من Aspose لا تدعم هذا العلم.

**الحل:** تأكد من استدعاء `pptxSaveOptions.setSaveEditableShape(true);` *قبل* استدعاء `save`، وتحقق من أنك تستخدم Aspose.Cells/Slides الإصدار 23.x أو أحدث.

### 2. عدم ظهور شرائح لبعض أوراق العمل

> **العَرَض:** تظهر الورقة الأولى فقط في PPTX.

**السبب:** تم حفظ المصنف بأوراق عمل مخفية، أو تم تكوين `SaveOptions` بشكل غير صحيح.

**الحل:** استخدم `workbook.getWorksheets().setVisible(true);` لضمان أن جميع الأوراق مرئية، أو عدّل `LoadOptions` إذا كنت تقوم بتحميل ملف محمي بكلمة مرور.

### 3. استثناءات File Not Found

> **العَرَض:** Java ترمي `FileNotFoundException` لملف Excel المصدر.

**السبب:** مسار غير صحيح أو أذونات ملف مفقودة.

**الحل:** استخدم مسارًا مطلقًا أو ضع الملف في مجلد `resources` الخاص بالمشروع وحمّله عبر `getClass().getResourceAsStream("/shapes.xlsx")`.

## متقدم: تحويل أوراق عمل محددة فقط

أحيانًا لا تحتاج إلى تحويل المصنف بأكمله—ربما تريد فقط تحويل ورقة “Dashboard” إلى شريحة. إليك تعديل سريع:

```java
        // Create a new workbook that contains only the desired sheet
        Workbook source = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        int sheetIndex = source.getWorksheets().get("Dashboard").getIndex();

        // Clone the target sheet into a fresh workbook
        Workbook singleSheet = new Workbook();
        singleSheet.getWorksheets().addCopy(source.getWorksheets().get(sheetIndex));

        // Save the single‑sheet workbook as PPTX
        singleSheet.save("YOUR_DIRECTORY/dashboard.pptx", SaveFormat.PPTX, pptxSaveOptions);
```

هذا المقتطف يوضح **كيفية تصدير الأشكال** من ورقة عمل واحدة مع الحفاظ على قابلية تعديلها.

## ملخص خطوة بخطوة (مرجع سريع)

| الخطوة | الإجراء | API الرئيسي |
|--------|----------|--------------|
| 1 | تحميل `.xlsx` | `new Workbook(path)` |
| 2 | تمكين الأشكال القابلة للتعديل | `pptxSaveOptions.setSaveEditableShape(true)` |
| 3 | حفظ كـ PPTX | `workbook.save(pptPath, SaveFormat.PPTX, pptxSaveOptions)` |

وجود هذا الجدول في متناول يدك يمكن أن يوفر لك بعض النقرات عندما تعود إلى الكود لاحقًا.

## اختبار النتيجة

بعد تشغيل البرنامج، افتح `editable.pptx` في PowerPoint و:

1. انقر على أي شكل – يجب أن ترى مربع الإطار المعتاد.
2. حاول تغيير لون التعبئة – يجب أن يتغير فورًا.
3. انقل الشكل إلى موقع جديد – يجب أن يحتفظ PowerPoint بالإحداثيات الجديدة.

إذا نجحت جميع الإجراءات الثلاث، فقد نجحت في **تحويل xlsx إلى pptx** مع الحفاظ على الأشكال قابلة للتعديل. إذا لاحظت أي شيء غير طبيعي، راجع علم `setSaveEditableShape` وتأكد من نسخة Aspose الخاصة بك.

## الأسئلة المتكررة

- **هل يمكنني تحويل XLSX إلى PPTX بدون Aspose؟**  
  نعم، يمكنك استخدام OpenXML SDK، لكنك ستفقد الحفاظ على الأشكال على مستوى عالٍ الذي توفره Aspose تلقائيًا.

- **هل يعمل هذا مع الماكرو أو كود VBA داخل المصنف؟**  
  التحويل يزيل VBA؛ يتم نقل العناصر البصرية فقط. إذا كنت بحاجة إلى منطق ماكرو في PowerPoint، سيتعين عليك إعادة إنشائه يدويًا.

- **ماذا عن المصنفات الكبيرة التي تحتوي على مئات الأشكال؟**  
  Aspose يعالجها بكفاءة، لكن استهلاك الذاكرة قد يرتفع. فكر في التحويل ورقةً ورقةً أو زيادة حجم heap الخاص بـ JVM (`-Xmx2g`).

## الخطوات التالية – طوّر مهارات التحويل لديك

الآن بعد أن أتقنت أساسيات **تحويل xlsx إلى pptx** مع كائنات قابلة للتعديل، يمكنك استكشاف:

- **إدراج مقاطع فيديو أو صوت** باستخدام واجهات وسائط Aspose.Slides.
- **تطبيق سمات الشرائح** برمجيًا لإضفاء مظهر موحد على العرض.
- **تحويل دفعة من المصنفات** باستخدام حلقة بسيطة—مثالي لخطوط تقارير آلية.
- **التصدير إلى صيغ أخرى** مثل PDF أو HTML مع الحفاظ على بيانات الشكل (`SaveFormat.PDF` مع خيارات مماثلة).

كل هذه المواضيع تعتمد على المفاهيم الأساسية التي غطيناها، لذا ستجد منحنى التعلم سلسًا.

---

![convert xlsx to pptx diagram](image.png "مخطط يوضح تحويل Excel → Aspose → PPTX قابل للتعديل")

*نص بديل للصورة: “مخطط سير عمل تحويل xlsx إلى pptx”*

---

### الخلاصة

استعرضنا العملية الكاملة لـ **تحويل xlsx إلى pptx**، موضحين بالضبط **كيفية تصدير الأشكال** و**كيفية الحفاظ على الأشكال** قابلة للتعديل باستخدام API الخاص بـ Aspose. البرنامج الكامل بلغة Java جاهز للإدراج في أي مشروع Maven، والتعديلات الاختيارية تتيح لك تخصيص التحويل وفقًا لاحتياجاتك الدقيقة. جرّبه، واختبر أوراق عمل مختلفة، ودع Aspose يتولى الجزء الصعب.

إذا واجهت أي صعوبات، راجع توثيق Aspose لأحدث خصائص `ImageOrPrintOptions`، أو اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بحرية إنشاء عروض PowerPoint قابلة للتعديل مباشرة من Excel!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Convert SmartArt to Group Shapes in Java using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/java/images-shapes/convert-smartart-group-shapes-java/)
- [How to Add and Style Shapes in Excel Using Aspose.Cells Java](/cells/english/java/images-shapes/aspose-cells-java-add-styling-shapes-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}