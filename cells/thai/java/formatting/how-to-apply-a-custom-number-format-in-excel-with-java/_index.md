---
category: general
date: 2026-11-22
description: เรียนรู้วิธีใช้รูปแบบตัวเลขแบบกำหนดเองเพื่อจัดรูปแบบคอลัมน์เป็นสกุลเงินใน
  Excel ด้วย Java ตั้งค่ารูปแบบตัวเลขของ Excel อย่างรวดเร็วด้วยสไตล์ง่าย ๆ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: th
lastmod: 2026-11-22
og_description: ใช้รูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java บทเรียนนี้แสดงวิธีตั้งค่ารูปแบบตัวเลขใน
  Excel และจัดรูปแบบคอลัมน์แรกเป็นสกุลเงิน.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: ใช้รูปแบบตัวเลขกำหนดเองใน Excel ด้วย Java – คู่มือขั้นตอนโดยละเอียด
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
title: วิธีใช้รูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java
url: /th/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้รูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย Java

หากคุณต้องการ **custom number format** คอลัมน์ในแผ่นงาน Excel คำแนะนำนี้จะแสดงให้คุณเห็นอย่างละเอียดว่าทำอย่างไรโดยใช้ Java ไม่ว่าคุณจะสร้างรายงานการเงินหรือส่งออกข้อมูลบัญชี การจัดรูปแบบคอลัมน์แรกเป็นสกุลเงินทำให้ผลลัพธ์อ่านง่ายทันที

ในตัวอย่างด้านล่าง เราจะ **format column as currency**, ใช้สไตล์กับคอลัมน์แรก แล้วนำเข้า `DataTable` ไปยังแผ่นงาน วิธีเดียวกันนี้ใช้ได้กับรูปแบบตัวเลขใด ๆ ที่คุณต้องการแสดง

## สิ่งที่คุณจะได้เรียนรู้

* วิธีสร้าง **custom number format** ด้วยอ็อบเจกต์ `Style` ของ Apache POI.  
* วิธี **set Excel number format** สำหรับคอลัมน์เฉพาะ รวมถึงกรณี **set currency format**.  
* วิธี **style first column** ขณะนำเข้า `DataTable`.  
* วิธีบันทึก workbook และตรวจสอบว่าการจัดรูปแบบแสดงผลอย่างถูกต้อง.  

### ข้อกำหนดเบื้องต้น

* Java 17 หรือใหม่กว่า.  
* Apache POI 5.x (ไลบรารีที่ให้ `Workbook`, `Worksheet`, และ `Style`).  
* การนำไปใช้ `DataTable` ที่สามารถวนลูปได้เช่นตัวอย่างในโค้ด.  
* ความคุ้นเคยพื้นฐานกับ Java และแนวคิดของ Excel.  

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้าข้อมูล

ขั้นแรก เพิ่ม Apache POI ลงในโปรเจกต์ของคุณ หากคุณใช้ Maven ให้ใส่ dependency ต่อไปนี้:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

ต่อไป ดึงข้อมูลต้นทางเป็น `DataTable` ในสถานการณ์จริงข้อมูลนี้อาจมาจากการ query ฐานข้อมูล ไฟล์ CSV หรือการตอบสนองจาก API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** ตรวจสอบให้แน่ใจว่าคอลัมน์ของ `DataTable` มีประเภท Java ที่ถูกต้อง (`Integer`, `Double` เป็นต้น) เนื่องจากรูปแบบตัวเลขมีผลต่อเซลล์ที่เป็นตัวเลขเท่านั้น.

---

## ขั้นตอนที่ 2: สร้าง **custom number format** สำหรับคอลัมน์แรก

**custom number format** บอก Excel ว่าจะแสดงค่าตัวเลขอย่างไร เพื่อแสดงค่าเป็นสกุลเงินเราจะใช้รูปแบบในตัว `CURRENCY` แต่คุณก็สามารถกำหนดแพทเทิร์นเช่น `"$#,##0.00"` ได้เช่นกัน.

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

