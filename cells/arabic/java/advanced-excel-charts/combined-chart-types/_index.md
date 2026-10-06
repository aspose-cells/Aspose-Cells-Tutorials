---
date: 2026-02-14
description: تعلم كيفية تصدير المخطط إلى PNG، إضافة سلسلة بيانات، دمج مخطط خطي وعمودي،
  حفظ المصنف كملف XLSX وإضافة وسيلة إيضاح للمخطط باستخدام Aspose.Cells for Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: تصدير المخطط إلى PNG وإضافة سلسلة بيانات للمخطط المركب
url: /ar/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى PNG وإضافة سلسلة بيانات للمخطط المركب

في هذا البرنامج التعليمي ستقوم **بإضافة سلسلة بيانات** إلى دفتر عمل Excel، **بدمج عناصر مخطط الخط والعمود**، وتتعلم كيفية **تصدير المخطط إلى PNG** باستخدام Aspose.Cells for Java. سنستعرض كل خطوة — من إعداد دفتر العمل، إضافة المخطط إلى ورقة عمل، تخصيص الأسطورة، إلى **حفظ دفتر العمل كـ xlsx** وإنشاء صورة PNG للمخطط. في النهاية، ستحصل على مخطط مركب جاهز للاستخدام يمكنك تضمينه في التقارير أو لوحات المعلومات.

## إجابات سريعة
- **أي مكتبة تنشئ مخططات مركبة؟** Aspose.Cells for Java  
- **كيف يمكنني إضافة سلسلة بيانات؟** استخدم `chart.getNSeries().add(...)`  
- **كيف يمكنني تصدير المخطط إلى png؟** استدعِ `chart.toImage("file.png", ImageFormat.getPng())`  
- **ما هو تنسيق الملف الذي يمكنني حفظ دفتر العمل به؟** `.xlsx` القياسي (حفظ دفتر العمل كـ xlsx)  
- **هل أحتاج إلى ترخيص للإنتاج؟** يلزم وجود ترخيص صالح لـ Aspose.Cells  

## ما هو **export chart to PNG** في Aspose.Cells؟
إن تصدير مخطط إلى PNG ينشئ صورة نقطية للمخطط في Excel يمكن عرضها في صفحات الويب أو التقارير أو رسائل البريد الإلكتروني دون الحاجة إلى تطبيق Excel.

## لماذا إنشاء **combined line column chart**؟
يتيح لك المخطط المركب عرض مجموعات بيانات مختلفة بتمثيلات بصرية متميزة (مثل سلسلة خط فوق سلسلة عمود) في عرض واحد. هذا مثالي لمقارنة الاتجاهات مع الإجماليات، إبراز الارتباطات، أو تقديم رؤى أغنى في تنسيق مدمج.

## المتطلبات المسبقة
- Java Development Kit (JDK) 8 أو أعلى  
- مكتبة Aspose.Cells for Java (تحميل من الرابط أدناه)  
- إلمام أساسي بصياغة Java ومفاهيم Excel  

## البدء

أولاً، قم بتحميل مكتبة Aspose.Cells for Java من الموقع الرسمي:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

بعد إضافة ملف JAR إلى مسار الفئة (classpath) في مشروعك، يمكنك البدء في بناء المخطط.

### الخطوة 1: استيراد فئات Aspose.Cells
```java
import com.aspose.cells.*;
```

### الخطوة 2: إنشاء دفتر عمل جديد
```java
Workbook workbook = new Workbook();
```

### الخطوة 3: الوصول إلى ورقة العمل الأولى
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### الخطوة 4: إضافة كائن مخطط مركب إلى ورقة العمل  
سنبدأ بمخطط خط ثم نضيف لاحقًا سلسلة عمود لتحقيق تأثير **combined line column chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## إضافة بيانات إلى المخطط

الآن بعد أن حاوية المخطط موجودة، نحتاج إلى تغذيتها بالبيانات.

### الخطوة 5: تعريف نطاقات البيانات و **إضافة سلسلة بيانات**
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

المخطط الجيد يروي قصة. دعنا نضيف له عناوين، تسميات المحاور، وأسطورة واضحة.

### الخطوة 7: **تعيين تسميات محاور المخطط** والعنوان
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### الخطوة 8: **إضافة أسطورة للمخطط** وتعديل موقعها
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## حفظ وتصدير المخطط

بعد التخصيص، سترغب في **حفظ دفتر العمل كـ xlsx** وكذلك إنشاء صورة.

### الخطوة 9: حفظ دفتر العمل كملف Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### الخطوة 10: **تصدير المخطط إلى PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> طريقة `chart.toImage` **تولد صور مخطط Excel** يمكن استخدامها في صفحات الويب أو التقارير أو رسائل البريد الإلكتروني.

## المشكلات الشائعة & استكشاف الأخطاء

| المشكلة | الحل |
|-------|----------|
| **No data appears** | تحقق من أن نطاقات الخلايا (`A1:A5`, `B1:B5`, `C1:C5`) تحتوي فعليًا على بيانات قبل إنشاء المخطط. |
| **Legend overlaps chart** | اضبط `chart.getLegend().setOverlay(false)` أو انقل الأسطورة إلى موقع مختلف (مثلاً `RIGHT`). |
| **Image file is blank** | تأكد من أن المخطط يحتوي على سلسلة واحدة على الأقل وأن `chart.toImage` تم استدعاؤه بعد جميع التخصيصات. |
| **Saving throws an exception** | تحقق من أن لديك صلاحيات كتابة إلى الدليل المستهدف وأن الملف غير مفتوح في Excel. |

## الأسئلة المتكررة

**س: كيف أقوم بتثبيت Aspose.Cells for Java؟**  
ج: قم بتحميل ملف JAR من الموقع الرسمي وأضفه إلى مسار الفئة (classpath) في مشروعك. رابط التحميل هو: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**س: هل يمكنني إنشاء أنواع مخططات أخرى غير الخط والعمود؟**  
ج: نعم، يدعم Aspose.Cells المخططات الشريطية، الدائرية، المبعثرة، المساحية، والعديد من الأنواع الأخرى. راجع وثائق API للقائمة الكاملة.

**س: هل يلزم وجود ترخيص للاستخدام في الإنتاج؟**  
ج: يلزم وجود ترخيص صالح لـ Aspose.Cells للنشر في بيئات الإنتاج. تتوفر نسخة تجريبية مجانية للتقييم.

**س: كيف يمكنني تغيير ألوان كل سلسلة؟**  
ج: استخدم `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (أو ما شابه) بعد إضافة السلاسل.

**س: أين يمكنني العثور على المزيد من أمثلة الشيفرة؟**  
ج: الوثائق الشاملة والعينات الإضافية متوفرة في موقع مرجع Aspose: [here](https://reference.aspose.com/cells/java/).

---

**آخر تحديث:** 2026-02-14  
**تم الاختبار مع:** أحدث نسخة من Aspose.Cells for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}