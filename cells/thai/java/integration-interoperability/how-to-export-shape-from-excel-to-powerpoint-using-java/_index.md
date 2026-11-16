---
category: general
date: 2026-11-16
description: เรียนรู้วิธีส่งออกรูปร่างจาก Excel ไปยัง PowerPoint ด้วย Java, แปลงแผนภูมิ
  Excel เป็นไฟล์ PPTX และบันทึกรูปร่าง PPTX ด้วย Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: th
lastmod: 2026-11-16
og_description: วิธีส่งออกรูปร่างจาก Excel ไปยัง PowerPoint ด้วย Java. ทำตามบทเรียนเต็มนี้เพื่อแปลงแผนภูมิ
  Excel, บันทึกรูปร่างเป็นไฟล์ PPTX, และฝังรูปร่างลงในไฟล์ PowerPoint.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: วิธีส่งออกรูปร่างจาก Excel ไปยัง PowerPoint ด้วย Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: วิธีส่งออกรูปร่างจาก Excel ไปยัง PowerPoint ด้วย Java
url: /th/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออก shape จาก Excel ไปยัง PowerPoint ด้วย Java

หากคุณต้องการ **how to export shape** จากเวิร์กบุ๊ก Excel ไปยังสไลด์ PowerPoint คำแนะนำนี้จะแสดงขั้นตอนที่แน่นอน คุณจะได้เห็นวิธี **convert Excel chart** วัตถุ, แปลงเป็น **shape to PowerPoint**, และสุดท้าย **save shape PPTX** ด้วยตัวเลือกการส่งออกที่ถูกต้อง.

การส่งออก shape เป็นความต้องการทั่วไปเมื่อคุณสร้างรายงานโดยอัตโนมัติ เมื่อจบบทเรียนนี้คุณจะมีโปรแกรม Java ที่ทำงานอิสระซึ่งสร้างไฟล์ `shape.pptx` พร้อมสำหรับการนำเสนอ ไม่จำเป็นต้องใช้สคริปต์ภายนอก และโค้ดทำงานร่วมกับ Aspose.Cells 2024‑R2 หรือใหม่กว่า.

## ข้อกำหนดเบื้องต้น

* Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับ JDK 8+ ใดก็ได้)
* ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจากเว็บไซต์ Aspose หรือเพิ่ม dependency ของ Maven)
* ไฟล์ Excel (`chart.xls`) ที่มีอย่างน้อยหนึ่ง shape (เช่น chart, textbox, หรือ SmartArt)
* ความคุ้นเคยพื้นฐานกับการจัดการข้อยกเว้นใน Java

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## วิธีส่งออก shape จาก Excel ไปยัง PowerPoint (กระบวนการโดยรวม)

กระบวนการประกอบด้วยสี่ส่วนหลัก:

1. **Load the workbook** ที่มี shape อยู่  
2. **Locate the shape** บน worksheet แรก  
3. **Configure export options** เพื่อให้ shape กลายเป็นอ็อบเจ็กต์ PowerPoint ที่แก้ไขได้  
4. **Save the shape as a PPTX file**  

แต่ละส่วนจะอธิบายรายละเอียดด้านล่าง และโปรแกรมที่สามารถรันได้เต็มรูปแบบจะตามมาหลังจากคำอธิบาย

## ขั้นตอนที่ 1: โหลด workbook ที่มี shape

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*ทำไมต้องทำขั้นตอนนี้?*  
`Workbook` เป็นจุดเริ่มต้นสำหรับการทำงานทั้งหมดของ Aspose.Cells การโหลดไฟล์ทำให้คุณเข้าถึง worksheets, cells, และ collection ของ shape หากไม่พบไฟล์ Aspose.Cells จะโยน `FileNotFoundException` ซึ่งเราจะจับในภายหลัง.

## ขั้นตอนที่ 2: เข้าถึง worksheet แรกและดึง shape ที่ต้องการ

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*ทำไมต้องทำขั้นตอนนี้?*  
Worksheets ถูกจัดเก็บในคอลเลกชันที่เริ่มจากศูนย์ ดังนั้น `get(0)` จะคืนค่า worksheet แรก Shapes ก็เช่นกัน; `get(0)` จะดึง shape แรก ซึ่งมักจะเป็น chart ที่คุณต้องการส่งออก หาก workbook ของคุณมีหลาย shape คุณสามารถวนลูปคอลเลกชันหรือใช้ `shape.getName()` เพื่อเลือกเฉพาะที่ต้องการได้.

## ขั้นตอนที่ 3: เตรียม export options – เราต้องการ shape เป็นอ็อบเจ็กต์ PPTX ที่แก้ไขได้

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*ทำไมต้องทำขั้นตอนนี้?*  
`ImageOrPrintOptions` ควบคุมวิธีการเรนเดอร์ shape โดยการเลือก `SaveFormat.PPTX` ไลบรารีจะแปลงกราฟิกจาก Excel เป็น shape ของ PowerPoint ที่เป็นเวกเตอร์และยังคงแก้ไขได้หลังการนำเข้า สิ่งนี้สำคัญสำหรับการแปลง **shape to PowerPoint** ที่แท้จริง; การใช้ PNG หรือ JPEG จะทำให้กราฟิกเป็นภาพคงที่.

