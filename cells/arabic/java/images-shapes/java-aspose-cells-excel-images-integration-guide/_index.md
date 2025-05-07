---
"date": "2025-04-08"
"description": "تعرّف على كيفية دمج الصور بسلاسة في تقارير Excel باستخدام Java وAspose.Cells. يغطي هذا الدليل كل شيء، من قراءة ملفات الصور إلى إنشاء مصنفات ديناميكية."
"title": "كيفية دمج الصور في مصنفات Excel باستخدام Java و Aspose.Cells"
"url": "/ar/java/images-shapes/java-aspose-cells-excel-images-integration-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# كيفية إنشاء مصنف Excel باستخدام Aspose.Cells والصور في Java

## مقدمة

هل تواجه صعوبة في دمج الصور في تقارير Excel باستخدام Java؟ سيوضح لك هذا الدليل الشامل كيفية الاستفادة من قوة Aspose.Cells لـ Java لإنشاء مصنفات Excel ديناميكية مليئة بالصور. سواء كنت مطورًا محترفًا أو جديدًا على Aspose.Cells، سيزودك هذا البرنامج التعليمي بالمهارات اللازمة لتحسين عروض بياناتك بفعالية.

**ما سوف تتعلمه:**
- كيفية قراءة ملفات الصور في جافا.
- إنشاء وتعديل مصنف Excel باستخدام Aspose.Cells.
- استخدام العلامات الذكية لإدراج البيانات الديناميكية.
- تحديد فئات البيانات المخصصة لإدارة البيانات المنظمة.

هل أنت مستعد لتحويل تقارير Excel الخاصة بك؟ لنبدأ بالمتطلبات الأساسية أولاً!

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن لديك ما يلي:

- **مجموعة تطوير Java (JDK):** يوصى باستخدام الإصدار 8 أو أعلى.
- **Aspose.Cells لـ Java:** سنستخدم الإصدار 25.3 في هذا البرنامج التعليمي.
- **بيئة التطوير المتكاملة:** سوف يعمل أي Java IDE مثل IntelliJ IDEA أو Eclipse.

يجب أن تكون على دراية ببرمجة Java الأساسية وأن يكون لديك بعض الفهم حول التعامل مع الملفات وهياكل البيانات.

## إعداد Aspose.Cells لـ Java

للبدء، عليك تضمين مكتبة Aspose.Cells في مشروعك. إليك كيفية القيام بذلك باستخدام Maven أو Gradle:

### مافن
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### جرادل
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

بعد إعداد التبعية، يمكنك الحصول على ترخيص لـ Aspose.Cells:

- **نسخة تجريبية مجانية:** قم بتنزيل المكتبة وتجربتها مع بعض القيود.
- **رخصة مؤقتة:** احصل على ترخيص مؤقت لاستكشاف الميزات الكاملة دون قيود.
- **شراء:** فكر في الشراء إذا كنت بحاجة إلى الوصول على المدى الطويل.

ابدأ مشروعك بإعداد عمليات الاستيراد اللازمة في ملفات فئة جافا، كما هو موضح أدناه. يُعد هذا الإعداد ضروريًا لقراءة الصور وإنشاء مصنفات Excel باستخدام Aspose.Cells.

## دليل التنفيذ

في هذا القسم، سنتناول كل ميزة خطوة بخطوة لمساعدتك في إنشاء مصنف Excel يحتوي على صور باستخدام Aspose.Cells.

### الميزة 1: قراءة ملفات الصور

أولاً، دعونا نفهم كيفية قراءة ملفات الصور من مجلد. هذا ضروري لإضافة الصور إلى مصنفنا لاحقًا.

#### ملخص
سنستخدم حزمة NIO من جافا لقراءة ملفات الصور في مصفوفات بايت. يتيح لنا هذا النهج التعامل مع مختلف صيغ الصور بسلاسة.

```java
import java.nio.file.*;
import java.io.IOException;

public class ReadImageFiles {
    public static void main(String[] args) throws IOException {
        String dataDir = "YOUR_DATA_DIRECTORY"; // تعيين مسار الدليل الخاص بك

        Path imagePath1 = Paths.get(dataDir + "sample1.png");
        byte[] photo1 = Files.readAllBytes(imagePath1);

        Path imagePath2 = Paths.get(dataDir + "sample2.jpg");
        byte[] photo2 = Files.readAllBytes(imagePath2);
    }
}
```

- **المعلمات وقيم الإرجاع:** ال `Paths.get()` الطريقة تقوم بإنشاء مسار، و `Files.readAllBytes()` يقوم بقراءة الملف في مجموعة بايتات.
- **لماذا هذا النهج؟** يؤدي استخدام NIO إلى تبسيط التعامل مع الملفات الكبيرة ويدعم تنسيقات الصور المختلفة.

### الميزة 2: إنشاء مصنف وتعديله باستخدام Aspose.Cells

