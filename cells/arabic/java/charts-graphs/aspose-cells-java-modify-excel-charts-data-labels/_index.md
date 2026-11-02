---
date: '2026-06-22'
description: تعلم كيفية تغيير chart data labels وتخصيص data labels في Excel باستخدام
  Aspose.Cells for Java. يغطي هذا الدليل chart modification وfont formatting، بالإضافة
  إلى أمثلة عملية.
keywords:
- change chart data labels
- customize data labels excel
- format data label fonts
- Aspose.Cells Java chart modification
- Excel automation Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to change chart data labels and customize data labels in
    Excel with Aspose.Cells for Java. This guide covers chart modification, font formatting,
    and practical examples.
  headline: How to Change Chart Data Labels and Modify Excel Charts Using Aspose.Cells
    for Java
  type: TechArticle
- description: Learn how to change chart data labels and customize data labels in
    Excel with Aspose.Cells for Java. This guide covers chart modification, font formatting,
    and practical examples.
  name: How to Change Chart Data Labels and Modify Excel Charts Using Aspose.Cells
    for Java
  steps:
  - name: Create a Workbook
    text: This line creates the `Workbook` instance, giving you full access to worksheets,
      charts, and cells.
  - name: Save the Modified Workbook
    text: After you finish editing, call `save` to write the changes to disk.
  - name: Access First Worksheet
    text: The `Worksheet` class represents a single sheet; accessing it via `getWorksheets().get(0)`
      gives you the first sheet.
  - name: Access First Chart
    text: The `Chart` class encapsulates all chart‑related properties. Once you have
      a reference, you can modify series, axes, and data labels.
  - name: Modify Data Label Text
    text: Use `setText("Your custom label")` on the `DataLabel` object to replace
      the default value.
  - name: Customize Font
    text: The `Font` class lets you set `setBold(true)`, `setColor(Color.getRed())`,
      and other attributes for precise visual control.
  type: HowTo
- questions:
  - answer: Yes, the free trial provides full functionality for development and testing;
      a commercial license is required for production deployments.
    question: Can I use Aspose.Cells for Java without a paid license?
  - answer: It can process files with over 500 MB and 100 + worksheets using less
      than 300 MB of RAM when memory‑optimized settings are enabled.
    question: How does Aspose.Cells handle large Excel files?
  - answer: Absolutely – iterate over `worksheet.getCharts()` and apply the same label‑changing
      logic to each chart object.
    question: Is it possible to modify multiple charts in one workbook?
  - answer: Forgetting to call `setShowValue(true)` on the series, or not disposing
      of the workbook, can lead to missing labels or memory leaks.
    question: What are the most common pitfalls when customizing data labels?
  - answer: Yes, simply add the Maven/Gradle dependency and inject the workbook handling
      code into a Spring service component.
    question: Can Aspose.Cells be integrated with Spring Boot?
  type: FAQPage
title: كيفية تغيير chart data labels وتعديل مخططات Excel باستخدام Aspose.Cells for
  Java
url: /ar/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير تسميات بيانات المخطط وتعديل مخططات Excel باستخدام Aspose.Cells for Java

## مقدمة

يمكن لتغيير تسميات بيانات المخطط برمجياً أن يوفر ساعات من التعديل اليدوي، خاصةً عندما تحتاج إلى إنشاء العشرات من التقارير المالية تلقائياً. في هذا الدرس ستكتشف كيفية **تغيير تسميات بيانات المخطط** في دفتر Excel باستخدام Aspose.Cells for Java، بالإضافة إلى كيفية تخصيص خطوط التسميات للحصول على مظهر مصقول. بنهاية الدليل ستكون قادرًا على تحميل دفتر العمل، تحديد المخطط، وتطبيق تنسيق نص غني على أي تسمية بيانات—كل ذلك دون فتح Excel.

**ما ستتعلمه**
- الوصول إلى دفاتر Excel وتعديلها
- التنقل بين أوراق العمل والمخططات
- تغيير تسميات بيانات المخطط وتخصيص مظهرها
- تنسيق خطوط تسميات البيانات لتأثير بصري قوي

دعنا نتأكد من أن لديك كل ما تحتاجه قبل أن نغوص في الشيفرة.

## إجابات سريعة
- **هل يمكنني تعديل تسميات بيانات المخطط دون فتح Excel؟** نعم، يتيح لك Aspose.Cells تغيير التسميات مباشرة في الملف.
- **أي نسخة من المكتبة تدعم هذه الميزة؟** جميع إصدارات Aspose.Cells for Java 20.10 وما بعدها.
- **هل أحتاج إلى ترخيص مدفوع لتشغيل العينة؟** نسخة التجربة المجانية تكفي للتطوير؛ الترخيص مطلوب للإنتاج.
- **هل Java 8 كافية؟** نعم، Java 8 أو أحدث مدعومة بالكامل.
- **هل يمكنني تنسيق خطوط التسميات (اللون، الغامق، الحجم)؟** بالتأكيد – توفر API تحكمًا كاملًا في نمط الخط.

