---
category: general
date: 2026-10-07
description: เรียนรู้วิธีทำสำเนาตาราง Pivot ใน Excel ด้วย Java และ Aspose.Cells คัดลอกตาราง
  Pivot โดยการคัดลอกช่วงของมันระหว่างเวิร์กบุ๊กอย่างรวดเร็ว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: th
lastmod: 2026-10-07
og_description: วิธีทำสำเนาตาราง Pivot ใน Excel ด้วย Java และ Aspose.Cells. ทำตามคำแนะนำนี้เพื่อคัดลอกตาราง
  Pivot โดยการคัดลอกช่วงของมันระหว่างเวิร์กบุ๊ก.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: วิธีทำสำเนาตาราง Pivot ใน Excel ด้วย Java – บทเรียนเต็ม
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: วิธีทำสำเนาตาราง Pivot ใน Excel ด้วย Java – คู่มือขั้นตอนโดยละเอียด
url: /th/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำสำเนาตาราง Pivot ใน Excel ด้วย Java – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **how to duplicate pivot** ตารางในเวิร์กบุ๊กของ Excel, บทแนะนำนี้จะแสดงวิธีแก้ที่สมบูรณ์และพร้อมใช้งาน. ด้วย Aspose.Cells for Java คุณสามารถคัดลอกตาราง Pivot พร้อมข้อมูลต้นทางโดยการคัดลอกช่วงข้อมูลที่อยู่ด้านล่าง, แล้วบันทึกผลลัพธ์เป็นเวิร์กบุ๊กใหม่.

การทำสำเนาตาราง Pivot มักรู้สึกยากเพราะแคชของ Pivot ถูกซ่อนอยู่ในชีต. ด้วยการคัดลอกช่วงทั้งหมดที่มี Pivot, Aspose.Cells จะสร้างแคชใหม่ในเวิร์กบุ๊กปลายทางโดยอัตโนมัติ, ทำให้คุณได้สำเนาที่ทำงานเต็มรูปแบบโดยไม่ต้องแก้ไข XML ด้วยตนเอง.

ในคู่มือนี้คุณจะ:

* โหลดเวิร์กบุ๊กต้นทางที่มีตาราง Pivot อยู่.  
* กำหนดช่วงที่แน่นอนที่เก็บ Pivot.  
* คัดลอกช่วงนั้นไปยังเวิร์กบุ๊กใหม่, รักษาการกำหนดค่า Pivot ไว้.  
* บันทึกไฟล์ใหม่และตรวจสอบว่าตาราง Pivot ทำงานได้.  

ขั้นตอนเหล่านี้ทำงานกับเวอร์ชัน Excel ใด ๆ ที่รองรับโดย Aspose.Cells (2007‑2024) และต้องการเพียงไม่กี่บรรทัดของโค้ด Java.

## ข้อกำหนดเบื้องต้น

| Requirement | ทำไมจึงสำคัญ |
|-------------|----------------|
| **Java 8 or newer** | Aspose.Cells ถูกสร้างขึ้นสำหรับ Java 8+. |
| **Aspose.Cells for Java** (latest version) | ให้ API `Workbook`, `Range`, และ `CopyRange` ที่ใช้ในตัวอย่าง. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Pivot ที่คุณต้องการทำสำเนา. |
| **Write permission** to the target directory | จำเป็นสำหรับการบันทึก `CopyWithPivot.xlsx`. |

เพิ่มการอ้างอิง Aspose.Cells Maven ลงในไฟล์ `pom.xml` ของคุณ (หรือดาวน์โหลด JAR ด้วยตนเอง):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## วิธีทำสำเนาตาราง Pivot – การทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรม Java ที่ทำงานอิสระซึ่งสาธิต **how to duplicate pivot** ตารางโดยการคัดลอกช่วงที่มี Pivot. โค้ดนี้รวมการจัดการข้อผิดพลาด, คอมเมนต์, และขั้นตอนการตรวจสอบ.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### คำอธิบายของแต่ละขั้นตอน

