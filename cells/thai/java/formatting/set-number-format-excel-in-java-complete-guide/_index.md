---
category: general
date: 2026-06-18
description: ตั้งค่ารูปแบบตัวเลขใน Excel ด้วย Java และเรียนรู้การใช้สัญลักษณ์วิทยาศาสตร์ใน
  Java, เขียนค่าลงในเซลล์, ตั้งค่าตัวเลขที่สำคัญ, และส่งออกข้อมูลเป็นไฟล์ xlsx ภายในไม่กี่นาที.
draft: false
keywords:
- set number format excel
- scientific notation java
- write value to cell
- set significant digits
- export data to xlsx
language: th
og_description: ตั้งค่ารูปแบบตัวเลขใน Excel ด้วย Java เรียนรู้วิธีใช้การแสดงผลแบบวิทยาศาสตร์ใน
  Java เขียนค่าไปยังเซลล์ ตั้งค่าตัวเลขที่สำคัญ และส่งออกข้อมูลเป็นไฟล์ xlsx อย่างมีประสิทธิภาพ
og_title: ตั้งค่ารูปแบบตัวเลขใน Excel ด้วย Java – คู่มือทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  headline: Set Number Format Excel in Java – Complete Guide
  type: TechArticle
- description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  name: Set Number Format Excel in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '| A (Formatted) | |---------------| | 1.235E7 |'
  - name: How do I change the number of significant digits?
    text: Just edit the format string. For three digits use `"0.###E0"`; for six digits
      use `"0.######E0"`.
  - name: What if I need a different locale (comma as decimal separator)?
    text: Add a locale‑aware format, e.g., `df.getFormat("0,####E0")`. Excel respects
      the user’s regional settings, so the comma will appear only if the workbook
      is opened on a system that uses it.
  - name: Can I apply the same style to an entire column?
    text: Absolutely. Create the style once (as shown) and then loop through rows,
      applying `cell.setCellStyle(sciStyle)` each time. For large sheets, consider
      using `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – it’s faster and
      keeps the code tidy.
  - name: What if I’m stuck with an older Java version that doesn’t support `var`?
    text: Replace `var` with the explicit type (`Workbook workbook = new XSSFWorkbook();`).
      The rest of the code stays identical.
  type: HowTo
tags:
- Java
- Excel
- Data Export
title: ตั้งค่ารูปแบบตัวเลขใน Excel ด้วย Java – คู่มือฉบับสมบูรณ์
url: /th/java/formatting/set-number-format-excel-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่ารูปแบบตัวเลขใน Excel ด้วย Java – คู่มือเต็ม

เคยสงสัยไหมว่า **set number format Excel** จากโปรแกรม Java อย่างไรโดยไม่ต้องบีบผม? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะสร้างรายงานการเงินหรือบันทึกข้อมูลเซนเซอร์ การทำให้ตัวเลขขนาดใหญ่แสดงผลอย่างสวยงามในไฟล์ *.xlsx* เป็นทักษะที่ต้องมี

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจร: การสร้าง workbook, การกำหนด **scientific notation java**, การจำกัด **set significant digits**, การเขียนค่าไปยังเซลล์, และสุดท้าย **export data to xlsx**. เมื่อจบคุณจะได้โค้ดสั้น ๆ ที่พร้อมนำไปใช้ในโปรเจคของคุณทันที

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการเริ่มต้น workbook ด้วย JExcel‑API (หรือ Apache POI) ใน Java.  
- คำสั่งที่ต้องใช้เพื่อ **set number format excel** ให้บังคับใช้ scientific notation.  
- วิธี **write value to cell** พร้อมรักษาความแม่นยำ.  
- การปรับตั้งค่า workbook เพื่อ **set significant digits** ให้เป็นจำนวนที่กำหนดเอง.  
- การบันทึกไฟล์เพื่อให้เปิดได้ในแอปสเปรดชีตสมัยใหม่ทุกตัว (**export data to xlsx**).  

ไม่มีบริการภายนอก ไม่มีเวทมนตร์ ใช้แค่ Java ธรรมดาและคลาสที่มีเอกสารครบถ้วน

---

## ข้อกำหนดเบื้องต้น

- JDK 17 หรือใหม่กว่า (โค้ดทำงานได้บนเวอร์ชันเก่าเช่นกัน แต่ตัวอย่างใช้ไวยากรณ์ `var` เพื่อความกระชับ).  
- Maven หรือ Gradle เพื่อดึง dependency `org.apache.poi:poi-ooxml`.  
- ความเข้าใจพื้นฐานเกี่ยวกับ Java collections – หากคุณเคยเขียน `for` loop มาก่อนก็พร้อมแล้ว.

---

## ขั้นตอนที่ 1: เพิ่ม Dependency ของ Apache POI

หากคุณใช้ Maven ให้วางโค้ดนี้ลงในไฟล์ `pom.xml` ของคุณ ผู้ใช้ Gradle สามารถแปลงเป็นไวยากรณ์ `implementation` ได้เอง

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

> **เคล็ดลับ:** ควรอัปเดต POI ให้เป็นเวอร์ชันล่าสุด เส้นทาง 5.x มีการสนับสนุนรูปแบบตัวเลขและ worksheet ขนาดใหญ่ที่ดีกว่า

---

## ขั้นตอนที่ 2: สร้าง Workbook และเข้าถึงการตั้งค่า  

สิ่งแรกที่เราต้องการคืออ็อบเจกต์ workbook ใหม่ Apache POI ไม่ได้มีคลาส `WorkbookSettings` เหมือน JExcel แต่เราสามารถทำผลเช่นเดียวกันได้โดยสร้าง `CellStyle` ในขั้นตอนต่อไป

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise a new workbook (this is where we "set number format excel")
        Workbook workbook = new XSSFWorkbook();   // XSSFWorkbook -> .xlsx format
        // No explicit WorkbookSettings, we'll configure a CellStyle later
```

