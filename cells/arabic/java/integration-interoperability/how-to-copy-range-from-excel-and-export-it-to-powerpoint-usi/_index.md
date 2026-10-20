---
category: general
date: 2026-09-05
description: تعلم كيفية نسخ النطاق في Excel، وتصدير Excel إلى PowerPoint، وتحويل Excel
  إلى pptx مع مثال Java كامل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: ar
lastmod: 2026-09-05
og_description: كيفية نسخ النطاق وتصدير Excel إلى PowerPoint باستخدام Java. اتبع هذا
  الدليل خطوة بخطوة لتحويل Excel إلى PPTX بكفاءة.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: كيفية نسخ نطاق من Excel وتصديره إلى PowerPoint باستخدام Java
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: كيفية نسخ نطاق من Excel وتصديره إلى PowerPoint باستخدام Java
url: /ar/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ نطاق من Excel وتصديره إلى PowerPoint باستخدام Java

إذا كنت بحاجة إلى **كيفية نسخ نطاق** من مصنف Excel ثم **تصدير Excel إلى PowerPoint**، فإن هذا الدليل يزودك بحل كامل وجاهز للتنفيذ. سترى بالضبط كيفية نسخ نطاق يحتوي على جدول محوري، وإنشاء ورقة عمل جديدة للنسخة، وأخيرًا **تحويل Excel إلى PPTX** باستدعاء طريقة واحدة.

نسخ النطاقات وتصدير المصنفات هو طلب شائع عندما تقوم بإنشاء تقارير أو عروض شرائح أو لوحات معلومات برمجيًا. بنهاية هذا البرنامج التعليمي ستحصل على برنامج Java يقوم بـ:

* تحميل ملف `.xlsx` موجود.
* نسخ النطاق `A1:H20` (بما في ذلك جدول محوري) إلى ورقة جديدة.
* حفظ المصنف كعرض تقديمي `.pptx` قابل للتحرير.

أنت بحاجة فقط إلى مكتبة Aspose.Cells for Java؛ لا توجد تبعيات إضافية مطلوبة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود:

* Java 17 (أو أحدث) مثبتة.
* Maven أو Gradle لإدارة التبعيات.
* Aspose.Cells for Java 23.9 (أو أحدث نسخة) – أضفها إلى مشروعك كما هو موضح في مقتطف Maven أدناه.
* ملف Excel (`input.xlsx`) يحتوي على البيانات والجدول المحوري الذي تريد نسخه.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## الخطوة 1: تحميل المصنف من ملف

العملية الأولى في **كيفية نسخ نطاق** هي فتح المصنف المصدر. هذا يمنحك الوصول إلى أوراق العمل والخلايا والجداول المحورية.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*لماذا هذه الخطوة؟*  
تحميل الملف ينشئ تمثيلًا في الذاكرة لوثيقة Excel، مما يتيح لك تعديل محتواها دون لمس الملف الأصلي.

## الخطوة 2: الحصول على ورقة العمل المصدر التي تحتوي على البيانات

عادةً ما تكون الورقة الأولى هي التي تحتوي على البيانات التي تريد نسخها. يمكنك استرجاعها حسب الفهرس.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

إذا كان المصنف يخزن الجدول المحوري في ورقة مختلفة، استبدل `0` بالفهرس المناسب أو استخدم `get("SheetName")`.

## الخطوة 3: إضافة ورقة عمل جديدة للنطاق المنسوخ

إنشاء ورقة وجهة يعزل البيانات المنسوخة ويجعل عملية التصدير لاحقًا أكثر نظافة.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

يمكنك تسمية الورقة بأي اسم تفضله؛ الاسم “Copy” يوضح بوضوح أنها تحمل النطاق المكرر.

## الخطوة 4: نسخ النطاق (كيفية نسخ نطاق) بما يشمل الجدول المحوري

الآن نقوم بتنفيذ العملية الأساسية **كيفية نسخ نطاق**. طريقة `copyRange` تنسخ القيم والتنسيق، وتحتفظ بتعريف الجدول المحوري.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*لماذا نستخدم `CopyOptions`؟*  
توفير كائن `CopyOptions` يتيح لك ضبط ما يتم نسخه (مثل الصيغ، عرض الأعمدة). المنشئ الافتراضي ينسخ كل شيء، وهو مثالي عندما تريد نسخة مطابقة تمامًا من **ورقة جدول محوري منسوخة**.

## الخطوة 5: إعداد الخيارات لتصدير المصنف كعرض PowerPoint قابل للتحرير

