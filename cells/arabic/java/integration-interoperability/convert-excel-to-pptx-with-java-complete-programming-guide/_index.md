---
category: general
date: 2026-06-18
description: تحويل Excel إلى PPTX باستخدام Aspose.Cells في Java. تعلم كيفية حفظ المصنف
  كملف PowerPoint وتصدير مربعات النص في Excel وأشكال المخططات بكفاءة.
draft: false
keywords:
- convert excel to pptx
- save workbook as powerpoint
- convert xlsx to pptx
- export excel text boxes
- export excel charts shapes
language: ar
og_description: تحويل Excel إلى PPTX في Java. يوضح هذا الدرس كيفية حفظ المصنف كملف
  PowerPoint وتصدير مربعات النص في Excel وأشكال المخططات.
og_title: تحويل Excel إلى PPTX باستخدام Java – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Convert Excel to PPTX using Aspose.Cells in Java. Learn how to save
    workbook as PowerPoint, export Excel text boxes and chart shapes efficiently.
  headline: Convert Excel to PPTX with Java – Complete Programming Guide
  type: TechArticle
- description: Convert Excel to PPTX using Aspose.Cells in Java. Learn how to save
    workbook as PowerPoint, export Excel text boxes and chart shapes efficiently.
  name: Convert Excel to PPTX with Java – Complete Programming Guide
  steps:
  - name: Each worksheet turned into a separate slide (or a single slide if the workbook
      has one sheet).
    text: Each worksheet turned into a separate slide (or a single slide if the workbook
      has one sheet).
  - name: Text boxes that you can click and edit directly.
    text: Text boxes that you can click and edit directly.
  - name: Charts that you can re‑format, change data series, or move around.
    text: Charts that you can re‑format, change data series, or move around.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
- File Conversion
title: تحويل Excel إلى PPTX باستخدام Java – دليل برمجي كامل
url: /ar/java/integration-interoperability/convert-excel-to-pptx-with-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PPTX باستخدام Java – دليل برمجة كامل

هل احتجت يومًا إلى **convert Excel to PPTX** لكن لم تكن متأكدًا أي مكتبة يمكنها إنجاز المهمة دون عشرات الحلول البديلة؟ لست وحدك. في العديد من مشاريع المؤسسات تظهر الحاجة إلى **save workbook as PowerPoint** عندما يجب مشاركة لوحات التقارير مع مستخدمين لا يستخدمون Excel.  

في هذا الدليل سنستعرض حلًا عمليًا باستخدام Aspose.Cells for Java يتيح لك **convert Excel to PPTX** ببضع أسطر من الشيفرة فقط. في النهاية ستعرف أيضًا كيفية **export Excel text boxes** و **export Excel charts shapes** بحيث تبدو الشرائح مطابقة تمامًا للورقة الأصلية.

## ما ستتعلمه

- تحميل ملف عمل `.xlsx` من القرص.  
- تمكين تصدير صناديق النص القابلة للتحرير والأشكال بحيث تظل قابلة للتحرير في PowerPoint.  
- **Save workbook as PowerPoint** (`.pptx`) باستدعاء طريقة واحدة.  
- التحقق من الناتج واستكشاف الأخطاء الشائعة.  

لا سكريبتات خارجية، لا نسخ ولصق يدوي — فقط شيفرة Java صافية يمكنك إدراجها في أي مشروع Maven أو Gradle.

