---
category: general
date: 2026-11-22
description: تصدير Excel كصورة باستخدام Java و Aspose.Cells. تعلّم كيفية إضافة صورة
  إلى ورقة العمل وحفظ Excel كملف PNG في بضع خطوات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: ar
lastmod: 2026-11-22
og_description: تصدير ملف Excel كصورة باستخدام Java و Aspose.Cells. اتبع هذا الدليل
  لإضافة صورة إلى ورقة العمل وحفظ ملف Excel كملف PNG بسرعة.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: تصدير إكسل كصورة باستخدام جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: تصدير إكسل كصورة باستخدام جافا – دليل كامل
url: /ar/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel كصورة باستخدام Java – دليل شامل

إذا كنت بحاجة إلى **تصدير Excel كصورة** في تطبيق Java، يوضح لك هذا الدرس حلاً جاهزًا للتنفيذ. ستتعرف على كيفية إضافة صورة إلى ورقة العمل، وتكوين خيارات التصدير، وأخيرًا **حفظ Excel كملف PNG** ببضع أسطر من الشيفرة فقط.

يغطي الدليل كل شيء بدءًا من إعداد Maven وحتى معالجة الحالات الحدية، بحيث يمكنك دمج التقنية في أي مشروع يتطلب لقطات بصرية من جداول البيانات.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 17 أو أحدث مثبتة.
* Maven 3.6+ (أو Gradle) لإدارة التبعيات.
* ترخيص Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي للاختبار).
* ملف Excel تجريبي (`sample.xlsx`) يحتوي على البيانات التي تريد تصديرها.

## الخطوة 1: إضافة تبعية Aspose.Cells

توفر Aspose.Cells الفئة `ImageOrPrintOptions` المستخدمة لـ **تصدير Excel كصورة**. أضف التبعية التالية إلى ملف `pom.xml` الخاص بك (أو الإدخال المكافئ في Gradle).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** احرص على تحديث رقم الإصدار؛ الإصدارات الأحدث تتضمن تحسينات في أداء عرض الصور.

## الخطوة 2: تحميل المصنف واختيار ورقة العمل

الخطوة البرمجية الأولى هي فتح ملف Excel والحصول على مرجع لورقة العمل التي تريد تصديرها.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*لماذا هذا مهم*: يتيح لك تحميل المصنف الوصول إلى كائناته الداخلية، واختيار ورقة العمل الصحيحة يضمن أن النطاق المناسب هو الذي يتم عرضه.

## الخطوة 3: تكوين ImageOrPrintOptions (export excel as image)

تتحكم `ImageOrPrintOptions` في تنسيق الصورة، الدقة، وغيرها من تفاصيل العرض. هنا نضبط التنسيق إلى PNG، ما يلبي متطلب **تصدير ورقة Excel إلى PNG**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

ضبط التنسيق إلى `PNG` يضمن ضغطًا بدون فقد، مما يجعل الملف مناسبًا للمعالجة الإضافية أو الإدراج في التقارير.

## الخطوة 4: إضافة صورة إلى ورقة العمل (add picture to worksheet)

إذا احتجت إلى تضمين صورة—مثل شعار أو لقطة لنطاق آخر—استخدم مجموعة `Pictures`. الشيفرة التالية تُدرج صورة للنطاق `A1:G20` في الزاوية العليا اليسرى من ورقة العمل.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **لماذا قد تقوم بذلك:** إضافة صورة قبل التصدير تسمح لك بدمج الرسومات الثابتة مع بيانات ورقة العمل، مما ينتج صورة نهائية أغنى.

## الخطوة 5: حفظ ورقة العمل كملف PNG (save excel as png file, save workbook as image)

أخيرًا، استدعِ `Workbook.save` مع الخيارات المكوَّنة. تُكتب الطريقة ملف PNG إلى الدليل المحدد.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

عند انتهاء البرنامج، يحتوي `output/pivot.png` على تمثيل بكسلي دقيق للورقة، بما في ذلك الصورة التي أضفتها.

### ملف المصدر الكامل

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

تشغيل الفئة ينتج ملف PNG الموضح أدناه (الصورة توضيحية؛ ملفك سيعكس محتوى ورقة العمل الفعلي).

![Exported Excel worksheet as PNG](/images/excel-to-png.png "Result of export excel as image using Java")

*نص بديل (alt):* **نتيجة تصدير Excel كصورة باستخدام Java – لقطة PNG للورقة** (يُلبّي متطلبات النص البديل للصورة).

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|--------|-----|
| **الملف غير موجود** | المسار إلى `sample.xlsx` غير صحيح. | استخدم مسارًا مطلقًا أو ضع الملف في جذر المشروع. |
| **صورة فارغة** | الورقة لا تحتوي على محتوى مرئي أو نطاق الصورة فارغ. | تحقق من أن الخلايا `A1:G20` تحتوي على بيانات أو عدل النطاق. |
| **دقة منخفضة** | دقة DPI الافتراضية هي 96، وقد تظهر غير واضحة عند الطباعة. | استدعِ `opts.setResolution(300)` (أو أعلى) قبل الحفظ. |
| **استثناء الترخيص** | استخدام نسخة التقييم قد يضيف علامة مائية. | قم بتطبيق ترخيص Aspose.Cells صالح باستخدام `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **تصدير Excel كصورة**، يمكنك استكشاف ما يلي:

* **تصدير ورقة Excel إلى PNG** لكل ورقة عمل في المصنف (التكرار عبر `wb.getWorksheets()`).
* تحويل PNG إلى PDF باستخدام Aspose.PDF إذا كنت تحتاج إلى تنسيق ملائم للوثائق.
* تضمين PNG المُولد مباشرةً في صفحة ويب أو مرفق بريد إلكتروني من خلال Java.

هذه الامتدادات تبني على نمط `ImageOrPrintOptions` نفسه، مما يحافظ على اتساق قاعدة الشيفرة.

## الخلاصة

تعلمت كيفية **تصدير Excel كصورة** باستخدام Java، وكيفية **إضافة صورة إلى ورقة العمل**، وكيفية **حفظ Excel كملف PNG** باستخدام Aspose.Cells. يُظهر المثال الكامل طريقة موثوقة لـ **حفظ المصنف كصورة**، مع معالجة الدقة وتجنّب الأخطاء الشائعة. طبّق النمط لت automatisation التقارير، إنشاء صور مصغرة، أو دمج مرئيات الجداول في أي سير عمل مبني على Java.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}