ทำไมเราต้องเริ่มด้วย **new workbook**? คิดว่าเป็นผืนผ้าใบเปล่า ทุกการตัดสินใจเกี่ยวกับการจัดรูปแบบที่ทำต่อจากนี้จะถูกนำไปใช้กับผืนผ้าใบนี้

---

## ขั้นตอนที่ 3: กำหนด CellStyle สำหรับ Scientific Notation และ Significant Digits  

Apache POI ให้คุณสร้างสตริงรูปแบบข้อมูล เพื่อบังคับใช้ **scientific notation java** และจำกัดจำนวนหลัก เราใช้แพทเทิร์น `"0.####E0"` – สัญลักษณ์ `#` ควบคุมจำนวนหลักสำคัญที่จะแสดง

```java
import org.apache.poi.ss.usermodel.CellStyle;
import org.apache.poi.ss.usermodel.DataFormat;

// Inside main(), after workbook creation:
DataFormat df = workbook.createDataFormat();
CellStyle sciStyle = workbook.createCellStyle();

// "0.####E0" -> 0 before the decimal, up to 4 significant digits after, exponent part
sciStyle.setDataFormat(df.getFormat("0.####E0"));
```

*เกิดอะไรขึ้น?* สตริงรูปแบบบอก Excel ว่า “แสดงตัวเลขในรูปแบบ scientific notation แต่ให้มีสูงสุดสี่หลักสำคัญ”. หากต้องการความแม่นยำอื่น ๆ เพียงเพิ่มหรือลบสัญลักษณ์ `#` ตามต้องการ

---

## ขั้นตอนที่ 4: เขียนตัวเลขขนาดใหญ่ลงในเซลล์  

ต่อไปเราจะ **write value to cell** เซลล์ *A1* ด้วยสไตล์ที่สร้างไว้ `sciStyle`. อ็อบเจกต์ `Sheet` และ `Row` มีน้ำหนักเบา การสร้างแบบ on‑the‑fly จึงเร็วและประหยัด

```java
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Cell;

// Continue inside main():
Sheet sheet = workbook.createSheet("Numbers");

// Row 0 (first row), Cell 0 (column A)
Row row = sheet.createRow(0);
Cell cell = row.createCell(0);
cell.setCellValue(12345678.9);   // The raw value we want to store
cell.setCellStyle(sciStyle);    // Apply our scientific notation style
```

สังเกตว่าเราไม่ต้องแคสต์ค่าตัวเลข; POI จัดการ `double` ให้โดยอัตโนมัติ การแนบ `sciStyle` ทำให้เมื่อผู้ใช้เปิดไฟล์ Excel จะแสดง `1.235E7` (ปัดเป็นสี่หลักสำคัญ) แทนการแสดงเป็นสตริง 8 หลักดิบ

---

## ขั้นตอนที่ 5: บันทึก Workbook – Export Data to XLSX  

ขั้นตอนสุดท้ายคือ **export data to xlsx** เราจะเขียน workbook ไปยังไฟล์ในไดเรกทอรีปัจจุบัน แต่คุณสามารถระบุพาธใดก็ได้ตามต้องการ