التصدير إلى PowerPoint يتم عبر `ImageOrPrintOptions`. ضبط صيغة الحفظ إلى `SaveFormat.PPTX` يخبر Aspose.Cells بإنشاء ملف PowerPoint بدلاً من صورة.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

يمكنك أيضًا تعديل أبعاد الشريحة، DPI، وإعدادات العرض الأخرى عبر `pptOptions` إذا كنت بحاجة إلى تخطيط مخصص.

## الخطوة 6: حفظ المصنف كملف PPTX (تحويل excel إلى pptx)

أخيرًا، استدعِ `workbook.save` مع خيارات PPTX. هذه الخطوة **كيفية تصدير excel** إلى مجموعة شرائح.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

بعد انتهاء البرنامج، سيحتوي `output.pptx` على شريحة واحدة حيث يظهر النطاق المنسوخ تمامًا كما كان في Excel، بما في ذلك عناصر التحكم في الجدول المحوري.

### النتيجة المتوقعة

افتح `output.pptx` في Microsoft PowerPoint أو أي عارض متوافق. يجب أن ترى شريحة واحدة تعرض النطاق `A1:H20` مع الحفاظ على ألوان الخلايا والحدود وتخطيط الجدول المحوري. الشريحة قابلة للتحرير بالكامل—يمكنك نقلها أو تغيير حجمها أو تنسيق الجدول كما تشاء كأي محتوى PowerPoint أصلي.

## مثال كامل قابل للتنفيذ

جمع جميع الخطوات معًا يمنحك فئة Java مستقلة:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

شغّل الفئة من بيئة التطوير المتكاملة أو عبر سطر الأوامر:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

ستظهر رسالة تأكيد بمجرد كتابة الملف.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني نسخ نطاق غير متصل؟** | استخدم `copyRange` مع نطاق مسمى يشمل مناطق متعددة، أو استدعِ `copyRange` عدة مرات لكل كتلة. |
| **ماذا لو احتوت ورقة المصدر على جداول محورية متعددة؟** | يتم نقل كل جدول محوري داخل المستطيل المنسوخ. بالنسبة للجداول خارج المستطيل، انسخها بشكل منفصل. |
| **كيف يمكنني تصدير عدة أوراق كشرائح منفصلة؟** | قم بالتكرار عبر أوراق العمل، انسخ كل واحدة إلى ورقة مؤقتة، واستدعِ `workbook.save` مع `pptOptions` لكل تكرار، مع إلحاقها إلى نفس ملف PPTX عبر واجهة `Presentation` API. |
| **هل الـ PPTX الناتج قابل للتحرير؟** | نعم. عملية التصدير تنشئ كائنات PowerPoint أصلية، لذا يمكنك تعديل النص، إعادة تشكيل الجداول، أو إضافة حركات بعد الإنشاء. |
| **ماذا عن المصنفات الكبيرة؟** | زد `pptOptions.setDpi(300)` للحصول على دقة أعلى، لكن كن على علم باستهلاك الذاكرة؛ عالج الأوراق على دفعات إذا لزم الأمر. |

## نصائح احترافية

* **الحفاظ على عرض الأعمدة** – اضبط `CopyOptions.setColumnWidth(true)` قبل النسخ إذا كنت تحتاج إلى مطابقة دقيقة للعرض.
* **استخدام حجم شريحة مخصص** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` لتتناسب مع عرض تقديمي بنسبة 16:9.
* **إضافة شريحة عنوان** – بعد التصدير، افتح ملف PPTX باستخدام Aspose.Slides وأضف شريحة عنوان وتاريخ في البداية.

## الخلاصة

أنت الآن تعرف **كيفية نسخ نطاق** من مصنف Excel، **تصدير Excel إلى PowerPoint**، و**تحويل Excel إلى PPTX** باستخدام Java. باتباع الخطوات الست المذكورة أعلاه يمكنك أتمتة إنشاء التقارير، وإعداد عروض شرائح من بيانات حية، والحفاظ على وظائف الجدول المحوري.

### ما التالي؟

* استكشف تنويعات **نسخ ورقة جدول محوري** مثل نسخ ذاكرة التخزين المؤقت للجدول فقط.
* دمج هذا التدفق مع **Aspose.Slides** لإضافة حركات أو علامات تجارية مخصصة.
* أتمتة المعالجة الدفعية لعشرات المصنفات في مهمة مجدولة.

لا تتردد في تجربة الخيارات وتكييف الكود مع خط أنابيب التقارير الخاص بك. إذا واجهت أي مشاكل، فإن وثائق Aspose.Cells for Java توفر رؤى أعمق حول `CopyOptions` و `ImageOrPrintOptions`. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}