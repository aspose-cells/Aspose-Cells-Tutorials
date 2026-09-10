---
date: '2026-07-07'
description: تعلم مثال Aspose Cells للمخطط لإنشاء Pivot Charts ديناميكية في Excel
  باستخدام Java. اتبع التعليمات خطوة بخطوة لتحليل بيانات سلس.
keywords:
- aspose cells chart example
- how to create pivot chart
- dynamic pivot chart excel
- export pivot chart excel
- add pivot chart workbook
og_description: تعلم مثال Aspose Cells للمخطط لإنشاء Pivot Charts ديناميكية في Excel
  باستخدام Java. اتبع التعليمات خطوة بخطوة لتحليل بيانات سلس.
og_title: 'مثال Aspose Cells على المخطط: إتقان Pivot Charts في Java'
schemas:
- author: Aspose
  dateModified: '2026-07-07'
  description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  headline: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  type: TechArticle
- description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  name: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  steps:
  - name: Load the Source Workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory.
  - name: Add a Worksheet for the Pivot Chart
    text: Create a dedicated chart sheet to keep the visual separate from raw data.
  - name: Insert a Pivot Table
    text: First, define the data range for the pivot table, then add it to the chart
      sheet. The `PivotTable` class represents a pivot table in a worksheet and provides
      methods to define its data source, layout, and calculations.
  - name: Create and Configure the Pivot Chart
    text: The `Chart` class represents any Excel chart. Here we create a column chart
      linked to the pivot table.
  - name: Export the Workbook
    text: Save the workbook with the new pivot chart to an `.xlsx` file, or directly
      to PDF if you need a static report.
  type: HowTo
- questions:
  - answer: Yes, call `chart.toImage("chart.png", ImageFormat.PNG)` after configuring
      the chart.
    question: Can I export a pivot chart directly to an image file?
  - answer: The library can preserve existing VBA macros, but it does not create or
      modify them programmatically.
    question: Does Aspose.Cells support Excel macros in pivot charts?
  - answer: Absolutely—invoke `pivotTable.refreshData()` and then `chart.refresh()`
      to reflect the latest values.
    question: Is it possible to update the pivot chart after changing the source data?
  - answer: Over 40 types, including column, line, area, pie, radar, and stacked bar,
      all fully supported for pivot data.
    question: Which chart types are available for pivot charts?
  - answer: Yes, a purchased license removes evaluation limits and enables full feature
      set.
    question: Do I need a license to use the Maven/Gradle setup in production?
  type: FAQPage
title: 'مثال Aspose Cells على المخطط: إتقان Pivot Charts في Java'
url: /ar/java/charts-graphs/aspose-cells-java-pivot-charts-excel-tutorial/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose Cells للرسوم البيانية: إتقان الرسوم البيانية المحورية في Java

في عالم اليوم القائم على البيانات، تحويل الأرقام الخام إلى رؤى بصرية واضحة أمر أساسي. يوضح هذا الدرس **aspose cells chart example** الذي تحتاجه لإنشاء رسوم بيانية محورية ديناميكية في Excel باستخدام Java. بنهاية هذا الدليل ستتمكن من تحميل دفتر عمل، إضافة ورقة رسوم بيانية مخصصة، ربط جدول محوري، وتصدير النتيجة—كل ذلك ببضع أسطر من الشيفرة.

## إجابات سريعة
- **ما هو الصنف الأساسي للعمل مع ملفات Excel؟** `Workbook` يمثل ملف Excel كامل في الذاكرة.  
- **أي حزمة Maven تضيف Aspose.Cells إلى المشروع؟** `com.aspose:aspose-cells` (الإصدار 25.3 أو أحدث).  
- **هل يمكن إنشاء رسم بياني محوري بدون ترخيص؟** نعم، النسخة التجريبية المجانية تعمل للتطوير، لكن الترخيص يزيل حدود التقييم.  
- **كم عدد أنواع الرسوم البيانية التي يدعمها Aspose.Cells؟** أكثر من 40 نوعًا، بما في ذلك الخطية، العمودية، الدائرية، والرادارية.  
- **ما هي أسرع طريقة لتصدير رسم بياني محوري إلى PDF؟** استدعِ `chart.toPdf("output.pdf")` بعد تكوين مصدر بيانات الرسم.

## ما هو الرسم البياني المحوري في Excel؟
**الرسم البياني المحوري** هو تمثيل بصري تفاعلي لجدول محوري، يتيح للمستخدمين استكشاف البيانات المجمعة ديناميكيًا. باستخدام Aspose.Cells، يمكنك إنشاء هذه الرسوم برمجيًا دون فتح Excel. يتم تحديثه تلقائيًا عندما يتغير الجدول المحوري الأساسي، يدعم الفلترة، ويمكن تخصيصه بأنواع مختلفة من الرسوم، العناوين، والأساطير، مما يجعله أداة قوية لتحليل البيانات.

