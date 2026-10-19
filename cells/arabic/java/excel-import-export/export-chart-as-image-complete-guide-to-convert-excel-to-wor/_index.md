---
category: general
date: 2026-06-30
description: صدّر المخطط كصورة وتعرّف على كيفية تصدير المخطط، حفظ Excel كملف Word،
  تحويل Excel إلى Word، وتحويل XLSX إلى DOCX في بضع خطوات سهلة.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: ar
og_description: تصدير المخطط كصورة وتحويل Excel إلى Word بسرعة. اتبع هذا الدليل لحفظ
  Excel كملف Word، وتصدير المخططات، وتحويل XLSX إلى DOCX.
og_title: تصدير المخطط كصورة – تحويل إكسل إلى وورد خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: تصدير المخطط كصورة – دليل شامل لتحويل إكسل إلى وورد
url: /ar/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير المخطط كصورة – دليل كامل لتحويل Excel إلى Word

هل تساءلت يومًا كيف يمكنك تصدير المخطط كصورة من مصنف Excel وإدراجه مباشرةً في مستند Word؟ لست وحدك—المطورون يسألون باستمرار: “كيف يمكنني تصدير المخطط من XLSX وإدراجه في DOCX دون فقدان الجودة؟”

الخبر السار هو أنه ببضع أسطر من كود Java يمكنك **تصدير المخطط كصورة**، ثم **حفظ Excel كـ Word** في تدفق واحد سلس. في هذا الدرس سنستعرض العملية بالكامل، بدءًا من تحميل المصنف وحتى تكوين خيارات الحفظ التي تحول مخططاتك إلى PNG واضح داخل ملف DOCX.

سنتطرق أيضًا إلى مهام ذات صلة مثل **convert Excel to Word**، **save Excel as Word**، و**convert XLSX to DOCX**—كل ذلك مع الحفاظ على وضوح الكود وقابليته للتنفيذ. لا حشو، مجرد حل عملي يمكنك نسخه‑ولصقه اليوم.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- **Java Development Kit (JDK) 8+** – الكود يعمل على أي JDK حديث.
- مكتبة **Aspose.Cells for Java** (الإصدار 23.10 أو أحدث). يمكنك الحصول عليها من Maven Central أو تحميل ملف JAR مباشرة.
- ملف **Excel** (`charts.xlsx`) يحتوي على مخطط واحد على الأقل تريد تصديره.
- **IDE للـ Java** (IntelliJ IDEA، Eclipse، أو VS Code) – أي منها يناسبك.
- إلمام أساسي بـ Java وMaven/Gradle (اختياري لكن مفيد).

هذا كل شيء. لا إضافات أخرى، لا COM interop، فقط Java صافية.

---

## الخطوة 1: تحميل مصنف Excel وتحديد موقع المخطط

أول ما علينا فعله هو فتح المصنف الذي يحتوي على المخطط. تجعل Aspose.Cells ذلك سهلًا—فقط أشِر إلى مسار الملف.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **لماذا هذا مهم:** تحميل المصنف يمنحنا الوصول إلى كائن المخطط، والذي سنخبر Aspose لاحقًا بتحويله إلى صورة. إذا كان المصنف يحتوي على عدة أوراق أو مخططات، يمكنك تعديل الفهارس أو التكرار عبرها.

---

## الخطوة 2: تكوين خيارات حفظ DOCX لتصدير المخططات كصور

توفر Aspose.Cells فئة `DocxSaveOptions` التي تسمح لك بالتحكم في سلوك التحويل. ضبط `setExportChartAsImage(true)` يخبر المكتبة بتحويل كل مخطط إلى صورة قبل إدراجه في ملف Word.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **نصيحة احترافية:** إذا كنت تفضل الرسومات المتجهية (EMF/WMF) يمكنك ترك هذا الخيار غير مفعّل، لكن الصور النقطية عادةً ما تُظهر بشكل أكثر اتساقًا عبر إصدارات Word المختلفة.

---

## الخطوة 3: حفظ المصنف كملف DOCX

