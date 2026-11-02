---
category: general
date: 2026-06-27
description: تضمين الخطوط في HTML عند تحويل Excel إلى HTML. تعلم كيفية حفظ المصنف
  كملف HTML مع خطوط مدمجة باستخدام كود Java بسيط.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: ar
og_description: تضمين الخطوط في HTML أثناء تحويل Excel إلى HTML. يوضح هذا الدليل كيفية
  حفظ المصنف كـ HTML مع تضمين الخطوط باستخدام Java.
og_title: تضمين الخطوط في HTML – تحويل Excel إلى HTML وحفظ المصنف
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: تضمين الخطوط في HTML – تحويل Excel إلى HTML وحفظ المصنف
url: /ar/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تضمين الخطوط في HTML – تحويل Excel إلى HTML وحفظ المصنف

هل احتجت يوماً إلى **تضمين الخطوط في HTML** عندما *تحول Excel إلى HTML*؟ ربما تقوم بإنشاء بوابة تقارير ولا تناسب الخطوط الافتراضية للويب. الخبر السار هو أنك لا تحتاج إلى القبول بالمظهر الباهت والعام—Aspose.Cells يتيح لك حزم الخطوط الدقيقة التي استخدمتها في جدول البيانات مباشرةً داخل ملف HTML المُولد.

في هذا الدرس سنستعرض مثال Java كامل جاهز للتنفيذ **يحفظ المصنف كملف HTML** مع تضمين الخطوط، نشرح لماذا قد ترغب في ذلك، ونشير إلى بعض المشكلات التي قد تواجهها. في النهاية ستحصل على صفحة HTML مستقلة تماماً تشبه ورقة Excel الأصلية، دون فقدان أي رموز، ودون مشاكل CSS خارجية.

## ما ستتعلمه

- كيفية تحميل مصنف Excel موجود (أو إنشاء واحد من الصفر) في Java.  
- كيفية تكوين `HtmlSaveOptions` لتضمين خطوط المصنف مباشرةً في ناتج HTML.  
- كيفية استدعاء `Workbook.save` بحيث يُكتب الملف كـ **HTML مع خطوط مضمّنة**.  
- نصائح للتعامل مع ملفات الخطوط الكبيرة، دلائل الخطوط المخصصة، وحل المشكلات الشائعة.

> **المتطلبات المسبقة:** تحتاج إلى Aspose.Cells for Java (أحدث نسخة) في مسار الـ classpath وبيئة تشغيل Java 8+. لا توجد مكتبات طرف ثالث أخرى مطلوبة.

---

## الخطوة 1: إعداد المشروع واستيراد الفئات المطلوبة

قبل الغوص في الشيفرة، لنتأكد أن بيئة التطوير جاهزة. إذا كنت تستخدم Maven، أضف تبعية Aspose.Cells إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

إذا كنت تفضّل Gradle، فإن المكافئ هو:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **نصيحة احترافية:** حافظ على تحديث المكتبة. الإصدارات الجديدة غالباً ما تحسّن من معالجة الخطوط وتقلل حجم البيانات المضمّنة.

الآن، استورد الفئات التي سنحتاجها:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

هذه الاستيرادات تمنحنا الوصول إلى نموذج المصنف، خيارات تصدير HTML، وبعض الفئات المساعدة.

---

## الخطوة 2: تحميل (أو إنشاء) مصنف Excel

يمكنك إما تحميل ملف `.xlsx` موجود أو إنشاء مصنف في الوقت الفعلي. للتوضيح، لنفترض أن لدينا ملفًا باسم `Sample.xlsx` في مجلد `resources` الخاص بالمشروع.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

إذا لم يكن لديك ملف مصدر، يمكنك توليد مصنف سريع:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **لماذا هذا مهم:** عند تضمين الخطوط، تقوم Aspose.Cells باستخراج تعريفات الخطوط الدقيقة المستخدمة في المصنف. إذا كان المصنف يحتوي على خطوط مخصصة، فستنتقل مع HTML، مما يضمن الحفاظ على المظهر البصري.

---

## الخطوة 3: تكوين HtmlSaveOptions لتضمين الخطوط