## لماذا نستخدم Aspose.Cells لـ Java لإنشاء الرسوم البيانية المحورية؟
معالجة Aspose.Cells **أكثر من 50 تنسيقًا للإدخال والإخراج** ويمكنه التعامل مع دفاتر عمل تحتوي على **مئات الأوراق** مع الحفاظ على استهلاك الذاكرة أقل من 200 ميغابايت. يتيح API الخاص به إنشاء وتعديل وعرض الرسوم في **أقل من ثانيتين** لمجموعات البيانات النموذجية بحجم 10 KB، مما يجعله مثاليًا للتقارير على الخادم.

## المتطلبات المسبقة

- **Aspose.Cells for Java** الإصدار 25.3 أو أحدث.  
- نظام بناء Maven أو Gradle.  
- JDK 8 أو أحدث وIDE مثل IntelliJ IDEA أو Eclipse أو NetBeans.  
- معرفة أساسية بـ Java؛ familiarity مع Excel مفيدة ولكن ليست ضرورية.

### المكتبات والاعتمادات المطلوبة
- **Maven:** أضف اعتماد Aspose.Cells (انظر قسم *aspose cells maven setup* أدناه).  
- **Gradle:** أدرج نفس الحزمة في ملف `build.gradle`.

### خطوات الحصول على الترخيص
- **نسخة تجريبية:** ابدأ بنسخة تجريبية لاستكشاف مثال aspose cells chart.  
- **ترخيص مؤقت:** احصل على مفتاح مؤقت للاختبار الموسع.  
- **شراء:** اشترِ ترخيصًا كاملًا من [الموقع الرسمي لـ Aspose](https://purchase.aspose.com/buy).

## كيفية إعداد Aspose.Cells لـ Java

### اعتماد Maven (aspose cells maven setup)

أضف المقتطف التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```

### اعتماد Gradle

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### التهيئة الأساسية
بعد إضافة الاعتماد، قم بتهيئة المكتبة كما هو موضح أدناه:

```java
// Initialize license (optional for trial)
License license = new License();
license.setLicense("Aspose.Cells.lic");

// Create a Workbook object – this loads or creates an Excel file.
Workbook workbook = new Workbook();
```

## كيفية إنشاء رسم بياني محوري باستخدام Aspose.Cells لـ Java؟

حمّل بيانات المصدر، أنشئ جدولًا محوريًا، واربطه برسم بياني—كل ذلك في خطوات بسيطة. تتضمن العملية تحميل دفتر عمل يحتوي على بيانات المصدر، إنشاء جدول محوري لتلخيص تلك البيانات، إضافة ورقة رسم بياني مخصصة، ربط الجدول المحوري بالرسم، تخصيص مظهر الرسم، وأخيرًا حفظ دفتر العمل بالتنسيق المطلوب.

### الخطوة 1: تحميل دفتر العمل المصدر
الصنف `Workbook` هو الكائن الأعلى مستوى في Aspose.Cells الذي يمثل ملف Excel واحد في الذاكرة.

```java
Workbook workbook = new Workbook("data.xlsx");
```

### الخطوة 2: إضافة ورقة عمل للرسم البياني المحوري
أنشئ ورقة رسم بياني مخصصة لتبقي العرض منفصلًا عن البيانات الخام.

```java
int chartSheetIndex = workbook.getWorksheets().addChart("PivotChartSheet");
Worksheet chartSheet = workbook.getWorksheets().get(chartSheetIndex);
```

### الخطوة 3: إدراج جدول محوري
أولاً، حدد نطاق البيانات للجدول المحوري، ثم أضفه إلى ورقة الرسم البياني.

الصنف `PivotTable` يمثل جدولًا محوريًا في ورقة عمل ويوفر طرقًا لتحديد مصدر البيانات، التخطيط، والحسابات.

```java
int pivotTableIndex = chartSheet.getPivotTables().add("A1:D100", "PivotTable1", 0, 0);
PivotTable pivotTable = chartSheet.getPivotTables().get(pivotTableIndex);
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);   // Category
pivotTable.addFieldToArea(PivotFieldType.DATA, 1);  // Values
```

### الخطوة 4: إنشاء وتكوين الرسم البياني المحوري
الصنف `Chart` يمثل أي رسم بياني في Excel. هنا ننشئ رسمًا عموديًا مرتبطًا بالجدول المحوري.

```java
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 5, 0, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
chart.getNSeries().add("=PivotTable1!$B$2:$B$5", true);
chart.setTitle("Sales by Region");
```

### الخطوة 5: تصدير دفتر العمل
احفظ دفتر العمل مع الرسم البياني المحوري الجديد إلى ملف `.xlsx`، أو مباشرة إلى PDF إذا كنت تحتاج إلى تقرير ثابت.

```java
workbook.save("PivotChartResult.xlsx", SaveFormat.XLSX);
// Optional PDF export
workbook.save("PivotChartResult.pdf", SaveFormat.PDF);
```

## تطبيقات عملية للرسوم البيانية المحورية الديناميكية

- **التقارير المالية:** إنشاء لوحات معلومات ربع سنوية تتحدث تلقائيًا عند استيراد بيانات جديدة.  
- **تحليل المبيعات:** تصور اتجاهات المبيعات الإقليمية باستدعاء API واحد.  
- **إدارة المخزون:** تتبع مستويات المخزون ونقاط إعادة الطلب في الوقت الفعلي.  
- **رؤى العملاء:** دمج البيانات الديموغرافية مع تاريخ الشراء لرسوم بيانية تفاعلية.  
- **إدارة المشاريع:** عرض تخصيص الموارد واختلاف الجداول الزمنية باستخدام الرسوم المحورية.

## نصائح الأداء لمجموعات البيانات الكبيرة

- **إدارة الذاكرة:** استدعِ `workbook.dispose()` بعد الحفظ لتحرير الموارد الأصلية.  
- **عمليات الدفعات:** استخدم `CellsHelper.copyRange` لنقل كتل بيانات كبيرة بدلاً من حلقات خلية‑بخلية.  
- **التحميل الكسول:** عند معالجة ملفات أكبر من 100 ميغابايت، فعّل `LoadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` لتقليل استهلاك الذاكرة.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **الجدول المحوري لا يعكس البيانات الجديدة** | قم بتحديث الجدول المحوري باستخدام `pivotTable.refreshData()` قبل إنشاء الرسم. |
| **الرسم يظهر فارغًا** | تأكد من أن نطاق مصدر بيانات الرسم يتطابق مع نطاق نتيجة الجدول المحوري. |
| **أخطاء نفاد الذاكرة على ملفات ضخمة** | استخدم `LoadOptions` مع `MemorySetting.MEMORY_PREFERENCE` وأغلق الأوراق التي لم تعد بحاجة إليها. |

## الأسئلة المتكررة

**س: هل يمكن تصدير رسم بياني محوري مباشرة إلى ملف صورة؟**  
ج: نعم، استدعِ `chart.toImage("chart.png", ImageFormat.PNG)` بعد تكوين الرسم.

**س: هل يدعم Aspose.Cells وحدات ماكرو Excel في الرسوم المحورية؟**  
ج: يمكن للمكتبة الحفاظ على وحدات VBA الموجودة، لكنها لا تنشئها أو تعدلها برمجيًا.

**س: هل يمكن تحديث الرسم البياني المحوري بعد تغيير بيانات المصدر؟**  
ج: بالتأكيد—استدعِ `pivotTable.refreshData()` ثم `chart.refresh()` لتحديث القيم الأخيرة.

**س: ما هي أنواع الرسوم المتاحة للرسوم المحورية؟**  
ج: أكثر من 40 نوعًا، بما في ذلك العمودي، الخطي، المساحي، الدائري، الراداري، والعمودي المتراكم، جميعها مدعومة بالكامل للبيانات المحورية.

**س: هل أحتاج إلى ترخيص لاستخدام إعداد Maven/Gradle في الإنتاج؟**  
ج: نعم، الترخيص المشتري يزيل حدود التقييم ويفعل مجموعة الميزات الكاملة.

---

**آخر تحديث:** 2026-07-07  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

## الموارد

- [توثيق Aspose.Cells](https://reference.aspose.com/cells/java/)  
- [تحميل Aspose.Cells لـ Java](https://releases.aspose.com/cells/java/)  
- [شراء ترخيص](https://purchase.aspose.com/buy)  
- [نسخة تجريبية وتراخيص مؤقتة](https://releases.aspose.com/cells/java/)  
- [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

```java
import com.aspose.cells.Workbook;

