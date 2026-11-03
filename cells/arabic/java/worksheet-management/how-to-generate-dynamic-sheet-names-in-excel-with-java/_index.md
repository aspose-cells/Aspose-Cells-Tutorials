---
category: general
date: 2026-09-27
description: تعرّف على كيفية إنشاء أسماء أوراق ديناميكية في Excel باستخدام Java أثناء
  ملء قالب Excel وإنشاء أوراق من البيانات لتقارير قوية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: ar
lastmod: 2026-09-27
og_description: تسمح لك أسماء الأوراق الديناميكية بإنشاء أوراق متعددة من مجموعة بيانات.
  يوضح هذا الدرس كيفية تعبئة قالب Excel في Java وإنشاء أوراق من البيانات باستخدام
  Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: إنشاء أسماء أوراق عمل ديناميكية في Excel باستخدام Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية إنشاء أسماء أوراق ديناميكية في Excel باستخدام Java
url: /ar/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء أسماء أوراق ديناميكية في Excel باستخدام Java

إذا كنت بحاجة إلى **أسماء أوراق ديناميكية** عند ملء قالب Excel في Java، فإن هذا الدليل يشرح العملية بالكامل. ستتعرف على كيفية *إنشاء أوراق متعددة* من مجموعة من البيانات، وكيف يحصل كل ورق على اسم فريد تلقائيًا. في النهاية ستحصل على مثال قابل للتنفيذ ينشئ أوراقًا من البيانات ويحفظ النتيجة باستخدام نمط التسمية المطلوب.

إن إنشاء الأوراق أثناء التشغيل هو طلب شائع لتقارير اللوحات، دفعات الفواتير، أو أي سيناريو لا يُعرف فيه عدد أقسام التفاصيل مسبقًا. تجعل محرك العلامات الذكية (Smart Marker) في Aspose.Cells هذه المهمة مختصرة وموثوقة، ويظهر الكود أدناه النهج الموصى به.

## استخدام أسماء أوراق ديناميكية مع Aspose.Cells

توفر Aspose.Cells for Java معالج **Smart Marker** يمكنه قراءة العلامات النائبة في دفتر عمل القالب وتوسيعها إلى صفوف أو أعمدة أو حتى أوراق عمل جديدة. من خلال ضبط `SmartMarkerOptions.DetailSheetNewName` يمكنك التحكم في اسم كل ورقة يتم إنشاؤها. يتم استبدال العلامة `{0}` بمؤشر الصف الحالي (بدءًا من الصفر)، مما يمنحك أسماء أوراق **ديناميكية** مثل `Detail_0`، `Detail_1`، …​.

> **نصيحة احترافية:** احتفظ بملف قالب دفتر العمل في مجلد موارد مخصص واستخدم مسارًا نسبيًا كلما أمكن. هذا يجنب الترميز الصلب للمسارات المطلقة التي قد تتعطل في بيئات مختلفة.

## الخطوة 1: تحميل قالب Excel (populate excel template java)

أولاً، قم بتحميل دفتر العمل الذي يحتوي على علامات Smart Marker. يجب أن يحتوي القالب على ورقة مسماة، على سبيل المثال، `Detail` مع علامة مثل `&=Orders!A1` تُخبر المعالج بمكان بدء إدراج الصفوف.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*لماذا هذه الخطوة مهمة:* يحدد القالب التخطيط (العناوين، الصيغ، التنسيق) الذي سيتم نسخه إلى كل ورقة يتم إنشاؤها. بدون قالب مناسب، سيفقد الناتج التنسيق والصيغ.

## الخطوة 2: إعداد مصدر البيانات لإنشاء أوراق من البيانات

بعد ذلك، أنشئ مصدر بيانات يمكن لمعالج Smart Marker التكرار عبره. في هذا المثال نستخدم `Map<String, Object>` حيث المفتاح `"Orders"` يطابق اسم العلامة في القالب.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*لماذا هذه الخطوة مهمة:* يقرأ محرك Smart Marker المصفوفة، ينشئ صفًا لكل `Object[]` داخلي، وبما أننا سنطلب منه إنشاء أوراق جديدة، فإنه ينشئ ورقة عمل منفصلة لكل صف. هذا هو جوهر **إنشاء أوراق من البيانات**.

## الخطوة 3: ضبط SmartMarkerOptions لإنشاء أوراق متعددة بأسماء فريدة

الآن أخبر Aspose.Cells كيف يسمي كل ورقة عمل جديدة. يتم استبدال العلامة `{0}` بمؤشر الصف الحالي.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*لماذا هذه الخطوة مهمة:* بدون ضبط `DetailSheetNewName`، سيعيد المعالج استخدام اسم الورقة الأصلية لكل صف، مما يؤدي إلى استبدال البيانات. هذا الخيار هو ما يتيح **أسماء أوراق ديناميكية**.

