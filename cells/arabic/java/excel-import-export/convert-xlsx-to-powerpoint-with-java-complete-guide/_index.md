---
category: general
date: 2026-08-11
description: تحويل ملف xlsx إلى باوربوينت باستخدام Java – دليل خطوة بخطوة باستخدام Aspose.Cells
  لتصدير مصنف Excel إلى تنسيق PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert xlsx to powerpoint
- excel workbook to powerpoint
- export excel using java
- excel to powerpoint format
- export excel to pptx
language: ar
lastmod: 2026-08-11
og_description: تحويل xlsx إلى PowerPoint باستخدام Aspose.Cells للغة Java. تعلّم كيفية
  تصدير مصنف Excel إلى تنسيق PPTX، مع الحفاظ على صناديق النص القابلة للتحرير، والتعامل
  مع المشكلات الشائعة.
og_image_alt: Screenshot of Java code converting an Excel file to a PowerPoint presentation
og_title: تحويل xlsx إلى PowerPoint باستخدام Java – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: convert xlsx to powerpoint with Java – step‑by‑step guide using Aspose.Cells
    to export an Excel workbook to PPTX format.
  headline: convert xlsx to powerpoint with Java – complete guide
  type: TechArticle
- description: convert xlsx to powerpoint with Java – step‑by‑step guide using Aspose.Cells
    to export an Excel workbook to PPTX format.
  name: convert xlsx to powerpoint with Java – complete guide
  steps:
  - name: '**Increase the JVM heap** – launch the program with `-Xmx2g` (or higher)
      if you encounter `OutOfMemoryError`.'
    text: '**Increase the JVM heap** – launch the program with `-Xmx2g` (or higher)
      if you encounter `OutOfMemoryError`.'
  - name: '**Convert worksheets individually** – loop through `workbook.getWorksheets()`
      and save each sheet to a separate PPTX file.'
    text: '**Convert worksheets individually** – loop through `workbook.getWorksheets()`
      and save each sheet to a separate PPTX file.'
  - name: '**Reduce image resolution** – use `saveOptions.setResolution(150)` to lower
      DPI; the default is 300 DPI.'
    text: '**Reduce image resolution** – use `saveOptions.setResolution(150)` to lower
      DPI; the default is 300 DPI.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: تحويل ملف xlsx إلى PowerPoint باستخدام Java – دليل كامل
url: /ar/java/excel-import-export/convert-xlsx-to-powerpoint-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل xlsx إلى PowerPoint باستخدام Java – دليل كامل

إذا كنت بحاجة إلى **convert xlsx to powerpoint** في تطبيق Java، يوضح لك هذا البرنامج التعليمي الخطوات الدقيقة. باستخدام Aspose.Cells for Java، يمكنك تصدير مصنف Excel إلى ملف PPTX مع الحفاظ على مربعات النص القابلة للتحرير وتنسيق الخلايا.

ستتعلم كيفية تحميل مصنف Excel، تهيئة خيارات الحفظ لتنسيق PowerPoint، وكتابة ملف PPTX الناتج إلى القرص. يغطي الدليل أيضًا المتغيّرات الشائعة، مثل تحويل ورقة عمل واحدة فقط أو معالجة المصنفات الكبيرة بكفاءة.

## ما يغطيه هذا البرنامج التعليمي

* المتطلبات المسبقة والمكتبات المطلوبة  
* تحميل مصنف Excel يحتوي على TextBox  
* تهيئة `ImageOrPrintOptions` لتحويل **excel workbook to powerpoint**  
* حفظ المصنف كملف PPTX (`export excel to pptx`)  
* التحقق من النتيجة وحل المشكلات الشائعة  

بحلول نهاية الدليل، ستحصل على برنامج Java مستقل يُجري تحويل **excel to powerpoint format** بشكل موثوق.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* مجموعة تطوير Java (JDK) 8 أو أعلى مثبتة  
* Maven أو Gradle لإدارة التبعيات (المثال يستخدم Maven)  
* ملف ترخيص Aspose.Cells for Java (الإصدار التجريبي يعمل للاختبار)  
* ملف Excel إدخال (`input.xlsx`) يحتوي على شكل TextBox واحد على الأقل  

إذا لم تكن familiar مع Aspose.Cells، فهي مكتبة Java صافية تعمل دون الحاجة إلى تثبيت Microsoft Office، مما يجعلها مثالية للأتمتة على الخادم.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أضف التبعية التالية إلى ملف `pom.xml`. سيؤدي ذلك إلى سحب أحدث نسخة مستقرة من Aspose.Cells for Java.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest release -->
</dependency>
```

> **نصيحة احترافية:** قم بتثبيت رقم الإصدار في بيئة الإنتاج لتجنب التغييرات المفاجئة غير المتوقعة.

## الخطوة 2: تحميل مصنف Excel الذي تريد تحويله

السطر الأول من الشيفرة يُنشئ كائن `Workbook` من ملف XLSX المصدر. قد يحتوي المصنف على أوراق عمل متعددة، مخططات، وأشكال TextBox.

```java
import com.aspose.cells.*;

