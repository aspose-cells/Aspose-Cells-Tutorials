---
category: general
date: 2026-10-26
description: เรียนรู้วิธีคัดลอกตาราง Pivot ไปยังเวิร์กบุ๊กใหม่โดยใช้ Java พร้อมรักษาการจัดรูปแบบและคำนิยามของ
  Pivot ในขณะที่คุณคัดลอกช่วง Excel พร้อมการจัดรูปแบบผ่าน Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: th
lastmod: 2026-10-26
og_description: คัดลอก Pivot Table ไปยังเวิร์กบุ๊กใหม่ใน Java ด้วย Aspose.Cells คู่มือนี้แสดงวิธีคัดลอกช่วง
  Excel, รักษาการจัดรูปแบบ, และสร้างเวิร์กบุ๊กเปล่าอย่างมีประสิทธิภาพ.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: คัดลอก Pivot Table ไปยังเวิร์กบุ๊กใหม่ใน Java – คู่มือแบบขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: วิธีคัดลอกตาราง Pivot ไปยังเวิร์กบุ๊กใหม่ใน Java
url: /th/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอก pivot table ไปยัง workbook ใหม่ใน Java

หากคุณต้องการ **copy pivot table** จากไฟล์ Excel หนึ่งไปยังอีกไฟล์หนึ่ง คู่มือนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และสามารถรันได้ คุณจะได้เห็นวิธีการรักษาการกำหนด pivot, รักษาการจัดรูปแบบทั้งหมด, และหลีกเลี่ยงข้อผิดพลาดทั่วไปเมื่อคัดลอกช่วง Excel

การคัดลอก pivot table มักทำให้เกิดคำถามเช่น *how to copy pivot* โดยไม่ทำให้แหล่งข้อมูลเสียหายหรือสูญเสียสไตล์ เมื่อตอนจบของบทแนะนำนี้คุณจะมีโปรแกรม Java ที่ทำงานได้เองซึ่งสร้าง workbook ว่าง, คัดลอกช่วงที่ต้องการ, และบันทึกผลลัพธ์พร้อม pivot ที่คงอยู่

## สิ่งที่คุณจะได้ทำ

* โหลด workbook ต้นทางที่มี pivot table.  
* **Create empty workbook** ที่จะรับข้อมูลที่คัดลอก.  
* **Copy excel range** ที่รวม pivot, โดยใช้ตัวเลือกที่รักษา pivot และการจัดรูปแบบ.  
* บันทึกไฟล์ปลายทางและตรวจสอบว่า pivot ทำงานเหมือนต้นฉบับอย่างแม่นยำ

### ข้อกำหนดเบื้องต้น

* Java 17 หรือใหม่กว่า.  
* Aspose.Cells for Java (เวอร์ชัน 23.10 หรือใหม่กว่า).  
* ความคุ้นเคยพื้นฐานกับ IDE ของ Java (IntelliJ IDEA, Eclipse ฯลฯ).  

> **เคล็ดลับมืออาชีพ:** ใช้ไลเซนส์การประเมิน Aspose.Cells ฟรีสำหรับการทดสอบอย่างรวดเร็ว; แทนที่ด้วยไลเซนส์เต็มก่อนใช้งานจริง.

## คัดลอก pivot table ไปยัง workbook ใหม่

ขั้นตอนแรกคือการตั้งค่า workbook ต้นทางและปลายทาง workbook ปลายทางเริ่มต้นด้วยการเรียก **create empty workbook**, ซึ่งจะให้ไฟล์สะอาดพร้อมแผ่นงานเดียว

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

* `new Workbook()` **creates empty workbook** พร้อมแผ่นงานเริ่มต้น, ป้องกันการต้องลบข้อมูลที่มีอยู่.  
* `CopyOptions` บอก Aspose.Cells ให้คัดลอก metadata ของ **pivot table**, ไม่ใช่แค่ค่าดิบ. โหมด `PASTE_ALL` ยังคัดลอกสไตล์ของเซลล์, รูปแบบตัวเลข, และการจัดรูปแบบตามเงื่อนไข—ทำให้ตรงกับความต้องการ **copy range with formatting**.  
* `copyRange` ทำการ **copy excel range** ที่เคารพโครงสร้างภายในของต้นทาง, ทำให้ pivot ยังคงทำงานได้หลังการคัดลอก.

## วิธีคัดลอก pivot โดยไม่สูญเสียการจัดรูปแบบ

หากคุณใช้ `CopyOptions` เริ่มต้นเพียงอย่างเดียว บางข้อมูลสไตล์อาจถูกละเว้นในเวอร์ชันเก่าของ Aspose.Cells การตั้งค่าประเภทการวางอย่างชัดเจนจะรับประกันว่า **copy range with formatting** จะได้รับการเคารพ

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

