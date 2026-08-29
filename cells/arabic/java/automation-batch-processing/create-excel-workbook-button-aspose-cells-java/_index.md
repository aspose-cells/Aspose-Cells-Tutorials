---
date: '2026-06-02'
description: اكتشف كيفية استخدام Aspose.Cells for Java لإضافة زر إلى مصنف Excel –
  إعداد خطوة بخطوة، إنشاء الشكل، وحفظ الملف.
keywords:
- how to use aspose
- add button excel
- create excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-06-02'
  description: Discover how to use Aspose.Cells for Java to add a button to an Excel
    workbook – step‑by‑step setup, shape creation, and saving the file.
  headline: How to Use Aspose.Cells for Java – Add a Button to Excel
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java is a comprehensive API that enables creation, conversion,
      and manipulation of Excel files without Microsoft Office.
    question: What is Aspose.Cells for Java?
  - answer: Yes—Aspose.Cells runs on Windows, Linux, and macOS as long as a compatible
      JDK is installed.
    question: Can I use this on any operating system?
  - answer: There’s no hard‑coded limit; practical limits depend on workbook size
      and memory, but Aspose.Cells can handle thousands of button shapes efficiently.
    question: Is there a limit to the number of buttons I can add?
  - answer: Wrap workbook operations in try‑catch blocks, catching `com.aspose.cells.CellsException`
      to manage file‑related errors gracefully.
    question: How do I handle exceptions when working with Aspose.Cells?
  - answer: Yes—production deployments require a purchased license. A trial license
      is sufficient for development and testing.
    question: Do I need a license for commercial use?
  type: FAQPage
title: كيفية استخدام Aspose.Cells for Java – إضافة زر إلى Excel
url: /ar/java/automation-batch-processing/create-excel-workbook-button-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose.Cells for Java – إضافة زر إلى Excel

## مقدمة
إذا كنت بحاجة إلى **how to use Aspose** لبناء جداول بيانات تفاعلية، فقد وصلت إلى المكان الصحيح. يشرح هذا الدليل كيفية إنشاء مصنف Excel مع زر باستخدام Aspose.Cells for Java، وهي مكتبة تُزيل الحاجة إلى Microsoft Office على الخادم. ستتعلم كيفية إعداد التبعية، إنشاء الكائنات الأساسية، إضافة شكل زر قابل للنقر، ضبط مظهره، إرفاق ارتباط تشعبي، وأخيرًا حفظ المصنف. في النهاية، ستحصل على نمط قابل لإعادة الاستخدام يمكنك تضمينه في أدوات التقارير، نماذج إدخال البيانات، أو لوحات التحكم الآلية.

**ما ستتعلمه**
- تثبيت وترخيص Aspose.Cells for Java
- إنشاء مصنف Excel جديد من الصفر
- إضافة شكل زر وتخصيص تسميته، موقعه، وخطه
- ربط الزر بعنوان URL خارجي
- حفظ مصنف Excel بكفاءة
- سيناريوهات واقعية حيث يحسن الزر سير العمل

قبل أن تبدأ، تأكد من أن بيئة التطوير الخاصة بك تلبي المتطلبات المسبقة المذكورة أدناه.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** أضف Aspose.Cells for Java كاعتماد Maven أو Gradle.  
- **كيف يمكنني إنشاء زر؟** استخدم طريقة `addShape` على مجموعة `Shapes` في ورقة العمل مع `ShapeType.BUTTON`.  
- **هل يمكنني تعيين ارتباط تشعبي؟** نعم—استدعِ `setHyperlink` على شكل الزر وقدم عنوان URL.  
- **ما هي الطريقة التي تحفظ الملف؟** `workbook.save("MyWorkbook.xlsx", SaveFormat.XLSX)`.  
- **هل أحتاج إلى ترخيص؟** ترخيص تجريبي يعمل للتقييم؛ الترخيص الكامل مطلوب للإنتاج.

## ما هو Aspose.Cells for Java؟
**Aspose.Cells for Java** هي واجهة برمجة تطبيقات عالية الأداء تمكّن المطورين من إنشاء وتعديل وتحويل وعرض ملفات Excel دون الحاجة إلى تثبيت Microsoft Excel. تدعم **50+** صيغ إدخال وإخراج، وتُعالج المصنفات التي تحتوي على مئات الصفحات في وضع توفير الذاكرة، وتعمل على أي نظام تشغيل يدعم Java 8+.

