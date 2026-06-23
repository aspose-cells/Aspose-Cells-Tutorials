---
date: '2026-04-08'
description: تعلم كيفية إنشاء مخطط خطي مع علامات باستخدام Aspose.Cells للغة Java،
  وإضافة المخطط إلى ورقة العمل، وتخصيص مخططات Excel للتقارير الآلية.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: إنشاء مخطط خطي مع علامات باستخدام Aspose.Cells للـ Java
url: /ar/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء وتنسيق مخططات Excel باستخدام Aspose.Cells Java

## مقدمة

في عالم اليوم القائم على البيانات، يُعد **مخطط خطي مع علامات** أحد أكثر الطرق فعالية لتصوير الاتجاهات والقيم الشاذة. سواءً كنت تبني تقارير آلية أو لوحة معلومات تُحدَّث يوميًا، فإن القدرة على إضافة مخطط خطي مع علامات إلى ورقة عمل برمجيًا توفر عددًا لا يُحصى من الخطوات اليدوية. يوضح هذا الدرس كيفية استخدام Aspose.Cells لـ Java لإنشاء، وتنسيق، وتصدير مثل هذه المخططات، بحيث يمكنك التركيز على الرؤى بدلاً من التلاعب الممل بملفات Excel.

**ما ستتعلمه**
- تهيئة دفتر عمل وتعبئته بالبيانات باستخدام Aspose.Cells.  
- **كيفية إضافة مخطط خطي مع علامات إلى ورقة عمل** وتكوين مظهره.  
- تخصيص ألوان السلاسل، والعلامات، وخيارات التنسيق الأخرى.  
- حفظ دفتر العمل كملف Excel يتضمن المخطط المنسق.

## إجابات سريعة
- **ما هو الصنف الأساسي للبدء؟** `Workbook` يهيئ ملف Excel جديد.  
- **أي نوع مخطط يُنشئ مخططًا خطيًا مع علامات؟** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **كيف يمكنني تعيين ألوان مخصصة لنقاط السلسلة؟** استخدم `chart.getNSeries().setColorVaried(true)` وحدد ألوان منطقة العلامة.  
- **هل أحتاج إلى ترخيص للوظائف الكاملة؟** نعم، الترخيص المدفوع أو المؤقت لـ Aspose.Cells يزيل حدود التقييم.  
- **هل يمكنني تصدير النتيجة كملف XLSX؟** بالتأكيد—`workbook.save("StyledChart.xlsx")` ينشئ ملف XLSX.

## المتطلبات المسبقة

قبل إنشاء وتنسيق المخططات باستخدام Aspose.Cells لـ Java، تأكد من إعداد ما يلي:

### المكتبات المطلوبة
قم بإضافة Aspose.Cells كاعتماد في مشروعك. إليك التعليمات لمستخدمي Maven وGradle:

**Maven:**
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

### متطلبات إعداد البيئة
- مجموعة تطوير جافا (JDK) مثبتة على نظامك.  
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse للبرمجة والاختبار.

### المتطلبات المعرفية
يتطلب الأمر فهمًا أساسيًا لبرمجة Java، بالإضافة إلى الإلمام بدفاتر عمل Excel ومفاهيم المخططات.

### الحصول على الترخيص
Aspose.Cells هو منتج تجاري يتطلب ترخيصًا للوظائف الكاملة. يمكنك الحصول على نسخة تجريبية مجانية لتقييم ميزاته، أو طلب ترخيص مؤقت للاختبار الموسع، أو شراء المنتج للاستخدام طويل الأمد.

