---
category: general
date: 2026-07-14
description: نسخ جدول محوري بين دفاتر العمل باستخدام جافا. تعلم كيفية نسخ الجدول المحوري،
  نسخ نطاق إكسل، وتصدير الجدول المحوري في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: ar
lastmod: 2026-07-14
og_description: انسخ جدولًا محوريًا في Java بسرعة. يوضح هذا الدليل كيفية نسخ الجدول
  المحوري، نسخ نطاق Excel، وتصدير الجدول المحوري باستخدام Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: نسخ جدول محوري بين المصنفات – دليل أتمتة جافا
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: نسخ جدول محوري بين دفاتر العمل – دليل جافا خطوة بخطوة
url: /ar/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول Pivot بين دفاتر العمل – دليل Java الكامل

هل احتجت إلى **نسخ جدول Pivot** من دفتر عمل إلى آخر وتساءلت لماذا تُفشل حيل النسخ‑اللصق التقليدية في الحفاظ على التخطيط؟ لست وحدك. في العديد من خطوط تقارير البيانات يعيش الـ Pivot في ملف رئيسي، لكن العمليات اللاحقة تتطلب نسخة خفيفة الوزن.

في هذا الدليل سنستعرض طريقة نظيفة برمجية لتكرار الـ Pivot — دون الحاجة إلى أي تعديل يدوي. بنهاية القراءة ستعرف **كيفية نسخ Pivot**، وكيفية **نسخ نطاق Excel** بأمان، وحتى **تصدير جدول Pivot** إلى ملف جديد، كل ذلك باستخدام Aspose.Cells for Java.

## ما ستبنيه

- تحميل دفتر مصدر يحتوي بالفعل على جدول Pivot.  
- إنشاء (أو فتح) دفتر هدف.  
- تحديد النطاق الدقيق الذي يحتوي على الـ Pivot.  
- نسخ ذلك النطاق — بما في ذلك تعريف الـ Pivot — إلى دفتر العمل الجديد.  
- حفظ النتيجة بحيث يمكن للتطبيقات الأخرى فتحها دون فقدان أي حسابات.

بدون أدوات خارجية، بدون VBA، مجرد كود Java نقي يمكنك إدراجه في أي مشروع Maven أو Gradle.

## المتطلبات المسبقة

- Java 17 أو أحدث (الكود يعمل على Java 8+، لكن إصدارات JDK الأحدث تقدم أداءً أفضل).  
- Aspose.Cells for Java 23.9 أو أحدث — أضف الاعتماد من Maven Central.  
- ملفا Excel: `SourceWithPivot.xlsx` (يحتوي على الـ Pivot) وملف فارغ كبديل للنسخة.

إذا كنت جديدًا على Aspose.Cells، فإن المكتبة تُجرد تفاصيل OOXML منخفضة المستوى، مما يسمح لك بالتعامل مع الأوراق ككائنات Java عادية.

## الخطوة 1: إعداد المشروع

أولاً، أضف حزمة Aspose.Cells إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

أو، إذا كنت تستخدم Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **نصيحة محترف:** إذا كنت تستخدم بيئة تطوير مثل IntelliJ، دعها تستورد المكتبة تلقائيًا؛ سيوفر لك ذلك الكثير من الكتابة.

## الخطوة 2: تحميل دفتر المصدر

نحتاج إلى كائن `Workbook` يشير إلى الملف الذي يحتوي على الـ Pivot. يقوم المُنشئ بقراءة الملف بالكامل إلى الذاكرة، بحيث يمكنك العمل عليه دون اتصال.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

لماذا نحمله أولًا؟ لأن ذاكرة التخزين المؤقت للـ Pivot، وقائمة الحقول، وتخطيطه كلها مخزنة داخل الورقة. تحميل دفتر العمل إلى الذاكرة يضمن نسخ *التعريف* وليس القيم المعروضة فقط.

## الخطوة 3: إنشاء أو فتح دفتر الهدف

لديك خياران: بدءًا من دفتر عمل جديد تمامًا، أو فتح قالب موجود. هنا سننشئ دفترًا فارغًا، وهو السيناريو الأكثر شيوعًا عندما تحتاج إلى نسخة نظيفة.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

إذا قررت لاحقًا النسخ إلى ورقة محددة، استبدل `getWorksheets().get(0)` بالفهرس أو الاسم المناسب.

## الخطوة 4: تحديد النطاق الدقيق الذي يحتوي الـ Pivot

