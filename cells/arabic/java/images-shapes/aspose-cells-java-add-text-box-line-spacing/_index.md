---
"date": "2025-04-08"
"description": "تعرّف على كيفية استخدام Aspose.Cells لجافا لإضافة مربعات نصية وضبط تباعد الأسطر في مصنفات Excel. حسّن عروضك التقديمية باستخدام أشكال نصية منسقة."
"title": "إضافة مربع نص وتعيين تباعد الأسطر في Excel باستخدام Aspose.Cells لـ Java"
"url": "/ar/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# إضافة مربع نص وتعيين مسافة السطور في Excel باستخدام Aspose.Cells لـ Java

## مقدمة

غالبًا ما يتطلب إنشاء تقارير Excel الديناميكية تنسيقًا نصيًا مخصصًا، مثل إضافة مربعات نصية بمسافات أسطر محددة. مع Aspose.Cells لـ Java، يصبح هذا الأمر بسيطًا وفعالًا. سيرشدك هذا البرنامج التعليمي إلى كيفية تحسين عروضك التقديمية باستخدام Aspose.Cells لـ Java لإضافة أشكال نصية منسقة.

بحلول نهاية هذا الدليل، سوف تتعلم كيفية:
- إنشاء مصنف Excel جديد والوصول إلى أوراق العمل الخاصة به
- إضافة شكل مربع نص إلى ورقة عمل
- تعيين مسافة مخصصة بين الأسطر داخل شكل النص
- احفظ المصنف المنسق بتنسيق XLSX

لنبدأ بإعداد البيئة الخاصة بك.

### المتطلبات الأساسية

قبل أن تبدأ، تأكد من أن لديك ما يلي:
- مجموعة تطوير Java (JDK) مثبتة على جهازك
- IDE أو محرر لكتابة كود Java
- نظام بناء Maven أو Gradle مُهيأ لإدارة التبعيات

سيكون من المفيد الحصول على فهم أساسي لبرمجة Java والتعرف على هياكل ملفات Excel.

## إعداد Aspose.Cells لـ Java

قم بتضمين Aspose.Cells في إدارة التبعيات الخاصة بمشروعك باستخدام Maven أو Gradle:

**مافن**

أضف كتلة التبعية التالية إلى ملفك `pom.xml` ملف:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**جرادل**

قم بتضمين هذا في `build.gradle` ملف:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

بعد ذلك، احصل على ترخيص لـ Aspose.Cells عن طريق اختيار نسخة تجريبية مجانية، أو طلب ترخيص مؤقت، أو شراء ترخيص كامل.

### تهيئة Aspose.Cells

بمجرد تضمين المكتبة في مشروعك، قم بتهيئتها داخل تطبيق Java الخاص بك:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // تهيئة مثيل لـ Workbook (يمثل ملف Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## دليل التنفيذ

### إنشاء مصنف وورقة عمل Access

ابدأ بإنشاء مصنف Excel جديد والوصول إلى ورقة العمل الأولى. هنا ستضيف مربع النص.

#### ملخص

يؤدي إنشاء مصنف جديد إلى توفير لوحة فارغة لإضافة البيانات والأشكال والتنسيق حسب الحاجة.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // إنشاء مصنف جديد (ملف Excel)
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### إضافة مربع نص إلى ورقة العمل

بعد ذلك، أضف شكل مربع نص إلى ورقة العمل التي اخترتها. يمكن أن يحتوي هذا الشكل على أي نص تحتاجه.

#### ملخص

تُعد مربعات النص أدوات متعددة الاستخدامات لتضمين نصوص مخصصة مثل الملاحظات أو الإرشادات مباشرةً داخل ورقة Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // إنشاء مصنف جديد (ملف Excel)
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // إضافة شكل مربع نص إلى ورقة العمل
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### تعيين النص في الشكل

بمجرد أن يصبح مربع النص جاهزًا، قم بتعيين المحتوى الخاص به وتنسيق النص الموجود بداخله.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // إنشاء مصنف جديد (ملف Excel)
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // إضافة شكل مربع نص إلى ورقة العمل
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // تعيين محتوى النص داخل الشكل
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### الوصول إلى فقرات النص في الشكل

يمكنك الوصول إلى فقرات فردية داخل مربع النص لتطبيق تنسيق محدد.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // إنشاء مصنف جديد (ملف Excel)
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // إضافة شكل مربع نص إلى ورقة العمل
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // تعيين محتوى النص داخل الشكل
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // الوصول إلى الفقرة الثانية في الشكل
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### تعيين المسافة بين أسطر الفقرة

تخصيص تباعد الأسطر يُحسّن سهولة القراءة. إليك كيفية ضبطه:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // إنشاء مصنف جديد (ملف Excel)
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // إضافة شكل مربع نص إلى ورقة العمل
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // تعيين محتوى النص داخل الشكل
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // الوصول إلى الفقرة الثانية في الشكل
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // ضبط مسافة الأسطر إلى 20 نقطة
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // تكوين المسافة قبل وبعد الفقرة
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### حفظ المصنف

وأخيرًا، احفظ المصنف الخاص بك باستخدام مربع النص المضاف والمنسق حديثًا.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // إنشاء مصنف جديد (ملف Excel)
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // إضافة شكل مربع نص إلى ورقة العمل
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // تعيين محتوى النص داخل الشكل
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // الوصول إلى الفقرة الثانية في الشكل
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // ضبط مسافة الأسطر إلى 20 نقطة
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // تكوين المسافة قبل وبعد الفقرة
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // حفظ المصنف
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## خاتمة

لقد نجحت في تعلّم كيفية إضافة مربع نص وضبط تباعد الأسطر في مصنف Excel باستخدام Aspose.Cells لـ Java. هذا يُحسّن قدرتك على إنشاء تقارير ديناميكية وجذابة بصريًا.

## توصيات الكلمات الرئيسية
- "Aspose.Cells لـ Java"
- "إضافة مربع نص في Excel"
- "تعيين تباعد الأسطر في Excel"
- "مصنف إكسل مع نص منسق"
- "Java و Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}