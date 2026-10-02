---
date: '2026-09-27'
description: تعلم كيفية إنشاء مخطط دائري Java باستخدام Aspose.Cells. دليل خطوة بخطوة
  لتخصيص مخطط دائري Excel، إعداد اعتماد Maven، وإنشاء مخططات احترافية.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: إنشاء مخطط دائري Java باستخدام Aspose.Cells للـ Java. تعلم كيفية تخصيص
  مخطط دائري Excel، إضافة اعتماد Maven، وإنشاء مخططات احترافية في دقائق.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: إنشاء مخطط دائري Java باستخدام Aspose.Cells – دليل Java كامل
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: كيفية إنشاء مخطط دائري Java باستخدام Aspose.Cells
url: /ar/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مخطط دائري java باستخدام Aspose.Cells

## مقدمة
إنشاء **pie chart** برمجياً غالبًا ما يشعر وكأنه لغز، خاصةً عندما تحتاج إلى تحكم دقيق في الألوان، والوسائط، والعناوين. في هذا الدليل ستتعلم كيفية **create pie chart java** باستخدام Aspose.Cells، ثم تخصيص مخطط Excel الدائري ليتطابق مع علامتك التجارية أو نمط التقارير الخاص بك. سنستعرض إعداد البيئة، تعبئة البيانات، إنشاء المخطط، وتعديلات بصرية — كل ذلك دون مغادرة بيئة تطوير Java الخاصة بك.

**ما ستتعلمه**
- أضف **Maven dependency Aspose.Cells** إلى مشروعك.
- أنشئ دفتر عمل، واملأ الخلايا بالبيانات، وأنشئ مخططًا دائريًا.
- طبّق ألوانًا مخصصة، وعناوين، ووسائط للمخطط.
- صدّر دفتر العمل إلى ملف XLSX جاهز للمشاركة.

قبل أن تبدأ، يجب أن تكون مرتاحًا مع بنية Java الأساسية وأن يكون لديك Maven أو Gradle مثبتًا.

## إجابات سريعة
- **أي مكتبة تنشئ مخططات دائرية في Java؟** Aspose.Cells for Java.
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتطوير؛ يلزم ترخيص مدفوع للإنتاج.
- **ما هي إحداثيات Maven المطلوبة؟** `com.aspose:aspose-cells:24.10`.
- **هل يمكنني تغيير ألوان القطاعات؟** نعم، عبر طريقة `setAreaColor` لكل سلسلة.
- **هل يمكن تصدير المخطط إلى XLSX؟** بالتأكيد—فقط استدعِ `workbook.save("output.xlsx")`.

## ما هو المخطط الدائري في Excel؟
المخطط الدائري يُظهر سلسلة بيانات واحدة كشرائح نسبية لدائرة، مما يجعل من السهل مقارنة أجزاء الكل. زاوية كل شريحة تتطابق مع قيمتها بالنسبة للإجمالي، مما يتيح نظرة سريعة على توزيع الفئات مثل حصة السوق، توزيع الميزانية، أو النسب السكانية.

## لماذا تستخدم Aspose.Cells لإنشاء مخطط دائري java؟
يدعم Aspose.Cells أكثر من 50 نوعًا من المخططات ويمكنه التعامل مع أوراق عمل تحتوي على ما يصل إلى مليون صف دون تحميل الملف بالكامل إلى الذاكرة. هذا التفوق في الأداء يتيح لك إنشاء تقارير كبيرة على أجهزة ذات موارد محدودة، مع توفير تحكم دقيق في مظهر المخطط، ربط البيانات، وصيغ التصدير، مما يجعله خيارًا متفوقًا على العديد من المكتبات المفتوحة المصدر.

## المتطلبات المسبقة
- **Java Development Kit (JDK)** 8 أو أحدث.
- **IDE** مثل IntelliJ IDEA أو Eclipse.
- **Maven** أو **Gradle** لإدارة الاعتمادات.
- **رخصة Aspose.Cells تجريبية أو مُشتراة**.

### المكتبات والاعتمادات المطلوبة
أضف قطعة Aspose.Cells Maven إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

