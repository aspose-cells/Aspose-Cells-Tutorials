---
date: 2026-09-02
description: تعلم كيفية تصدير chart إلى PNG، إضافة سلسلة بيانات، دمج line and column
  chart، حفظ المصنف كـ XLSX وإضافة legend chart باستخدام Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: تصدير chart إلى PNG وإضافة سلسلة بيانات للchart المدمج
og_description: تصدير chart إلى PNG باستخدام Aspose.Cells for Java، دمج line and column
  chart، إضافة سلسلة بيانات، وحفظ المصنف كـ XLSX في دليل واحد.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: تصدير chart إلى PNG وإضافة سلسلة بيانات للchart المدمج
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: تصدير chart إلى PNG وإضافة سلسلة بيانات للchart المدمج
url: /ar/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى PNG وإضافة سلسلة بيانات للمخطط المدمج

في هذا البرنامج التعليمي ستقوم **بإضافة سلسلة بيانات** إلى دفتر عمل Excel، **بدمج عناصر مخطط الخط والعمود**، وتتعلم كيفية **تصدير المخطط إلى PNG** باستخدام Aspose.Cells for Java. سنستعرض كل خطوة — من إعداد دفتر العمل، إضافة المخطط إلى ورقة عمل، تخصيص الأسطورة، إلى **حفظ دفتر العمل كـ XLSX** وإنشاء صورة PNG للمخطط. في النهاية، ستحصل على مخطط مدمج جاهز للاستخدام يمكنك تضمينه في التقارير أو لوحات المعلومات.