การเพิ่ม `setPasteSpecialType` ทำให้ความกว้างของคอลัมน์, ความสูงของแถว, และแม้กระทั่งกฎการตรวจสอบข้อมูลเดินทางพร้อมกับช่วง นี่มีประโยชน์เป็นพิเศษเมื่อ pivot table ขยายหลายคอลัมน์ที่มีความกว้างกำหนดเอง

## สร้าง empty workbook ก่อนการคัดลอก

บางครั้งนักพัฒนาพยายามคัดลอกเข้า workbook ที่มีอยู่แล้วซึ่งมีข้อมูลอยู่แล้ว สิ่งนี้อาจทำให้ช่วงทับซ้อนหรือเขียนทับโดยไม่คาดคิด การเริ่มต้นด้วยการเรียก **create empty workbook** จะแยกการดำเนินการออกจากกัน:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

หากคุณต้องการมากกว่าหนึ่งแผ่นงานในปลายทาง คุณสามารถเพิ่มแผ่นงานเหล่านั้นหลังจากการคัดลอกได้:

```java
destWb.getWorksheets().add("Summary");
```

## คัดลอก Excel Range พร้อมการจัดรูปแบบโดยใช้ CopyOptions

นอกเหนือจาก pivot table, รูปแบบเดียวกันทำงานได้กับ **copy excel range** ใด ๆ ที่ต้องการการรักษาการจัดรูปแบบ—เช่น แผนภูมิ, ตาราง, หรือการจัดรูปแบบตามเงื่อนไข

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

อินสแตนซ์ `CopyOptions` ยังคงเหมือนเดิม ดังนั้นคุณจะได้พฤติกรรมที่สอดคล้องกันในหลายช่วง

### กรณีขอบเขตที่ควรพิจารณา

| สถานการณ์                              | วิธีการแนะนำ |
|----------------------------------------|----------------------|
| Workbook ต้นทางมีหลาย pivot           | คัดลอกช่วงของแต่ละ pivot แยกกันหรือคัดลอกทั้งแผ่นงาน |
| ปลายทางมีข้อมูลอยู่แล้ว               | เลือกเซลล์เริ่มต้นที่ไม่ขัดแย้ง (เช่น "H1") เมื่อเรียก `copyRange` |
| แหล่งข้อมูลของ pivot เป็นภายนอก (เช่น DB) | ตรวจสอบให้แน่ใจว่า workbook ปลายทางชี้ไปยังแหล่งข้อมูลภายนอกเดียวกัน, หรือรีเฟรช pivot หลังการคัดลอก |
| Workbook ขนาดใหญ่ ( > 10 MB )         | เพิ่มขนาด heap ของ Java (`-Xmx2g`) เพื่อหลีกเลี่ยง `OutOfMemoryError` |

## ตรวจสอบผลลัพธ์

หลังจากรันโปรแกรม, เปิด `destination.xlsx`. คุณควรเห็น:

* รูปแบบ Pivot Table ที่เหมือนกับใน `source.xlsx`.  
* สีของเซลล์, รูปแบบตัวเลข, และความกว้างของคอลัมน์ทั้งหมดถูกเก็บไว้  
* แหล่งข้อมูลของ Pivot ยังคงชี้ไปยังช่วงข้อมูลเดิมในไฟล์ใหม่, ดังนั้นการรีเฟรช Pivot จะอัปเดตค่าตามอย่างถูกต้อง

หาก pivot ปรากฏเป็นตารางคงที่, ตรวจสอบให้แน่ใจว่าได้ตั้งค่า `CopyOptions.setPasteType(PasteType.PASTE_ALL)` แล้ว หากไม่มีตัวเลือกนี้ Aspose.Cells จะถือ pivot เป็นข้อมูลธรรมดา

## สรุป

คุณตอนนี้รู้วิธี **copy pivot table** ไปยัง workbook ใหม่ใน Java พร้อมการรักษาการจัดรูปแบบ, การเชื่อมต่อข้อมูล, และโครงสร้างแผ่นงานแล้ว โซลูชันเต็มรูปแบบนี้แสดงการโหลดไฟล์ต้นทาง, **create empty workbook**, การกำหนดค่าตัวเลือก **copy excel range**, และการบันทึกผลลัพธ์

จากที่นี่คุณสามารถสำรวจหัวข้อที่เกี่ยวข้องเช่น **how to copy pivot** ข้ามแผ่นงานต่าง ๆ, ฝังแผนภูมิพร้อม pivot, หรืออัตโนมัติการประมวลผลหลาย workbook ทดลองปรับตั้งค่า `CopyOptions` ให้ตรงกับความต้องการอัตโนมัติของคุณ, แล้วคุณจะมีชุดเครื่องมือการจัดการ Excel ที่แข็งแกร่งอยู่ในมือ

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโครงการของคุณ

- [สร้าง Workbook ใหม่ใน Java – คู่มือเต็มการคัดลอก Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [คัดลอก Pivot Table ระหว่าง Workbook – คู่มือ Java ทีละขั้นตอน](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [วิธีคัดลอกช่วงและรักษา Pivot Table ใน Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}