---
category: general
date: 2026-10-07
description: تعلم كيفية تكرار جداول المحور في Excel باستخدام Java و Aspose.Cells.
  قم بنسخ جدول محوري عن طريق نسخ نطاقه بين المصنفات بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: ar
lastmod: 2026-10-07
og_description: كيفية تكرار جداول Pivot في Excel باستخدام Java و Aspose.Cells. اتبع
  هذا الدليل لنسخ جدول Pivot عن طريق نسخ نطاقه بين المصنفات.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: كيفية تكرار جداول Pivot في Excel باستخدام Java – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: كيفية تكرار الجداول المحورية في إكسل باستخدام جافا – دليل خطوة بخطوة
url: /ar/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار جداول Pivot في Excel باستخدام Java – دليل خطوة بخطوة

إذا كنت بحاجة إلى **كيفية تكرار Pivot** في مصنف Excel، فإن هذا الدليل يوضح لك حلاً كاملاً وجاهزًا للتنفيذ. باستخدام Aspose.Cells for Java يمكنك نسخ جدول Pivot مع بياناته المصدر عن طريق نسخ النطاق الأساسي، ثم حفظ النتيجة كمصنف جديد.

غالبًا ما يبدو تكرار جدول Pivot أمرًا صعبًا لأن ذاكرة التخزين المؤقت للـ Pivot مخفية داخل الورقة. عن طريق نسخ النطاق الكامل الذي يحتوي على الـ Pivot، يقوم Aspose.Cells بإعادة إنشاء الذاكرة المؤقتة تلقائيًا في المصنف الهدف، وبالتالي تحصل على نسخة تعمل بالكامل دون الحاجة إلى تعديل ملفات XML يدويًا.

في هذا الدليل ستقوم بـ:

* تحميل مصنف مصدر يحتوي على جدول Pivot.  
* تحديد النطاق الدقيق الذي يحتوي على الـ Pivot.  
* نسخ ذلك النطاق إلى مصنف جديد، مع الحفاظ على تعريف الـ Pivot.  
* حفظ الملف الجديد والتحقق من عمل الـ Pivot.

تعمل الخطوات مع أي إصدار من Excel يدعمه Aspose.Cells (2007‑2024) وتحتاج فقط إلى بضع أسطر من كود Java.

## المتطلبات المسبقة

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| **Java 8 أو أحدث** | Aspose.Cells مبني لـ Java 8+. |
| **Aspose.Cells for Java** (أحدث إصدار) | يوفر واجهات `Workbook` و `Range` و `CopyRange` المستخدمة في المثال. |
| **مصنف المصدر** يحتوي على جدول Pivot (مثلًا `Source.xlsx`) | الـ Pivot الذي تريد تكراره. |
| **صلاحية كتابة** إلى الدليل الهدف | ضرورية لحفظ `CopyWithPivot.xlsx`. |

أضف تبعية Aspose.Cells Maven إلى ملف `pom.xml` الخاص بك (أو قم بتحميل ملف JAR يدويًا):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## كيفية تكرار جداول Pivot – التنفيذ الكامل

فيما يلي برنامج Java مستقل يوضح **كيفية تكرار Pivot** عن طريق نسخ النطاق الذي يحتوي على الـ Pivot. يتضمن الكود معالجة الأخطاء، تعليقات، وخطوة التحقق.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### شرح كل خطوة

