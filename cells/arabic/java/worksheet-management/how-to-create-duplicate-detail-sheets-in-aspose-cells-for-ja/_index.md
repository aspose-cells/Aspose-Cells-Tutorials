---
category: general
date: 2026-08-17
description: تعلم كيفية إنشاء أوراق تفاصيل مكررة باستخدام Aspose.Cells للغة Java والسماح
  بأسماء أوراق مكررة باستخدام SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: ar
lastmod: 2026-08-17
og_description: إنشاء أوراق تفاصيل مكررة في Aspose.Cells للغة Java والسماح بأسماء
  أوراق مكررة. اتبع هذا الدرس الكامل للحصول على نتائج فورية.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: إنشاء أوراق تفاصيل مكررة في Aspose.Cells for Java – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: كيفية إنشاء أوراق تفاصيل مكررة في Aspose.Cells للغة Java
url: /ar/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء أوراق تفاصيل مكررة في Aspose.Cells for Java

إذا كنت بحاجة إلى **إنشاء أوراق تفاصيل مكررة** في مصنف Excel، فإن Aspose.Cells for Java يجعل ذلك بسيطًا. يوضح هذا الدرس بالضبط كيفية السماح بأسماء أوراق مكررة أثناء إنشاء أوراق التفاصيل باستخدام SmartMarkerProcessor، بحيث يمكنك إنتاج مصنف يحتوي على عدة أوراق تشترك في نفس الاسم.

سترى مثالًا كاملاً قابلاً للتنفيذ، وتحليلًا لكل خيار تكوين، ونصائح للتعامل مع الحالات الشائعة مثل تصادم الأسماء ومجموعات البيانات الكبيرة. لا توجد مراجع خارجية مطلوبة—كل ما تحتاجه مضمّن في الشيفرة أدناه.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود:

* مجموعة تطوير جافا (JDK) 8 أو أحدث.
* Maven أو Gradle لإدارة التبعيات.
* مكتبة Aspose.Cells for Java (الإصدار 23.9 أو أحدث). أضف تبعية Maven التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* قالب مصنف رئيسي (`master_template.xlsx`) يحتوي على منطقة Smart Marker لبيانات التفاصيل.

## نظرة عامة على الحل

يتبع الحل أربع خطوات منطقية:

1. تحميل قالب المصنف الرئيسي.
2. تكوين `SmartMarkerProcessor` **للسماح بأسماء أوراق مكررة**.
3. معالجة المصنف لإنشاء ورقة تفاصيل جديدة لكل مجموعة بيانات.
4. حفظ المصنف الناتج الذي يحتوي الآن على أوراق تفاصيل مكررة.

يتم شرح كل خطوة بالتفصيل أدناه، ويتم توفير ملف المصدر الكامل في نهاية الدليل.

## الخطوة 1: تحميل قالب المصنف الرئيسي

العملية الأولى تنشئ كائن `Workbook` يمثل ملف القالب. يجب أن يحتوي القالب على عنصر نائب Smart Marker (مثل `&=DetailData`) يحدد للمعالج مكان إدراج البيانات.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**لماذا هذا مهم:** تحميل القالب يعزل التخطيط والتنسيق عن منطق توليد البيانات، مما يبقي الشيفرة نظيفة ويسهل إعادة استخدام نفس القالب لمجموعات بيانات مختلفة.

## الخطوة 2: تكوين SmartMarkerProcessor للسماح بأسماء أوراق مكررة

بشكل افتراضي، يولد Aspose.Cells أسماء أوراق فريدة عند إنشاء أوراق التفاصيل. لـ **السماح بأسماء أوراق مكررة**، اضبط خيار `DetailSheetNewName` على قيمة ثابتة. سيعيد المعالج استخدام هذا الاسم لكل ورقة يتم إنشاؤها.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**لماذا هذا مهم:** ضبط `DetailSheetNewName` يخبر المحرك بإعادة استخدام نفس الاسم لكل ورقة تفاصيل، وهو ما يلبي مباشرةً المتطلب **السماح بأسماء أوراق مكررة**. هذا النهج مفيد عندما تعتمد الأدوات اللاحقة على موقع الورقة بدلاً من اسمها.

## الخطوة 3: معالجة المصنف لإنشاء أوراق التفاصيل

