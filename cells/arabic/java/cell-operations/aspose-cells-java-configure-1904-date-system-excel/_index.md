---
date: '2026-02-22'
description: تعلم كيفية تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells للغة
  Java، وضبط تنسيق تاريخ Excel، وتحويل نظام Excel 1904 بكفاءة.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells Java
url: /ar/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells Java

إدارة البيانات التاريخية في Excel يمكن أن تكون صعبة لأن Excel يدعم نظامي تاريخ مختلفين. **في هذا الدرس ستتعلم كيفية تغيير نظام تاريخ Excel إلى صيغة 1904 باستخدام Aspose.Cells للغة Java**، مما يجعل التعامل مع التواريخ القديمة سهلًا. سنستعرض كيفية تهيئة مصنف، تمكين نظام تاريخ 1904، وحفظ التغيير.

## إجابات سريعة
- **ماذا يفعل نظام التاريخ 1904؟** يبدأ العد من 1 يناير 1904، مما يغيّر جميع التواريخ بمقدار 1462 يومًا مقارنةً بالنظام الافتراضي 1900.  
- **لماذا نستخدم Aspose.Cells لتغيير نظام التاريخ؟** يوفر واجهة برمجة تطبيقات بسيطة تعمل دون الحاجة إلى تثبيت Excel ويدعم الملفات الكبيرة.  
- **ما إصدارات Java المدعومة؟** JDK 8 أو أحدث.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتقييم؛ الترخيص يزيل حدود الاستخدام.  
- **هل يمكنني التحويل مرة أخرى إلى نظام 1900 لاحقًا؟** نعم، فقط استدعِ `setDate1904(false)`.

## ما هو نظام التاريخ 1904 في Excel؟
كان نظام التاريخ 1904 يُستخدم أصلاً في إصدارات Excel المبكرة على نظام Macintosh. يعد الأيام من 1 يناير 1904، وهو مفيد للتوافق مع جداول البيانات القديمة وبعض النماذج المالية.

## لماذا نغير نظام تاريخ Excel باستخدام Aspose.Cells؟
- **توافق عابر للمنصات** – يعمل على Windows وLinux وmacOS.  
- **لا يلزم تثبيت Excel** – مثالي للمعالجة على الخادم.  
- **أداء عالي** – يتعامل مع مصنفات كبيرة بأقل استهلاك للذاكرة.  

## المتطلبات المسبقة
- مجموعة تطوير Java (JDK) 8 أو أعلى.  
- Maven أو Gradle لإدارة التبعيات.  
- معرفة أساسية ببرمجة Java.  

## إعداد Aspose.Cells للغة Java

