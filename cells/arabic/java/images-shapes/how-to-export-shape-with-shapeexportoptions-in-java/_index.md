---
category: general
date: 2026-10-01
description: تعلم كيفية تصدير الشكل باستخدام ShapeExportOptions في جافا، مع الحفاظ
  على إمكانية تعديل الشكل عند التحويل إلى PPTX باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: ar
lastmod: 2026-10-01
og_description: تصدير الشكل باستخدام ShapeExportOptions في Java لإنشاء ملفات PPTX
  قابلة للتحرير. يشرح هذا البرنامج التعليمي العملية بالكامل باستخدام Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: تصدير الشكل باستخدام ShapeExportOptions في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: كيفية تصدير الشكل باستخدام ShapeExportOptions في جافا
url: /ar/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير الشكل باستخدام ShapeExportOptions في Java

إذا كنت بحاجة إلى **تصدير الشكل باستخدام ShapeExportOptions** من مصنف Excel، فإن هذا الدليل يوضح لك الخطوات الدقيقة. ستتعرف على كيفية الحفاظ على قابلية تعديل الشكل عند تحويله إلى ملف PPTX، وهو أمر أساسي للتحرير اللاحق في PowerPoint.

تصدير الأشكال هو مهمة شائعة عندما تقوم بإنشاء عروض شرائح من جداول البيانات—سواءً كنت تبني عروض مبيعات، أو لوحات تقارير، أو عروض تقديمية آلية. يغطي هذا البرنامج التعليمي كل ما تحتاجه، من إعداد المشروع إلى التحقق من الملف المُصدّر، ويستخدم مكتبة **Aspose.Cells for Java**.

## ما ستحتاجه

قبل أن تبدأ، تأكد من توفر ما يلي:

- Java 17 أو أحدث (الكود يتوافق مع أي JDK حديث)
- Maven أو Gradle لإدارة الاعتمادات
- ملف Excel (`Shapes.xlsx`) يحتوي على صندوق نص أو أي شكل آخر
- إلمام أساسي بواجهات Aspose.Cells API

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك (Aspose Cells export shape)

إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

لـ Gradle، ضع هذا في `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **نصيحة احترافية:** سجّل رخصتك مبكرًا لتجنب علامات التقييم المائية.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## الخطوة 2: تحميل المصنف الذي يحتوي على الشكل

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

كائن `Workbook` يمثل ملف Excel بالكامل. تحميله هو الشرط الأول لأي عملية تعديل للأشكال.

## الخطوة 3: الوصول إلى ورقة العمل واسترجاع الشكل المطلوب (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **لماذا هذا مهم:** تُخزن الأشكال على مستوى كل ورقة عمل، لذا يجب الانتقال إلى الورقة الصحيحة قبل أن تتمكن من تصدير شكل معين.

## الخطوة 4: تكوين **ShapeExportOptions** للحفاظ على قابلية تعديل الشكل (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

ضبط `ExportAsEditable` على `true` يخبر Aspose.Cells بالحفاظ على بيانات المتجهات الخاصة بالشكل، مما يسمح لمستخدمي PowerPoint بتعديل الشكل بعد الاستيراد.

## الخطوة 5: تصدير الشكل مباشرة إلى ملف PPTX (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

طريقة `exportToImage` تعمل لعدة صيغ صور؛ عندما ينتهي اسم الملف المستهدف بـ `.pptx`، يقوم Aspose.Cells بإنشاء شريحة PowerPoint تحتوي على الشكل.

### النتيجة المتوقعة

- يظهر الملف `textbox.pptx` في الدليل المحدد.
- عند فتح الملف في PowerPoint تظهر شريحة واحدة تحتوي على صندوق النص الأصلي.
- يكون صندوق النص قابلاً للتعديل بالكامل (يمكنك تغيير النص، الخط، الحجم، إلخ).

## الخطوة 6: التحقق من النتيجة ومعالجة الحالات الشائعة

### التحقق برمجياً

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

إذا كان `slideCount` يساوي `1`، فإن التصدير نجح.

### حالة خاصة: عدة أشكال

إذا كانت ورقة العمل تحتوي على عدة أشكال وتريد فقط شكلًا محددًا، حدد موقعه بالاسم:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### حالة خاصة: الشكل غير موجود

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### حالة خاصة: التصدير إلى صيغ أخرى

يدعم `ShapeExportOptions` أيضًا PNG، JPEG، SVG، و EMF. غيّر امتداد الملف واستخدم `exportOptions.setImageFormat(ImageFormat.PNG)` إذا لزم الأمر.

## مثال كامل قابل للتنفيذ

جمع جميع الأجزاء معًا يمنحك برنامجًا مستقلاً يمكنك نسخه ولصقه في بيئة التطوير المتكاملة الخاصة بك:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

تشغيل البرنامج ينشئ `textbox.pptx`. افتحه في PowerPoint، انقر بزر الماوس الأيمن على صندوق النص، وسترى مقابض التحرير المعتادة—مما يؤكد أن **تصدير الشكل باستخدام ShapeExportOptions** حافظ على قابلية التعديل.

## الأسئلة المتكررة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني تصدير شكل مخطط؟* | نعم. نفس استدعاء `exportToImage` يعمل مع المخططات، الصور، وSmartArt. |
| *ماذا لو احتجت إلى PNG بدقة أعلى؟* | اضبط `options.setImageFormat(ImageFormat.PNG)` وغيّر `options.setResolution(300)` قبل التصدير. |
| *هل ملف PPTX المُصدّر متوافق مع إصدارات PowerPoint القديمة؟* | المكتبة تكتب Office Open XML (PPTX) المدعوم من PowerPoint 2007 وما بعده. |
| *هل أحتاج إلى رخصة لتشغيل هذا؟* | النسخة التجريبية المجانية تعمل ولكنها تضيف علامة مائية. سجّل رخصة لإزالتها. |

## الخطوات التالية

- استكشف **Aspose.Slides for Java** إذا كنت بحاجة إلى دمج عدة أشكال مُصدَّرة في مجموعة شرائح واحدة.
- استخدم **ShapeExportOptions.setExportAsEditable(false)** عندما تفضّل صورة نقطية (PNG/JPEG) لتسريع العرض.
- أتمتة المعالجة الدفعية: كرّر عبر جميع أوراق العمل وصدر كل شكل إلى ملفات PPTX منفصلة.

---

### الخلاصة

أصبحت الآن تعرف كيفية **تصدير الشكل باستخدام ShapeExportOptions** في Java، مع الحفاظ على قابلية التعديل عند تحويل صندوق نص (أو أي شكل آخر) إلى ملف PPTX. باتباع الخطوات السابقة—إعداد المكتبة، تحميل المصنف، تكوين `ShapeExportOptions`، واستدعاء `exportToImage`—يمكنك دمج تصدير الأشكال في أي خط أنابيب تقارير آلي.

لا تتردد في تجربة أشكال مختلفة، صيغ إخراج، وإعدادات دقة. إذا وجدت هذا الدليل مفيدًا، شاركه مع زملائك أو احفظه للرجوع إليه لاحقًا. برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Adjust Shape Margins in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [How to Apply 3D Shape Formatting in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Workbook Shape Copying Guide](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}