بعد التكوين، استدعِ `process` على المصنف. يقرأ المعالج منطقة Smart Marker، ينشئ ورقة جديدة لكل مجموعة بيانات، ويملأها بالصفوف المقابلة.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**لماذا هذا مهم:** استدعاء `process` يقوم بالعمل الشاق—تحليل Smart Markers، استنساخ ورقة القالب، وإدخال البيانات. بما أن خيار `DetailSheetNewName` تم ضبطه مسبقًا، فإن كل ورقة جديدة تحصل على نفس الاسم، مما ينتج عنه أسماء أوراق مكررة في الملف النهائي.

## الخطوة 4: حفظ المصنف الناتج

أخيرًا، اكتب المصنف المعدل إلى ملف جديد. سيحتوي ملف الإخراج على عدد من علامات “DetailSheet” يساوي عدد مجموعات البيانات.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**لماذا هذا مهم:** حفظ الملف ينهى التغييرات التي أجراها المعالج. يمكن فتح المصنف الناتج في Microsoft Excel أو LibreOffice أو أي تطبيق جداول يدعم تنسيق XLSX.

## الشيفرة المصدرية الكاملة

بدمج جميع الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### النتيجة المتوقعة

عند فتح `duplicate_detail.xlsx`، ستلاحظ وجود عدة علامات باسم **DetailSheet**. كل علامة تحتوي على مجموعة البيانات التي توافق مجموعة Smart Marker معينة في القالب. يتم الحفاظ على التخطيط والتنسيق والصيغ من القالب الرئيسي في كل ورقة مكررة.

## التعامل مع المشكلات الشائعة

| المشكلة | الشرح | الحل |
|-------|-------------|--------|
| Excel يعرض تحذيرًا حول أسماء الأوراق المكررة | يسمح Excel بالأسماء المكررة لكنه قد يظهر تحذيرًا عند فتح الملف. | التحذير غير ضار؛ يعمل المصنف بشكل صحيح. إذا رغبت في إخفاء التحذير، أعد تسمية الأوراق بعد المعالجة باستخدام `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| مجموعات البيانات الكبيرة تستهلك ذاكرة عالية | كل ورقة مكررة تنشئ نسخة كاملة من القالب، مما قد يستهلك RAM. | فعّل وضع البث باستخدام `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` قبل تحميل القالب. |
| لم يتم العثور على منطقة Smart Marker | المعالج لا يستطيع تحديد `&=DetailData` في القالب. | تحقق من أن بناء الجملة للعنصر النائب يتطابق مع مصدر البيانات وأن ورقة القالب غير مخفية. |

## نصيحة احترافية: تخصيص نمط تسمية المكررات

إذا كنت بحاجة إلى نمط تسمية متوقع مع السماح بالمكررات، اجمع اسم أساسي مع فهرس:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

يتم استبدال العنصر النائب `{0}` بفهرس الورقة، مما ينتج أسماء مثل `DetailSheet_1`، `DetailSheet_2`، إلخ. هذا لا يزال يفي بمتطلب **السماح بأسماء أوراق مكررة** لأن الاسم الأساسي يبقى ثابتًا.

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **إنشاء أوراق تفاصيل مكررة**، يمكنك استكشاف المواضيع التالية:

* **ملء أوراق التفاصيل بالصور** – استخدم كائنات `Picture` لإدراج شعارات أو مخططات.
* **تطبيق التنسيق الشرطي** – أضف قواعد `FormatCondition` لتسليط الضوء على الصفوف بناءً على القيم.
* **التصدير إلى PDF** – استدعِ `workbook.save("output.pdf", SaveFormat.PDF);` لإنشاء نسخة PDF من الأوراق المكررة.

كل من هذه الإضافات يبني على نفس سير عمل Smart Marker الموضح هنا، مما يتيح لك أتمتة تقارير Excel المعقدة بثقة.

---

*لقد تعلمت كيفية إنشاء أوراق تفاصيل مكررة في Aspose.Cells for Java وكيفية السماح بأسماء أوراق مكررة باستخدام SmartMarkerProcessor. طبّق الشيفرة، عدّل القالب، ودمج التقنية في خطوط تقاريرك.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء والوصول إلى أوراق Excel، إضافة إشارات PDF باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [إنشاء والوصول إلى أوراق Excel وإضافة إشارات PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [إنشاء والوصول إلى أوراق Excel وإضافة إشارات PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}