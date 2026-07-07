---
category: general
date: 2026-07-03
description: تعلم كيفية توسيع المصفوفة في Excel باستخدام Java. يغطي هذا الدرس توسيع
  المصفوفة إلى صفوف، وكيفية استخدام التوسيع، وكيفية إدراج الصيغة بكفاءة.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: ar
og_description: قم بتوسيع المصفوفة في Excel باستخدام Java. اتبع هذا الدليل لتتعلم
  كيفية استخدام التوسيع، وضع الصيغة في الخلية، وتوسيع المصفوفة إلى الصفوف فورًا.
og_title: توسيع المصفوفة في إكسل باستخدام جافا – دليل برمجة شامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: توسيع المصفوفة في إكسل باستخدام جافا – دليل خطوة بخطوة
url: /ar/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# توسيع المصفوفة في Excel باستخدام Java – دليل برمجة كامل

هل تساءلت يومًا كيف **توسيع المصفوفة في Excel** دون سحب الخلايا يدويًا؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى إنشاء نطاق ديناميكي برمجيًا—خاصةً عندما تكون دالة Excel `EXPAND` الجديدة لا تزال حديثة. في هذا الدليل سنوضح لك بالضبط **كيفية استخدام EXPAND**، وإدراج الصيغة في ورقة العمل، وجعل النتيجة تمتد إلى الصفوف التي تريدها. بنهاية القراءة ستتمكن من **توسيع المصفوفة إلى صفوف** بسطر واحد من كود Java.

سنمر عبر مثال كامل قابل للتنفيذ باستخدام مكتبة Aspose.Cells for Java. لا مراجع غامضة، فقط كود ملموس يمكنك نسخه‑ولصقه، تجميعه، وتشغيله. على طول الطريق سنناقش لماذا كل خطوة مهمة، نتناول الحالات الخاصة مثل المصفوفات غير المتصلة، ونضيف بعض النصائح الاحترافية التي لا تجدها في الوثائق الرسمية. جاهز؟ لنبدأ.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* Java 17 (أو أي JDK حديث) مثبت.
* Maven أو Gradle لإدارة الاعتمادات.
* ترخيص صالح لـ Aspose.Cells for Java (الإصدار التجريبي المجاني يكفي للاختبار).
* إلمام أساسي بصيغ Excel—إذا كنت قد استخدمت `VLOOKUP` أو `SUMIF` من قبل، فأنت جاهز.

إذا كان أي من هذه غير مألوف لك، توقف وقم بإعداده أولًا؛ باقي الدرس يفترض أن كل شيء جاهز.

## الخطوة 1: إعداد مشروع Maven وإضافة Aspose.Cells

للحفاظ على التنظيم، أنشئ مشروع Maven جديد باسم `ExpandArrayDemo`. أضف اعتماد Aspose.Cells إلى ملف `pom.xml` الخاص بك:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **نصيحة احترافية:** إذا كنت تستخدم Gradle، فإن الاعتماد نفسه يكون كالتالي `implementation 'com.aspose:aspose-cells:23.12'`.

بعد أن ينتهي Maven من تحميل الاعتمادات، ستكون جاهزًا لكتابة كود Java **يضع صيغة في الخلية**.

## الخطوة 2: إنشاء Workbook والوصول إلى الورقة الأولى

القطعة الأولى من الكود تعكس المقتطف الذي رأيته مسبقًا، لكننا سنضيف بعض فحوصات الأمان وتعليقات لتفهم *السبب* وراء كل سطر.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*لماذا هذا مهم:* إنشاء كائن `Workbook` يخصص البُنى الداخلية التي تحتاجها Aspose لإدارة الخلايا، الصيغ، والأنماط. الوصول إلى الورقة الأولى هو نقطة الدخول الأكثر شيوعًا، خاصةً عندما تكون في مرحلة التجربة.

## الخطوة 3: إدراج صيغة EXPAND – “كيفية إدراج الصيغة”

الآن يأتي قلب الدرس: **كيفية إدراج صيغة** توسع مصفوفة. دالة Excel `EXPAND` تأخذ ثلاثة معاملات—المصفوفة المصدر، عدد الصفوف المطلوب، وعدد الأعمدة المطلوب. في حالتنا نريد توسيع `{1,2,3}` إلى **5 صفوف** و**عمود واحد**.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

لاحظ أننا استخدمنا `putFormula` بدلاً من `putValue`. هذا يخبر Aspose بأن يتعامل مع السلسلة كصيغة Excel فعلية، وليس كقيمة نصية عادية. طريقة `putFormula` تقوم تلقائيًا بتحليل السلسلة وتخزين شجرة الصيغة داخليًا.

### لماذا نستخدم EXPAND؟

`EXPAND` يلغي الحاجة إلى سحب مقبض التعبئة يدويًا. كما أنها تعمل مع المصفوفات الديناميكية، مما يعني أنه إذا تغيرت المصفوفة المصدر، يتم تحديث النطاق الممتد تلقائيًا. هذا مفيد جدًا عند إنشاء تقارير برمجيًا.

