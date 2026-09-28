---
category: general
date: 2026-09-11
description: إنشاء ورقة عمل جديدة ونسخ نطاق Excel باستخدام Aspose.Cells. تعلّم كيفية
  نسخ النطاق بين الأوراق مع الحفاظ على الجداول المحورية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: ar
lastmod: 2026-09-11
og_description: إنشاء ورقة عمل جديدة ونسخ نطاق Excel باستخدام Aspose.Cells. يوضح هذا
  الدليل الخطوات الدقيقة لنسخ النطاق بين الأوراق مع الحفاظ على جداول Pivot دون تغيير.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: إنشاء ورقة عمل جديدة ونسخ نطاق إكسل – دليل Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: إنشاء ورقة عمل جديدة ونسخ نطاق Excel باستخدام Aspose.Cells
url: /ar/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ورقة عمل جديدة ونسخ نطاق Excel باستخدام Aspose.Cells

إذا كنت بحاجة إلى **إنشاء ورقة عمل جديدة** ونقل البيانات داخل ملف Excel، فإن Aspose.Cells يجعل ذلك بسيطًا. يوضح هذا الدليل بالضبط كيفية نسخ نطاق Excel من ورقة إلى أخرى مع الحفاظ على أي جداول محورية داخل النطاق.

سوف تتعلم كيفية **copy excel range**، وكيفية **copy range between sheets**، ولماذا طريقة `copy` في Aspose.Cells تحافظ على تعريفات الجداول المحورية دون تغيير. لا تحتاج إلى أدوات خارجية—فقط مشروع Java مع مكتبة Aspose.Cells.

## المتطلبات المسبقة

- Java 17 أو أحدث مثبت
- Aspose.Cells for Java (الإصدار 23.12 أو أحدث) مضاف إلى مسار الفئة (classpath) في مشروعك
- دفتر عمل مصدر (`input.xlsx`) يحتوي على جدول محوري في النطاق الذي تريد نسخه
- إلمام أساسي بصياغة Java وإدارة الاعتمادات باستخدام Maven/Gradle

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

أنشئ مشروع Maven بسيط (أو Gradle إذا كنت تفضله) وأضف اعتماد Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

ثم استورد الفئات المطلوبة في ملف Java المصدر الخاص بك:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*لماذا هذه الخطوة مهمة*: استيراد الفئات الصحيحة يمنحك الوصول إلى `Workbook` و `Worksheet` و `Range` وطريقة `copy` التي ستتعامل مع نقل النطاق.

## الخطوة 2: تحميل دفتر العمل المصدر

افتح دفتر العمل الذي يحتوي على البيانات التي تريد نسخها. الكود التالي يحمل `input.xlsx` من الدليل الذي تحدده:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*شرح*: `Workbook` يمثل ملف Excel بالكامل. تحميله مرة واحدة يمنحك صلاحية القراءة/الكتابة على كل ورقة ومجموعة خلايا.

## الخطوة 3: تحديد النطاق المصدر الذي يتضمن الجدول المحوري

اختر ورقة العمل التي تحتوي على الجدول المحوري وحدد كتلة الخلايا الدقيقة التي تريد نسخها. في هذا المثال نقوم بنسخ الخلايا من A1 إلى D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*لماذا هذا مهم*: بإنشاء كائن `Range`، تخبر Aspose.Cells بالضبط أي الخلايا (بما في ذلك أي كائنات مدمجة مثل الجداول المحورية) يجب تكرارها.

## الخطوة 4: **Create new worksheet** التي ستستقبل البيانات المنسوخة

الآن نضيف ورقة جديدة إلى نفس دفتر العمل. هذه هي النقطة التي يظهر فيها الكلمة المفتاحية الأساسية:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*شرح*: إضافة ورقة جديدة تعزل البيانات المنسوخة، مما يجعل من السهل التحقق من نجاح عملية **copy excel range** دون التأثير على الورقة الأصلية.

## الخطوة 5: نسخ النطاق – يتم الحفاظ على الجدول المحوري تلقائيًا

