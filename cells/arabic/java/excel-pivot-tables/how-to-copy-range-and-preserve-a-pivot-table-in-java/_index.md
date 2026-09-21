---
category: general
date: 2026-09-21
description: تعلم كيفية نسخ النطاق في جافا مع الحفاظ على الجدول المحوري. يوضح لك هذا
  الدليل خطوة بخطوة كيفية تصدير الجدول المحوري بأمان.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: ar
lastmod: 2026-09-21
og_description: كيفية نسخ النطاق في جافا مع الحفاظ على جدول المحور. اتبع هذا الدليل
  الكامل لتصدير جداول المحور بأمان.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: كيفية نسخ النطاق والحفاظ على جدول محوري في جافا
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: كيفية نسخ النطاق والحفاظ على جدول محوري في جافا
url: /ar/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ النطاق والحفاظ على جدول محوري في Java

إذا كنت بحاجة إلى **how to copy range** التي تحتوي على جدول محوري، فإن هذا الدليل يوضح لك طريقة موثوقة للحفاظ على الجدول المحوري دون تغيير. يواجه العديد من المطورين مشكلة فقدان الجدول المحوري عند تصدير البيانات، لكن النهج أدناه يتيح لك **copy pivot table** البيانات دون كسر وظيفتها. بحلول نهاية هذا الشرح ستتمكن من **preserve pivot table** الهيكل، **export pivot table** الملفات، وفهم **how to preserve pivot** في سيناريوهات مختلفة.

المثال يستخدم Aspose.Cells for Java، مكتبة شهيرة لأتمتة Excel. لا يتطلب أي أدوات إضافية بخلاف بيئة تطوير Java القياسية.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 17 (أو أحدث) مثبتة.
* Maven أو Gradle لإدارة التبعيات.
* Aspose.Cells for Java (الإصدار 23.9 أو أحدث). أضف تبعية Maven التالية:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* دفتر عمل مصدر (`Source.xlsx`) يحتوي على الجدول المحوري الذي تريد نسخه.

## كيفية نسخ النطاق والحفاظ على الجدول المحوري دون تغيير

الفكرة الأساسية هي نسخ **النطاق** الذي يحيط بالجدول المحوري بالكامل—بما في ذلك مصدر البيانات—باستخدام `copyRange`. هذه الطريقة تنسخ كلًا من البيانات الخام وتعريف الجدول المحوري، مما يضمن أن دفتر العمل الوجهة يستقبل جدولًا محوريًا يعمل بالكامل.

### الخطوة 1: تحميل دفتر العمل المصدر

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*لماذا هذه الخطوة؟*  
تحميل دفتر العمل يمنحك الوصول إلى ورقة العمل التي تستضيف الجدول المحوري. فئة `Workbook` تمثل ملف Excel بالكامل، بينما توفر `Worksheet` عمليات على مستوى الخلايا.

### الخطوة 2: تحديد النطاق الذي يغطي الجدول المحوري

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*لماذا هذه الخطوة؟*  
الجدول المحوري ليس خلية واحدة؛ إنه يمتد على كتلة تشمل العناوين، صفوف البيانات، وذاكرة التخزين المؤقت للجدول المحوري. بتحديد نطاق يحتوي بالكامل على الجدول المحوري، تضمن أن `copyRange` سينسخ أيضًا الذاكرة المؤقتة الأساسية، وهو أمر ضروري لسلوك **preserve pivot table**.

### الخطوة 3: إنشاء دفتر عمل وجهة فارغ

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*لماذا هذه الخطوة؟*  
البدء بدفتر عمل نظيف يمنع التعارضات العرضية مع الأوراق أو النطاقات المسماة الموجودة. سيتلقى دفتر العمل الوجهة النطاق المنسوخ، وبالتالي **export pivot table** المحتوى.

### الخطوة 4: نسخ النطاق – يتم الحفاظ على الجدول المحوري

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*لماذا هذه الخطوة؟*  
`copyRange` تقوم بنسخ عميق: قيم الخلايا، التنسيق، وبيانات تعريف الجدول المحوري تُنقل. هذه العملية الحرجة تمكّنك من **copy pivot table** دون فقدان وظيفتها. كائن `CellArea` يحدد مكان وصول النطاق في ورقة الوجهة.

### الخطوة 5: حفظ دفتر العمل الوجهة

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*لماذا هذه الخطوة؟*  
الحفظ يُكمل عملية **export pivot table**. الملف الناتج (`DestWithPivot.xlsx`) يحتوي على جدول محوري يعمل بالكامل يمكنك فتحه في Excel أو Google Sheets أو أي عارض جداول آخر.