### Maven
أضف التبعية التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
أدرج السطر التالي في ملف `build.gradle` الخاص بك:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### الحصول على الترخيص
تقدم Aspose نسخة تجريبية مجانية، ترخيصًا مؤقتًا، وترخيصًا تجاريًا كاملًا. يمكنك البدء بالـ[نسخة التجريبية المجانية](https://releases.aspose.com/cells/java/) أو الحصول على ترخيص مؤقت من [صفحة الترخيص المؤقت](https://purchase.aspose.com/temporary-license/).

## تغيير نظام تاريخ Excel باستخدام Aspose.Cells Java

فيما يلي دليل خطوة بخطوة يغيّر **نظام تاريخ Excel** فعليًا. كل خطوة تتضمن شرحًا مختصرًا يليه الكود المطلوب.

### الخطوة 1: تهيئة وتحميل المصنف
أولًا، أنشئ كائن `Workbook` يشير إلى ملف Excel الحالي لديك.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### الخطوة 2: تمكين نظام التاريخ 1904
استخدم إعدادات المصنف لتبديل نظام التاريخ.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**نصيحة:** يمكنك أيضًا استدعاء `setDate1904(false)` لاحقًا إذا أردت العودة إلى النظام السابق.

### الخطوة 3: حفظ المصنف المعدل
أخيرًا، اكتب التغييرات إلى ملف جديد (أو استبدل الأصلي).

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **ملاحظة:** يستخدم الكود أعلاه اسم الفئة `tWorkbook` كما هو موضح أصلاً. تأكد من أن هذا الخطأ المطبعي يتطابق مع تسمية مشروعك أو صححه إلى `Workbook` إذا لزم الأمر.

## تعيين تاريخ Excel برمجيًا (الكلمة المفتاحية الثانوية)
إذا احتجت لتعديل قيم خلايا فردية بعد تغيير النظام، يمكنك استخدام `Cells.get(i, j).putValue(Date)` حيث سيتم تفسير التاريخ وفقًا للنظام النشط.

## تحويل نظام Excel 1904 إلى 1900 (الكلمة المفتاحية الثانوية)
للعودة، ما عليك سوى استدعاء:

```java
workbook.getSettings().setDate1904(false);
```

ثم احفظ المصنف مرة أخرى.

## تطبيقات عملية
1. **أرشفة البيانات** – الحفاظ على الطوابع الزمنية القديمة عند ترحيل جداول بيانات قديمة من Mac.  
2. **تقارير عابرة للمنصات** – إنشاء تقارير يمكن فتحها على كل من Windows وmacOS دون اختلافات في التواريخ.  
3. **نمذجة مالية** – مواءمة حسابات التاريخ مع نماذج مالية قديمة تتوقع نظام 1904.

## اعتبارات الأداء
- حدّ من عمليات المصنف في جلسة واحدة للحفاظ على استهلاك الذاكرة منخفضًا.  
- استخدم ضبط جمع القمامة في Java للملفات الكبيرة جدًا.  

## الأسئلة المتكررة

**س: ما الفرق بين نظامي التاريخ 1900 و1904؟**  
ج: يبدأ نظام 1900 من 1 يناير 1900، بينما يبدأ نظام 1904 من 1 يناير 1904، ما يغيّر جميع التواريخ بمقدار 1462 يومًا.

**س: هل يمكنني تغيير نظام التاريخ لمصنف مفتوح حاليًا في Excel؟**  
ج: نعم، لكن يجب إغلاق الملف في Excel أولًا؛ وإلا سيفشل عملية الحفظ.

**س: هل أحتاج إلى ترخيص لاستخدام `setDate1904`؟**  
ج: الطريقة تعمل في النسخة التجريبية المجانية، لكن الترخيص الكامل يزيل قيود التقييم.

**س: هل يمكن تغيير نظام التاريخ لورقة عمل واحدة فقط؟**  
ج: لا، نظام التاريخ هو إعداد على مستوى المصنف؛ يطبق على جميع أوراق العمل.

**س: كيف يمكنني التحقق من أن نظام التاريخ قد تم تغييره؟**  
ج: افتح الملف المحفوظ في Excel، انتقل إلى **ملف → خيارات → متقدم**، وتأكد من تحديد خانة **"استخدام نظام تاريخ 1904"**.

## الخلاصة
الآن تعرف كيف **تغيير نظام تاريخ Excel** إلى 1904 باستخدام Aspose.Cells للغة Java، وكيفية تعيين صيغ تاريخ Excel، وكيفية العودة إذا لزم الأمر. دمج هذه المقاطع في خطوط معالجة البيانات يضمن توافق التواريخ عبر المنصات.

---

**آخر تحديث:** 2026-02-22  
**تم الاختبار مع:** Aspose.Cells 25.3 للغة Java  
**المؤلف:** Aspose  

**الموارد**
- **الوثائق:** [مرجع Aspose.Cells Java](https://reference.aspose.com/cells/java/)
- **التنزيل:** [إصدارات Aspose.Cells](https://releases.aspose.com/cells/java/)
- **شراء الترخيص:** [شراء Aspose.Cells](https://purchase.aspose.com/buy)
- **النسخة التجريبية المجانية:** [ابدأ النسخة التجريبية المجانية](https://releases.aspose.com/cells/java/)
- **الترخيص المؤقت:** [احصل على ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)
- **منتدى الدعم:** [دعم Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}