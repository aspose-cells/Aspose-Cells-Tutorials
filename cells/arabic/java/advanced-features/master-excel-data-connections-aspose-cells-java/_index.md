---
date: '2025-12-27'
description: تعلم كيفية تغيير مصدر بيانات Excel برمجيًا باستخدام Aspose.Cells للغة
  Java، وتعديل اتصالات بيانات Excel، وأتمتة سير عملك.
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: كيفية تغيير مصدر بيانات Excel باستخدام Aspose.Cells للـ Java
url: /ar/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تغيير مصدر بيانات Excel باستخدام Aspose.Cells for Java

## المقدمة
هل تواجه صعوبة في **تغيير مصدر بيانات Excel** وتعديل اتصالات البيانات داخل ملفات Excel برمجياً؟ هذا الدليل الشامل مخصص للمطورين الذين يرغبون في أتمتة خطوط تقاريرهم باستخدام مكتبة **Aspose.Cells for Java** القوية. سنرشدك إلى تحميل مصنف Excel، تحديث الاتصال الخارجي، وحفظ التغييرات—كل ذلك باستخدام كود Java.

### ما ستتعلمه
- كيفية إعداد Aspose.Cells for Java في Maven أو Gradle.  
- **Load Excel workbook Java** – قراءة ملف موجود إلى الذاكرة.  
- **Modify Excel data connections** – تحديث اسم الاتصال، مسار ODC، وأمر SQL.  
- **Save Excel workbook Java** – كتابة المصنف المحدث إلى القرص.  

لنتأكد من أن لديك كل ما تحتاجه قبل أن نبدأ.

## إجابات سريعة
- **ما هي المكتبة الأساسية؟** Aspose.Cells for Java.  
- **أي طريقة تُحمِّل المصنف؟** `new Workbook(filePath)`.  
- **كيف يمكنني تحديث سلسلة الاتصال؟** استخدم `DBConnection.setConnectionInfo(...)`.  
- **هل يمكنني تغيير مسار ملف ODC؟** نعم، عبر `ExternalConnection.setOdcFile(...)`.  
- **هل أحتاج إلى ترخيص للإنتاج؟** الترخيص التجاري يزيل حدود التقييم.

## المتطلبات المسبقة
قبل أن نبدأ، تحقق من أن لديك ما يلي:

### المكتبات المطلوبة
إصدار Aspose.Cells for Java 25.3 أو أحدث يوفر واجهات برمجة التطبيقات المستخدمة في هذا البرنامج التعليمي.

### إعداد البيئة
- تثبيت Java Development Kit (JDK).  
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse أو NetBeans.

### المتطلبات المعرفية
الإلمام بـ Java، Maven أو Gradle، ومفاهيم SQL الأساسية سيساعدك على المتابعة بسلاسة.

## إعداد Aspose.Cells for Java
للبدء في استخدام Aspose.Cells، أضف المكتبة إلى مشروعك:

**إعداد Maven**  
أضف الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**إعداد Gradle**  
أدرج السطر التالي في `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### خطوات الحصول على الترخيص
توفر Aspose.Cells نسخة تجريبية مجانية لتقييم المكتبة قبل الشراء:

- زر [صفحة التجربة المجانية](https://releases.aspose.com/cells/java/) وحمّل حزمة التقييم.  
- للاستخدام الكامل، اشترِ ترخيصًا من [بوابة الشراء](https://purchase.aspose.com/buy).  
- هل تحتاج وصولًا مؤقتًا؟ اطلب [ترخيصًا مؤقتًا](https://purchase.aspose.com/temporary-license/).

بمجرد الإشارة إلى المكتبة وترخيصها، ستكون جاهزًا للبرمجة.

## دليل التنفيذ

### الميزة 1: تحميل المصنف من ملف
**ما الذي يفعله هذا الخطوة؟** تُظهر كيفية **load Excel workbook Java** حتى تتمكن من العمل مع اتصالات البيانات الخاصة به.

#### تعليمات خطوة بخطوة
**تحديد دليل البيانات** – أخبر البرنامج بمكان وجود ملف المصدر:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
تأكد من وجود `DataConnection.xlsx` في ذلك المجلد.

**تحميل المصنف** – إنشاء كائن `Workbook`:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
الآن تمثل نسخة `Workbook` ملف Excel الخاص بك في الذاكرة.

### الميزة 2: تعديل اتصال البيانات في المصنف
**لماذا التعديل؟** تحديث الاتصال الخارجي يتيح لك **تغيير مصدر بيانات Excel** دون فتح الملف يدويًا.

#### تعليمات خطوة بخطوة
**الوصول إلى اتصال البيانات** – استرجاع أول اتصال (يمكنك التكرار للاتصالات المتعددة):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` تُعيد مجموعة من جميع الاتصالات، مما يتيح لك **modify excel data connections** بشكل فردي.