## إجابات سريعة
- **أي مكتبة تنشئ مخططات مدمجة؟** Aspose.Cells for Java.  
- **كيف يمكنني إضافة سلسلة بيانات؟** استدعِ `chart.getNSeries().add(...)` مع النطاق المناسب.  
- **كيف يمكنني تصدير المخطط إلى PNG؟** استخدم `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **ما هو تنسيق الملف الذي يمكنني حفظ دفتر العمل به؟** تنسيق `.xlsx` القياسي (حفظ دفتر العمل كـ XLSX).  
- **هل أحتاج إلى ترخيص للإنتاج؟** نعم – يلزم وجود ترخيص Aspose.Cells صالح لاستخدامه في بيئات الإنتاج.

## ما هو تصدير المخطط إلى PNG في Aspose.Cells؟
إن تصدير مخطط إلى PNG يُنشئ صورة نقطية للمخطط في Excel يمكن عرضها في صفحات الويب أو التقارير أو رسائل البريد الإلكتروني دون الحاجة إلى تطبيق Excel. تلتقط هذه الطريقة التخطيط البصري الدقيق، الألوان، وعلامات البيانات، مما ينتج ملف صورة قابل للنقل.

## لماذا إنشاء مخطط خط وعمود مدمج؟
يسمح لك مخطط الخط‑العمود المدمج بعرض مجموعات بيانات مختلفة بتمثيلات بصرية متميزة (مثل سلسلة خط فوق سلسلة عمود) في عرض واحد. هذا النهج مثالي لمقارنة الاتجاهات مع الإجماليات، إبراز الارتباطات، أو تقديم رؤى أغنى مع الحفاظ على بصمة بصرية صغيرة.

## المتطلبات المسبقة
- Java Development Kit (JDK) 8 أو أعلى  
- مكتبة Aspose.Cells for Java (قم بالتنزيل من الرابط أدناه)  
- إلمام أساسي بصياغة Java ومفاهيم Excel  

## البدء

أولاً، قم بتنزيل مكتبة Aspose.Cells for Java من الموقع الرسمي:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

بمجرد إضافة ملف JAR إلى مسار الفئة (classpath) لمشروعك، يمكنك البدء في بناء المخطط.

### الخطوة 1: استيراد فئات aspose.cells
`Workbook` هو الكائن الأساسي في Aspose.Cells الذي يمثل ملف Excel كامل في الذاكرة.  
```java
import com.aspose.cells.*;
```

### الخطوة 2: إنشاء دفتر عمل جديد
`Worksheet` يمثل ورقة واحدة داخل `Workbook` ويوفر الوصول إلى الخلايا والصفوف والمخططات.  
```java
Workbook workbook = new Workbook();
```

### الخطوة 3: الوصول إلى ورقة العمل الأولى
`Chart` هو الكائن الذي يحتوي على جميع إعدادات المخطط، السلاسل، وخيارات العرض.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### الخطوة 4: إضافة كائن مخطط مدمج إلى ورقة العمل  
سنبدأ بمخطط خط ثم نضيف لاحقًا سلسلة عمود لتحقيق تأثير **مخطط خط عمود مدمج**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## إضافة بيانات إلى المخطط

الآن بعد أن حاوية المخطط موجودة، نحتاج إلى تزويدها بالبيانات.

### الخطوة 5: تعريف نطاقات البيانات وإضافة سلسلة بيانات
`NSeries` هي المجموعة التي تخزن كل سلسلة بيانات للمخطط. إضافة سلسلة تربط نطاقًا من الخلايا بالمخطط.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **نصيحة احترافية:** المعامل الأول (`"A1:A5"`) هو النطاق للسلسلة الأولى، والثاني (`"B1:B5"`) ينشئ سلسلة ثانية سيتم دمجها مع الأولى.

### الخطوة 6: تعيين بيانات الفئة (محور X)
`CategoryAxis` يمثل المحور الأفقي للمخطط، ويتحكم في التسميات المعروضة على طول محور X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## تخصيص المخطط

المخطط الجيد يروي قصة. دعنا نضيف له عناوين، تسميات للمحاور، وأساطير واضحة.

### الخطوة 7: تعيين تسميات محاور المخطط والعنوان
`Title` يحدد العنوان الرئيسي للمخطط، وكائنات `Axis` تمثل محوري X و Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### الخطوة 8: إضافة أسطورة للمخطط وضبط موقعها
`Legend` يتحكم في موضع ومظهر أسطورة السلاسل في المخطط.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## حفظ وتصدير المخطط

بعد التخصيص، ستحتاج إلى **حفظ دفتر العمل كـ XLSX** وأيضًا إنشاء صورة.

### الخطوة 9: حفظ دفتر العمل كملف Excel (XLSX)
`Workbook.save` يكتب دفتر العمل الموجود في الذاكرة إلى ملف بالتنسيق المحدد.  
```java
workbook.save("CombinedChart.xlsx");
```

### الخطوة 10: تصدير المخطط إلى PNG
`Chart.toImage` يُظهر المخطط كملف صورة بالتنسيق المختار.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> طريقة `chart.toImage` **تُنشئ صور مخططات Excel** التي يمكن استخدامها في صفحات الويب أو التقارير أو رسائل البريد الإلكتروني.

## المشكلات الشائعة & استكشاف الأخطاء

| المشكلة | الحل |
|-------|----------|
| **لا تظهر البيانات** | تحقق من أن نطاقات الخلايا (`A1:A5`, `B1:B5`, `C1:C5`) تحتوي على بيانات فعلًا قبل إنشاء المخطط. |
| **الأسطورة تتداخل مع المخطط** | قم بتعيين `chart.getLegend().setOverlay(false)` أو انقل الأسطورة إلى موضع مختلف (مثلاً، `RIGHT`). |
| **ملف الصورة فارغ** | تأكد من أن المخطط يحتوي على سلسلة واحدة على الأقل وأن `chart.toImage` يتم استدعاؤه بعد جميع التخصيصات. |
| **حفظ يسبب استثناء** | تحقق من أن لديك أذونات كتابة إلى الدليل المستهدف وأن الملف غير مفتوح في Excel. |

## الأسئلة المتكررة

**س: كيف أقوم بتثبيت Aspose.Cells for Java؟**  
ج: قم بتنزيل ملف JAR من الموقع الرسمي وأضفه إلى مسار الفئة (classpath) لمشروعك. رابط التنزيل هو: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**س: هل يمكنني إنشاء أنواع مخططات أخرى غير الخط والعمود؟**  
ج: نعم، يدعم Aspose.Cells المخططات الشريطية، الدائرية، المبعثرة، المساحية، والعديد من الأنواع الأخرى. راجع وثائق API للقائمة الكاملة.

**س: هل يلزم وجود ترخيص للاستخدام في الإنتاج؟**  
ج: يلزم وجود ترخيص Aspose.Cells صالح لاستخدامه في بيئات الإنتاج. يتوفر إصدار تجريبي مجاني للتقييم.

**س: كيف يمكنني تغيير ألوان كل سلسلة؟**  
ج: استخدم `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (أو ما شابه) بعد إضافة السلسلة.

**س: أين يمكنني العثور على مزيد من أمثلة الشيفرة؟**  
ج: الوثائق الشاملة وعينات إضافية متاحة على موقع مرجع Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**آخر تحديث:** 2026-09-02  
**تم الاختبار مع:** أحدث نسخة من Aspose.Cells for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [كيفية إضافة تسميات إلى مخططات Excel باستخدام Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [كيفية إنشاء مخطط Excel مع خط الاتجاه وتصديره كصورة باستخدام Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells for Java: دليل أحجام الصفحات المخصصة](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}