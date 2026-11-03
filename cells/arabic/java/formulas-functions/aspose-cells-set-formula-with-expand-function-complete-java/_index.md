---
category: general
date: 2026-10-16
description: Aspose.Cells تعيين الصيغة في Java باستخدام دالة EXPAND. تعلّم مثالًا
  خطوة بخطوة واكتشف كيفية استخدام EXPAND للنطاقات الديناميكية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: ar
lastmod: 2026-10-16
og_description: Aspose.Cells يحدد الصيغة في Java باستخدام دالة EXPAND. اتبع مثالًا
  كاملاً لتوسيع النطاقات ديناميكيًا في دفاتر عمل Excel.
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells تعيين الصيغة باستخدام EXPAND – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: 'Aspose.Cells: تعيين الصيغة باستخدام دالة EXPAND – دليل Java الكامل'
url: /ar/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل Java الكامل لاستخدام Aspose.Cells لتعيين الصيغة باستخدام الدالة EXPAND

إذا كنت بحاجة إلى **aspose cells set formula** برمجياً، فإن هذا الدرس يوضح لك بالضبط كيفية القيام بذلك. ستتعلم كيفية استخدام الدالة EXPAND لإنشاء نطاق ديناميكي ينمو بخمسة صفوف وخمسة أعمدة من خلية بداية، كل ذلك من خلال كود Java.

التعامل مع صيغ Excel من Java غالباً ما يكون غير مريح، لكن Aspose.Cells يبسط التعقيد. في الأقسام أدناه سنستعرض مثالاً كاملاً قابلاً للتنفيذ، نناقش لماذا كل سطر مهم، ونستكشف بعض الاختلافات الشائعة مثل خلايا البداية المختلفة أو أحجام التوسيع المتغيرة.

## ما يغطيه هذا الدرس

* تحميل مصنف موجود باستخدام Aspose.Cells  
* الوصول إلى ورقة العمل ومجموعة الخلايا الخاصة بها  
* **aspose cells set formula** باستخدام الدالة `EXPAND`  
* إعادة حساب المصنف حتى يتم تقييم الصيغة  
* حفظ النتيجة والتحقق من المخرجات  

لا تحتاج إلى مكتبات خارجية غير Aspose.Cells، والكود يعمل على أي بيئة تشغيل Java 8+. في النهاية ستتمكن من تعديل النمط لاستخدام صيغ ديناميكية أخرى.

## المتطلبات المسبقة

