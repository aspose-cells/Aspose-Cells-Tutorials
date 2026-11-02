---
date: 2026-08-21
description: تعلم كيفية إضافة tooltips و data labels وتغيير chart type في مخططات Excel
  باستخدام Aspose.Cells for Java – دليل خطوة بخطوة مع أمثلة تفاعلية.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: تغيير Excel Chart Type
og_description: تعلم كيفية إضافة tooltips و data labels وتغيير chart type في مخططات
  Excel باستخدام Aspose.Cells for Java – دليل خطوة بخطوة مع أمثلة تفاعلية.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: كيفية إضافة tooltips و data labels إلى مخططات Excel في Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: كيفية إضافة tooltips و data labels إلى مخططات Excel في Java
url: /ar/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة تسميات البيانات إلى مخطط Excel وتغيير نوع المخطط – Aspose.Cells Java

تمنح المخططات التفاعلية تقارير Excel مستوى جديدًا من الفهم، و**كيفية إضافة تلميحات** تجعل المعلومات قابلة للقراءة فورًا. في هذا الدرس ستتعلم كيفية **إضافة تسميات البيانات إلى مخطط Excel**، **تغيير نوع المخطط**، وإنشاء حلول Java تفاعلية باستخدام Aspose.Cells. سنظهر لك أيضًا كيفية إضافة تلميحات ورابط تنقيب بسيط حتى يتمكن جمهورك من استكشاف البيانات بعمق.

## إجابات سريعة
- **ما المكتبة المستخدمة؟** Aspose.Cells for Java  
- **هل يمكنني تغيير نوع المخطط؟** نعم – فقط عدل تعداد `ChartType` عند إنشاء المخطط.  
- **كيف أضيف تلميحات إلى مخطط؟** استخدم واجهة برمجة تطبيقات تسميات البيانات (`setHasDataLabels(true)`) وفعل عرض القيم.  
- **هل يدعم التنقيب (drill‑down)؟** يمكنك إرفاق روابط تشعبية بنقاط البيانات لسلوك تنقيب أساسي.  
- **المتطلبات المسبقة؟** بيئة تطوير Java، ملف JAR الخاص بـ Aspose.Cells، وملف Excel يحتوي على بيانات نموذجية.

## ما هو كيفية إضافة تلميحات؟
**كيفية إضافة تلميحات** تشير إلى عملية تمكين نص يظهر عند التحويم يعرض قيمة نقطة البيانات أو معلومات مخصصة على مخطط Excel. في Aspose.Cells يتم ذلك عبر إعدادات تسميات البيانات للمخطط. تساعد التلميحات المستخدمين على فهم البيانات بسرعة دون إغراق المخطط، ويمكن تخصيصها للخط، اللون، والتنسيق.

## لماذا نستخدم المخططات التفاعلية مع Aspose.Cells؟
يدعم Aspose.Cells **أكثر من 50 تنسيقًا للإدخال والإخراج**—بما في ذلك XLSX، CSV، PDF، وHTML—ويمكنه معالجة دفاتر العمل التي تحتوي على **أكثر من 1 000 ورقة** دون تحميل الملف بالكامل في الذاكرة، مما يوفر توليد مخططات سريع على الخادم لتقارير المؤسسات. تسمح المخططات التفاعلية أيضًا بإدراج روابط تشعبية، تحديثات بيانات ديناميكية، وتصدير إلى تنسيقات صديقة للويب، مما يجعلها مثالية للوحة التحكم وبوابات التقارير.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

