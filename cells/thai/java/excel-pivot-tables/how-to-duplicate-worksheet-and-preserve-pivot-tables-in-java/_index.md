---
category: general
date: 2026-08-17
description: วิธีทำสำเนาแผ่นงานใน Java ด้วย Aspose.Cells โดยคงรักษาตาราง Pivot, คัดลอก
  Pivot ไปยังเวิร์กบุ๊กใหม่, และสร้างเวิร์กบุ๊กจากแผ่นงานหนึ่ง
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: th
lastmod: 2026-08-17
og_description: วิธีทำสำเนาแผ่นงานใน Java ด้วย Aspose.Cells โดยคงตาราง Pivot ไว้,
  คัดลอก Pivot ไปยังเวิร์กบุ๊กใหม่, และสร้างเวิร์กบุ๊กจากแผ่นงาน—อธิบายทุกขั้นตอน
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: วิธีทำสำเนาแผ่นงานและคง Pivot Table – คู่มือ Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: วิธีทำสำเนาแผ่นงานและคงตาราง Pivot ไว้ใน Java
url: /th/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำสำเนา worksheet และคงไว้ pivot tables ใน Java

การทำสำเนา worksheet พร้อมคง pivot table ไว้เป็นสิ่งที่ต้องการบ่อยครั้งเมื่อคุณทำอัตโนมัติการรายงานด้วย Excel คู่มือฉบับนี้จะแสดงวิธีคัดลอก pivot ไปยัง workbook ใหม่โดยใช้ Aspose.Cells for Java และยังอธิบายวิธีคง pivot ไว้เมื่อคุณสร้าง workbook จาก sheet

คุณจะได้เรียนรู้วิธีโหลด workbook ที่มีอยู่แล้ว ทำสำเนา worksheet ที่มี pivot table และบันทึกผลลัพธ์เป็นไฟล์ใหม่ คู่มือสมมติว่าคุณมีสภาพแวดล้อมการพัฒนา Java พื้นฐานและมีใบอนุญาต Aspose.Cells ที่ถูกต้อง (การทดลองใช้ฟรีสามารถใช้สำหรับการทดสอบ) ไม่จำเป็นต้องใช้เครื่องมือภายนอกใด ๆ นอกจากไฟล์ JAR ของ Aspose.Cells

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน, โปรดตรวจสอบว่าคุณมี:

* Java Development Kit (JDK) 8 หรือใหม่กว่า.
* Maven หรือ Gradle เพื่อจัดการ dependency ของ Aspose.Cells.
* ไฟล์ Excel (`source.xlsx`) ที่มีอย่างน้อยหนึ่ง pivot table บน worksheet แรก.
* โฟลเดอร์ที่คุณสามารถอ่านไฟล์ต้นฉบับและเขียน workbook ที่ทำสำเนาได้.

เพิ่ม dependency ของ Aspose.Cells ลงใน `pom.xml` (สำหรับ Maven) หรือ `build.gradle` (สำหรับ Gradle) ตัวอย่างสำหรับ Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## วิธีทำสำเนา worksheet ที่มี pivot table

การดำเนินการหลักเป็นกระบวนการสามขั้นตอน: โหลด, คัดลอก, และบันทึก แต่ละขั้นตอนจะอธิบายด้านล่าง

### ขั้นตอนที่ 1 – โหลด workbook ที่มี pivot table

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*ทำไมขั้นตอนนี้สำคัญ*: วัตถุ `Workbook` แทนไฟล์ Excel ทั้งไฟล์ โดยการดึง worksheet แรก (`get(0)`) คุณจะเจาะจงไปที่ sheet ที่มี pivot table ที่ต้องการทำสำเนา

