---
category: general
date: 2026-08-04
description: نسخ جدول محوري باستخدام Aspose.Cells للغة Java. تعلم كيفية نسخ نطاق Excel،
  تكرار الجدول المحوري، ونسخ ورقة العمل التي تحتوي على جدول محوري في بضع أسطر فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: ar
lastmod: 2026-08-04
og_description: نسخ جدول محوري باستخدام Aspose.Cells للغة Java. يوضح هذا البرنامج
  التعليمي كيفية نسخ نطاق Excel، وتكرار جدول محوري، والحفاظ على جميع البيانات في ورقة
  عمل جديدة.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: نسخ جدول محوري في جافا – دليل كامل لـ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: نسخ جدول محوري في جافا – دليل خطوة بخطوة باستخدام Aspose.Cells
url: /ar/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري في Java – دليل خطوة بخطوة باستخدام Aspose.Cells

إذا كنت بحاجة إلى **نسخ جدول محوري** من ورقة عمل إلى أخرى في Java، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells. سواءً كنت تُنشئ تقارير برمجياً أو تبني أداة هجرة بيانات، سترى مثالًا كاملاً قابلاً للتنفيذ يحافظ على تعريف الجدول المحوري وبياناته.

نسخ جدول محوري هو أكثر من مجرد نسخ نطاق خلايا؛ يجب أن يبقى التخزين المؤقت (cache) ومصدر البيانات الأساسيان سليمين. في هذا الشرح نغطي أيضًا كيفية **نسخ نطاق إكسل**، وكيفية **تكرار جدول محوري** عبر أوراق العمل، وكيفية **نسخ ورقة عمل مع جدول محوري** باستخدام نفس الـ API.

## المتطلبات المسبقة

* Java Development Kit (JDK) 8 أو أحدث.
* Maven أو Gradle لإدارة التبعيات.
* Aspose.Cells for Java (أحدث إصدار، مثلاً 23.12). أضف إحداثيات Maven التالية إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* مصنف مصدر (`Source.xlsx`) يحتوي على جدول محوري في ورقة العمل الأولى.

## كيفية نسخ جدول محوري في Java باستخدام Aspose.Cells

الفكرة الأساسية هي نسخ *النطاق المصدر* الذي يحيط بالجدول المحوري ثم لصقه في ورقة عمل جديدة. تقوم Aspose.Cells بنسخ التخزين المؤقت للجدول المحوري تلقائيًا، لذا فإن الورقة الناتجة تحتوي على **جدول محوري مكرر** يعمل بالكامل.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### لماذا يعمل هذا

* **نسخ النطاق يتضمن التخزين المؤقت للجدول المحوري** – تعتبر Aspose.Cells الجدول المحوري ككائن خاص مدمج في نطاق الخلايا. عندما تستدعي `Range.copy`، تقوم المكتبة بنسخ كل من الخلايا الظاهرة والتخزين المؤقت المخفي الذي يُشغّل الجدول المحوري.
* **لا حاجة لإعادة إنشاء يدوية** – لا تحتاج إلى إعادة بناء حقول الجدول المحوري أو مصدر البيانات؛ النسخة المكررة جاهزة للتحديث فورًا.
* **يعمل مع أي نسخة من Excel** – الملف المُنتج يتبع معيار Office Open XML (XLSX)، لذا يمكن لـ Excel 2007+ فتحه دون تحذيرات.

## نسخ نطاق إكسل – إعادة استخدام نفس الكود للبيانات غير المحورية

إذا كنت تحتاج فقط إلى **نسخ نطاق إكسل** دون جدول محوري، ينطبق النمط نفسه. فقط عدل عنوان النطاق إلى المنطقة التي تريد تكرارها.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

طريقة `copy` تحافظ على الصيغ، التنسيق، والتعليقات، مما يجعلها حلاً عالميًا لأي كتلة من بيانات Excel.

## تكرار جدول محوري عبر عدة أوراق عمل

أحيانًا تحتاج إلى **تكرار جدول محوري** عدة مرات—مثلاً، واحد لكل قسم. قم بالتكرار عبر أوراق العمل الوجهة وأعد استخدام نفس استدعاء `sourceRange.copy`:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

