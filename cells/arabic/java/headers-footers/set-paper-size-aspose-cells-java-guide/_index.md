---
"date": "2025-04-09"
"description": "تعرّف على كيفية ضبط واسترجاع أحجام الورق مثل A4 وA3 وA2 وLetter باستخدام Aspose.Cells لـ Java. يغطي هذا الدليل كل شيء، من الإعداد إلى الإعدادات المتقدمة."
"title": "إعداد حجم الورقة الرئيسي في Aspose.Cells Java - تكوين الرؤوس والتذييلات بسهولة"
"url": "/ar/java/headers-footers/set-paper-size-aspose-cells-java-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إعداد حجم الورقة الرئيسي في Aspose.Cells Java: تكوين الرؤوس والتذييلات بسهولة

## كيفية ضبط حجم الورق باستخدام Aspose.Cells Java: دليل المطور

**مقدمة**

هل تواجه صعوبة في ضبط أحجام ورق مختلفة لجداول البيانات في تطبيقات جافا؟ مع Aspose.Cells لجافا، يمكنك بسهولة إدارة وضبط أبعاد ورق مختلفة مثل A2 وA3 وA4 وLetter. يرشدك هذا الدليل إلى كيفية استخدام Aspose.Cells لإدارة إعدادات الورق بكفاءة.

**ما سوف تتعلمه:**
- قم بتعيين أحجام ورق مختلفة باستخدام Aspose.Cells في تطبيق Java.
- احصل على عرض وارتفاع هذه الأحجام الورقية بالبوصة.
- قم بتحسين تطبيقاتك باستخدام نصائح الأداء الخاصة بـ Aspose.Cells.

دعونا نستكشف كيف يمكنك الاستفادة من هذه المكتبة القوية لمشاريعك!

**المتطلبات الأساسية**

قبل أن نبدأ، تأكد من أن لديك:
- **مجموعة تطوير Java (JDK):** تم تثبيت الإصدار 8 أو أعلى على جهازك.
- **Aspose.Cells لمكتبة Java:** تأكد من تضمين الإصدار 25.3 في تبعيات مشروعك.
- **إعداد IDE:** استخدم IDE مثل IntelliJ IDEA أو Eclipse لكتابة وتنفيذ كود Java.

تأكد من أن لديك فهمًا أساسيًا لبرمجة Java، بالإضافة إلى الإلمام بأدوات بناء Maven أو Gradle إذا كنت تدير التبعيات عبر هذه الأنظمة.

**إعداد Aspose.Cells لـ Java**

للبدء، قم بتضمين مكتبة Aspose.Cells في مشروعك باستخدام أدوات إدارة التبعيات:

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

