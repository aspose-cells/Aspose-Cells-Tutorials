---
category: general
date: 2026-07-17
description: استخدم دالة لامدا في جافا لإنشاء مصنف إكسل، وعرض وظائف EXPAND و REDUCE،
  وحساب وظائف المصفوفة في إكسل باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use lambda function java
- create excel workbook java
- use reduce function excel
- use expand function excel
- calculate array functions excel
language: ar
lastmod: 2026-07-17
og_description: استخدم دالة لامدا في جافا لإنشاء مصنف إكسل، وتطبيق EXPAND و REDUCE،
  وحساب الدوال المصفوفية في إكسل – دليل كامل خطوة بخطوة.
og_image_alt: Screenshot of use lambda function java creating Excel workbook with
  formulas
og_title: استخدام دالة لامدا في جافا – إنشاء مصنف إكسل باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: Use lambda function java to create an Excel workbook, demonstrate EXPAND
    and REDUCE functions, and calculate array functions in Excel with Aspose.Cells.
  headline: Use Lambda Function Java to Create Excel Workbook Example
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
- Lambda
title: استخدام دالة لامدا في جافا لإنشاء مثال لمصنف إكسل
url: /ar/java/workbook-operations/use-lambda-function-java-to-create-excel-workbook-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخدم دالة لامدا في جافا لإنشاء مثال على دفتر عمل إكسل

هل تريد **use lambda function java** لإنشاء دفتر عمل إكسل؟ في هذا الدليل سنستعرض مثالًا كاملاً باستخدام Aspose.Cells لا يقتصر فقط على إنشاء الملف بل يوضح أيضًا كيفية **use expand function excel**، **use reduce function excel**، و**calculate array functions excel** في سكريبت واحد سهل المتابعة.

إذا سبق لك أن نظرت إلى جدول بيانات وفكرت، “يجب أن يكون هناك طريقة برمجية لتوسيع هذا المصفوفة أو تقليل هذه القيم”، فأنت في المكان الصحيح. بنهاية هذا الدليل ستحصل على برنامج جافا قابل للتنفيذ يُنشئ ملف إكسل، يضيف صيغًا لـ EXPAND، REDUCE، COT، وCOTH، ويحفظ النتائج المُقيمة — كل ذلك مع إظهار قوة نهج **lambda function java**.

---

## المتطلبات المسبقة – ما تحتاجه قبل البدء

- **Java Development Kit (JDK) 8+** – يستخدم الكود تعبيرات لامدا، لذا تأكد من أنك تستخدم على الأقل JDK 8.  
- **Aspose.Cells for Java** – مكتبة تجارية تتيح لك التعامل مع ملفات إكسل دون الحاجة إلى تثبيت Office. احصل على أحدث ملف JAR من موقع Aspose وأضفه إلى مسار الفئة (classpath) في مشروعك.  
- بيئة تطوير متكاملة (IntelliJ IDEA، Eclipse، VS Code) – أي منها يناسبك، لكن وجود دعم Maven/Gradle يجعل إدارة الاعتمادات أسهل.  

لا توجد أي تثبيتات إضافية مطلوبة؛ المكتبة تتولى كل الأعمال الثقيلة خلف الكواليس.

---

## الخطوة 1: إعداد المشروع واستيراد الاعتمادات

أنشئ مشروع Maven جديد (أو Gradle إذا كنت تفضله) وأضف اعتماد Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

إذا لم تكن تستخدم Maven، فقط ضع ملف `aspose-cells-24.10.jar` في مجلد `libs` وأضفه إلى مسار البناء.

> **نصيحة احترافية:** حافظ على تحديث الاعتمادات الخاصة بك. الإصدارات الأحدث غالبًا ما تجلب تحسينات في الأداء وإصلاحات للأخطاء في الدوال مثل EXPAND وREDUCE.

---

## استخدم دالة لامدا في جافا لإنشاء دفتر عمل إكسل

الآن بعد أن أصبح البيئة جاهزة، دعنا **use lambda function java** لإدراج تعبير LAMBDA مباشرةً داخل صيغة إكسل. دالة REDUCE في إكسل تتوقع لامدا، وتعامل السلاسل النصية في جافا يجعل ذلك بسيطًا.

