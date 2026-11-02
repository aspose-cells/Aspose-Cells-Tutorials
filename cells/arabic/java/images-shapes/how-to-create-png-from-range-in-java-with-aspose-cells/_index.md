---
category: general
date: 2026-10-07
description: تعلم كيفية إنشاء PNG من نطاق وتصدير البيانات كـ PNG في Java. يوضح لك
  هذا الدليل كيفية حفظ صورة نطاق Excel باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: ar
lastmod: 2026-10-07
og_description: إنشاء PNG من نطاق في Java وتصدير البيانات كملف PNG باستخدام Aspose.Cells.
  اتبع هذا الدليل الكامل لحفظ صورة نطاق Excel على الفور.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: إنشاء PNG من نطاق في Java – دليل Aspose.Cells خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية إنشاء PNG من نطاق في Java باستخدام Aspose.Cells
url: /ar/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء PNG من نطاق في Java باستخدام Aspose.Cells

إذا كنت بحاجة إلى **إنشاء PNG من نطاق** في مصنف Excel، فإن هذا الدرس يوضح لك بالضبط كيفية القيام بذلك. بحلول نهاية الدليل، ستكون قادرًا على **تصدير البيانات كـ PNG**، حفظ صورة نطاق Excel، وإعادة استخدام الملف في التقارير أو صفحات الويب.

سترى برنامج Java كامل وقابل للتنفيذ يقوم بتحميل مصنف، اختيار الخلايا المطلوبة، تحويلها إلى PNG، وحفظ النتيجة على القرص. لا تحتاج إلى أدوات خارجية—Aspose.Cells يتولى كل شيء داخليًا.

## ما يغطيه هذا الدرس

* المتطلبات الأولية وإعداد Maven لـ Aspose.Cells
* تحميل مصنف يحتوي على جدول محوري أو أي نطاق بيانات
* تحديد نطاق الخلايا الدقيق الذي تريد تحويله
* تكوين خيارات الصورة لإخراج PNG
* تحويل النطاق وحفظ ملف PNG
* المشكلات الشائعة ونصائح للحصول على صور عالية الجودة

بعد إكمال هذه الخطوات، ستكون قادرًا على **تحويل ورقة العمل إلى PNG** لأي نطاق، سواء كان جدولًا بسيطًا أو مخططًا محوريًا معقدًا.

## المتطلبات المسبقة

* Java 17 أو أحدث (الكود يُترجم مع JDK 11+)
* Maven 3.6+ (أو Gradle إذا كنت تفضل)
* Aspose.Cells for Java 23.12 أو أحدث – أضف الاعتمادية الموضحة أدناه
* ملف Excel موجود (`PivotWithStyle.xlsx`) يحتوي على النطاق الذي تريد التقاطه

> **نصيحة احترافية:** إذا لم يكن لديك ترخيص، يمكنك طلب مفتاح تقييم مؤقت من Aspose. المكتبة تعمل في وضع التقييم دون الحاجة إلى إعدادات إضافية.

### اعتماد Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## الخطوة 1: تحميل المصنف الذي يحتوي على النطاق المستهدف

العملية الأولى هي فتح ملف Excel. تقوم Aspose.Cells بقراءة الملف إلى الذاكرة دون الحاجة إلى Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*لماذا هذا مهم*: تحميل المصنف يمنحك الوصول إلى أوراق العمل، الخلايا، وخصائص إعداد الصفحة اللازمة للتحويل.

## الخطوة 2: الوصول إلى ورقة العمل التي تحتوي على النطاق

معظم المصنفات تحتوي على ورقة افتراضية في الفهرس 0، لكن يمكنك أيضًا استخدام اسم الورقة.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

إذا كانت بياناتك موجودة في ورقة مختلفة، استبدل `0` بالفهرس المناسب أو استخدم `workbook.getWorksheets().get("SheetName")`.

## الخطوة 3: تحديد نطاق الخلايا الذي تريد تحويله

يمكنك تحديد أي مساحة مستطيلة باستخدام صيغة A1. في هذا المثال نلتقط `A1:D15`، والتي قد تكون جدولًا محوريًا أو كتلة بيانات عادية.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*حالة خاصة*: عندما يتضمن النطاق خلايا مدمجة، تقوم Aspose.Cells تلقائيًا بتوسيع الصورة لتشمل المنطقة المدمجة.

## الخطوة 4: إعداد خيارات صورة PNG

`ImageOrPrintOptions` يتيح لك التحكم في الصيغة، الدقة، وتفاصيل التحويل الأخرى. ضبط صيغة الحفظ إلى PNG يضمن جودة غير مضغوطة.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

زيادة DPI مفيدة عندما تحتوي الخلايا المصدرية على خطوط صغيرة أو مخططات مفصلة.