### ขั้นตอนที่ 2 – สร้าง workbook ใหม่และทำสำเนา worksheet ทั้งหมด

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` ทำสำเนา worksheet **รวมถึง** วัตถุที่ฝังอยู่ทั้งหมด, สูตร, และ pivot cache. นี่เป็นวิธีที่แนะนำสำหรับ **วิธีคัดลอก pivot** เนื่องจากคำนิยามของ pivot และแหล่งข้อมูลของมันจะถูกถ่ายโอนพร้อมกัน

### ขั้นตอนที่ 3 – บันทึก workbook ใหม่

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

หลังจากดำเนินการ, `copy_with_pivot.xlsx` จะมีสำเนาแบบเต็มของ sheet ต้นฉบับ, และ pivot table จะทำงานโดยไม่ต้องตั้งค่าเพิ่มเติม

**ผลลัพธ์ที่คาดหวัง**: การเปิด `copy_with_pivot.xlsx` ใน Excel จะแสดง worksheet ที่ทำสำเนาโดยมีรูปแบบ pivot, ตัวกรอง, และฟิลด์คำนวณเดียวกับไฟล์ต้นฉบับ

## วิธีคัดลอก pivot ไปยัง workbook อื่น

หากคุณต้องการย้าย pivot table โดยไม่ต้องคัดลอกทั้ง sheet, คุณสามารถดึง pivot cache ออกมาและแนบไปยัง worksheet ใหม่ โค้ดตัวอย่างต่อไปนี้แสดงแนวทางนั้น:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

โค้ดนี้ตอบ **วิธีคัดลอก pivot** โดยคัดลอกเฉพาะวัตถุ pivot เท่านั้น, ไม่ใช่ทั้ง worksheet. เมธอด `addCopy` บนคอลเลกชัน `PivotTables` ทำให้ pivot cache ถูกทำสำเนา, ตอบสนองความต้องการ **วิธีคง pivot** 

## วิธีคง pivot ไว้เมื่อสร้าง workbook จาก sheet

บางครั้งคุณอาจเริ่มต้นด้วย sheet ที่ไม่ได้เป็นส่วนหนึ่งของ workbook (เช่น คุณสร้าง sheet ในหน่วยความจำ). เพื่อ **สร้าง workbook จาก sheet** พร้อมคง pivot, ทำตามขั้นตอนต่อไปนี้:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

โดยการเพิ่ม worksheet ไปยัง `Workbook` ใหม่หลังจากที่กำหนด pivot ครบถ้วน, คุณรับประกันว่า **วิธีคง pivot** จะทำงานแม้ว่า worksheet จะมาจากไฟล์ที่ไม่มีอยู่ก่อน

## เคล็ดลับปฏิบัติและข้อผิดพลาดทั่วไป

| เคล็ดลับ | ทำไมถึงสำคัญ |
|-----|----------------|
| ใช้ `addCopy` แทน `copy` | `addCopy` ทำสำเนา pivot cache ด้านล่าง; การใช้ `copy` ธรรมดาอาจทำให้การเชื่อมต่อกับแหล่งข้อมูลหายไป |
| เก็บไฟล์ต้นฉบับและไฟล์ปลายทางไว้บนระบบไฟล์เดียวกัน | เส้นทางสัมพันธ์ในแหล่งข้อมูลของ pivot จะถูกแก้ไขอย่างถูกต้อง, ลดข้อผิดพลาด “source not found” |
| ตรวจสอบ pivot cache หลังการคัดลอก | เรียก `pivot.refresh()` หากข้อมูลต้นฉบับเปลี่ยนแปลงระหว่างการคัดลอกและการบันทึก |
| ปล่อย workbook เมื่อเสร็จ | `sourceWorkbook.dispose();` ปล่อยทรัพยากรเนทีฟ, สิ่งสำคัญสำหรับไฟล์ขนาดใหญ่ |

## กรณีขอบเขตที่คุณอาจเจอ

* **หลาย worksheet ที่มี pivot พึ่งพากัน** – คัดลอกแต่ละ worksheet แยกกัน; cache ที่ใช้ร่วมกันจะถูกทำสำเนาโดยอัตโนมัติ, แต่คุณอาจต้องกำหนดการเชื่อมต่อข้อมูลภายนอกใหม่
* **Pivot table ที่อ้างอิงจาก query SQL ภายนอก** – ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมปลายทางสามารถเข้าถึงฐานข้อมูลเดียวกัน; มิฉะนั้น pivot จะแสดงข้อผิดพลาด “#REF!” 
* **Workbook ขนาดใหญ่ (>100 MB)** – ใช้ `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` เพื่อลดความกดดันของหน่วยความจำระหว่างการคัดลอก

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่รวมทุกขั้นตอนที่อธิบายไว้ บันทึกเป็น `CopyPivotTable.java`, ปรับเส้นทางไฟล์ตามต้องการ, และรันด้วย IDE ที่คุณชอบหรือผ่าน `javac`/`java`.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);

        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving the pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);

        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");

        // Optional: copy only the pivot table to a separate workbook
        PivotTable pivot = sourceWorksheet.getPivotTables().get(0);
        Workbook pivotOnlyWorkbook = new Workbook();
        Worksheet pivotSheet = pivotOnlyWorkbook.getWorksheets().add("PivotOnly");
        pivotSheet.getPivotTables().addCopy(pivot);
        pivotOnlyWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");

        // Optional: create a new workbook from a freshly built sheet with a pivot
        Worksheet tempSheet = new Worksheet();
        PivotTable newPivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");
        // Configure newPivot (data source, rows, columns, etc.) here...

        Workbook createdFromSheet =


## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโครงการของคุณ

- [วิธีสร้าง Pivot Tables ใน Excel ด้วย Aspose.Cells สำหรับ Java: คู่มือฉบับสมบูรณ์](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [วิธีอัปเดตแหล่งข้อมูล Pivot Table ใน Excel ด้วย Aspose.Cells สำหรับ Java: คู่มือฉบับสมบูรณ์](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [วิธีนำ Slicers ไปใช้ใน Pivot Tables ด้วย Aspose.Cells สำหรับ Java: คู่มือฉบับสมบูรณ์](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}