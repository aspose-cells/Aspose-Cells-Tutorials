---
category: general
date: 2026-06-18
description: كيفية استخدام SmartMarkerProcessor لتسمية أوراق العمل الديناميكية في
  مشاريع Excel – دليل كامل خطوة بخطوة مع كود Java كامل.
draft: false
keywords:
- how to use smartmarkerprocessor
- dynamic worksheet naming excel
language: ar
og_description: تعلم كيفية استخدام SmartMarkerProcessor لتسمية أوراق العمل ديناميكياً
  في ملفات Excel مع مثال عملي بلغة Java.
og_title: كيفية استخدام SmartMarkerProcessor لتسمية الأوراق ديناميكياً
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to use SmartMarkerProcessor for dynamic worksheet naming Excel
    projects – a complete, step‑by‑step guide with full Java code.
  headline: How to Use SmartMarkerProcessor for Dynamic Sheet Naming
  type: TechArticle
- description: How to use SmartMarkerProcessor for dynamic worksheet naming Excel
    projects – a complete, step‑by‑step guide with full Java code.
  name: How to Use SmartMarkerProcessor for Dynamic Sheet Naming
  steps:
  - name: Expected Output
    text: 'When you open `detailSheets.xlsx` you should see:'
  - name: How does the processor know which row maps to which sheet?
    text: The library internally uses the order of the collection. The first element
      becomes `Detail_1`, the second `Detail_2`, and so on. If you need a custom order,
      sort the collection before calling `process`.
  - name: What if my sheet name needs to include a date?
    text: 'Just embed another placeholder and make sure the data source provides it:'
  - name: Can I prevent certain columns from being copied to the new sheets?
    text: Yes—use the `SmartMarkerOptions` object to specify `setIgnoreUnusedColumns(true)`.
      That way only markers you’ve placed will be evaluated.
  - name: Is there a performance impact with very large data sets?
    text: Processing is O(n) where *n* is the number of rows. For tens of thousands
      of rows, consider streaming the data or batching the workbook saves to avoid
      excessive memory consumption.
  type: HowTo
tags:
- Excel
- SmartMarkerProcessor
- Java
- Automation
title: كيفية استخدام SmartMarkerProcessor لتسمية الأوراق بشكل ديناميكي
url: /ar/java/worksheet-management/how-to-use-smartmarkerprocessor-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام SmartMarkerProcessor لتسمية الأوراق ديناميكياً

هل تساءلت يوماً **عن كيفية استخدام SmartMarkerProcessor** عندما تحتاج إلى استخراج مجموعة من أوراق التفاصيل من قالب؟ لست وحدك—المطورون يواجهون صعوبة مستمرة في الحفاظ على أسماء الأوراق مرتبة بينما البيانات تنتج عشرات الصفوف. الخبر السار؟ ببضع أسطر من Java يمكنك السماح لـ SmartMarkerProcessor بالقيام بالعمل الشاق وإعطاء كل ورقة عمل تم إنشاؤها اسمًا ذا معنى تلقائيًا.

في هذا الدرس سنستعرض سيناريو واقعي: أخذ ملف Excel قالب، إمداده بمصدر بيانات، والحصول في النهاية على ملف تكون فيه كل ورقة تفاصيل مسماة **بنمط تسمية أوراق Excel الديناميكي** (مثل `Detail_1`, `Detail_2`, …). بنهاية الدرس ستعرف بالضبط ما يفعله كل سطر، لماذا نمط التسمية مهم، وكيفية تعديل الكود لحالات الحافة مثل الأحرف الخاصة أو مواقع المجلدات المخصصة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* Java 8+ مثبتة (الكود يستخدم صsyntax Java القياسي).
* Aspose.Cells for Java (أو أي مكتبة توفر `SmartMarkerProcessor`).
* ملف Excel قالب (`template.xlsx`) يحتوي على Smart Markers في الأماكن التي تريد إدخال البيانات فيها.
* POJO بسيط أو `Map<String, Object>` يعمل كمصدر للبيانات.

هل لديك كل ذلك؟ عظيم—لنبدأ.

## الخطوة 1: تحميل ملف الـ Workbook القالب

