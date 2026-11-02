---
category: general
date: 2026-07-06
description: كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells – دليل خطوة بخطوة
  لتكرار جداول Pivot في Excel برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: ar
lastmod: 2026-07-06
og_description: كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells يتيح لك تكرار جداول
  Excel المحورية بسرعة وموثوقية.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: كيفية نسخ جدول محوري في جافا – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: كيفية نسخ جدول محوري في جافا باستخدام Aspose.Cells
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells

هل تساءلت يومًا **كيفية نسخ الجداول المحورية** داخل ملف Excel دون فتح المصنف يدويًا؟ لست وحدك. في العديد من خطوط تقارير البيانات تحتاج إلى **تكرار جداول Excel المحورية** بسرعة—ربما لإنشاء لقطة، أو لنقلها إلى ورقة جديدة، أو لإنشاء قالب للمستخدمين اللاحقين.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ يوضح ذلك بالضبط. باستخدام مكتبة Aspose.Cells for Java سنقوم بتحميل مصنف، وتحديد نطاق الجدول المحوري المصدر، ونسخه إلى موقع جديد، ثم حفظ النتيجة. لا مراجع غامضة، بل حل ملموس يمكنك إدراجه في مشروعك اليوم.

---

## المتطلبات المسبقة

* **Java Development Kit (JDK) 8+** – يُترجم الكود مع أي JDK حديث.
* **Aspose.Cells for Java** الإصدار 25.11 أو أحدث – تم تقديم طريقة `Range.copy` التي تدعم الجداول المحورية في هذا الإصدار.
* ملف **input.xlsx** يحتوي بالفعل على جدول محوري (يمكنك إنشاء واحد في Excel للاختبار).
* أداة بناء من اختيارك (Maven، Gradle، أو مجرد `javac`). سنعرض اعتماد Maven للبدء السريع.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## الخطوة 1: تحميل المصنف المصدر

أول شيء نقوم به هو فتح ملف Excel الذي يحتوي على الجدول المحوري الأصلي. تتعامل Aspose.Cells مع المصنف ككائن في الذاكرة، لذا يمكنك التلاعب به دون تشغيل Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **لماذا هذا مهم:** تحميل المصنف يمنحنا الوصول إلى أوراق العمل، الخلايا، والأهم من ذلك، ذاكرة التخزين المؤقت للجدول المحوري التي تدعم الجدول المحوري. بدون هذه الخطوة لا تمتلك المكتبة ما لتنسخه.

---

## الخطوة 2: الحصول على ورقة العمل التي تحتوي على الجدول المحوري

إذا كان المصنف يحتوي على عدة أوراق، تحتاج إلى الإشارة إلى الورقة الصحيحة. هنا نأخذ ببساطة الورقة الأولى، لكن يمكنك أيضًا استخدام `get("SheetName")` للبحث بالاسم.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **نصيحة احترافية:** عند التعامل مع العديد من الأوراق، احفظ الفهرس أو الاسم في ملف إعدادات لتجنب كتابة الأرقام بشكل ثابت.

---

## الخطوة 3: تحديد النطاق المصدر الذي يشمل الجدول المحوري

بدءًا من الإصدار 25.11 تسمح Aspose.Cells لك بمعاملة الجدول المحوري كنطاق خلايا عادي. حدد الخلايا العليا اليسرى والسفلى اليمنى التي تحيط بالجدول المحوري بالكامل.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **حالة حافة:** إذا كان الجدول المحوري يتوسع ديناميكيًا (مثلاً تُضاف صفوف لاحقًا)، فكر في استخدام `worksheet.getPivotTables().get(0).getDataRange()` للحصول على النطاق الدقيق برمجيًا.

---

## الخطوة 4: تحديد النطاق الهدف حيث سيتم نسخ الجدول المحوري

اختر أي خلية فارغة حيث تريد ظهور النسخة المكررة من الجدول المحوري. في هذا العرض نبدأ عند **F1**، مما يترك فجوة بين الأصلي والنسخة.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **لماذا لا تستخدم ورقة جديدة؟** يمكنك أيضًا إنشاء ورقة عمل جديدة (`workbook.getWorksheets().add("Copy")`) واستخدام خلاياها كوجهة. طريقة `copy` نفسها تعمل عبر الأوراق.

---

## الخطوة 5: نسخ الجدول المحوري إلى الموقع الجديد

