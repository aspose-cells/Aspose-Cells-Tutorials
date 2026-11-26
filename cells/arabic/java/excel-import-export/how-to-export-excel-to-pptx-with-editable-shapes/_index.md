---
category: general
date: 2026-11-25
description: تعلم كيفية تصدير Excel إلى PPTX مع أشكال قابلة للتحرير. يوضح هذا الدليل
  أيضًا كيفية تحديد منطقة الطباعة وتحويل مخطط Excel للعروض التقديمية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: ar
lastmod: 2026-11-25
og_description: كيفية تصدير Excel إلى PPTX بأشكال قابلة للتحرير باستخدام Aspose.Cells،
  بالإضافة إلى نصائح لتحديد منطقة الطباعة وتحويل مخطط Excel للعروض التقديمية.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: كيفية تصدير Excel إلى PPTX مع أشكال قابلة للتحرير
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: كيفية تصدير Excel إلى PPTX بأشكال قابلة للتحرير
url: /ar/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى PPTX مع أشكال قابلة للتحرير

إذا كنت بحاجة إلى **how to export Excel** ملفات إلى PowerPoint مع الحفاظ على صناديق النص والأشكال القابلة للتحرير، فإن هذا الدليل يشرح لك العملية بالكامل. ستتعلم أيضًا كيفية **set print area** لشريحة مركزة وكيفية **convert Excel chart** بحيث تظل قابلة للتحرير بالكامل بعد التصدير.

تصدير Excel إلى PPTX شائع عند إنشاء عروض تقديمية من تقارير مدفوعة بالبيانات. باستخدام Aspose.Cells for Java تتجنب النسخ واللصق اليدوي، وتحافظ على التنسيق، وتكتسب تحكمًا برمجيًا في النتيجة.

## ما ستتعلمه

* تحميل دفتر عمل XLSX موجود يحتوي على صندوق نص أو مخطط.  
* تكوين خيارات التصدير بحيث يحتوي ملف PPTX الناتج على **editable shapes**.  
* **Set the print area** لتحديد نطاق التصدير إلى الخلايا التي تحتاجها.  
* حفظ ورقة العمل كملف PPTX والتحقق من إمكانية تحرير صناديق النص والمخططات في PowerPoint.  

**المتطلبات المسبقة**

* Java 17 أو أحدث مثبت.  
* Maven أو Gradle لإدارة التبعيات.  
* فهم أساسي لدفاتر عمل Excel وبرمجة Java.

---

## كيفية تصدير Excel إلى PPTX مع أشكال قابلة للتحرير

يوفر هذا القسم الكود الأساسي الذي يقوم بعملية التصدير. يستخدم المثال Aspose.Cells 23.9 (الأحدث عند كتابة هذا الدليل) ويظهر كل خطوة مطلوبة.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### لماذا كل سطر مهم

1. **Dependency** – توفر Aspose.Cells الفئة `ImageOrPrintOptions` التي يمكنها تحويل أوراق العمل إلى شرائح PPTX. إضافة هذه الفئة عبر Maven يضمن وجود المكتبة في مسار الفئة.  
2. **Imports** – استيراد الفئات الصحيحة يحافظ على نظافة الكود ويتجنب الأسماء المؤهلة بالكامل.  
3. **Loading the workbook** – يجب الإشارة إلى الملف الدقيق الذي يحتوي على الكائنات التي تريد تصديرها. يمكن أن يكون المسار مطلقًا أو نسبيًا إلى جذر المشروع.  
4. **Export options** – ضبط `setEditable(true)` هو المفتاح لـ **how to export Excel** بحيث تظل الأشكال في PowerPoint الناتج قابلة للتحرير. بدون هذا الإعداد، تتحول صناديق النص إلى صور ثابتة.  
5. **Print area** – يستدعي `setPrintArea` لتحديد نطاق التصدير إلى المنطقة المطلوبة، مما يقلل حجم الملف ويزيل الصفوف/الأعمدة غير المرغوب فيها. هذا يلبي مباشرةً متطلب **set print area excel**.  
6. **Saving** – الثابت `SaveFormat.PPTX` يخبر Aspose.Cells بإنشاء ملف PowerPoint بدلاً من صورة أو PDF.  

