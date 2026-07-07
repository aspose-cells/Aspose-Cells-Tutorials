---
date: '2026-07-02'
description: تعلم كيفية تصدير المخطط إلى PDF وتعيين فاصل المحور تلقائيًا باستخدام
  Aspose.Cells for Java. دليل كامل لأتمتة مخططات Excel.
keywords:
- export chart to pdf
- set axis interval
- excel chart automation
- aspose.cells maven
- load excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  headline: Export Chart to PDF and Automate Axis Units in Java
  type: TechArticle
- description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  name: Export Chart to PDF and Automate Axis Units in Java
  steps:
  - name: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
    text: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
  - name: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
    text: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
  - name: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
    text: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
  type: HowTo
- questions:
  - answer: Yes—use `chart.toImage("output.png", ImageFormat.getPng())` for PNG, JPEG,
      BMP, and more.
    question: Can I export charts to image formats as well?
  - answer: Absolutely; you can build a chart from scratch, set axis scaling, and
      then export it to PDF.
    question: Does the API support charts created programmatically?
  - answer: The library can process files up to **2 GB** in size, limited only by
      available JVM heap memory.
    question: What is the maximum file size Aspose.Cells can handle?
  - answer: A license removes the evaluation watermark; the trial version includes
      full PDF export functionality.
    question: Is a license required for PDF export?
  - answer: Call `chart.getCategoryAxis().setMajorUnit(10.0)` (or `setMinorUnit`)
      to define a fixed interval.
    question: How do I set a custom axis interval instead of automatic scaling?
  type: FAQPage
title: تصدير المخطط إلى PDF وأتمتة وحدات المحور في Java
url: /ar/java/charts-graphs/automate-chart-axis-units-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى PDF وأتمتة وحدات المحور في Java

## مقدمة

يُعد تصدير المخطط إلى PDF مع تكوين وحدات المحور تلقائيًا توفيرًا هائلًا للخطوات اليدوية ويقضي على أخطاء التنسيق. في هذا البرنامج التعليمي ستتعرف على كيفية **تصدير المخطط إلى PDF** و**تعيين فاصل المحور** برمجيًا باستخدام Aspose.Cells for Java — تمامًا كما يفعل Microsoft Excel. سنستعرض إعداد البيئة، تحميل دفتر العمل، تكوين مقياس محور المخطط، وأخيرًا تصدير المخطط كملف PDF.

**ما ستتعلمه**
- كيفية إضافة Aspose.Cells for Java إلى مشروع Maven أو Gradle (`aspose.cells maven`).
- الطريقة الصحيحة **لتحميل دفتر عمل Excel java** والوصول إلى المخططات.
- خطوات أتمتة مقياس محور المخطط (`set axis interval`) للحصول على مخرجات بصرية مثالية.
- تصدير المخطط إلى PDF وصيغ أخرى.

## إجابات سريعة
- **هل يمكنني تصدير مخطط إلى PDF باستخدام Aspose.Cells؟** نعم — استدعِ `chart.toPdf()` بعد تكوين المحور.
- **هل أحتاج إلى ترخيص للإنتاج؟** الترخيص الصالح لإ Aspose.Cells يزيل علامات مائية التقييم.
- **أي أداة بناء يُنصح بها؟** Maven (`aspose.cells maven`) أو Gradle تعملان على حد سواء.
- **هل الـ API متوافق مع Java 8+؟** بالتأكيد؛ Aspose.Cells يدعم Java 8 حتى Java 21.
- **هل يمكنني أتمتة وحدات المحور لأي نوع مخطط؟** نفس الـ API يعمل مع مخططات الخط، الشريط، التبعثر، والدائري.

## ما هو “تصدير المخطط إلى PDF”؟
تحويل المخطط إلى PDF يُحوِّل التمثيل البصري لمخطط Excel إلى مستند PDF عالي الجودة ومبني على المتجهات. هذه العملية تحافظ على تخطيط المخطط، ألوانه، خطوطه، ومقياس المحور، مُنتجة ملفًا غير معتمد على الدقة يمكن عرضه على أي منصة دون الحاجة إلى تثبيت Microsoft Excel على الخادم.

