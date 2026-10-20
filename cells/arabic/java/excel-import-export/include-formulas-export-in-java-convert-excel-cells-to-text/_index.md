---
category: general
date: 2026-07-03
description: تضمين تصدير الصيغ في جافا لتحويل خلايا إكسل إلى نص باستخدام Aspose.Cells.
  تعلّم كيفية طباعة نطاق إكسل والحصول على قيم الخلايا كسلسلة نصية بكفاءة.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: ar
og_description: تضمين تصدير الصيغ في جافا لتحويل خلايا إكسل إلى نص. دليل خطوة بخطوة
  يوضح كيفية طباعة نطاق إكسل واسترجاع قيم الخلايا كسلسلة نصية.
og_title: تضمين تصدير الصيغ في جافا – تحويل خلايا إكسل إلى نص
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: تضمين تصدير الصيغ في جافا – تحويل خلايا إكسل إلى نص
url: /ar/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تضمين تصدير الصيغ في Java – تحويل خلايا Excel إلى نص

هل احتجت يومًا إلى **تضمين تصدير الصيغ** عند استخراج البيانات من مصنف Excel؟ ربما تقوم ببناء خدمة تقارير يجب أن تحافظ على الصيغ الأصلية مع تقديم نص منسق. في هذه الحالة، أنت في المكان المناسب. يوضح لك هذا الدليل كيفية تحويل خلايا Excel إلى نص عادي —*متضمنًا* أي صيغ مدمجة — باستخدام Aspose.Cells for Java.

سنتطرق أيضًا إلى كيفية **طباعة نطاق Excel**، وتعديل **خيارات تصدير الجدول**، وأخيرًا **الحصول على سلسلة قيم الخلايا** التي يمكنك تسجيلها، أو إرسالها عبر API، أو تخزينها في قاعدة بيانات. بنهاية الدليل ستحصل على مقطع شفرة قابل للتنفيذ بالكامل وفهم قوي للسبب وراء كل استدعاء.

## ما ستحصل عليه

- برنامج Java كامل جاهز للنسخ واللصق يقرأ ملف `.xlsx`، يحدد نطاقًا، ويصدره كسلسلة منسقة.
- فهم لفئة `ExportTableOptions` ولماذا يؤثر تبديل `setExportAsString` و `setIncludeFormula`.
- نصائح للتعامل مع أوراق عمل كبيرة، ومعالجة أنواع البيانات المختلفة، وتخصيص تنسيق الإخراج.
- قائمة سريعة لأخطاء شائعة (مثل الخلايا المدمجة، الصفوف المخفية، وتنسيقات الأرقام حسب اللغة).

### المتطلبات المسبقة

- Java 17 أو أحدث (الكود يُترجم مع الإصدارات الأقدم لكننا سنستخدم أحدث نسخة LTS).
- Aspose.Cells for Java 23.10 (أو أي إصدار حديث) — يمكنك الحصول عليه من Maven Central.
- ملف `input.xlsx` تجريبي موجود في مجلد تتحكم فيه (المسار مُحدد صراحة في المثال للتوضيح).

إذا كان لديك هذه المتطلبات، لنبدأ.

## الخطوة 1: إعداد المشروع وإضافة الاعتمادات

أولًا، أنشئ مشروع Maven (أو Gradle إذا تفضل). أضف اعتماد Aspose.Cells إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **نصيحة احترافية:** إذا كنت تستخدم بروكسي مؤسسي، تأكد من إمكانية الوصول إلى المستودع؛ وإلا سيفشل البناء برسالة الخطأ “Could not resolve dependencies”.

بعد أن ينتهي Maven من التحميل، ستكون جاهزًا لكتابة بعض شفرة Java.

## الخطوة 2: تحميل المصنف والحصول على ورقة العمل المطلوبة

السطر الأول من مثال الشفرة يوضح كيفية فتح مصنف موجود:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي إلى ملفك. مُنشئ `Workbook` يكتشف تنسيق الملف تلقائيًا (XLS, XLSX, CSV، إلخ)، لذا لا تحتاج إلى تحديده.

Next, we fetch the first sheet:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

لماذا الورقة الأولى؟ في العديد من القوالب تكون البيانات في التبويب الأول، لكن يمكنك تمرير أي فهرس أو حتى استخدام `get("SheetName")` إذا كنت تفضل طريقة بالاسم.

## الخطوة 3: تحديد النطاق الذي تريد تصديره

