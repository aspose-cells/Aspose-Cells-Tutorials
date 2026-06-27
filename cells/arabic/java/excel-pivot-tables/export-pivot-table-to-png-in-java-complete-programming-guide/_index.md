---
category: general
date: 2026-06-27
description: تصدير جدول محوري كصورة محورية في Excel باستخدام Java. تعلّم كيفية تعيين
  تنسيق PNG، وتكوين الخيارات، وحفظ الملف في بضع خطوات فقط.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: ar
og_description: تصدير جدول محوري كصورة محورية في Excel باستخدام Java. يوضح هذا الدليل
  كيفية تعيين تنسيق PNG وحفظ الصورة بثقة.
og_title: تصدير جدول محوري إلى PNG في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: تصدير جدول محوري إلى PNG في جافا – دليل برمجة كامل
url: /ar/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير جدول محوري إلى PNG في Java – دليل برمجي كامل

هل احتجت يومًا إلى **export pivot table** من مصنف Excel لكنك لم تكن متأكدًا من كيفية الحصول على ملف صورة نظيف؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند بناء لوحات التقارير. الخبر السار هو أنه ببضع أسطر من كود Java يمكنك تحويل أي جدول محوري إلى **Excel pivot image** واضح يُحفظ بصيغة PNG.  

في هذا الدرس سنستعرض العملية بالكامل: قراءة المصنف، تحديد أول جدول محوري، ضبط التصدير لتحديد **set PNG format**، وأخيرًا كتابة الصورة إلى القرص. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- كيفية تحميل ملف Excel باستخدام Aspose.Cells (أو Apache POI إذا كنت تفضل).
- استدعاءات API الدقيقة اللازمة لـ **export pivot table** كملف PNG.
- لماذا يهم ضبط صيغة الصورة وكيفية **set PNG format** بشكل صحيح.
- الأخطاء الشائعة—مثل التعامل مع جداول محورية متعددة أو أوراق عمل مفقودة—وكيفية تجنبها.
- مثال Java كامل جاهز للتنفيذ يمكنك نسخه‑ولصقه.

> **المتطلبات المسبقة**  
> • Java 17 أو أحدث (الكود يعمل مع إصدارات أقدم، لكن يُنصح بـ 17).  
> • مكتبة Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي).  
> • معرفة أساسية بملفات Excel وJava I/O.

---

## الخطوة 1: إضافة تبعية Aspose.Cells

إذا كنت تستخدم Maven، أدرج التبعية التالية في ملف `pom.xml` الخاص بك. وإلا، حمّل ملف JAR من موقع Aspose وأضفه إلى مسار الـ classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*نصيحة احترافية:* حافظ على توافق إصدارات المكتبة مع ملاحظات الإصدار الرسمية لتجنب الأخطاء غير المتوقعة.

## الخطوة 2: تحميل المصنف وتحديد جدول Pivot

أولاً نفتح ملف Excel، ثم نسترجع أول جدول محوري في أول ورقة عمل. إذا لم يحتوي المصنف على أي جداول محورية، نتوقف بأمان.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **لماذا هذه الخطوة مهمة** – كائن `PivotTable` هو نقطة الدخول لأي تصدير صورة. محاولة استدعاء `toImage` على جدول غير موجود ستؤدي إلى `NullPointerException`، لذا نتحقق من عدد الجداول أولًا.

## الخطوة 3: ضبط خيارات تصدير الصورة (Set PNG Format)

الآن ننشئ كائن `ImageOrPrintOptions` ونحدد صراحةً **set PNG format**. PNG غير مضغوط، ما يحافظ على وضوح خطوط الشبكة والخطوط.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*ملاحظة:* إذا كنت تحتاج JPEG بدلاً من ذلك، استبدل `ImageFormat.PNG` بـ `ImageFormat.JPEG`. نفس كائن الخيارات يعمل لكليهما.

## الخطوة 4: تصدير جدول Pivot كملف صورة

