---
category: general
date: 2026-06-27
description: احفظ ملف Excel بصيغة TSV بسرعة باستخدام Java. تعلم كيفية تصدير ورقة العمل
  إلى نص، وتصدير الورقة كنص عادي، وتصدير سلسلة بيانات Excel باستخدام Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: ar
og_description: احفظ ملف Excel كـ TSV باستخدام Java. يوضح هذا الدليل كيفية تصدير ورقة
  العمل إلى نص، وتصدير الورقة كنص عادي، وتصدير سلسلة بيانات Excel بكفاءة.
og_title: حفظ Excel كملف TSV – دليل التصدير خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: حفظ إكسل بصيغة TSV – دليل شامل لتصدير أوراق العمل إلى نص
url: /ar/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ Excel كملف TSV – دليل شامل لتصدير الأوراق إلى نص

هل احتجت يومًا إلى **حفظ Excel كملف TSV** لكن لم تكن متأكدًا من أي استدعاء API تستخدمه؟ لست وحدك. يواجه الكثير من المطورين صعوبة عندما يحاولون تحويل جدول بيانات إلى ملف مفصول بعلامات جدولة للمعالجة اللاحقة. الخبر السار؟ ببضع أسطر من Java و Aspose.Cells يمكنك تصدير ورقة عمل إلى نص، وتصدير نص ورقة، وحتى تصدير سلسلة بيانات Excel دون عناء.

في هذا البرنامج التعليمي سنستعرض سير العمل بالكامل — من تحميل المصنف إلى تكوين خيارات التصدير وأخيرًا كتابة ملف TSV على القرص. في النهاية ستتمكن من **حفظ Excel كملف TSV** في أي مشروع Java، سواء كنت تتعامل مع ورقة واحدة أو تقوم بتجميع عشرات الملفات.

## ما يغطيه هذا الدليل

* تحميل مصنف Excel من القرص  
* اختيار الورقة المناسبة (أو التكرار عبر عدة أوراق)  
* تكوين `ExportTableOptions` لإنتاج مخرجات نصية صافية  
* كتابة البيانات كملف قيم مفصولة بعلامات جدولة (TSV)  
* نصائح للتعامل مع نطاقات كبيرة، وفواصل مختلفة، وحروف Unicode  

لا تحتاج إلى أدوات خارجية — فقط Aspose.Cells for Java وبيئة تشغيل Java 8+.

---

## الخطوة 1: إعداد المشروع وتحميل المصنف

قبل أن نغوص في الشيفرة، تأكد من إضافة ملف JAR الخاص بـ Aspose.Cells إلى مسار الفئات في مشروعك. إذا كنت تستخدم Maven، فإن التبعية تكون كالتالي:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

الآن يمكننا تحميل المصنف:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **لماذا هذا مهم:** تحميل الملف هو الخطوة الأولى في أي سير عمل **export Excel data string**. إذا تعذر فتح الملف، لن يعمل أي شيء آخر.