هذا هو جوهر الدرس. بشكل افتراضي، يكتب `HtmlSaveOptions` CSS يشير إلى الخطوط النظامية. لتغيير هذا السلوك، نفعّل العلامة `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### ما تفعله الخيارات

| الخيار | القيمة الافتراضية | الأثر عند التغيير |
|--------|-------------------|-------------------|
| `setEmbedFonts(true)` | `false` | يضمّن ملفات الخط بالكامل (عادةً كـ URI مشفر Base64) داخل HTML المُولد. |
| `setSubsetFonts(true)` | `false` | يقتصر الخط المضمّن على الأحرف المستخدمة فقط، مما يقلل حجم الملف بشكل كبير. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | يمكنك اختيار تضمين خطوط محددة فقط إذا كان لديك قيود ترخيص. |

> **حالة حافة:** إذا كان المصنف يستخدم خطًا غير مثبت على الخادم، فإن Aspose.Cells يلجأ إلى خط نظام افتراضي. لتجنب المفاجآت، تأكد من توفر جميع الخطوط المخصصة في دليل الخطوط الخاص ببيئة Java أو سجّلها يدويًا عبر `FontConfig`.

---

## الخطوة 4: حفظ المصنف كـ HTML مع خطوط مضمّنة

الآن بعد ضبط الخيارات، نكتفي باستدعاء `save`. سيصبح الناتج ملف `.html` واحد يحتوي على بيانات المصنف **والخطوط** مشفّرة مباشرةً داخل العلامات.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

عند فتح `page.html` في أي متصفح حديث، سيظهر المحتوى بنفس الخطوط التي رأيتها في Excel—دون ملفات خطوط خارجية، ودون أحرف مفقودة.

---

## الخطوة 5: التحقق من النتيجة وفهم المخرجات

افتح ملف HTML المُولد في متصفح (Chrome, Firefox, Edge—أيًا كان). يجب أن ترى ورقة العمل معروضة بأمانة. لتتأكد من أن الخطوط مضمّنة فعلاً:

1. انقر بزر الفأرة الأيمن على الصفحة → “View Page Source”.  
2. ابحث عن `@font-face`. ستجد قاعدة CSS تحتوي على سطر `src: url(data:font/ttf;base64,…)`—هذا هو بيانات الخط المشفّرة Base64.  

إذا رأيت ذلك، فإن خطوة **تضمين الخطوط في HTML** نجحت.

### أسئلة شائعة

- **“لماذا حجم ملف HTML أكبر مما توقعت؟”**  
  تضمين ملفات الخط بالكامل قد يضيف مئات الكيلوبايت. استخدم `setSubsetFonts(true)` لتقليصه، أو فكر في تحويل الأوراق المطلوبة فقط.

- **“هل يمكنني تضمين خط معين فقط؟”**  
  نعم. اضبط `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` ثم أضف أسماء الخطوط عبر `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **“ماذا لو كان الخط مرخصًا ولا يمكنني تضمينه؟”**  
  عطل العلامة (`setEmbedFonts(false)`) ووفّر بديلًا آمنًا عبر CSS، أو استضف الخط على CDN حيث لديك الإذن.

---

## الخطوة 6: التعامل مع المصنفات الكبيرة ونصائح الأداء

تعمل عملية تضمين الخطوط جيدًا مع جداول البيانات المتوسطة، لكن المصنف الذي يحتوي على عشرات الخطوط المخصصة قد يضاعف حجم HTML. إليك بعض التوصيات الموجهة للأداء:

- **قَصّ الخطوط** (كما هو موضح) للاحتفاظ فقط بالرموز المستخدمة.  
- **صدّر الأوراق المطلوبة فقط** باستخدام `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **ضغط HTML** بعد الإنشاء (مثلاً gzip على الخادم) لتقليل زمن النقل.  
- **تخزين HTML المُولد مؤقتًا** إذا تم طلب نفس ملف Excel بشكل متكرر.

---

## الخطوة 7: الخطوات التالية – ما بعد التصدير الأساسي

الآن بعد أن أتقنت **تضمين الخطوط في HTML**، قد ترغب في استكشاف قدرات ذات صلة:

- **تحويل Excel إلى HTML مع الصور** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **إنشاء PDF بدلاً من HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **إنشاء HTML متجاوب** عبر تعديل `htmlOpts.setExportActiveWorksheetOnly` و `htmlOpts.setExportGridLines`.  

جميع هذه الميزات تتبع نفس النمط: تكوين كائن `*SaveOptions`، تفعيل العلامات المناسبة، ثم استدعاء `Workbook.save`.

---

## الخلاصة

لقد تعلمت الآن كيفية **تضمين الخطوط في HTML** أثناء **تحويل Excel إلى HTML** و**حفظ المصنف كـ HTML** باستخدام Aspose.Cells for Java. الخطوات الأساسية هي:

1. تحميل أو إنشاء المصنف.  
2. إنشاء `HtmlSaveOptions` وتفعيل `setEmbedFonts(true)`.  
3. استدعاء `Workbook.save` مع تلك الخيارات.

النتيجة هي ملف HTML واحد محمول يبدو تمامًا مثل جدول البيانات الأصلي—دون خطوط مفقودة، دون ملفات CSS إضافية، ودون الاعتماد على خطوط العميل المثبتة.

لا تتردد في تجربة تقليل حجم الخطوط، التضمين الانتقائي، أو حتى دمج ذلك مع التخزين المؤقت على الخادم لتلبية سيناريوهات المرور العالي. إذا واجهت أي شذوذ (مثل ملفات كبيرة غير متوقعة أو رموز مفقودة)، راجع الإعدادات الاختيارية التي ناقشناها وعدّلها وفق الحاجة.

برمجة سعيدة، واستمتع بصفحات HTML المتقنة التي يمكنك الآن تقديمها مباشرةً من تطبيقات Java الخاصة بك!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Convert Excel to HTML in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Export Excel to HTML Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Export Excel to HTML using IStreamProvider & Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}