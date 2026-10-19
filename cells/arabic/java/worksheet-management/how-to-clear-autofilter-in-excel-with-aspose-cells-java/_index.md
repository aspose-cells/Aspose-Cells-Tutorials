---
category: general
date: 2026-08-11
description: كيفية مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells للـ Java – تعلم
  كيفية إزالة الفلتر التلقائي من Excel، وتعطيل الفلتر التلقائي في Excel، وإزالة فلتر
  Excel برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to clear autofilter
- remove autofilter from excel
- remove excel filter
- how to remove autofilter
- disable autofilter in excel
language: ar
lastmod: 2026-08-11
og_description: كيفية مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells للغة Java.
  اتبع هذا الدليل الكامل لإزالة الفلتر التلقائي من Excel، وتعطيل الفلتر التلقائي في
  Excel، وتنظيف أوراق العمل الخاصة بك.
og_image_alt: Screenshot showing Java code that clears an autofilter in an Excel file
  with Aspose.Cells
og_title: كيفية مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells (Java) – دليل خطوة
  بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to clear autofilter in Excel with Aspose.Cells for Java – learn
    to remove autofilter from Excel, disable autofilter in Excel, and remove Excel
    filter programmatically.
  headline: How to clear autofilter in Excel with Aspose.Cells (Java)
  type: TechArticle
- description: How to clear autofilter in Excel with Aspose.Cells for Java – learn
    to remove autofilter from Excel, disable autofilter in Excel, and remove Excel
    filter programmatically.
  name: How to clear autofilter in Excel with Aspose.Cells (Java)
  steps:
  - name: '`TableWithFilter.xlsx` remains unchanged.'
    text: '`TableWithFilter.xlsx` remains unchanged.'
  - name: '`NoAutoFilter.xlsx` contains the same data, but the AutoFilter drop‑down
      arrows are no longer visible.'
    text: '`NoAutoFilter.xlsx` contains the same data, but the AutoFilter drop‑down
      arrows are no longer visible.'
  - name: If you open the file, the **remove autofilter from excel** operation will
      be evident in the UI (no filter icons on column headers).
    text: If you open the file, the **remove autofilter from excel** operation will
      be evident in the UI (no filter icons on column headers).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells (Java)
url: /ar/java/worksheet-management/how-to-clear-autofilter-in-excel-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells (Java)

مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells for Java هو احتياج شائع عند إنشاء التقارير برمجياً. يوضح هذا الدليل كيفية إزالة الفلتر التلقائي من أوراق Excel بسرعة وأمان، بحيث يبدو الملف النهائي نظيفاً للمستخدمين النهائيين.

سترى مثالاً كاملاً قابلاً للتنفيذ يقوم بتحميل مصنف، الوصول إلى الجدول الأول، مسح AutoFilter، وحفظ النتيجة. يغطي الدرس أيضاً تنويعات مثل التعامل مع جداول متعددة، العمل مع إصدارات Aspose.Cells القديمة، وتجنب الأخطاء الشائعة. لا تحتاج إلى أي وثائق خارجية—فقط انسخ الشيفرة، عدل مسارات الملفات، وشغّلها.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* Java 8 أو أحدث مثبت.
* Aspose.Cells for Java 25.11 أو أحدث (تم إضافة طريقة `clear()` في الإصدار 25.11).
* ملف Excel (`TableWithFilter.xlsx`) يحتوي على جدول مع تطبيق AutoFilter.
* بيئة تطوير (IDE، Maven/Gradle، أو مجرد `javac`).

إذا كنت تستخدم Maven، أضف الاعتماد:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.11</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## كيفية مسح الفلتر التلقائي في Excel باستخدام Aspose.Cells

