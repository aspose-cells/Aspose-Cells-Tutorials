---
"date": "2025-04-07"
"description": "تعلّم كيفية تحسين ملفات Excel الخاصة بك من خلال إنشاء مخططات تفاعلية مع مربعات اختيار باستخدام Aspose.Cells لجافا. اتبع هذا الدليل خطوة بخطوة لتحسين عرض البيانات."
"title": "إنشاء مخططات تفاعلية في Excel باستخدام مربعات الاختيار باستخدام Aspose.Cells لـ Java"
"url": "/ar/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إنشاء مخططات تفاعلية في Excel باستخدام مربعات الاختيار باستخدام Aspose.Cells لـ Java

## مقدمة

يمكن تحسين عرض البيانات وتفاعليتها في Excel من خلال دمج عناصر ديناميكية، مثل مربعات الاختيار، في المخططات البيانية. سيرشدك هذا البرنامج التعليمي إلى كيفية إنشاء مخططات بيانية تفاعلية باستخدام Aspose.Cells لـ Java، وهو مثالي لإضافة وظائف إلى ملفات Excel.

**ما سوف تتعلمه:**
- كيفية إعداد Aspose.Cells واستخدامه في Java
- خطوات إنشاء مصنف Excel وإدراج المخططات البيانية
- طرق إضافة مربعات الاختيار داخل منطقة الرسم البياني الخاص بك
- تقنيات لحفظ تعديلاتك في ملف Excel

قبل أن نبدأ، تأكد من أن لديك الأدوات والمعرفة اللازمة.

## المتطلبات الأساسية

لمتابعة هذا البرنامج التعليمي، تأكد من أن لديك:
- **مجموعة تطوير Java (JDK):** تم تثبيت الإصدار 8 أو أعلى على جهازك.
- **Aspose.Cells لـ Java:** أحدث إصدار من مكتبة Aspose.Cells. في هذا الدليل، سنستخدم الإصدار 25.3.
- **Maven أو Gradle:** قم بإعداد بيئة التطوير الخاصة بك لإدارة التبعيات.

### متطلبات المعرفة

على الرغم من أن الفهم الأساسي لبرمجة Java والتعرف على هياكل ملفات Excel سيكون مفيدًا، إلا أن هذا الدليل يغطي جميع التفاصيل الضرورية للمبتدئين.

## إعداد Aspose.Cells لـ Java

دمج Aspose.Cells في مشروعك سهل للغاية. لنبدأ بإعداد المكتبة باستخدام Maven أو Gradle.

### استخدام Maven

أضف التبعية التالية إلى ملفك `pom.xml` ملف:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### استخدام Gradle

قم بتضمين هذا السطر في `build.gradle` ملف:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### خطوات الحصول على الترخيص

لاستكشاف كامل إمكانيات Aspose.Cells، فكّر في الحصول على ترخيص مؤقت أو دائم. يمكنك البدء بفترة تجريبية مجانية بتنزيلها من [موقع Aspose](https://releases.aspose.com/cells/java/)للاستخدام الإنتاجي، قد ترغب في شراء ترخيص أو طلب ترخيص مؤقت لأغراض التقييم.

#### التهيئة الأساسية

بمجرد إضافة Aspose.Cells إلى مشروعك، قم بتهيئته في تطبيق Java الخاص بك على النحو التالي:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // تهيئة كائن المصنف.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## دليل التنفيذ

بعد إعداد البيئة الخاصة بك، دعنا نقوم بإنشاء مخطط يحتوي على مربع اختيار في Excel.

### إنشاء مصنف وإضافة مخطط

#### ملخص

يشرح هذا القسم كيفية إنشاء مصنف Excel وإضافة مخطط عمودي باستخدام Aspose.Cells لـ Java. تساعد المخططات البيانية على عرض البيانات بفعالية، مما يجعلها أساسية للتقارير ولوحات المعلومات.

##### الخطوة 1: إنشاء مصنف جديد

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // إنشاء كائن مصنف جديد يمثل ملف Excel.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### الخطوة 2: إضافة ورقة عمل للمخطط

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // إضافة ورقة عمل الرسم البياني إلى المصنف.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### الخطوة 3: إدراج مخطط عمودي

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // أضف مخططًا عائمًا من نوع COLUMN إلى ورقة عمل المخطط المضافة حديثًا.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### الخطوة 4: إضافة بيانات السلسلة

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // أضف مخططًا عائمًا من نوع COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // إضافة بيانات السلسلة إلى الرسم البياني.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

### إضافة مربع الاختيار إلى الرسم البياني

#### ملخص

يتيح لك تضمين مربع اختيار في مخطط Excel التبديل الديناميكي بين خيارات الرؤية والميزات الأخرى. يرشدك هذا القسم إلى كيفية تضمين مربع اختيار في المخطط.

##### الخطوة 1: تضمين شكل مربع الاختيار

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // أضف شكل مربع الاختيار داخل منطقة الرسم البياني على الرسم البياني الأول في ورقة العمل.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

##### الخطوة 2: تعيين نص مربع الاختيار

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // أضف شكل مربع الاختيار داخل الرسم البياني.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // تعيين النص لشكل مربع الاختيار المضاف حديثًا.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

### حفظ المصنف كملف Excel

#### ملخص

بمجرد تكوين الرسم البياني ومربعات الاختيار، احفظ المصنف للاحتفاظ بالتغييرات الخاصة بك.

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // أضف شكل مربع الاختيار وقم بتسميته.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // حفظ المصنف
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // استبدله بمسار دليل الإخراج الفعلي لديك.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## التطبيقات العملية

فيما يلي بعض السيناريوهات الواقعية التي يمكنك من خلالها تطبيق المعرفة المكتسبة من هذا البرنامج التعليمي:
1. **التقارير التفاعلية:** استخدم مربعات الاختيار لتبديل رؤية سلسلة البيانات في التقارير، مما يعزز تفاعل المستخدم والتخصيص.
2. **تحليل البيانات:** يمكنك تمكين أو تعطيل مجموعات بيانات معينة في المخططات للتحليل المقارن، مما يجعل من الأسهل التركيز على جوانب محددة من بياناتك.
3. **الأدوات التعليمية:** إنشاء مواد تعليمية ديناميكية حيث يمكن للطلاب التفاعل مع المحتوى عن طريق تحديد خيارات مختلفة في المخططات البيانية.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}