## الخطوة 4: إجبار الحساب – إظهار النتيجة

عند **وضع صيغة في الخلية** عبر الـ API، لا يقوم الـ workbook بإعادة حساب الصيغ تلقائيًا. عليك تشغيل عملية حساب واحدة حتى يتم **توسيع المصفوفة إلى صفوف** وتظهر القيم في الورقة.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

إذا تخطيت هذه الخطوة، سيفتح ملف `.xlsx` في Excel مع عرض الصيغة فقط دون القيم الممتدة حتى تضغط **F9**. باستدعاء `calculate()`، تضمن أن الـ workbook جاهز للاستخدام مباشرةً.

## الخطوة 5: حفظ الـ Workbook والتحقق من الناتج

أخيرًا، احفظ الـ workbook إلى ملف وربما اطبع القيم الممتدة إلى وحدة التحكم للتحقق.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

عند تشغيل البرنامج، يجب أن ترى مخرجات وحدة التحكم:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel يملأ الصفوف المتبقية بالأصفار لأن المصفوفة المصدر تحتوي فقط على ثلاثة عناصر. هذا هو السلوك الافتراضي لـ `EXPAND`. إذا كنت تفضل فراغات بدلاً من الأصفار، يمكنك تغليف المصفوفة بـ `IFERROR` أو استخدام حيل `CHOOSE`—المزيد في قسم “التحولات المتقدمة” أدناه.

## التحولات المتقدمة وحالات الحافة

### 1. توسيع مصفوفة أفقية إلى عدة أعمدة

إذا كنت بحاجة إلى **توسيع المصفوفة إلى صفوف** *وأعمدة*، فقط غيّر المعامل الثالث:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

الآن يمتد النطاق إلى كتلة 5 × 3، مع ملء الخلايا الناقصة بالأصفار.

### 2. استخدام نطاق مسمى كمصدر

بدلاً من `{1,2,3}` الصريحة، يمكنك الإشارة إلى نطاق مسمى قد يتغير أثناء التشغيل:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

تأكد من وجود `MySourceRange` (يمكنك إنشاؤه عبر `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")`).

### 3. التعامل مع بيانات غير رقمية

`EXPAND` يعمل مع النص أيضًا. على سبيل المثال:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

الصف الإضافي سيظهر كسلسلة فارغة، وليس كصفر.

### 4. تجنب ملء بالأصفار باستخدام `IFERROR`

إذا كنت تفضل رؤية فراغات بدلاً من الأصفار، غلف `EXPAND` بـ `IFERROR`:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

الآن الصفوف 4 و5 ستكون فارغة فعليًا.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا تحدث | الحل |
|---------|------------|------|
| **الصيغة لا تُعاد حسابها** | نسيان استدعاء `ws.getCells().calculate()` | احرص دائمًا على استدعاء `calculate()` بعد `putFormula`. |
| **قيمة صفرية حيث يُتوقع فراغ** | `EXPAND` يملأ بالأصفار افتراضيًا | استخدم `IFERROR(..., "")` أو غلفها بـ `CHOOSE`. |
| **عنوان خلية غير صحيح** | استخدام `"A0"` أو `"1A"` | عناوين Excel تبدأ من 1؛ Aspose تتوقع النمط `"A1"`. |
| **عدم توافق نسخة المكتبة** | استخدام نسخة قديمة من Aspose.Cells لا تدعم `EXPAND` | حدّث إلى أحدث نسخة (23.12 وقت كتابة هذا). |

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الجاهز للنسخ‑اللصق. احفظه باسم `ExpandArrayDemo.java`، ثم قم بتجميعه وتشغيله.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

تشغيل هذا البرنامج ينتج ملف Excel حيث **الخلية A1** تحتوي الآن على صيغة `EXPAND`، وتعرض الصفوف 1‑5 من العمود A القيم `1, 2, 3, 0, 0`. افتح الملف في Excel لتلاحظ النتيجة نفسها فورًا—بدون الحاجة لسحب يدوي.

## الخلاصة

لقد تعلمت الآن **كيفية توسيع المصفوفة في Excel** باستخدام Java، **كيفية استخدام EXPAND**، والخطوات الدقيقة **لوضع صيغة في الخلية** و**توسيع المصفوفة إلى صفوف** برمجيًا. باستخدام Aspose.Cells، تتجنب الحيل اليدوية وتترك الكود يقوم بالعمل الشاق. سواء كنت تبني محرك تقارير، أداة إدخال بيانات آلية، أو مولد جداول مخصص، فإن هذه التقنية ستوفر لك ساعات لا تحصى.

ما الخطوة التالية؟ جرّب استبدال المصفوفة الثابتة بنطاق ديناميكي يُستخرج من ورقة أخرى، جرب الامتدادات متعددة الأعمدة، أو اجمع بين `EXPAND` و `FILTER` لتحولات بيانات قوية. السماء هي الحد، والآن لديك أساس صلب لتبني عليه.

هل لديك أسئلة أو تريد مشاركة حالة استخدام مميزة؟ شاركنا

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2022023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}