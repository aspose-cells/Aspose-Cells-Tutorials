---
date: '2026-04-11'
description: تعلم كيفية عرض إصدار Aspose Cells، وتحميل دفتر عمل Excel في Java، ومعالجة
  تعداد المخططات باستخدام Aspose.Cells. اتبع أمثلة خطوة بخطوة.
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: إظهار نسخة Aspose Cells ومعالجة تعداد المخطط في Java
url: /ar/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# عرض إصدار Aspose Cells ومعالجة تعداد المخطط في Java

## مقدمة

إذا كنت بحاجة إلى **عرض إصدار Aspose Cells**، وتحميل مصنف Excel في Java، والعمل مع تعداد المخطط، فأنت في المكان الصحيح. في هذا الدرس سنستعرض الخطوات الدقيقة التي تحتاجها لدمج Aspose.Cells for Java في مشاريعك، واستخراج بيانات المخطط، وتحويل التعدادات القائمة على الأعداد الصحيحة إلى سلاسل قابلة للقراءة. في النهاية ستحصل على حل قوي وجاهز للإنتاج يمكنك إدراجه مباشرةً في قاعدة الشيفرة الخاصة بك.

**ما ستتعلمه**
- كيفية عرض إصدار Aspose.Cells.
- كيفية **تحميل مصنف Excel في Java** والوصول إلى بيانات المخطط.
- كيفية تحويل قيم التعداد الصحيحة إلى ما يعادلها من سلاسل.
- كيفية استرجاع أنواع قيم X و Y من نقطة المخطط.

هيا نبدأ!

## إجابات سريعة
- **كيف يمكنني التحقق من إصدار Aspose.Cells؟** استدعِ `CellsHelper.getVersion()` واطبع النتيجة.  
- **ما هو إحداثي Maven الذي يضيف Aspose.Cells؟** `com.aspose:aspose-cells:25.3`.  
- **هل يمكنني تحميل مصنف Excel في Java؟** نعم—استخدم `new Workbook(filePath)`.  
- **كيف يتم تحويل قيم التعداد؟** احفظها في `HashMap<Integer, String>` وابحث عن المفتاح الصحيح.  
- **ما الطريقة التي تطبع أنواع قيم X/Y؟** `pnt.getXValueType()` و `pnt.getYValueType()`.

## ما هو “عرض إصدار Aspose Cells”؟
تشير العبارة إلى استرجاع سلسلة إصدار وقت تشغيل المكتبة. معرفة الإصدار الدقيق يساعد في تصحيح الأخطاء، وضمان التوافق، وتأكيد أن الترخيص الخاص بك مطبق على الإصدار المقصود.

## لماذا عرض الإصدار وتحميل مصنف Excel في Java؟
- **التصحيح** – يؤكد أن المكتبة الصحيحة موجودة في مسار الفئات.  
- **الامتثال** – يسهل التحقق من أنك تستخدم نسخة مرخصة.  
- **الأتمتة** – تمكّن السكريبتات من التكيف مع إصدارات المكتبة المختلفة دون تغييرات يدوية.  

## المتطلبات المسبقة

### المكتبات والاعتمادات المطلوبة
- **Aspose.Cells for Java** – المكتبة الأساسية لمعالجة Excel.  
- **Java Development Kit (JDK)** – الإصدار 8 أو أحدث.

### إعداد البيئة
- بيئة التطوير المتكاملة التي تختارها (IntelliJ IDEA، Eclipse، NetBeans).  
- أداة البناء: Maven **أو** Gradle (التعليمات أدناه).

### المعرفة المطلوبة
- برمجة Java الأساسية.  
- الإلمام بمفاهيم Excel (الأوراق، المخططات) مفيد لكنه غير مطلوب.

## إعداد Aspose.Cells for Java

