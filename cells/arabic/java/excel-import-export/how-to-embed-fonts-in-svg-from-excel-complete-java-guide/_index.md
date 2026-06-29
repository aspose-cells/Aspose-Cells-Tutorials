---
category: general
date: 2026-06-27
description: كيفية تضمين الخطوط في SVG من Excel باستخدام Aspose.Cells. تعلّم تصدير
  Excel إلى SVG، تحويل xlsx إلى SVG، وتضمين الخطوط في SVG بكفاءة.
draft: false
keywords:
- how to embed fonts
- export excel to svg
- convert excel to vector
- embed fonts in svg
- convert xlsx to svg
language: ar
og_description: كيفية تضمين الخطوط في SVG من Excel باستخدام Aspose.Cells. دليل خطوة
  بخطوة لتصدير Excel إلى SVG، وتضمين الخطوط، وتحويل xlsx إلى SVG.
og_title: كيفية تضمين الخطوط في SVG من Excel – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to embed fonts in SVG from Excel using Aspose.Cells. Learn to export
    Excel to SVG, convert xlsx to SVG, and embed fonts in SVG efficiently.
  headline: How to Embed Fonts in SVG from Excel – Complete Java Guide
  type: TechArticle
- description: How to embed fonts in SVG from Excel using Aspose.Cells. Learn to export
    Excel to SVG, convert xlsx to SVG, and embed fonts in SVG efficiently.
  name: How to Embed Fonts in SVG from Excel – Complete Java Guide
  steps:
  - name: Why This Matters
    text: Think of the SVG as a web page. If you link to an external stylesheet that
      references a font not present on the visitor’s device, the browser falls back
      to Arial or Times New Roman. By embedding, we ship the exact glyph outlines,
      just like a PDF does. This is why **embed fonts in svg** is a non‑nego
  - name: 1. Missing Custom Fonts on the Server
    text: If the source Excel references a font that isn’t installed on the machine
      running the conversion, Aspose.Cells will fall back to a default font **before**
      embedding. To avoid this, install the required fonts on the server or copy the
      `.ttf`/`.otf` files into a known directory and add them to the Jav
  - name: 2. Very Large Fonts Blow Up SVG Size
    text: Embedding a full TrueType collection can balloon the SVG to several megabytes.
      If size is a concern, consider subsetting the font to only the glyphs used in
      the sheet. Aspose.Cells doesn’t expose subsetting directly, but you can post‑process
      the SVG with tools like **fonttools** to trim unused glyph
  - name: 3. Color Profiles and Transparency
    text: SVG handles transparency natively, but some older Excel themes use indexed
      colors that may render differently. Test with a few sample sheets to ensure
      colors stay true. Adjust the `options.setTransparent(true)` flag if you need
      a transparent background.
  - name: 4. Converting Excel to Vector Formats Other Than SVG
    text: Because we’ve already set up the `ImageOrPrintOptions`, swapping `SaveFormat.SVG`
      for `SaveFormat.PDF` or `SaveFormat.EMF` is trivial. This satisfies the **convert
      excel to vector** requirement without rewriting any logic.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
- Font Embedding
title: كيفية تضمين الخطوط في SVG من Excel – دليل Java الكامل
url: /ar/java/excel-import-export/how-to-embed-fonts-in-svg-from-excel-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في SVG من Excel – دليل Java الكامل

تعد مسألة كيفية تضمين الخطوط في SVG من ملف Excel سؤالًا شائعًا بين المطورين الذين يحتاجون إلى رسومات حادة وقابلة للتوسع للويب. سواء كنت تحول لوحة تحكم مبيعات إلى توضيح متجه أو تريد ببساطة أن تبدو المخططات المستندة إلى Excel متطابقة في المتصفح، فإن ضبط الخطوط بشكل صحيح أمر حاسم. في هذا الدرس سنستعرض **export Excel to SVG** مع التأكد من أن كل حرف يبقى مضمّنًا، بحيث يكون الملف النهائي مستقلًا تمامًا.

سنستخدم Aspose.Cells for Java—مكتبة مجربة تتولى قراءة ملفات XLSX، تحويلها إلى صيغ متجهة، وتفعيل خيارات تضمين الخطوط. بنهاية الدليل ستتمكن من **convert xlsx to SVG**، **embed fonts in SVG**، وحتى إعادة استخدام نفس الكود لـ **convert Excel to vector** إلى صيغ أخرى مثل PDF أو EMF إذا رغبت. لا أدوات خارجية، فقط بضع أسطر من Java.

## ما الذي ستحتاجه