بعد إعداد الخيارات، نستدعي `toImage`. الطريقة تكتب الملف مباشرة، لذا لا تحتاج إلى تدفقات إضافية.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

تشغيل البرنامج ينتج ملفًا باسم `pivot.png` يبدو تمامًا مثل الجدول المحوري في Excel. افتحه بأي عارض صور للتحقق.

### النتيجة المتوقعة

```
Pivot table exported successfully to: C:/exports/pivot.png
```

ستطابق الصورة الناتجة التخطيط المعروض على الشاشة، بما في ذلك عرض الأعمدة، ارتفاع الصفوف، وأي تنسيق شرطي قمت بتطبيقه.

## التعامل مع جداول Pivot متعددة (متقدم)

ماذا لو احتوت ورقة العمل على عدة جداول محورية وتريد فقط أحدها؟ يمكنك التكرار عبر `ws.getPivotTables()` واختيار الجدول بالاسم:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*لماذا هذا مفيد*: في التقارير الواقعية غالبًا ما يكون لديك جدول ملخص بالإضافة إلى جدول تفصيلي. الاختيار بالاسم يمنع الكتابة فوق الجداول عن طريق الخطأ.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | الأعراض | الحل |
|------|----------|-----|
| **ورقة عمل مفقودة** | `IndexOutOfBoundsException` عند الوصول إلى `ws` | تحقق من `workbook.getWorksheets().getCount() > 0` قبل الفهرسة. |
| **لا توجد جداول Pivot** | فشل صامت أو صورة فارغة | استخدم فحص `ws.getPivotTables().getCount()` (انظر الخطوة 2). |
| **صيغة صورة خاطئة** | المخرجات تبدو ضبابية أو بها تشويش | دائمًا `setImageFormat(ImageFormat.PNG)` لإخراج غير مضغوط؛ تجنب JPEG للجداول النصية الكثيفة. |
| **مسار الملف غير قابل للكتابة** | `IOException` عند `toImage` | تأكد من وجود الدليل (`new File(outputPath).getParentFile().mkdirs()`). |

## نصيحة احترافية: تصدير إلى مصفوفة بايت لتطبيقات الويب

إذا كنت تبني خدمة ويب تُعيد PNG مباشرة إلى المتصفح، يمكنك الكتابة إلى `ByteArrayOutputStream` بدلاً من ملف:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

هذا يلغي الحاجة إلى ملفات مؤقتة ويسرّع الاستجابة.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل جاهز للنسخ‑واللصق والذي يتضمن جميع أفضل الممارسات التي تم مناقشتها.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

تشغيل هذه الفئة سيولد `pivot.png` داخل `C:/exports`. افتح الملف وسترى نسخة بصرية مطابقة تمامًا للجدول المحوري الأصلي—مثالي لتضمينه في التقارير، الرسائل الإلكترونية، أو صفحات الويب.

![Exported pivot table saved as PNG – example of an excel pivot image](https://example.com/images/pivot-export.png "export pivot table example")

*نص بديل للصورة:* **export pivot table example showing a PNG Excel pivot image**

---

## الخلاصة

لقد أظهرنا لك كيفية **export pivot table** من Excel إلى PNG عالي الجودة باستخدام Java. الخطوات الأساسية هي تحميل المصنف، تحديد الجدول المحوري، ضبط `ImageOrPrintOptions` لتحديد **set PNG format**، وأخيرًا استدعاء `toImage`.  

مع هذه المعرفة يمكنك الآن أتمتة توليد التقارير، تضمين لقطات Pivot في لوحات التحكم، أو تقديمها مباشرة عبر واجهة برمجة تطبيقات ويب. في الخطوة التالية قد تستكشف خيارات **excel pivot image** للتكبير، إضافة علامات مائية، أو حتى تحويل PNG إلى PDF لتقارير قابلة للطباعة.  

هل لديك أسئلة حول التعامل مع مصنفات أكبر أو التكامل مع Spring Boot؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}