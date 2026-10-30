---
category: general
date: 2026-08-20
description: สร้าง workbook Excel ใน Java ด้วย Aspose.Cells ตั้งค่ารูปแบบสกุลเงิน
  เพิ่มฟอนต์หนา และนำเข้าชุดสไตล์สำหรับเซลล์ที่มีสไตล์
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: th
lastmod: 2026-08-20
og_description: สร้างไฟล์ Excel workbook ด้วย Java ตั้งค่ารูปแบบสกุลเงิน เพิ่มฟอนต์หนา
  และเรียนรู้วิธีนำเข้ารูปแบบโดยใช้ Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: สร้างไฟล์ Excel พร้อมเซลล์สกุลเงินที่จัดสไตล์ใน Java
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
title: วิธีสร้างไฟล์ Excel พร้อมรูปแบบสกุลเงินและตัวหนาใน Java
url: /th/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Excel Workbook พร้อมรูปแบบสกุลเงินและตัวอักษรหนาใน Java

หากคุณต้องการ **สร้าง Excel Workbook** ด้วยโปรแกรมมิ่ง คู่มือนี้จะแสดงวิธีทำอย่างละเอียด เราจะสร้าง Workbook, ตั้งค่ารูปแบบสกุลเงิน, เพิ่มตัวอักษรหนา, และใช้คุณลักษณะ **วิธีนำเข้ารูปแบบ** ของ Aspose.Cells เพื่อให้เซลล์ที่นำเข้ามีลักษณะสอดคล้องกันทุกเซลล์

คุณจะได้ไฟล์ `DataTableWithStyleArray.xlsx` ที่พร้อมใช้งาน แสดงตัวเลขเป็นดอลลาร์และทำให้เป็นตัวหนา ไม่ต้องทำการจัดรูปแบบด้วยตนเองใน Excel

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

- Java 17 หรือใหม่กว่า
- ใบอนุญาต Aspose.Cells for Java (หรือคีย์ทดลองฟรี)
- Maven หรือ Gradle เพื่อจัดการ dependency `aspose-cells`
- ความคุ้นเคยพื้นฐานกับคอลเลกชันของ Java และ `DataTable`

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **เคล็ดลับ:** หากพบ `LicenseException` ให้วางไฟล์ใบอนุญาตใน classpath แล้วเรียก `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` ก่อนสร้าง workbook

## วิธีสร้าง Excel Workbook พร้อมเซลล์สกุลเงินที่มีสไตล์

ส่วนนี้ประกอบด้วยขั้นตอนหลัก แต่ละขั้นตอนอธิบาย **ทำไม** ถึงสำคัญ ไม่ใช่แค่ **ทำอะไร** เท่านั้น

### ขั้นตอน 1: เริ่มต้น Workbook และ Worksheet

การสร้าง workbook ใหม่ทำให้คุณมีคอนเทนเนอร์ที่สะอาดสำหรับการจัดรูปแบบต่อไป

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **ทำไม:** อ็อบเจกต์ `Workbook` แทนไฟล์ Excel ทั้งไฟล์ การเข้าถึง `Worksheet` แรกทำให้คุณเริ่มใส่ข้อมูลได้ทันที

### ขั้นตอน 2: สร้าง DataTable พร้อมข้อมูลเชิงตัวเลข

`DataTable` ทำหน้าที่เหมือนตารางฐานข้อมูล ทำให้การนำเข้าข้อมูลหลายแถวเป็นเรื่องง่าย

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **ทำไม:** การใช้ `DOUBLE` รับประกันว่าค่าจะรักษาความแม่นยำของทศนิยมไว้ ซึ่งจำเป็นเมื่อคุณจะ **จัดรูปแบบเซลล์เป็นสกุลเงิน** ต่อไป

### ขั้นตอน 3: กำหนดสไตล์ – รูปแบบสกุลเงินและตัวอักษรหนา

ที่นี่เราจะ **ตั้งค่ารูปแบบสกุลเงิน** และ **เพิ่มตัวอักษรหนา** ให้กับอ็อบเจกต์ `Style`

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **ทำไม:** สตริงรูปแบบ `Number` `$#,##0.00` บอก Excel ให้ถือเซลล์เป็นค่าเงิน ส่วน `setBold(true)` ทำให้ตัวเลขโดดเด่น การใส่สไตล์ลงในอาเรย์เตรียมพร้อมสำหรับขั้นตอน **วิธีนำเข้ารูปแบบ** ต่อไป

### ขั้นตอน 4: ตั้งค่า ImportOptions ให้ใช้สไตล์อาเรย์

Aspose.Cells ให้คุณส่ง `Style[]` ผ่าน `ImportTableOptions` นี่คือวิธี **วิธีนำเข้ารูปแบบ** อย่างเป็นทางการ

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **ทำไม:** หากไม่มี `ImportTableOptions` เซลล์ที่นำเข้าจะใช้สไตล์เริ่มต้น ทำให้สูญเสียรูปแบบสกุลเงินและความหนาที่เรากำหนดไว้

### ขั้นตอน 5: นำเข้า DataTable ไปยัง Worksheet

