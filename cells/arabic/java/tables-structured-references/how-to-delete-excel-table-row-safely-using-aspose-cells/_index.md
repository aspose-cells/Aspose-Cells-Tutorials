---
category: general
date: 2026-08-20
description: تعلم كيفية حذف صف جدول Excel باستخدام Aspose.Cells مع الحفاظ على سلامة
  الجدول. يوضح هذا الدليل خطوة بخطوة حذف الصف بأمان ومعالجة الأخطاء.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to delete excel table row
- delete rows aspose.cells
language: ar
lastmod: 2026-08-20
og_description: كيفية حذف صف جدول Excel باستخدام Aspose.Cells. اتبع هذا الدليل الكامل
  لإزالة الصفوف بأمان ومعالجة الأخطاء المحتملة.
og_image_alt: Screenshot of Java code deleting a row from an Excel table with Aspose.Cells
og_title: كيفية حذف صف جدول Excel باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  headline: How to delete Excel table row safely using Aspose.Cells
  type: TechArticle
- description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  name: How to delete Excel table row safely using Aspose.Cells
  steps:
  - name: Why each step matters
    text: 1. **Load the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you programmatic access to its sheets, tables, and cells. 2. **Access
      the worksheet** – `getWorksheets().get(0)` selects the first sheet, which is
      where the target table lives. 3. **Retrieve the table** – In Excel, a st
  - name: Expected console output
    text: '*If the deletion is allowed*:'
  - name: Deleting multiple rows
    text: 'To delete three consecutive rows starting at the second data row:'
  - name: Deleting the last data row
    text: 'Attempting to delete the final data row will also raise an exception because
      a table cannot exist without at least one data row. Handle it the same way:'
  type: HowTo
tags:
- Aspose.Cells
- Excel
- Java
title: كيفية حذف صف جدول Excel بأمان باستخدام Aspose.Cells
url: /ar/java/tables-structured-references/how-to-delete-excel-table-row-safely-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حذف صف جدول Excel بأمان باستخدام Aspose.Cells

إذا كنت بحاجة إلى **how to delete Excel table row** دون كسر بنية الجدول، يوضح هذا الدليل نهجًا موثوقًا باستخدام Aspose.Cells للـ Java. سترى مثالًا كاملاً قابلًا للتنفيذ يلتقط استثناء الأمان ويحفظ المصنف بعد محاولة الحذف.

كما يغطي الدليل **delete rows aspose.cells** بطريقة تعمل مع سيناريوهات الصف الواحد والصفوف المتعددة، بحيث يمكنك تعديل الكود لمشاريعك الخاصة.

## ما يغطيه هذا الدليل

* تحميل مصنف موجود يحتوي على جدول Excel (ListObject).  
* الوصول إلى ورقة العمل الأولى والجدول الأول في تلك الورقة.  
* محاولة حذف صف بينما تقوم Aspose.Cells بالتحقق من صحة العملية.  
* معالجة الاستثناء الذي ترميه Aspose.Cells عندما يؤدي الحذف إلى إفساد الجدول.  
* حفظ المصنف بعد محاولة حذف آمنة.  

المتطلبات المسبقة: Java 17 أو أحدث، Aspose.Cells للـ Java (الإصدار 23.12 أو أحدث)، وفهم أساسي لصياغة Java. لا توجد مكتبات إضافية مطلوبة.

---

## كيفية حذف صف جدول Excel باستخدام Aspose.Cells

