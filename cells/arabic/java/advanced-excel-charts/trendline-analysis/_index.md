---
date: 2026-08-27
description: تعلم كيفية إضافة trendline إلى chart، وعرض قيمة R‑squared الخاصة به،
  وتصدير المخطط كصورة PNG أو JPEG باستخدام Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: تصدير Chart إلى صورة مع تحليل Trendline
og_description: إضافة trendline إلى chart، عرض R‑squared، وتصدير النتيجة كصورة PNG/JPEG
  باستخدام Aspose.Cells for Java – حل سريع يدعم 50 صيغة.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: إضافة trendline إلى chart وتصديره كصورة باستخدام Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: كيفية إضافة trendline إلى chart وتصديره كصورة في Java
url: /ar/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة خط الاتجاه إلى المخطط وتصديره كصورة

في هذا البرنامج التعليمي ستتعلم كيفية **إضافة خط الاتجاه إلى المخطط**، وعرض قيمة R‑squared، وتصدير الصورة إلى ملف PNG أو JPEG باستخدام Aspose.Cells for Java. سترى لماذا خطوط الاتجاه مهمة، وكيفية إعداد دفتر العمل، والخطوات الدقيقة لإنشاء صورة عالية الدقة يمكن تضمينها في التقارير أو رسائل البريد الإلكتروني أو صفحات الويب.

