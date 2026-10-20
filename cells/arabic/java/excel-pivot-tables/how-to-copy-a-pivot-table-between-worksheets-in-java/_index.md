---
category: general
date: 2026-10-16
description: كيفية نسخ جدول محوري في جافا باستخدام Aspose.Cells – تعلم كيفية نسخ النطاق
  إلى ورقة أخرى ونسخ النطاق بين أوراق العمل بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: ar
lastmod: 2026-10-16
og_description: كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells. يوضح لك هذا الدليل
  كيفية نسخ نطاق إلى ورقة أخرى وكيفية نسخ النطاق بين أوراق العمل مع الشيفرة الكاملة.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: كيفية نسخ جدول محوري بين أوراق العمل في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: كيفية نسخ جدول محوري بين أوراق العمل في جافا
url: /ar/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري بين أوراق العمل في Java

إذا كنت بحاجة إلى **كيفية نسخ جدول محوري** من ورقة إلى أخرى في نفس المصنف، فإن هذا الدليل يقدم حلاً كاملاً وجاهزًا للتنفيذ. سترى كيفية نسخ النطاق المصدر الذي يحتوي على الجدول المحوري، والحفاظ على وظيفته، والتحقق من النتيجة — كل ذلك باستخدام Aspose.Cells for Java.

نسخ جدول محوري هو مهمة شائعة عندما تقوم بإنشاء تقارير برمجياً، والقيام بذلك بشكل صحيح يمنع فقدان ذاكرة التخزين المؤقت للجدول المحوري أو كسر الصيغ. بنهاية هذا الشرح ستتمكن من **نسخ نطاق إلى ورقة أخرى** و**نسخ نطاق بين أوراق العمل** دون أي خطوات يدوية.

## ما ستتعلمه

* تحميل ملف Excel موجود يحتوي على جدول محوري.
* تحديد النطاق المصدر الذي يحتوي على الجدول المحوري.
* تحديد نطاق الوجهة في ورقة عمل مختلفة.
* استخدام `CopyOptions` للحفاظ على الجدول المحوري دون تغيير.
* التحقق من أن الجدول المحوري المنسوخ يعمل كما هو متوقع.

**المتطلبات المسبقة**

* Java 17 أو أحدث.
* Aspose.Cells for Java (الإصدار 23.12 أو أحدث).  
* ملف Excel (`input.xlsx`) يحتوي على جدول محوري في الورقة الأولى.

---

## كيفية نسخ جدول محوري باستخدام Aspose.Cells

جوهر العملية هو عملية من أربع خطوات: تحميل المصنف، تحديد النطاق المصدر، تعيين نطاق الوجهة، وإجراء النسخ. يتم شرح كل خطوة بالتفصيل أدناه.

### الخطوة 1: تحميل المصنف

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*لماذا هذه الخطوة؟*  
تحميل المصنف يجلب الملف بالكامل إلى الذاكرة، مما يمنحك إمكانية الوصول إلى أوراق العمل، الخلايا، وذاكرة التخزين المؤقت للجدول المحوري. Aspose.Cells يقرأ تنسيق الملف تلقائيًا، لذا لا تحتاج للقلق بشأن `.xls` مقابل `.xlsx`.

### الخطوة 2: تحديد النطاق المصدر الذي يحتوي على الجدول المحوري

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*لماذا هذه الخطوة؟*  
يتم تخزين الجدول المحوري في كتلة خلايا تُشير أيضًا إلى ذاكرة مخبأة مخفية. باختيار النطاق الدقيق (`A1:G20` في هذا المثال)، تضمن بقاء الذاكرة المرتبطة عندما يتم نسخ النطاق.

### الخطوة 3: تحديد نطاق الوجهة في ورقة أخرى

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*لماذا هذه الخطوة؟*  
اختيار وجهة في ورقة عمل مختلفة يتيح لك **نسخ نطاق إلى ورقة أخرى**. الخلية العلوية اليسرى (`A1`) هي نقطة بدء شائعة، لكن يمكنك وضعه في أي مكان بتغيير العنوان.

### الخطوة 4: نسخ النطاق المصدر مع الحفاظ على الجدول المحوري

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*لماذا هذه الخطوة؟*  
`CopyOptions` يتحكم في ما يتم نقله. استخدام `PasteType.PASTE_ALL` يضمن أن الجدول المحوري، تنسيقه، والصيغ الأساسية يتم تكرارها. بدون هذه الخيارات، قد يتم نسخ القيم الخام فقط، مما يكسر وظيفة الجدول المحوري.

