---
date: '2026-04-05'
description: تعلم كيفية إضافة مربع نص إلى مخطط Excel باستخدام Aspose.Cells للغة Java،
  مع تغطية تحميل المصنف وحفظ ملف Excel باستخدام Java.
keywords:
- how to add textbox
- save excel file java
- excel chart textbox
- load excel workbook java
- Aspose.Cells Java
title: كيفية إضافة مربع نص إلى مخطط إكسل باستخدام Aspose.Cells Java
url: /ar/java/charts-graphs/add-textbox-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة TextBox إلى مخطط Excel باستخدام Aspose.Cells Java

## مقدمة

التنقل في عالم تصور البيانات يمكن أن يكون صعبًا، خاصة عندما تحتاج إلى إضافة تعليقات نصية مخصصة أو تسميات مباشرةً على المخططات داخل جداول Excel الخاصة بك. سيوجهك هذا الدرس عبر استخدام Aspose.Cells for Java — مكتبة قوية تُبسّط هذه المهام — لتكامل TextBox بسلاسة في مخطط Excel.

**ما ستتعلمه:**
- تحميل ومعالجة ملفات Excel باستخدام Aspose.Cells for Java.
- الوصول إلى كائنات المخططات وتعديلها في دفاتر عمل Excel.
- إضافة وتخصيص عنصر تحكم TextBox على المخطط.
- حفظ التغييرات مرة أخرى في ملف Excel.

### إجابات سريعة
- **ما هي الفئة الأساسية لتحميل دفتر العمل؟** `Workbook` from `com.aspose.cells`.
- **ما هي الطريقة التي تضيف TextBox إلى مخطط؟** `addTextBoxInChart` on the chart's shape collection.
- **هل يمكنني تغيير لون تعبئة TextBox؟** Yes, via `FillFormat` and `SolidFill`.
- **كيف أحفظ الملف المعدل؟** Use `workbook.save` with a chosen `SaveFormat`.
- **هل أحتاج إلى ترخيص للإنتاج؟** Yes, a commercial license removes evaluation limits.

## كيفية إضافة TextBox إلى مخطط Excel

الآن بعد أن فهمت سير العمل العام، دعنا نتعمق في التنفيذ خطوة بخطوة. كل خطوة تتضمن مقطع شفرة قصير (يبقى دون تغيير) وتفسير واضح لما يفعله.

## المتطلبات المسبقة

- **المكتبات المطلوبة:** Aspose.Cells for Java الإصدار 25.3 أو أحدث. يستخدم هذا الدرس إعدادات Maven و Gradle.
- **إعداد البيئة:** مجموعة تطوير Java (JDK) متوافقة مثبتة على جهازك.
- **المتطلبات المعرفية:** فهم أساسي لبرمجة Java ومعرفة بهياكل ملفات Excel.

## إعداد Aspose.Cells للـ Java

لاستخدام Aspose.Cells في مشروعك، ستحتاج إلى إضافتها كاعتماد. إليك كيفية القيام بذلك باستخدام Maven أو Gradle:

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### الحصول على الترخيص

