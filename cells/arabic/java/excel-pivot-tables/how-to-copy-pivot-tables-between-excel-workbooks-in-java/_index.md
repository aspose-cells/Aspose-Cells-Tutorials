---
category: general
date: 2026-10-01
description: تعلم كيفية نسخ جداول المحور بين ملفات إكسل باستخدام جافا. يوضح هذا الدليل
  خطوة بخطوة أيضًا كيفية نسخ النطاق بين الملفات وتكرار نطاقات إكسل بأمان.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: ar
lastmod: 2026-10-01
og_description: كيفية نسخ جداول المحور بين مصنفات Excel باستخدام Java. اتبع هذا الدليل
  لنسخ النطاق إلى المصنف، وتكرار نطاقات Excel، والحفاظ على بيانات الجداول المحورية.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: كيفية نسخ الجداول المحورية بين ملفات Excel في Java – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: كيفية نسخ جداول المحور بين ملفات Excel في Java
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جداول Pivot بين دفاتر Excel في Java

إذا كنت بحاجة إلى **how to copy pivot** جداول من ملف Excel إلى آخر، فإن هذا الدليل يقدم لك حلاً جاهزًا للتنفيذ. بحلول نهاية الجملتين الأوليين ستعرف بالضبط أي استدعاءات API تحافظ على تعريف الـ Pivot أثناء نسخ نطاق البيانات.

سوف تتعلم أيضًا كيفية **copy range between workbooks**، **duplicate Excel range** objects، و**copy range to workbook** بأمان دون فقدان الصيغ أو التنسيق. لا تحتاج إلى أي سكريبتات خارجية—فقط مشروع Java واحد يستخدم Aspose.Cells for Java.

## المتطلبات المسبقة

* Java Development Kit 17 أو أحدث.
* Maven أو Gradle لإدارة التبعيات.
* ترخيص صالح لـ Aspose.Cells for Java (التقييم المجاني يعمل للاختبار).
* ملفا Excel: `source.xlsx` (يحتوي على جدول Pivot) و `destination.xlsx` فارغ (أو دع الكود ينشئه).

## الخطوة 1: إعداد مشروع Maven

أنشئ ملف `pom.xml` يتضمن Aspose.Cells. هذه التبعيات توفر لك الفئات `Workbook` و `Worksheet` و `Range` المستخدمة في المثال.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **نصيحة احترافية:** حافظ على تحديث نسخة Aspose.Cells؛ الإصدارات الأحدث تضيف دعمًا أفضل لهياكل Pivot Cache المعقدة.

## الخطوة 2: تحميل دفتر العمل المصدر الذي يحتوي على جدول Pivot

يظهر الكود الأول **how to copy excel** عن طريق تحميل ملف المصدر. يقوم مُنشئ `Workbook` بقراءة الملف بالكامل إلى الذاكرة، مع الحفاظ على جميع كائنات الأوراق، بما في ذلك الـ Pivot.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*لماذا هذا مهم:* تقوم Aspose.Cells بتخزين جداول Pivot كجزء من النموذج الداخلي للورقة. تحميل دفتر العمل يضمن توفر Pivot Cache للنسخ لاحقًا.

## الخطوة 3: تعريف النطاق الذي يتضمن جدول Pivot

قد يمتد جدول Pivot عبر عدة صفوف وأعمدة. في معظم الحالات يمكنك نسخ النطاق المستخدم بالكامل للورقة. طريقة `createRange` تنشئ كائن `Range` الذي سيتعامل معه عملية النسخ.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

إذا امتد الـ Pivot إلى ما بعد `H20`، قم ببساطة بتغيير سلسلة العنوان. هذه الخطوة هي جوهر معالجة **duplicate excel range**؛ كائن النطاق يعرف الصيغ والأنماط والصفوف المخفية.

## الخطوة 4: إنشاء دفتر عمل جديد سيستقبل النطاق المنسوخ

يمكنك إما البدء بدفتر عمل فارغ أو تحميل ملف وجهة موجود. هنا نقوم بإنشاء دفتر عمل جديد، وهو أنظف طريقة لـ **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **ملاحظة:** إذا كنت بحاجة إلى نسخ الـ Pivot إلى اسم ورقة محدد، أعد تسمية `destWs` باستخدام `destWs.setName("Report")` قبل اللصق.

## الخطوة 5: نسخ النطاق – Aspose.Cells يحافظ تلقائيًا على الـ Pivot

