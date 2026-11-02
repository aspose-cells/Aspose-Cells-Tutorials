---
category: general
date: 2026-08-08
description: วิธีคัดลอก Pivot ใน Aspose.Cells และคัดลอกช่วงข้อมูลไปยังเวิร์กบุ๊กโดยใช้
  Java. เรียนรู้ขั้นตอนที่ชัดเจนในการทำสำเนาตาราง Pivot ด้วย CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: th
lastmod: 2026-08-08
og_description: วิธีคัดลอก Pivot ใน Aspose.Cells และคัดลอกช่วงไปยังเวิร์กบุ๊กด้วย
  Java. ปฏิบัติตามคู่มือฉบับเต็มนี้เพื่อทำสำเนาตาราง Pivot โดยใช้ CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: วิธีคัดลอก Pivot ใน Aspose.Cells – คัดลอกช่วงไปยังเวิร์กบุ๊ก
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: วิธีคัดลอก Pivot ใน Aspose.Cells – คัดลอกช่วงไปยังเวิร์กบุ๊ก
url: /th/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอกพีโวตใน Aspose.Cells – คัดลอกช่วงไปยังเวิร์กบุ๊ก

หากคุณต้องการ **how to copy pivot** ในไฟล์ Excel ด้วย Aspose.Cells คู่มือนี้จะแสดงขั้นตอนที่แน่นอนให้คุณ เมื่อจบบทเรียนคุณจะสามารถ **copy range to workbook** พร้อมคงการกำหนดตารางพีโวตไว้ได้

ตัวอย่างใช้ Java แต่แนวคิดเดียวกันสามารถใช้กับภาษา .NET ใด ๆ ที่ทำงานกับ Aspose.Cells ได้ ไม่จำเป็นต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี Aspose.Cells สำหรับ Java และสภาพแวดล้อมการพัฒนาพื้นฐาน

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่ม ให้ตรวจสอบว่าคุณมี:

* Java Development Kit (JDK) 8 หรือใหม่กว่า.
* Maven หรือ Gradle เพื่อจัดการ dependencies (ตัวอย่างใช้ Maven).
* Aspose.Cells for Java 23.9 (หรือเวอร์ชันล่าสุด) ที่เพิ่มในโปรเจคของคุณ.
* เวิร์กบุ๊กอินพุต (`input.xlsx`) ที่มีตารางพีโวตอย่างน้อยหนึ่งตารางบนแผ่นงานแรก.

การเตรียมสิ่งเหล่านี้ไว้ล่วงหน้าจะช่วยป้องกันข้อผิดพลาดระหว่างรันไทม์เมื่อโค้ดเข้าถึงเวิร์กบุ๊ก

## วิธีคัดลอกพีโวตด้วย Aspose.Cells

ส่วนนี้จะอธิบายขั้นตอนแต่ละขั้นที่จำเป็นเพื่อ **how to copy pivot** จากส่วนหนึ่งของแผ่นงานไปยังอีกส่วนหนึ่ง โดยใช้คลาส `CopyOptions`.

### ขั้นตอน 1: เพิ่ม Aspose.Cells ไปยังโปรเจคของคุณ

หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*ทำไมขั้นตอนนี้ถึงสำคัญ*: ไลบรารีนี้ให้คลาส `Workbook`, `CopyOptions` และคลาสอื่น ๆ ที่จำเป็นสำหรับการดำเนินการ **aspose.cells copy range** หากไม่มี dependency ตัวคอมไพเลอร์จะไม่สามารถระบุประเภทเหล่านั้นได้.

### ขั้นตอน 2: โหลดเวิร์กบุ๊กต้นฉบับ

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

การโหลดไฟล์จะสร้างการแสดงผลของสเปรดชีตในหน่วยความจำ `Workbook` ให้คุณเข้าถึงแผ่นงาน, เซลล์, และตารางพีโวต.

