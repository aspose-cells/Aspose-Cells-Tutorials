---
category: general
date: 2026-11-22
description: تحويل Excel إلى PowerPoint في Java باستخدام Aspose.Cells. تعلّم كيفية
  إنشاء PowerPoint من ملف Excel، وتصدير أوراق العمل كشرائح PPTX، وأتمتة العروض التقديمية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: ar
lastmod: 2026-11-22
og_description: تحويل Excel إلى PowerPoint في Java باستخدام Aspose.Cells. يوضح لك
  هذا الدليل كيفية إنشاء PowerPoint من ملف Excel وتصدير ملفات .xlsx إلى شرائح .pptx.
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: تحويل Excel إلى PowerPoint باستخدام Java – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: تحويل Excel إلى PowerPoint في Java – دليل خطوة بخطوة
url: /ar/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PowerPoint في Java – دليل خطوة بخطوة

إذا كنت بحاجة إلى **convert Excel to PowerPoint in Java**، يوضح لك هذا الدليل كيفية القيام بذلك باستخدام Aspose.Cells. سواء كنت تبني محرك تقارير أو تقوم بأتمتة عروض الشرائح، ستتعلم **create PowerPoint from Excel file** برمجيًا وتصدير كل ورقة عمل كشرائح PPTX قابلة للتحرير.

يغطي الدرس كل شيء من إعداد المشروع إلى حفظ العرض النهائي. في النهاية ستحصل على برنامج Java قابل للتنفيذ يحول مصنف `.xlsx` إلى ملف `.pptx` يمكنك تحريره في Microsoft PowerPoint. لا يلزم النسخ واللصق يدويًا.

## المتطلبات المسبقة

* Java 17 أو أحدث مثبت (الكود يستخدم نظام الوحدات الحديث).  
* رخصة Aspose.Cells for Java أو مفتاح تقييم مؤقت.  
* Maven أو Gradle لإدارة التبعيات (المثال يستخدم Maven).  
* مصنف Excel تجريبي (`input.xlsx`) موجود في دليل معروف.

> **نصيحة احترافية:** Aspose.Cells يدعم كل من `.xls` و `.xlsx`. يعمل نفس الكود مع أي من الصيغ؛ فقط غيّر امتداد الملف.

## الخطوة 1: إعداد مشروع Java لـ **convert Excel to PowerPoint**

أنشئ مشروع Maven جديد (أو أضفه إلى مشروع موجود) وضمّن تبعية Aspose.Cells:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

نفّذ `mvn clean install` لتنزيل المكتبة. إذا كان لديك ملف ترخيص (`Aspose.Total.lic`)، ضعّه في مجلد `src/main/resources`؛ سيقوم الكود بتحميله تلقائيًا.

## الخطوة 2: تحميل مصنف Excel

الخطوة الوظيفية الأولى في عملية **convert excel workbook to pptx slides** هي تحميل ملف المصدر. يمكن لـ Aspose.Cells فتح الملفات من نظام الملفات، أو من تدفق، أو حتى من مصفوفة بايت.

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**لماذا هذا مهم:** تحميل المصنف يتحقق من صحة تنسيق الملف ويجهز الهياكل الداخلية التي سيحولها Aspose.Cells لاحقًا إلى كائنات PowerPoint.

## الخطوة 3: تكوين خيارات الحفظ لـ **create PowerPoint from Excel file**

يستخدم Aspose.Cells `ImageOrPrintOptions` لتحديد تنسيق الإخراج عند التحويل إلى ملفات عرض. اضبط `SaveFormat` إلى `SaveFormat.PPTX` لإنشاء شرائح قابلة للتحرير.

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**لماذا هذا مهم:** علم `setOnePagePerSheet(false)` يخبر Aspose.Cells بمعالجة كل ورقة عمل كشرائح منفصلة، وهو السيناريو الأكثر شيوعًا عندما تقوم **convert Excel to PowerPoint** للعروض.

## الخطوة 4: حفظ المصنف كشرائح PPTX

الآن يمكنك كتابة العرض إلى القرص. طريقة `Workbook.save` تقبل مسار الإخراج والخيارات التي قمت بتكوينها.

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

عند فتح `editable.pptx` في Microsoft PowerPoint، سترى شريحة لكل ورقة عمل، مع جميع الخلايا معروضة كصناديق نصية وأشكال قابلة للتحرير. يمكنك تعديل الخطوط، الألوان، أو إضافة رسوم متحركة مباشرة في PowerPoint.

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

ويظهر الملف `editable.pptx` في الدليل المحدد، جاهز للتعديل اليدوي أو للمزيد من الأتمتة.

## الخطوة 5: التغييرات الشائعة وحالات الحافة

### تحويل أوراق محددة فقط

إذا كنت تريد **convert Excel workbook to PPTX slides** ولكن تستثني بعض أوراق العمل، قم بفلترتها قبل الحفظ:

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### معالجة المصنفات الكبيرة

في المصنفات التي تحتوي على العديد من الأوراق، قد يصبح استهلاك الذاكرة كبيرًا. استخدم `WorkbookSettings` لتمكين البث:

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### الحفاظ على الصيغ

يقوم Aspose.Cells بتقييم الصيغ قبل العرض. إذا كنت بحاجة إلى نص الصيغة الأصلي على الشريحة، اضبط `opts.setExportFormulas(true)`.

## الخطوة 6: التحقق من النتيجة برمجيًا (اختياري)

يمكنك تحميل ملف PPTX المُولد باستخدام Aspose.Slides لتأكيد أن عدد الشرائح يطابق عدد أوراق العمل:

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

هذا الفحص الإضافي مفيد في خطوط CI حيث تريد التأكد من نجاح التحويل.

## الخاتمة

أصبحت الآن تمتلك حلاً كاملاً وجاهزًا للإنتاج لـ **convert Excel to PowerPoint in Java**. يقوم البرنامج بتحميل مصنف `.xlsx`، ويضبط `ImageOrPrintOptions` لـ **create PowerPoint from Excel file**، ويحفظ النتيجة كشرائح PPTX قابلة للتحرير. من خلال تعديل الخيارات يمكنك ضبط الدقة، اختيار أوراق معينة، أو بث ملفات كبيرة، مما يجعل النهج مرنًا للعديد من سيناريوهات الأتمتة.

**الخطوات التالية**

- استكشف **java convert .xlsx to .pptx** أكثر بإضافة تخطيطات شرائح مخصصة باستخدام Aspose.Slides.  
- أتمتة معالجة دفعات متعددة من المصنفات باستخدام مراقب دليل بسيط.  
- اجمع هذا التحويل مع إنشاء مخططات مدفوعة بالبيانات لإنتاج عروض تقديمية ديناميكية.

لا تتردد في تجربة الإعدادات ومشاركة نتائجك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحويل Excel إلى PowerPoint باستخدام Aspose.Cells في Java](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells لـ .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [تحويل Excel إلى PowerPoint باستخدام Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}