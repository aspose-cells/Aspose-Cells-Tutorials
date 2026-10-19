---
category: general
date: 2026-06-27
description: เรียนรู้วิธีนำเข้า DataTable ไปยัง Excel พร้อมสีคอลัมน์สลับ คู่มือขั้นตอนการนำเข้าข้อมูลพร้อมการจัดรูปแบบและตั้งค่าสีฟอนต์ของคอลัมน์โดยใช้
  Java.
draft: false
keywords:
- alternating column colors
- import data with formatting
- import datatable to excel
- set column font color
- how to import datatable
language: th
og_description: เชี่ยวชาญการสลับสีคอลัมน์ขณะนำเข้า DataTable ไปยัง Excel คู่มือนี้แสดงวิธีนำเข้าข้อมูลพร้อมการจัดรูปแบบและตั้งค่าสีฟอนต์ของคอลัมน์ใน
  Java.
og_title: สีคอลัมน์สลับใน Excel – นำเข้า DataTable พร้อมการจัดรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  headline: Alternating Column Colors in Excel – Import DataTable with Formatting
  type: TechArticle
- description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  name: Alternating Column Colors in Excel – Import DataTable with Formatting
  steps:
  - name: Prerequisites
    text: '- Java 8+ (the code works with newer releases as well). - Apache POI 5.x
      on your classpath – the library that talks to Excel files. - A `DataTable` implementation
      that offers `getColumns()` and `size()` (or adapt the example to a `ResultSet`).'
  - name: – Obtain the DataTable You Want to Export
    text: First, you need a source of rows and columns. In real projects this might
      be a database query, a CSV parser, or an in‑memory collection. The example assumes
      a helper method `getDataTable()` that returns a ready‑to‑use `DataTable`.
  - name: – Prepare a Style for Each Column
    text: We create a `Style[]` whose length matches the number of columns. Each entry
      will hold a font color that alternates between blue and green.
  - name: – Create Styles with Alternating Font Colors
    text: 'Now the fun part: loop through the array and assign a blue font to even‑indexed
      columns and a green font to odd‑indexed ones. This is where **alternating column
      colors** is implemented.'
  - name: – Import the DataTable with the Style Array
    text: Finally, we hand the `DataTable` and the `columnStyles` array to POI’s `importDataTable`
      method. The `true` flag tells POI to treat the first row as column headers.
  - name: – Save the Workbook (Optional but Recommended)
    text: After the import, you’ll probably want to write the workbook to disk or
      stream it to a client.
  type: HowTo
