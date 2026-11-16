---
category: general
date: 2026-11-16
description: تعلم كيفية تصدير الشكل من Excel إلى PowerPoint باستخدام Java، وتحويل
  مخطط Excel إلى ملف PPTX وحفظ الشكل كملف PPTX باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: ar
lastmod: 2026-11-16
og_description: كيفية تصدير الشكل من Excel إلى PowerPoint باستخدام Java. اتبع هذا
  الدرس الكامل لتحويل مخطط Excel، حفظ الشكل بصيغة PPTX، وإدراج الشكل في ملف PowerPoint.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: كيفية تصدير الشكل من Excel إلى PowerPoint باستخدام Java – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: كيفية تصدير الشكل من إكسل إلى باوربوينت باستخدام جافا
url: /ar/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير الشكل من Excel إلى PowerPoint باستخدام Java

إذا كنت بحاجة إلى **كيفية تصدير الشكل** من مصنف Excel إلى شريحة PowerPoint، فإن هذا الدليل يوضح لك الخطوات الدقيقة. ستتعرف على كيفية **تحويل كائنات مخطط Excel**، وتحويلها إلى **شكل إلى PowerPoint**، وأخيرًا **حفظ الشكل بصيغة PPTX** مع خيارات التصدير الصحيحة.

تصدير الشكل هو طلب شائع عند إنشاء تقارير برمجياً. بنهاية هذا الشرح ستحصل على برنامج Java مستقل يُنشئ ملف `shape.pptx` جاهز للعرض. لا تحتاج إلى أي سكريبتات خارجية، والكود يعمل مع Aspose.Cells 2024‑R2 أو أحدث.

## المتطلبات المسبقة

* Java 17 أو أحدث (الكود يُجمَّع مع أي JDK 8+)
* مكتبة Aspose.Cells for Java (حمّلها من موقع Aspose أو أضف الاعتماد في Maven)
* ملف Excel (`chart.xls`) يحتوي على شكل واحد على الأقل (مخطط، مربع نص، أو SmartArt)
* إلمام أساسي بمعالجة الاستثناءات في Java

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## كيفية تصدير الشكل من Excel إلى PowerPoint (التدفق العام)

تتكون العملية من أربعة أقسام منطقية:

1. **تحميل المصنف** الذي يحتوي على الشكل.  
2. **تحديد موقع الشكل** في الورقة الأولى.  
3. **تهيئة خيارات التصدير** بحيث يصبح الشكل كائن PowerPoint قابل للتحرير.  
4. **حفظ الشكل كملف PPTX**.

يتم شرح كل قسم بالتفصيل أدناه، ويتبع الشرح البرنامج القابل للتنفيذ بالكامل.

## الخطوة 1: تحميل المصنف الذي يحتوي على الشكل

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*لماذا هذه الخطوة؟*  
`Workbook` هو نقطة الدخول لجميع عمليات Aspose.Cells. تحميل الملف يمنحك إمكانية الوصول إلى الأوراق، الخلايا، ومجموعة الأشكال. إذا تعذر العثور على الملف، تقوم Aspose.Cells بإلقاء استثناء `FileNotFoundException`، والذي نلتقطه لاحقًا.

## الخطوة 2: الوصول إلى الورقة الأولى واسترجاع الشكل المستهدف

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*لماذا هذه الخطوة؟*  
الأوراق مخزنة في مجموعة ذات فهرس يبدأ من الصفر، لذا `get(0)` يُعيد الورقة الأولى. الأشكال أيضًا مفهرسة؛ `get(0)` يجلب الشكل الأول، والذي عادةً ما يكون المخطط الذي تريد تصديره. إذا كان المصنف يحتوي على عدة أشكال، يمكنك التكرار عبر المجموعة أو استخدام `shape.getName()` لاختيار شكل محدد.

## الخطوة 3: إعداد خيارات التصدير – نريد الشكل ككائن PPTX قابل للتحرير

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*لماذا هذه الخطوة؟*  
`ImageOrPrintOptions` يتحكم في طريقة عرض الشكل. باختيار `SaveFormat.PPTX`، تقوم المكتبة بتحويل الرسوم البيانية في Excel إلى شكل PowerPoint قائم على المتجهات يبقى قابلاً للتحرير بعد الاستيراد. هذا أساسي لتحويل **shape to PowerPoint** الحقيقي؛ استخدام PNG أو JPEG سيقفل الشكل كصورة.

