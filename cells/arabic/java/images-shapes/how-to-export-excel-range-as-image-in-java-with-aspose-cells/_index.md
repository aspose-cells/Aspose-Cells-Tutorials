---
category: general
date: 2026-10-10
description: تعلم كيفية تصدير نطاق إكسل كصورة في جافا باستخدام Aspose.Cells. يغطي
  الدليل أيضًا تصدير الخلايا المحددة كصورة وحفظ ورقة عمل إكسل كصورة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: ar
lastmod: 2026-10-10
og_description: تصدير نطاق Excel كصورة في Java مع حل خطوة بخطوة. يتضمن تصدير الخلايا
  المحددة كصورة وحفظ ورقة عمل Excel كصورة.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: تصدير نطاق Excel كصورة في Java – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: كيفية تصدير نطاق إكسل كصورة في جافا باستخدام Aspose.Cells
url: /ar/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير نطاق Excel كصورة في Java باستخدام Aspose.Cells

إذا كنت بحاجة إلى **export Excel range as image**، فإن هذا الدرس يشرح لك حلاً كاملاً بلغة Java باستخدام مكتبة Aspose.Cells. ستتعلم أيضًا كيفية **export selected cells as image** وكيفية **save Excel worksheet as picture** لأغراض التقارير أو الوثائق.

تصدير جزء من المصنف إلى صورة يلغي الحاجة إلى أدوات التقاط الشاشة من طرف ثالث ويضمن نتائج دقيقة على مستوى البكسل. بنهاية هذا الدليل ستحصل على طريقة قابلة لإعادة الاستخدام تكتب ملف PNG (أو أي تنسيق مدعوم) مباشرةً إلى القرص، جاهزة للإدراج في ملفات PDF، رسائل البريد الإلكتروني، أو صفحات الويب.

## المتطلبات المسبقة

* Java 17 أو أحدث مثبت.
* Maven 3.8+ (أو أداة بناء أخرى يمكنها التعامل مع تبعيات Maven).
* رخصة Aspose.Cells for Java (التقييم المجاني يعمل لكنه يضيف علامة مائية).
* ملف Excel تجريبي (`input.xlsx`) موجود في دليل معروف.

الأقسام التالية تفترض أنك مرتاح مع تطوير Java الأساسي وإعداد مشروع Maven.

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أضف تبعية Aspose.Cells Maven إلى ملف `pom.xml`. توفر هذه المكتبة الفئات `Workbook` و `Worksheet` و `ImageOrPrintOptions` المستخدمة في مثال الشيفرة.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** حافظ على تحديث رقم الإصدار؛ الإصدارات الأحدث تضيف دعمًا للتنسيقات وتحسينات في الأداء.

## الخطوة 2: إنشاء طريقة مساعدة لتصدير نطاق

تغليف منطق التصدير في طريقة يجعل من السهل إعادة استخدامها عبر المشاريع ومعالجة الحالات الخاصة مثل الخلايا المدمجة أو الصفوف المخفية.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### لماذا هذه الطريقة مهمة

* **Separation of concerns:** التحميل، تكوين الخيارات، والتصدير مقسمة بوضوح.
* **Flexibility:** يمكنك تغيير تنسيق الصورة أو DPI دون تعديل المنطق الأساسي.
* **Error handling:** رمي `Exception` يسمح للمتصل بتحديد ما إذا كان سيقوم بالتسجيل، إعادة المحاولة، أو الإلغاء.

## الخطوة 3: استدعاء الطريقة مع معلمات حقيقية

فيما يلي طريقة `main` بسيطة توضح كيفية **export selected cells as image** وأيضًا كيفية **save Excel worksheet as picture** باستخدام نطاق الورقة الكامل.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### النتيجة المتوقعة

Running the program creates two PNG files:

* `range.png` – صورة تحتوي فقط على الخلايا **A1:G20**.
* `full_sheet.png` – صورة للمنطقة المستخدمة بالكامل في الورقة الأولى، مما يعني **saving Excel worksheet as picture**.

يمكنك فتح الملفات بأي عارض صور للتحقق من أن التخطيط البصري يتطابق مع عرض Excel، بما في ذلك حدود الخلايا، الألوان، والخلايا المدمجة.

## الخطوة 4: معالجة الحالات الخاصة الشائعة

### 1. الخلايا المدمجة

تقوم Aspose.Cells تلقائيًا بالحفاظ على مظهر الخلايا المدمجة، ولكن إذا كنت بحاجة إلى التحكم في العرض، اضبط `options.setOnePagePerSheet(true)` لإجبار الورقة بأكملها على صفحة واحدة قبل التصدير.

### 2. الصفوف أو الأعمدة المخفية

By default, hidden rows/columns are not rendered. To include them, enable:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. النطاقات الكبيرة واستهلاك الذاكرة

Exporting very large ranges can consume significant memory. If you encounter `OutOfMemoryError`, consider:

* تقليل DPI (`options.setHorizontalResolution(150)`).
* تصدير النطاق على أجزاء أصغر وتجميع الصور معًا باستخدام مكتبة رسومات.

## الخطوة 5: التحقق من النتيجة برمجيًا (اختياري)

If your downstream process needs to confirm that the image was generated correctly, you can load the PNG using `javax.imageio.ImageIO` and check its dimensions:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

عرض وارتفاع غير صفرين يشيران إلى نجاح عملية التصدير.

## الخلاصة

أنت الآن تعرف كيفية **export Excel range as image** في Java، وكيفية **export selected cells as image**، وكيفية **save Excel worksheet as picture** باستخدام Aspose.Cells. طريقة `exportRangeAsImage` القابلة لإعادة الاستخدام تُجرد التعقيد، وتتيح لك التحكم في جودة الصورة، وتعمل مع أي فهرس ورقة عمل أو نطاق خلايا.

Next steps you might explore:

* تحويل PNG إلى PDF باستخدام Aspose.PDF للتقارير.
* معالجة دفعة من عدة مصنفات في دليل.
* دمج تصدير الصورة في نقطة نهاية REST باستخدام Spring Boot حتى يتمكن العملاء من طلب الصور عند الحاجة.

لا تتردد في تجربة تنسيقات صور مختلفة (`ImageFormat.JPEG`, `ImageFormat.BMP`) وإعدادات DPI لتلبية متطلبات المشروع البصرية. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تصدير مصنف Excel كصورة باستخدام Aspose.Cells للـ Java: دليل خطوة بخطوة](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [كيفية إنشاء مخطط Excel مع خط الاتجاه وتصديره كصورة باستخدام Aspose.Cells للـ Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [تصدير خلايا Excel إلى صورة باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}