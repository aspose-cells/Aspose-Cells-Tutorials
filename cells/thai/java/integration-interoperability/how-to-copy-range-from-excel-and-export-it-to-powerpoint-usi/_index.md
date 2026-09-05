---
category: general
date: 2026-09-05
description: เรียนรู้วิธีคัดลอกช่วงใน Excel, ส่งออก Excel ไปยัง PowerPoint และแปลง
  Excel เป็นไฟล์ pptx พร้อมตัวอย่าง Java ฉบับสมบูรณ์
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: th
lastmod: 2026-09-05
og_description: วิธีคัดลอกช่วงข้อมูลและส่งออก Excel ไปยัง PowerPoint ด้วย Java. ปฏิบัติตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อแปลง
  Excel เป็น PPTX อย่างมีประสิทธิภาพ.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: วิธีคัดลอกช่วงจาก Excel แล้วส่งออกไปยัง PowerPoint ด้วย Java
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: วิธีคัดลอกช่วงจาก Excel และส่งออกไปยัง PowerPoint ด้วย Java
url: /th/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอกช่วงจาก Excel และส่งออกไปยัง PowerPoint ด้วย Java

หากคุณต้องการ **how to copy range** จากเวิร์กบุ๊ก Excel แล้ว **export excel to PowerPoint**, คู่มือนี้จะให้วิธีแก้ที่สมบูรณ์และพร้อมใช้งาน คุณจะได้เห็นวิธีคัดลอกช่วงที่มี pivot‑table, สร้าง worksheet ใหม่สำหรับการคัดลอก, และสุดท้าย **convert Excel to PPTX** ด้วยการเรียกเมธอดเดียว

การคัดลอกช่วงและการส่งออกเวิร์กบุ๊กเป็นความต้องการทั่วไปเมื่อคุณสร้างรายงาน, สไลด์เด็ค, หรือแดชบอร์ดโดยอัตโนมัติ เมื่อจบบทเรียนนี้คุณจะมีโปรแกรม Java ที่:

* โหลดไฟล์ `.xlsx` ที่มีอยู่
* คัดลอกช่วง `A1:H20` (รวม pivot table) ไปยังชีตใหม่
* บันทึกเวิร์กบุ๊กเป็นไฟล์พรีเซนเทชัน `.pptx` ที่แก้ไขได้

คุณต้องการเพียงไลบรารี Aspose.Cells for Java; ไม่ต้องมี dependency เพิ่มเติม

## Prerequisites

ก่อนเริ่มทำงาน, โปรดตรวจสอบว่าคุณมี:

* Java 17 (หรือใหม่กว่า) ติดตั้งอยู่
* Maven หรือ Gradle สำหรับจัดการ dependency
* Aspose.Cells for Java 23.9 (หรือเวอร์ชันล่าสุด) – เพิ่มเข้าไปในโปรเจกต์ตามตัวอย่าง Maven ด้านล่าง
* ไฟล์ Excel (`input.xlsx`) ที่มีข้อมูลและ pivot table ที่ต้องการคัดลอก

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Step 1: Load the workbook from a file

ขั้นตอนแรกของ **how to copy range** คือการเปิดเวิร์กบุ๊กต้นฉบับ ซึ่งทำให้คุณเข้าถึง worksheet, cell, และ pivot table ได้

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Why this step?*  
การโหลดไฟล์จะสร้างการแสดงผลในหน่วยความจำของเอกสาร Excel, ทำให้คุณสามารถจัดการเนื้อหาได้โดยไม่ต้องแก้ไขไฟล์ต้นฉบับ

## Step 2: Get the source worksheet that holds the data

โดยทั่วไปชีตแรกจะเป็นที่เก็บข้อมูลที่คุณต้องการคัดลอก คุณสามารถดึงได้โดยใช้ดัชนี

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

หากเวิร์กบุ๊กของคุณเก็บ pivot table ไว้ในชีตอื่น, ให้เปลี่ยน `0` เป็นดัชนีที่เหมาะสมหรือใช้ `get("SheetName")`

## Step 3: Add a new worksheet for the copied range

การสร้างชีตปลายทางช่วยแยกข้อมูลที่คัดลอกออกและทำให้ขั้นตอนการส่งออกต่อไปสะอาดขึ้น

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

คุณสามารถตั้งชื่อชีตตามต้องการ; ชื่อ “Copy” จะสื่อให้เห็นว่าเป็นช่วงที่ถูกทำซ้ำ

## Step 4: Copy the range (how to copy range) including the pivot table

ตอนนี้เราจะทำการคัดลอก **how to copy range** หลัก `copyRange` จะคัดลอกทั้งค่าและรูปแบบ, พร้อมรักษาการกำหนด pivot table ไว้

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Why use `CopyOptions`?*  
การให้ `CopyOptions` ช่วยให้คุณปรับแต่งสิ่งที่ต้องการคัดลอก (เช่น สูตร, ความกว้างคอลัมน์) ตัวสร้างค่าเริ่มต้นจะคัดลอกทุกอย่าง, เหมาะเมื่อคุณต้องการสำเนาที่ตรงกับ **copy pivot table sheet** อย่างสมบูรณ์

