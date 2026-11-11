---
category: general
date: 2026-10-26
description: تعلم كيفية نسخ جدول محوري إلى مصنف جديد باستخدام Java، مع الحفاظ على
  التنسيق وتعريف الجدول المحوري أثناء نسخ نطاق Excel مع التنسيق عبر Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: ar
lastmod: 2026-10-26
og_description: نسخ جدول محوري إلى مصنف جديد في Java باستخدام Aspose.Cells. يوضح هذا
  الدليل كيفية نسخ نطاق Excel، الحفاظ على التنسيق، وإنشاء مصنف فارغ بكفاءة.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: نسخ جدول محوري إلى مصنف جديد في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية نسخ جدول محوري إلى مصنف جديد في جافا
url: /ar/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري إلى مصنف جديد في Java

إذا كنت بحاجة إلى **copy pivot table** من ملف Excel إلى آخر، يوضح لك هذا الدليل حلاً كاملاً وقابلاً للتنفيذ. سترى كيفية الحفاظ على تعريف الجدول المحوري، والاحتفاظ بجميع التنسيقات، وتجنب المشكلات الشائعة عند نسخ نطاق Excel.

غالبًا ما يثير نسخ جدول محوري أسئلة مثل *how to copy pivot* دون كسر مصدر البيانات أو فقدان الأنماط. بنهاية هذا الدرس ستحصل على برنامج Java مستقل ينشئ مصنفًا فارغًا، ينسخ النطاق المطلوب، ويحفظ النتيجة مع الحفاظ على الجدول المحوري.

## ما ستحققه

* تحميل مصنف مصدر يحتوي على جدول محوري.  
* **Create empty workbook** الذي سيتلقى البيانات المنسوخة.  
* **Copy excel range** الذي يتضمن الجدول المحوري، باستخدام خيارات تحافظ على الجدول المحوري والتنسيق.  
* حفظ ملف الوجهة والتحقق من أن الجدول المحوري يعمل تمامًا مثل الأصلي.

### المتطلبات المسبقة

* Java 17 أو أحدث.  
* Aspose.Cells for Java (الإصدار 23.10 أو أحدث).  
* إلمام أساسي ببيئات تطوير Java (IntelliJ IDEA، Eclipse، إلخ).  

> **نصيحة احترافية:** استخدم ترخيص التقييم المجاني لـ Aspose.Cells للاختبار السريع؛ استبدله بترخيص كامل قبل الاستخدام في الإنتاج.

## نسخ جدول محوري إلى مصنف جديد

الخطوة الأولى هي إعداد مصنفات المصدر والوجهة. تبدأ الوجهة كنداء **create empty workbook**، مما يمنحك ملفًا نظيفًا بورقة عمل واحدة.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### لماذا يعمل هذا

* `new Workbook()` **creates empty workbook** مع ورقة افتراضية، مما يجنب الحاجة إلى حذف البيانات الموجودة.  
* `CopyOptions` يخبر Aspose.Cells بنسخ بيانات **pivot table** الوصفية، وليس القيم الخام فقط. وضع `PASTE_ALL` ينقل أيضًا أنماط الخلايا، تنسيقات الأرقام، والتنسيق الشرطي—مما يلبي متطلب **copy range with formatting**.  
* `copyRange` ينفذ عملية **copy excel range** تحترم البُنى الداخلية للمصدر، لذا يظل الجدول المحوري فعالًا بعد النسخ.

## كيفية نسخ الجدول المحوري دون فقدان التنسيق

إذا استخدمت فقط `CopyOptions` الافتراضية، قد تُحذف بعض معلومات الأنماط في إصدارات Aspose.Cells القديمة. يضمن تحديد نوع اللصق صراحةً أن **copy range with formatting** يُحترم.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