**ทำไมวิธีนี้ถึงได้ผล:**  
* `createCellStyle()` คืนค่าอ็อบเจกต์สไตล์ที่สามารถนำกลับมาใช้ใหม่ได้.  
* `setDataFormat()` ผูก **set currency format** กับสไตล์ ซึ่ง Excel จะนำไปใช้กับทุกเซลล์ที่ใช้สไตล์นี้.  
* การเก็บสไตล์ไว้ใน `columnStyles[0]` ทำให้เรามั่นใจว่าเฉพาะคอลัมน์แรกเท่านั้นที่ได้รับการจัดรูปแบบสกุลเงิน.

---

## ขั้นตอนที่ 3: นำเข้า `DataTable` พร้อมใช้สไตล์คอลัมน์

ตอนนี้เรานำเข้าข้อมูลไปยังแผ่นงาน เมธอด `importDataTable` รับอาร์เรย์สไตล์ ทำให้เราสามารถ **style first column** และปล่อยคอลัมน์ที่เหลือให้ใช้การจัดรูปแบบเริ่มต้น.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

การเรียกด้านบน **sets Excel number format** เฉพาะคอลัมน์แรกเท่านั้น คอลัมน์อื่น ๆ จะสืบทอดสไตล์เริ่มต้นของ workbook ซึ่งทำให้โค้ดง่ายและมีประสิทธิภาพ.

---

## ขั้นตอนที่ 4: บันทึก workbook และตรวจสอบผลลัพธ์

สุดท้าย เขียน workbook ลงไฟล์และเปิดใน Excel เพื่อตรวจสอบว่าคอลัมน์แรกแสดงสัญลักษณ์สกุลเงิน.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อคุณเปิดไฟล์ *FormattedReport.xlsx* ค่าที่คอลัมน์ A จะปรากฏพร้อมสัญลักษณ์สกุลเงินที่เหมาะสม (เช่น `$1,234.00`). คอลัมน์อื่น ๆ จะคงรูปแบบตัวเลขเดิมไว้.

---

## ความหลากหลายและกรณีขอบที่พบบ่อย

| สถานการณ์ | การปรับเปลี่ยน |
|-----------|------------|
| **Different currency** (e.g., Euro) | Replace `Style.CustomNumberFormat.CURRENCY` with a custom pattern: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **More than one styled column** | Populate additional entries in `columnStyles[]` with their own `CellStyle` objects. |
| **Large data sets** | Use `importDataTable` in batches or stream rows to avoid `OutOfMemoryError`. |
| **Locale‑specific separators** | Use `java.text.NumberFormat` to generate a locale‑aware pattern and pass it to `setDataFormat`. |

> **Watch out for:** การใช้ `CellStyle` เดียวซ้ำหลายคอลัมน์อาจทำให้เกิดการจัดรูปแบบที่ไม่คาดคิด เนื่องจาก Excel จำกัดจำนวนสไตล์ที่แตกต่างกันต่อ workbook ควรสร้างสไตล์แยกสำหรับแต่ละรูปแบบที่ต้องการ.

---

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่ทำงานอิสระซึ่งแสดงขั้นตอนทั้งหมด ตั้งแต่การสร้างข้อมูลจนถึงการบันทึก workbook ที่จัดรูปแบบ.

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

การรันโปรแกรมจะสร้างไฟล์ **FormattedReport.xlsx** ที่คอลัมน์ A (คอลัมน์ “Amount”) แสดงด้วย **custom number format** ที่มีสัญลักษณ์ดอลลาร์และทศนิยมสองตำแหน่ง.

---

## สรุป

ตอนนี้คุณรู้วิธี **custom number format** แผ่นงาน Excel จาก Java, **format column as currency**, และ **style first column** ขณะนำเข้าข้อมูล ด้วยการสร้าง `CellStyle` ที่นำกลับมาใช้ได้และส่งให้ `importDataTable` คุณสามารถ **set Excel number format** สำหรับคอลัมน์ใดก็ได้โดยไม่ต้องวนลูปผ่านแต่ละเซลล์ด้วยตนเอง.

Next, try:

* ใช้ `setDataFormat` กับแพทเทิร์นที่ขึ้นกับ locale เพื่อ **set currency format**

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ.

- [ตั้งค่ารูปแบบตัวเลขใน Excel ด้วย Java – คู่มือเต็ม](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [ใช้รูปแบบตัวเลขใน Excel ด้วย Java – คู่มือ Aspose.Cells เต็ม](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [วิธีสร้าง workbook Excel ด้วยรูปแบบสกุลเงินและตัวหนาใน Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}