---
category: general
date: 2026-10-23
description: تعلم كيفية تكرار ورقة Excel في Java مع الحفاظ على الجداول المحورية. يوضح
  هذا الدليل أيضًا كيفية نسخ الجداول المحورية، ونسخ نطاقات Excel، ونسخ ورقة تحتوي
  على بيانات محورية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: ar
lastmod: 2026-10-23
og_description: قم بنسخ ورقة Excel في Java مع الحفاظ على جداول المحور. اتبع هذا الدرس
  الكامل لنسخ جداول المحور، ونسخ نطاقات Excel، ونسخ ورقة تحتوي على بيانات المحور.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: نسخ ورقة إكسل تحتوي على جداول محورية في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: كيفية استنساخ ورقة إكسل والحفاظ على جداول المحور سليمة في جافا
url: /ar/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار ورقة Excel والحفاظ على جداول Pivot دون تغيير في Java

إذا كنت بحاجة إلى **duplicate Excel sheet** مع الحفاظ على كل جدول Pivot فعال، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. سترى حلاً مختصرًا ينسخ ورقة، ينسخ نطاقًا محددًا، وحتى ينسخ جدول Pivot إلى مصنف آخر—كل ذلك باستخدام Java النقي مع Aspose.Cells.

تكرار ورقة Excel هو مهمة شائعة عندما تقوم بإنشاء تقارير شهرية من قالب أو عندما تحتاج إلى نسخة تجريبية للاختبار. يعمل الكود أدناه مع Aspose.Cells 25.11 أو أحدث، الذي قدم خيار `setCopyPivotTable(true)`.

## ما ستحتاجه

- Java 17 (أو أي JDK حديث) مثبت
- Aspose.Cells for Java 25.11 أو أحدث في مشروعك (إحداثيات Maven `com.aspose:aspose-cells:25.11`)
- مصنف مصدر (`SourceWithPivot.xlsx`) يحتوي بالفعل على جدول Pivot
- بيئة تطوير متكاملة أو أداة بناء من اختيارك (IntelliJ IDEA، Eclipse، Maven، Gradle، إلخ)

## الخطوة 1: تحميل المصنف المصدر الذي يحتوي على جدول Pivot

العملية الأولى هي فتح المصنف الذي يحتوي على الـ Pivot الذي تريد الحفاظ عليه.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **لماذا هذه الخطوة مهمة:** تحميل المصنف المصدر يمنحك الوصول إلى كائنات الورقة، الخلايا، وجداول Pivot المدمجة. بدون ذلك لا يمكنك الإشارة إلى بيانات الـ Pivot التي تخطط لنسخها.

## الخطوة 2: إنشاء مصنف هدف فارغ (أو تحميل مصنف موجود)

يمكنك إما البدء من مصنف فارغ أو فتح ملف موجود سيستقبل الورقة المكررة.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **نصيحة:** إذا كان لديك بالفعل مصنف تقارير، استبدل السطر أعلاه بـ `new Workbook("ExistingReport.xlsx")` لإضافة الورقة المكررة إليه.

## الخطوة 3: نسخ الورقة بالكامل – يتم الحفاظ على جدول Pivot تلقائيًا

نسخ الورقة بأكملها هو أبسط طريقة لـ **copy sheet with pivot**. تقوم Aspose.Cells بنسخ تعريف الـ Pivot والذاكرة المؤقتة تلقائيًا.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **لماذا يعمل ذلك:** `addCopy` يستنسخ بنية الورقة، قيم الخلايا، الأنماط، وأي جداول Pivot مدمجة. ستظهر الورقة الجديدة في `dstWb` مطابقة تمامًا للأصل، بما في ذلك ذاكرة الـ Pivot المؤقتة.

## الخطوة 4: (اختياري) نسخ نطاق محدد يحتوي على جدول Pivot

أحيانًا لا تحتاج إلى نسخ الورقة بالكامل—ربما تحتاج فقط إلى جزء يحتوي على الـ Pivot. هنا يأتي دور **copy Excel range** وتحديدًا طلب نسخ الـ Pivot.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **كيف يساعدك ذلك:** `setCopyPivotTable(true)` يجبر المحرك على تكرار تعريف الـ Pivot حتى عند نسخ نطاق محدود. بدون هذا العلم، سيتم نسخ البيانات الخام فقط، وسيُفقد الـ Pivot.

## الخطوة 5: حفظ المصنف الهدف

أخيرًا، اكتب المحتوى المكرر إلى ملف جديد.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج يتم إنشاء `DuplicatedWithPivot.xlsx` في الدليل المستهدف. افتح الملف في Excel وسترى:

- ورقة عمل جديدة باسم `Sheet1 (Copy)` (أو الاسم الأصلي مع إضافة “Copy”)
- يظهر جدول الـ Pivot تمامًا كما هو في الورقة الأصلية، ويعمل بكامل وظائفه
- إذا استخدمت نسخ النطاق الاختياري، ستكون الخلايا فقط من A1 إلى G30 موجودة، لكن الـ Pivot سيظل يعمل لأن ذاكرة التخزين المؤقت تم نسخها

## أسئلة شائعة وحالات خاصة

### كيف يمكن نسخ Pivot إلى مصنف آخر دون نسخ الورقة بالكامل؟

إذا كنت تحتاج فقط إلى الـ Pivot وبياناته الأساسية، انسخ النطاق الذي يحتوي على كل من البيانات المصدر والـ Pivot، ثم استخدم `setCopyPivotTable(true)`. نفس الكود من **الخطوة 4** ينطبق؛ فقط تأكد أن النطاق يغطي مصدر البيانات.

### ماذا لو كان للمصنف المصدر عدة أوراق عمل تحتوي على جداول Pivot؟

كرر **الخطوة 3** لكل ورقة عمل تريد تكرارها:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### هل يعمل هذا مع الأوراق المحمية؟

يمكن لـ Aspose.Cells نسخ الأوراق المحمية، لكن يجب إلغاء حمايتها أولًا إذا كنت بحاجة لتعديل الـ Pivot بعد النسخ:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### هل يمكنني نسخ جدول Pivot إلى مصنف موجود يحتوي بالفعل على ورقة بنفس الاسم؟

نعم. استخدم `addCopy` مع اسم فريد:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## نصيحة احترافية: التحقق من ذاكرة Pivot المؤقتة

بعد النسخ، يمكنك برمجيًا التأكد من وجود ذاكرة الـ Pivot:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

إذا طبع معرف الذاكرة رقمًا غير سالب، فإن الـ Pivot تم نسخه بنجاح.

## الخلاصة

أنت الآن تعرف كيف **duplicate Excel sheet** في Java مع الحفاظ على كل جداول Pivot، وكيف **copy pivot** مباشرة، وكيف **copy Excel range** الذي يتضمن Pivot، وكيف **copy sheet with pivot** أو **copy pivot to workbook** باستخدام Aspose.Cells 25.11+. طبّق هذه الأنماط لأتمتة إنشاء التقارير، إنشاء نسخ من القوالب، أو بناء بيئات اختبار تحتاج إلى تحليلات مدفوعة بـ Pivot متطابقة.

هل أنت مستعد لاستكشاف المزيد؟ جرّب تصدير المصنف المكرر إلى PDF، أو تحديث ذاكرة الـ Pivot برمجيًا بعد النسخ لضمان انعكاس أحدث البيانات. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}