---
date: '2026-04-05'
description: تعلم كيفية إنشاء مخطط في Java باستخدام Aspose.Cells، وتحويل مخطط Excel
  إلى صورة، وتصدير المخطط بكفاءة.
keywords:
- how to create chart
- excel chart to image
- convert excel chart
- aspose cells chart
- how to export chart
- create chart java
title: كيفية إنشاء مخطط وتصديره كصورة في جافا باستخدام Aspose.Cells – دليل شامل
url: /ar/java/charts-graphs/aspose-cells-java-create-export-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مخطط وتصديره كصورة في جافا باستخدام Aspose.Cells – دليل كامل

## مقدمة

إذا كنت تبحث عن طريقة موثوقة **how to create chart** لإنشاء كائنات المخطط مباشرةً من كود جافا، فإن Aspose.Cells for Java يجعل الأمر بسيطًا. في هذا الدرس ستتعلم كيفية إنشاء مخطط هرمي، وتكوين إخراج صورة عالية الدقة، وأخيرًا تصدير المخطط كملف PNG. في النهاية ستفهم أيضًا كيفية **convert excel chart** إلى ملف صورة ولماذا يعتبر هذا النهج مثاليًا للتقارير الآلية.

**ما ستتعلمه**
- إعداد Aspose.Cells for Java
- إنشاء مخطط هرمي في مصنف Excel باستخدام جافا
- تكوين خيارات إخراج الصورة لتص rendering عالي الجودة
- تصدير المخططات كصور للوحة البيانات، البريد الإلكتروني، أو ملفات PDF

الآن دعنا نستعرض المتطلبات المسبقة ونجهز بيئتك.

## إجابات سريعة
- **ما المكتبة المطلوبة؟** Aspose.Cells for Java (v25.3+)
- **ما نوع المخطط المعروض؟** مخطط هرمي (يمكنك التبديل إلى أي نوع آخر)
- **كيف يتم تصدير المخطط؟** استخدم `Chart.toImage()` مع `ImageOrPrintOptions`
- **هل يمكنني التصدير إلى صيغ أخرى؟** نعم – PNG، JPEG، BMP، GIF، وTIFF مدعومة
- **هل أحتاج إلى رخصة؟** رخصة تجريبية مجانية تعمل للتقييم؛ رخصة تجارية مطلوبة للإنتاج

## ما هو “how to create chart” مع Aspose.Cells؟
توفر Aspose.Cells واجهة برمجة تطبيقات غنية تتيح للمطورين إنشاء أوراق عمل Excel برمجيًا، وإضافة مخططات، وتحويلها إلى صور — كل ذلك دون الحاجة إلى تثبيت Microsoft Office. هذا يجعلها مثالية للتقارير على الخادم، ولوحات تحليلات البيانات، وإنشاء المستندات تلقائيًا.

## لماذا تستخدم Aspose.Cells لتحويل مخطط Excel إلى صورة؟
- **عدم الاعتماد على Office:** يعمل على أي منصة تدعم جافا.
- **عرض عالي الدقة:** يدعم مضاد التعرج وإعدادات DPI للحصول على صور واضحة.
- **دعم صيغ متعددة:** تصدير إلى PNG، JPEG، SVG، PDF، وأكثر.
- **موجه للأداء:** يعمل بكفاءة مع مصنفات كبيرة ويمكن دمجه مع تعدد الخيوط.

## المتطلبات المسبقة

- **المكتبات المطلوبة:** Aspose.Cells for Java الإصدار 25.3 أو أعلى.
- **بيئة التطوير المتكاملة:** IntelliJ IDEA، Eclipse، أو أي بيئة تطوير متوافقة مع جافا.
- **JDK:** Java 8 أو أحدث.
- **المعرفة الأساسية:** الإلمام بجافا، Maven/Gradle، ومفاهيم ملفات Excel.

## إعداد Aspose.Cells لجافا

### Maven
أضف الاعتمادية التالية إلى ملف `pom.xml` الخاص بك:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
أدرج هذا السطر في ملف `build.gradle` الخاص بك:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

**الحصول على الترخيص:** تقدم Aspose.Cells رخصة تجريبية مجانية، يمكنك الحصول عليها من [صفحة الشراء](https://purchase.aspose.com/buy). قم بتطبيق الترخيص المؤقت لفتح جميع الوظائف أثناء التطوير.

### التهيئة الأساسية

للبدء، أنشئ كائن `Workbook`. هذا الكائن سيحمل بياناتك ومخططك:
```java
import com.aspose.cells.Workbook;

public class AsposeCellsInit {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        // Your chart creation code will go here.
    }
}
```

## كيفية إنشاء مخطط في جافا باستخدام Aspose.Cells

### إنشاء مخطط هرمي في Excel

#### الخطوة 1: تهيئة المصنف وورقة العمل
أولاً، قم بإعداد المصنف واحصل على مرجع إلى ورقة العمل الافتراضية.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY"; // Update with your directory path

Workbook workbook = new Workbook();
WorksheetCollection worksheets = workbook.getWorksheets();
```

#### الخطوة 2: إضافة مخطط هرمي
استخدم `ChartCollection` لإدراج مخطط هرمي. هذا يوضح عملية إنشاء **aspose cells chart**.
```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

Worksheet sheet = worksheets.get(0);
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.PYRAMID, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);
```

## تكوين خيارات إخراج الصورة (كيفية تصدير المخطط)

### الخطوة 1: ضبط الدقة ومضاد التعرج
ضبط إعدادات العرض بدقة للحصول على تحويل **excel chart to image** حاد.
```java
import com.aspose.cells.ImageOrPrintOptions;
import java.awt.RenderingHints;

