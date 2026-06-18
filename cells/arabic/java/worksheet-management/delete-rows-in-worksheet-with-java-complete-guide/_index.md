---
category: general
date: 2026-06-18
description: حذف الصفوف في ورقة العمل باستخدام Aspose.Cells للغة Java. تعلّم كيفية
  إزالة صف رأس الجدول وحذف الصفوف من جدول Excel بأمان.
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: ar
og_description: حذف الصفوف في ورقة العمل باستخدام Aspose.Cells للـ Java. يوضح هذا
  الدليل كيفية إزالة صف رأس الجدول وحذف الصفوف من جدول Excel بكفاءة.
og_title: حذف الصفوف في ورقة العمل باستخدام جافا – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  headline: Delete rows in worksheet with Java – Complete Guide
  type: TechArticle
- description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  name: Delete rows in worksheet with Java – Complete Guide
  steps:
  - name: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
    text: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
  - name: With the header now a regular row, `deleteRows(0, …)` works without complaints.
    text: With the header now a regular row, `deleteRows(0, …)` works without complaints.
  - name: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
    text: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
  - name: Loads a workbook.
    text: Loads a workbook.
  - name: Checks if the first table exists.
    text: Checks if the first table exists.
  - name: Deletes **all** rows *including* the header safely.
    text: Deletes **all** rows *including* the header safely.
  - name: Re‑creates the table from the remaining rows (if any).
    text: Re‑creates the table from the remaining rows (if any).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Worksheet
title: حذف الصفوف في ورقة العمل باستخدام جافا – دليل كامل
url: /ar/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف الصفوف في ورقة العمل – دليل Java كامل

هل احتجت يومًا إلى **حذف الصفوف في ورقة العمل** لكن واجهت صعوبة لأن رأس الجدول يرفض التحرك؟ لست وحدك. في العديد من سيناريوهات أتمتة Excel تكون الصف الأول جزءًا من جدول منظم، واستدعاء `deleteRows` بطريقة ساذجة يثير استثناءً أو يترك الرأس دون تعديل.  

في هذا الدرس سنستعرض بالضبط كيفية *إزالة صف رأس الجدول* و*إزالة الصفوف من جدول Excel* دون كسر الورقة. في النهاية ستحصل على مقتطف نظيف قابل للتنفيذ يعمل مع أحدث نسخة من Aspose.Cells for Java (v23.10 في وقت كتابة هذا الدرس).  

سنغطي المتطلبات المسبقة، ثلاث طرق عملية، وبعض النصائح التي قد ترغب في حفظها. لا إطالة—فقط ما تتوقعه من مطور متمرس أثناء فنجان القهوة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- Java 17 أو أحدث (الكود يُترجم مع إصدارات أقدم، لكن يُنصح بـ 17).
- Aspose.Cells for Java 23.10 أو أحدث مضاف إلى ملف Maven `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- ملف Excel تجريبي (`Sample.xlsx`) يحتوي على جدول في ورقة العمل الأولى. رأس الجدول يقع في الصف 0 (صف Excel 1).

هذا كل شيء. جاهز؟ لنبدأ.

## حذف الصفوف في ورقة العمل – لماذا يهم صف الرأس

عند استدعائك:

```java
ws.getCells().deleteRows(0, 2, true);
```

ترفض Aspose.Cells حذف الصف 0 لأنه جزء من **جدول**. تحمي الـ API سلامة الجدول؛ إزالة الرأس سيترك صفوف البيانات معزولة. الاستثناء الذي ستراه يكون شيئًا مثل *“The specified row belongs to a table and cannot be deleted.”*  

فهم هذه الحماية هو الخطوة الأولى نحو حل ناجح.

## النهج 1 – حذف الصفوف **أسفل** الرأس (الأكثر شيوعًا)

إذا كنت ترغب ببساطة في مسح البيانات مع الحفاظ على بنية الجدول، ابدأ الحذف من الصف **بعد** الرأس.

```java
import com.aspose.cells.*;