طريقة `copy` تنقل كل ما داخل النطاق المصدر، بما في ذلك تعريف الـ Pivot، الـ cache، والتنسيق. لا يلزم أي كود إضافي للحفاظ على عمل الـ Pivot.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*لماذا يعمل:* تعتبر Aspose.Cells الـ Pivot مجموعة من الخلايا المخفية والبيانات الوصفية المرتبطة بالنطاق. عند استدعاء `copy`، تقوم المكتبة بتكرار تلك البيانات الوصفية في دفتر العمل الهدف.

## الخطوة 6: حفظ دفتر العمل الوجهة

أخيرًا، احفظ النتيجة على القرص. الملف المحفوظ يحتوي على جدول Pivot مطابق يمكنك تحديثه أو تعديله مثل الأصلي.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

تشغيل البرنامج يطبع تأكيدًا وينتج ملف `destination.xlsx` يحتوي على Pivot كامل الوظيفة.

## مثال كامل قابل للتنفيذ

بجمع جميع الخطوات معًا، تبدو فئة Java الكاملة هكذا:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### النتيجة المتوقعة

* وحدة التحكم: `Pivot table copied successfully.`
* يفتح `destination.xlsx` في Excel مع جدول Pivot مطابق للجدول الموجود في `source.xlsx`. تحديث الـ Pivot يظهر نفس مصدر البيانات، مما يثبت أن **how to copy pivot** يعمل كما هو مقصود.

## التعامل مع الاختلافات الشائعة

### نسخ أوراق عمل متعددة

إذا كان مشروعك يتطلب نسخ عدة أوراق، قم بالتكرار عبر أوراق دفتر العمل وكرر الخطوات 2‑4 لكل ورقة. سيتم الحفاظ على الـ Pivot في كل ورقة بشكل مستقل.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### الحفاظ على اتصالات البيانات الخارجية

جداول Pivot التي تعتمد على مصادر بيانات خارجية تحتفظ بسلسلة الاتصال بعد النسخ. ومع ذلك، يجب أن يكون للملف الوجهة إمكانية الوصول إلى نفس مصدر البيانات. تحقق من الاتصال بفتح الـ Pivot وفحص علامة تبويب **Data**.

### التعامل مع الخلايا المدمجة

إذا كان النطاق المصدر يحتوي على خلايا مدمجة، تقوم Aspose.Cells بنسخ تخطيط الدمج تلقائيًا. ومع ذلك، تحقق من النتيجة إذا كان دفتر العمل الوجهة يستخدم عرض عمود افتراضي مختلف.

## أفضل الممارسات للنسخ الموثوق

| Practice | Reason |
|----------|--------|
| استخدام النطاق المستخدم الدقيق (`srcWs.getCells().getMaxDisplayRange()`) بدلاً من عنوان مشفر ثابت | يضمن تضمين الـ Pivot بالكامل وبيانات المصدر الخاصة به. |
| تطبيق الترخيص قبل العمليات الثقيلة | يمنع علامة مائية التقييم ويحسن الأداء. |
| تحديث الـ Pivot بعد النسخ (`pivotTable.refresh()`) إذا تغيرت بيانات المصدر | يضمن أن الوجهة تعكس أحدث القيم. |
| كتابة اختبارات وحدة تفتح دفتر العمل الوجهة وتتحقق من أن `pivotTable.getPivotFields().size()` يطابق المصدر | يكشف عن فقدان الحقول عن طريق الخطأ أثناء تغييرات الكود المستقبلية. |

## الخلاصة

أنت الآن تعرف **how to copy pivot** جداول بين دفاتر Excel في Java، بالإضافة إلى كيفية **copy range between workbooks**، **duplicate excel range**، و **copy range to workbook** مع الحفاظ على جميع التنسيقات والصيغ. يستخدم المثال Aspose.Cells، الذي ي abstracts التعامل منخفض المستوى مع XML المطلوب من قبل OpenXML SDK.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **updating pivot cache programmatically**، **exporting pivot data to CSV**، أو **creating pivot tables from scratch**. كل منها يبني على نفس المفاهيم التي تم توضيحها هنا.

برمجة سعيدة، ولا تتردد في تجربة نطاقات أكبر، أو عدة Pivot، أو تنسيقات مخصصة – النمط نفسه ينطبق على جميع السيناريوهات.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء جداول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية نسخ أعمدة متعددة في Excel باستخدام Aspose.Cells Java: دليل كامل](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [نسخ الصور بين الأوراق في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}