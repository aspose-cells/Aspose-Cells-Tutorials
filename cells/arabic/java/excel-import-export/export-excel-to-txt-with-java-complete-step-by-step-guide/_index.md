---
category: general
date: 2026-07-16
description: تصدير Excel إلى TXT باستخدام Aspose.Cells في Java. تعلّم كيفية ضبط الأرقام
  ذات الدقة، حفظ Excel كملف نصي، والتحكم في تنسيق الإخراج.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set significant digits
- save excel as text file
- save workbook as txt
language: ar
lastmod: 2026-07-16
og_description: تصدير Excel إلى TXT في Java باستخدام Aspose.Cells. يوضح لك هذا البرنامج
  التعليمي كيفية ضبط الأرقام ذات الدقة، وحفظ ملف Excel كملف نصي، والحصول على نتائج
  موثوقة.
og_image_alt: Screenshot of Java code exporting an Excel workbook to a TXT file with
  4 significant digits
og_title: تصدير Excel إلى TXT في Java – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  headline: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  name: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java Development Kit (JDK) 8 or newer. - Maven or Gradle to manage the
      Aspose.Cells dependency (we’ll show the Maven snippet). - A basic understanding
      of Java syntax (if you’ve written a “Hello World”, you’re good).'
  - name: Understanding `setSignificantDigits`
    text: '- **Definition:** The number of digits that remain after the decimal point,
      *including* leading digits. For `123.456789` with `4` significant digits, the
      output becomes `123.5`. - **When to use:** If the downstream system expects
      a fixed precision (e.g., scientific data files), or you need to trunca'
  - name: Folder Considerations
    text: '- The `output` folder must exist, or you’ll get an `IOException`. You can
      create it programmatically:'
  - name: 1️⃣ What if I need a different delimiter?
    text: "`TxtSaveOptions` also offers `setSeparator('\t')` for tabs or `setSeparator(',')`
      for CSV‑style output. Example:"
  - name: 2️⃣ How does locale affect decimal separators?
    text: 'By default Aspose uses the system locale. If you need a period (`.`) regardless
      of locale, set:'
  - name: 3️⃣ Large worksheets – memory concerns?
    text: Aspose.Cells streams data to disk when working with worksheets larger than
      1 GB, so you usually won’t hit an `OutOfMemoryError`. Still, avoid loading massive
      sheets into memory if you only need a subset; use `Workbook.getWorksheets().get(index)`
      to target a specific sheet.
  - name: 4️⃣ Can I export only a range?
    text: Yes. Use `txtOptions.setExportRange("A1:B10")` to restrict the output to
      a specific area. This reduces file size and speeds up the export.
  - name: 5️⃣ What if I don’t have a license?
    text: The evaluation mode adds a watermark line (`"Aspose.Cells for Java Evaluation
      Version"`). For production you’ll need a license; otherwise the watermark may
      break downstream parsers.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: تصدير Excel إلى TXT باستخدام Java – دليل خطوة بخطوة كامل
url: /ar/java/excel-import-export/export-excel-to-txt-with-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى TXT باستخدام Java – دليل خطوة بخطوة كامل

هل تساءلت يومًا **عن كيفية تصدير Excel إلى TXT** دون فقدان الدقة العددية؟ ربما تحتاج إلى تفريغ نصي بسيط لنظام قديم، أو أنك تُغذّي البيانات إلى خط أنابيب علمي يتوقع عددًا محددًا من الأرقام ذات الدلالة. في هذا الدرس سنستعرض **مثال Java كامل وقابل للتنفيذ** يوضح لك ذلك بالضبط—بالإضافة إلى **كيفية تعيين الأرقام ذات الدلالة**, **حفظ Excel كملف نصي**, و**حفظ المصنف كملف txt** باستخدام Aspose.Cells.

سنغطي كل شيء من إعداد المشروع حتى خطوة التحقق النهائية، بحيث يمكنك نسخ‑لصق الشيفرة، تشغيلها، ورؤية النتيجة فورًا. لا توجد تبعيات غامضة، ولا اختصارات “انظر إلى الوثائق”—فقط حل واضح من البداية حتى النهاية.

---

## ما ستتعلمه

- كيفية إنشاء مصنف برمجيًا باستخدام Aspose.Cells.
- استدعاء API الدقيق **لتعيين الأرقام ذات الدلالة** لتصدير TXT.
- الفرق بين `TxtSaveOptions` وخيارات الحفظ الأخرى.
- كيفية **حفظ Excel كملف نصي** على أي نظام تشغيل (Windows, macOS, Linux).
- المشكلات الشائعة (فواصل عشرية حسب اللغة، أوراق عمل ضخمة) وكيفية تجنّبها.
- فئة Java كاملة وجاهزة للتنفيذ يمكنك تعديلها لتناسب مشاريعك.

