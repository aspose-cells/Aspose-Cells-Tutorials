---
category: general
date: 2026-06-18
description: สร้างบทเรียน Java การสร้างไฟล์ Excel แสดงวิธีตั้งค่าสีพื้นหลังของแถว,
  สร้าง Excel จาก DataTable, และบันทึกเวิร์กบุ๊กเป็น XLSX พร้อมการไล่สีแถวสลับกัน.
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: th
og_description: สร้างไฟล์ Excel ด้วย Java ทีละขั้นตอน เรียนรู้การตั้งค่าสีพื้นหลังของแถว
  การใช้สีสลับแถว การสร้าง Excel จาก DataTable และการบันทึกเวิร์กบุ๊กเป็นรูปแบบ XLSX.
og_title: สร้างไฟล์ Excel ด้วย Java – คู่มือการจัดรูปแบบและส่งออกอย่างครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: สร้างไฟล์ Excel ด้วย Java – คู่มือเต็มพร้อมการจัดรูปแบบแถวและการส่งออกเป็น
  XLSX
url: /th/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างไฟล์ Excel ด้วย Java – คู่มือเต็มพร้อมการจัดรูปแบบแถวและการส่งออกเป็น XLSX

เคยสงสัยไหมว่าจะ **create excel file java** อย่างไรให้ดูเป็นมืออาชีพตั้งแต่แรก? คุณไม่ได้อยู่คนเดียว—นักพัฒนามักต้องการวิธีรวดเร็วในการแปลงข้อมูลตารางให้เป็นสเปรดชีตที่จัดรูปแบบสวยงามโดยไม่ต้องเปิด Excel ด้วยตนเอง ในบทแนะนำนี้เราจะเดินผ่านโซลูชันครบวงจร: ดึงข้อมูลจาก `DataTable`, ใส่ **alternating row shading excel**, แล้ว **save workbook as xlsx** สุดท้าย คุณจะได้สคริปต์ที่นำกลับไปใช้ใหม่ได้ในโปรเจค Java ใดก็ได้

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: ไลบรารีที่จำเป็น (Aspose.Cells for Java), โค้ดที่ตั้งค่า **row background color**, วิธี **generate excel from datatable**, และเคล็ดลับปฏิบัติเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป ไม่ฟุ่มเฟือย เพียงตัวอย่างที่พร้อมรันและปรับใช้ได้ทันที

## Prerequisites

ก่อนจะเริ่ม โปรดตรวจสอบว่าคุณมี:

- Java 17 หรือใหม่กว่า (โค้ดทำงานกับ JDK เวอร์ชันล่าสุด)
- Maven หรือ Gradle เพื่อจัดการ dependencies
- ความเข้าใจพื้นฐานเกี่ยวกับ Java collections
- การเข้าถึง Asp Aspose.Cells for Java (รุ่นทดลองหรือแบบลิขสิทธิ์)

หากคุณต้องการทางเลือกแบบโอเพ่นซอร์ส สามารถแปลงตรรกะนี้ไปใช้กับ Apache POI ได้ง่าย—เพียงเปลี่ยนการเรียก API เท่านั้น เพื่อความกระชับ เราจะใช้ Aspose.Cells เนื่องจากเมธอด `importDataTable` ทำให้ขั้นตอน **generate excel from datatable** เป็นบรรทัดเดียว

## Step 1: Set Up the Project and Add Aspose.Cells

เพิ่ม dependency ต่อไปนี้ใน `pom.xml` (Maven) หรือ `build.gradle` (Gradle) เพื่อดึงไลบรารีหลักที่ให้เราจัดการ workbook, style, และสี

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

รีเฟรชโปรเจคแล้ว คุณก็พร้อมเขียนโค้ด Java ที่ **create excel file java** แล้ว

## Step 2: Create the Workbook and Load Your Data

แรกเริ่มเราจะสร้าง `Workbook` ใหม่ จากนั้นรับ `DataTable`—อาจมาจากผลลัพธ์ของ JDBC query, ตัวแปลง CSV, หรือเทเบิลในหน่วยความจำที่คุณมีอยู่แล้ว

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

ตอนนี้เรามี workbook ที่สะอาดและ `DataTable` ที่เต็มข้อมูล ขั้นตอนต่อไปคือการทำให้มองเห็นได้สวยงาม

## Step 3: Define Row Styles – Setting Row Background Color

เราต้องการให้แต่ละแถวมีพื้นหลังที่แตกต่างกัน สลับระหว่างสีฟ้าอ่อนและสีเทาอ่อน เพื่อเพิ่มความอ่านง่ายโดยเฉพาะในรายงานขนาดใหญ่ โค้ดด้านล่างสร้างอาเรย์ `Style`—หนึ่งรายการต่อแถวข้อมูล—and กำหนด **set row background color** ตามดัชนีแถว

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

สังเกตว่าเราใช้ `Color.getLightBlue()` และ `Color.getLightGray()` Aspose.Cells มีพาเลตสีที่หลากหลาย คุณสามารถเปลี่ยนเป็น `Color` ใดก็ได้ตามสีแบรนด์ขององค์กร

## Step 4: Import the DataTable with Styling

ต่อไปเราจะนำข้อมูลและอาเรย์สไตล์มารวมกัน เมธอด `importDataTable` จะคัดลอกแถว, ใส่สไตล์ที่สอดคล้อง, และเพิ่มหัวคอลัมน์หากคุณส่งค่า `true` ให้พารามิเตอร์ `importColumnNames`

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

