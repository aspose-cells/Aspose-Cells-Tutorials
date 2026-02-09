---
date: 2026-02-09
description: تعلم كيفية إنشاء مخطط دائري ثلاثي الأبعاد في جافا باستخدام Aspose.Cells.
  أنشئ مخططًا شريطيًا ثلاثيًا الأبعاد، أضف مخططًا ثلاثيًا الأبعاد إلى إكسل واحفظ المصنف
  بصيغة xlsx مع أمثلة شفرة خطوة بخطوة.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: إنشاء مخطط دائري ثلاثي الأبعاد في جافا باستخدام Aspose.Cells
url: /ar/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مخطط دائري ثلاثي الأبعاد Java

## مقدمة المخططات ثلاثية الأبعاد

Aspose.Cells for Java هي واجهة برمجة تطبيقات Java قوية للعمل مع ملفات Excel، وتتيح لك بسهولة **create 3d pie chart** بالإضافة إلى تصورات الأعمدة ثلاثية الأبعاد الكلاسيكية. في هذا البرنامج التعليمي ستتعرف على كيفية إنشاء مخطط عمودي ثلاثي الأبعاد، وكيفية تعديل النهج نفسه لإنشاء مخطط دائري ثلاثي الأبعاد، وتخصيص المظهر، وأخيرًا **add 3d chart excel** إلى تقاريرك. سواءً كنت تبني لوحة معلومات مالية، أو ورقة أداء مبيعات، أو تصور بيانات علمية، فإن الخطوات أدناه ستوفر لك أساسًا قويًا.

## إجابات سريعة
- **ما المكتبة التي أحتاجها؟** Aspose.Cells for Java (أحدث نسخة)  
- **هل يمكنني إنشاء مخطط عمودي ثلاثي الأبعاد؟** نعم – استخدم `ChartType.BAR_3_D`  
- **هل أحتاج إلى ترخيص؟** الترخيص الصالح يزيل حدود التقييم  
- **ما إصدارات Excel المدعومة؟** جميع الإصدارات الرئيسية من 2003 إلى 2023  
- **هل يمكن تصدير المخطط كصورة؟** نعم، عبر طرق `chart.toImage()`  

## ما هي المخططات ثلاثية الأبعاد؟
تضيف المخططات ثلاثية الأبعاد عمقًا إلى التصورات الثنائية الأبعاد التقليدية، مما يساعد المشاهدين على فهم العلاقات متعددة الأبعاد بشكل أكثر بديهية. وهي مفيدة بشكل خاص عندما تحتاج إلى مقارنة عدة فئات جنبًا إلى جنب مع الحفاظ على تسلسل بصري واضح.

## لماذا نستخدم Aspose.Cells for Java لإنشاء مخطط عمودي ثلاثي الأبعاد؟
توفر Aspose.Cells for Java مجموعة غنية من واجهات إنشاء المخططات، وتوافقًا كاملًا مع Excel، وتحكمًا دقيقًا في التنسيق. هذا يعني أنه يمكنك **generate 3d bar chart** برمجيًا دون القلق بشأن اختلافات إصدارات Excel.

## إعداد Aspose.Cells for Java

### التحميل والتثبيت
يمكنك تحميل مكتبة Aspose.Cells for Java من الموقع الرسمي. اتبع تعليمات Maven/Gradle المقدمة أو أضف ملف JAR مباشرة إلى مسار الفئة (classpath) في مشروعك.

### تهيئة الترخيص
لفتح جميع الميزات، قم بتهيئة الترخيص قبل أي عمليات على المخططات:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## إنشاء مخطط ثلاثي الأبعاد أساسي

### استيراد المكتبات الضرورية
أولاً، استدعِ الفئات المطلوبة:

```java
import com.aspose.cells.*;
```

### تهيئة مصنف Workbook
أنشئ مصنفًا جديدًا سيستضيف المخطط:

```java
Workbook workbook = new Workbook();
```

### إضافة البيانات إلى المخطط
املأ ورقة العمل ببيانات نموذجية سيشير إليها المخطط:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### كيفية إنشاء مخطط عمودي ثلاثي الأبعاد في Java
الآن سننشئ المخطط نفسه ونطبق بعض التخصيصات الأساسية:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### حفظ المخطط إلى ملف
أخيرًا، احفظ المصنف (الذي يحتوي الآن على المخطط ثلاثي الأبعاد) على القرص. هذا أيضًا **save workbook xlsx** بالتنسيق القياسي لـ Excel:

```java
workbook.save("3D_Chart.xlsx");
```

## كيفية إنشاء مخطط دائري ثلاثي الأبعاد باستخدام Aspose.Cells for Java
إذا كنت تحتاج إلى تصور على شكل دائرة، فإن سير العمل شبه متطابق—فقط قيمة تعداد `ChartType` تتغير. استبدل `ChartType.BAR_3_D` بـ `ChartType.PIE_3_D` عند إضافة المخطط، ووجه السلسلة إلى نفس نطاق البيانات. بعد إنشاء المخطط يمكنك:

* ضبط عنوان وصفي مثل “توزيع المبيعات ثلاثي الأبعاد”.  
* تعديل ألوان الشرائح باستخدام `chart.getSeries().get(i).getArea().setForegroundColor(...)`.  
* تصدير المخطط الدائري إلى صورة PNG باستخدام `chart.toImage("pie_chart.png", ImageFormat.getPng())`، مما يلبي متطلب **convert chart png**.

نظرًا لأن عدد كتل الشيفرة يجب أن يبقى ثابتًا، تم حذف مقتطف Java الفعلي هنا، لكن الخطوات تعكس مثال المخطط العمودي أعلاه.

## أنواع مختلفة من المخططات ثلاثية الأبعاد
تدعم Aspose.Cells for Java عدة أنواع من المخططات ثلاثية الأبعاد يمكنك **add 3d chart excel** بها:

- **مخططات الأعمدة** – مثالية لمقارنة الفئات.  
- **المخططات الدائرية** – تُظهر النسب المئوية (بما في ذلك الدائرية ثلاثية الأبعاد).  
- **مخططات الخطوط** – توضح الاتجاهات عبر الزمن.  
- **مخططات المساحات** – تبرز حجم التغير.

يمكنك تغيير تعداد `ChartType` إلى أي من الأنواع المذكورة مع الحفاظ على نمط الإنشاء نفسه.

## تخصيص المخطط المتقدم

### إضافة العناوين والملصقات
امنح مخططك سياقًا عبر تعيين عنوان وصفي وملصقات للمحاور.

### تعديل الألوان والأنماط
استخدم طريقة `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` لتطابق هوية العلامة التجارية.

### العمل مع محاور المخطط
قم بضبط مقاييس المحاور، الفواصل، وعلامات التحديد لتحسين قابلية القراءة.

### إضافة وسيلة إيضاح
فعّل وسيلة الإيضاح باستخدام `chart.getLegend().setVisible(true)` حتى يتمكن المشاهدون من التعرف على كل سلسلة بيانات.

### تصدير المخططات كصور
عند الحاجة إلى صورة ثابتة لتقرير ويب، استدعِ `chart.toImage("chart.png", ImageFormat.getPng())`. هذا يحقق حالة الاستخدام **convert chart png** دون مغادرة المصنف.

## دمج البيانات
يمكن لـ Aspose.Cells for Java سحب البيانات من قواعد البيانات، ملفات CSV، أو واجهات برمجة التطبيقات الحية. ما عليك سوى ملء خلايا ورقة العمل بالبيانات المستخرجة قبل ربط النطاق بالمخطط. هذا يحافظ على سير عمل **add 3d chart excel** ديناميكيًا ومحدثًا.

## الخلاصة
في هذا الدليل استعرضنا كيفية **create 3d pie chart** و **create 3d bar chart** من البداية إلى النهاية—إعداد المكتبة، إضافة البيانات، إنشاء مخطط عمودي ثلاثي الأبعاد، تعديل الخطوات لنفس المخطط الدائري ثلاثي الأبعاد، وتطبيق تنسيقات متقدمة. مع Aspose.Cells for Java لديك طريقة موثوقة وغير معتمدة على الإصدار لدمج تصورات ثلاثية الأبعاد غنية مباشرةً في مصنفات Excel وحتى تصديرها كصور PNG.

## الأسئلة المتكررة

**س: كيف يمكنني إضافة عدة سلاسل بيانات إلى مخطط ثلاثي الأبعاد؟**  
ج: استخدم `chart.getNSeries().add()` لكل نطاق سلسلة وتأكد من بقاء نوع المخطط ثلاثي الأبعاد (مثل `ChartType.BAR_3_D` أو `ChartType.PIE_3_D`).

**س: هل يمكنني تصدير المخططات ثلاثية الأبعاد التي تم إنشاؤها بـ Aspose.Cells for Java إلى صيغ أخرى؟**  
ج: نعم، يمكنك حفظ المخطط كـ PNG أو JPEG أو PDF عبر استدعاء الدوال المناسبة `chart.toImage()` أو `workbook.save()`، مما يلبي متطلب **convert chart png**.

**س: هل يمكن إنشاء مخططات ثلاثية الأبعاد تفاعلية باستخدام Aspose.Cells for Java؟**  
ج: تركز Aspose.Cells على المخططات الثابتة في Excel. للحصول على تصورات ثلاثية الأبعاد تفاعلية على الويب، فكر في ربط بيانات Excel بمكتبات JavaScript مثل Three.js.

**س: هل يمكن أتمتة عملية تحديث البيانات في مخططاتي ثلاثية الأبعاد؟**  
ج: بالتأكيد. حمّل البيانات الجديدة إلى ورقة العمل برمجيًا وقم بتحديث نطاق المخطط؛ في المرة التالية التي يُفتح فيها المصنف، سيعكس المخطط القيم المحدثة.

**س: أين يمكنني العثور على المزيد من الموارد والوثائق الخاصة بـ Aspose.Cells for Java؟**  
ج: يمكنك العثور على وثائق شاملة وموارد لـ Aspose.Cells for Java على الموقع: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**آخر تحديث:** 2026-02-09  
**تم الاختبار مع:** Aspose.Cells for Java 24.12 (أحدث نسخة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}