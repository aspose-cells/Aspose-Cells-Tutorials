---
category: general
date: 2026-08-20
description: เรียนรู้วิธีตั้งพื้นที่พิมพ์ใน Excel แล้วส่งออก Excel ไปเป็น PPTX ด้วย
  Aspose.Cells คู่มือนี้จะพาคุณผ่านขั้นตอนการแปลงแผ่นงานเป็น PowerPoint และบันทึกเป็นไฟล์
  PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: th
lastmod: 2026-08-20
og_description: ตั้งค่าพื้นที่พิมพ์ใน Excel แล้วส่งออก Excel เป็น PPTX ด้วย Aspose.Cells
  ทำตามบทแนะนำขั้นตอนต่อขั้นตอนนี้เพื่อแปลงแผ่นงานเป็น PowerPoint และบันทึกเป็นไฟล์
  PPTX.
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: ตั้งค่าพื้นที่พิมพ์ใน Excel และส่งออกไปยัง PowerPoint – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: วิธีตั้งพื้นที่พิมพ์ใน Excel และส่งออกไปยัง PowerPoint
url: /th/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งพื้นที่พิมพ์ใน Excel และส่งออกเป็น PowerPoint

หากคุณต้องการ **set print area excel** ก่อนแชร์ข้อมูลในสไลด์เด็ค, บทเรียนนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด คุณจะได้เรียนรู้วิธีกำหนดพื้นที่พิมพ์, แล้ว **export excel to pptx** พร้อมคงกล่องข้อความให้แก้ไขได้, ทำให้ PowerPoint ที่ได้พร้อมสำหรับการแก้ไขต่อไป

เราจะใช้ Aspose.Cells for Java เพื่อ **convert worksheet to PowerPoint** และสุดท้าย **save worksheet as PowerPoint** ในรูปแบบ PPTX ไม่จำเป็นต้องใช้ไลบรารีเพิ่มเติมนอกจาก Aspose.Cells JAR เมื่อคุณอ่านจบบทเรียนนี้แล้ว คุณจะสามารถรันโค้ดบนสภาพแวดล้อมที่รองรับ Java ใดก็ได้และสร้างงานนำเสนอที่สะท้อนช่วง Excel ที่เลือกไว้

## Prerequisites

- Java Development Kit 17 หรือใหม่กว่า  
- Aspose.Cells for Java (ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการของ Aspose)  
- ไฟล์ Excel workbook ที่มีรูปทรง (shapes) ที่คุณต้องการให้แก้ไขได้ (เช่น `BookWithShapes.xlsx`)  

ตรวจสอบให้แน่ใจว่า Aspose.Cells JAR อยู่ใน classpath ของคุณ:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## Step 1: Set print area excel using Aspose.Cells

ขั้นตอนแรกคือการกำหนดช่วงที่ต้องการส่งออก การตั้งค่าพื้นที่พิมพ์จะจำกัดการแปลงให้เฉพาะเซลล์ที่คุณสนใจและช่วยเพิ่มประสิทธิภาพ

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**ทำไมจึงสำคัญ** – เมธอด `setPrintArea` บอก Aspose.Cells ว่าเซลล์ใดเป็นส่วนของหน้าที่พิมพ์ได้ เมื่อคุณ **export excel to pptx** หลังจากนั้น จะเรนเดอร์เฉพาะพื้นที่นี้เท่านั้น ทำให้ข้อมูลที่ไม่ต้องการไม่ปรากฏบนสไลด์

### Pro tip
หากต้องการช่วงแบบไดนามิก คุณสามารถคำนวณที่อยู่โดยโปรแกรมได้:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## Step 2: Export excel to pptx with editable text boxes

หลังจากกำหนดพื้นที่พิมพ์แล้ว ให้ตั้งค่า options สำหรับการส่งออก การเปิดใช้งาน `setExportEditableTextBoxes` จะทำให้ข้อความในรูปทรงคงเป็นฟิลด์ที่แก้ไขได้ใน PowerPoint

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**ทำไมจึงสำคัญ** – โดยค่าเริ่มต้น Aspose.Cells จะทำ rasterize กล่องข้อความ ทำให้กลายเป็นส่วนของภาพ การตั้งค่า `ExportEditableTextBoxes` เป็น `true` จะคงวัตถุ shape ดั้งเดิมไว้ ทำให้ผู้ใช้สามารถแก้ไขข้อความโดยตรงใน PowerPoint ได้

