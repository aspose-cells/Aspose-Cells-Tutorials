---
category: general
date: 2026-06-21
description: วิธีใช้สไตล์ขณะแปลง DataTable เป็น Excel ใน Java เรียนรู้การนำเข้า DataTable
  ไปยัง Excel, เพิ่มสไตล์ที่กำหนดเองใน Excel, และบันทึกเวิร์กบุ๊กเป็นไฟล์ในไม่กี่นาที.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: th
og_description: วิธีใช้สไตล์ขณะแปลง DataTable เป็น Excel ใน Java คู่มือนี้จะแสดงวิธีนำเข้า
  DataTable ไปยัง Excel, เพิ่มสไตล์ที่กำหนดเองใน Excel, และบันทึกเวิร์กบุ๊กเป็นไฟล์
og_title: วิธีการใส่สไตล์เมื่อแปลง DataTable เป็น Excel – บทเรียน Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  headline: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  type: TechArticle
- description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  name: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  steps:
  - name: 5.1 Conditional Formatting Instead of Fixed Styles
    text: If you need to highlight rows where `Score > 90`, you can add a `ConditionalFormattingCollection`
      after the import. This gives you dynamic coloring without hard‑coding extra
      styles.
  - name: 5.2 Merging Cells for Titles
    text: Sometimes a report needs a big title spanning multiple columns. Use `worksheet.getCells().merge(0,
      0, 1, 3)` and then apply a distinct style to that merged region.
  - name: 5.3 Large DataSets – Performance Considerations
    text: When dealing with >100k rows, set `ImportDataTableOptions` to `ImportDataTableOptions.NO_FORMATTING`
      first, then apply styles in a second pass. This avoids the overhead of styling
      each cell during import.
  - name: 5.4 Multi‑Sheet Export
    text: If you have several `DataTable`s, just create additional worksheets via
      `workbook.getWorksheets().add("Sheet2")` and repeat the **import datatable to
      excel** step for each sheet.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- DataTable
title: วิธีใช้สไตล์เมื่อแปลง DataTable เป็น Excel – คู่มือ Java ฉบับเต็ม
url: /th/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการใช้สไตล์เมื่อแปลง DataTable เป็น Excel – คู่มือ Java ฉบับเต็ม

เคยสงสัย **วิธีการใช้สไตล์** เมื่อคุณต้อง **แปลง DataTable เป็น Excel** หรือไม่? คุณไม่ได้เป็นคนเดียวที่คิดแบบนั้น ในเครื่องมือภายในหลายๆ ตัว เราดึงข้อมูลจากฐานข้อมูล ใส่ลงใน `DataTable` แล้วคาดหวังให้ได้สเปรดชีตที่สวยงามโดยไม่ต้องทำอะไรเพิ่มเติม เฉลย: คุณต้องบอกไลบรารี *อย่างชัดเจน* ว่า “สวย” หมายถึงอะไร

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และพร้อมรันที่แสดง **วิธีการใช้สไตล์** ด้วย Aspose.Cells for Java, นำเข้า `DataTable` ไปยัง Excel, **เพิ่มสไตล์แบบกำหนดเองใน Excel**, และสุดท้าย **บันทึกเวิร์กบุ๊กลงไฟล์**. เมื่อจบคุณจะมีโค้ดสั้นที่นำกลับมาใช้ใหม่ได้และสามารถใส่ลงในโปรเจกต์ใดก็ได้

---

## สิ่งที่คุณต้องการ

- **Java 17** (หรือ JDK ล่าสุดใดก็ได้) – โค้ดนี้ทำงานบน Java 8+ ด้วย  
- **Aspose.Cells for Java** JAR (เวอร์ชันทดลองฟรีก็ใช้ได้สำหรับการทดสอบ)  
- แหล่ง `DataTable` – เราจะจำลองตัวอย่างง่ายๆ แต่คุณสามารถเปลี่ยนเป็นผลลัพธ์การคิวรีจริงได้  
- IDE ที่คุณชอบ (IntelliJ, Eclipse, VS Code… ตามที่คุณเลือก)

ไม่จำเป็นต้องใช้เครื่องมือสร้างเพิ่มเติม; `pom.xml` ของ Maven ธรรมดาก็เพียงพอ, แต่คุณก็สามารถเพิ่ม JAR ด้วยตนเองได้เช่นกัน

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และการพึ่งพา

ก่อนอื่นเลย—ให้เพิ่มไลบรารีลงใน classpath

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- check the latest version -->
    </dependency>
