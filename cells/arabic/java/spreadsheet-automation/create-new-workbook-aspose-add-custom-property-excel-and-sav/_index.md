---
category: general
date: 2026-08-11
description: إنشاء مصنف جديد Aspose في Java، إضافة خاصية مخصصة إلى Excel، ثم حفظ المصنف
  بصيغة XLSB مع مثال كامل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: ar
lastmod: 2026-08-11
og_description: إنشاء مصنف جديد باستخدام Aspose في Java، إضافة خاصية مخصصة إلى Excel،
  وحفظ المصنف بصيغة XLSB مع مثال كامل وجاهز للتنفيذ.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: إنشاء دفتر عمل جديد Aspose – إضافة خاصية مخصصة في Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: إنشاء دفتر عمل جديد باستخدام Aspose – إضافة خاصية مخصصة إلى Excel وحفظه كملف
  XLSB
url: /ar/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف جديد Aspose – إضافة خاصية مخصصة Excel وحفظه كـ XLSB

إذا كنت بحاجة إلى **create new workbook Aspose** في تطبيق Java، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعلم **add custom property Excel**، استرجاع القيمة، و**save workbook as XLSB** دون فقدان أي بيانات وصفية.

يغطي الدرس كل شيء من إعداد المشروع إلى التحقق من الملف المحفوظ. لا حاجة إلى وثائق خارجية؛ فقط اتبع الخطوات وشغّل الكود.

## المتطلبات المسبقة

- Java Development Kit (JDK) 8 أو أعلى مثبت.
- Maven أو Gradle لإدارة التبعيات (المثال يستخدم Maven).
- رخصة Aspose.Cells for Java سارية (أو استخدم وضع التقييم المجاني للاختبار).

## الخطوة 1: إضافة Aspose.Cells إلى مشروعك

أضف حزمة Aspose.Cells Maven إلى ملف `pom.xml`. هذه التبعية توفر الفئات اللازمة لـ **create new workbook Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **نصيحة احترافية:** إذا كنت تفضّل Gradle، استبدل مقتطف Maven بالسطر المكافئ `implementation "com.aspose:aspose-cells:23.12"`.

## الخطوة 2: إنشاء مصنف جديد Aspose

الخطوة الوظيفية الأولى هي إنشاء كائن `Workbook`. هذا الكائن يمثل ملف Excel في الذاكرة وهو نقطة الدخول لجميع العمليات اللاحقة.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

إنشاء مصنف جديد Aspose يمنحك مصنفًا نظيفًا مع ورقة عمل افتراضية، جاهزًا للتخصيصات.

## الخطوة 3: إضافة خاصية مخصصة Excel

تسمح الخصائص المخصصة لك بتخزين بيانات وصفية عشوائية داخل ملف Excel. هنا نقوم **add custom property Excel** باسم `ProjectId` بقيمة رقمية.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

طريقة `add` تقبل اسم الخاصية وقيمة من أي نوع مدعوم (سلسلة، رقم، تاريخ، إلخ). هذه البيانات الوصفية تنتقل مع الملف أينما قمت بنسخه.

## الخطوة 4: استرجاع وعرض الخاصية المخصصة

قراءة الخاصية مرة أخرى يتحقق من أنها تم تخزينها بشكل صحيح. يمكنك أيضًا استخدام القيمة المسترجعة في منطق عملك.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

التحويل إلى `int` يعمل لأننا خزنّا قيمة رقمية. إذا خزنّت سلسلة، استخدم `(String)` بدلاً من ذلك.

## الخطوة 5: حفظ المصنف كـ XLSB

الآن تقوم **save workbook as XLSB**. تنسيق XLSB يخزن المصنف بتمثيل ثنائي، مما يجعله أسرع في الفتح وأصغر على القرص. جميع الخصائص المخصصة تُحفظ تلقائيًا.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

استبدل `"WithCustomProps.xlsb"` بمسار مطلق إذا كنت بحاجة إلى الملف في دليل محدد. تعداد `SaveFormat.XLSB` يخبر Aspose.Cells بكتابة التنسيق الثنائي.

## الخطوة 6: التحقق من الناتج

شغّل البرنامج من بيئة التطوير المتكاملة IDE أو سطر الأوامر:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

يجب أن ترى:

```
ProjectId = 12345
```

افتح `WithCustomProps.xlsb` في Excel. انتقل إلى **File → Info → Properties → Advanced Properties → Custom**. سيظهر الإدخال `ProjectId` بالقيمة `12345`، مما يؤكد أن خطوة **add custom property excel** نجحت وأن عملية **save workbook as xlsb** احتفظت بالبيانات الوصفية.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت لتخزين خاصية سلسلة؟

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

استرجعها باستخدام:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### هل يمكنني إضافة عدة خصائص مخصصة مرة واحدة؟

نعم. استدعِ `add` بشكل متكرر لكل زوج اسم/قيمة. لا يحد Aspose.Cells عدد الخصائص المخصصة، لكن احرص على أن يكون الحجم الإجمالي معقولًا لتجنب زيادة حجم الملف.

### كيف يؤثر التنسيق الثنائي على الأداء؟

ملفات XLSB تُحمَّل أسرع لأنها تتجنب تحليل XML. هذا واضح خصوصًا في المصنفات التي تحتوي على الكثير من الصفوف أو الصيغ أو الصور المدمجة.

### ماذا لو احتجت للعمل مع ملف XLSX موجود؟

استبدل مُنشئ `new Workbook()` بـ `new Workbook("ExistingFile.xlsx")`. بقية الخطوات (إضافة الخصائص، حفظ كـ XLSB) تبقى كما هي.

## الكود المصدر الكامل

فيما يلي المثال الكامل الجاهز للتنفيذ. انسخه في ملف باسم `CustomPropertiesXlsb.java` داخل مجلد `src/main/java` الخاص بك.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

تشغيل هذه الفئة ينتج ملف XLSB يحتوي على الخاصية المخصصة ويمكن فتحه في أي نسخة حديثة من Microsoft Excel.

## الخلاصة

أنت الآن تعرف كيف تقوم بـ **create new workbook Aspose**، **add custom property Excel**، و**save workbook as XLSB** باستخدام Java. يوضح المثال دورة الحياة الكاملة: التهيئة، حقن البيانات الوصفية، التحقق، والتسلسل الثنائي.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **setting document properties**، **working with Excel formulas**، أو **converting between XLSX and XLSB**. كلٌ منها يبني على نفس Aspose.Cells API الذي استخدمته للتو، لذا يمكنك توسيع الحل دون الحاجة لتعلم مكتبات جديدة.

لا تتردد في تجربة أنواع بيانات مختلفة، أوراق عمل متعددة، أو حماية بكلمة مرور—Aspose.Cells يدعم كل هذه السيناريوهات مباشرة. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء وحفظ مصنف Excel باستخدام Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [كيفية إنشاء وحفظ مصنف Excel كملف SVG باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [إنشاء مصنف Excel وإضافة تسميات باستخدام Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}