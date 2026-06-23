---
date: '2026-03-31'
description: تعلم كيفية تغيير حجم التسميات في مخططات Excel باستخدام Aspose.Cells للغة
  Java، وتعديل تسميات المخطط تلقائيًا لتناسب مثالي وقابلية قراءة عالية.
keywords:
- auto-resize chart data labels
- Aspose.Cells for Java
- Excel charts customization
title: كيفية تغيير حجم التسميات في مخططات Excel باستخدام Aspose.Cells للـ Java
url: /ar/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير حجم التسميات في مخططات Excel باستخدام Aspose.Cells للـ Java

## المقدمة

إذا كنت تبحث **كيفية تغيير حجم التسميات** في مخططات Excel، فقد وصلت إلى المكان الصحيح. يشرح هذا البرنامج التعليمي كيفية استخدام Aspose.Cells للـ Java لتغيير حجم أشكال تسميات بيانات المخطط تلقائيًا، مما يضمن أن التسميات تتناسب تمامًا داخل حاوياتها. في نهاية هذا الدليل، ستتمكن من تعديل تسميات مخططات Excel بسرعة، تحسين قابلية القراءة، وإنتاج تقارير مصقولة دون تعديل يدوي.

**ما ستتعلمه**
- كيفية إعداد Aspose.Cells للـ Java في مشروعك.
- الخطوات الدقيقة لـ **تغيير حجم تسميات مخطط Excel** تلقائيًا.
- سيناريوهات واقعية حيث يوفر تغيير الحجم التلقائي الوقت.
- نصائح الأداء للدفاتر الكبيرة أو المخططات المعقدة.

## إجابات سريعة

- **ما معنى “how to resize labels”؟** يشير إلى تعديل شكل تسميات بيانات المخطط تلقائيًا بحيث يتناسب النص دون قص.  
- **أي مكتبة تتعامل مع هذا؟** Aspose.Cells للـ Java توفر الخاصية `setResizeShapeToFitText`.  
- **هل أحتاج إلى ترخيص؟** الإصدار التجريبي يعمل للاختبار؛ الترخيص الكامل مطلوب للإنتاج.  
- **هل سيعمل على جميع أنواع المخططات؟** نعم—الأعمدة، الأشرطة، الفطائر، الخطوط، وأكثر مدعومة.  
- **هل هناك تأثير على الأداء؟** قليل؛ فقط استدعِ `chart.calculate()` بعد التغييرات.

## ما هو تغيير حجم تسميات بيانات المخطط تلقائيًا؟

تغيير حجم تسميات بيانات المخطط تلقائيًا هو ميزة تقوم بتوسيع أو تقليص صندوق حدود التسمية ديناميكيًا ليتطابق مع طول النص الذي يحتويه. هذا يلغي المشكلة الشائعة للتسميات المقطوعة أو المتداخلة، خاصةً عند التعامل مع صيغ رقمية متغيرة أو أسماء فئات طويلة.

## لماذا تعديل تسميات مخططات Excel؟

- **قابلية القراءة:** يمنع قطع الأرقام ويضمن رؤية كل نقطة بيانات.  
- **المظهر الاحترافي:** يجعل لوحات التحكم والتقارير تبدو مصقولة دون تعديلات يدوية.  
- **توفير الوقت:** ي automatis عملية تنسيق متكررة، مفيد خاصةً في التقارير المولدة دفعة واحدة.

## المتطلبات المسبقة

- مجموعة تطوير جافا (JDK) 8 أو أعلى.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse أو VS Code.  
- معرفة أساسية بجافا وإلمام بمعالجة ملفات Excel.  

## إعداد Aspose.Cells للـ Java

### معلومات التثبيت

أضف Aspose.Cells إلى مشروعك عبر Maven أو Gradle.

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

