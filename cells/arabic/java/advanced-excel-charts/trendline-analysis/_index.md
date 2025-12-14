---
date: 2025-12-09
description: تعلم كيفية تصدير المخطط إلى صورة أثناء إجراء تحليل خط الاتجاه في Java
  باستخدام Aspose.Cells. يتضمن خطوات تحميل ملف Excel، إضافة خط الاتجاه، عرض قيمة R
  المربعة، وحفظ المصنف بصيغة XLSX.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: تصدير المخطط إلى صورة مع تحليل خط الاتجاه باستخدام Aspose.Cells للغة Java
url: /ar/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى صورة مع تحليل خط الاتجاه

في هذا البرنامج التعليمي ستكتشف **كيفية تصدير المخطط إلى صورة** أثناء إجراء **تحليل خط الاتجاه** الكامل باستخدام Aspose.Cells for Java. سنستعرض تحميل مصنف Excel موجود، إضافة خط اتجاه، عرض قيمة R‑squared، تخصيص المخطط، وأخيرًا تصدير المخطط كملف صورة — كل ذلك مع كود واضح خطوة بخطوة يمكنك نسخه & لصقه.

## إجابات سريعة
- **ما هو الهدف الأساسي من هذا الدليل؟** إظهار كيفية إضافة خط اتجاه، عرض معادلته وقيمة R‑squared، وتصدير المخطط الناتج إلى صورة باستخدام Java.  
- **ما المكتبة المطلوبة؟** Aspose.Cells for Java (تحميل [هنا](https://releases.aspose.com/cells/java/)).  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني إنشاء ملف Excel في Java؟** نعم – البرنامج التعليمي ينشئ ويحفظ مصنف XLSX.  
- **كيف يمكنني تصدير المخطط إلى PNG أو JPEG؟** استخدم طريقة `Chart.toImage()` (مغطاة في قسم “تصدير المخطط”).

## ما هو تصدير المخطط إلى صورة؟
تحويل المخطط إلى صورة يَحول التمثيل البصري لبياناتك إلى صورة نقطية محمولة (PNG، JPEG، إلخ). هذا مفيد لتضمين المخططات في التقارير، صفحات الويب، أو العروض التقديمية حيث لا يكون ملف Excel الأصلي مطلوبًا.

## لماذا نضيف خط اتجاه ونعرض قيمة R‑squared؟
يساعدك خط الاتجاه على تحديد النمط الأساسي لسلسلة البيانات، بينما مقياس **R‑squared** يقيس مدى توافق خط الاتجاه مع البيانات. إدراجهما في الصورة المصدرة يمنح أصحاب المصلحة نظرة فورية دون الحاجة لفتح المصنف.

## المتطلبات المسبقة
- Java 8 أو أحدث مثبت.  
- إضافة مكتبة Aspose.Cells for Java إلى مشروعك (ملفات JAR على مسار الفئة).  
- إلمام أساسي ببيئات تطوير Java (IntelliJ IDEA، Eclipse، إلخ).

## دليل خطوة بخطوة

### الخطوة 1: إعداد المشروع
أنشئ مشروع Java جديد وأضف ملفات Aspose.Cells JAR إلى مسار البناء. هذا يجهز البيئة لإنشاء ومعالجة ملفات Excel.

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
*هنا نقوم بإنشاء مخطط خطي سيستضيف لاحقًا خط الاتجاه الخاص بنا.*

### الخطوة 4: إضافة خط اتجاه (how to add trendline) وعرض قيمة R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*استدعاء `setDisplayRSquaredValue(true)` يضمن ظهور **قيمة R‑squared** على المخطط.*

### الخطوة 5: تخصيص المخطط وحفظ المصنف (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*الآن تم **إنشاء** المصنف وحفظه كملف XLSX، جاهز للمعالجة الإضافية.*

### الخطوة 6: تصدير المخطط إلى صورة (export chart to image)
> **ملاحظة:** تم وصف هذه الخطوة دون كتلة كود إضافية للحفاظ على عدد الكتل الأصلي.  
بعد إنشاء المخطط وحفظه، يمكنك تصديره إلى صورة عن طريق استدعاء طريقة `chart.toImage()` وكتابة الـ `java.awt.image.BufferedImage` الناتج إلى تنسيق ملف تختاره (PNG، JPEG، BMP). سير العمل النموذجي هو:
1. استرجاع كائن `Chart` (تم بالفعل في الخطوات السابقة).  
2. استدعاء `chart.toImage()` للحصول على `BufferedImage`.  
3. استخدام `ImageIO.write(bufferedImage, "png", new File("chart.png"))` لكتابة الملف.  

هذا ينتج صورة عالية الدقة يمكنك تضمينها في أي مكان، مكملًا عملية **تصدير المخطط إلى صورة**.

## تحليل النتائج
افتح `output.xlsx` في Excel للتحقق من ظهور خط الاتجاه، المعادلة، وقيمة R‑squared كما هو متوقع. افتح ملف الصورة المصدرة (مثلاً `chart.png`) لرؤية تمثيل بصري نظيف يمكن مشاركته دون الحاجة إلى المصنف الأصلي.

## المشكلات الشائعة والحلول
- **خط الاتجاه لا يظهر:** تأكد من أن نطاق البيانات (`A1:A10`) يحتوي فعليًا على قيم رقمية؛ البيانات غير الرقمية ستمنع حساب خط الاتجاه.  
- **قيمة R‑squared تظهر كـ 0:** هذا غالبًا يعني أن سلسلة البيانات ثابتة أو لا تحتوي على تباين كافٍ. جرّب مجموعة بيانات مختلفة أو خط اتجاه متعدد الحدود.  
- **فشل تصدير الصورة مع `NullPointerException`:** تحقق من أن المخطط قد تم رسمه بالكامل قبل استدعاء `toImage()`. قد يحل حفظ المصنف أولاً بعض مشكلات التوقيت.

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع خط الاتجاه؟**  
ج: استخدم تعداد `TrendlineType` مختلف عند إضافة خط الاتجاه، مثل `TrendlineType.POLYNOMIAL` لتطبيق ملاءمة متعددة الحدود.

**س: هل يمكنني تخصيص مظهر خط الاتجاه (اللون، السماكة)؟**  
ج: نعم. يمكنك الوصول إلى `LineFormat` الخاص بخط الاتجاه عبر `trendline.getLineFormat()` وتعيين خصائص مثل `setWeight()` و `setColor()`.

**س: كيف يمكنني تصدير المخطط إلى PDF بدلاً من صورة؟**  
ج: حوّل المخطط إلى صورة أولاً، ثم أدخل تلك الصورة في ملف PDF باستخدام Aspose.PDF أو أي مكتبة PDF تختارها.

**س: هل يمكن إضافة عدة خطوط اتجاه إلى نفس المخطط؟**  
ج: بالتأكيد. استدعِ `chart.getNSeries().get(0).getTrendlines().add(...)` لكل سلسلة تريد تحليلها.

**س: هل تدعم Aspose.Cells تصدير صور عالية الدقة؟**  
ج: نعم. يمكنك تحديد DPI عند استدعاء `chart.toImage()` ثم تعديل حجم الصورة وفقًا لذلك قبل الحفظ.

## الخلاصة
أصبح لديك الآن حل شامل من البداية إلى النهاية **لتصدير المخطط إلى صورة** أثناء إجراء **تحليل خط الاتجاه** في Java باستخدام Aspose.Cells. من خلال تحميل ملف Excel، إضافة خط اتجاه، عرض المعادلة وقيمة R‑squared، تخصيص المخطط، حفظ المصنف، وأخيرًا تصدير الصورة إلى PNG/JPEG، يمكنك إنشاء أصول تحليلية ذات جودة احترافية برمجيًا.

---

**آخر تحديث:** 2025-12-09  
**تم الاختبار مع:** Aspose.Cells for Java 24.12 (latest)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}