#### النتيجة المتوقعة

بعد تشغيل البرنامج، افتح `EditableShapes.pptx` في PowerPoint. يجب أن ترى شريحة تعكس النطاق المحدد في Excel، ويمكن النقر المزدوج على أي صندوق نص أو وسيلة إيضاح للمخطط وتحريره كما هو الحال مع كائنات PowerPoint الأصلية.

---

## تحديد نطاق الطباعة في Excel

عندما تحتاج فقط إلى جزء من ورقة العمل، فإن تعريف **print area** يحسن الأداء والوضوح البصري.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*نصيحة:* إذا قمت بتغيير نطاق البيانات لاحقًا، استدعِ `setPrintArea` مرة أخرى قبل التصدير. يحترم التصدير الإعداد الأخير.

---

## تحويل مخطط XLSX إلى مخطط PowerPoint قابل للتحرير

تتعامل Aspose.Cells مع المخططات ككائنات رسومية. بتمكين `setEditable(true)`، يتم تحويل المخطط إلى مخطط PowerPoint أصلي يمكن تحريره (مثل تغيير السلاسل أو عناوين المحاور).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

إذا كنت بحاجة إلى **how to convert xlsx** ملفات تحتوي على مخططات متعددة، كرّر عملية التصدير لكل ورقة عمل أو استخدم `Workbook.save` مع `SaveFormat.PPTX` بعد تعديل الورقة النشطة.

---

## كيفية تحويل XLSX برمجيًا (مكافأة)

إلى جانب PPTX، قد ترغب أيضًا في تحويل دفتر العمل إلى تنسيق آخر مثل PDF أو PNG. الفئة `ImageOrPrintOptions` نفسها تعمل مع هذه الأهداف:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

هذا يوضح القدرة الأوسع لـ **how to convert xlsx** في Aspose.Cells.

---

## المشكلات الشائعة ونصائح الممارسات الأفضل

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| الأشكال تتحول إلى صور | `setEditable(false)` (الافتراضي) | استدعِ `exportOptions.setEditable(true)` |
| الشريحة المصدرة فارغة | نطاق الطباعة لا يتضمن أي بيانات | تحقق من سلسلة النطاق الممررة إلى `setPrintArea` |
| المخطط يفقد التنسيق | استخدام نسخة قديمة من Aspose.Cells | قم بالترقية إلى أحدث مكتبة (≥ 23.9) |
| حجم الملف كبير | تصدير كامل ورقة العمل | قصر نطاق الطباعة أو إخفاء الصفوف/الأعمدة غير المستخدمة |

---

## الخلاصة

أنت الآن تعرف **how to export Excel** دفاتر العمل إلى PPTX مع أشكال ومخططات قابلة للتحرير بالكامل، وكيفية **set print area** لتركيز النتيجة، وكيفية **convert Excel chart** الكائنات لتعديل العرض التقديمي بسلاسة. يمكن إدراج مثال Java القابل للتنفيذ أعلاه في أي مشروع يستخدم Aspose.Cells بالفعل.

**الخطوات التالية**

* استكشف خيارات **convert excel chart** في PowerPoint (مثل تغيير نوع المخطط).  
* دمج هذا التصدير مع أتمتة **set print area excel** لإنشاء شرائح متعددة من دفتر عمل واحد.  
* جرّب التصدير إلى تنسيقات أخرى (PDF, PNG) باستخدام نمط `ImageOrPrintOptions` نفسه.

لا تتردد في تجربة نطاقات مختلفة، أوراق عمل متعددة، أو تخطيطات شرائح مخصصة. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحديد نطاق الطباعة في Excel وتصديره إلى PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [تحويل Excel إلى PowerPoint وتحديد نطاق الطباعة](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [تحديد نطاق الطباعة في Excel وتصديره إلى PowerPoint – دليل خطوة بخطوة](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}