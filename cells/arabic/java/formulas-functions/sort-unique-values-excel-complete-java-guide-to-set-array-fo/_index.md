---
category: general
date: 2026-06-30
description: فرز القيم الفريدة في Excel باستخدام Java. تعلم كيفية تعيين الصيغة، وإعادة
  حساب الصيغ، وإنشاء قائمة فريدة في Excel باستخدام Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: ar
og_description: فرز القيم الفريدة في إكسل باستخدام جافا. يوضح هذا الدليل كيفية ضبط
  الصيغة، وإعادة حساب الصيغ، وإنشاء قائمة فريدة في إكسل خلال دقائق.
og_title: ترتيب القيم الفريدة في إكسل – درس جافا لصيغ المصفوفات
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: ترتيب القيم الفريدة في إكسل – دليل جافا الكامل لإنشاء صيغ المصفوفة
url: /ar/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# فرز القيم الفريدة في Excel – دليل Java الكامل لتعيين صيغ المصفوفة

هل تساءلت يومًا كيف **فرز القيم الفريدة في Excel** دون سحب الصيغ يدويًا؟ لست وحدك. في العديد من سيناريوهات التقارير تحتاج إلى قائمة نظيفة مرتبة أبجديًا من الإدخالات المميزة، والقيام بذلك يدويًا أمر مرهق.  

الخبر السار؟ ببضع أسطر من كود Java يمكنك **تعيين صيغة مصفوفة** في ورقة عمل، ثم **إعادة حساب الصيغ** بحيث يتم ملء النطاق المتسرب تلقائيًا. في هذا الدرس سنستعرض كل شيء—من إنشاء ملف عمل إلى توليد قائمة فريدة بأسلوب Excel—حتى تتمكن من دمج الحل مباشرةً في تطبيقك.

## ما يغطيه هذا الدرس

- إعداد مشروع Java مع Aspose.Cells (المكتبة التي تشغل مقتطف الكود).  
- استخدام دالتي `SORT` و `UNIQUE` معًا **لإنشاء قائمة فريدة في Excel**.  
- تطبيق **صيغة مصفوفة** على خلية برمجيًا.  
- تشغيل عملية حسابية بحيث يحدث خطوة **كيفية إعادة حساب الصيغ** فورًا.  
- التحقق من النتيجة وتعديل الحل لحالات الحافة مثل الخلايا الفارغة أو النطاقات غير المتصلة.

بنهاية هذا الدليل ستكون قادرًا على إدراج طريقة جاهزة للاستخدام في أي خدمة Java تحتاج إلى تصدير جداول Excel نظيفة.

> **نصيحة احترافية:** إذا كنت تستخدم Maven بالفعل، فإن إضافة Aspose.Cells كاعتماد يوفر عليك التعامل اليدوي مع ملفات JAR.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| Java 8 أو أحدث | Aspose.Cells تستهدف Java 8+. |
| Maven (أو Gradle) | يبسط إدارة الاعتمادات. |
| Aspose.Cells for Java | يوفر كائنات `Workbook` و `Worksheet` وواجهات الصيغ التي سنستخدمها. |
| إلمام أساسي بدوال Excel | فهم `SORT` و `UNIQUE` يساعدك على تعديل الكود. |

> *إذا لم تكن تمتلك Aspose.Cells بعد، أضف هذا إلى ملف `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## الخطوة 1: إنشاء ملف عمل جديد (بدء تعيين الصيغة يبدأ من هنا)

أولًا نحتاج إلى ملف عمل فارغ. فكر فيه كقماش فارغ حيث سنقوم لاحقًا **بتعيين صيغة مصفوفة** على الخلية `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *لماذا ننشئ ملف عمل جديد؟*  
> يضمن بيئة نظيفة، متجنبًا الصيغ المخفية التي قد تتداخل مع بيانات الاختبار الخاصة بنا.

---

## الخطوة 2: ملء بيانات عينة (اختياري لكن مفيد)

لرؤية النتيجة بوضوح، لنملأ العمود **B** ببعض القيم المتكررة.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *لماذا نستخدم العمود B؟*  
> الصيغة التي سنكتبها تشير إلى النطاق `B1:B10`، لذا إبقاء البيانات هناك يعكس المثال الكلاسيكي في Excel.

---

## الخطوة 3: تعيين صيغة مصفوفة **فرز القيم الفريدة في Excel**

الآن يحدث السحر. نجمع `UNIQUE` (لإزالة التكرارات) مع `SORT` (لترتيبها أبجديًا). التعبير الناتج هو **صيغة مصفوفة**، أي أنها ستنتشر إلى الخلايا المجاورة تلقائيًا.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### كيف تعمل الصيغة

- `UNIQUE(B1:B10)` يمر على النطاق ويعيد مصفوفة عمودية من السلاسل المميزة.  
- `SORT(...)` يأخذ تلك المصفوفة ويرتبها تصاعديًا.  
- وضع العلامة `=` واستدعاء `setFormulaArray` يخبر Aspose.Cells بمعالجة النتيجة كـ **مصفوفة متسربة**، تمامًا كما يفعل Excel.

