---
category: general
date: 2026-09-27
description: إنشاء نطاق مسمى في Excel باستخدام Aspose.Cells، تعيين اسم الجدول، إضافة
  نطاق مسمى، إنشاء جدول Excel، واكتشاف أخطاء تكرار الاسم.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: ar
lastmod: 2026-09-27
og_description: إنشاء نطاق مسمى في Excel باستخدام Aspose.Cells، ثم تعيين اسم الجدول،
  إضافة النطاق المسمى، إنشاء جدول Excel، واكتشاف أخطاء تكرار الاسم.
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: إنشاء نطاق مسمى واكتشاف الاسم المكرر في إكسل
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: إنشاء نطاق مسمى واكتشاف اسم مكرر في إكسل
url: /ar/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء نطاق مسمى واكتشاف الاسم المكرر في Excel

إذا كنت بحاجة إلى **إنشاء نطاق مسمى** في مصنف Excel وتريد تجنب تصادم الأسماء، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for Java. ستتعلم **إضافة نطاق مسمى**، **إنشاء جدول Excel**، **تعيين اسم الجدول**، و**اكتشاف أخطاء الاسم المكرر** في مثال واحد متكامل.

يُعد العمل مع النطاقات المسمَّاة مطلبًا شائعًا عندما تبني أدوات تقارير، أوراق تحقق من البيانات، أو لوحات تحكم ديناميكية. في نهاية هذا البرنامج التعليمي ستحصل على برنامج قابل للتنفيذ يُنشئ نطاقًا مسمى بأمان، يبني جدولًا، ويتعامل بأناقة مع أي استثناء يتعلق بتصادم الأسماء.

## المتطلبات المسبقة

- Java 17 أو أحدث مثبتة
- Maven أو Gradle لإدارة التبعيات
- Aspose.Cells for Java (أحدث إصدار؛ إحداثيات Maven `com.aspose:aspose-cells:23.9` في وقت كتابة الدليل)
- إلمام أساسي بمفاهيم Excel مثل أوراق العمل، النطاقات، والجداول

## الخطوة 1: إنشاء نطاق مسمى في المصنف

الخطوة الأولى هي إنشاء كائن `Workbook` وإضافة نطاق مسمى يشير إلى مجموعة خلايا محددة.

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**لماذا هذا مهم:**  
النطاق المسمى يعمل كمرجع قابل لإعادة الاستخدام يمكن للصيغ والجداول الإشارة إليه. إضافته مبكرًا يضمن أن الخطوات اللاحقة يمكنها إعادة استخدام نفس المعرف دون الحاجة إلى كتابة عناوين الخلايا يدويًا.

## الخطوة 2: إنشاء جدول Excel يستخدم النطاق المسمى

بعد ذلك، نقوم بإنشاء جدول منظم (ListObject) يشغل نفس المنطقة التي يغطيها النطاق المسمى. هذا يوضح مفهوم **إنشاء جدول Excel**.

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**لماذا هذا مهم:**  
الجداول توفر فرزًا وتصفية وتنسيقًا مدمجين. من خلال محاذاة الجدول مع النطاق المسمى، تحافظ على اتساق نموذج البيانات.

## الخطوة 3: تعيين اسم الجدول ومعالجة احتمال حدوث تعارض

الآن نحاول إعطاء الجدول اسمًا يطابق النطاق المسمى الذي أنشأناه مسبقًا. تُظهر هذه الخطوة **تعيين اسم الجدول** وتُسبب تعمدًا تعارضًا في الأسماء.

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**لماذا هذا مهم:**  
Excel لا يسمح للجدول والنطاق المسمى بأن يشتركا في نفس المعرف. اكتشاف التعارض مبكرًا يمنع تلف المصنفات ويسهل عملية تصحيح الأخطاء.

## الخطوة 4: اكتشاف الاسم المكرر وحله

عند التقاط الاستثناء، يمكنك إما إعادة تسمية الجدول أو حذف النطاق المسمى المتعارض. فيما يلي استراتيجية حل بسيطة تعيد تسمية الجدول بإضافة لاحقة.

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**نقاط رئيسية في الحل:**

- **اكتشاف الاسم المكرر** – كتلة `catch` تؤكد وجود التعارض.
- الحلقة تتحقق من مجموعة أسماء المصنف لضمان أن المعرف الجديد فريد.
- أخيرًا، يتم حفظ المصنف بحيث يمكنك فتحه في Excel والتحقق من أن الجدول يحمل اسمًا مميزًا بينما يبقى النطاق المسمى الأصلي سليمًا.

## مثال كامل قابل للتنفيذ

بجمع جميع الأجزاء معًا، يبدو البرنامج الكامل كالتالي:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**الناتج المتوقع عند تشغيل البرنامج:**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

عند فتح `NamedRangeDemo.xlsx` في Excel ستظهر:

- نطاق مسمى **MyRange** يشير إلى الخلايا A1:C5.
- جدول باسم **MyRange_1** يغطي نفس الخلايا.
- لا يوجد خطأ في التسمية عند محاولة إضافة صيغ تشير إلى `MyRange`.

## الأخطاء الشائعة وأفضل الممارسات

- **عدم إعادة استخدام المعرفات**: تحقق دائمًا من أن الاسم غير موجود مسبقًا قبل تعيينه للجدول.  
- **تفضيل الفحوصات الصريحة**: `workbook.getNames().get("Name")` تُعيد `null` إذا كان الاسم متاحًا، وهذا أكثر أمانًا من التقاط استثناء عام.  
- **الحفاظ على اتساق قواعد التسمية**: استخدام بادئة مثل `tbl_` للجداول و`rng_` للنطاقات يقلل من فرص حدوث تصادم.  
- **توافق الإصدارات**: يعمل الكود مع Aspose.Cells 23.9 وما بعده؛ قد تختلف رسائل الاستثناء في الإصدارات الأقدم.

## الخلاصة

أصبح بإمكانك الآن **إنشاء نطاق مسمى**، **إضافة نطاق مسمى**، **إنشاء جدول Excel**، **تعيين اسم الجدول**، و**اكتشاف الأخطاء الناتجة عن الاسم المكرر** باستخدام Aspose.Cells for Java. من خلال معالجة تصادم الأسماء بشكل استباقي، تحافظ على نظافة المصنفات وتزيد من موثوقية سكريبتات الأتمتة الخاصة بك.

**الخطوات التالية**

- استكشف واجهة برمجة التطبيقات **set table name** بمزيد من التفصيل لتطبيق خيارات التنسيق.  
- استخدم نمط **detect duplicate name** عند إنشاء جداول متعددة برمجيًا.  
- اجمع بين النطاقات المسمَّاة والصيغ أو التحقق من البيانات لتقارير ديناميكية.

Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Style Named Range Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Create Style Named Range Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Create Style Named Range Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}