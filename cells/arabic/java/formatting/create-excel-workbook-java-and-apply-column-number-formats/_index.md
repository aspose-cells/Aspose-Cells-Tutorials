---
category: general
date: 2026-09-27
description: إنشاء دفتر عمل Excel باستخدام Java، استيراد بيانات SQL، تعيين تنسيق رقم
  للعمود، وحفظ دفتر العمل كملف XLSX باستخدام Aspose.Cells في Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: ar
lastmod: 2026-09-27
og_description: إنشاء ملف عمل Excel باستخدام Java، استيراد بيانات SQL، تعيين تنسيق
  رقم للعمود، وحفظ الملف بصيغة XLSX مع مثال Java كامل يعمل.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: إنشاء دفتر عمل إكسل جافا – استيراد بيانات SQL وتعيين تنسيقات أرقام الأعمدة
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: إنشاء مصنف إكسل باستخدام جافا وتطبيق تنسيقات أرقام الأعمدة
url: /ar/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel java وتطبيق تنسيقات أرقام الأعمدة

إذا كنت بحاجة إلى **إنشاء دفتر عمل Excel java** وتنسيق الأعمدة الرقمية، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعلم كيفية استيراد بيانات SQL إلى Excel، وتعيين تنسيق رقم لكل عمود، و**حفظ دفتر العمل كملف XLSX** باستخدام مكتبة Aspose.Cells.

العمل مع جداول البيانات من Java غالبًا ما يكون متشتتًا—يقوم المطورون بنسخ‑لصق الشفرات، ينسون تنسيق الأرقام، أو ينتهي بهم الأمر بملفات CSV بدلاً من ملفات Excel الحقيقية. يزيل هذا البرنامج التعليمي تلك العوائق من خلال توفير حل شامل من البداية إلى النهاية يمكنك إدراجه في أي مشروع Java.

بنهاية المقال ستتمكن من:

* الاتصال بقاعدة بيانات واسترجاع `DataTable` (أو `ResultSet`)  
* إنشاء دفتر عمل جديد باستخدام Aspose.Cells  
* تطبيق نمط **add number format excel** متسق على كل عمود  
* **حفظ دفتر العمل كملف XLSX** في الموقع الذي تختاره  

المتطلب الوحيد هو بيئة تطوير Java (يوصى بـ JDK 8+ ) ومكتبة Aspose.Cells for Java JAR على مسار الفئات الخاص بك.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| JDK 8 أو أحدث | يوفر ميزات اللغة المستخدمة في المثال. |
| Aspose.Cells for Java (أحدث نسخة) | يتعامل مع إنشاء Excel، التنسيق، والحفظ دون الحاجة إلى تثبيت Office. |
| قاعدة بيانات متوافقة مع JDBC (مثل MySQL, PostgreSQL) | تزودنا ببيانات SQL التي سنستوردها. |
| Maven أو Gradle (اختياري) | يبسط إدارة الاعتمادات. |

أضف Aspose.Cells إلى ملف `pom.xml` الخاص بـ Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

أو قم بتحميل ملف JAR مباشرةً من موقع Aspose وأضفه إلى مسار الفئات في مشروعك.

---

## الخطوة 1: إنشاء دفتر عمل Excel java

الكتلة المنطقية الأولى هي إنشاء كائن `Workbook` جديد. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة ويمنحك الوصول إلى الأوراق، الخلايا، والأنماط.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

إنشاء دفتر العمل مسبقًا يمنحنا أيضًا مصنع `Style` الذي سنحتاجه لاحقًا عندما **نحدد تنسيق رقم العمود**.

---

## الخطوة 2: استرجاع البيانات من SQL (import sql data excel)

