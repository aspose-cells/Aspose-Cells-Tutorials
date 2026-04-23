---
date: '2026-04-08'
description: تعلم كيفية إنشاء مخطط عمودي في Java باستخدام Aspose.Cells، مع تغطية إنشاء
  المخطط في Java، إضافة ورقة مخطط، وتصدير دفتر العمل إلى Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: إنشاء مخطط عمودي باستخدام Aspose.Cells دليل Java
url: /ar/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مخطط عمودي باستخدام Aspose.Cells Java

في تطبيقات اليوم المعتمدة على البيانات، **generating a column chart** بسرعة وبرمجياً يمكن أن يحول الأرقام الخام إلى رؤى بصرية واضحة. سواءً كنت تبني لوحة تقارير، أداة تحليل، أو ميزة تصدير بسيطة، توفر لك Aspose.Cells for Java واجهة برمجة تطبيقات سلسة **create chart java** للمشاريع دون الحاجة للتعامل مع واجهة Excel. في هذا البرنامج التعليمي ستتعلم كيفية إعداد المكتبة، **populate Excel cells**، إضافة **chart sheet**، تخصيص **chart title**، وأخيراً **export workbook excel** إلى ملف.

## إجابات سريعة
- **What does “generate column chart” mean?** إنه ينشئ تصورًا من نوع شريط عمودي من البيانات الجدولية.  
- **Which library is required?** Aspose.Cells for Java (متاح نسخة تجريبية مجانية).  
- **Do I need an Excel installation?** لا، المكتبة تعمل بشكل مستقل عن Microsoft Excel.  
- **Can I export to formats other than XLS?** نعم – PDF، PNG، SVG، إلخ، عبر `workbook.save()`.  
- **Is a license mandatory for production?** نعم، يلزم الحصول على ترخيص مشترا أو مؤقت.  

## ما هو generate column chart؟
مخطط عمودي يعرض سلاسل البيانات كأشرطة عمودية، مما يسهل مقارنة القيم عبر الفئات مثل المناطق، الأشهر، أو خطوط المنتجات. تتيح لك Aspose.Cells بناء هذا المخطط بالكامل عبر الكود، مما يمنحك تحكمًا كاملاً في البيانات، التنسيق، وصيغة الإخراج.

## لماذا تستخدم Aspose.Cells لإنشاء chart java؟
- **No COM interop** – يعمل على أي نظام تشغيل يحتوي على JVM.  
- **Rich styling options** – صور، تدرجات، أساطير، وخطوط مخصصة.  
- **High performance** – مناسب لمجموعات البيانات الكبيرة.  
- **Multiple export formats** – XLS، XLSX، PDF، PNG، وأكثر.  

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8+** مثبت.  
- معرفة أساسية بـ Java وإلمام بمفاهيم Excel.  

### المكتبات المطلوبة
أضف Aspose.Cells إلى مشروعك باستخدام أحد المقاطع البرمجية أدناه.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### الحصول على الترخيص
توفر Aspose نسخة تجريبية مجانية وترخيصًا مؤقتًا للاختبار المكثف.

- **Free Trial**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Request Here](https://purchase.aspose.com/temporary-license/)

## إعداد Aspose.Cells لـ Java

أولاً، أنشئ كائن `Workbook` – سيكون هذا القماش لبياناتنا ومخططنا.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## دليل خطوة بخطوة

### 1. إنشاء وتسمية ورقة عمل
سنخزن البيانات الخام في ورقة تسمى **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. ملء خلايا Excel
أدرج أسماء المناطق وأرقام المبيعات التي سيعرضها المخطط العمودي.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. إضافة ورقة مخطط
فصل المخطط عن البيانات الخام يحافظ على تنظيم المصنف.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. إنشاء مخطط عمودي
الآن نقوم فعليًا بإنشاء كائنات **generate column chart**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. تعيين صورة كملء خلفية في منطقة الرسم
يمكن أن تجعل الصورة الخلفية المخطط يبرز.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. تعيين عنوان المخطط
تخصيص **set chart title** يحسن قابلية القراءة.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. تكوين بيانات السلسلة والوسيلة الإيضاحية
ربط نطاق البيانات بالمخطط وتحديد موضع الوسيلة الإيضاحية.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. تصدير مصنف Excel
أخيرًا، **export workbook excel** إلى ملف XLS (أو أي صيغة مدعومة).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## تطبيقات عملية
- **Business Reports** – إنشاء تلقائي لمخططات المبيعات للملفات PDF الشهرية.  
- **Data Analysis Tools** – تضمين مخططات ديناميكية في لوحات تحليلات مخصصة.  
- **Enterprise Dashboards** – تحديث صور المخططات فورًا للمراقبة في الوقت الحقيقي.  

## اعتبارات الأداء
- تحديثات خلايا على دفعات عند العمل مع مجموعات بيانات كبيرة لتقليل الحمل.  
- تحرير الموارد (`workbook.dispose()`) إذا قمت بمعالجة العديد من المصنفات في حلقة.  

## المشكلات الشائعة والحلول
- **Image not showing** – تحقق من مسار الملف وأن صيغة الصورة (PNG، JPEG) مدعومة.  
- **Chart appears blank** – تأكد من أن مراجع نطاق البيانات (`Data!B2:B8`) تتطابق مع الخلايا المملوءة.  
- **Out‑of‑memory errors** – عالج البيانات على دفعات واستدعِ `System.gc()` بعد عمليات حفظ كبيرة.  

## الأسئلة المتكررة

**Q: كيف يمكنني إضافة سلاسل متعددة إلى مخطط عمودي؟**  
A: Call `chart.getNSeries().add()` repeatedly with different data ranges, e.g., `"Data!C2:C8"` for a second series.

**Q: هل يمكنني تغيير تسميات المحاور؟**  
A: Yes. Use `chart.getCategoryAxis().setTitle("Regions")` and `chart.getValueAxis().setTitle("Sales")`.

**Q: ما الصيغ التي يمكنني التصدير إليها بخلاف XLS؟**  
A: Use `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, or `workbook.save("chart.xlsx")` for PDF, PNG, and XLSX respectively.

**Q: هل الترخيص مطلوب لبنات التطوير؟**  
A: A free trial works for evaluation, but a permanent or temporary license is needed for production deployments.

**Q: كيف يمكنني تحسين سرعة العرض لآلاف الصفوف؟**  
A: Populate cells using `cells.importArray()` and minimize chart redraws by creating the chart after all data is loaded.

**آخر تحديث:** 2026-04-08  
**تم الاختبار باستخدام:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

## الموارد

- [توثيق Aspose.Cells](https://reference.aspose.com/cells/java/)
- [تحميل Aspose.Cells](https://releases.aspose.com/cells/java/)
- [شراء ترخيص](https://purchase.aspose.com/buy)
- [نسخة تجريبية](https://releases.aspose.com/cells/java/)
- [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)
- [منتدى الدعم](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}