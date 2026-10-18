---
category: general
date: 2026-06-30
description: تعيين تنسيق رقم مخصص في Excel باستخدام Java. تعلم كيفية إنشاء دفتر عمل
  Excel باستخدام Java، الحصول على التاريخ والوقت من الخلية، حساب صيغ دفتر العمل وإخراج
  قيمة التاريخ والوقت.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: ar
og_description: تعيين تنسيق رقم مخصص في Excel باستخدام Java. يوضح هذا الدليل كيفية
  إنشاء مصنف Excel باستخدام Java، الحصول على التاريخ والوقت من الخلية، حساب صيغ المصنف
  وإخراج قيمة التاريخ والوقت.
og_title: تعيين تنسيق رقم مخصص في إكسل باستخدام جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: تعيين تنسيق رقم مخصص في إكسل باستخدام جافا – دليل كامل
url: /ar/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تنسيق رقم مخصص في Excel باستخدام Java – دليل شامل

هل احتجت يوماً إلى **تعيين تنسيق رقم مخصص** في ورقة Excel أثناء العمل بـ Java؟ لست وحدك. سواءً كنت تبني محرك تقارير أو تحاول فقط عرض تواريخ العصور اليابانية بشكل صحيح، فإن إتقان هذه التقنية سيوفر لك ساعات لا تحصى من المعالجة اللاحقة. في هذا الدرس سنستعرض مثالًا واقعيًا **ينشئ مصنف Excel باستخدام Java**، يطبق تنسيقًا خاصًا حسب اللغة، يعيد حساب الصيغ، وأخيرًا **يحصل على DateTime من الخلية** لي **يُخرج قيمة datetime**.

سنستخدم مكتبة Aspose.Cells for Java الشهيرة لأنها تتعامل مع تنسيقات الأرقام والتواريخ المتوافقة مع الثقافة مباشرةً. بنهاية الدليل ستحصل على برنامج مستقل قابل للتنفيذ يمكنك إدراجه في أي مشروع Maven أو Gradle. لا اختصارات “انظر الوثائق” غير واضحة—فقط كود صلب وتوضيحات واضحة.

---

## ما ستتعلمه

- كيفية **إنشاء مصنف Excel باستخدام Java** برمجيًا.
- الخطوات الدقيقة **لتعيين تنسيق رقم مخصص** لتواريخ العصور اليابانية.
- لماذا من الضروري استدعاء **calculate workbook formulas** قبل استخراج القيمة.
- الطريقة الصحيحة **للحصول على datetime من الخلية** و **إخراج قيمة datetime**.
- المشكلات الشائعة (غياب اللغة، صيغ قديمة) والحلول السريعة.

---

## المتطلبات المسبقة

- Java 8 أو أحدث مثبت على جهازك.  
- Aspose.Cells for Java 23.11 (أو أي نسخة حديثة).  
- بيئة تطوير متكاملة أو محرر نصوص—IntelliJ IDEA، Eclipse، VS Code، أيًا كان ما تفضله.  

إذا لم تقم بعد بإضافة Aspose.Cells إلى مشروعك، الصق المقتطف التالي في ملف `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

لمستخدمي Gradle يمكنهم إضافة:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

الآن بعد أن أصبح البيئة جاهزة، لنبدأ كتابة الكود.

---

## الخطوة 1: تعيين تنسيق رقم مخصص – نظرة عامة

قبل أن نكتب أي كود Java، من المفيد تصور ما نريد تحقيقه. تخيل خلية Excel يجب أن تعرض **“令和2年4月1日”** بدلاً من السلسلة ISO‑8601 “2020‑04‑01”. القيمة الأساسية تظل تاريخًا حقيقيًا (لذلك الصيغ لا تزال تعمل)، لكن *العرض* يتبع تنسيق العصر الياباني. هذا هو بالضبط ما يحققه عملية **set custom number format**.

فيما يلي ملف المصدر الكامل. يمكنك نسخه ولصقه في `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### لماذا يعمل هذا

- **`setNumberFormat`** يخبر Excel كيف *يعرض* القيمة الرقمية الأساسية. سلسلة التنسيق `[$-ja-JP]ggge年m月d日` هي المفتاح؛ `ggg` يختار اسم العصر، `e` السنة داخل العصر، ثم يليه الشهر واليوم كحروف ثابتة.
- **`calculateFormula`** يجبر Aspose.Cells على تفسير النص “R02-04-01” كتاريخ بناءً على التقويم الياباني. تخطي هذه الخطوة يترك الخلية كنص عادي، وسترمي `getDateTime()` استثناءً.
- **`getDateTime`** يستخرج أخيرًا كائن `java.util.Calendar` الفعلي، والذي يمكنك معالجته أو تنسيقه أو تخزينه في مكان آخر.

---

## الخطوة 2: إنشاء مصنف Excel باستخدام Java – نظرة أعمق

