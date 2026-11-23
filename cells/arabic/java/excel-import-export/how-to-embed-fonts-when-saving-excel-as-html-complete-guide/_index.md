---
category: general
date: 2026-11-22
description: تعلم كيفية تضمين الخطوط عند حفظ ملف Excel كـ HTML، مما يتيح تضمين الخطوط
  لضمان عرض ثابت عبر المتصفحات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- enable font embedding
- save excel html
- html font embedding
- embed fonts html
language: ar
lastmod: 2026-11-22
og_description: كيفية تضمين الخطوط عند حفظ Excel كملف HTML. اتبع هذا الدليل لتمكين
  تضمين الخطوط وتأكد من أن جداول البيانات الخاصة بك تبدو متطابقة في أي متصفح.
og_image_alt: Screenshot showing an Excel file exported to HTML with embedded fonts
og_title: كيفية تضمين الخطوط عند حفظ Excel كملف HTML – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to embed fonts while saving Excel as HTML, enabling font
    embedding for consistent rendering across browsers.
  headline: How to embed fonts when saving Excel as HTML – complete guide
  type: TechArticle
- description: Learn how to embed fonts while saving Excel as HTML, enabling font
    embedding for consistent rendering across browsers.
  name: How to embed fonts when saving Excel as HTML – complete guide
  steps:
  - name: What if the font is not found?
    text: Aspose.Cells can embed only fonts that the JVM can locate. If you receive
      a warning like *“Font not found, falling back to default”*, make sure the font
      file is installed on the operating system or placed in a directory listed in
      the `java.library.path`.
  - name: Does embedding increase file size?
    text: 'Yes. Embedding a full TrueType font can add 30–200 KB to the HTML file,
      depending on the font. If size is a concern, consider:'
  - name: Can I embed multiple fonts?
    text: Absolutely. The library examines every cell style, extracts all referenced
      fonts, and embeds each one when `setEmbedFonts(true)` is active.
  - name: Is the approach compatible with older browsers?
    text: The `@font-face` rule works in all browsers that support CSS 2.1 and later,
      which includes IE 9 +, Chrome, Firefox, Safari, and Edge. For very old browsers
      (IE 8‑), you may need to provide a fallback font family.
  type: HowTo
tags:
- Excel
- HTML
- Font embedding
title: كيفية تضمين الخطوط عند حفظ إكسل كملف HTML – دليل كامل
url: /ar/java/excel-import-export/how-to-embed-fonts-when-saving-excel-as-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط عند حفظ Excel كـ HTML – دليل كامل

إذا كنت بحاجة إلى **كيفية تضمين الخطوط** أثناء تصدير مصنف Excel إلى HTML، يوضح لك هذا الدليل الخطوات الدقيقة. يضمن تضمين الخطوط أن ملف HTML المُنشأ يعرض نفس الخطوط كما في المصنف الأصلي، حتى على الأنظمة التي لا تتوفر فيها الخطوط المطلوبة. ستتعلم أيضًا كيفية **تمكين تضمين الخطوط** باستخدام Aspose.Cells for Java، وهي طريقة موثوقة لـ **حفظ Excel كـ HTML** مع الحفاظ الكامل على المظهر البصري.

في هذا الدرس ستقوم بـ:

* إعداد مشروع Java مع مكتبة Aspose.Cells.  
* إنشاء كائن `HtmlSaveOptions` وتفعيل **تضمين خطوط HTML**.  
* حفظ المصنف كملف HTML يحتوي على ملفات الخط المطلوبة.  

المتطلبات المسبقة:

* Java 8 أو أحدث.  
* Aspose.Cells for Java (يفضل أحدث نسخة).  
* معرفة أساسية بـ Java وتعامل مع ملفات Excel.

---

## ما ستحتاجه

| العنصر | السبب |
|------|--------|
| **Aspose.Cells for Java** | يوفر فئة `HtmlSaveOptions` وطريقة `setEmbedFonts`. |
| **خط TrueType أو OpenType** مثبت على الجهاز | يمكن للمكتبة تضمين الخطوط التي يمكن للـ JVM الوصول إليها فقط. |
| **بيئة تطوير متكاملة (IDE) أو أداة بناء** (مثل Maven أو Gradle أو `javac` العادي) | لتجميع وتشغيل المثال. |

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

إذا كنت تستخدم Maven، أضف الاعتماد إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

بالنسبة لـ Gradle، ضع ما يلي في `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

*نصيحة احترافية:* احرص على تحديث نسخة المكتبة؛ الإصدارات الأحدث تتضمن إصلاحات للأخطاء المتعلقة بـ **embed fonts html**.

## الخطوة 2: إنشاء مصنف وتعبئته

فيما يلي برنامج Java بسيط ومستقل يُنشئ مصنفًا، يكتب نصًا منسقًا، ويُعده لتصدير HTML.

```java
import com.aspose.cells.*;

public class ExcelHtmlFontEmbedding {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet sheet = wb.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // 3️⃣ Put some text in A1 and apply a custom font
        Cell a1 = cells.get("A1");
        a1.putValue("Hello, embedded fonts!");
        Style style = a1.getStyle();
        Font font = style.getFont();
        font.setName("Comic Sans MS");   // any installed font works
        font.setSize(14);
        a1.setStyle(style);

