---
date: '2026-04-02'
description: تعلم كيفية إنشاء مخطط وتوليد مخطط فقاعة في Excel باستخدام Aspose.Cells
  للغة Java. يشرح هذا الدليل خطوات الإعداد والبيانات وحفظ المخطط.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'كيفية إنشاء مخطط: مخطط الفقاعات في Excel باستخدام Aspose.Cells Java'
url: /ar/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مخطط: مخطط فقاعة Excel باستخدام Aspose.Cells Java

Enhance your Excel reports with dynamic bubble charts using Aspose.Cells for Java. In this tutorial, you'll learn **how to create chart** objects that visualize data as bubble charts, making your presentations more insightful and interactive. We'll walk through every step—from setting up the development environment to configuring the chart data and finally saving the workbook.

## إجابات سريعة
- **ما هي المكتبة الأفضل لمخططات Excel في Java؟** Aspose.Cells for Java.
- **هل يمكنني إنشاء مخطط فقاعة Excel برمجيًا؟** نعم، باستخدام واجهة برمجة المخططات المعروضة أدناه.
- **هل أحتاج إلى ترخيص لتشغيل الكود؟** النسخة التجريبية المجانية تعمل، لكن الترخيص الكامل يفتح جميع الميزات.
- **ما هي أدوات بناء Java المدعومة؟** Maven و Gradle كلاهما مدعومان.
- **ما هي الطريقة الأساسية لتعيين بيانات مخطط الفقاعة؟** استخدم `setBubbleSizes` و `setXValues` و `setValues` على السلسلة.

## ما هو مخطط الفقاعة؟
A bubble chart is a variation of a scatter plot where each data point is represented by a bubble. The X‑axis and Y‑axis determine the position, while the bubble size conveys a third dimension of information—perfect for visualizing financial, sales, or scientific data.

## لماذا تستخدم Aspose.Cells for Java؟
- **محرك Excel بدون تثبيت** – لا حاجة لـ Microsoft Office على الخادم.
- **واجهة برمجة مخططات غنية** – تدعم جميع أنواع المخططات الحديثة، بما في ذلك مخططات الفقاعة.
- **متعدد المنصات** – يعمل على Windows و Linux و macOS.
- **أداء عالي** – مُحسّن لمجموعات البيانات الكبيرة وتوليد التقارير ذات الحجم الكبير.

## المتطلبات المسبقة

### المكتبات والاعتمادات المطلوبة
- **Aspose.Cells for Java**: قم بتثبيت أحدث نسخة (مثال: 25.3).

### متطلبات إعداد البيئة
- تثبيت مجموعة تطوير Java (JDK) المتوافقة.
- قم بتهيئة مشروعك لاستخدام Maven أو Gradle.

### المتطلبات المعرفية
- فهم أساسي لبرمجة Java.
- إلمام بهياكل ملفات Excel وأنواع المخططات.

## إعداد Aspose.Cells for Java

### التثبيت عبر Maven
Add the following dependency to your `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### التثبيت عبر Gradle
For those using Gradle, add this to your `build.gradle`:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص
Aspose.Cells offers a free trial with limited functionality. For full capabilities:
- **شراء**: زر [صفحة الشراء](https://purchase.aspose.com/buy) للحصول على خيارات الترخيص.
- **ترخيص مؤقت**: احصل على ترخيص مؤقت من [هنا](https://purchase.aspose.com/temporary-license/) للاختبار الكامل.

### التهيئة الأساسية
Before using Aspose.Cells, initialize it in your Java project:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## دليل التنفيذ

### كيفية إنشاء مخطط: تهيئة كائن Workbook
A `Workbook` represents an entire Excel file, allowing you to manipulate sheets, cells, and more. Initialize it as follows:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### كيفية تعيين بيانات مخطط الفقاعة: الوصول إلى الأوراق ومعالجتها
Prepare the data that will feed the bubble chart:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### كيفية إنشاء مخطط فقاعة Excel: إنشاء وتكوين المخطط
Create a bubble chart by adding it to the worksheet and setting its data sources:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### كيفية حفظ المخطط: حفظ الـ Workbook
Persist the workbook (and the embedded chart) to disk:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## التطبيقات العملية
- **التقارير المالية** – تصور الإيرادات، الأرباح، وحصة السوق في عرض واحد.
- **تحليل بيانات المبيعات** – إبراز أداء المبيعات الإقليمية حيث يُظهر حجم الفقاعة الحجم.
- **البحث العلمي** – عرض النتائج التجريبية بثلاث متغيرات في آن واحد.

## اعتبارات الأداء
- تخلص من الكائنات غير المستخدمة بسرعة لتحرير الذاكرة.
- حافظ على أن تكون نطاقات البيانات ضيقة قدر الإمكان؛ النطاقات الكبيرة غير الضرورية قد تبطئ عملية العرض.
- استخدم أفضل ممارسات إدارة الذاكرة في Java عند معالجة مجموعات بيانات ضخمة.

## المشكلات الشائعة والحلول
| المشكلة | السبب | الحل |
|-------|-------|----------|
| **مخطط فارغ** | نطاقات البيانات لا تتطابق مع السلسلة | تحقق من أن `setBubbleSizes` و `setXValues` و `setValues` تشير إلى الخلايا الصحيحة. |
| **أحجام فقاعات غير صحيحة** | اختلاف أطوال النطاقات | تأكد من أن جميع النطاقات الثلاث تحتوي على نفس عدد النقاط. |
| **استثناء الترخيص** | تشغيل بدون ترخيص صالح | طبّق ترخيصًا مؤقتًا أو مُشتَرًى قبل إنشاء الـ Workbook. |

## الأسئلة المتكررة

**س: ما هي أقل نسخة من Aspose.Cells مطلوبة؟**  
ج: يُنصح باستخدام النسخة 25.3 لهذا الدرس لضمان التوافق مع جميع الميزات المعروضة.

**س: كيف يمكنني تخصيص ألوان مخطط الفقاعة؟**  
ج: استخدم طرق تنسيق السلسلة، مثل `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**س: هل يمكنني تشغيل هذا الكود على خوادم Linux؟**  
ج: نعم، Aspose.Cells for Java متوافق تمامًا مع جميع الأنظمة التي تدعم JDK متوافق.

**س: ماذا أفعل إذا حصلت على خطأ “Data source size mismatch”؟**  
ج: تحقق مرة أخرى من أن النطاقات الخاصة بأحجام الفقاعات، قيم X، وقيم Y تحتوي على نفس عدد الخلايا.

**س: أين يمكنني الحصول على ترخيص مؤقت للاختبار؟**  
ج: زر [صفحة الترخيص المؤقت لـ Aspose](https://purchase.aspose.com/temporary-license/) لطلب ترخيص تجريبي.

## الموارد
- **الوثائق**: لمزيد من التفاصيل، راجع [الوثائق الرسمية](https://reference.aspose.com/cells/java/).
- **التنزيل**: احصل على أحدث نسخة من [صفحة الإصدار](https://releases.aspose.com/cells/java/).
- **الشراء**: استكشف خيارات الترخيص على [هذه الصفحة](https://purchase.aspose.com/buy).
- **النسخة التجريبية المجانية**: ابدأ بنسخة تجريبية مجانية لاختبار القدرات في [قسم الإصدارات الخاص بـ Aspose](https://releases.aspose.com/cells/java/).
- **منتدى الدعم**: لأي استفسارات، يتوفر [منتدى الدعم](https://forum.aspose.com/c/cells/9).

**آخر تحديث:** 2026-04-02  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}