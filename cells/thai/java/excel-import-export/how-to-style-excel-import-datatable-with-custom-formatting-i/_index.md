---
category: general
date: 2026-07-03
description: วิธีจัดรูปแบบไฟล์ Excel ด้วย Java เรียนรู้การจัดรูปแบบคอลัมน์วันที่ใน
  Excel, การใช้รูปแบบตัวเลขใน Excel, การส่งออก DataTable ไปเป็นไฟล์ XLSX และการนำเข้า
  DataTable ไปยัง Excel ด้วย Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: th
og_description: วิธีจัดรูปแบบไฟล์ Excel ใน Java บทเรียนนี้แสดงวิธีการจัดรูปแบบคอลัมน์วันที่ใน
  Excel, ใช้รูปแบบตัวเลขใน Excel, ส่งออก DataTable ไปเป็น XLSX และนำเข้า DataTable
  ไปยัง Excel.
og_title: วิธีจัดรูปแบบ Excel – คู่มือ Java สำหรับการกำหนดรูปแบบคอลัมน์แบบกำหนดเอง
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: วิธีจัดรูปแบบ Excel – นำเข้า DataTable พร้อมการจัดรูปแบบแบบกำหนดเองใน Java
url: /th/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีจัดรูปแบบ Excel – นำเข้า DataTable พร้อมการจัดรูปแบบแบบกำหนดเองใน Java

เคยสงสัย **วิธีจัดรูปแบบ Excel** ด้วยโปรแกรมโดยไม่ต้องเปิดไฟล์ด้วยตนเองหรือไม่? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ นักพัฒนาหลายคนต้องสร้างรายงานที่คอลัมน์แรกเป็นตัวหนา, คอลัมน์ที่สองแสดงวันที่, และส่วนที่เหลือมีการจัดวางที่เรียบง่าย ในคู่มือนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่ง **นำเข้า DataTable ไปยัง Excel**, ใส่หัวข้อเป็นตัวหนา, จัดรูปแบบคอลัมน์วันที่, และสุดท้าย **ส่งออก DataTable เป็น XLSX**  

เราจะใช้ Aspose.Cells for Java, แต่แนวคิดนี้สามารถนำไปใช้กับไลบรารีใดก็ได้ที่ให้คุณทำงานกับสไตล์ได้ โดยเมื่อเสร็จคุณจะได้รูปแบบที่นำกลับมาใช้ได้สำหรับ **apply number format Excel** cells, **format column date Excel**, และส่งมอบเวิร์กบุ๊กที่ดูเป็นมืออาชีพให้ผู้ใช้ของคุณ

## Prerequisites

- Java 17 (หรือ JDK ล่าสุดใดก็ได้)  
- Aspose.Cells for Java 23.9 หรือใหม่กว่า (เวอร์ชันทดลองฟรีก็ใช้ได้)  
- โครงสร้างแบบ `DataTable`‑like (ตัวอย่างใช้ mock ง่าย)  
- IDE ที่คุณชอบ (IntelliJ IDEA, Eclipse, VS Code…)

ไม่ต้องใช้ปลั๊กอิน Maven เพิ่มเติม; เพียงแค่เพิ่มไฟล์ JAR ของ Aspose.Cells ไปยัง classpath ของคุณ

---

## Step 1: Obtain the Source DataTable – “Export DataTable to XLSX” Preparation

ก่อนที่เราจะ **import datatable into excel** เราต้องมีอ็อบเจกต์ `DataTable` ที่แทนข้อมูลที่คุณต้องการส่งออก ในโครงการจริงคุณอาจดึงข้อมูลนี้จากฐานข้อมูล, ไฟล์ CSV, หรือ API สำหรับบทเรียนนี้เราจะ mock ตารางขนาดเล็ก:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Why this matters:** การได้ข้อมูลที่ถูกต้องตั้งแต่แรกหมายความว่าตรรกะการจัดรูปแบบที่เหลือสามารถมุ่งเน้นที่การนำเสนอเท่านั้น ไม่ต้องกังวลเรื่องการจัดการข้อมูล

---

## Step 2: Create an Array to Hold Style Definitions for Each Column

Aspose.Cells ให้คุณส่งอาร์เรย์ **Style[]** เมื่อทำการนำเข้า `DataTable` แต่ละรายการจะสอดคล้องกับคอลัมน์และกำหนดว่าคอลัมน์นั้นจะมีลักษณะอย่างไรหลังการนำเข้า เรามาจัดสรรอาร์เรย์ตามจำนวนคอลัมน์กัน:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** หากคุณมีหลายคอลัมน์, พิจารณาสร้างอาร์เรย์ในลูปและใช้ `Style` ตัวเดียวซ้ำเมื่อรูปแบบเดียวกัน นี่จะช่วยลดการใช้หน่วยความจำ

---

## Step 3: Define the Styles – Bold Header & Date Formatting

ตอนนี้เราจะตอบคำถามคลาสสิก **format column date excel** และยังแสดง **apply number format excel** สำหรับคอลัมน์อื่น ๆ

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**What’s happening here?**  
- `StyleNumberFormat.DATE` บอก Excel ให้ถือค่าของเซลล์เป็นวันที่สั้น (เช่น *01/31/2024*)  
- `StyleNumberFormat.CURRENCY_USD` จะเพิ่มสัญลักษณ์ `$` และแสดงสองตำแหน่งทศนิยมโดยอัตโนมัติ  
- การตั้งค่าแบบอักษรเป็นตัวหนาที่คอลัมน์แรกทำให้หัวข้อเด่นชัด ซึ่งเป็นความต้องการบ่อยเมื่อคุณ **how to style excel** สเปรดชีตเพื่อความอ่านง่าย

