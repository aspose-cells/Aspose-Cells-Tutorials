---
category: general
date: 2026-06-21
description: كيفية استخدام WRAPCOLS مع Aspose.Cells Java لتحويل المصفوفة إلى صفوف،
  كتابة الصيغة في الخلية، وتعبئة الخلايا بالصيغ – دليل خطوة بخطوة.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: ar
og_description: كيفية استخدام WRAPCOLS في جافا مع Aspose.Cells لتحويل مصفوفة إلى صفوف،
  كتابة صيغة في خلية، وتعبئة الخلايا بالصيغ—كل ذلك في دليل واحد.
og_title: كيفية استخدام WRAPCOLS في جافا – مثال كامل على WRAPCOLS في إكسل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: كيفية استخدام WRAPCOLS في Java – مثال كامل لـ WRAPCOLS في Excel
url: /ar/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS في Java – مثال كامل لـ Excel WRAPCOLS

هل تساءلت يومًا **كيفية استخدام WRAPCOLS** عندما تحتاج إلى تحويل مصفوفة بسيطة إلى جدول منظم في Excel؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يرون دالة `WRAPCOLS` لأول مرة ويفكرون، “كيف يمكنني كتابة هذه الصيغة في خلية من Java فعليًا؟” الخبر السار؟ الأمر بسيط جدًا بمجرد معرفة الخطوات الصحيحة.

في هذا البرنامج التعليمي سنستعرض مثالًا قابلاً للتنفيذ بالكامل باستخدام Aspose.Cells للـ Java ي **يحول مصفوفة إلى صفوف**، يكتب الصيغة مباشرةً في خلية، ويظهر لك كيفية **ملء الخلايا بالصيغ** لسيناريوهات العالم الحقيقي. في النهاية ستحصل على صورة واضحة عن **مثال excel wrapcols** وستكون جاهزًا لتكييفه مع مشاريعك الخاصة.

## المتطلبات المسبقة

- Java 17 أو أحدث (الكود يعمل مع أي JDK حديث).
- مكتبة Aspose.Cells للـ Java (يمكنك الحصول على أحدث JAR من Maven Central).
- فهم أساسي لصياغة Java وصيغ Excel.
- بيئة تطوير متكاملة (IDE) أو محرر نصوص بسيط—لا حاجة لأدوات خاصة.

هل لديك كل شيء؟ رائع، لنبدأ.

## الخطوة 1: إعداد المشروع وتحميل مصنف

أولاً، أنشئ مشروع Maven (أو Gradle) جديد وأضف تبعية Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

الآن يمكننا تحميل مصنف موجود (أو إنشاء واحد جديد) والحصول على الورقة الأولى:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **لماذا نقوم بتحميل مصنف** – Aspose.Cells يعمل مع تمثيل في الذاكرة لملف Excel. من خلال تحميل (أو إنشاء) مصنف نحصل على إمكانية الوصول إلى الخلايا والصفوف والصيغ، وهو أمر أساسي لأي عملية **كتابة صيغة إلى خلية**.

## الخطوة 2: إدراج صيغة WRAPCOLS في خلية

جوهر البرنامج التعليمي يكمن في دالة `WRAPCOLS`. فهي تأخذ مصفوفة أحادية البُعد وتـ“تلف”ها إلى عدد محدد من الأعمدة، وتقوم تلقائيًا بتوزيع المتبقي على صفوف جديدة. إليكم الصياغة التي سنستخدمها:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

لاحظ كيف أن الصيغة هي سلسلة نصية عادية تُمرَّر إلى `setFormula`. تقوم Aspose.Cells بالعمل الشاق—تحليل الصيغة، تقييمها، وتوزيع النتائج في الورقة. هذه هي الطريقة الأكثر مباشرةً لـ **ملء الخلايا بالصيغ** دون الحاجة إلى التكرار اليدوي عبر الصفوف والأعمدة.

### ما تقوم به الصيغة

- `{1,2,3}` – مصفوفة حرفية تحتوي على ثلاثة أرقام.
- `2` – عدد الأعمدة لكل صف.
- النتيجة:
  - **A1** = 1، **B1** = 2
  - **A2** = 3، **B2** = (فارغ)

إذا أردت ثلاثة أعمدة بدلاً من ذلك، فقط غيّر الوسيط الثاني إلى `3`، وستملأ المصفوفة صفًا واحدًا.

## الخطوة 3: حفظ المصنف والتحقق من النتيجة

الآن بعد أن وضعت الصيغة في **A1**، لنحفظ المصنف على القرص حتى تتمكن من فتحه في Excel ورؤية التوزيع:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

افتح `output.xlsx` وسترى بالضبط ما وصفه التعليق—عمودان في الصف الأول والقيمة المتبقية في الصف الثاني. هذه هي جوهر **مثال excel wrapcols**.

