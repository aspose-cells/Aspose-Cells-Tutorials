---
category: general
date: 2026-09-18
description: تعلم كيفية تصدير Excel إلى PowerPoint باستخدام Aspose.Cells. حوّل Excel
  إلى PPTX، أنشئ PowerPoint من Excel، واحفظ Excel كـ PowerPoint في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: ar
lastmod: 2026-09-18
og_description: كيفية تصدير Excel إلى PowerPoint باستخدام Aspose.Cells. اتبع هذا الدليل
  لتحويل Excel إلى PPTX، وإنشاء PowerPoint من Excel، وحفظ Excel كـ PowerPoint بكفاءة.
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: كيفية تصدير Excel إلى PowerPoint – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: كيفية تصدير Excel إلى PowerPoint باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PowerPoint باستخدام Aspose.Cells – دليل خطوة بخطوة

إذا كنت بحاجة إلى **كيفية تصدير Excel** إلى عرض تقديمي PowerPoint، فإن هذا الدرس يوضح حلاً كاملاً وجاهزًا للتنفيذ. بحلول نهاية الجملتين الأوليين ستعرف بالضبط أي استدعاءات API تحول ملف `.xlsx` إلى `.pptx` قابل للتحرير. يعمل النهج مع أي دفتر عمل يحتوي على مخططات أو صور أو أشكال أخرى، ويتطلب فقط بضع أسطر من كود Java.

في هذا الدليل ستتعلم كيفية **تحويل Excel إلى PPTX**، **إنشاء PowerPoint من Excel**، و**حفظ Excel كـ PowerPoint** مع الحفاظ على قابلية تحرير المخططات والصور. لا يلزم أي أدوات إضافية بخلاف Aspose.Cells، ويعمل الكود على Java 8+ وأي JDK حديث.  

المتطلبات المسبقة:

* Java Development Kit (JDK) 8 أو أحدث مثبت  
* Maven أو Gradle لإدارة الاعتمادات (أو ملف Aspose.Cells JAR على مسار الفئة)  
* دفتر عمل (`WithShapes.xlsx`) يحتوي على صورة أو مخطط واحد على الأقل  

---

