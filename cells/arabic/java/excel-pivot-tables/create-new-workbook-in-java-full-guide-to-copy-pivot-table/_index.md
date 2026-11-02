---
category: general
date: 2026-07-23
description: أنشئ مصنفًا جديدًا في جافا وتعلم كيفية نسخ جدول محوري، نسخ نطاق إكسل،
  وتصدير الجدول المحوري باستخدام Aspose.Cells في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: ar
lastmod: 2026-07-23
og_description: أنشئ مصنفًا جديدًا في Java وانسخ جدولًا محوريًا فورًا، وانسخ نطاق
  Excel، ثم صدّر الجدول المحوري باستخدام Aspose.Cells. اتبع هذا الدرس الكامل.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: إنشاء دفتر عمل جديد في جافا – نسخ جدول محوري خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: إنشاء دفتر عمل جديد في جافا – دليل كامل لنسخ جدول محوري
url: /ar/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل جديد في Java – دليل كامل لنسخ Pivot Table

هل تساءلت يومًا كيف **create new workbook** في Java مع الحفاظ على جدول Pivot Table معقد؟ لست الوحيد الذي يحك رأسه حيال ذلك. في العديد من تطبيقات التقارير تحتاج إلى نقل جدول محوري من ملف المصدر إلى دفتر عمل جديد، ربما لإرساله إلى عميل أو لإجراء حسابات إضافية. الخبر السار؟ ببضع أسطر يمكنك فعل ذلك تمامًا—دون الحاجة إلى النسخ واللصق اليدوي.

في هذا الدرس سنستعرض العملية بالكامل: تحميل ملف المصدر، تعريف النطاق الذي يحتوي على الجدول المحوري، **copying the Excel range**، إنشاء **new workbook**، وأخيرًا **exporting the pivot table** إلى ملف جديد. في النهاية ستحصل على برنامج Java مستقل وقابل للتنفيذ يجيب على سؤال “**how to copy pivot**” دون أي تخمين.

## المتطلبات المسبقة

- Java 17 أو أحدث (الكود يعمل مع أي JDK حديث)
- مكتبة Aspose.Cells for Java (نسخة تجريبية مجانية أو نسخة مرخصة)
- ملف عينة `source.xlsx` يحتوي على جدول Pivot Table في النطاق `A1:G20`
- بيئة تطوير متكاملة أو أداة بناء (Maven/Gradle) لإدارة ملف JAR الخاص بـ Aspose.Cells

هل لديك هذه المتطلبات؟ رائع—لنبدأ.

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

أولًا وقبل كل شيء، تحتاج إلى إضافة Aspose.Cells إلى مشروعك. إذا كنت تستخدم Maven، ضع هذه الاعتمادية في ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

إذا كنت تفضل Gradle، فإن المكافئ هو:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

بعد إضافة المكتبة إلى مسار الفئات (classpath)، استورد الفئات التي ستحتاجها:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells هي مكتبة تجارية، لكنها تقدم نسخة تجريبية كاملة الوظائف لمدة 30 يومًا تُضيف علامة مائية على الناتج—مثالية لتجربة هذا.

## الخطوة 2: تحميل دفتر العمل المصدر

الآن سنقوم بـ **create new workbook**، لكن أولًا نحتاج إلى المصدر الذي يحتوي على الجدول المحوري. هذه الخطوة هي الأساس لأي عملية **copy excel range** لأن كائن النطاق يعرف بالضبط أي الخلايا (بما في ذلك ذاكرة التخزين المؤقت للجدول المحوري) يجب نقلها.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

لماذا لا نقرأ النطاق مباشرةً؟ لأن بيانات التعريف للجدول المحوري موجودة في ذاكرة التخزين المؤقت للورقة، وتقوم Aspose.Cells تلقائيًا بتجميعها عند نسخ النطاق.

## الخطوة 3: تعريف النطاق الذي يحتوي على جدول Pivot Table

في العديد من الملفات الواقعية، يشغل الجدول المحوري كتلة مستطيلة. في هذا المثال سنفترض أنه يقع في `A1:G20`. يمكنك بالطبع تعديل العنوان ليتطابق مع تخطيطك الفعلي.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

إذا لم تكن متأكدًا من العنوان الدقيق، يمكنك استخدام `sourceSheet.getCells().getMaxDataRow()` و `getMaxDataColumn()` لحساب الحدود بشكل ديناميكي. هذه حيلة مفيدة عندما يتغير حجم الجدول المحوري مع مرور الوقت.

## الخطوة 4: **Create New Workbook** وورقة العمل الوجهة

هذه هي اللحظة التي نقوم فيها فعليًا بـ **create new workbook** التي ستستقبل المحتوى المنسوخ. فكر فيها كقماش فارغ ستلصق عليه الجدول المحوري.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