```java
import com.aspose.cells.*;

public class Office365FunctionsDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create a new workbook and obtain the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Demonstrate the EXPAND function – expands a seed array to a larger size
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3},5,1)");
        // Explanation: EXPAND turns the 3‑element seed into a 5‑row, 1‑column array.

        // Step 4: Demonstrate the REDUCE function – aggregates an array into a single value
        // Here we **use lambda function java** inside the Excel formula.
        sheet.getCells().get("A2").setFormula(
            "=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))"
        );
        // Explanation: Starting at 0, the lambda (a,b) → a+b adds each element together.

        // Step 5: Use the COT function to calculate the cotangent of π/4
        sheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 6: Use the COTH function to calculate the hyperbolic cotangent of 1
        sheet.getCells().get("A4").setFormula("=COTH(1)");

        // Step 7: Recalculate all formulas so the results are stored in the cells
        workbook.calculateFormula();

        // Step 8: Save the workbook with the evaluated results
        workbook.save("Office365Funcs.xlsx");
    }
}
```

### لماذا يعمل هذا

- **`Workbook`** هو نقطة الدخول لمهام **create excel workbook java**. يمثل الملف بالكامل في الذاكرة.  
- **`Worksheet`** يمنحنا ورقة للعمل عليها؛ دفتر العمل الافتراضي يحتوي بالفعل على ورقة واحدة.  
- **`setFormula`** يدرج نص صيغة إكسل الخام. لاحظ أن سطر REDUCE يحتوي على الجزء `LAMBDA(a,b,a+b)` – هذا هو المكان الذي **use lambda function java** نخبر فيه إكسل كيفية دمج القيم.  
- **`calculateFormula()`** يجبر Aspose.Cells على تقييم كل صيغة، بحيث تُحفظ الأرقام الناتجة مباشرةً في الملف. بدون هذا الاستدعاء ستبقى الخلايا تحتوي فقط على نص الصيغة.

---

## كيفية استخدام دالة EXPAND في إكسل – توسيع مصفوفة أثناء التشغيل

مثال **use expand function excel** موجود في الخلية `A1`. لنفصل ما تفعله الصيغة:

```excel
=EXPAND({1,2,3},5,1)
```

- `{1,2,3}` هي مصفوفة البذور (ثلاثة أرقام).  
- `5` يطلب من إكسل توسيع النتيجة إلى خمس صفوف.  
- `1` يحدد عدد الأعمدة (عمود واحد فقط).  

عند فتح دفتر العمل في إكسل، سيظهر النطاق `A1:A5` كالتالي:

| A |
|---|
| 1 |
| 2 |
| 3 |
| 0 |
| 0 |

الأصفار المت trailing هي قيم حشو لأن البذور لم تكن كافية لملء الحجم المطلوب.

> **خطأ شائع:** نسيان استدعاء `workbook.calculateFormula()` سيتركك مع النص الخام `=EXPAND(...)` بدلاً من الأرقام الموسعة.

---

## كيفية استخدام دالة REDUCE في إكسل – الجمع باستخدام لامدا

سطر **use reduce function excel** موجود في الخلية `A2`. يبدو هكذا:

```excel
=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))
```

- `0` هو قيمة المجموع الأولية.  
- `{1,2,3,4}` هي المصفوفة التي نريد تقليلها.  
- `LAMBDA(a,b,a+b)` يخبر إكسل أن يضيف كل عنصر (`b`) إلى المجموع الجاري (`a`).  

بعد الحساب، تحتوي `A2` على **10**. إذا أردت حاصل ضرب بدلاً من الجمع، استبدل ببساطة `a+b` بـ `a*b` – نمط **use lambda function java** يبقى نفسه.

---

## حساب دوال المصفوفات في إكسل – COT وCOTH

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/english/java/calculation-engine/)
- [Custom SUM Function in Excel using Aspose.Cells Java&#58; Enhance Your Calculations](/cells/english/java/formulas-functions/custom-sum-function-excel-aspose-cells-java/)
- [How to Use Aspose.Cells for Excel Slicer Automation in Java](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}