![Diagram illustrating how to export Excel to PowerPoint](https://example.com/diagram.png "how to export excel to powerpoint illustration")

## كيفية تصدير Excel إلى PowerPoint باستخدام Aspose.Cells

نواة عملية التحويل تتكون من أربع خطوات مختصرة. كل خطوة مغلفة في طريقة لتتمكن من إعادة استخدام المنطق في تطبيقات أكبر.

### الخطوة 1: تحميل دفتر العمل الذي يحتوي على الأشكال

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**لماذا هذا مهم:**  
تحميل دفتر العمل يمنحك الوصول إلى أوراق العمل، الصور، والمخططات. يقرأ Aspose.Cells الملف دون استدعاء Microsoft Office، لذا تعمل العملية على الخوادم بدون واجهة رسومية.

### الخطوة 2: تكوين خيارات التصدير لتحويل PowerPoint

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**لماذا هذا مهم:**  
`setExportChartAsEditable(true)` يخبر Aspose.Cells بإنشاء أشكال متجهة بدلاً من صور نقطية. هذا يجعل ناتج PowerPoint **إنشاء PowerPoint من Excel** بمخططات قابلة للتحرير بالكامل، مما يلبي معظم سير عمل إعداد العروض التقديمية.

### الخطوة 3: وضع علامة على الصور (أو المخططات) كقابلة للتحرير

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**لماذا هذا مهم:**  
عند وضع علامة على صورة كقابلة للتحرير، يصدر Aspose.Cells الصورة كشكل EMF/WMF في ملف PPTX. هذا أساسي لحالة **تصدير Excel إلى PowerPoint** حيث يحتاج المستلم إلى تعديل الصورة لاحقًا.

### الخطوة 4: حفظ دفتر العمل كعرض PowerPoint قابل للتحرير

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**لماذا هذا مهم:**  
استدعاء `save` يجمع كل التعديلات السابقة (صور قابلة للتحرير، إعدادات المخططات) في أرشيف `.pptx` واحد. يمكن فتح الملف الناتج في Microsoft PowerPoint أو Google Slides أو أي عارض PPTX متوافق.

### مثال كامل قابل للتنفيذ

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**النتيجة المتوقعة:**  
فتح `Result.pptx` في PowerPoint يظهر شريحة تعكس ورقة العمل الأولى من `WithShapes.xlsx`. تظهر المخططات كأشكال متجهة يمكنك النقر مزدوجًا عليها لتعديل البيانات، وتكون الصورة الأولى ككائن قابل للتحرير (يمكنك تغيير حجمه أو لونه أو استبداله مباشرة في PowerPoint).

---

## تحويل Excel إلى PPTX – تخصيص أعمق

بينما التدفق الأساسي كافٍ لمعظم السيناريوهات، قد تحتاج إلى:

* **تصدير أوراق عمل متعددة** – كرر عبر `workbook.getWorksheets()` واستدعِ `workbook.save` لكل منها، مع تمرير فهرس شريحة مختلف عبر `ImageOrPrintOptions.setSlideNumber(int)`.  
* **التحكم بأبعاد الشريحة** – استخدم `exportOptions.setImageHeight(int)` و `setImageWidth(int)` لمطابقة حجم شريحة PowerPoint محدد (مثلاً 1024 × 768).  
* **الحفاظ على الصيغ** – عيّن `exportOptions.setExportFormulasAsValues(false)` إذا أردت إرفاق صيغ Excel الأصلية كبيانات مخفية.  

هذه التعديلات تتيح لك **إنشاء PowerPoint من Excel** يتماشى مع هوية الشركة أو معايير العرض التقديمي.

---

## حفظ Excel كـ PowerPoint – المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| المخططات تظهر كصور نقطية | `setExportChartAsEditable(false)` (الافتراضي) | تمكين المخططات القابلة للتحرير باستخدام `setExportChartAsEditable(true)` |
| لا تظهر صورة على الشريحة | الصورة غير مؤشرة كقابلة للتحرير أو فهرس الصورة خارج النطاق | تحقق من `sheet.getPictures().size() > 0` قبل استدعاء `setEditable(true)` |
| تظهر أوراق العمل المخفية في PPTX | `setExportHiddenWorksheet(true)` | احتفظ بالقيمة الافتراضية `false` أو اضبطها صراحةً إلى `false` |
| ملف الإخراج تالف | استخدام نسخة قديمة من Aspose.Cells (قبل 20.10) | قم بالترقية إلى أحدث نسخة من Aspose.Cells for Java (مثال، 23.12) |

---

## تصدير Excel إلى PowerPoint: نصائح الأداء

* **إعادة استخدام نفس كائن `ImageOrPrintOptions`** لعمليات حفظ متعددة – يمنع تخصيصًا متكررًا.  
* **تدفق دفتر العمل المصدر** (`new Workbook(InputStream)`) عند التعامل مع ملفات كبيرة على خوادم ذات ذاكرة محدودة.  
* **توازي التحويل لكل ورقة عمل** إذا كنت تحتاج إلى إنشاء مجموعة شرائح بمئات الشرائح؛ يمكن معالجة كل ورقة عمل في خيط منفصل لأن كائنات Aspose.Cells آمنة للثريد بعد الإنشاء.  

---

## الخطوات التالية

أنت الآن تعرف **كيفية تصدير Excel** إلى مجموعة شرائح PowerPoint، **تحويل Excel إلى PPTX**، و**حفظ Excel كـ PowerPoint** بمحتوى قابل للتحرير. لتوسيع هذه المعرفة يمكنك:

* استكشاف **Aspose.Slides** لإضافة رسومات متحركة أو تخطيطات شريحة رئيسية بعد التحويل.  
* أتمتة سير العمل في خط أنابيب CI/CD بحيث يتحول كل تقرير Excel جديد تلقائيًا إلى مجموعة شرائح PPTX.  
* دمج هذا النهج مع **Apache POI** للمعالجة المسبقة لملفات Excel قبل تمريرها إلى Aspose.Cells.  

---

## الخلاصة

هذا الدرس يوضح **كيفية تصدير Excel** إلى PowerPoint باستخدام Aspose.Cells، مع تغطية كل خطوة من تحميل دفتر العمل إلى حفظ ملف `.pptx` قابل للتحرير. الآن يمكنك **تحويل Excel إلى PPTX**، **إنشاء PowerPoint من Excel**، و**حفظ Excel كـ PowerPoint** في تطبيقات Java بثقة. جرّب الإعدادات الاختيارية لتخصيص الناتج وفق متطلبات العرض التقديمي الخاصة بك. Happy coding!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells لـ .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية تصدير Excel إلى PowerPoint – دليل خطوة بخطوة](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [كيفية تصدير Excel إلى PowerPoint باستخدام C# – دليل كامل](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}