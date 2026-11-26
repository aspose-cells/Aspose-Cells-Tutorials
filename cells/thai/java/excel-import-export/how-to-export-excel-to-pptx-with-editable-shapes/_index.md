---
category: general
date: 2026-11-25
description: เรียนรู้วิธีส่งออก Excel ไปเป็น PPTX พร้อมรูปทรงที่แก้ไขได้ คู่มือนี้ยังแสดงวิธีตั้งค่าพื้นที่พิมพ์และแปลงแผนภูมิ
  Excel สำหรับการนำเสนอ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: th
lastmod: 2026-11-25
og_description: วิธีส่งออก Excel ไปเป็น PPTX พร้อมรูปทรงที่แก้ไขได้โดยใช้ Aspose.Cells
  พร้อมเคล็ดลับการตั้งค่าพื้นที่พิมพ์และแปลงแผนภูมิ Excel สำหรับการนำเสนอ.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: วิธีส่งออก Excel ไปยัง PPTX พร้อมรูปทรงที่แก้ไขได้
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: วิธีส่งออก Excel ไปยัง PPTX พร้อมรูปทรงที่แก้ไขได้
url: /th/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออก Excel ไปเป็น PPTX พร้อมรูปร่างที่แก้ไขได้

หากคุณต้องการ **วิธีส่งออก Excel** ไปยัง PowerPoint พร้อมคงไว้ซึ่งกล่องข้อความและรูปร่างที่แก้ไขได้ คู่มือนี้จะพาคุณผ่านกระบวนการทั้งหมด คุณจะได้เรียนรู้วิธี **ตั้งค่าพื้นที่พิมพ์** เพื่อสร้างสไลด์ที่เน้นข้อมูลที่ต้องการและวิธี **แปลงวัตถุแผนภูมิ Excel** ให้ยังคงแก้ไขได้หลังการส่งออก

การส่งออก Excel ไปเป็น PPTX เป็นเรื่องทั่วไปเมื่อสร้างชุดงานนำเสนอจากรายงานที่ขับเคลื่อนด้วยข้อมูล ด้วยการใช้ Aspose.Cells for Java คุณจะหลีกเลี่ยงการคัดลอก‑วางด้วยตนเอง รักษาการจัดรูปแบบให้คงเดิม และได้การควบคุมเชิงโปรแกรมต่อผลลัพธ์

## สิ่งที่คุณจะได้เรียนรู้

* โหลดไฟล์ XLSX ที่มีกล่องข้อความหรือแผนภูมิอยู่  
* กำหนดตัวเลือกการส่งออกเพื่อให้ไฟล์ PPTX ที่ได้มี **รูปร่างที่แก้ไขได้**  
* **ตั้งค่าพื้นที่พิมพ์** เพื่อจำกัดช่วงที่ส่งออกให้ตรงกับเซลล์ที่ต้องการ  
* บันทึกแผ่นงานเป็นไฟล์ PPTX และตรวจสอบว่ากล่องข้อความและแผนภูมิสามารถแก้ไขใน PowerPoint ได้  

**ข้อกำหนดเบื้องต้น**

* Java 17 หรือใหม่กว่า  
* Maven หรือ Gradle สำหรับการจัดการ dependencies  
* ความเข้าใจพื้นฐานเกี่ยวกับเวิร์กบุ๊กของ Excel และการเขียนโปรแกรมด้วย Java  

---

## วิธีส่งออก Excel ไปเป็น PPTX พร้อมรูปร่างที่แก้ไขได้

ส่วนนี้ให้โค้ดหลักที่ทำการส่งออก ตัวอย่างใช้ Aspose.Cells 23.9 (รุ่นล่าสุด ณ เวลาที่เขียน) และแสดงขั้นตอนที่จำเป็นทั้งหมด

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### ทำไมแต่ละบรรทัดจึงสำคัญ

1. **Dependency** – Aspose.Cells มีคลาส `ImageOrPrintOptions` ที่สามารถเรนเดอร์แผ่นงานเป็นสไลด์ PPTX การเพิ่มผ่าน Maven ทำให้ไลบรารีอยู่ใน classpath  
2. **Imports** – การนำเข้าคลาสที่ถูกต้องทำให้โค้ดสะอาดและหลีกเลี่ยงการใช้ชื่อเต็มของคลาส  
3. **Loading the workbook** – ต้องระบุไฟล์ที่มีวัตถุที่ต้องการส่งออกอย่างแม่นยำ พาธอาจเป็นแบบ absolute หรือ relative จากโฟลเดอร์รากของโปรเจกต์  
4. **Export options** – การตั้งค่า `setEditable(true)` คือกุญแจสำคัญของ **วิธีส่งออก Excel** เพื่อให้รูปร่างใน PowerPoint คงเป็นแบบแก้ไขได้ หากไม่ตั้งค่านี้ กล่องข้อความจะกลายเป็นภาพคงที่  
5. **Print area** – คำสั่ง `setPrintArea` จำกัดการส่งออกให้เฉพาะพื้นที่ที่ต้องการ ซึ่งช่วยลดขนาดไฟล์และตัดแถว/คอลัมน์ที่ไม่ต้องการออก นี่เป็นการตอบสนองต่อความต้องการ **ตั้งค่าพื้นที่พิมพ์ excel**  
6. **Saving** – ค่าคงที่ `SaveFormat.PPTX` บอก Aspose.Cells ให้สร้างไฟล์ PowerPoint แทนการสร้างภาพหรือ PDF  