## التحقق من أن الجدول المحوري تم الحفاظ عليه

افتح `DestWithPivot.xlsx` في Excel وتحقق من التالي:

1. يظهر الجدول المحوري في نفس الموقع (A1:G20) كما هو في المصدر.
2. تحديث (Refresh) الجدول المحوري يحدّث البيانات بشكل صحيح، مما يثبت أن الذاكرة المؤقتة تم نسخها.
3. جميع التنسيقات (عرض الأعمدة، تنسيقات الأرقام) مطابقة للأصل.

إذا فشل أي من هذه الفحوصات، تحقق من أن النطاق المصدر يغلق بالكامل الجدول المحوري ومصدر بياناته. الخطأ الشائع هو اختيار نطاق لا يشمل الذاكرة المؤقتة للبيانات، ما يؤدي إلى جدول محوري معطوب.

## اعتبارات إضافية

### نسخ الجدول المحوري عبر إصدارات دفتر عمل مختلفة

يدعم Aspose.Cells ملفات `.xls` القديمة وكذلك تنسيق `.xlsx` الأحدث. يعمل نفس الكود بغض النظر عن امتداد الملف، مما يجعله حلاً عالميًا لـ **how to preserve pivot** عبر الإصدارات.

### الحفاظ على الجدول المحوري عند استخدام مصدر مُفلتر

إذا كان الجدول المحوري المصدر مُفلترًا، يتم نسخ حالة الفلتر أيضًا. إذا احتجت إلى إعادة تعيين الفلاتر في الوجهة، استدعِ `PivotTable.refreshData()` بعد النسخ:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### تصدير الجدول المحوري كصورة ثابتة

أحيانًا قد ترغب في نسخة ثابتة (قيمة فقط) بدلاً من جدول محوري حي. استبدل `copyRange` بـ `copyRange` متبوعًا بـ `pt.setEnableRefresh(false)` لتعطيل الحسابات اللاحقة.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### التعامل مع دفاتر عمل كبيرة

لدفاتر العمل التي تحتوي على العديد من الأوراق، قصر عملية النسخ على الورقة المحددة لتقليل استهلاك الذاكرة. استخدم `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` لضبط الأداء بدقة.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله. عدّل مسارات الملفات لتتناسب مع بيئتك.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**الناتج المتوقع**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

عند فتح `DestWithPivot.xlsx`، يجب أن ترى الجدول المحوري الأصلي يعمل بالكامل، مؤكدًا أنك نجحت في **how to copy range** مع **preserve pivot table**.

## الأخطاء الشائعة ونصائح احترافية

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| يظهر الجدول المحوري لكن يظهر أخطاء `#REF!` | تم إهمال ورقة الذاكرة المؤقتة المخفية أثناء النسخ | وسّع النطاق المصدر ليشمل الذاكرة المؤقتة بالكامل (عادةً الصفوف تحت الجدول) |
| حجم دفتر العمل الوجهة أكبر من المتوقع | `copyRange` ينسخ أيضًا التنسيق | استخدم `CopyOptions` لاستبعاد التنسيق إذا كان الحجم مصدر قلق |
| فشل التحديث مع “Data source not found” | دفتر العمل المصدر يستخدم اتصالات بيانات خارجية | كرّر الاتصال في الوجهة أو انسخ ورقة مصدر البيانات أولاً |

**نصيحة احترافية:** دائمًا نفّذ فحصًا سريعًا بـ `destWs.getPivotTables().size()` بعد النسخ. إذا كان العدد صفرًا، فهذا يعني أن النطاق لم يشمل تعريف الجدول المحوري وتحتاج إلى توسيعه.

## الخلاصة

في هذا الشرح أظهرنا **how to copy range** التي تحتوي على جدول محوري وضمان بقاء سلوك **preserve pivot table** دون تغيير. من خلال تحميل دفتر العمل المصدر، تحديد نطاق شامل، استخدام `copyRange`، وحفظ الملف الوجهة، يمكنك بثقة **export pivot table** البيانات والإجابة على سؤال **how to preserve pivot** في مشاريع Java.

الخطوات التالية التي قد تستكشفها تشمل:

* أتمتة النسخ لعدة أوراق (استخدم الكلمة المفتاحية الثانوية **copy pivot table** داخل حلقة).
* تحويل دفتر العمل المصدر إلى CSV مع الحفاظ على البيانات الخام (ما زال يُطبق منطق **preserve pivot table** على المصدر).

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}