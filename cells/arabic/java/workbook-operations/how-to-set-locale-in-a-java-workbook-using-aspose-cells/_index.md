---
category: general
date: 2026-11-22
description: تعلم كيفية تعيين اللغة المحلية في دفتر عمل Java، وتغيير لغة دفتر العمل،
  وتعيين التقويم إلى اليابانية مع أمثلة شفرة واضحة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: ar
lastmod: 2026-11-22
og_description: كيفية ضبط اللغة المحلية في دفتر عمل Java بسرعة. اتبع هذا الدرس لتغيير
  لغة دفتر العمل، وضبط اللغة المحلية إلى اليابانية، وتكوين التقويم الياباني.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: كيفية تعيين اللغة في دفتر عمل جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: كيفية تعيين الإعدادات الإقليمية في دفتر عمل Java باستخدام Aspose.Cells
url: /ar/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين اللغة المحلية في دفتر عمل Java باستخدام Aspose.Cells

تعيين اللغة المحلية في دفتر عمل Java هو طلب شائع عندما تحتاج إلى تكييف جدول البيانات الخاص بك مع مناطق مختلفة. في هذا الدليل ستتعلم كيفية تعيين اللغة المحلية، تغيير لغة دفتر العمل، وتعيين التقويم إلى اليابانية باستخدام Aspose.Cells API.

تدويل دفتر العمل يتجاوز مجرد ترجمة النص؛ فهو يؤثر أيضًا على تنسيقات الأرقام، تحليل التواريخ، ونظام التقويم الافتراضي. بنهاية هذا البرنامج التعليمي ستكون قادرًا على:

* تكوين اللغة المحلية لدفتر العمل إلى اليابانية (اليابان) – **set locale to japanese**.  
* تغيير لغة دفتر العمل بحيث تحترم الصيغ وسلاسل واجهة المستخدم الثقافة المستهدفة – **change workbook language**.  
* تبديل التقويم إلى التقويم الإمبراطوري الياباني – **how to set calendar**.  

تعمل الخطوات مع أي نسخة حديثة من Aspose.Cells for Java (v23.9 أو أحدث) وتتطلب فقط بيئة تطوير Java قياسية.

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| Java 8 أو أعلى | المكتبة تستهدف Java 8+. |
| Aspose.Cells for Java (v23.9+) | توفر الكائنات `Workbook`، `WorkbookSettings`، وأدوات اللغة المحلية. |
| IDE (IntelliJ IDEA، Eclipse، أو VS Code) | لتجميع وتشغيل العينة. |
| معرفة أساسية بـ Java | مطلوبة لفهم مقتطفات الشيفرة. |

أضف تبعية Aspose.Cells Maven إلى ملف `pom.xml` الخاص بك (أو قم بتنزيل ملف JAR يدويًا):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## كيفية تعيين اللغة المحلية والتقويم في دفتر عمل

الخطوة الأولى هي إنشاء نسخة من دفتر العمل والحصول على كائن الإعدادات الخاص به. كائن الإعدادات يتيح الوصول إلى واجهات برمجة التطبيقات للغة المحلية والتقويم.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### لماذا كل سطر مهم

* **`new Workbook()`** – ينشئ دفتر عمل فارغ يمكنك التلاعب به قبل الحفظ.  
* **`getSettings()`** – يُعيد كائن `WorkbookSettings`؛ جميع الخيارات الإقليمية موجودة هنا.  
* **`setCalendar(...)`** – يستبدل التقويم الميلادي الافتراضي بالتقويم الإمبراطوري الياباني، مما يؤثر على طريقة عرض وتحليل التواريخ.  
* **`setLocale(new Locale("ja","JP"))`** – يغيّر اللغة والاتفاقيات الإقليمية (مثل الشهور، فواصل الأعداد). هذا هو جوهر **how to set locale** لدفتر العمل.  

تشغيل البرنامج ينشئ ملف `LocaleDemo.xlsx`. افتحه في Excel أو LibreOffice وسترى أسماء الشهور اليابانية، رموز عملة الين الياباني، وتواريخ مُنسقة وفقًا للتقويم الياباني.

## تغيير لغة دفتر العمل (تعيين اللغة المحلية إلى اليابانية)

إذا كان هدفك الأساسي هو **تغيير لغة دفتر العمل**، يمكنك التركيز على استدعاء `setLocale` فقط. المقتطف التالي يعزل تلك الخطوة:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**ما الذي يتغير؟**  
* سلاسل تنسيق الخلايا تتحول إلى اليابانية (مثال، `#,##0.00` يصبح `#,##0.00` مع رمز الين).  
* أسماء الدوال المدمجة (مثل `SUM`) تبقى بالإنجليزية لأن لغة دوال Excel مستقلة، لكن سلاسل التواريخ ورسائل الأخطاء تتبع conventions اليابانية.  