- **نسخة تجريبية مجانية:** [تحميل نسخة تجريبية مجانية](https://releases.aspose.com/cells/java/)  
- **ترخيص مؤقت:** [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)  
- **شراء:** [شراء Aspose.Cells](https://purchase.aspose.com/buy)

## إعداد Aspose.Cells لـ Java

بعد تثبيت الاعتمادات اللازمة، قم بإعداد بيئة التطوير لاستخدام Aspose.Cells. ابدأ باستيراد المكتبة وتهيئة كائن `Workbook` في تطبيق Java الخاص بك:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## دليل التنفيذ

في هذا القسم، سنقسم التنفيذ إلى ميزات متميزة: تهيئة دفتر العمل وتعبئة البيانات، إنشاء المخطط وتكوينه، تخصيص السلاسل، وحفظ دفتر العمل.

### الميزة 1: تهيئة دفتر العمل وتعبئة البيانات

**نظرة عامة:** تركز هذه الميزة على إنشاء دفتر عمل جديد، الوصول إلى ورقته الأولى، وتعبئته بالبيانات اللازمة لإنشاء المخطط.

#### الخطوة 1: تهيئة دفتر العمل
ابدأ بإنشاء كائن `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### الخطوة 2: تعيين عناوين الأعمدة وتعبئة البيانات
حدد رؤوس الأعمدة واملأ الصفوف ببيانات نموذجية:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### الميزة 2: إنشاء المخطط وتكوينه

**نظرة عامة:** توضح هذه الميزة كيفية إضافة مخطط إلى ورقة العمل، تعيين نمطه، وتكوين الخصائص الأساسية.

#### الخطوة 3: إضافة مخطط إلى ورقة العمل
أضف مخططًا خطيًا مع علامات البيانات:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### الميزة 3: تكوين السلسلة وتخصيصها

**نظرة عامة:** عزّز المظهر البصري لمخططاتك عبر تخصيص إعدادات السلسلة، مثل الألوان المتنوعة وأنماط العلامات.

#### الخطوة 4: تخصيص إعدادات السلسلة
قم بتكوين بيانات السلسلة، تطبيق تنسيق مخصص، وتعديل العلامات:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### الميزة 4: حفظ دفتر العمل

**نظرة عامة:** أخيرًا، احفظ دفتر العمل لتثبيت تغييراتك وضمان تضمين المخطط في ملف Excel.

#### الخطوة 5: حفظ دفتر العمل
احفظ دفتر العمل مع المخططات التي تم إنشاؤها حديثًا:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### المشكلات الشائعة واستكشاف الأخطاء

- **المخطط يظهر فارغًا:** تحقق من أن نطاقات الخلايا المستخدمة في `setXValues` و `setValues` تشير إلى خلايا مملوءة بشكل صحيح.  
- **الألوان لم تُطبق:** تأكد من استدعاء `chart.getNSeries().setColorVaried(true)` قبل تخصيص السلاسل الفردية.  
- **أخطاء الترخيص:** قد يحد الترخيص التجريبي عدد المخططات؛ قم بتثبيت ترخيص كامل لإزالة القيود.

## الأسئلة المتكررة

**س: هل يمكنني إنشاء أنواع مخططات أخرى (مثل الأعمدة، الدوائر) باستخدام Aspose.Cells؟**  
ج: نعم، يدعم Aspose.Cells مجموعة واسعة من أنواع المخططات؛ ما عليك سوى استبدال `ChartType.LINE_WITH_DATA_MARKERS` بالقيمة المطلوبة من التعداد.

**س: هل أحتاج إلى إغلاق دفتر العمل أو تحرير الموارد؟**  
ج: يدير صنف `Workbook` الموارد تلقائيًا، لكن يمكنك استدعاء `workbook.dispose()` في التطبيقات طويلة التشغيل لتحرير الذاكرة.

**س: هل يمكن إضافة مخططات متعددة إلى نفس ورقة العمل؟**  
ج: بالتأكيد—استدعِ `worksheet.getCharts().add(...)` لكل مخطط تريد إدراجه.

**س: كيف يمكنني تصدير الملف كتنسيق Excel أقدم (XLS)؟**  
ج: استخدم `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**س: هل سيحتفظ المخطط بتنسيقه عند فتحه في Microsoft Excel؟**  
ج: نعم، يكتب Aspose.Cells كائنات مخطط Excel أصلية، لذا تظهر جميع الأنماط والألوان والعلامات كما تم تعريفها.

---

**آخر تحديث:** 2026-04-08  
**تم الاختبار مع:** Aspose.Cells 25.3 لـ Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}