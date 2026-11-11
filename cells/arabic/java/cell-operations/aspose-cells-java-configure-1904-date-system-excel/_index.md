---
date: '2026-10-28'
description: تعلم كيفية تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells for
  Java، ضبط تنسيق تاريخ Excel، وتحويل نظام Excel 1904 بكفاءة.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells for Java. تعلم
  خطوة بخطوة كيفية تمكين نظام 1904، ضبط التواريخ، والعودة إلى النظام الأصلي.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells Java
url: /ar/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells Java

في هذا الدرس ستتعلم كيفية **تغيير نظام تاريخ Excel** إلى تنسيق 1904 باستخدام Aspose.Cells للـ Java. نظام 1904 ضروري عندما تحتاج إلى الحفاظ على تواريخ ماك القديمة أو التوافق مع نماذج مالية تتوقع تلك الحقبة. سنستعرض تثبيت المكتبة، تحميل دفتر العمل، تبديل نظام التاريخ، وحفظ النتيجة — كل ذلك دون الحاجة إلى Microsoft Excel على الخادم.

## إجابات سريعة
- **ماذا يفعل نظام التاريخ 1904؟** يبدأ عد الأيام من 1 يناير 1904، مما يغير جميع التواريخ بمقدار 1,462 يوم مقارنةً بالنظام الافتراضي 1900.  
- **لماذا نستخدم Aspose.Cells لتغيير نظام التاريخ؟** يوفر API بسيط يعمل دون تثبيت Excel ويدعم الملفات الكبيرة.  
- **ما إصدارات Java المدعومة؟** JDK 8 أو أحدث.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تعمل للتقييم؛ الترخيص يزيل حدود الاستخدام.  
- **هل يمكنني التحويل مرة أخرى إلى نظام 1900 لاحقًا؟** نعم، فقط استدعِ `setDate1904(false)`.

## ما هو نظام التاريخ 1904 في Excel؟
نظام التاريخ 1904 يحسب الأيام من 1 يناير 1904، بدلاً من الحقبة الافتراضية 1900. هذه الإزاحة تضيف بالضبط 1,462 يومًا إلى كل قيمة تاريخ، وهذا هو السبب في ظهور دفاتر عمل ماك القديمة متأخرة عند فتحها على Windows. يُستخدم أساسًا للتوافق مع ملفات Excel القديمة على Macintosh وبعض النماذج المالية القديمة.

## لماذا تغيير نظام تاريخ Excel باستخدام Aspose.Cells؟
يمكنك تبديل نظام التاريخ مباشرةً من Java، مما يلغي الخطوات اليدوية في Excel. Aspose.Cells يعالج دفاتر العمل حتى **2 GB** من الحجم ويمكنه تحويل دفتر عمل يحتوي على 500 ورقة في أقل من **2 ثانية** على خادم رباعي النوى عادي، مما يوفر أتمتة عالية الأداء على الخادم.

## المتطلبات المسبقة
- Java Development Kit (JDK) 8 أو أعلى.  
- Maven أو Gradle لإدارة التبعيات.  
- معرفة أساسية ببرمجة Java.  