الآن يحدث السحر. طريقة `copy` تستنسخ الجدول المحوري، وذاكرة التخزين المؤقت الخاصة به، والتنسيق، وحتى أي مقاطع (slicers) مرتبطة (حسب أحدث إصدار).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **مهم:** عملية النسخ هي *عميقة*؛ لا تُنشئ **إشارة** إلى الجدول المحوري الأصلي. يمكنك تعديل النسخة الجديدة بشكل مستقل دون التأثير على المصدر.

---

## الخطوة 6: حفظ المصنف مع الجدول المحوري المكرر

أخيرًا، اكتب المصنف المعدل مرة أخرى إلى القرص. يمكنك استبدال الأصلي أو إنشاء ملف جديد؛ هنا نختار الخيار الأخير للحفاظ على المصدر دون تعديل.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

عند فتح **output.xlsx** في Excel، سترى الجدول المحوري الأصلي في الأعمدة A‑D ونسخة مطابقة تبدأ من العمود F. يمكن تحديث كلا الجدولين المحوريين بشكل منفصل.

---

## مثال عملي كامل

بدمج كل شيء معًا، إليك الفئة الكاملة في Java التي يمكنك تجميعها وتشغيلها مباشرةً:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**النتيجة المتوقعة:** فتح `output.xlsx` يظهر الجدول المحوري الأصلي (A1:D20) ونسخة مطابقة تبدأ من F1. كلا الجدولين يحتفظان بمرشحاتهما، أنماطهما، والحقول المحسوبة.

---

## التعامل مع التغييرات الشائعة

| الحالة | ما الذي يجب تعديله |
|-----------|----------------|
| **Multiple pivots** on the same sheet | Loop through `worksheet.getPivotTables()` and copy each with its own destination range. |
| **Dynamic data range** | Use `worksheet.getPivotTables().get(0).getDataRange()` to auto‑detect the source area. |
| **Copy to another workbook** | Load a second `Workbook` instance, create a destination worksheet, then call `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | As of 25.12, slicers are copied automatically when the range includes them. Verify in Excel after saving. |

---

## نصائح احترافية ومخاطر

* **التحقق من الإصدار:** تم إضافة طريقة `copy` التي تدعم الجداول المحورية في **Aspose.Cells 25.11**. إذا كنت تستخدم إصدارًا أقدم ستحصل على استثناء. تحقق دائمًا من إصدار `aspose-cells` في ملف `pom.xml` الخاص بك.
* **الأداء:** نسخ الجداول المحورية الكبيرة قد يستهلك الكثير من الذاكرة. إذا كنت تحتاج فقط إلى البيانات، فكر في تصدير الجدول المحوري إلى جدول مسطح بدلاً من استنساخ الكائن بالكامل.
* **سلوك التحديث:** يحتفظ الجدول المحوري المكرر بذاكرة التخزين المؤقت الخاصة به. إذا قمت بتعديل البيانات الأساسية، استدعِ `pivotTable.refresh()` على الجدول الجديد لإعادة الحساب.
* **مشكلات التنسيق:** قد لا تنجح بعض تنسيقات الأرقام المخصصة في النسخ على إصدارات Excel القديمة جدًا (<2007). اختبر مع نسخة Excel التي يستخدمها جمهورك المستهدف.

---

## الخلاصة

أصبح لديك الآن إجابة شاملة من البداية إلى النهاية حول **كيفية نسخ الجداول المحورية** باستخدام Aspose.Cells for Java، ورأيت كيف **تكرار جداول Excel المحورية** في بضع أسطر من الشيفرة. يعمل النهج مع جدول واحد أو عدة جداول، عبر أوراق العمل، وحتى بين المصنفات.

الخطوات التالية قد تشمل:
* أتمتة النسخ لكل جدول محوري في مهمة دفعة.
* إضافة شفرة لإعادة تسمية الجدول المحوري المكرر (مثال: `pivotTable.setName("Copy_of_Sales")`).
* دمج الروتين في خدمة تقارير أكبر تُنشئ ملفات PDF أو تصدير CSV.

جرّبه، عدّل النطاقات لتتناسب مع بياناتك الفعلية، ودع المكتبة تتولى العمل الشاق. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء جداول محورية في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [معالجة جداول محورية في Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [كيفية تحديث مصدر جدول محوري في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}