### المتطلبات المسبقة

- مجموعة تطوير Java (JDK) 8 أو أحدث.
- Maven أو Gradle لإدارة تبعية Aspose.Cells (سنظهر لك مقطع Maven).
- فهم أساسي لصياغة Java (إذا كتبت “Hello World” فأنت جاهز).

---

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

أولًا، لنُدخل المكتبة إلى بناء المشروع. إذا كنت تستخدم Maven، أضف هذا إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** Aspose تقدم ترخيص تجريبي مجاني لمدة 30 يومًا. ضع ملف `Aspose.Total.lic` في جذر مشروعك، أو استدعِ `License.setLicense("path/to/license")` قبل أي استخدام للـ API.

بعد حل التبعيات، يمكنك البدء بالبرمجة. إذا كنت تفضّل Gradle، فالمقابل هو:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

---

## الخطوة 2: تصدير Excel إلى TXT – إنشاء مصنف

الآن سننشئ مصنفًا جديدًا، نضيف قيمة عددية، ونُحضّره للتصدير. هذا هو جوهر **تصدير Excel إلى txt**.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fresh workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet – it's created by default
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 3️⃣ Put a numeric value into cell A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue(123.456789); // Example number with many decimals
```

**لماذا هذا مهم:** من خلال إنشاء المصنف في الشيفرة نتجنّب أي تنسيق مخفي قد يتسلل من ملف قالب. طريقة `putValue` تكتشف نوع البيانات تلقائيًا، فتصبح الخلية **عددية**—not a string.

---

## الخطوة 3: كيفية تعيين الأرقام ذات الدلالة لإخراج TXT

عند تصدير إلى نص عادي، Aspose.Cells يكتب القيمة العددية الخام افتراضيًا. لتحديد الإخراج إلى، مثلاً، **4 أرقام ذات دلالة**، تحتاج إلى تعديل `TxtSaveOptions`.

```java
        // 4️⃣ Configure TXT save options – this is where we set the precision
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4); // <-- controls significant digits
```

### فهم `setSignificantDigits`

- **التعريف:** عدد الأرقام التي تبقى بعد الفاصلة العشرية، *بما في ذلك* الأرقام القيادية. بالنسبة لـ `123.456789` مع `4` أرقام ذات دلالة، يصبح الناتج `123.5`.
- **متى تُستخدم:** إذا كان النظام المستقبلي يتوقع دقة ثابتة (مثل ملفات البيانات العلمية)، أو إذا أردت تقصير الأرقام لتجنب ضوضاء النقطة العائمة.
- **حالة حافة:** إذا كان للرقم أرقام أقل من العدد المحدد، سيحافظ Aspose على القيمة الأصلية (دون إضافة أصفار).

> **لماذا لا نستخدم `setDecimalPlaces`؟** هذه الخاصية تتحكم *فقط* في عدد الأرقام بعد الفاصلة العشرية، متجاهلة الأرقام القيادية. بالنسبة للبيانات العلمية، `significantDigits` هو الخيار المناسب عادةً.

---

## الخطوة 4: حفظ Excel كملف نصي (TXT)

مع إعداد الخيارات، نكتب المصنف أخيرًا إلى ملف `.txt`. هذه هي خطوة **حفظ المصنف كملف txt**.

```java
        // 5️⃣ Persist the workbook as a TXT file
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Excel exported to TXT at: " + outputPath);
    }
}
```

### ملاحظات حول المجلد

- يجب أن يكون مجلد `output` موجودًا، وإلا ستحصل على `IOException`. يمكنك إنشاؤه برمجيًا:

```java
new java.io.File("output").mkdirs();
```

- على Linux/macOS، المسارات حساسة لحالة الأحرف؛ أما على Windows فليس كذلك. استخدم أسماء مجلدات بأحرف صغيرة لضمان التوافق عبر الأنظمة.

---

## الخطوة 5: التحقق من النتيجة

شغّل البرنامج (`mvn compile exec:java -Dexec.mainClass=ExportExcelToTxtDemo`) وافتح الملف `output/SignificantDigits.txt`. يجب أن ترى:

```
123.5
```

هذا السطر الواحد يؤكد:

- تم **حفظ المصنف كملف نصي** بنجاح.
- القيمة العددية تحترم **4 أرقام ذات دلالة** التي عيّنّاها.
- لا توجد فواصل إضافية، علامات تبويب، أو بيانات تعريفية خاصة بـ Excel تسللت إلى الملف.

إذا احتجت تخطيطًا مفصولًا بعلامات تبويب لعدة أعمدة، ما عليك سوى ملء خلايا إضافية وسيتولى Aspose إدراج علامات التبويب تلقائيًا.

---

## أسئلة شائعة وحالات حافة

### 1️⃣ ماذا لو أردت فاصلًا مختلفًا؟

`TxtSaveOptions` يوفر أيضًا `setSeparator('\t')` للعلامات التبويب أو `setSeparator(',')` لإخراج بنمط CSV. مثال:

```java
txtOptions.setSeparator('\t'); // Tab delimiter
```

### 2️⃣ كيف يؤثر الإعداد المحلي على الفواصل العشرية؟

بشكل افتراضي يستخدم Aspose إعداد النظام المحلي. إذا كنت تحتاج إلى نقطة (`.`) بغض النظر عن الإعداد المحلي، عيّن:

```java
txtOptions.setCultureInfo(java.util.Locale.US);
```

### 3️⃣ أوراق عمل ضخمة – مخاوف الذاكرة؟

Aspose.Cells يبث البيانات إلى القرص عند التعامل مع أوراق عمل أكبر من 1 GB، لذا عادةً لا تواجه `OutOfMemoryError`. مع ذلك، تجنّب تحميل أوراق ضخمة بالكامل إذا كنت تحتاج جزءًا فقط؛ استخدم `Workbook.getWorksheets().get(index)` لاستهداف ورقة معينة.

### 4️⃣ هل يمكن تصدير نطاق محدد فقط؟

نعم. استخدم `txtOptions.setExportRange("A1:B10")` لتقليل الإخراج إلى منطقة معينة. هذا يقلل حجم الملف ويسرّع عملية التصدير.

### 5️⃣ ماذا لو لم أمتلك ترخيصًا؟

وضع التقييم يضيف سطر علامة مائية (`"Aspose.Cells for Java Evaluation Version"`). للإنتاج ستحتاج إلى ترخيص؛ وإلا قد تعطل العلامة المائية محللاتك اللاحقة.

---

## مثال كامل جاهز للنسخ واللصق

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Ensure output directory exists
        new File("output").mkdirs();

        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 2️⃣ Put several numbers to illustrate formatting
        sheet.getCells().get("A1").putValue(123.456789);
        sheet.getCells().get("A2").putValue(0.0012345);
        sheet.getCells().get("A3").putValue(98765.4321);

        // 3️⃣ Configure TXT options – 4 significant digits, tab delimiter
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4);
        txtOptions.setSeparator('\t'); // optional, defaults to tab
        txtOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator

        // 4️⃣ Save as TXT
        String outPath = "output/SignificantDigits.txt";
        workbook.save(outPath, txtOptions);

        System.out.println("Export completed: " + outPath);
    }
}
```

