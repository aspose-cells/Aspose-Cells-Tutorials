---
category: general
date: 2026-10-07
description: كيفية تقسيم الأعمدة باستخدام Aspose.Cells للغة Java. تعلّم تقسيم السلسلة
  إلى أعمدة، أتمتة صيغ Excel، وكتابة الصيغة إلى خلية في بضع أسطر من الشيفرة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: ar
lastmod: 2026-10-07
og_description: كيفية تقسيم الأعمدة في جافا باستخدام Aspose.Cells. يوضح لك هذا الدرس
  كيفية تقسيم السلسلة إلى أعمدة، وأتمتة تقييم صيغ Excel، وكتابة صيغة في خلية.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: كيفية تقسيم الأعمدة في جافا باستخدام Aspose.Cells – دليل سريع
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية تقسيم الأعمدة في Java باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تقسيم الأعمدة في Java باستخدام Aspose.Cells – دليل خطوة بخطوة

إذا كنت بحاجة إلى **كيفية تقسيم الأعمدة** في ورقة عمل Excel برمجياً، يوضح لك هذا الدليل العملية الكاملة باستخدام Aspose.Cells for Java. ستتعلم أيضًا كيفية **تقسيم سلسلة إلى أعمدة**، **أتمتة تقييم صيغ Excel**، و **كتابة صيغة إلى خلية** باستخدام كود مختصر وجاهز للإنتاج.

يُزيل تقسيم الأعمدة برمجياً الحاجة إلى النسخ واللصق اليدوي، يقلل الأخطاء، ويمكنك من تنفيذ تحويلات بيانات على نطاق واسع. بحلول نهاية هذا الدليل يمكنك إنشاء الصيغ وتعديلها وتقييمها في الوقت الفعلي، مما يجعل Excel جزءًا حقيقيًا من خلفية Java الخاصة بك.

## المتطلبات المسبقة

* Java 17 أو أحدث مثبتة.
* Maven 3.8+ (أو Gradle) لإدارة الاعتمادات.
* رخصة Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي للتعلم).
* إلمام أساسي بصياغة Java ومفاهيم Excel.

إذا كان أي من هذه العناصر مفقودًا، قم بتثبيتها أولاً؛ عينات الكود تفترض مشروع Maven قياسي.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أضف الاعتماد التالي إلى ملف `pom.xml`. سيقوم هذا بجلب أحدث مكتبة مستقرة من Aspose.Cells.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**لماذا هذه الخطوة مهمة:** توفر المكتبة الفئات `Workbook` و `Worksheet` و `Cell` اللازمة للتعامل مع ملفات Excel دون الحاجة إلى Microsoft Office. بدون هذا الاعتماد لن يتم تجميع الكود.

## الخطوة 2: إنشاء مصنف واختيار ورقة العمل الأولى

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

كائن `Workbook` يمثل ملف Excel بالكامل. الوصول إلى ورقة العمل الأولى يضمن نقطة بدء متوقعة للصيغة التي سنكتبها.

## الخطوة 3: كتابة صيغة WRAPCOLS إلى الخلية المستهدفة

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**لماذا نستخدم `WRAPCOLS`:** الدالة المدمجة في Excel `WRAPCOLS` تقسم قيمة نصية واحدة إلى عدد محدد من الأعمدة تلقائيًا، مع معالجة حدود الكلمات بذكاء. هذه هي الطريقة الأكثر موثوقية لـ **تقسيم سلسلة إلى أعمدة** دون الحاجة إلى منطق تحليل مخصص.

## الخطوة 4: إجبار المصنف على تقييم الصيغة

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

استدعاء `calculateFormula()` **يُؤتمت تقييم صيغ Excel** على جانب الخادم. بدون هذا الاستدعاء ستظل الخلية تحتوي على نص الصيغة، وليس القيم المحسوبة.

## الخطوة 5: استرجاع وعرض النتيجة المُقسمة

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

عند تشغيل البرنامج، سيطبع الطرفية:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

الملف الناتج `SplitColumnsResult.xlsx` يُظهر الثلاثة أعمدة المملوءة بالنص المقسم.

## فهم دالة WRAPCOLS