## ما هو Aspose.Cells for Java؟
Aspose.Cells for Java هو API قوي يتيح إنشاء ومعالجة وتحويل جداول Excel دون الحاجة إلى Microsoft Excel. يدعم **أكثر من 50** تنسيق ملف—بما في ذلك XLSX و CSV و PDF و HTML—ويمكنه معالجة دفاتر عمل متعددة الصفحات باستخدام أقل من 200 ميغابايت من الذاكرة.

## لماذا تغيير تسميات بيانات المخطط؟
يقلل تغيير تسميات بيانات المخطط برمجياً من الأخطاء اليدوية، ويضمن الاتساق عبر التقارير، ويسمح بالتحديثات الديناميكية بناءً على البيانات الفورية. باستخدام Aspose.Cells يمكنك تحديث آلاف المخططات في ثوانٍ، وهو ما قد يستغرق أيامًا إذا تم يدوياً.

## المتطلبات المسبقة

- **مكتبة Aspose.Cells** – أضف ملف JAR عبر Maven أو Gradle (انظر أدناه).  
- **مجموعة تطوير جافا (JDK)** – الإصدار 8 أو أحدث.  
- **IDE** – IntelliJ IDEA أو Eclipse أو أي محرر يدعم Java.

### المكتبات والاعتمادات المطلوبة

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص

توفر Aspose.Cells نسخة تجريبية مجانية، تراخيص مؤقتة للتقييم، وترخيصًا تجاريًا كاملًا. للبدء بالنسخة التجريبية:

1. زر صفحة [Aspose's Free Trial](https://releases.aspose.com/cells/java/).  
2. حمّل المكتبة وطبق ترخيص التجربة في مشروعك.

للاستخدام في الإنتاج، احصل على ترخيص مؤقت أو دائم من [Purchase Page](https://purchase.aspose.com/buy).

### التهيئة الأساسية

فئة `Workbook` هي الكائن الأساسي في Aspose.Cells الذي يمثل ملف Excel كامل في الذاكرة. قم بتهيئتها مع مسار دفتر العمل المصدر:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/source.xlsx");
```

## إعداد Aspose.Cells for Java

بعد إضافة المكتبة إلى مشروعك، قم بتكوين البيئة لتتمكن من التعامل مع ملفات Excel بسلاسة.

### متطلبات إعداد البيئة

- JDK 8+  
- IDE مفضلة (IntelliJ IDEA، Eclipse)  
- Maven أو Gradle لإدارة الاعتمادات  

## دليل التنفيذ

سنستعرض كل خطوة مطلوبة لـ **تغيير تسميات بيانات المخطط** وتطبيق تنسيق خط مخصص.

### الوصول وتعديل دفتر Excel

**نظرة عامة**: تحميل دفتر عمل موجود، إجراء التغييرات، وحفظ نسخة جديدة.

#### كيفية تحميل وحفظ دفتر العمل

حمّل دفتر العمل باستخدام `new Workbook("input.xlsx")` واحفظه عبر `workbook.save("output.xlsx")`. هذا النمط المكوّن من سطرين هو الأساس لجميع العمليات اللاحقة.

#### الخطوة 1: إنشاء دفتر عمل  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/source.xlsx");
```  
هذا السطر ينشئ كائن `Workbook`، مما يمنحك وصولًا كاملًا إلى أوراق العمل، المخططات، والخلايا.

#### الخطوة 2: حفظ دفتر العمل المعدل  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ModifiedData_out.xlsx");
```  
بعد الانتهاء من التعديل، استدعِ `save` لكتابة التغييرات إلى القرص.

### الوصول إلى ورقة العمل في دفتر Excel

**نظرة عامة**: استرجاع ورقة العمل المحددة التي تحتوي على المخطط الذي تريد تحريره.

#### الخطوة 1: الوصول إلى الورقة الأولى  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```  
تمثل فئة `Worksheet` ورقة واحدة؛ الوصول إليها عبر `getWorksheets().get(0)` يعطيك الورقة الأولى.

### الوصول وتعديل المخطط في ورقة العمل

**نظرة عامة**: تحديد كائن المخطط داخل ورقة العمل وتحضيره لتغييرات التسميات.

#### الخطوة 1: الوصول إلى المخطط الأول  
```java
Chart chart = worksheet.getCharts().get(0);
```  
فئة `Chart` تحوي جميع خصائص المخطط. بمجرد الحصول على مرجع، يمكنك تعديل السلاسل، المحاور، وتسميات البيانات.

### تعديل تسميات البيانات في نقطة سلسلة المخطط

**نظرة عامة**: تغيير النص الظاهر لتسمية البيانات لعرض معلومات مخصصة.

`DataLabel` يمثل النص المرفق بنقطة بيانات في المخطط.  
#### الخطوة 1: تعديل نص تسمية البيانات  
```java
DataLabels dlbls = chart.getNSeries().get(0).getPoints().get(0).getDataLabels();
dlbls.setText("Rich Text Label");
```  
استخدم `setText("Your custom label")` على كائن `DataLabel` لاستبدال القيمة الافتراضية.

### تخصيص إعدادات الخط لتسميات البيانات

**نظرة عامة**: تطبيق نمط غامق، تغيير اللون، وتعديل حجم الخط لجعل التسميات بارزة.

#### الخطوة 1: تخصيص الخط  
```java
FontSetting fntSetting = dlbls.characters(0, 10);
fntSetting.getFont().setColor(Color.getRed());
fntSetting.getFont().setBold(true);
```  
تتيح لك فئة `Font` ضبط `setBold(true)`, `setColor(Color.getRed())` وغيرها من الخصائص للتحكم البصري الدقيق.

## كيفية تغيير تسميات بيانات المخطط في Excel باستخدام Aspose.Cells؟

حمّل دفتر العمل، استخرج المخطط المستهدف، ثم تكرار عبر نقاط السلسلة واستدعِ `setText` على كل `DataLabel`. أخيرًا، عدل خصائص `Font` للتسمية لتحقيق المظهر المطلوب. يعمل هذا النهج مع أي نوع مخطط—عمودي، خطي، دائري، أو راداري—ويحدّث جميع التسميات في خطوة واحدة.

## حالات الاستخدام الشائعة

- **لوحات التحكم المالية** – تحديث الأرقام ربع السنوية تلقائيًا مع وصول بيانات جديدة.  
- **تقارير المبيعات** – إبراز المنتجات الأعلى أداءً عبر جعل تسميات البيانات غامقة.  
- **إدارة المشاريع** – عرض نسب إكمال المهام مباشرة على مخططات بنمط Gantt.  

## اعتبارات الأداء

عند معالجة دفاتر عمل كبيرة (200 + صفحة)، ضع في اعتبارك النصائح التالية:

- استخدم `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` لتقليل استهلاك الذاكرة.  
- أغلق كائن `Workbook` فورًا باستخدام `workbook.dispose()` بعد الحفظ.  
- للعمليات الدفعة، أعد استخدام كائن `Workbook` واحد قدر الإمكان لتقليل حمل الـ GC.

## الأسئلة المتكررة

**س: هل يمكنني استخدام Aspose.Cells for Java بدون ترخيص مدفوع؟**  
ج: نعم، نسخة التجربة المجانية توفر جميع الوظائف للتطوير والاختبار؛ الترخيص التجاري مطلوب للنشر في بيئات الإنتاج.

**س: كيف يتعامل Aspose.Cells مع ملفات Excel الكبيرة؟**  
ج: يمكنه معالجة ملفات تزيد عن 500 ميغابايت و100 + ورقة عمل باستخدام أقل من 300 ميغابايت من الذاكرة عند تفعيل إعدادات الذاكرة المُحسّنة.

**س: هل يمكن تعديل عدة مخططات في دفتر عمل واحد؟**  
ج: بالتأكيد – يمكنك التكرار عبر `worksheet.getCharts()` وتطبيق منطق تغيير التسميات على كل مخطط.

**س: ما هي الأخطاء الشائعة عند تخصيص تسميات البيانات؟**  
ج: نسيان استدعاء `setShowValue(true)` على السلسلة، أو عدم إغلاق دفتر العمل، قد يؤدي إلى فقدان التسميات أو تسرب الذاكرة.

**س: هل يمكن دمج Aspose.Cells مع Spring Boot؟**  
ج: نعم، فقط أضف اعتماد Maven/Gradle وحقن كود التعامل مع دفتر العمل في مكوّن خدمة Spring.

## الموارد

- [Aspose Documentation](https://reference.aspose.com/cells/java/)
- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [Purchase Aspose.Cells](https://purchase.aspose.com/buy)
- [Free Trial License](https://releases.aspose.com/cells/java/)
- [Temporary License Acquisition](https://purchase.aspose.com/temporary-license/)
- [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

استكشف هذه الروابط لتعميق خبرتك واكتشاف واجهات برمجة تطبيقات إضافية متعلقة بالمخططات.

---

**آخر تحديث:** 2026-06-22  
**تم الاختبار مع:** Aspose.Cells 24.12 for Java  
**المؤلف:** Aspose  

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [How to Auto-Resize Chart Data Labels in Excel Using Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [How to Add Labels to Excel Charts Using Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Master Aspose.Cells Java for Excel Chart Customization: A Complete Guide](/cells/java/charts-graphs/aspose-cells-java-excel-charts-customization/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}