## الخطوة 5: تحديد منطقة التحويل إلى النطاق المحدد

عن طريق تعيين النطاق كمنطقة طباعة، تقوم Aspose.Cells بتحويل تلك الخلايا فقط وتجاهل باقي الورقة.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

إذا تخطيت هذه الخطوة، سيتم تحويل كامل ورقة العمل إلى صورة نقطية، مما قد يستهلك الذاكرة وينتج صورة أكبر.

## الخطوة 6: تحويل النطاق وإضافة الصورة إلى ورقة العمل (اختياري)

إذا رغبت في تضمين PNG المُولد مرة أخرى في المصنف (لأغراض المعاينة)، يمكنك إضافته كصورة. هذه الخطوة اختيارية في سيناريوهات التصدير البحتة.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*لماذا قد تقوم بذلك*: بعض سير العمل يتطلب أن تكون الصورة جزءًا من المصنف قبل التوزيع، مثل إنشاء تقرير قابل للطباعة يجمع بين الخلايا الأصلية والصور.

## الخطوة 7: حفظ ملف PNG على القرص

أخيرًا، احفظ الصورة إلى ملف. طريقة `save` تحترم الصيغة المحددة في `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

عند انتهاء البرنامج، سيحتوي `PivotImage.png` على لقطة دقيقة بكسلية للخلايا `A1:D15`.

### النتيجة المتوقعة

- ملف باسم `PivotImage.png` موجود في `YOUR_DIRECTORY`.
- الصورة تعرض التخطيط الدقيق، الخطوط، الألوان، والحدود من النطاق المحدد.
- إذا كان النطاق المصدر يحتوي على جدول محوري، فإن الصورة المصدرة تشمل نفس التنسيق والقيم المحسوبة كما هو معروض في Excel.

## التعامل مع السيناريوهات الشائعة

### تصدير نطاق غير متصل

Aspose.Cells لا يحول النطاقات المتقطعة إلى صورة واحدة. لتصدير مناطق متعددة، أنشئ صورًا منفصلة لكل نطاق وادمجها لاحقًا باستخدام مكتبة معالجة الصور (مثل ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### حفظ ورقة عمل كبيرة كـ PNG

تحويل ورقة كاملة تحتوي على آلاف الصفوف قد يستهلك ذاكرة كبيرة. يمكن التخفيف من ذلك عن طريق:

- تقليل DPI (`imageOptions.setResolution(72)`) للحصول على ملف أصغر.
- استخدام `setPageCount` لتحديد عدد الصفحات التي سيتم تحويلها.
- تصدير صفحة طباعة واحدة في كل مرة عبر `worksheet.getPageSetup().setPrintArea(...)`.

### الحفاظ على صيغ الخلايا

صورة PNG هي تنسيق نقطي؛ الصيغ لا تُحفظ. إذا كان المستهلكون اللاحقون يحتاجون إلى البيانات الأصلية، قم أيضًا بتصدير النطاق كـ CSV أو JSON باستخدام `Range.exportDataTable()`.

## مثال كامل وقابل للتنفيذ

فيما يلي فئة Java الكاملة التي يمكنك نسخها ولصقها في بيئة التطوير المتكاملة الخاصة بك. استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي على جهازك.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

شغّل البرنامج باستخدام `mvn compile exec:java` (أو أداة البناء التي تفضلها). بعد التنفيذ، افتح `PivotImage.png` للتحقق من النتيجة.

## الخلاصة

أنت الآن تعرف كيفية **إنشاء PNG من نطاق** في Java باستخدام Aspose.Cells، وبشكل فعال **تصدير البيانات كـ PNG** و**حفظ صورة نطاق Excel** لأي سيناريو تقارير أو مشاركة. الخطوات—تحميل المصنف، تحديد النطاق، تكوين خيارات الصورة، تعيين منطقة الطباعة، وحفظ الملف—تغطي سير العمل الكامل لـ **تحويل ورقة العمل إلى PNG** و**حفظ الخلايا كـ PNG**.

### الخطوات التالية

- جرب قيم `Resolution` المختلفة لتحقيق توازن بين الجودة وحجم الملف.
- استخدم `ImageOrPrintOptions.setTransparent(true)` إذا كنت بحاجة إلى PNG بخلفية شفافة.
- دمج صور نطاقات متعددة في ملف PDF واحد باستخدام `PdfSaveOptions` لتقارير متعددة الصفحات.
- استكشف التصدير إلى تنسيقات نقطية أخرى (JPEG, BMP) عن طريق تغيير `setSaveFormat`.

لا تتردد في تعديل هذا النمط للمخططات، الجداول، أو حتى أوراق العمل بالكامل. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}