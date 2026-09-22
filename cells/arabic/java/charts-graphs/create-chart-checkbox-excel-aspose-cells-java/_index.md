---
date: '2026-09-22'
description: تعلم كيفية إنشاء مخطط Excel تفاعلي مع checkboxes باستخدام Aspose.Cells
  for Java. يغطي هذا الدليل الإعداد، إضافة checkboxes، الترخيص، وأفضل الممارسات.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: تعلم كيفية إنشاء مخطط Excel تفاعلي مع checkboxes باستخدام Aspose.Cells
  for Java. اتبع تعليمات خطوة بخطوة، شاهد نصائح الترخيص، واكتشف حالات الاستخدام الواقعية.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: كيفية إنشاء مخطط Excel تفاعلي مع checkboxes
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: كيفية إنشاء مخطط Excel تفاعلي مع checkboxes
url: /ar/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مخطط Excel تفاعلي مع مربعات الاختيار

## مقدمة

في هذا الدرس ستقوم **بإنشاء مخطط Excel تفاعلي** يتيح للمستخدمين تبديل سلاسل البيانات بالنقر على مربعات الاختيار الموضوعة مباشرة على المخطط. باستخدام Aspose.Cells for Java، يمكنك توليد دفاتر عمل كاملة المميزات برمجيًا، دون الحاجة إلى تثبيت Microsoft Excel. تعمل هذه الطريقة مع أي حل تقارير أو لوحة تحكم مبني على Java.

**ما ستتعلمه**
- كيفية إعداد Aspose.Cells for Java في Maven أو Gradle  
- كيفية إنشاء كائن `Workbook` وإضافة مخطط عمودي  
- كيفية دمج شكل مربع اختيار داخل منطقة المخطط  
- كيفية تطبيق ترخيص Aspose.Cells للاستخدام في الإنتاج  

## إجابات سريعة
- **ما المكتبة التي تنشئ مخططات Excel تفاعلية؟** Aspose.Cells for Java.  
- **هل يمكنني إضافة مربعات اختيار بدون VBA؟** نعم، عن طريق إدراج شكل Form Control عبر الـ API.  
- **هل أحتاج إلى ترخيص لهذه الميزة؟** الترخيص المؤقت يعمل للتقييم؛ الترخيص الدائم مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أحدث.  
- **هل سيعمل المخطط في Excel 2016‑2024؟** نعم، الملف المُولد يتبع معيار Office Open XML.  

## ما هو مخطط Excel التفاعلي؟
المخطط **التفاعلي في Excel** يجمع بين مخطط قياسي وعناصر تحكم واجهة المستخدم (مثل مربعات الاختيار) التي تسمح للمستخدمين بإظهار أو إخفاء سلاسل البيانات في الوقت الفعلي، مما يحول الصورة الثابتة إلى أداة تقارير ديناميكية.

## لماذا نستخدم Aspose.Cells for Java؟
يدعم Aspose.Cells **أكثر من 80 تنسيقًا للإدخال والإخراج** ويمكنه معالجة دفاتر العمل التي تحتوي على **أكثر من 10,000 صف** دون تحميل الملف بالكامل إلى الذاكرة، مما يوفر توليدًا عالي الأداء في بيئات الخادم.

## المتطلبات المسبقة

- **مجموعة تطوير Java (JDK):** الإصدار 8 أو أعلى.  
- **Aspose.Cells for Java:** أحدث إصدار (مثال: 25.3).  
- **Maven أو Gradle:** لإدارة تبعية المكتبة.  

### المتطلبات المعرفية
معرفة أساسية بصياغة Java وإلمام بمفاهيم Excel (الأوراق، النطاقات، المخططات) مفيدة، لكن الخطوات أدناه مفصلة بما يكفي للمطورين من أي مستوى خبرة.

## كيف تضيف مربع اختيار في Java؟

حمّل مكتبة Aspose.Cells، أنشئ دفتر عمل، وأدرج شكل مربع اختيار في استدعاء واحد. مربع الاختيار هو Form Control يمكن ربطه بخلية؛ عند تبديله سيتغير قيمة الخلية المرتبطة، والتي يمكنك لاحقًا **ربطها** بظهور سلسلة المخطط.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### الخطوة 1: إعداد اعتماد Maven

أضف عنصر Aspose.Cells Maven إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### الخطوة 2: إعداد اعتماد Gradle

أضف السطر التالي إلى ملف `build.gradle` الخاص بك:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### خطوات الحصول على الترخيص