Aspose offers a free trial to test the capabilities of its libraries:
1. **Free Trial**: قم بتنزيل ترخيص مؤقت من [this link](https://releases.aspose.com/cells/java/) لمدة 30 يومًا.  
2. **Temporary License**: اطلب وصولًا أطول عبر [purchase page](https://purchase.aspose.com/temporary-license/).  
3. **Purchase**: للاستخدام المستمر، فكر في شراء ترخيص كامل من [Aspose purchase page](https://purchase.aspose.com/buy).

### التهيئة والإعداد الأساسي

Once Aspose.Cells is added to your project, initialize it in your Java application:

```java
import com.aspose.cells.Workbook;

public class InitializeAspose {
    public static void main(String[] args) throws Exception {
        // Create a new Workbook instance or open an existing one
        Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
        
        // Save the modified Excel file
        workbook.save("output/path/output_file.xlsx");
    }
}
```

## دليل التنفيذ

### تغيير حجم تسميات بيانات المخطط تلقائيًا

فيما يلي الكود خطوة بخطوة الذي تحتاجه لت **تغيير حجم تسميات مخطط Excel** تلقائيًا.

#### 1️⃣ تحميل دفتر العمل

```java
import com.aspose.cells.Workbook;
import AsposeCellsExamples.Utils;

public class ResizeChartDataLabelShapeToFitText {
    public static void main(String[] args) throws Exception {
        // Define the directory of your document
        String dataDir = Utils.getSharedDataDir(ResizeChartDataLabelShapeToFitText.class) + "TechnicalArticles/";
        
        // Load an existing workbook containing charts
        Workbook book = new Workbook(dataDir + "report.xlsx");
    }
}
```

#### 2️⃣ الوصول إلى المخططات وتسميات البيانات

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartCollection;

public class ResizeChartDataLabelShapeToFitText {
    public static void main(String[] args) throws Exception {
        // (Load workbook code here...)
        
        // Access the first worksheet in the workbook
        Worksheet sheet = book.getWorksheets().get(0);
        
        // Get all charts from the worksheet
        ChartCollection charts = sheet.getCharts();

        for (int chartIndex = 0; chartIndex < charts.getCount(); chartIndex++) {
            com.aspose.cells.Chart chart = charts.get(chartIndex);
            
            // Process each series in the chart
            for (int seriesIndex = 0; seriesIndex < chart.getNSeries().getCount(); seriesIndex++) {
                DataLabels labels = chart.getNSeries().get(seriesIndex).getDataLabels();
                
                // Enable auto‑resizing of data label shape to fit text
                labels.setResizeShapeToFitText(true);
            }
            
            // Recalculate the chart after changes
            chart.calculate();
        }
    }
}
```

#### 3️⃣ حفظ دفتر العمل المعدل

```java
public class ResizeChartDataLabelShapeToFitText {
    public static void main(String[] args) throws Exception {
        // (Previous code...)
        
        // Save the workbook to a new file
        book.save(dataDir + "RCDLabelShapeToFitText_out.xlsx");
    }
}
```

### نصائح استكشاف الأخطاء وإصلاحها

- **المخطط لا يتم تحديثه:** تحقق من أنك استدعيت `chart.calculate()` بعد تعديل خصائص التسمية.  
- **قيود الترخيص:** إذا واجهت قيودًا على الميزات، تحقق مرة أخرى من تحميل ملف الترخيص بشكل صحيح أو انتقل إلى ترخيص مؤقت للوصول الكامل.

## التطبيقات العملية

فيما يلي سيناريوهات شائعة حيث يصبح **كيفية تغيير حجم التسميات** أمرًا أساسيًا:

1. **التقارير المالية** – قيمة العملات والنسب المئوية تختلف في الطول؛ يضمن تغيير الحجم التلقائي نظافة التخطيط.  
2. **لوحات مبيعات** – يمكن أن تكون أسماء المنتجات طويلة؛ تضمن الميزة بقاء كل تسمية قابلة للقراءة.  
3. **البحوث الأكاديمية** – غالبًا ما تنتج مجموعات البيانات المعقدة تسميات بأطوال غير متساوية؛ التعديل التلقائي يوفر ساعات من التنسيق اليدوي.

## اعتبارات الأداء

عند العمل مع دفاتر عمل كبيرة:

- **إدارة الذاكرة:** تخلص من الكائنات (`workbook.dispose()`) عندما لا تحتاجها.  
- **المعالجة الدفعية:** قم بالتكرار على المخططات في مجموعات أصغر لتجنب استهلاك الذاكرة الزائد.  
- **ابق محدثًا:** استخدم أحدث نسخة من Aspose.Cells لتحسينات الأداء وإصلاح الأخطاء.

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|-------|----------|
| التسميات تبقى بنفس الحجم | `setResizeShapeToFitText` لم يتم استدعاؤه | تأكد من ضبط الخاصية على `true` لكل سلسلة. |
| المخطط يظهر فارغًا بعد الحفظ | الترخيص غير مفعّل | حمّل ترخيصًا صالحًا قبل فتح دفتر العمل. |
| معالجة بطيئة على ملفات ضخمة | معالجة جميع المخططات مرة واحدة | عالج المخططات على دفعات أو زد حجم الذاكرة المخصصة للـ JVM. |

## الأسئلة المتكررة

**س: ما هو الاستخدام الأساسي لتغيير حجم تسميات بيانات المخطط؟**  
**ج:** لتحسين قابلية القراءة في المخططات التي تختلف فيها أطوال التسميات، مما يمنع القطع أو التداخل.

**س: هل يمكنني تطبيق ذلك على كل نوع مخطط؟**  
**ج:** نعم، Aspose.Cells يدعم الأعمدة، الأشرطة، الفطائر، الخطوط، والعديد من أنواع المخططات الأخرى.

**س: هل يؤثر تغيير الحجم التلقائي بشكل كبير على الأداء؟**  
**ج:** التأثير ضئيل؛ العبء الرئيسي هو استدعاء `chart.calculate()`، وهو مطلوب لأي تعديل على المخطط.

**س: هل الترخيص إلزامي للإنتاج؟**  
**ج:** نعم، ترخيص Aspose.Cells الكامل مطلوب للنشر في بيئات الإنتاج بعد انتهاء الفترة التجريبية.

**س: هل يمكنني استخدام هذه الميزة على المخططات التي تم إنشاؤها برمجيًا؟**  
**ج:** بالطبع. قم بتطبيق نفس استدعاء `setResizeShapeToFitText(true)` بعد إنشاء المخطط.

## الموارد

- [توثيق Aspose.Cells](https://reference.aspose.com/cells/java/)
- [تحميل Aspose.Cells للـ Java](https://releases.aspose.com/cells/java/)
- [شراء ترخيص](https://purchase.aspose.com/buy)
- [نسخة تجريبية مجانية](https://releases.aspose.com/cells/java/)
- [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)
- [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9)

---

**آخر تحديث:** 2026-03-31  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}