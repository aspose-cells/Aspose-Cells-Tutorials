---
category: general
date: 2026-11-25
description: تصدير Excel إلى SVG باستخدام Aspose.Cells في Java – دليل خطوة بخطوة لحفظ
  Excel كملف SVG وإنشاء صورة متجهة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: ar
lastmod: 2026-11-25
og_description: تصدير Excel إلى SVG باستخدام Aspose.Cells في Java. تعلّم كيفية حفظ
  Excel كملف SVG وإنشاء صور متجهة عالية الجودة ببضع أسطر من الشيفرة.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: تصدير Excel إلى SVG في Java – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: كيفية تصدير Excel إلى SVG باستخدام Aspose.Cells في Java
url: /ar/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى SVG باستخدام Aspose.Cells في Java

إذا كنت بحاجة إلى **تصدير Excel إلى SVG**، يوضح لك هذا الدليل كيفية القيام بذلك باستخدام Aspose.Cells للـ Java. ستتعلم كيفية **حفظ Excel كـ SVG** وإنشاء صورة **متجهة** عالية الجودة في بضع أسطر من الشيفرة فقط.

يتيح تصدير مصنف Excel إلى ملف SVG إمكانية تضمين الورقة في صفحات الويب أو التقارير أو أي بيئة تفضّل الرسومات القابلة للتوسيع. يحافظ تنسيق SVG على الخطوط والألوان وحدود الخلايا دون التشويش الذي تحصل عليه من الصور النقطية.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 17 أو أحدث مثبتة.
* ترخيص فعال لـ Aspose.Cells للـ Java (أو مفتاح تقييم مؤقت).
* مشروع Maven أو Gradle يمكنك من خلاله إضافة تبعية Aspose.Cells.

أضف مكتبة Aspose.Cells إلى مشروعك:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## تصدير Excel إلى SVG – خطوة بخطوة

تتكون العملية من ثلاث خطوات بسيطة: تحميل المصنف، ضبط خيارات تصدير SVG، وحفظ النتيجة. يتم شرح كل خطوة أدناه.

### الخطوة 1: تحميل المصنف الذي يحتوي على البيانات

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**لماذا هذا مهم:**  
`Workbook` هو الكائن المركزي في Aspose.Cells. تحميل الملف مرة واحدة يمنحك الوصول إلى جميع أوراق العمل، الأنماط، والكائنات المدمجة، والتي سيقوم مُصدّر SVG لاحقًا برسمها.

### الخطوة 2: إعداد خيارات تصدير الصورة لـ SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**لماذا هذا مهم:**  
`ImageOrPrintOptions` يتيح لك التحكم في تنسيق الإخراج. اختيار `ImageFormat.SVG` يضمن أن النتيجة تكون **صورة متجهة** بدلاً من صورة نقطية. تمكين `OnePagePerSheet` يمنع وجود فواصل صفحات داخل الورقة، وهو ما يكون عادةً مرغوبًا عندما يتم عرض SVG في عرض ويب.

### الخطوة 3: حفظ المصنف كملف SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**لماذا هذا مهم:**  
طريقة `save` تجمع بين المصنف المحمّل وخيارات `exportOptions` المكوّنة. تقوم العملية بكتابة ملف SVG متوافق بالكامل يمكن فتحه في المتصفحات أو Inkscape أو أي محرر يدعم الرسومات المتجهة.

## مثال كامل قابل للتنفيذ

جمع الخطوات الثلاث معًا يمنحك برنامجًا مستقلاً يمكنك تجميعه وتشغيله فورًا:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**الناتج المتوقع**

عند تشغيل البرنامج يتم طباعة:

```
Export complete: Excel saved as SVG.
```

ستجد الملف `WithVariationSelectors.svg` في `C:/Output`. فتح الملف في المتصفح يظهر ورقة العمل مُرسَّمة كرسومات قابلة للتوسيع، مع الحفاظ على النصوص والحدود وألوان الخلايا.

## الاختلافات الشائعة والحالات الخاصة

| الحالة | التعديل الموصى به |
|-----------|------------------------|
| **عدة أوراق عمل** | قم بالتكرار عبر `workbook.getWorksheets()` واستدعِ `save` لكل ورقة، مع إرفاق اسم الورقة إلى اسم الملف إذا رغبت. |
| **مصنفات كبيرة** | زد قيمة `exportOptions.setRenderThreadCount(int)` لاستخدام المعالجة المتوازية، مما يقلل من زمن التحويل. |
| **دقة DPI مخصصة** | استدعِ `exportOptions.setHorizontalResolution(int)` و `exportOptions.setVerticalResolution(int)` للتحكم في مقياس الـ viewBox الخاص بـ SVG. |
| **تضمين الخطوط** | عيّن `exportOptions.setExportFontAsSVG(true)` لتضمين تعريفات الخط مباشرة داخل SVG، مما يضمن الحفاظ على المظهر على الأجهزة التي لا تتوفر فيها الخطوط الأصلية. |
| **ملفات محمية بكلمة مرور** | قدّم كلمة المرور عند التحميل: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## نصائح احترافية

* **تجنب التحويل إلى نقطية** – إذا احتوت ورقة العمل على مخططات معقدة، تحقق من ظهورها كعناصر متجهة في SVG. إذا لم يحدث ذلك، فعّل `exportOptions.setExportChartAsSVG(true)`.
* **الأداء** – في عمليات التحويل الجماعية، أعد استخدام كائن `ImageOrPrintOptions` واحد بدلاً من إنشاء كائن جديد لكل ملف.
* **الاختبار** – تحقق من صحة SVG المُولَّد باستخدام أداة تحقق عبر الإنترنت (مثل أداة W3C SVG Validator) لاكتشاف أي أخطاء في العلامات مبكرًا.

## التحقق من التحويل

يمكنك التأكد برمجيًا من أن ملف الإخراج هو بالفعل SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

وجود عنصر الجذر `<svg>` يدل على نجاح عملية **تحويل Excel إلى SVG**.

## الخلاصة

يُظهر هذا الدليل كيفية **تصدير Excel إلى SVG** باستخدام Aspose.Cells للـ Java. من خلال تحميل المصنف، ضبط `ImageOrPrintOptions` لتكون بصيغة SVG، واستدعاء `save`، يمكنك **حفظ Excel كـ SVG** والحصول على تحويل نظيف من Excel إلى صورة متجهة. الآن يمكنك تضمين SVG في صفحات الويب، أو إدراجه في الوثائق، أو معالجته بمزيد من الأدوات المتخصصة في الرسومات المتجهة.

### ما الذي يمكنك استكشافه لاحقًا

* **تصدير Excel كـ PNG أو JPEG** – غيّر `exportOptions.setImageFormat(ImageFormat.PNG)` للحصول على إخراج نقطي.
* **تحويل Excel إلى PDF** – استخدم `PdfSaveOptions` لإنشاء مستندات قابلة للطباعة.
* **المعالجة الدفعية** – اجمع الشيفرة السابقة مع مراقب نظام ملفات لتقوم تلقائيًا **بتحويل Excel إلى SVG** لكل مصنف جديد يُضاف إلى مجلد معين.

لا تتردد في تجربة الخيارات المختلفة، ودع مرونة Aspose.Cells تحول بيانات Excel إلى أي تنسيق بصري تحتاجه. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel to SVG – Step‑by‑Step Java Guide](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}