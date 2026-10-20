---
category: general
date: 2026-07-03
description: تصدير صورة جدول محوري في Excel باستخدام Java. تعلم كيفية تعيين تنسيق
  الصورة PNG باستخدام Aspose.Cells خطوة بخطوة.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: ar
og_description: تصدير صورة جدول محوري في Excel باستخدام Java موضح. اتبع هذا الدرس
  لتعيين تنسيق الصورة PNG بسرعة وبشكل موثوق.
og_title: صورة جدول محوري في Excel – دليل Java لتصدير PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'صورة جدول محوري في إكسل: تصدير إلى PNG باستخدام جافا'
url: /ar/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – تصدير Pivot Table كملف PNG في Java

هل احتجت يومًا إلى تحويل **excel pivot table image** إلى PNG جاهز للمشاركة لكن لم تعرف من أين تبدأ؟ لست وحدك. في العديد من خطوط التقارير يكون Pivot Table هو النجم، بينما يرغب باقي الفريق في صورة ثابتة فقط. الخبر السار؟ ببضع أسطر من Java وAspose.Cells يمكنك **set image format png** والحصول على ما تحتاجه بالضبط.

في هذا الدليل سنستعرض العملية كاملة: تحميل ملف العمل، الحصول على أول Pivot Table، ضبط خيارات التصدير، وأخيرًا كتابة ملف PNG واضح إلى القرص. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع Java.

## ما ستتعلمه

- كيفية تحميل مصنف Excel من نظام الملفات.
- كيفية تحديد Pivot Table معين في ورقة العمل.
- الخطوات الدقيقة لـ **set image format png** للصورة المصدرة.
- المشكلات الشائعة (وجود عدة Pivot Tables، مجموعات بيانات ضخمة) وكيفية تجنبها.
- فئة Java جاهزة للتنفيذ يمكنك نسخها ولصقها.

### المتطلبات المسبقة

- Java 8 أو أحدث مثبتة.
- مكتبة Aspose.Cells for Java (أحدث نسخة حتى 2026‑07‑03).
- ملف Excel (`input.xlsx`) يحتوي على Pivot Table واحد على الأقل.
- إلمام أساسي بـ Maven أو Gradle لإدارة الاعتمادات.

---

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أولًا، تأكد من أن ملف JAR الخاص بـ Aspose.Cells موجود في مسار الـ classpath. إذا كنت تستخدم Maven، أضف ما يلي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

لـ Gradle، الأمر مشابه:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **نصيحة احترافية:** Aspose تقدم مفتاح تقييم مجاني لمدة 30 يومًا. سجّل في موقعهم، ثم أضف `License.setLicense("Aspose.Cells.lic");` في بداية برنامجك لفتح جميع الميزات.

## الخطوة 2: تحميل المصنف والوصول إلى Pivot Table

الآن سنفتح ملف Excel ونستخرج أول Pivot Table. الشيفرة أدناه تقوم بذلك، وهي مكتوبة بطريقة دفاعية—إذا لم يحتوي المصنف على أوراق عمل أو إذا كانت الورقة لا تحتوي على Pivot Table سنرمي استثناء واضح.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### لماذا هذه الخطوات مهمة

- **Loading the workbook** يمنحنا الوصول إلى هياكل البيانات الداخلية؛ Aspose.Cells يختصر عملية تحليل OpenXML منخفضة المستوى.
- **Accessing the worksheet** ضروري لأن Pivot Tables مرتبطة بورقة معينة. إذا كان لديك عدة أوراق، يمكنك التكرار عبر `wb.getWorksheets()` واختيار الورقة التي تحتوي على الـ Pivot المطلوب.
- **Retrieving the pivot table** هو جوهر العملية. `ws.getPivotTables().get(0)` يجلب الأول، لكن يمكنك أيضًا البحث بالاسم باستخدام `ws.getPivotTables().get("MyPivot")`.
- **Setting image format png** (الكلمة المفتاحية الثانوية) يخبر Aspose.Cells بأن يرسم النتيجة كملف PNG غير مضغوط. هذا التنسيق يحافظ على الخطوط والنصوص الحادة، وهو مثالي للتقارير.
- **Exporting with `toImage`** يكتب الملف في استدعاء واحد، مع معالجة التقسيم والقياس تلقائيًا.

