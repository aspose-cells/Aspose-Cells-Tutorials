---
"date": "2025-04-07"
"description": "برنامج تعليمي لبرمجة Aspose.Words في Java"
"title": "تدوير النص في أشكال Excel باستخدام Aspose.Cells Java"
"url": "/ar/java/images-shapes/rotate-text-excel-shapes-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# إتقان Aspose.Cells في Java: تدوير النص مع الأشكال في Excel

## مقدمة

عند العمل مع جداول بيانات Excel، قد تواجه حالات تتطلب محاذاة النص داخل الشكل بدقة دون تدويره بالكامل. سيرشدك هذا البرنامج التعليمي إلى كيفية استخدام **Aspose.Cells لـ Java** لتحقيق هذه الوظيفة. باتباعك هذا الدليل، ستتعلم كيفية تدوير النص بكفاءة داخل الأشكال مع الحفاظ على ثبات الشكل، مما يُحسّن قابلية قراءة مستند Excel وعرضه.

### ما سوف تتعلمه:
- قم بتحميل ملف Excel الموجود باستخدام Aspose.Cells.
- الوصول إلى خلايا وأشكال ورقة العمل والتلاعب بها.
- تدوير النص داخل الأشكال دون تغيير اتجاهها.
- حفظ التغييرات مرة أخرى في ملف Excel جديد.

دعونا نلقي نظرة على المتطلبات الأساسية التي ستحتاجها للبدء.

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن لديك ما يلي:

### المكتبات المطلوبة
- **Aspose.Cells لـ Java**تتيح لك هذه المكتبة التعامل مع ملفات Excel. تأكد من استخدام الإصدار 25.3 أو أحدث.
  
### متطلبات إعداد البيئة
- **مجموعة تطوير جافا (JDK)**:قم بتثبيت JDK 8 أو إصدار أحدث على جهازك.
- **بيئة تطوير متكاملة**:استخدم بيئة تطوير متكاملة مثل IntelliJ IDEA، أو Eclipse، أو NetBeans.

### متطلبات المعرفة
- فهم أساسي لبرمجة Java والمعرفة بأدوات بناء Maven أو Gradle.
- ستكون المعرفة بهياكل ملفات Excel مفيدة ولكنها ليست ضرورية.

## إعداد Aspose.Cells لـ Java

للإستخدام **Aspose.Cells لـ Java**يمكنك دمجه بسهولة في مشروعك باستخدام Maven أو Gradle. إليك الطريقة:

### استخدام Maven
أضف التبعية التالية إلى ملفك `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### استخدام Gradle
قم بتضمين هذا في `build.gradle` ملف:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### خطوات الحصول على الترخيص

لتجربة Aspose.Cells، يمكنك الحصول على ترخيص مؤقت مجاني أو شرائه للاستفادة من كامل وظائفه. اتبع الخطوات التالية:

1. **نسخة تجريبية مجانية**:تحميل المكتبة من [تنزيلات Aspose](https://releases.aspose.com/cells/java/).
2. **رخصة مؤقتة**اطلب ترخيصًا مؤقتًا في [ترخيص Aspose المؤقت](https://purchase.aspose.com/temporary-license/).
3. **شراء**:للاستخدام طويل الأمد، قم بشراء ترخيص عبر [شراء Aspose](https://purchase.aspose.com/buy).

### التهيئة والإعداد الأساسي

بمجرد التثبيت، قم بتهيئة Aspose.Cells في تطبيق Java الخاص بك على النحو التالي:

```java
import com.aspose.cells.Workbook;

public class ExcelApp {
    public static void main(String[] args) throws Exception {
        // قم بتهيئة ترخيص Aspose.Cells هنا إذا كان متاحًا
        Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleRotateTextWithShapeInsideWorksheet.xlsx");
        
        // منطق الكود الخاص بك يذهب هنا
    }
}
```

## دليل التنفيذ

### الميزة 1: تحميل ملف Excel النموذجي

#### ملخص
إن تحميل ملف Excel الموجود هو الخطوة الأولى في عمليتنا.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/sampleRotateTextWithShapeInsideWorksheet.xlsx");
```

**توضيح**: ال `Workbook` تمثل الفئة جدول البيانات بأكمله. بتمرير مسار الملف، يمكنك تحميل مستند Excel إلى الذاكرة.

### الميزة 2: الوصول إلى ورقة العمل الأولى

#### ملخص
يتيح لنا الوصول إلى أوراق عمل محددة استهداف مناطق محددة للتلاعب بالنصوص والأشكال.

```java
import com.aspose.cells.Worksheet;

Worksheet ws = wb.getWorksheets().get(0);
```

**توضيح**: `getWorksheets()` يعيد مجموعة من كل الأوراق، بينما `get(0)` الوصول إلى ورقة العمل الأولى.

### الميزة 3: إضافة رسالة إلى خلية