## Step 5: Prepare options to export the workbook as an editable PowerPoint presentation

การส่งออกเป็น PowerPoint ทำผ่าน `ImageOrPrintOptions` การตั้งค่า `SaveFormat.PPTX` จะบอก Aspose.Cells ให้สร้างไฟล์ PowerPoint แทนภาพ

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

คุณยังสามารถปรับขนาดสไลด์, DPI, และการตั้งค่าอื่น ๆ ของพรีเซนเทชันผ่าน `pptOptions` หากต้องการเลย์เอาต์แบบกำหนดเอง

## Step 6: Save the workbook as a PPTX file (convert excel to pptx)

สุดท้ายเรียก `workbook.save` พร้อมตัวเลือก PPTX ขั้นตอนนี้คือ **how to export excel** ไปยังสไลด์เด็ค

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

เมื่อโปรแกรมทำงานเสร็จ, `output.pptx` จะมีสไลด์เดียวที่แสดงช่วงที่คัดลอกตรงตามที่อยู่ใน Excel, รวมถึงการควบคุม pivot table ด้วย

### Expected output

เปิด `output.pptx` ด้วย Microsoft PowerPoint หรือโปรแกรมดูที่รองรับ คุณควรเห็นสไลด์หนึ่งที่แสดงช่วง `A1:H20` พร้อมสีเซลล์, เส้นขอบ, และรูปแบบ pivot table ชัดเจน สไลด์นี้สามารถแก้ไขได้ – คุณสามารถย้าย, ปรับขนาด, หรือจัดรูปแบบตารางได้เหมือนเนื้อหา PowerPoint ปกติ

## Full runnable example

การรวมขั้นตอนทั้งหมดจะได้คลาส Java ที่ทำงานได้เอง:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

เรียกใช้คลาสจาก IDE หรือผ่าน command line:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

คุณจะเห็นข้อความยืนยันเมื่อไฟล์ถูกเขียนสำเร็จ

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Can I copy a non‑contiguous range?** | ใช้ `copyRange` กับ named range ที่รวมหลายพื้นที่, หรือเรียก `copyRange` หลายครั้งสำหรับแต่ละบล็อก |
| **What if the source sheet contains multiple pivot tables?** | Pivot table ทั้งหมดที่อยู่ภายในสี่เหลี่ยมที่คัดลอกจะถูกถ่ายโอน; ตารางที่อยู่นอกสี่เหลี่ยมต้องคัดลอกแยกต่างหาก |
| **How do I export multiple sheets as separate slides?** | วนลูปผ่าน worksheets, คัดลอกแต่ละชีตไปยังชีตชั่วคราว, แล้วเรียก `workbook.save` ด้วย `pptOptions` ในแต่ละรอบ, เพิ่มสไลด์ใน PPTX เดียวผ่าน API ของ Presentation |
| **Is the generated PPTX editable?** | ใช่. การส่งออกสร้างอ็อบเจกต์ PowerPoint แบบเนทีฟ, คุณจึงสามารถแก้ไขข้อความ, ปรับรูปตาราง, หรือเพิ่มแอนิเมชันได้ |
| **What about large workbooks?** | เพิ่ม `pptOptions.setDpi(300)` เพื่อความคมชัดสูงขึ้น, แต่ต้องระวังการใช้หน่วยความจำ; ควรประมวลผลชีตเป็นชุดหากจำเป็น |

## Pro tips

* **Preserve column widths** – ตั้ง `CopyOptions.setColumnWidth(true)` ก่อนคัดลอกหากต้องการความกว้างคอลัมน์ที่ตรงกัน
* **Use a custom slide size** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` เพื่อให้ตรงกับพรีเซนเทชัน 16:9
* **Add a title slide** – หลังการส่งออก, เปิด PPTX ด้วย Aspose.Slides และเพิ่มสไลด์หัวเรื่องพร้อมวันที่

## Conclusion

คุณได้เรียนรู้ **how to copy range** จากเวิร์กบุ๊ก Excel, **export excel to PowerPoint**, และ **convert excel to pptx** ด้วย Java ด้วยหกขั้นตอนข้างต้น คุณสามารถอัตโนมัติการสร้างรายงาน, ทำสไลด์เด็คจากข้อมูลสด, และรักษาฟังก์ชันการทำงานของ pivot‑table ไว้ได้

### What’s next?

* สำรวจรูปแบบ **copy pivot table sheet** เช่นการคัดลอกเฉพาะ pivot cache
* ผสาน workflow นี้กับ **Aspose.Slides** เพื่อเพิ่มแอนิเมชันหรือแบรนด์ดิ้ง
* ทำการประมวลผลเป็นชุดสำหรับหลายสิบเวิร์กบุ๊กในงานที่กำหนดเวลา

ลองปรับแต่งตัวเลือกต่าง ๆ และนำโค้ดไปใช้ใน pipeline รายงานของคุณ หากพบปัญหา, เอกสาร Aspose.Cells for Java มีข้อมูลเชิงลึกเพิ่มเติมเกี่ยวกับ `CopyOptions` และ `ImageOrPrintOptions` ขอให้สนุกกับการเขียนโค้ด!

## What Should You Learn Next?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโปรเจกต์ของคุณ

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}