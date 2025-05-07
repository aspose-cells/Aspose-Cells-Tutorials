---
"description": "تعلّم كيفية إنشاء جداول محورية في Excel باستخدام Aspose.Cells لجافا. أتمتة تجميع البيانات وتحليلها باستخدام أمثلة من أكواد المصدر."
"linktitle": "تجميع البيانات في جداول محورية"
"second_title": "واجهة برمجة تطبيقات معالجة Excel لـ Aspose.Cells Java"
"title": "تجميع البيانات في جداول محورية"
"url": "/ar/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تجميع البيانات في جداول محورية


تُعد الجداول المحورية أداة فعّالة لتحليل البيانات وتلخيصها في جداول البيانات. فهي تتيح لك تجميع البيانات وتصنيفها للحصول على رؤى قيّمة. في هذه المقالة، سنستكشف كيفية تجميع البيانات بفعالية في الجداول المحورية باستخدام Aspose.Cells لجافا، بالإضافة إلى أمثلة على الكود المصدري.

## مقدمة

تُوفر جداول البيانات المحورية طريقةً مرنةً لتنظيم البيانات وتلخيصها من مجموعات بيانات كبيرة. فهي تُتيح لك إنشاء عروض مُخصصة لبياناتك من خلال تجميعها في فئات أو تسلسلات هرمية. يُساعدك هذا على تحديد الاتجاهات والأنماط والقيم الشاذة في بياناتك بسهولة أكبر.

## الخطوة 1: إنشاء جدول محوري

لنبدأ بإنشاء جدول محوري باستخدام Aspose.Cells لجافا. فيما يلي مثال لكيفية إنشاء جدول محوري من ملف Excel نموذجي.

```java
// تحميل ملف Excel
Workbook workbook = new Workbook("sample.xlsx");

// الوصول إلى ورقة العمل التي تحتوي على البيانات
Worksheet worksheet = workbook.getWorksheets().get(0);

// تحديد نطاق البيانات
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // بافتراض وجود 20 صفًا من البيانات
sourceData.startColumn = 0;
sourceData.endColumn = 3; // بافتراض وجود 4 أعمدة من البيانات

// إنشاء جدول محوري استنادًا إلى نطاق البيانات
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

في Aspose.Cells لـ Java، يمكنك تجميع البيانات داخل جدول المحور باستخدام `PivotField` الصف. إليك مثال لكيفية تجميع حقل في جدول محوري:

```java
// الوصول إلى حقل "المنتج" في الجدول المحوري
PivotField productField = pivotTable.getPivotFields().get("Product");

// قم بتجميع حقل "المنتج" حسب معيار محدد، على سبيل المثال، حسب الحرف الأول
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// حفظ ملف Excel المعدل مع البيانات المجمعة
workbook.save("output_grouped.xlsx");
```

## الخطوة 3: تخصيص التجميع

يمكنك تخصيص إعدادات التجميع بشكل أكبر، مثل تحديد فترات تجميع مبنية على التاريخ أو قواعد تجميع مخصصة. إليك مثال على تخصيص التجميع بناءً على التاريخ:

```java
// الوصول إلى حقل "التاريخ" في الجدول المحوري (على افتراض أنه حقل تاريخ)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// تواريخ المجموعة حسب الأشهر
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// حفظ ملف Excel المعدّل مع تجميع التاريخ المخصص
workbook.save("output_custom_grouping.xlsx");
```

## خاتمة

يُعد تجميع البيانات في جداول محورية تقنية قيّمة لتحليل البيانات وتلخيصها في Excel، ويُسهّل Aspose.Cells لـ Java أتمتة هذه العملية. باستخدام أمثلة التعليمات البرمجية المصدرية المُقدّمة، يمكنك إنشاء جداول محورية، وتخصيص التجميع، والاستفادة من بياناتك بكفاءة.

## الأسئلة الشائعة

### 1. ما هو الغرض من الجداول المحورية في Excel؟

تُستخدم جداول البيانات المحورية في Excel لتلخيص وتحليل مجموعات البيانات الكبيرة. تتيح لك هذه الجداول إنشاء عروض مخصصة لبياناتك، مما يُسهّل تحديد الأنماط والاتجاهات.

### 2. كيف يمكنني تخصيص تجميع البيانات في جدول محوري؟

يمكنك تخصيص تجميع البيانات في جدول محوري باستخدام `PivotField` في Aspose.Cells لجافا، يمكنك تحديد معايير التجميع، مثل الفواصل الزمنية القائمة على التاريخ أو القواعد المخصصة.

### 3. هل يمكنني أتمتة إنشاء الجداول المحورية باستخدام Aspose.Cells لـ Java؟

نعم، يمكنك أتمتة إنشاء جداول البيانات المحورية في Excel باستخدام Aspose.Cells for Java، كما هو موضح في أمثلة التعليمات البرمجية المصدر المقدمة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}