الآن بعد أن أصبحت صورنا جاهزة، فلنقم بإنشاء مصنف Excel ودمجها باستخدام العلامات الذكية.

#### ملخص
سنستخدم Aspose.Cells لإنشاء مصنف، وتخصيص مظهره، وإدراج الصور بشكل ديناميكي استنادًا إلى البيانات.

```java
import com.aspose.cells.*;
import java.util.ArrayList;

public class CreateAndModifyWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        Path path1 = Paths.get(dataDir + "sample1.png");
        byte[] photo1 = Files.readAllBytes(path1);
        
        Path path2 = Paths.get(dataDir + "sample2.jpg");
        byte[] photo2 = Files.readAllBytes(path2);

        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        worksheet.getCells().setStandardHeight(35);
        worksheet.getCells().setColumnWidth(3, 20); // العمود د
        worksheet.getCells().setColumnWidth(4, 20); // العمود هـ
        worksheet.getCells().setColumnWidth(5, 40); // العمود F

        Style st = worksheet.getCells().get("D1").getStyle();
        st.getFont().setBold(true);
        
        worksheet.getCells().get("D1").putValue("Name");
        worksheet.getCells().get("E1").putValue("City");
        worksheet.getCells().get("F1").putValue("Photo");

        worksheet.getCells().get("D1").setStyle(st);
        worksheet.getCells().get("E1").setStyle(st);
        worksheet.getCells().get("F1").setStyle(st);

        worksheet.getCells().get("D2").putValue("&=Person.Name(group:normal,skip:1)");
        worksheet.getCells().get("E2").putValue("&=Person.City");
        worksheet.getCells().get("F2").putValue("&=Person.Photo(Picture:FitToCell)");

        ArrayList<Person> persons = new ArrayList<>();
        persons.add(new Person("George", "New York", photo1));
        persons.add(new Person("George", "New York", photo2));
        persons.add(new Person("Johnson", "London", photo2));
        persons.add(new Person("Simon", "Paris", photo1));
        persons.add(new Person("Henry", "Sydney", photo2));

        WorkbookDesigner designer = new WorkbookDesigner(workbook);
        designer.setDataSource("Person", persons);
        designer.process();

        workbook.save(outDir + "output.xlsx", SaveFormat.XLSX);
    }
}
```

- **العلامات الذكية:** هذه العلامات (`&=`) تسمح بالإدراج الديناميكي للبيانات، مما يجعل العملية فعالة وقابلة للتطوير.
- **فئة البيانات المخصصة:** نحن نحدد `Person` فئة لإدارة البيانات المنظمة مع خصائص مثل الاسم والمدينة والصورة.

### الميزة 3: تعريف فئة بيانات مخصصة واستخدامها

للتعامل مع بيانات صورتنا، نحتاج إلى فئة مخصصة. إليك كيفية تعريفها:

```java
class Person {
    private String m_Name;
    private String m_City;
    private byte[] m_Photo;

    public Person(String name, String city, byte[] photo) {
        this.m_Name = name;
        this.m_City = city;
        this.m_Photo = photo;
    }

    public String getName() { return m_Name; }
    public void setName(String name) { this.m_Name = name; }

    public String getCity() { return m_City; }
    public void setCity(String city) { this.m_City = city; }

    public byte[] getPhoto() { return m_Photo; }
    public void setPhoto(byte[] photo) { this.m_Photo = photo; }
}
```

- **لماذا استخدام فئة مخصصة؟** ويقوم بتنظيم البيانات بكفاءة، مما يجعل من السهل إدارتها وتوسيعها في تطبيقات أكبر.

## التطبيقات العملية

وفيما يلي بعض السيناريوهات الواقعية التي يمكنك تطبيق هذه التقنيات فيها:

1. **التقارير التجارية:** إنشاء تقارير مخصصة تلقائيًا باستخدام صور الموظفين.
2. **كتالوجات التجارة الإلكترونية:** إنشاء كتالوجات المنتجات مع الصور للمتاجر عبر الإنترنت.
3. **تخطيط الحدث:** قم بتجميع قوائم الحضور مع صور الملفات الشخصية للأحداث.
4. **المواد التعليمية:** قم بتطوير أدلة الدراسة باستخدام الوسائل البصرية المدمجة في جداول Excel.

## اعتبارات الأداء

عند العمل مع Aspose.Cells ومعالجة مجموعات بيانات كبيرة أو صور متعددة، ضع في اعتبارك النصائح التالية:

- تحسين استخدام الذاكرة عن طريق إدارة البيانات بكفاءة في Java.
- استخدم ميزات Aspose المضمنة لضغط الصور إذا لزم الأمر.
- اختبار الأداء مع أحجام مختلفة لمجموعات البيانات لضمان قابلية التوسع.

## خاتمة

باتباع هذا الدليل، ستتعلم كيفية دمج الصور في مصنفات Excel باستخدام Java وAspose.Cells. هذه التقنية قيّمة للغاية لتحسين التقارير والعروض التقديمية بمحتوى مرئي.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}