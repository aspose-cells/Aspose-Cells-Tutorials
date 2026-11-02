---
date: '2026-09-02'
description: تعلم كيفية إنشاء دفاتر عمل Excel تحتوي على صور قابلة للنقر باستخدام Aspose.Cells
  for Java، وإضافة روابط تشعبية للصور لإنشاء جداول بيانات تفاعلية.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: تعلم كيفية إنشاء دفاتر عمل Excel تحتوي على صور قابلة للنقر باستخدام
  Aspose.Cells for Java، وإضافة hyperlinks، screen tips، وoptimizing performance في
  بضع أسطر من code.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: إنشاء صورة قابلة للنقر في Excel باستخدام Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: إنشاء صورة قابلة للنقر في Excel باستخدام Aspose.Cells for Java
url: /ar/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء صورة Excel قابلة للنقر باستخدام Aspose.Cells للـ Java

## المقدمة

إذا كنت ترغب في **إنشاء صورة Excel قابلة للنقر** تسمح للمستخدمين بالانتقال إلى مواقع ويب أو مستندات أو موارد أخرى بنقرة واحدة، فأنت في المكان الصحيح. في هذا الدرس سنستعرض كيف يتيح لك Aspose.Cells للـ Java **إضافة كائنات صورة Excel مع ارتباط تشعبي**، وتكوين تلميحات الشاشة، والحفاظ على جداول البيانات جميلة وعملية في آنٍ واحد.

### ما ستتعلمه
- تهيئة دفتر عمل Aspose.Cells في Java.  
- إدراج صورة وتحويلها إلى ارتباط تشعبي قابل للنقر.  
- الطرق الأساسية مثل `addHyperlink`، `setPlacement`، و `setScreenTip`.  
- أفضل الممارسات للأداء والترخيص.

## الإجابات السريعة
- **ما المكتبة المطلوبة؟** Aspose.Cells for Java.  
- **هل يمكنني استخدام ملفات .xlsx؟** نعم – الـ API يعمل مع كل من .xls و .xlsx.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية تعمل للتقييم؛ الترخيص الدائم مطلوب للإنتاج.  
- **كم عدد أسطر الكود؟** حوالي 20 سطرًا لإضافة صورة قابلة للنقر.  
- **هل هو آمن للخطوط المتعددة؟** كائنات Workbook ليست آمنة للخطوط المتعددة؛ أنشئ نسخًا منفصلة لكل خيط.  
- **هل يمكنني إضافة تلميح شاشة في Excel؟** نعم – استخدم `Hyperlink.setScreenTip()` لعرض نص مفيد عند التحويم.

## كيفية إنشاء صورة Excel قابلة للنقر باستخدام Aspose.Cells للـ Java

تقوم بإنشاء دفتر عمل Excel قابل للنقر بتحميل أو إنشاء `Workbook`، إدراج كائن `Picture`، إرفاق `Hyperlink` بهذه الصورة، اختيارياً ضبط تلميح الشاشة، وأخيراً حفظ الملف. يتولى الـ API كل تفاصيل XML منخفضة المستوى في Excel، لذا تحتاج فقط إلى بضع أسطر بسيطة من كود Java.

### المتطلبات المسبقة
قبل البدء، تأكد من وجود:

- **Aspose.Cells للـ Java** (الإصدار 25.3 أو أحدث).  
- **JDK 8+** مثبت.  
- بيئة تطوير متكاملة (IntelliJ IDEA، Eclipse، أو NetBeans) و Maven أو Gradle لإدارة التبعيات.  

### المكتبات المطلوبة
أضف Aspose.Cells إلى مشروعك:

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### الحصول على الترخيص
Aspose.Cells تجاري، لكن يمكنك البدء بنسخة تجريبية مجانية أو طلب ترخيص مؤقت:

- النسخة التجريبية المجانية: حمّل من [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- ترخيص مؤقت: اطلب عبر [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- الشراء: للاستخدام طويل الأمد، زر [Aspose Purchase](https://purchase.aspose.com/buy).

### التهيئة الأساسية
فئة `Workbook` تمثل ملف Excel كامل في الذاكرة. تقوم بإنشائها، ثم الحصول على مرجع إلى الورقة الأولى. `Worksheet` تمثل ورقة واحدة داخل دفتر العمل.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## تنفيذ خطوة بخطوة

### الخطوة 1: إعداد دفتر العمل الخاص بك
نبدأ بإنشاء دفتر عمل جديد واختيار الورقة الأولى.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### الخطوة 2: إدراج تسمية وضبط حجم الخلية
أضف تسمية وصفية ومنح الخلية مساحة كافية للصورة.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### الخطوة 3: إضافة الصورة
`Picture` تمثل كائن صورة موضع على ورقة العمل.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*نصيحة*: استبدل `"path/to/aspose-logo.jpg"` بالمسار الفعلي لملف الصورة الخاص بك.

### الخطوة 4: ضبط الموضع وإضافة الارتباط التشعبي
`Hyperlink` يحدد رابطًا مرتبطًا بخلية أو شكل أو صورة، مما يتيح التنقل عند النقر.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### الخطوة 5: تعيين تلميح شاشة وحفظ دفتر العمل
قدم تلميحًا مفيدًا واكتب دفتر العمل إلى القرص.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## لماذا إضافة ارتباط تشعبي لصورة Excel؟

إدراج صورة قابلة للنقر يتيح لك تحويل عناصر العلامة التجارية أو الأيقونات أو المخططات إلى نقاط تنقل مباشرة، مما يقلل عدد النقرات المطلوبة للوصول إلى المحتوى المرتبط. يعزز هذا النهج كفاءة المستخدم في لوحات التحكم التسويقية، الأدلة التقنية، وأوراق العمل التعليمية.

## كيفية إضافة تلميح شاشة في Excel

تضيف تلميح الشاشة عن طريق استدعاء `hyperlink.setScreenTip("Your tip here")` على كائن `Hyperlink` المرفق بالصورة. يظهر التلميح عندما يمر المؤشر فوق الصورة، موفرًا إرشادًا سياقيًا دون إغراق الورقة بالمعلومات.

## نصائح استكشاف الأخطاء وإصلاحها
- **أخطاء مسار الصورة** – تحقق مرة أخرى من موقع الملف وتأكد أن التطبيق لديه صلاحيات القراءة.  
- **الترخيص غير مفعّل** – إذا انتهت النسخة التجريبية، قد تتوقف الروابط التشعبية عن العمل؛ فعّل ترخيصًا صالحًا باستخدام `License.setLicense`.  
- **الارتباط التشعبي غير قابل للنقر** – تحقق من أن `PlacementType` للصورة مضبوط على `FREE_FLOATING`.

## التطبيقات العملية
إدراج صور قابلة للنقر مفيد في العديد من السيناريوهات:

1. **تقارير التسويق** – ربط شعارات العلامة التجارية بصفحات المنتجات.  
2. **الوثائق التقنية** – إرفاق مخططات تفتح مخططات تفصيلية.  
3. **أوراق العمل التعليمية** – تحويل الأيقونات إلى اختصارات للفيديوهات الإضافية.  
4. **لوحات معلومات المشروع** – جعل أيقونات الحالة تفتح متتبعات المهام ذات الصلة.

## اعتبارات الأداء
- حافظ على حجم ملفات الصور معقولًا؛ الصور الكبيرة تزيد من استهلاك الذاكرة في دفتر العمل.  
- تخلص من الكائنات غير المستخدمة (`workbook.dispose()`) عند معالجة العديد من الملفات في حلقة.  
- قم بالترقية إلى أحدث إصدار من Aspose.Cells لتحسين الأداء وإصلاح الأخطاء.

## الخلاصة
أنت الآن تعرف كيف تضيف ارتباطًا تشعبيًا إلى الصور في Excel باستخدام Aspose.Cells للـ Java، مما يتيح لك **إنشاء صورة Excel قابلة للنقر** تكون أكثر غنى وتفاعلية. جرّب روابط مختلفة، تلميحات شاشة، ووضعيات صور لتناسب احتياجات تقاريرك. بعد ذلك، قد تستكشف إضافة روابط تشعبية إلى الأشكال أو أتمتة إدراج الصور على نطاق واسع عبر أوراق عمل متعددة.

## الأسئلة المتكررة

**س:** ما هو الحد الأقصى لحجم الصورة المدعوم من قبل Aspose.Cells للـ Java؟  
**ج:** لا يوجد حد صارم، لكن الصور الكبيرة قد تؤثر على الأداء وتزيد حجم الملف.

**س:** هل يمكنني استخدام هذه الميزة مع ملفات .xlsx؟  
**ج:** نعم، الـ API يعمل مع صيغ `.xls` و `.xlsx`.

**س:** كيف يجب أن أتعامل مع الاستثناءات عند إضافة الروابط التشعبية؟  
**ج:** احط الكود بكتلة try‑catch وسجل تفاصيل `Exception` لتشخيص مشاكل المسار أو الترخيص.

**س:** هل يمكن إزالة الارتباط التشعبي من صورة بعد إضافتها؟  
**ج:** نعم – احصل على كائن `Picture` واستدعِ `pic.getHyperlink().remove()` أو احذف الصورة من المجموعة.

**س:** لماذا قد لا يعمل الارتباط التشعبي كما هو متوقع؟  
**ج:** الأسباب الشائعة تشمل سلسلة URL غير صحيحة، أو عدم وجود بادئة `http://`/`https://`، أو نسخة تجريبية غير مرخصة تعطل بعض الميزات.

## موارد إضافية
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Purchase and trial:** زر [Aspose Purchase](https://purchase.aspose.com/buy) أو [Temporary License Page](https://purchase.aspose.com/temporary-license/) للحصول على خيارات الترخيص.  
- **Support forum:** للحصول على المساعدة، راجع [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Last updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java 25.3  
**Author:** Aspose

## الدروس ذات الصلة

- [كيفية إنشاء روابط تشعبية في Excel باستخدام Aspose.Cells للـ Java - دليل خطوة بخطوة](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [كيفية تنسيق خلايا Excel وإضافة روابط تشعبية باستخدام Aspose.Cells للـ Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [إضافة صورة إلى تعليق Excel باستخدام Aspose.Cells للـ Java: دليل كامل](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}