---
category: general
date: 2026-09-08
description: كيفية نسخ النطاق في Java باستخدام Aspose.Cells – تعلم نسخ الجدول المحوري،
  تكرار الجدول المحوري، وتصدير الجدول المحوري مع الحفاظ على التنسيق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: ar
lastmod: 2026-09-08
og_description: كيفية نسخ النطاق في Java باستخدام Aspose.Cells. يوضح لك هذا البرنامج
  التعليمي كيفية نسخ جدول محوري، تكرار جدول محوري، وتصدير جدول محوري مع الحفاظ على
  التنسيق.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: كيفية نسخ النطاق في جافا – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية نسخ النطاق في جافا باستخدام Aspose.Cells
url: /ar/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ النطاق في Java باستخدام Aspose.Cells

إذا كنت بحاجة إلى **كيفية نسخ النطاق** في Java، فإن Aspose.Cells يجعل المهمة بسيطة. سواءً كنت تنقل مجموعة خلايا عادية أو جدول محوري كامل الميزات، تتولى المكتبة عملية النسخ مع الحفاظ على الصيغ، الأنماط، وذاكرة التخزين المؤقت للجدول المحوري. في هذا الدليل ستتعلم **نسخ الجدول المحوري**، **تكرار الجدول المحوري**، وحتى **تصدير الجدول المحوري** إلى مصنف جديد مع الحفاظ على جميع التنسيقات.

يغطي البرنامج التعليمي كل شيء من إعداد المشروع إلى خطوة التحقق النهائية، بحيث يمكنك تشغيل الكود فورًا بعد القراءة. لا توجد أدوات خارجية مطلوبة بخلاف Aspose.Cells for Java JAR.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- Java 17 (أو أي JDK مدعوم) مثبت ومُعد في بيئة التطوير المتكاملة الخاصة بك.
- Maven أو Gradle لإدارة الاعتمادات (الأمثلة تستخدم Maven).
- ملف Excel مصدر (`source.xlsx`) يحتوي على جدول محوري في النطاق `A1:H20`.
- إلمام أساسي ببرمجة Java.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

Aspose.Cells مكتبة تجارية، لكن نسخة تقييم مجانية متاحة. أضف الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **نصيحة احترافية:** إذا كنت تفضّل Gradle، فإن الإدخال المكافئ هو:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

إضافة الـ JAR يمنحك الوصول إلى الفئات `Workbook`، `Worksheet`، `Range`، و`CopyOptions` المستخدمة طوال هذا الدليل.

## الخطوة 2: تحميل المصنف المصدر واختيار الورقة الأولى

الجزء الأول من **كيفية نسخ النطاق** هو فتح المصنف الذي يحتوي على البيانات التي تريد نقلها.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **لماذا هذا مهم:** فتح المصنف يُنشئ تمثيلًا في الذاكرة يمكن للـ API التلاعب به دون لمس الملف الأصلي على القرص.

## الخطوة 3: تحديد النطاق الذي يحتوي على الجدول المحوري

الجدول المحوري يعيش داخل كتلة مستطيلة. يجب عليك تحديد تلك الكتلة حتى يعرف Aspose.Cells ما الذي سيُنسخ.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **ملاحظة:** طريقة `createRange` **لا** تنسخ أي شيء بعد؛ إنها فقط تُنشئ كائن `Range` يشير إلى الخلايا التي تنوي تكرارها.

## الخطوة 4: إنشاء مصنف جديد والحصول على ورقته الأولى

الآن أنشئ المصنف الوجهة حيث سيقع النطاق المنسوخ.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **لماذا مصنف جديد؟** استخدام ملف جديد يضمن عدم وجود أنماط مخفية أو نطاقات مسماة تتداخل مع عملية النسخ، وهو أمر مهم خاصةً عندما **تصدّر الجدول المحوري** إلى ملف منفصل.

## الخطوة 5: نسخ النطاق (بما في ذلك الجدول المحوري) إلى الورقة الوجهة

هذا هو جوهر **كيفية نسخ النطاق مع التنسيق**. كائن `CopyOptions` يخبر Aspose.Cells بالحفاظ على كل شيء: القيم، الصيغ، الأنماط، وذاكرة التخزين المؤقت للجدول المحوري.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **نسخ الجدول المحوري:** لأن النطاق المصدر يتضمن الجدول المحوري، يقوم الـ API تلقائيًا بتكرار ذاكرة التخزين المؤقت للجدول، وبالتالي تحتوي الورقة الجديدة على جدول محوري يعمل بالكامل ويتصرف تمامًا مثل الأصلي.

