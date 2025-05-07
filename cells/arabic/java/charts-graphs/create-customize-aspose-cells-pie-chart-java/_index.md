---
"date": "2025-04-08"
"description": "تعلم كيفية إنشاء وتخصيص المخططات الدائرية باستخدام Aspose.Cells لجافا. دليل خطوة بخطوة مع أمثلة برمجية للمطورين."
"title": "إتقان Aspose.Cells - إنشاء وتخصيص المخططات الدائرية في Java"
"url": "/ar/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# إتقان Aspose.Cells: إنشاء مخططات دائرية وتخصيصها في Java

## مقدمة
يُعد إنشاء مخططات بيانية جذابة بصريًا متطلبًا شائعًا عند التعامل مع تصور البيانات في Excel. سواء كنت تعرض معلومات ديموغرافية أو تحلل اتجاهات السوق، توفر المخططات الدائرية طريقة واضحة لتمثيل البيانات النسبية. ومع ذلك، قد يكون إعداد هذه المخططات برمجيًا معقدًا. يرشدك هذا البرنامج التعليمي خلال إنشاء مخطط بياني دائري Aspose.Cells وتخصيصه باستخدام Java، مما يُبسط العملية للمطورين.

**ما سوف تتعلمه:**
- قم بإعداد بيئتك باستخدام Aspose.Cells لـ Java.
- إنشاء مصنف جديد والوصول إلى خلايا ورقة العمل.
- قم بتعبئة البيانات في خلايا محددة للتحضير لإنشاء الرسم البياني.
- إنشاء مخطط دائري من هذه البيانات.
- قم بتخصيص مظهر مخططك الدائري، بما في ذلك الألوان والعناوين والأساطير.

قبل البدء، تأكد من فهمك الأساسي لبرمجة جافا وإدارة تبعيات Maven أو Gradle. لنبدأ بإعداد بيئتنا!

## المتطلبات الأساسية
لمتابعة هذا البرنامج التعليمي، ستحتاج إلى:
- **مجموعة تطوير جافا (JDK)**:الإصدار 8 أو أعلى.
- **بيئة التطوير المتكاملة (IDE)**:مثل IntelliJ IDEA أو Eclipse.
- **إدارة التبعيات**:استخدم Maven أو Gradle لإدارة التبعيات الخاصة بك.

### المكتبات والتبعيات المطلوبة
تأكد من تضمين Aspose.Cells for Java في مشروعك باستخدام Maven أو Gradle.

