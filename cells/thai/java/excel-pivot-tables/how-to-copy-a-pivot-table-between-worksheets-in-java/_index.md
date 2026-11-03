---
category: general
date: 2026-10-16
description: วิธีคัดลอก Pivot Table ใน Java ด้วย Aspose.Cells – เรียนรู้การคัดลอกช่วงข้อมูลไปยังแผ่นงานอื่นและการคัดลอกช่วงระหว่างแผ่นงานอย่างมีประสิทธิภาพ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: th
lastmod: 2026-10-16
og_description: วิธีคัดลอก Pivot Table ใน Java ด้วย Aspose.Cells บทเรียนนี้จะแสดงวิธีคัดลอกช่วงข้อมูลไปยังแผ่นงานอื่นและคัดลอกช่วงข้อมูลระหว่างแผ่นงานพร้อมโค้ดเต็ม
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: วิธีคัดลอก Pivot Table ระหว่างแผ่นงานใน Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: วิธีคัดลอกตาราง Pivot ระหว่างแผ่นงานใน Java
url: /th/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอก Pivot Table ระหว่าง Worksheet ใน Java

หากคุณต้องการ **how to copy pivot table** จากแผ่นงานหนึ่งไปยังอีกแผ่นงานในเวิร์กบุ๊กเดียวกัน คู่มือนี้จะให้วิธีแก้ที่สมบูรณ์และพร้อมใช้งาน คุณจะได้เห็นวิธีคัดลอกช่วงต้นฉบับที่มี Pivot Table, รักษาฟังก์ชันการทำงานของมัน, และตรวจสอบผลลัพธ์—ทั้งหมดโดยใช้ Aspose.Cells for Java

การคัดลอก Pivot Table เป็นงานทั่วไปเมื่อคุณสร้างรายงานโดยอัตโนมัติ และการทำอย่างถูกต้องจะช่วยหลีกเลี่ยงการสูญเสีย Pivot Cache หรือทำให้สูตรเสียหาย เมื่อจบบทเรียนนี้คุณจะสามารถ **copy range to another sheet** และ **copy range between worksheets** ได้โดยไม่ต้องทำขั้นตอนด้วยตนเอง

## สิ่งที่คุณจะได้เรียนรู้

* โหลดไฟล์ Excel ที่มี Pivot Table อยู่แล้ว
* กำหนดช่วงต้นฉบับที่เก็บ Pivot Table
* กำหนดช่วงปลายทางบน Worksheet ที่ต่างกัน
* ใช้ `CopyOptions` เพื่อรักษา Pivot Table ให้อยู่ครบถ้วน
* ตรวจสอบว่า Pivot Table ที่คัดลอกทำงานตามที่คาดหวัง

**Prerequisites**

* Java 17 หรือใหม่กว่า
* Aspose.Cells for Java (เวอร์ชัน 23.12 หรือใหม่กว่า)  
* ไฟล์ Excel (`input.xlsx`) ที่มี Pivot Table อยู่บนแผ่นแรก

---

## วิธีคัดลอก Pivot Table ด้วย Aspose.Cells

หัวใจของการดำเนินการคือกระบวนการสี่ขั้นตอน: โหลดเวิร์กบุ๊ก, ค้นหาช่วงต้นฉบับ, กำหนดช่วงปลายทาง, และทำการคัดลอก ด้านล่างแต่ละขั้นตอนจะอธิบายอย่างละเอียด

### ขั้นตอน 1: โหลดเวิร์กบุ๊ก

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*ทำไมต้องทำขั้นตอนนี้?*  
การโหลดเวิร์กบุ๊กจะนำไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้คุณเข้าถึง Worksheet, เซลล์, และ Pivot Cache ได้ Aspose.Cells จะอ่านรูปแบบไฟล์โดยอัตโนมัติ ดังนั้นคุณไม่ต้องกังวลเรื่อง `.xls` กับ `.xlsx`

### ขั้นตอน 2: ค้นหาช่วงต้นฉบับที่มี Pivot Table

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*ทำไมต้องทำขั้นตอนนี้?*  
Pivot Table ถูกเก็บในบล็อกเซลล์ที่อ้างอิงถึงแคชที่ซ่อนอยู่ โดยการเลือกช่วงที่ตรงกัน (`A1:G20` ในตัวอย่างนี้) คุณจะทำให้แคชยังคงเชื่อมต่อเมื่อคัดลอกช่วงนั้น

### ขั้นตอน 3: กำหนดช่วงปลายทางบนแผ่นงานอื่น

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*ทำไมต้องทำขั้นตอนนี้?*  
การเลือกปลายทางบน Worksheet ที่ต่างกันทำให้คุณสามารถ **copy range to another sheet** เซลล์ซ้ายบน (`A1`) เป็นจุดเริ่มต้นที่ทั่วไป แต่คุณสามารถวางไว้ที่ใดก็ได้โดยเปลี่ยนที่อยู่

### ขั้นตอน 4: คัดลอกช่วงต้นฉบับพร้อมรักษา Pivot Table

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*ทำไมต้องทำขั้นตอนนี้?*  
`CopyOptions` ควบคุมสิ่งที่ถูกถ่ายโอน การใช้ `PasteType.PASTE_ALL` รับประกันว่า Pivot Table, การจัดรูปแบบ, และสูตรพื้นฐานจะถูกทำซ้ำ หากไม่มีตัวเลือกเหล่านี้ อาจจะคัดลอกเฉพาะค่าดิบเท่านั้น ทำให้ฟังก์ชัน Pivot เสีย