### الخطوة 5: حفظ المصنف والتحقق من النتيجة

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

افتح `output.xlsx` في Excel وتأكد من أن:

* الورقة الثانية تحتوي على جدول محوري يعمل بالكامل ومطابق للأصل.
* تحديث الجدول المحوري يحدّث البيانات، مما يثبت أن الذاكرة لا تزال سليمة.

---

## نسخ نطاق إلى ورقة أخرى باستخدام Java

إذا كان هدفك ببساطة هو **نسخ نطاق إلى ورقة أخرى** دون جدول محوري، فإن نفس الكود يعمل مع نطاق خلايا عادي. التغيير الوحيد هو عنوان المصدر. يبقى تكوين `CopyOptions` كما هو، مما يضمن حفظ الصيغ والتنسيقات.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

هذا المقتطف يوضح مرونة الـ API لكل من السيناريوهات مع وبدون جدول محوري.

---

## نسخ نطاق بين أوراق العمل دون فقدان الصيغ

عند **نسخ نطاق بين أوراق العمل**، قد تتعطل الصيغ التي تشير إلى أوراق أخرى إذا تغيرت المراجع النسبية. لتجنب ذلك:

1. استخدم `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` إذا كنت تحتاج فقط إلى الصيغ.
2. احتفظ بورقة الوجهة في نفس المصنف بحيث تبقى المراجع الداخلية صالحة.
3. بعد النسخ، استدعِ `workbook.calculateFormula();` لإجبار إعادة حساب.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

هذه الخطوات الإضافية تضمن أن النطاق المنسوخ يتصرف تمامًا كما الأصل، حتى عندما يمتد عبر عدة أوراق عمل.

---

## نصائح احترافية ومشكلات شائعة

| Situation | Tip |
|-----------|-----|
| **ذاكرة التخزين المؤقت للجدول المحوري لا يتم تحديثها** | بعد النسخ، استدعِ `destSheet.getPivotTables().get(0).refresh();` لتحديث الذاكرة. |
| **النسخ إلى مصنف مختلف** | استخدم `Workbook destWorkbook = new Workbook();` ثم `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. تذكر نسخ ذاكرة التخزين المؤقت للجدول المحوري بشكل منفصل إذا لزم الأمر. |
| **جداول محورية كبيرة** | قم بزيادة حجم الذاكرة المخصصة للـ Java (`-Xmx2g`) لتجنب حدوث `OutOfMemoryError` أثناء النسخ. |
| **الحفاظ على الأنماط** | اضبط `copyOptions.setPasteType(PasteType.PASTE_ALL)`؛ وإلا سيتم نسخ القيم فقط. |

---

## النتيجة المتوقعة

تشغيل البرنامج الكامل ينتج `output.xlsx`. عند فتحه في Excel:

* **Sheet2!A1:G20** يعرض نفس الجدول المحوري كما في **Sheet1!A1:G20**.
* قائمة حقول الجدول المحوري، تسميات الصفوف/الأعمدة، وقيم البيانات تتطابق مع المصدر.
* تحديث الجدول المحوري يحدّث الأرقام، مؤكدًا أن الذاكرة تعمل.

ستطبع وحدة التحكم:

```
Pivot table copied successfully.
```

---

## الخلاصة

في هذا الشرح تعلمت **كيفية نسخ جدول محوري** من ورقة عمل إلى أخرى باستخدام Aspose.Cells for Java. من خلال تحميل المصنف، اختيار النطاق المصدر الصحيح، تحديد الوجهة، وتكوين `CopyOptions`، يمكنك بثقة **نسخ نطاق إلى ورقة أخرى** و**نسخ نطاق بين أوراق العمل** مع الحفاظ على جميع وظائف الجدول المحوري.  

بعد ذلك، قد ترغب في استكشاف:

* تصدير الجدول المحوري المنسوخ إلى PDF أو HTML.
* أتمتة تحديثات الجداول المحورية عبر عدة مصنفات.
* استخدام `CopyOptions` لنسخ عناصر محددة فقط (مثل القيم، التنسيقات).

لا تتردد في تجربة عناوين نطاق مختلفة، هياكل المصنفات، أو حتى نسخ عبر المصنفات. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة للكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية نسخ النطاق في Java – نسخ جدول محوري باستخدام Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [كيفية نسخ جدول محوري في Java – دليل Aspose.Cells الكامل](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [نسخ جدول محوري Excel – دليل خطوة بخطوة باستخدام Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}