- **Java Development Kit (JDK) 8 أو أحدث** – الكود يعمل على أي JVM حديث.
- **Aspose.Cells for Java** (أحدث إصدار حتى يونيو 2026). يمكنك الحصول عليه من Maven Central أو تنزيل ملف JAR من موقع Aspose.
- ملف **input.xlsx** يستخدم خطوطًا مخصصة (مثل “Calibri”، “Roboto”) تريد الحفاظ عليها.
- بيئة تطوير متوسطة (IntelliJ IDEA، Eclipse، أو VS Code) – أي شيء يتيح لك تجميع وتشغيل برنامج Java.

هذا كل شيء. لا محولات إضافية، لا تعديل سطر أوامر. لنبدأ.

![كيفية تضمين الخطوط في SVG من Excel](image.png){alt="كيفية تضمين الخطوط في SVG من Excel"}

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

أولاً، أنشئ مشروع Maven (أو Gradle) جديد. أضف تبعية Aspose.Cells إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

إذا كنت تفضّل إعداد JAR بسيط، فقط ضع `aspose-cells-24.8.jar` في مسار الـ classpath. **نصيحة محترف:** Aspose يأتي بترخيص تجريبي يضيف علامة مائية؛ استبدله بملف ترخيص صحيح للحصول على SVG نظيف.

## الخطوة 2: تحميل المصنف الذي يحتوي على الخطوط المتغيرة

الآن سنفتح ملف Excel. تُجسّد فئة `Workbook` الملف بالكامل، وتمنحنا الوصول إلى الأوراق، الأنماط، والأهم من ذلك خيارات إعداد الصفحة التي سنعدلها لاحقًا.

```java
import com.aspose.cells.*;

public class ExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the workbook containing the variable fonts
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

لاحظ أننا لم نقم بأي شيء معقد بعد—فقط تحميل بسيط. إذا كان الملف موجودًا في classpath، يمكنك استخدام `getClass().getResourceAsStream(...)` بدلاً من ذلك.

## الخطوة 3: تمكين تضمين الخطوط في SVG المُولَّد

تضمين الخطوط هو جوهر **how to embed fonts in SVG**. بدون هذا الإعداد، سيشير الـ SVG إلى خطوط النظام، وأي شخص يفتح الملف على جهاز لا يملك هذه الخطوط سيظهر له بديل، مما قد يفسد التصميم.

```java
        // Step 3: Enable embedding of fonts in the generated SVG
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet
        worksheet.getPageSetup().setSvgEmbeddedFonts(true);
```

استدعاء `setSvgEmbeddedFonts(true)` يخبر Aspose.Cells بدمج بيانات الخط (كـ base‑64) مباشرةً في قسم `<style>` داخل الـ SVG. هذا يجعل الملف أكبر—توقع زيادة بنسبة 20‑30 %—لكن يضمن دقة العرض عبر المتصفحات.

### لماذا هذا مهم

فكّر في الـ SVG كصفحة ويب. إذا ربطت ملفًا نمطيًا خارجيًا يشير إلى خط غير موجود على جهاز الزائر، سيتراجع المتصفح إلى Arial أو Times New Roman. عبر التضمين، نرسل مخططات الحروف الدقيقة، تمامًا كما يفعل PDF. لهذا السبب **embed fonts in svg** هو مطلب لا يمكن التفاوض عليه لأصول العلامة التجارية.

## الخطوة 4: إعداد خيارات الصورة/الطباعة واختيار SVG كصيغة إخراج

تستخدم Aspose.Cells الفئة `ImageOrPrintOptions` للتحكم في خط أنابيب التصيير. سنحدد صيغة الحفظ إلى SVG ونضبط الدقة أو التكبير إذا كنت تحتاج إلى متجه عالي الكثافة.

```java
        // Step 4: Prepare image/print options and set the output format to SVG
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.SVG);
        // Optional: increase DPI for sharper text outlines (default is 96)
        // options.setResolution(300);
```

يمكنك أيضًا تفعيل `setOnePagePerSheet(true)` إذا أردت أن تتحول كل ورقة إلى ملف SVG منفصل بدلاً من مستند متعدد الصفحات. بالنسبة لمعظم لوحات التحكم، الإخراج الافتراضي بصفحة واحدة يكفي.

## الخطوة 5: حفظ المصنف كملف SVG مع خطوط مضمّنة

أخيرًا، نستدعي `save`. تأخذ الطريقة مسار الإخراج و`ImageOrPrintOptions` التي قمنا بتكوينها. النتيجة هي SVG مستقل تمامًا يمكنك إدراجه في أي صفحة HTML.

```java
        // Step 5: Save the workbook as an SVG file with embedded fonts
        workbook.save("YOUR_DIRECTORY/output.svg", options);
        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

