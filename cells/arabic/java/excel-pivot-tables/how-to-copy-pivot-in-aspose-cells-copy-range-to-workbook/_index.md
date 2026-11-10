---
category: general
date: 2026-08-08
description: كيفية نسخ جدول محوري في Aspose.Cells ونسخ نطاق إلى المصنف باستخدام Java.
  تعلّم الخطوات الدقيقة لتكرار جدول محوري باستخدام CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: ar
lastmod: 2026-08-08
og_description: كيفية نسخ جدول محوري في Aspose.Cells ونسخ النطاق إلى مصنف باستخدام
  Java. اتبع هذا الدليل الكامل لتكرار جدول محوري باستخدام CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: كيفية نسخ الجدول المحوري في Aspose.Cells – نسخ النطاق إلى المصنف
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: كيفية نسخ Pivot في Aspose.Cells – نسخ النطاق إلى المصنف
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ Pivot في Aspose.Cells – نسخ النطاق إلى مصنف

إذا كنت بحاجة إلى **كيفية نسخ Pivot** في ملف Excel باستخدام Aspose.Cells، فإن هذا الدليل يوضح لك العملية الدقيقة. في نهاية البرنامج التعليمي ستتمكن من **نسخ النطاق إلى مصنف** مع الحفاظ على تعريف جدول Pivot.

المثال يستخدم Java، لكن نفس المفاهيم تنطبق على أي لغة .NET تعمل مع Aspose.Cells. لا توجد أدوات خارجية مطلوبة—فقط مكتبة Aspose.Cells for Java وبيئة تطوير أساسية.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* مجموعة تطوير جافا (JDK) 8 أو أحدث.
* Maven أو Gradle لإدارة التبعيات (المثال يستخدم Maven).
* Aspose.Cells for Java 23.9 (أو أحدث نسخة) مضافة إلى مشروعك.
* مصنف إدخال (`input.xlsx`) يحتوي على جدول Pivot واحد على الأقل في ورقة العمل الأولى.

وجود هذه العناصر جاهزة يمنع حدوث أخطاء وقت التشغيل عندما يصل الكود إلى المصنف.

## كيفية نسخ Pivot باستخدام Aspose.Cells

يستعرض هذا القسم كل خطوة مطلوبة لـ **كيفية نسخ Pivot** من جزء من الورقة إلى آخر، باستخدام الفئة `CopyOptions`.

### الخطوة 1: إضافة Aspose.Cells إلى مشروعك

إذا كنت تستخدم Maven، أضف التبعية التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*لماذا هذه الخطوة مهمة*: المكتبة توفر الفئات `Workbook` و `CopyOptions` وغيرها المطلوبة لعمليات **aspose.cells copy range**. بدون هذه التبعية لا يستطيع المترجم حل هذه الأنواع.

### الخطوة 2: تحميل مصنف المصدر

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

تحميل الملف ينشئ تمثيلاً في الذاكرة للجدول الإلكتروني. كائن `Workbook` يمنحك الوصول إلى أوراق العمل، الخلايا، وجداول Pivot.

### الخطوة 3: تكوين خيارات النسخ لتضمين جدول Pivot

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` يخبر Aspose.Cells بأن العملية يجب أن تحتفظ ببيانات تعريف جدول Pivot. إذا حذفت هذه العلامة، سيتحول جدول Pivot إلى بيانات ثابتة، مما يفقده التفاعلية.

### الخطوة 4: نسخ النطاق المطلوب مع جدول Pivot

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

طريقة `copyRange` تنسخ الخلايا، التنسيق، و—بسبب الخيارات المحددة في الخطوة السابقة—أي جداول Pivot تتقاطع مع النطاق. هذه هي جوهر وظيفة **copy range to workbook**.

### الخطوة 5: حفظ المصنف المعدل

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

الحفظ يكتب التغييرات إلى ملف جديد (`output.xlsx`). يمكنك الآن فتح هذا الملف في Excel ورؤية أن جدول Pivot تم نسخه تمامًا إلى المكان الذي تم فيه نسخ النطاق.

## مثال كامل قابل للتنفيذ

بجمع جميع الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك تجميعه وتشغيله:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### النتيجة المتوقعة

* `output.xlsx` يحتوي على نفس البيانات مثل `input.xlsx`.
* جدول Pivot الذي كان يشغل النطاق المصدر يظهر في خلايا الوجهة، ويعمل بالكامل (مرشحات، قدرة التحديث، إلخ).
* جميع تنسيقات الخلايا، الصيغ، وعرض الأعمدة محفوظة لأن `copyRange` ينسخ كامل كتلة الخلية.

## أسئلة شائعة وحالات خاصة

**ماذا لو كان النطاق الهدف يتداخل مع جدول Pivot موجود؟**  
ستقوم Aspose.Cells بالكتابة فوق الخلايا المستهدفة. لتجنب فقدان البيانات، تأكد من أن منطقة الوجهة فارغة أو انقل جدول Pivot الموجود أولاً.

**هل يمكنني نسخ جدول Pivot عبر أوراق العمل؟**  
نعم. استخدم `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` حيث يشير `targetSheetIndex` إلى ورقة الوجهة.

**هل `setCopyPivotTable(true)` ينسخ مصدر البيانات الأساسي؟**  
الطريقة تنسخ فقط إشارة مخزن Pivot. إذا كان مصدر البيانات في نفس المصنف، فإن Pivot الوجهة سيشير إلى نفس المخزن. لتكرار المخزن، يجب إنشاء مخزن Pivot جديد يدويًا.

**كيف يمكن نسخ نطاق كبير بكفاءة؟**  
عند نسخ نطاقات كبيرة جدًا، فكر في استخدام `CopyOptions.setCopyFormula(true)` و `setCopyDataValidation(true)` فقط إذا لزم الأمر. تقليل عدد الخيارات يمكن أن يحسن الأداء.

## نصائح لاستخدام **aspose.cells copy range** بشكل موثوق

* **نصيحة احترافية:** دائمًا استدعِ `workbook.calculateFormula()` بعد النسخ إذا كان النطاق يحتوي على صيغ تعتمد على مخزن Pivot.
* **احذر من:** أوراق العمل المخفية. `copyRange` يعمل فقط على أوراق العمل المرئية ما لم تقم بالإشارة صراحةً إلى الورقة المخفية بواسطة الفهرس.
* **تحقق من الإصدار:** علامة `setCopyPivotTable` متاحة بدءًا من Aspose.Cells 20.9. تأكد من أن نسخة المكتبة التي تستخدمها تدعمها.

## الخلاصة

أنت الآن تعرف **كيفية نسخ Pivot** في Aspose.Cells وكيفية **نسخ النطاق إلى مصنف** مع الحفاظ على كامل وظائف Pivot. الخطوات—إضافة المكتبة، تحميل المصنف، تكوين `CopyOptions`، تنفيذ النسخ، والحفظ—تشكل نمطًا قابلاً للتكرار يمكنك تطبيقه على سيناريوهات النسخ واللصق الأخرى.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **aspose.cells copy range** للمخططات، التنسيق الشرطي، والتحقق من البيانات. جرب النسخ بين صيغ ملفات مختلفة (XLSX → XLS) لتوسيع قدرات الأتمتة لديك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء جداول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية تحديث مصدر جدول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [كيفية تنفيذ مقاطع (Slicers) في جداول Pivot باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}