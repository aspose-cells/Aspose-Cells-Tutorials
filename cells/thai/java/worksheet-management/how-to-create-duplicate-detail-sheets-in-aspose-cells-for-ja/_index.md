---
category: general
date: 2026-08-17
description: เรียนรู้วิธีสร้างชีตรายละเอียดซ้ำด้วย Aspose.Cells สำหรับ Java และอนุญาตให้ใช้ชื่อชีตซ้ำโดยใช้
  SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: th
lastmod: 2026-08-17
og_description: สร้างแผ่นรายละเอียดซ้ำใน Aspose.Cells สำหรับ Java และอนุญาตให้ใช้ชื่อแผ่นซ้ำได้
  ตามบทแนะนำฉบับเต็มนี้เพื่อผลลัพธ์ทันที
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: สร้างแผ่นรายละเอียดซ้ำใน Aspose.Cells สำหรับ Java – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: วิธีสร้างแผ่นรายละเอียดซ้ำใน Aspose.Cells สำหรับ Java
url: /th/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างแผ่นรายละเอียดซ้ำใน Aspose.Cells สำหรับ Java

หากคุณต้อง **สร้างแผ่นรายละเอียดซ้ำ** ในเวิร์กบุ๊ก Excel, Aspose.Cells สำหรับ Java ทำให้กระบวนการนี้ง่ายดาย ตัวอย่างสอนนี้จะแสดงอย่างละเอียดว่าอย่างไรจึงจะอนุญาตให้ใช้ชื่อแผ่นซ้ำกันขณะสร้างแผ่นรายละเอียดด้วย SmartMarkerProcessor, เพื่อให้คุณสามารถสร้างเวิร์กบุ๊กที่มีหลายแผ่นที่ใช้ชื่อเดียวกันได้

คุณจะได้เห็นตัวอย่างเต็มรูปแบบที่สามารถรันได้, การอธิบายแต่ละตัวเลือกการกำหนดค่า, และเคล็ดลับสำหรับการจัดการกรณีขอบที่พบบ่อย เช่น การชนกันของชื่อและชุดข้อมูลขนาดใหญ่ ไม่ต้องอ้างอิงภายนอก—ทุกอย่างที่คุณต้องการรวมอยู่ในโค้ดด้านล่างนี้แล้ว

## ข้อกำหนดเบื้องต้น

ก่อนเริ่ม, โปรดตรวจสอบว่าคุณมี:

* Java Development Kit (JDK) 8 หรือใหม่กว่า
* Maven หรือ Gradle เพื่อจัดการ dependencies
* ไลบรารี Aspose.Cells สำหรับ Java (เวอร์ชัน 23.9 หรือใหม่กว่า) เพิ่ม dependency ของ Maven ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* เทมเพลตเวิร์กบุ๊กหลัก (`master_template.xlsx`) ที่มีพื้นที่ Smart Marker สำหรับข้อมูลรายละเอียด

## ภาพรวมของวิธีแก้

วิธีแก้ประกอบด้วยสี่ขั้นตอนหลัก:

1. โหลดเทมเพลตเวิร์กบุ๊กหลัก
2. กำหนดค่า `SmartMarkerProcessor` ให้ **อนุญาตให้ใช้ชื่อแผ่นซ้ำ**
3. ประมวลผลเวิร์กบุ๊กเพื่อสร้างแผ่นรายละเอียดใหม่สำหรับแต่ละกลุ่มข้อมูล
4. บันทึกเวิร์กบุ๊กที่ได้ซึ่งตอนนี้มีแผ่นรายละเอียดซ้ำแล้ว

แต่ละขั้นตอนจะอธิบายรายละเอียดต่อไปนี้, และไฟล์ซอร์สเต็มจะอยู่ที่ส่วนท้ายของคู่มือ

## ขั้นตอนที่ 1: โหลดเทมเพลตเวิร์กบุ๊กหลัก