* مجموعة تطوير Java (JDK) 8 أو أحدث  
* Aspose.Cells for Java (قم بالتنزيل من [الموقع الرسمي](https://downloads.aspose.com/cells/java))  
* ملف Excel إدخالي (`input.xlsx`) موجود في دليل معروف  
* إلمام أساسي بصياغة Java وإدارة الاعتمادات عبر Maven/Gradle  

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

لـ Gradle، المكافئ هو:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** استخدم دائمًا أحدث نسخة مستقرة؛ الإصدارات الأحدث تتضمن تحسينات في أداء حساب الصيغ.

## الخطوة 2: تحميل المصنف

السطر الأول من حلنا يفتح مصنفًا موجودًا. استبدل `YOUR_DIRECTORY` بالمسار المطلق حيث يقع `input.xlsx`.

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*لماذا هذا مهم*: تحميل المصنف يُنشئ تمثيلًا في الذاكرة يتيح لك تعديل أوراق العمل، الخلايا، والصيغ دون الحاجة إلى الوصول إلى نظام الملفات مرة أخرى.

## الخطوة 3: الوصول إلى ورقة العمل المستهدفة ومجموعة الخلايا

نعمل مع أول ورقة عمل (الفهرس 0). كائن `Cells` يمنحك وصولًا مباشرًا إلى الخلايا الفردية عبر العنوان.

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

إذا كنت تحتاج إلى ورقة مختلفة، غيّر الفهرس أو استخدم `get("SheetName")`.

## الخطوة 4: **aspose cells set formula** – تطبيق دالة EXPAND

الآن نضع الصيغة في الخلية **B2**. الدالة `EXPAND` تأخذ ثلاثة معطيات: خلية المرجع، عدد الصفوف التي سيتم توسيعها، وعدد الأعمدة التي سيتم توسيعها.

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### كيفية استخدام EXPAND

* **خلية المرجع (`A2`)** – نقطة البداية للنطاق الديناميكي.  
* **الصفوف (`5`)** – عدد الصفوف التي يجب أن ينمو فيها النطاق إلى الأسفل.  
* **الأعمدة (`5`)** – عدد الأعمدة التي يجب أن ينمو فيها النطاق إلى اليمين.

يمكنك استبدال هذه القيم بمتغيرات إذا كنت بحاجة إلى حل مرن:

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## الخطوة 5: إعادة حساب المصنف

بعد تعيين الصيغة، يجب إخبار Aspose.Cells بحسابها. طريقة `calculateFormula()` تعالج جميع الصيغ في المصنف.

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **لماذا نعيد الحساب؟**  
> بدون هذا الاستدعاء، ستبقى الصيغة غير مُقيمة وسيظهر في ملف الإخراج النص الخام `=EXPAND(...)` بدلاً من المصفوفة الموسعة.

## الخطوة 6: حفظ المصنف المحدث

أخيرًا، اكتب التغييرات إلى ملف جديد. هذا يحافظ على المصنف الأصلي للمقارنة.

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

عند فتح `output.xlsx` في Excel، ستظهر الخلية **B2** كتلة 5 × 5 من القيم المنقولة من المنطقة التي تبدأ بـ **A2**. إذا كان **A2** يحتوي على الرقم `1`، فستظهر القيمة `1` في كل خلية لأن `EXPAND` يكرر قيمة المصدر عبر النطاق الموسع.

## الكود الكامل القابل للتنفيذ

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### النتيجة المتوقعة

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

(القيم الفعلية تعتمد على ما يحتويه `A2` في ملفك المصدر.)

## الاختلافات الشائعة وحالات الحافة

| السيناريو | تغيير الكود | السبب |
|----------|-------------|--------|
| **خلية بداية مختلفة** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | استخدم أي خلية كمرجع؛ الصيغة تتوسع نسبةً إلى تلك الخلية. |
| **حجم توسيع متغير** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | يسمح بنطاقات تُحدد أثناء وقت التشغيل، مفيد في التقارير المعتمدة على البيانات. |
| **توسيع بحجم صفر** | `=EXPAND(A2,0,0)` | يُعيد قيمة الخلية الأصلية فقط؛ مفيد للمنطق الشرطي حيث قد تزيد الحجم لاحقًا. |
| **استخدام نطاق مسمى** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | يعمل عندما يكون `MyRange` معرفًا في المصنف؛ يبقي الصيغ قابلة للقراءة. |

> **احذر من:** الحد الأقصى لحجم المصفوفة في Excel (16,384 عمود × 1,048,576 صف). محاولة التوسيع بما يتجاوز هذه الحدود ستؤدي إلى خطأ في الحساب.

## نصائح التصحيح

* **الصيغة لا تُقيم؟** تأكد من استدعاء `workbook.calculateFormula();` بعد كل `setFormula`.  
* **قيم غير متوقعة؟** تحقق من أن خلية المرجع (`A2` في المثال) تحتوي على البيانات التي تريد نشرها.  
* **مخاوف الأداء** – التوسعات الكبيرة قد تكون مكلفة. إذا كنت تحتاج فقط إلى جزء من النطاق، قلل من معطيات الصف/العمود.

## الخلاصة

أصبح لديك الآن مثال كامل على **aspose cells set formula** يوضح **كيفية استخدام EXPAND** في Java. من خلال تحميل المصنف، تعيين صيغة `EXPAND`، إعادة الحساب، ثم الحفظ، يمكنك إنشاء نطاقات ديناميكية دون الحاجة إلى التفاعل اليدوي مع Excel.

من هنا يمكنك استكشاف:

* استخدام دوال ديناميكية أخرى مثل `FILTER` أو `SEQUENCE` مع Aspose.Cells.  
* دمج المنطق في خدمة ويب تُنشئ تقارير حسب الطلب.  
* الجمع بين `EXPAND` وتنسيق الخلايا الشرطي عبر واجهة برمجة Aspose.Cells.

لا تتردد في تجربة خلايا بداية مختلفة، أحجام متغيرة، أو نطاقات مسماة لتتناسب مع سيناريو الأتمتة الخاص بك. إذا وجدت مثال **دالة EXPAND** مفيدًا، شاركه مع فريقك أو ساهم بتحسينات على GitHub. Happy coding!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إتقان Aspose.Cells Java: كيفية إيقاف حساب الصيغ في Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [تحويل جداول Excel إلى نطاقات باستخدام Aspose.Cells Java&#58; دليل خطوة بخطوة](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [كيفية تعيين إصدار مستند Excel باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}