### ขั้นตอน 3: กำหนดค่า copy options เพื่อรวมตารางพีโวต

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` บอก Aspose.Cells ว่าการดำเนินการควรคง metadata ของตารางพีโวตไว้ หากคุณละเว้นแฟล็กนี้ ตารางพีโวตจะถูกแปลงเป็นข้อมูลคงที่และสูญเสียความโต้ตอบ

### ขั้นตอน 4: คัดลอกช่วงที่ต้องการพร้อมตารางพีโวต

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

เมธอด `copyRange` จะคัดลอกเซลล์, การจัดรูปแบบ, และ—เนื่องจากตัวเลือกที่ตั้งค่าในขั้นตอนก่อนหน้า—ตารางพีโวตใด ๆ ที่ตัดกับช่วงนั้น นี่คือหัวใจของฟังก์ชัน **copy range to workbook**.

### ขั้นตอน 5: บันทึกเวิร์กบุ๊กที่แก้ไขแล้ว

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

การบันทึกจะเขียนการเปลี่ยนแปลงลงในไฟล์ใหม่ (`output.xlsx`). ตอนนี้คุณสามารถเปิดไฟล์นี้ใน Excel และเห็นว่าตารางพีโวตได้ถูกทำสำเนาอย่างตรงตำแหน่งที่ช่วงถูกคัดลอก.

## ตัวอย่างเต็มที่สามารถรันได้

เมื่อรวมส่วนต่าง ๆ เข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคอมไพล์และรันได้:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

* `output.xlsx` มีข้อมูลเดียวกับ `input.xlsx`.
* ตารางพีโวตที่เคยอยู่ในช่วงต้นฉบับจะปรากฏในเซลล์ปลายทาง ทำงานเต็มรูปแบบ (ฟิลเตอร์, ความสามารถรีเฟรช ฯลฯ).
* การจัดรูปแบบเซลล์, สูตร, และความกว้างของคอลัมน์ทั้งหมดจะถูกคงไว้เนื่องจาก `copyRange` คัดลอกบล็อกเซลล์ทั้งหมด.

## คำถามทั่วไปและกรณีขอบ

**ถ้าช่วงปลายทางทับกับตารางพีโวตที่มีอยู่แล้วจะเป็นอย่างไร?**  
Aspose.Cells จะเขียนทับเซลล์เป้าหมาย เพื่อหลีกเลี่ยงการสูญเสียข้อมูล ให้ตรวจสอบว่าพื้นที่ปลายทางว่างเปล่าหรือย้ายตารางพีโวตที่มีอยู่ก่อน.

**ฉันสามารถคัดลอกตารางพีโวตข้ามแผ่นงานได้หรือไม่?**  
ได้. ใช้ `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` โดยที่ `targetSheetIndex` ชี้ไปยังแผ่นงานปลายทาง.

**`setCopyPivotTable(true)` จะคัดลอกแหล่งข้อมูลพื้นฐานหรือไม่?**  
เมธอดนี้คัดลอกเพียงการอ้างอิง pivot cache เท่านั้น หากข้อมูลต้นทางอยู่ในเวิร์กบุ๊กเดียวกัน พีโวตปลายทางจะชี้ไปยัง cache เดียวกัน เพื่อทำสำเนา cache คุณต้องสร้าง pivot cache ใหม่ด้วยตนเอง.

**จะคัดลอกช่วงขนาดใหญ่อย่างมีประสิทธิภาพอย่างไร?**  
เมื่อคัดลอกช่วงที่ใหญ่มาก ควรพิจารณาใช้ `CopyOptions.setCopyFormula(true)` และ `setCopyDataValidation(true)` เฉพาะเมื่อจำเป็น การลดจำนวนตัวเลือกสามารถเพิ่มประสิทธิภาพได้.

## เคล็ดลับสำหรับการใช้ **aspose.cells copy range** อย่างเชื่อถือได้

* **เคล็ดลับมืออาชีพ:** ควรเรียก `workbook.calculateFormula()` หลังจากคัดลอก หากช่วงมีสูตรที่พึ่งพา pivot cache.
* **ระวัง:** แผ่นงานที่ซ่อนอยู่ `copyRange` ทำงานเฉพาะบนแผ่นงานที่มองเห็นได้ หากไม่ได้อ้างอิงแผ่นงานที่ซ่อนโดยชี้ดัชนี.
* **ตรวจสอบเวอร์ชัน:** แฟล็ก `setCopyPivotTable` มีตั้งแต่ Aspose.Cells 20.9 ตรวจสอบให้แน่ใจว่าไลบรารีของคุณรองรับ.

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to copy pivot** ใน Aspose.Cells และวิธี **copy range to workbook** พร้อมคงการทำงานของพีโวตทั้งหมด ขั้นตอน—การเพิ่มไลบรารี, การโหลดเวิร์กบุ๊ก, การกำหนดค่า `CopyOptions`, การทำการคัดลอก, และการบันทึก—เป็นรูปแบบที่ทำซ้ำได้และคุณสามารถปรับใช้กับสถานการณ์คัดลอก‑วางอื่น ๆ

ต่อไปสำรวจหัวข้อที่เกี่ยวข้องเช่น **aspose.cells copy range** สำหรับแผนภูมิ, การจัดรูปแบบตามเงื่อนไข, และการตรวจสอบข้อมูล ทดลองคัดลอกจากรูปแบบไฟล์ต่าง ๆ (XLSX → XLS) เพื่อขยายความสามารถในการอัตโนมัติของคุณ ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจคของคุณ.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}