---
date: '2026-06-12'
description: تعلم كيفية تصدير المخطط إلى PNG باستخدام Aspose.Cells Java، إنشاء صور
  المخططات، عرض مخططات Excel كملفات PNG، وتخصيص التصورات بفعالية.
keywords:
- export chart to png
- java generate chart image
- render excel chart image
- java chart visualization library
- Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-06-12'
  description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  headline: Export chart to PNG using Aspose.Cells Java
  type: TechArticle
- description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  name: Export chart to PNG using Aspose.Cells Java
  steps:
  - name: Verify that **JDK 8** or newer is on your `PATH`.
    text: Verify that **JDK 8** or newer is on your `PATH`.
  - name: Open your preferred IDE and create a new Maven/Gradle Java project.
    text: Open your preferred IDE and create a new Maven/Gradle Java project.
  - name: Add the Aspose.Cells dependency using the snippets above.
    text: Add the Aspose.Cells dependency using the snippets above.
  - name: Add the Maven or Gradle dependency as shown earlier.
    text: Add the Maven or Gradle dependency as shown earlier.
  - name: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
    text: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
  - name: 'Load the license at runtime:'
    text: 'Load the license at runtime:'
  type: HowTo
- questions:
  - answer: Place the `Aspose.Cells.lic` file in the resources folder and load it
      with `License license = new License(); license.setLicense("Aspose.Cells.lic");`.
    question: How do I resolve license activation issues?
  - answer: Yes, it integrates seamlessly with Spring Boot, Jakarta EE, or any servlet
      container.
    question: Can I use Aspose.Cells for Java in a web application?
  - answer: Forgetting to update the source data before calling `calculate()` leads
      to stale visuals.
    question: What are common pitfalls when refreshing charts?
  - answer: Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` and process
      worksheets in streams.
    question: How do I handle large Excel files efficiently?
  - answer: PNG, JPEG, BMP, and TIFF are fully supported; choose PNG for loss‑less
      quality.
    question: What image formats are supported for rendering charts?
  type: FAQPage
title: تصدير المخطط إلى PNG باستخدام Aspose.Cells Java
url: /ar/java/charts-graphs/aspose-cells-java-load-customize-excel-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى PNG باستخدام Aspose.Cells Java

## المقدمة

تصدير مخطط إلى PNG هو طلب شائع عندما تحتاج إلى تضمين بيانات بصرية في التقارير أو العروض التقديمية أو صفحات الويب. باستخدام **Aspose.Cells for Java**، يمكنك تحميل مصنف Excel موجود، تحديث بيانات المخطط، تطبيق إعدادات العولمة، وعرض المخطط مباشرة كصورة PNG عالية الجودة — كل ذلك دون الحاجة إلى تثبيت Microsoft Excel. في هذا البرنامج التعليمي ستكتشف كيفية **export chart to PNG**، إنشاء صور المخططات برمجياً، وتخصيص المخرجات للجماهير العالمية.

## إجابات سريعة
- **كيف يمكنني تصدير مخطط إلى PNG؟** حمّل المصنف، وصول إلى المخطط، واستدعِ `chart.toImage()` مع ضبط `ImageOrPrintOptions` على PNG.  
- **أي مكتبة تدعم إنشاء صور مخططات Java؟** Aspose.Cells for Java توفر API كاملة لتصيير مخططات Excel كصور.  
- **هل أحتاج إلى ترخيص لتصدير PNG؟** النسخة التجريبية المجانية تعمل، لكن الترخيص التجاري يزيل حدود التقييم.  
- **هل يمكنني تخصيص تنسيقات الأرقام عالمياً؟** نعم، استخدم `Workbook.getSettings().setGlobalizationSettings()` قبل التصيير.  
- **هل PNG هو التنسيق الوحيد؟** لا، يمكنك أيضاً تصيير إلى JPEG أو BMP أو TIFF بتغيير خيار تنسيق الصورة.

## ما هو Aspose.Cells for Java؟
`Aspose.Cells for Java` هي **مكتبة معالجة جداول بيانات مبنية على Java** تمكّن المطورين من إنشاء، تعديل، تحويل، وعرض ملفات Excel دون الحاجة إلى Microsoft Office. تدعم أكثر من 50 تنسيق ملف، تتعامل مع مصنفات تحتوي على آلاف الصفوف، ويمكنها تصيير المخططات إلى صور في أقل من ثانية على عتاد الخادم النموذجي.

## لماذا تصدير المخطط إلى PNG باستخدام Aspose.Cells؟
تصدير المخططات إلى PNG باستخدام Aspose.Cells يوفر أداءً عاليًا، استهلاكًا منخفضًا للذاكرة، وتنوعًا في الصيغ مع إلغاء الحاجة إلى Microsoft Excel. المكتبة تصيّر المخططات في أقل من ثانية، تحافظ على استهلاك الذاكرة بشكل معتدل، وتدعم PNG و JPEG و BMP و TIFF، مما يجعلها مثالية للنشر على الويب، الطباعة، والتوزيع عبر المنصات.

## المتطلبات المسبقة

- **Aspose.Cells for Java** v25.3 (أو أحدث).  
- **JDK 8+** مثبت على جهاز التطوير الخاص بك.  
- **IDE** مثل IntelliJ IDEA أو Eclipse.  
- **Maven أو Gradle** لإدارة التبعيات.  

### المكتبات والتبعيات المطلوبة

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

### إعداد البيئة

1. تحقق من أن **JDK 8** أو أحدث موجود في `PATH` الخاص بك.  
2. افتح IDE المفضل لديك وأنشئ مشروع Java جديد باستخدام Maven/Gradle.  
3. أضف تبعية Aspose.Cells باستخدام المقاطع أعلاه.  

### الحصول على الترخيص

توفر Aspose.Cells نسخة تجريبية مجانية لتقييم ميزاتها:

- [تحميل نسخة تجريبية مجانية](https://releases.aspose.com/cells/java/)  
- لالاستخدام الإنتاجي، اشترِ ترخيصًا عبر [شراء Aspose.Cells](https://purchase.aspose.com/buy).  
- يمكن طلب ترخيص مؤقت للاختبار الموسع.

## إعداد Aspose.Cells للـ Java

بمجرد أن تكون بيئتك جاهزة، قم بتهيئة Aspose.Cells في مشروعك:

1. أضف تبعية Maven أو Gradle كما هو موضح أعلاه.  
2. ضع ملف الترخيص الخاص بك (`Aspose.Cells.lic`) في مجلد الموارد (resources) بالمشروع.  
3. حمّل الترخيص أثناء التشغيل:

```java
   License license = new License();
   license.setLicense("path/to/Aspose.Total.Java.lic");
   ```  

## دليل التنفيذ

سنستعرض ثلاث سيناريوهات أساسية: تحميل وتحديث مخطط، تخصيص إعدادات العولمة، وتصيير المخطط إلى PNG.

### كيفية تصدير المخطط إلى PNG باستخدام Aspose.Cells Java؟

لتصدير مخطط إلى PNG باستخدام Aspose.Cells للـ Java، أولاً حمّل المصنف باستخدام الفئة `Workbook`، ثم استخرج كائن `Chart` المطلوب من ورقة العمل المناسبة. اضبط `ImageOrPrintOptions` لتحديد تنسيق الصورة إلى PNG، وأخيرًا استدعِ `chart.toImage(outputStream, options)`. يحتوي التيار الناتج على صورة PNG عالية الجودة يمكن حفظها أو إرسالها مباشرةً إلى العميل.

### تحميل وتحديث مخطط من ملف Excel

**نظرة عامة**: حمّل مصنفًا موجودًا، تأكد من أن المخطط يعكس أحدث البيانات، وحضّره للتصيير.

#### 1. تحميل المصنف  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  
*تعريف*: تمثل فئة `Workbook` ملف Excel كامل في الذاكرة، وتوفر الوصول إلى أوراق العمل، المخططات، والخلايا.

#### 2. الوصول إلى ورقة العمل والمخطط  
```java
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
```  
*تعريف*: كائن `Worksheet` يمنحك إمكانية الوصول إلى الصفوف/الأعمدة، بينما كائن `Chart` يضم جميع خصائص المخطط.

#### 3. تحديث المخطط  
```java
chart.calculate();
```  
استدعاء `calculate()` يجبر المخطط على إعادة حساب سلاسله بناءً على أي بيانات مصدر تم تغييرها، مما يضمن دقة العرض.

### تخصيص إعدادات العولمة للمخططات

**نظرة عامة**: ضبط تنسيقات التاريخ والوقت والأرقام لتتناسب مع المعايير الإقليمية قبل التصيير.

#### 1. تحميل المصنف  
```java
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  

