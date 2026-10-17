---
date: '2026-10-17'
description: تعلم كيفية تعيين شكل تسميات بيانات مخطط Excel في Java باستخدام Aspose.Cells.
  يوضح لك هذا الدليل كيفية تعديل تسميات مخطط Excel بسرعة وكفاءة.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: تعلم كيفية تعيين شكل تسميات بيانات مخطط Excel في Java باستخدام Aspose.Cells.
  يساعدك هذا الدليل خطوة بخطوة على تعديل تسميات مخطط Excel بسرعة.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: كيفية تعيين شكل تسميات بيانات مخطط Excel في Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: كيفية تعيين شكل تسميات بيانات مخطط Excel في Java
url: /ar/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إتقان تخصيص المخططات في Java باستخدام Aspose.Cells: تعديل أشكال تسميات البيانات

## مقدمة

تحسين الجاذبية البصرية لمخططات Excel أمر حاسم عند إعداد التقارير أو لوحات التحكم، خاصة إذا كنت تستخدم Java. مع Aspose.Cells—مكتبة قوية لإدارة وتعديل جداول البيانات—يمكنك **how to set shape** لتسميات بيانات المخطط في بضع أسطر من الشيفرة فقط. سيوجهك هذا الدرس عبر تغيير شكل تسميات البيانات في مخطط Excel باستخدام Aspose.Cells لـ Java. في النهاية، ستعرف كيف:

- الوصول إلى تسميات بيانات المخطط وتعديلها
- تعيين أشكال مخصصة لتسميات البيانات
- حفظ التغييرات في المصنف الخاص بك

## إجابات سريعة
- **ما هو الصنف الأساسي للعمل مع ملفات Excel؟** `Workbook` يمثل ملف Excel كامل في الذاكرة.  
- **ما هي الطريقة التي تحدد شكل التسمية؟** `setShapeType(DataLabelShapeType shape)` على كائن `DataLabel`.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص مؤقت مجاني يعمل للتقييم؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل يمكنني تطبيق الشكل على عدة سلاسل؟** نعم—قم بالتكرار عبر كل سلسلة واستدعِ `setShapeType`.  
- **هل هذا النهج متوافق مع المصنفات الكبيرة؟** Aspose.Cells يعالج مصنفات متعددة المئات من الصفحات دون تحميل الملف بالكامل في الذاكرة.

## ما هو how to set shape؟
تشير عبارة **how to set shape** إلى تكوين الشكل البصري لتسمية بيانات المخطط، مثل تحويل مستطيل عادي إلى فقاعة أو إهليلج. تحسين الشكل يعزز قابلية القراءة ويسلط الضوء على نقاط البيانات الرئيسية. باختيار الشكل المناسب، يمكنك جعل التسمية بارزة، تجميع النقاط ذات الصلة، أو مطابقة إرشادات العلامة التجارية للشركة، مما يحسن القراءة العامة للمخطط.

## لماذا نستخدم Aspose.Cells لتخصيص تسميات المخطط؟
يدعم Aspose.Cells **أكثر من 50 تنسيقًا للإدخال والإخراج**—بما في ذلك XLSX و CSV و ODS و PDF—ويمكنه معالجة مصنفات تحتوي على **ما يصل إلى مليون صف** دون استنزاف الذاكرة. يتيح لك API الخاص به تعديل المخططات برمجيًا، مما يلغي الحاجة إلى تعديلات يدوية في Excel ويضمن تنسيقًا موحدًا عبر التقارير الآلية.

## المتطلبات المسبقة

- **مكتبة Aspose.Cells لـ Java**: الإصدار 25.3 أو أحدث مطلوب.
- **بيئة تطوير Java**: JDK مثبت على جهازك.
- **إعداد IDE**: استخدم IDE مثل IntelliJ IDEA أو Eclipse لكتابة وتشغيل الشيفرة.

### المكتبات والاعتماديات المطلوبة

لمستخدمي Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

يجب على مستخدمي Gradle إضافة هذا إلى ملف `build.gradle` الخاص بهم:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص

توفر Aspose.Cells ترخيصًا تجريبيًا مجانيًا، يمكنك الحصول عليه من [صفحة الترخيص المؤقتة لـ Aspose](https://purchase.aspose.com/temporary-license/). يتيح لك ذلك الوصول الكامل إلى جميع الميزات دون قيود لفترة محدودة.

## إعداد Aspose.Cells لـ Java

بمجرد أن يصبح بيئتك جاهزة، لنقم بإعداد Aspose.Cells. إليك كيفية البدء:

### خطوات التثبيت

1. **تحميل المكتبة**: استخدم Maven أو Gradle كما هو موضح أعلاه.
2. **تكوين الترخيص**:  
   - `License` هو صنف يطبق ملف ترخيص Aspose.Cells الخاص بك لتمكين الوظائف الكاملة.  
   - قم بتحميل وتطبيق ترخيص مؤقت باستخدام مقتطف الشيفرة التالي بعد تهيئة كائن `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **التهيئة الأساسية**: أنشئ مثيلًا من `Workbook` لبدء العمل مع ملفات Excel.

## كيفية تعيين شكل تسميات البيانات في المخطط؟

حمّل المصنف الخاص بك، حدد المخطط المستهدف، وطبق الشكل المطلوب على تسميات البيانات. الخطوات التالية تنفذ ذلك في أقل من دقيقة.

### دليل خطوة بخطوة

#### الخطوة 1: تحميل المصنف الخاص بك

الصنف `Workbook` هو الكائن الأعلى مستوى في Aspose.Cells الذي يمثل ملف Excel واحد في الذاكرة. استخدم `new Workbook("input.xlsx")` لتحميل الملف الذي تريد تعديله.

#### الخطوة 2: الوصول إلى المخطط

`Worksheet` يمثل ورقة واحدة داخل المصنف.  
`Worksheet ws = workbook.getWorksheets().get(0);` يسترجع الورقة الأولى.  
`Chart` هو كائن يمثل مخططًا مدمجًا في ورقة العمل.  
`Chart chart = ws.getCharts().get(0);` يحصل على المخطط الأول في تلك الورقة.

#### الخطوة 3: استرجاع السلاسل وتعديل تسميات البيانات

`Series` يمثل سلسلة بيانات مرسومة على المخطط.  
كل كائن `Series` يحتوي على مجموعة `DataLabel`.  
`DataLabel` يتحكم في مظهر تسمية البيانات لسلسلة معينة.  
`DataLabelShapeType` هو تعداد للأشكال الممكنة لتسميات البيانات.  
استدعِ `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` لتعيين الشكل. يوفر التعداد عشرات الخيارات، مثل `RECTANGLE` و `CLOUD` و `WEDGE_ELLIPSE_CALLOUT`.

#### الخطوة 4: حفظ المصنف الخاص بك

بعد تطبيق الشكل، استدعِ `workbook.save("output.xlsx");` لكتابة التغييرات إلى القرص.

## نصائح استكشاف الأخطاء وإصلاحها

- **مشكلات مسار الملف**: تأكد من أن مسار الملف مطلق أو نسبي بشكل صحيح بالنسبة إلى دليل عمل المشروع.  
- **عدم توافق إصدارات المكتبة**: تأكد من أنك تستخدم Aspose.Cells الإصدار 25.3 أو أحدث؛ الإصدارات القديمة لا تحتوي على طريقة `setShapeType`.  
- **أنواع المخططات غير المدعومة**: بعض أنواع المخططات القديمة (مثل radar) قد لا تعرض خصائص شكل تسمية البيانات؛ استبدلها بنوع مخطط مدعوم مثل العمود أو الخط.

## تطبيقات عملية

1. **التقارير المالية** – إبراز هوامش الربح الرئيسية باستخدام تسميات بنمط الفقاعة.  
2. **المحتوى التعليمي** – استخدم تسميات على شكل سحابة لجذب الانتباه إلى نقاط البيانات المهمة في المواد التعليمية.  
3. **تحليلات التسويق** – تطبيق أشكال مخصصة لتمييز مقاييس أداء الحملات في لوحات التحكم.

دمج Aspose.Cells مع خطوط أنابيب البيانات أو أنظمة CRM يتيح لك إنشاء تقارير ذات تنسيق كامل تلقائيًا، مما يقلل الجهد اليدوي ويضمن توافقًا بصريًا مع العلامة التجارية.

## اعتبارات الأداء

عند العمل مع ملفات Excel الكبيرة:

- **تحسين استهلاك الذاكرة**: استدعِ `workbook.dispose();` بعد الحفظ لإطلاق الموارد الأصلية فورًا.  
- **المعالجة الدفعية**: عالج المخططات على مجموعات بدلاً من واحدة تلو الأخرى لتقليل عبء إنشاء الكائنات.  
- **معالجة البيانات بكفاءة**: تجنّب الحسابات الثقيلة داخل الحلقات التي تتكرر على آلاف الصفوف؛ احسب القيم مسبقًا.

## الخلاصة

أنت الآن تعرف **how to set shape** لتسميات بيانات مخطط Excel في Java باستخدام Aspose.Cells. هذه القدرة لا تعزز فقط جمالية المخطط بل تحسن أيضًا فهم البيانات للمستخدمين النهائيين. استكشف خيارات تخصيص إضافية—مثل ألوان التسميات، الخطوط، وخطوط القائد—لتحسين تصوراتك أكثر.

لأي أسئلة أو مساعدة، راجع [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).

## الأسئلة المتكررة

**س: كيف يمكنني تغيير شكل عدة تسميات بيانات مرة واحدة؟**  
ج: قم بالتكرار عبر كل سلسلة في المخطط واستدعِ `setShapeType` على كائن `DataLabel` الخاص بالسلسلة.

**س: هل يمكن لـ Aspose.Cells لـ Java معالجة ملفات Excel الكبيرة بكفاءة؟**  
ج: نعم. مع إدارة الذاكرة المناسبة، يعالج المصنفات التي تحتوي على مئات الآلاف من الصفوف دون تحميل الملف بالكامل في الذاكرة.

**س: ما هي المشكلات الشائعة عند إعداد Aspose.Cells؟**  
ج: الاعتماديات المفقودة في Maven، استخدام إصدار مكتبة قديم، أو توفير ملف ترخيص غير صالح هي من المشكلات النموذجية.

**س: هل هناك طريقة لإرجاع أشكال تسميات البيانات إلى الوضع الافتراضي؟**  
ج: عيّن نوع الشكل إلى `DataLabelShapeType.DEFAULT` لاستعادة المظهر الأصلي.

**س: كيف يمكنني تطبيق هذا التخصيص على عدة مخططات في مصنف واحد؟**  
ج: قم بالتكرار عبر `ws.getCharts()` وطبق نفس منطق `setShapeType` على مجموعة السلاسل لكل مخطط.

## الموارد

- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [Purchase a License](https://purchase.aspose.com/buy)
- [Free Trial License](https://releases.aspose.com/cells/java/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)

---  

**آخر تحديث:** 2026-10-17  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## دروس ذات صلة

- [تعديل تسميات بيانات مخطط Excel باستخدام Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [كيفية تغيير حجم التسميات في مخططات Excel باستخدام Aspose.Cells لـ Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [إضافة تسميات إلى مخططات Excel باستخدام Aspose Cells لـ Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}