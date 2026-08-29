---
category: general
date: 2026-08-17
description: كيفية تكرار ورقة العمل في Java باستخدام Aspose.Cells مع الحفاظ على جدول
  المحور، نسخ جدول المحور إلى مصنف جديد، وإنشاء مصنف من ورقة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: ar
lastmod: 2026-08-17
og_description: كيفية تكرار ورقة العمل في جافا باستخدام Aspose.Cells مع الحفاظ على
  جدول المحور، نسخ جدول المحور إلى مصنف جديد، وإنشاء مصنف من ورقة—جميع الخطوات موضحة.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: كيفية تكرار ورقة العمل مع الحفاظ على جداول المحور – دليل جافا
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: كيفية تكرار ورقة العمل والحفاظ على الجداول المحورية في جافا
url: /ar/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار ورقة العمل والحفاظ على جداول Pivot في Java

تكرار ورقة العمل مع الحفاظ على جدول Pivot الخاص بها هو حاجة متكررة عند أتمتة تقارير Excel. يوضح هذا الدليل كيفية نسخ Pivot إلى مصنف جديد باستخدام Aspose.Cells for Java، كما يغطي كيفية الحفاظ على Pivot عند إنشاء مصنف من ورقة.

ستتعلم كيفية تحميل مصنف موجود، تكرار ورقة العمل التي تحتوي على جدول Pivot، وحفظ النتيجة كملف جديد. يفترض الدليل أن لديك بيئة تطوير Java أساسية ورخصة صالحة لـ Aspose.Cells (التقييم المجاني يعمل للاختبار). لا توجد أدوات خارجية مطلوبة بخلاف ملف JAR الخاص بـ Aspose.Cells.

## المتطلبات المسبقة

قبل البدء، تأكد من وجود ما يلي:

* Java Development Kit (JDK) 8 أو أحدث.
* Maven أو Gradle لإدارة تبعية Aspose.Cells.
* ملف Excel (`source.xlsx`) يحتوي على جدول Pivot واحد على الأقل في ورقة العمل الأولى.
* دليل يمكنك من قراءة ملف المصدر وكتابة المصنف المكرر.

أضف تبعية Aspose.Cells إلى ملف `pom.xml` (Maven) أو `build.gradle` (Gradle). بالنسبة لـ Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## كيفية تكرار ورقة العمل مع جدول Pivot

العملية الأساسية هي عملية من ثلاث خطوات: التحميل، النسخ، والحفظ. يتم شرح كل خطوة أدناه.

### الخطوة 1 – تحميل المصنف الذي يحتوي على جدول Pivot

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*لماذا هذه الخطوة مهمة*: كائن `Workbook` يمثل ملف Excel بالكامل. من خلال استدعاء ورقة العمل الأولى (`get(0)`)، تستهدف الورقة التي تحتوي على جدول Pivot الذي تريد تكراره.

### الخطوة 2 – إنشاء مصنف جديد وتكرار ورقة العمل بالكامل

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` ينسخ ورقة العمل **بما في ذلك** جميع الكائنات المدمجة، الصيغ، وذاكرة التخزين المؤقتة لجداول Pivot. هذه هي الطريقة الموصى بها لـ **كيفية نسخ Pivot** لأن تعريف Pivot ومصدر البيانات يتم نقلهما معًا.

### الخطوة 3 – حفظ المصنف الجديد

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

بعد التنفيذ، يحتوي `copy_with_pivot.xlsx` على نسخة مطابقة من الورقة الأصلية، ويعمل جدول Pivot دون أي إعداد إضافي.

**النتيجة المتوقعة**: فتح `copy_with_pivot.xlsx` في Excel يظهر ورقة العمل المكررة بنفس تخطيط Pivot، الفلاتر، والحقول المحسوبة كما في ملف المصدر.

## كيفية نسخ Pivot إلى مصنف آخر

إذا كنت بحاجة إلى نقل جدول Pivot دون نسخ الورقة بالكامل، يمكنك استخراج ذاكرة التخزين المؤقتة للـ Pivot وإرفاقها بورقة عمل جديدة. يوضح المقتطف التالي هذا النهج:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

هذا الكود يجيب على **كيفية نسخ Pivot** عن طريق نسخ كائن الـ Pivot فقط، وليس الورقة بأكملها. الطريقة `addCopy` في مجموعة `PivotTables` تضمن تكرار ذاكرة التخزين المؤقتة للـ Pivot، مما يلبي متطلبات **كيفية الحفاظ على Pivot**.

## كيفية الحفاظ على Pivot عند إنشاء مصنف من ورقة

أحيانًا تبدأ بورقة لا تنتمي إلى مصنف (على سبيل المثال، تولد ورقة في الذاكرة). لـ **إنشاء مصنف من ورقة** مع الحفاظ على الـ Pivot، اتبع الخطوات التالية:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

بإضافة ورقة العمل إلى `Workbook` جديد بعد تعريف الـ Pivot بالكامل، تضمن أن **كيفية الحفاظ على Pivot** تعمل حتى عندما تكون الورقة قد نشأت خارج ملف موجود.

## نصائح عملية ومخاطر شائعة

| نصيحة | لماذا يهم |
|-------|-----------|
| استخدم `addCopy` بدلاً من `copy` | `addCopy` ينسخ ذاكرة التخزين المؤقتة للـ Pivot الأساسية؛ قد يفقد `copy` العادي الاتصال بمصدر البيانات. |
| احتفظ بملفات المصدر والوجهة على نفس نظام الملفات | المسارات النسبية في مصدر بيانات الـ Pivot تُحل بشكل صحيح، مما يقلل من أخطاء “المصدر غير موجود”. |
| تحقق من ذاكرة التخزين المؤقتة للـ Pivot بعد النسخ | استدعِ `pivot.refresh()` إذا تغيرت بيانات المصدر بين عملية النسخ والحفظ. |
| تحرير المصنفات عند الانتهاء | `sourceWorkbook.dispose();` يحرر الموارد الأصلية، وهو مهم للملفات الكبيرة. |

## الحالات الحدية التي قد تواجهها

* **Multiple worksheets with inter‑dependent pivots** – انسخ كل ورقة عمل على حدة؛ يتم تكرار الذاكرات المشتركة تلقائيًا، لكن قد تحتاج إلى إعادة تعيين اتصالات البيانات الخارجية.  
* **Pivot tables based on external SQL queries** – تأكد من أن البيئة الوجهة يمكنها الوصول إلى نفس قاعدة البيانات؛ وإلا سيظهر للـ Pivot أخطاء “#REF!”.  
* **Large workbooks (>100 MB)** – استخدم `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` لتقليل ضغط الذاكرة أثناء عملية النسخ.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يدمج جميع الخطوات التي نوقشت. احفظه كملف `CopyPivotTable.java`، عدّل مسارات الملفات، وشغّله باستخدام بيئة التطوير المفضلة لديك أو عبر `javac`/`java`.



## ما الذي يجب أن تتعلمه بعد ذلك؟

تغطي الدروس التالية مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إنشاء جداول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية تحديث مصدر جدول Pivot في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [كيفية تنفيذ مقاطع التصفية (Slicers) في جداول Pivot باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}