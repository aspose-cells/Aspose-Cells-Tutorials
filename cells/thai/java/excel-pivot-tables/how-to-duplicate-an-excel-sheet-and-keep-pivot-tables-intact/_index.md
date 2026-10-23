---
category: general
date: 2026-10-23
description: เรียนรู้วิธีทำสำเนาแผ่นงาน Excel ใน Java โดยคงรักษาตาราง Pivot ไว้ คู่มือนี้ยังแสดงวิธีคัดลอกตาราง
  Pivot, คัดลอกช่วงข้อมูล Excel, และคัดลอกแผ่นงานที่มีข้อมูล Pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: th
lastmod: 2026-10-23
og_description: ทำสำเนาแผ่นงาน Excel ใน Java พร้อมคงตาราง Pivot ไว้ตามเดิม ติดตามบทเรียนฉบับเต็มนี้เพื่อคัดลอกตาราง
  Pivot, คัดลอกช่วงข้อมูล Excel, และคัดลอกแผ่นงานพร้อมข้อมูล Pivot.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: ทำสำเนาแผ่นงาน Excel ที่มี Pivot Table ใน Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: วิธีทำสำเนาแผ่นงาน Excel และคงตาราง Pivot ไว้ไม่เสียหายใน Java
url: /th/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำสำเนาแผ่นงาน Excel และคงตาราง Pivot ไว้ครบถ้วนใน Java

หากคุณต้องการ **duplicate Excel sheet** พร้อมกับคงตาราง Pivot ทั้งหมดให้ทำงานอยู่ คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เห็นวิธีแก้ไขสั้น ๆ ที่คัดลอกแผ่นงาน, คัดลอกช่วงเฉพาะ, และแม้กระทั่งคัดลอกตาราง Pivot ไปยังเวิร์กบุ๊กอื่น—ทั้งหมดใน Java ธรรมดาโดยใช้ Aspose.Cells.

การทำสำเนาแผ่นงาน Excel เป็นงานทั่วไปเมื่อคุณสร้างรายงานรายเดือนจากเทมเพลตหรือเมื่อคุณต้องการสำเนา sandbox สำหรับการทดสอบ โค้ดด้านล่างทำงานกับ Aspose.Cells 25.11 หรือใหม่กว่า ซึ่งได้แนะนำตัวเลือก `setCopyPivotTable(true)`.

## สิ่งที่คุณต้องการ

- Java 17 (หรือ JDK ล่าสุด) ที่ติดตั้งแล้ว
- Aspose.Cells for Java 25.11 หรือใหม่กว่าในโปรเจกต์ของคุณ (Maven coordinate `com.aspose:aspose-cells:25.11`)
- เวิร์กบุ๊กต้นทาง (`SourceWithPivot.xlsx`) ที่มีตาราง Pivot อยู่แล้ว
- IDE หรือเครื่องมือสร้างตามที่คุณเลือก (IntelliJ IDEA, Eclipse, Maven, Gradle, ฯลฯ)

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กต้นทางที่มีตาราง Pivot

การดำเนินการแรกคือการเปิดเวิร์กบุ๊กที่เก็บ Pivot ที่คุณต้องการคงไว้

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **ทำไมขั้นตอนนี้สำคัญ:** การโหลดเวิร์กบุ๊กต้นทางทำให้คุณเข้าถึงอ็อบเจกต์แผ่นงาน, เซลล์, และตาราง Pivot ที่ฝังอยู่ หากไม่มีขั้นตอนนี้ คุณจะไม่สามารถอ้างอิงข้อมูล Pivot ที่คุณตั้งใจจะคัดลอกได้

## ขั้นตอนที่ 2: สร้างเวิร์กบุ๊กปลายทางเปล่า (หรือโหลดที่มีอยู่แล้ว)

คุณสามารถเริ่มจากเวิร์กบุ๊กเปล่า หรือเปิดไฟล์ที่มีอยู่แล้วซึ่งจะรับแผ่นงานที่ทำสำเนา

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **เคล็ดลับ:** หากคุณมีเวิร์กบุ๊กรายงานอยู่แล้ว ให้แทนที่บรรทัดด้านบนด้วย `new Workbook("ExistingReport.xlsx")` เพื่อเพิ่มแผ่นงานที่ทำสำเนาเข้าไป

## ขั้นตอนที่ 3: คัดลอกแผ่นงานทั้งหมด – ตาราง Pivot จะถูกคงไว้โดยอัตโนมัติ

การคัดลอกแผ่นงานทั้งหมดเป็นวิธีที่ง่ายที่สุดในการ **copy sheet with pivot**. Aspose.Cells จะคัดลอกคำนิยาม Pivot และแคชของมันโดยอัตโนมัติ

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **ทำไมถึงได้ผล:** `addCopy` ทำการโคลนโครงสร้างแผ่นงาน, ค่าเซลล์, สไตล์, และตาราง Pivot ที่ฝังอยู่ใด ๆ แผ่นงานใหม่ใน `dstWb` จะดูเหมือนกับต้นฉบับอย่างสมบูรณ์ รวมถึงแคชของ Pivot ด้วย