พารามิเตอร์ `"A1"` บอก Aspose ให้เริ่มเขียนที่มุมบน‑ซ้ายของชีต เนื่องจากเราได้ส่งอาเรย์ `rowStyles` ไปแล้ว แต่ละแถวจึงสืบทอดสีพื้นหลังที่ตั้งไว้ก่อนหน้า ทำให้ได้ **alternating row shading excel** โดยไม่ต้องวนลูปหลังการนำเข้า

## Step 5: Save the Styled Workbook as XLSX

สุดท้าย เราบันทึก workbook ลงดิสก์ เมธอด `save` จะกำหนดรูปแบบไฟล์อัตโนมัติตามส่วนขยาย ดังนั้นการใช้ `.xlsx` จะให้ไฟล์ Office Open XML ที่เปิดได้ใน Excel, Google Sheets, หรือ LibreOffice

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

เมื่อรันเมธอด `main` จะสร้างไฟล์ชื่อ `styledTable.xlsx` ที่โฟลเดอร์รากของโปรเจค เปิดไฟล์แล้วคุณจะเห็นตารางที่จัดรูปแบบเรียบร้อยพร้อมสีแถวสลับ—ตรงกับที่ผู้มีส่วนได้ส่วนเสียคาดหวังจากรายงาน

![Screenshot of styled Excel file created with Java](images/styled_excel_java.png "create excel file java example")

*Image alt text:* **create excel file java** screenshot แสดงการสลับสีแถว

## Why This Approach Works Better Than Manual Cell‑by‑Cell Styling

คุณอาจสงสัยว่าทำไมต้องใช้อาเรย์สไตล์แทนการวนลูปปรับสไตล์แต่ละแถวหลังการนำเข้า คำตอบมีสองประการ:

1. **Performance** – การกำหนดสไตล์ขณะนำเข้าช่วยหลีกเลี่ยงการทำรอบเพิ่มเติมบน worksheet ซึ่งอาจทำให้ช้ากับแถวหลายพันแถว
2. **Maintainability** – ตรรกะสไตล์อยู่ในที่เดียว (`rowStyles`) ทำให้เปลี่ยนสี, เพิ่มขอบ, หรือปรับรูปแบบอื่นได้ง่ายโดยไม่ต้องแก้โค้ดการนำเข้า

หากในภายหลังต้องการเพิ่มสัญญาณภาพเพิ่มเติม (เช่น ไฮไลท์แถวที่คะแนนต่ำกว่าค่าที่กำหนด) เพียงขยายบล็อก `if` ภายในลูป—ไม่มีการเปลี่ยนแปลงอื่น ๆ ที่จำเป็น

## Common Variations and Edge Cases

### Exporting a Large DataTable

เมื่อจัดการกับแถว 100k+ คุณอาจเจอข้อจำกัดของหน่วยความจำ Aspose.Cells รองรับโหมด **streaming**:

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

ตั้งค่าความต้องการหน่วยความจำก่อนสร้างสไตล์ แล้วไลบรารีจะเขียนข้อมูลลงไฟล์ชั่วคราวแทนการเก็บทั้งหมดใน RAM

### Using Apache POI Instead of Aspose.Cells

หากเรื่องลิขสิทธิ์เป็นปัญหา คุณสามารถแทนที่ตรรกะการนำเข้าด้วย `CellStyle` ของ POI แนวคิดยังคงเหมือนเดิม: สร้างสอง `CellStyle`, วนลูปแถว, แล้วใช้ `setFillForegroundColor` พร้อม `IndexedColors` ข้อเสียเดียวคือโค้ดจะยาวขึ้นเล็กน้อย

### Adding Conditional Formatting

สมมติว่าต้องการไฮไลท์คะแนนที่มากกว่า 90 ด้วยสีเขียว เพิ่มโค้ดต่อจากการนำเข้า:

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

ตอนนี้ worksheet มีทั้งสลับสีแถวและไฮไลท์แบบไดนามิก

## Recap: What We Accomplished

- **Create excel file java** จาก `DataTable` ด้วย Aspose.Cells
- **Set row background color** อย่างเป็นโปรแกรม ทำให้ได้ **alternating row shading excel**
- **Save workbook as xlsx** เพื่อความเข้ากันได้กับเครื่องมือสเปรดชีตสมัยใหม่
- แสดงวิธี **generate excel from datatable** อย่างมีประสิทธิภาพและยืดหยุ่น

ทั้งหมดนี้อยู่ในคลาส Java ขนาดกะทัดรัดที่คุณสามารถคัดลอก‑วางเข้าโค้ดของคุณได้ทันที

## Next Steps and Related Topics

หากคุณชอบบทแนะนำนี้ อาจสนใจสำรวจต่อ:

- **Exporting charts** จาก Java ไป Excel (Aspose.Cells chart API)
- **Password‑protecting** workbook ที่สร้าง (`workbook.protect(...)`)
- **Writing large datasets** ด้วย streaming เพื่อลดการใช้หน่วยความจำ
- **Integrating with Spring Boot** เพื่อให้ไฟล์ที่สร้างเป็นการดาวน์โหลดจาก API

หัวข้อเหล่านี้ต่อยอดจากพื้นฐานที่เราได้วางไว้แล้ว—ลองทดลองและขยายต่อไปได้เลย

---

*Happy coding! หากเจออุปสรรคหรือมีไอเดียเพิ่มเติม อย่าลังเลที่จะแสดงความคิดเห็นด้านล่าง เราจะสนทนาต่อกัน*

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจคของคุณ

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Set Excel Row Heights Using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}