---
"date": "2025-04-07"
"description": "تعلّم كيفية إنشاء وتخصيص المخططات الدائرية في Excel باستخدام Aspose.Cells لجافا. اتبع هذا الدليل خطوة بخطوة لتحسين مهاراتك في تصور البيانات."
"title": "إنشاء مخططات دائرية في Excel باستخدام Aspose.Cells لـ Java - دليل شامل"
"url": "/ar/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إنشاء مخططات دائرية في Excel باستخدام Aspose.Cells لـ Java
## مقدمة
إنشاء مخططات دائرية جذابة وغنية بالمعلومات في Excel يُحوّل البيانات الخام إلى رؤى قيّمة، مما يُمكّنك من اتخاذ قرارات عمل مدروسة بسرعة. هل تواجه صعوبة في استخدام ميزات Microsoft Excel المدمجة أو تبحث عن حل قابل للتطوير يتكامل بسلاسة مع تطبيقات Java؟ Aspose.Cells for Java هنا لمساعدتك.

يرشدك هذا البرنامج التعليمي إلى كيفية إنشاء وتخصيص مخططات دائرية في ملفات Excel باستخدام Aspose.Cells لجافا. اكتشف كيفية إضافة البيانات بكفاءة، وتكوين عناصر المخطط، وإنهاء مصنفك - كل ذلك بسهولة ودقة.

**ما سوف تتعلمه:**
- إعداد Aspose.Cells واستخدامه في Java
- إنشاء مصنف جديد وملئه ببيانات العينة
- إضافة المخططات الدائرية وتخصيصها داخل ورقة عمل Excel
- أفضل الممارسات لتكوين المخططات وتحسينها

