---
category: general
date: 2026-10-20
description: تعلم كيفية نسخ جدول محوري باستخدام Aspose.Cells في Java. يوضح هذا البرنامج
  التعليمي كيفية نسخ النطاق إلى ورقة جديدة وتكرار ورقة الجدول المحوري بأمان.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: ar
lastmod: 2026-10-20
og_description: كيفية نسخ جدول محوري باستخدام Aspose.Cells في Java. اتبع هذا الدليل
  لنسخ النطاق إلى ورقة جديدة وتكرار ورقة الجدول المحوري دون فقدان البيانات.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: كيفية نسخ جدول محوري في جافا – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells – دليل خطوة بخطوة

إذا كنت بحاجة إلى **how to copy pivot table** في تطبيق Java، فإن هذا الدليل يوضح لك الخطوات الدقيقة. سواءً كنت تبني محرك تقارير أو تقوم بأتمتة ترحيل البيانات، سترى كيفية نسخ النطاق إلى ورقة جديدة مع الحفاظ على تعريف جدول المحور وبياناته.

قد يبدو نسخ جدول محوري أمرًا محفوفًا بالمخاطر لأن ذاكرة التخزين المؤقت الأساسية وإعدادات الحقول غالبًا ما تُفقد. يوضح هذا البرنامج التعليمي نهجًا موثوقًا باستخدام Aspose.Cells، ويعرض الكود القابل للتنفيذ بالكامل، ويشرح لماذا كل سطر مهم. في النهاية، ستكون قادرًا على تكرار ورقة جدول المحور في ثوانٍ.

## المتطلبات المسبقة

* تم تثبيت Java 8 أو أحدث.
* تم إضافة Aspose.Cells for Java (الإصدار 23.10 أو أحدث) إلى مسار الفئات (classpath) في مشروعك.
* مصنف مصدر (`source.xlsx`) يحتوي على جدول محوري في النطاق `A1:G20`.
* إلمام أساسي بـ Java ومفاهيم Excel.

لا توجد مكتبات إضافية مطلوبة؛ حيث يتعامل Aspose.Cells مع جميع عمليات Excel داخليًا.

## كيفية نسخ جدول محوري – الاستراتيجية العامة

الفكرة الأساسية بسيطة:

1. تحميل المصنف الذي يحتوي على جدول المحور الأصلي.
2. تحديد النطاق الدقيق الذي يشمل جدول المحور.
3. إنشاء ورقة عمل جديدة ستستقبل البيانات المنسوخة.
4. استخدام طريقة `Range.copy` لنقل النطاق إلى الورقة الجديدة.  
   تقوم هذه الطريقة بنسخ ذاكرة التخزين المؤقت للجدول المحوري تلقائيًا، لذا يظل جدول المحور فعالًا.
5. حفظ المصنف إلى ملف جديد.

نظرًا لأن عملية النسخ تعمل على مستوى النطاق، فإن **duplicate pivot table sheet** تحتفظ بجميع تكوينات الحقول، والفلاتر، والعناصر المحسوبة.

## الخطوة 1: تحميل مصنف المصدر

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*لماذا هذا مهم*: تحميل المصنف يمنحك الوصول إلى أوراق العمل، الخلايا، وذاكرة التخزين المؤقت للجدول المحوري. يقرأ Aspose.Cells الملف بالكامل إلى الذاكرة، لذا تكون العمليات اللاحقة سريعة وآمنة عبر الخيوط.

## الخطوة 2: تعريف النطاق المصدر الذي يحتوي على جدول المحور

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*لماذا هذا مهم*: استدعاء `createRange` يخبر Aspose.Cells بالضبط أي خلايا يجب نسخها. تضمين كامل مساحة جدول المحور يضمن نقل صفوف الذاكرة المخفية أيضًا. إذا حذفت أي جزء من الذاكرة المؤقتة، سيظهر جدول المحور المنسوخ فارغًا.

## الخطوة 3: إضافة ورقة عمل وجهة للبيانات المنسوخة

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*لماذا هذا مهم*: إضافة ورقة مخصصة تعزل جدول المحور المنسوخ عن الأصلي، مما يسهل مقارنة النتائج أو استخدام الورقة كقالب لمعالجة إضافية.

## الخطوة 4: نسخ النطاق إلى ورقة العمل الوجهة (يتم الحفاظ على جدول المحور)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*لماذا هذا مهم*: طريقة `copy` لا تنسخ فقط قيم الخلايا وتنسيقها بل أيضًا تكرر ذاكرة التخزين المؤقت للجدول المحوري. هذه هي الخطوة الأساسية التي تمكنك من **duplicate pivot table sheet** دون فقدان أي وظيفة.