أول شيء تحتاجه هو كائن `Workbook` يشير إلى ملف القالب الخاص بك. فكر فيه كفتح لوحة جديدة تحتوي بالفعل على العناصر النائبة.

```java
// Step 1: Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");
```

*لماذا هذا مهم*: تحميل الـ workbook مرة واحدة يقلل من استهلاك الذاكرة. إذا قمت بإنشاء workbook جديد لكل صف، ستنفد مساحة الـ heap بسرعة.

> **نصيحة احترافية**: استخدم مسارًا مطلقًا أو موردًا من classpath (`getClass().getResourceAsStream`) إذا كان تطبيقك يعمل من داخل JAR.

## الخطوة 2: إنشاء SmartMarkerProcessor

الآن نقوم بإنشاء المعالج الذي سيفحص الـ workbook بحثًا عن Smart Markers ويستبدلها بالبيانات.

```java
// Step 2: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

`SmartMarkerProcessor` هو المحرك وراء السحر. فهو يعرف كيف يقرأ العلامات مثل `&=Customers.Name` ويحولها إلى قيم خلايا فعلية.

## الخطوة 3: تعريف نمط تسمية لأوراق التفاصيل

هنا يأتي دور **تسمية أوراق Excel الديناميكية**. تخبر المعالج كيف يجب أن يكون اسم الورقة الجديدة، باستخدام `{0}` كعنصر نائبي لمؤشر الصف (أو أي متغير آخر تختاره).

```java
// Step 3: Define a naming pattern for the detail sheets (row index will replace {0})
processor.setDetailSheetNewName("Detail_{0}");
```

عندما ينشئ المعالج ورقة جديدة لكل صف من البيانات، سيستبدل `{0}` بـ `1`, `2`, `3`, … فينتج `Detail_1`, `Detail_2`, إلخ. هذا يحافظ على تنظيم الـ workbook ويسهل المعالجة اللاحقة (مثل ماكرو VBA).

> **ماذا لو** احتجت اسمًا أكثر وصفًا، مثل `Invoice_2024_01`؟ فقط غيّر النمط إلى: `"Invoice_{0}_{1}"` وقدم عناصر نائبة إضافية في مصدر البيانات.

## الخطوة 4: معالجة Smart Markers بمصدر البيانات الخاص بك

الآن العملية الأساسية—إدخال البيانات في القالب. طريقة `process` تأخذ ثلاثة معاملات: مجموعة الخلايا التي سيتم فحصها، مصدر البيانات، وخيارياً كائن خيارات مخصص (سنستخدم أبسط نسخة).

```java
// Step 4: Process smart markers in the first worksheet using the data source
processor.process(workbook.getWorksheets().get(0).getCells(), dataSource);
```

*لماذا نستهدف الورقة الأولى*: في معظم القوالب تكون الورقة الرئيسية في الفهرس 0. إذا كان القالب يحتوي على علامات في ورقة أخرى، غير الفهرس وفقًا لذلك.

يمكن أن يكون `dataSource` أحدًا مما يلي:

* `List<Map<String, Object>>` حيث يمثل كل خريطة صفًا.
* مجموعة من الـ POJOs (كائنات Java العادية) ذات getters.
* أي كائن يمكن للمكتبة عكسه (reflect).

سيقوم المعالج بالتكرار على المجموعة، استنساخ الورقة الرئيسية لكل عنصر، استبدال العلامات، وإعادة تسمية النسخة وفق النمط الذي حددته مسبقًا.

## الخطوة 5: حفظ الـ Workbook الناتج

أخيرًا، اكتب الـ workbook إلى القرص. الملف المُولد سيحتوي على ورقة لكل صف من البيانات، كل واحدة مسماة بشكل صحيح.

```java
// Step 5: Save the resulting workbook with the generated detail sheets
workbook.save("YOUR_DIRECTORY/detailSheets.xlsx");
```

يمكنك الآن فتح `detailSheets.xlsx` في Excel ورؤية `Detail_1`, `Detail_2`, … كل واحدة مملوءة بالسجل المقابل.

> **حالة حافة**: إذا كان مصدر البيانات يحتوي على أكثر من 255 ورقة، سيظهر خطأ في Excel. فكر في تقسيم الناتج إلى عدة workbooks أو استخدام استراتيجية ترقيم الصفحات.

## مثال كامل يعمل

نجمع كل ما سبق في برنامج بسيط من البداية إلى النهاية يمكنك نسخه ولصقه في IDE الخاص بك:

```java
import com.aspose.cells.*;