การดำเนินการแรกสร้างอ็อบเจ็กต์ `Workbook` ที่แทนไฟล์เทมเพลต เทมเพลตต้องมีตัวแทน Smart Marker (เช่น `&=DetailData`) เพื่อบอกโปรเซสเซอร์ว่าต้องใส่ข้อมูลที่ไหน

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**ทำไมจึงสำคัญ:** การโหลดเทมเพลตแยกส่วนการจัดรูปแบบและเลย์เอาต์ออกจากตรรกะการสร้างข้อมูล ทำให้โค้ดของคุณสะอาดและง่ายต่อการใช้เทมเพลตเดียวกันกับชุดข้อมูลต่าง ๆ

## ขั้นตอนที่ 2: กำหนดค่า SmartMarkerProcessor ให้อนุญาตชื่อแผ่นซ้ำ

โดยค่าเริ่มต้น, Aspose.Cells จะสร้างชื่อแผ่นที่ไม่ซ้ำกันเมื่อสร้างแผ่นรายละเอียด เพื่อ **อนุญาตให้ใช้ชื่อแผ่นซ้ำ**, ตั้งค่าตัวเลือก `DetailSheetNewName` เป็นค่าคงที่ โปรเซสเซอร์จะใช้ชื่อนี้ซ้ำสำหรับแต่ละแผ่นที่สร้างขึ้น

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**ทำไมจึงสำคัญ:** การตั้งค่า `DetailSheetNewName` บอกให้เอนจินใช้ชื่อเดียวกันสำหรับทุกแผ่นรายละเอียด, ซึ่งตรงกับความต้องการ **อนุญาตให้ใช้ชื่อแผ่นซ้ำ** วิธีนี้มีประโยชน์เมื่อเครื่องมือ downstream ระบุตำแหน่งแผ่นโดยอิงตำแหน่งแทนชื่อ

## ขั้นตอนที่ 3: ประมวลผลเวิร์กบุ๊กเพื่อสร้างแผ่นรายละเอียด

หลังจากกำหนดค่า, เรียก `process` บนเวิร์กบุ๊ก โปรเซสเซอร์จะอ่านพื้นที่ Smart Marker, สร้างแผ่นใหม่สำหรับแต่ละกลุ่มข้อมูล, และเติมข้อมูลลงในแผ่นนั้น

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**ทำไมจึงสำคัญ:** คำสั่ง `process` ทำหน้าที่หลัก—การพาร์ส Smart Marker, การโคลนแผ่นเทมเพลต, และการใส่ข้อมูล เนื่องจากได้ตั้งค่า `DetailSheetNewName` ไว้แล้ว, แผ่นใหม่แต่ละแผ่นจะได้รับชื่อเดียวกัน, ทำให้ไฟล์สุดท้ายมีชื่อแผ่นซ้ำกัน

## ขั้นตอนที่ 4: บันทึกเวิร์กบุ๊กที่ได้

สุดท้าย, เขียนเวิร์กบุ๊กที่แก้ไขแล้วลงไฟล์ใหม่ ไฟล์ผลลัพธ์จะมีแท็บ “DetailSheet” จำนวนเท่ากับจำนวนกลุ่มข้อมูล

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**ทำไมจึงสำคัญ:** การบันทึกไฟล์เป็นการสรุปการเปลี่ยนแปลงที่โปรเซสเซอร์ทำ เวิร์กบุ๊กที่ได้สามารถเปิดด้วย Microsoft Excel, LibreOffice หรือแอปพลิเคชันสเปรดชีตอื่น ๆ ที่รองรับรูปแบบ XLSX

## โค้ดต้นฉบับเต็ม