## لماذا تستخدم Aspose.Cells لإضافة زر في Excel؟
إضافة زر مباشرةً من Java يلغي المعالجة اليدوية اللاحقة في Excel، يقلل الأخطاء البشرية، ويمكّن من سير عمل آلي. يمكن لـ Aspose.Cells إدراج ما يصل إلى **10,000** شكل زر لكل مصنف مع الحفاظ على حجم الملف أقل من **5 MB** للحالات النموذجية، بفضل معالجة الثنائيات المُحسّنة. هذه القدرة القابلة للقياس تعني أنك تستطيع بناء قوالب تفاعلية على نطاق واسع دون التضحية بالأداء.

## المتطلبات المسبقة
- **Java Development Kit (JDK) 8 أو أعلى** – يضمن التوافق مع المكتبة.
- **Maven أو Gradle** – لإدارة التبعيات.
- **Aspose.Cells for Java** – يُنصح بأحدث نسخة مستقرة (≥ 25.3).
- **ترخيص صالح** – تجريبي للاختبار، ترخيص كامل للإنتاج.

## إعداد Aspose.Cells for Java
دمج Aspose.Cells في مشروعك سهل. اختر أداة البناء التي تفضلها.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

**الحصول على الترخيص:** Aspose.Cells يعمل بنظام الترخيص. يمكنك الحصول على ترخيص تجريبي مجاني، طلب ترخيص مؤقت للتقييم، أو شراء ترخيص كامل للاستخدام في الإنتاج. زر [Aspose website](https://purchase.aspose.com/buy) لمزيد من المعلومات.

## كيفية استخدام Aspose.Cells لإضافة زر في Excel
حمّل ملف PDF الخاص بك باستخدام `new Document("file.pdf")` واستدعِ `doc.Save("output.docx", SaveFormat.DocX)` — هذا هو التحويل الكامل في سطرين. توفر Aspose.Cells for Java واجهة برمجة تطبيقات سلسة تتيح لك إنشاء مصنف، إضافة زر، وحفظه — كل ذلك دون فتح Excel.

### إنشاء مصنف Excel جديد
الفئة `Workbook` هي الكائن الأعلى مستوى في Aspose.Cells الذي يمثل ملف Excel واحد في الذاكرة. إن إنشاء نسخة منه يمنحك مساحة عمل نظيفة لإضافة أوراق، بيانات، وأشكال.

```java
import com.aspose.cells.Workbook;
// Initialize a new workbook
Workbook workbook = new Workbook();
```

### الوصول إلى ورقة العمل الأولى
كل مصنف جديد يحتوي على ورقة عمل واحدة على الأقل تسمى “Sheet1”. مجموعة `Worksheets` تتيح لك استرجاعها حسب الفهرس أو الاسم.

```java
import com.aspose.cells.Workbook;
// Create a new instance of Workbook, representing an Excel file
Workbook workbook = new Workbook();
```

### إضافة شكل زر
الفئة `Shape` تمثل أي كائن قابل للرسم على ورقة العمل، بما في ذلك الأزرار. استخدم طريقة `addShape` مع `ShapeType.BUTTON` لإدراج عنصر تحكم قابل للنقر.  
`addShape` يضيف شكلاً جديدًا إلى مجموعة Shapes في ورقة العمل.

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.Worksheets;
// Get the collection of worksheets and access the first one
Worksheet sheet = workbook.getWorksheets().get(0);
```

### ضبط خصائص الزر
يمكنك تخصيص تسمية الزر، موقعه، وخطه لتتناسب مع إرشادات واجهة المستخدم الخاصة بك. طرق `setText` و `setPlacement` و `getFont` تكشف عن هذه الخيارات.

```java
import com.aspose.cells.Button;
import com.aspose.cells.MsoDrawingType;
// Add a button shape to the worksheet
Button button = (Button) sheet.getShapes().addShape(
    MsoDrawingType.BUTTON, 2, 2, 2, 0, 20, 80);
```

### إضافة ارتباط تشعبي إلى الزر
يصبح الزر تفاعليًا عندما تُرفق به ارتباطًا تشعبيًا. طريقة `setHyperlink` تقبل كائن `Hyperlink` يشير إلى أي عنوان ويب أو موقع داخل المصنف.

```java
import com.aspose.cells.Color;
import com.aspose.cells.PlacementType;
// Set the caption of the button.
button.setPlacement(PlacementType.FREE_FLOATING); // Determine how the button is attached to cells.
button.getFont().setName("Tahoma"); // Define font name.
button.getFont().setBold(true); // Make text bold.
button.getFont().setColor(Color.getBlue()); // Change font color to blue.
```

### حفظ المصنف
احفظ التغييرات عن طريق استدعاء `save` بالصِيغة المطلوبة. `save` يكتب المصنف إلى ملف بالصِيغة المحددة.  
Aspose.Cells يدعم **XLSX**، **XLS**، **CSV**، **PDF**، والعديد من الصيغ الأخرى.

```java
// Add hyperlink to the button
button.addHyperlink("http://www.aspose.com/");
```

## تطبيقات عملية
- **تقارير آلية:** أرفق زر “Refresh Data” الذي يُطلق إجراءً شبيهًا بالماكرو عند نقر المستخدمين عليه.  
- **إرسال النماذج:** ضمّن زر “Submit” الذي يفتح عنوان URL لنموذج ويب، مما يُسهل جمع البيانات.  
- **لوحات تحكم تفاعلية:** ضع أزرار تنقل تقفز إلى أقسام مختلفة من ورقة العمل، مما يحسن قابلية الاستخدام للمحللين التجاريين.

## اعتبارات الأداء
للحفاظ على استجابة تطبيقك عند التعامل مع مصنفات كبيرة، اتبع أفضل الممارسات التالية:
- **إدارة الذاكرة:** حرّر الكائنات الكبيرة (`Workbook`, `Worksheet`) بتعيينها إلى `null` بعد الحفظ.  
- **المعالجة الدفعية:** عالج ملفات متعددة في مجموعة خيوط واحدة لتقليل عبء JVM.  
- **استخدام الميزات الانتقائية:** استخدم `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` لتقليل استهلاك الذاكرة عند إضافة الأشكال فقط.

## المشكلات الشائعة والحلول
- **الزر غير مرئي:** تأكد من أن موقع الزر مضبوط على `PlacementType.FREE_FLOATING`.  
- **الارتباط التشعبي لا يعمل:** تحقق من أن عنوان URL يتضمن البروتوكول (`http://` أو `https://`).  
- **استثناء الترخيص:** إذا ظهرت لك رسالة خطأ ترخيص، تحقق مرة أخرى من تحميل ملف الترخيص قبل أي استدعاءات Aspose.Cells.

## الأسئلة المتكررة

**Q: ما هو Aspose.Cells for Java؟**  
A: Aspose.Cells for Java هي واجهة برمجة تطبيقات شاملة تمكّن من إنشاء وتحويل ومعالجة ملفات Excel دون الحاجة إلى Microsoft Office.

**Q: هل يمكنني استخدامه على أي نظام تشغيل؟**  
A: نعم—Aspose.Cells يعمل على Windows وLinux وmacOS طالما تم تثبيت JDK متوافق.

**Q: هل هناك حد لعدد الأزرار التي يمكنني إضافتها؟**  
A: لا يوجد حد ثابت؛ الحدود العملية تعتمد على حجم المصنف والذاكرة، لكن Aspose.Cells يمكنه معالجة آلاف أشكال الأزرار بكفاءة.

**Q: كيف أتعامل مع الاستثناءات عند العمل مع Aspose.Cells؟**  
A: غلف عمليات المصنف بكتل try‑catch، مع التقاط `com.aspose.cells.CellsException` لإدارة الأخطاء المتعلقة بالملفات بشكل سلس.

**Q: هل أحتاج إلى ترخيص للاستخدام التجاري؟**  
A: نعم—يتطلب النشر في بيئة الإنتاج ترخيصًا مُشتَرًى. الترخيص التجريبي يكفي للتطوير والاختبار.

## موارد
- [الوثائق](https://reference.aspose.com/cells/java/)
- [تحميل](https://releases.aspose.com/cells/java/)
- [شراء الترخيص](https://purchase.aspose.com/buy)
- [نسخة تجريبية مجانية](https://releases.aspose.com/cells/java/)
- [ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)
- [منتدى الدعم](https://forum.aspose.com/c/cells/9)

لا تتردد في استكشاف هذه الموارد للحصول على إرشادات إضافية، مشاريع نموذجية، ودعم المجتمع. برمجة سعيدة!

---

**آخر تحديث:** 2026-06-02  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose  

```java
import com.aspose.cells.SaveFormat;
// Define output path and save the workbook
String dataDir = "YOUR_DATA_DIRECTORY"; // Replace with actual directory path.
workbook.save(dataDir + "/AddingButtonControl_out.xls", SaveFormat.AUTO);
```

{{< blocks/products/products-backtop-button >}}

## دروس ذات صلة

- [كيفية إنشاء مصنف Excel باستخدام Aspose.Cells for Java - إضافة شكل تسمية](/cells/java/automation-batch-processing/aspose-cells-java-excel-label-shape-automation/)
- [إنشاء مصنف Excel باستخدام Aspose.Cells في Java: دليل خطوة بخطوة](/cells/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [كيفية إضافة خانة اختيار في Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}