---
category: general
date: 2026-08-04
description: كيفية استخدام wrapcols مع مثال كامل بلغة Java، وإعادة تشكيل مصفوفة في
  Excel وحفظ المصنف إلى ملف باستخدام Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: ar
lastmod: 2026-08-04
og_description: كيفية استخدام wrapcols لإعادة تشكيل مصفوفة في Excel باستخدام Java.
  تعلم مثالًا كاملاً عن wrapcols في Excel، إنشاء دفتر عمل Excel باستخدام Java وحفظ
  الدفتر إلى ملف.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: كيفية استخدام wrapcols في Java – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية استخدام wrapcols في جافا – إعادة تشكيل المصفوفة في إكسل
url: /ar/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS في Java – إعادة تشكيل المصفوفة في Excel

إذا كنت بحاجة إلى **كيفية استخدام WRAPCOLS** لتحويل قائمة مسطحة من القيم إلى نطاق متعدد الصفوف، فإن هذا الدليل يوضح لك الخطوات الدقيقة. سترى **مثال Excel WRAPCOLS** يعيد تشكيل مصفوفة أحادية البعد إلى كتلة 3 صفوف × 2 أعمدة، وستتعلم كيفية **حفظ المصنف إلى ملف** باستخدام Aspose.Cells.

بنهاية هذا الشرح ستكون قادرًا على كتابة كود **إنشاء مصنف Excel Java** يقوم بـ:

* تهيئة مصنف جديد وتحديد الخلية A1.  
* تطبيق دالة `WRAPCOLS` لإعادة تشكيل البيانات.  
* إجبار حساب الصيغ حتى يظهر النتيجة فورًا.  
* استخراج قيمة من المصفوفة المحسوبة.  
* حفظ المصنف على القرص.

المتطلب الوحيد هو بيئة تطوير Java (JDK 8 أو أحدث) ومكتبة Aspose.Cells for Java.

---

## المتطلبات المسبقة

* JDK 8 + (أو أي إصدار أحدث).  
* Maven أو Gradle لإدارة تبعية Aspose.Cells.  
* إلمام أساسي بصياغة Java وصيغ Excel.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، استبدل مقطع XML بسطر `implementation` المقابل.

---

## الخطوة 1: إنشاء مصنف Excel في Java

العملية الأولى هي كتابة كود **إنشاء مصنف Excel Java** يفتح مصنفًا جديدًا ويستخرج الورقة الأولى والخلية A1.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

إنشاء المصنف بهذه الطريقة يمنحك مساحة عمل نظيفة، مما يضمن أن المثال يعمل على أي جهاز دون الحاجة إلى ملف موجود مسبقًا.

---

## الخطوة 2: تطبيق دالة WRAPCOLS – مثال Excel WRAPCOLS

تأخذ `WRAPCOLS` مصفوفة أحادية البعد وعدد الأعمدة، ثم تُعيد نطاقًا يملأ الصفوف أولًا. هذا هو جوهر **إعادة تشكيل المصفوفة في Excel**.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

لماذا يعمل هذا:

* المصفوفة الحرفية `{1,2,3,4,5,6}` توفر ستة أرقام.  
* `WRAPCOLS(..., 2)` يخبر Excel بلف القيم إلى عمودين، مولدًا تلقائيًا عدد الصفوف الكافي (في هذه الحالة 3) لاستيعاب جميع العناصر.  
* النطاق الناتج يملأ الخلايا **A1:B3**:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## الخطوة 3: إجبار الحساب حتى يعكس المصنف الصيغة

لا تقوم Aspose.Cells بتقييم الصيغ تلقائيًا عند تعيينها. يجب استدعاء `calculateFormula()` لتجسيد النتيجة.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

استدعاء هذه الطريقة يضمن أن المصفوفة التي ينتجها `WRAPCOLS` تُكتب في الخلايا، مما يسمح بقراءة القيم فورًا.

---

## الخطوة 4: استخراج قيمة من المصفوفة المعاد تشكيلها

