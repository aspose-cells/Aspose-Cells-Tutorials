---
category: general
date: 2026-09-27
description: نسخ جدول محوري في جافا باستخدام Aspose.Cells – دليل خطوة بخطوة يوضح كيفية
  نسخ النطاق والحفاظ على تعريفات الجدول المحوري.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: ar
lastmod: 2026-09-27
og_description: نسخ جدول محوري في جافا باستخدام Aspose.Cells. اتبع هذا الدليل الكامل
  لنسخ النطاق باستخدام Aspose.Cells والحفاظ على تعريفات الجداول المحورية دون تغيير.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: نسخ جدول محوري في جافا – دليل سريع لـ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية نسخ جدول محوري في جافا باستخدام Aspose.Cells
url: /ar/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells

إذا كنت بحاجة إلى **نسخ جدول محوري** من مصنف إلى آخر، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for Java. الحل يعمل مع أي جدول محوري قمت بإنشائه، ويحافظ على تعريف الجدول المحوري دون الحاجة إلى إعادة إنشائه يدويًا.

سوف تتعلم كيفية تحميل ملف المصدر، تعريف النطاق الذي يحتوي على الجدول المحوري، نسخ ذلك النطاق إلى مصنف جديد، وأخيرًا حفظ النتيجة. يغطي الدليل أيضًا الأخطاء الشائعة، مثل الحفاظ على مصادر البيانات ومعالجة المصنفات الكبيرة.

## ما ستحتاجه

* Java 17 أو أحدث (الكود يتوافق مع JDK 8+ أيضًا)
* Aspose.Cells for Java 23.9 أو أحدث – الإصدار الأخير يقدم أكثر دعم موثوق به لـ **copy range aspose cells**
* ملف Excel مصدر يحتوي على جدول محوري (مثال: `SourceWithPivot.xlsx`)
* بيئة تطوير متكاملة أو أداة بناء (Maven/Gradle) يمكنها الإشارة إلى ملف JAR الخاص بـ Aspose.Cells

## الخطوة 1: تحميل المصنف المصدر الذي يحتوي على الجدول المحوري

الإجراء الأول هو فتح المصنف الذي يحتوي على الجدول المحوري الذي تريد نسخه. تحميل الملف يُنشئ تمثيلًا في الذاكرة لجميع أوراق العمل، الخلايا، وذاكرة التخزين المؤقت للجدول المحوري.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**لماذا هذا مهم:**  
Aspose.Cells يقرأ المصنف بالكامل، بما في ذلك أوراق ذاكرة التخزين المؤقت المخفية للجدول المحوري. إذا تخطيت هذه الخطوة، فإن عملية **نسخ جدول محوري** اللاحقة ستفقد مصدر البيانات الأساسي.

## الخطوة 2: إنشاء مصنف وجهة فارغ

بعد ذلك، أنشئ مصنفًا جديدًا سيستقبل الجدول المحوري المنسوخ. البدء بمصنف نظيف يجنب الكتابة فوق البيانات عن طريق الخطأ.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**نصيحة:** المصنف الافتراضي يحتوي على ورقة واحدة فارغة، وهو مثالي لعملية نسخ بسيطة. إذا كنت بحاجة إلى النسخ إلى اسم ورقة محدد، أعد تسمية `destWs` باستخدام `destWs.setName("TargetSheet")`.

## الخطوة 3: تعريف النطاق المصدر الذي يتضمن الجدول المحوري

الجدول المحوري يشغل كتلة مستطيلة من الخلايا. يجب عليك تحديد النطاق الدقيق؛ وإلا سيتم نسخ البيانات الخام فقط. في هذا المثال نفترض أن الجدول المحوري يشغل **A1:G20**، لكن يمكنك تعديل العنوان ليتطابق مع ملفك.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**لماذا هذا يعمل:**  
عند استدعاء `createRange` على مجموعة `Cells` في ورقة العمل، يقوم Aspose.Cells بتضمين تعريف الجدول المحوري، ذاكرته، وأي تنسيق. هذا هو جوهر **كيفية نسخ جدول محوري** بشكل صحيح.

## الخطوة 4: نسخ النطاق المحدد إلى ورقة الوجهة

