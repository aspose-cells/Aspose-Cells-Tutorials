---
category: general
date: 2026-06-21
description: نسخ نطاق ورقة العمل برمجيًا في Java باستخدام Aspose.Cells. تعلم كيفية
  نسخ نطاق Excel إلى مصنف آخر بكفاءة.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: ar
og_description: نسخ نطاق ورقة العمل برمجيًا في جافا. يوضح هذا الدليل كيفية نسخ نطاق
  إكسل إلى مصنف آخر مع الشيفرة الكاملة والنصائح.
og_title: نسخ نطاق ورقة العمل برمجياً – جافا خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: نسخ نطاق ورقة العمل برمجيًا – دليل جافا الكامل
url: /ar/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ نطاق ورقة العمل برمجيًا – دليل Java كامل

هل تساءلت يومًا كيف **نسخ نطاق ورقة العمل برمجيًا** دون فتح Excel يدويًا؟ لست وحدك. سواء كنت بحاجة إلى تكرار تقرير، أو استنساخ لوحة تحكم تعتمد على Pivot، أو ببساطة نقل البيانات بين الملفات، فإن القيام بذلك عبر الكود يوفر الوقت ويقضي على الأخطاء البشرية.

في هذا البرنامج التعليمي سنستعرض حلًا نظيفًا وشاملًا يوضح **كيفية نسخ نطاق Excel إلى مصنف آخر** باستخدام Java ومكتبة Aspose.Cells. في النهاية ستحصل على برنامج جاهز للتنفيذ، وتفهم سبب كل خطوة، وتعرف الفخاخ التي يجب الانتباه إليها.

---

## ما ستحتاجه

- **Java Development Kit (JDK) 11+** – الكود يُترجم مع أي JDK حديث.
- **Aspose.Cells for Java** (نسخة تجريبية مجانية أو مرخصة). أضف تبعية Maven أو حمّل ملف JAR.
- ملفان Excel: `input.xlsx` يحتوي على النطاق المصدر (بما في ذلك جدول Pivot) و`output.xlsx` فارغ حيث سيُوضع النطاق.
- أي بيئة تطوير (IDE) تفضلها – IntelliJ IDEA، Eclipse، أو حتى محرر نصوص بسيط.

هذا كل شيء. لا خدمات إضافية، لا تفاعل COM، مجرد Java نقي.

![مخطط يوضح نسخ نطاق ورقة العمل برمجيًا بين مصنفين](image.png)

*نص بديل للصورة: توضيح نسخ نطاق ورقة العمل برمجيًا*

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

أولًا، نحتاج إلى المكتبة في مسار الفئة (classpath). إذا كنت تستخدم Maven، أضف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

إذا كنت تفضّل JAR يدويًا، ضعها في مجلد `libs` وأضفها إلى مسار البناء.

لماذا هذا مهم: Aspose.Cells يزودنا بنموذج كائن غني (`Workbook`، `Worksheet`، `Range`) يتيح لنا نسخ البيانات **بما في ذلك جداول Pivot، الصيغ، والتنسيق** في استدعاء واحد—وهو ما لا تستطيع مكتبة Apache POI العادية القيام به بسهولة.

## الخطوة 2: تحميل مصنف المصدر

سنفتح المصنف الذي يحتوي على البيانات التي نريد استنساخها. مُنشئ `Workbook` يأخذ مسار الملف، وستقوم Aspose بقراءة الملف بالكامل إلى الذاكرة.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*نصيحة احترافية:* ضع التحميل داخل كتلة try‑catch إذا كان الملف قد يكون مفقودًا؛ وإلا سيتوقف البرنامج مع خطأ واضح.

## الخطوة 3: إنشاء مصنف هدف فارغ

مصنف جديد يمنحنا لوحة رسم نظيفة. لا نحتاج إلى ملء أي أوراق مسبقًا؛ ستضيف Aspose واحدة لنا.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

لماذا لا نعيد استخدام المصدر؟ الحفاظ على الفصل بينهما يمنع الكتابة فوق غير المقصودة ويجعل الكود قابلًا لإعادة الاستخدام في عمليات الدفعات.

## الخطوة 4: تحديد النطاق الدقيق للنسخ

هنا يبدأ سحر **نسخ نطاق ورقة العمل برمجيًا**. نحدد الخلايا `A1:D20` من أول ورقة عمل في ملف المصدر. تُعيد طريقة `createRange` كائن `Range` يمثل تلك الخلايا بالضبط، بما في ذلك جداول Pivot.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

إذا كنت تحتاج إلى نطاق ديناميكي (مثلًا، “آخر صف مستخدم”)، يمكنك استبدال العنوان الثابت بـ `Cells.maxDisplayRange` أو حسابه باستخدام `Cells.getMaxDataColumn()` و `Cells.getMaxDataRow()`.

## الخطوة 5: إضافة ورقة عمل هدف في مصنف الوجهة

تنشئ Aspose ورقة افتراضية باسم “Sheet1” عند إنشاء `Workbook`. سنضيف ورقة جديدة للحفاظ على النظام، خاصة إذا كنت تخطط لنسخ نطاقات متعددة لاحقًا.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

يمكنك إعطاء الورقة اسمًا ودودًا:

```java
        targetWorksheet.setName("CopiedData");
```

## الخطوة 6: تنفيذ النسخ – بما في ذلك جداول Pivot

الآن العملية الأساسية: `copyRange`. هذه الطريقة تنسخ **القيم، الصيغ، التنسيق، والكائنات المدمجة** (مثل جداول Pivot) من النطاق المصدر إلى خلية الهدف (`A1` في ورقتنا الجديدة). إنها أبسط طريقة لتحقيق **كيفية نسخ نطاق Excel إلى مصنف آخر** دون العبث بحلقات الخلايا منخفضة المستوى.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

خلف الكواليس، تقوم Aspose بتسلسل النطاق المصدر إلى تنسيق وسيط، ثم تعيده إلى ورقة الهدف—وبذلك يبقى كل شيء سليمًا.

## الخطوة 7: حفظ مصنف الوجهة والتحقق

أخيرًا، نكتب مصنف الوجهة إلى القرص. افتح `output.xlsx` في Excel لرؤية النطاق المنسوخ، جدول Pivot، وكل التنسيقات محفوظة.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

عند فتح `output.xlsx`، يجب أن ترى ورقة باسم “CopiedData” بنفس تخطيط `A1:D20` من المصدر، بما في ذلك جدول Pivot الذي يشير الآن إلى البيانات المنسوخة.

## معالجة الحالات الطرفية الشائعة

### 1. النسخ عبر إصدارات Excel المختلفة
تعمل Aspose.Cells مع `.xls`، `.xlsx`، `.xlsb`، وحتى `.csv`. إذا كان المصدر والوجهة يستخدمان صيغًا مختلفة، تقوم المكتبة بتحويلهما تلقائيًا. فقط تأكد من أن امتدادات الملفات تتطابق مع المخرجات المطلوبة.

### 2. الحفاظ على مصادر البيانات الخارجية في جداول Pivot
إذا كان جدول Pivot في المصدر يشير إلى مصدر بيانات خارجي (مثل اتصال قاعدة بيانات)، سيحتفظ Pivot المنسوخ بسلسلة الاتصال لكنه **لن يتم تحديثه تلقائيًا**. استدعِ `pivotTable.refreshData()` بعد النسخ إذا كنت بحاجة إلى نتائج محدثة.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. النطاقات الكبيرة واستهلاك الذاكرة
نسخ نطاقات ضخمة (مئات الآلاف من الصفوف) قد يرفع استهلاك الذاكرة. استخدم `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` قبل تحميل الملفات الكبيرة لتقليل البصمة.

### 4. أوراق أو نطاقات متعددة
إذا كنت بحاجة إلى نسخ عدة نطاقات غير متجاورة، كرّر الخطوات 4‑6 لكل نطاق، أو استخدم `copyRange` مع نطاق موحد (`Cells.createRange("A1:B10,C1:D10")`).

## نصائح احترافية للأتمتة القوية

- **تحقق من صحة النطاق المصدر** قبل النسخ. استخدم `sourceRange.isValid()` لتجنب أخطاء وقت التشغيل.
- **قفل ملف الوجهة** باستخدام `FileInfo.setReadOnly(false)` إذا كنت تستبدل مصنفًا موجودًا.
- **سجّل الإجراءات** باستخدام مسجل خفيف الوزن (SLF4J) – مفيد خاصةً عند معالجة دفعات.
- **تخلص من المصنفات** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) في الخدمات طويلة التشغيل لتحرير الموارد الأصلية.

## ملخص المثال الكامل العامل

فيما يلي الفئة الكاملة المستقلة في Java التي يمكنك لصقها في IDE وتشغيلها. تذكر استبدال `YOUR_DIRECTORY` بمسار المجلد الفعلي على جهازك.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**الناتج المتوقع:** ملف `output.xlsx` يحتوي على ورقة باسم “CopiedData”. الخلايا `A1:D20` ستعكس المصدر، وأي جدول Pivot داخل ذلك النطاق سيكون فعالًا بالكامل، مشيرًا إلى البيانات المنسوخة.

## الخلاصة

لقد عرضنا للتو حلاً نظيفًا، **نسخ نطاق ورقة العمل برمجيًا** في Java، مجيبين على السؤال الشائع **كيفية نسخ نطاق Excel إلى مصنف آخر**. من خلال الاستفادة من API عالي المستوى في Aspose.Cells تجنبنا حلقات الخلايا منخفضة المستوى، وحافظنا على جداول Pivot، وجعلنا الكود سهل القراءة.

ما التالي؟ جرّب توسيع هذا النمط إلى:

- نسخ أوراق العمل بالكامل بدلاً من نطاق واحد.
- معالجة دفعات من عشرات المصنفات في مجلد.
- تصدير النطاق المنسوخ إلى CSV أو PDF لسلاسل تقارير.

لا تتردد في التجربة، وعند مواجهة مشكلة، اترك تعليقًا. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية نسخ أعمدة متعددة في Excel باستخدام Aspose.Cells Java&#58; دليل كامل](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [نسخ أعمدة Excel بكفاءة باستخدام Aspose.Cells for Java&#58; دليل شامل](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [نسخ الصور بين الأوراق في Excel باستخدام Aspose.Cells for Java&#58; دليل شامل](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}