public class DeleteRowsBelowHeader {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Determine how many data rows the table currently has
        Table table = ws.getTables().get(0);
        int dataRowCount = table.getDataRange().getRowCount();

        // Delete all data rows (keep header)
        // startRow = 1 because row index 0 is the header
        ws.getCells().deleteRows(1, dataRowCount, true);

        // Save the result
        wb.save("Result_DeleteRowsBelowHeader.xlsx");
    }
}
```

**لماذا يعمل هذا:** `deleteRows` يستقبل فهرس بدء بقيمة 1، لذا يبقى الرأس دون تعديل. العلامة `true` تنقل الصفوف المتبقية للأعلى، محافظًا على أي صيغ تشير إليها. بعد تشغيل الكود سترى جدولًا نظيفًا مع سطر الرأس فقط.

### نصيحة سريعة

إذا احتجت لحذف نطاق *محدد* من الصفوف (مثلاً الصفوف 5‑10)، فقط عدّل فهرس البداية والعدد وفقًا لذلك. سيقوم الجدول تلقائيًا بتغيير حجمه ليتطابق مع نطاق البيانات الجديد.

## النهج 2 – تحويل الجدول إلى نطاق عادي، ثم الحذف

أحيانًا تحتاج حقًا إلى **إزالة صف رأس الجدول** ومعاملة البيانات كنطاق عادي. الحيلة هي أولاً *إلغاء إدراج* الجدول.

```java
import com.aspose.cells.*;

public class RemoveHeaderAndDeleteRows {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // 1️⃣ Unlist the table – it becomes a normal range
        table.unlist();

        // 2️⃣ Now you can delete the header row (row 0) and any other rows
        // Delete header + first two data rows (total 3 rows)
        ws.getCells().deleteRows(0, 3, true);

        // 3️⃣ (Optional) Re‑create a table from the remaining data
        // Assuming you still have data starting at row 0
        int firstDataRow = 0;
        int lastDataRow = ws.getCells().getMaxDataRow();
        int firstCol = ws.getCells().getMaxDataColumn();
        int lastCol = ws.getCells().getMaxDataColumn();

        String range = new CellArea(firstDataRow, 0, lastDataRow, firstCol).format();
        ws.getTables().add(range, true);
        ws.getTables().get(0).setName("NewTable");

        wb.save("Result_RemoveHeaderAndDeleteRows.xlsx");
    }
}
```

**الشرح:**  

1. `table.unlist()` يزيل بيانات تعريف الجدول، محولًا الكتلة إلى خلايا عادية.  
2. مع تحول الرأس الآن إلى صف عادي، `deleteRows(0, …)` يعمل دون أي مشاكل.  
3. إذا كنت لا تزال بحاجة إلى جدول بعد التنظيف، يمكنك إعادة إنشائه باستخدام `ws.getTables().add(...)`.

هذا النهج مفيد عندما يكون الرأس نفسه غير صحيح أو ترغب في استبدال تعريف الجدول بالكامل.

## النهج 3 – استخدام API الجدول لحذف صفوف محددة

تقدم Aspose.Cells أيضًا طريقة **على مستوى الجدول** لحذف الصفوف، والتي تتعامل تلقائيًا مع حماية الرأس.

```java
import com.aspose.cells.*;

public class DeleteRowsViaTableAPI {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // Delete the first two data rows (index 0 = first data row, not the header)
        // The Table API counts only data rows, so we don't touch the header.
        table.deleteRows(0, 2);