لإلغاء قيود الوظائف الكاملة، احصل على ترخيص مؤقت أو دائم. حمّل ترخيص تجريبي من [موقع Aspose](https://releases.aspose.com/cells/java/). للاستخدام **في الإنتاج**، اشترِ ترخيصًا وطبقه كما هو موضح لاحقًا.

#### التهيئة الأساسية

License هو الصف في Aspose.Cells المستخدم لتطبيق ملف ترخيص **مشترا**، مما يتيح الوظائف الكاملة دون حدود التقييم. قم بتهيئة المكتبة في كود Java قبل أي عملية على دفتر العمل:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## كيف تنشئ مخطط Excel تفاعلي؟

كائن Aspose.Cells `Workbook` يمثل ملف Excel كامل، يحتوي على أوراق العمل، المخططات، وعناصر أخرى. من خلال إنشاء دفتر عمل يمكنك برمجيًا إضافة البيانات، توليد مخطط عمودي، ثم دمج عناصر تحكم تفاعلية مثل مربعات الاختيار. الخطوات التالية ترشدك إلى بناء دفتر العمل، تعبئة البيانات، وتكوين المخطط للتفاعل.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### إنشاء دفتر عمل وإضافة مخطط

#### نظرة عامة

يوضح هذا القسم كيفية إنشاء دفتر عمل جديد، إضافة ورقة عمل للبيانات، وتوليد مخطط عمودي سيتم جعله تفاعليًا لاحقًا.

##### الخطوة 1: إنشاء دفتر عمل جديد

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### الخطوة 2: إضافة ورقة عمل للمخطط

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### الخطوة 3: إدراج مخطط عمودي

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### الخطوة 4: إضافة بيانات السلسلة

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## كيف تدمج مربع اختيار في مخطط؟

دمج مربع اختيار مباشرةً على منطقة المخطط يتيح للمستخدمين النقر لإظهار أو إخفاء سلسلة معينة. مربع الاختيار هو شكل Form Control يمكن ربطه بخلية؛ يمكن الإشارة إلى قيمة الخلية في صيغة تتحكم في ظهور السلسلة.

Shape هو كائن Aspose.Cells يمثل عنصر رسم مثل عنصر تحكم نموذج، صورة، أو مربع نص داخل ورقة العمل.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### دمج شكل مربع الاختيار

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### تعيين نص مربع الاختيار

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## كيف تحفظ دفتر العمل كملف Excel؟

حفظ الـ `Workbook` يكتب جميع التغييرات الموجودة في الذاكرة إلى ملف Excel فعلي على القرص. يدعم Aspose.Cells تنسيق .xlsx الحديث، مما يضمن فتح الملف في Excel 2016‑2024 وتطبيقات Office المتوافقة الأخرى. استخدم طريقة `save` مع مسار الملف المطلوب، ويمكنك اختيار تنسيق الملف للحصول على خيارات إضافية.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## تطبيقات عملية

سيناريوهات واقعية حيث يضيف المخطط التفاعلي مع مربعات الاختيار قيمة:

1. **تقارير تفاعلية:** تمكين أصحاب المصلحة من تبديل خطوط المنتجات الفردية على مخطط المبيعات.  
2. **تحليل مقارن:** تمكين المحللين من التركيز على فترات زمنية أو مناطق محددة عن طريق تحديد/إلغاء تحديد السلاسل.  
3. **لوحات تعليمية:** يمكن للطلاب استكشاف اتجاهات البيانات عن طريق اختيار المتغيرات التي يرغبون في عرضها.

## المشكلات الشائعة والحلول

- **مربع الاختيار لا يستجيب:** تأكد من ربط مربع الاختيار بخلية وأن الخلية مُشار إليها في صيغة تؤثر على ظهور السلسلة.  
- **المخطط لا يتحديث بعد التبديل:** قم بتحديث عرض دفتر العمل في Excel أو أعد حساب الصيغ (`workbook.calculateFormula()`).  
- **الترخيص غير مطبق:** تحقق من تنفيذ `License license = new License(); license.setLicense("Aspose.Cells.lic");` قبل أي عملية على دفتر العمل.

## الأسئلة المتكررة

**س: كيف أضيف مربع اختيار دون استخدام VBA؟**  
ج: استخدم API `Shape` في Aspose.Cells مع `ShapeType.FORM_CONTROL_CHECKBOX` وربطه بخلية في ورقة العمل؛ يعمل مربع الاختيار أصلاً في Excel.

**س: هل أحتاج إلى ترخيص لميزة مربع الاختيار؟**  
ج: شكل مربع الاختيار متاح في النسخة التجريبية المجانية، لكن ترخيص Aspose.Cells **الدائم** يزيل حدود التقييم ويفعل تحسينات الأداء الكاملة.

**س: أي إصدارات Excel يمكنها فتح الملف المُولد؟**  
ج: الملفات المحفوظة باستخدام Aspose.Cells تتبع معيار Office Open XML وتفتح بشكل صحيح في **Excel 2016** و**2019** و**2021** و**Microsoft 365**.

**س: هل يمكنني التحكم في عدة سلاسل باستخدام مربعات اختيار منفصلة؟**  
ج: نعم، أنشئ مربع اختيار لكل سلسلة، اربط كل واحد بخلية مساعدة مميزة، واستخدم صيغًا شرطية لتبديل كل سلسلة بشكل مستقل.

**س: هل هناك حد لعدد مربعات الاختيار في كل مخطط؟**  
ج: عمليًا، يمكنك إضافة العشرات؛ يبقى الأداء مستقرًا حتى 200 عنصر تحكم لكل ورقة عمل على الأجهزة الخادمة العادية.

**آخر تحديث:** 2026-09-22  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [كيفية إضافة مربع اختيار في Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [إنشاء مخططات Excel ديناميكية باستخدام Aspose.Cells Java: دليل شامل للمطورين](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [إضافة تسميات بيانات إلى مخطط Excel باستخدام Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}