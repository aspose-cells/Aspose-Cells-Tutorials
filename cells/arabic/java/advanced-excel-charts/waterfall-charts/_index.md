---
date: 2026-09-02
description: تعلم كيفية إنشاء مخطط waterfall chart في Java باستخدام Aspose.Cells،
  تعيين نطاق بيانات المخطط، تخصيص التسميات وتصديره إلى XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: مخططات Waterfall
og_description: إنشاء مخطط waterfall chart باستخدام Aspose.Cells for Java – تعيين
  نطاق بيانات المخطط، إضافة تسميات البيانات، وتصديره إلى XLSX في بضع خطوات.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: إنشاء مخطط waterfall chart في Excel باستخدام Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: إنشاء مخطط waterfall chart في Excel باستخدام Aspose.Cells for Java
url: /ar/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مخططات الشلال

## مقدمة في مخططات الشلال باستخدام Aspose.Cells for Java

في هذا الدرس ستتعلم كيفية **إنشاء مخطط شلال في Excel** و **تعيين نطاق بيانات المخطط** باستخدام Aspose.Cells for Java. تحول مخططات الشلال سلسلة من الأرقام الإيجابية والسلبية إلى قصة بصرية واضحة، مما يجعلها مثالية للبيانات المالية، مراجعات أداء المبيعات، وأي سيناريو تحتاج فيه إلى رؤية كيفية مساهمة العناصر الفردية في المجموع الكلي.

## إجابات سريعة
- **ما هو مخطط الشلال؟** تصور يوضح كيف يتم زيادة القيمة الأولية وتقليلها بواسطة سلسلة من القيم المتوسطة، وينتهي بإجمالي نهائي.  
- **ما المكتبة المستخدمة؟** Aspose.Cells for Java.  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني حفظ الملف بصيغة XLSX؟** نعم – استخدم `workbook.save("FileName.xlsx")`.  
- **هل هو مناسب لتصوير البيانات في Java؟** بالتأكيد؛ توفر Aspose.Cells ميزات مخططات غنية دون الحاجة إلى تثبيت Office.

## ما هو مخطط الشلال؟
يعرض مخطط الشلال المساهمات الإيجابية والسلبية المتسلسلة لقيمة ابتدائية، مما يساعدك على فهم كيفية تأثير كل مكون على النتيجة النهائية. من خلال تصور المكاسب والخسائر جنبًا إلى جنب، يجعل التدفقات المالية المعقدة قابلة للقراءة فورًا.

## لماذا تستخدم Aspose.Cells for Java لإضافة مخطط شلال؟
تتيح لك Aspose.Cells إنشاء مخططات Excel على أي خادم، خط أنابيب CI، أو سطح مكتب دون الحاجة إلى Microsoft Excel. تدعم **أكثر من 15 تنسيق إخراج** (XLSX، PDF، HTML، CSV، وغيرها)، وتعالج المصنفات التي تحتوي على **أكثر من 500 صف** في أقل من ثانية، وتوفر تحكمًا برمجيًا في كل عنصر من عناصر المخطط—من الألوان إلى تسميات البيانات.

## المتطلبات المسبقة

قبل الغوص في الكود، تأكد من توفر المتطلبات التالية:

- Aspose.Cells for Java: ستحتاج إلى تثبيت Aspose.Cells for Java. يمكنك تنزيله من صفحة إصدارات Aspose.Cells for Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- بيئة تطوير Java: تأكد من تثبيت Java على نظامك وتوافر أداة بناء (Maven/Gradle) جاهزة.

الآن، لنبدأ بإنشاء مخطط الشلال خطوة بخطوة.

## كيفية تعيين نطاق بيانات المخطط لمخطط شلال في Java
قم بتحميل مصنف جديد، املأه بالبيانات، أضف كائن `Chart`، حدد نطاق السلسلة، وأخيرًا احفظ الملف. هذه العملية بسيطة: تنشئ مصنفًا، تملأ الخلايا بالفئات والقيم، تنشئ مخططًا، تربط نطاقات البيانات، ثم تصدر المصنف. النتيجة هي مخطط شلال كامل الوظائف جاهز للاستخدام في التقارير أو لوحات المعلومات.

### الخطوة 1: استيراد Aspose.Cells
حزمة `com.aspose.cells` تحتوي على جميع الفئات المطلوبة للتعامل مع Excel، بما في ذلك إنشاء المصنفات، معالجة أوراق العمل، وتوليد المخططات.

### الخطوة 2: تهيئة المصنف وورقة العمل
تمثل **Workbook** ملف Excel، و**Worksheet** هي ورقة واحدة داخل ذلك الملف. إنشاء هذه الكائنات يوفر القاعدة لكل من البيانات الخام والمخطط.

### الخطوة 3: إدخال البيانات
العمود A يحتوي على تسميات الفئات، بينما العمود B يحتوي على القيم الرقمية لمخطط الشلال. يتطابق هذا التخطيط مع تدفق الأرباح والخسائر النموذجي المستخدم في التحليل المالي.

