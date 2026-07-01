---
category: general
date: 2026-06-30
description: ตั้งค่าฟอนต์ให้เป็นตัวหนาขณะนำเข้า DataTable ไปยัง Excel ด้วย Java. เรียนรู้โค้ดการจัดรูปแบบตามเงื่อนไข,
  นำเข้า DataTable ไปยัง Excel และจัดสไตล์ตารางได้อย่างง่ายดาย.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: th
og_description: ตั้งค่าฟอนต์เป็นตัวหนาใน Java เมื่อส่งออก DataTable ไปยัง Excel คู่มือนี้ครอบคลุมโค้ดการจัดรูปแบบตามเงื่อนไข
  การนำเข้า DataTable ไปยัง Excel และการจัดสไตล์ตาราง
og_title: ตั้งค่าฟอนต์เป็นตัวหนาในการส่งออก Excel ด้วย Java – คู่มือขั้นตอนโดยละเอียด
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
title: ตั้งค่าตัวอักษรเป็นตัวหนาในการส่งออก Excel ด้วย Java – คู่มือฉบับสมบูรณ์
url: /th/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่าตัวอักษรหนาใน Java Excel Export – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีตั้งค่าตัวอักษรหนา** สำหรับคอลัมน์เฉพาะขณะ **นำเข้าไฟล์ datatable excel** หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจออุปสรรคเมื่อต้องการสเปรดชีตที่สวยงามโดยไม่ต้องปรับเซลล์แต่ละเซลล์ด้วยตนเอง ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของ Java คุณสามารถนำเข้า `DataTable` ใส่ฟอนต์หนา และแม้กระทั่งเพิ่ม **โค้ดการจัดรูปแบบตามเงื่อนไข** — ทั้งหมดทำโดยโปรแกรม

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างเต็มรูปแบบที่สามารถรันได้ ซึ่งแสดง **วิธีนำเข้า datatable** ไปยังเวิร์กบุ๊ก Excel, ใช้ **set font bold** กับทุกคอลัมน์ที่มีดัชนีเป็นเลขคู่, และเพิ่มการจัดรูปแบบตามเงื่อนไขอย่างง่ายโดยออปชัน สุดท้ายคุณจะได้สแนปช็อตที่พร้อมรันและความเข้าใจชัดเจนเกี่ยวกับ **import table with styles** สำหรับทุกโครงการ

## ความต้องการเบื้องต้น

- Java 8 หรือใหม่กว่า (โค้ดทำงานบน Java 17 ด้วย)  
- Aspose.Cells for Java (เวอร์ชันทดลองฟรีก็ใช้ได้) – เพิ่ม dependency ของ Maven หรือใส่ JAR ลง classpath  
- ความคุ้นเคยพื้นฐานกับการแปลง `java.sql` `ResultSet` → `DataTable` (เราจะจำลองตารางเพื่อความง่าย)  
- IDE หรือเครื่องมือสร้างเช่น Maven/Gradle

> **เคล็ดลับ:** หากคุณใช้ Maven ให้เพิ่มส่วนนี้ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## ภาพรวมของวิธีแก้

1. **สร้าง `DataTable` จำลอง** ที่เลียนแบบข้อมูลที่คุณมักดึงจากฐานข้อมูล  
2. **สร้างอาเรย์ `CellStyle`** ที่คอลัมน์เลขคู่ทั้งหมดจะใช้ฟอนต์หนา – นี่คือหัวใจของ **set font bold**  
3. **ดึง worksheet แรก** จากเวิร์กบุ๊ก  
4. **นำเข้า `DataTable`** พร้อมหัวคอลัมน์ เริ่มที่เซลล์ `A1` และใช้สไตล์ที่เตรียมไว้  
5. (ออปชัน) **เพิ่มกฎการจัดรูปแบบตามเงื่อนไข** เพื่อแสดงตัวอย่างคีย์เวิร์ด **conditional formatting code**

แต่ละขั้นตอนอธิบายด้วยภาษาอังกฤษธรรมดา และโค้ดบล็อกเป็นอิสระเต็มที่ คุณจึงคัดลอก‑วางและรันได้ทันที

---

