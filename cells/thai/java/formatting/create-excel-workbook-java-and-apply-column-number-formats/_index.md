---
category: general
date: 2026-09-27
description: สร้างไฟล์ Excel workbook ด้วย Java, นำเข้าข้อมูลจาก SQL, ตั้งค่ารูปแบบตัวเลขให้คอลัมน์,
  และบันทึกไฟล์เป็น XLSX โดยใช้ Aspose.Cells ใน Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: th
lastmod: 2026-09-27
og_description: สร้างไฟล์ Excel ด้วย Java, นำเข้าข้อมูลจาก SQL, ตั้งค่ารูปแบบตัวเลขในคอลัมน์,
  และบันทึกไฟล์เป็น XLSX พร้อมตัวอย่าง Java ที่ทำงานได้เต็มรูปแบบ.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: สร้างไฟล์ Excel ด้วย Java – นำเข้าข้อมูล SQL และตั้งค่ารูปแบบตัวเลขของคอลัมน์
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
title: สร้างไฟล์ Excel ด้วย Java และกำหนดรูปแบบตัวเลขของคอลัมน์
url: /th/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel workbook java และกำหนดรูปแบบตัวเลขของคอลัมน์

หากคุณต้องการ **create Excel workbook java** และกำหนดรูปแบบตัวเลขของคอลัมน์ คู่มือนี้จะแสดงวิธีทำอย่างละเอียด คุณจะได้เรียนรู้การนำเข้าข้อมูล SQL ไปยัง Excel ตั้งค่ารูปแบบตัวเลขสำหรับแต่ละคอลัมน์ และ **save workbook as XLSX** ด้วยไลบรารี Aspose.Cells

การทำงานกับสเปรดชีตจาก Java มักรู้สึกกระจัดกระจาย—นักพัฒนาคัดลอก‑วางโค้ดสั้น ๆ ลืมกำหนดรูปแบบตัวเลข หรือจบลงด้วยไฟล์ CSV แทนไฟล์ Excel จริง คู่มือนี้ขจัดอุปสรรคเหล่านั้นโดยให้โซลูชันครบวงจรที่คุณสามารถนำไปใช้ในโปรเจค Java ใดก็ได้

โดยเมื่ออ่านจบบทความคุณจะสามารถ:

* เชื่อมต่อกับฐานข้อมูลและดึง `DataTable` (หรือ `ResultSet`)  
* สร้าง workbook ใหม่ด้วย Aspose.Cells  
* ใช้สไตล์ **add number format excel** อย่างสม่ำเสมอกับทุกคอลัมน์  
* **Save workbook as XLSX** ไปยังตำแหน่งที่คุณเลือก  

ข้อกำหนดเบื้องต้นเพียงอย่างเดียวคือสภาพแวดล้อมการพัฒนา Java (แนะนำ JDK 8 ขึ้นไป) และไฟล์ JAR ของ Aspose.Cells for Java บน classpath ของคุณ

---

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| JDK 8 หรือใหม่กว่า | ให้คุณสมบัติของภาษาที่ใช้ในตัวอย่าง |
| Aspose.Cells for Java (latest version) | จัดการการสร้าง Excel, การกำหนดสไตล์ และการบันทึกโดยไม่ต้องติดตั้ง Office |
| ฐานข้อมูลที่รองรับ JDBC (เช่น MySQL, PostgreSQL) | ให้ข้อมูล SQL ที่เราจะนำเข้า |
| Maven หรือ Gradle (ไม่บังคับ) | ทำให้การจัดการ dependencies ง่ายขึ้น |

เพิ่ม Aspose.Cells ไปยังไฟล์ `pom.xml` ของ Maven ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

หรือดาวน์โหลดไฟล์ JAR โดยตรงจากเว็บไซต์ Aspose แล้วเพิ่มลงใน classpath ของโปรเจคของคุณ

---

## ขั้นตอนที่ 1: สร้าง Excel workbook java

บล็อกแรกที่ต้องทำคือการสร้างอินสแตนซ์ใหม่ของ `Workbook` วัตถุนี้เป็นตัวแทนของไฟล์ Excel ทั้งหมดในหน่วยความจำและให้คุณเข้าถึง worksheets, cells, และ styles

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

การสร้าง workbook ล่วงหน้ายังทำให้เรามี `Style` factory ที่จะต้องใช้ต่อไปเมื่อเราต้อง **set number format column**

## ขั้นตอนที่ 2: ดึงข้อมูลจาก SQL (import sql data excel)

ด้านล่างเราจะเปิดการเชื่อมต่อ JDBC, รันคำสั่ง `SELECT` ง่าย ๆ, และโหลดผลลัพธ์ลงใน Aspose `DataTable` คลาส `DataTable` จำลองพฤติกรรมของ .NET `DataTable` และทำงานร่วมกับเมธอด `importDataTable` ได้อย่างราบรื่น

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

> **Tip:** หากคุณมี `DataTable` มาจากแหล่งอื่นแล้ว (เช่น การแปลง CSV) คุณสามารถข้ามโค้ด JDBC และคืนตารางนั้นโดยตรงได้

