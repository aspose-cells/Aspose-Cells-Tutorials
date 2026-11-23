---
category: general
date: 2026-11-22
description: تعلم كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells للغة Java،
  بما في ذلك خطوات تصدير مخطط Excel إلى PowerPoint في سير عمل واحد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: ar
lastmod: 2026-11-22
og_description: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells للغة Java. اتبع هذا
  الدليل الكامل خطوة بخطوة لتصدير مخطط Excel إلى PowerPoint أيضًا.
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells للـ Java
url: /ar/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells للـ Java

إذا كنت بحاجة إلى **تحويل Excel إلى PowerPoint**، يوضح لك هذا الدليل طريقة بسيطة باستخدام Aspose.Cells للـ Java. ستتعرف أيضًا على كيفية **تصدير مخطط Excel إلى PowerPoint** كجزء من نفس العملية، بحيث يمكنك إدراج المخططات مباشرةً في عرض تقديمي دون النسخ واللصق اليدوي.

تحويل جداول البيانات إلى عروض شرائح شائع عندما تريد مشاركة رؤى مستندة إلى البيانات مع جمهور غير تقني. بدلاً من إعادة إنشاء المخططات في PowerPoint، يمكنك أتمتة العملية بالكامل، والحفاظ على التنسيق كما هو، وتوفير ساعات من العمل.

في هذا الدرس ستقوم بـ:

* إعداد Aspose.Cells في مشروع Maven أو Gradle.  
* تحميل دفتر عمل موجود يحتوي على البيانات والمخططات.  
* تهيئة `ImageOrPrintOptions` لاستهداف تنسيق PPTX.  
* حفظ دفتر العمل كعرض تقديمي PowerPoint.  
* التحقق من النتيجة ومعالجة الحالات الطرفية الشائعة.

> **المتطلبات المسبقة** – تحتاج إلى ترخيص صالح لـ Aspose.Cells للـ Java (أو يمكنك العمل بالإصدار التجريبي). يعمل الكود مع Java 8+ وأي بيئة تطوير تدعم Maven/Gradle.

![مخطط يوضح تحويل Excel إلى PowerPoint باستخدام Aspose.Cells](convert_excel_to_powerpoint.png)

## ما ستحتاجه

| العنصر | السبب |
|------|--------|
| **Java Development Kit (JDK) 8 or newer** | مطلوب لتجميع وتشغيل المثال. |
| **Maven or Gradle** | يبسط إدارة الاعتمادات لـ Aspose.Cells. |
| **Aspose.Cells for Java** | يوفر واجهات برمجة التطبيقات `Workbook` و `ImageOrPrintOptions` المستخدمة في التحويل. |
| **An Excel file (`shapes.xlsx`) containing at least one chart** | يوضح سيناريو *تصدير مخطط Excel إلى PowerPoint*. |

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **لماذا هذه الخطوة مهمة** – إضافة المكتبة تجعل الفئات `Workbook` و `ImageOrPrintOptions` و `SaveFormat` متاحة. بدون الاعتماد الصحيح لن يتم تجميع الكود.

## الخطوة 2: تحميل دفتر العمل الذي يحتوي على المخطط(ات)

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**شرح:**  
`Workbook` هو نقطة الدخول لجميع عمليات Excel. بتحميل `shapes.xlsx` تجلب كلًا من جداول البيانات وأي مخططات مدمجة إلى الذاكرة، مما يتيح التحويل اللاحق.

## الخطوة 3: إنشاء خيارات التحويل وتعيين التنسيق المستهدف إلى PPTX

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**لماذا نستخدم `ImageOrPrintOptions`؟**  
تتحكم هذه الخيارات في كيفية عرض كل ورقة عمل أو مخطط. تعيين `SaveFormat.PPTX` يوجه المكتبة لوضع كل ورقة (أو مخطط) على شريحة خاصة بها، مع الحفاظ على الدقة البصرية.

## الخطوة 4: حفظ دفتر العمل كعرض تقديمي PowerPoint

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**ماذا يحدث هنا؟**  
يقوم Aspose.Cells بالتكرار عبر أوراق العمل والمخططات في دفتر العمل، ويحولها إلى رسومات متوافقة مع الشرائح، ثم يكتب حزمة `.pptx` إلى الموقع المحدد. يمكن فتح الملف الناتج في Microsoft PowerPoint أو Google Slides أو أي عارض يدعم PPTX.

## الخطوة 5: التحقق من التحويل

1. افتح `withShapes.pptx` في PowerPoint.  
2. تأكد من أن كل ورقة Excel تظهر كشريحة منفصلة.  
3. تحقق من أن المخططات تحتفظ بألوانها، وأساطيرها، وعلامات البيانات.  

