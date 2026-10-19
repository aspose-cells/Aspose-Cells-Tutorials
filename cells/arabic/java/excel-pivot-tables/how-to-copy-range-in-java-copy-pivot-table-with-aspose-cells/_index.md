---
category: general
date: 2026-06-30
description: كيفية نسخ نطاق في Java باستخدام Aspose.Cells – تكرار نطاق Excel، نسخ
  جدول محوري، وتحميل مصنف Excel بكفاءة.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: ar
og_description: كيفية نسخ النطاق في Java باستخدام Aspose.Cells. تعلم كيفية تكرار نطاق
  Excel، نسخ جدول محوري، وتحميل دفتر عمل Excel في دقائق.
og_title: كيفية نسخ النطاق في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: كيفية نسخ النطاق في جافا – نسخ جدول محوري باستخدام Aspose.Cells
url: /ar/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ نطاق في Java – نسخ جدول محوري باستخدام Aspose.Cells

هل تساءلت يومًا **عن كيفية نسخ نطاق** من مصنف Excel إلى آخر دون فقدان سلامة الجدول المحوري؟ لست وحدك. في العديد من خطوط تقارير البيانات تحتاج إلى *تكرار نطاق Excel* مع الحفاظ على منطق الجدول المحوري يوميًا. لحسن الحظ، تجعل Aspose.Cells for Java هذا الأمر سهلًا، وفي هذا الدرس سنستعرض مثالًا كاملاً قابلًا للتنفيذ يوضح لك أيضًا **كيفية تحميل مصنف Excel**، نسخ جدول محوري، وحفظ النتيجة.

بنهاية هذا الدليل ستحصل على برنامج Java مستقل يقوم بـ:

* تحميل مصنف موجود (`load excel workbook`);
* تحديد الخلايا الدقيقة التي تحتوي على جدول محوري;
* **نسخ الجدول المحوري إلى ورقة** في مصنف جديد تمامًا;
* حفظ الملف الجديد، جاهزًا للمعالجة اللاحقة.

بدون سكريبتات خارجية، بدون خطوات يدوية—فقط كود نقي.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود:

* Java 8 أو أحدث (الكود يعمل أيضًا مع Java 11+);
* مكتبة Aspose.Cells for Java (يمكنك الحصول عليها من Maven Central);
* ملفي Excel تجريبيين – أحدهما مصدر يحتوي على جدول محوري (`source.xlsx`) ومجلد هدف ستكتب فيه `copy-pivot.xlsx`.

هذا كل شيء. لا تحتاج إلى أدوات IDE معقدة؛ أي محرر نصوص مع `javac` يكفي.

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

أولًا، لنضيف المكتبة إلى المشروع. إذا كنت تستخدم Maven، أضف هذا الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

إذا لم تكن تستخدم Maven، قم بتحميل ملف JAR من موقع Aspose وضعه في مسار الـ classpath. بعد ذلك، أنشئ فئة Java جديدة باسم `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **نصيحة احترافية:** حافظ على نظافة مجلد `src/main/java` ومنح الفئة اسمًا ذا معنى؛ فهذا يسهل الصيانة المستقبلية.

## الخطوة 2: تحميل مصنف المصدر (`load excel workbook`)

الآن نقوم **بتحميل مصنف Excel** الذي يحتوي على الجدول المحوري الذي نريد نسخه. يأخذ مُنشئ `Workbook` مسار الملف، لذا تأكد من صحة المسار.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

لماذا نختار الورقة الأولى؟ في أغلب الحالات البسيطة يكون الجدول المحوري على الورقة الأولى، لكن يمكنك تغيير الفهرس أو استخدام اسم الورقة إذا لزم الأمر. هذه المرونة هي أحد أسباب تميز Aspose.Cells.

## الخطوة 3: تحديد النطاق الذي يحتوي على الجدول المحوري

عادةً ما يمتد الجدول المحوري على مجموعة من الخلايا. لنفترض أنه يغطي `A1:G20`. يمكنك تعديل العنوان ليتناسب مع بياناتك الفعلية.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

إذا لم تكن متأكدًا من العنوان الدقيق، افتح المصنف في Excel، حدد كامل الجدول المحوري، وانظر إلى صندوق الاسم. تذكر أن **تكرار نطاق Excel** يعمل بأفضل صورة عندما تستهدف المنطقة الدقيقة—بدون صفوف إضافية، بدون أعمدة مفقودة.

## الخطوة 4: إنشاء مصنف جديد للوجهة

نحتاج إلى مصنف جديد سيستقبل النطاق المنسوخ. هنا سنقوم **بنقل الجدول المحوري** إلى ورقة جديدة.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

في هذه المرحلة يكون مصنف الوجهة فارغًا، لكن Aspose.Cells يضيف تلقائيًا ورقة افتراضية، سنستخدمها كهدف.

## الخطوة 5: نسخ النطاق – يبقى الجدول المحوري سليمًا

هذه هي السطر السحري الذي **ينسخ الجدول المحوري** مع الحفاظ على جميع الروابط الداخلية حية.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

طريقة `copy` تأخذ معاملين: النطاق المصدر `Range` والنطاق الهدف `Range`. ببدء الهدف عند `A1`، نضع الجدول المحوري في نفس الموضع كما كان في المصدر. Aspose.Cells ينسخ ذاكرة التخزين المؤقت للجدول المحوري، لذا المصنف الجديد لا يزال يعرف كيفية تحديثه.

## الخطوة 6: حفظ المصنف الناتج

أخيرًا، اكتب الملف الجديد إلى القرص. يمكنك اختيار أي تنسيق تدعمه Aspose (`.xlsx`, `.xls`, `.csv`, إلخ). سنستمر مع `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

