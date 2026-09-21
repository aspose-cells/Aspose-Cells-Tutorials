---
category: general
date: 2026-09-21
description: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells في Java – تعلّم كيفية
  تصدير المخطط إلى PPTX وحفظ المصنف كملف PPTX في بضع أسطر من الشيفرة فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: ar
lastmod: 2026-09-21
og_description: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells في Java. يوضح هذا
  البرنامج التعليمي كيفية تصدير مخطط إلى PPTX وحفظ المصنف كملف PPTX مع صناديق نصية
  قابلة للتحرير.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: تحويل Excel إلى PowerPoint باستخدام Aspose.Cells في Java
url: /ar/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل Excel إلى PowerPoint باستخدام Aspose.Cells في Java

إذا كنت بحاجة إلى **تحويل Excel إلى PowerPoint**، فإن هذا الدليل يوضح لك طريقة مختصرة وجاهزة للإنتاج للقيام بذلك. ستتعرف على كيفية تصدير مخطط إلى PPTX، والحفاظ على صناديق النص قابلة للتحرير، و**حفظ المصنف كملف PPTX** في ثلاثة أسطر فقط من كود Java.

يقوم العديد من المطورين بتصدير البيانات إلى PDF، لكن PowerPoint غالبًا ما يكون الأنسب للعروض التي تتطلب مخططات حية وعناصر قابلة للتحرير. يغطي هذا البرنامج التعليمي كل ما تحتاجه—من إعداد المشروع إلى التعامل مع المشكلات الشائعة—حتى تتمكن من إنشاء عرض PowerPoint من مخطط Excel دون مغادرة بيئة تطوير Java الخاصة بك.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Java 17 أو أحدث مثبتة.
* Maven (أو Gradle) لإدارة التبعيات.
* ترخيص Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي للتقييم).
* ملف Excel (`ChartAndTextbox.xlsx`) يحتوي على مخطط واحد على الأقل وصندوق نص.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

الخطوة الأولى هي تضمين مكتبة Aspose.Cells. باستخدام Maven، أضف التبعية التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن المكافئ هو:
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

إدراج المكتبة يمنحك الوصول إلى `Workbook` و `PdfSaveOptions` وعداد `SaveFormat` المطلوبين للتحويل.

## الخطوة 2: تحميل المصنف الذي يحتوي على المخطط وصندوق النص

الآن قم بتحميل ملف Excel. تقوم فئة `Workbook` بقراءة المصنف بالكامل في الذاكرة، مع الحفاظ على المخططات والصيغ وصناديق النص.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**لماذا هذا مهم:** تحميل المصنف أولاً يضمن أن جميع الكائنات المدمجة (المخططات، الصور، صناديق النص) متاحة لعملية التصدير. إذا تعذر العثور على الملف، فإن Aspose.Cells يرمي استثناء `FileNotFoundException` واضح، يمكنك التقاطه لتوفير تجربة مستخدم أفضل.

## الخطوة 3: تكوين خيارات التصدير للحفاظ على صناديق النص قابلة للتحرير

تستخدم Aspose.Cells `PdfSaveOptions` للتحكم في طريقة كتابة الكائنات عندما يكون التنسيق المستهدف هو PowerPoint. من خلال تمكين `setExportEditableTextBoxes(true)`، يظل أي صندوق نص في ورقة Excel قابلاً للتحرير بعد التحويل.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **لماذا نستخدم `PdfSaveOptions` لـ PPTX؟**  
> داخليًا، تعيد Aspose.Cells استخدام خط أنابيب تصيير PDF لإنتاج PowerPoint، مما يسمح بالتحكم الدقيق في العناصر القابلة للتحرير. ضبط هذا العلم هو الطريقة الموصى بها للحفاظ على قابلية تحرير صندوق النص.

## الخطوة 4: حفظ المصنف كعرض تقديمي PowerPoint

أخيرًا، استدعِ `workbook.save` مع `SaveFormat.PPTX`. تكمل هذه الخطوة سير عمل **إنشاء PowerPoint من مخطط Excel**.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

بوضع كل شيء معًا، يبدو البرنامج الكامل كالتالي:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج يتم طباعة:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

عند فتح `Result.pptx` في Microsoft PowerPoint، ستلاحظ ما يلي:

* يتم عرض المخطط الأصلي من Excel كمخطط PowerPoint أصلي (قابل للتحرير في محرر المخططات الخاص بـ PowerPoint).
* يظهر صندوق النص من Excel كشكل قابل للتحرير، مما يسمح لك بتغيير النص مباشرةً على الشريحة.

## التعامل مع الحالات الحدية الشائعة

| الحالة | النهج الموصى به |
|-----------|----------------------|
| **الملف غير موجود** | ضع مُنشئ `Workbook` داخل كتلة `try‑catch` واعرض رسالة واضحة. |
| **المصنف لا يحتوي على مخطط** | تحقق من أن الورقة تحتوي على مخطط (`worksheet.getCharts().getCount() > 0`) قبل التحويل؛ وإلا، تخطِ الخطوة أو أضف عنصرًا نائبًا. |
| **ملفات Excel الكبيرة** | زد حجم ذاكرة JVM (`-Xmx2g`) لتجنب `OutOfMemoryError` أثناء التصيير. |
| **عدم ضبط الترخيص** | استدعِ `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` قبل تحميل المصنف لإزالة علامة التقييم. |

## الأسئلة المتكررة

**س: هل يمكنني تحويل عدة أوراق عمل إلى شرائح PowerPoint منفصلة؟**  
ج: نعم. قم بالتكرار عبر كل ورقة عمل، صدّر مخططها إلى شريحة جديدة باستخدام `PdfSaveOptions`، ثم احفظ المصنف مرة واحدة بعد معالجة جميع الأوراق.

**س: هل يحافظ هذا الأسلوب على تنسيق الخلايا؟**  
ج: يتم نقل مخططات وصناديق النص فقط إلى PowerPoint. يبقى تنسيق الخلايا في ملف Excel ولا يظهر في ملف PPTX.

**س: ماذا لو أردت التصدير إلى PDF بدلاً من PPTX؟**  
ج: استخدم `SaveFormat.PDF` و`PdfSaveOptions` نفسها. علم `setExportEditableTextBoxes` يعمل أيضًا مع PDF.

## الخطوات التالية

الآن بعد أن عرفت كيفية **حفظ المصنف كـ PPTX** و**تصدير المخطط إلى PPTX**، يمكنك استكشاف ما يلي:

* إضافة مخططات متعددة إلى شرائح مختلفة (`create powerpoint from excel chart` باستخدام حلقة).
* تخصيص تخطيطات الشرائح باستخدام Aspose.Slides for Java للحصول على تنسيق عرض تقديمي أكثر غنى.
* تضمين صور من خلايا Excel في PowerPoint باستخدام فئة `Picture`.

تتيح لك هذه الإضافات بناء خطوط أنابيب تقارير مؤتمتة بالكامل تُنتج عروضًا تقديمية مصقولة مباشرةً من بيانات Excel.

---

**ملخص:** يوضح هذا البرنامج التعليمي طريقة موثوقة **لتحويل Excel إلى PowerPoint** باستخدام Aspose.Cells for Java. من خلال تحميل المصنف، تكوين `PdfSaveOptions` للحفاظ على صناديق النص قابلة للتحرير، وحفظه باستخدام `SaveFormat.PPTX`، ستحصل على ملف PowerPoint يحتوي على مخططات حية وأشكال قابلة للتحرير—مثالي للعروض التقديمية الديناميكية. لا تتردد في تعديل الكود للمعالجة الدفعية أو دمجه في حلول تقارير أكبر.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}