---
category: general
date: 2026-06-08
description: كيفية نسخ جدول محوري باستخدام Aspose.Cells في Java. تعلم كيفية نسخ النطاق
  بين دفاتر العمل والحفاظ على الجداول المحورية بسهولة.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: ar
og_description: كيفية نسخ جدول محوري في جافا باستخدام Aspose.Cells. يوضح هذا البرنامج
  التعليمي كيفية نسخ النطاق بين المصنفات والحفاظ على الجدول المحوري دون تغيير.
og_title: كيفية نسخ جدول محوري في Java – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: كيفية نسخ جدول محوري في جافا – دليل Aspose.Cells الكامل
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في Java – دليل Aspose.Cells الكامل

هل تساءلت يومًا **كيف تنسخ جدولًا محوريًا** من مصنف Excel إلى آخر باستخدام Java؟ الخبر السار هو أن Aspose.Cells يجعل الأمر سهلًا **لنسخ النطاق بين المصنفات** مع الحفاظ على كل تفاصيل الجدول المحوري.  

في هذا الدرس سنستعرض مثالًا واقعيًا لا ينسخ الجدول المحوري نفسه فحسب، بل يحافظ أيضًا على البيانات الأساسية، والتنسيق، والصيغ كما هي. بنهاية الدرس ستعرف بالضبط **كيفية الحفاظ على هياكل الجدول المحوري**، وكيفية نقل جدول محوري إلى مصنف جديد تمامًا، وكيفية تجنب الأخطاء الشائعة التي تعيق العديد من المطورين.

سنغطي:

- المتطلبات الأساسية الأدنى (Java 17+، Aspose.Cells for Java 23.9+).  
- تحليل خطوة بخطوة للكود، مع شرح **لماذا** كل سطر مهم.  
- معالجة الحالات الخاصة للنطاقات المحورية الكبيرة ومصادر البيانات الخارجية.  
- برنامج كامل قابل للتنفيذ يمكنك وضعه في بيئة التطوير المتكاملة وتشغيله اليوم.

> **نصيحة احترافية:** إذا كنت تستخدم Maven أو Gradle بالفعل، فإن إضافة Aspose.Cells كاعتماد يتم بسطر واحد—دون الحاجة إلى التعامل اليدوي مع ملفات JAR.

---

## نظرة عامة خطوة بخطوة على كيفية نسخ جدول محوري

فيما يلي نظرة عامة على ما سنحققه:

1. تحميل مصنف المصدر الذي يحتوي على الجدول المحوري.  
2. تحديد النطاق الخلوي الدقيق الذي يحيط بالجدول المحوري.  
3. إنشاء مصنف وجهة جديد.  
4. **نسخ النطاق** إلى الورقة الجديدة، مما يسمح لـ Aspose.Cells بالحفاظ تلقائيًا على الجدول المحوري.  
5. حفظ النتيجة كملف جديد.

كل خطوة موضحة بمقاطع كود وتبرير قصير، لتفهم الآلية — وليس مجرد الآلية.

![Diagram illustrating how a pivot table is copied from a source workbook to a destination workbook while preserving its structure](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="مخطط نسخ جدول محوري"}

### الخطوة 1: إعداد Aspose.Cells في مشروعك

قبل أن تتمكن من التعامل مع ملفات Excel، تحتاج إلى مكتبة Aspose.Cells في مسار الفئات (classpath). إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

بالنسبة لـ Gradle، هو سطر واحد أيضًا:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*لماذا هذا مهم:* تقوم Aspose.Cells بإخفاء تفاصيل OpenXML منخفضة المستوى، وتوفر لك واجهة برمجة تطبيقات بسيطة **لنسخ جدول محوري إلى مصنف جديد** دون فقدان أي بيانات وصفية.

### الخطوة 2: تحميل مصنف المصدر

نحتاج إلى كائن `Workbook` يشير إلى الملف الذي يحتوي على الجدول المحوري. استبدل `YOUR_DIRECTORY/src.xlsx` بالمسار الفعلي على جهازك.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **ملاحظة:** تقوم Aspose.Cells تلقائيًا باكتشاف تنسيق الملف (XLSX، XLS، CSV، إلخ)، لذا لا تحتاج للقلق بشأن تحويل التنسيق.

### الخطوة 3: تعريف النطاق المحيط بالجدول المحوري

يعيش الجدول المحوري داخل كتلة مستطيلة من الخلايا. يمكنك تحديد موقعه يدويًا (مثلاً `A1:G20`) أو برمجيًا عن طريق فحص مجموعة `PivotTables` في ورقة العمل. في هذا الدرس سنقوم بتحديد النطاق يدويًا للتوضيح.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*لماذا نستخدم `createRange`*: فإنه ينشئ كائن `Range` خفيف الوزن يمكن تمريره إلى `copyRange`. هذه هي الطريقة الأكثر موثوقية **لنسخ النطاق بين المصنفات** مع ضمان تضمين البُنى الداخلية للجدول المحوري.