> **ملاحظة:** إذا كنت تستخدم نسخة أقدم من Excel لا تدعم `SORT` أو `UNIQUE`، يمكنك الرجوع إلى `SORT(UNIQUE(...))` مع دالة **LET** أو استخدام صيغ المصفوفة التقليدية (`=INDEX(...)`). يركز هذا الدرس على نهج المصفوفة الديناميكية الحديث لأنه الأنسب **لإنشاء قائمة فريدة في Excel** اليوم.

---

## الخطوة 4: إعادة حساب الصيغ لتعبئة النطاق المتسرب

بعد وضع الصيغة، لا يقوم ملف العمل بتقييمها تلقائيًا. هنا تأتي خطوة **كيفية إعادة حساب الصيغ**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

استدعاء `calculateFormula()` يجبر Aspose.Cells على تشغيل محرك Excel، مما يملأ الخلايا `A1`، `A2`، … بالقيم الفريدة المرتبة.

> *لماذا لا نعتمد على التقييم الكسول؟*  
> في سياق الخادم غالبًا ما تحتاج إلى جاهزية البيانات للتصدير (CSV، PDF، إلخ) مباشرةً بعد الحساب، لذا فإن الاستدعاء الصريح يضمن الاتساق.

---

## الخطوة 5: التحقق من النتيجة (تصحيح اختياري)

من الجيد دائمًا طباعة القيم المتسربة إلى وحدة التحكم—خاصةً عندما تتعلم واجهة برمجة تطبيقات جديدة.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

تشغيل البرنامج يطبع:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

افتح الملف `SortedUniqueValues.xlsx` وسترى نفس البيانات تتسرب من `A1` إلى الأسفل.

---

## معالجة حالات الحافة

### خلايا فارغة في النطاق المصدر

إذا كان النطاق `B1:B10` يحتوي على خلايا فارغة، فإن `UNIQUE` سيعاملها كقيمة مميزة. لتجاهل الفراغات، غلف النطاق بـ `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### بيانات غير متصلة

عندما تكون بياناتك موزعة على أعمدة متعددة، يمكنك دمجها باستخدام `CHOOSE` أو `TEXTJOIN` قبل تطبيق `UNIQUE`. مثال:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

تظهر هذه التعديلات مرونة **كيفية تعيين الصيغة** لسيناريوهات أكثر تعقيدًا.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل القابل للتنفيذ بلغة Java. انسخه إلى بيئة التطوير، أضف اعتماد Aspose.Cells، ثم اضغط *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**المخرجات المتوقعة** (المعروضة في وحدة التحكم) تتطابق مع القائمة المرتبة والمزالة التكرارات التي ناقشناها. فتح ملف Excel المُولد يُظهر نفس القيم المتسربة من `A1` إلى الأسفل.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع إصدارات Excel القديمة (قبل Office 365)؟**  
ج: دالتا `SORT` و `UNIQUE` جزء من محرك المصفوفة الديناميكية الذي تم تقديمه في Excel 365. بالنسبة للملفات القديمة تحتاج إلى استخدام صيغ المصفوفة الكلاسيكية مثل `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. لا يزال Aspose.Cells قادرًا على تقييمها، لكن الصياغة تكون أكثر إطالة.

**س: هل يمكنني تعيين صيغة المصفوفة على نطاق غير `A1`؟**  
ج: بالتأكيد. فقط غيّر العنوان في `cells.get("A1")`. ستبدأ المصفوفة المتسربة دائمًا من الخلية التي تحددها وتتمدد يمينًا وأسفلًا حسب الحاجة.

**س: ماذا لو كان حجم البيانات المصدر أكبر من `B1:B10`؟**  
ج: استبدل النطاق الثابت بنطاق ديناميكي، مثل `B:B` أو نطاق مسمى. تصبح الصيغة `=SORT(UNIQUE(B:B))`. احذر من مراجع الأعمدة الكاملة في الأوراق الكبيرة جدًا؛ قد تؤثر على الأداء.

---

## الخلاصة

لقد غطينا **كيفية تعيين صيغة** في Java لـ **فرز القيم الفريدة في Excel**، وكيفية **إعادة حساب الصيغ**، وكيفية **إنشاء قائمة فريدة في Excel** باستخدام واجهة Aspose.Cells القوية. الخطوات بسيطة: إنشاء ملف عمل، ملء البيانات، تطبيق صيغة مصفوفة، تشغيل الحساب، والتحقق من النتيجة.  

من هنا يمكنك التوسع—إضافة تنسيق شرطي، تصدير إلى PDF، أو دمج الطريقة في خدمة ويب تقدم تقارير جاهزة. الفكرة الأساسية تبقى نفسها: دع وظائف Excel تقوم بالعمل الشاق، ودع Java يدير العملية.

هل أنت مستعد للارتقاء بأتمتة Excel؟ جرّب استبدال `SORT` بـ `SORTBY` للترتيب حسب عمود ثانوي، أو جرب `FILTER` لاستبعاد الصفوف التي لا تلبي قواعد العمل. الاحتمالات لا حدود لها.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}