| ขั้นตอน | โค้ดทำอะไร | ทำไมจึงสำคัญสำหรับ **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` อ่านไฟล์ `Source.xlsx`. | ไฟล์ต้นทางเป็นที่เดียวที่มี Pivot ดั้งเดิมอยู่. |
| **2️⃣ Define the range** | `createRange("A1:G20")` สร้างอ็อบเจ็กต์ `Range` ที่ครอบคลุม Pivot และข้อมูลของมัน. | ตาราง Pivot จะถูกเก็บพร้อมกับแคช; การคัดลอกช่วงทั้งหมดทำให้แคชถูกย้ายด้วย. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` เขียนช่วงลงในชีตปลายทาง. | นี่คือหัวใจของ **copy range between workbooks** – API จะจัดการวัตถุที่ซ่อนโดยอัตโนมัติ. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` บังคับให้ Pivot คำนวณใหม่. | รับประกันว่า Pivot ที่ทำสำเนาจะแสดงค่าตรงกับต้นฉบับ, โดยเฉพาะหลังการแก้ไข. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` เขียนไฟล์ลงดิสก์. | สร้างผลลัพธ์ **copy excel range** สุดท้ายที่คุณสามารถเปิดใน Excel. |

#### ผลลัพธ์ที่คาดหวัง

หลังจากรันโปรแกรม, เปิดไฟล์ `CopyWithPivot.xlsx`. คุณจะเห็นชีตที่ดูเหมือนกับชีตต้นฉบับอย่างสมบูรณ์, และตาราง Pivot ทำงานเหมือนกับต้นฉบับ – คุณสามารถขยายแถว, กรองฟิลด์, และรีเฟรชข้อมูลได้โดยไม่มีข้อผิดพลาด.

## ความแปรผันทั่วไปและกรณีขอบ

### 1️⃣ การคัดลอก Pivot ที่ขยายหลายชีต

หากข้อมูลต้นทางของ Pivot อยู่บนชีตที่ต่างจาก Pivot เอง, ให้รวมทั้งสองชีตในการคัดลอก. วิธีที่ง่ายที่สุดคือคัดลอกชีตต้นทางทั้งหมดก่อน, แล้วคัดลอกชีต Pivot:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ การจัดการกับ Named Ranges

Aspose.Cells รักษา Named Ranges ไว้เมื่อคุณคัดลอกช่วง. อย่างไรก็ตาม, หากเวิร์กบุ๊กปลายทางมีชื่อเดียวกันอยู่แล้ว, จะเกิด `CellsException`. แก้ไขโดยเปลี่ยนชื่อที่ขัดแย้งก่อนทำการคัดลอก:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ เวิร์กบุ๊กขนาดใหญ่และประสิทธิภาพ

การคัดลอกช่วงขนาดใหญ่มาก (หลายแสนแถว) อาจใช้หน่วยความจำสูง. เปิด **memory optimization**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ รักษาสูตรให้คงที่

หากช่วงต้นทางมีสูตรที่อ้างอิงเซลล์นอกพื้นที่ที่คัดลอก, การอ้างอิงเหล่านั้นจะเสียหลังการคัดลอก. เพื่อหลีกเลี่ยง, ขยายช่วงให้รวมเซลล์ที่พึ่งพาทั้งหมด, หรือใช้ `copyRange` พร้อมแฟล็ก `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## เคล็ดลับมืออาชีพสำหรับ **copy range between workbooks** ที่เชื่อถือได้

* **Always use absolute addresses** (`$A$1:$G$20`) เมื่อชีตต้นทางอาจถูกเปลี่ยนชื่อ.  
* **Refresh after copy** – แม้ว่า Aspose.Cells จะสร้างแคชใหม่, การเรียก `refresh()` จะขจัดคำเตือนแคชเก่าที่อาจปรากฏใน Excel.  
* **Validate the pivot**: หลังบันทึก, เปิดไฟล์โดยโปรแกรมและเรียก `pivotTable.validate()` เพื่อให้แน่ใจว่าไม่มีการอ้างอิงที่เสีย.  
* **Version compatibility**: โค้ดทำงานกับไฟล์ Excel 2007‑2024 (`.xlsx`, `.xlsm`). สำหรับไฟล์ `.xls` เก่า, ตั้งค่า `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## รายการซอร์สโค้ดเต็ม (พร้อมคอมไพล์)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานสมบูรณ์พร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบอื่นในโครงการของคุณ.

- [วิธีคัดลอกตาราง Pivot ใน Java – คู่มือ Aspose.Cells ฉบับสมบูรณ์](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [วิธีสร้างตาราง Pivot ใน Excel ด้วย Aspose.Cells for Java: คู่มือเชิงลึก](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [วิธีอัปเดตแหล่งข้อมูลตาราง Pivot ใน Excel ด้วย Aspose.Cells for Java: คู่มือเชิงลึก](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}