### الخطوة 4: إنشاء مصنف وجهة فارغ

الآن نقوم بإنشاء مصنف فارغ سيستقبل البيانات المنسوخة.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

المصنف الافتراضي يحتوي بالفعل على ورقة عمل واحدة، وهو مثالي لغرضنا. إذا كنت بحاجة إلى اسم ورقة محدد، يمكنك إعادة تسميتها:

```java
destinationSheet.setName("PivotCopy");
```

### الخطوة 5: نسخ النطاق والحفاظ على الجدول المحوري

هنا يحدث السحر. طريقة `copyRange` تقبل كائن `CopyOptions`، لكن لا نحتاج لتعديل أي شيء—حفظ الجدول المحوري مفعّل تلقائيًا.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*لماذا هذا يعمل:* تعتبر Aspose.Cells الجدول المحوري جزءًا من مجموعة الخلايا. عندما تستدعي `copyRange`، فإنها تكرر مخزن الجدول المحوري الأساسي، وحقول البيانات، والتخطيط، مما يحقق **كيفية الحفاظ على الجدول المحوري** دون الحاجة إلى كود إضافي.

### الخطوة 6: حفظ مصنف الوجهة

أخيرًا، اكتب الملف الجديد إلى القرص.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

افتح الملف الناتج `copied-with-pivot.xlsx` في Excel، وسترى نسخة مطابقة تمامًا للجدول المحوري الأصلي، جاهزة لمزيد من التحليل.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله مباشرة. يجمع جميع المقاطع أعلاه، ويضيف بعض الفحوصات الوقائية، ويطبع رسالة تأكيد ودية.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**المخرجات المتوقعة عند تشغيل البرنامج**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

افتح ملف الوجهة—يجب أن يبدو جدولك المحوري مطابقًا للأصل، مع الشرائح (slicers)، الفلاتر، والحقول المحسوبة.

## التعامل مع الحالات الخاصة الشائعة

| الحالة | ما الذي يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| **الجدول المحوري يستخدم مصدر بيانات خارجي** (مثل قاعدة بيانات) | الاتصال الخارجي غير مدمج في المصنف، لذا قد يؤدي النسخ إلى كسر الرابط. | صدّر البيانات إلى ورقة أولاً، ثم أنشئ جدولًا محوريًا على تلك الورقة قبل النسخ. |
| **جدول محوري كبير جدًا (آلاف الصفوف)** | `copyRange` قد يستهلك ذاكرة كبيرة. | زيادة حجم الذاكرة المخصصة للـ JVM (`-Xmx2g`) أو نسخ الجدول المحوري على دفعات أصغر باستخدام `copyRows`/`copyColumns`. |
| **وجود جداول محورية متعددة في نفس الورقة** | التحديد الصلب `A1:G20` ينسخ فقط أول جدول محوري. | التكرار عبر `sourceWorksheet.getPivotTables()` ونسخ كل `PivotTable.getDataRange()`. |
| **المصنف الوجهة يحتوي بالفعل على ورقة بنفس الاسم** | `setName` سيطلق استثناء. | استخدام `Workbook.getWorksheets().add("PivotCopy")` لإنشاء ورقة باسم فريد. |

هذه النصائح تضمن أن **كيفية نسخ جدول محوري** تعمل بشكل موثوق، حتى في سيناريوهات الإنتاج.

## الأسئلة المتكررة

**س: هل تنسخ هذه الطريقة تنسيق الجدول المحوري أيضًا؟**  
ج: نعم. لأننا ننسخ النطاق الخلوي بالكامل، فإن الأنماط، والتنسيق الشرطي، وتنسيقات الأرقام تنتقل مع البيانات.

**س: ماذا لو أردت نسخ الجدول المحوري إلى خلية محددة غير `A1`؟**  
ج: ببساطة غيّر الوسيط الثالث في `copyRange` إلى العنوان العلوي‑الأيسر المطلوب، مثل `"B5"`.

**س: هل يمكنني نسخ جدول محوري دون بيانات المصدر؟**  
ج: ليس مباشرة. مخزن الجدول المحوري موجود داخل المصنف؛ إزالة بيانات المصدر سيجعل الجدول غير قابل للاستخدام. صدّر بيانات المصدر إلى ورقة مخفية إذا كنت تريد نسخة خفيفة.

## الخلاصة

أصبح لديك الآن إجابة واضحة وشاملة حول **كيفية نسخ جدول محوري** في Java باستخدام Aspose.Cells. من خلال تحميل مصنف المصدر، وتعريف نطاق الجدول المحوري، واستخدام `copyRange`، يمكنك بسهولة **نسخ النطاق بين المصنفات** مع ضمان بقاء الجدول المحوري.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}