## ขั้นตอนที่ 3: เตรียมสไตล์ที่ใช้ซ้ำได้ (add number format excel)

เราต้องการให้ทุกคอลัมน์ที่เป็นตัวเลขแสดงผลด้วยทศนิยมสองตำแหน่งและคั่นด้วยเครื่องหมายคอมม่า แทนการกำหนดสไตล์ให้แต่ละเซลล์แยกกัน เราจะสร้างอ็อบเจกต์ `Style` หนึ่งครั้งต่อคอลัมน์และนำกลับมาใช้ซ้ำระหว่างการนำเข้า นี่เป็นวิธีที่มีประสิทธิภาพที่สุดในการ **add number format excel**

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

คุณสามารถปรับสตริงรูปแบบ (`"#,##0.00"`) ให้ตรงกับรูปแบบตัวเลขของ Excel ที่ต้องการได้ สำหรับวันที่ให้ใช้ `styles[i].setCustom("mm-dd-yyyy")` เป็นต้น

## ขั้นตอนที่ 4: นำเข้า DataTable และใช้สไตล์คอลัมน์

ตอนนี้เราจะรวมทุกอย่างเข้าด้วยกัน เมธอด `importDataTable` ที่มีการ overload ให้เราส่ง `DataTable` เข้าไป ระบุว่าต้องการให้แถวแรกเป็นหัวคอลัมน์หรือไม่ และส่งอาร์เรย์สไตล์เข้าไป ซึ่งจะทำให้ **set number format column** โดยอัตโนมัติสำหรับแต่ละเซลล์ในคอลัมน์ที่สอดคล้องกัน

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

เนื่องจากเราใส่ค่า `true` ให้กับแฟล็ก `importColumnNames` แถวแรกของ worksheet จะมีชื่อคอลัมน์จาก `DataTable` แถวต่อ ๆ ไปจะได้รับข้อมูลที่ถูกจัดรูปแบบตามสไตล์ที่เรากำหนดไว้แล้ว

## ขั้นตอนที่ 5: บันทึก workbook เป็น xlsx

ขั้นตอนสุดท้ายคือการบันทึก workbook ที่อยู่ในหน่วยความจำลงไฟล์จริง Aspose.Cells รองรับหลายรูปแบบ; เราจะใช้รูปแบบ XLSX สมัยใหม่ซึ่งเป็นรูปแบบที่แอปพลิเคชันส่วนใหญ่คาดหวังในปัจจุบัน

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

คุณสามารถเปลี่ยนค่า `filePath` ให้เป็นตำแหน่งใดก็ได้ที่ระบบของคุณรับได้ เมธอดจะโยน `IOException` หากไดเรกทอรีไม่มีอยู่หรือคุณไม่มีสิทธิ์เขียน

## ตัวอย่างเต็มที่สามารถรันได้

การรวมส่วนต่าง ๆ เข้าด้วยกันจะได้โปรแกรมที่เป็นอิสระและสามารถคอมไพล์และรันได้ทันที

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

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะสร้างไฟล์ชื่อ **DataTableWithNumberFormat.xlsx** ในไดเรกทอรีทำงานของคุณ เปิดไฟล์ด้วย Microsoft Excel, LibreOffice Calc หรือโปรแกรมดูไฟล์ XLSX ใดก็ได้ แล้วคุณจะเห็น:

| รหัส | จำนวนเงิน | วันที่สร้าง |
|------|-----------|--------------|
| 1    | 1,234.56  | 2023‑01‑15   |
| 2    | 78,900.00 | 2023‑02‑20   |
| …    | …         | …            |

*คอลัมน์ **จำนวนเงิน** แสดงตัวเลขด้วยทศนิยมสองตำแหน่งและคั่นด้วยเครื่องหมายคอมม่า เนื่องจากเราได้ใช้สไตล์ **add number format excel** ที่กำหนดไว้*

## คำถามที่พบบ่อยและการจัดการกรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้าคำสั่ง query ของฉันไม่คืนแถวใดเลย?** | `DataTable` จะว่างเปล่าแต่ยังคงมีการกำหนดคอลัมน์ไว้ Workbook จะมีเพียงแถวหัวเท่านั้น ซึ่งมักเพียงพอสำหรับกระบวนการต่อไป |
| **ฉันจะกำหนดรูปแบบต่าง ๆ ให้แต่ละคอลัมน์อย่างไร?** | ปรับ `buildColumnStyles` ให้ตรวจสอบชื่อคอลัมน์หรือประเภทข้อมูลแล้วกำหนดรูปแบบที่กำหนดเอง (เช่น วันที่, เปอร์เซ็นต์) |
| **ฉันสามารถเขียนโดยตรงไปยัง `ByteArrayOutputStream` ได้หรือไม่?** | ได้. แทนที่ `workbook.save(filePath, SaveFormat.XLSX);` ด้วย ... |

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบอื่น ๆ ในโปรเจคของคุณเอง

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}