## Step 3: Convert worksheet to PowerPoint and save the file

ตอนนี้ทำการแปลงจริง ๆ เมธอด `Workbook.save` จะรับชื่อไฟล์เป้าหมายและ options ที่เตรียมไว้ก่อนหน้า

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

เมื่อโค้ดทำงานเสร็จ `SheetWithEditableShapes.pptx` จะมีสไลด์เดียวที่สะท้อนพื้นที่พิมพ์ที่กำหนด (`A1:G30`) ทั้งหมด shape รวมถึงกล่องข้อความจะยังคงแก้ไขได้

### Expected output
เปิดไฟล์ PPTX ที่สร้างขึ้นใน Microsoft PowerPoint:

- สไลด์จะแสดงเซลล์จาก **A1 ถึง G30** ตรงตามที่ปรากฏใน Excel  
- รูปทรงใด ๆ ที่อยู่ใน worksheet ดั้งเดิมจะปรากฏเป็น shape ของ PowerPoint  
- ข้อความภายใน shape เหล่านั้นสามารถแก้ไขได้โดยตรงใน PowerPoint (ไม่มีการ rasterization)

## Step 4: Full, runnable example

ด้านล่างเป็นโปรแกรมเต็มรูปแบบ แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริงบนเครื่องของคุณ

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

รันโปรแกรมตามที่อธิบายในส่วน *Prerequisites* ไฟล์ PowerPoint ที่สร้างจะถูกวางไว้ในไดเรกทอรีเดียวกันที่คุณระบุ

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Can I export multiple worksheets?** | ได้ คุณสามารถวนลูป `workbook.getWorksheets()` แล้วเรียก `save` สำหรับแต่ละชีต พร้อมปรับชื่อไฟล์ผลลัพธ์ตามต้องการ |
| **What if my workbook contains charts?** | โดยค่าเริ่มต้นแผนภูมิจะถูกเรนเดอร์เป็นภาพ หากต้องการให้แก้ไขได้คุณต้องแปลงเป็น shape ของ PowerPoint ด้วยตนเอง ซึ่งอยู่นอกขอบเขตของคู่มือนี้ |
| **Is the print area required?** | ไม่จำเป็น หากคุณละ `setPrintArea` Aspose.Cells จะส่งออกช่วงที่ใช้ทั้งหมดของ worksheet การตั้งค่าจะช่วยให้คุณควบคุมได้แม่นยำยิ่งขึ้น |
| **Does this work with .xlsx files created by other tools?** | แน่นอน Aspose.Cells รองรับ workbook รูปแบบ Office Open XML ใด ๆ ไม่ว่าจะสร้างจากเครื่องมือใดก็ตาม |

## Next steps

- **Save worksheet as PowerPoint** ด้วยเลย์เอาต์สไลด์ที่กำหนดเอง: สำรวจคลาส `Presentation` จาก Aspose.Slides เพื่อรวมสไลด์ที่ส่งออกเข้าเด็คที่ใหญ่ขึ้น  
- **Export excel to pptx** ด้วยความละเอียดภาพต่าง ๆ: ปรับ `exportOptions.setResolution(300)` เพื่อให้ได้ผลลัพธ์ DPI สูง  
- **Automate batch conversions**: ผสานโค้ดนี้กับ file‑watcher เพื่อประมวลผลไฟล์ Excel หลายไฟล์ในโฟลเดอร์เดียวกัน  

โดยการเชี่ยวชาญ **set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint**, และ **save worksheet as powerpoint** คุณจะสามารถรวมข้อมูล Excel เข้าไปในสไลด์เด็คได้โดยอัตโนมัติ ช่วยเร่งกระบวนการรายงานและลดงานคัดลอก‑วางด้วยตนเอง

---


## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}