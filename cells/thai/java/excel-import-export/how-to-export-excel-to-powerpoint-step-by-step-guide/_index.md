---
category: general
date: 2026-08-04
description: วิธีส่งออก Excel ไปยัง PowerPoint อย่างรวดเร็ว เรียนรู้การแปลง Excel
  เป็น PPTX ตั้งค่าพื้นที่พิมพ์ และสร้างสไลด์ที่แก้ไขได้ด้วย Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- set print area excel
- create powerpoint from excel
- convert spreadsheet to ppt
language: th
lastmod: 2026-08-04
og_description: วิธีส่งออก Excel ไปยัง PowerPoint อย่างรวดเร็ว บทเรียนนี้แสดงวิธีแปลง
  Excel เป็น PPTX ตั้งค่าพื้นที่พิมพ์ และสร้างไฟล์ PowerPoint ที่สามารถแก้ไขได้โดยใช้
  Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet being transformed into a PowerPoint
  slide with editable shapes
og_title: วิธีส่งออก Excel ไปยัง PowerPoint – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to export Excel to PowerPoint quickly. Learn to convert Excel to
    PPTX, set print area, and create editable slides with Aspose.Cells.
  headline: How to export Excel to PowerPoint – step‑by‑step guide
  type: TechArticle
- description: How to export Excel to PowerPoint quickly. Learn to convert Excel to
    PPTX, set print area, and create editable slides with Aspose.Cells.
  name: How to export Excel to PowerPoint – step‑by‑step guide
  steps:
  - name: Load the workbook containing the data to export
    text: You must open the Excel file before any export options can be applied. Loading
      the workbook also validates that the file exists and is readable.
  - name: Set the print area in Excel before export
    text: Defining a print area tells Aspose.Cells which cells should appear on the
      slide. If you skip this, the entire worksheet may be rendered, leading to oversized
      slides.
  - name: Configure export options for PPTX
    text: Export options allow you to specify the target format and control how the
      sheet is translated into a slide. Here we request PPTX, which creates an editable
      PowerPoint file.
  - name: Save the first worksheet as an editable PowerPoint presentation
    text: Finally, invoke `save` with the PPTX format. The resulting file contains
      a single slide that mirrors the defined print area, and all shapes remain editable.
  type: HowTo
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
- Export
title: วิธีส่งออก Excel ไปยัง PowerPoint – คู่มือขั้นตอนโดยละเอียด
url: /th/java/excel-import-export/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออก Excel ไปยัง PowerPoint – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **วิธีส่งออก Excel** ไปยังงานนำเสนอ PowerPoint ที่สามารถแก้ไขได้ คู่มือนี้จะให้วิธีแก้ไขที่สมบูรณ์ คุณจะได้เห็นวิธีแปลง Excel เป็น PPTX การตั้งค่าพื้นที่พิมพ์ และการสร้างสไลด์เด็คที่สามารถแก้ไขโดยตรงใน PowerPoint

การส่งออกข้อมูลจากสเปรดชีตมักจะจบลงด้วยภาพคงที่ แต่ด้วย Aspose.Cells คุณสามารถคงรูปทรง ตาราง และการจัดรูปแบบข้อความไว้ได้ เมื่อจบการสอนนี้คุณจะมีไฟล์ `.pptx` ที่ทำงานเหมือนสไลด์ PowerPoint ดั้งเดิม พร้อมสำหรับการออกแบบต่อไป

## ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดใช้ Java API ของ Aspose.Cells)
- Aspose.Cells for Java 23.9 หรือใหม่กว่า (ดาวน์โหลดจาก [Aspose website](https://products.aspose.com/cells/java/))
- เวิร์กบุ๊กชื่อ `PresentationDemo.xlsx` ที่วางไว้ในไดเรกทอรีที่รู้จัก
- ความคุ้นเคยพื้นฐานกับการพัฒนา Java (IDE ใดก็ได้)

## วิธีส่งออก Excel – การอธิบายโค้ดเต็มขั้นตอน

ส่วนต่อไปนี้จะแบ่งกระบวนการออกเป็นขั้นตอนที่ชัดเจนและนำกลับมาใช้ใหม่ได้ แต่ละขั้นตอนอธิบาย **ทำไม** จึงสำคัญ ไม่ใช่แค่ **อะไร** ที่ต้องพิมพ์

### ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กที่มีข้อมูลที่จะส่งออก

คุณต้องเปิดไฟล์ Excel ก่อนที่จะใช้ตัวเลือกการส่งออกใด ๆ การโหลดเวิร์กบุ๊กยังเป็นการตรวจสอบว่ามีไฟล์อยู่และสามารถอ่านได้

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PresentationDemo.xlsx");
        // Proceed with export configuration...
```

*ทำไมต้องทำขั้นตอนนี้?*  
`Workbook` เป็นจุดเริ่มต้นของการทำงานทั้งหมดของ Aspose.Cells หากไม่มีคุณจะไม่สามารถเข้าถึงชีต, การตั้งค่าหน้า, หรือฟังก์ชันการส่งออกได้

### ขั้นตอนที่ 2: ตั้งค่าพื้นที่พิมพ์ใน Excel ก่อนการส่งออก

การกำหนดพื้นที่พิมพ์บอก Aspose.Cells ว่าเซลล์ใดบ้างที่ควรปรากฏบนสไลด์ หากข้ามขั้นตอนนี้ ชีตทั้งหมดอาจถูกเรนเดอร์ ทำให้สไลด์มีขนาดใหญ่เกินไป

```java
        // Define the printable range (A1 to H30)
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");
```

*ทำไมต้องทำขั้นตอนนี้?*  
`setPrintArea` ทำหน้าที่เหมือนฟีเจอร์ **ตั้งค่าพื้นที่พิมพ์ Excel** ของ Excel เพื่อให้แน่ใจว่าเฉพาะเซลล์ที่เลือกเท่านั้นที่แสดงในสไลด์ PowerPoint ซึ่งช่วยลดขนาดไฟล์และทำให้เลย์เอาต์เป็นระเบียบ

### ขั้นตอนที่ 3: กำหนดตัวเลือกการส่งออกสำหรับ PPTX

ตัวเลือกการส่งออกช่วยให้คุณระบุรูปแบบเป้าหมายและควบคุมวิธีการแปลงชีตเป็นสไลด์ ที่นี่เราขอ PPTX ซึ่งจะสร้างไฟล์ PowerPoint ที่แก้ไขได้

```java
        // Configure export options to generate a PPTX file
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*ทำไมต้องทำขั้นตอนนี้?*  
`ImageOrPrintOptions` รวมการตั้งค่าต่าง ๆ เช่น คุณภาพภาพ, การปรับสเกลหน้า, และคำสั่ง **แปลง Excel เป็น PPTX** การตั้งค่า `SaveFormat.PPTX` รับประกันว่าผลลัพธ์จะเป็นเด็ค PowerPoint ไม่ใช่ภาพคงที่

### ขั้นตอนที่ 4: บันทึกชีตแรกเป็นงานนำเสนอ PowerPoint ที่แก้ไขได้

สุดท้ายเรียก `save` ด้วยรูปแบบ PPTX ไฟล์ที่ได้จะมีสไลด์เดียวที่สะท้อนพื้นที่พิมพ์ที่กำหนดไว้ และรูปทรงทั้งหมดยังคงแก้ไขได้

```java
        // Export the first worksheet to an editable PowerPoint file
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);
    }
}
```

*ทำไมต้องทำขั้นตอนนี้?*  
`workbook.save` ทำการแปลงจริง ๆ เนื่องจากเราได้ตั้งค่าพื้นที่พิมพ์และตัวเลือกการส่งออกไว้ก่อนแล้ว สไลด์ที่สร้างจึงรักษาเลย์เอาต์ที่คุณออกแบบใน Excel ไฟล์ผลลัพธ์สามารถเปิดใน Microsoft PowerPoint เพื่อย้าย, ปรับขนาด, หรือเปลี่ยนสีรูปทรง — ตอบสนองความต้องการ **สร้าง PowerPoint จาก Excel** อย่างครบถ้วน

#### ผลลัพธ์ที่คาดหวัง

- ไฟล์ชื่อ `EditableShapes.pptx` ปรากฏใน `YOUR_DIRECTORY`
- เปิดไฟล์ใน PowerPoint จะเห็นสไลด์เดียวที่มีช่วง `A1:H30` จากเวิร์กบุ๊กต้นฉบับ
- กล่องข้อความ, แผนภูมิ, และรูปทรงทั้งหมดสามารถแก้ไขได้เต็มที่ เหมือนกับอ็อบเจ็กต์ PowerPoint ดั้งเดิม

## แปลง Excel เป็น PPTX – จัดการหลายชีต

หากคุณต้องการ **แปลงสเปรดชีตเป็น PPT** สำหรับมากกว่าหนึ่งชีต ให้ทำซ้ำขั้นตอนการส่งออกสำหรับแต่ละชีตและอาจรวมสไลด์เข้าด้วยกันเป็นงานนำเสนอเดียว

```java
        // Loop through all worksheets and add each as a separate slide
        for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
            Worksheet sheet = workbook.getWorksheets().get(i);
            sheet.getPageSetup().setPrintArea("A1:H30"); // adjust per sheet if needed
            // Save each sheet as an individual PPTX (or merge later)
            sheet.getPageSetup().setPrintArea("A1:H30");
            workbook.save("YOUR_DIRECTORY/Slide_" + (i + 1) + ".pptx", SaveFormat.PPTX);
        }
```

*เคล็ดลับ:* ใช้วัตถุ `Presentation` จาก Aspose.Slides หากต้องการรวมสไลด์ที่สร้างขึ้นเป็นเด็คเดียวโดยอัตโนมัติ

## ตั้งค่าพื้นที่พิมพ์ Excel – แนวทางปฏิบัติที่ดีที่สุด

- เลือกพื้นที่พิมพ์ที่ตรงกับเลย์เอาต์ที่ต้องการบนสไลด์  
- หลีกเลี่ยงการรวมเซลล์ที่ขยายออกนอกช่วงที่กำหนด เพราะอาจทำให้สเกลผิดพลาด  
- ทดสอบพื้นที่พิมพ์โดยพิมพ์เป็น PDF ก่อน; มุมมอง PDF จะสะท้อนผลลัพธ์ใน PowerPoint

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|----------|
| สไลด์เปล่า | ไม่ได้ตั้งค่าพื้นที่พิมพ์หรือตั้งค่าเป็นช่วงว่าง | ตรวจสอบว่า `setPrintArea` ชี้ไปที่เซลล์ที่มีข้อมูล |
| รูปทรงบิดเบี้ยว | ระดับการซูมของชีต > 100% | รีเซ็ตซูมเป็น 100% ก่อนส่งออก |
| ฟอนต์หาย | ฟอนต์ไม่ได้ติดตั้งบนเซิร์ฟเวอร์ | ฝังฟอนต์ที่ต้องการหรือใช้ฟอนต์ที่มีในระบบ |
| ไฟล์ขนาดใหญ่ | ส่งออกชีตทั้งหมด | จำกัดช่วงด้วย **ตั้งค่าพื้นที่พิมพ์ Excel** หรือแยกเป็นหลายสไลด์ |

## แปลง Excel เป็น PPTX – วิธีทางเลือกโดยใช้ Aspose.Slides

หากคุณใช้ Aspose.Slides อยู่แล้ว สามารถนำเข้า PPTX ที่สร้างโดย Aspose.Cells แล้วเพิ่มแอนิเมชัน, การเปลี่ยนสไลด์, หรือสไลด์เพิ่มเติม วิธีนี้แสดงให้เห็นถึงความยืดหยุ่นของกระบวนการ **แปลงสเปรดชีตเป็น PPT**  

```java
import com.aspose.slides.*;

Presentation pres = new Presentation("YOUR_DIRECTORY/EditableShapes.pptx");
// Add a title slide
ISlide titleSlide = pres.getSlides().addEmptySlide(pres.getSlideSize().getSize());
// Save the enhanced deck
pres.save("YOUR_DIRECTORY/FinalPresentation.pptx", SaveFormat.Pptx);
```

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีส่งออก Excel** ไปยังเด็ค PowerPoint ที่แก้ไขได้เต็มรูปแบบโดยใช้ Aspose.Cells for Java การสอนนี้ครอบคลุมกระบวนการ **แปลง Excel เป็น PPTX**, แสดงวิธี **ตั้งค่าพื้นที่พิมพ์ Excel** เพื่อควบคุมอย่างแม่นยำ, และสาธิตวิธี **สร้าง PowerPoint จาก Excel** อย่างรวดเร็ว ด้วยขั้นตอนเหล่านี้คุณสามารถอัตโนมัติการสร้างรายงาน, สร้างแดชบอร์ดแบบสไลด์, หรือทำให้การนำเสนอข้อมูลเป็นเรื่องง่ายขึ้น

**ขั้นตอนต่อไป**

- สำรวจ **แปลงสเปรดชีตเป็น PPT** สำหรับหลายชีตเพื่อสร้างเด็คหลายสไลด์  
- เพิ่มแผนภูมิ, ตาราง, หรือรูปภาพในแหล่งข้อมูล Excel แล้วสังเกตว่าปรากฏอย่างไรใน PowerPoint  
- ใช้ Aspose.Slides เพื่อเพิ่มแอนิเมชัน, การเปลี่ยนสไลด์, หรือโน้ตผู้พูดโดยอัตโนมัติ

ลองปรับพื้นที่พิมพ์, แนวตั้งของหน้า, และตัวเลือกการส่งออกต่าง ๆ เพื่อให้ได้ผลลัพธ์ที่ตรงกับความต้องการรายงานของคุณเอง ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}