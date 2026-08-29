---
category: general
date: 2026-06-21
description: حوّل ملفات Excel إلى PowerPoint باستخدام Java في دقائق. تعلّم كيفية تصدير
  مخططات Excel إلى PowerPoint وحفظ المصنف كملف PPTX باستخدام Aspose.Cells.
draft: false
keywords:
- convert excel to powerpoint
- export excel charts to powerpoint
- save workbook as pptx
language: ar
og_description: حوّل Excel إلى PowerPoint فورًا. يوضح هذا الدليل كيفية تصدير مخططات
  Excel إلى PowerPoint وحفظ المصنف كملف PPTX مع الكود الكامل.
og_title: تحويل Excel إلى PowerPoint – دليل Java خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Convert Excel to PowerPoint with Java in minutes. Learn how to export
    Excel charts to PowerPoint and save workbook as PPTX using Aspose.Cells.
  headline: Convert Excel to PowerPoint – Complete Java Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Office Automation
title: تحويل Excel إلى PowerPoint – دليل Java الكامل
url: /ar/java/integration-interoperability/convert-excel-to-powerpoint-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PowerPoint – دليل Java الكامل

هل تساءلت يومًا كيف **convert Excel to PowerPoint** دون نسخ كل مخطط يدويًا؟ لست وحدك—الفرق التي تُعد تقارير أسبوعية غالبًا ما تقضي وقتًا طويلاً في إعادة إنشاء الرسوم البيانية في الشرائح.  

الأخبار السارة؟ ببضع أسطر من Java يمكنك **export Excel charts to PowerPoint** وحتى الحفاظ عليها قابلة للتحرير لتعديلات لاحقة. في هذا الدرس سنستعرض الخطوات الدقيقة لـ **save workbook as PPTX**، حتى تتمكن من أتمتة إنشاء العروض التقديمية بسهولة.

## ما يغطيه هذا الدرس

سنبدأ بإعداد مشروع Java صغير، ثم تحميل ملف workbook موجود، وضبط خيارات التحويل، وأخيرًا كتابة ملف PowerPoint يحافظ على قابلية تحرير المخططات. في النهاية ستحصل على ملف `Main.java` جاهز للتنفيذ يمكنك وضعه في أي نظام بناء. لا سكريبتات خارجية، ولا حيل واجهة مستخدم معقدة—فقط كود نقي.

المتطلبات الأساسية قليلة: تثبيت Java 8+، نسخة من Aspose.Cells for Java JAR، وملف Excel (`charts.xls`) يحتوي على مخطط واحد على الأقل. إذا كان أي منها غير متوفر، احصل عليه قبل المتابعة.

---

## الخطوة 1: إعداد مشروع Java لتحويل Excel إلى PowerPoint

قبل الغوص في الكود، دعنا نتأكد من جاهزية البيئة. أنشئ دليلًا جديدًا، وضع ملف Aspose.Cells JAR داخل مجلد `libs`، وأضفه إلى classpath الخاص بك. مثال سريع لـ Maven يبدو هكذا (يمكنك أيضًا استخدام Gradle أو `javac` العادي إذا تفضّل):

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- latest as of June 2026 -->
</dependency>
```

إذا لم تكن تستخدم Maven، فقط قم بتحميل ملف JAR من موقع Aspose وارجعه عند التجميع:

```bash
javac -cp "libs/aspose-cells-24.8.jar" src/Main.java
```

**نصيحة احترافية:** حافظ على تحديث نسخة JAR؛ الإصدارات الأحدث تضيف تحسينًا في معالجة المخططات وتُحسّن خط أنابيب **export excel charts to powerpoint**.

## الخطوة 2: تحميل ملف Excel Workbook الذي يحتوي على المخططات

الآن بعد ربط المشروع، السطر الحقيقي الأول من الكود هو تحميل الـ workbook. هنا يبدأ فعليًا مسار **convert excel to powerpoint**.

```java
import com.aspose.cells.*;

public class Main {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the Excel workbook containing the charts
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xls");
        // Continue with conversion options...
```

فئة `Workbook` تمثل ملف Excel بالكامل—الأوراق، الخلايا، والأهم من ذلك، المخططات. إذا كان ملفك موجودًا في مكان آخر، فقط عدل المسار.

*ماذا لو لم يُعثر على الملف؟* Aspose يرمي استثناء `FileNotFoundException`. غلف الاستدعاء بكتلة try‑catch إذا كنت تحتاج إلى معالجة أخطاء سلسة.

## الخطوة 3: ضبط ImageOrPrintOptions لتصدير PPTX

Aspose يستخدم `ImageOrPrintOptions` لإبلاغ المحرك **كيف** يتم عرض الـ workbook. هنا سنحدد الصيغة المستهدفة إلى PowerPoint (`SaveFormat.PPTX`) ونتأكد من أن الشرائح الناتجة جاهزة للتحرير.

```java
        // Step 3: Create options for the conversion and specify the target format (PowerPoint)
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
```

لماذا `ImageOrPrintOptions` وليس شيء آخر؟ لأنها تمنحنا تحكمًا دقيقًا في جودة الصورة، التقسيم إلى صفحات،—والأهم بالنسبة لنا—قابلية تحرير المخططات.

*حالة حدية:* إذا كنت تحتاج إلى حجم شريحة مختلف، يمكنك أيضًا استدعاء `options.setSlideSize(SlideSizeType.WIDESCREEN)` قبل الحفظ.

## الخطوة 4: تمكين المخططات القابلة للتحرير – جوهر **export Excel Charts to PowerPoint**

بشكل افتراضي Aspose يعرض المخططات كصور ثابتة. لتحقيق **export excel charts to powerpoint** مع إمكانية التحرير، قم بتفعيل علم `setEditableCharts`.

```java
        // Step 4: Enable editable charts so they remain editable after conversion
        options.setEditableCharts(true);
```

عند تفعيل هذا العلم، يتحول كل مخطط إلى كائن مخطط PowerPoint أصلي. هذا يعني أن زملائك يمكنهم فتح ملف PPTX وتعديل السلاسل، المحاور، أو الألوان دون الحاجة إلى لمس ملف Excel الأصلي.

*مشكلة شائعة:* بعض أنواع المخططات القديمة (مثل مخططات الرادار) قد لا تُترجم بالكامل. اختبر شريحة نموذجية وتأكد من أن المخطط يبدو كما هو متوقع.

## الخطوة 5: حفظ Workbook كملف PPTX – القطعة الأخيرة من اللغز

السطر الأخير يكتب ملف PowerPoint إلى القرص. هنا نُكمل أخيرًا **save workbook as pptx**.

```java
        // Step 5: Save the workbook as an editable PowerPoint presentation
        workbook.save("YOUR_DIRECTORY/editable.pptx", options);
        System.out.println("Conversion complete! Check YOUR_DIRECTORY/editable.pptx");
    }
}
```

تشغيل البرنامج ينتج `editable.pptx`. افتحه في PowerPoint، انقر على مخطط، وسترى شريط تحرير المخطط المألوف. Voilà—تم **export excel charts to powerpoint** لمخططات Excel الخاصة بك مع إمكانية تحرير كاملة.

### قائمة المصدر الكاملة

بجمع كل ذلك، إليك الملف الكامل الجاهز للتنفيذ:

```java
import com.aspose.cells.*;