## الخطوة 4: تصدير الشكل إلى ملف PowerPoint

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*لماذا هذه الخطوة؟*  
طريقة `save` تكتب الشكل باستخدام الخيارات التي عُرِّفت مسبقًا. الملف الناتج `shape.pptx` يحتوي على شريحة واحدة يظهر فيها الشكل تمامًا كما كان في Excel، لكن الآن يمكنك تحريره في PowerPoint (تغيير الألوان، تعديل الحجم، إضافة حركات، إلخ). هذا يحقق مطلب **save shape PPTX**.

## مثال كامل قابل للتنفيذ

انسخ الفئة بالكامل إلى ملف باسم `ExportShapeDemo.java`، استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي، ثم نفّذ الأمر `javac ExportShapeDemo.java && java ExportShapeDemo`. بعد التنفيذ ستجد `shape.pptx` في المجلد المستهدف.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### النتيجة المتوقعة

```
Export completed. File saved as shape.pptx
```

افتح `shape.pptx` في Microsoft PowerPoint. ستظهر شريحة واحدة تحتوي على المخطط (أو مربع النص) الأصلي من Excel كشكل PowerPoint قابل للتحرير بالكامل.

## الاختلافات الشائعة والحالات الخاصة

| الحالة | التعديل الموصى به |
|-----------|------------------------|
| **أشكال متعددة** | كرّر عبر `worksheet.getShapes()` واستدعِ `save` لكل شكل، أو اختر باستخدام `shape.getName()`. |
| **الشكل مخطط يحتوي على سلاسل بيانات** | استخدم `exportOptions.setExportChartAsEditable(true)` للحفاظ على قابلية تحرير السلاسل. |
| **الحاجة إلى تخطيط شريحة محدد** | بعد الحفظ، افتح PPTX باستخدام Aspose.Slides وأدرج الشكل في تخطيط مخصص. |
| **مصنف كبير** | حمّل الورقة المطلوبة فقط باستخدام `Workbook(String, LoadOptions)` لتقليل استهلاك الذاكرة. |
| **صيغة إخراج مختلفة (PDF, PNG)** | غيّر `exportOptions.setSaveFormat(SaveFormat.PDF)` أو `SaveFormat.PNG`. هذا مفيد عندما تريد **convert Excel chart** إلى صورة ثابتة بدلاً من شكل PowerPoint. |

**نصيحة محترف:** تأكد دائمًا من أن فهرس الشكل (`get(0)`) يطابق العنصر البصري الذي تنوي تصديره. ترتيب مجموعة الأشكال يعكس ترتيب الإدراج في Excel، والذي قد يختلف عن ترتيب الطبقات البصرية.

## قائمة التحقق من استكشاف الأخطاء وإصلاحها لتصدير الشكل من Excel إلى PowerPoint

* **الملف غير موجود** – تأكد من أن المسار في `new Workbook()` يشير إلى ملف `.xls` أو `.xlsx` موجود.  
* **لم يتم إرجاع أي أشكال** – تحقق من أن الورقة تحتوي فعلاً على شكل؛ يمكنك استدعاء `worksheet.getShapes().getCount()` للتصحيح.  
* **الملف المُصدَّر فارغ** – تأكد من ضبط `exportOptions.setSaveFormat(SaveFormat.PPTX)`؛ استخدام صيغة صورة سينتج صورة بدلاً من شكل.  
* **مشكلات توافق** – Aspose.Cells 24.9+ يدعم تصدير PPTX على جميع المنصات الرئيسية. قم بالترقية إذا صادفت `UnsupportedOperationException`.

## الخلاصة

أنت الآن تعرف **كيفية تصدير الشكل** من مصنف Excel وإدراجه في عرض PowerPoint باستخدام Java. غطى الشرح تحميل المصنف، تحديد الشكل، تهيئة خيارات **export shape from Excel**، وأخيرًا **save shape PPTX**. مع هذا الأساس يمكنك أتمتة إنشاء التقارير، بناء لوحات معلومات، أو دمج مرئيات Excel في الشرائح دون الحاجة إلى النسخ واللصق اليدوي.

### الخطوات التالية

* استكشف **convert Excel chart** إلى صيغ Office أخرى مثل PDF أو DOCX.  
* دمج هذه التقنية مع Aspose.Slides لوضع عدة أشكال في شريحة واحدة.  
* جرّب خصائص `ImageOrPrintOptions` (مثل `setResolution`، `setTransparent`) لضبط جودة الشكل المُصدَّر بدقة.

لا تتردد في تعديل الكود للمعالجة الدفعية أو دمجه في خدمة تقارير أكبر. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تصدير الشكل باستخدام ShapeExportOptions في Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [كيفية تصدير ورقة Excel إلى PowerPoint باستخدام Aspose.Cells في Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [كيفية تصدير المخططات من Excel إلى PowerPoint – دليل Java كامل](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}