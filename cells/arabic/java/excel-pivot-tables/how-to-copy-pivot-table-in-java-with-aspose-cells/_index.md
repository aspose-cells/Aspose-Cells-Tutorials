---
category: general
date: 2026-11-19
description: تعلم كيفية نسخ جدول محوري في Java مع الحفاظ على بياناته وتنسيقه. يوضح
  هذا الدليل خطوة بخطوة أيضًا كيفية نسخ الجداول المحورية في Excel بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: ar
lastmod: 2026-11-19
og_description: نسخ جدول محوري في جافا باستخدام Aspose.Cells. اتبع هذا الدليل لتتعلم
  كيفية الحفاظ على الجداول المحورية ونسخ بيانات الجداول المحورية في Excel بدقة.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: نسخ جدول محوري في جافا – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: كيفية نسخ جدول محوري في جافا باستخدام Aspose.Cells
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells

إذا كنت بحاجة إلى **نسخ جدول محوري** من مصنف إلى آخر، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك في Java. سواء كنت تبني محرك تقارير أو تقوم بترحيل البيانات، ستجد طريقة موثوقة للحفاظ على ذاكرة التخزين المؤقت للجدول المحوري، الحقول، والتنسيق.

نسخ جدول محوري قد يكون معقدًا لأن النسخ البسيط للنطاق غالبًا ما يفقد مصدر البيانات الأساسي. في هذا البرنامج التعليمي سنستخدم Aspose.Cells **كيفية نسخ جدول محوري** مع الحفاظ على جميع الحسابات، وسنغطي أيضًا **كيفية الحفاظ على الجداول المحورية** عندما يكون المصنف الوجهة فارغًا.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 17 أو أحدث مثبتة.
* Aspose.Cells for Java (الإصدار 23.9 أو أحدث) مضاف إلى مسار الفئات في مشروعك.
* ملفا Excel: مصنف مصدر يحتوي على الجدول المحوري ومصنف وجهة فارغ (أو مصنف تريد الدمج فيه).

لا تحتاج إلى أي ترخيص خاص لقطعة الكود، لكن ترخيص Aspose.Cells صالح يزيل علامات التقييم المائية.

## الخطوة 1: تحميل المصنف المصدر الذي يحتوي على الجدول المحوري

الخطوة الأولى هي فتح المصنف الذي يحمل الجدول المحوري الأصلي. تحميل الملف يمنحك الوصول إلى ورقة العمل، الخلايا، وذاكرة التخزين المؤقت للجدول المحوري.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*لماذا هذا مهم*: Aspose.Cells يقرأ المصنف بالكامل، بما في ذلك بيانات الذاكرة المخفية التي تشغل الجدول المحوري. بدون تحميل الملف بالكامل، ستفقد عملية النسخ تعريف الجدول المحوري.

## الخطوة 2: إعداد مصنف الوجهة

أنشئ مصنفًا جديدًا (أو افتح مصنفًا موجودًا) واحصل على ورقة العمل الأولى الخاصة به. هذا هو المكان الذي سيُوضع فيه الجدول المحوري.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*نصيحة*: إذا كان لديك بالفعل مصنف هدف، استبدل استدعاء `new Workbook()` بـ `new Workbook("target.xlsx")`. سيمكنك ذلك من **نسخ جدول محوري Excel** إلى مصنف مُعبأ مسبقًا.

## الخطوة 3: تحديد نطاق الخلايا الذي يحيط بالجدول المحوري

يجب عليك تحديد النطاق الدقيق الذي يغطي الجدول المحوري. يشمل النطاق جدول المحور، قائمة الحقول، وأي بيانات محيطة تريد الاحتفاظ بها.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*لماذا هذا مهم*: `CellArea` يخبر Aspose.Cells ما الذي يجب نسخه. إذا كان النطاق صغيرًا جدًا، سيُقصَّ الجدول المحوري؛ إذا كان كبيرًا جدًا، ستنسخ بيانات غير ضرورية. عدِّل الإحداثيات بناءً على حجم الجدول المحوري الفعلي لديك.

## الخطوة 4: تنفيذ عملية النسخ باستخدام CopyOptions

استخدم طريقة `copy` على مجموعة خلايا ورقة العمل المصدر. تمرير كائن `CopyOptions()` جديد يضمن نقل جميع التنسيقات، الصيغ، وذاكرة التخزين المؤقت للجدول المحوري.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### لماذا يحافظ `CopyOptions` على الجدول المحوري

`CopyOptions` يخبر Aspose.Cells بمعاملة النطاق ككائن *كامل* بدلاً من مجموعة مسطحة من القيم. هذه هي المفتاح لـ **كيفية الحفاظ على الجداول المحورية**: يتم تكرار ذاكرة التخزين المؤقت للجدول المحوري، وبالتالي يمكن لمصنف الوجهة إعادة حساب الجدول دون تدخل يدوي.

