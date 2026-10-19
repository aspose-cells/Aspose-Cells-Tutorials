---
category: general
date: 2026-09-11
description: สร้างแผ่นงานใหม่และคัดลอกช่วงของ Excel ด้วย Aspose.Cells เรียนรู้วิธีคัดลอกช่วงระหว่างแผ่นงานพร้อมคงรักษาตาราง
  Pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: th
lastmod: 2026-09-11
og_description: สร้างแผ่นงานใหม่และคัดลอกช่วง Excel ด้วย Aspose.Cells บทเรียนนี้แสดงขั้นตอนที่แน่นอนในการคัดลอกช่วงระหว่างแผ่นงานและรักษาตาราง
  Pivot ไว้ไม่เปลี่ยนแปลง
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: สร้างแผ่นงานใหม่และคัดลอกช่วง Excel – คู่มือ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: สร้างแผ่นงานใหม่และคัดลอกช่วงของ Excel ด้วย Aspose.Cells
url: /th/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผ่นงานใหม่และคัดลอกช่วง Excel ด้วย Aspose.Cells

หากคุณต้องการ **สร้างแผ่นงานใหม่** และย้ายข้อมูลภายในไฟล์ Excel, Aspose.Cells ทำให้ขั้นตอนนี้ง่ายดาย คู่มือนี้จะแสดงวิธีคัดลอกช่วง Excel จากแผ่นหนึ่งไปยังอีกแผ่นหนึ่งโดยคงไว้ซึ่ง Pivot Table ใด ๆ ที่อยู่ในช่วงนั้น

คุณจะได้เรียนรู้วิธี **คัดลอกช่วง Excel**, วิธี **คัดลอกช่วงระหว่างแผ่น**, และทำไมเมธอด `copy` ของ Aspose.Cells จึงรักษาการกำหนด Pivot Table ไว้ครบถ้วน ไม่ต้องใช้เครื่องมือภายนอก—เพียงโครงการ Java ที่มีไลบรารี Aspose.Cells

## ข้อกำหนดเบื้องต้น

ก่อนเริ่ม, โปรดตรวจสอบว่าคุณมี:

- Java 17 หรือใหม่กว่า
- Aspose.Cells for Java (เวอร์ชัน 23.12 หรือใหม่กว่า) ที่เพิ่มใน classpath ของโครงการ
- เวิร์กบุ๊กต้นทาง (`input.xlsx`) ที่มี Pivot Table อยู่ในช่วงที่คุณต้องการคัดลอก
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และการจัดการ dependency ด้วย Maven/Gradle

## ขั้นตอนที่ 1: ตั้งค่าโครงการและนำเข้า Aspose.Cells

สร้างโครงการ Maven ง่าย ๆ (หรือ Gradle หากคุณต้องการ) แล้วเพิ่ม dependency ของ Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

จากนั้นนำเข้าคลาสที่จำเป็นในไฟล์ Java ของคุณ:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*ทำไมขั้นตอนนี้สำคัญ*: การนำเข้าคลาสที่ถูกต้องทำให้คุณเข้าถึง `Workbook`, `Worksheet`, `Range` และเมธอด `copy` ที่จะจัดการการถ่ายโอนช่วงให้ได้

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กต้นทาง

เปิดเวิร์กบุ๊กที่มีข้อมูลที่คุณต้องการคัดลอก โค้ดต่อไปนี้จะโหลด `input.xlsx` จากโฟลเดอร์ที่คุณระบุ:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*คำอธิบาย*: `Workbook` แทนไฟล์ Excel ทั้งไฟล์ การโหลดครั้งเดียวทำให้คุณสามารถอ่าน/เขียนทุกแผ่นและคอลเลกชันของเซลล์ได้

## ขั้นตอนที่ 3: ระบุช่วงต้นทางที่รวม Pivot Table

เลือกแผ่นงานที่มี Pivot Table และกำหนดบล็อกเซลล์ที่ต้องการคัดลอก ในตัวอย่างนี้เราจะคัดลอกเซลล์ A1 ถึง D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*ทำไมขั้นตอนนี้สำคัญ*: การสร้างอ็อบเจ็กต์ `Range` ทำให้ Aspose.Cells รู้ว่าต้องคัดลอกเซลล์ใด (รวมถึงอ็อบเจ็กต์ฝังเช่น Pivot Table) อย่างชัดเจน

## ขั้นตอนที่ 4: **สร้างแผ่นงานใหม่** ที่จะรับข้อมูลที่คัดลอก

ตอนนี้เราจะเพิ่มแผ่นงานใหม่ในเวิร์กบุ๊กเดียวกัน นี่คือจุดที่คีย์เวิร์ดหลักปรากฏ:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*คำอธิบาย*: การเพิ่มแผ่นงานใหม่ทำให้ข้อมูลที่คัดลอกแยกออกจากแผ่นเดิม ช่วยให้ตรวจสอบการทำงานของ **copy excel range** ได้ง่ายโดยไม่กระทบแผ่นต้นฉบับ

## ขั้นตอนที่ 5: คัดลอกช่วง – Pivot Table จะถูกเก็บไว้โดยอัตโนมัติ