في الأسفل نفتح اتصال JDBC، ننفذ جملة `SELECT` بسيطة، ونحمّل مجموعة النتائج في `DataTable` من Aspose. فئة `DataTable` تحاكي .NET `DataTable` وتعمل بسلاسة مع طريقة `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **نصيحة:** إذا كان لديك بالفعل `DataTable` من مصدر آخر (مثل تحليل CSV)، يمكنك تخطي كود JDBC وإرجاع ذلك الجدول مباشرة.

---

## الخطوة 3: إعداد نمط قابل لإعادة الاستخدام (add number format excel)

نريد أن يعرض كل عمود رقمي الأرقام بفاصل آلاف ومكانين عشريين. بدلاً من تنسيق كل خلية على حدة، ننشئ كائن `Style` مرة واحدة لكل عمود ونعيد استخدامه أثناء الاستيراد. هذه هي الطريقة الأكثر كفاءة لـ **add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

يمكنك تعديل سلسلة التنسيق (`"#,##0.00"`) إلى أي تنسيق رقم في Excel تحتاجه. للتواريخ، استخدم `styles[i].setCustom("mm-dd-yyyy")`، إلخ.

---

## الخطوة 4: استيراد DataTable وتطبيق أنماط الأعمدة

الآن نجمع كل شيء معًا. تسمح لنا نسخة `importDataTable` المتعددة المعاملات بتمرير `DataTable`، وتحديد ما إذا كان يجب اعتبار الصف الأول كعناوين أعمدة، وتوفير مصفوفة الأنماط. هذا يقوم تلقائيًا **بتحديد تنسيق رقم العمود** لكل خلية في العمود المقابل.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

نظرًا لأننا مررنا `true` للمعامل `importColumnNames`، فإن الصف الأول من الورقة يحتوي على أسماء الأعمدة من `DataTable`. كل صف لاحق يتلقى البيانات، مُنسَّقة بالفعل وفق النمط الذي عرّفناه.

---

## الخطوة 5: حفظ دفتر العمل كملف xlsx

الخطوة الأخيرة هي حفظ دفتر العمل الموجود في الذاكرة إلى ملف فعلي. تدعم Aspose.Cells العديد من الصيغ؛ سنستخدم صيغة XLSX الحديثة، وهي الصيغة التي تتوقعها معظم التطبيقات اليوم.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

يمكنك تغيير `filePath` إلى أي موقع صالح على نظامك. تُطلق الطريقة استثناء `IOException` إذا لم يكن الدليل موجودًا أو إذا لم يكن لديك صلاحية كتابة.

---

## مثال كامل قابل للتنفيذ

جمع كل الأجزاء معًا ينتج برنامجًا مستقلًا يمكنك تجميعه وتشغيله فورًا.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج ينشئ ملفًا باسم **DataTableWithNumberFormat.xlsx** في دليل العمل. افتحه باستخدام Microsoft Excel أو LibreOffice Calc أو أي عارض XLSX وسترى:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*عمود **Amount** يعرض الأرقام بمكانين عشريين وفاصل آلاف، بفضل نمط **add number format excel** الذي طبقناه.*

---

## الأسئلة الشائعة ومعالجة الحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو أعادت الاستعلام الخاص بي لا صفوف؟** | سيظل `DataTable` فارغًا لكنه سيحتوي على تعريفات الأعمدة. سيحتوي دفتر العمل فقط على صف العناوين، وهو غالبًا ما يكون كافيًا للعمليات اللاحقة. |
| **كيف يمكنني تطبيق تنسيقات مختلفة لكل عمود؟** | عدل الدالة `buildColumnStyles` لتفحص اسم العمود أو نوع البيانات وتُعيّن تنسيقًا مخصصًا (مثل التواريخ أو النسب المئوية). |
| **هل يمكنني الكتابة مباشرةً إلى `ByteArrayOutputStream`؟** | نعم. استبدل `workbook.save(filePath, SaveFormat.XLSX);` بـ |

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إنشاء وحفظ دفتر عمل Excel كملف SVG باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [إنشاء وحفظ دفتر عمل Excel Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [إنشاء وحفظ دفتر عمل Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}