إذا كان المخطط مشوهًا، قد تحتاج إلى تعديل DPI في `ImageOrPrintOptions`:

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## تصدير مخطط Excel إلى PowerPoint – تعديل مركّز

أحيانًا تحتاج فقط إلى نقل مخطط واحد بدلاً من دفتر العمل بالكامل. يمكنك تحقيق ذلك بتحويل المخطط إلى صورة أولاً ثم إدراجها يدويًا في شريحة PowerPoint، لكن Aspose.Cells يبسط العملية:

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**لماذا هذا مهم:**  
يعزل المقتطف مخططًا واحدًا، يقلل من حجم الملف، ويمنحك تحكمًا أدق في أي من الرسومات تصبح شرائح. إنها الطريقة الأكثر مباشرةً لـ **تصدير مخطط Excel إلى PowerPoint** عندما لا تحتاج إلى دفتر العمل الكامل.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|-------|-----|
| **شرائح فارغة** | الورقة لا تحتوي على بيانات مرئية أو المخطط مخفي. | تأكد من أن المخطط مرئي وأن الورقة تحتوي على بيانات قبل الحفظ. |
| **صور منخفضة الدقة** | DPI الافتراضي هو 96، وقد يكون غير كافٍ للشرائح المطبوعة. | استدعِ `options.setResolution(200‑300)` قبل `workbook.save`. |
| **أنواع مخططات غير مدعومة** | أنواع المخططات الجديدة أو المخصصة قد لا تُعرض بشكل مثالي. | صدّر المخطط كصورة (`ImageFormat.PNG`) ثم أدخله يدويًا. |
| **أخطاء مسار الملف** | مسار نسبي غير صحيح على أنظمة تشغيل مختلفة. | استخدم `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` لمسارات مستقلة عن النظام. |

## نصائح احترافية لتحويلات على مستوى الإنتاج

* المعالجة الدفعية: تكرار عبر دليل يحتوي على ملفات Excel واستدعاء نفس منطق التحويل.  
* إدارة الذاكرة: بالنسبة لدفاتر العمل الكبيرة، استدعِ `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` لتقليل استهلاك الذاكرة.  
* تنشيط الترخيص: ضع ملف الترخيص (`Aspose.Cells.lic`) في مسار الفئة واستدعِ `License license = new License(); license.setLicense("Aspose.Cells.lic");` قبل أي استخدام لواجهة Aspose.  
* سلامة الخيوط: يجب أن يعمل كل خيط مع نسخة `Workbook` خاصة به؛ كائنات Aspose.Cells ليست آمنة للاستخدام المتعدد الخيوط.

## مثال كامل يعمل

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**الناتج المتوقع:**  

تشغيل البرنامج يطبع `Conversion completed successfully.` وينشئ ملفين:

* `withShapes.pptx` – مجموعة شرائح حيث تظهر كل ورقة عمل (ومخططاتها) على شريحة منفصلة.  
* `singleChart.pptx` – عرض تقديمي بشريحة واحدة يحتوي فقط على أول مخطط من دفتر العمل.

افتح هذه الملفات في PowerPoint للتحقق من أن المخططات تحتفظ بالتنسيق الأصلي وعلامات البيانات.

## الخلاصة

أنت الآن تعرف كيفية **تحويل Excel إلى PowerPoint** باستخدام Aspose.Cells للـ Java، ورأيت أيضًا الطريقة الأكثر كفاءة لـ **تصدير مخطط Excel إلى PowerPoint** عندما تحتاج إلى مرئيات محددة فقط. من خلال تهيئة `ImageOrPrintOptions` وتعيين `SaveFormat` إلى `PPTX`، تتولى المكتبة الجزء الأكبر من عملية عرض أوراق العمل والمخططات كرسومات متوافقة مع الشرائح.

من هنا يمكنك:

* أتمتة التحويلات الدفعية لأنابيب التقارير.  
* دمج ملف PPTX المُولد مع أصول شرائح أخرى باستخدام واجهة Apache POI `XSLF`.  
* استكشاف صيغ تصدير إضافية مثل PDF أو HTML للتوزيع عبر قنوات متعددة.

لا تتردد في تجربة إعدادات DPI، أو تخطيطات شرائح مخصصة، أو تضمين ملف PPTX المُولد في سير عمل البريد الإلكتروني. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تصدير ورقة Excel إلى PowerPoint باستخدام Aspose.Cells في Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [كيفية تحويل Excel إلى PDF في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [كيفية تصدير مخطط إلى docx من Excel باستخدام Aspose.Cells للـ Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}