- questions:
  - answer: Replace `setFontColor` with `setPatternForegroundColor` and call `setPattern(BackgroundType.SOLID)`
      on the style.
    question: What if I need background colors instead of font colors?
  - answer: 'Absolutely—just swap the loop logic: iterate over rows and assign a style
      per row index.'
    question: Can I apply the same color scheme to rows instead of columns?
  - answer: Excel caps at 16,384 columns (XFD). The code will throw an exception once
      you exceed that limit. Guard against it by checking `columnCount` against `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.
    question: What if the DataTable has more columns than the worksheet can handle?
  - answer: Yes, POI abstracts the format. However, the older binary format supports
      fewer colors, so you might see a fallback to the nearest palette entry.
    question: Does this work with .xls (Excel 97‑2003) files?
  type: FAQPage
tags:
- excel
- java
- datatable
- formatting
- apache-poi
title: สีคอลัมน์สลับใน Excel – นำเข้า DataTable พร้อมการจัดรูปแบบ
url: /th/java/excel-import-export/alternating-column-colors-in-excel-import-datatable-with-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสลับสีคอลัมน์ใน Excel – นำเข้า DataTable พร้อมการจัดรูปแบบ

เคยสงสัยไหมว่าจะแต่งสีให้การส่งออก Excel ของคุณดูสวยงามโดยไม่ต้องออกจากโค้ด? **การสลับสีคอลัมน์** เป็นวิธีเร็ว ๆ ที่ทำให้ตารางขนาดใหญ่อ่านง่ายขึ้น และคุณสามารถทำได้ขณะ **import datatable to excel** ในบทเรียนนี้เราจะเดินผ่านโซลูชัน Java ครบชุดที่ไม่เพียงแค่นำข้อมูลของคุณเข้าสู่ worksheet แต่ยังใส่รูปแบบฟอนต์สีน้ำเงิน‑เขียวให้แต่ละคอลัมน์ด้วย

คุณจะได้เห็นวิธี **import data with formatting**, ตั้งค่าสีฟอนต์ของแต่ละคอลัมน์, และตอบคำถาม “**how to import datatable**” อย่างถาวร ไม่ต้องใช้เครื่องมือภายนอก เพียงแค่ Java ธรรมดาและไลบรารีสเปรดชีตที่เป็นที่นิยม

## สิ่งที่คุณจะสร้าง

เมื่อจบคู่มือนี้คุณจะมีโค้ดสั้น ๆ ของ Java ที่สามารถทำงานได้:

1. ดึง `DataTable` (หรือคอลเลกชันแบบ `ResultSet`)  
2. สร้างอาร์เรย์ `Style` ที่คอลัมน์เลขคู่เป็นสีน้ำเงินและคอลัมน์เลขคี่เป็นสีเขียว  
3. เรียก `importDataTable` เพื่อนำข้อมูลลงในเซลล์ **A1** พร้อมใช้สไตล์ที่กำหนด  

ทั้งหมดทำได้ในไม่กี่บรรทัด แต่ผลลัพธ์ดูเหมือนรายงานที่ทำด้วยมือ

### ข้อกำหนดเบื้องต้น

- Java 8+ (โค้ดทำงานกับเวอร์ชันใหม่กว่าได้เช่นกัน)  
- Apache POI 5.x อยู่ใน classpath – ไลบรารีที่สื่อสารกับไฟล์ Excel  
- การนำเข้า `DataTable` ที่มีเมธอด `getColumns()` และ `size()` (หรือปรับตัวอย่างให้ทำงานกับ `ResultSet`)  

ถ้าคุณใช้ POI อยู่แล้วสำหรับงาน Excel อื่น ๆ คุณสามารถใส่โค้ดนี้ได้ทันที  

---

## การสลับสีคอลัมน์ขณะนำเข้า DataTable ไปยัง Excel

หัวใจของวิธีการอยู่ในสี่ขั้นตอนสั้น ๆ มาดูรายละเอียดกัน

### ขั้นตอนที่ 1 – รับ DataTable ที่ต้องการส่งออก

ก่อนอื่นคุณต้องมีแหล่งข้อมูลของแถวและคอลัมน์ ในโปรเจกต์จริงอาจมาจากการ query ฐานข้อมูล, ตัวแปลง CSV, หรือคอลเลกชันในหน่วยความจำ ตัวอย่างสมมติว่ามีเมธอดช่วยเหลือ `getDataTable()` ที่คืน `DataTable` พร้อมใช้

```java
// Step 1: Obtain the data to be imported
DataTable dataTable = getDataTable();   // your own method that fills the table
```

> **ทำไมจึงสำคัญ:**  
> การได้ข้อมูลก่อนทำให้คุณตรวจสอบจำนวนคอลัมน์ได้ ซึ่งจะใช้กำหนดขนาดอาร์เรย์สไตล์ต่อไป นอกจากนี้ยังทำให้ขั้นตอนการนำเข้ามีอ็อบเจกต์ที่ชัดเจนให้ทำงานด้วย

### ขั้นตอนที่ 2 – เตรียมสไตล์สำหรับแต่ละคอลัมน์

เราจะสร้าง `Style[]` ที่ความยาวตรงกับจำนวนคอลัมน์ แต่ละตำแหน่งจะเก็บสีฟอนต์ที่สลับกันระหว่างสีน้ำเงินและสีเขียว

```java
// Step 2: Prepare a style for each column (same count as the number of columns)
int columnCount = dataTable.getColumns().size();
Style[] columnStyles = new Style[columnCount];
```

> **เคล็ดลับ:** หาก `DataTable` ของคุณอาจเปลี่ยนรูปแบบระหว่างการทำงาน ให้คำนวณ `columnCount` ใหม่ทุกครั้งที่ส่งออก เพื่อหลีกเลี่ยง `ArrayIndexOutOfBoundsException`

### ขั้นตอนที่ 3 – สร้างสไตล์ด้วยสีฟอนต์สลับกัน

ตอนนี้มาสร้างสีกันเถอะ: วนลูปผ่านอาร์เรย์และกำหนดฟอนต์สีน้ำเงินให้คอลัมน์ที่มีดัชนีคู่ และฟอนต์สีเขียวให้คอลัมน์ที่มีดัชนีคี่ นี่คือการทำ **alternating column colors** จริง ๆ

```java
// Step 3: Create styles with alternating font colors for visual distinction
for (int i = 0; i < columnStyles.length; i++) {
    columnStyles[i] = workbook.createStyle();               // create a fresh style
    // Even columns → blue, odd columns → green
    columnStyles[i].setFontColor(
        (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
    );
}
```

> **ทำไมต้องสลับสี?**  
> ดวงตามนุษย์สแกนแถวได้ง่ายขึ้นเมื่อคอลัมน์ข้างเคียงโดดเด่น การใช้จังหวะสีน้ำเงิน‑เขียวช่วยลดความเมื่อยล้าของสายตา โดยเฉพาะในตารางกว้าง

### ขั้นตอนที่ 4 – นำเข้า DataTable พร้อมอาร์เรย์สไตล์

สุดท้าย เราจะส่ง `DataTable` และอาร์เรย์ `columnStyles` ให้กับเมธอด `importDataTable` ของ POI ธง `true` บอก POI ให้ถือแถวแรกเป็นหัวคอลัมน์

```java
// Step 4: Import the data table into the worksheet starting at cell A1, applying the styles
worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);
```

> **เบื้องหลังทำงานอย่างไร:**  
> POI จะวนลูปแต่ละคอลัมน์ ดึง `Style` ที่ตรงกันจากอาร์เรย์ แล้วเขียนแต่ละเซลล์ด้วยสไตล์นั้น เนื่องจากเราเพียงตั้งค่าสีฟอนต์ ส่วนอื่น ๆ (เช่นขอบ, พื้นหลัง) จะใช้ค่าเริ่มต้น – คุณสามารถขยายสไตล์ได้หากต้องการความสวยงามเพิ่ม

### ขั้นตอนที่ 5 – บันทึก Workbook (เลือกทำแต่แนะนำ)

หลังจากนำเข้าแล้ว คุณอาจต้องการเขียน workbook ลงไฟล์หรือส่งสตรีมให้ไคลเอนต์

```java
// Optional: write the workbook to a file
try (FileOutputStream fos = new FileOutputStream("ExportedReport.xlsx")) {
    workbook.save(fos);
}
```

> **กรณีขอบ:** หากไฟล์เป้าหมายมีอยู่แล้ว `FileOutputStream` จะเขียนทับ คุณควรตรวจสอบก่อนหรือขอการยืนยันจากผู้ใช้ใน UI

---

## คำถามที่พบบ่อยและข้อควรระวัง

- **ต้องการสีพื้นหลังแทนสีฟอนต์ทำอย่างไร?**  
  แทนที่ `setFontColor` ด้วย `setPatternForegroundColor` แล้วเรียก `setPattern(BackgroundType.SOLID)` บนสไตล์

- **สามารถใช้โทนสีเดียวกันกับแถวแทนคอลัมน์ได้ไหม?**  
  ทำได้ – เพียงสลับลอจิกของลูป: วนลูปตามแถวและกำหนดสไตล์ต่อดัชนีแถว

- **ถ้า DataTable มีคอลัมน์มากกว่าที่ worksheet รองรับจะเป็นอย่างไร?**  
  Excel มีขีดจำกัดที่ 16,384 คอลัมน์ (XFD) โค้ดจะโยนข้อยกเว้นเมื่อเกินขีดจำกัด ตรวจสอบ `columnCount` กับ `SpreadsheetVersion.EXCEL2007.getMaxColumns()` ก่อน

- **ทำงานกับไฟล์ .xls (Excel 97‑2003) ได้หรือไม่?**  
  ได้, POI จะจัดการรูปแบบให้เอง อย่างไรก็ตามรูปแบบไบนารีเก่ามีสีได้น้อยกว่า จึงอาจเห็นการแมปสีไปยังพาเลตที่ใกล้ที่สุด

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นคลาสที่สามารถคัดลอกไปใส่ในโปรเจกต์ Maven ที่มี `org.apache.poi:poi-ooxml:5.2.3` อยู่แล้ว ปรับ `getDataTable()` ให้คืนแหล่งข้อมูลของคุณ

```java
import com.aspose.cells.*;
import java.io.FileOutputStream;

