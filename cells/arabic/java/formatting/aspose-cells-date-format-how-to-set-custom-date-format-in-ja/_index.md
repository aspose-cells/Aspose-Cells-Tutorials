---
category: general
date: 2026-06-21
description: دليل تنسيق التاريخ في Aspose Cells – تعلم كيفية تعيين تنسيق تاريخ مخصص،
  وتغيير لغة دفتر العمل، وتطبيق تنسيق تاريخ عالمي في Java.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: ar
og_description: 'دليل تنسيق التاريخ في Aspose Cells: تعلم كيفية تعيين تنسيق تاريخ
  مخصص، وتغيير لغة المصنف، وتعيين تنسيق تاريخ عالمي لمشاريع Java.'
og_title: تنسيق تاريخ Aspose Cells – تعيين تنسيق تاريخ مخصص في Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'تنسيق التاريخ في Aspose Cells: كيفية تعيين تنسيق تاريخ مخصص في Java'
url: /ar/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل Aspose Cells لتنسيق التاريخ – دليل Java كامل

هل تساءلت يومًا كيف تضبط تنسيق تاريخ مخصص في Aspose Cells for Java؟ لست الوحيد. سواء كنت تُنشئ تقارير لعميل ياباني أو تحتاج فقط إلى نمط تاريخ موحد عبر كامل دفتر العمل، فإن إتقان **aspose cells date format** أمر أساسي.

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح لك **how to set date format** عالميًا، وتغيير إعدادات المنطقة (locale) لدفتر العمل، وتطبيق نمط مخصص مثل سنة العصر الياباني. في النهاية ستحصل على قطعة شفرة قابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع—بدون تخمين.

## ما يغطيه هذا الدليل

- إنشاء نسخة جديدة من `Workbook`.
- تغيير إعدادات المنطقة لدفتر العمل بحيث تحترم الصيغ المدمجة القواعد الإقليمية.
- تعريف **set custom date format** باستخدام `DateTimeFormatter`.
- تطبيق هذا التنسيق عالميًا باستخدام `WorkbookSettings`.
- المشكلات الشائعة (مثل تجاوز تنسيقات الخلايا) وكيفية تجنبها.
- تغييرات سريعة للغات أخرى أو سلاسل التنسيق.

كل ما تحتاجه هو بيئة تطوير Java، Maven أو Gradle لجلب Aspose Cells، وفهم أساسي لبنية Java. جاهز؟ لنبدأ.

## الخطوة 1: إعداد المشروع واستيراد Aspose Cells

أولاً وقبل كل شيء—تأكد من أن Aspose Cells for Java موجود في مسار الفئات (classpath). إذا كنت تستخدم Maven، أضف الاعتماد التالي إلى ملف `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

مستخدمي Gradle يمكنهم إضافة:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **نصيحة احترافية:** Aspose تقدم ترخيص تجريبي مجاني لمدة 30 يومًا. ضع ملف `Aspose.Cells.lic` في جذر المشروع واستدعِ `License license = new License(); license.setLicense("Aspose.Cells.lic");` قبل إنشاء أي دفتر عمل.

الآن استورد الفئات التي سنحتاجها:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

هذه الاستيرادات تمنحنا الوصول إلى حاوية دفتر العمل، إعداداته، والملفّ المعياري المتوافق مع المنطقة.

## الخطوة 2: إنشاء دفتر عمل جديد والوصول إلى إعداداته

نسخة جديدة من `Workbook` تبدأ بالإعداد الافتراضي (عادةً US). للتحكم في معالجة التاريخ عالميًا، يجب جلب كائن `WorkbookSettings` الخاص به:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

كائن `settings` هو مركز التحكم. أي تغيير تجريه هنا—مثل تنسيق التاريخ—سيؤثر على كل خلية **لا** تملك نمطًا صريحًا يتجاوز ذلك.

## الخطوة 3: تعريف تنسيق تاريخ/وقت مخصص (مثال العصر الياباني)

لنفترض أنك تحتاج تواريخ بنمط العصر الياباني، مثل “令和04.10.01”. النمط `"ggyy.MM.dd"` ينجح عندما يُقترن بثقافة يابانية:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

إذا كنت تفضّل نمط ISO أبسط (`"yyyy-MM-dd"`)، استبدل سلسلة النمط فقط—دون أي تغييرات أخرى.

## الخطوة 4: تطبيق التنسيق المخصص كتنسيق تاريخ عالمي

الآن نربط المُنسق بإعدادات دفتر العمل العالمية. هذه هي خطوة **set global date format** التي تضمن أن أي خلية تعرض تاريخًا تستخدم نمطنا تلقائيًا:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

في هذه المرحلة، أي تاريخ تكتبه في الورقة—سواء عبر `Cell.putValue(new Date())` أو بقراءة من مصدر بيانات—سيُعرض باستخدام نمط العصر الياباني.

## الخطوة 5: ملء دفتر العمل بتواريخ تجريبية (اختياري)

لنضيف بضع صفوف لترى التنسيق قيد التنفيذ. هذا الجزء ليس ضروريًا تمامًا لمنطق تنسيق التاريخ، لكنه يساعد على التحقق من أن كل شيء يعمل:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

عند حفظ دفتر العمل، ستظهر تلك الخلايا شيئًا مثل:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(السنة الدقيقة للعصر تعتمد على التقويم الياباني الحالي.)

## الخطوة 6: حفظ دفتر العمل والتحقق من النتيجة

أخيرًا، اكتب دفتر العمل إلى ملف لتتمكن من فتحه في Excel أو LibreOffice أو أي عارض يحترم التنسيق:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

افتح `CustomDateFormatDemo.xlsx` وسترى التواريخ مُعروضة وفق النمط الذي حددناه. إذا لاحظت أي اختلاف، تحقق مرة أخرى من عدم وجود نمط على مستوى الخلية يتجاوز الإعداد العالمي (انظر قسم “Edge Cases” أدناه).

## الحالات الخاصة والاختلافات

### 1. تجاوز التنسيق العالمي على مستوى الخلية

إذا كانت الخلية لديها نمط بصيغة رقمية محددة، يتم تجاهل الإعداد العالمي لتلك الخلية. لإجبار الخلية على استخدام التنسيق العالمي، امسح نمط الخلية:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. تغيير إعدادات المنطقة لدفتر العمل دون نمط مخصص

أحيانًا قد ترغب فقط في **change workbook locale** بحيث تتبع صيغ التاريخ المدمجة (مثل `14‑03‑2024`) العادات الإقليمية. يمكنك فعل ذلك دون `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