كل ورقة جديدة تحتوي على جدول محوري مستقل يمكن تحديثه بشكل منفصل. يتم تكرار التخزين المؤقت، لذا فإن التغييرات في ورقة واحدة لن تؤثر على الأخريات.

## نسخ ورقة عمل مع جدول محوري – الحفاظ على إعدادات المستوى الورقي

إذا كنت تريد **نسخ ورقة عمل مع جدول محوري** مع الحفاظ أيضًا على إعدادات الصفحة، عرض الأعمدة، والنطاقات المسماة، استخدم `Worksheet.copy` بدلاً من نسخ النطاق يدويًا. هذه الطريقة تستنسخ الورقة بالكامل، بما في ذلك الجدول المحوري.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` مفيدة عندما تحتوي ورقة العمل على مخططات، صور، أو أنماط مخصصة يجب أن تنتقل مع الجدول المحوري.

## الأخطاء الشائعة وكيفية تجنّبها

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **فقدان التخزين المؤقت للجدول المحوري بعد النسخ** | استخدام `Cell.copy` على خلايا فردية (بدلاً من نطاق) يتجاهل التخزين المؤقت المخفي. | دائمًا قم بنسخ *النطاق الكامل* الذي يحيط بالجدول المحوري، كما هو موضح في الخطوة 2. |
| **النطاق المصدر صغير جدًا** | النطاق لا يشمل منطقة بيانات الجدول المحوري، لذا تظهر الورقة الجديدة قيمًا ثابتة فقط. | قم بتوسيع العنوان (مثال: `A1:G20`) لتغطية الجدول المحوري بالكامل بالإضافة إلى أي مقاطع أو فلاتر. |
| **عدم توافق نسخة المصنف الوجهة** | حفظ الملف كـ XLS (قديم) يؤدي إلى فقدان ميزات الجداول المحورية الحديثة. | احفظ كـ XLSX (الافتراضي) أو اضبط صراحةً `SaveFormat.XLSX`. |
| **انكسار مصدر البيانات الخارجي** | الجدول المحوري يشير إلى مصدر بيانات خارج المصنف؛ النسخ لا يدمجه. | استخدم `PivotTable.refreshData()` بعد النسخ، أو دمج بيانات المصدر في نفس المصنف. |

## النتيجة المتوقعة

بعد تشغيل البرنامج:

1. يظهر الملف `CopyWithPivot.xlsx` في `YOUR_DIRECTORY`.
2. عند فتح الملف في Excel يظهر ورقة جديدة باسم **CopySheet**.
3. تحتوي **CopySheet** على جدول محوري يعمل بالكامل ومطابق للأصل، جاهز للتحديث.
4. جميع التنسيقات، الفلاتر، والحقول المحسوبة محفوظة.

إذا فتحت `FullCopy.xlsx`، سترى نسخة كاملة من ورقة العمل الأصلية، بما في ذلك أي مخططات أو صور كانت على ورقة المصدر.

## ملخص

* تعلمت كيفية **نسخ جدول محوري** في Java باستخدام Aspose.Cells.
* نفس النهج يعمل لسيناريوهات **نسخ نطاق إكسل** أو **copy range java** العادية.
* للعمليات الضخمة، يمكنك **تكرار جدول محوري** عبر عدة أوراق.
* عندما تحتاج إلى النسخة الكاملة من الورقة، **نسخ ورقة عمل مع جدول محوري** باستخدام `addCopy`.

## الخطوات التالية

* استكشف **PivotTable.refreshData()** لتحديث التخزين المؤقت برمجيًا بعد النسخ.
* دمج منطق النسخ مع **Excel file streaming** للتعامل مع مصنفات كبيرة دون تحميل كل شيء في الذاكرة.
* اطلع على دعم Aspose.Cells لـ **pivot slicers** إذا كانت تقاريرك تعتمد على الفلاتر التفاعلية.

لا تتردد في تعديل الكود ليتناسب مع بنية مشروعك، تجربة أحجام نطاق مختلفة، أو دمجه في خط معالجة بيانات أكبر. برمجة سعيدة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحديث مصدر جدول محوري في Excel باستخدام Aspose.Cells لـ Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [معالجة جدول محوري في Excel باستخدام Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [إنشاء مصنف Excel جديد – نسخ وتكرار جدول محوري](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}