public class ExcelAlternatingColorsExport {

    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 1️⃣ Obtain the data to be imported
        DataTable dataTable = getDataTable(); // implement this method

        // 2️⃣ Prepare a style for each column
        int columnCount = dataTable.getColumns().size();
        Style[] columnStyles = new Style[columnCount];

        // 3️⃣ Create alternating font colors (blue for even, green for odd)
        for (int i = 0; i < columnStyles.length; i++) {
            columnStyles[i] = workbook.createStyle();
            columnStyles[i].setFontColor(
                (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
            );
        }

        // 4️⃣ Import the data with formatting
        worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);

        // 5️⃣ Save the file
        try (FileOutputStream fos = new FileOutputStream("AlternatingColorsReport.xlsx")) {
            workbook.save(fos);
        }

        System.out.println("Export complete – open AlternatingColorsReport.xlsx to see the result.");
    }

    // Dummy implementation – replace with real data retrieval
    private static DataTable getDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID");
        dt.getColumns().add("Name");
        dt.getColumns().add("Score");
        dt.getRows().add(new DataRow(new Object[]{1, "Alice", 85}));
        dt.getRows().add(new DataRow(new Object[]{2, "Bob", 92}));
        dt.getRows().add(new DataRow(new Object[]{3, "Carol", 78}));
        return dt;
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `AlternatingColorsReport.xlsx` คอลัมน์ A และ C (ดัชนีคู่) จะมีข้อความสีฟ้า ส่วนคอลัมน์ B (ดัชนีคี่) จะเป็นสีเขียว ฟอนต์ของแถวแรกจะเป็นตัวหนาเนื่องจาก `importDataTable` ถือว่าเป็นหัวตาราง