ตอนนี้เรานำข้อมูลเข้าชีตที่เซลล์ `A1` พร้อมใช้สไตล์อาเรย์โดยอัตโนมัติ

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` ระบุว่าแถวแรกของ `DataTable` มีหัวคอลัมน์
- `"A1"` คือมุมบน‑ซ้ายที่การนำเข้าจะเริ่มต้น

> **ทำไม:** การนำเข้าพร้อมสไตล์อาเรย์รับประกันว่าแต่ละเซลล์ที่นำเข้าจะได้รับสไตล์ **จัดรูปแบบเซลล์เป็นสกุลเงิน** ที่เราจัดเตรียมไว้ล่วงหน้า

### ขั้นตอน 6: บันทึก Workbook ลงดิสก์

สุดท้ายให้เขียน workbook ที่อยู่ในหน่วยความจำลงไฟล์จริง

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **ทำไม:** การบันทึกทำให้รูปแบบที่ตั้งค่าถูกบันทึกไว้ สามารถเปิดไฟล์ใน Excel แล้วเห็นลักษณะที่ต้องการได้

## โค้ดเต็ม

ด้านล่างเป็นคลาส Java ที่พร้อมรัน คัดลอกไปวางใน IDE ของคุณ แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่มีอยู่ แล้วรัน

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

### ผลลัพธ์ที่คาดหวัง

เมื่อเปิด `DataTableWithStyleArray.xlsx` ใน Microsoft Excel คุณควรเห็น:

| จำนวน |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- ตัวเลขแสดงด้วย **รูปแบบสกุลเงิน** (สัญลักษณ์ `$` และทศนิยมสองตำแหน่ง)
- ฟอนต์ของทั้งสองเซลล์เป็น **ตัวหนา** ทำให้เด่นชัด

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|----------|----------------|--------|
| **สกุลเงินต่างประเทศ** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | ใช้สัญลักษณ์ยูโรหรือรูปแบบตามโลคัลอื่น |
| **หลายคอลัมน์ที่มีสไตล์ต่างกัน** | สร้างอ็อบเจกต์ `Style` หลายตัว แล้วใส่ลงใน `styleArray` ตามลำดับคอลัมน์ | แต่ละคอลัมน์สามารถมีรูปแบบตัวเลข, ฟอนต์, พื้นหลัง ฯลฯ ของตนเอง |
| **ชุดข้อมูลขนาดใหญ่** | ใช้ `cells.importDataTable(dataTable, false, "A1", importOptions);` และตั้ง `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | ปรับปรุงประสิทธิภาพโดยข้ามแถวหัวข้อหรือเมตาดาต้าที่ไม่จำเป็น |
| **การใช้สไตล์หลังการนำเข้า** | เรียก `cells.get("A2").setStyle(currencyStyle);` สำหรับเซลล์เดี่ยว | มีประโยชน์เมื่อต้องการจัดรูปแบบเฉพาะบางแถวเท่านั้น |

## เคล็ดลับสำหรับการใช้งานในสภาพแวดล้อมจริง

- **ลงทะเบียนใบอนุญาตล่วงหน้า**: ลงทะเบียนใบอนุญาต Aspose.Cells ก่อนสร้าง workbook เพื่อหลีกเลี่ยงลายน้ำการประเมินผล
- **ความปลอดภัยของเธรด**: อินสแตนซ์ `Workbook` **ไม่** ปลอดภัยต่อเธรดหลาย ๆ ตัว สร้างอินสแตนซ์แยกสำหรับแต่ละเธรดหากต้องสร้างไฟล์จำนวนมากพร้อมกัน
- **การจัดการหน่วยความจำ**: สำหรับชีตขนาดใหญ่มาก ให้พิจารณาใช้ Streaming API ของ `Workbook` (`Workbook` → `WorkbookDesigner`) เพื่อลดการใช้หน่วยความจำ
- **การทดสอบ**: เพิ่ม unit test ที่เปิดไฟล์ที่บันทึกด้วย Apache POI และตรวจสอบว่า `Number` format ของเซลล์ตรงกับ `"$#,##0.00"`  

## สรุป

คุณได้เรียนรู้วิธี **สร้าง Excel Workbook** ด้วย Java, **ตั้งค่ารูปแบบสกุลเงิน**, **เพิ่มตัวอักษรหนา**, และใช้ **วิธีนำเข้ารูปแบบ** อย่างถูกต้องด้วย `ImportTableOptions` ของ Aspose.Cells โซลูชันครบวงจรนี้ช่วยขจัดขั้นตอนการจัดรูปแบบใน Excel ด้วยตนเองและทำให้ทุกเซลล์ที่นำเข้ามีสไตล์ **จัดรูปแบบเซลล์เป็นสกุลเงิน** เดียวกัน

พร้อมรับความท้าทายต่อไปหรือยัง? ลองเพิ่ม Conditional Formatting, ฝัง Chart, หรือส่งออก Workbook เป็น PDF — ทั้งหมดนี้ใช้เทคนิคสไตล์‑อาเรย์เดียวกันได้ Happy coding!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}