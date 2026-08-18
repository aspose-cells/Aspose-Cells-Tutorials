---
category: general
date: 2026-08-17
description: تصدير Excel إلى TXT مع تحديد عدد الأرقام ذات الدقة – تعلم كيفية ضبط عدد
  الأرقام وتحويل Excel إلى نص في Java مع مثال كامل لـ Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: ar
lastmod: 2026-08-17
og_description: تصدير Excel إلى TXT مع تحديد عدد الأرقام المهمة. يوضح هذا الدليل كيفية
  ضبط عدد الأرقام وتحويل Excel إلى نص باستخدام Aspose.Cells للغة Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: تصدير Excel إلى TXT مع عدد محدود من الأرقام ذات الدقة – دليل Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: كيفية تصدير Excel إلى TXT مع تحديد عدد الأرقام ذات الدقة باستخدام Java
url: /ar/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى TXT مع تحديد عدد الأرقام ذات الدلالة باستخدام Java

إذا كنت بحاجة إلى **تصدير Excel إلى TXT** مع التحكم في عدد الأرقام ذات الدلالة، فإن هذا الدليل يوفر حلاً جاهزًا للتنفيذ. ستتعرف على كيفية ضبط الأرقام، تحويل Excel إلى نص، والحفاظ على نظافة الناتج من خلال تغيير تكوين واحد.

العينة تستخدم Aspose.Cells for Java 25.10، والتي تقدم خيار `setSignificantDigits`. بنهاية هذا الشرح يمكنك إنشاء ملف TXT يحتوي فقط على الأرقام التي تريدها، دون الحاجة إلى كود إضافي للتقريب.

## ما ستحققه

- إنشاء مصنف برمجيًا.
- إدراج قيمة رقمية في خلية.
- تكوين خيارات حفظ TXT لتحديد عدد الأرقام ذات الدلالة.
- حفظ المصنف كملف نصي عادي.
- فهم كيفية عمل إعداد `significantDigits` وكيفية تكييفه لسيناريوهات أخرى.

### المتطلبات المسبقة