public class ExportToPptx {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook that contains a TextBox
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*لماذا هذا مهم:* تحميل المصنف يتحقق من صحة تنسيق الملف ويجهز تمثيلًا في الذاكرة يمكن للمكتبة تحويله إلى صيغ أخرى.

## الخطوة 3: تهيئة خيارات الحفظ لإخراج PowerPoint

تستخدم Aspose.Cells الفئة `ImageOrPrintOptions` للتحكم في عملية العرض. ضبط `SaveFormat` إلى `PPTX` يُخبر المكتبة بإنشاء عرض تقديمي PowerPoint بدلاً من صورة.

```java
        // Set up save options to export as PPTX
        ImageOrPrintOptions saveOptions = new ImageOrPrintOptions();
        saveOptions.setSaveFormat(SaveFormat.PPTX);   // TextBoxes remain editable
```

*لماذا هذا مهم:* عندما يكون التنسيق `PPTX`، تقوم Aspose.Cells بإنشاء شريحة لكل صفحة قابلة للطباعة من ورقة العمل. تُترجم مربعات النص إلى أشكال PowerPoint تبقى قابلة للتحرير، وهو أمر أساسي للتعديل اللاحق.

## الخطوة 4: تصدير المصنف بالكامل (أو ورقة واحدة) إلى PPTX

يمكنك تصدير المصنف بالكامل، ورقة عمل محددة، أو حتى نطاق صفحات. المثال أدناه يحفظ المصنف بالكامل.

```java
        // Export the entire workbook (including the editable TextBox) to PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", saveOptions);
    }
}
```

إذا كنت تفضّل تحويل الورقة الأولى فقط، استبدل استدعاء `save` بـ:

```java
        // Export only the first worksheet
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G20");
        workbook.save("YOUR_DIRECTORY/output.pptx", saveOptions);
```

*لماذا هذا مهم:* التحكم في منطقة الطباعة يحدّ من عدد الشرائح المُولدة، مما يمكن أن يحسّن الأداء للمصنفات الكبيرة.

## الخطوة 5: تشغيل البرنامج والتحقق من النتيجة

قم بتجميع وتنفيذ الفئة:

```bash
mvn compile exec:java -Dexec.mainClass=ExportToPptx
```

بعد التنفيذ، افتح `output.pptx` في Microsoft PowerPoint أو أي عارض متوافق. يجب أن ترى:

* شريحة واحدة لكل صفحة قابلة للطباعة من ورقة العمل  
* جميع بيانات الخلايا، التنسيق، والرسوم البيانية تم إعادة إنتاجها كصور  
* أشكال TextBox محفوظة كمربعات نص PowerPoint قابلة للتحرير  

إذا ظهر TextBox كصورة ثابتة، تحقق مرة أخرى من أن `saveOptions.setSaveFormat(SaveFormat.PPTX)` مُعَدل بشكل صحيح. يعتمد سير عمل **export excel using java** على هذه العلامة للحفاظ على قابلية تحرير الأشكال.

## التعامل مع المصنفات الكبيرة واستهلاك الذاكرة

عند تحويل المصنفات التي تحتوي على أوراق عمل كثيرة أو رسومات عالية الدقة، قد يرتفع استهلاك الذاكرة. ضع في اعتبارك الاستراتيجيات التالية:

1. **زيادة حجم Heap في JVM** – شغّل البرنامج باستخدام `-Xmx2g` (أو أعلى) إذا واجهت `OutOfMemoryError`.  
2. **تحويل أوراق العمل بشكل فردي** – استخدم حلقة عبر `workbook.getWorksheets()` واحفظ كل ورقة في ملف PPTX منفصل.  
3. **تقليل دقة الصورة** – استخدم `saveOptions.setResolution(150)` لتقليل DPI؛ الإعداد الافتراضي هو 300 DPI.  

هذه التعديلات تضمن أن عملية **export excel to pptx** تتوسع لتناسب سيناريوهات المؤسسات.

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب | الحل |
|---------|-------|-----|
| يتحول TextBox إلى نص عادي | تم تعيين `SaveFormat` إلى `PDF` أو تنسيق نقطي آخر | استخدم `SaveFormat.PPTX` |
| الشرائح فارغة | لم يتم تعريف منطقة الطباعة وتحتوي ورقة العمل على محتوى غير قابل للطباعة | استدعِ `worksheet.getPageSetup().setPrintArea("A1:Z50")` |
| ملف الإخراج تالف | كتابة غير مكتملة بسبب خروج JVM مبكرًا | تأكد من إكمال `workbook.save` قبل إنهاء البرنامج |
| الأداء بطيء | مصنف كبير يحتوي على العديد من الرسوم البيانية | صدّر فقط الأوراق المطلوبة أو قلل الدقة |

معالجة هذه المشكلات مبكرًا توفر الوقت أثناء التكامل.

## توسيع التحويل: إضافة عنوان شريحة مخصص

يمكنك إدراج شريحة عنوان قبل المحتوى المُصدّر بإنشاء كائن `Presentation` جديد من مكتبة `aspose.slides` ودمج ملف PPTX الذي أنشأته Aspose.Cells.

```java
import com.aspose.slides.*;

public class MergeWithTitle {
    public static void main(String[] args) throws Exception {
        // First, generate the PPTX from Excel (as shown earlier)
        ExportToPptx.main(args);

        // Load the generated PPTX
        Presentation excelPresentation = new Presentation("YOUR_DIRECTORY/output.pptx");

        // Create a new presentation for the title slide
        Presentation finalPresentation = new Presentation();
        ISlide titleSlide = finalPresentation.getSlides().addEmptySlide(finalPresentation.getLayoutSlides().get_Item(0));
        titleSlide.getShapes().addAutoShape(ShapeType.Rectangle, 50, 150, 600, 100)
                .getTextFrame().setText("Quarterly Sales Report");

        // Append the Excel slides
        finalPresentation.getSlides().insertCloneAfter(titleSlide, excelPresentation.getSlides());

        // Save the combined file
        finalPresentation.save("YOUR_DIRECTORY/final_output.pptx", SaveFormat.Pptx);
    }
}
```

يوضح هذا المقتطف كيف يمكن أن يكون تحويل **excel workbook to powerpoint** جزءًا من خط أنابيب توليد PowerPoint أكبر.

## الكود الكامل لمحول مستقل

فيما يلي الفئة Java الكاملة الجاهزة للتنفيذ التي تُجري عملية **convert xlsx to powerpoint** الأساسية. احفظها باسم `ExportToPptx.java`.

```java
import com.aspose.cells.*;

public class ExportToPptx {
    public static void main(String[] args) throws Exception {
        // 1. Load the source Excel file
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Prepare PPTX save options – keep TextBoxes editable
        ImageOrPrintOptions saveOptions = new ImageOrPrintOptions();
        saveOptions.setSaveFormat(SaveFormat.PPTX);

        // 3. Export the workbook (or a specific worksheet) to PowerPoint
        workbook.save("YOUR_DIRECTORY/output.pptx", saveOptions);

        System.out.println("Conversion complete: output.pptx created.");
    }
}
```

قم بتجميع وتشغيل الفئة كما هو موضح في **الخطوة 5**. سيطبع الطرفية رسالة تأكيد بمجرد كتابة الملف.

## الخلاصة

قَدَّم لك هذا الدليل عملية **convert xlsx to powerpoint** باستخدام Aspose.Cells for Java. تعلمت كيفية:

* تحميل مصنف Excel يحتوي على TextBoxes  
* تعيين `ImageOrPrintOptions` الصحيح لإنتاج ملف PPTX  
* تصدير المصنف بالكامل أو الأوراق المحددة  
* التحقق من النتيجة وحل المشكلات الشائعة  
* توسيع التحويل بمحتوى PowerPoint إضافي  

مسلحًا بهذه المعرفة، يمكنك دمج تحويل Excel إلى PowerPoint في خطوط تقارير، مولدات عروض تقديمية آلية، أو أي سير عمل مبني على Java يتطلب **excel to powerpoint format**.

## الخطوات التالية

* استكشف **export excel using java** لتنسيقات أخرى مثل PDF أو HTML أو PNG.  
* اجمع المحول مع Aspose.Slides لإضافة المخططات أو الرسوم المتحركة أو ملاحظات المتحدث برمجيًا.  
* حسّن الأداء للتحويلات الجماعية بإعادة استخدام نسخة `Workbook` واحدة وبث الإخراج إلى `ByteArrayOutputStream`.  

لا تتردد في تجربة الشيفرة، تعديل خيارات الحفظ، ومشاركة نتائجك مع المجتمع. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تحويل Excel إلى PDF في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [تحويل Excel إلى تنسيق XPS باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-xps-aspose-cells-java/)
- [تحويل Excel إلى HTML باستخدام Aspose.Cells Java: دليل خطوة بخطوة](/cells/english/java/workbook-operations/excel-to-html-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}