الآن استخدم طريقة `copy` لتكرار النطاق. تقوم الطريقة بنسخ كل ما داخل النطاق، بما في ذلك تعريف الجدول المحوري، الصيغ، والأنماط.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**ملاحظة هامة:**  
إذا كنت تحتاج فقط إلى البيانات دون الجدول المحوري، يمكنك استخدام `srcRange.copyData`. ومع ذلك، للحصول على **نسخ جدول محوري** حقيقي، يجب نسخ النطاق بالكامل كما هو موضح أعلاه.

## الخطوة 5: حفظ مصنف الوجهة

أخيرًا، احفظ المصنف الجديد إلى القرص. الملف الناتج سيحتوي على جدول محوري يعمل بالكامل ومطابق للمصدر.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

تشغيل البرنامج ينتج ملف `CopyPivotResult.xlsx` بنفس تخطيط الجدول المحوري، الفلاتر، والحسابات كما في الملف الأصلي.

## النتيجة المتوقعة

عند فتح `CopyPivotResult.xlsx` في Excel:

* يظهر الجدول المحوري في **A1:G20** على الورقة الأولى.
* جميع حقول الصف/العمود، الفلاتر، وحقول القيم بحالة سليمة.
* تحديث الجدول المحوري يجدد نفس مصدر البيانات كما في المصنف المصدر (إذا كانت البيانات مدمجة).

## الحالات الخاصة والنصائح العملية

| Situation | How to handle it |
|-----------|------------------|
| **الجدول المحوري يمتد على أعمدة أكثر مما هو متوقع** | استخدم `srcWs.getPivotTables().get(0).getPivotTableArea()` للحصول على العنوان الدقيق برمجيًا. |
| **المصنف المصدر يحتوي على جداول محورية متعددة** | قم بالتكرار عبر `srcWs.getPivotTables()` ونسخ كل نطاق على حدة، مع تعديل عناوين الوجهة. |
| **المصنفات الكبيرة تسبب ضغطًا على الذاكرة** | فعّل `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` قبل تحميل المصدر. |
| **تحتاج إلى نسخ تعريف الجدول المحوري فقط، دون البيانات** | بعد النسخ، احذف صفوف البيانات المصدر في الوجهة باستخدام `destWs.getCells().deleteRows(startRow, count)`. |
| **ملف الوجهة يجب أن يحتفظ بالتنسيق الأصلي** | عيّن `CopyOptions` باستخدام `options.setPasteType(PasteType.ALL)` للحصول على نسخة ذات دقة كاملة. |

**نصيحة احترافية:** تحقق دائمًا من صحة النسخة المنسوخة للجدول المحوري عن طريق استدعاء `destWs.getPivotTables().get(0).refresh()` برمجيًا. هذا يضمن أن الذاكرة المؤقتة محدثة، خاصة عندما تكون بيانات المصدر موجودة في اتصال خارجي.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في بيئة التطوير المتكاملة الخاصة بك. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

تشغيل هذا الكود سيقوم **بن نسخ جدول محوري** بالضبط كما هو موضح، ويظهر أبسط طريقة لـ **copy range aspose cells** مع الحفاظ على وظيفة الجدول المحوري.

## الخلاصة

أنت الآن تعرف كيفية **نسخ جدول محوري** في Java باستخدام Aspose.Cells، بدءًا من تحميل المصنف المصدر وحتى حفظ ملف الوجهة. يغطي الدليل الخطوات الأساسية، ويوضح لماذا كل خطوة مهمة، ويتناول الحالات الخاصة الشائعة.  

بعد ذلك، قد ترغب في استكشاف:

* **كيفية نسخ جدول محوري** عبر أوراق عمل مختلفة داخل نفس المصنف
* استخدام **copy range aspose cells** لتكرار المخططات أو التنسيق الشرطي
* أتمتة تحديث الجدول المحوري بعد النسخ للحفاظ على تحديث البيانات

لا تتردد في تجربة نطاقات أكبر، جداول محورية متعددة، أو دمج هذه المنطق في خط أنابيب معالجة Excel أكبر. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [نسخ جدول محوري في Java – الحفاظ عليه، تصديره إلى PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [كيفية تحديث مصدر جدول محوري في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [معالجة جداول محورية في Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}