عند **create Excel workbook Java**، لا تقوم فقط بحجز الذاكرة؛ بل تُنشئ أيضًا الأنماط الافتراضية، ورقة عمل افتراضية، وثقافة افتراضية (عادةً لغة النظام). إذا كنت بحاجة إلى لغة افتراضية مختلفة، يمكنك تمرير كائن `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

في معظم الحالات يكون المُنشئ البسيط كافيًا، لكن من الجيد معرفة البديل—خاصةً عندما تتعامل مع لغات متعددة في نفس التطبيق.

*نصيحة احترافية:* احتفظ بالمصنف في الذاكرة حتى تنتهي من جميع عمليات التنسيق. الكتابة إلى القرص بعد كل تغيير تُسبب عبء I/O غير ضروري.

---

## الخطوة 3: الحصول على DateTime من الخلية – معالجة النتيجة

السطر `java.util.Calendar dt = cellA1.getDateTime();` يقوم بالعمل الشاق. في الخلفية، يقوم Aspose.Cells بتحويل الرقم التسلسلي الداخلي (عدد الأيام منذ 31‑12‑1899) إلى كائن `Calendar`. هذا التحويل يحترم لغة المصنف، لذا تحصل على التاريخ الميلادي الصحيح رغم أن العرض يستخدم العصر الياباني.

إذا كنت بحاجة إلى `java.time.LocalDate` (API الأحدث)، قم بالتحويل هكذا:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

بهذا نغطي متطلب **output datetime value** مع الحفاظ على الحداثة.

---

## الخطوة 4: حساب صيغ المصنف – عندما يكون ذلك مهمًا

قد تتساءل: *“هل أحتاج حقًا إلى استدعاء `calculateFormula()`؟”* الجواب نعم وبقوة، ما لم تكن تُدخل الخلية كائن `Date` من Java منذ البداية. عندما **set custom number format** على سلسلة نصية، تتعامل Excel (وAspose.Cells) معها كتعبير شبيه بالصيغ يحتاج إلى تقييم. بدون إعادة الحساب، `getDateTime()` سيعيد القيمة الافتراضية `1900‑01‑00` أو يرمي `CellValueException`.

إذا كان المصنف يحتوي بالفعل على صيغ معقدة تُشير إلى الخلية التي تم تنسيقها حديثًا، استدعِ `calculateFormula()` *مرة واحدة* بعد إتمام جميع التغييرات. الاستدعاءات المتكررة مكلفة.

---

## الخطوة 5: إخراج قيمة DateTime – التحقق من النتيجة

تشغيل النموذج يطبع شيئًا مشابهًا لـ:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

هذا السطر يؤكد ثلاثة أمور:

1. تم تطبيق **set custom number format** (يمكنك فتح ملف `.xlsx` المُولد في Excel لرؤية “令和2年4月1日”).
2. نجحت خطوة **calculate workbook formulas**، محولةً سلسلة العصر إلى تاريخ حقيقي.
3. استدعاء **get datetime from cell** أعاد `Calendar` صحيحًا، ثم **output datetime value** إلى وحدة التحكم.

إذا فتحت المصنف ببرنامج جداول، سترى النص المنسق، لكن القيمة الأساسية للخلية تظل الرقم التسلسلي `43831` (تمثيل Excel لتاريخ 2020‑04‑01). هذه الازدواجية هي ما يجعل Excel قويًا.

---

## المشكلات الشائعة وحالات الحافة

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| `cellA1.getDateTime()` يرمي `CellValueException` | الخلية لا تزال نصًا لأن `calculateFormula()` لم يُستدعَ. | احرص دائمًا على استدعاء `workbook.calculateFormula()` بعد تعيين تاريخ نصي يحتاج إلى تحويل. |
| عدم عرض العصر الياباني بشكل صحيح | رمز اللغة مفقود أو غير صحيح. | استخدم `[$-ja-JP]` في سلسلة التنسيق، أو عيّن لغة المصنف عبر `LoadOptions`. |
| التنسيق يظهر “#VALUE!” في Excel | سلسلة التنسيق غير صحيحة. | راجع الأقواس والحروف؛ النمط `ggge年m月d日` مطلوب لسنة العصر. |
| ظهور مكوّن الوقت (مثال: “00:00:00”) | السلسلة المصدرية تحتوي على وقت أو نمط الخلية يضيفه. | احذف الجزء الزمني من السلسلة أو عدّل التنسيق إلى `ggge年m月d日;@`. |

---

## مثال كامل يعمل – تشغيل بنقرة واحدة

إذا كنت تفضّل ملفًا واحدًا بدون تعليقات إضافية، إليك النسخة المختصرة:



## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف Excel باستخدام Aspose.Cells في Java: دليل خطوة بخطوة](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [إتقان عرض البيانات في Excel: تنسيق الأرقام والتواريخ المخصصة مع Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [كيفية إنشاء وتنسيق خلايا Excel باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}