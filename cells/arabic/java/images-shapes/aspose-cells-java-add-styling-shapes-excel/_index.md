---
"date": "2025-04-07"
"description": "تعلّم كيفية إضافة أشكال وتصميمها، مثل المستطيلات، في Excel باستخدام مكتبة Aspose.Cells القوية مع Java. يغطي هذا الدليل كل شيء، من الإعداد إلى التنفيذ."
"title": "كيفية إضافة الأشكال وتنسيقها في Excel باستخدام Aspose.Cells Java"
"url": "/ar/java/images-shapes/aspose-cells-java-add-styling-shapes-excel/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# كيفية إضافة الأشكال وتنسيقها في Excel باستخدام Aspose.Cells Java

## مقدمة

قم بتعزيز أوراق عمل Excel الخاصة بك عن طريق إضافة أشكال مخصصة برمجيًا باستخدام `Aspose.Cells` لجافا. يرشدك هذا البرنامج التعليمي إلى كيفية إضافة شكل مستطيل، وتكوين أنماط خطوطه، وتطبيق تدرجات لونية.

**ما سوف تتعلمه:**
- إعداد Aspose.Cells في مشروع Java الخاص بك.
- إضافة شكل مستطيل إلى ورقة عمل Excel.
- تكوين أنماط الخطوط والتدرجات للأشكال.
- حفظ المصنف المعدل.

لنبدأ بالتأكد من استيفائك لجميع المتطلبات الأساسية.

## المتطلبات الأساسية

قبل الغوص في الكود، تأكد من:
- **المكتبات:** تم تضمين مكتبة Aspose.Cells (الإصدار 25.3 أو أحدث) في مشروعك.
- **بيئة:** المعرفة ببيئات تطوير Java مثل Maven أو Gradle لإدارة التبعيات.
- **معرفة:** فهم أساسي لبرمجة Java ومعالجة ملفات Excel.

## إعداد Aspose.Cells لـ Java

دمج Aspose.Cells في مشروع Java الخاص بك باستخدام أداة البناء الخاصة بك:

**مافن:**
أضف إلى `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**جرادل:**
تضمين في `build.gradle` ملف:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص

يمكنك الحصول على ترخيص مؤقت لاختبار Aspose.Cells دون قيود أو شرائه للاستخدام طويل الأمد. ابدأ بـ [نسخة تجريبية مجانية](https://releases.aspose.com/cells/java/) وفكر في الحصول على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) إذا لزم الأمر.

### التهيئة الأساسية

بعد إضافة التبعية، قم بتهيئة Aspose.Cells في مشروع Java الخاص بك:
```java
import com.aspose.cells.Workbook;

public class ExcelShapeDemo {
    public static void main(String[] args) throws Exception {
        Workbook excelBook = new Workbook();
        // سيتم إجراء المزيد من العمليات هنا.
    }
}
```

## دليل التنفيذ

### إضافة شكل مستطيل إلى ورقة عمل Excel

**ملخص:** تعرف على كيفية إضافة شكل مستطيل وتحديد موضعه في ورقة العمل الخاصة بك باستخدام Aspose.Cells.

#### الخطوة 1: إنشاء مصنف جديد
```java
Workbook excelBook = new Workbook();
```
سيؤدي هذا إلى تهيئة مثيل جديد لمصنف العمل حيث ستضيف الأشكال.

#### الخطوة 2: إضافة شكل مستطيل
```java
import com.aspose.cells.RectangleShape;
import com.aspose.cells.MsoDrawingType;

RectangleShape rectangle = (RectangleShape) excelBook.getWorksheets().get(0)
        .getShapes().addShape(MsoDrawingType.RECTANGLE, 3, 2, 0, 0, 70, 130);
```
هنا، يُضاف مستطيل إلى ورقة العمل الأولى. تُحدد المعلمات نوعه وموقعه وحجمه.

#### الخطوة 3: تحديد الموضع
```java
rectangle.setPlacement(com.aspose.cells.PlacementType.FREE_FLOATING);
```
يؤدي هذا إلى تكوين الشكل ليكون عائمًا حرًا بدلاً من أن يكون مرتبطًا بنطاق خلية محدد.

### تكوين نمط خط الشكل

**ملخص:** قم بتخصيص نمط الخط والتعبئة المتدرجة لشكل المستطيل الخاص بك.

#### الخطوة 1: تكوين نمط الخط
```java
import com.aspose.cells.LineFormat;
import com.aspose.cells.MsoLineStyle;