## الخطوة 4: توسيع المثال – تحويل مصفوفات أكبر

نادراً ما تعمل المشاريع الحقيقية بثلاثة أرقام فقط. افترض أن لديك مجموعة أكبر، مثل `{10,20,30,40,50,60,70}` وتريد ثلاثة أعمدة لكل صف. إليك كيفية تعديل الكود:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

الآن يبدأ التوزيع عند **C5**، وينتج:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

هذا يوضح كيف يمكنك **تحويل المصفوفة إلى صفوف** بشكل ديناميكي، فقط بتعديل سلسلة الصيغة. لا حلقات، لا تعيين يدوي للخلايا—Aspose.Cells يتولى الباقي.

## الخطوة 5: معالجة الحالات الحدية والمشكلات الشائعة

### 1. المصفوفات الفارغة

إذا كانت المصفوفة الحرفية فارغة (`{}`)، فإن `WRAPCOLS` تُرجع خطأ `#VALUE!`. لتجنب كسر الورقة، احمِ توليد الصيغة:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. البيانات غير الرقمية

`WRAPCOLS` تعمل مع النص أيضًا. على سبيل المثال، `WRAPCOLS({"A","B","C","D"},2)` تُنتج تخطيطًا من عمودين للسلاسل. فقط تذكر وضع علامات اقتباس حول السلاسل داخل المصفوفة الحرفية.

### 3. التوافق

دالة `WRAPCOLS` متوفرة في Excel 365 وExcel 2019+ (Office 2019، Excel للويب). إذا كنت بحاجة لدعم إصدارات أقدم، سيتعين عليك الرجوع إلى التكرار اليدوي أو استخدام دالة أخرى متوافقة مع التوزيع.

## الخطوة 6: نصائح عملية وحيل احترافية

- **نصيحة احترافية:** استخدم `Cell.setFormulaLocal` إذا كنت بحاجة إلى فاصل خاص بالمنطقة (فاصلة أو فاصلة منقوطة) حسب إعدادات المستخدم الإقليمية.
- **احذر من:** الكتابة فوق البيانات الموجودة. ستستبدل منطقة التوزيع أي محتوى موجود مسبقًا في النطاق المستهدف.
- **ملاحظة أداء:** ضبط الصيغة تكلفة قليلة؛ العمل الشاق يحدث عند **حفظ** أو **إعادة حساب** المصنف. إذا كنت تُنشئ آلاف الصيغ، فكر في تعطيل الحساب التلقائي (`wb.calculateFormula()` لاحقًا) لتسريع المعالجة.

## مثال كامل يعمل

فيما يلي الفئة الكاملة للـ Java جاهزة للتنفيذ والتي تضم كل ما ناقشناه:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**الناتج المتوقع:** افتح `output.xlsx` وسترى ثلاث مناطق توزيع متميزة:

- **A1:B2** – الأرقام 1‑3 مُلفَّة إلى عمودين.
- **C5:E7** – الأرقام 10‑70 مُلفَّة إلى ثلاثة أعمدة.
- **G1:H2** – أسماء الفواكه مُلفَّة إلى عمودين.

## الخلاصة

لقد غطينا للتو **كيفية استخدام WRAPCOLS** مع Aspose.Cells للـ Java، موضحين لك كيفية **تحويل المصفوفة إلى صفوف**، **كتابة صيغة إلى خلية**، و**ملء الخلايا بالصيغ** بطريقة نظيفة وقابلة للتكرار. هذه الطريقة تلغي الحاجة إلى التكرار الممل، وتستفيد من سلوك التوزيع الأصلي في Excel، وتحافظ على اختصار الكود.

هل أنت مستعد للتحدي التالي؟ جرّب دمج `WRAPCOLS` مع مصادر بيانات ديناميكية—ربما سحب القيم من قاعدة بيانات، إنشاء سلسلة المصفوفة في الوقت الفعلي، وترك Excel يقوم بعمل التخطيط. يمكنك أيضًا تجربة وظائف توزيع أخرى مثل `SEQUENCE` أو `FILTER` لإنشاء تقارير أكثر غنى.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو استكشف وثائق Aspose الواسعة. ترميز سعيد، واستمتع بقوة صيغ Excel الحديثة مباشرةً من Java!

![مثال على كيفية استخدام wrapcols](/images/wrapcols-demo.png "كيفية استخدام wrapcols في Java – لقطة شاشة للبيانات الموزعة")


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحديد نطاقات الخلايا في Excel باستخدام Aspose.Cells للـ Java (دليل 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [كيفية تعيين خلية نشطة في Excel باستخدام Aspose.Cells للـ Java: دليل كامل](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [كيفية إدراج صفوف في مصنفات Excel باستخدام Aspose.Cells للـ Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}