| الخطوة | ما يفعله الكود | لماذا يهم **نسخ جدول Pivot** |
|------|-------------------|----------------------------------------|
| **1️⃣ تحميل مصنف المصدر** | `new Workbook(srcPath)` يقرأ `Source.xlsx`. | ملف المصدر هو المكان الوحيد الذي يوجد فيه الـ Pivot الأصلي. |
| **2️⃣ تحديد النطاق** | `createRange("A1:G20")` ينشئ كائن `Range` يغطي الـ Pivot وبياناته. | يتم تخزين جدول Pivot مع ذاكرة التخزين المؤقت؛ نسخ النطاق بالكامل يضمن نقل الذاكرة أيضًا. |
| **3️⃣ نسخ النطاق** | `copyRange(srcRange, "A1")` يكتب النطاق في الورقة الهدف. | هذا هو جوهر **نسخ النطاق بين المصنفات** – الواجهة البرمجية تتعامل مع الكائنات المخفية تلقائيًا. |
| **4️⃣ تحديث الـ Pivot** | `pivotTable.refresh()` يجبر الـ Pivot على إعادة الحساب. | يضمن أن الـ Pivot المنسوخ يعرض نفس القيم كما الأصلي، خاصة بعد التعديلات. |
| **5️⃣ حفظ المصنف** | `destWb.save(destPath)` يكتب الملف على القرص. | ينتج النتيجة النهائية لـ **نسخ نطاق Excel** التي يمكنك فتحها في Excel. |

#### النتيجة المتوقعة

بعد تشغيل البرنامج، افتح `CopyWithPivot.xlsx`. ستلاحظ ورقة عمل تبدو مطابقة تمامًا للورقة المصدر، ويعمل جدول الـ Pivot بنفس طريقة الأصلي – يمكنك توسيع الصفوف، تصفية الحقول، وتحديث البيانات دون أي أخطاء.

## الاختلافات الشائعة وحالات الحافة

### 1️⃣ نسخ Pivot يمتد عبر عدة أوراق

إذا كانت بيانات مصدر الـ Pivot موجودة في ورقة مختلفة عن ورقة الـ Pivot نفسها، قم بتضمين كلتا الورقتين في عملية النسخ. أبسط طريقة هي نسخ الورقة المصدر بالكامل أولاً، ثم نسخ ورقة الـ Pivot:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ التعامل مع النطاقات المسماة

يحافظ Aspose.Cells على النطاقات المسماة عند نسخ نطاق. ومع ذلك، إذا كان المصنف الهدف يحتوي بالفعل على اسم بنفس المعرف، سيتم إلقاء استثناء `CellsException`. حل هذه المشكلة يتم بإعادة تسمية الاسم المتعارض قبل النسخ:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ المصنفات الكبيرة والأداء

نسخ نطاقات ضخمة (مئات الآلاف من الصفوف) قد يكون مستهلكًا للذاكرة. فعّل **تحسين الذاكرة**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ الحفاظ على الصيغ دون تغيير

إذا كان النطاق المصدر يحتوي على صيغ تشير إلى خلايا خارج المنطقة المنسوخة، فإن تلك الإشارات ستصبح مكسورة بعد النسخ. لتجنب ذلك، وسّع النطاق ليشمل جميع الخلايا التابعة، أو استخدم `copyRange` مع علم `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## نصائح احترافية لنسخ نطاق موثوق بين المصنفات **copy range between workbooks**

* **استخدم دائمًا العناوين المطلقة** (`$A$1:$G$20`) عندما قد يتم إعادة تسمية ورقة المصدر.  
* **قم بالتحديث بعد النسخ** – رغم أن Aspose.Cells يعيد بناء الذاكرة المؤقتة، فإن استدعاء `refresh()` يزيل التحذيرات العرضية للذاكرة المؤقتة القديمة في Excel.  
* **تحقق من الـ Pivot**: بعد الحفظ، افتح الملف برمجيًا واستدعِ `pivotTable.validate()` للتأكد من عدم وجود مراجع مكسورة.  
* **توافق الإصدارات**: يعمل الكود مع ملفات Excel 2007‑2024 (`.xlsx`, `.xlsm`). بالنسبة للملفات القديمة `.xls`، اضبط `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## القائمة الكاملة للمصدر (جاهزة للترجمة)



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية نسخ جدول Pivot في Java – دليل Aspose.Cells الكامل](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [كيفية إنشاء جداول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية تحديث مصدر جدول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}