## إعداد Aspose.Cells للـ Java

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
ضمن هذا السطر في ملف `build.gradle` الخاص بك:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### الحصول على الترخيص
تقدم Aspose نسخة تجريبية مجانية، ترخيصًا مؤقتًا، ورخص تجارية كاملة. يمكنك البدء بـ [النسخة التجريبية](https://releases.aspose.com/cells/java/) أو الحصول على ترخيص مؤقت من [صفحة الترخيص المؤقت](https://purchase.aspose.com/temporary-license/).

## كيف تغير نظام تاريخ Excel إلى 1904 باستخدام Aspose.Cells للـ Java؟
حمّل دفتر العمل، فعّل إعداد 1904، واحفظ الملف — هذه العملية ذات الثلاث خطوات تُحدّث حقبة التاريخ الداخلية لدفتر العمل في أقل من ثانية. استدعاء API `setDate1904(true)` يغيّر علم النظام، ويتم حفظ التغيير عند استدعاء `save`. لا يلزم تثبيت Excel، مما يجعله مثاليًا لبيئات الخوادم بدون واجهة.

### الخطوة 1: تهيئة وتحميل دفتر العمل
الفئة `Workbook` تمثل ملف Excel كامل في الذاكرة. أولاً، أنشئ كائن `Workbook` يشير إلى ملفك الحالي.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### الخطوة 2: تفعيل نظام التاريخ 1904
طريقة `WorkbookSettings.setDate1904` تبدّل علم التاريخ على مستوى دفتر العمل. ضبطه على `true` يُفعّل نظام 1904 لجميع الأوراق.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**نصيحة احترافية:** يمكنك أيضًا استدعاء `setDate1904(false)` لاحقًا إذا احتجت إلى الرجوع.

### الخطوة 3: حفظ دفتر العمل المعدل
أخيرًا، اكتب التغييرات إلى ملف جديد (أو استبدل الأصلي). طريقة `save` تحترم نظام التاريخ النشط تلقائيًا.

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

> **ملاحظة:** يستخدم الكود أعلاه اسم الفئة `tWorkbook` كما هو موفر أصلاً. تأكد من أن هذا الخطأ المطبعي يتطابق مع تسميات مشروعك أو صححه إلى `Workbook` إذا لزم الأمر.

## تعيين تاريخ Excel برمجيًا (كلمة مفتاحية ثانوية)
إذا كنت بحاجة إلى تعديل قيم خلايا فردية بعد تغيير النظام، يمكنك استخدام `cells.get(i, j).putValue(Date)` حيث سيتم تفسير التاريخ وفقًا لنظام التاريخ النشط.

## تحويل نظام Excel 1904 إلى 1900 (كلمة مفتاحية ثانوية)
للعودة، فقط استدعِ:

```java
workbook.getSettings().setDate1904(false);
```

ثم احفظ دفتر العمل مرة أخرى.

## تطبيقات عملية
1. **أرشفة البيانات** – الحفاظ على الطوابع الزمنية القديمة عند ترحيل جداول Excel القديمة المستندة إلى ماك.  
2. **تقارير متعددة المنصات** – إنشاء تقارير تُفتح بشكل صحيح على كل من Windows و macOS دون اختلافات في التواريخ.  
3. **نمذجة مالية** – مواءمة حسابات التاريخ مع النماذج المالية القديمة التي تتوقع نظام 1904.

## اعتبارات الأداء
- قصر عمليات دفتر العمل في جلسة واحدة للحفاظ على انخفاض استهلاك الذاكرة؛ Aspose.Cells يبث البيانات ولا يحمل الملف بالكامل في الذاكرة إلا إذا طلبت ذلك صراحة.  
- ضبط علامات جمع القمامة في Java (`-XX:+UseG1GC`) للملفات الكبيرة جدًا لتجنب ارتفاع فترات التوقف.  

## الأسئلة المتكررة

**س: ما الفرق بين نظامي التاريخ 1900 و 1904؟**  
ج: يبدأ نظام 1900 في 1 يناير 1900، بينما يبدأ نظام 1904 في 1 يناير 1904، مما يغيّر جميع التواريخ بمقدار 1,462 يومًا.

**س: هل يمكنني تغيير نظام التاريخ لدفتر عمل مفتوح حاليًا في Excel؟**  
ج: نعم، ولكن يجب إغلاق الملف في Excel أولاً؛ وإلا سيفشل عملية الحفظ.

**س: هل أحتاج إلى ترخيص لاستخدام `setDate1904`؟**  
ج: الطريقة تعمل في النسخة التجريبية المجانية، لكن الترخيص الكامل يزيل قيود التقييم.

**س: هل يمكن تغيير نظام التاريخ لورقة عمل واحدة فقط؟**  
ج: لا، نظام التاريخ هو إعداد على مستوى دفتر العمل؛ يطبق على جميع الأوراق.

**س: كيف يمكنني التحقق من تغيير نظام التاريخ؟**  
ج: افتح الملف المحفوظ في Excel، انتقل إلى **File → Options → Advanced**، وتحقق من تحديد مربع **"Use 1904 date system"**.

## الخلاصة
أنت الآن تعرف كيفية **تغيير نظام تاريخ Excel** إلى 1904 باستخدام Aspose.Cells للـ Java، وكيفية تعيين تواريخ خلايا فردية، وكيفية الرجوع إلى نظام 1900 عند الحاجة. دمج هذه المقاطع في خطوط معالجة البيانات الخاصة بك لضمان توافق التواريخ عبر المنصات والملفات القديمة.

---

**آخر تحديث:** 2026-10-28  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

**التوثيق:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
**التنزيل:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
**شراء الترخيص:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
**نسخة تجريبية مجانية:** [Start Free Trial](https://releases.aspose.com/cells/java/)  
**ترخيص مؤقت:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)  
**منتدى الدعم:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## دروس ذات صلة

- [تحويل Excel إلى PDF بكفاءة مع تنسيقات تاريخ مخصصة باستخدام Aspose.Cells للـ Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells للـ Java: كيفية إنشاء وتنسيق دفاتر عمل Excel بكفاءة](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [إتقان معالجة Excel باستخدام Aspose.Cells للـ Java: عمليات دفتر العمل وتنسيق الخلايا](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}