import java.util.*;

public class SmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load template
        Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // 2️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // 3️⃣ Set naming pattern
        processor.setDetailSheetNewName("Detail_{0}");

        // 4️⃣ Build a simple data source (List of Maps)
        List<Map<String, Object>> dataSource = new ArrayList<>();

        Map<String, Object> row1 = new HashMap<>();
        row1.put("Name", "Alice");
        row1.put("Amount", 1200);
        dataSource.add(row1);

        Map<String, Object> row2 = new HashMap<>();
        row2.put("Name", "Bob");
        row2.put("Amount", 850);
        dataSource.add(row2);

        // 5️⃣ Process the first worksheet
        processor.process(workbook.getWorksheets().get(0).getCells(), dataSource);

        // 6️⃣ Save output
        workbook.save("YOUR_DIRECTORY/detailSheets.xlsx");
        System.out.println("Workbook generated with dynamic sheet names!");
    }
}
```

### النتيجة المتوقعة

عند فتح `detailSheets.xlsx` يجب أن ترى:

| اسم الورقة | الخلية A1 (مثال) |
|------------|-------------------|
| Detail_1   | Alice             |
| Detail_2   | Bob               |

كل ورقة تحتوي على البيانات من الخريطة المقابلة، وأسماء الأوراق تتبع النمط الذي عرّفناه.

## أسئلة شائعة ونصائح

### كيف يعرف المعالج أي صف يطابق أي ورقة؟

المكتبة تستخدم داخليًا ترتيب المجموعة. العنصر الأول يصبح `Detail_1`، الثاني `Detail_2`، وهكذا. إذا احتجت ترتيبًا مخصصًا، رتب المجموعة قبل استدعاء `process`.

### ماذا لو كان اسم الورقة يحتاج إلى تضمين تاريخ؟

فقط أضف عنصرًا نائبيًا آخر وتأكد من أن مصدر البيانات يقدمه:

```java
processor.setDetailSheetNewName("Report_{0}_{1}");
```

حيث يمكن أن يكون `{0}` مؤشر الصف و`{1}` سلسلة تاريخ منسقة تضيفها لكل خريطة (`"Date", "2024-01-31"`).

### هل يمكن منع نسخ أعمدة معينة إلى الأوراق الجديدة؟

نعم—استخدم كائن `SmartMarkerOptions` لتحديد `setIgnoreUnusedColumns(true)`. بهذه الطريقة سيتم تقييم العلامات التي وضعتها فقط.

### هل هناك تأثير على الأداء مع مجموعات بيانات ضخمة؟

المعالجة هي O(n) حيث *n* هو عدد الصفوف. بالنسبة لعشرات الآلاف من الصفوف، فكر في تدفق البيانات (streaming) أو حفظ الـ workbook على دفعات لتجنب استهلاك الذاكرة الزائد.

## الخلاصة

أصبحت الآن تمتلك فهماً قوياً **لكيفية استخدام SmartMarkerProcessor** لتحقيق **تسمية أوراق Excel الديناميكية**. عبر تحميل قالب، ضبط نمط التسمية، إمداد مصدر البيانات، وحفظ النتيجة، يمكنك توليد أوراق تفاصيل منظمة ومسمّاة بشكل جيد في بضع أسطر فقط.

ما الخطوة التالية؟ جرّب إضافة مخططات، تنسيقات شرطية، أو حتى حماية الأوراق المُولدة. وإذا كنت تتعامل مع مصادر CSV، ببساطة حوّلها إلى قائمة من الخرائط قبل تمريرها إلى المعالج.

لا تتردد في التجربة—غيّر نمط التسمية، العب بهياكل بيانات مختلفة، أو دمج هذا المقتطف في خط أنابيب تقارير أكبر. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [كيفية استخدام Aspose.Cells لأتمتة مقاطع Excel Slicer في Java](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)
- [كيفية استخدام Aspose لإدارة روابط Excel في Java](/cells/english/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [كيفية تحويل Excel إلى PDF في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}