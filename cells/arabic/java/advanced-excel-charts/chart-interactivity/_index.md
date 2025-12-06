---
date: 2025-12-06
description: تعلم كيفية تغيير نوع مخطط Excel وإنشاء مخططات تفاعلية باستخدام Java و
  Aspose.Cells. أضف تلميحات الأدوات إلى المخطط، وعلامات البيانات، وإمكانية الحفر العميق
  للحصول على تصور بيانات أكثر غنى.
language: ar
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: تغيير نوع مخطط Excel باستخدام Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تغيير نوع مخطط Excel وإضافة التفاعلية

## المقدمة

تقدم المخططات التفاعلية مستوى جديدًا من الفهم لتقارير Excel الخاصة بك، حيث تسمح للمستخدمين بالتمرير فوق العناصر، والنقر، واستكشاف نقاط البيانات مباشرة. في هذا البرنامج التعليمي ستقوم **بتغيير نوع مخطط Excel** و **إنشاء حلول مخطط تفاعلية بلغة Java** باستخدام Aspose.Cells for Java. سنستعرض إضافة تلميحات الأدوات إلى المخطط، وعلامات البيانات، ورابط تشعب بسيط للتنقيب العميق حتى يتمكن جمهورك من الغوص أكثر في الأرقام.

## إجابات سريعة
- **ما المكتبة المستخدمة؟** Aspose.Cells for Java  
- **هل يمكنني تغيير نوع المخطط؟** نعم – فقط عدل تعداد `ChartType` عند إنشاء المخطط.  
- **كيف أضيف تلميحات الأدوات إلى مخطط؟** استخدم واجهة برمجة تطبيقات تسمية البيانات (`setHasDataLabels(true)`) وفعل عرض القيمة.  
- **هل يدعم التنقيب العميق؟** يمكنك إرفاق روابط تشعبية بنقاط البيانات لسلوك تنقيب أساسي.  
- **المتطلبات المسبقة؟** بيئة تطوير Java، ملف JAR الخاص بـ Aspose.Cells، وملف Excel يحتوي على بيانات نموذجية.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- بيئة تطوير Java (يوصى بـ JDK 8 أو أعلى)  
- مكتبة Aspose.Cells for Java (قم بتنزيلها من [هنا](https://releases.aspose.com/cells/java/))  
- مصنف نموذجية (`data.xlsx`) يحتوي على البيانات التي تريد تصورها  

## الخطوة 1: إعداد مشروع Java الخاص بك

1. أنشئ مشروع Java جديد في بيئة التطوير المفضلة لديك (IntelliJ IDEA، Eclipse، إلخ).  
2. أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار بناء المشروع أو إلى تبعيات Maven/Gradle.  

## الخطوة 2: تحميل البيانات

للعمل مع المخططات تحتاج أولاً إلى تحميل المصنف في الذاكرة.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## الخطوة 3: إنشاء مخطط (وتغيير نوعه)

يمكنك اختيار أي نوع مخطط يتناسب مع تحليلك. أدناه نقوم بإنشاء **مخطط عمودي**، ولكن يمكنك بسهولة التحويل إلى مخطط خطي أو دائري أو شريطي عن طريق تعديل تعداد `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **نصيحة احترافية:** لت **تغيير نوع مخطط Excel**، استبدل `ChartType.COLUMN` بـ `ChartType.LINE` أو `ChartType.PIE`، إلخ.

## الخطوة 4: إضافة التفاعلية

### 4.1. إضافة تلميحات الأدوات (Add Tooltips to Chart)

تظهر تلميحات الأدوات عندما يمر المستخدم فوق نقطة البيانات. الكود التالي يفعّل تسميات البيانات ويظهر القيمة كتلميح.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. إضافة علامات البيانات

توفر تسميات البيانات إشارة بصرية دائمة على المخطط نفسه. يمكنك عرضها كقوالب لتسهيل القراءة.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. تنفيذ التنقيب العميق (Hyperlink on a Data Point)

طريقة بسيطة لإضافة قدرة التنقيب العميق هي إرفاق رابط تشعبي بنقطة معينة. عند النقر على النقطة يفتح صفحة ويب تحتوي على معلومات مفصلة.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## الخطوة 5: حفظ المصنف

بعد تكوين المخطط، احفظ المصنف حتى تُحفظ الميزات التفاعلية في ملف الإخراج.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **تلميحات الأدوات لا تظهر** | تأكد من استدعاء `setHasDataLabels(true)` قبل تكوين `setShowValue(true)`. |
| **الرابط التشعبي غير قابل للنقر** | تحقق من أن تنسيق الإخراج يدعم الروابط التشعبية (مثل XLSX، وليس CSV). |
| **نوع المخطط لا يتغير** | تحقق مرة أخرى من تعديل تعداد `ChartType` الصحيح عند إضافة المخطط. |

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع المخطط بعد إنشائه؟**  
ج: تحتاج إلى إنشاء مخطط جديد باستخدام `ChartType` المطلوب. لا توفر Aspose.Cells تحويل النوع في المكان، لذا احذف المخطط القديم وأضف مخططًا جديدًا.

**س: هل يمكنني تخصيص مظهر تلميحات الأدوات؟**  
ج: نعم. استخدم خصائص `DataLabel` مثل `setFontSize` و `setFontColor` و `setBackgroundColor` لتنسيق نص التلميح.

**س: كيف أتعامل مع تفاعلات المستخدم في تطبيق ويب؟**  
ج: صدّر المصنف إلى ملف HTML أو XLSX واستخدم JavaScript على جانب العميل لالتقاط أحداث النقر على عناصر المخطط.

**س: أين يمكنني العثور على المزيد من الأمثلة والوثائق؟**  
ج: زر [مرجع Aspose.Cells Java API](https://reference.aspose.com/cells/java/) للحصول على قائمة كاملة بالفئات والطرق المتعلقة بالمخططات.

## الخاتمة

أنت الآن تعرف كيف **تغيير نوع مخطط Excel**، **إنشاء حلول مخطط تفاعلية بلغة Java**، وإثرائها بتلميحات الأدوات، وعلامات البيانات، وروابط التشعب للتنقيب العميق باستخدام Aspose.Cells for Java. هذه التحسينات تجعل تقارير Excel الخاصة بك أكثر جاذبية وفهمًا للمستخدمين النهائيين.

---

**آخر تحديث:** 2025-12-06  
**تم الاختبار مع:** Aspose.Cells for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}