استخدم طريقة `copy` لنقل النطاق من الورقة المصدر إلى ورقة الوجهة. تقوم Aspose.Cells بنسخ الصيغ، والتنسيق، وتعريفات الجداول المحورية:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*لماذا هذا يعمل*: طريقة `copy` تقوم بنسخ عميق للخلايا المصدر. لا تقوم بنسخ القيم فقط؛ بل تكرر هيكل الخلية بالكامل، بما في ذلك مخزن البيانات (pivot cache). لهذا يمكنك **copy range aspose.cells** ولا يزال بإمكانك رؤية جدول محوري فعال على الورقة الجديدة.

## الخطوة 6: حفظ دفتر العمل مع ورقة العمل الجديدة

أخيرًا، اكتب دفتر العمل المعدل إلى القرص:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*النتيجة*: `output.xlsx` الآن يحتوي على الورقة الأصلية بالإضافة إلى ورقة جديدة تسمى **Copy** تحتوي على نفس النطاق تمامًا، بما في ذلك الجدول المحوري.

## مثال كامل يعمل

بجمع جميع الأجزاء معًا، إليك البرنامج الكامل القابل للتنفيذ:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**الناتج المتوقع**: افتح `output.xlsx` في Excel. سترى ورقة تسمى **Copy** تحتوي خلاياها من A1 إلى D20 على نفس البيانات، التنسيق، وجدول محوري نشط مطابق للأصل.

## أسئلة شائعة وحالات حافة

- **ماذا لو كان النطاق المصدر يحتوي على خلايا مدمجة؟**  
  طريقة `copy` تنسخ أيضًا معلومات الدمج، لذا تظهر الخلايا المدمجة دون تغيير في ورقة الوجهة.

- **هل يمكنني النسخ إلى دفتر عمل مختلف؟**  
  نعم. حمّل نسخة ثانية من `Workbook`، أنشئ نطاق وجهة في ذلك الدفتر، واستدعِ `sourceRange.copy(destinationRange)`. الطريقة تتعامل مع النسخ عبر دفاتر العمل تلقائيًا.

- **ماذا لو كانت ورقة الوجهة تحتوي بالفعل على بيانات؟**  
  عملية النسخ تستبدل أي خلايا موجودة تتقاطع مع نطاق الوجهة. لتجنب فقدان البيانات، تأكد من أن منطقة الوجهة فارغة أو استخدم خلية بداية مختلفة (مثلاً، `"B2"`).

- **هل يتم تكرار مخزن البيانات (pivot cache)؟**  
  Aspose.Cells يعيد استخدام مخزن البيانات الأصلي، مما يعني أن الجدول المحوري الجديد يظل مرتبطًا بنفس بيانات المصدر. إذا كنت بحاجة إلى مخزن مستقل، يجب إعادة إنشاء الجدول المحوري بعد النسخ.

## نصائح وأفضل الممارسات

- **نصيحة احترافية**: استخدم `Workbook.setForceFormulaRecalculation(true)` قبل الحفظ إذا كان النطاق يحتوي على صيغ تعتمد على بيانات خارج الكتلة المنسوخة.
- **احذر من** النطاقات الكبيرة: نسخ أوراق ضخمة قد يستهلك ذاكرة كبيرة. فكر في النسخ على أجزاء أصغر إذا واجهت `OutOfMemoryError`.
- **نصيحة أداء**: عطل تحديث الشاشة (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) عند العمل مع ملفات كبيرة جدًا لتسريع عملية النسخ.

## الخلاصة

أنت الآن تعرف كيفية **create new worksheet** و **copy excel range** بين الأوراق باستخدام Aspose.Cells، مع الحفاظ على الجداول المحورية وجميع خصائص الخلايا. تتيح لك هذه التقنية تكرار كتل البيانات برمجيًا، بناء قوالب تقارير، أو إعادة هيكلة دفاتر العمل دون الحاجة إلى النسخ واللصق اليدوي.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **copy range aspose.cells** للعمليات عبر دفاتر العمل، أتمتة تحديث الجداول المحورية، أو تصدير الورقة المنسوخة إلى PDF. جرّب نطاقات مصدر مختلفة وأسماء أوراق لتناسب سيناريو الأتمتة الخاص بك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [نسخ الأشكال بين أوراق Excel باستخدام Aspose.Cells لـ .NET&#58; دليل كامل](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [نسخ الصور بين الأوراق في Excel باستخدام Aspose.Cells لـ Java&#58; دليل شامل](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}