شغّل البرنامج، ويجب أن ترى مصنفًا جديدًا يحتوي على نفس تخطيط الجدول المحوري. افتحه في Excel—إذا سارت الأمور على ما يرام، ستتمكن من تحديث الجدول المحوري دون أخطاء.

### النتيجة المتوقعة

عند تنفيذ `CopyPivotDemo`، سيطبع الطرفية:

```
Pivot table successfully copied to copy-pivot.xlsx
```

فتح `copy-pivot.xlsx` سيظهر ورقة تبدو مطابقة تمامًا لمنطقة الجدول المحوري في المصدر، و**نقل الجدول المحوري إلى ورقة** يعمل كما الأصل.

## مثال كامل يعمل

فيما يلي الفئة Java الكاملة الجاهزة للتنفيذ والتي تجمع جميع الخطوات معًا. انسخها والصقها في IDE الخاص بك، عدل مسارات الملفات، وشغّلها.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **ملاحظة:** إذا كان جدولك المحوري يمتد على أكثر من ورقة، كرر خطوة النسخ لكل ورقة ذات صلة، أو استخدم `Workbook.copy` لاستنساخ أوراق العمل بالكامل.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان مصنف المصدر يحتوي على عدة أوراق؟

يمكنك التكرار عبر `sourceWorkbook.getWorksheets()` ونسخ كل نطاق ذي صلة. احرص فقط على الحفاظ على أسماء الأوراق نفسها في الوجهة إذا كنت بحاجة إلى الحفاظ على المراجع.

### هل يحتفظ الجدول المحوري المنسوخ بمصدر بياناته؟

نعم. Aspose.Cells ينسخ ذاكرة التخزين المؤقت للجدول المحوري مع النطاق، لذا يظل مصنف الوجهة يشير إلى مصدر البيانات الأصلي داخل نفس الملف. إذا نقلت البيانات لاحقًا إلى ورقة مختلفة، قد تحتاج إلى تحديث الجدول يدويًا.

### كيف يمكن نسخ جدول محوري يستخدم مصدر بيانات خارجي؟

عند استخدام مصدر بيانات خارجي، عليك أولًا دمج ذلك البيانات في مصنف الوجهة (مثلاً، نسخ نطاق البيانات المصدر) قبل نسخ الجدول المحوري. وإلا سيظهر الخطأ “#REF!”.

### هل يمكن نسخ الجدول المحوري دون البيانات المحيطة؟

بالطبع. ما عليك سوى تعديل `pivotRange` ليغطي فقط خلايا الجدول المحوري (عادةً الزاوية العليا اليسرى بالإضافة إلى منطقة البيانات). يمكنك أيضًا استخدام `sourceSheet.getPivotTables().get(0).getPivotTableArea()` للحصول على النطاق الدقيق برمجيًا.

## نصائح للمشاريع الواقعية

* **معالجة دفعات:** إذا كنت بحاجة إلى تكرار العملية على العشرات من المصنفات، ضع الكود أعلاه داخل دالة واستدعها داخل حلقة تتنقل عبر مجلد.
* **الأداء:** للملفات الكبيرة، أعد استخدام كائن `Workbook` واحد واستدع `Workbook.calculateFormula()` فقط بعد إتمام جميع النسخ.
* **معالجة الأخطاء:** احط منطق النسخ بكتل `try‑catch` وسجل `Exception.getMessage()`؛ Aspose يرمي `CellsException` للنطاقات غير الصالحة.

## الخلاصة

لقد غطينا **كيفية نسخ نطاق** في Java باستخدام Aspose.Cells، موضحين لك كيفية **تكرار نطاق Excel**، **نسخ جدول محوري**، و**تحميل مصنف Excel**—all in a tidy program. الخطوات بسيطة، والكود قابل للتنفيذ بالكامل، والنهج قابل للتوسع من عرض توضيحي لورقة واحدة إلى وظائف دفعات على مستوى المؤسسة.

هل أنت مستعد للتحدي التالي؟ جرّب تصدير الجدول المحوري المنسوخ إلى PDF، أو تحديثه برمجيًا بعد إضافة بيانات جديدة. كلا المهمتين يبنيان على الأساس الذي وضعناه هنا، لذا ستكون مجهزًا جيدًا للتعامل معهما.

هل لديك أسئلة أو ترغب بمشاركة تعديلاتك؟ اترك تعليقًا أدناه—برمجة سعيدة! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}