شغّل البرنامج، افتح `output.svg` في Chrome أو Firefox، وسترى ورقة Excel تُعرض تمامًا كما تظهر في التطبيق المكتبي—مع الخطوط وكل شيء.

## التحقق من الخطوط المضمّنة

للتأكد من أن الخطوط فعلاً مضمّنة:

1. افتح الـ SVG في محرر نصوص.
2. ابحث عن `@font-face`. ستجد كتلة طويلة من `src: url(data:font/ttf;base64,…)`.
3. إذا وجدت تلك الكتلة، فإن عملية التضمين نجحت.

يمكنك أيضًا استخدام أدوات المطور في المتصفح → “Computed” → “font-family” لتأكيد أن اسم الخط يطابق الأصلي.

## الحالات الخاصة والمشكلات الشائعة

### 1. فقدان الخطوط المخصصة على الخادم

إذا كان ملف Excel الأصلي يشير إلى خط غير مثبت على الجهاز الذي يجري التحويل، سيعود Aspose.Cells إلى خط افتراضي **قبل** التضمين. لتجنب ذلك، ثبّت الخطوط المطلوبة على الخادم أو انسخ ملفات `.ttf`/`.otf` إلى دليل معروف وأضفها إلى `GraphicsEnvironment` في Java:

```java
GraphicsEnvironment ge = GraphicsEnvironment.getLocalGraphicsEnvironment();
ge.registerFont(Font.createFont(Font.TRUETYPE_FONT, new File("fonts/Roboto-Regular.ttf")));
```

### 2. الخطوط الكبيرة جدًا تُضاعف حجم SVG

تضمين مجموعة TrueType كاملة قد يرفع حجم الـ SVG إلى عدة ميغابايت. إذا كان الحجم مصدر قلق، فكر في تقليص الخط إلى الحروف المستخدمة فقط في الورقة. لا توفر Aspose.Cells خاصية التقسيم مباشرة، لكن يمكنك معالجة الـ SVG لاحقًا بأدوات مثل **fonttools** لإزالة الحروف غير المستخدمة.

### 3. ملفات تعريف الألوان والشفافية

يدعم SVG الشفافية أصلاً، لكن بعض سمات Excel القديمة تستخدم ألوانًا مفهرسة قد تُظهر بشكل مختلف. اختبر مع عدة أوراق عينة للتأكد من بقاء الألوان صحيحة. عدّل الإعداد `options.setTransparent(true)` إذا احتجت خلفية شفافة.

### 4. تحويل Excel إلى صيغ متجهة غير SVG

بما أننا قد أعددنا بالفعل `ImageOrPrintOptions`، فإن استبدال `SaveFormat.SVG` بـ `SaveFormat.PDF` أو `SaveFormat.EMF` سهل جدًا. هذا يلبي مطلب **convert excel to vector** دون إعادة كتابة أي منطق.

```java
options.setSaveFormat(SaveFormat.PDF); // for PDF
options.setSaveFormat(SaveFormat.EMF); // for EMF
```

## مثال كامل يعمل (جميع الخطوات معًا)

فيما يلي البرنامج الكامل الجاهز للتنفيذ بلغة Java الذي يدمج كل ما ناقشنا. انسخه، عدّل المسارات، وستكون جاهزًا.

```java
import com.aspose.cells.*;
import java.awt.Font;
import java.awt.GraphicsEnvironment;
import java.io.File;

public class ExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Optional: Register custom fonts if they aren't installed on the host OS
        GraphicsEnvironment ge = GraphicsEnvironment.getLocalGraphicsEnvironment();
        ge.registerFont(Font.createFont(Font.TRUETYPE_FONT, new File("fonts/Roboto-Regular.ttf")));

        // Load the workbook (Step 2)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Enable font embedding (Step 3)
        Worksheet worksheet = workbook.getWorksheets().get(0);
        worksheet.getPageSetup().setSvgEmbeddedFonts(true);

        // Configure SVG options (Step 4)
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.SVG);
        // options.setResolution(300); // uncomment for higher DPI if needed

        // Save as SVG with embedded fonts (Step 5)
        workbook.save("YOUR_DIRECTORY/output.svg", options);
        System.out.println("SVG exported successfully with embedded fonts.");


## ماذا ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Convert Excel to SVG Using Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/convert-excel-to-svg-aspose-cells-net/)
- [Convert Excel Sheets to SVG using Aspose.Cells Java: دليل شامل](/cells/english/java/workbook-operations/convert-excel-to-svg-aspose-cells-java/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (دليل خطوة بخطوة)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}