## الخطوة 4: معالجة SmartMarkers وإنشاء دفتر العمل

شغّل المعالج مع مصدر البيانات والخيارات التي قمنا بضبطها للتو.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*لماذا هذه الخطوة مهمة:* يقوم المعالج بتوسيع العلامات، وإنشاء العدد المطلوب من أوراق العمل، ونسخ تخطيط القالب، وتعبئة كل ورقة بالبيانات المقابلة للصف.

## الخطوة 5: حفظ النتيجة والتحقق منها

أخيرًا، اكتب دفتر العمل إلى القرص. افتح الملف في Excel لرؤية الأوراق التي تم إنشاؤها تلقائيًا.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**الناتج المتوقع**

عند فتح `MasterDetailResult.xlsx` يجب أن ترى ثلاث أوراق عمل جديدة:

* `Detail_0` – يحتوي على الطلب 101 (Alice، 250.00)  
* `Detail_1` – يحتوي على الطلب 102 (Bob، 175.50)  
* `Detail_2` – يحتوي على الطلب 103 (Carol، 320.75)

كل ورقة تحتفظ بالتنسيق، وعرض الأعمدة، وأي صيغ كانت موجودة في ورقة القالب الأصلية `Detail`.

## مثال كامل قابل للتنفيذ

جمع جميع الأقسام معًا يمنحك برنامجًا مستقلًا يمكنك تجميعه وتشغيله:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### كيفية التشغيل

1. أضف ملف JAR الخاص بـ Aspose.Cells for Java إلى مسار الفئات (classpath) في مشروعك (متوفر عبر Maven Central أو موقع Aspose).  
2. ضع `MasterDetailTemplate.xlsx` في المجلد `templates/` نسبةً إلى جذر المشروع.  
3. نفّذ طريقة `main`. سيحتوي المجلد `output/` على الملف الناتج.

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **نمط تسمية مختلف** | استخدم `"OrderSheet_{0}_v{1}"` وأدرج علامات نائبة إضافية مثل `{1}` لتمثيل فهرس ثانٍ (مثلاً رقم الصفحة). |
| **مجموعات بيانات ضخمة** | زد حجم ذاكرة JVM (`-Xmx2g`) لتجنب `OutOfMemoryError` عند إنشاء مئات الأوراق. |
| **إنشاء أوراق شرطية** | قبل استدعاء `process`، قم بترشيح مصفوفة البيانات بحيث تُستبعد الصفوف التي لا تفي بالمعايير، مما يمنع إنشاء أوراق غير ضرورية. |
| **الحفاظ على الصيغ التي تشير إلى أوراق أخرى** | احتفظ باسم الورقة الأصلي كعلامة نائبة مخفية (مثلاً `DetailTemplate`) واستخدم `SmartMarkerOptions.setDetailSheetNewName` فقط للاسم الظاهر؛ الصيغ التي تشير إلى الاسم المخفي ستظل تعمل بشكل صحيح. |

## نصائح لأتمتة Excel قوية

* **تحقق من صحة مصدر البيانات** – تأكد من أن كل مصفوفة داخلية تحتوي على نفس عدد العناصر كما هو معرف في الأعمدة بالقالب؛ الاختلاف يسبب أخطاء وقت التشغيل.  
* **استخدم النطاقات المسماة** في القالب لتبسيط صياغة Smart Marker (`&=Orders!A1`).  
* **أغلق الموارد** – رغم أن Aspose.Cells يدير التدفقات داخليًا، فإن استدعاء `templateWorkbook.dispose()` ضمن كتلة `finally` يسرّع تحرير الذاكرة الأصلية.  
* **اختبر القيم الحدية** – يجب أن ينتج عن صفر صفوف دفتر عمل يحتوي فقط على ورقة القالب الأصلية؛ مصدر بيانات فارغ يثبت أن الكود يتعامل مع حالة “لا بيانات” بسلاسة.

## الخلاصة

أنت الآن تعرف كيف **تنشئ أسماء أوراق ديناميكية** في Excel باستخدام Java، وكيف **تملأ قالب Excel** وت **تنشئ أوراقًا من البيانات**، وكيف **تنشئ أوراقًا متعددة** تلقائيًا باستخدام Smart Markers في Aspose.Cells. باتباع الخطوات أعلاه يمكنك تعديل النمط لأي سيناريو تقارير—سواء كنت تحتاج إلى العشرات من أوراق التفاصيل، أو نمط تسمية مخصص، أو إنشاء أوراق شرطية.

هل تريد توسيع هذا الحل؟ جرّب إضافة مخططات إلى كل ورقة تم إنشاؤها، أو صدّر دفتر العمل إلى PDF باستخدام `Workbook.save("result.pdf", SaveFormat.PDF)`. كلا التقنيتين يبنيان على أساس الأوراق الديناميكية الذي تعلمته للتو. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Master Dynamic Excel Sheets in Java with Aspose.Cells: A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}