## الخطوة 6: حفظ المصنف الوجهة

أخيرًا، اكتب النتيجة إلى القرص.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

عند فتح `dest.xlsx`، سترى نسخة مطابقة تمامًا للجدول المحوري الأصلي، بما في ذلك تنسيقه، المقاطع، والحقول المحسوبة.

## النتيجة المتوقعة

- يحتوي `dest.xlsx` على ورقة تسمى **Sheet1**.
- الخلايا `A1:H20` تحتفظ بنفس البيانات والجدول المحوري كما في المصدر.
- جميع أنماط الخلايا (الخطوط، الألوان، الحدود) محفوظة.
- الجدول المحوري تفاعلي بالكامل؛ تحديثه يعكس البيانات الأساسية في النطاق المنسوخ.

## كيفية نسخ النطاق مع التنسيق – نظرة أعمق

المثال السابق يُظهر أبسط سيناريو، لكن قد تواجه تنوعات تتطلب نهجًا مختلفًا قليلًا.

### نسخ الجدول المحوري إلى مصنف موجود مسبقًا

إذا كنت بحاجة إلى **تكرار الجدول المحوري** داخل مصنف يحتوي بالفعل على بيانات، استخدم نفس استدعاء `copyRange` لكن وجهه إلى عنوان وجهة مختلف:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### تصدير الجدول المحوري فقط (دون البيانات المحيطة)

أحيانًا تريد فقط الجدول المحوري، وليس البيانات المصدر. حدد نطاق عرض الجدول المحوري عبر طريقة `getPivotTable` الخاصة به:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### الحفاظ على التنسيق الشرطي

قواعد التنسيق الشرطي هي جزء من مجموعة الأنماط. علم `PasteType.ALL` ينسخها بالفعل، لكن يمكنك أن تكون صريحًا:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### الحالات الخاصة واستكشاف الأخطاء

| الحالة | ما يجب مراقبته | الحل الموصى به |
|-----------|-------------------|-----------------|
| المصنفات المصدر والوجهة تستخدم إصدارات Excel مختلفة | قد لا تُعرض بعض ميزات الجدول المحوري الحديثة (مثل نموذج البيانات) بشكل صحيح | استخدم أحدث نسخة من Aspose.Cells واضبط `Workbook.setFileFormatType(FileFormatType.XLSX)` لكلا المصنفين |
| الجداول المحورية الكبيرة جدًا ( > 10 000 صف) تُسبب ضغطًا على الذاكرة | أخطاء نفاد الذاكرة أثناء النسخ | فعّل `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` قبل التحميل |
| الورقة الوجهة تحتوي بالفعل على نطاق مسمى بنفس اسم المصدر | تصادم الأسماء يؤدي إلى فشل `CopyOptions` | استدعِ `copyOptions.setIgnoreNameConflicts(true)` |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في فئة Java. يتضمن جميع الاستيرادات، معالجة الأخطاء، والتعليقات.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

شغّل البرنامج، ثم افتح `dest.xlsx` للتحقق من أن الجدول المحوري يعمل تمامًا كما الأصلي.

## الخلاصة

أنت الآن تعرف **كيفية نسخ النطاق** في Java باستخدام Aspose.Cells، بما في ذلك كيفية **نسخ الجدول المحوري**، **تكرار الجدول المحوري**، و**تصدير الجدول المحوري** مع الحفاظ على جميع التنسيقات. المكتبة تُجردك من تفاصيل XML الخاصة بـ Excel، مما يتيح لك التركيز على منطق الأعمال.

### الخطوات التالية

- استكشف **نسخ النطاق مع التنسيق** للرسوم البيانية والصور (استخدم `PasteType.PICTURES`).
- أتمتة المعالجة الدفعية: حلقة عبر ملفات مصدر متعددة ودمج جداولها المحورية في مصنف ملخص.
- دمج هذه التقنية مع Aspose.Slides لإنشاء تقارير PowerPoint تُضمّن الجدول المحوري المنسوخ.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحديث مصدر جدول Excel المحوري باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [تحسين تحميل الجداول المحورية في Java باستخدام Aspose.Cells – دليل شامل](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [كيفية نسخ الجدول المحوري في C# – تحويل Excel إلى PPTX، نسخ النطاق وإنشاء مربع نص](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}