### الخطوة 4: إنشاء مخطط الشلال
كائن **Chart** ينشئ تمثيلًا بصريًا؛ ضبط نوعه إلى `ChartType.WATERFALL` يكوّنه كمخطط شلال. استخدم طريقة `add` لتعيين نطاق بيانات المخطط للسلسلة (`"B2:B6"`)، وربط محور الفئات بـ `"A2:A6"`.

### الخطوة 5: حفظ المصنف
حفظ المصنف يكتب المخطط والبيانات إلى تنسيق الملف المحدد. استدعِ `workbook.save("WaterfallChart.xlsx")` لإنشاء ملف XLSX، أو غيّر معلمة التنسيق لتصدير إلى PDF أو CSV أو HTML.

## المشكلات الشائعة والحلول

- **المخطط يظهر فارغًا** – تحقق من أن مراجع نطاق البيانات (`B2:B6` و `A2:A6`) تتطابق مع الخلايا الفعلية التي تحتوي على القيم والفئات.  
- **القيم السلبية لا تُعرض بشكل صحيح** – تأكد من ضبط نوع السلسلة إلى `ChartType.WATERFALL`؛ الأنواع الأخرى تتعامل مع السالب بطريقة مختلفة.  
- **الملف لا يفتح في Excel** – استخدم أحدث إصدار من Aspose.Cells وتأكد من أن امتداد الملف يتطابق مع التنسيق (`.xlsx` لـ Excel).

## الأسئلة المتكررة

### كيف يمكنني تخصيص مظهر مخطط الشلال الخاص بي؟
يمكنك تعديل خصائص مثل `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` لتغيير ألوان الأعمدة، تمكين تسميات البيانات باستخدام `setShowDataLabels(true)`، وتعديل عناوين المحاور عبر `getCategoryAxis().setTitle("Stage")`. يوفر مرجع API الخاص بـ Aspose.Cells قائمة كاملة بالخيارات القابلة للتخصيص.

### هل يمكنني إنشاء مخططات شلال متعددة في نفس ورقة العمل؟
نعم. بعد إضافة المخطط الأول، كرّر خطوات إنشاء المخطط بنطاق بيانات مختلف وكائن `Chart` جديد. كل مخطط مستقل ويمكن وضعه في أي مكان على الورقة.

### هل Aspose.Cells متوافق مع بيئات تطوير Java المختلفة؟
بالطبع. تعمل المكتبة مع Eclipse، IntelliJ IDEA، NetBeans، وأي نظام بناء يدعم Maven أو Gradle. لا تحتاج إلى إضافات إضافية.

### هل يمكنني إضافة سلاسل بيانات إضافية إلى مخطط الشلال؟
يمكنك إضافة سلاسل أخرى عبر استدعاء `chart.getNSeries().add("C2:C6", true)` وتكوين كل سلسلة على حدة. يتيح لك ذلك مقارنة سيناريوهات متعددة جنبًا إلى جنب.

### أين يمكنني العثور على المزيد من الموارد والأمثلة لـ Aspose.Cells for Java؟
استكشف الوثائق الكاملة في مرجع API الخاص بـ Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## الأسئلة المتكررة

**س: كيف يمكنني تعيين نطاق بيانات المخطط لمخطط شلال مالي؟**  
ج: استخدم طريقة `add` على سلسلة المخطط، مع تمرير نطاق الخلايا الذي يحتوي على القيم، مثل `"B2:B6"`.

**س: هل يمكنني تصدير المصنف إلى PDF بدلاً من XLSX؟**  
ج: نعم، استدعِ `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` لإنشاء نسخة PDF.

**س: ماذا لو احتجت إلى إنشاء مخطط شلال مع فئات أكثر؟**  
ج: قم بتمديد نطاق البيانات في كل من عمود القيم وعمود الفئات، ثم حدّث استدعاءات `add` و `setCategoryData` وفقًا لذلك.

**س: هل هناك طريقة لتنسيق الأعمدة الإيجابية والسلبية تلقائيًا؟**  
ج: قم بالتكرار عبر مجموعة `Series` وضبط لون `FillFormat` بناءً على إشارة كل قيمة؛ تتيح لك Aspose.Cells تطبيق التنسيق الشرطي برمجيًا.

**س: هل تدعم Aspose.Cells تحديث البيانات الديناميكي للمخططات؟**  
ج: نعم. بعد تعديل قيم الخلايا، ما عليك سوى إعادة حفظ المصنف—سيعكس المخطط البيانات الجديدة تلقائيًا.

---

**آخر تحديث:** 2026-09-02  
**تم الاختبار مع:** Aspose.Cells for Java (latest)  
**المؤلف:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## دروس ذات صلة

- [تخصيص تسميات بيانات مخطط Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [إضافة تسميات بيانات إلى مخطط Excel باستخدام Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [كيفية إنشاء وتصدير المخططات في Java باستخدام Aspose.Cells: دليل شامل](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}