---

## สรุป

เราได้สรุปทุกอย่างที่คุณต้องการเพื่อ **import datatable to excel** พร้อมกับ **alternating column colors** และ **set column font color** ผ่านโปรแกรม วิธีนี้เบา ใช้แค่ Apache POI เท่านั้น และสามารถต่อขยายเพื่อทำสไตล์อื่น ๆ เช่น ขอบหรือพื้นหลังเซลล์ได้

ต่อไปลองสำรวจ:

- **Import data with formatting** สำหรับแถว (สลับสีแถว)  
- เพิ่ม **conditional formatting** เพื่อไฮไลท์คะแนนสูง  
- ส่งออกโดยตรงเป็น HTTP response สำหรับเว็บแอป

ปรับใช้รูปแบบนี้ใน pipeline การรายงานของคุณ – เมื่อคุณเชี่ยวชาญพื้นฐานแล้ว ความเป็นไปได้ไม่มีที่สิ้นสุด ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อ

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [วิธีจัดเรียงข้อมูล Excel ตามสีคอลัมน์โดยใช้ Aspose.Cells Java: คู่มือฉบับสมบูรณ์](/cells/english/java/formatting/sort-excel-data-by-column-color-aspose-cells-java/)
- [เชี่ยวชาญการป้องกันคอลัมน์ Excel ด้วย Aspose.Cells for Java: คู่มือฉบับครอบคลุม](/cells/english/java/security-protection/excel-column-protection-aspose-cells-java/)
- [วิธีแทรกคอลัมน์ใน Excel โดยใช้ Aspose.Cells for Java - คู่มือฉบับสมบูรณ์](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}