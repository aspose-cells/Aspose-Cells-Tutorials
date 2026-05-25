---
date: '2026-03-15'
description: تعلم كيفية تقسيم الأسماء إلى أعمدة منفصلة وحفظ المصنف بصيغة xlsx باستخدام
  Aspose.Cells Java في دليل خطوة بخطوة.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: Aspose Cells Java – تقسيم الأسماء إلى أعمدة
url: /ar/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إتقان **aspose cells java**: تقسيم الأسماء إلى أعمدة

مرحبًا بكم في دليل **aspose cells java** الشامل. في هذا الشرح ستتعلم **كيفية تقسيم الأسماء** المخزنة في عمود Excel واحد إلى عمودين منفصلين — الاسم الأول والاسم الأخير — باستخدام ميزة النص‑إلى‑أعمدة القوية. سواءً كنت تقوم بتنظيف قائمة جهات الاتصال، أو إعداد البيانات لاستيراد إلى نظام CRM، أو تحتاج فقط إلى طريقة سريعة لإعادة هيكلة الجداول، يوضح لك هذا الدليل بالضبط كيفية **save workbook xlsx** بعد التحويل.

## إجابات سريعة
- **ماذا يغطي هذا الشرح؟** تقسيم سلاسل الأسماء الكاملة إلى أعمدة الاسم الأول والاسم الأخير باستخدام Aspose.Cells للغة Java.  
- **ما نسخة المكتبة المستخدمة؟** أحدث إصدار مستقر (حتى عام 2026).  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكنني التقسيم باستخدام فواصل أخرى؟** نعم — فقط غيّر الفاصل في `TxtLoadOptions`.  
- **هل الناتج ملف .xlsx؟** بالتأكيد، يتم حفظ المصنف بصيغة XLSX.

## ما هو **aspose cells java**؟
**Aspose.Cells java** هو واجهة برمجة تطبيقات Java عالية الأداء تتيح للمطورين إنشاء وتعديل وتحويل وعرض ملفات Excel دون الحاجة إلى Microsoft Office. يدعم جميع صيغ Excel الرئيسية ويقدم ميزات متقدمة مثل الصيغ، والرسوم البيانية، ومعالجة البيانات.

## لماذا نستخدم **aspose cells java** لتقسيم الأسماء؟
- **بدون تثبيت**: يعمل على أي بيئة Java من جانب الخادم.  
- **السرعة**: يتعامل مع جداول البيانات الكبيرة أسرع من التفاعل الأصلي مع Excel.  
- **الدقة**: تحكم كامل في الفواصل، ونطاقات الأعمدة، وصيغ الإخراج.  
- **الموثوقية**: لا يعتمد على COM أو Office، مما يجعله مثاليًا للنشر في السحابة أو الحاويات.

## المتطلبات المسبقة
- مجموعة تطوير Java (JDK) 8 أو أحدث.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse (اختياري لكن يُنصح به).  
- Maven أو Gradle لإدارة الاعتمادات.  