عادةً ما يشغل جدول Pivot كتلة مستطيلة. أكثر الطرق أمانًا هي تحديد الخلية العلوية اليسرى والسفلية اليمنى صراحة. في مثالنا، الـ Pivot يمتد من **A1** إلى **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **لماذا لا نستخدم `copyRows`؟**  
> `copyRows` ينسخ قيم الخلايا الخام لكنه يتجاهل ذاكرة التخزين المؤقت للـ Pivot. بنسخ النطاق بالكامل، يحافظ Aspose.Cells على بيانات الـ Pivot الوصفية، مما يسمح للهدف بالحفاظ على التفاعلية الكاملة.

## الخطوة 5: نسخ النطاق (بما في ذلك الـ Pivot) إلى الهدف

الآن يحدث السحر. طريقة `copy` تستنسخ كل شيء — القيم، الصيغ، التنسيقات، وكائن الـ Pivot نفسه — إلى الموقع المستهدف.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

إذا أردت اللصق في خلية مختلفة، غير `"A1"` إلى `"C5"` أو أي عنوان تفضله. تقوم الطريقة تلقائيًا بتعديل المراجع الداخلية بحيث يظل الـ Pivot يعمل.

## الخطوة 6: حفظ دفتر الهدف

أخيرًا، اكتب دفتر العمل الجديد إلى القرص. يمكن فتح الملف الناتج في Excel، LibreOffice، أو أي عارض جداول آخر، وسيعمل الـ Pivot تمامًا كما كان في المصدر.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### النتيجة المتوقعة

- يفتح `CopyPivotResult.xlsx` مع جدول Pivot كامل الوظائف ومطابق للأصل.  
- جميع أدوات التصفية، الفلاتر، والحقول المحسوبة تبقى سليمة.  
- لا فقدان للبيانات — تُحسب القيم عند تحديث الـ Pivot.

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تعديله |
|-----------|----------------|
| **النسخ إلى دفتر موجود** | حمّل دفتر الهدف بدلاً من إنشاء واحد جديد: `new Workbook("ExistingFile.xlsx")`. |
| **الـ Pivot يمتد بحجم غير معروف** | استخدم `Worksheet.getPivotTables().get(0).getPivotTableRange()` للحصول على العنوان الدقيق برمجيًا. |
| **الحفاظ على اتصالات البيانات** | بعد النسخ، استدعِ `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` لإبقاء الروابط الخارجية نشطة. |
| **تصدير جدول Pivot كملف CSV** | بمجرد النسخ، يمكنك استدعاء `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` — هذا يُسطّح قيم الـ Pivot فقط. |

> **احذر:** عندما يستخدم دفتر المصدر والهدف إعدادات لغة مختلفة، قد تتغير تنسيقات الأرقام. اضبط `setLocale` للدفتر إذا كنت تحتاج إلى اتساق.

## مثال عملي كامل (جميع الاستيرادات مشمولة)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

شغّل البرنامج، افتح `CopyPivotResult.xlsx`، وسترى نفس الـ Pivot تمامًا كما بدأته — جاهزًا لمزيد من التحليل أو التوزيع.

## ملخص

لقد عرضنا **كيفية نسخ Pivot** من دفتر عمل إلى آخر باستخدام Aspose.Cells for Java. شمل الشرح تحميل المصدر، تحديد **نطاق Excel للنسخ** بدقة، تنفيذ النسخ، وأخيرًا **تصدير جدول Pivot** إلى ملف جديد. من خلال التعامل مع النطاق بدلاً من الخلايا الفردية، نضمن أن ذاكرة التخزين المؤقت الداخلية للـ Pivot تنتقل معه، مما يحافظ على الديناميكية في التقرير.

## ما الذي يمكنك استكشافه لاحقًا

- **أتمتة التحديث**: جدولة عملية النسخ باستخدام مهمة Quartz حتى تظل ملفاتك اللاحقة محدثة.  
- **نسخ عدة Pivot**: تكرار عبر `sourceWorkbook.getWorksheets().get(0).getPivotTables()` ونسخ كل واحد إلى أوراق منفصلة.  
- **تطبيق الأنماط**: استخدم كائنات `Style` لتوحيد الخطوط والألوان عبر دفتر الهدف.  

إذا كان لديك أسئلة حول التعامل مع دفاتر عمل كبيرة أو الحفاظ على مصادر البيانات الخارجية، اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بحرية أتمتة Excel البرمجية!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}