public class Main {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the charts
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xls");

        // Create conversion options and target PowerPoint format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);

        // Enable editable charts for true export excel charts to powerpoint
        options.setEditableCharts(true);

        // Save the workbook as PPTX – our final step to convert excel to powerpoint
        workbook.save("YOUR_DIRECTORY/editable.pptx", options);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/editable.pptx");
    }
}
```

**الناتج المتوقع:** بعد التنفيذ ستظهر رسالة وحدة التحكم أعلاه، وسيحتوي ملف `editable.pptx` على شريحة واحدة لكل ورقة عمل (أو لكل مخطط، حسب التخطيط). يمكن النقر المزدوج على أي مخطط داخل PowerPoint لفتح محرر المخطط الأصلي.

---

## التعامل مع السيناريوهات الشائعة والحالات الحدية

| السيناريو | ما يجب فعله |
|----------|------------|
| **لا توجد مخططات في الـ workbook** | ستظل عملية التحويل تنتج شرائح، لكنها ستكون فارغة. أضف شرطًا: `if (workbook.getWorksheets().get(0).getCharts().getCount() == 0) { /* warn */ }` |
| **Workbook كبير ( > 50 MB )** | زيادة حجم heap للـ Java: `java -Xmx2g -cp ... Main` |
| **تنسيق Excel قديم (.xls)** | Aspose يتعامل معها مباشرة، لكن يُفضَّل حفظها كـ `.xlsx` أولاً للحصول على دقة مخططات أفضل. |
| **الحاجة إلى تحويل جزء فقط من الأوراق** | استخدم `Workbook.save(outputPath, options, sheetIndex, sheetCount)` لاستهداف أوراق محددة. |
| **تخطيطات شرائح مخصصة** | بعد الحفظ، يمكنك معالجة ملف PPTX باستخدام Apache POI لتعديل الشرائح الرئيسية. |

هذه النصائح تحافظ على صلابة خط أنابيب **convert excel to powerpoint** بغض النظر عن خصوصيات ملف المصدر.

---

## نظرة بصرية

![مخطط يوضح سير عمل convert excel to powerpoint: تحميل الـ workbook → ضبط الخيارات → تمكين المخططات القابلة للتحرير → حفظ كـ PPTX](convert-excel-to-powerpoint-workflow.png)

*نص بديل:* مخطط يوضح الخطوات لتحويل excel إلى powerpoint باستخدام Aspose.Cells.

## ملخص وخطوات مستقبلية

لقد استعرضنا للتو مثالًا مختصرًا وشاملًا يوضح **convert excel to powerpoint** باستخدام Java. في بضع أسطر تعلمت كيفية **export excel charts to powerpoint**، الحفاظ على قابلية التحرير، و**save workbook as pptx** لأتمتة لاحقة.

إذا كنت ترغب بالمزيد، فكر في المواضيع التالية:

- **Batch processing** عدة workbooks في مجلد (ما زال يستخدم نفس منطق `convert excel to powerpoint`).
- **Embedding images** جنبًا إلى جنب مع المخططات عن طريق دمج `ImageOrPrintOptions` مع `Worksheet.getPictures()`.
- **Integrating with Apache POI** لتخصيص ملف PPTX المُولد بشكل إضافي (مثل إضافة عناوين شرائح أو ملاحظات المتحدث).

لا تتردد في التجربة—استبدل المصدر `.xls` بـ `.xlsx`، عدل حجم الشريحة، أو أوقف `setEditableCharts` إذا كنت تحتاج فقط إلى صور ثابتة. المرونة لك.

### هل لديك أسئلة؟

اترك تعليقًا أدناه أو تواصل معي على GitHub. برمجة سعيدة، واستمتع بتحويل جداول البيانات إلى عروض شرائح مذهلة ببضع نقرات فقط!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل مخططات Excel إلى SVG باستخدام Aspose.Cells في Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells لـ .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية تحويل مخططات Excel إلى SVG باستخدام Aspose.Cells لـ .NET (دليل خطوة بخطوة)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}