</dependencies>
```

หากคุณไม่ได้ใช้ Maven เพียงแค่วางไฟล์ `aspose-cells-24.9.jar` ลงในโฟลเดอร์ `libs` ของคุณและเพิ่มเข้าไปใน build path

> **เคล็ดลับ:** Aspose มีคลาส `License` ให้ใช้ ลงทะเบียนไลเซนส์ของคุณตั้งแต่ต้น, มิฉะนั้นไฟล์ผลลัพธ์จะมีลายน้ำ

```java
import com.aspose.cells.*;

public class ExcelExporter {
    static {
        try {
            License license = new License();
            license.setLicense("Aspose.Cells.lic"); // place your license file in resources
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
    }
    // …rest of the class
}
```

ตอนนี้เราพร้อมที่จะพูดถึง **วิธีการใช้สไตล์** แล้ว

## ขั้นตอนที่ 2: สร้างสไตล์แบบกำหนดเองสำหรับ Excel

ความมหัศจรรย์ของสเปรดชีตที่ดูดีอยู่ที่สไตล์ของเซลล์ Aspose ให้คุณกำหนดอ็อบเจ็กต์ `Style`, ปรับฟอนต์, สี, เส้นขอบ, แล้วนำกลับมาใช้ซ้ำได้ทุกที่ ด้านล่างเป็นวิธีแบบกระชับเพื่อ **เพิ่มสไตล์แบบกำหนดเองใน Excel** ทั้งหมด

```java
/**
 * Builds an array of two custom styles:
 * 1. Header style – bold, gray background, centered.
 * 2. Data style   – thin borders, left‑aligned.
 */
private static Style[] buildImportStyles(Workbook workbook) {
    // Header style
    Style headerStyle = workbook.createStyle();
    Font headerFont = headerStyle.getFont();
    headerFont.setBold(true);
    headerFont.setColor(Color.getWhite());
    headerStyle.setPattern(BackgroundType.SOLID);
    headerStyle.setBackgroundColor(Color.getGray25());
    headerStyle.setHorizontalAlignment(TextAlignmentType.CENTER);
    headerStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    // Data style
    Style dataStyle = workbook.createStyle();
    dataStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setHorizontalAlignment(TextAlignmentType.LEFT);
    dataStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    return new Style[] { headerStyle, dataStyle };
}
```

สังเกตว่าเราสร้าง **สองสไตล์ที่แตกต่างกัน** — หนึ่งสำหรับหัวคอลัมน์และหนึ่งสำหรับแถวข้อมูล คุณสามารถขยายอาเรย์นี้ด้วยสไตล์ที่ต้องการได้เท่าไหร่ก็ได้; Aspose จะนำไปใช้ตามลำดับเมื่อคุณเรียก `importDataTable`

## ขั้นตอนที่ 3: นำเข้า DataTable ไปยัง Worksheet

ต่อไปคือส่วนที่จริงๆ แล้ว **นำเข้า DataTable ไปยัง Excel** เมธอด `importDataTable` รับ `DataTable` แหล่งที่มา, ธงบ่งบอกหัวคอลัมน์, แถว/คอลัมน์เริ่มต้น, และอาเรย์สไตล์ที่เราสร้างไว้

```java
public static void exportDataTableToExcel(DataTable dataTable, String outputPath) throws Exception {
    // 1️⃣ Create a new workbook and grab the first worksheet
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.getWorksheets().get(0);

    // 2️⃣ Build the custom styles (header + data)
    Style[] importStyles = buildImportStyles(workbook);

    // 3️⃣ Import the DataTable – start at A1 (0,0), keep column names, apply styles
    worksheet.getCells().importDataTable(dataTable, true, 0, 0, importStyles);

    // 4️⃣ Auto‑fit columns for a tidy look
    worksheet.autoFitColumns();

    // 5️⃣ Finally, **save workbook to file**
    workbook.save(outputPath);
}
```

หมายเหตุสั้น: อาร์กิวเมนต์ `true` บอก Aspose ให้ **รักษาหัวคอลัมน์** — นี่เป็นกรณีทั่วไปเมื่อคุณต้องการรายงานที่อ่านง่าย หากตั้งเป็น `false` แถวข้อมูลแรกจะกลายเป็นหัวตาราง

## ขั้นตอนที่ 4: เชื่อมต่อทั้งหมด – ตัวอย่างทำงานขั้นต่ำ

ด้านล่างเป็นเมธอด `main` ที่ทำงานอิสระซึ่งสร้าง `DataTable` จำลอง, เรียกฟังก์ชันส่งออก, และเขียน `output.xlsx` ไปยังโฟลเดอร์ `./results`

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExporter {

    // (License block omitted for brevity – see Step 1)

    public static void main(String[] args) throws Exception {
        // Mock a DataTable – replace this with your real DB call
        DataTable dataTable = createSampleDataTable();

        // Define where the Excel file should land
        String outputPath = "results/output.xlsx";

        // Perform the conversion and styling
        exportDataTableToExcel(dataTable, outputPath);

        System.out.println("Excel file generated at: " + outputPath);
    }

    /** Helper that builds a simple DataTable with three columns */
    private static DataTable createSampleDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", CellValueType.INTEGER);
        dt.getColumns().add("Name", CellValueType.STRING);
        dt.getColumns().add("Score", CellValueType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[] {1, "Alice", 85.5});
        dt.getRows().add(new Object[] {2, "Bob", 92.0});
        dt.getRows().add(new Object[] {3, "Charlie", 78.3});
        return dt;
    }

    // (Style builder and export method from Steps 2‑3 go here)
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `output.xlsx` แล้วคุณจะเห็นแถวหัวข้อเป็นสีเทาและตัวหนา, เซลล์ข้อมูลมีเส้นขอบบาง, และคอลัมน์ถูกปรับขนาดอัตโนมัติเพื่อให้พอดีกับเนื้อหา นั่นคือ **วิธีการใช้สไตล์** เพื่อทำให้ชีตดูเป็นมืออาชีพ

![วิธีการใช้สไตล์ในเวิร์กบุ๊ก Excel](/images/excel-styles.png){alt="วิธีการใช้สไตล์ในเวิร์กบุ๊ก Excel"}

*(ภาพหน้าจอแสดงหัวข้อเป็นสีเทาตัวหนาและแถวข้อมูลมีเส้นขอบบาง)*

## ขั้นตอนที่ 5: เคล็ดลับขั้นสูงและกรณีขอบ

### 5.1 Conditional Formatting Instead of Fixed Styles  
หากคุณต้องการไฮไลท์แถวที่ `Score > 90` คุณสามารถเพิ่ม `ConditionalFormattingCollection` หลังการนำเข้าได้ วิธีนี้ให้การเปลี่ยนสีแบบไดนามิกโดยไม่ต้องกำหนดสไตล์เพิ่มเติมแบบคงที่

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Merging Cells for Titles  
บางครั้งรายงานต้องการหัวเรื่องใหญ่ที่ขยายครอบหลายคอลัมน์ ใช้ `worksheet.getCells().merge(0, 0, 1, 3)` แล้วจึงใช้สไตล์ที่แตกต่างกับพื้นที่ที่รวมกันนั้น

### 5.3 Large DataSets – Performance Considerations  
เมื่อทำงานกับแถว >100k ให้ตั้งค่า `ImportDataTableOptions` เป็น `ImportDataTableOptions.NO_FORMATTING` ก่อน, แล้วจึงใช้สไตล์ในรอบที่สอง วิธีนี้ช่วยลดภาระการจัดรูปแบบแต่ละเซลล์ระหว่างการนำเข้า

### 5.4 Multi‑Sheet Export  
หากคุณมีหลาย `DataTable` เพียงสร้างเวิร์กชีตเพิ่มเติมผ่าน `workbook.getWorksheets().add("Sheet2")` แล้วทำซ้ำขั้นตอน **นำเข้า DataTable ไปยัง Excel** สำหรับแต่ละชีต

## สรุป

เราได้ครอบคลุม **วิธีการใช้สไตล์** ตั้งแต่ต้นจนจบ: ตั้งค่า Aspose.Cells, สร้าง **สไตล์แบบกำหนดเองใน Excel**, **นำเข้า DataTable ไปยัง Excel**, และสุดท้าย **บันทึกเวิร์กบุ๊กลงไฟล์** ตัวอย่างโค้ดเต็มพร้อมคัดลอก‑วาง, และเคล็ดลับเพิ่มเติมช่วยให้คุณมีแผนที่สำหรับรายงานที่ซับซ้อนยิ่งขึ้น

ต่อไปคุณอาจสำรวจ **การเพิ่มสไตล์แบบกำหนดเองใน Excel** สำหรับแผนภูมิ, หรือทดลอง **แปลง DataTable เป็น Excel** ใน endpoint ของ Spring Boot REST ไม่ว่าคุณจะเลือกทางไหน คุณก็มีพื้นฐานที่แข็งแรงสำหรับการเปลี่ยนตารางดิบให้เป็นสเปรดชีตที่ดูเป็นมืออาชีพ—โดยไม่ต้องจัดรูปแบบด้วยมือ

มีคำถาม

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่นในโปรเจกต์ของคุณ

- [วิธีการใช้สไตล์กับเซลล์ Excel ด้วย Aspose.Cells for Java - คู่มือฉบับสมบูรณ์](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [รวมเซลล์และใช้สไตล์ใน Excel ด้วย Aspose.Cells for Java - คู่มือฉบับสมบูรณ์](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [วิธีการนำเข้า DataTable ไปยัง Excel ด้วย Aspose.Cells for .NET (คู่มือขั้นตอนโดยละเอียด)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}