## الخطوة 5: حفظ المصنف مع النطاق المنسوخ

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*لماذا هذا مهم*: الحفظ ينشئ ملف Excel جديد (`result.xlsx`) يحتوي على كل من الأصلي وورقة جدول المحور المكررة. يمكنك الآن فتح الملف في Excel للتحقق من أن جدول المحور يعمل تمامًا كما كان.

## مثال كامل قابل للتنفيذ

بجمع كل شيء معًا، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في بيئة التطوير المتكاملة (IDE) الخاصة بك:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### النتيجة المتوقعة

* فتح `result.xlsx` يُظهر ورقتين عمل:
  * **Sheet1** – البيانات الأصلية وجدول المحور.
  * **CopyResult** – نسخة مطابقة تمامًا من جدول المحور، تعمل بالكامل.
* جميع حقول الجدول المحوري، الفلاتر، والعناصر المحسوبة تتصرف بنفس طريقة المصدر.

إذا قمت بتعديل جدول المحور المصدر بعد النسخ، فإن الورقة المكررة **لن** تعكس تلك التغييرات لأن الذاكرة المؤقتة تم نسخها في وقت النسخ. هذا العزل غالبًا ما يكون مرغوبًا عندما تحتاج إلى لقطة من التقرير.

## المشكلات الشائعة وكيفية تجنبها

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot table appears blank** | النطاق المنسوخ حذف صفوف الذاكرة المخفية. | تأكد من أن النطاق يشمل الذاكرة الكاملة (عادةً بضع صفوف أسفل الجدول المرئي). |
| **Destination sheet name already exists** | `add("CopyResult")` يطرح استثناءً إذا كان الاسم مستخدمًا. | استخدم `workbook.getWorksheets().addUniqueName("CopyResult")` أو تحقق من `contains` قبل الإضافة. |
| **File path errors** | `YOUR_DIRECTORY` غير صحيح يؤدي إلى `FileNotFoundException`. | استخدم مسارات مطلقة أو `Paths.get(...).toAbsolutePath()` في Java لتحديد المواقع. |
| **Performance slowdown on large workbooks** | نسخ نطاقات ضخمة ينسخ خلايا غير ضرورية. | قصر النطاق على مساحة جدول المحور الدقيقة، أو استخدم `Range.copy` مع `CopyOptions` لتخطي التنسيق إذا لم يكن مطلوبًا. |

## نصيحة احترافية: استخدام `CopyOptions` للتحكم الدقيق

إذا كنت تحتاج فقط إلى بيانات جدول المحور وتريد تخطي تنسيق الخلايا، يمكنك تمرير كائن `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

هذا يقلل من حجم ملف الورقة المكررة ويسرع عملية النسخ، خاصةً في المصنفات الكبيرة.

## كيفية نسخ النطاق إلى ورقة جديدة دون فقدان الصيغ

المثال أعلاه ينسخ الصيغ بالفعل لأن `Range.copy` يحافظ عليها افتراضيًا. إذا كنت تريد القيم فقط (مثلاً لتجميد الحالة الحالية)، عيّن `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

الآن تحتوي ورقة الوجهة على قيم ثابتة، لكن جدول المحور سيظل يعمل لأن ذاكرته المؤقتة جزء من النطاق.

## ملخص الحل

* **How to copy pivot table** – تحميل المصنف، تعريف النطاق الدقيق، إضافة ورقة عمل جديدة، نسخ النطاق، ثم حفظ.
* العملية توضح أيضًا **copy range to new sheet** وكيفية **duplicate pivot table sheet** بأمان.
* يمكنك ضبط النسخ بدقة باستخدام `CopyOptions` لأداء أفضل أو سيناريوهات القيم فقط.

## الخطوات التالية والمواضيع ذات الصلة

* **Refresh pivot cache programmatically** – استخدم `PivotTable.refreshData()` بعد تحديث بيانات المصدر.
* **Export pivot table to PDF** – دمج تقنية النسخ هذه مع `PdfSaveOptions` لإنشاء تقارير لقطات.
* **Automate multi‑sheet duplication** – كرر عبر جميع أوراق العمل وطبق نفس منطق النسخ.

جرّب هذه التغييرات لتكييف النمط مع خط أنابيب التقارير الخاص بك. إذا واجهت حالات خاصة، مثل مصادر بيانات خارجية أو جداول محورية مدفوعة بـ VBA، فإن نهج نسخ النطاق يعمل أيضًا، لكن قد تحتاج إلى نسخ كائنات الاتصال الأساسية كذلك.

---

*Happy coding! إذا ساعدك هذا البرنامج التعليمي في تعلم **how to copy pivot table**، لا تتردد في مشاركته مع زملائك أو المساهمة في تحسينه.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية نسخ النطاق والحفاظ على جدول محوري في Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [إنشاء مصنف جديد في Java – دليل كامل لنسخ جدول محوري](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [نسخ جدول محوري بين المصنفات – دليل Java خطوة بخطوة](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}