---
category: general
date: 2026-11-22
description: تعلم كيفية استخدام تنسيق رقم مخصص لتنسيق عمود كعملة في Excel باستخدام
  Java. قم بتعيين تنسيق رقم Excel بسرعة باستخدام نمط بسيط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: ar
lastmod: 2026-11-22
og_description: تطبيق تنسيق رقم مخصص في Excel باستخدام Java. يوضح هذا الدرس كيفية
  تعيين تنسيق الأرقام في Excel وتنسيق العمود الأول كعملة.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: تطبيق تنسيق رقم مخصص في إكسل باستخدام جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: كيفية تطبيق تنسيق رقم مخصص في إكسل باستخدام جافا
url: /ar/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تطبيق تنسيق رقم مخصص في Excel باستخدام Java

إذا كنت بحاجة إلى **تنسيق رقم مخصص** لعمود في ورقة عمل Excel، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Java. سواءً كنت تُنشئ تقارير مالية أو تُصدّر بيانات محاسبية، فإن تنسيق العمود الأول كعملة يجعل المخرجات قابلة للقراءة فورًا.

في المثال أدناه سنقوم **بتنسيق العمود كعملة**، وتطبيق النمط على العمود الأول، ثم استيراد `DataTable` إلى ورقة العمل. نفس النهج يعمل مع أي تنسيق رقمي تريد عرضه.

## ما ستتعلمه

* كيفية إنشاء **تنسيق رقم مخصص** باستخدام كائن `Style` في Apache POI.  
* كيفية **تعيين تنسيق رقم Excel** لعمود محدد، بما في ذلك حالة **تعيين تنسيق العملة**.  
* كيفية **تنسيق العمود الأول** أثناء استيراد `DataTable`.  
* كيفية حفظ المصنف والتحقق من ظهور التنسيق بشكل صحيح.

### المتطلبات المسبقة

* Java 17 أو أحدث.  
* Apache POI 5.x (المكتبة التي توفر `Workbook` و `Worksheet` و `Style`).  
* تنفيذ `DataTable` يمكن تكراره كما هو موضح في عينة الشيفرة.  
* إلمام أساسي بـ Java ومفاهيم Excel.

---

## الخطوة 1: إعداد المشروع واستيراد البيانات

أولاً، أضف Apache POI إلى مشروعك. إذا كنت تستخدم Maven، أدرج الاعتماد التالي:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

بعد ذلك، احصل على البيانات المصدرية كـ `DataTable`. في سيناريو واقعي قد تأتي هذه البيانات من استعلام قاعدة بيانات، ملف CSV، أو استجابة API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **نصيحة احترافية:** تأكد من أن أعمدة `DataTable` لها الأنواع Java الصحيحة (`Integer`، `Double`، إلخ) لأن تنسيق الرقم يؤثر فقط على الخلايا الرقمية.

---

## الخطوة 2: إنشاء **تنسيق رقم مخصص** للعمود الأول

**تنسيق الرقم المخصص** يخبر Excel كيف يعرض القيم الرقمية. لعرض القيم كعملة نستخدم التنسيق المدمج `CURRENCY`، لكن يمكنك أيضًا تعريف أنماط مثل `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**لماذا يعمل هذا:**  
* `createCellStyle()` يُعيد كائن نمط قابل لإعادة الاستخدام.  
* `setDataFormat()` يربط **تعيين تنسيق العملة** بالنمط، والذي يطبقه Excel على كل خلية تستخدم هذا النمط.  
* بتخزين النمط في `columnStyles[0]` نضمن أن العمود الأول فقط يحصل على تنسيق العملة.

---

## الخطوة 3: استيراد `DataTable` مع تطبيق أنماط الأعمدة

الآن نستورد البيانات إلى ورقة العمل. طريقة `importDataTable` تقبل مصفوفة الأنماط، مما يسمح لنا **بتنسيق العمود الأول** وترك الأعمدة المتبقية بالتنسيق الافتراضي.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

النداء أعلاه **يحدد تنسيق رقم Excel** للعمود الأول فقط. جميع الأعمدة الأخرى ترث النمط الافتراضي للمصنف، مما يبقي الشيفرة بسيطة وفعّالة.

---

## الخطوة 4: حفظ المصنف والتحقق من النتيجة

أخيرًا، اكتب المصنف إلى ملف وافتحه في Excel لتتأكد من أن العمود الأول يظهر رموز العملة.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**الناتج المتوقع:**  
عند فتح *FormattedReport.xlsx*، تظهر القيم في العمود A مع رمز العملة المناسب (مثال: `$1,234.00`). جميع الأعمدة الأخرى تحتفظ بتمثيلها الرقمي الأصلي.

---

## الاختلافات الشائعة وحالات الحافة

| الحالة | التعديل |
|-----------|------------|
| **عملة مختلفة** (مثال: يورو) | استبدل `Style.CustomNumberFormat.CURRENCY` بنمط مخصص: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **أكثر من عمود مُنسق** | عَبّئ مداخل إضافية في `columnStyles[]` بكائنات `CellStyle` الخاصة بها. |
| **مجموعات بيانات كبيرة** | استخدم `importDataTable` على دفعات أو بث الصفوف لتجنب `OutOfMemoryError`. |
| **فواصل خاصة بالمنطقة** | استخدم `java.text.NumberFormat` لإنشاء نمط يعتمد على الإعدادات المحلية ومرره إلى `setDataFormat`. |

> **احذر من:** إعادة استخدام كائن `CellStyle` واحد عبر أعمدة متعددة قد يسبب تنسيقًا غير متوقع لأن Excel يحدّ عدد الأنماط المتميزة لكل مصنف. أنشئ نمطًا منفصلًا لكل تنسيق فريد تحتاجه.

---

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مستقل يوضح سير العمل بالكامل، من إنشاء البيانات إلى حفظ المصنف المنسق.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

تشغيل البرنامج يُنشئ **FormattedReport.xlsx** حيث يُعرض العمود A (عمود “Amount”) باستخدام **تنسيق رقم مخصص** يُظهر علامة الدولار ومكانين عشريين.

---

## الخلاصة

أنت الآن تعرف كيف **تُنشئ تنسيق رقم مخصص** لورقة عمل Excel من خلال Java، **وتُنسق العمود كعملة**، و**تُنسق العمود الأول** أثناء استيراد البيانات. من خلال إنشاء `CellStyle` قابل لإعادة الاستخدام وتمريره إلى `importDataTable`، يمكنك **تعيين تنسيق رقم Excel** لأي عمود دون الحاجة إلى حلقة على كل خلية يدويًا.

جرب الآن:

* استخدام `setDataFormat` مع أنماط خاصة بالمنطقة لتطبيق **تنسيق العملة**  

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}