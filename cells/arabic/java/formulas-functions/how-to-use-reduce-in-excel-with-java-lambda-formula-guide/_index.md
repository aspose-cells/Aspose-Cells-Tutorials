---
category: general
date: 2026-06-08
description: كيفية استخدام reduce في Excel مع Java باستخدام Aspose.Cells. تعلم صيغة
  lambda في Excel، المصفوفات الديناميكية في Java، كيفية كتابة lambda، وجمع القيم باستخدام
  reduce في دليل خطوة بخطوة واضح.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: ar
og_description: كيفية استخدام reduce في Excel مع Java. إتقان صيغة lambda في Excel،
  المصفوفات الديناميكية في Java، وجمع القيم باستخدام reduce من خلال مثال كامل قابل
  للتنفيذ.
og_title: كيفية استخدام Reduce في Excel مع Java – دليل صيغ Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: كيفية استخدام Reduce في Excel مع Java – دليل صيغ Lambda
url: /ar/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Reduce في Excel مع Java – دليل صيغ Lambda

هل تساءلت يومًا **how to use reduce** في Excel أثناء كتابة كود Java؟ لست وحدك. يواجه العديد من المطورين صعوبة في دمج الدالات الديناميكية الجديدة في Excel مع الأتمتة القائمة على Java، والإجابة ليست معقدة كما تبدو في البداية.

في هذا الدليل سنستعرض مثالًا عمليًا يوضح **how to use reduce** مع تعبير **lambda formula Excel**، كل ذلك باستخدام مكتبة Aspose.Cells for Java. في النهاية ستتمكن من إنشاء مصفوفات ديناميكية في Java، كتابة دوال lambda، وحساب **sum with reduce**—دون الحاجة إلى تعديل يدوي في الجداول.

---

## ما ستقوم ببنائه

- دفتر عمل جديد يتم إنشاؤه بالكامل من خلال Java.  
- مصفوفة ديناميكية **EXPAND** تملأ الخلايا A1:A5 بالأرقام 1‑5.  
- صيغة **REDUCE** تجمع هذه الأرقام باستخدام **lambda formula Excel**.  
- ملف `.xlsx` محفوظ يمكنك فتحه في أي برنامج جدول بيانات للتحقق من النتيجة.

بدون ماكرو خارجي، بدون VBA—فقط كود Java صافي ودالات Excel الحديثة.

---

## المتطلبات المسبقة

- Java 17 (أو أي JDK حديث) – الإصدارات القديمة تعمل لكنك ستفقد ميزات `var`.  
- Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي لهذا العرض).  
- إلمام أساسي بصياغة Java وصيغ Excel.  

إذا كنت جديدًا على **dynamic arrays java**، لا تقلق—هذا الدليل يشرح كل جزء.

---

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

أولًا، أضف تبعية Aspose.Cells إلى ملف `pom.xml` (أو احصل على الـ JAR يدويًا).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **نصيحة احترافية:** حافظ على تحديث تبعياتك؛ الإصدارات الأحدث تحسن سرعة تقييم الصيغ، وهو أمر مهم عندما تكون **how to use reduce** في جداول كبيرة.

---

## الخطوة 2: إنشاء دفتر عمل والوصول إلى الورقة الأولى

الآن سننشئ دفتر عمل جديد تمامًا. هذا هو الأساس لتعلم **how to use reduce** لأن كائن دفتر العمل يمنحنا بيئة لإدخال الصيغ.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*لماذا هذا مهم:* فئة `Workbook` تمثل ملف Excel بالكامل، بينما `Worksheet` تمثل تبويبًا واحدًا. ستلاحظ لاحقًا كيف يمكن لـ **dynamic arrays java** ملء عدة خلايا من صيغة واحدة موضوعة في A1.

---

## الخطوة 3: إنشاء مصفوفة رأسية باستخدام EXPAND

دالة `EXPAND` في Excel يمكنها أن تنثر القيم في نطاق. سنستخدمها لإنشاء الأرقام 1 إلى 5 في العمود A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

إذا فتحت دفتر العمل الناتج، ستجد الخلايا A1:A5 تحتوي على 1, 2, 3, 4, 5. هذا هو جزء **dynamic arrays java**—صيغة واحدة تملأ نطاقًا كاملًا.

---

## الخطوة 4: كتابة دالة REDUCE Lambda لجمع المصفوفة

هنا نجيب على السؤال الأساسي: **how to use reduce** في Excel من خلال Java. دالة `REDUCE` تتكرر على مصفوفة، وتطبق دالة lambda التي تزودها. في مثالنا سنجمع الأرقام.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

لنوضح ذلك:

- `0` – القيمة الأولية للمجمع (`acc`).  
- `A1:A5` – المصفوفة التي أنشأناها باستخدام **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – **lambda formula Excel** التي تضيف كل عنصر (`x`) إلى المجمع (`acc`).  

عند تنفيذ الصيغة، ستحتوي الخلية `B1` على **15**، وهو **sum with reduce** للأرقام 1‑5.

> **How to write lambda** في Excel؟ فكر فيها كدالة مجهولة حيث تكون المعاملات الأولى هي المتغيرات، والتعبير الأخير هو قيمة الإرجاع. في Java ندرج النص فقط؛ محرك Excel يتولى الحساب.

---

## الخطوة 5: حفظ دفتر العمل

أخيرًا، نحفظ دفتر العمل على القرص حتى تتمكن من فتحه في Excel أو Google Sheets أو أي عارض يدعم `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

افتح الملف وسترى:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

يظهر **sum with reduce** في B1، مما يؤكد أننا نجحنا في توضيح **how to use reduce** مع **lambda formula Excel** من خلال Java.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى بيئتك التطويرية، عدل مسار الإخراج، ثم اضغط **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**الناتج المتوقع** عند فتح `new-functions.xlsx`:

- الخلايا **A1:A5** تحتوي على `1, 2, 3, 4, 5`.  
- الخلية **B1** تعرض `15`، مما يؤكد **sum with reduce**.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت مصفوفة أفقية بدلًا من رأسية؟

غيّر معطيات العمود/الصف في `EXPAND`. للحصول على انسكاب أفقي عبر B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### هل يمكنني استخدام REDUCE للضرب بدلًا من الجمع؟

بالتأكيد. فقط غير جسم الدالة lambda:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

الآن ستظهر B1 القيمة `120` (5 ! = 120).

### هل تدعم Aspose.Cells دوال LAMBDA مخصصة؟

نعم، يمكنك تعريف دوال LAMBDA مسماة عبر مجموعة `Names` في دفتر العمل، ثم استدعاؤها كأي صيغة مدمجة. هذا موضوع أعمق لدليل لاحق حول **how to write lambda** التي تتجاوز خلية واحدة.

### ماذا عن إصدارات Excel القديمة التي لا تتعرف على REDUCE؟

إذا استهدفت Excel 2019 أو أقدم، سيُظهر المحرك الخطأ `#NAME?`. في مثل هذه الحالات


## ماذا تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}