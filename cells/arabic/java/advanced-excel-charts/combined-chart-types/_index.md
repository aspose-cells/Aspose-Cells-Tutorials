---
date: 2025-12-06
description: تعلم كيفية إضافة سلاسل البيانات، وإنشاء أنواع مخططات مركبة، وحفظ ملف
  Excel، وتصدير المخطط إلى PNG باستخدام Aspose.Cells للغة Java.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: إضافة سلسلة بيانات لإنشاء مخطط مركب باستخدام Aspose.Cells
url: /ar/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة سلسلة بيانات لإنشاء مخطط مركب باستخدام Aspose.Cells

في هذا البرنامج التعليمي سوف **تضيف سلسلة بيانات** إلى مصنف Excel وتتعلم كيفية **إنشاء مخططات مركبة** باستخدام Aspose.Cells for Java. سنمرّ بكل خطوة — من إعداد المصنف، إضافة السلاسل، تخصيص المفتاح، إلى **حفظ مصنف Excel** وتصدير **المخطط إلى PNG**. في النهاية، ستحصل على مخطط مركب جاهز للاستخدام يمكنك تضمينه في التقارير أو لوحات المعلومات.

## إجابات سريعة
- **ما المكتبة التي تنشئ مخططات مركبة؟** Aspose.Cells for Java  
- **كيف أضيف سلسلة بيانات؟** استخدم `chart.getNSeries().add(...)`  
- **هل يمكنني تصدير المخطط كصورة؟** نعم، باستخدام `chart.toImage(...)` (PNG)  
- **ما تنسيق الملف الذي يمكنني حفظ المصنف به؟** `.xlsx` القياسي (Excel)  
- **هل أحتاج إلى ترخيص للإنتاج؟** يلزم وجود ترخيص صالح لـ Aspose.Cells  

## ما هو **add data series** في Aspose.Cells؟
إضافة سلسلة بيانات تخبر المخطط أي خلايا تحتوي على القيم التي تريد رسمها. يمكن أن تمثل كل سلسلة خطًا أو عمودًا أو أي نوع مخطط آخر، ويمكنك دمجها لبناء **مخطط مركب**.

## لماذا ننشئ **مخططًا مركبًا**؟
المخطط المركب يتيح لك عرض مجموعات بيانات مختلفة بتمثيلات بصرية متميزة (مثل سلسلة خطية فوق سلسلة عمودية) في عرض واحد. هذا مثالي لمقارنة الاتجاهات مع الإجماليات، إبراز الارتباطات، أو تقديم رؤى أغنى في تنسيق مضغوط.

## المتطلبات المسبقة
- مجموعة تطوير جافا (JDK) 8 أو أعلى  
- مكتبة Aspose.Cells for Java (قم بتنزيلها من الرابط أدناه)  
- إلمام أساسي بصياغة جافا ومفاهيم Excel  

## البدء

أولاً، قم بتنزيل مكتبة Aspose.Cells for Java من الموقع الرسمي:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

بعد إضافة ملف JAR إلى مسار الفئات (classpath) في مشروعك، يمكنك البدء في بناء المخطط.

### الخطوة 1: استيراد فئات Aspose.Cells
```java
import com.aspose.cells.*;
```

### الخطوة 2: إنشاء مصنف جديد
```java
Workbook workbook = new Workbook();
```

### الخطوة 3: الوصول إلى ورقة العمل الأولى
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### الخطوة 4: إضافة كائن مخطط مركب  
سنبدأ بمخطط خطي ثم نضيف سلاسل أخرى لتحقيق تأثير **المخطط المركب**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## إضافة بيانات إلى المخطط

الآن بعد أن تم إنشاء حاوية المخطط، نحتاج إلى تغذيتها بالبيانات.

### الخطوة 5: تعريف نطاقات البيانات و **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **نصيحة احترافية:** المعامل الأول (`"A1:A5"`) هو النطاق للسلسلة الأولى، والثاني (`"B1:B5"`) ينشئ سلسلة ثانية سيتم دمجها مع الأولى.

### الخطوة 6: تعيين بيانات الفئة (محور X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## تخصيص المخطط

المخطط الجيد يروي قصة. لنضيف له عناوين، تسميات محاور، ومفتاح واضح.

### الخطوة 7: تعيين عنوان المخطط وتسميات المحاور
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### الخطوة 8: **Add legend chart** وتعديل موقعه
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## حفظ وتصدير المخطط

بعد التخصيص، سترغب في **حفظ مصنف Excel** وكذلك إنشاء صورة.

### الخطوة 9: حفظ المصنف كملف Excel
```java
workbook.save("CombinedChart.xlsx");
```

### الخطوة 10: تصدير **المخطط إلى PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> طريقة `chart.toImage` **تولد صور مخططات Excel** يمكن استخدامها في صفحات الويب، التقارير، أو الرسائل الإلكترونية.

## المشكلات الشائعة & استكشاف الأخطاء وإصلاحها

| المشكلة | الحل |
|-------|----------|
| **لا تظهر البيانات** | تحقق من أن نطاقات الخلايا (`A1:A5`, `B1:B5`, `C1:C5`) تحتوي على بيانات فعلًا قبل إنشاء المخطط. |
| **المفتاح يتداخل مع المخطط** | اضبط `chart.getLegend().setOverlay(false)` أو انقل المفتاح إلى موقع مختلف (مثل `RIGHT`). |
| **ملف الصورة فارغ** | تأكد من أن المخطط يحتوي على سلسلة واحدة على الأقل وأن `chart.toImage` يتم استدعاؤه بعد جميع التخصيصات. |
| **الحفظ يسبب استثناء** | تحقق من أن لديك صلاحيات كتابة إلى الدليل المستهدف وأن الملف غير مفتوح في Excel. |

## الأسئلة المتكررة

**س: كيف أقوم بتثبيت Aspose.Cells for Java؟**  
ج: قم بتنزيل ملف JAR من الموقع الرسمي وأضفه إلى مسار الفئات (classpath) في مشروعك. رابط التنزيل هو: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**س: هل يمكنني إنشاء أنواع مخططات أخرى غير الخط والعمود؟**  
ج: نعم، يدعم Aspose.Cells المخططات الشريطية، الدائرية، المبعثرة، المساحية، والعديد غيرها. راجع وثائق API للحصول على القائمة الكاملة.

**س: هل يلزم وجود ترخيص للاستخدام في الإنتاج؟**  
ج: يلزم وجود ترخيص صالح لـ Aspose.Cells للاستخدام في بيئات الإنتاج. تتوفر نسخة تجريبية مجانية للتقييم.

**س: كيف يمكنني تغيير ألوان كل سلسلة؟**  
ج: استخدم `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (أو ما شابه) بعد إضافة السلسلة.

**س: أين يمكنني العثور على المزيد من أمثلة الشيفرة؟**  
ج: الوثائق الشاملة وعينات إضافية متوفرة في موقع Aspose المرجعي: [here](https://reference.aspose.com/cells/java/).

---

**آخر تحديث:** 2025-12-06  
**تم الاختبار مع:** Aspose.Cells for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