## الخطوة 3: التحقق من النتيجة

بعد تشغيل البرنامج، انتقل إلى `YOUR_DIRECTORY` وستجد ملف `pivot.png`. افتحه بأي عارض صور—ستلاحظ خطوط الشبكة الحادة والتخطيط الدقيق كما هو في Excel. إذا بدت الصورة غير واضحة، زد قيمة DPI في `imgOpt.setResolution()`؛ 300‑600 تعمل جيدًا للصور ذات جودة الطباعة.

![excel pivot table image exported as PNG](excel-pivot-table-image.png "excel pivot table image exported as PNG")

*نص بديل للصورة:* **excel pivot table image تم تصديره كـ PNG**

## التعامل مع عدة Pivot Tables

ماذا لو احتوت ورقتك على أكثر من Pivot Table؟ المقتطف أعلاه يلتقط الأول فقط، لكن يمكنك التكرار:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

هذا الحلقة ستنتج `pivot_0.png`، `pivot_1.png`، إلخ، كل منها يمثل Pivot Table مختلف. تذكر **set image format png** مرة واحدة قبل الحلقة؛ يمكن إعادة استخدام نفس كائن `ImageOrPrintOptions`.

## الحالات الخاصة والنصائح

| الحالة | ما يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| **Pivot كبير (عدد كبير من الصفوف/الأعمدة)** | قد يصبح حجم PNG كبيرًا، مما يضغط على الذاكرة. | استخدم `imgOpt.setOnePagePerSheet(false)` لتقسيمه على عدة صفحات، أو قلل الـ DPI. |
| **صفوف/أعمدة مخفية** | Aspose يحترم الخصوصية؛ البيانات المخفية لن تظهر. | أظهرها برمجيًا باستخدام `ws.showRows(start, count, true)`. |
| **أنماط مخصصة (خطوط، ألوان)** | قد لا تُرسم بعض الخطوط المؤسسية إذا لم تكن مثبتة على الخادم. | دمج الخط داخل JVM أو استخدم الخطوط النظامية عبر `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **احتياج لتنسيق إخراج مختلف لاحقًا** | قد ترغب في JPEG أو BMP. | غيّر `imgOpt.setImageFormat(ImageFormat.JPEG)`—الكود يبقى نفسه، فقط قيمة الـ enum تتغير. |

## مثال كامل جاهز (نسخ‑لصق)

فيما يلي الفئة الكاملة، جاهزة للترجمة. الصقها في `PivotTableToPng.java`، عدّل المسارات، ثم نفّذ `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

شغّله، وستحصل على **excel pivot table image** محفوظًا كملف PNG—تمامًا ما وعد به الدليل.

---

## الخلاصة

غطّينا كل ما تحتاجه لت **export an excel pivot table image** باستخدام Java، وأظهرنا لك بالضبط كيف **set image format png** مع Aspose.Cells. من تحميل المصنف إلى معالجة الحالات الخاصة، الحل مختصر، موثوق، وجاهز للإنتاج.

ما الخطوة التالية؟ جرّب تصدير عدة Pivot Tables دفعة واحدة، جرّب إعدادات DPI مختلفة لأصول جاهزة للطباعة، أو غيّر التنسيق إلى JPEG للصور المهيأة للويب. يمكنك أيضًا استكشاف دمج PNG داخل تقرير PDF—Aspose.PDF يجعل ذلك سهلًا.

هل لديك تعديل في سير العمل أو عائق؟ اترك تعليقًا، وسنساعدك على حل المشكلة. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}