ใช้เมธอด `copy` เพื่อย้ายช่วงจากแผ่นต้นทางไปยังแผ่นปลายทาง Aspose.Cells จะคัดลอกสูตร, การจัดรูปแบบ, และการกำหนด Pivot Table:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*ทำไมวิธีนี้ได้ผล*: เมธอด `copy` ทำการคัดลอกเชิงลึกของเซลล์ต้นทาง ไม่ได้คัดลอกแค่ค่าเท่านั้น แต่จำลองโครงสร้างเซลล์ทั้งหมดรวมถึง Pivot Cache ด้วย นี่คือเหตุผลที่คุณสามารถ **copy range aspose.cells** แล้วยังเห็น Pivot Table ทำงานบนแผ่นใหม่ได้

## ขั้นตอนที่ 6: บันทึกเวิร์กบุ๊กพร้อมแผ่นงานใหม่

สุดท้าย, เขียนเวิร์กบุ๊กที่แก้ไขแล้วลงดิสก์:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*ผลลัพธ์*: `output.xlsx` ตอนนี้มีแผ่นเดิมบวกกับแผ่นใหม่ชื่อ **Copy** ที่บรรจุช่วงเดียวกันรวมถึง Pivot Table

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกส่วนเข้าด้วยกัน นี่คือโปรแกรมที่สมบูรณ์และสามารถรันได้:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง**: เปิด `output.xlsx` ใน Excel คุณจะเห็นแผ่นชื่อ **Copy** ที่เซลล์ A1:D20 มีข้อมูล, การจัดรูปแบบ, และ Pivot Table ที่ทำงานเหมือนต้นฉบับ

## คำถามที่พบบ่อยและกรณีขอบ

- **ถ้าช่วงต้นทางมีเซลล์ที่รวมกัน (merged cells) จะทำอย่างไร?**  
  เมธอด `copy` จะคัดลอกข้อมูลการรวมเซลล์ด้วย ดังนั้นเซลล์ที่รวมกันจะปรากฏเหมือนเดิมบนแผ่นปลายทาง

- **ฉันสามารถคัดลอกไปยังเวิร์กบุ๊กอื่นได้หรือไม่?**  
  ได้ โหลดอินสแตนซ์ `Workbook` ตัวที่สอง, สร้างช่วงปลายทางในเวิร์กบุ๊กนั้น, แล้วเรียก `sourceRange.copy(destinationRange)` เมธอดจะจัดการการคัดลอกข้ามเวิร์กบุ๊กโดยอัตโนมัติ

- **ถ้าแผ่นปลายทางมีข้อมูลอยู่แล้วจะเกิดอะไรขึ้น?**  
  การคัดลอกจะเขียนทับเซลล์ที่ทับกันกับช่วงปลายทาง เพื่อหลีกเลี่ยงการสูญเสียข้อมูล ให้ตรวจสอบให้แน่ใจว่าพื้นที่ปลายทางว่างหรือใช้เซลล์เริ่มต้นอื่น (เช่น `"B2"`)

- **Pivot Cache ถูกทำสำเนาไหม?**  
  Aspose.Cells ใช้ Pivot Cache เดิม ซึ่งหมายความว่า Pivot Table ใหม่ยังเชื่อมโยงกับข้อมูลต้นทางเดียวกัน หากต้องการ Cache แยกคุณต้องสร้าง Pivot Table ใหม่หลังการคัดลอก

## เคล็ดลับและแนวทางปฏิบัติที่ดีที่สุด

- **Pro tip**: ใช้ `Workbook.setForceFormulaRecalculation(true)` ก่อนบันทึก หากช่วงของคุณมีสูตรที่อ้างอิงข้อมูลนอกบล็อกที่คัดลอก
- **ระวัง** ช่วงขนาดใหญ่: การคัดลอกแผ่นงานขนาดมหาศาลอาจใช้หน่วยความจำมาก พิจารณาคัดลอกเป็นชิ้นย่อยหากเจอ `OutOfMemoryError`
- **Performance tip**: ปิดการอัปเดตหน้าจอ (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) เมื่อต้องทำงานกับไฟล์ขนาดใหญ่มาก เพื่อเร่งกระบวนการคัดลอก

## สรุป

คุณได้เรียนรู้วิธี **สร้างแผ่นงานใหม่** และ **คัดลอกช่วง Excel** ระหว่างแผ่นด้วย Aspose.Cells โดยคง Pivot Table และคุณลักษณะของเซลล์ทั้งหมดไว้ เทคนิคนี้ช่วยให้คุณทำสำเนาบล็อกข้อมูลแบบอัตโนมัติ, สร้างเทมเพลตรายงาน, หรือจัดโครงสร้างเวิร์กบุ๊กใหม่โดยไม่ต้องคัดลอก‑วางด้วยมือ

ต่อไป, สำรวจหัวข้อที่เกี่ยวข้องเช่น **copy range aspose.cells** สำหรับการทำงานข้ามเวิร์กบุ๊ก, การอัตโนมัติการรีเฟรช Pivot Table, หรือการส่งออกแผ่นที่คัดลอกเป็น PDF ทดลองใช้ช่วงต้นทางและชื่อแผ่นต่าง ๆ เพื่อให้เหมาะกับสถานการณ์อัตโนมัติของคุณเอง ขอให้เขียนโค้ดสนุก!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโครงการของคุณ

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}