### إعداد Maven
أضف اعتماد Aspose.Cells إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### إعداد Gradle
أضف المكتبة إلى ملف `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **نصيحة احترافية:** استخدم ترخيصًا مؤقتًا من بوابة Aspose لفتح جميع الوظائف أثناء التطوير.

## تنفيذ خطوة بخطوة

### الخطوة 1: إنشاء مصنف والوصول إلى الورقة الأولى
أولًا، استورد الفئات الأساسية وأنشئ مصنفًا جديدًا. سيعطيك ذلك ملف Excel نظيف جاهز لإدخال البيانات.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### الخطوة 2: ملء الورقة بأسماء تجريبية
بعد ذلك، أضف بعض سلاسل الأسماء الكاملة إلى العمود **A**. في مشروع حقيقي ستقرأ هذه البيانات من قاعدة بيانات أو ملف CSV.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### الخطوة 3: تكوين خيارات تحميل النص لتقسيم الأعمدة
تخبر فئة `TxtLoadOptions` Aspose.Cells كيفية تفسير النص. هنا نستخدم مسافة (`' '`) كفاصل.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### الخطوة 4: تقسيم النص إلى عمودين
الآن استدعِ `textToColumns()` على نطاق الخلايا الذي يحتوي على الأسماء. المعاملات `(0, 0, 5, opts)` تعني *ابدأ من الصف 0، العمود 0، عالج 5 صفوف، باستخدام الخيارات التي عرّفناها*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

بعد هذا الاستدعاء، يحتوي العمود A على الأسماء الأولى والعمود B على الأسماء الأخيرة.

### الخطوة 5: حفظ المصنف كملف XLSX
أخيرًا، احفظ المصنف المعدل على القرص. يضمن تعداد `SaveFormat` تخزين الملف بصيغة XLSX الحديثة.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **لماذا هذا مهم:** باستخدام **save workbook xlsx**، تضمن التوافق مع أحدث إصدارات Excel، وGoogle Sheets، وغيرها من أدوات الجداول.

## تطبيقات عملية
- **تنظيف البيانات:** فصل الحقول المتصلة بسرعة قبل تحميلها إلى خطوط أنابيب التحليل.  
- **تكامل CRM:** تحويل قائمة جهات اتصال مسطحة إلى جدول منظم للاستيراد.  
- **أنظمة الموارد البشرية:** تقسيم الأسماء الكاملة للموظفين لمعالجة الرواتب أو المزايا.

## اعتبارات الأداء
عند التعامل مع آلاف الصفوف:

1. **تحديثات دفعية:** استخدم `ws.getCells().setRowHeight()` أو طرق دفعية مشابهة لتقليل الحمل.  
2. **إدارة الذاكرة:** استدعِ `wb.calculateFormula()` فقط عند الضرورة، وتخلص من الكائنات الكبيرة فور الانتهاء.  
3. **جمع القمامة:** شغّل JVM بإعدادات كومة مناسبة (`-Xmx2g` للملفات الكبيرة) لتفادي أخطاء OutOfMemory.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **الأسماء تحتوي على أحرف وسطية** (مثل “John A. Doe”) | عدّل الفاصل أو عالج العمود الثاني لاستخراج الاسم الأخير. |
| **وجود خلايا فارغة غير متوقعة** | تأكد من أن نطاق المصدر (`textToColumns` parameters) يطابق عدد الصفوف الفعلية. |
| **الترخيص غير موجود** | ضع ملف الترخيص المؤقت (`Aspose.Cells.lic`) في جذر المشروع أو اضبط الترخيص برمجيًا. |

## الأسئلة المتكررة

**س: ما هو Aspose.Cells Java؟**  
ج: مكتبة قوية تسمح لك بإنشاء وتعديل وتحويل ملفات Excel برمجيًا باستخدام Java.

**س: هل يمكنني تقسيم الأعمدة بناءً على فواصل غير المسافات؟**  
ج: نعم، خصّص فاصل `TxtLoadOptions` حسب احتياجك.

**س: كيف أتعامل مع مجموعات بيانات كبيرة باستخدام Aspose.Cells؟**  
ج: حسّن الأداء بإدارة الذاكرة وتقليل عمليات المصنف، كما هو موضح أعلاه.

**س: هل هناك دعم متاح إذا واجهت مشاكل؟**  
ج: زر [منتدى Aspose](https://forum.aspose.com/c/cells/9) للحصول على مساعدة المجتمع أو تواصل مباشرة مع فريق دعم Aspose.

**س: ما الصيغ التي يمكن لـ Aspose.Cells حفظ المصنفات بها؟**  
ج: يدعم مجموعة واسعة من صيغ Excel، بما فيها XLSX، XLS، CSV، وأكثر.

## موارد

- **الوثائق**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **التنزيل**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **الشراء**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **التجربة المجانية**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **الترخيص المؤقت**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

نتمنى لك برمجة ممتعة، واستمتع بالاستفادة من القوة الكاملة لـ **aspose cells java** في مشاريعك!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2026-03-15  
**تم الاختبار مع:** Aspose.Cells 25.3 للغة Java  
**المؤلف:** Aspose