## ขั้นตอนที่ 1: ดึงหรือสร้าง DataTable เพื่อทำการนำเข้า

ในแอปพลิเคชันจริงคุณอาจเรียกใช้ยูทิลิตี้แปลง `ResultSet` → `DataTable` สำหรับคู่มือนี้เราจะสร้าง `DataTable` อย่างง่ายด้วยตนเอง เพื่อให้คุณโฟกัสที่ส่วนของ Excel

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

> **ทำไมเรื่องนี้สำคัญ:** การมี `DataTable` พร้อมใช้งานทำให้เรามุ่งเน้นที่ API **import datatable excel** และตรรกะการจัดสไตล์ วิธีนี้สามารถนำกลับมาใช้ใหม่ได้ — เพียงเปลี่ยนแถวที่เขียนแบบคงที่เป็นคิวรีฐานข้อมูลเมื่อเข้าสู่การผลิต

---

## ขั้นตอนที่ 2: เตรียมสไตล์ – ที่นี่คือจุดที่เราจะ **Set Font Bold**

ต่อไปเราจะสร้างอาเรย์ของอ็อบเจกต์ `CellStyle` หนึ่งอันต่อคอลัมน์ กฎง่าย ๆ: **set font bold** สำหรับคอลัมน์ที่มีดัชนีเป็นเลขคู่ (0, 2, 4,…) ส่วนคอลัมน์เลขคี่จะเป็นปกติ

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

### ทำไมต้องใช้อาเรย์สไตล์?

- **ประสิทธิภาพ:** การใช้สไตล์ต่อคอลัมน์เร็วกว่าใส่สไตล์ต่อเซลล์หนึ่ง ๆ  
- **ความสอดคล้อง:** ทุกเซลล์ในคอลัมน์สืบทอดฟอร์แมตเดียวกัน ทำให้ดูเป็นระเบียบ  
- **การขยายตัว:** เพิ่มคอลัมน์ในภายหลังเพียงขยายอาเรย์ — ไม่ต้องเขียนโค้ดใหม่

---

## ขั้นตอนที่ 3: เข้าถึง Worksheet แรกในเวิร์กบุ๊ก

Aspose.Cells สร้าง worksheet เริ่มต้นให้เราโดยอัตโนมัติ แต่การดึงมันอย่างชัดเจนเป็นแนวปฏิบัติที่ดี อีกทั้งยังแสดง **วิธีนำเข้า datatable** ไปยังชีตที่ระบุ

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## ขั้นตอนที่ 4: นำเข้า DataTable พร้อมสไตล์ – การทำงานหลักของ **Import Table With Styles**

เมธอด `importDataTable` ทำหน้าที่หลักทั้งหมด มันคัดลอกข้อมูล, เพิ่มหัวคอลัมน์, และใช้สไตล์อาเรย์ที่เราสร้างไว้ก่อนหน้า

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

เมื่อคุณรันตัวอย่าง จะเห็น **set font bold** ถูกนำไปใช้กับคอลัมน์ `ID` และ `Score` ส่วน `Name` จะเป็นแบบปกติ

---

## ขั้นตอนที่ 5 (ออปชัน): เพิ่มการจัดรูปแบบตามเงื่อนไข – ตัวอย่าง **Conditional Formatting Code** อย่างรวดเร็ว

หากต้องการไฮไลท์แถวที่คะแนนเกิน 90 เพียงเพิ่มบรรทัดไม่กี่บรรทัดก็ทำได้ นี่เป็นการแสดงคีย์เวิร์ด **conditional formatting code** โดยไม่ทำให้โฟลว์หลักสับสน

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

> **หมายเหตุ:** โค้ดส่วนข้างบนเป็นออปชัน แต่แสดงให้เห็นว่าคุณสามารถวาง **conditional formatting code** บนตารางที่มีสไตล์แล้วได้อย่างไร

---

## รวมทุกอย่างไว้ด้วยกัน – ตัวอย่างเต็มที่สามารถรันได้

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
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


## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Implement Custom Font Settings in Aspose.Cells Java for Excel Formatting](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Set Font Size in Excel Using Aspose.Cells Java - Comprehensive Guide](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}