### ขั้นตอน 5: บันทึกเวิร์กบุ๊กและตรวจสอบผลลัพธ์

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

เปิด `output.xlsx` ใน Excel และยืนยันว่า:

* แผ่นที่สองมี Pivot Table ที่ทำงานเต็มรูปแบบและเหมือนกับต้นฉบับ
* การรีเฟรช Pivot Table จะอัปเดตข้อมูล แสดงว่าแคชยังคงอยู่

---

## คัดลอกช่วงไปยังแผ่นอื่นโดยใช้ Java

หากเป้าหมายของคุณคือเพียง **copy range to another sheet** โดยไม่มี Pivot Table โค้ดเดียวกันก็ทำงานกับช่วงเซลล์ปกติ การเปลี่ยนแค่ที่อยู่ของต้นฉบับเท่านั้น การตั้งค่า `CopyOptions` ยังคงเหมือนเดิม เพื่อให้สูตรและการจัดรูปแบบถูกเก็บไว้

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

ส่วนโค้ดนี้แสดงให้เห็นถึงความยืดหยุ่นของ API สำหรับสถานการณ์ที่มีและไม่มี Pivot

---

## คัดลอกช่วงระหว่าง Worksheet โดยไม่สูญเสียสูตร

เมื่อคุณ **copy range between worksheets** สูตรที่อ้างอิงถึงแผ่นอื่นอาจเสียหายหากการอ้างอิงเชิงสัมพันธ์เปลี่ยนแปลง เพื่อหลีกเลี่ยงสิ่งนี้:

1. ใช้ `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` หากคุณต้องการเพียงสูตร
2. เก็บแผ่นปลายทางในเวิร์กบุ๊กเดียวกันเพื่อให้การอ้างอิงภายในยังคงใช้ได้
3. หลังการคัดลอก ให้เรียก `workbook.calculateFormula();` เพื่อบังคับให้คำนวณใหม่

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

ขั้นตอนเพิ่มเติมเหล่านี้ทำให้แน่ใจว่าช่วงที่คัดลอกทำงานเหมือนต้นฉบับ แม้จะขยายข้ามหลาย Worksheet

---

## เคล็ดลับระดับมืออาชีพและข้อผิดพลาดทั่วไป

| สถานการณ์ | เคล็ดลับ |
|-----------|----------|
| **Pivot cache ไม่อัปเดต** | หลังการคัดลอก ให้เรียก `destSheet.getPivotTables().get(0).refresh();` เพื่อรีเฟรชแคช |
| **คัดลอกไปยังเวิร์กบุ๊กอื่น** | ใช้ `Workbook destWorkbook = new Workbook();` แล้ว `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. จำไว้ว่าต้องคัดลอก Pivot Cache แยกต่างหากหากจำเป็น |
| **Pivot Table ขนาดใหญ่** | เพิ่มขนาด heap ของ Java (`-Xmx2g`) เพื่อหลีกเลี่ยง `OutOfMemoryError` ระหว่างการคัดลอก |
| **รักษารูปแบบ** | ตั้งค่า `copyOptions.setPasteType(PasteType.PASTE_ALL)`; มิฉะนั้นจะคัดลอกเฉพาะค่าเท่านั้น |

---

## ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมเต็มจะสร้าง `output.xlsx`. เมื่อเปิดใน Excel:

* **Sheet2!A1:G20** แสดง Pivot Table เดียวกันกับ **Sheet1!A1:G20**.
* รายการฟิลด์ Pivot, ป้ายแถว/คอลัมน์, และค่าข้อมูลตรงกับต้นฉบับ.
* การรีเฟรช Pivot จะอัปเดตตัวเลข ยืนยันว่าแคชทำงาน.

คอนโซลจะแสดง:

```
Pivot table copied successfully.
```

---

## สรุป

ในบทเรียนนี้คุณได้เรียนรู้ **how to copy pivot table** จาก Worksheet หนึ่งไปยังอีก Worksheet หนึ่งโดยใช้ Aspose.Cells for Java ด้วยการโหลดเวิร์กบุ๊ก, เลือกช่วงต้นฉบับที่ถูกต้อง, กำหนดปลายทาง, และตั้งค่า `CopyOptions` คุณสามารถ **copy range to another sheet** และ **copy range between worksheets** ได้อย่างมั่นใจพร้อมรักษาฟังก์ชันการทำงานของ Pivot ทั้งหมด  

ต่อไปคุณอาจสำรวจ:

* ส่งออก Pivot Table ที่คัดลอกเป็น PDF หรือ HTML
* อัตโนมัติการรีเฟรช Pivot Table ในหลายเวิร์กบุ๊ก
* ใช้ `CopyOptions` เพื่อคัดลอกเฉพาะส่วนที่ต้องการ (เช่น ค่า, รูปแบบ)

ลองทดลองกับที่อยู่ช่วงต่าง ๆ, โครงสร้างเวิร์กบุ๊ก, หรือแม้กระทั่งการคัดลอกข้ามเวิร์กบุ๊กได้ตามต้องการ ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ

- [วิธีคัดลอกช่วงใน Java – คัดลอก Pivot Table ด้วย Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [วิธีคัดลอก Pivot Table ใน Java – คู่มือ Aspose.Cells ฉบับสมบูรณ์](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [คัดลอก Pivot Table Excel – คู่มือขั้นตอนโดยใช้ Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}