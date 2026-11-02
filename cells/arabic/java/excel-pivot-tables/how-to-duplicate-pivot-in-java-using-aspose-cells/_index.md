---
category: general
date: 2026-09-18
description: كيفية تكرار جدول محوري في Java باستخدام Aspose.Cells – نسخ جدول محوري
  بين دفاتر العمل بسرعة وبشكل موثوق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: ar
lastmod: 2026-09-18
og_description: كيفية تكرار جدول محوري في جافا باستخدام Aspose.Cells. اتبع هذا الدرس
  الكامل لنسخ جدول محوري بين دفاتر العمل باستخدام كود جافا نظيف.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: نسخ جدول محوري في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية تكرار الجدول المحوري في Java باستخدام Aspose.Cells
url: /ar/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار Pivot في Java باستخدام Aspose.Cells

إذا كنت بحاجة إلى **كيفية تكرار Pivot** في تطبيق Java، يوضح لك هذا الدليل الخطوات الدقيقة. من خلال تحميل مصنف Excel، وتعريف نطاق خلايا الـ Pivot، ونسخ ذلك النطاق إلى مصنف جديد، يمكنك نقل جدول Pivot دون فقدان تعريفه أو بياناته.

نسخ جدول Pivot هو طلب شائع عندما تقوم بإنشاء تقارير، أرشفة تحليلات، أو تقسيم مصنف كبير إلى أجزاء معيارية. في هذا الدرس ستتعلم كيفية **نسخ النطاق بين المصنفات**، وكيفية **تحميل مصنف Excel Java**، وفروق **كيفية نسخ Pivot** بأمان.

سوف تنتهي ببرنامج Java جاهز للتنفيذ يكرر جدول Pivot من `Source.xlsx` إلى `PivotCopied.xlsx` باستخدام Aspose.Cells for Java.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* تثبيت JDK 8 أو أحدث.
* Maven (أو أداة بناء أخرى) لإدارة التبعيات.
* Aspose.Cells for Java الإصدار 23.10 أو أحدث. أضف تبعية Maven التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* مصنف مصدر (`Source.xlsx`) يحتوي على جدول Pivot في النطاق **A1:H30**.

## كيفية تكرار Pivot في Java

الفكرة الأساسية بسيطة:

1. **تحميل مصنف المصدر** – يمنحك ذلك إمكانية الوصول إلى ورقة العمل التي تحتوي على الـ Pivot.
2. **تحديد نطاق الخلايا** الذي يحيط بالـ Pivot.
3. **إنشاء مصنف وجهة** – ملف فارغ سيتلقى النطاق المنسوخ.
4. **نسخ النطاق** – Aspose.Cells يكرر تعريف الـ Pivot تلقائيًا.
5. **حفظ مصنف الوجهة** – لديك الآن ملف منفصل يحتوي على نفس الـ Pivot.

فيما يلي برنامج Java كامل وقابل للتنفيذ يتبع هذه الخطوات.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### لماذا يعمل هذا

* **Aspose.Cells** يتعامل مع جدول Pivot كجزء من مجموعة خلايا ورقة العمل. عندما تستدعي `copyRange`، تقوم المكتبة بنسخ ليس فقط قيم الخلايا بل أيضًا ذاكرة التخزين المؤقت للـ Pivot وتعريفه، وبالتالي يحتوي المصنف الجديد على نسخة كاملة الوظيفة.
* كائن `CopyOptions` يحتفظ افتراضيًا بالمعادلات، التنسيقات، والكائنات المضمنة. يمكنك تخصيصه (مثال، `setCopyColumnWidths(true)`) إذا كنت بحاجة إلى تحكم إضافي.

## نسخ النطاق بين المصنفات – نظرة أعمق