قم بتنزيل نسخة تجريبية مجانية من [موقع Aspose](https://releases.aspose.com/cells/java/) أو الحصول على ترخيص مؤقت للوصول إلى الميزات الكاملة.

### دليل تنفيذ الميزة

#### ضبط حجم الورق إلى A2

**ملخص**
توضح هذه الميزة ضبط حجم ورقة العمل إلى A2 واسترجاع أبعادها بالبوصة. مفيدة لإنشاء تقارير تتطلب أبعادًا محددة.

**دليل خطوة بخطوة:**
1. **تهيئة المصنف وورقة العمل**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeA2 {
       public static void main(String[] args) throws Exception {
           // إنشاء مثيل جديد للمصنف
           Workbook wb = new Workbook();

           // الوصول إلى ورقة العمل الأولى في المصنف
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **ضبط حجم الورق**
   ```java
           // ضبط حجم الورق إلى A2
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_A_2);
   ```
3. **استرجاع وطباعة الأبعاد**
   ```java
           // استرداد وطباعة عرض وارتفاع الورق بالبوصة
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // تحويل النقاط إلى بوصات
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("A2 Paper Width: " + paperWidth + " inches");
           System.out.println("A2 Paper Height: " + paperHeight + " inches");
       }
   }
   ```
**المعلمات وأغراض الطريقة**
- `setPaperSize(PaperSizeType.PAPER_A_2)`:تعيين حجم الورق إلى A2.
- `getPaperWidth()` و `getPaperHeight()`:استرجاع الأبعاد بالنقاط، وتحويلها إلى بوصات للعرض.

#### ضبط حجم الورق إلى A3

**ملخص**
على غرار إعداد A2، تعمل هذه الميزة على ضبط إعدادات ورق ورقة العمل الخاصة بك إلى A3.

**دليل خطوة بخطوة:**
1. **تهيئة المصنف وورقة العمل**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeA3 {
       public static void main(String[] args) throws Exception {
           // إنشاء مثيل جديد للمصنف
           Workbook wb = new Workbook();

           // الوصول إلى ورقة العمل الأولى في المصنف
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **ضبط حجم الورق**
   ```java
           // ضبط حجم الورق إلى A3
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_A_3);
   ```
3. **استرجاع وطباعة الأبعاد**
   ```java
           // استرداد وطباعة عرض وارتفاع الورق بالبوصة
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // تحويل النقاط إلى بوصات
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("A3 Paper Width: " + paperWidth + " inches");
           System.out.println("A3 Paper Height: " + paperHeight + " inches");
       }
   }
   ```
#### ضبط حجم الورق إلى A4

**ملخص**
يتناول هذا القسم تعيين أبعاد ورقة العمل إلى A4، وهو متطلب شائع لإنشاء المستندات.

**دليل خطوة بخطوة:**
1. **تهيئة المصنف وورقة العمل**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeA4 {
       public static void main(String[] args) throws Exception {
           // إنشاء مثيل جديد للمصنف
           Workbook wb = new Workbook();

           // الوصول إلى ورقة العمل الأولى في المصنف
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **ضبط حجم الورق**
   ```java
           // ضبط حجم الورق إلى A4
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_A_4);
   ```
3. **استرجاع وطباعة الأبعاد**
   ```java
           // استرداد وطباعة عرض وارتفاع الورق بالبوصة
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // تحويل النقاط إلى بوصات
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("A4 Paper Width: " + paperWidth + " inches");
           System.out.println("A4 Paper Height: " + paperHeight + " inches");
       }
   }
   ```
#### ضبط حجم الورق إلى Letter

**ملخص**
تتيح لك هذه الميزة تكوين حجم ورقة العمل الخاصة بك إلى تنسيق Letter القياسي، المستخدم على نطاق واسع في أمريكا الشمالية.

**دليل خطوة بخطوة:**
1. **تهيئة المصنف وورقة العمل**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeLetter {
       public static void main(String[] args) throws Exception {
           // إنشاء مثيل جديد للمصنف
           Workbook wb = new Workbook();

           // الوصول إلى ورقة العمل الأولى في المصنف
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **ضبط حجم الورق**
   ```java
           // ضبط حجم الورق إلى Letter
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_LETTER);
   ```
3. **استرجاع وطباعة الأبعاد**
   ```java
           // استرداد وطباعة عرض وارتفاع الورق بالبوصة
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // تحويل النقاط إلى بوصات
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("Letter Paper Width: " + paperWidth + " inches");
           System.out.println("Letter Paper Height: " + paperHeight + " inches");
       }
   }
   ```
**التطبيقات العملية**
- **طباعة التقارير:** قم بتكوين التقارير تلقائيًا للطباعة على أحجام قياسية مختلفة مثل A2 أو A3 أو A4 أو Letter.
- **أنظمة إدارة المستندات:** ضبط وإدارة تنسيقات المستندات في حلول البرامج المتكاملة.
- **قوالب مخصصة:** إنشاء قوالب تتكيف مع متطلبات حجم الورق المحددة.

**اعتبارات الأداء**
- **إدارة الذاكرة:** دائما قريبة `Workbook` الحالات بعد الاستخدام لتحرير الموارد.
- **معالجة الدفعات:** قم بمعالجة مستندات متعددة بكفاءة من خلال إعداد منطق المعالجة الدفعية.

**خاتمة**
يُعدّ إتقان تحديد أحجام أوراق العمل واسترجاعها باستخدام Aspose.Cells في Java مهارةً قيّمةً للمطورين الذين يعملون في مجال إنشاء المستندات. يضمن هذا الدليل أن تطبيقاتك تلبي المتطلبات المحددة بسلاسة.

بعد ذلك، استكشف المزيد من ميزات Aspose.Cells أو انغمس في التكوينات المتقدمة.

**الأسئلة الشائعة:**
- **كيف أقوم بتحويل الأبعاد من النقاط إلى البوصات؟**
  قسّم عدد النقاط على 72.
- **هل يمكنني استخدام هذا الدليل للتطبيقات التجارية؟**
  نعم، طالما أنك ملتزم بشروط ترخيص Aspose.Cells.

**قراءة إضافية:**
- [توثيق Aspose.Cells](https://docs.aspose.com/cells/java/)
- [أساسيات برمجة جافا](https://docs.oracle.com/javase/tutorial/index.html)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}