الآن أي نمط تاريخ افتراضي سيظهر كـ `21/04/2025` بدلاً من `04/21/2025`.

### 3. استخدام تنسيقات مخصصة متعددة في دفتر عمل واحد

Aspose Cells يسمح لك بتعريف عدة تنسيقات مخصصة وتطبيقها بشكل انتقائي:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. إعادة الضبط إلى التنسيق الافتراضي

إذا احتجت للعودة إلى معالجة التاريخ الافتراضية في Aspose، ما عليك سوى تمرير `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## الأسئلة الشائعة

- **هل يؤثر هذا على أوراق العمل الموجودة؟**  
  نعم—أي ورقة تُحمَّل إلى `Workbook` بعد ضبط التنسيق العالمي ستورثه، ما لم تكن الخلية لديها نمط صريح مسبقًا.

- **هل يمكنني ضبط التنسيق بعد كتابة البيانات؟**  
  بالتأكيد. يُطبق التنسيق العالمي وقت العرض، لذا يمكنك ملء الخلايا أولًا ثم ضبط التنسيق لاحقًا.

- **ماذا لو احتجت تقويمًا إقليميًا (مثل التقويم البوذي التايلاندي)؟**  
  استخدم رمز `CultureInfo` المناسب (`"th-TH"`)، وسيحترم المُنسق ذلك التقويم تلقائيًا.

- **هل هناك تأثير على الأداء؟**  
  ضئيل جدًا. يُخزن المُنسق في ذاكرة `WorkbookSettings`، لذا يُستدعى مرة واحدة فقط لكل دفتر عمل.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ والذي يضم كل خطوة تم مناقشتها:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**الناتج المتوقع في Excel:**

| الخلية | القيمة المعروضة |
|------|----------------|
| A1   | 令和05.04.21   |
| A2   | 令和06.12.31   |
| A3   | 令和05.04.21 14:45:03 (قد يختلف الجزء الزمني) |

افتح الملف، وسترى التواريخ مُنسقة تمامًا كما عُرِّفت.

## الخلاصة

لقد تعلمت الآن كيفية **aspose cells date format** دفتر عمل في Java، من تغيير الإعداد الإقليمي إلى تطبيق **set custom date format** يعمل عالميًا. باستخدام `WorkbookSettings` و `DateTimeFormatter`، تحصل على تحكم دقيق في طريقة عرض كل تاريخ—دون الحاجة لتنسيق يدوي.

بعد ذلك، قد ترغب في استكشاف **how to set date format** لأعمدة محددة فقط، أو دمج تنسيقات رقمية مخصصة مع التنسيق الشرطي للحصول على تقرير مصقول. المبادئ نفسها تنطبق: عرّف مُنسقًا، اربطه عبر النمط، ودع Aspose يتولى البقية.

برمجة سعيدة، ولا تتردد في تجربة لغات أخرى—سيشكرك المستخدمون على جداول البيانات المتقنة والمتوافقة ثقافيًا!

## ما الذي ينبغي أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحويل Excel إلى PDF بكفاءة مع تنسيقات تاريخ مخصصة باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [إتقان عرض البيانات في Excel: تنسيق الأرقام وتواريخ مخصصة باستخدام Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [كيفية إنشاء وتنسيق خلايا Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}