- Java 17 أو أحدث (الكود يتوافق أيضًا مع Java 8).
- Aspose.Cells for Java 25.10 أو أحدث. حمّل ملف JAR من [موقع Aspose](https://products.aspose.com/cells/java) وأضفه إلى مسار الـ classpath في مشروعك.
- بيئة تطوير متكاملة أو محرر نصوص بسيط وأداة بناء سطر الأوامر (Maven/Gradle).

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

أنشئ مشروع Java جديد وأضف ملف JAR الخاص بـ Aspose.Cells إلى مسار البناء. إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **نصيحة احترافية:** استخدم المصنف `jdk17` لأحدث بيئة تشغيل Java؛ فهو يقلل من خطر التحذيرات المتعلقة بالتوافق.

## الخطوة 2: إنشاء مصنف وكتابة قيمة

المصنف يمثل ملف Excel في الذاكرة. يمكنك إضافة بيانات إلى أي خلية باستخدام طريقة `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

العدد `123.456789` سيكون المصدر لتصديرنا إلى TXT. بشكل افتراضي، كان Aspose.Cells سيكتب جميع الأرقام العشرية، مما ينتج ملفات نصية صاخبة.

## الخطوة 3: تكوين خيارات حفظ TXT لتحديد عدد الأرقام ذات الدلالة

يوفر Aspose.Cells `TxtSaveOptions` للتحكم الدقيق في مخرجات النص العادي. طريقة `setSignificantDigits` تخبر المصدّر بعدد الأرقام التي يجب الاحتفاظ بها **إجماليًا**، وليس فقط بعد الفاصلة العشرية.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

عند ضبط `significantDigits` على `4`، يقوم المصدّر بتقريب القيمة `123.456789` إلى `123.5`. يتطابق هذا السلوك مع تعريف الأرقام ذات الدلالة الرياضية: يتم الاحتفاظ بأول أربعة أرقام غير صفرية.

### كيف يختلف هذا الإعداد عن “تحديد عدد الكسور العشرية”

- **تحديد عدد الكسور العشرية** (`setDecimalPlaces`) يقتصر على حذف الأرقام *بعد* الفاصلة العشرية، بغض النظر عن الجزء الصحيح.
- **الأرقام ذات الدلالة** (`setSignificantDigits`) تُعدّ الأرقام بدءًا من أول رقم غير صفري، وهو مفيد عندما تختلف القيم في الحجم.

إذا كنت تحتاج إلى عدد ثابت من الكسور العشرية بدلاً من ذلك، استبدل السطر السابق بـ:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## الخطوة 4: حفظ المصنف كملف TXT

الآن اكتب المصنف إلى القرص باستخدام الخيارات التي تم تكوينها.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

تشغيل البرنامج ينشئ الملف `significant_digits.txt` في دليل العمل. يحتوي الملف على سطر واحد:

```
123.5
```

### النتيجة المتوقعة

| الخلية | القيمة الأصلية | المصدّر (4 أرقام ذات دلالة) |
|--------|----------------|-----------------------------|
| A1     | 123.456789     | 123.5                       |

إذا غيرت `setSignificantDigits(4)` إلى `6`، ستصبح النتيجة `123.457`. جرّب قيمًا مختلفة لترى كيف يتكيف التقريب.

## الخطوة 5: تنويعات شائعة وحالات حافة

### تصدير نطاق كامل

إذا أردت تصدير أكثر من خلية واحدة، ما عليك سوى ملء النطاق قبل الحفظ:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

إعداد `significantDigits` نفسه يُطبق على كل خلية رقمية، مما يضمن دقة موحدة عبر الملف.

### التعامل مع فواصل عشرية خاصة بالمنطقة

يحترم Aspose.Cells إعدادات المنطقة المحلية للنظام عند كتابة النص. لفرض نقطة (`.`) كفاصل عشري، اضبط ثقافة `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

هذا مفيد عندما يتوقع التطبيق المستهدف تنسيقًا معينًا، مثل محللات CSV التي تقبل `.` فقط.

### الكتابة فوق الملفات الموجودة

طريقة `save` تكتب فوق الملف الهدف بشكل افتراضي. إذا رغبت في تجنب فقدان البيانات عن طريق الخطأ، تحقق أولًا من وجود الملف:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### المصنفات الكبيرة واستهلاك الذاكرة

عند تصدير أوراق عمل ضخمة، فكر في تدفق الإخراج:

```java
saveOptions.setEnableMemorySaving(true);
```

هذا الخيار يقلل من استهلاك الذاكرة عن طريق كتابة الصفوف تدريجيًا.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله فورًا:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

تشغيل هذا الكود ينتج الملف `significant_digits.txt` بالمحتوى التالي (أعمدة مفصولة بعلامة تبويب):

```
123.5	0.001235	98770
```

كل رقم يلتزم بقاعدة **4 أرقام ذات دلالة**، مما يوضح أن الإعداد يعمل عبر قيم ذات أحجام مختلفة.

## الخلاصة

أنت الآن تعرف كيف **تصدّر Excel إلى TXT** مع التحكم في عدد الأرقام ذات الدلالة. باستخدام `TxtSaveOptions.setSignificantDigits`، يمكنك **ضبط عدد الأرقام**، **تحديد عدد الكسور العشرية**، و**تحديد الأرقام ذات الدلالة** في سطر كود واحد قابل للصيانة. النهج يعمل مع خلايا منفردة، نطاقات كاملة، ومصنفات كبيرة على حد سواء.

### الخطوات التالية

- استكشف خصائص أخرى في `TxtSaveOptions` مثل `setDelimiter('\t')` لتخصيص فواصل الأعمدة.
- اجمع المصدّر مع `CsvSaveOptions` إذا كنت تحتاج إلى قيم مفصولة بفواصل بدلاً من نص عادي.
- دمج الروتين في خدمة ويب تستقبل ملفات Excel مرفوعة وتعيد ملف TXT مقصوصًا مباشرةً.

لا تتردد في تجربة حدود أرقام مختلفة ومناطق محلية مختلفة. إذا صادفت حالة لا تلبي فيها الخيارات المدمجة متطلبات خاصة، يمكنك دائمًا معالجة ملف TXT الناتج باستخدام أدوات I/O القياسية في Java.

برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية تحويل النص إلى أرقام في Excel باستخدام Aspose.Cells للـ Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [كيفية تصدير خصائص Excel المخصصة إلى PDF باستخدام Aspose.Cells للـ Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}