بعد ضبط الخيارات، نكتفي بحفظ المصنف. تتولى المكتبة تحويل جميع الأوراق، الجداول، وبفضل الإعداد الذي فعلناه—المخططات كصور.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **ما ستحصل عليه:** ملف `charts.docx` حيث يظهر المخطط الأصلي من Excel كصورة PNG عالية الدقة (أو JPEG حسب إعداداتك) داخل مستند Word. افتحه في Microsoft Word لتشاهد النتيجة.

---

## الخطوة 4: التحقق من النتيجة (اختياري لكن موصى به)

من الجيد دائمًا التحقق برمجيًا من نجاح التحويل، خاصةً عند أتمتة عمليات الدفعة.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

إذا نفّذت المقتطف ورأيت رسالة النجاح، فقد قمت فعليًا **convert XLSX to DOCX** مع الحفاظ على المخططات كصور.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ بلغة Java الذي يجمع جميع الخطوات. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**الناتج المتوقع عند تشغيل البرنامج:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

افتح `charts.docx` في Microsoft Word، وسترى المخطط معروضًا كصورة نظيفة، موضوعة بدقة في الموضع الذي كان فيه المخطط الأصلي في Excel.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كان المصنف يحتوي على عدة مخططات؟

لا تحتاج لتغيير شيء—ضبط `setExportChartAsImage(true)` يطبق على **جميع** المخططات في المصنف. إذا أردت تحويل مخططات معينة فقط إلى صور، سيتعين عليك تصديرها يدويًا باستخدام `chart.toImage()` ثم إدراجها في ملف Word بنفسك.

### هل يمكن التحكم بصيغة الصورة (PNG أم JPEG)؟

تستخدم Aspose.Cells PNG كإعداد افتراضي لتصدير المخططات كصور. للتحويل إلى JPEG، يمكنك تعديل `ImageOrPrintOptions` قبل الحفظ:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### هل يعمل هذا مع ملفات Excel القديمة (.xls)؟

بالطبع. نفس الكود يعمل مع كل من `.xls` و`.xlsx`. تقوم Aspose.Cells بالكشف التلقائي عن الصيغة، لذا يمكنك **save Excel as Word** بغض النظر عن نسخة المصدر.

### كيف يختلف هذا عن “convert Excel to Word” باستخدام interop الأصلي لـ Office؟

يتطلب interop الأصلي عادةً جهاز Windows مثبت عليه Office، وقد تفقد المخططات جودتها. استخدام Aspose.Cells لا يعتمد على نظام تشغيل معين، يعمل على Linux/macOS، ويحافظ على جودة المخطط عبر تحويله إلى صورة نقطية.

---

## نصائح لتطبيقات جاهزة للإنتاج

- **معالجة دفعات:** كرر العملية على جميع ملفات XLSX في مجلد معين، مع تطبيق نفس `DocxSaveOptions`. احيط التحويل بكتلة `try‑catch` للتعامل مع الملفات التالفة بأمان.
- **إدارة الذاكرة:** بالنسبة للمصنفات الكبيرة جدًا، استدعِ `workbook.dispose()` بعد الحفظ لتحرير الموارد الأصلية.
- **تخصيص:** يمكنك أيضًا ضبط `saveOptions.setPreserveCellFormatting(true)` إذا احتجت للحفاظ على تنسيقات الخلايا أثناء التحويل.
- **التسجيل (Logging):** دمج إطار تسجيل (SLF4J، Log4j) لتسجيل إحصائيات التحويل—مفيد لتتبع عمليات المراجعة.

---

## الخلاصة

أصبح لديك الآن حل شامل من البداية للنهاية يتيح لك **export chart as image**، **save Excel as Word**، و**convert XLSX to DOCX** ببضع أسطر من Java فقط. الفكرة الأساسية هي أن `DocxSaveOptions` في Aspose.Cells يجعل التعامل مع المخططات سهلًا—دون استخراج يدوي للصور، دون COM interop، ومع دعم كامل عبر المنصات.

لا تتردد في التجربة: جرّب تصدير أوراق عمل متعددة، عدّل دقة الصور، أو اجمع هذا النهج مع مكتبات Aspose أخرى (مثل Aspose.Words) لإنشاء مستندات Word أغنى. السماء هي الحد عندما تعرف كيف تصدر المخطط بصورة صحيحة.

هل لديك أسئلة إضافية حول تحويل ملفات Excel، إدراج الصور، أو تحسين الأداء؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Excel Chart to Image with Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}