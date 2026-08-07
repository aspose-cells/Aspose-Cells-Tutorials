---
date: '2026-04-11'
description: تعلم أتمتة Excel باستخدام Java مع Aspose.Cells. يوضح هذا البرنامج التعليمي
  كيفية إنشاء دفتر عمل Excel باستخدام Java، وتعبئة بيانات Excel باستخدام Java، وحفظ
  ملف Excel باستخدام Java مع المخططات.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'أتمتة إكسل جافا: إنشاء دفاتر عمل ومخططات باستخدام Aspose'
url: /ar/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# أتمتة Excel باستخدام Java: إنشاء دفاتر عمل ومخططات باستخدام Aspose

## مقدمة

يمكن لأتمتة مهام Excel باستخدام Java أن توفر ساعات من العمل اليدوي، خاصة عندما تحتاج إلى إنشاء تقارير أو لوحات معلومات أو مخططات مدفوعة بالبيانات بشكل فوري. **Excel automation java** مع Aspose.Cells يمنحك واجهة برمجة تطبيقات نظيفة وعالية الأداء تتعامل مع كل شيء من إنشاء دفتر العمل إلى تنسيق المخططات المتقدم. في هذا الدرس ستتعلم كيفية إعداد Aspose.Cells، **create an Excel workbook java**، ملء البيانات، إضافة مخطط، تطبيق تنسيق ثلاثي الأبعاد، وأخيرًا **save the Excel file java**.

### إجابات سريعة
- **أي مكتبة تبسط أتمتة Excel في Java؟** Aspose.Cells for Java.  
- **هل يمكنني إضافة مخططات ثلاثية الأبعاد برمجياً؟** نعم – الواجهة تدعم تنسيق ثلاثي الأبعاد وتأثيرات الإضاءة.  
- **هل أحتاج إلى ترخيص للتطوير؟** ترخيص تجريبي مجاني متاح؛ الترخيص التجاري مطلوب للإنتاج.  
- **ما أدوات بناء Java المدعومة؟** Maven و Gradle مدعومان بالكامل.  
- **ما صيغ الملفات التي يمكنني تصديرها؟** XLS، XLSX، CSV، PDF والعديد غيرها.

## ما هي أتمتة Excel باستخدام Java؟

تشير أتمتة Excel باستخدام Java إلى عملية إنشاء وتعديل وحفظ دفاتر عمل Excel برمجياً باستخدام كود Java. إنها تلغي تحرير الجداول يدويًا، تضمن الاتساق، وتمكن من التكامل مع أنظمة أخرى مثل قواعد البيانات أو خدمات الويب.

## لماذا تستخدم Aspose.Cells لـ Java؟

- **مجموعة ميزات غنية** – من قيم الخلايا البسيطة إلى المخططات المعقدة، وجداول المحور، والتنسيق الشرطي.  
- **بدون اعتماد على Microsoft Office** – يعمل على أي بيئة خادم.  
- **أداء عالي** – مُحسّن لمجموعات البيانات الكبيرة والسيناريوهات متعددة الخيوط.  
- **دعم صيغ واسع** – قراءة/كتابة XLS، XLSX، ODS، CSV، PDF، HTML، وأكثر.

## المتطلبات المسبقة

- **Java Development Kit (JDK) 8+**  
- **Maven أو Gradle** لإدارة الاعتمادات  
- **Aspose.Cells لـ Java 25.3 أو أحدث** (تجريبي أو مرخص)  

## إعداد Aspose.Cells لـ Java

أضف المكتبة إلى مشروعك باستخدام أحد التكوينات التالية.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### الحصول على الترخيص

اطلب ترخيصًا تجريبيًا مجانيًا من موقع Aspose، أو اشترِ ترخيصًا كاملًا للاستخدام في الإنتاج. ضع ملف الترخيص في مشروعك وحمّله أثناء وقت التشغيل.

## التهيئة الأساسية والإعداد

بمجرد حل الاعتماد، يمكنك بدء كتابة الكود.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## دليل خطوة بخطوة

### الخطوة 1: كيفية إنشاء دفتر عمل excel باستخدام Java

أنشئ نسخة جديدة من دفتر العمل الذي سيحتوي على جميع أوراق العمل.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### الخطوة 2: إضافة أوراق العمل (بما في ذلك ورقة مخطط)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### الخطوة 3: كيفية ملء بيانات excel باستخدام Java

أدخل بيانات عينة سيشير إليها المخطط.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### الخطوة 4: إضافة مخطط عمودي إلى دفتر العمل

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### الخطوة 5: تطبيق تنسيق اللون على منطقة المخطط

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### الخطوة 6: تكوين الأسطورة وسلسلة البيانات

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### الخطوة 7: تطبيق تنسيق ثلاثي الأبعاد على السلسلة

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### الخطوة 8: تعيين ألوان السلسلة لتمييز بصري أفضل

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### الخطوة 9: كيفية حفظ ملف excel باستخدام Java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## تطبيقات عملية

- **التقارير المالية** – إنشاء بيانات ربع سنوية مع مخططات ديناميكية.  
- **لوحات معلومات تحليل البيانات** – بناء لوحات تفاعلية تتجدد تلقائيًا.  
- **إدارة المخزون** – تصدير مستويات المخزون والاتجاهات إلى Excel لمراجعة أصحاب المصلحة.  
- **تخطيط المشاريع** – إنشاء مخططات على نمط Gantt مباشرةً من أنظمة الجدولة المبنية على Java.

## نصائح الأداء لأتمتة Excel باستخدام Java

- **إعادة استخدام كائنات دفتر العمل** عند معالجة عدة أوراق لتقليل استهلاك الذاكرة.  
- **تحديث الخلايا على دفعات** باستخدام `Cells.importArray` لمجموعات بيانات كبيرة بدلاً من استدعاءات `putValue` الفردية.  
- **تحرير الموارد** عن طريق استدعاء `book.dispose()` بعد حفظ الملفات الكبيرة.

## الأسئلة المتكررة

**س: هل يمكنني إنشاء XLSX بدلاً من XLS؟**  
ج: نعم – فقط غيّر امتداد الملف في `book.save("output.xlsx")`؛ Aspose يختار الصيغة الصحيحة تلقائيًا.

**س: هل يلزم وجود ترخيص للتطوير؟**  
ج: ترخيص تجريبي مجاني يعمل للتطوير والاختبار. النشر في الإنتاج يتطلب ترخيصًا مُشتراً.

**س: كيف يمكنني إضافة أنواع مخططات أخرى؟**  
ج: استخدم تعداد `ChartType` (مثل `ChartType.PIE`، `ChartType.LINE`) عند استدعاء `charts.add(...)`.

**س: ماذا لو احتجت لحماية دفتر العمل؟**  
ج: استدعِ `book.getSettings().setPassword("yourPassword")` قبل الحفظ.

**س: هل يدعم Aspose.Cells الملفات الممكّنّة للماكرو؟**  
ج: نعم – يمكنك إنشاء أو الحفاظ على ماكرو VBA في دفاتر عمل XLSM.

---

**آخر تحديث:** 2026-04-11  
**تم الاختبار مع:** Aspose.Cells 25.3 (Java)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}