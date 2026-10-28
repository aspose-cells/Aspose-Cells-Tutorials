---
category: general
date: 2026-08-14
description: تضمين الخطوط في SVG أثناء تصدير Excel إلى SVG باستخدام Aspose.Cells.
  تعلّم كيفية تحديد منطقة الطباعة، وضبط خيارات الطباعة، واستخدام دالة WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: ar
lastmod: 2026-08-14
og_description: تضمين الخطوط في SVG أثناء تصدير Excel إلى SVG باستخدام Aspose.Cells.
  يوضح هذا الدليل كيفية تحديد منطقة الطباعة، وتكوين خيارات الطباعة، وتطبيق دالة WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: تضمين الخطوط في SVG أثناء تصدير Excel إلى SVG – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: تضمين الخطوط في SVG أثناء تصدير Excel إلى SVG
url: /ar/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تضمين الخطوط في SVG أثناء تصدير Excel إلى SVG

إذا كنت بحاجة إلى **تضمين الخطوط في SVG أثناء تصدير Excel إلى SVG**، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for Java. سنغطي أيضًا كيفية **تحديد منطقة الطباعة**، **تحديد خيارات الطباعة**، و**استخدام دالة WRAPCOLS** لتنسيق البيانات دون فقدان التخطيط.

ستتبع مثالًا كاملاً قابلاً للتنفيذ يقوم بتحميل مصنف موجود، تطبيق صيغة `WRAPCOLS`، تكوين خيارات الصورة الخاصة بـ SVG، تعريف منطقة الطباعة، وأخيرًا حفظ الملف كـ SVG مع الخطوط المضمنة. لا تحتاج إلى أي وثائق خارجية—فقط انسخ الشيفرة، شغلها، وتفحص ملف SVG الناتج.

## تضمين الخطوط في SVG – تكوين ImageOrPrintOptions

يضمن تضمين الخطوط أن يتم عرض SVG تمامًا كما يظهر في Excel، حتى على الأجهزة التي لا تتوفر فيها الخطوط الأصلية مثبتة.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*لماذا هذا مهم*: عندما يتم تمكين `setEmbedFonts(true)`، تقوم Aspose.Cells بكتابة بيانات الخط مباشرةً داخل قسم `<defs>` في SVG. النتيجة هي ملف مستقل يبدو متطابقًا عبر المتصفحات والمنصات.

## تصدير Excel إلى SVG – سير العمل الكامل

الخطوات التالية توضح العملية من تحميل المصنف إلى حفظ ملف SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**الناتج المتوقع**: يظهر `output.svg` في `YOUR_DIRECTORY`. عند فتحه في المتصفح سيظهر ورقة العمل مع جميع الخطوط المضمنة، والبيانات مُلتفة إلى ثلاثة أعمدة (بفضل `WRAPCOLS`)، وتُعرض فقط الخلايا داخل `A1:H30`.

## تحديد منطقة الطباعة لورقة العمل

تحديد منطقة الطباعة يحد من SVG المُصدّر إلى نطاق معين، مما يقلل حجم الملف ويركز المشاهد على البيانات ذات الصلة.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*نصيحة*: النطاق يتبع صيغة A1 في Excel. إذا كنت بحاجة إلى نطاق ديناميكي، يمكنك حسابه برمجيًا باستخدام `ws.getCells().getMaxDisplayRange()`.

## تحديد خيارات الطباعة لإخراج SVG

تتحكم خيارات الطباعة في طريقة تحويل Aspose.Cells لورقة العمل إلى صورة. بالإضافة إلى تضمين الخطوط، يمكنك ضبط الدقة، والتكبير/التصغير، وتخطيط الصفحة.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*لماذا يجب عليك تحديد خيارات الطباعة*: بدون خيارات صريحة، تستخدم Aspose.Cells الإعدادات الافتراضية التي قد تتجاهل تضمين الخطوط أو تطبق عامل تكبير غير مرغوب فيه، مما يؤدي إلى SVG غير واضح أو غير مُنسق بشكل صحيح.

## استخدام دالة WRAPCOLS لتغليف بيانات الأعمدة

`WRAPCOLS` هي صيغة Excel توزع نطاقًا عموديًا على عدد محدد من الأعمدة. إنها مفيدة عندما تريد عرض قائمة طويلة في شبكة مدمجة.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

عند حفظ المصنف، تقوم Aspose.Cells بتقييم الصيغة، مما ينتج تخطيطًا من ثلاثة أعمدة داخل منطقة الطباعة المحددة. تعمل هذه التقنية على أي نطاق حجمي—فقط عدّل الوسيط الثاني إلى عدد الأعمدة المطلوب.

## مثال كامل قابل للتنفيذ

فيما يلي برنامج Java الكامل الذي يمكنك لصقه في أي بيئة تطوير. تأكد من وجود مكتبة Aspose.Cells for Java في مسار الـ classpath الخاص بك.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**خطوات التحقق**

1. شغّل البرنامج.  
2. افتح `output.svg` في متصفح ويب.  
3. تأكد من أن النص يستخدم نفس الخط كما في ملف Excel الأصلي (الخطوط مضمَّنة).  
4. تحقق من ظهور الخلايا داخل `A1:H30` فقط وأن البيانات من `A2:A10` معروضة في ثلاثة أعمدة.

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| الخطوط مفقودة في SVG | `setEmbedFonts(false)` أو ملف الخط غير متاح | تأكد من `setEmbedFonts(true)` وأن الخط مثبت على الجهاز الذي يشغّل الشيفرة |
| WRAPCOLS لا يتم تقييمه | محرك الحساب معطَّل | استدعِ `workbook.calculateFormula()` قبل التصدير، أو دع Aspose.Cells تقوم بالتقييم أثناء الحفظ |
| SVG المُصدّر فارغ | منطقة الطباعة لا تشمل أي بيانات | راجع النطاق الممرَّر إلى `setPrintArea` |
| ملف SVG كبير الحجم | لم يتم تطبيق أي تكبير/تصغير، دقة الصورة عالية | عدّل `imgOptions.setResolution(96)` أو ما شابه للتحكم في DPI |

## نصيحة احترافية: إعادة استخدام ImageOrPrintOptions لعدة أوراق عمل

إذا كان المصنف يحتوي على عدة أوراق تحتاج إلى إعدادات SVG متطابقة، أنشئ كائنًا واحدًا من `ImageOrPrintOptions` وعيّنه لكل `PageSetup` في أوراق العمل. هذا يقلل استهلاك الذاكرة ويضمن تضمين الخطوط بشكل متسق عبر جميع الملفات المُصدَّرة.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## الخطوات التالية

* **التصدير إلى صيغ متجهة أخرى** – غيّر `ImageFormat.SVG` إلى `ImageFormat.PDF` للحصول على ملفات PDF عالية الجودة.  
* **المعالجة الدفعية** – كرّر العملية على مجلد يحتوي على ملفات `.xlsx` لتوليد SVGs تلقائيًا.  
* **معالجة الخطوط المخصصة** – استخدم `FontSettings` لتحميل الخطوط من دليل محدد عندما تكون خطوط النظام غير كافية.  

بتقنّك **embed fonts in SVG**، **export excel to svg**، **set print area**، **set print options**، و**use WRAPCOLS function**، يمكنك أتمتة إنشاء SVG عالي الدقة للتقارير، ولوحات التحكم، والمرئيات الويب مباشرةً من بيانات Excel. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}