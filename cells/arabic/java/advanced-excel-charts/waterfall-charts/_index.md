---
date: 2026-02-16
description: تعلم كيفية تعيين نطاق بيانات المخطط وإنشاء مخطط شلالي في جافا باستخدام
  Aspose.Cells. دليل خطوة بخطوة لإضافة مخطط سلسلة البيانات، تخصيصه، وتصديره إلى XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: تعيين نطاق بيانات المخطط – مخطط الشلال في Aspose.Cells for Java
url: /ar/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# مخططات الشلال

## مقدمة عن مخططات الشلال باستخدام Aspose.Cells for Java

في هذا البرنامج التعليمي ستتعلم كيفية **set chart data range** وإنشاء **waterfall chart** باستخدام Aspose.Cells for Java. تُعد مخططات الشلال أداة أساسية في تصور البيانات لأنها تتيح لك رؤية التأثير التراكمي لسلسلة من القيم الإيجابية والسلبية. سواءً كنت تُعد بيانًا ماليًا أو تقرير أداء مبيعات أو أي تحليل آخر قائم على البيانات، يمكن لمخطط الشلال تحويل الأرقام الخام إلى رؤى واضحة وقابلة للتنفيذ.

## إجابات سريعة
- **What is a waterfall chart?** تصور يُظهر كيف يتم زيادة القيمة الأولية وتقليلها من خلال سلسلة من القيم الوسيطة، لينتهي بإجمالي نهائي.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** نسخة تجريبية مجانية تكفي للتطوير؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **Can I save the file as XLSX?** نعم – استخدم `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** بالتأكيد؛ توفر Aspose.Cells ميزات مخططات غنية دون الحاجة إلى تثبيت Office.

## ما هو مخطط الشلال؟

يعرض مخطط الشلال المساهمات الإيجابية والسلبية المتتابعة لقيمة ابتدائية، مما يساعدك على فهم كيف يؤثر كل مكون على النتيجة الكلية.

## لماذا تستخدم Aspose.Cells for Java لإضافة مخطط شلال؟

- **No Microsoft Excel required** – إنشاء المخططات على أي خادم أو خط أنابيب CI.  
- **Full control over formatting** – يمكن تخصيص الألوان، وعناوين البيانات، والمحاور برمجياً.  
- **Supports multiple output formats** – يدعم صيغ XLSX، PDF، HTML، وغيرها.  
- **High performance** – مثالي لدفاتر العمل الكبيرة والتقارير الآلية.

## المتطلبات المسبقة

قبل الغوص في الكود، تأكد من توفر المتطلبات التالية:

- Aspose.Cells for Java: ستحتاج إلى تثبيت Aspose.Cells for Java. يمكنك تنزيله من [here](https://releases.aspose.com/cells/java/).
- Java Development Environment: تأكد من تثبيت Java على نظامك.

الآن، لنبدأ بإنشاء مخطط الشلال خطوة بخطوة.

## كيفية تعيين نطاق بيانات المخطط لمخطط شلال في Java

### الخطوة 1: استيراد Aspose.Cells

```java
import com.aspose.cells.*;
```

أولاً، تحتاج إلى استيراد مكتبة Aspose.Cells إلى مشروع Java الخاص بك. توفر هذه المكتبة وظائف واسعة للعمل مع ملفات Excel، بما في ذلك إنشاء المخططات.

### الخطوة 2: تهيئة Workbook و Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

أنشئ دفتر عمل جديد وأضف إليه ورقة عمل. سنستخدم هذه الورقة لإدخال بياناتنا و **add chart to worksheet**.

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

لقد أضفنا مخطط شلال إلى ورقة العمل، وحددنا سلسلة البيانات وبيانات الفئات. هذه هي الخطوة الأساسية التي **adds waterfall chart** إلى ورقتك. لاحظ كيف يستخدم أسلوب `add` النطاق `"B2:B6"` – هذا هو المكان الذي **set chart data range** للسلسلة. يمكنك مزيدًا من تخصيص مظهر المخطط (الألوان، وعناوين البيانات، إلخ) باستخدام خصائص كائن `Chart`.

### الخطوة 5: حفظ دفتر العمل

```java
workbook.save("WaterfallChart.xlsx");
```

احفظ دفتر العمل إلى ملف. يستخدم المثال صيغة XLSX، لكن Aspose.Cells يتيح لك أيضًا **export excel pdf java**‑compatible ملفات مثل PDF، CSV، والعديد من الصيغ الأخرى. هذا يلبي متطلب **save workbook xlsx**.

## المشكلات الشائعة والحلول

- **Chart appears blank** – تحقق من أن مراجع نطاق البيانات (`B2:B6` و `A2:A6`) تتطابق مع الخلايا الفعلية التي تحتوي على القيم والفئات.  
- **Negative values not displayed correctly** – تأكد من ضبط نوع السلسلة إلى `ChartType.WATERFALL`؛ الأنواع الأخرى من المخططات تتعامل مع القيم السلبية بشكل مختلف.  
- **File not opening in Excel** – تأكد من أنك تستخدم نسخة حديثة من Aspose.Cells (أحدث إصدار) وأن امتداد الملف يتطابق مع الصيغة (`.xlsx` لExcel).

## الأسئلة المتكررة

### كيف يمكنني تخصيص مظهر مخطط الشلال الخاص بي؟

يمكنك تخصيص مظهر مخطط الشلال الخاص بك عن طريق تعديل خصائص مثل الألوان، وعناوين البيانات، وعناوين المحاور. راجع وثائق Aspose.Cells للحصول على إرشادات مفصلة.

### هل يمكنني إنشاء مخططات شلال متعددة في نفس ورقة العمل؟

نعم، يمكنك إنشاء مخططات شلال متعددة في نفس ورقة العمل باتباع نفس الخطوات مع نطاقات بيانات مختلفة.

### هل Aspose.Cells متوافق مع بيئات تطوير Java المختلفة؟

نعم، Aspose.Cells for Java متوافق مع بيئات تطوير Java المختلفة، بما في ذلك Eclipse، IntelliJ IDEA، و NetBeans.

### هل يمكنني إضافة سلاسل بيانات إضافية إلى مخطط الشلال الخاص بي؟

بالتأكيد، يمكنك إضافة المزيد من سلاسل البيانات إلى مخطط الشلال لتمثيل سيناريوهات بيانات معقدة بفعالية. هذا مثال على كيفية **add data series chart** برمجيًا.

### أين يمكنني العثور على المزيد من الموارد والأمثلة لـ Aspose.Cells for Java؟

يمكنك استكشاف وثائق Aspose.Cells for Java على [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) للحصول على معلومات متعمقة وأمثلة على الشيفرة.

## الأسئلة الشائعة

**س: كيف يمكنني تعيين نطاق بيانات المخطط لمخطط شلال مالي؟**  
ج: استخدم أسلوب `add` على سلسلة المخطط، مع تمرير نطاق الخلايا الذي يحتوي على قيمك، مثل `"B2:B6"`.

**س: هل يمكنني تصدير دفتر العمل إلى PDF بدلاً من XLSX؟**  
ج: نعم، استدعِ `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` للحصول على مخرجات **export excel pdf java**‑compatible.

**س: ماذا لو احتجت لإنشاء مخطط شلال مالي مع فئات أكثر؟**  
ج: قم بتمديد نطاق البيانات في كل من عمود القيم وعمود الفئات، ثم حدّث استدعاءات `add` و `setCategoryData` وفقًا لذلك.

**س: هل هناك طريقة لتنسيق الأعمدة الإيجابية والسلبية تلقائيًا؟**  
ج: يمكنك التكرار عبر مجموعة `Series` وتعيين لون `FillFormat` بناءً على إشارة كل قيمة.

**س: هل يدعم Aspose.Cells تحديثات البيانات الديناميكية للمخططات؟**  
ج: نعم، يمكنك تعديل قيم الخلايا بعد إنشاء المخطط؛ سيعكس المخطط التغييرات عند حفظ دفتر العمل.

---

**آخر تحديث:** 2026-02-16  
**تم الاختبار مع:** Aspose.Cells for Java (latest)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}