**متى تستخدم هذا؟**  
* عندما تحتاج إلى جدول بيانات يعرض الأرقام والتواريخ لجمهور ياباني لكن يمكن أن يبقى التقويم الأساسي Gregorian.  
* للتقارير التي تُصدّر إلى PDF أو تُطبع، لضمان أن اللغة البصرية تتطابق مع السوق المستهدف.

## كيفية تعيين التقويم إلى التقويم الياباني

أحيانًا يكون طلب **how to set calendar** منفصلًا عن اللغة المحلية. بالنسبة للأنظمة القديمة التي تخزن التواريخ في العصر الإمبراطوري الياباني، يجب عليك تعيين التقويم صراحةً مع إمكانية الاحتفاظ باللغة المحلية الافتراضية.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**نقاط رئيسية:**

* `Calendar.getInstance(Locale.JAPAN)` تُعيد كائن `java.util.Calendar` مُكوَّن للعصر الياباني.  
* سيعرض دفتر العمل الآن التواريخ باستخدام رموز العصور (R لـ Reiwa، H لـ Heisei، إلخ).  
* هذا الإعداد **لا** يؤثر على تنسيق الأرقام أو لغة واجهة المستخدم؛ اجمعه مع `setLocale` إذا كنت بحاجة إلى كليهما.

## مثال كامل من البداية إلى النهاية

فيما يلي برنامج كامل وقابل للتنفيذ يوضح **how to set locale**، **change workbook language**، و **set the calendar** في تدفق موحد. كما يضيف خلية عينة لتوضيح التأثير.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**الناتج المتوقع:**  
فتح `FullJapaneseLocale.xlsx` يُظهر الخلية الأولى بتاريخ مثل `R3/04/01` (ريiwa 3) والخلية الثانية مُنسقة كـ `¥1,234,567.89`. هذا يؤكد أن **how to set locale**، **change workbook language**، و **how to set calendar** تعمل جميعًا معًا.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|---------|----------------|-----|
| استخدام `Locale.CHINA` بدلاً من `new Locale("ja","JP")` | `Locale.CHINA` يحدد اللغة الصينية، وليس اليابانية. | دائمًا أنشئ `Locale` باستخدام `"ja", "JP"` للغة اليابانية. |
| نسيان استدعاء `settings.setCalendar(...)` بعد `setLocale` | التقويم ي默认 إلى Gregorian، لذا تظهر التواريخ في العصر الخطأ. | استدعِ `setCalendar` **بعد** تعيين اللغة المحلية، أو عيّن كليهما معًا كما هو موضح. |
| حفظ دفتر العمل قبل تطبيق الإعدادات | الإعدادات تُطبق على الكائن في الذاكرة؛ الحفظ المبكر يكتب اللغة المحلية الافتراضية. | طبق جميع تغييرات اللغة المحلية/التقويم **قبل** استدعاء `workbook.save()`. |
| استخدام نسخة قديمة من Aspose.Cells | الإصدارات القديمة تفتقر إلى التحميل الزائد `setCalendar`. | قم بالترقية إلى v23.9+ أو تحقق من ملاحظات الإصدار لدعم اللغة المحلية. |

## اختبار التكوين الخاص بك

1. شغّل الفئة **FullLocaleExample**.  
2. افتح الملف `FullJapaneseLocale.xlsx` المُنشأ في Excel.  
3. تحقق من أن:  
   * عمود التاريخ يظهر رموز العصور اليابانية (`R`، `H`، إلخ).  
   * عمود الأرقام يستخدم رمز الين وفواصل الفواصل.  
   * أي رسائل خطأ مدمجة (مثل `#DIV/0!`) تظهر باليابانية إذا كان دفتر العمل يحتوي على أخطاء.  

إذا فشل أي من هذه الفحوصات، تحقق مرة أخرى من أن كائن `WorkbookSettings` الذي عدلته هو نفس المثيل المستخدم عند الحفظ.

## الخطوات التالية

* **توطين الصيغ** – بينما تتحكم اللغة المحلية في التنسيق، يمكنك أيضًا ترجمة أسماء الدوال المخصصة باستخدام `FormulaParser`.  
* **تطبيق اللغة المحلية على دفاتر العمل الموجودة** – حمّل دفتر عمل باستخدام `new Workbook

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تنسيق تاريخ Aspose Cells: كيفية تعيين تنسيق تاريخ مخصص في Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [كيفية تعيين اللغة في ملفات Excel باستخدام Aspose.Cells .NET للدعم متعدد اللغات](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [كيفية تعيين تنسيق رقم الخلية وتحويل التواريخ اليابانية في C# باستخدام Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}