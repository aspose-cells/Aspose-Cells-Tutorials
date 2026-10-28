---
category: general
date: 2026-07-03
description: รวมการส่งออกสูตรใน Java เพื่อแปลงเซลล์ Excel เป็นข้อความโดยใช้ Aspose.Cells.
  เรียนรู้วิธีพิมพ์ช่วง Excel และดึงค่าข้อความของเซลล์อย่างมีประสิทธิภาพ.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: th
og_description: รวมการส่งออกสูตรใน Java เพื่อแปลงเซลล์ Excel เป็นข้อความ คู่มือแบบขั้นตอนแสดงวิธีพิมพ์ช่วง
  Excel และดึงค่าของเซลล์เป็นสตริง
og_title: รวมการส่งออกสูตรใน Java – แปลงเซลล์ Excel เป็นข้อความ
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: รวมการส่งออกสูตรใน Java – แปลงเซลล์ Excel เป็นข้อความ
url: /th/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รวมการส่งออกสูตรใน Java – แปลงเซลล์ Excel เป็นข้อความ

เคยต้องการ **include formulas export** ขณะดึงข้อมูลออกจากเวิร์กบุ๊ก Excel หรือไม่? บางทีคุณอาจกำลังสร้างบริการรายงานที่ต้องคงสูตรเดิมไว้ในขณะที่ยังส่งมอบข้อความที่เป็นระเบียบ. ในกรณีนั้น คุณอยู่ในที่ถูกต้อง คู่มือนี้จะพาคุณผ่านการแปลงเซลล์ Excel เป็นข้อความธรรมดา—*including* สูตรที่ฝังอยู่—โดยใช้ Aspose.Cells for Java.

เราจะพูดถึงวิธี **print Excel range**, ปรับ **export table options**, และสุดท้าย **get cell values string** ที่คุณสามารถบันทึก, ส่งผ่าน API, หรือเก็บไว้ในฐานข้อมูล. เมื่อจบคุณจะมีโค้ดสั้นที่รันได้เต็มรูปแบบและเข้าใจเหตุผลเบื้องหลังแต่ละการเรียกใช้.

## สิ่งที่คุณจะได้เรียนรู้

- โปรแกรม Java ที่พร้อมคัดลอก‑วางครบถ้วน สามารถอ่านไฟล์ `.xlsx`, เลือกช่วง, และส่งออกเป็นสตริงที่จัดรูปแบบแล้ว
- ความเข้าใจในคลาส `ExportTableOptions` และเหตุผลที่ต้องสลับ `setExportAsString` กับ `setIncludeFormula`
- เคล็ดลับการจัดการเวิร์กชีตขนาดใหญ่, ประเภทข้อมูลต่าง ๆ, และการปรับแต่งรูปแบบผลลัพธ์
- เช็คลิสต์สั้น ๆ สำหรับข้อผิดพลาดทั่วไป (เช่น เซลล์ที่รวมกัน, แถวที่ซ่อน, และรูปแบบตัวเลขตามโลคัล)

### ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับเวอร์ชันเก่าได้ แต่เราจะใช้ LTS ล่าสุด)
- Aspose.Cells for Java 23.10 (หรือเวอร์ชันล่าสุดใด ๆ) — สามารถดาวน์โหลดจาก Maven Central
- ตัวอย่างไฟล์ `input.xlsx` ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม (เส้นทางถูกกำหนดแบบคงที่ในตัวอย่างเพื่อความชัดเจน)

ถ้าคุณมีทั้งหมดนี้แล้ว, มาเริ่มกันเลย.

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Dependencies

แรกสุด, สร้างโปรเจกต์ Maven (หรือ Gradle หากคุณชอบ). เพิ่ม dependency ของ Aspose.Cells ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** หากคุณใช้พร็อกซีขององค์กร, ตรวจสอบให้แน่ใจว่ารีโพซิทอรีเข้าถึงได้; มิฉะนั้นการสร้างจะล้มเหลวด้วยข้อผิดพลาด “Could not resolve dependencies”.

เมื่อ Maven ดาวน์โหลดเสร็จ, คุณพร้อมเขียนโค้ด Java แล้ว.

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กและดึงแผ่นงานที่ต้องการ

บรรทัดแรกของตัวอย่างโค้ดแสดงวิธีเปิดเวิร์กบุ๊กที่มีอยู่:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางแบบ absolute หรือ relative ไปยังไฟล์ของคุณ. คอนสตรัคเตอร์ `Workbook` จะตรวจจับรูปแบบไฟล์โดยอัตโนมัติ (XLS, XLSX, CSV, ฯลฯ) ดังนั้นคุณไม่จำเป็นต้องระบุ.

ต่อไป, เราดึงแผ่นแรก:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

ทำไมต้องเป็นแผ่นแรก? ในเทมเพลตหลายแบบข้อมูลอยู่บนแท็บแรก, แต่คุณสามารถระบุดัชนีใดก็ได้หรือแม้ใช้ `get("SheetName")` หากต้องการอ้างอิงตามชื่อ.

## ขั้นตอนที่ 3: กำหนดช่วงที่คุณต้องการส่งออก