تشغيل الكود أعلاه ينتج ملف `output/SignificantDigits.txt` يحتوي على:

```
123.5
0.001235
98770
```

لاحظ كيف أن كل رقم يلتزم بقاعدة **4 أرقام ذات دلالة**، حتى القيم الصغيرة جدًا والكبيرة جدًا.

---

## الخلاصة

لقد عرضنا طريقة **متكاملة ومستقلة لتصدير Excel إلى TXT** باستخدام Java وAspose.Cells، مع تغطية **كيفية تعيين الأرقام ذات الدلالة**, **حفظ Excel كملف نصي**, و**حفظ المصنف كملف txt**. النقاط الأساسية:

- استخدم `TxtSaveOptions.setSignificantDigits` للتحكم في دقة الأرقام.
- عدّل الفواصل، الثقافة، ونطاقات التصدير حسب الحاجة.
- الشيفرة تعمل على أي منصة، تحتاج مكتبة واحدة فقط، وتنتج نصًا نظيفًا جاهزًا للمعالجة اللاحقة.

مستعد للخطوة التالية؟ جرّب إضافة أعمدة متعددة، جرب فواصل مختلفة، أو دمج التصدير في خط أنابيب ETL أكبر. إذا واجهت أي غموض—مثل مشكلة إعداد محلي أو ورقة عمل ضخمة—ارجع إلى قسم “أسئلة شائعة وحالات حافة” أعلاه.

هل لديك حالة استخدام تريد مشاركتها؟ اترك تعليقًا، أو قم بعمل fork للمستودع وفتح طلب سحب. برمجة سعيدة، واستمتع ببساطة تحويل الجداول إلى نص عادي!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذية بديلة في مشاريعك.

- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}