#### ผลลัพธ์ที่คาดหวัง

หลังจากรันโปรแกรม เปิดไฟล์ `EditableShapes.pptx` ใน PowerPoint คุณควรเห็นสไลด์ที่สะท้อนช่วง Excel ที่เลือก และกล่องข้อความหรือคำอธิบายแผนภูมิใด ๆ สามารถดับเบิล‑คลิกเพื่อแก้ไขได้เหมือนวัตถุ PowerPoint ดั้งเดิม  

---

## การตั้งค่าพื้นที่พิมพ์ใน Excel

เมื่อคุณต้องการส่งออกเพียงส่วนย่อยของแผ่นงาน การกำหนด **พื้นที่พิมพ์** จะช่วยเพิ่มประสิทธิภาพและความชัดเจนของภาพ

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*เคล็ดลับ:* หากคุณเปลี่ยนช่วงข้อมูลภายหลัง ให้เรียก `setPrintArea` อีกครั้งก่อนทำการส่งออก โปรแกรมจะใช้ค่าที่ตั้งล่าสุด

---

## การแปลงแผนภูมิ XLSX ให้เป็นแผนภูมิ PowerPoint ที่แก้ไขได้

Aspose.Cells ถือแผนภูมิเป็นวัตถุการวาด การเปิดใช้งาน `setEditable(true)` ทำให้แผนภูมิถูกแปลงเป็นแผนภูมิ PowerPoint ดั้งเดิมที่สามารถแก้ไขได้ (เช่น เปลี่ยนซีรีส์หรือชื่อแกน)

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

หากคุณต้องการ **วิธีแปลง xlsx** ที่มีหลายแผนภูมิ ให้ทำการส่งออกซ้ำสำหรับแต่ละแผ่นงาน หรือใช้ `Workbook.save` พร้อม `SaveFormat.PPTX` หลังจากสลับแผ่นงานที่ต้องการเป็นแอคทีฟ

---

## วิธีแปลง XLSX ด้วยโปรแกรม (โบนัส)

นอกจาก PPTX แล้ว คุณอาจต้องการแปลงเวิร์กบุ๊กเป็นรูปแบบอื่นเช่น PDF หรือ PNG คลาส `ImageOrPrintOptions` เดียวกันทำงานได้กับเป้าหมายเหล่านั้นเช่นกัน:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

นี่แสดงถึงความสามารถ **วิธีแปลง xlsx** ที่กว้างขวางของ Aspose.Cells  

---

## ข้อผิดพลาดทั่วไปและเคล็ดลับปฏิบัติที่ดีที่สุด

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| รูปร่างกลายเป็นภาพ | `setEditable(false)` (ค่าเริ่มต้น) | เรียก `exportOptions.setEditable(true)` |
| สไลด์ที่ส่งออกเป็นค่าว่าง | พื้นที่พิมพ์ไม่ได้รวมข้อมูลใด ๆ | ตรวจสอบสตริงช่วงที่ส่งให้ `setPrintArea` |
| แผนภูมิสูญเสียการจัดรูปแบบ | ใช้ Aspose.Cells เวอร์ชันเก่า | อัปเกรดเป็นไลบรารีล่าสุด (≥ 23.9) |
| ขนาดไฟล์ใหญ่ | ส่งออกทั้งแผ่นงาน | จำกัดพื้นที่พิมพ์หรือซ่อนแถว/คอลัมน์ที่ไม่ได้ใช้ |

---

## สรุป

คุณได้เรียนรู้ **วิธีส่งออก Excel** ไปเป็น PPTX พร้อมรูปร่างและแผนภูมิที่แก้ไขได้เต็มรูปแบบ วิธี **ตั้งค่าพื้นที่พิมพ์** เพื่อโฟกัสผลลัพธ์ และวิธี **แปลงวัตถุแผนภูมิ Excel** เพื่อให้การแก้ไขในงานนำเสนอเป็นไปอย่างราบรื่น ตัวอย่าง Java ที่ทำงานได้เต็มรูปแบบด้านบนสามารถนำไปใส่ในโปรเจกต์ใด ๆ ที่ใช้ Aspose.Cells อยู่แล้ว  

**ขั้นตอนต่อไป**

* สำรวจตัวเลือก **แปลงแผนภูมิ Excel** ใน PowerPoint (เช่น การเปลี่ยนประเภทแผนภูมิ)  
* ผสานการส่งออกนี้กับการ **ตั้งค่าพื้นที่พิมพ์ excel** แบบอัตโนมัติเพื่อสร้างหลายสไลด์จากเวิร์กบุ๊กเดียว  
* ทดลองส่งออกเป็นรูปแบบอื่น (PDF, PNG) ด้วยรูปแบบ `ImageOrPrintOptions` เดียวกัน  

ลองเล่นกับช่วงต่าง ๆ, แผ่นงานหลายแผ่น, หรือเลย์เอาต์สไลด์ที่กำหนดเองได้เลย ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่อธิบายในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to set print area excel and export to PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Convert Excel to PowerPoint and set print area](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}