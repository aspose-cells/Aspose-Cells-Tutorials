---
category: general
date: 2026-07-20
description: نسخ جدول محوري في Java باستخدام Aspose.Cells. تعلم كيفية نسخ الجدول المحوري
  إلى ملف آخر، استخراج نطاق الجدول المحوري، ونسخ النطاق إلى مصنف جديد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy pivot table to another file
- copy range to new workbook
- how to copy pivot table
- extract pivot table range
language: ar
lastmod: 2026-07-20
og_description: نسخ جدول محوري في Java باستخدام Aspose.Cells. اتبع هذا الدليل لنسخ
  الجدول المحوري إلى ملف آخر، استخراج نطاقه، ونسخ النطاق إلى مصنف جديد.
og_image_alt: Diagram illustrating how to copy pivot table from one workbook to another
  using Java
og_title: نسخ جدول محوري في جافا – دليل Aspose.Cells خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  headline: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  type: TechArticle
- description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  name: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  steps:
  - name: Expected Output
    text: '- `CopyWithPivot.xlsx` contains a single worksheet. - The worksheet shows
      the same pivot layout as the source. - All pivot fields, filters, and calculated
      items are intact. - Refreshing the pivot updates totals based on the newly copied
      data.'
  - name: Copying Multiple Pivot Tables
    text: If your source sheet has more than one pivot, repeat the `createRange`/`copy`
      pair for each table, adjusting the address accordingly. You can also loop through
      `sourceWorksheet.getPivotTables()` to automate discovery.
  - name: Preserving Styles and Formatting
    text: The `Range.copy` method copies cell values, formulas, and formatting by
      default. However, if you only need the data without styles, use `sourceRange.copy(destinationRange,
      new CopyOptions());` and tweak the `CopyOptions` flags.
  - name: Working with Large Workbooks
    text: 'For workbooks exceeding a few hundred MB, consider enabling **memory‑efficient
      loading**:'
  - name: Quick Recap
    text: '- Loaded a source workbook containing a pivot table. - Identified the exact
      **extract pivot table range** (`A1:G20`). - Created a fresh workbook and **copied
      range to new workbook**, preserving the pivot. - Saved the result, effectively
      **copying pivot table to another file**.'
  type: HowTo