// Load an existing workbook
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
```

```java
   import com.aspose.cells.Workbook;
   ```

```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
   ```

```java
   import com.aspose.cells.SheetType;
   import com.aspose.cells.Worksheet;
   ```

```java
   int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
   Worksheet sheet3 = workbook.getWorksheets().get(sheetIndex);
   sheet3.setName("PivotChart");
   ```

```java
   import com.aspose.cells.Chart;
   import com.aspose.cells.ChartType;
   ```

```java
   int chartIndex = sheet3.getCharts().add(ChartType.COLUMN, 0, 5, 28, 16);
   Chart chart = sheet3.getCharts().get(chartIndex);
   ```

```java
   chart.setPivotSource("PivotTable!PivotTable1");
   chart.setHidePivotFieldButtons(false);
   ```

```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   workbook.save(outDir + "/CPCBasedOnPTable_out.xls");
   ```

## دروس ذات صلة

- [إتقان الجداول المحورية في Excel باستخدام Aspose.Cells لـ Java: دليل شامل لتحليل البيانات](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)  
- [إنشاء دفتر عمل وإضافة رسوم بيانية باستخدام Aspose.Cells لـ Java: دليل شامل](/cells/java/charts-graphs/create-workbook-add-charts-aspose-cells-java/)  
- [تخصيص رسوم Excel في Java: إتقان Aspose.Cells لتصور البيانات بسلاسة](/cells/java/charts-graphs/excel-chart-customization-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}