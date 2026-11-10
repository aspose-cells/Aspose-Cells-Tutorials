---
category: general
date: 2026-09-08
description: เรียนรู้วิธีส่งออก Excel ไปยัง PowerPoint ด้วย Java และ Aspose.Cells
  พร้อมคงไว้ซึ่งกล่องข้อความที่สามารถแก้ไขได้ในไฟล์ PPTX ที่ส่งออก
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- Aspose.Cells Java
- editable text boxes
- ImageOrPrintOptions
- Workbook save
- PowerPoint PPTX export
language: th
lastmod: 2026-09-08
og_description: ส่งออก Excel ไปยัง PowerPoint ด้วย Java โดยใช้ Aspose.Cells คู่มือนี้จะแสดงวิธีทำให้ข้อความในแผนภูมิสามารถแก้ไขได้และสร้างไฟล์
  PPTX ภายในไม่กี่นาที
og_image_alt: Screenshot of Java code exporting an Excel worksheet to a PowerPoint
  slide
og_title: ส่งออก Excel ไปยัง PowerPoint ด้วย Java – คู่มือแบบขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to export Excel to PowerPoint using Java and Aspose.Cells,
    preserving editable text boxes in the PPTX output.
  headline: How to export Excel to PowerPoint with Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
title: วิธีส่งออก Excel ไปยัง PowerPoint ด้วย Java
url: /th/java/excel-import-export/how-to-export-excel-to-powerpoint-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออก Excel ไปยัง PowerPoint ด้วย Java

หากคุณต้องการ **export Excel to PowerPoint** บทแนะนำนี้จะแสดงวิธีแก้ปัญหา Java ที่สะอาดตา โดยใช้ **Aspose.Cells Java** คุณสามารถคงรูปแบบของแผนภูมิและเปิดใช้งาน **editable text boxes** ในไฟล์ PPTX ที่สร้างขึ้น

การส่งออกสเปรดชีตไปยังงานนำเสนอเป็นความต้องการทั่วไปเมื่อคุณต้องการใช้แผนภูมิที่ขับเคลื่อนด้วยข้อมูลซ้ำในสไลด์เด็ค ในคู่มือนี้คุณจะได้เรียนรู้วิธี:

* โหลดเวิร์กบุ๊ก Excel ที่มีแผนภูมิอยู่แล้ว
* กำหนดค่า **ImageOrPrintOptions** เพื่อให้สไลด์ที่ส่งออกเก็บกล่องข้อความที่แก้ไขได้
* บันทึกเวิร์กชีตเป็นไฟล์ **PowerPoint PPTX** ด้วยการเรียกเมธอดเดียว
* รันตัวอย่างที่สมบูรณ์และเป็นอิสระที่คุณสามารถคัดลอกไปใช้ในโปรเจกต์ของคุณได้

ข้อกำหนดเบื้องต้นเพียงอย่างเดียวคือ Java 8 (หรือใหม่กว่า) runtime และไลเซนส์ Aspose.Cells for Java ที่ถูกต้อง หากคุณใช้เวอร์ชันประเมินผลฟรี ผลลัพธ์จะมีลายน้ำ แต่โค้ดยังคงทำงานเช่นเดียวกัน

---

## Export Excel to PowerPoint – ตั้งค่าสภาพแวดล้อมการพัฒนา

ก่อนเขียนโค้ด ให้ตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

| รายการ | เหตุผล |
|------|--------|
| **Java Development Kit (JDK) 8+** | จำเป็นสำหรับคอมไพล์และรันตัวอย่าง |
| **Aspose.Cells for Java** library | ให้คลาส `Workbook`, `ImageOrPrintOptions` และ `SaveFormat` ที่ใช้สำหรับการแปลง |
| **ไลเซนส์ Aspose.Cells ที่ถูกต้อง** (ไม่บังคับ) | ลบลายน้ำการประเมินและเปิดใช้งานฟังก์ชันเต็ม |
| **ไฟล์ Excel (`chartSheet.xlsx`)** ที่มีอย่างน้อยหนึ่งแผนภูมิ | เวิร์กบุ๊กต้นทางที่คุณจะส่งออก |

เพิ่มไฟล์ JAR ของ Aspose.Cells ไปยัง classpath ของโปรเจกต์ หากคุณใช้ Maven ให้เพิ่ม dependency:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

