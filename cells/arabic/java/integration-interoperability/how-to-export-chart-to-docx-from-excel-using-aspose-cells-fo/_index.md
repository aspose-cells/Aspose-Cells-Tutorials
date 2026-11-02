---
category: general
date: 2026-08-20
description: تعلم كيفية تصدير المخطط إلى ملف docx وتحويل مصنف Excel إلى ملف docx باستخدام
  Aspose.Cells في Java. دليل خطوة بخطوة مع الكود الكامل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: ar
lastmod: 2026-08-20
og_description: تصدير المخطط إلى ملف docx وتحويل مصنف Excel إلى ملف docx باستخدام
  Aspose.Cells للغة Java. اتبع هذا الدرس الكامل القابل للتنفيذ.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: تصدير المخطط إلى ملف docx باستخدام Aspose.Cells – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: كيفية تصدير المخطط إلى ملف docx من Excel باستخدام Aspose.Cells للـ Java
url: /ar/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط إلى docx من مصنف Excel باستخدام Java

إذا كنت بحاجة إلى **export chart to docx** مباشرةً من ملف Excel، فإن هذا الدليل يوضح لك حلاً جاهزًا للتنفيذ. في نهاية الدليل ستعرف أيضًا كيفية **convert Excel workbook to docx** مع الحفاظ على مخطط قابل للتحرير، بحيث يمكن تعديل مستند Word الناتج دون فقدان الدقة.

تصدير المخططات شائع عندما تقوم بإنشاء تقارير تجمع بين حسابات الجداول وتنسيقات Word الغنية. تجعل Aspose.Cells for Java عملية التحويل بسيطة، وتتيح لك الـ API الحفاظ على المخطط قابلًا للتحرير—دون الحاجة إلى صورة ثابتة.

## ما يغطيه هذا الدليل

* تحميل مصنف موجود يحتوي على مخطط.  
* تهيئة `ImageOrPrintOptions` لاستهداف تنسيق DOCX.  
* تمكين علم `ExportEditableCharts` (متاح بدءًا من الإصدار 25.10).  
* حفظ المصنف كملف DOCX يحتفظ بمخطط قابل للتحرير.  

لا تحتاج إلى أدوات خارجية بخلاف ملف Aspose.Cells JAR. يعمل الكود مع Java 8+ وأي إصدار حديث من Aspose.Cells.

## المتطلبات المسبقة

| المتطلب | سبب الأهمية |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 أو أحدث) | تم تقديم ميزة `setExportEditableCharts` في هذا الإصدار. |
| **Java Development Kit (JDK) 8 أو أحدث** | يوفر بيئة التشغيل لتجميع وتنفيذ المثال. |
| **مصنف Excel (`.xlsx`) يحتوي على مخطط واحد على الأقل** | المخطط هو الكائن الذي سيتم تصديره إلى DOCX. |
| **بيئة تطوير Java أو أداة بناء (مثل Maven, Gradle)** | تبسط إدارة الاعتمادات والتنفيذ. |