- بيئة تطوير Java (يفضل JDK 8 أو أحدث)  
- مكتبة Aspose.Cells for Java (حمّلها من [صفحة تحميل Aspose.Cells for Java](https://releases.aspose.com/cells/java/))  
- دفتر عمل نموذجي (`data.xlsx`) يحتوي على البيانات التي تريد تصورها  

## الخطوة 1: إعداد مشروع Java الخاص بك

1. أنشئ مشروع Java جديد في بيئة التطوير المفضلة لديك (IntelliJ IDEA، Eclipse، إلخ).  
2. أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار بناء المشروع أو إلى تبعيات Maven/Gradle.

## الخطوة 2: تحميل البيانات

للعمل مع المخططات تحتاج أولاً إلى تحميل دفتر عمل في الذاكرة.

فئة `Workbook` تمثل ملف Excel، و`Worksheet` تمثل ورقة واحدة داخل ذلك الملف.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## كيفية تغيير نوع المخطط في Aspose.Cells؟

أنشئ مخططًا جديدًا باستخدام تعداد `ChartType` المطلوب؛ لا يقوم Aspose.Cells بتعديل نوع مخطط موجود في مكانه، لذا يجب إضافة مخطط جديد من النوع الصحيح وإزالة القديم إذا لزم الأمر. يضمن هذا النهج إعادة بناء جميع السلاسل والمحاور بشكل صحيح للتمثيل البصري الجديد.

## الخطوة 3: إنشاء مخطط (وتغيير نوعه)

يمكنك اختيار أي نوع مخطط يناسب تحليلك. أدناه ننشئ **مخطط عمودي**، لكن يمكنك بسهولة التحويل إلى مخطط خطي، دائري، أو شريطي بتغيير تعداد `ChartType`.

كائن `Chart` يوفر طرقًا لتكوين التمثيل البصري للبيانات في ورقة العمل.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **نصيحة احترافية:** لتغيير **نوع مخطط Excel**، استبدل `ChartType.COLUMN` بـ `ChartType.LINE` أو `ChartType.PIE` وغيرها.

## كيفية إضافة تلميحات إلى مخطط Excel؟

حمّل مخططك، فعّل تسميات البيانات، واضبط علم `showValue`. سيعرض التلميح قيمة الخلية الأساسية كلما حرك المستخدم المؤشر فوق نقطة البيانات في ملف Excel أو عرض HTML. يمكنك أيضًا تخصيص خط التلميح، لونه، وخلفيته لتتناسب مع نمط تقريرك.

فئة `DataLabel` تتحكم في مظهر ومحتوى تسميات البيانات، والتي تعمل أيضًا كتلميحات.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## الخطوة 4: إضافة التفاعلية

### 4.1. إضافة تلميحات (add tooltips to chart)

تظهر التلميحات عندما يحوم المستخدم فوق نقطة البيانات. يفعّل الكود التالي تسميات البيانات ويظهر القيمة كتلميح.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. إضافة تسميات البيانات – **add data labels to excel chart**

توفر تسميات البيانات إشارة بصرية دائمة على المخطط نفسه. يمكنك عرضها كـ callouts لتحسين قابلية القراءة.

فئة `DataLabel` تتحكم في مظهر التسميات لكل سلسلة. عبر استدعاء `setHasDataLabels(true)` وتكوين خصائص مثل `setShowValue(true)`، تُدمج القيمة الرقمية مباشرة على المخطط، مما يجعلها مرئية فورًا دون أي تفاعل. تتيح الخيارات الإضافية إظهار أسماء السلاسل، النسب المئوية، أو نص مخصص لسياق أغنى.

> **لماذا نضيف تسميات البيانات؟** تضمين تسميات البيانات مباشرة على المخطط يلغي الحاجة إلى التحويم أو التخمين، مما يحسن وضوح التقرير.

### 4.3. تنفيذ التنقيب (رابط تشعبي على نقطة بيانات)

طريقة بسيطة لإضافة قدرة التنقيب هي إرفاق رابط تشعبي بنقطة معينة. النقر على النقطة يفتح صفحة ويب تحتوي على معلومات مفصلة.

فئة `Hyperlink` تُرفق رابطًا قابلًا للنقر إلى عنصر المخطط، مما يتيح تنقلًا للتنقيب.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## كيفية إضافة تسميات البيانات إلى مخطط Excel؟

فئة `DataLabel` تتحكم في مظهر التسميات لكل سلسلة. عبر استدعاء `setHasDataLabels(true)` وتكوين خصائص مثل `setShowValue(true)`، تُدمج القيمة الرقمية مباشرة على المخطط، مما يجعلها مرئية فورًا دون أي تفاعل. تتيح الخيارات الإضافية إظهار أسماء السلاسل، النسب المئوية، أو نص مخصص لسياق أغنى.

## الخطوة 5: حفظ دفتر العمل

بعد تكوين المخطط، احفظ دفتر العمل بحيث تُحفظ الميزات التفاعلية في ملف الإخراج.

استدعاء `workbook.save` يكتب دفتر العمل المعدل إلى ملف بالتنسيق المختار.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **التلميحات لا تظهر** | تأكد من استدعاء `setHasDataLabels(true)` قبل تكوين `setShowValue(true)`. |
| **الرابط التشعبي غير قابل للنقر** | تحقق من أن تنسيق الإخراج يدعم الروابط التشعبية (مثل XLSX، وليس CSV). |
| **نوع المخطط لا يتغير** | تأكد من تعديل تعداد `ChartType` الصحيح عند إضافة المخطط. |

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع المخطط بعد إنشائه؟**  
ج: تحتاج إلى إنشاء مخطط جديد باستخدام تعداد `ChartType` المطلوب. لا يوفر Aspose.Cells تحويلًا مباشرًا للنوع داخل المخطط، لذا احذف المخطط القديم وأضف جديدًا.

**س: هل يمكنني تخصيص مظهر التلميحات؟**  
ج: نعم. استخدم خصائص `DataLabel` مثل `setFontSize`، `setFontColor`، و`setBackgroundColor` لتنسيق نص التلميح.

**س: كيف أتعامل مع تفاعلات المستخدم في تطبيق ويب؟**  
ج: صدّر دفتر العمل إلى ملف HTML أو XLSX واستخدم JavaScript على جانب العميل لالتقاط أحداث النقر على عناصر المخطط.

**س: أين يمكنني العثور على المزيد من الأمثلة والوثائق؟**  
ج: زر [مرجع Aspose.Cells Java API](https://reference.aspose.com/cells/java/) للحصول على قائمة كاملة بالفئات والطرق المتعلقة بالمخططات.

## الخلاصة

أنت الآن تعرف كيفية **إضافة تسميات البيانات إلى مخطط Excel**، **تغيير نوع مخطط Excel**، **إنشاء حلول مخططات Java تفاعلية**، وإثرائها بالتلميحات، تسميات البيانات، وروابط التنقيب باستخدام Aspose.Cells for Java. تجعل هذه التحسينات تقارير Excel أكثر جذبًا وإفادة للمستخدمين النهائيين.

---

**آخر تحديث:** 2026-08-21  
**تم الاختبار مع:** Aspose.Cells for Java 24.12  
**المؤلف:** Aspose

## دروس ذات صلة

- [How to Modify Excel Charts and Data Labels Using Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extract Excel Chart Axis Labels Using Aspose.Cells Java: A Comprehensive Guide](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Create Bubble Charts in Excel Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}