### نصيحة احترافية
إذا كنت تتعامل مع ملفات محمية بكلمة مرور، استدعِ `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## الخطوة 2: اختيار الورقة التي تريد تصديرها

يمكنك الحصول على الورقة الأولى، أو ورقة بالاسم، أو التكرار عبر جميعها. إليك أبسط حالة — تصدير الورقة الأولى:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

إذا كنت بحاجة إلى **export worksheet to text** لكل ورقة، غلف الشيفرة السابقة داخل حلقة `for`:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## الخطوة 3: إنشاء وتكوين خيارات التصدير

جوهر **export sheet plain text** يكمن في `ExportTableOptions`. من خلال تبديل بعض الخصائص نحول النطاق إلى سلسلة نصية صافية بفاصل جدولة:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **لماذا نستخدم `setExportAsString(true)`؟**  
> يخبر Aspose.Cells أن يعامل الناتج كنص خام، وهذا بالضبط ما تحتاجه عندما تريد **حفظ Excel كملف TSV**. البديل سيكون تصدير CSV أو HTML، ولا أحد منهما يمنحك فصلًا نظيفًا بعلامات جدولة.

### حالة حافة: فواصل مخصصة
إذا كان نظامك المستقبلي يتوقع عمودًا (`|`) بدلًا من علامة جدولة، فقط غيّر الفاصل:

```java
exportOptions.setDelimiter('|');
```

---

## الخطوة 4: تصدير النطاق المطلوب إلى ملف نصي

الآن نكتب ملف TSV فعليًا. طريقة `exportTable` تأخذ ثلاث معطيات: نطاق الخلايا، مسار الإخراج، و `ExportTableOptions` التي قمنا بتكوينها.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

إذا أردت تصدير *النطاق المستخدم بالكامل*، استبدل `"A1:D20"` بـ `ws.getCells().getMaxDisplayRange()`:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### نصيحة احترافية
بعد التصدير، يمكنك أيضًا التقاط السلسلة مباشرة:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

هذا يمنحك **export Excel data string** الخام دون الحاجة إلى نظام الملفات.

---

## الخطوة 5: التعامل مع الملفات الكبيرة ونصائح الأداء

عند التعامل مع جداول ضخمة (مئات الآلاف من الصفوف)، ضع في اعتبارك هذه التحسينات:

| المشكلة | الحل |
|---------|------|
| ضغط الذاكرة | استخدم `WorkbookFactory.create(InputStream)` لبث الملف بدلاً من تحميله بالكامل. |
| بطء الإدخال/الإخراج | اكتب إلى `BufferedWriter` أو استخدم NIO `Files.newBufferedWriter`. |
| حروف Unicode | تأكد من كتابة ملف الإخراج بـ UTF‑8: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

فيما يلي مقطع يجمع بين البث وترميز UTF‑8:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## الأخطاء الشائعة وكيفية تجنّبها

1. **نسيان ضبط `setExportAsString(true)`.**  
   بدون هذا العلم سيولد Aspose ملف Excel ثنائي، مما يعرقل هدفك في **export worksheet to text**.

2. **استخدام الفاصل الخاطئ.**  
   الفاصلة بدلاً من علامة الجدولة ستنتج ملف CSV، وليس TSV. تحقق من `setDelimiter('\t')`.

3. **صيغة النطاق غير صحيحة.**  
   `"A1:D20"` صحيحة، لكن `"A1:D20:"` (نقطة مزدوجة إضافية) ستؤدي إلى رمي `IllegalArgumentException`.

4. **أذونات الملف.**  
   تأكد من أن الدليل المستهدف قابل للكتابة. على Linux، غالبًا ما يحل `chmod 755` المشكلة.

---

## الخلاصة – مثال كامل يعمل

إليك البرنامج الكامل الجاهز للتنفيذ والذي يوضح **حفظ Excel كملف TSV** من البداية حتى النهاية:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

تشغيل هذا البرنامج ينتج ملفًا مفصولًا بعلامات جدولة (`out.tsv`) يمكن لأي نظام لاحق — سواء كان محمل قاعدة بيانات، أو سكريبت Unix `awk`، أو عارض جداول بسيط — استهلاكه.

---

## الخاتمة

غطّينا كل ما تحتاجه لت **حفظ Excel كملف TSV** باستخدام Java و Aspose.Cells. بدءًا من تحميل المصنف، اختيار الورقة المناسبة، تكوين `ExportTableOptions`، وأخيرًا كتابة الملف، لديك الآن نمط جاهز للإنتاج لتصديـر **export worksheet to text**، **export sheet plain text**، و **export Excel data string**.

ما الخطوة التالية؟ جرّب تصدير نطاقات متعددة، أو تبديل الفواصل أثناء التشغيل، أو بث الناتج مباشرةً إلى استجابة HTTP لتنزيلات الويب. المبادئ نفسها تنطبق، وستجد أن التعامل مع بيانات Excel كنص صافي يصبح سهلًا بمجرد إتقان الأساسيات.

هل لديك أسئلة أو صادفت حالة حافة غريبة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}