أو ما يعادله في Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### خطوات الحصول على الترخيص
Aspose.Cells for Java تجاري، لكن يمكنك البدء بنسخة تجريبية مجانية. زر [purchase page](https://purchase.aspose.com/buy) للحصول على مفتاح ترخيص مؤقت.

## إعداد Aspose.Cells لـ Java
أولاً، تأكد من أن المكتبة موجودة في مسار الفئات (classpath). بعد إضافة الاعتماد، يمكنك تهيئة الـ API كما هو موضح أدناه.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## دليل التنفيذ

### إنشاء وتكوين دفتر عمل
تمثل الفئة `Workbook` ملف Excel كامل في الذاكرة.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### الخطوة 1: إنشاء دفتر عمل
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
هذا ينشئ دفتر عمل جديد فارغ يمكنك البدء في ملئه فورًا.

### الوصول إلى خلايا ورقة العمل أو تعديلها
تمثل الفئة `Worksheet` ورقة واحدة داخل دفتر العمل، تحتوي على خلايا، صفوف، وأعمدة.  
ستكتب البيانات التي تُغذي المخطط الدائري في ورقة العمل.

#### الخطوة 2: الحصول على أول ورقة عمل وخلاياها
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
املأ الخلايا بأسماء الفئات والقيم التي سيستخدمها المخطط.

### إنشاء مخطط دائري
كائنات `Chart` تُظهر البيانات في ورقة العمل وتدعم أنواعًا مختلفة مثل الدائري، العمودي، والخطي.

#### الخطوة 3: إضافة مخطط دائري إلى ورقة العمل
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### تكوين سلسلة البيانات للمخطط الدائري
تحدد الفئة `Series` نطاق البيانات وتنسيق المخطط، ربطًا بين خلايا ورقة العمل والعناصر البصرية.

#### الخطوة 4: تعيين السلسلة للمخطط
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### تكوين مظهر وسيلة الإيضاح والعنوان للمخطط
تُظهر وسيلة إيضاح `Legend` للمخطط أسماء السلاسل والألوان، مما يساعد القارئ على التعرف على كل شريحة.

#### الخطوة 5: تخصيص وسيلة إيضاح المخطط والعنوان
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### تخصيص ألوان سلسلة المخطط
`setAreaColor` يحدد لون تعبئة شريحة سلسلة المخطط باستخدام قيمة RGB.

#### الخطوة 6: تغيير ألوان شرائح المخطط الدائري
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### ضبط الأعمدة تلقائيًا وحفظ دفتر العمل
`autoFitColumns` يضبط عرض الأعمدة تلقائيًا ليتناسب مع محتوى الخلايا.

#### الخطوة 7: ضبط عرض الأعمدة وحفظ الملف
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## حالات الاستخدام الشائعة
- **Demographic analysis:** عرض توزيع السكان عبر المناطق.
- **Market‑share reporting:** تصور حصة كل منافس بنظرة واحدة.
- **Budget allocation:** إبراز كيفية توزيع الأموال بين الأقسام.

## اعتبارات الأداء
- حرّر الكائنات (`workbook.dispose()`) عندما لا تكون بحاجة إليها لتحرير الذاكرة الأصلية.
- لمجموعات البيانات الضخمة، استخدم `WorkbookDesigner` لبث البيانات بدلاً من تحميل كل شيء مرة واحدة.
- قم بعمل ملف تعريف باستخدام Java Flight Recorder لتحديد أي عنق زجاجة في توليد المخططات.

## الأسئلة المتكررة

**س: هل يمكنني إنشاء مخططات دائرية متعددة في نفس دفتر العمل؟**  
ج: نعم، كرّر خطوات إنشاء المخطط لكل نطاق بيانات؛ كل مخطط مستقل.

**س: هل يدعم Aspose.Cells مخططات دائرية ثلاثية الأبعاد؟**  
ج: نعم؛ اضبط نوع المخطط إلى `ChartType.PIE_3D` عند إضافة المخطط.

**س: كيف يمكنني تطبيق سمة مخصصة على جميع المخططات؟**  
ج: استخدم طريقة `Workbook.setDefaultTheme` قبل إنشاء أي مخططات.

**س: ما هي صيغ الملفات التي يمكنني تصدير دفتر العمل إليها؟**  
ج: أكثر من 30 صيغة، بما في ذلك XLSX، CSV، PDF، وHTML.

**س: هل يلزم وجود ترخيص للنشر التجاري؟**  
ج: نعم، الترخيص الصالح يزيل علامات التقييم ويُفعل جميع الوظائف.

## الخاتمة
الآن لديك وصفة كاملة من البداية إلى النهاية لإنشاء **create pie chart java** باستخدام Aspose.Cells. باتباع الخطوات أعلاه يمكنك توليد مخططات Excel دائرية مصقولة، تخصيص الألوان والعناوين، ودمجها في أي خط أنابيب تقارير. استكشف أنواع مخططات أخرى—عمودية، خطية، رادارية—لتوسيع مجموعة أدواتك في تصور البيانات.

---

**آخر تحديث:** 2026-09-27  
**تم الاختبار مع:** Aspose.Cells 24.10 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [تخصيص تسميات بيانات مخطط Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [إنشاء مخططات Excel ديناميكية باستخدام Aspose.Cells Java: دليل شامل للمطورين](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [إنشاء وتخصيص دفاتر عمل Excel باستخدام Aspose.Cells Java: دليل خطوة بخطوة](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}