LineFormat linestyle = rectangle.getLine();
linestyle.setDashStyle(MsoLineStyle.THICK_THIN);
linestyle.setWeight(4);
```
يؤدي هذا إلى ضبط نمط الخط إلى نمط خط سميك-رفيع وضبط وزنه.

#### الخطوة 2: تطبيق التعبئة المتدرجة
```java
import com.aspose.cells.FillFormat;
import com.aspose.cells.GradientStyleType;

FillFormat fillformat = rectangle.getFill();
fillformat.setOneColorGradient(com.aspose.cells.Color.getBlue(), 1, 
    GradientStyleType.HORIZONTAL, 1);
```
يتم تطبيق تأثير التدرج على تعبئة المستطيل لتحسين المظهر البصري.

### حفظ المصنف

وأخيرًا، احفظ المصنف الخاص بك مع جميع التكوينات:
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
excelBook.save(outDir + "/StyledRectangle_out.xls");
```

## التطبيقات العملية

- **التصور البياني للبيانات:** استخدم الأشكال في لوحات المعلومات لتسليط الضوء على نقاط البيانات الرئيسية.
- **تصميم القالب:** إنشاء قوالب للتقارير أو الفواتير التي تتطلب عناصر رسومية محددة.
- **إنشاء التقارير التلقائية:** قم بتعزيز العمليات الآلية عن طريق إضافة الأشكال وتصميمها برمجيًا.

## اعتبارات الأداء

عند العمل مع ملفات Excel كبيرة، ضع هذه النصائح في الاعتبار:
- قم بتقليل استخدام الذاكرة عن طريق التخلص من الكائنات التي لم تعد هناك حاجة إليها.
- استخدم هياكل البيانات الفعالة لتخزين خصائص الشكل قبل تطبيقها.
- قم بتحديث مكتبة Aspose.Cells بانتظام لتحسين الأداء.

## خاتمة

لقد تعلمتَ كيفية إضافة الأشكال وتنسيقها في مصنف Excel باستخدام Aspose.Cells لجافا. لمزيد من التعمق في إمكانياته، تعمق في عمليات أكثر تعقيدًا، مثل إضافة المخططات أو التنسيق الشرطي.

**الخطوات التالية:**
قم بتجربة أنواع وأشكال وأنماط مختلفة أو قم بدمج المكتبة في تطبيقات أكبر تتطلب إنشاء مستندات Excel ديناميكية.

## قسم الأسئلة الشائعة

1. **ما هي إصدارات Aspose.Cells المتوافقة مع Java 11؟**
   - يجب أن يكون الإصدار 25.3 والإصدارات الأحدث متوافقًا، ولكن تحقق دائمًا من ملاحظات الإصدار لمعرفة أي متطلبات محددة.
   
2. **كيف يمكنني تطبيق تعبئة التدرج على الأشكال الأخرى بالإضافة إلى المستطيلات؟**
   - الطريقة `setOneColorGradient` يمكن تطبيقها بطريقة مماثلة على أنواع الأشكال المختلفة التي تدعم التعبئة.

3. **هل يمكن لـ Aspose.Cells التعامل مع ملفات Excel الكبيرة بكفاءة؟**
   - نعم، مع إدارة الذاكرة المناسبة وتحديثات المكتبة، فإنه يتعامل جيدًا مع الملفات الكبيرة.

4. **ما هي بعض المشكلات الشائعة عند تصميم الأشكال في Aspose.Cells؟**
   - تتضمن الأخطاء الشائعة إعدادات الإحداثيات غير الصحيحة أو عدم تطبيق الأنماط قبل حفظ المصنف.

5. **كيف يمكنني المساهمة في تحسين وثائق أو ميزات Aspose.Cells؟**
   - التفاعل مع المجتمع بشأن [منتدى الدعم](https://forum.aspose.com/c/cells/9) ومشاركة التعليقات أو الاقتراحات للتحسينات.

## موارد
- **التوثيق:** استكشف الأدلة التفصيلية في [وثائق Aspose](https://reference.aspose.com/cells/java/).
- **تحميل:** الوصول إلى إصدارات Aspose.Cells من [هنا](https://releases.aspose.com/cells/java/).
- **شراء:** للحصول على الميزات الكاملة، فكر في شراء ترخيص [هنا](https://purchase.aspose.com/buy).
- **يدعم:** اطلب المساعدة على [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}