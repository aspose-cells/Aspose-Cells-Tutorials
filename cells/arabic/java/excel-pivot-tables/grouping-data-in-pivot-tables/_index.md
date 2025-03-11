---
title: تجميع البيانات في جداول محورية
linktitle: تجميع البيانات في جداول محورية
second_title: واجهة برمجة تطبيقات معالجة Excel في Java من Aspose.Cells
description: تعرف على كيفية إنشاء جداول محورية في Excel باستخدام Aspose.Cells for Java. قم بأتمتة تجميع البيانات وتحليلها باستخدام أمثلة التعليمات البرمجية المصدرية.
weight: 14
url: /ar/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تجميع البيانات في جداول محورية


تُعد الجداول المحورية أداة فعّالة لتحليل البيانات وتلخيصها في جداول البيانات. فهي تسمح لك بتجميع البيانات وتصنيفها للحصول على رؤى قيّمة. في هذه المقالة، سنستكشف كيفية تجميع البيانات بفعالية في الجداول المحورية باستخدام Aspose.Cells for Java، إلى جانب أمثلة التعليمات البرمجية المصدرية.

## مقدمة

توفر جداول البيانات المحورية طريقة مرنة لتنظيم البيانات وتلخيصها من مجموعات البيانات الكبيرة. وهي تسمح لك بإنشاء وجهات نظر مخصصة لبياناتك من خلال تجميعها في فئات أو تسلسلات هرمية. ويمكن أن يساعدك هذا في تحديد الاتجاهات والأنماط والقيم المتطرفة في بياناتك بسهولة أكبر.

## الخطوة 1: إنشاء جدول محوري

لنبدأ بإنشاء جدول محوري باستخدام Aspose.Cells for Java. فيما يلي مثال لكيفية إنشاء جدول محوري من ملف Excel نموذجي.

```java
// تحميل ملف Excel
Workbook workbook = new Workbook("sample.xlsx");

// الوصول إلى ورقة العمل التي تحتوي على البيانات
Worksheet worksheet = workbook.getWorksheets().get(0);

// تحديد نطاق البيانات
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // بافتراض 20 صفًا من البيانات
sourceData.startColumn = 0;
sourceData.endColumn = 3; // بافتراض وجود 4 أعمدة من البيانات

// إنشاء جدول محوري بناءً على نطاق البيانات
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// احصل على جدول المحور حسب الفهرس
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// إضافة الحقول إلى الصفوف والأعمدة
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// إضافة القيم وتطبيق التجميع
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// حفظ ملف Excel المعدل
workbook.save("output.xlsx");
```

## الخطوة 2: تجميع البيانات

 في Aspose.Cells لـ Java، يمكنك تجميع البيانات داخل جدول المحور باستخدام`PivotField` فيما يلي مثال لكيفية تجميع حقل في جدول محوري:

```java
// الوصول إلى حقل "المنتج" في الجدول المحوري
PivotField productField = pivotTable.getPivotFields().get("Product");

//قم بتجميع حقل "المنتج" حسب معيار محدد، على سبيل المثال، حسب الحرف الأول
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// حفظ ملف Excel المعدّل بالبيانات المجمعة
workbook.save("output_grouped.xlsx");
```

## الخطوة 3: تخصيص التجميع

يمكنك تخصيص إعدادات التجميع بشكل أكبر، مثل تحديد فترات التجميع المستندة إلى التاريخ أو قواعد التجميع المخصصة. فيما يلي مثال لتخصيص التجميع المستند إلى التاريخ:

```java
// الوصول إلى حقل "التاريخ" في الجدول المحوري (على افتراض أنه حقل تاريخ)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// تواريخ المجموعة حسب الأشهر
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// حفظ ملف Excel المعدّل باستخدام مجموعة التاريخ المخصصة
workbook.save("output_custom_grouping.xlsx");
```

## خاتمة

إن تجميع البيانات في جداول محورية يعد تقنية قيمة لتحليل البيانات وتلخيصها في Excel، كما يسهل برنامج Aspose.Cells for Java أتمتة هذه العملية. باستخدام أمثلة التعليمات البرمجية المصدرية المقدمة، يمكنك إنشاء جداول محورية وتخصيص التجميع والحصول على رؤى من بياناتك بكفاءة.

## الأسئلة الشائعة

### 1. ما هو الغرض من الجداول المحورية في Excel؟

تُستخدم الجداول المحورية في Excel لتلخيص وتحليل مجموعات البيانات الكبيرة. وهي تسمح لك بإنشاء عروض مخصصة لبياناتك، مما يجعل من السهل تحديد الأنماط والاتجاهات.

### 2. كيف يمكنني تخصيص تجميع البيانات في جدول محوري؟

 يمكنك تخصيص تجميع البيانات في جدول محوري باستخدام`PivotField` الفئة في Aspose.Cells لـ Java. يتيح لك هذا تحديد معايير التجميع، مثل الفواصل الزمنية القائمة على التاريخ أو القواعد المخصصة.

### 3. هل يمكنني أتمتة إنشاء الجداول المحورية باستخدام Aspose.Cells لـ Java؟

نعم، يمكنك أتمتة إنشاء جداول محورية في Excel باستخدام Aspose.Cells for Java، كما هو موضح في أمثلة التعليمات البرمجية المصدر المقدمة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