---

## กำหนดค่า ImageOrPrintOptions สำหรับกล่องข้อความที่แก้ไขได้

คลาส `ImageOrPrintOptions` ควบคุมวิธีการเรนเดอร์เวิร์กชีตเมื่อทำการส่งออก การตั้งค่า `setExportEditableTextBox(true)` บอก Aspose.Cells ให้เก็บองค์ประกอบข้อความภายในแผนภูมิเป็น **editable text boxes** ใน PowerPoint แทนการแปลงเป็นภาพคงที่

```java
// Create export options for PowerPoint
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);          // Target format is PPTX
exportOptions.setExportEditableTextBox(true);        // Keep chart text editable
```

ทำไมจึงสำคัญ: เมื่อคุณเปิดไฟล์ PPTX ใน PowerPoint ต่อไป คุณสามารถคลิกที่ป้ายกำกับของแผนภูมิและแก้ไขเนื้อหาโดยตรง ซึ่งจำเป็นสำหรับการนำเสนอที่ต้องการการปรับเปลี่ยนแบบทันที

---

## โหลดเวิร์กบุ๊กและส่งออกเป็นไฟล์ PPTX

ตอนนี้ให้โหลดไฟล์ Excel ใช้ตัวเลือกจากขั้นตอนก่อนหน้า และเรียก `save` เมธอด `Workbook.save` รับพาธเอาต์พุตและอินสแตนซ์ `ImageOrPrintOptions` ทำการแปลงภายใน

```java
// Load the workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

// Export the first worksheet to PowerPoint using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);
```

**ประเด็นสำคัญ**

* `Workbook` แทนไฟล์ Excel ทั้งไฟล์ คุณยังสามารถเลือกชีตเฉพาะด้วย `workbook.getWorksheets().get(0)` หากต้องการส่งออกเฉพาะชีตเดียว
* เมธอด `save` จะเขียนไฟล์ PPTX ที่มีหนึ่งสไลด์ต่อเวิร์กชีตโดยค่าเริ่มต้น
* หากเวิร์กบุ๊กของคุณมีหลายชีตและคุณต้องการแค่ชีตแผนภูมิ ให้ลบชีตที่ไม่ต้องการก่อนบันทึก หรือใช้ `ExportOptions.setOnePagePerSheet(false)` เพื่อควบคุมการแบ่งหน้า

---

## ตัวอย่างที่สามารถรันได้อย่างสมบูรณ์