Aspose.Cells offers a free trial, temporary licenses for extended testing, and commercial purchase options:
- **نسخة تجريبية مجانية:** Download the library to start experimenting with its features.
- **ترخيص مؤقت:** Obtain one from [here](https://purchase.aspose.com/temporary-license/) to evaluate full capabilities without limitations.
- **شراء:** For ongoing use in production environments, purchase a license at [Aspose Purchase](https://purchase.aspose.com/buy).

### التهيئة الأساسية والإعداد

Once you've added the library, initialize it with your license if available:
```java
License license = new License();
license.setLicense("path/to/your/license/file.lic");
```

## دليل التنفيذ

سنستعرض الآن إضافة TextBox إلى مخطط Excel باستخدام Aspose.Cells for Java. سيتم تفصيل كل ميزة في هذا الدليل.

### تحميل ملف Excel

**Overview:** We start by loading an existing Excel file into our application, allowing us to manipulate its content programmatically.

#### الخطوة 1: استيراد الفئات المطلوبة
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

#### الخطوة 2: تحميل دفتر العمل
```java
String dataDir = "YOUR_DATA_DIRECTORY";
String filePath = dataDir + "/chart.xls";
Workbook workbook = new Workbook(filePath);
Worksheet worksheet = workbook.getWorksheets().get(0);
```
**Explanation:** فئة `Workbook` تمثل ملف Excel. تحميلها يتيح الوصول إلى جميع الأوراق والمحتوى.

### الوصول إلى كائن المخطط

**Overview:** Once the file is loaded, we need to retrieve the chart object from a specified worksheet.

#### الخطوة 3: استيراد فئة المخطط
```java
import com.aspose.cells.Chart;
```

#### الخطوة 4: الوصول إلى المخطط الأول
```java
Chart chart = worksheet.getCharts().get(0);
```
**Explanation:** هذا يسترجع أول مخطط في ورقة العمل النشطة للتلاعب الإضافي.

### إضافة عنصر تحكم TextBox إلى مخطط

**Overview:** الآن، لنضيف TextBox مخصصًا إلى مخططنا لعرض أي تعليقات نصية نريدها.

#### الخطوة 5: استيراد الفئات المطلوبة
```java
import com.aspose.cells.TextBox;
import com.aspose.cells.FillFormat;
import com.aspose.cells.LineFormat;
import java.awt.Color;
import com.aspose.cells.MsoLineDashStyle;
```

#### الخطوة 6: إضافة وتخصيص TextBox
```java
TextBox txt = chart.getShapes().addTextBoxInChart(100, 100, 850, 2500);
txt.setText("Aspose");
txt.getFont().setItalic(true);
txt.getFont().setSize(20);
txt.getFont().setBold(true);

// Set Fill Format
FillFormat fillformat = txt.getFill();
fillformat.setFillType(FillFormat.FillType.SOLID);
fillformat.getSolidFill().setColor(Color.getSilver());

// Configure Line Format
LineFormat lineformat = txt.getLine();
lineformat.setWeight(2);
lineformat.setDashStyle(MsoLineDashStyle.SOLID);
```
**Explanation:** يضيف هذا TextBox عند إحداثيات محددة، يخصص مظهر النص، ويطبق تعبئة وخطوط.

### حفظ ملف Excel

**Overview:** Finally, save the modified workbook back to an Excel file format.

#### الخطوة 7: استيراد فئة SaveFormat
```java
import com.aspose.cells.SaveFormat;
```

#### الخطوة 8: حفظ دفتر العمل
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ATBoxControl_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
**Explanation:** يتم حفظ دفتر العمل في الدليل المحدد، مع الحفاظ على التغييرات التي تم إجراؤها أثناء التنفيذ.

## تطبيقات عملية

فيما يلي بعض السيناريوهات الواقعية التي يمكن أن يكون فيها إضافة TextBox إلى مخطط Excel مفيدًا:
1. **التعليقات التوضيحية للتقارير:** استخدم صناديق النص لتوفير السياق أو تسليط الضوء على النتائج الرئيسية مباشرةً على المخططات.
2. **وسوم وعناوين مخصصة:** تحسين الفهم بمعلومات إضافية أو توضيحات قد لا تغطيها وسوم المخطط القياسية.
3. **العلامة التجارية:** إضافة شعارات الشركة أو عبارات العلامة التجارية داخل المخططات للعروض التقديمية.

## اعتبارات الأداء

عند العمل مع ملفات Excel الكبيرة، ضع في اعتبارك النصائح التالية:
- **تحسين استخدام الموارد:** قلل عدد عمليات تعديل المخططات وإنشاء الكائنات لتقليل استهلاك الذاكرة.
- **إدارة ذاكرة Java:** تأكد من التعامل الصحيح مع كائنات `Workbook` بإغلاقها بعد الاستخدام لتحرير الموارد بسرعة.
- **معالجة البيانات بكفاءة:** حمّل الأجزاء الضرورية فقط من دفتر العمل عند التعامل مع مجموعات بيانات ضخمة.

## كيفية حفظ ملف Excel باستخدام Java

الخطوة النهائية—حفظ دفتر العمل—توضح سير عمل **save excel file java**. من خلال تحديد `SaveFormat` المطلوب، يمكنك الإخراج إلى صيغة `.xls` القديمة، أو `.xlsx` الحديثة، أو حتى صيغ CSV، مما يمنحك سيطرة كاملة على نوع الملف الأنسب لعملياتك اللاحقة.

## كيفية تحميل دفتر عمل Excel باستخدام Java

توضح تهيئة `Workbook` السابقة نمط **load excel workbook java**. Aspose.Cells يبسط تعقيد تحليل هياكل Excel الثنائية، مما يسمح لك بالتركيز على منطق الأعمال بدلاً من تفاصيل إدخال/إخراج الملفات.

## الخلاصة

لقد استعرضنا إضافة TextBox إلى مخطط Excel باستخدام Aspose.Cells for Java. غطى هذا الدليل كل شيء من إعداد بيئتك وتحميل الملفات، وصولًا إلى كائنات المخططات، تخصيص صناديق النص، وحفظ المستند النهائي.

**الخطوات التالية:** جرب المزيد بتطبيق أنماط مختلفة أو استكشاف أنواع مخططات أخرى متاحة في Aspose.Cells. اطلع على وثائقهم على [Aspose Reference](https://reference.aspose.com/cells/java/) لمزيد من الوظائف المتقدمة.

## قسم الأسئلة المتكررة

1. **هل يمكنني إضافة عدة TextBoxes إلى مخطط؟**  
   - نعم، يمكنك تكرار طريقة `addTextBoxInChart` حسب الحاجة مع إحداثيات مختلفة.
2. **ماذا يحدث إذا لم يحتوي ملف Excel على مخططات؟**  
   - سيؤدي محاولة الوصول إلى مخطط غير موجود إلى استثناء. تأكد من أن دفتر العمل يحتوي على مخطط واحد على الأقل قبل المتابعة.
3. **هل من الممكن حفظ الملفات بصيغ غير .xls؟**  
   - نعم، يمكنك استخدام خيارات `SaveFormat` المختلفة مثل `XLSX` حسب احتياجاتك.
4. **كيف أتعامل مع الاستثناءات أثناء عمليات الملف؟**  
   - نفّذ كتل try‑catch حول عمليات تحميل وحفظ الملفات لإدارة الأخطاء بشكل ملائم.
5. **هل يمكن استخدام Aspose.Cells للـ Java مع لغات برمجة أخرى؟**  
   - رغم أن هذا الدليل يركز على Java، فإن Aspose.Cells متاح أيضًا لـ .NET و C++ وغيرها. راجع وثائقهم [documentation](https://reference.aspose.com/cells/java/) للحصول على أدلة خاصة باللغات.

## أسئلة شائعة

**س: هل يؤثر إضافة TextBox على أداء المخطط؟**  
ج: التأثير ضئيل؛ ومع ذلك، بالنسبة لدفاتر العمل الكبيرة جدًا، قلل عدد كائنات الشكل للحفاظ على استهلاك الذاكرة منخفضًا.

**س: هل يمكنني وضع TextBox باستخدام مراجع الخلايا بدلاً من البكسل؟**  
ج: نعم، يمكنك حساب إحداثيات البكسل من مؤشرات الخلايا أو استخدام طريقة `addTextBox` على ورقة العمل لتحديد الموقع بناءً على الخلايا.

**س: هل هناك طريقة لربط نص TextBox بقيمة خلية؟**  
ج: Aspose.Cells لا يوفر ربطًا مباشرًا للبيانات مع الأشكال، لكن يمكنك تحديث نص TextBox برمجيًا بعد قراءة قيمة الخلية.

**س: ما هي التراخيص المطلوبة للنشر التجاري؟**  
ج: الترخيص التجاري المشترا من Aspose.Cells يزيل جميع قيود التقييم وهو مطلوب للاستخدام في بيئات الإنتاج.

**س: أين يمكنني العثور على المزيد من أمثلة تعديل المخططات؟**  
ج: الوثائق الرسمية لـ Aspose.Cells ومستودع الأمثلة يحتويان على العديد من السيناريوهات، بما في ذلك السلاسل الديناميكية، وأنواع المخططات، وتنسيقها.

## الموارد

- **الوثائق:** استكشف أدلة شاملة على [Aspose Reference](https://reference.aspose.com/cells/java/).
- **التنزيل:** احصل على أحدث نسخة من المكتبة عبر [Releases](https://releases.aspose.com/cells/java/).
- **خيارات الشراء والتجربة:** احصل على الترخيص أو ابدأ بتجربة مجانية عبر [Purchase Aspose](https://purchase.aspose.com/buy) و[Free Trial](https://releases.aspose.com/cells/java/).
- **الدعم:** انضم إلى المجتمع على [Aspose Forum](https://forum.aspose.com/c/cells/9) للحصول على المساعدة.

باتباعك لهذا الدليل، يمكنك دمج Aspose.Cells بفعالية في مشاريع Java الخاصة بك لتعزيز وظائف مخططات Excel بإضافات نصية مخصصة. Happy coding!

---

**آخر تحديث:** 2026-04-05  
**تم الاختبار مع:** Aspose.Cells Java 25.3  
**المؤلف:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}