فيما يلي البرنامج الكامل بلغة Java. كل خطوة تتضمن شرحًا قصيرًا “لماذا” لتفهم تدفق الـ API، وليس مجرد الصياغة.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Step 2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first ListObject (table) on the worksheet
        // ListObject represents an Excel table; it holds the AutoFilter object.
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Clear the AutoFilter applied to the table (new API in 25.11)
        // The clear() method removes the filter criteria and disables the drop‑down arrows.
        table.getAutoFilter().clear();

        // Step 5: Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/NoAutoFilter.xlsx");
    }
}
```

### لماذا كل سطر مهم

| الخطوة | الغرض |
|------|---------|
| **تحميل المصنف** | يفتح ملف Excel في الذاكرة حتى يتمكن Aspose.Cells من تعديل محتوياته. |
| **الوصول إلى ورقة العمل** | يمكن لملفات Excel أن تحتوي على عدة أوراق؛ تحتاج إلى الورقة الصحيحة للعمل مع الجدول. |
| **استرجاع ListObject** | ListObject هو التمثيل البرمجي لجدول Excel. يحتوي الجدول على كائن AutoFilter. |
| **مسح AutoFilter** | `clear()` يزيل معايير الفلترة ويخفي أسهم الفلتر. هذه هي العملية الأساسية لـ *remove autofilter from excel*. |
| **حفظ المصنف** | يكتب التغييرات إلى القرص، منتجاً ملفاً تم تعطيل الفلتر فيه. |

## إزالة فلتر Excel من جداول متعددة (اختياري)

إذا كان المصنف يحتوي على أكثر من جدول، كرّر عبر مجموعة `ListObjects`:

```java
Worksheet ws = workbook.getWorksheets().get(0);
for (int i = 0; i < ws.getListObjects().getCount(); i++) {
    ListObject tbl = ws.getListObjects().get(i);
    tbl.getAutoFilter().clear();   // disables filter for each table
}
```

هذا المقتطف يوضح **كيفية إزالة الفلتر التلقائي** من كل جدول في ورقة، وهو مفيد لمعالجة التقارير على دفعات.

## التعامل مع المصنفات التي لا تحتوي على AutoFilter

استدعاء `clear()` على جدول لا يحتوي على فلتر لا يثير استثناءً—إنه لا يفعل شيئًا. ومع ذلك، إذا حاولت الوصول إلى جدول غير موجود (`get(0)` عندما تكون المجموعة فارغة)، سيطلق Aspose.Cells استثناء `IndexOutOfRangeException`. احمِ نفسك من ذلك بفحص بسيط:

```java
if (worksheet.getListObjects().getCount() > 0) {
    ListObject firstTable = worksheet.getListObjects().get(0);
    firstTable.getAutoFilter().clear();
}
```

هذا النمط الوقائي يساعدك على **تعطيل الفلتر التلقائي في Excel** بأمان عبر ملفات الإدخال المختلفة.

## التوافق مع إصدارات Aspose.Cells القديمة

تم تقديم طريقة `clear()` في الإصدار 25.11. للإصدارات السابقة، يجب إعادة تعيين نطاق الفلتر يدويًا:

```java
AutoFilter filter = table.getAutoFilter();
filter.setRange("");               // removes the filter range
filter.setShowFilter(false);       // hides filter arrows
```

على الرغم من أن هذا يعمل، فإن API `clear()` الأحدث أكثر قابلية للقراءة وأقل عرضة للأخطاء. إذا كان بإمكانك التحديث، فافعل ذلك لتبسيط الشيفرة.

## الأخطاء الشائعة ونصائح الخبراء

* **فواصل مسار الملف** – استخدم `File.separator` أو الشرط المائل (`/`) لتجنب المشكلات الخاصة بالمنصة.
* **قفل المصنف** – تأكد من أن ملف المصدر غير مفتوح في Excel عندما يكتب عملية Java الخاصة بك إليه؛ وإلا سيؤدي `save()` إلى رمي `IOException`.
* **المصنفات الكبيرة** – للملفات التي حجمها >100 ميغابايت، فكر في استخدام معامل `loadOptions` لتحميل الأوراق المطلوبة فقط، مما يقلل استهلاك الذاكرة.
* **اختبار النتيجة** – افتح الملف المحفوظ `NoAutoFilter.xlsx` في Excel وتأكد من أن أسهم الفلتر اختفت. يمكنك أيضاً التحقق برمجياً من `table.getAutoFilter().isShowFilter()`؛ يجب أن تُعيد `false`.

## النتيجة المتوقعة

بعد تشغيل البرنامج:

1. يبقى `TableWithFilter.xlsx` دون تغيير.
2. يحتوي `NoAutoFilter.xlsx` على نفس البيانات، لكن أسهم القائمة المنسدلة للـ AutoFilter لم تعد مرئية.
3. إذا فتحت الملف، ستظهر عملية **remove autofilter from excel** بوضوح في واجهة المستخدم (لا أيقونات فلتر على رؤوس الأعمدة).

## ملف المصدر الكامل للنسخ واللصق

احفظ ما يلي كملف `RemoveAutoFilter.java`. عدل العنصر النائب `YOUR_DIRECTORY` إلى مسار مطلق أو نسبي على جهازك.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Retrieve the first ListObject (table) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Clear the AutoFilter applied to the table (new API in 25.11)
        table.getAutoFilter().clear();

        // Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/NoAutoFilter.xlsx");
    }
}
```

قم بالترجمة والتشغيل:

```bash
javac -cp "path/to/aspose-cells-25.11.jar" RemoveAutoFilter.java
java -cp ".:path/to/aspose-cells-25.11.jar" RemoveAutoFilter
```

يجب ألا ترى أي مخرجات في وحدة التحكم إذا نجح كل شيء؛ سيكون الملف الناتج في نفس الدليل.

## الخلاصة

أنت الآن تعرف **كيفية مسح الفلتر التلقائي** في Excel باستخدام Aspose.Cells for Java. غطى الدرس الخطوات الأساسية، وكيفية **إزالة الفلتر التلقائي من Excel** لجداول متعددة، وكيفية التعامل مع المصنفات بدون فلاتر، وما يجب فعله عند استخدام إصدارات المكتبة القديمة. باتباع المثال الكامل، يمكنك دمج إزالة الفلتر في أي خط أنابيب تقارير مؤتمت.

**الخطوات التالية**

* استكشف ميزات Aspose.Cells الأخرى مثل **disable autofilter in excel** مع الحفاظ على تنسيق الجدول.
* دمج هذه التقنية مع إزالة التحقق من البيانات (`ListObject.getValidation().clear()`) لتصدير نظيف بالكامل.
* راجع مرجع Aspose.Cells API لمزيد من عمليات تعديل الجداول، مثل إضافة صفوف أو تنسيق الخلايا.

لا تتردد في تجربة هياكل ملفات مختلفة ومشاركة نتائجك. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [أتمتة تصفية Excel باستخدام Aspose.Cells في Java: دليل شامل لتطبيق AutoFilter Implementation](/cells/english/java/data-analysis/aspose-cells-java-apply-autofilter-excel/)
- [تنفيذ AutoFilter 'يبدأ بـ' في Excel باستخدام Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)
- [تنفيذ AutoFilter 'ينتهي بـ' في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}