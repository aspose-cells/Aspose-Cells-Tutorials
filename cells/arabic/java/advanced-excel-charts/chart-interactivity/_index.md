---
date: 2025-12-04
description: تعلم كيفية إنشاء مخطط تفاعلي في Java باستخدام Aspose.Cells، وإضافة تلميحات
  إلى المخطط، وإضافة مخطط تفصيلي لتوفير تصور بيانات أغنى.
language: ar
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: إنشاء مخطط تفاعلي بلغة Java باستخدام Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مخطط تفاعلي Java

## المقدمة

تتيح المخططات التفاعلية للمستخدمين استكشاف نقاط البيانات، ورؤية التفاصيل عند التحويم، وحتى الغوص في مجموعات بيانات أعمق — كل ذلك دون مغادرة جدول البيانات. في هذا البرنامج التعليمي ستتعلم **كيفية إنشاء مخطط تفاعلي Java** باستخدام Aspose.Cells. سنستعرض إضافة تلميحات الأدوات، وتسميات البيانات، وتنفيذ تجربة الحفر إلى أسفل، لتصبح مخططاتك أكثر جاذبية وإفادة.

## إجابات سريعة
- **ما المكتبة المستخدمة؟** Aspose.Cells for Java  
- **هل يمكنني إضافة تلميحات أدوات إلى المخطط؟** Yes, using the NSeries data‑label API  
- **هل يدعم الحفر إلى أسفل؟** Yes, by attaching hyperlinks to data points  
- **ما تنسيق الملف الناتج؟** Standard XLSX workbook with embedded charts  
- **هل أحتاج إلى ترخيص؟** A free trial works for evaluation; a commercial license is required for production  

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

- بيئة تطوير Java (يفضل JDK 8+)
- مكتبة Aspose.Cells for Java (قم بتنزيلها من [صفحة إصدار Aspose الرسمية](https://releases.aspose.com/cells/java/))
- ملف Excel تجريبي اسمه **data.xlsx** يحتوي على البيانات التي تريد تصورها  

## الخطوة 1: إعداد مشروع Java الخاص بك

1. أنشئ مشروع Java جديد في بيئة التطوير المتكاملة المفضلة لديك (IntelliJ IDEA، Eclipse، VS Code، إلخ).  
2. أضف ملف JAR الخاص بـ Aspose.Cells إلى مسار الفئة (classpath) لمشروعك — إما بوضع الملف في مجلد `libs` أو بإضافة تبعية Maven/Gradle.  

## الخطوة 2: تحميل البيانات

لبناء مخطط تفاعلي تحتاج أولاً إلى ورقة عمل تحتوي على بيانات. المقتطف أدناه يفتح مصنفًا موجودًا ويستخرج أول ورقة عمل.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **نصيحة احترافية:** تأكد من أن نطاق البيانات الذي تنوي رسمه متصل؛ سيقوم Aspose.Cells تلقائيًا باكتشاف النطاق عند ربط السلسلة.

## الخطوة 3: إنشاء مخطط

الآن نقوم بإنشاء مخطط عمودي وتحديد موقعه على ورقة العمل. يمكنك تغيير `ChartType.COLUMN` إلى أي نوع آخر (مثال: `ChartType.LINE`) إذا كنت تفضل نمطًا بصريًا مختلفًا.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **لماذا هذا مهم:** إضافة المخطط برمجيًا يمنحك تحكمًا كاملًا في حجمه وموقعه ومصدر البيانات، وهو أمر أساسي لبناء تجارب تفاعلية.

## الخطوة 4: إضافة التفاعلية

### كيفية إضافة تلميحات أدوات إلى المخطط

تساعد تلميحات الأدوات (أو تسميات البيانات التي تُظهر القيم) المستخدمين على رؤية الرقم الدقيق خلف كل شريط فورًا. الشيفرة التالية تمكّن تسميات البيانات وتضبطها لعرض القيمة.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### كيفية إضافة تسميات البيانات (ملاحظة)

إذا كنت تريد أن تظهر التسميات كملاحظة بدلاً من نص عادي، قم بتغيير خاصية `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### كيفية إضافة مخطط حفر إلى أسفل

يتيح الحفر إلى أسفل للمستخدم النقر على نقطة بيانات والانتقال إلى عرض تفصيلي ذي صلة — عادةً ما يُنفّذ باستخدام ارتباط تشعبي. أدناه نرفق عنوان URL بالنقطة الأولى في السلسلة.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **خطأ شائع:** تذكر ضبط هدف الارتباط التشعبي إلى صفحة يمكنها عرض البيانات التفصيلية (مثل تقرير ويب أو ورقة Excel أخرى). وإلا سيؤدي النقر إلى رابط غير صالح.

## الخطوة 5: حفظ المصنف

بعد تكوين المخطط، احفظ المصنف. يحتوي الملف الناتج على المخطط التفاعلي جاهزًا للفتح في Excel أو أي عارض متوافق.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## الخلاصة

في هذا الدليل تعلمت **كيفية إنشاء مخطط تفاعلي Java** باستخدام Aspose.Cells، وشمل ذلك:

- تحميل البيانات من مصنف موجود  
- إنشاء مخطط عمودي برمجيًا  
- إضافة تلميحات أدوات وتسمية بيانات كملاحظة  
- تنفيذ وظيفة الحفر إلى أسفل عبر الارتباطات التشعبية  
- حفظ المصنف النهائي  

تحول هذه التقنيات جداول البيانات الثابتة إلى لوحات معلومات ديناميكية وسهلة الاستخدام تعزز فهم البيانات واتخاذ القرار.

## الأسئلة المتكررة

**س: كيف يمكنني تغيير نوع المخطط؟**  
ج: عدل تعداد `ChartType` في طريقة `add` (مثال: `ChartType.LINE` لمخطط خطي).

**س: هل يمكنني تخصيص مظهر تلميحات الأدوات؟**  
ج: نعم، يمكنك تعديل حجم الخط، اللون، الخلفية، وغيرها من خصائص النمط عبر كائن `DataLabels`.

**س: كيف أتعامل مع تفاعلية المخطط في تطبيق ويب؟**  
ج: صدّر المصنف إلى XLSX، ثم استخدم مكتبة رسم مخططات JavaScript (مثل Highcharts) لعرض البيانات على جانب العميل، أو دمج ملف Excel في Web الذي يدعم الارتباطات التشعبية.

**س: أين يمكنني العثور على المزيد من الأمثلة؟**  
ج: زر [مرجع Aspose.Cells Java API الرسمي](https://reference.aspose.com/cells/java/) للحصول على قائمة كاملة بفئات وطرق المخططات.

**س: هل أحتاج إلى ترخيص للاستخدام في الإنتاج؟**  
ج: نعم، يلزم ترخيص تجاري للنشر؛ يتوفر ترخيص تجريبي مجاني للاختبار.

---

**آخر تحديث:** 2025-12-04  
**تم الاختبار مع:** Aspose.Cells for Java 24.12 (latest at time of writing)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}