لإثبات أن الصيغة نجحت، اقرأ تمثيل السلسلة للخلية المستهدفة. لأن `WRAPCOLS` تُعيد مصفوفة، تعرض Excel **العنصر الأول** (القيمة `1`) في الخلية التي توجد فيها الصيغة.

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**الناتج المتوقع في وحدة التحكم**

```
First element: 1
```

إذا فحصت الورقة في Excel، سترى الكتلة الكاملة 3 × 2 مملوءة كما هو موضح أعلاه.

---

## الخطوة 5: حفظ المصنف إلى ملف – كيفية حفظ المصنف إلى ملف

حفظ المصنف يتيح لك فتحه لاحقًا في Excel أو مشاركته مع الزملاء. استخدم طريقة `save` مع مسار كامل.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

تشغيل البرنامج ينتج ملف `WrapFunctions.xlsx` في دليل العمل. فتح الملف يُظهر المصفوفة المعاد تشكيلها في الخلايا A1:B3، مؤكدًا أن **حفظ المصنف إلى ملف** تم بنجاح.

---

## مثال كامل قابل للتنفيذ

بدمج جميع الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑لصقه في بيئة تطوير وتشغيله:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**التحقق من النتيجة**

1. تُطبع وحدة التحكم `First element: 1`.  
2. يحتوي الملف `WrapFunctions.xlsx` المُنشأ على:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

إذا احتجت إلى الإشارة إلى المصفوفة في مكان آخر، يمكنك قراءة أي من الخلايا المملوءة باستخدام `worksheet.getCells().get("B2").getIntValue()`، على سبيل المثال.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكن لـ WRAPCOLS التعامل مع مصفوفات غير رقمية؟* | نعم. يمكنك تمرير سلاسل نصية أو تواريخ أو قيم منطقية داخل الأقواس المعقوفة، وسيقوم Excel بلفها وفقًا لذلك. |
| *ماذا لو احتجت إلى صفوف أكثر مما يمكن لـ Excel عرضه؟* | ستستمر WRAPCOLS في الامتداد إلى صفوف إضافية حتى تُستنفد المصفوفة المصدرية. تأكد من أن الورقة تحتوي على عدد كافٍ من الصفوف (الحد الافتراضي هو 1,048,576). |
| *كيف أغيّر عدد الأعمدة؟* | عدل الوسيط الثاني لـ `WRAPCOLS`. للحصول على ثلاثة أعمدة، استخدم `=WRAPCOLS({1,2,3,4,5,6}, 3)`, مما ينتج كتلة 2 × 3. |
| *هل يمكن كتابة النتيجة في خلية بداية مختلفة؟* | نعم. ضع الصيغة في أي خلية (مثلاً `C5`) وسيتوسع النطاق الملتف بالنسبة لتلك الخلية. |
| *هل يجب استدعاء `calculateFormula` في كل مرة أغيّر فيها الصيغة؟* | كلما عدلت صيغة برمجيًا، استدعِ `calculateFormula` أو `calculateFormula(true)` لتحديث الخلايا التابعة. |

---

## الخلاصة

عرض هذا الشرح **كيفية استخدام WRAPCOLS** في Java لإ **إعادة تشكيل المصفوفة في Excel**، قدم مثالًا واضحًا **Excel WRAPCOLS**، وأظهر الطريقة الصحيحة لـ **حفظ المصنف إلى ملف**. الآن لديك أساس قوي لمشاريع **إنشاء مصنف Excel Java** التي تتطلب تحويلات مصفوفية ديناميكية.

بعد ذلك، استكشف مواضيع ذات صلة مثل **استخدام دوال مصفوفية أخرى** (`TRANSPOSE`, `SEQUENCE`) أو **كتابة مجموعات بيانات كبيرة** باستخدام واجهة البث في Aspose.Cells. جرّب مصفوفات مصدر مختلفة، وعدد أعمدة مختلف، ومواقع بدء مختلفة لتكييف النمط مع تقاريرك أو سير عمل معالجة البيانات. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Open an Excel File Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [How to Render Excel Sheets as Images Using Aspose.Cells for Java (Workbook Operations)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}