* **الصياغة:** `WRAPCOLS(text, columns, [delimiter])`
* **المعلمات:**
  * `text` – السلسلة التي تريد تقسيمها.
  * `columns` – عدد الأعمدة التي سيُوزع عليها النص.
  * `delimiter` (اختياري) – الحرف المستخدم لتقسيم السلسلة؛ الافتراضي هو المسافة.
* **قيمة الإرجاع:** مصفوفة تُسقِط إلى الخلايا المجاورة، كل عنصر يحتوي على جزء من النص الأصلي.

نظرًا لأن الدالة تُسقِط أفقياً، تحتاج فقط إلى كتابة الصيغة في الخلية الأكثر يسارًا (A1 في المثال). يقوم Excel تلقائيًا بملء B1 و C1 … حسب الحاجة.

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل الموصى به |
|-----------|------------------------|
| **عدد أعمدة متغير** | استبدل القيمة الثابتة `3` بمتغير: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **فاصل مخصص** | استخدم الوسيط الثالث، مثلاً `=WRAPCOLS(A2,4,",")` للتقسيم باستخدام الفواصل. |
| **سلسلة مصدر فارغة** | تُعيد الدالة خلايا فارغة؛ احرص على التحقق من عدم كون السلسلة `null` أو فارغة قبل ضبط الصيغة. |
| **مجموعات بيانات كبيرة** | طبّق الصيغة داخل حلقة لكل صف، ثم استدعِ `calculateFormula()` مرة واحدة بعد انتهاء الحلقة لتحسين الأداء. |
| **حروف غير ASCII** | WRAPCOLS يعمل مع Unicode؛ تأكد من حفظ ملف مصدر Java بترميز UTF‑8. |

**نصيحة احترافية:** عند معالجة عدد كبير من الصفوف، احفظ الصيغة في متغير نصي وأعد استخدامها لتجنب تكلفة الجمع المتكرر للسلاسل.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. يتضمن عبارات الاستيراد، معالجة الاستثناءات، وعملية حفظ اختيارية.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

تشغيل هذا البرنامج ينتج نفس مخرجات الطرفية المعروضة سابقًا ويكتب ملف Excel يوضح بوضوح **كيفية تقسيم الأعمدة**.

## قائمة التحقق من استكشاف الأخطاء وإصلاحها

* **الصيغة لا تُقيم** – تأكد من استدعاء `workbook.calculateFormula()` بعد ضبط الصيغة.
* **خلايا فارغة بعد التقسيم** – تحقق من أن السلسلة المصدر ليست `null` أو فارغة، وأن عدد الأعمدة أكبر من الصفر.
* **استثناء الترخيص** – قدّم ملف ترخيص Aspose.Cells صالح (`License license = new License(); license.setLicense("Aspose.Total.lic");`) قبل إنشاء المصنف لإزالة علامات التقييم التجريبي.
* **بطء الأداء على أوراق كبيرة** – استدعِ `calculateFormula()` مرة واحدة بعد كتابة جميع الصيغ، وليس بعد كل خلية على حدة.

## الخلاصة

أنت الآن تعرف **كيفية تقسيم الأعمدة** في Java باستخدام Aspose.Cells، وكيفية **تقسيم سلسلة إلى أعمدة** باستخدام دالة `WRAPCOLS`، وكيفية **أتمتة تقييم صيغ Excel**، وكيفية **كتابة صيغة إلى خلية** برمجيًا. تُزيل هذه التقنية خطوات إعداد البيانات اليدوية وتدمج قدرات معالجة النص القوية في Excel مباشرةً في تطبيقات Java الخاصة بك.

### الخطوات التالية

* استكشف وظائف نصية أخرى مثل `TEXTSPLIT` و `FILTERXML` لسيناريوهات تحليل أكثر تعقيدًا.
* اجمع `WRAPCOLS` مع `IFERROR` للتعامل مع المدخلات غير المتوقعة بسلاسة.
* دمج الحل في خدمة Spring Boot تستقبل بيانات CSV عبر REST وتعيد ملف Excel مُعبأ.

بتقنّك لهذه الأنماط يمكنك بناء تدفقات عمل Excel آلية وقوية تتوسع مع احتياجات عملك. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [aspose cells java – Split Names into Columns](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [How to Delete Blank Columns in Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}