لماذا نبدأ بدفتر عمل فارغ؟ يضمن ذلك عدم وجود أنماط مخفية أو جداول محورية سابقة تتداخل مع النسخ، مما يمنحك نتيجة نظيفة جاهزة لـ **export pivot table**.

## الخطوة 5: نسخ جدول Pivot Table (والنطاق الأساسي له)

الآن نصل إلى جوهر الدرس: **copy pivot table**. تتعامل Aspose.Cells مع نسخ النطاق كنسخة عميقة، مما يعني أن ذاكرة التخزين المؤقت للجدول المحوري تنتقل مع الخلايا. لهذا السبب تقوم هذه السطر الواحد بالعمل الشاق.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

إذا تساءلت يومًا **how to copy pivot** دون فقدان وظائفه، فهذه هي الإجابة. الآن تحتوي ورقة الوجهة على جدول محوري يعمل بالكامل يمكنك تحديثه أو تعديله أو ببساطة تصديره.

### حالة خاصة: الحفاظ على إعدادات التحديث

أحيانًا يتم ضبط الجدول المحوري المصدر ليتم تحديثه عند الفتح. للحفاظ على هذا السلوك، يمكنك نسخ خيارات الجدول المحوري صراحةً:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

هذا المقتطف يضمن أن الجدول المحوري المنسوخ يتصرف تمامًا مثل الأصلي.

## الخطوة 6: حفظ دفتر العمل الوجهة – **Export Pivot Table**

أخيرًا، نقوم بـ **export pivot table** عن طريق حفظ دفتر العمل الجديد على القرص. يمكنك اختيار أي تنسيق تدعمه Aspose: XLSX، XLS، CSV، PDF، إلخ. في هذا الدليل سنستخدم XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

إذا كنت بحاجة لإرسال الملف عبر خدمة ويب، يمكنك كتابته إلى `ByteArrayOutputStream` بدلاً من مسار ملف—Aspose يجعل ذلك سهلًا.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك برنامج كامل جاهز للتنفيذ. لا تتردد في نسخه، لصقه، وتشغيله في بيئة التطوير المتكاملة الخاصة بك.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### المخرجات المتوقعة

عند تشغيل البرنامج، ستطبع وحدة التحكم:

```
Pivot table copied successfully!
```

وسيظهر الملف `copied_with_pivot.xlsx` في `YOUR_DIRECTORY`. افتحه في Excel، وسترى جدول Pivot Table كما هو، جاهز للتحديث أو التعديل.

## أسئلة شائعة & استكشاف الأخطاء

- **ماذا لو كان الجدول المحوري المصدر يمتد على أكثر من ورقة عمل؟**  
  ستحتاج إلى نسخ كل نطاق ذي صلة بشكل منفصل، ثم إعادة إنشاء الجدول المحوري على ورقة الوجهة باستخدام واجهات برمجة `PivotTable`.

- **هل يمكنني نسخ تخطيط الجدول المحوري فقط دون البيانات؟**  
  اضبط `sourceRange.setCopyDataOnly(false)` قبل النسخ. هذا يخبر Aspose بالحفاظ على الذاكرة المؤقتة دون البيانات المصدرية الأساسية.

- **هل هناك طريقة لنسخ الجدول المحوري إلى ملف CSV؟**  
  CSV لا يدعم الجداول المحورية، لكن يمكنك تصدير *نتيجة* الجدول المحوري عن طريق استدعاء `pivotTable.calculate()` ثم حفظ الورقة كملف CSV.

- **لماذا يفقد الجدول المحوري المنسوخ تنسيقه؟**  
  التنسيق موجود في مجموعة الأنماط. بعد النسخ، يمكنك استدعاء `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` لنقل الأنماط.

## الخلاصة

لقد أظهرنا لك الآن كيفية **create new workbook** في Java، **copy pivot table**، و**export pivot table**—كل ذلك باستخدام مثال شفرة نظيف وقابل لإعادة الإنتاج. من خلال تعريف **copy excel range** بدقة، والاستفادة من سلوك النسخ العميق في Aspose.Cells، والحفاظ على الإعدادات الاختيارية، يمكنك أتمتة أي مهمة نقل جدول محوري تقريبًا.

هل أنت مستعد للخطوة التالية؟ جرّب تغيير تنسيق الإخراج إلى PDF، أو كرّر العملية عبر ملفات مصدر متعددة لمعالجة عشرات الجداول المحورية دفعة واحدة. النمط نفسه ينطبق—فقط عدّل مسارات الملفات وعناوين النطاقات.

إذا واجهت أي مشكلة، اترك تعليقًا أدناه أو راجع وثائق Aspose.Cells للحصول على معلومات متقدمة حول معالجة الجداول المحورية. برمجة سعيدة، واستمتع بالوقت الذي وفرته بأتمتة تلك المهام المملة للنسخ واللصق!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء جداول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية تحديث مصدر جدول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات دفتر العمل](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}