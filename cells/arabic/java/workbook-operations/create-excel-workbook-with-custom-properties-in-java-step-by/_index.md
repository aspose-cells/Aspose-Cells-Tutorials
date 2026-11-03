---
category: general
date: 2026-08-04
description: إنشاء مصنف إكسل في جافا وتعلم كيفية إضافة خاصية مخصصة مثل المؤلف. اتبع
  هذا الدليل الكامل لتعيين الخصائص وحفظ الملف بصيغة XLSB.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add custom property
- how to add author
- how to set property
- add author excel
language: ar
lastmod: 2026-08-04
og_description: إنشاء مصنف إكسل في جافا، ثم تعلم كيفية إضافة المؤلف وخصائص مخصصة أخرى.
  يوضح هذا الدليل الشيفرة الدقيقة ويشرح كل خطوة.
og_image_alt: Screenshot of a Java IDE displaying code that creates an Excel workbook
  and adds a custom author property
og_title: إنشاء مصنف إكسل بخصائص مخصصة – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create Excel workbook in Java and learn how to add custom property
    like author. Follow this complete tutorial to set properties and save as XLSB.
  headline: Create Excel workbook with custom properties in Java – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- Java
- Aspose.Cells
- Custom Properties
- Workbook
title: إنشاء مصنف إكسل بخصائص مخصصة في جافا – دليل خطوة بخطوة
url: /ar/java/workbook-operations/create-excel-workbook-with-custom-properties-in-java-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel بخصائص مخصصة في Java – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إنشاء مصنف Excel** برمجيًا، فإن هذا الدليل يوضح لك بالضبط كيفية ذلك. ستتعرف على كيفية إضافة خاصية مخصصة مثل المؤلف، حفظ الملف كمصنف XLSB، والتحقق من بقاء الخاصية.

التعامل مع ملفات Excel من Java غالبًا ما يتطلب أكثر من مجرد البيانات – فالميتا بيانات مثل المؤلف، اسم المشروع، أو الإصدار يمكن أن تكون حاسمة للعمليات اللاحقة. في هذا الدليل ستتعلم **إضافة خاصية مخصصة**، وفهم **كيفية تعيين قيم الخاصية**، واكتشاف أفضل طريقة لـ **كيفية إضافة معلومات المؤلف** إلى مصنف Excel.

## المتطلبات المسبقة

* تثبيت Java 17 أو أحدث  
* Maven أو Gradle لإدارة التبعيات  
* رخصة Aspose.Cells for Java (التقييم المجاني يعمل للاختبار)  

هذه المتطلبات تضمن تشغيل الكود دون إعداد إضافي.

## الخطوة 1: إعداد تبعية Aspose.Cells

أضف مكتبة Aspose.Cells إلى مشروعك. باستخدام Maven، أدرج:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

إذا كنت تفضل Gradle:

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

> **نصيحة احترافية:** حافظ على تحديث المكتبة؛ الإصدارات الأحدث تضيف دعمًا لصيغ Excel إضافية وتحسن الأداء.

## الخطوة 2: إنشاء مصنف Excel

الكتلة المنطقية الأولى هي **إنشاء مصنف Excel**. هذا الكائن يمثل الملف بالكامل ويمنحك الوصول إلى الأوراق، الأنماط، والخصائص.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {

    public static void main(String[] args) throws Exception {
        // Step 2‑1: Initialize a new workbook (this creates a default worksheet)
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.setName("Report");
```

إنشاء المصنف هو الأساس؛ بدون ذلك لا يمكنك إضافة أي ميتا بيانات مخصصة. كما توفر فئة `Workbook` مجموعة `getCustomProperties()` التي تخزن أزواج المفتاح‑القيمة.

## الخطوة 3: إضافة خاصية مخصصة – كيفية إضافة المؤلف

الآن نتناول **كيفية إضافة المؤلف** إلى المصنف. المؤلف هو مجرد خاصية مخصصة باسم `"Author"`.

```java
        // Step 3‑1: Access the custom properties collection
        CustomDocumentPropertyCollection props = workbook.getWorksheets().getCustomProperties();

        // Step 3‑2: Add the "Author" property with the value "Alice"
        props.add("Author", "Alice");

        // Verify that the property was added (helps during debugging)
        System.out.println("Added property: Author = " + props.get("Author").getValue());
```

الطريقة `add(String name, Object value)` هي الطريقة القياسية لـ **إضافة خاصية مخصصة**. يمكنك تخزين سلاسل نصية، أرقام، تواريخ، أو قيم منطقية. السطر أعلاه يوضح **كيفية تعيين خاصية** لقيمة نصية بسيطة.

### كيفية إضافة مؤلف Excel – طرق بديلة

* **استخدام خصائص المستند المدمجة:** تدعم Aspose.Cells أيضًا خصائص مدمجة مثل `Author`.  
  ```java
  workbook.getBuiltInDocumentProperties().setAuthor("Alice");
  ```
* **مؤلفون متعددون:** إذا كنت بحاجة إلى قائمة، احفظ سلسلة مفصولة أو استخدم حمولة JSON مخصصة.  
  ```java
  props.add("Authors", "Alice;Bob;Charlie");
  ```

كلا النهجين صالحان؛ مسار الخاصية المخصصة يمنحك تحكمًا كاملاً في التسمية ونوع البيانات.

## الخطوة 4: حفظ المصنف بصيغة XLSB

حفظ الملف بصيغة ثنائية (XLSB) يحافظ على الخاصية المخصصة مع الحفاظ على حجم الملف صغيرًا.

```java
        // Step 4‑1: Define the output path
        String outputPath = "output/CustomProp.xlsb";

        // Step 4‑2: Save using the XLSB format
        workbook.save(outputPath, SaveFormat.XLSB);

        System.out.println("Workbook saved to " + outputPath);
    }
}
```

عند فتح `CustomProp.xlsb` في Excel وتفقد **File → Info → Properties**، سترى إدخال **Author** الذي أضفته. هذا يؤكد أن عملية **add author excel** نجحت.

## كيفية قراءة خاصية مخصصة (التحقق)

أحيانًا تحتاج إلى قراءة القيمة مرة أخرى للتحقق منها أو عرضها في واجهة المستخدم.

```java
        // Load the workbook we just saved
        Workbook loaded = new Workbook(outputPath);

        // Retrieve the custom property
        CustomDocumentProperty authorProp = loaded.getWorksheets().getCustomProperties().get("Author");
        if (authorProp != null) {
            System.out.println("Loaded Author: " + authorProp.getValue());
        } else {
            System.out.println("Author property not found.");
        }