**تعديل خصائص الاتصال** – تغيير الاسم، ملف ODC، نوع الأمر، وتعليمة SQL:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

تحويل إلى `DBConnection` لإعدادات قاعدة البيانات الخاصة:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
هنا تقوم **update excel external connection** بتفاصيل مثل استعلام SQL وسلسلة الاتصال.

### الميزة 3: حفظ المصنف إلى ملف
**ماذا يحدث بعد ذلك؟** بعد تحديث الاتصال، تحتاج إلى **save Excel workbook Java** حتى تبقى التغييرات محفوظة.

#### تعليمات خطوة بخطوة
**تحديد دليل الإخراج** – حيث سيُكتب الملف المعدل:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**حفظ المصنف** – كتابة المصنف مرة أخرى إلى القرص:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
طريقة `save()` تُكمل عملية **change excel data source**.

## تطبيقات عملية
تعديل اتصالات بيانات Excel برمجياً يفتح العديد من الأبواب:

1. **التقارير الآلية** – إنشاء تقارير تُجلب دائمًا أحدث البيانات من قاعدة البيانات.  
2. **مزامنة البيانات** – الحفاظ على تزامن المصنفات مع الأنظمة الحية دون تحديث يدوي.  
3. **لوحات معلومات ديناميكية** – بناء لوحات تُظهر مؤشرات الوقت الحقيقي.

دمج Aspose.Cells مع منصات CRM أو ERP أو BI يمكن أن يقلل الجهد اليدوي بشكل كبير.

## اعتبارات الأداء
عند التعامل مع مصنفات كبيرة أو مجموعات نتائج ضخمة:

- عالج البيانات على دفعات لتجنب ارتفاع الذاكرة.  
- حسّن استعلامات SQL للسرعة.  
- حرّر الموارد فورًا؛ استدعِ `workbook.dispose()` إذا لم تعد بحاجة إلى الكائن.

هذه الممارسات تضمن بقاء تطبيقك مستجيبًا أثناء **changing Excel data source**.

## الخلاصة
لقد تعلمت الآن كيفية **change Excel data source** عن طريق تحميل مصنف، **modify excel data connections**، وحفظ الملف المحدث باستخدام **Aspose.Cells for Java**. هذه القدرة تمكّنك من أتمتة سير العمل القائم على البيانات والحفاظ على تزامن ملفات Excel مع الأنظمة الخارجية.

### الخطوات التالية
- جرّب عدة اتصالات باستخدام حلقة فوق `workbook.getDataConnections()`.  
- استكشف ميزات Aspose.Cells الأخرى مثل إنشاء المخططات، تنسيق الخلايا، ومعالجة الجداول المحورية.

هل أنت مستعد لتعزيز أتمتتك؟ نفّذ هذه الشفرات اليوم وشاهد إنتاجيتك ترتفع!

## الأسئلة المتكررة

**س1: كيف يمكنني التعامل مع اتصالات بيانات متعددة في مصنف؟**  
ج1: استخدم `workbook.getDataConnections().get(index)` داخل حلقة للوصول إلى كل اتصال على حدة.

**س2: هل يمكنني تعديل خصائص أخرى لملف Excel باستخدام Aspose.Cells Java؟**  
ج2: بالتأكيد! Aspose.Cells يدعم تنسيق الخلايا، إدارة أوراق العمل، إنشاء المخططات، وأكثر من ذلك.

**س3: ماذا لو فشل أمر SQL في التنفيذ؟**  
ج3: تحقق من سلسلة الاتصال، افحص أذونات قاعدة البيانات، وراجع تفاصيل الاستثناء للحصول على مؤشرات.

**س4: أين يمكنني الحصول على دعم لمشكلات Aspose.Cells؟**  
ج4: زر [منتدى Aspose](https://forum.aspose.com/c/cells/9) لطرح الأسئلة أو تصفح الحلول الموجودة.

**س5: هل هناك قيود في نسخة التجربة المجانية؟**  
ج5: نسخة التقييم تضيف علامات مائية وقد تحد من سعة المعالجة. اشترِ ترخيصًا للاستخدام غير المقيد.

## الموارد
- **الوثائق:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **التنزيل:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2025-12-27  
**تم الاختبار مع:** Aspose.Cells Java 25.3  
**المؤلف:** Aspose