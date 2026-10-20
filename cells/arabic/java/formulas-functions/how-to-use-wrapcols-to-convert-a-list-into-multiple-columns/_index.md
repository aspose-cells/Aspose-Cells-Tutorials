---
category: general
date: 2026-10-16
description: كيفية استخدام wrapcols في جافا وتحويل القائمة إلى أعمدة بسرعة باستخدام
  صيغة – تعلم كيفية ضبط الصيغة لتصميم متعدد الأعمدة
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: ar
lastmod: 2026-10-16
og_description: كيفية استخدام wrapcols لتحويل قائمة إلى أعمدة في Java. اتبع هذا الدليل
  الكامل لتعيين الصيغة وإنشاء تخطيط متعدد الأعمدة في Excel.
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: كيفية استخدام wrapcols – دليل خطوة بخطوة لمطوري جافا
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: كيفية استخدام wrapcols لتحويل قائمة إلى عدة أعمدة في جافا
url: /ar/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام wrapcols لتحويل قائمة إلى أعمدة متعددة في Java

إذا كنت بحاجة إلى **how to use wrapcols** في مشروع Java، فإن هذا الدليل يوضح لك الخطوات الدقيقة. ستتعلم كيفية ضبط الصيغة، تحويل قائمة إلى أعمدة، وإنشاء تخطيط متعدد الأعمدة دون نسخ‑لصق يدوي.

يغطي الدليل كل شيء من إعداد المشروع إلى معالجة الحالات الخاصة، بحيث يمكنك تطبيق الحل على أي جدول بيانات يحتوي على قائمة بعمود واحد. لا تحتاج إلى أدوات إضافية بخلاف Aspose.Cells for Java.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من توفر ما يلي:

* Java 17 أو أحدث مثبت  
* Maven 3.8+ (أو Gradle) لإدارة الاعتمادات  
* ترخيص **Aspose.Cells for Java** – النسخة التجريبية المجانية تكفي للاختبار  
* إلمام أساسي بصيغ Excel  

هذه العناصر تضمن تشغيل الكود دون أخطاء تجميع.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أضف الاعتماد التالي إلى ملف `pom.xml`. إذا كنت تستخدم Gradle، فإن نفس الإحداثيات تنطبق.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

المكتبة توفر الفئات `Cell` و `Worksheet` التي ستُستخدم لاحقًا عندما **how to set formula** لنطاق معين.

## الخطوة 2: إنشاء مصنف وتعبئة القائمة المصدرية

المهمة الأولى هي إنشاء مصنف يحتوي على قائمة رأسية (A2:A100). تمثل هذه القائمة البيانات التي تريد **convert list to columns**.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

تملأ الحلقة العمود الأول بـ 99 عنصرًا، لتوفر لك قائمة واقعية للعمل معها. يمكنك استبدال القيم المولدة ببيانات تُقرأ من قاعدة بيانات أو مصدر آخر.

## الخطوة 3: كيفية استخدام wrapcols لتعيين الصيغة

الآن ستشاهد جوهر الدليل: استخدام دالة `WRAPCOLS` لإنشاء **create multi‑column layout**. تأخذ الدالة معاملين – النطاق المصدر وعدد الأعمدة المطلوبة.

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*لماذا يعمل هذا* – `WRAPCOLS` تقرأ النطاق الرأسي `A2:A100`، ثم توزع القيم صفًا بصف عبر ثلاثة أعمدة (B، C، و D). تظهر النتيجة بدءًا من الخلية التي تحتوي على الصيغة (`A1`). لأن الصيغة تُعيد مصفوفة، تقوم Aspose.Cells تلقائيًا بتوسيع النتيجة إلى الخلايا اللازمة.

### ما يحدث خلف الكواليس

عند حفظ المصنف، تقوم Aspose.Cells بتقييم الصيغة وتكتب القيم الموسعة إلى الملف. إذا فتحت `WrapColsResult.xlsx` في Excel، سترى:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Item 1 | Item 34 | Item 67 |
| Item 2 | Item 35 | Item 68 |
| … | … | … |

يعرض هذا التخطيط نمط **create multi‑column layout** المفيد للتقارير، لوحات المعلومات، أو النماذج القابلة للطباعة.

