---
category: general
date: 2026-08-20
description: تعلم تصدير Excel إلى TXT مع تحديد عدد المنازل العشرية، والحفاظ على الأرقام
  الهامة، وحفظ المصنف كملف TXT باستخدام Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: ar
lastmod: 2026-08-20
og_description: تصدير Excel إلى TXT باستخدام Aspose.Cells. يوضح هذا الدليل كيفية تحديد
  عدد المنازل العشرية، الحفاظ على الأرقام ذات الدقة، وحفظ المصنف كملف TXT في Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: تصدير Excel إلى TXT في Java – التحكم في المنازل العشرية والأرقام ذات الدقة
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: كيفية تصدير Excel إلى TXT باستخدام Aspose.Cells والتحكم في دقة الأعداد العشرية
url: /ar/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Excel إلى TXT باستخدام Aspose.Cells والتحكم في دقة الفاصلة العشرية

إذا كنت بحاجة إلى **تصدير Excel إلى TXT** وضمان أن الناتج يحترم عددًا محددًا من الأماكن العشرية، فإن هذا الدليل يوفر حلاً كاملاً. سترى كيفية تحديد عدد الأماكن العشرية، الحفاظ على الأرقام ذات الدلالة، و**حفظ المصنف كملف TXT** باستخدام مكتبة Aspose.Cells للغة Java.

يقوم البرنامج التعليمي بشرح إنشاء مصنف، إدخال قيمة ذات دقة عالية، تكوين خيارات حفظ TXT، وكتابة الملف إلى القرص. في النهاية يمكنك إنشاء ملف نصي يحتوي على الدقة المطلوبة بالضبط، دون الحاجة إلى معالجة يدوية لاحقة.

## ما ستحتاجه

- Java 17 (أو أي JDK مدعوم)
- Aspose.Cells for Java 23.10 أو أحدث
- بيئة تطوير متكاملة أو أداة بناء (Maven/Gradle) لإدارة التبعيات
- صلاحية كتابة إلى دليل الإخراج

## الخطوة 1: إنشاء مصنف والوصول إلى ورقة العمل الأولى

إنشاء مصنف هو الخطوة الأولى عندما تريد **تصدير Excel إلى TXT**. تمثل الفئة `Workbook` ملف Excel بالكامل، وتوفر `Worksheet` الوصول إلى الخلايا.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*لماذا هذا مهم*: كائن المصنف يحتوي على جميع البيانات والأنماط والبيانات الوصفية. بدءًا بمصنف جديد يضمن عدم تدخل أي تنسيق مخفي في عملية تصدير النص.

## الخطوة 2: إضافة قيمة عددية وتحديد عدد الأماكن العشرية

أدخل رقمًا يحتوي على العديد من الأماكن العشرية حتى تتمكن من توضيح كيفية **تحديد عدد الأماكن العشرية** أثناء التصدير.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*لماذا هذا مهم*: Excel يخزن الدقة الكاملة، ولكن عندما تقوم بالتصدير لاحقًا، قد ترغب في قطع أو تقريب القيمة. سيقوم إعداد `limit decimal places` بمعالجة ذلك تلقائيًا.

## الخطوة 3: تكوين خيارات حفظ TXT للحفاظ على الأرقام ذات الدلالة

توفر Aspose.Cells الفئة `TxtSaveOptions`. ضبط `significantDigits` يخبر أداة التصدير بالحفاظ فقط على العدد المطلوب من الأرقام ذات الدلالة، متجاهلًا الأصفار البادئة.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*لماذا هذا مهم*: خيار **keep significant digits** يضمن أن ملف الإخراج يحتوي على كمية دقيقة متوقعة، وهو أمر أساسي للأنظمة المتلقية التي تتوقع تنسيقًا رقميًا ثابت العرض.

## الخطوة 4: حفظ المصنف كملف TXT

أخيرًا، قم بكتابة المصنف إلى ملف نصي. طريقة `save` تحترم الخيارات التي قمت بتكوينها، لذا سيحتوي الملف الناتج على تمثيل عشري محدود.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*لماذا هذا مهم*: استخدام **save workbook as txt** مع `TxtSaveOptions` المُعد يضمن أن ملف التصدير يطابق قيود الدقة التي حددتها في الخطوة السابقة.

### المحتوى المتوقع لـ `SignificantDigits.txt`

```
0.00012346
```

القيمة تُظهر خمسة أرقام ذات دلالة (`12346`) بعد التقريب، وتُحافظ على الأصفار البادئة وفقًا لتنسيق TXT.

## المتغيّرات والحالات الخاصة

| السيناريو | التعديل |
|----------|------------|
| **عدد مختلف من الأرقام ذات الدلالة** | استدعِ `txtOptions.setSignificantDigits(n)` حيث `n` تتراوح بين 1‑15. |
| **تصدير نطاق بدلاً من كامل الورقة** | استخدم `txtOptions.setExportRange("A1:B10")` قبل الحفظ. |
| **الحفاظ على فواصل الأعمدة** | عيّن `txtOptions.setSeparator('\t')` لإخراج مفصول بعلامة تبويب. |
| **أوراق عمل كبيرة** | زد `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` لتجنب `OutOfMemoryError`. |

## الأخطاء الشائعة والنصائح الاحترافية

- **لا تخلط بين الأرقام ذات الدلالة والأماكن العشرية**. الأصفار البادئة لا تُحسب كأرقام ذات دلالة؛ استخدم `setSignificantDigits` للدقة المعنوية و`setDecimalPlaces` إذا كنت بحاجة إلى عدد ثابت من الأرقام بعد الفاصلة العشرية.
- **دائمًا حدد مسار إخراج مطلق** عند التشغيل من بيئة التطوير المتكاملة لتجنب أخطاء الأذونات.
- **تحقق من صحة الملف المُولد** باستخدام استدعاء بسيط `java.nio.file.Files.readAllLines(Paths.get(outputPath))` للتأكد من أن المحتوى يطابق التوقعات قبل تمريره إلى العمليات اللاحقة.

## الكود الكامل للمرجعية

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

تشغيل البرنامج ينتج ملف `SignificantDigits.txt` يحتوي على السطر الوحيد `0.00012346`، مما يوضح أن عملية **export excel to txt** تحترم كلًا من متطلبات **limit decimal places** و**keep significant digits**.

## الخلاصة

أنت الآن تعرف كيفية **تصدير Excel إلى TXT** باستخدام Aspose.Cells للغة Java مع التحكم في دقة الأرقام. من خلال تكوين `TxtSaveOptions` يمكنك **تحديد عدد الأماكن العشرية**، **الحفاظ على الأرقام ذات الدلالة**، وحفظ المصنف كملف txt بشكل موثوق دون الحاجة إلى معالجة لاحقة إضافية.

التالي، قد تستكشف:

- تصدير عدة أوراق إلى ملفات TXT منفصلة (`save workbook as txt` لكل ورقة)
- استخدام `setSeparator` لإنشاء إخراج متوافق مع CSV
- أتمتة التحويلات الدفعية لمجموعات بيانات كبيرة

لا تتردد في تجربة عدد مختلف من الأرقام والفواصل لتتناسب مع احتياجات مشروعك الدقيقة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [حفظ Excel كنص – دليل C# كامل لتصدير Excel إلى TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [تصدير مصنف Excel كصورة باستخدام Aspose.Cells للغة Java&#58; دليل خطوة بخطوة](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}