بينما المثال أعلاه ينسخ كتلة مستمرة واحدة، يمكن لـ `copyRange` التعامل مع أي مساحة مستطيلة. إذا كان الـ Pivot الخاص بك يمتد عبر نطاقات غير متجاورة، يمكنك استدعاء `copyRange` عدة مرات أو استخدام `Worksheet.copy` لتكرار الورقة بأكملها.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**نصيحة:** عند نسخ مصنفات كبيرة، فعّل `CopyOptions.setPreserveCellStyle(true)` لتجنب تكرار الأنماط غير الضرورية، مما يمكن أن يحسن الأداء.

## كيفية نسخ Pivot إلى مصنف – التعامل مع عدة Pivot

إذا كانت ورقة المصدر تحتوي على أكثر من Pivot واحد، يمكنك التكرار عبر جداول الـ Pivot في ورقة العمل ونسخ كل واحدة على حدة:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

هذه الطريقة تضمن أن كل Pivot يحتفظ باسمه الأصلي ومصدر البيانات الخاص به.

## تحميل مصنف Excel Java – الأخطاء الشائعة

* **فواصل مسار الملفات:** استخدم الشرطات المائلة (`/`) أو `File.separator` لجعل الكود مستقلاً عن النظام.
* **الترخيص المفقود:** Aspose.Cells يعمل في وضع التقييم، لكن الناتج سيحتوي على علامة مائية. سجّل ترخيصًا باستخدام `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` قبل تحميل المصنف لإزالة العلامة المائية.
* **الملفات الكبيرة:** للمصنفات التي يزيد حجمها عن 100 ميغابايت، فكر في استخدام `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` مع خيارات البث لتقليل استهلاك الذاكرة.

## ملخص المثال الكامل من البداية إلى النهاية

بجمع كل شيء معًا، إليك البرنامج النهائي الذي يمكنك نسخه ولصقه في بيئة التطوير المتكاملة (IDE) الخاصة بك:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**الناتج المتوقع:** بعد التنفيذ، يظهر `PivotCopied.xlsx` في الدليل المحدد. فتحه في Excel يُظهر نفس تخطيط جدول Pivot، الفلاتر، والبيانات كما في `Source.xlsx`. جميع الحقول المحسوبة والتنسيقات محفوظة.

## الأسئلة المتكررة

* **هل يعمل هذا مع صيغ Excel القديمة (.xls)؟**  
  نعم. Aspose.Cells يكتشف الصيغة تلقائيًا. استخدم `new Workbook("file.xls")` وتطبق نفس منطق النسخ.

* **ماذا لو كان الـ Pivot يشير إلى مصادر بيانات خارجية؟**  
  النسخة تحتفظ بالإشارة إلى مصدر البيانات الأصلي. إذا لم يتمكن بيئة الوجهة من الوصول إلى ذلك المصدر، سيظهر الـ Pivot أخطاء `#REF!`. لتجنب ذلك، قم بتحديث الـ Pivot بعد النسخ أو غيّر مصدر البيانات عبر `PivotTable.setDataSource(...)`.

* **هل يمكنني نسخ Pivot إلى اسم ورقة محدد؟**  
  بالتأكيد. بعد إنشاء ورقة العمل الوجهة، أعد تسميتها:

```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## الخلاصة

أنت الآن تعرف **كيفية تكرار جداول Pivot** في Java باستخدام Aspose.Cells، وكيف **نسخ النطاق بين المصنفات**، وأفضل الممارسات لـ **تحميل مصنف Excel Java**. باتباع عملية الخمس خطوات — التحميل، التعريف، إنشاء الوجهة، النسخ، والحفظ — يمكنك أتمتة إنشاء التقارير، أرشفة التحليلات، أو تقسيم المصنفات المعقدة دون فقدان وظيفة الـ Pivot.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **نسخ Pivot إلى مصنف** مع عدة أوراق، أو دمج الـ Pivot المكرر في خط معالجة بيانات أكبر باستخدام Apache POI للسيناريوهات غير Aspose. جرّب إعدادات `CopyOptions` المختلفة لضبط الأداء للمصنفات الضخمة.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء جداول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية تحديث مصدر جدول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [تجميع حقول Pivot في مصنفات Excel باستخدام Aspose.Cells for Java - دليل شامل](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}