รวมทุกส่วนเข้าด้วยกัน, นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก, วาง, และรันได้:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด `duplicate_detail.xlsx`, คุณจะเห็นแท็บหลายแท็บที่ชื่อ **DetailSheet** แต่ละแท็บจะมีชุดข้อมูลที่สอดคล้องกับกลุ่ม Smart Marker เฉพาะในเทมเพลต การจัดรูปแบบ, ฟอร์แมต, และสูตรจากเทมเพลตหลักจะถูกคงไว้ในทุกแผ่นซ้ำ

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | คำอธิบาย | วิธีแก้ |
|-------|----------|---------|
| Excel แสดงคำเตือนเกี่ยวกับชื่อแผ่นซ้ำ | Excel อนุญาตให้ใช้ชื่อซ้ำได้แต่บางครั้งจะแสดงคำเตือนเมื่อเปิดไฟล์ | คำเตือนไม่มีผลเสีย; เวิร์กบุ๊กทำงานได้ตามปกติ หากต้องการปิดคำเตือน, ให้เปลี่ยนชื่อแผ่นหลังการประมวลผลโดยใช้ `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);` |
| ชุดข้อมูลขนาดใหญ่ทำให้ใช้หน่วยความจำสูง | การสร้างแผ่นซ้ำแต่ละแผ่นจะคัดลอกเทมเพลตเต็มรูปแบบ, ทำให้ใช้ RAM มาก | เปิดโหมดสตรีมมิ่งด้วย `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` ก่อนโหลดเทมเพลต |
| ไม่พบพื้นที่ Smart Marker | โปรเซสเซอร์ไม่สามารถหาตัวแทน `&=DetailData` ในเทมเพลต | ตรวจสอบว่าซินแทกซ์ของตัวแทนตรงกับแหล่งข้อมูลและแผ่นเทมเพลตไม่ได้ถูกซ่อน |

## เคล็ดลับพิเศษ: ปรับแต่งรูปแบบการตั้งชื่อซ้ำ

หากคุณต้องการรูปแบบการตั้งชื่อที่คาดเดาได้พร้อมยังคงอนุญาตให้ซ้ำ, สามารถผสานชื่อฐานกับดัชนีได้:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

ตัวแทน `{0}` จะถูกแทนที่ด้วยดัชนีของแผ่น, ผลลัพธ์เป็นชื่อเช่น `DetailSheet_1`, `DetailSheet_2` เป็นต้น วิธีนี้ยังคงตอบสนองความต้องการ **อนุญาตให้ใช้ชื่อแผ่นซ้ำ** เนื่องจากชื่อฐานคงที่

## ขั้นตอนต่อไป

ตอนนี้คุณสามารถ **สร้างแผ่นรายละเอียดซ้ำ** แล้ว, คุณอาจสำรวจหัวข้อต่อไปนี้:

* **เติมแผ่นรายละเอียดด้วยรูปภาพ** – ใช้วัตถุ `Picture` เพื่อฝังโลโก้หรือแผนภูมิ
* **ใช้ Conditional Formatting** – เพิ่มกฎ `FormatCondition` เพื่อไฮไลท์แถวตามค่า
* **ส่งออกเป็น PDF** – เรียก `workbook.save("output.pdf", SaveFormat.PDF);` เพื่อสร้างไฟล์ PDF ของแผ่นที่ซ้ำกัน

ส่วนขยายเหล่านี้อิงจากเวิร์กโฟลว์ Smart Marker ที่แสดงในบทนี้, ช่วยให้คุณอัตโนมัติการสร้างรายงาน Excel ที่ซับซ้อนได้อย่างมั่นใจ

---

*คุณได้เรียนรู้วิธีสร้างแผ่นรายละเอียดซ้ำใน Aspose.Cells สำหรับ Java และวิธีอนุญาตให้ใช้ชื่อแผ่นซ้ำด้วย SmartMarkerProcessor. นำโค้ดไปใช้, ปรับเทมเพลต, และผสานเทคนิคนี้เข้ากับกระบวนการรายงานของคุณ*


## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโครงการของคุณ

- [Create & Access Excel Sheets, Add PDF Bookmarks Using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}