#### ملخص
تعتبر إضافة النص إلى الخلايا أمرًا بسيطًا باستخدام Aspose.Cells.

```java
import com.aspose.cells.Cell;

Cell b4 = ws.getCells().get("B4");
b4.putValue("Text is not rotating with shape because RotateTextWithShape is false.");
```

**توضيح**: `getCells()` يقوم بجلب جميع كائنات الخلية، و `putValue` تعيين النص إلى خلية محددة.

### الميزة 4: الوصول إلى الشكل الأول في ورقة العمل

#### ملخص
يتضمن التعامل مع الأشكال الوصول إلى خصائصها لضبط محاذاة النص.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.ShapeTextAlignment;

Shape sh = ws.getShapes().get(0);
ShapeTextAlignment shapeTextAlignment = sh.getTextBody().getTextAlignment();
shapeTextAlignment.setRotateTextWithShape(false);
```

**توضيح**: ال `getShapes()` تسترجع الطريقة جميع الأشكال، ونقوم بتعديل محاذاة النص عن طريق ضبط `setRotateTextWithShape` إلى خطأ.

### الميزة 5: حفظ ملف Excel في دليل الإخراج

#### ملخص
وأخيرًا، احفظ التغييرات في ملف جديد.

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
wb.save(outDir + "/outputRotateTextWithShapeInsideWorksheet.xlsx");
```

**توضيح**: ال `save()` تكتب الطريقة جميع التعديلات إلى دليل الإخراج المحدد.

## التطبيقات العملية

1. **إنشاء التقارير**:قم بتخصيص التقارير حيث تكون تسميات النصوص ضرورية دون تشويه الرسومات.
2. **تخصيص لوحة المعلومات**:الحفاظ على الصور الثابتة في لوحات معلومات الأعمال أثناء تدوير النصوص الوصفية.
3. **المواد التعليمية**:إنشاء محتوى تعليمي مع تعليقات توضيحية واضحة ومتناسقة.
4. **المواد التسويقية**:قم بتصميم أوراق تسويقية تتطلب اتجاهًا شكليًا ثابتًا على الرغم من اتجاهات النص المتنوعة.

## اعتبارات الأداء

- **تحسين تحميل الملفات**:قم بتحميل أوراق العمل الضرورية فقط لتقليل استخدام الذاكرة.
- **معالجة الدفعات**:عند معالجة ملفات متعددة، ضع في اعتبارك العمليات الدفعية لتحقيق الكفاءة.
- **إدارة الذاكرة**:تخلص من الكائنات على الفور واستخدم إعدادات JVM المناسبة للتعامل مع ملفات Excel الكبيرة.

## خاتمة

في هذا البرنامج التعليمي، استكشفنا كيفية معالجة النصوص داخل الأشكال في Excel باستخدام Aspose.Cells لجافا. بفهم هذه التقنيات، يمكنك تحسين المظهر المرئي ووضوح جداول البيانات. تتضمن الخطوات التالية استكشاف المزيد من الميزات التي يقدمها Aspose.Cells أو دمجه مع أنظمة أخرى مثل قواعد البيانات أو تطبيقات الويب.

## قسم الأسئلة الشائعة

1. **كيف أقوم بتثبيت Aspose.Cells لـ Java؟**
   - قم بالتثبيت عبر Maven أو Gradle كما هو موضح في قسم الإعداد.
2. **هل يمكنني استخدام هذا النهج مع تنسيقات Excel القديمة؟**
   - نعم، يدعم Aspose.Cells تنسيقات ملفات متعددة بما في ذلك XLS وXLSX.
3. **ماذا لو تداخلت الأشكال بعد تعديلات تدوير النص؟**
   - قم بضبط خصائص الشكل يدويًا للتأكد من عدم تداخلها.
4. **كيف يمكنني تدوير النص بدرجة معينة؟**
   - يستخدم `setRotationAngle` على `TextBody` لإجراء تعديلات دقيقة على الزاوية.
5. **هل يتوفر الدعم إذا واجهت مشاكل؟**
   - نعم، تقدم Aspose خدمات شاملة [يدعم](https://forum.aspose.com/c/cells/9).

## موارد

- التوثيق: [مرجع Aspose.Cells Java](https://reference.aspose.com/cells/java/)
- تحميل: [الإصدارات](https://releases.aspose.com/cells/java/)
- شراء: [شراء Aspose.Cells](https://purchase.aspose.com/buy)
- تجربة مجانية: [تنزيلات Aspose](https://releases.aspose.com/cells/java/)
- رخصة مؤقتة: [ترخيص Aspose](https://purchase.aspose.com/temporary-license/)

جرّب هذه التقنيات، وخذ عمليات معالجة مستندات Excel الخاصة بك إلى المستوى التالي باستخدام Aspose.Cells لـ Java!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}