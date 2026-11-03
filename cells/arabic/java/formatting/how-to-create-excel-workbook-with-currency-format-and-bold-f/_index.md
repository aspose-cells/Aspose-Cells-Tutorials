---
category: general
date: 2026-08-20
description: إنشاء مصنف إكسل في جافا باستخدام Aspose.Cells، تعيين تنسيق العملة، إضافة
  خط عريض، واستيراد مصفوفة الأنماط للخلايا ذات التنسيق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: ar
lastmod: 2026-08-20
og_description: إنشاء دفتر عمل Excel في Java، تعيين تنسيق العملة، إضافة خط غامق، وتعلم
  كيفية استيراد النمط باستخدام Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: إنشاء مصنف إكسل بخلايا عملة منسقة في جافا
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: كيفية إنشاء مصنف إكسل بتنسيق العملة وخط عريض في جافا
url: /ar/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مصنف إكسل بتنسيق عملة وخط عريض في جافا

إذا كنت بحاجة إلى **create excel workbook** برمجيًا، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. سنستعرض بناء مصنف، تطبيق تنسيق عملة، إضافة خط عريض، واستخدام ميزة **how to import style** في Aspose.Cells بحيث يبدو كل خلية مستوردة متسقة.

ستنتهي بملف `DataTableWithStyleArray.xlsx` جاهز للاستخدام يعرض الأرقام بالدولار ويبرزها بخط عريض. لا يلزم أي تنسيق يدوي في إكسل.

## المتطلبات المسبقة

- Java 17 أو أحدث مثبت.
- رخصة Aspose.Cells for Java (أو مفتاح تقييم مجاني).
- Maven أو Gradle لإدارة تبعية `aspose-cells`.
- إلمام أساسي بمجموعات جافا و`DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **نصيحة احترافية:** إذا واجهت `LicenseException`، ضع ملف الترخيص في مسار الفئة (classpath) واستدعِ `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` قبل إنشاء المصنف.

## كيفية إنشاء مصنف إكسل بخلايا عملة منسقة

يحتوي هذا القسم على الخطوات الأساسية. كل خطوة تشرح **لماذا** هي مهمة، وليس فقط **ماذا** تكتب.

### الخطوة 1: تهيئة المصنف وورقة العمل

إنشاء مصنف جديد يمنحك حاوية نظيفة لجميع التنسيقات اللاحقة.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **لماذا:** كائن `Workbook` يمثل ملف إكسل بالكامل. الوصول إلى أول `Worksheet` يتيح لك بدء تعبئة البيانات فورًا.

### الخطوة 2: بناء DataTable ببيانات رقمية

`DataTable` يحاكي جدول قاعدة بيانات، مما يسهل استيراد الصفوف دفعة واحدة.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **لماذا:** استخدام `DOUBLE` يضمن بقاء القيم بدقة عشرية، وهو أمر أساسي عندما تقوم لاحقًا **format cells currency**.

### الخطوة 3: تعريف نمط – تنسيق عملة وخط عريض

هنا نقوم **set currency format** و**add bold font** لكائن `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **لماذا:** سلسلة تنسيق `Number` `$#,##0.00` تخبر إكسل بمعاملة الخلية كقيمة مالية، بينما `setBold(true)` يبرز الأرقام. وضع النمط في مصفوفة يجهزنا لخطوة **how to import style**.

### الخطوة 4: تكوين خيارات الاستيراد لاستخدام مصفوفة النمط

تتيح لك Aspose.Cells تمرير `Style[]` عبر `ImportTableOptions`. هذه هي الطريقة الرسمية لـ **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **لماذا:** بدون `ImportTableOptions`، ستورث الخلايا المستوردة النمط الافتراضي، مما يفقد تنسيق العملة والخط العريض الذي حددناه.

### الخطوة 5: استيراد DataTable إلى ورقة العمل

الآن ننقل البيانات إلى الورقة في الخلية `A1`، مع تطبيق مصفوفة النمط تلقائيًا.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` يشير إلى أن الصف الأول من `DataTable` يحتوي على رؤوس الأعمدة.
- `"A1"` هو الزاوية العليا اليسرى حيث يبدأ الاستيراد.

> **لماذا:** يضمن الاستيراد باستخدام مصفوفة النمط أن كل خلية مستوردة تتلقى نمط **format cells currency** الذي أعددناه مسبقًا.

### الخطوة 6: حفظ المصنف على القرص

أخيرًا، اكتب المصنف الموجود في الذاكرة إلى ملف فعلي.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **لماذا:** الحفظ يحفظ التنسيق، مما يسمح لك أو للعمليات اللاحقة بفتح الملف في إكسل بالمظهر المطلوب.

## الكود المصدر الكامل

فيما يلي الفئة الكاملة الجاهزة للتنفيذ في جافا. انسخها إلى بيئة التطوير المتكاملة (IDE)، استبدل `YOUR_DIRECTORY` بمجلد موجود، ثم نفذ.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### النتيجة المتوقعة

عند فتح `DataTableWithStyleArray.xlsx` في Microsoft Excel، يجب أن ترى:

| المبلغ |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- الأرقام معروضة بتنسيق **currency format** (علامة `$`، منزلتين عشريتين).
- الخط في كلتا الخليتين هو **bold**، مما يجعلهما بارزين.

## الاختلافات الشائعة وحالات الحافة

| السيناريو | ما الذي يجب تغييره | السبب |
|----------|-------------------|--------|
| **عملة مختلفة** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | استخدم رمز اليورو أو أي تنسيق خاص بالموقع. |
| **أعمدة متعددة بأنماط مختلفة** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | يمكن لكل عمود أن يمتلك تنسيق رقم خاص به، خط، خلفية، إلخ. |
| **مجموعات بيانات كبيرة** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | يحسن الأداء عن طريق تخطي صفوف العناوين أو البيانات الوصفية غير الضرورية. |
| **تطبيق النمط بعد الاستيراد** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | مفيد عندما يحتاج فقط جزء من الصفوف إلى تنسيق خاص. |

## نصائح للاستخدام في الإنتاج

- **سجّل الترخيص مبكرًا**: سجّل ترخيص Aspose.Cells قبل إنشاء المصنف لتجنب علامة مائية التقييم.
- **سلامة الخيوط**: كائنات `Workbook` **ليست** آمنة للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة لكل خيط إذا كنت تولد العديد من الملفات في وقت واحد.
- **إدارة الذاكرة**: للأوراق الكبيرة جدًا، فكر في استخدام API البث لـ `Workbook` (`Workbook` → `WorkbookDesigner`) لتقليل استهلاك الذاكرة.
- **الاختبار**: أدرج اختبار وحدة يفتح الملف المحفوظ باستخدام Apache POI ويتأكد من أن تنسيق رقم نمط الخلية يطابق `"$#,##0.00"`.

## الخلاصة

أنت الآن تعرف كيفية **create excel workbook** في جافا، **set currency format**، **add bold font**، واستخدام **how to import style** بشكل صحيح باستخدام `ImportTableOptions` في Aspose.Cells. هذا الحل المتكامل يلغي خطوات إكسل اليدوية ويضمن أن كل خلية مستوردة تتبع نفس نمط **format cells currency**.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة تنسيق شرطي، تضمين مخططات، أو تصدير المصنف إلى PDF—كل ذلك مع إعادة استخدام تقنية مصفوفة النمط نفسها. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}