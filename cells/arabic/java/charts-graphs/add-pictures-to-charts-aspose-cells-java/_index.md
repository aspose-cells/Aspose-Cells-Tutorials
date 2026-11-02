---
date: '2026-03-31'
description: تعلم كيفية إضافة صورة إلى مخططات Java باستخدام Aspose.Cells، بما في ذلك
  خطوات إدراج الصور، إضافة شعار إلى المخطط، وتخصيص صورة المخطط.
keywords:
- add pictures to charts
- enhance Java charts
- Aspose.Cells integration
title: كيفية إضافة صورة إلى مخططات Java باستخدام Aspose.Cells
url: /ar/java/charts-graphs/add-pictures-to-charts-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة صورة إلى مخططات Java باستخدام Aspose.Cells

## المقدمة

إن تصور البيانات بفعالية يمكن أن يكون عامل تغيير للعرض التقديمي، التقارير، ولوحات معلومات ذكاء الأعمال. إذا كنت تتساءل **كيفية إضافة صورة** إلى مخطط — مثل شعار الشركة أو أيقونة المنتج — فإن Aspose.Cells for Java يمنحك التحكم الكامل في كائنات المخطط. في هذا البرنامج التعليمي سنستعرض العملية الكاملة لإدراج صورة في مخطط، وتخصيص مظهرها، وحفظ النتيجة.

### إجابات سريعة
- **ما هي المكتبة الأساسية؟** Aspose.Cells for Java  
- **هل يمكنني إضافة شعار إلى أي نوع من المخططات؟** نعم، معظم أنواع المخططات المدمجة تدعم إدراج الصور.  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص مطلوب للإنتاج.  
- **ما نسخة Java المطلوبة؟** Java 8 أو أعلى.  
- **هل يمكن إضافة صور متعددة؟** بالتأكيد — استدعِ `addPictureInChart` لكل صورة.

## كيفية إضافة صورة إلى مخطط

إضافة صورة إلى مخطط أمر بسيط بمجرد أن تكون لديك كائنات المصنف والمخطط جاهزة. أدناه نقسم المهمة إلى خطوات واضحة مرقمة لتتمكن من المتابعة بسهولة.

## المتطلبات المسبقة

1. **المكتبات والاعتماديات المطلوبة**  
   - Aspose.Cells for Java (الإصدار 25.3 أو أحدث)  
   - بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse  

2. **إعداد البيئة**  
   - Java Development Kit (JDK) 8+ مثبت  
   - نظام بناء Maven أو Gradle  

3. **المتطلبات المعرفية**  
   - التعامل الأساسي مع الملفات في Java  
   - الإلمام بهياكل مخططات Excel  

## إعداد Aspose.Cells for Java

أضف المكتبة إلى مشروعك باستخدام Maven أو Gradle.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص

توفر Aspose نسخة تجريبية مجانية، ويمكنك طلب ترخيص مؤقت للاختبار الموسع. زر [صفحة شراء Aspose](https://purchase.aspose.com/buy) للحصول على تفاصيل حول الحصول على ترخيص دائم.

### التهيئة الأساسية

بمجرد وجود الاعتماد، أنشئ كائن `Workbook` واحصل على ورقة العمل الأولى:

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## دليل التنفيذ

### تحميل مخطط Excel

**الخطوة 1 – تحميل المصنف**  

```java
String dataDir = Utils.getSharedDataDir(AddingPictureToChart.class) + "Charts/";
Workbook workbook = new Workbook(dataDir + "chart.xls");
```

### إضافة صور إلى المخططات

**الخطوة 2 – الوصول إلى المخطط**  

```java
Worksheet worksheet = workbook.getWorksheets().get(0);
Chart chart = worksheet.getCharts().get(0);
```

**الخطوة 3 – إضافة صورة في المخطط**  

```java
FileInputStream stream = new FileInputStream(dataDir + "logo.jpg");
Picture pic = chart.getShapes().addPictureInChart(50, 50, stream, 40, 40);
```

**الخطوة 4 – تخصيص مظهر الصورة**  

```java
LineFormat lineformat = pic.getLine();
lineformat.setFillType(FillType.SOLID);
lineformat.getSolidFill().setColor(Color.getBlue());
lineformat.setDashStyle(MsoLineDashStyle.DASH_DOT_DOT);
```

### الإخراج والحفظ

```java
workbook.save(dataDir + "APToChart_out.xls");
system.out.println("Picture added to chart successfully.");
```

> **نصيحة احترافية:** استخدم صور PNG ذات خلفيات شفافة للحصول على مظهر أنظف عند إدراج الشعارات.

## تطبيقات عملية

- **إضافة شعار إلى المخطط** – تعزيز هوية العلامة التجارية في العروض التقديمية.  
- **إدراج صورة في المخطط** – تسليط الضوء على نقاط البيانات الرئيسية بأيقونات ذات صلة.  
- **تخصيص صورة المخطط** – مطابقة ألوان الشركة عن طريق تعديل تنسيقات الخط.  

## اعتبارات الأداء

- **تحسين أحجام الصور** – الصور الأصغر تقلل من استهلاك الذاكرة.  
- **إغلاق التدفقات** – أغلق كائنات `FileInputStream` فورًا.  
- **المعالجة الدفعية** – عالج عدة مصنفات في حلقة لتحسين الإنتاجية.  

## الخلاصة

أنت الآن تعرف **كيفية إضافة صورة** إلى مخططات Java باستخدام Aspose.Cells، من تحميل المصنف إلى تخصيص نمط الصورة وحفظ الملف. جرّب أنواع مخططات وصيغ صور مختلفة لإنشاء تقارير مصقولة ومتسقة مع العلامة التجارية.

نحن نشجعك على استكشاف المزيد من الميزات في المكتبة. للحصول على رؤى أعمق، اطلع على [توثيق Aspose](https://reference.aspose.com/cells/java/).

## الأسئلة المتكررة

**س1: كيف أطبق ترخيصًا مؤقتًا لـ Aspose.Cells؟**  
ج1: زر [صفحة الترخيص المؤقت لـ Aspose](https://purchase.aspose.com/temporary-license/) لطلب واحد، مما يتيح لك تقييم النسخة الكاملة دون قيود.

**س2: هل يمكنني إضافة صور متعددة إلى مخطط واحد باستخدام Aspose.Cells؟**  
ج2: نعم، استدعِ `addPictureInChart` عدة مرات مع تدفقات صور وإحداثيات مختلفة.

**س3: ماذا لو لم تظهر صوري بشكل صحيح في المخطط؟**  
ج3: تحقق من صحة مسار الصورة، وأن الصيغة مدعومة (PNG، JPEG، إلخ)، وقم بضبط إحداثيات X/Y أو معلمات الحجم.

**س4: كيف أتعامل مع الاستثناءات عند إضافة صور إلى المخططات؟**  
ج4: احط عمليات الإدخال/الإخراج في Aspose.Cells بكتل try‑catch للتعامل بسلاسة مع `IOException` أو `CellsException`.

**س5: هل يمكن إضافة صور من URL بدلاً من مسار محلي؟**  
ج5: نعم — قم بتحميل الصورة باستخدام `HttpURLConnection` في Java أو مكتبة مثل Apache HttpClient، ثم مرّر `InputStream` الناتج إلى `addPictureInChart`.

## الموارد

- **التوثيق:** [مرجع Aspose.Cells for Java](https://reference.aspose.com/cells/java/)  
- **التنزيل:** [أحدث إصدارات Aspose.Cells for Java](https://releases.aspose.com/cells/java/)  
- **الشراء:** [شراء تراخيص Aspose.Cells](https://purchase.aspose.com/buy)  
- **التجربة المجانية:** [اختبار ميزات Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **ترخيص مؤقت:** [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)  
- **الدعم:** [منتدى Aspose للأسئلة والمساعدة](https://forum.aspose.com/c/cells/9)

---

**آخر تحديث:** 2026-03-31  
**تم الاختبار مع:** Aspose.Cells for Java 25.3  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}