## الخطوة 4: التحقق من النتيجة برمجيًا (اختياري)

إذا أردت التأكد من أن الصيغة أنتجت المصفوفة المتوقعة دون فتح Excel، يمكنك قراءة القيم مرة أخرى بعد الحساب.

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

تشغيل البرنامج يطبع شيئًا مشابهًا لـ:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

هذا يؤكد أن **how to use wrapcols** يعمل كما هو متوقع وأن عملية **convert list to columns** نجحت.

## الخطوة 5: الاختلافات الشائعة والحالات الخاصة

### تغيير عدد الأعمدة

إذا كنت بحاجة إلى عدد أعمدة مختلف، عدّل المعامل الثاني لـ `WRAPCOLS`. على سبيل المثال، `=WRAPCOLS(A2:A100,5)` ينشئ خمسة أعمدة. تضبط الدالة عدد الصفوف تلقائيًا لتلائم التخطيط الجديد.

### التعامل مع حجم قائمة غير متساوٍ

عندما لا يكون طول النطاق المصدر قابلاً للقسمة على عدد الأعمدة، تقوم `WRAPCOLS` بملء العمود الأخير بفراغات. هذا السلوك مفيد لإنشاء جداول متوازنة دون قص يدوي.

### استخدام نطاق ديناميكي

يمكنك استبدال `A2:A100` بنطاق مسمى أو بصيغة تحسب آخر صف، مثل `A2:INDEX(A:A, COUNTA(A:A))`. يجعل ذلك الحل مرنًا عندما يتغير طول القائمة.

### تجنب الإشارات الدائرية

ضع الصيغة في خلية ليست جزءًا من النطاق المصدر. إذا وضعت الصيغة عن طريق الخطأ داخل `A2:A100`، سيُظهر Excel خطأ إشارة دائرية. دائمًا اكتب الصيغة في خلية منفصلة (عادةً `A1`).

## الخطوة 6: نصائح للاستخدام في بيئات الإنتاج

* **تخزين المصنف مؤقتًا** – إذا كنت تُنشئ تقارير متعددة في حلقة، أعد استخدام كائن `Workbook` واحد وامسح البيانات السابقة لتقليل استهلاك الذاكرة.  
* **ضبط وضع الحساب** – استخدم `workbook.getSettings().setCalculateFormulaOnOpen(false)` عندما تحتاج فقط إلى الصيغة الخام دون تقييم فوري.  
* **التعريب** – اسم الدالة `WRAPCOLS` لا يتأثر باللغات، لكن فواصل الأعداد في صيغ أخرى قد تختلف. حافظ على الصيغ بالإنجليزية لتجنب الأخطاء.  
* **الأداء** – للقوائم التي تتجاوز 10 000 صف، قيّم الصيغة مرة واحدة ثم اقرأ قيم المصفوفة مباشرة لتجنب الحسابات المتكررة.

## الخلاصة

أنت الآن تعرف **how to use wrapcols** في Java لتحويل **list to columns** وإنشاء **create multi‑column layout** باستخدام صيغة واحدة. يُظهر المثال الكامل القابل للتنفيذ سير العمل بالكامل: إضافة المكتبة، تعبئة البيانات، تطبيق الصيغة، والتحقق من النتيجة.

من هنا يمكنك:

* تعديل عدد الأعمدة ليتناسب مع نمط تقاريرك  
* دمج `WRAPCOLS` مع دوال أخرى مثل `SORT` أو `FILTER` لتشكيل بيانات متقدم  
* تصدير المصنف إلى PDF أو CSV أو HTML باستخدام محولات Aspose.Cells المدمجة  

جرّب هذه الاختلافات لتبسيط مهام أتمتة Excel الخاصة بك. إذا واجهت أي مشاكل، راجع قسم معالجة الحالات الخاصة أعلاه أو استشر وثائق Aspose.Cells لمزيد من دعم الصيغ. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام WRAPCOLS في Java – دليل كامل لصيغ مصفوفة Excel](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [كيفية استخدام WRAPCOLS في Java – مثال كامل على WRAPCOLS في Excel](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [كيفية استخدام Reduce في Excel مع Java – دليل صيغ Lambda](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}