> **Edge case:** หากข้อมูลต้นทางของคุณมีสตริงที่จัดรูปแบบแล้วอยู่แล้ว, คุณอาจต้องแปลงเป็นอ็อบเจกต์ `java.util.Date` ก่อนนำเข้า; ไม่เช่นนั้น Excel จะถือเป็นข้อความธรรมดา

---

## Step 4: Create a New Workbook and Access Its First Worksheet

เวิร์กบุ๊กใหม่ให้ผืนผ้าใบที่สะอาด เราจะดึงเวิร์กชีตแรกซึ่งเป็นที่ที่การนำเข้าจะถูกวางไว้

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Why a new workbook?** การเริ่มจากศูนย์รับประกันว่าไม่มีสไตล์ที่เหลืออยู่หรือแถวที่ซ่อนอยู่มาขัดขวางผลลัพธ์สุดท้าย—สิ่งสำคัญเมื่อคุณ **how to style excel** ไฟล์อย่างสม่ำเสมอในหลาย ๆ ครั้ง

---

## Step 5: Import the DataTable with the Column Styles

นี่คือหัวใจของการทำงาน: ป้อน `DataTable` เข้าไปในชีตพร้อมกับอาร์เรย์สไตล์ที่เราสร้างไว้

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Explanation:**  
- `importDataTable` คัดลอกทั้งแถวหัวเรื่องและแถวข้อมูล  
- อาร์เรย์ `columnStyles` สอดคล้องกับแต่ละคอลัมน์, ดังนั้นหัวเรื่องคอลัมน์แรกจะเป็นตัวหนา, คอลัมน์ที่สองจะแสดงวันที่, และคอลัมน์ที่สามจะแสดงเป็นสกุลเงิน  
- บรรทัดเดียวนี้แทนที่ขั้นตอนการจัดรูปแบบเซลล์ทีละเซลล์หลายสิบขั้นตอน, แสดงวิธีที่สะอาดในการ **apply number format excel** ด้วยโปรแกรม

---

## Step 6: Save the Styled Workbook – Completing the “Export DataTable to XLSX”

สุดท้ายเราบันทึกเวิร์กบุ๊กลงดิสก์ ปรับเส้นทางให้เป็นโฟลเดอร์ที่เขียนได้บนเครื่องของคุณ

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

เปิดไฟล์ใน Excel แล้วคุณควรเห็น:

- คอลัมน์ **ID** มีหัวเรื่องเป็นตัวหนา  
- คอลัมน์ **OrderDate** ถูกจัดรูปแบบเป็นวันที่ (เช่น *04/27/2024*)  
- คอลัมน์ **Total** แสดงด้วยสัญลักษณ์ดอลลาร์และสองตำแหน่งทศนิยม

> **Pro tip:** หากต้องการสนับสนุนเวอร์ชัน Excel เก่ากว่า, เรียก `workbook.save(outputPath, SaveFormat.XLS)` แทนค่าเริ่มต้น XLSX

---

## Step 7: Verify the Result & Optional Tweaks

เป็นการปฏิบัติที่ดีที่จะตรวจสอบไฟล์ที่สร้างขึ้น, โดยเฉพาะอย่างยิ่งเมื่อทำรายงานอัตโนมัติให้ผู้มีส่วนได้ส่วนเสีย

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

หาก `isBold` พิมพ์ค่า `true`, ขั้นตอน **how to style excel** ของคุณทำงานสำเร็จ จากนี้คุณสามารถ:

- เพิ่ม conditional formatting (เช่น ไฮไลท์ยอดรวม > $200)  
- Freeze แถวบนสุดเพื่อการเลื่อนที่ง่ายขึ้น  
- แทรกแผนภูมิที่อ้างอิงข้อมูลที่นำเข้า

ส่วนขยายทั้งหมดนี้ทำตามรูปแบบเดียวกัน: กำหนด `Style`, นำไปใช้, แล้วบันทึก

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I style more than one column the same way?** | Yes—reuse a single `Style` instance for all columns that share formatting. |
| **What if my DataTable has more columns than styles?** | Any column without a corresponding entry in `columnStyles` will use the default style. |
| **How do I change the date format to “dd‑MMM‑yyyy”?** | Use `columnStyles[1].setCustom("#dd-MMM-yyyy#");` instead of the built‑in `DATE`. |
| **Is there a way to auto‑size columns after import?** | Call `worksheet.autoFitColumns();` after `importDataTable`. |
| **Will this work on Linux/macOS?** | Absolutely—Aspose.Cells is platform‑agnostic as long as you have a compatible JDK. |

---

## Conclusion

คุณมีตัวอย่างครบวงจรของ **how to style Excel** โดย **importing datatable into excel**, **format column date excel**, และ **apply number format excel** ด้วย Java โค้ดแสดงขั้นตอนเต็มจาก **export datatable to xlsx** จนถึงการเปิดไฟล์ใน Excel, ครอบคลุมทั้ง *what* และ *why* ของแต่ละขั้นตอน  

ลองปรับอาร์เรย์สไตล์, เพิ่มคอลัมน์, หรือเชื่อมต่อกับการสืบค้นฐานข้อมูลจริง รูปแบบเดียวกันนี้จะช่วยให้คุณสร้างรายงานที่ดูเป็นมืออาชีพได้เพียงคลิกเดียว, ไม่ต้องทำการจัดรูปแบบด้วยตนเอง

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Image alt text: “Styled Excel worksheet created using Java and Aspose.Cells, showing bold header and formatted date column.”*


## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}