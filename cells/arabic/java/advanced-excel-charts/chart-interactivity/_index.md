---
date: 2026-02-09
description: تعلم كيفية إضافة تسميات البيانات إلى مخطط Excel وتغيير نوع المخطط باستخدام
  Aspose.Cells for Java، بالإضافة إلى تلميحات الأدوات والتفاعل القابل للتفصيل.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: إضافة تسميات البيانات إلى مخطط Excel باستخدام Aspose.Cells Java
url: /ar/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة تسميات البيانات إلى مخطط Excel وتغيير نوع المخطط – Aspose.Cells Java

تُضيف المخططات التفاعلية مستوىً جديدًا من الفهم لتقارير Excel الخاصة بك، و**إضافة تسميات البيانات إلى مخطط Excel** تجعل المعلومات قابلة للقراءة فورًا. في هذا الدرس ستتعلم كيفية **إضافة تسميات البيانات إلى مخطط Excel**، وتغيير نوع المخطط، وإنشاء حلول Java تفاعلية باستخدام Aspose.Cells. سنُظهر لك أيضًا كيفية إضافة تلميحات أدوات (tooltips) ورابط تنقيب بسيط (drill‑down hyperlink) حتى يتمكن جمهورك من استكشاف البيانات بعمق.

## إجابات سريعة
- **ما المكتبة المستخدمة؟** Aspose.Cells for Java  
- **هل يمكنني تغيير نوع المخطط؟** نعم – فقط عدل تعداد `ChartType` عند إنشاء المخطط.  
- **كيف أضيف تلميحات أدوات إلى المخطط؟** استخدم API تسميات البيانات (`setHasDataLabels(true)`) وفعل عرض القيم.  
- **هل يدعم التنقيب (drill‑down)؟** يمكنك إرفاق روابط تشعبية بنقاط البيانات لسلوك تنقيب أساسي.  
- **المتطلبات المسبقة؟** بيئة تطوير Java، ملف JAR الخاص بـ Aspose.Cells، وملف Excel يحتوي على بيانات نموذجية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- بيئة تطوير Java (يفضل JDK 8 أو أعلى)  
- مكتبة Aspose.Cells for Java (حمّلها من [هنا](https://releases.aspose.com/cells/java/))  
- مصنف نموذج (`data.xlsx`) يحتوي على البيانات التي تريد تصورها  

## الخطوة 1: إعداد مشروع Java الخاص بك

1. أنشئ مشروع Java جديد في بيئة التطوير المفضلة لديك (IntelliJ IDEA، Eclipse، إلخ).  
2. أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار بناء المشروع أو إلى تبعيات Maven/Gradle.

## الخطوة 2: تحميل البيانات

للعمل مع المخططات تحتاج أولاً إلى تحميل مصنف في الذاكرة.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## الخطوة 3: إنشاء مخطط (وتغيير نوعه)

يمكنك اختيار أي نوع مخطط يناسب تحليلك. أدناه ننشئ **مخطط عمودي**، لكن يمكنك بسهولة التحويل إلى مخطط خطي أو دائري أو شريطي بتغيير تعداد `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **نصيحة احترافية:** لتغيير **نوع مخطط Excel**، استبدل `ChartType.COLUMN` بـ `ChartType.LINE` أو `ChartType.PIE`، إلخ.

## الخطوة 4: إضافة التفاعلية

### 4.1. إضافة تلميحات أدوات (Add Tooltips to Chart)

تظهر تلميحات الأدوات عندما يمر المستخدم فوق نقطة بيانات. الكود التالي يُفعّل تسميات البيانات ويظهر القيمة كتلميح أدوات.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. إضافة تسميات البيانات – **add data labels to excel chart**

توفر تسميات البيانات إشارة بصرية دائمة على المخطط نفسه. يمكنك عرضها كـ callouts لتحسين القابلية للقراءة.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **لماذا نضيف تسميات البيانات؟** إضافة تسميات البيانات مباشرةً على المخطط تُلغي الحاجة إلى تمرير المؤشر أو تخمين القيم، مما يحسّن وضوح التقرير.

### 4.3. تنفيذ التنقيب (رابط تشعبي على نقطة بيانات)

طريقة بسيطة لإضافة قدرة التنقيب هي إرفاق رابط تشعبي بنقطة معينة. النقر على النقطة يفتح صفحة ويب تحتوي على معلومات مفصلة.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## الخطوة 5: حفظ المصنف

بعد تكوين المخطط، احفظ المصنف بحيث تُحفظ الميزات التفاعلية في ملف الإخراج.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **التلميحات لا تظهر** | تأكد من استدعاء `setHasDataLabels(true)` قبل تكوين `setShowValue(true)`. |
| **الرابط التشعبي غير قابل للنقر** | تحقق من أن تنسيق الإخراج يدعم الروابط التشعبية (مثل XLSX، وليس CSV). |
| **نوع المخطط لا يتغير** | تأكد من تعديل تعداد `ChartType` الصحيح عند إضافة المخطط. |

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع المخطط بعد إنشائه؟**  
ج: تحتاج إلى إنشاء مخطط جديد باستخدام `ChartType` المطلوب. لا توفر Aspose.Cells تحويلًا مباشرًا للنوع داخل المخطط الحالي، لذا احذف المخطط القديم وأضف واحدًا جديدًا.

**س: هل يمكنني تخصيص مظهر تلميحات الأدوات؟**  
ج: نعم. استخدم خصائص `DataLabel` مثل `setFontSize` و `setFontColor` و `setBackgroundColor` لتنسيق نص التلميح.

**س: كيف أتعامل مع تفاعلات المستخدم في تطبيق ويب؟**  
ج: صدّر المصنف إلى ملف HTML أو XLSX واستخدم JavaScript على جانب العميل لالتقاط أحداث النقر على عناصر المخطط.

**س: أين يمكنني العثور على مزيد من الأمثلة والوثائق؟**  
ج: زر [مرجع API لـ Aspose.Cells Java](https://reference.aspose.com/cells/java/) للحصول على قائمة كاملة بالفئات والطرق المتعلقة بالمخططات.

## الخلاصة

أنت الآن تعرف كيف **تضيف تسميات البيانات إلى مخطط Excel**، **تغير نوع مخطط Excel**، **تنشئ حلول مخططات Java تفاعلية**، وتُثريها بتلميحات أدوات، وتسميات بيانات، وروابط تنقيب باستخدام Aspose.Cells for Java. هذه التحسينات تجعل تقارير Excel أكثر جذبًا وإفادة للمستخدمين النهائيين.

---

**آخر تحديث:** 2026-02-09  
**تم الاختبار مع:** Aspose.Cells for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}