```

هذا المقتطف يوضح **كيفية تعيين خاصية** ثم قراءتها، مما يثبت أن الميتا بيانات نجت من دورة الحفظ/التحميل.

## المشكلات الشائعة والحالات الحدية

| المشكلة | سبب حدوثها | الحل |
|---------|------------|------|
| **تعارض اسم الخاصية** | إضافة خاصية باسم موجود مسبقًا يستبدل القيمة القديمة. | تحقق من `containsKey(name)` قبل `add`، أو استخدم `props.get(name).setValue(newValue)`. |
| **نوع بيانات غير مدعوم** | تمرير كائن لا يمكن لـ Aspose.Cells تسلسله (مثل فئة مخصصة). | حوّل القيمة إلى نوع مدعوم (`String`, `Integer`, `Date`, `Boolean`). |
| **الحفظ في مجلد للقراءة فقط** | `IOException` عند `workbook.save`. | تأكد من وجود الدليل الهدف وأن العملية لديها أذونات كتابة. |
| **استخدام نسخة قديمة من Aspose.Cells** | تم إضافة بعض الصيغ مثل XLSB في إصدارات لاحقة. | قم بالترقية إلى أحدث نسخة (كما هو موضح في كتلة التبعيات). |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله بعد إضافة تبعية Maven/Gradle.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {

    public static void main(String[] args) throws Exception {
        // 1. Create a new workbook (create excel workbook)
        Workbook workbook = new Workbook();

        // 2. Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        worksheet.setName("Report");

        // 3. Add a custom property – how to add author
        CustomDocumentPropertyCollection customProps = workbook.getWorksheets().getCustomProperties();
        customProps.add("Author", "Alice");               // add custom property
        System.out.println("Added property: Author = " + customProps.get("Author").getValue());

        // 4. Save as XLSB (preserves the custom property)
        String outputPath = "output/CustomProp.xlsb";
        workbook.save(outputPath, SaveFormat.XLSB);
        System.out.println("Workbook saved to " + outputPath);

        // 5. Load the workbook again to verify the property (how to set property)
        Workbook loaded = new Workbook(outputPath);
        CustomDocumentProperty author = loaded.getWorksheets().getCustomProperties().get("Author");
        if (author != null) {
            System.out.println("Loaded Author: " + author.getValue());
        } else {
            System.out.println("Author property not found.");
        }
    }
}
```

**الناتج المتوقع**

```
Added property: Author = Alice
Workbook saved to output/CustomProp.xlsb
Loaded Author: Alice
```

عند فتح `CustomProp.xlsb` في Microsoft Excel، تظهر الخاصية المخصصة **Author** تحت **File → Info → Properties**.

## الخلاصة

أنت الآن تعرف كيفية **إنشاء مصنف Excel** في Java، **إضافة خاصية مخصصة**، وبشكل خاص **كيفية إضافة مؤلف** كميتا بيانات. يغطي الدليل سير العمل الكامل — من إعداد التبعيات، مرورًا بإنشاء الخاصية، إلى الحفظ والتحقق — بحيث يمكنك دمج هذا النمط في أي مشروع تقارير أو أتمتة.

**الخطوات التالية**

* استكشف **كيفية تعيين خاصية** للتواريخ، الأرقام، أو العلامات المنطقية.  
* استخدم التقنية نفسها لتخزين نسخة المستند أو معرف فريد (`add custom property` “DocId”).  
* دمج الخصائص المخصصة مع **خصائص Aspose.Cells المدمجة** للحصول على ميتا بيانات أغنى.  

لا تتردد في تجربة أسماء خصائص مختلفة، أوراق عمل متعددة، وصيغ ملفات أخرى مثل XLSX أو CSV. إضافة الميتا بيانات مبكرًا في خط الأنابيب تجعل المعالجة اللاحقة، التدقيق، وتجربة المستخدم أكثر سلاسة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف Excel وإضافة تسميات باستخدام Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [كيفية إضافة أوراق عمل في Excel باستخدام Aspose.Cells for Java: دليل كامل](/cells/english/java/worksheet-management/add-spreadsheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}