        wb.save("Result_DeleteRowsViaTableAPI.xlsx");
    }
}
```

**لماذا قد تختار هذا:** إنه الطريقة الأكثر *دلالة* — فأنت تخبر الجدول بـ “إزالة صفوف البيانات الخاصة بي”. تقوم الـ API بتحديث نطاق الجدول تلقائيًا، ولن تحتاج أبدًا إلى التعامل مع فهارس الصفوف الخام.

## الحالات الحدية والمشكلات الشائعة

| الحالة | ما يجب مراقبته | الإصلاح المقترح |
|-----------|------------------|-----------------|
| **جداول متعددة على نفس الورقة** | `ws.getTables().get(0)` قد يستهدف الجدول الخطأ. | استخدم `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` |
| **خلية مدمجة في الرأس** | حذف الصفوف قد يقسم المناطق المدمجة، مما يسبب تشوهات في التخطيط. | قم بإلغاء الدمج قبل الحذف: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **صيغ تشير إلى الرأس** | إزالة الرأس تكسر المراجع الخارجية. | قم بتحديث الصيغ بعد الحذف أو احتفظ بصف بديل. |
| **أوراق عمل كبيرة (>10 000 صف)** | `deleteRows` قد يكون أبطأ بسبب التحريك الداخلي. | استخدم `ws.getCells().clearRows(start, count)` إذا لم تكن بحاجة إلى التحريك. |

## مثال عملي كامل – دمج أفضل ما في جميع الأساليب

فيما يلي برنامج مستقل يقوم بـ:

1. تحميل دفتر عمل.
2. التحقق مما إذا كان الجدول الأول موجودًا.
3. حذف **جميع** الصفوف *بما في ذلك* الرأس بأمان.
4. إعادة إنشاء الجدول من الصفوف المتبقية (إن وجدت).

```java
import com.aspose.cells.*;

public class DeleteRowsInWorksheetFullDemo {
    public static void main(String[] args) throws Exception {
        // ① Load the workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // ② Guard: make sure a table is present
        if (ws.getTables().getCount() == 0) {
            System.out.println("No tables found – nothing to delete.");
            return;
        }

        // ③ Grab the first table (adjust if you have a named table)
        Table table = ws.getTables().get(0);

        // ④ Unlist so we can delete the header row
        table.unlist();

        // ⑤ Determine total rows to delete (header + data)
        int totalRows = table.getRange().getRowCount(); // includes header
        ws.getCells().deleteRows(0, totalRows, true);

        // ⑥ If there are still rows left, rebuild the table
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();

        if (maxRow >= 0) { // there is at least one row left
            String newRange = new CellArea(0, 0, maxRow, maxCol).format();
            Table newTable = ws.getTables().add(newRange, true);
            newTable.setName("RebuiltTable");
        }

        // ⑦ Save the result
        wb.save("Result_DeleteRowsInWorksheetFullDemo.xlsx");
        System.out.println("Rows deleted and table rebuilt successfully.");
    }
}
```

**الناتج المتوقع:** بعد التنفيذ ستجد الملف `Result_DeleteRowsInWorksheetFullDemo.xlsx` مع حذف الجدول الأصلي، وإذا بقيت أي بيانات، جدولًا جديدًا يسمى `RebuiltTable`. يطبع الطرفية رسالة نجاح مختصرة.

## ملخص بصري

![ورقة عمل Excel قبل وبعد حذف الصفوف](https://example.com/images/delete-rows-workbook.png "قبل وبعد حذف الصفوف في ورقة العمل")

*نص بديل:* “قبل وبعد حذف الصفوف في ورقة العمل – تم إزالة الرأس، وتم مسح صفوف البيانات.”

## الخلاصة

لقد غطينا ثلاث طرق موثوقة لـ **حذف الصفوف في ورقة العمل** مع معالجة سيناريو *إزالة صف رأس الجدول* الصعب وحذف **صفوف من جدول Excel** بأمان. سواء كنت تفضل عمليات الخلايا الخام، أو API الجدول، أو دورة إلغاء الإدراج وإعادة الإدراج الكاملة، فإن مقتطفات الشيفرة أعلاه جاهزة للإدماج في مشروعك.  

الخطوات التالية؟ جرّب دمج هذه التقنيات مع منطق شرطي — احذف الصفوف فقط عندما يحتوي عمود معين على “Inactive”، أو عالج دفعات متعددة

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إدارة الصفوف بفعالية في Excel باستخدام Aspose.Cells for Java: إدراج وحذف الصفوف](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [كيفية إزالة الصفوف الفارغة من ملفات Excel باستخدام Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [كيفية حذف الصفوف في Excel باستخدام Aspose.Cells for Java | دليل وتعليمات](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}