### استخدام Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### استخدام Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### خطوات الحصول على الترخيص
- **نسخة تجريبية مجانية**: حمّل من [Aspose's Release Page](https://releases.aspose.com/cells/java/).  
- **ترخيص مؤقت**: احصل على ترخيص قصير الأمد من [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/).  
- **شراء**: للمشاريع طويلة الأمد، اشترِ ترخيصًا عبر [Aspose Purchase Page](https://purchase.aspose.com/buy).

### التهيئة الأساسية والإعداد
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## دليل التنفيذ

### كيفية عرض إصدار Aspose Cells
**نظرة عامة** – تحقق بسرعة من إصدار المكتبة أثناء التشغيل.

#### الخطوة 1: استيراد الحزم المطلوبة
```java
import com.aspose.cells.*;
```

#### الخطوة 2: إنشاء فئة وطريقة Main
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### شرح
- `CellsHelper.getVersion()` تُعيد سلسلة الإصدار الدقيقة لملف Aspose.Cells DLL الذي يستخدمه تطبيقك.

### كيفية تحويل التعدادات الصحيحة إلى تعداد نصي
**نظرة عامة** – تحويل قيم التعداد الرقمية (مثل `CellValueType.IS_NUMERIC`) إلى نص قابل للقراءة.

#### الخطوة 1: إعداد HashMap للتحويل
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### الخطوة 2: تحويل وطباعة قيمة التعداد
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### شرح
- خريطة `cvTypes` تجسر الفجوة بين الثابت الرقمي والملصق القابل للقراءة من قبل الإنسان.

### كيفية تحميل مصنف Excel في Java والوصول إلى بيانات المخطط
**نظرة عامة** – فتح مصنف موجود، تحديد مخطط، وضمان أن بياناته محدثة.

#### الخطوة 1: استيراد الحزم الضرورية
```java
import com.aspose.cells.*;
```

#### الخطوة 2: تحميل المصنف والوصول إلى ورقة العمل
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### شرح
- `new Workbook(filePath)` يحمل الملف في الذاكرة.  
- `ch.calculate()` يجبر المخطط على إعادة حساب أي صيغ بحيث تكون البيانات التي تقرأها محدثة.

### كيفية استرجاع وطباعة أنواع قيم X و Y لنقطة المخطط
**نظرة عامة** – استخراج نوع البيانات لقيم X و Y لنقطة معينة في المخطط.

#### الخطوة 1: إعداد HashMap لتحويل التعداد (إعادة استخدام من السابق)
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### الخطوة 2: الوصول إلى نقطة المخطط وطباعة أنواع القيم
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### شرح
- `pnt.getXValueType()` / `pnt.getYValueType()` تُعيد ثوابت عددية تشير إلى ما إذا كانت القيمة رقمية، نصية، تاريخية، إلخ.  
- خريطة `cvTypes` تُحوّل تلك الأعداد إلى نص قابل للقراءة.

## التطبيقات العملية
1. **التقارير المالية** – إنشاء مخططات تلقائيًا بأنواع بيانات مُتحقّق منها لسجلات التدقيق.  
2. **لوحات تصور البيانات** – سحب نقاط المخطط إلى مكونات واجهة مستخدم مخصصة.  
3. **الاختبار الآلي** – التحقق من أن سلاسل المخطط تحتوي على أنواع البيانات المتوقعة.  
4. **ذكاء الأعمال** – تغذية بيانات تعريف المخطط إلى خطوط التحليل اللاحقة.  
5. **أدوات التقارير المخصصة** – بناء محركات تقارير مخصصة تحتاج إلى معالجة دقيقة للتعدادات.

## اعتبارات الأداء
- **تحميل الأوراق المطلوبة فقط** – استخدم `Workbook.getWorksheets().get(index)` بدلاً من تحميل كل ورقة عند التعامل مع ملفات كبيرة.  
- **تحرير الكائنات بسرعة** – عيّن مراجع المصنف إلى `null` بعد المعالجة للمساعدة في جمع القمامة.  
- **معالجة الملفات على دفعات** – عند التعامل مع العديد من المصنفات، عالجها على دفعات للحفاظ على استهلاك الذاكرة متوقعًا.

## المشكلات الشائعة والحلول
- **الترخيص غير موجود** – تأكد من صحة مسار ملف الترخيص وأن الملف مضمن في مخرجات البناء.  
- **المخطط غير محسوب** – استدعِ دائمًا `chart.calculate()` قبل قراءة قيم النقاط.  
- **خريطة تعداد غير صحيحة** – تحقق من أنك أضفت جميع ثوابت `CellValueType` ذات الصلة إلى `HashMap`.

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا الكود مع Aspose.Cells 24.x؟**  
ج: نعم، واجهة برمجة التطبيقات لاسترجاع الإصدار، تحميل المصنف، والوصول إلى نقاط المخطط ظلت مستقرة عبر الإصدارات الأخيرة.

**س: ماذا لو كان المخطط يحتوي على قيم تاريخية؟**  
ج: أضف `CellValueType.IS_DATE_TIME` إلى خريطة `cvTypes` واربطه بـ "IsDateTime".

**س: هل أحتاج إلى ترخيص للاستخدام التجريبي؟**  
ج: الترخيص التجريبي مطلوب للوظائف الكاملة؛ بدون ذلك سترى علامات مائية على الملفات المُولدة.

**س: كيف أتعامل مع أوراق عمل متعددة؟**  
ج: قم بالتكرار عبر `wb.getWorksheets()` وعالج كل كائن `Chart` تصادفه.

**س: هل هناك طريقة لتصدير بيانات المخطط إلى CSV؟**  
ج: نعم—استخرج قيم السلسلة عبر `chart.getNSeries().get(i).getValues()` واكتبها باستخدام إدخال/إخراج Java القياسي.

---

**آخر تحديث:** 2026-04-11  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}