فيما يلي البرنامج الكامل المستقل. يتم شرح كل خطوة، ويمكن نسخ الكود إلى مشروع Java وتشغيله فورًا.

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Attempt to delete a row that would break the table structure
        //         The operation is wrapped in a try‑catch to demonstrate the safety check
        try {
            // Row index is zero‑based; this tries to delete the third data row.
            table.deleteRows(2, 1);
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            // Aspose.Cells throws an exception if the deletion would leave the table invalid.
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Step 5: Save the workbook after the safe‑deletion attempt
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

### لماذا كل خطوة مهمة

1. **Load the workbook** – `Workbook` يقرأ ملف `.xlsx` إلى الذاكرة، مما يمنحك وصولًا برمجيًا إلى أوراقه وجداولها وخلاياه.  
2. **Access the worksheet** – `getWorksheets().get(0)` يختار الورقة الأولى، حيث يقع الجدول المستهدف.  
3. **Retrieve the table** – في Excel، يُمثَّل الجدول المُنظم بـ `ListObject`. هذا الكائن يوفر طرقًا مثل `deleteRows`.  
4. **Safe deletion** – `deleteRows` يتحقق من سلامة الجدول. إذا كان حذف الصف سيكسر الجدول (مثلاً ترك رأس دون بيانات)، ترمي Aspose.Cells استثناءً. يُظهر كتلة `try‑catch` معالجة أمان **delete rows aspose.cells**.  
5. **Save the workbook** – `workbook.save` يكتب التغييرات إلى القرص، منتجًا ملفًا جديدًا يعكس عملية الحذف attempted.

### مخرجات وحدة التحكم المتوقعة

*إذا سُمح بالحذف*:

```
Row deleted successfully.
```

*إذا كان الحذف سيؤدي إلى إفساد الجدول* (شائع عندما يحتوي الجدول على صف بيانات واحد فقط متبقٍ):

```
Partial‑deletion prevented: Deleting the specified rows would break the table structure.
```

---

## تحميل المصنف (الخطوة 1)

`منشئ` `Workbook` يقبل مسار ملف. تأكد من أن المسار يشير إلى ملف Excel موجود يحتوي على جدول واحد على الأقل. إذا كان الملف مفقودًا، ترمي Aspose.Cells استثناء `FileNotFoundException`، والذي يمكنك التقاطه بطريقة مشابهة لاستثناء حذف الجدول.

```java
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**نصيحة:** استخدم مسارًا مطلقًا أثناء التطوير لتجنب ارتباك المسارات النسبية، خاصةً عند التشغيل من بيئة تطوير متكاملة (IDE).

---

## الوصول إلى ورقة العمل (الخطوة 2)

قد يحتوي المصنف على العديد من أوراق العمل. يستخدم المثال الأولى (`index 0`). إذا كنت بحاجة إلى ورقة محددة بالاسم، استبدل الاستدعاء بـ:

```java
Worksheet worksheet = workbook.getWorksheets().get("SheetName");
```

---

## استرجاع الجدول (الخطوة 3)

`ListObject` يمثل جدول Excel. إذا لم تحتوي ورقة العمل على جداول، فإن `getListObjects().size()` تُعيد `0`، واستدعاء `get(0)` سيؤدي إلى رفع استثناء `IndexOutOfBoundsException`. يبدو الفحص الوقائي هكذا:

```java
if (worksheet.getListObjects().getCount() == 0) {
    System.out.println("No tables found on the worksheet.");
    return;
}
ListObject table = worksheet.getListObjects().get(0);
```

---

## حذف الصفوف باستخدام Aspose.Cells (الخطوة 4)

جوهر **how to delete Excel table row** هو طريقة `deleteRows`:

```java
table.deleteRows(startIndex, count);
```

* `startIndex` – الفهرس الصفري للصف الأول الذي سيُحذف ضمن نطاق بيانات الجدول.  
* `count` – عدد الصفوف التي سيتم إزالتها.  

تتحقق Aspose.Cells من العملية مقابل رأس الجدول، إجمالي الصفوف، وأي صيغ تشير إلى الجدول. إذا كان الحذف سيترك الجدول في حالة غير صالحة، يُرمى استثناء، وهذا هو السبب في أن نمط `try‑catch` ضروري.

### حذف عدة صفوف

لحذف ثلاثة صفوف متتالية بدءًا من الصف البيانات الثاني:

```java
table.deleteRows(1, 3);
```

### حذف الصف البيانات الأخير

محاولة حذف الصف البيانات الأخير ستؤدي أيضًا إلى رفع استثناء لأن الجدول لا يمكن أن يوجد بدون صف بيانات واحد على الأقل. عالجه بنفس الطريقة:

```java
try {
    table.deleteRows(table.getDataRows().getCount() - 1, 1);
} catch (Exception ex) {
    System.out.println("Cannot delete the last row: " + ex.getMessage());
}
```

---

## حفظ المصنف (الخطوة 5)

بعد محاولة الحذف الآمن، حفظ التغييرات أمر بسيط:

```java
workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
```

يمكنك اختيار أي تنسيق مدعوم (`.xlsx`، `.xls`، `.csv`، إلخ) عن طريق تغيير امتداد الملف.

---

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|---------|------------|------|
| **عدم وجود جدول في الورقة** | `getListObjects().get(0)` يرفع `IndexOutOfBoundsException`. | تحقق من `getCount()` قبل الوصول. |
| **فهرس الصف غير صحيح** | `deleteRows` يستخدم فهرسة صفرية نسبة إلى الجدول، وليس إلى ورقة العمل. | تحقق من الفهرس بطباعة `table.getDataRows().getCount()`. |
| **حذف صف البيانات الوحيد** | Aspose.Cells يحمي سلامة الجدول ويرمي استثناءً. | إما أضف صفًا مؤقتًا أولًا أو قرر إزالة الجدول بالكامل باستخدام `table.remove()`. |
| **مشكلات مسار الملف** | قد تُفسر المسارات النسبية إلى دليل العمل الخاص بالـ IDE، مما يسبب `FileNotFoundException`. | استخدم مسارات مطلقة أو اضبط دليل العمل للـ IDE. |

---

## ملخص المثال الكامل العامل

فيما يلي البرنامج بالكامل مرة أخرى للنسخ السريع. يتضمن الفحوصات الوقائية التي نوقشت سابقًا.

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Ensure a table exists
        if (worksheet.getListObjects().getCount() == 0) {
            System.out.println("No tables found on the worksheet.");
            return;
        }

        // Retrieve the first table
        ListObject table = worksheet.getListObjects().get(0);

        // Attempt safe deletion
        try {
            table.deleteRows(2, 1); // zero‑based index
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Save the result
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

تشغيل هذا البرنامج يطبع إما رسالة نجاح أو رسالة الاستثناء الوقائي، ثم يكتب `TableSafeDelete.xlsx` إلى المجلد المحدد.

---

## الخلاصة

أنت الآن تعرف **how to delete Excel table row** بأمان باستخدام Aspose.Cells للـ Java. أظهر الدليل كيفية تحميل مصنف، تحديد جدول، إجراء حذف صف محمي، معالجة استثناء الأمان **delete rows aspose.cells**، وحفظ الملف المحدث.

من هنا يمكنك:

* حذف عدة صفوف في استدعاء واحد.  
* التكرار عبر قائمة فهارس الصفوف لإجراء حذف دفعي.  
* استبدال `try‑catch` بتسجيل مخصص لبيئات الإنتاج.  

جرّب تخطيطات جداول مختلفة، صيغ، وقواعد التحقق من البيانات لترى كيف تفرض Aspose.Cells السلامة. عندما تحتاج إلى معالجة ملفات Excel برمجيًا، فإن النمط المعروض هنا يوفر أساسًا قويًا ومدركًا للأخطاء.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إدراج وحذف الصفوف في Excel باستخدام Aspose.Cells للـ .NET: دليل شامل](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [كيفية حذف الصفوف الفارغة في Excel باستخدام Aspose.Cells .NET لتنظيف البيانات](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [كيفية حذف عمود في Excel باستخدام Aspose.Cells .NET بلغة C# - دليل شامل](/cells/english/net/worksheet-management/delete-column-aspose-cells-dotnet-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}