## ขั้นตอนที่ 4: (ทางเลือก) คัดลอกเฉพาะช่วงที่รวมตาราง Pivot

บางครั้งคุณอาจไม่ต้องการคัดลอกทั้งแผ่นงาน—อาจต้องการเพียงส่วนที่มี Pivot นี่คือจุดที่คุณ **copy Excel range** และระบุให้คัดลอก Pivot อย่างชัดเจน

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **ประโยชน์:** `setCopyPivotTable(true)` บังคับให้เอนจินทำสำเนาคำนิยาม Pivot แม้เมื่อคุณคัดลอกช่วงที่จำกัด หากไม่มีแฟล็กนี้ จะคัดลอกเฉพาะข้อมูลดิบและตาราง Pivot จะหายไป

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กปลายทาง

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อรันโปรแกรมจะสร้างไฟล์ `DuplicatedWithPivot.xlsx` ในไดเรกทอรีเป้าหมาย เปิดไฟล์ใน Excel แล้วคุณจะเห็น:

- แผ่นงานใหม่ชื่อ `Sheet1 (Copy)` (หรือชื่อเดิมที่ต่อด้วย “Copy”)
- ตาราง Pivot ปรากฏเหมือนเดิมในแผ่นงานต้นทาง ทำงานเต็มที่
- หากคุณใช้การคัดลอกช่วงแบบเลือกเฉพาะ จะมีเฉพาะเซลล์ A1:G30 เท่านั้น แต่ Pivot ยังทำงานได้เพราะแคชของมันถูกคัดลอกไป

## คำถามทั่วไปและกรณีขอบ

### วิธีคัดลอก Pivot ไปยังเวิร์กบุ๊กอื่นโดยไม่คัดลอกทั้งแผ่นงาน?

หากคุณต้องการเพียง Pivot และข้อมูลพื้นฐานของมัน ให้คัดลอกช่วงที่รวมทั้งข้อมูลต้นทางและ Pivot แล้วใช้ `setCopyPivotTable(true)`. โค้ดเดียวกันจาก **Step 4** ใช้ได้; เพียงตรวจสอบให้ช่วงครอบคลุมแหล่งข้อมูล

### ถ้าเวิร์กบุ๊กต้นทางมีหลายแผ่นงานที่มี Pivot จะทำอย่างไร?

ทำซ้ำ **Step 3** สำหรับแต่ละแผ่นงานที่คุณต้องการทำสำเนา:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### ทำงานกับแผ่นงานที่ถูกป้องกันได้หรือไม่?

Aspose.Cells สามารถคัดลอกแผ่นงานที่ถูกป้องกันได้ แต่คุณต้องยกเลิกการป้องกันก่อนหากต้องการแก้ไข Pivot หลังจากคัดลอก

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### ฉันสามารถคัดลอกตาราง Pivot ไปยังเวิร์กบุ๊กที่มีแผ่นงานชื่อเดียวกันอยู่แล้วได้หรือไม่?

ได้ ใช้ `addCopy` พร้อมชื่อที่ไม่ซ้ำกัน:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## เคล็ดลับพิเศษ: ตรวจสอบแคชของ Pivot

หลังจากคัดลอก คุณสามารถตรวจสอบโดยโปรแกรมว่ามีแคชของ Pivot อยู่หรือไม่:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

หากค่า ID ของแคชพิมพ์เป็นเลขที่ไม่เป็นลบ แสดงว่า Pivot ถูกทำสำเนาเรียบร้อยแล้ว

## สรุป

ตอนนี้คุณรู้วิธี **duplicate Excel sheet** ใน Java พร้อมกับคงตาราง Pivot ทั้งหมด, วิธี **copy pivot** ตารางโดยตรง, วิธี **copy Excel range** ที่รวม Pivot, และวิธี **copy sheet with pivot** หรือ **copy pivot to workbook** ด้วย Aspose.Cells 25.11+ แล้ว ใช้รูปแบบเหล่านี้เพื่ออัตโนมัติการสร้างรายงาน, สร้างสำเนาเทมเพลต, หรือสร้างสภาพแวดล้อมการทดสอบที่ต้องการการวิเคราะห์ด้วย Pivot ที่เหมือนกัน

พร้อมสำรวจต่อหรือยัง? ลองส่งออกเวิร์กบุ๊กที่ทำสำเนาเป็น PDF, หรือรีเฟรชแคชของ Pivot โดยโปรแกรมหลังการคัดลอกเพื่อให้แน่ใจว่าข้อมูลล่าสุดถูกแสดงออกมา ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [วิธีทำสำเนาแผ่นงานและคงตาราง Pivot ใน Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [วิธีคัดลอกตาราง Pivot ใน Java – คู่มือ Aspose.Cells ฉบับสมบูรณ์](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [วิธีคัดลอกช่วงและคงตาราง Pivot ใน Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}