## الخطوة 5: حفظ مصنف الوجهة

أخيرًا، اكتب ملف الوجهة إلى القرص. الملف المحفوظ سيحتوي على نسخة كاملة الوظيفة من الجدول المحوري الأصلي.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*النتيجة المتوقعة*: فتح `copied_with_pivot.xlsx` في Excel يُظهر جدولًا محوريًا مطابقًا، كاملًا مع المقاطع، الفلاتر، والحقول المحسوبة. يمكنك تحديثه، وسيشير مصدر البيانات إلى النطاق المنسوخ داخل نفس المصنف.

---

![Diagram showing copy pivot table process](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram illustrating the copy pivot table workflow from source to destination workbook"}

## كيفية نسخ الجداول المحورية عبر أوراق عمل متعددة

إذا كنت بحاجة إلى **نسخ جدول محوري Excel** من عدة أوراق، كرّر الخطوتين 3‑4 لكل ورقة عمل مصدر. يمكنك أيضًا التكرار عبر `srcWb.getWorksheets()` ونسخ كل جدول محوري إلى ورقة مقابلة في `destWb`. إليك مثالًا مختصرًا على حلقة التكرار:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*نصيحة احترافية*: استخدم `srcWs.getPivotTables().getCount()` للتحقق مما إذا كانت الورقة تحتوي فعلاً على جدول محوري قبل النسخ. هذا يتجنب نسخ بيانات غير ذات صلة.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا تحدث | الحل |
|-------|----------------|-----|
| **يفقد الجدول المحوري ذاكرة التخزين المؤقت** | استخدام `Worksheet.copy()` بدون `CopyOptions` ينسخ القيم فقط. | استخدم دائمًا `srcWs.getCells().copy(..., new CopyOptions())`. |
| **تظهر أخطاء #REF! في الوجهة** | لا يزال الجدول المحوري المنسوخ يشير إلى مصدر بيانات خارجي في المصنف الأصلي. | بعد النسخ، استدعِ `destWs.getPivotTables().get(0).refresh();` لإعادة ربط الذاكرة بالنطاق الجديد. |
| **اختفاء المقاطع (Slicers)** | المقاطع مخزنة خارج نطاق الخلايا الرئيسي. | وسّع `CellArea` لتشمل نطاقات المقاطع، أو انسخ الورقة بالكامل (`srcWs.copy(destWs, new CopyOptions())`). |
| **تباطؤ الأداء عند الجداول المحورية الكبيرة** | نسخ نطاقات ضخمة مع تنسيقات قد يكون بطيئًا. | استخدم `CopyOptions.setOnlyData(true)` إذا لم تكن بحاجة إلى التنسيق، ثم أعد تطبيق الأنماط يدويًا. |

## كيفية الحفاظ على تنسيق الجدول المحوري أثناء تحديث البيانات

أحيانًا تحتاج إلى **كيفية الحفاظ على تنسيق الجدول المحوري** بعد تغيير بيانات المصدر. بعد النسخ، يمكنك قفل نمط الجدول المحوري:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

تعيين `PreserveFormatting` يضمن بقاء أي أنماط مخصصة طبقتها في المصدر بعد النسخ.

## التحقق من النسخ

طريقة سريعة لتأكيد نجاح النسخ هي مقارنة تعريفات الجداول المحورية:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

إذا تطابقت الأعداد وفتح الوجهة دون أخطاء، فقد نجحت في **نسخ جدول محوري**.

## الخلاصة

الآن تعرف كيف **تنسخ جدول محوري** من مصنف Excel إلى آخر باستخدام Aspose.Cells for Java، ورأيت الخطوات الدقيقة لـ **كيفية نسخ جدول محوري** مع ضمان بقاء ذاكرة التخزين المؤقت، التنسيق، والمقاطع سليمة. نفس النمط يعمل في سيناريوهات **نسخ جدول محوري Excel** عبر أوراق متعددة، ويمكنك تعديل الكود لتلبية حالات خاصة مثل الحفاظ على تنسيق الجدول المحوري أو التعامل مع مجموعات بيانات كبيرة.

### الخطوات التالية

* استكشف خيارات **حفظ جدول محوري** مثل `setPreserveFormatting` و `refresh` لمصادر البيانات الديناميكية.  
* جرّب نسخ الجداول المحورية بين مصنفات ذات ترتيب أعمدة مختلف—عدّل `CellArea` وفقًا لذلك.  
* دمج هذه التقنية مع Aspose.Slides لتضمين لقطات من الجداول المحورية في عروض PowerPoint.

برمجة سعيدة، ولا تتردد في تجربة تعديلات لتناسب خط أنابيب الأتمتة الخاص بك!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [How to copy a pivot table between worksheets in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [How to copy pivot table to a new workbook in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}