#### 2. تعيين إعدادات العولمة المخصصة  
```java
CustomSettings customGlobalizationSettings = new CustomSettings();
customGlobalizationSettings.setChartSettings(new CustomChartGlobalizationSettings());
book.getSettings().setGlobalizationSettings(customGlobalizationSettings);
```  
يمكنك تحديد أنماط خاصة بالمنطقة مثل `"dd-MMM-yyyy"` للتواريخ أو `"#,##0.00"` للأرقام، لضمان أن PNG المُصدّر يحترم المعايير المحلية.

### تصيير المخطط إلى صورة

**نظرة عامة**: تحويل المخطط المحدث إلى ملف PNG يمكن استخدامه في العروض التقديمية أو ملفات PDF أو صفحات الويب.

#### 1. تحميل المصنف والوصول إلى المخطط  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
chart.calculate();
```  

#### 2. التصيير إلى صورة  
```java
ImageOrPrintOptions options = new ImageOrPrintOptions();
chart.toImage(outDir + "CustomTextforOtherLabelofPieChart_out.png", options);
```  
طريقة `toImage()` تكتب المخطط إلى `java.io.OutputStream`. من خلال ضبط `ImageOrPrintOptions.setImageFormat(ImageFormat.png)`, ستحصل على ملف PNG واضح.

## تطبيقات عملية

- **تقارير الأعمال** – تضمين مخططات PNG في مستندات PDF أو Word لتوزيعها على أصحاب المصلحة.  
- **لوحات البيانات** – تحديث المخططات مباشرةً مع وصول بيانات جديدة، ثم تصييرها إلى PNG لتسليم سريع على الويب.  
- **الامتثال العالمي** – تطبيق تنسيقات أرقام وتواريخ خاصة بالمنطقة لتلبية المتطلبات التنظيمية الإقليمية.

## اعتبارات الأداء

- **إدارة الذاكرة**: استخدم `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` للملفات الكبيرة.  
- **تحديث انتقائي**: استدعِ `chart.calculate()` فقط على المخططات التي تغيرت بيانات مصدرها.  
- **سلامة الخيوط**: أنشئ كائن `Workbook` منفصل لكل خيط لتجنب مشكلات التزامن.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| الترخيص غير موجود | تحقق من مسار `Aspose.Cells.lic` وتأكد من أنه على classpath. |
| إخراج PNG فارغ | تأكد من أن المخطط غير مخفي وأنه تم استدعاء `calculate()` قبل التصيير. |
| تصيير بطيء على ملفات كبيرة | فعّل `MemorySetting.MEMORY_PREFERENCE` وصيّر فقط ورقة العمل المطلوبة. |

## الأسئلة المتكررة

**س: كيف يمكنني حل مشكلات تفعيل الترخيص؟**  
ج: ضع ملف `Aspose.Cells.lic` في مجلد الموارد وحمّله باستخدام `License license = new License(); license.setLicense("Aspose.Cells.lic");`.

**س: هل يمكنني استخدام Aspose.Cells for Java في تطبيق ويب؟**  
ج: نعم، يتكامل بسلاسة مع Spring Boot أو Jakarta EE أو أي حاوية servlet.

**س: ما هي الأخطاء الشائعة عند تحديث المخططات؟**  
ج: نسيان تحديث بيانات المصدر قبل استدعاء `calculate()` يؤدي إلى صور قديمة.

**س: كيف يمكنني التعامل مع ملفات Excel الكبيرة بكفاءة؟**  
ج: استخدم `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` وعالج أوراق العمل في تدفقات.

**س: ما هي صيغ الصور المدعومة لتصيير المخططات؟**  
ج: PNG و JPEG و BMP و TIFF مدعومة بالكامل؛ اختر PNG لجودة بدون فقدان.

## الموارد

- **الوثائق**: [Aspose.Cells Java API](https://reference.aspose.com/cells/java/)  
- **التنزيلات**: [إصدارات Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **الشراء والترخيص**: [شراء Aspose.Cells](https://purchase.aspose.com/buy)  
- **نسخة تجريبية مجانية**: [احصل على نسخة تجريبية مجانية من Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **ترخيص مؤقت**: [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)  
- **الدعم والمنتديات**: [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9)

من خلال إتقان هذه الخطوات، يمكنك بثقة **export chart to PNG** ودمج تصورات بصرية عالية الجودة في أي حل مبني على Java.

---

**آخر تحديث:** 2026-06-12  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [كيفية تصدير مخططات Excel كـ SVG باستخدام Aspose.Cells Java للرسومات المتجهة القابلة للتوسع](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells للـ Java: دليل أحجام الصفحات المخصصة](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [كيفية تخصيص مخططات Excel بألوان السمة باستخدام Aspose.Cells Java](/cells/java/charts-graphs/customize-excel-charts-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```text
// Direct answer (no code block needed here as per preservation rules)
```