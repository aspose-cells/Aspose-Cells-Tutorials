---
category: general
date: 2026-06-30
description: اجعل الخط عريضًا أثناء استيراد DataTable إلى Excel باستخدام Java. تعلم
  كود التنسيق الشرطي، استيراد DataTable إلى Excel وتنسيق الجداول بسهولة.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: ar
og_description: تعيين الخط غامق في جافا عند تصدير DataTable إلى إكسل. يغطي هذا الدليل
  كود التنسيق الشرطي، استيراد جدول البيانات إلى إكسل، وتنسيق الجدول.
og_title: تعيين الخط عريض في تصدير Excel باستخدام Java – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: تعيين الخط عريض في تصدير إكسل بجافا – دليل كامل
url: /ar/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين الخط غامق في تصدير Excel باستخدام Java – دليل شامل

هل تساءلت يومًا **كيف تُعيّن الخط غامقًا** لأعمدة معينة أثناء **استيراد ملفات Excel من جدول البيانات**؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى جدول بيانات مُنسق بشكل جميل دون تعديل كل خلية يدويًا. الخبر السار؟ ببضع أسطر من Java يمكنك استيراد `DataTable`، تطبيق الخط الغامق، وحتى إضافة **كود تنسيق شرطي**—كل ذلك برمجيًا.

في هذا الدرس سنستعرض مثالًا كاملًا قابلًا للتنفيذ يُظهر **كيفية استيراد جدول البيانات** إلى مصنف Excel، تطبيق **تعيين الخط غامق** على كل عمود ذو فهرس زوجي، وإضافة تنسيق شرطي بسيط اختياريًا. بنهاية الدرس ستحصل على مقتطف جاهز للتنفيذ وفهم واضح لـ **استيراد جدول مع الأنماط** لأي مشروع.

## المتطلبات المسبقة

- Java 8 أو أحدث (الكود يعمل على Java 17 أيضًا)  
- Aspose.Cells for Java (نسخة التجربة المجانية تكفي) – أضف تبعية Maven أو ملف JAR إلى مسار الـ classpath.  
- إلمام أساسي بتحويل `java.sql` `ResultSet` → `DataTable` (سنقوم بمحاكاة جدول للبساطة).  
- بيئة تطوير متكاملة (IDE) أو أداة بناء مثل Maven/Gradle.

> **نصيحة محترف:** إذا كنت تستخدم Maven، أضف ما يلي إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## نظرة عامة على الحل

1. **إنشاء `DataTable` تجريبي** يحاكي البيانات التي عادةً ما تستخرجها من قاعدة البيانات.  
2. **إنشاء مصفوفة `CellStyle`** حيث يحصل كل عمود زوجي على خط غامق – هذا هو جوهر **تعيين الخط غامق**.  
3. **الحصول على الورقة الأولى** من المصنف.  
4. **استيراد `DataTable`** مع رؤوس الأعمدة، بدءًا من الخلية `A1`، وتطبيق الأنماط المُعدة.  
5. (اختياري) **إضافة قاعدة تنسيق شرطي** لتوضيح كلمة المفتاح **كود تنسيق شرطي**.

كل خطوة مشروحة بلغة بسيطة، وكتل الكود مكتملة ذاتيًا بحيث يمكنك نسخها ولصقها وتشغيلها فورًا.

---

## الخطوة 1: استرجاع أو بناء الـ DataTable للاستيراد

في التطبيقات الواقعية قد تستدعي أدوات تحويل `ResultSet` → `DataTable`. لهذا الدليل سنُنشئ `DataTable` بسيط يدويًا لتتمكن من التركيز على جزء Excel.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **لماذا هذا مهم:** وجود `DataTable` جاهز يسمح لنا بالتركيز على واجهة **استيراد جدول Excel** ومنطق الأنماط. الطريقة أعلاه قابلة لإعادة الاستخدام—فقط استبدل الصفوف المُحددة صراحةً باستعلام قاعدة بيانات عندما تنتقل إلى بيئة الإنتاج.

---

## الخطوة 2: إعداد الأنماط – هنا نـ **تعيّن الخط غامق**

الآن سنُنشئ مصفوفة من كائنات `CellStyle`، واحدة لكل عمود. القاعدة بسيطة: **تعيّن الخط غامق** لكل عمود ذو فهرس زوجي (0، 2، 4، …). الأعمدة الفردية تبقى عادية.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### لماذا نستخدم مصفوفة من الأنماط؟

- **الأداء:** تطبيق نمط على مستوى العمود أسرع من تنسيق كل خلية على حدة.  
- **الاتساق:** كل خلية في العمود ترث نفس التنسيق، ما يضمن مظهرًا موحدًا.  
- **القابلية للتوسع:** إضافة أعمدة لاحقًا يتطلب فقط توسيع المصفوفة—دون الحاجة لإعادة كتابة الكود.

---

## الخطوة 3: الوصول إلى الورقة الأولى في المصنف

إن Aspose.Cells ينشئ ورقة عمل افتراضية لنا، لكن من الأفضل جلبها صراحة. هذا أيضًا يوضح **كيفية استيراد جدول البيانات** إلى ورقة محددة.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## الخطوة 4: استيراد الـ DataTable مع الأنماط – عملية **استيراد جدول مع الأنماط** الأساسية

طريقة `importDataTable` تقوم بالعمل الشاق. فهي تنسخ البيانات، تضيف رؤوس الأعمدة، وتطبق مصفوفة الأنماط التي أنشأناها مسبقًا.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

عند تشغيل المثال، ستلاحظ تطبيق **تعيين الخط غامق** على الأعمدة `ID` و `Score`، بينما يبقى `Name` عاديًا.

---

## الخطوة 5 (اختياري): إضافة تنسيق شرطي – مثال سريع على **كود تنسيق شرطي**

إذا رغبت في تمييز الصفوف التي يتجاوز فيها الـ score قيمة 90، بضعة أسطر إضافية تكفي. هذا يوضح كلمة المفتاح **كود تنسيق شرطي** دون إرباك التدفق الرئيسي.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **ملاحظة:** المقتطف أعلاه اختياري لكنه يُظهر كيف يمكنك إضافة **كود تنسيق شرطي** فوق الجدول المُنسق مسبقًا.

---

## تجميع كل شيء – مثال كامل قابل للتنفيذ

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ إنشاء مصنف جديد (في الذاكرة)
        Workbook wb = new Workbook();

        // 2️⃣ استرجاع الـ DataTable الذي نريد تصديره
        DataTable dataTable = getDataTable();

        // 3️⃣ إعداد أنماط الأعمدة – هنا نُعيّن الخط غامق
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ جلب الورقة الأولى
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ استيراد الجدول مع الرؤوس وأنماطنا
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ اختياري: إضافة قاعدة تنسيق شرطي
        addConditionalFormatting(sheet);

        // 7️⃣ حفظ المصنف إلى القرص
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- الدوال المساعدة من الأقسام السابقة -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Implement Custom Font Settings in Aspose.Cells Java for Excel Formatting](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Set Font Size in Excel Using Aspose.Cells Java - Comprehensive Guide](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}