![مقتطف كود Java يوضح كيفية تحويل Excel إلى PPTX](https://example.com/images/convert-excel-to-pptx-java.png "كود Java لتحويل Excel إلى PPTX")

## الخطوة 1: إعداد Aspose.Cells في مشروعك

أولًا، تحتاج إلى مكتبة Aspose.Cells for Java. إذا كنت تستخدم Maven، أضف الاعتماد إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

بالنسبة لـ Gradle، الأمر مشابه:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **نصيحة احترافية:** تقدم Aspose ترخيصًا مؤقتًا مجانيًا للتقييم. سجّل على موقعهم، حمّل ملف `Aspose.Cells.lic`، وضعه في مسار الـ classpath لتجنب علامة التقييم المائية.

## الخطوة 2: تحميل ملف Excel Workbook

الآن بعد أن أصبحت المكتبة جاهزة، يمكنك **load the Excel workbook** الذي تنوي تحويله. فئة `Workbook` تمثل الملف بالكامل، مما يتيح لك تعديل الإعدادات قبل التصدير.

```java
import com.aspose.cells.*;

public class ExportEditableShapesDemo {
    public static void main(String[] args) throws Exception {
        // Load the source .xlsx file
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        // ... further steps follow
    }
}
```

> **لماذا هذا مهم:** تحميل ملف الـ workbook أولًا يمنحك الوصول إلى كائن `Settings`، حيث ستمكن خيارات **export Excel text boxes** و **export Excel charts shapes**.

## الخطوة 3: تمكين تصدير صناديق النص القابلة للتحرير

إذا كان جدول البيانات يحتوي على صناديق نص تشبه التعليقات وتريد تحريرها لاحقًا في PowerPoint، يجب تشغيل العلامة المقابلة. هذه الخطوة أساسية لتجربة **convert excel to pptx** حقيقية حيث تبقى الأشكال تفاعلية.

```java
// Enable exporting of editable text boxes
workbook.getSettings().setExportEditableTextBoxes(true);
```

> **سؤال شائع:** *ماذا يحدث إذا تخطيت هذه الخطوة؟* تصبح صناديق النص صورًا ثابتة في الشريحة، وتفقد القدرة على التحرير. تشغيل العلامة يحافظ على سلوكها الأصلي.

## الخطوة 4: تمكين تصدير الأشكال القابلة للتحرير (الرسوم البيانية، SmartArt، إلخ)

الرسوم البيانية، SmartArt، وغيرها من كائنات الرسم تُعامل أيضًا كأشكال. للحفاظ على قابليتها للتحرير بعد التحويل، اضبط العلامة التالية:

```java
// Enable exporting of editable shapes (charts, SmartArt, etc.)
workbook.getSettings().setExportEditableShapes(true);
```

> **حالة خاصة:** قد لا تحتفظ بعض أنواع الرسوم البيانية المعقدة (مثل الرسوم السطحية ثلاثية الأبعاد) بقابلية تحرير كاملة بسبب قيود PowerPoint. في هذه الحالات، تعود المكتبة إلى صورة نقطية، لكن بقية الشريحة تظل قابلة للتحرير.

## الخطوة 5: حفظ الـ Workbook كملف PowerPoint (تحويل XLSX إلى PPTX)

هذه هي لحظة الحقيقة — **convert xlsx to pptx** بسطر واحد. طريقة `save` تأخذ مسار الوجهة وتعداد `SaveFormat.PPTX`.

```java
// Save the workbook as a PowerPoint presentation
workbook.save("YOUR_DIRECTORY/presentation.pptx", SaveFormat.PPTX);
```

هذا كل شيء. بعد انتهاء هذا الاستدعاء، ستحصل على ملف `.pptx` كامل يعكس تخطيط ورقة Excel الأصلية، مع صناديق نص قابلة للتحرير وأشكال الرسوم البيانية.

## الخطوة 6: التحقق من الناتج

افتح `presentation.pptx` في Microsoft PowerPoint أو LibreOffice Impress. يجب أن ترى:

1. كل ورقة عمل تتحول إلى شريحة منفصلة (أو شريحة واحدة إذا كان الـ workbook يحتوي على ورقة واحدة).  
2. صناديق النص التي يمكنك النقر عليها وتحريرها مباشرة.  
3. الرسوم البيانية التي يمكنك إعادة تنسيقها، تغيير سلاسل البيانات، أو تحريكها.

إذا ظهر أي شيء غير صحيح، تحقق مرة أخرى من الإعدادين الذين فعلناهما في الخطوتين 3 و4. فهما المفتاحان الوحيدان اللذان يؤثران على قابلية التحرير.

## مثال كامل يعمل

فيما يلي الفئة الكاملة للـ Java الجاهزة للتنفيذ والتي تضم جميع الخطوات السابقة. لا تتردد في نسخها ولصقها في بيئة التطوير المتكاملة الخاصة بك.

```java
import com.aspose.cells.*;

public class ExportEditableShapesDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Enable exporting of editable text boxes
        workbook.getSettings().setExportEditableTextBoxes(true);

        // 3️⃣ Enable exporting of editable shapes (charts, SmartArt, etc.)
        workbook.getSettings().setExportEditableShapes(true);

        // 4️⃣ Save the workbook as a PowerPoint presentation (convert xlsx to pptx)
        workbook.save("YOUR_DIRECTORY/presentation.pptx", SaveFormat.PPTX);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/presentation.pptx");
    }
}
```

**المخرجات المتوقعة في وحدة التحكم**

```
Conversion complete! Check YOUR_DIRECTORY/presentation.pptx
```

وسيظهر الملف `presentation.pptx` في مجلد الهدف، جاهزًا للمشاركة.

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| صناديق النص تظهر كصور | `setExportEditableTextBoxes(false)` أو تم إغفالها | تأكد من استدعاء `setExportEditableTextBoxes(true)`. |
| الرسوم البيانية تم تحويلها إلى صورة نقطية | `setExportEditableShapes(false)` أو نوع رسم غير مدعوم | فعّل `setExportEditableShapes(true)`؛ بالنسبة للرسوم غير المدعومة، فكر في تبسيط الرسم في Excel أولاً. |
| خطأ ملف غير موجود | مسار خاطئ في `new Workbook(...)` | استخدم مسارات مطلقة أو ضع الملف نسبياً إلى جذر المشروع. |
| استثناء الترخيص | لا توجد ترخيص Aspose.Cells صالح | حمّل `Aspose.Cells.lic` عند بدء التطبيق: `License lic = new License(); lic.setLicense("Aspose.Cells.lic");` |

## نصائح الأداء

- **تحويل دفعي:** إذا كنت بحاجة إلى تحويل العشرات من ملفات الـ workbook، أعد استخدام كائن `Workbook` واحد بتحميل كل ملف على التتابع — هذا يقلل من استهلاك الـ JVM.  
- **إدارة الذاكرة:** للملفات Excel الكبيرة جدًا، فعّل `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` للحفاظ على استهلاك الذاكرة ضمن الحدود.  
- **المعالجة المتوازية:** يمكن لـ `ForkJoinPool` في Java معالجة عدة تحويلات في وقت واحد، لكن احرص على مراعاة نموذج الترخيص — كل خيط لا يزال يستهلك مقعد ترخيص.

## ما التالي؟

الآن بعد أن أصبحت متمكنًا من سير عمل **convert excel to pptx**، فكر في الاستكشافات التالية:

- **export Excel charts shapes** إلى PowerPoint مع تنسيق مخصص (مثل تغيير ألوان السمة بعد التحويل).  
- **تحويل دفعي لمجلد من ملفات `.xlsx`** إلى مجموعة شرائح PowerPoint واحدة باستخدام واجهة برمجة `Presentation` لدمج الشرائح.  
- **إضافة ملاحظات المتحدث** برمجيًا عن طريق إدراج `NotesSlide` لكل شريحة — مفيد لسلاسل تقارير آلية.  

كل من هذه المواضيع يبني على الأساس الذي غطيناه، لذا أنت في موقع جيد لتوسيع الحل.

### ملخص

استعرضنا طريقة بسيطة لـ **convert Excel to PPTX** باستخدام Aspose.Cells for Java، مع شرح كيفية **save workbook as PowerPoint**، وتمكين **export Excel text boxes**، و **export Excel charts shapes**. المثال الكامل قابل للتنفيذ فورًا، والنصائح أعلاه ستساعدك على تجنب أكثر المشكلات شيوعًا.

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا، أو جرّب الشيفرة وأخبرنا بالنتيجة. تحويل سعيد!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل مخططات Excel إلى SVG باستخدام Aspose.Cells في Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [كيفية إنشاء وتكوين صناديق النص في Excel باستخدام Aspose.Cells Java لتحسين عرض البيانات](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
- [كيفية إنشاء وحفظ ملف Excel Workbook كـ SVG باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}