```java
import java.io.FileOutputStream;

// Still inside main():
try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
    workbook.write(out);
}
workbook.close();   // Free resources
System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

เมื่อคุณดับเบิล‑คลิก `sigDigits.xlsx` คุณจะเห็นคอลัมน์ **A** แสดง `1.235E7` – พอดีกับที่เราตั้งค่าไว้

### ผลลัพธ์ที่คาดหวัง

| A (Formatted) |
|---------------|
| 1.235E7       |

หากคุณเปิดไฟล์และเปลี่ยนรูปแบบเซลล์ด้วยตนเอง คุณจะสังเกตว่าค่าตามฐานยังคงเป็น `12345678.9`. นั่นคือความมหัศจรรย์ของ **set number format excel**: การแสดงผลเปลี่ยน แต่ข้อมูลยังคงบริสุทธิ์

---

## คำถามที่พบบ่อย & กรณีขอบเขต

### จะเปลี่ยนจำนวนหลักสำคัญได้อย่างไร?

เพียงแก้ไขสตริงรูปแบบ สำหรับสามหลักใช้ `"0.###E0"`; สำหรับหกหลักใช้ `"0.######E0"`.

### ถ้าต้องการ locale ที่ใช้คอมม่าเป็นตัวคั่นทศนิยมล่ะ?

เพิ่มรูปแบบที่รับ locale เช่น `df.getFormat("0,####E0")`. Excel จะเคารพการตั้งค่าภูมิภาคของผู้ใช้ ดังนั้นคอมม่าอาจปรากฏเฉพาะเมื่อเปิด workbook บนระบบที่ตั้งค่าเช่นนั้น

### สามารถใช้สไตล์เดียวกันกับคอลัมน์ทั้งหมดได้ไหม?

ทำได้แน่นอน สร้างสไตล์ครั้งเดียว (ตามที่แสดง) แล้ววนลูปผ่านแถว ๆ ไปใช้ `cell.setCellStyle(sciStyle)` ทุกครั้ง สำหรับ sheet ขนาดใหญ่ ควรใช้ `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – เร็วกว่าและโค้ดดูสะอาด

### ถ้าติดอยู่กับ Java เวอร์ชันเก่าที่ไม่รองรับ `var` จะทำอย่างไร?

เปลี่ยน `var` เป็นประเภทที่ระบุอย่างชัดเจน (`Workbook workbook = new XSSFWorkbook();`). ส่วนอื่นของโค้ดยังคงเหมือนเดิม

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.*;

import java.io.FileOutputStream;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (set number format excel)
        Workbook workbook = new XSSFWorkbook();

        // Define a style for scientific notation with 4 significant digits
        DataFormat df = workbook.createDataFormat();
        CellStyle sciStyle = workbook.createCellStyle();
        sciStyle.setDataFormat(df.getFormat("0.####E0")); // set significant digits

        // Access the first worksheet and write a large number into cell A1
        Sheet sheet = workbook.createSheet("Numbers");
        Row row = sheet.createRow(0);
        Cell cell = row.createCell(0);
        cell.setCellValue(12345678.9);   // write value to cell
        cell.setCellStyle(sciStyle);    // apply scientific notation

        // Save the workbook – export data to xlsx
        try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
            workbook.write(out);
        }
        workbook.close();

        System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

รันคลาสนี้ เปิด `sigDigits.xlsx` แล้วคุณจะเห็นตัวเลขแสดงในรูปแบบ scientific notation พร้อมสี่หลักสำคัญพอดี นั่นคือขั้นตอน **set number format excel** ทั้งหมดใน Java

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **set number format excel** จาก Java: สร้าง workbook, สร้างสไตล์ scientific‑notation ที่ **set significant digits**, **write value to cell**, และสุดท้าย **export data to xlsx**. วิธีนี้เบา ใช้แค่ Apache POI และทำงานได้บนทุกแพลตฟอร์มที่รองรับ Java

ต่อไปคุณอาจต้องการ:

- เพิ่ม conditional formatting เพื่อไฮไลท์ค่าที่อยู่นอกช่วง.  
- สร้างหลาย sheet ที่มีสไตล์ตัวเลขต่างกัน (เช่น currency vs. scientific).  
- ใช้ `SXSSFWorkbook` สำหรับการสตรีมข้อมูลขนาดใหญ่เพื่อประหยัดหน่วยความจำ

ลองทำตามดู แล้วคุณจะเป็นคนที่ทีมของคุณพึ่งพาในการทำออโตเมชัน Excel หากมีคำถามหรือกรณีการใช้งานแปลก ๆ คอมเมนต์ด้านล่างได้เลย – Happy coding!

--- 

*ภาพแสดงขั้นตอนการทำงาน (alt text: “set number format excel workflow diagram showing Java code, scientific notation, and export to xlsx”)*


## คุณควรเรียนรู้อะไรต่อไป?


บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจคของคุณ

- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/german/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/french/java/cell-operations/aspose-cells-java-set-active-cell-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}