## ขั้นตอนที่ 4: ส่งออก shape ไปยังไฟล์ PowerPoint

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*ทำไมต้องทำขั้นตอนนี้?*  
เมธอด `save` จะเขียน shape ด้วยตัวเลือกที่กำหนดไว้ก่อนหน้านี้ ไฟล์ `shape.pptx` ที่ได้จะมีสไลด์เดียวที่แสดง shape เหมือนเดิมจาก Excel แต่ตอนนี้คุณสามารถแก้ไขใน PowerPoint (เปลี่ยนสี, ปรับขนาด, เพิ่มแอนิเมชัน ฯลฯ) ซึ่งสอดคล้องกับความต้องการ **save shape PPTX**.

## ตัวอย่างเต็มที่สามารถรันได้

คัดลอกคลาสทั้งหมดไปยังไฟล์ชื่อ `ExportShapeDemo.java` แทนที่ `YOUR_DIRECTORY` ด้วยพาธแบบ absolute หรือ relative แล้วรัน `javac ExportShapeDemo.java && java ExportShapeDemo`. หลังจากทำงานเสร็จคุณจะพบไฟล์ `shape.pptx` ในโฟลเดอร์เป้าหมาย.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

```
Export completed. File saved as shape.pptx
```

เปิด `shape.pptx` ด้วย Microsoft PowerPoint คุณจะเห็นสไลด์เดียวที่มี chart (หรือ textbox) ของ Excel ดั้งเดิมเป็น shape ของ PowerPoint ที่สามารถแก้ไขได้เต็มที่.

## ความแตกต่างทั่วไปและกรณีขอบ

| สถานการณ์ | การปรับแนะนำ |
|-----------|------------------------|
| **Multiple shapes** | Loop through `worksheet.getShapes()` and call `save` for each shape, or select by `shape.getName()`. |
| **Shape is a chart with data series** | Use `exportOptions.setExportChartAsEditable(true)` to keep series editable. |
| **Need a specific slide layout** | After saving, open the PPTX with Aspose.Slides and insert the shape into a custom layout. |
| **Large workbook** | Load only the required worksheet using `Workbook(String, LoadOptions)` to reduce memory consumption. |
| **Different output format (PDF, PNG)** | Change `exportOptions.setSaveFormat(SaveFormat.PDF)` or `SaveFormat.PNG`. This is useful when you **convert Excel chart** to a static image instead of a PowerPoint shape. |

**เคล็ดลับ:** ตรวจสอบเสมอว่า index ของ shape (`get(0)`) ตรงกับองค์ประกอบที่คุณต้องการส่งออก คอลเลกชันของ shape จะเรียงตามลำดับการแทรกใน Excel ซึ่งอาจแตกต่างจากลำดับการซ้อนกันของภาพ.

## วิธีส่งออก shape จาก Excel ไปยัง PowerPoint – รายการตรวจสอบการแก้ไขปัญหา

* **File not found** – ตรวจสอบให้แน่ใจว่า path ใน `new Workbook()` ชี้ไปยังไฟล์ `.xls` หรือ `.xlsx` ที่มีอยู่  
* **No shapes returned** – ยืนยันว่า worksheet มี shape จริง ๆ; คุณสามารถเรียก `worksheet.getShapes().getCount()` เพื่อตรวจสอบ  
* **Exported file is empty** – ตรวจสอบว่าได้ตั้งค่า `exportOptions.setSaveFormat(SaveFormat.PPTX)`; การใช้รูปแบบภาพจะทำให้ได้ภาพแทน shape  
* **Compatibility issues** – Aspose.Cells 24.9+ รองรับการส่งออก PPTX บนแพลตฟอร์มหลักทั้งหมด อัปเกรดหากพบ `UnsupportedOperationException`

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to export shape** จากเวิร์กบุ๊ก Excel และฝังลงในงานนำเสนอ PowerPoint ด้วย Java บทเรียนได้อธิบายการโหลด workbook, การค้นหา shape, การกำหนดค่าตัวเลือก **export shape from Excel**, และสุดท้าย **save shape PPTX** ด้วยพื้นฐานนี้คุณสามารถอัตโนมัติการสร้างรายงาน, สร้างแดชบอร์ด, หรือรวมภาพจาก Excel ลงในสไลด์โดยไม่ต้องคัดลอก‑วางด้วยมือ.

### ขั้นตอนต่อไป

* สำรวจ **convert Excel chart** ไปยังรูปแบบ Office อื่น ๆ เช่น PDF หรือ DOCX.  
* ผสานเทคนิคนี้กับ Aspose.Slides เพื่อวางหลาย shape บนสไลด์เดียว.  
* ทดลองคุณสมบัติของ `ImageOrPrintOptions` (เช่น `setResolution`, `setTransparent`) เพื่อปรับคุณภาพภาพของ shape ที่ส่งออกให้ละเอียดขึ้น.

คุณสามารถปรับโค้ดสำหรับการประมวลผลเป็นชุดหรือผสานเข้ากับบริการรายงานขนาดใหญ่ได้ตามต้องการ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานได้ครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ.

- [วิธีส่งออก shape ด้วย ShapeExportOptions ใน Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [วิธีส่งออกแผ่นงาน Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint – คู่มือ Java ฉบับเต็ม](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}