يمكنك تنزيل أحدث ملف Aspose.Cells JAR من [Aspose website](https://products.aspose.com/cells/java/).

## الخطوة 1: إعداد المشروع وإضافة تبعية Aspose.Cells

إذا كنت تستخدم Maven، أضف التبعية التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

لـ Gradle، أضف:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

**نصيحة احترافية:** استخدم الإصدار الدقيق الذي قدم `ExportEditableCharts` (25.10) أو أي إصدار أحدث. الإصدارات القديمة ستتجاهل العلم وتنتج صورة ثابتة بدلاً من ذلك.

## الخطوة 2: تحميل المصنف الذي يحتوي على المخطط

تمثل الفئة `Workbook` ملف Excel بالكامل. تحميله عملية سطر واحد:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

**سبب الأهمية:** يجب تحميل المصنف بالكامل قبل أن تتمكن من تطبيق أي خيارات تصدير. إذا كان مسار الملف غير صحيح، فإن Aspose.Cells يطرح استثناء `FileNotFoundException`.

## الخطوة 3: تهيئة خيارات الصورة/الطباعة لإخراج DOCX

`ImageOrPrintOptions` يتحكم في كيفية عرض المصنف. ضبط صيغة الحفظ إلى `DOCX` يخبر Aspose.Cells بإنتاج مستند Word بدلاً من صورة.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

يمكنك أيضًا تعديل حجم الصفحة أو DPI أو جودة الصورة هنا، لكنها اختيارية لتصدير المخطط.

## الخطوة 4: تمكين تصدير المخططات القابلة للتحرير

بدءًا من الإصدار 25.10، يمكن لـ Aspose.Cells تضمين المخططات ككائنات مخطط Word أصلية. هذا يجعلها قابلة للتحرير بالكامل في Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

**حالة خاصة:** إذا قمت بتعيين هذا العلم إلى `false` (أو تركته)، سيتم عرض المخطط كصورة ثابتة. استخدم `true` فقط عندما يحتاج الجمهور المستهدف إلى تحرير المخطط بعد التحويل.

## الخطوة 5: حفظ المصنف كملف DOCX

أخيرًا، استدعِ `Workbook.save` مع الخيارات المهيأة:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

عند انتهاء البرنامج، افتح `ChartEditable.docx` في Microsoft Word. يجب أن ترى المخطط الأصلي، وإذا نقرت عليه بزر الفأرة الأيمن، سيكون خيار **Edit Data** متاحًا—مما يؤكد أن المخطط قابل للتحرير فعليًا.

## مثال كامل قابل للتنفيذ

فيما يلي ملف المصدر الكامل. انسخه إلى بيئة التطوير IDE الخاصة بك، استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي، ثم شغّله.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**النتيجة المتوقعة**

* ملف باسم `ChartEditable.docx` في الدليل المحدد.  
* فتح الملف في Word يعرض المخطط تمامًا كما ظهر في Excel، ويمكنك النقر المزدوج على المخطط لتحرير سلسلة البيانات الخاصة به.

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب | الحل |
|---------|-------|-----|
| Word يعرض **صورة ثابتة** بدلاً من مخطط قابل للتحرير | `setExportEditableCharts` لم يتم استدعاؤه أو تم استخدام إصدار أقل من 25.10 | تأكد من تعيين العلم إلى `true` وأنك تستخدم Aspose.Cells 25.10 أو أحدث. |
| ملف DOCX الناتج **فارغ** | مسار ملف المصنف المصدر غير صحيح أو أذونات غير كافية | تحقق من مسار المصنف وأن التطبيق لديه صلاحية القراءة/الكتابة. |
| مظهر المخطط **مشوه** | إعداد الصفحة في Excel (مثل الصفوف/الأعمدة المخفية) يختلف عن الإعدادات الافتراضية في Word | اضبط `ImageOrPrintOptions` (مثال `setOnePagePerSheet(true)`) للتحكم في التحجيم. |
| **الأداء** يتدهور في المصنفات الكبيرة | تصدير العديد من المخططات أو مجموعات بيانات كبيرة | قم بتصدير الأوراق المطلوبة فقط أو استخدم `setSheetIndex` لتحديد نطاق المعالجة. |

## توسيع الحل

* **مخططات متعددة:** كرّر عبر جميع أوراق العمل واستدعِ `worksheet.getCharts()` لتصدير كل مخطط على حدة.  
* **تنسيق DOCX مخصص:** بعد الحفظ، استخدم Aspose.Words لتطبيق رؤوس، تذييلات أو أنماط على المستند المُنشأ.  
* **تحويل دفعي:** ضع الكود داخل حلقة تعالج مجلدًا من ملفات `.xlsx`، وتنتج DOCX لكل منها.

## الخلاصة

أصبح لديك الآن طريقة موثوقة لـ **export chart to docx** و **convert Excel workbook to docx** مع الحفاظ على قابلية تحرير المخطط بالكامل. الخطوات الأساسية هي تحميل المصنف، تهيئة `ImageOrPrintOptions` لـ DOCX، تمكين `ExportEditableCharts`، وحفظ النتيجة.

جرّب خيارات إضافية—مثل ضبط هوامش الصفحة أو تضمين صيغ المصنف—لتخصيص المخرجات وفقًا لسير عمل التقارير الخاص بك. عندما تحتاج إلى إنشاء تقارير Word من بيانات Excel برمجيًا، يوفر هذا النهج حلاً نظيفًا وقابلًا للصيانة.

--- 

*هل أنت مستعد لتجربته؟ استنسخ المثال، حدّث مسارات الملفات، وشغّل البرنامج. إذا واجهت أي مشاكل، راجع وثائق Aspose.Cells for Java أو استكشف المواضيع ذات الصلة أدناه.*  

### مواضيع ذات صلة قد ترغب في استكشافها لاحقًا

* **convert excel workbook to pdf** – إنشاء تقارير PDF من نفس المصنف.  
* **Aspose.Cells chart formatting** – تخصيص الألوان، العلامات، والمحاور قبل التصدير.  
* **Embedding images in DOCX with Aspose.Words** – دمج المخططات مع محتوى Word آخر.  

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء مخطط Excel مع خط الاتجاه وتصديره كصورة باستخدام Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [أتمتة الوصول إلى مخططات Excel باستخدام Aspose.Cells Java: دليل خطوة بخطوة](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [تخصيص تسميات بيانات مخطط Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}