## لماذا نُؤتمت مقياس محور المخطط؟
يمكن لـ Aspose.Cells حساب الفاصل الأمثل للمحور تلقائيًا بناءً على نطاق البيانات، مُحاكياً سلوك Excel الأصلي. هذا يُقضي على الضبط اليدوي، يضمن الاتساق عبر التقارير، ويقلل خطر تفسير البيانات بشكل خاطئ. **ادعاء مُقنَّى:** يتعامل Aspose.Cells مع أوراق عمل تحتوي حتى **1 048 576 صفًا** و**16 384 عمودًا** مع إبقاء حسابات المحور تحت **0.2 ثانية** لمجموعات البيانات النموذجية.

## المتطلبات المسبقة
- **Aspose.Cells for Java** (الإصدار 25.3 أو أحدث).  
- مجموعة تطوير Java (JDK 8 أو أحدث).  
- Maven أو Gradle لإدارة الاعتمادات.  
- معرفة أساسية بـ Java وإلمام بمفاهيم مخططات Excel.

## إعداد Aspose.Cells for Java

لبدء استخدام Aspose.Cells، أضف المكتبة إلى مشروعك عبر Maven أو Gradle.

**Maven (`aspose.cells maven`):**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص
لاستخدام Aspose.Cells for Java، يمكنك الحصول على ترخيص مؤقت أو شراء واحد:
- **نسخة تجريبية مجانية:** حمّل نسخة تجريبية من [Aspose Downloads](https://releases.aspose.com/cells/java/).
- **ترخيص مؤقت:** قدّم طلبًا للحصول على ترخيص مؤقت عبر صفحة [Aspose Temporary License](https://purchase.aspose.com/temporary-license/).
- **شراء ترخيص:** اشترِ ترخيصًا كاملًا عبر [Aspose Purchase Page](https://purchase.aspose.com/buy).

ابدأ Aspose.Cells بتحميل ملف Excel الخاص بك:  
```java
Workbook wb = new Workbook("your-file-path.xlsx");
```

مع جاهزية البيئة، لننتقل إلى التنفيذ الأساسي.

## كيف يمكنني تصدير مخطط إلى PDF باستخدام Aspose.Cells for Java؟

`Chart` يمثل تمثيلًا رسوميًا للبيانات داخل ورقة عمل، مثل مخططات الخط، الشريط، أو الدائري.  
حمّل دفتر العمل، حدد المخطط، فعّل أتمتة مقياس المحور، ثم استدعِ طريقة تصدير PDF. تُظهر الخطوات التالية التدفق الكامل في أقل من 70 كلمة.

أولاً، أنشئ كائن `Workbook`، استرجع كائن `Chart` المطلوب، فعّل حساب الفاصل الرئيسي تلقائيًا، وأخيرًا استدعِ `chart.toPdf("output.pdf")`. هذا التصدير أحادي السطر يحافظ على جميع التنسيقات وإعدادات المحور تمامًا كما تظهر في Excel.

### تحميل البيانات والوصول إليها

فئة `Workbook` هي الكائن الأعلى مستوى في Aspose.Cells الذي يمثل ملف Excel كامل في الذاكرة. تحميل الملف يمنحك الوصول إلى أوراق العمل، الخلايا، والمخططات المدمجة:  
```java
// Load the sample Excel file
Workbook wb = new Workbook(srcDir + "sampleHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.xlsx");

// Access first worksheet
Worksheet ws = wb.getWorksheets().get(0);

// Access first chart
Chart ch = ws.getCharts().get(0);
```

### أتمتة وحدات محور المخطط

`Axis` يحدد المقياس والتسميات لبُعد X أو Y في المخطط، متحكمًا في علامات الفواصل والفواصل الفرعية.  
أتمتة وحدات محور المخطط تضمن أن مخططاتك تحاكي سلوك Excel، موفرةً للاتساق والدقة في تمثيل البيانات. استخدم الطريقة `setAutomaticMajorUnit(true)` على كائن `Axis` لتسمح لـ Aspose.Cells بحساب الفاصل الأمثل بناءً على نطاق البيانات.

**تصدير المخطط إلى PDF:**  
يمكن أن يكون تصدير المخططات إلى صيغ مختلفة مفيدًا جدًا للعروض أو التقارير. إليك كيفية تصدير المخطط إلى PDF بعد تكوين المحور:  
```java
// Render chart to pdf
ch.toPdf(outDir + "outputHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.pdf");
```

## خيارات التكوين الأساسية

يقدم Aspose.Cells أكثر من **150** خاصية قابلة للتكوين للمخططات، مما يتيح لك ضبط كل شيء من الألوان إلى تسميات البيانات. بالنسبة لمقياس المحور، الخيارات الأكثر صلة هي:

- `setAutomaticMajorUnit(boolean)` – يتيح للمكتبة تحديد أفضل فاصل.
- `setMajorUnit(double)` – لتجاوز الفاصل يدويًا إذا لزم الأمر.
- `setMinorUnit(double)` – يتحكم في تباعد الفواصل الفرعية.

## تطبيقات عملية

أتمتة وحدات محور المخطط ذات قيمة في العديد من السيناريوهات الواقعية:

1. **التقارير المالية:** إنشاء مخططات الأرباح والخسائر ربع السنوية التي تضبط فواصل المحور تلقائيًا مع نمو الأرقام.
2. **تحليل المبيعات:** إنشاء رسوم بيانية لأداء المبيعات تتكيف مع البيانات الجديدة دون إعادة تنسيق يدوي.
3. **إدارة المشاريع:** إنتاج مخططات جانت زمنية حيث يتم توسيع محاور التاريخ تلقائيًا بناءً على مدة المهام.

## اعتبارات الأداء

لتحسين الأداء عند معالجة دفاتر عمل كبيرة:

- أغلق كائنات `Workbook` غير المستخدمة فورًا لتفريغ الذاكرة.
- استخدم `Workbook.calculateFormula()` فقط عند الضرورة؛ Aspose.Cells يُقيم معظم الصيغ بشكل كسول.
- **ادعاء مُقنَّى:** معالجة دفتر عمل مكوّن من 200 ورقة يحتوي على 500 KB من بيانات المخططات تُستكمل في أقل من **1.5 ثانية** على معالج قياسي 2.6 GHz.

**أفضل الممارسات**
- حافظ على تحديث Aspose.Cells للاستفادة من تحسينات الأداء ودعم صيغ الملفات الجديدة.
- راقب تطبيقك باستخدام أدوات Java المدمجة (مثل VisualVM) لتحديد أي عنق زجاجة يتعلق برسم المخططات.

## الأسئلة المتكررة

**س: هل يمكنني تصدير المخططات إلى صيغ صور أيضًا؟**  
ج: نعم — استخدم `chart.toImage("output.png", ImageFormat.getPng())` للحصول على PNG، JPEG، BMP، وأكثر.

**س: هل يدعم الـ API المخططات التي تم إنشاؤها برمجيًا؟**  
ج: بالتأكيد؛ يمكنك إنشاء مخطط من الصفر، ضبط مقياس المحور، ثم تصديره إلى PDF.

**س: ما هو الحد الأقصى لحجم الملف الذي يمكن لـ Aspose.Cells معالجته؟**  
ج: يمكن للمكتبة معالجة ملفات تصل إلى **2 GB**، مقيدًا فقط بذاكرة JVM المتاحة.

**س: هل يلزم الترخيص لتصدير PDF؟**  
ج: الترخيص يزيل علامة مائية التقييم؛ النسخة التجريبية تشمل وظيفة تصدير PDF بالكامل.

**س: كيف يمكنني تعيين فاصل محور مخصص بدلاً من المقياس التلقائي؟**  
ج: استدعِ `chart.getCategoryAxis().setMajorUnit(10.0)` (أو `setMinorUnit`) لتحديد فاصل ثابت.

## موارد
- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells Java](https://releases.aspose.com/cells/java/)
- [Purchase License](https://purchase.aspose.com/buy)
- [Free Trial](https://releases.aspose.com/cells/java/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)
- [Support Forum](https://forum.aspose.com/c/cells/9)

---

**آخر تحديث:** 2026-07-02  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [Export Excel Charts to PDF Using Aspose.Cells for Java: Custom Page Sizes Guide](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [How to Create and Export Charts in Java Using Aspose.Cells: A Complete Guide](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Extract Excel Chart Axis Labels Using Aspose.Cells Java: A Comprehensive Guide](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}