**مافن**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**جرادل**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### خطوات الحصول على الترخيص
Aspose.Cells لجافا هي مكتبة تجارية، ولكن يمكنك البدء بفترة تجريبية مجانية أو التقدم بطلب للحصول على ترخيص مؤقت. تفضل بزيارة [صفحة الشراء](https://purchase.aspose.com/buy) لاستكشاف خيارات الترخيص.

## إعداد Aspose.Cells لـ Java
أولاً، تأكد من أن بيئة مشروعك تتضمن المكتبات اللازمة بإضافتها عبر Maven أو Gradle كما هو موضح أعلاه. بعد إضافتها، يمكنك تهيئة Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// تهيئة مثيل مصنف جديد
Workbook workbook = new Workbook();
```

## دليل التنفيذ

### إنشاء مصنف وتكوينه
إن إنشاء مصنف هو الخطوة الأولى لإعداد بياناتك.

#### استيراد المكتبات
تأكد من تضمين هذه الواردات في أعلى ملفك:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### الخطوة 1: إنشاء مثيل مصنف
```java
// إنشاء مثيل مصنف فارغ للعمل عليه.
Workbook workbook = new Workbook();
```
تعمل هذه الخطوة على تهيئة ملف Excel الخاص بك برمجيًا، مما يسمح لك بالتعامل معه باستخدام وظائف Aspose.Cells.

### الوصول إلى خلايا ورقة العمل أو تعديلها
بعد ذلك، قم بملء البيانات في خلايا ورقة العمل التي سيتم استخدامها في الرسم البياني الدائري.

#### الخطوة 2: الوصول إلى ورقة العمل وخلاياها
```java
// قم بالوصول إلى ورقة العمل الأولى في المصنف.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// ضع قيم العينة المستخدمة في مخطط دائري في خلايا محددة.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// وضع قيم النسب المئوية لمخطط دائري في خلايا محددة.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
هنا، يمكنك ملء ورقة العمل بالبيانات التي ستمثل أجزاء مختلفة من مخطط دائري.

### إنشاء مخطط دائري

#### الخطوة 3: إضافة مخطط دائري إلى ورقة العمل
```java
// إنشاء مخطط دائري في ورقة العمل.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
تضيف هذه الخطوة مخططًا دائريًا جديدًا إلى ورقة العمل الخاصة بك في المواضع والأبعاد المحددة.

### تكوين سلسلة مخططات الفطيرة والبيانات

#### الخطوة 4: تعيين السلسلة للرسم البياني
```java
// قم بتكوين نطاق بيانات السلسلة للرسم البياني.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// ربط عنوان المخطط الدائري بالخلية التي تحتوي على نص العنوان.
pie.getTitle().setLinkedSource("D2");
```
يقوم هذا الكود بربط نطاق البيانات لديك وإعداد السلسلة لمخطط الفطيرة.

### تكوين أسطورة الرسم البياني ومظهر العنوان

#### الخطوة 5: تخصيص أسطورة الرسم البياني والعنوان
```java
// تعيين موضع الأسطورة في أسفل الرسم البياني.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// تعيين خصائص الخط لعنوان الرسم البياني.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
يؤدي تخصيص المظهر إلى تحسين إمكانية القراءة والجاذبية البصرية.

### تخصيص ألوان سلسلة المخططات

#### الخطوة 6: تغيير ألوان أجزاء الدائرة
```java
import com.aspose.cells.Color;

// الوصول إلى ألوان أجزاء المخطط الدائري الفردية وتخصيصها.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
تعمل هذه الإعدادات على تخصيص الرسم البياني الخاص بك ليناسب أنظمة الألوان المحددة.

### ضبط الأعمدة تلقائيًا وحفظ المصنف

#### الخطوة 7: ضبط عرض الأعمدة وحفظ الملف
```java
// ملائمة جميع الأعمدة تلقائيًا.
worksheet.autoFitColumns();

// قم بتحديد مسار العنصر النائب لدليل الإخراج لحفظ المصنف.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// احفظ المصنف المعدل في ملف Excel في الدليل المحدد.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
وأخيرًا، قم بضبط الأعمدة تلقائيًا وحفظ المصنف الخاص بك.

## التطبيقات العملية
1. **التحليل الديموغرافي**:استخدم المخططات الدائرية لعرض توزيعات السكان عبر بلدان أو مناطق مختلفة.
2. **تقارير حصة السوق**:توضيح حصة السوق للشركات المختلفة في قطاع معين.
3. **تخصيص الميزانية**:تصور كيفية تخصيص الميزانيات عبر الأقسام المختلفة داخل المنظمة.

تُظهر هذه التطبيقات تنوع وفائدة Aspose.Cells في السيناريوهات الواقعية.

## اعتبارات الأداء
لتحسين الأداء عند استخدام Aspose.Cells:
- قم بتقليل استخدام الذاكرة عن طريق التخلص من الكائنات التي لم تعد هناك حاجة إليها.
- استخدم هياكل البيانات الفعالة لمعالجة مجموعات البيانات الكبيرة.
- قم بإنشاء ملف تعريف لتطبيقك لتحديد الاختناقات.

إن الالتزام بأفضل الممارسات يضمن تطبيقات سلسة وسريعة الاستجابة.

## خاتمة
شرح لك هذا البرنامج التعليمي خطوات إنشاء مخطط دائري وتخصيصه باستخدام Aspose.Cells في جافا. بفضل هذه المعرفة، يمكنك الآن تطبيق هذه التقنيات على مختلف مهام تصور البيانات في مشاريعك. لمزيد من الاستكشاف، يمكنك التعمق في أنواع المخططات الإضافية وخيارات التخصيص المتقدمة المتاحة مع Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}