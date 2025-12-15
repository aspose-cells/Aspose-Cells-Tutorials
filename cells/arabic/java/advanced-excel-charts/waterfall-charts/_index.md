---
date: 2025-12-10
description: تعلم كيفية إنشاء مخطط شلال في جافا باستخدام Aspose.Cells. دليل خطوة بخطوة
  لإضافة المخطط إلى ورقة العمل، تخصيصه، وحفظ المصنف بصيغة XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: كيفية إنشاء مخطط شلال باستخدام Aspose.Cells للـ Java
url: /ar/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# مخططات الشلال

## مقدمة حول مخططات الشلال باستخدام Aspose.Cells for Java

في هذا البرنامج التعليمي ستتعلم كيفية **إنشاء مخطط شلال** باستخدام Aspose.Cells for Java. تُعد مخططات الشلال أداة أساسية في تصور البيانات لأنها تتيح لك رؤية التأثير التراكمي لسلسلة من القيم الإيجابية والسلبية. سواءً كنت تُعد بيانًا ماليًا، أو تقرير أداء مبيعات، أو أي تحليل آخر قائم على البيانات، يمكن لمخطط الشلال تحويل الأرقام الخام إلى رؤى واضحة وقابلة للتنفيذ.

## إجابات سريعة
- **ما هو مخطط الشلال؟** تصور يُظهر كيف يتم زيادة القيمة الأولية وتقليلها بواسطة سلسلة من القيم المتوسطة، لينتهي بمجموع نهائي.  
- **ما المكتبة المستخدمة؟** Aspose.Cells for Java.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **هل يمكنني حفظ الملف بصيغة XLSX؟** نعم – استخدم `workbook.save("FileName.xlsx")`.  
- **هل هو مناسب لتصور البيانات في Java؟** بالتأكيد؛ توفر Aspose.Cells ميزات رسم مخططات غنية دون الحاجة إلى تثبيت Office.

## ما هو مخطط الشلال؟
مخطط الشلال يعرض المساهمات الإيجابية والسلبية المتسلسلة لقيمة ابتدائية، مما يساعدك على فهم كيفية تأثير كل مكوّن على النتيجة الكلية.

## لماذا تستخدم Aspose.Cells for Java لإضافة مخطط شلال؟
- **لا حاجة إلى Microsoft Excel** – يمكنك إنشاء المخططات على أي خادم أو خط أنابيب CI.  
- **تحكم كامل في التنسيق** – يمكن تخصيص الألوان، وعناوين البيانات، والمحاور برمجياً.  
- **يدعم صيغ إخراج متعددة** – XLSX، PDF، HTML، وأكثر.  
- **أداء عالي** – مثالي للدفاتر الكبيرة والتقارير الآلية.

## المتطلبات المسبقة

قبل أن نغوص في الكود، تأكد من توفر المتطلبات التالية:

- Aspose.Cells for Java: ستحتاج إلى تثبيت Aspose.Cells for Java. يمكنك تنزيله من [here](https://releases.aspose.com/cells/java/).

- بيئة تطوير Java: تأكد من تثبيت Java على نظامك.

الآن، لنبدأ في إنشاء مخطط الشلال خطوةً بخطوة.

## كيفية إنشاء مخطط شلال في Java

### الخطوة 1: استيراد Aspose.Cells

```java
import com.aspose.cells.*;
```

أولاً، تحتاج إلى استيراد مكتبة Aspose.Cells إلى مشروع Java الخاص بك. توفر هذه المكتبة وظائف واسعة للعمل مع ملفات Excel، بما في ذلك إنشاء المخططات### الخطوة 2: تهيئة Workbook و Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

أنشئ دفتر عمل جديدًا وأضف ورقة عمل إليه. سنستخدم هذه الورقة لإدخال بياناتنا و**إضافة مخطط إلى ورقة العمل**.

### الخطوة 3: إدخال البيانات

الآن، لنملأ ورقة العمل بالبيانات التي نريد تمثيلها في مخطط الشلال.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

في هذا المثال، لدينا الفئات في العمود A والقيم المقابلة في العمود B. يمكنك استبدال هذه البيانات بمجموعة البيانات الخاصة بك.

### الخطوة 4: إنشاء مخطط الشلال

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

لقد أضفنا مخطط شلال إلى ورقة العمل، وحددنا سلسلة البيانات وبيانات الفئات. هذه هي الخطوة الأساسية التي **تضيف مخطط شلال** إلى الورقة. يمكنك تعديل مظهر المخطط أكثر (الألوان، وعناوين البيانات، إلخ) باستخدام خصائص كائن `Chart`.

### الخطوة 5: حفظ دفتر العمل

```java
workbook.save("WaterfallChart.xlsx");
```

احفظ دفتر العمل إلى ملف. يستخدم المثال صيغة XLSX، لكن Aspose.Cells يتيح لك أيضًا التصدير إلى PDF، CSV، والعديد من الصيغ الأخرى. هذا يفي بمتطلب **حفظ دفتر العمل بصيغة xlsx**.

## المشكلات الشائعة والحلول

- **المخطط يظهر فارغًا** – تحقق من أن مراجع نطاق البيانات (`B2:B6` و `A2:A6`) تتطابق مع الخلايا الفعلية التي تحتوي على القيم والفئات.  
- **القيم السلبية لا تُعرض بشكل صحيح** – تأكد من ضبط نوع السلسلة إلى `ChartType.WATERFALL`؛ الأنواع الأخرى من المخططات تتعامل مع السالب بطريقة مختلفة.  
- **الملف لا يفتح في Excel** – تأكد من أنك تستخدم أحدث إصدار من Aspose.Cells (الإصدار الأخير) وأن امتداد الملف يتطابق مع الصيغة (`.xlsx` لـ Excel).

## الأسئلة المتكررة

### كيف يمكنني تخصيص مظهر مخطط الشلال الخاص بي؟

يمكنك تخصيص مظهر مخطط الشلال عن طريق تعديل الخصائص مثل الألوان، وعناوين البيانات، وعناوين المحاور. راجع وثائق Aspose.Cells للحصول على إرشادات مفصلة.

### هل يمكنني إنشاء عدة مخططات شلال في نفس ورقة العمل؟

نعم، يمكنك إنشاء عدة مخططات شلال في نفس ورقة العمل باتباع نفس الخطوات مع نطاقات بيانات مختلفة.

### هل Aspose.Cells متوافق مع بيئات تطوير Java المختلفة؟

نعم، Aspose.Cells for Java متوافق مع بيئات تطوير Java المتنوعة، بما في ذلك Eclipse، IntelliJ IDEA، و NetBeans.

### هل يمكنني إضافة سلاسل بيانات إضافية إلى مخطط الشلال؟

بالطبع، يمكنك إضافة سلاسل بيانات إضافية إلى مخطط الشلال لتمثيل سيناريوهات بيانات معقدة بفعالية.

### أين يمكنني العثور على المزيد من الموارد والأمثلة لـ Aspose.Cells for Java؟

يمكنك استكشاف وثائق Aspose.Cells for Java على [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) للحصول على معلومات متعمقة وأمثلة على الشيفرات.

---

**آخر تحديث:** 2025-12-10  
**تم الاختبار مع:** Aspose.Cells for Java 24.12 (latest)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}