دعونا نبدأ بتغطية المتطلبات الأساسية.
## المتطلبات الأساسية
قبل أن تبدأ، تأكد من أن لديك ما يلي:
### المكتبات والإصدارات والتبعيات المطلوبة
تأكد من تضمين Aspose.Cells لإصدار Java 25.3 أو أحدث في مشروعك باستخدام Maven أو Gradle.
**مافن:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**جرادل:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### متطلبات إعداد البيئة
- مجموعة تطوير Java (JDK) مثبتة على نظامك.
- بيئة التطوير المتكاملة (IDE) مثل IntelliJ IDEA، أو Eclipse، أو NetBeans.
### متطلبات المعرفة
سيكون من المفيد فهم أساسيات برمجة Java والتعرف على هياكل ملفات Excel.
## إعداد Aspose.Cells لـ Java
Aspose.Cells مكتبة فعّالة تُمكّن المطورين من إنشاء جداول بيانات Excel وتعديلها وعرضها في تطبيقات Java. إليك كيفية إعدادها:
1. **تثبيت**:أضف تبعية Maven أو Gradle كما هو موضح أعلاه.
2. **الحصول على الترخيص**:
   - احصل على ترخيص تجريبي مجاني للاختبار الأولي من [نسخة تجريبية مجانية من Aspose](https://releases.aspose.com/cells/java/).
   - قم بتقديم طلب للحصول على ترخيص مؤقت لاختبار الميزات الكاملة دون قيود عبر [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/).
3. **التهيئة الأساسية**:ابدأ بإنشاء مثيل لـ `Workbook` الفئة التي تمثل ملف Excel الخاص بك.
```java
import com.aspose.cells.Workbook;
// إنشاء مصنف جديد وتهيئته
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## دليل التنفيذ
الآن، دعنا ننفذ كل ميزة خطوة بخطوة لإنشاء مصنف Excel مع مخطط دائري.
### 1. إنشاء المصنف وتهيئته
**ملخص**:نبدأ بتهيئة `Workbook` الكائن والوصول إلى ورقة العمل الأولى الخاصة به حيث سنضيف البيانات والرسوم البيانية.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// إنشاء مثيل جديد للمصنف
Workbook workbook = new Workbook();
// الوصول إلى ورقة العمل الأولى في المصنف
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. إضافة بيانات العينة إلى الخلايا
**ملخص**:قم بملء ورقة العمل الخاصة بك ببيانات العينة التي سيتم تمثيلها في مخطط الفطيرة.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// أضف أسماء البلدان في العمود أ
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// متابعة للدول الأخرى...
// أضف بيانات المبيعات المقابلة في العمود B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// تابع لبقية البيانات...
```
### 3. إضافة مخطط دائري إلى ورقة العمل
**ملخص**:أدرج مخططًا دائريًا في ورقة العمل باستخدام نطاقات البيانات المحددة مسبقًا.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// إضافة مخطط دائري في الموقع والحجم المحددين
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. تكوين سلسلة المخططات
**ملخص**:قم بتحديد نطاق البيانات لبيانات المبيعات والفئات (أسماء البلدان) للتأكد من أن الرسم البياني الدائري يمثل مجموعة البيانات الخاصة بك بدقة.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// تعيين بيانات المبيعات كمصدر بيانات للرسم البياني
serieses.add("B1:B8", true);
// تحديد بيانات الفئة (أسماء البلدان)
serieses.setCategoryData("A1:A8");
// تمكين الألوان المتنوعة لكل شريحة فطيرة
serieses.setColorVaried(true);

// عرض جدول البيانات على الرسم البياني للتوضيح
chart.setShowDataTable(true);
```
### 5. تعيين عنوان ونمط الرسم البياني
**ملخص**:قم بتخصيص عنوان الرسم البياني الخاص بك لتحسين إمكانية القراءة والعرض.
```java
import com.aspose.cells.Color;

// تعيين عنوان الرسم البياني باستخدام خيارات التصميم
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. تكوين تسميات البيانات لسلسلة المخططات
**ملخص**:أضف تسميات البيانات إلى كل شريحة فطيرة، مما يوفر تفصيلاً واضحًا للقيم.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // ضع العلامات داخل قاعدة كل شريحة فطيرة
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // تكوين خيارات عرض الملصق
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. حفظ المصنف
**ملخص**:قم بإنهاء ملف Excel الخاص بك مع حفظ كافة البيانات والرسوم البيانية على القرص.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// حفظ المصنف في ملف Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## التطبيقات العملية
- **تحليلات الأعمال**:استخدم المخططات الدائرية في تقارير المبيعات لتوضيح حصة السوق أو توزيع الإيرادات عبر المناطق.
- **الأدوات التعليمية**:إنشاء وحدات تعليمية تفاعلية تعرض توزيعات البيانات الإحصائية.
- **إدارة المشاريع**:تمثيل تخصيص الموارد واستخدام الميزانية بصريًا لأصحاب المصلحة.
## اعتبارات الأداء
لتحسين الأداء:
- قم بتقليل استخدام الذاكرة عن طريق إدارة حجم المصنف بكفاءة.
- استخدم ميزات Aspose.Cells مثل بث الملفات الكبيرة إذا كنت تتعامل مع مجموعات بيانات واسعة النطاق.
- اتبع أفضل ممارسات Java لإدارة الذاكرة، والتأكد من تحرير الموارد بشكل مناسب بعد الاستخدام.
## خاتمة
باتباع هذا الدليل، ستتعلم كيفية إنشاء وتكوين وتخصيص المخططات الدائرية في Excel باستخدام Aspose.Cells for Java. تُمكّن هذه المكتبة القوية المطورين من دمج وظائف جداول البيانات المتقدمة في تطبيقات Java بسلاسة.
لمزيد من الاستكشاف، فكر في التعمق في أنواع أخرى من المخططات أو توسيع قدرات معالجة البيانات لديك باستخدام الميزات الإضافية التي تقدمها Aspose.Cells.
## قسم الأسئلة الشائعة
1. **هل يمكنني استخدام Aspose.Cells مجانًا؟**
   - نعم، تتوفر نسخة تجريبية مجانية. للوصول إلى كامل الميزات دون قيود، يمكنك التقدم بطلب للحصول على ترخيص مؤقت.
2. **هل من الممكن إنشاء أنواع أخرى من المخططات باستخدام Aspose.Cells؟**
   - بالتأكيد! يمكنك إنشاء مخططات شريطية ومخططات خطية وغيرها عن طريق تعديل `ChartType`.
3. **كيف أتعامل مع مجموعات البيانات الكبيرة في Excel باستخدام Java؟**
   - استخدم تقنيات تحميل البيانات الفعالة وفكر في البث المباشر للملفات الكبيرة جدًا.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}