- questions:
  - answer: Yes. Aspose handles format conversion automatically during `save()`. Just
      specify the desired extension in the output path.
    question: Can I copy a pivot table across different Excel formats (XLSX → XLS)?
  - answer: The copy will overwrite existing cells. To avoid data loss, either clear
      the area first (`destinationSheet.getCells().clearRange("A1:G20")`) or choose
      a different start cell.
    question: What if the destination workbook already contains data in the target
      range?
  - answer: 'The source workbook is opened in read‑write mode by default. If you only
      need to read, pass `LoadOptions` with `setReadOnly(true)`. ## Next Steps & Related
      Topics Now that you know **how to copy pivot table** programmatically, you might
      explore: - **Refreshing pivot caches** after copying (`pivotTab'
    question: Does this work with read‑only source files?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot Table
title: نسخ جدول محوري في جافا باستخدام Aspose.Cells – دليل شامل
url: /ar/java/excel-pivot-tables/copy-pivot-table-in-java-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري في Java باستخدام Aspose.Cells – دليل شامل

هل احتجت يومًا إلى **نسخ جدول محوري** من ملف Excel إلى آخر لكن لم تكن متأكدًا من أين تبدأ؟ أنت لست وحدك. في العديد من خطوط تقارير البيانات نحتاج إلى نقل ملخص يعتمد على الجدول المحوري من دفتر عمل رئيسي إلى ملف خفيف للتوزيع، والقيام بذلك يدويًا أمر مؤلم.  

في هذا البرنامج التعليمي سنستعرض حلًا برمجيًا نظيفًا يتيح لك **نسخ جدول محوري إلى ملف آخر**، استخراج نطاقه الدقيق، وحتى **نسخ النطاق إلى دفتر عمل جديد** في خطوة واحدة. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يعمل مع أي مشروع Java يدعم Aspose.Cells.

## ما يغطيه هذا الدليل

- تحميل دفتر عمل مصدر يحتوي بالفعل على جدول محوري  
- تحديد النطاق الدقيق **استخراج نطاق الجدول المحوري** الذي تحتاجه  
- إنشاء دفتر عمل جديد ولصق النطاق مع الحفاظ على منطق الجدول المحوري  
- حفظ النتيجة كملف جديد، جاهز للمعالجة اللاحقة  

بدون أدوات خارجية، بدون حركات ماكرو—فقط شفرة Java صافية وقليل من استدعاءات Aspose.Cells. إذا كنت قد عملت مع Excel من قبل، ستشعر بالمفاهيم مألوفة؛ إذا كنت جديدًا على Aspose، فإن المكتبة تُجرد التعامل مع XML منخفض المستوى، مما يتيح لك التركيز على منطق الأعمال.

> **المتطلبات المسبقة**  
> - Java 8 أو أحدث  
> - Aspose.Cells for Java (أحدث إصدار حتى يوليو 2026)  
> - إلمام أساسي بجداول Pivot في Excel  

الآن، دعنا نغوص في التفاصيل.

## الخطوة 1: إعداد مشروعك واستيراد Aspose.Cells

قبل أن نتعامل مع أي دفتر عمل، تأكد من أن ملف JAR الخاص بـ Aspose.Cells موجود في مسار الفئات (classpath). إذا كنت تستخدم Maven، أضف الاعتماد التالي:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of 2026 -->
</dependency>
```

إذا كنت تفضل إعدادًا يدويًا، ضع `aspose-cells-24.10.jar` في مجلد `libs` وأشر إليه في بيئة التطوير المتكاملة (IDE) الخاصة بك.

> **نصيحة احترافية:** حافظ على توافق إصدار المكتبة مع نسخة Java الخاصة بك لتجنب `UnsupportedClassVersionError`.

## الخطوة 2: تحميل دفتر العمل المصدر الذي يحتوي على الجدول المحوري

أول شيء نحتاجه هو كائن `Workbook` يشير إلى الملف الذي يوجد فيه الجدول المحوري. هنا يبدأ عملية **نسخ جدول محوري**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that already has the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

لماذا نقوم بتحميله بهذه الطريقة؟ تقوم Aspose بقراءة الملف بالكامل إلى الذاكرة، مما يمنحنا وصولًا كاملاً إلى أوراق العمل، الخلايا، والذاكرة المؤقتة للجدول المحوري. هذا يضمن بقاء تعريف الجدول المحوري (الحقول، الفلاتر، مصدر البيانات) سليمًا عندما نقوم بنسخه لاحقًا.

## الخطوة 3: تحديد النطاق الدقيق الذي يحتوي على الجدول المحوري

الجدول المحوري ليس مجرد مجموعة من الخلايا؛ فهو مدعوم بذاكرة مخفية. ومع ذلك، عند نسخ النطاق المرئي، تقوم Aspose بنقل الذاكرة المؤقتة تلقائيًا. لضمان الأمان، سنحدد النطاق صراحةً—هذه هي خطوة **استخراج نطاق الجدول المحوري**.

```java
        // Define the range covering the pivot table (adjust as needed)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                // first worksheet
                                          .getCells()
                                          .createRange("A1:G20"); // typical size; change if larger
```

إذا لم تكن متأكدًا من الأبعاد، يمكنك تحديد موقع الجدول المحوري برمجيًا باستخدام `Worksheet.getPivotTables()`. للاختصار نفترض وجود مستطيل معروف، لكن نفس المنطق يعمل للاكتشاف الديناميكي.

## الخطوة 4: إنشاء دفتر عمل جديد لاستقبال النطاق المنسوخ

الآن نقوم بإنشاء دفتر عمل جديد سيصبح ملف الوجهة. هنا يحدث **نسخ النطاق إلى دفتر عمل جديد**.

```java
        // Create an empty workbook that will receive the copy
        Workbook destinationWorkbook = new Workbook(); // starts with a default sheet
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

لماذا دفتر عمل جديد تمامًا؟ البدء من الصفر يضمن عدم وجود تنسيقات عشوائية أو أوراق مخفية تتداخل مع مراجع الجدول المحوري الداخلية. إذا كنت بحاجة إلى الدمج في ملف موجود، ما عليك سوى تحميل ذلك الملف بدلاً من `new Workbook()`.

## الخطوة 5: تنفيذ النسخ – الحفاظ على الجدول المحوري

هذا هو جوهر البرنامج التعليمي: نسخ النطاق مع الحفاظ على وظيفة الجدول المحوري. طريقة `Range.copy` في Aspose تقوم بالعمل الشاق.

```java
        // Copy the source range (including the pivot) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

عند تنفيذ هذا السطر، تقوم Aspose باستنساخ الخلايا المرئية **وأيضًا** استنساخ الذاكرة المؤقتة للجدول المحوري إلى دفتر العمل الجديد. النتيجة هي جدول محوري يعمل بالكامل يمكنك تحديثه، تصفيته، أو تصديره مثل الأصل.

> **سؤال شائع:** *ماذا لو كان الوجهة يحتوي بالفعل على جدول محوري بنفس الاسم؟*  
> تقوم Aspose بإعادة تسمية الجدول المنسوخ تلقائيًا لتجنب التعارضات (مثال: “PivotTable1_1”).

## الخطوة 6: حفظ دفتر العمل الوجهة

أخيرًا، نقوم بحفظ الملف الجديد. هذه هي الخطوة التي تقوم فعليًا **بنقل جدول محوري إلى ملف آخر** على القرص.

```java
        // Save the workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

بعد تشغيل البرنامج، افتح `CopyWithPivot.xlsx` في Excel. سترى نفس تخطيط الجدول المحوري، الفلاتر، ومصدر البيانات (الذي الآن يشير إلى النطاق المنسوخ). سيعيد تحديث الجدول المحوري حساب القيم بناءً على كتلة البيانات الجديدة.

## مثال كامل يعمل

بجمع كل ما سبق، إليك الفئة الكاملة الجاهزة للتنفيذ:

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Define the range that includes the pivot table (e.g., A1:G20)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:G20");

        // 3️⃣ Create a new workbook to receive the copied range
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range to the destination worksheet; the pivot table is preserved
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### النتيجة المتوقعة

- يحتوي `CopyWithPivot.xlsx` على ورقة عمل واحدة.  
- تُظهر ورقة العمل نفس تخطيط الجدول المحوري كما في المصدر.  
- جميع حقول الجدول المحوري، الفلاتر، والعناصر المحسوبة سليمة.  
- تحديث الجدول المحوري يُحدّث الإجماليات بناءً على البيانات المنسوخة حديثًا.

## التعامل مع الحالات الخاصة والاختلافات

### نسخ جداول محورية متعددة

إذا كانت ورقة المصدر تحتوي على أكثر من جدول محوري، كرّر زوج `createRange`/`copy` لكل جدول، مع تعديل العنوان وفقًا لذلك. يمكنك أيضًا التكرار عبر `sourceWorksheet.getPivotTables()` لأتمتة الاكتشاف.

### الحفاظ على الأنماط والتنسيق

طريقة `Range.copy` تنسخ قيم الخلايا، الصيغ، والتنسيق بشكل افتراضي. ومع ذلك، إذا كنت تحتاج فقط إلى البيانات بدون الأنماط، استخدم `sourceRange.copy(destinationRange, new CopyOptions());` وعدل أعلام `CopyOptions`.

### العمل مع دفاتر عمل كبيرة

لدفاتر العمل التي تتجاوز بضع مئات من الميجابايت، فكر في تمكين **التحميل الفعال للذاكرة**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook sourceWorkbook = new Workbook("bigfile.xlsx", loadOptions);
```

هذا يقلل من استهلاك الذاكرة heap مع الاستمرار في السماح بنسخ النطاق.

## الأسئلة المتكررة

**س: هل يمكنني نسخ جدول محوري عبر صيغ Excel مختلفة (XLSX → XLS)؟**  
ج: نعم. تقوم Aspose بمعالجة تحويل الصيغة تلقائيًا أثناء `save()`. فقط حدد الامتداد المطلوب في مسار الإخراج.

**س: ماذا لو كان دفتر العمل الوجهة يحتوي بالفعل على بيانات في النطاق المستهدف؟**  
ج: سيقوم النسخ بالكتابة فوق الخلايا الموجودة. لتجنب فقدان البيانات، إما امسح المنطقة أولًا (`destinationSheet.getCells().clearRange("A1:G20")`) أو اختر خلية بداية مختلفة.

**س: هل يعمل هذا مع ملفات مصدر للقراءة فقط؟**  
ج: يتم فتح دفتر العمل المصدر في وضع القراءة والكتابة بشكل افتراضي. إذا كنت تحتاج فقط للقراءة، مرّر `LoadOptions` مع `setReadOnly(true)`.

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن عرفت **كيفية نسخ جدول محوري** برمجيًا، قد ترغب في استكشاف:

- **تحديث ذاكرة التخزين المؤقت للجدول المحوري** بعد النسخ (`pivotTable.refresh();`)  
- **تصدير بيانات الجدول المحوري إلى CSV** للتحليلات اللاحقة  
- **إضافة مقاطع (slicers) برمجيًا** إلى الجدول المحوري المنسوخ (`PivotTable.addSlicer(...)`)  
- **نسخ المخططات المرتبطة بالجداول المحورية** باستخدام `Chart.copy()`  

كل من هذه يبني على الأساس الذي وضعناه، مما يتيح لك بناء خطوط أتمتة Excel من البداية إلى النهاية في Java.

---

### ملخص سريع

- تم تحميل دفتر عمل مصدر يحتوي على جدول محوري.  
- تم تحديد النطاق الدقيق **استخراج نطاق الجدول المحوري** (`A1:G20`).  
- تم إنشاء دفتر عمل جديد و**نسخ النطاق إلى دفتر عمل جديد**، مع الحفاظ على الجدول المحوري.  
- تم حفظ النتيجة، مما أدى فعليًا إلى **نسخ جدول محوري إلى ملف آخر**.  

جرّب ذلك مع ملفاتك الخاصة، عدّل النطاق، وشاهد الجدول المحوري ينتقل بسلاسة. إذا واجهت أي مشاكل، اترك تعليقًا أدناه—برمجة سعيدة!

![Copy pivot table diagram showing source and destination workbooks](https://example.com/images/copy-pivot-table-diagram.png)


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحديث مصدر جدول Pivot في Excel باستخدام Aspose.Cells لـ Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [تحسين تحميل جدول Pivot في Java باستخدام Aspose.Cells: دليل شامل](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [معالجة جدول Pivot في Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}