الآن يأتي جوهر عملية **convert excel cells text**. تخبر Aspose.Cells أي خلايا سحبها بإنشاء كائن `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

السلسلة `"A1:C3"` هي عنوان نمط A1 الكلاسيكي. يمكن أيضًا بناؤها برمجيًا:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

تلك المرونة تساعد عندما يكون حجم النطاق ديناميكيًا — مثلاً، تقرأ آخر صف مستخدم باستخدام `ws.getCells().getMaxDataRow()`.

## الخطوة 4: تكوين خيارات تصدير الجدول لتضمين الصيغ

هنا تكمن سحر **include formulas export**. بشكل افتراضي، تُعيد Aspose.Cells القيم *المعروضة*. إذا كانت الخلية تحتوي على `=SUM(A1:A3)`، ستحصل على الرقم المحسوب، وليس نص الصيغة. لتغيير ذلك، قم بإعداد `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

لماذا كلا العلامتين؟ `setExportAsString(true)` يخبر الـ API بدمج الخلايا باستخدام الفاصل الافتراضي (علامة تبويب للأعمدة، سطر جديد للصفوف). `setIncludeFormula(true)` يغيّر مصدر القيمة من “القيمة المعروضة” إلى “الصيغة الخام”. إذا كنت تريد القيم فقط، اتركه `false`.

### تعديلات اختيارية

- `eto.setExportHiddenRows(true);` – تضمين الصفوف المخفية في Excel.
- `eto.setExportHiddenColumns(true);` – نفس الشيء للأعمدة.
- `eto.setExportAsHTML(true);` – الحصول على HTML بدلاً من النص العادي.

لا تتردد في التجربة؛ ففئة الخيارات هي ملعب **export table options**.

## الخطوة 5: استرجاع النطاق كسلسلة منسقة

Now we pull the data:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

النص `txt` المُرجع يبدو كالتالي (بافتراض أن A1:C3 يحتوي على مزيج من القيم والصيغ):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

لاحظ علامة التبويب (`\t`) التي تفصل الأعمدة وسطر جديد (`\n`) الذي يفصل الصفوف. يمكنك تقسيم السلسلة لاحقًا إذا كنت تحتاج إلى مصفوفة ثنائية الأبعاد:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## الخطوة 6: طباعة النتيجة – “Print Excel Range” ببساطة

Finally, we dump the string to the console:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

تشغيل البرنامج يطبع النتيجة الدقيقة المعروضة أعلاه. من هنا يمكنك كتابة السلسلة إلى ملف سجل، أو إرسالها عبر HTTP، أو تخزينها في مستند NoSQL.

## مثال كامل وجاهز للتنفيذ

بجمع كل ذلك معًا، إليك البرنامج الكامل. انسخه، الصقه، واضغط **Run** — بدون أي استيرادات مفقودة.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### النتيجة المتوقعة (عينة)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

إذا كان المصنف يحتوي على أرقام مُنسقة كتواريخ، فستظهر بالتنسيق الخاص بالمنطقة (مثال: `2026‑07‑03`). لفرض تواريخ ISO، يمكنك تعديل `ExportTableOptions` باستخدام `NumberFormat` مخصص.

## معالجة الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان النطاق يحتوي على خلايا مدمجة؟

تُعامل الخلايا المدمجة كقيمة الخلية العليا‑اليسرى. بقية المنطقة المدمجة ستظهر كسلاسل فارغة. إذا كنت تحتاج إلى عنوان المنطقة المدمجة، استعلم `Cell.getMergedRange()` قبل التصدير.

### هل يمكنني تصدير ورقة ضخمة (مئات الآلاف من الصفوف)؟

نعم، لكن احذر من استهلاك الذاكرة. استخدم `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` للسماح لـ Aspose.Cells ببث البيانات إلى القرص. أيضًا، فكر في التصدير على دفعات (مثلاً 10 000 صف في كل مرة) للحفاظ على حجم السلسلة قابلًا للإدارة.

### كيف يمكنني تغيير فاصل الأعمدة؟

`ExportTableOptions` يتيح `setSeparator(char separator)`. للحصول على مخرجات بنمط CSV، اضبطه إلى `','`:

```java
eto.setSeparator(',');
```

### هل تحترم الصيغ المراجع الخارجية؟

إذا أشارت صيغة إلى مصنف آخر، سيحافظ Aspose.Cells على نص المرجع (`='[Other.xlsx]Sheet1'!A1`). لن يقوم بتقييم القيمة الخارجية ما لم تقم بتحميل ذلك المصنف أيضًا.

## نصائح احترافية لكود جاهز للإنتاج

- **Cache the workbook** إذا كنت تقرأ الـ

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [كيفية تحويل Excel إلى PDF في Java باستخدام Aspose.Cells: دليل خطوة بخطوة](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [تصدير مصنف Excel كصورة باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}