ด้านล่างเป็นโปรแกรม Java ขั้นต่ำที่สามารถรันได้เต็มรูปแบบซึ่งสาธิตกระบวนการทั้งหมด แทนที่ `YOUR_DIRECTORY` ด้วยพาธแบบเต็มหรือแบบสัมพันธ์ที่ชี้ไปยังไฟล์ของคุณ

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook that holds the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

            // 2. Prepare export options for PowerPoint and enable editable text boxes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
            exportOptions.setExportEditableTextBox(true);        // Keep text boxes editable

            // 3. Export the worksheet(s) to a PPTX file
            workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);

            System.out.println("Export completed successfully. Check output.pptx.");
        } catch (Exception e) {
            System.err.println("Error during export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

เมื่อรันโปรแกรมจะพิมพ์:

```
Export completed successfully. Check output.pptx.
```

เมื่อคุณเปิด `output.pptx` ใน Microsoft PowerPoint คุณจะเห็นสไลด์ที่สะท้อนแผนภูมิจาก Excel ดับเบิล‑คลิกที่ป้ายกำกับของแผนภูมิใดก็ได้ คุณสามารถแก้ไขข้อความโดยตรง ยืนยันว่า **editable text boxes** ทำงานอยู่

---

## การจัดการกับความแตกต่างและกรณีขอบต่าง ๆ

| สถานการณ์ | วิธีการแนะนำ |
|-----------|----------------------|
| **หลายเวิร์กชีต** แต่ต้องการส่งออกเฉพาะชีตแผนภูมิหนึ่งชีต | ใช้ `workbook.getWorksheets().removeAt(index)` เพื่อลบชีตที่ไม่ต้องการก่อนเรียก `save` หรือกำหนด `exportOptions.setOnePagePerSheet(false)` แล้วเลือกชีตที่ต้องการเรนเดอร์ด้วยตนเอง |
| **ไฟล์ Excel ขนาดใหญ่** ทำให้เกิดความกดดันด้านหน่วยความจำ | เปิดโหมดสตรีมมิ่งด้วย `loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` เมื่อสร้าง `Workbook` |
| **ไม่มีการตั้งค่าไลเซนส์** (เวอร์ชันประเมินผล) | PPTX ที่สร้างจะมีลายน้ำ เพิ่มโค้ด `License license = new License(); license.setLicense("Aspose.Cells.lic");` ที่จุดเริ่มต้นของ `main` เพื่อเอาลายน้ำออก |
| **ต้องการส่งออกเฉพาะช่วงที่กำหนด** | สร้างเวิร์กชีตชั่วคราว คัดลอกช่วงที่ต้องการด้วย `worksheet.getCells().copyRange(...)` แล้วส่งออกชีตชั่วคราวนั้น |
| **ความเข้ากันได้กับเวอร์ชัน PowerPoint** | Aspose.Cells สร้าง Office Open XML (PPTX) เสมอ ซึ่งทำงานกับ PowerPoint 2007 ขึ้นไป สำหรับรูปแบบ PPT เก่าให้เปลี่ยนเป็น `SaveFormat.PPT` (แม้ว่ากล่องข้อความที่แก้ไขได้จะสนับสนุนเฉพาะ PPTX) |

---

## เคล็ดลับระดับมืออาชีพสำหรับการใช้งานในผลิตภัณฑ์

* **การแปลงเป็นชุด** – วนลูปผ่านไดเรกทอรีของไฟล์ Excel ใช้อินสแตนซ์ `ImageOrPrintOptions` เพียงตัวเดียวเพื่อลดค่าโอเวอร์เฮดของการสร้างอ็อบเจ็กต์
* **การวัดประสิทธิภาพ** – วัดเวลาที่ใช้โดย `workbook.save` สำหรับไฟล์ขนาดใหญ่; พิจารณาเพิ่ม heap ของ JVM (`-Xmx2g`) หากพบ `OutOfMemoryError`
* **การจัดรูปแบบสไลด์แบบกำหนดเอง** – หลังการส่งออก คุณสามารถจัดการ PPTX ต่อด้วย Aspose.Slides for Java เพื่อเพิ่มหัวเรื่อง, ส่วนท้าย หรือใช้มาสเตอร์สไลด์

---

## สรุป

คุณได้เรียนรู้วิธี **export Excel to PowerPoint** ด้วย Java โดยคงความแม่นยำของแผนภูมิและเปิดใช้งาน **editable text boxes** ผ่าน `ImageOrPrintOptions` ตัวอย่างเต็มแสดงการโหลดเวิร์กบุ๊ก, กำหนดค่าตัวเลือกการส่งออก, และบันทึกไฟล์ PPTX เพียงสามขั้นตอนสั้น ๆ  

จากนี้คุณสามารถสำรวจหัวข้อที่เกี่ยวข้อง เช่น **การจัดการแผนภูมิ Aspose.Cells Java**, **การส่งออก PPTX ด้วยเทมเพลตกำหนดเอง**, หรือ **การประมวลผลชุดหลายสเปรดชีต** ทดลองเปลี่ยนค่า `SaveFormat` ต่าง ๆ ผสานวิธีนี้กับ Aspose.Slides และผสานเวิร์กโฟลว์เข้าสู่สายงานรายงานของคุณ

![Java code exporting Excel to PowerPoint](/images/export-excel-to-powerpoint.png){: .responsive-img alt="ภาพหน้าจอของโค้ด Java ที่ส่งออกแผ่นงาน Excel ไปยังสไลด์ PowerPoint"}

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโปรเจกต์ของคุณเอง

- [วิธีสร้างและกำหนดค่ากล่องข้อความใน Excel ด้วย Aspose.Cells Java เพื่อการนำเสนอข้อมูลที่ดียิ่งขึ้น](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
- [วิธีส่งออกแผนภูมิ Excel เป็น SVG ด้วย Aspose.Cells Java สำหรับกราฟิกเวกเตอร์ที่ปรับขนาดได้](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [วิธีส่งออกเวิร์กชีต Excel เป็น PNG ด้วย Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}