        // 4️⃣ Save as HTML with font embedding (see next step)
        saveWithEmbeddedFonts(wb);
    }

    private static void saveWithEmbeddedFonts(Workbook wb) throws Exception {
        // This method contains the core of **html font embedding**
        HtmlSaveOptions saveOptions = new HtmlSaveOptions();
        // Enable font embedding so the HTML contains the required .ttf files
        saveOptions.setEmbedFonts(true);

        // Optional: specify a folder for the generated assets (fonts, images)
        saveOptions.setExportImagesAsBase64(true); // reduces external files
        String outputPath = "output/embedded.html";

        // Perform the save operation
        wb.save(outputPath, saveOptions);
        System.out.println("Workbook saved with embedded fonts to: " + outputPath);
    }
}
```

**لماذا يعمل هذا:**  
* `HtmlSaveOptions#setEmbedFonts(true)` يُخبر Aspose.Cells بتضمين ملفات الخط المستخدمة في المصنف داخل ملف HTML المُولد.  
* ضبط `ExportImagesAsBase64` يحافظ على نظافة المخرجات، لكنه اختياري.

## الخطوة 3: التحقق من ملف HTML المُولد

افتح `output/embedded.html` في أي متصفح حديث. يجب أن ترى النص معروضًا بخط *Comic Sans MS* حتى إذا لم يكن الخط مثبتًا على جهاز العميل. لتأكيد أن الخط مُضمّن فعليًا، اعرض مصدر الصفحة؛ ستجد كتلة `<style>` تحتوي على قاعدة `@font-face` تشير إلى ملف خط مُشفّر بـ base64.

```html
<style>
@font-face {
    font-family: 'Comic Sans MS';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

**الناتج المتوقع:** تعرض الصفحة النص “Hello, embedded fonts!” باستخدام الخط المحدد، ويحتوي ملف HTML على بيانات الخط المُضمّن.

## أسئلة شائعة وحالات خاصة

### ماذا لو لم يتم العثور على الخط؟

يمكن لـ Aspose.Cells تضمين الخطوط التي يستطيع الـ JVM العثور عليها فقط. إذا تلقيت تحذيرًا مثل *“Font not found, falling back to default”*، تأكد من تثبيت ملف الخط على نظام التشغيل أو وضعه في دليل مُدرج في `java.library.path`.

### هل يؤدي التضمين إلى زيادة حجم الملف؟

نعم. قد يضيف تضمين خط TrueType كامل ما بين 30–200 KB إلى ملف HTML، حسب الخط. إذا كان الحجم مصدر قلق، فكر في:

* استخدام الأحرف فقط التي تظهر في المصنف (Aspose.Cells يزيل الرموز غير المستخدمة).  
* اختيار خط ويب خفيف الوزن يدعمه معظم المتصفحات بالفعل.

### هل يمكنني تضمين عدة خطوط؟

بالطبع. تقوم المكتبة بفحص كل نمط خلية، استخراج جميع الخطوط المشار إليها، وتضمين كل منها عندما يكون `setEmbedFonts(true)` مفعلاً.

### هل النهج متوافق مع المتصفحات القديمة؟

قاعدة `@font-face` تعمل في جميع المتصفحات التي تدعم CSS 2.1 وما بعده، بما في ذلك IE 9 +، Chrome، Firefox، Safari، و Edge. بالنسبة للمتصفحات القديمة جدًا (IE 8‑)، قد تحتاج إلى توفير عائلة خطوط احتياطية.

## نصائح احترافية للاستخدام في الإنتاج

* **تخزين HTML المُولد مؤقتًا** – يؤدي تضمين الخطوط إلى زيادة حجم كل تصدير؛ احفظ النتيجة إذا كنت بحاجة إلى تقديمها بشكل متكرر.  
* **مجلد أصول منفصل** – بدلاً من base64، يمكنك السماح لـ Aspose.Cells بكتابة ملفات `.ttf` إلى مجلد (`saveOptions.setExportFontFile(true)`). هذا يحافظ على صغر حجم HTML ويسمح للمتصفحات بتخزين الخط مؤقتًا.  
* **الأمان** – لا تقم أبدًا بتضمين خطوط من مصادر غير موثوقة؛ قد تحتوي على بيانات خبيثة. استخدم فقط الخطوط التي تتحكم فيها.

## الخلاصة

أنت الآن تعرف **كيفية تضمين الخطوط** عند **حفظ Excel كـ HTML** باستخدام Aspose.Cells for Java. من خلال تمكين **تضمين الخطوط**، يحتوي HTML المُولد على قواعد `@font-face` الضرورية، مما يضمن أن جدول البيانات يبدو متطابقًا في جميع المتصفحات. تحل هذه التقنية مشكلة *html font embedding* الكلاسيكية وتُعد الطريقة الموصى بها لـ **تمكين تضمين الخطوط** لأي سير عمل لتحويل Excel إلى HTML.

هل أنت مستعد للخطوة التالية؟ استكشف المواضيع ذات الصلة مثل **حفظ Excel كـ PDF مع خطوط مضمّنة**، أو تعلم كيفية **تخصيص مخرجات CSS** لصفحات ويب متجاوبة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تضمين الخطوط عند حفظ Excel إلى HTML باستخدام Aspose.Cells لـ C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-saving-excel-to-html-with-c/)
- [كيفية استخدام wrapcols وتضمين الخطوط عند حفظ Excel إلى HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/)
- [كيفية تضمين الخطوط في HTML عند حفظ مصنف](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-saving-a-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}