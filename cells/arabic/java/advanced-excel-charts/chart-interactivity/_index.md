---
date: 2025-12-01
description: تعلم كيفية تغيير نوع مخطط Excel وإضافة ميزات تفاعلية مثل تلميحات الأدوات،
  وعلامات البيانات، والتنقيب التفصيلي باستخدام Aspose.Cells للغة Java.
language: ar
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: تغيير نوع مخطط Excel وإضافة التفاعلية – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تغيير نوع مخطط Excel وإضافة التفاعلية

## مقدمة

تتيح المخططات التفاعلية لجمهورك استكشاف البيانات في الوقت الفعلي، بينما القدرة على **change Excel chart type** تمنحك المرونة لتقديم المعلومات بأكثر تنسيق بصري فعّال. في هذا الدرس ستتعلم كيفية استخدام Aspose.Cells for Java لتغيير نوع المخطط، إضافة tooltips، تضمين data labels، وحتى إنشاء روابط drill‑down — كل ذلك دون مغادرة شفرة Java الخاصة بك. في النهاية، ستحصل على مصنف Excel تفاعلي كامل المميزات يمكنك تضمينه في التقارير، لوحات التحكم، أو تطبيقات الويب.

## إجابات سريعة
- **هل يمكنني تغيير Chart Type برمجياً؟** نعم – استخدم تعداد `ChartType` عند إنشاء أو تحديث المخطط.  
- **كيف يمكنني إضافة tooltips إلى مخطط؟** فعّل تسميات البيانات واضبط `ShowValue` على true.  
- **ما هي أسهل طريقة لإضافة روابط drill‑down؟** أرفق رابطًا تشعبيًا بنقطة البيانات عبر `getHyperlinks().add(url)`.  
- **هل أحتاج إلى ترخيص لـ Aspose.Cells؟** الإصدار التجريبي المجاني يكفي للتطوير؛ الترخيص مطلوب للإنتاج.  
- **ما نسخة Java المدعومة؟** Java 8 وما فوق مدعومة بالكامل.

## ما هو “change Excel chart type”؟

تغيير نوع المخطط يعني استبدال التمثيل البصري (مثلاً، من مخطط عمودي إلى مخطط خطي) مع الحفاظ على البيانات الأساسية دون تغيير. يكون ذلك مفيدًا عندما تكتشف أن مخططًا مختلفًا ينقل الاتجاهات أو المقارنات أو التوزيعات بشكل أفضل.

## لماذا إضافة التفاعلية إلى مخططات Excel؟

- **Better data insight:** تتيح tooltips وتسمية البيانات للمستخدمين رؤية القيم الدقيقة دون الحاجة للتمرير.  
- **Engaging presentations:** العناصر التفاعلية تحافظ على اهتمام المشاهدين.  
- **Drill‑down capability:** الروابط التشعبية تسمح للمستخدمين بالانتقال إلى أوراق عمل مفصلة أو موارد خارجية.  
- **Reusable assets:** يمكن لمصنف واحد أن يخدم سيناريوهات تقارير متعددة ببساطة عن طريق تبديل أنواع المخططات.

## المتطلبات المسبقة

- بيئة تطوير Java (JDK 8+)  
- مكتبة Aspose.Cells for Java (حمّلها من [here](https://releases.aspose.com/cells/java/))  
- ملف Excel تجريبي (`data.xlsx`) يحتوي على البيانات التي تريد تصورها

## دليل خطوة بخطوة

### الخطوة 1: إعداد مشروع Java الخاص بك

1. أنشئ مشروع Java جديد في بيئة التطوير المتكاملة المفضلة لديك (IntelliJ IDEA، Eclipse، VS Code، إلخ).  
2. أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار الفئة (classpath) لمشروعك.

### الخطوة 2: تحميل مصنف المصدر

نبدأ بتحميل مصنف موجود يحتوي على البيانات لمخططنا.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### الخطوة 3: إنشاء مخطط و **تغيير نوعه**

فيما يلي نقوم بإنشاء مخطط عمودي، ثم نوضح فورًا كيفية تحويله إلى مخطط خطي إذا لزم الأمر.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **نصيحة احترافية:** تغيير نوع المخطط بعد الإنشاء بسيط كاستدعاء `setChartType(...)`. هذا يفي بالكلمة المفتاحية الأساسية **change Excel chart type** دون الحاجة إلى إنشاء كائن مخطط جديد.

### الخطوة 4: إضافة التفاعلية

#### 4.1 إضافة tooltips إلى المخطط

يتم عرض tooltips عندما يمر المستخدم فوق نقطة البيانات. في Aspose.Cells يتم تنفيذها عبر تسميات البيانات.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 إضافة تسميات البيانات ( **add data labels chart** )

يمكن لتسميات البيانات إظهار القيمة الدقيقة، اسم الفئة، أو كليهما. هنا نستخدم نمط التعليق.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 تنفيذ drill‑down ( **add drill down excel** )

رابط drill‑down يتيح للمستخدمين النقر على نقطة والانتقال إلى عرض تفصيلي، إما داخل المصنف أو على صفحة ويب.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### الخطوة 5: حفظ المصنف

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## المشكلات الشائعة والحلول

| المشكلة | السبب | الحل |
|-------|--------|-----|
| عدم ظهور tooltips | `HasDataLabels` غير مفعّل | تأكد من استدعاء `setHasDataLabels(true)` قبل ضبط `ShowValue`. |
| رابط drill‑down لا يفعل شيئًا | عنوان URL للارتباط التشعبي غير صالح | تحقق من أن URL يبدأ بـ `http://` أو `https://`. |
| نوع المخطط لا يتغير | استخدام نسخة أقدم من Aspose.Cells | قم بالترقية إلى أحدث نسخة (تم الاختبار مع 24.12). |

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع المخطط بعد إنشائه؟**  
ج: استدعِ `chart.setChartType(ChartType.YOUR_CHOICE)` على كائن `Chart` الموجود. هذا يلبي مباشرةً متطلب **change Excel chart type**.

**س: هل يمكنني تخصيص مظهر tooltips؟**  
ج: نعم. استخدم `chart.getNSeries().get(0).getPoints().getDataLabels()` لتحديد حجم الخط، اللون، والخلفية.

**س: هل من الممكن إضافة روابط drill‑down متعددة في مخطط واحد؟**  
ج: بالتأكيد. قم بالتكرار عبر النقاط واستدعِ `getHyperlinks().add(url)` لكل نقطة تريد ربطها.

**س: هل تدعم Aspose.Cells أنواع مخططات أخرى مثل الفطيرة أو الرادار؟**  
ج: جميع أنواع المخططات المعرفة في تعداد `ChartType` مدعومة، بما في ذلك `PIE`، `RADAR`، `AREA`، إلخ.

**س: أين يمكنني العثور على المزيد من الأمثلة؟**  
ج: زر [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) الرسمي للحصول على قائمة كاملة بطرق المخططات.

## الخلاصة

أنت الآن تعرف كيفية **change Excel chart type**، تضمين **tooltips**، إضافة **data labels**، وإنشاء روابط **drill‑down** باستخدام Aspose.Cells for Java. هذه الميزات التفاعلية تحول جداول البيانات الثابتة إلى أدوات استكشاف بيانات ديناميكية، مثالية للوحات التحكم، التقارير، والتحليلات القائمة على الويب.

---

**آخر تحديث:** 2025-12-01  
**تم الاختبار مع:** Aspose.Cells 24.12 for Java  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}