ImageOrPrintOptions options = new ImageOrPrintOptions();
options.setVerticalResolution(300);
options.setHorizontalResolution(300);
options.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
options.setRenderingHint(RenderingHints.KEY_TEXT_ANTIALIASING, RenderingHints.VALUE_TEXT_ANTIALIAS_ON);
```

## تصدير المخطط كصورة (تحويل مخطط Excel)

### الخطوة 1: حفظ المخطط كصورة
أخيرًا، احفظ المخطط كملف PNG باستخدام الخيارات التي تم تكوينها مسبقًا.
```java
chart.toImage(dataDir + "chart.png", options);
```

**نصائح استكشاف الأخطاء**
- تحقق من أن `dataDir` يشير إلى مجلد قابل للكتابة.
- تأكد من أن إصدار Aspose.Cells لديك هو 25.3 أو أحدث؛ الإصدارات القديمة قد تفتقر إلى الدالة `toImage` المستخدمة هنا.

## تطبيقات عملية

إليك سيناريوهات شائعة حيث تبرز قدرات **how to export chart**:
1. **تقارير الأعمال:** إنشاء لوحات مبيعات شهرية تلقائيًا.
2. **أدوات تعليمية:** إنشاء تقارير أداء بصرية للطلاب.
3. **تحليلات الرعاية الصحية:** عرض إحصاءات المرضى للعروض التقديمية دون الحاجة إلى عمل يدوي في Excel.

## اعتبارات الأداء

عند التوسع:
- تخلص من كائنات `Workbook` غير المستخدمة لتحرير الذاكرة.
- استخدم واجهات برمجة التطبيقات المتدفقة (Streaming APIs) لمجموعات البيانات الضخمة.
- قم بتوازي إنشاء المخططات عند توليد تقارير متعددة في آن واحد.

اتباع هذه النصائح يضمن بقاء خدمة جافا الخاصة بك سريعة الاستجابة حتى تحت حمل ثقيل.

## الخلاصة

أصبح لديك الآن أساس قوي لإنشاء كائنات **how to create chart**، تخصيص العرض، و**export chart** كصور باستخدام Aspose.Cells for Java. جرب قيم `ChartType` أخرى، طبق التنسيق، أو دمج مخرجات PNG في ملفات PDF، صفحات الويب، أو مرفقات البريد الإلكتروني.

**الخطوات التالية**
- جرب مخططات الخط، الشريط، أو الفطيرة بتغيير `ChartType.PYRAMID`.
- استكشف فئة `Chart` لتخصيص العنوان، الأسطورة، والمحاور.
- انضم إلى المجتمع للحصول على رؤى أعمق.

فكر في زيارة [منتدى Aspose](https://forum.aspose.com/c/cells/9) للحصول على نصائح إضافية وأمثلة من العالم الحقيقي.

## الأسئلة المتكررة

**س: كيف يمكنني إضافة نوع مخطط مختلف؟**  
**ج:** استخدم قيمة أخرى من تعداد `ChartType`، مثل `ChartType.BAR` أو `ChartType.PIE`.

**س: هل يمكنني إنشاء مخطط من ملف Excel موجود؟**  
**ج:** نعم. حمّل المصنف باستخدام `new Workbook("existing.xlsx")` ثم أضف أو عدّل المخططات.

**س: ما هي المشكلات الشائعة عند استخدام **excel chart to image**؟**  
**ج:** مسارات ملفات غير صحيحة، أذونات كتابة غير كافية، أو استخدام نسخة من Aspose.Cells أقدم من 25.3.

**س: كيف يمكنني التعامل مع مصنفات ضخمة بكفاءة؟**  
**ج:** استفد من واجهات برمجة التطبيقات المتدفقة (Streaming APIs) في Aspose.Cells وتخلص من الكائنات بسرعة للحفاظ على انخفاض استهلاك الذاكرة.

**س: هل يمكن تخصيص عناوين المخططات أو الأساطير؟**  
**ج:** بالتأكيد. توفر فئة `Chart` طرقًا مثل `setTitle()`، `setLegend()`، و`setSeries()` لتخصيص كامل.

---

**آخر تحديث:** 2026-04-05  
**تم الاختبار مع:** Aspose.Cells for Java 25.3  
**المؤلف:** Aspose  

## الموارد
- [التوثيق](https://reference.aspose.com/cells/java/)
- [تحميل Aspose.Cells لجافا](https://releases.aspose.com/cells/java/)
- [شراء رخصة](https://purchase.aspose.com/buy)
- [تحميل نسخة تجريبية مجانية](https://releases.aspose.com/cells/java/)
- [الحصول على رخصة مؤقتة](https://purchase.aspose.com/temporary-license/)
- [منتدى الدعم](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}