ตอนนี้มาถึงหัวใจของการ **convert excel cells text**. คุณบอก Aspose.Cells ว่าต้องการดึงเซลล์ใดโดยสร้างอ็อบเจ็กต์ `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

สตริง `"A1:C3"` เป็นที่อยู่แบบ A1‑style คลาสสิก. สามารถสร้างแบบโปรแกรมได้เช่นกัน:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

ความยืดหยุ่นนี้ช่วยเมื่อขนาดช่วงเป็นแบบไดนามิก—เช่น คุณอ่านแถวสุดท้ายที่ใช้ด้วย `ws.getCells().getMaxDataRow()`.

## ขั้นตอนที่ 4: ตั้งค่า Export Table Options เพื่อรวมสูตร

นี่คือที่ที่ **include formulas export** ทำงาน. โดยค่าเริ่มต้น, Aspose.Cells จะคืนค่า *displayed* (ค่าที่แสดง). หากเซลล์มี `=SUM(A1:A3)`, คุณจะได้ตัวเลขที่คำนวณแล้ว, ไม่ใช่ข้อความสูตร. เพื่อเปลี่ยนแปลง, ตั้งค่า `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

ทำไมต้องตั้งค่าสองฟลัก? `setExportAsString(true)` บอก API ให้ต่อเซลล์ด้วยตัวคั่นเริ่มต้น (แท็บสำหรับคอลัมน์, newline สำหรับแถว). `setIncludeFormula(true)` เปลี่ยนแหล่งค่าจาก “ค่าที่แสดง” เป็น “สูตรดิบ”. หากต้องการค่าอย่างเดียว, ตั้งเป็น `false`.

### การปรับแต่งเพิ่มเติม

- `eto.setExportHiddenRows(true);` – รวมแถวที่ซ่อนใน Excel
- `eto.setExportHiddenColumns(true);` – รวมคอลัมน์ที่ซ่อน
- `eto.setExportAsHTML(true);` – รับผลเป็น HTML แทนข้อความธรรมดา

ลองทดลองได้ตามสบาย; คลาส options นี้เป็นสนามเด็กเล่นของ **export table options**.

## ขั้นตอนที่ 5: ดึงช่วงเป็นสตริงที่จัดรูปแบบแล้ว

ตอนนี้เราดึงข้อมูล:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

สตริง `txt` ที่คืนมาจะมีลักษณะประมาณนี้ (สมมติว่า A1:C3 มีค่าผสมสูตรและค่าอื่น):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

สังเกตว่าแท็บ (`\t`) คั่นคอลัมน์และ newline (`\n`) คั่นแถว. คุณสามารถแยกสตริงนี้ต่อไปเพื่อสร้างอาเรย์ 2‑D ได้:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## ขั้นตอนที่ 6: พิมพ์ผลลัพธ์ – “Print Excel Range” ทำให้เรียบง่าย

สุดท้าย, เราแสดงสตริงลงคอนโซล:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

การรันโปรแกรมจะพิมพ์ผลลัพธ์ที่แสดงข้างต้นอย่างตรงกัน. จากนี้คุณสามารถบันทึกสตริงลงไฟล์ล็อก, ส่งผ่าน HTTP, หรือเก็บในเอกสาร NoSQL ได้.

## ตัวอย่างเต็มพร้อมรัน

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมที่สมบูรณ์. คัดลอก, วาง, แล้วกด **Run**—ไม่มี import ที่หายไป.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### ผลลัพธ์ที่คาดหวัง (ตัวอย่าง)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

หากเวิร์กบุ๊กของคุณมีตัวเลขที่ฟอร์แมตเป็นวันที่, จะปรากฏในรูปแบบตามโลคัล (เช่น `2026‑07‑03`). เพื่อบังคับให้เป็นรูปแบบ ISO, คุณสามารถปรับ `ExportTableOptions` ด้วย `NumberFormat` ที่กำหนดเอง.

## การจัดการกรณีขอบและคำถามทั่วไป

### ถ้าช่วงมีเซลล์ที่รวมกัน (merged cells) อย่างไร?

เซลล์ที่รวมกันจะถือเป็นค่าของเซลล์ซ้ายบน. ส่วนอื่นของพื้นที่ที่รวมจะปรากฏเป็นสตริงว่าง. หากต้องการที่อยู่ของช่วงที่รวม, ให้เรียก `Cell.getMergedRange()` ก่อนส่งออก.

### ฉันสามารถส่งออกชีตขนาดใหญ่ (หลายแสนแถว) ได้หรือไม่?

ได้, แต่ต้องระวังการใช้หน่วยความจำ. ใช้ `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` เพื่อให้ Aspose.Cells สตรีมข้อมูลไปยังดิสก์. อีกทางหนึ่ง, พิจารณาส่งออกเป็นชิ้นส่วน (เช่น 10 000 แถวต่อครั้ง) เพื่อทำให้สตริงจัดการได้ง่ายขึ้น.

### ฉันจะเปลี่ยนตัวคั่นคอลัมน์ได้อย่างไร?

`ExportTableOptions` มีเมธอด `setSeparator(char separator)`. สำหรับผลลัพธ์แบบ CSV, ตั้งค่าเป็น `','`:

```java
eto.setSeparator(',');
```

### สูตรเคารพการอ้างอิงภายนอกหรือไม่?

หากสูตรอ้างอิงไปยังเวิร์กบุ๊กอื่น, Aspose.Cells จะเก็บข้อความอ้างอิง (`='[Other.xlsx]Sheet1'!A1`). จะไม่ประมวลผลค่าภายนอกจนกว่าคุณจะโหลดเวิร์กบุ๊กนั้นด้วย.

## เคล็ดลับระดับมืออาชีพสำหรับโค้ดพร้อมใช้งานใน Production

- **Cache the workbook** if you’re reading the

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}