إضافة `setPasteSpecialType` تضمن أن عرض الأعمدة، ارتفاع الصفوف، وحتى قواعد التحقق من البيانات تنتقل مع النطاق. هذا مفيد بشكل خاص عندما يمتد الجدول المحوري عبر أعمدة متعددة بعروض مخصصة.

## إنشاء مصنف فارغ قبل النسخ

أحيانًا يحاول المطورون النسخ إلى مصنف موجود يحتوي بالفعل على بيانات. قد يتسبب ذلك في تداخل النطاقات أو استبدالات غير متوقعة. بدءًا بـ نداء **create empty workbook** يعزل العملية:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

إذا كنت بحاجة إلى أكثر من ورقة عمل في الوجهة، يمكنك إضافتها بعد النسخ:

```java
destWb.getWorksheets().add("Summary");
```

## نسخ نطاق Excel مع التنسيق باستخدام CopyOptions

بعيدًا عن الجداول المحورية، يعمل النمط نفسه لأي **copy excel range** يتطلب الحفاظ على التنسيق—الرسوم البيانية، الجداول، أو التنسيقات الشرطية.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

تظل نسخة `CopyOptions` كما هي، لذا تحصل على سلوك متسق عبر النطاقات المختلفة.

### حالات الحافة التي يجب مراعاتها

| الحالة                                 | الإجراء الموصى به |
|----------------------------------------|-------------------|
| المصنف المصدر يحتوي على جداول محورية متعددة | نسخ نطاق كل جدول محوري على حدة أو نسخ الورقة بأكملها. |
| الوجهة تحتوي بالفعل على بيانات          | اختر خلية بداية غير متعارضة (مثال: "H1") عند استدعاء `copyRange`. |
| مصدر بيانات الجدول المحوري خارجي (مثال: قاعدة بيانات) | تأكد من أن المصنف الوجهة يشير إلى نفس مصدر البيانات الخارجي، أو قم بتحديث الجدول المحوري بعد النسخ. |
| مصنف كبير ( > 10 ميغابايت )           | زيادة حجم الذاكرة المخصصة لـ Java (`-Xmx2g`) لتجنب `OutOfMemoryError`. |

## التحقق من النتيجة

بعد تشغيل البرنامج، افتح `destination.xlsx`. يجب أن ترى:

* نفس تخطيط الجدول المحوري كما في `source.xlsx`.  
* جميع ألوان الخلايا، تنسيقات الأرقام، وعروض الأعمدة محفوظة.  
* ما زال مصدر بيانات الجدول المحوري يشير إلى نطاق البيانات الأصلي داخل الملف الجديد، لذا تحديث الجدول المحوري يحدث القيم بشكل صحيح.

إذا ظهر الجدول المحوري كجدول ثابت، تحقق مرة أخرى من ضبط `CopyOptions.setPasteType(PasteType.PASTE_ALL)`. بدون هذا الخيار، يتعامل Aspose.Cells مع الجدول المحوري كبيانات عادية.

## الخلاصة

أنت الآن تعرف كيف **copy pivot table** إلى مصنف جديد في Java مع الحفاظ على التنسيق، وصلات البيانات، وتخطيط الورقة. يُظهر الحل الكامل تحميل ملف المصدر، **create empty workbook**، تكوين خيارات **copy excel range**، وحفظ النتيجة.  

من هنا يمكنك استكشاف مواضيع ذات صلة مثل **how to copy pivot** عبر أوراق عمل مختلفة، تضمين الرسوم البيانية بجانب الجداول المحورية، أو أتمتة معالجة دفعات متعددة من المصنفات. جرب إعدادات `CopyOptions` لتناسب احتياجاتك الخاصة في الأتمة، وستحصل على مجموعة أدوات قوية لمعالجة Excel بين يديك.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف جديد في Java – دليل كامل لنسخ جدول محوري](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [نسخ جدول محوري بين المصنفات – دليل Java خطوة بخطوة](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [كيفية نسخ النطاق والحفاظ على جدول محوري في Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}