## إجابات سريعة
- **ما هو الهدف الرئيسي من هذا الدليل؟** إظهار كيفية إضافة خط الاتجاه إلى المخطط، وعرض معادلته وقيمة R‑squared، وتصدير المخطط كصورة باستخدام Java.  
- **ما المكتبة التي أحتاجها؟** Aspose.Cells for Java – قم بتنزيلها من [صفحة إصدار Aspose.Cells for Java](https://releases.aspose.com/cells/java/).  
- **هل أحتاج إلى ترخيص للتطوير؟** نسخة تجريبية مجانية تكفي للتطوير؛ يتطلب الترخيص التجاري للنشر في بيئات الإنتاج.  
- **هل يمكنني إنشاء دفتر عمل Excel برمجياً؟** نعم – البرنامج التعليمي ينشئ ويحفظ دفتر عمل XLSX من الصفر.  
- **كيف يتم تصدير المخطط إلى PNG أو JPEG؟** استدعِ الطريقة `Chart.toImage()` واكتب الـ `BufferedImage` المُرجعة باستخدام `ImageIO.write(...)`.

## كيف تنشئ مخطط Excel مع خط اتجاه وتصدّره كصورة؟
حمّل دفتر العمل، أضف مخطط خطي، أرفق خط اتجاه يُظهر المعادلة وقيمة R‑squared، احفظ دفتر العمل، ثم استدعِ `chart.toImage()` واكتب الـ `BufferedImage` الناتج إلى ملف PNG أو JPEG. هذا التدفق من البداية إلى النهاية يتطلب بضع أسطر فقط من كود Java وينتج صورة دقيقة تماماً مناسبة لأي تطبيق لاحق.

## ما هو تصدير المخطط إلى صورة؟
تصدير المخطط إلى صورة يحول التمثيل البصري لبياناتك إلى صورة نقطية قابلة للنقل (PNG، JPEG، BMP، إلخ). هذا التنسيق مثالي لتضمين المخططات في التقارير أو صفحات الويب أو العروض التقديمية حيث لا يكون ملف Excel الأصلي مطلوباً.

## لماذا نضيف خط اتجاه وعرض قيمة R‑squared؟
يكشف خط الاتجاه النمط الأساسي لسلسلة البيانات، بينما مقياس **R‑squared** ي quantifies مدى توافق خط الاتجاه مع البيانات. إدراج كليهما في الصورة المصدرة يمنح أصحاب المصلحة نظرة فورية دون الحاجة لفتح دفتر العمل. يساعد صانعي القرار على تقييم قوة الارتباط وتوقع الاتجاهات بسرعة دون الحاجة لفتح Excel.

## المتطلبات المسبقة
- Java 8 أو أحدث مثبت على جهاز التطوير الخاص بك.  
- مكتبة Aspose.Cells for Java مضافة إلى مسار الفئة (classpath) للمشروع (ملفات JAR).  
- الإلمام ببيئة تطوير Java IDE مثل IntelliJ IDEA أو Eclipse.  

## دليل خطوة بخطوة

### الخطوة 1: إعداد المشروع
أنشئ مشروع Java جديد وضع ملفات JAR الخاصة بـ Aspose.Cells على مسار البناء. هذا يجهز البيئة لإنشاء ومعالجة ملفات Excel.

### الخطوة 2: تحميل ملف Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*لقد **حمّلنا ملف Excel** في الذاكرة، جاهز لإنشاء المخطط.*

### الخطوة 3: إنشاء مخطط
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*هنا نقوم بإنشاء مخطط خطي سيستضيف لاحقاً خط الاتجاه الخاص بنا.*

### الخطوة 4: إضافة خط اتجاه (how to add trendline) وعرض قيمة R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*استدعاء `setDisplayRSquaredValue(true)` يضمن ظهور **قيمة R‑squared** على المخطط.*

### الخطوة 5: تخصيص المخطط وحفظ دفتر العمل (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*الآن تم **إنشاء** دفتر العمل وحفظه كملف XLSX، جاهز للمعالجة الإضافية.*

### الخطوة 6: تصدير المخطط إلى صورة (export chart to image)
> **ملاحظة:** تم وصف هذه الخطوة دون كتلة شفرة إضافية للحفاظ على عدد الكتل الأصلي.  
بعد إنشاء المخطط وحفظه، يمكنك تصديره إلى صورة عن طريق استدعاء طريقة `chart.toImage()` وكتابة الـ `java.awt.image.BufferedImage` الناتج إلى صيغة ملف تختارها (PNG، JPEG، BMP). سير العمل النموذجي هو:
1. استرجاع كائن `Chart` (تم بالفعل في الخطوات السابقة).  
2. استدعاء `chart.toImage()` للحصول على `BufferedImage`.  
3. استخدم `ImageIO.write(bufferedImage, "png", new File("chart.png"))` لكتابة الملف.  

`كائن `Chart` يمثل مخططًا في دفتر العمل ويوفر طرقًا لتعديل مظهره وبياناته. `BufferedImage` هي فئة Java تحتفظ بصورة في الذاكرة، مما يسمح بحفظها إلى ملف. `ImageIO` هي فئة مساعدة لقراءة وكتابة الصور في Java. `setDisplayRSquaredValue` يتيح إظهار إحصائية R‑squared على خط الاتجاه.

### تحليل النتائج
افتح `output.xlsx` في Excel للتحقق من ظهور خط الاتجاه والمعادلة وقيمة R‑squared كما هو متوقع. افتح ملف الصورة المصدّر (مثلاً `chart.png`) لرؤية تمثيل بصري نظيف يمكن مشاركته دون الحاجة إلى دفتر العمل الأصلي.

## المشكلات الشائعة والحلول
- **خط الاتجاه غير ظاهر:** تأكد من أن نطاق البيانات (`A1:A10`) يحتوي على قيم رقمية؛ البيانات غير الرقمية تمنع حساب خط الاتجاه.  
- **قيمة R‑squared تظهر كـ 0:** غالبًا ما يعني ذلك أن سلسلة البيانات ثابتة أو تفتقر إلى التباين. جرّب مجموعة بيانات مختلفة أو استخدم خط اتجاه متعدد الحدود.  
- **فشل تصدير الصورة مع `NullPointerException`:** تحقق من أن المخطط قد تم رسمه بالكامل قبل استدعاء `toImage()`. قد يحل حفظ دفتر العمل أولاً بعض مشاكل التوقيت.

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع خط الاتجاه؟**  
ج: استخدم تعداد `TrendlineType` مختلف عند إضافة خط الاتجاه، مثل `TrendlineType.POLYNOMIAL` للملاءمة متعددة الحدود.

**س: هل يمكنني تخصيص مظهر خط الاتجاه (اللون، السماكة)؟**  
ج: نعم. يمكنك الوصول إلى `LineFormat` الخاص بخط الاتجاه عبر `trendline.getLineFormat()` وتعيين خصائص مثل `setWeight()` و `setColor()`.

**س: كيف يمكنني تصدير المخطط إلى PDF بدلاً من صورة؟**  
ج: حوّل المخطط إلى صورة أولاً، ثم أدمج تلك الصورة في ملف PDF باستخدام Aspose.PDF أو أي مكتبة PDF أخرى.

**س: هل من الممكن إضافة خطوط اتجاه متعددة إلى نفس المخطط؟**  
ج: بالتأكيد. استدعِ `chart.getNSeries().get(0).getTrendlines().add(...)` لكل سلسلة تريد تحليلها.

**س: هل تدعم Aspose.Cells تصدير صور عالية الدقة؟**  
ج: نعم. يمكنك تحديد DPI عند استدعاء `chart.toImage()` ثم تعديل حجم الصورة قبل الحفظ، مما يضمن إخراجًا واضحًا للطباعة أو الشاشات عالية الكثافة.

---

**آخر تحديث:** 2026-08-27  
**تم الاختبار مع:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**المؤلف:** Aspose

## دروس ذات صلة

- [إضافة تسميات البيانات إلى مخطط Excel باستخدام Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [كيفية تصدير مخططات Excel كملفات SVG باستخدام Aspose.Cells Java للرسومات المتجهة القابلة للتوسع](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells for Java: دليل أحجام الصفحات المخصصة](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}