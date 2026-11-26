---
category: general
date: 2026-11-25
description: ส่งออก Excel เป็น SVG ด้วย Aspose.Cells ใน Java – คู่มือแบบขั้นตอนต่อขั้นตอนเพื่อบันทึก
  Excel เป็น SVG และสร้างภาพเวกเตอร์
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: th
lastmod: 2026-11-25
og_description: ส่งออก Excel เป็น SVG ด้วย Aspose.Cells ใน Java. เรียนรู้วิธีบันทึก
  Excel เป็น SVG และสร้างภาพเวกเตอร์คุณภาพสูงด้วยเพียงไม่กี่บรรทัดของโค้ด.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: ส่งออก Excel เป็น SVG ใน Java – บทเรียน Aspose.Cells อย่างสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: วิธีส่งออกไฟล์ Excel เป็น SVG ด้วย Aspose.Cells ใน Java
url: /th/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออก Excel เป็น SVG ด้วย Aspose.Cells ใน Java

หากคุณต้องการ **ส่งออก Excel เป็น SVG** คู่มือนี้จะแสดงวิธีทำด้วย Aspose.Cells สำหรับ Java คุณจะได้เรียนรู้วิธี **บันทึก Excel เป็น SVG** และสร้าง **vector image** คุณภาพสูงเพียงไม่กี่บรรทัดของโค้ด

การส่งออกเวิร์กบุ๊ก Excel ไปเป็นไฟล์ SVG ทำให้คุณสามารถฝังแผ่นงานลงในหน้าเว็บ รายงาน หรือสภาพแวดล้อมใด ๆ ที่ต้องการกราฟิกที่สามารถขยายได้ รูปแบบ SVG จะคงฟอนต์ สี และเส้นขอบของเซลล์โดยไม่เกิดการพิกเซลที่เห็นได้จากภาพแบบแรสเตอร์

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

* Java 17 หรือใหม่กว่า
* ใบอนุญาต Aspose.Cells สำหรับ Java ที่ใช้งานได้ (หรือคีย์ประเมินผลชั่วคราว)
* โปรเจกต์ Maven หรือ Gradle ที่สามารถเพิ่มการอ้างอิง Aspose.Cells ได้

เพิ่มไลบรารี Aspose.Cells ลงในโปรเจกต์ของคุณ:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## ส่งออก Excel เป็น SVG – ขั้นตอนทีละขั้น

กระบวนการประกอบด้วยสามขั้นตอนง่าย ๆ: โหลดเวิร์กบุ๊ก ตั้งค่าตัวเลือกการส่งออก SVG และบันทึกผลลัพธ์ แต่ละขั้นตอนอธิบายไว้ด้านล่าง

### ขั้นตอน 1: โหลดเวิร์กบุ๊กที่มีข้อมูล

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**ทำไมขั้นตอนนี้สำคัญ:**  
`Workbook` เป็นอ็อบเจ็กต์หลักใน Aspose.Cells การโหลดไฟล์เพียงครั้งเดียวทำให้คุณเข้าถึงทุกแผ่นงาน สไตล์ และอ็อบเจ็กต์ฝังที่ตัวส่งออก SVG จะใช้ต่อไป

### ขั้นตอน 2: ตั้งค่าตัวเลือกการส่งออกภาพสำหรับ SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**ทำไมขั้นตอนนี้สำคัญ:**  
`ImageOrPrintOptions` ให้คุณควบคุมรูปแบบผลลัพธ์ การเลือก `ImageFormat.SVG` ทำให้ผลลัพธ์เป็น **vector image** แทนบิตแมพ การเปิดใช้งาน `OnePagePerSheet` จะหลีกเลี่ยงการแบ่งหน้าในแผ่นงาน ซึ่งมักต้องการเมื่อ SVG จะถูกแสดงในเว็บวิว

### ขั้นตอน 3: บันทึกเวิร์กบุ๊กเป็นไฟล์ SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**ทำไมขั้นตอนนี้สำคัญ:**  
เมธอด `save` จะรวมเวิร์กบุ๊กที่โหลดไว้กับ `exportOptions` ที่กำหนดไว้ การเรียกนี้จะเขียนไฟล์ SVG ที่เป็นมาตรฐานเต็มรูปแบบ ซึ่งสามารถเปิดในเบราว์เซอร์ Inkscape หรือโปรแกรมแก้ไขเวกเตอร์ใด ๆ

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

การรวมสามขั้นตอนเข้าด้วยกันจะได้โปรแกรมที่พร้อมคอมไพล์และรันทันที:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

เมื่อรันโปรแกรมจะพิมพ์:

```
Export complete: Excel saved as SVG.
```

คุณจะพบไฟล์ `WithVariationSelectors.svg` ใน `C:/Output` การเปิดไฟล์ในเบราว์เซอร์จะแสดงแผ่นงานเป็นกราฟิกที่ขยายได้ โดยคงข้อความ เส้นขอบ และสีของเซลล์ไว้ครบถ้วน

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | การปรับแนะนำ |
|-----------|------------------------|
| **หลายแผ่นงาน** | วนลูปผ่าน `workbook.getWorksheets()` และเรียก `save` สำหรับแต่ละแผ่นงาน โดยอาจต่อชื่อแผ่นงานเข้าไปในชื่อไฟล์ |
| **เวิร์กบุ๊กขนาดใหญ่** | เพิ่มค่า `exportOptions.setRenderThreadCount(int)` เพื่อใช้การเรนเดอร์แบบขนาน ลดเวลาการแปลง |
| **กำหนด DPI เอง** | เรียก `exportOptions.setHorizontalResolution(int)` และ `exportOptions.setVerticalResolution(int)` เพื่อควบคุมการสเกลของ viewBox ใน SVG |
| **ฝังฟอนต์** | ตั้งค่า `exportOptions.setExportFontAsSVG(true)` เพื่อฝังคำนิยามฟอนต์โดยตรงใน SVG ทำให้แสดงผลได้แม้ไม่มีฟอนต์ต้นฉบับ |
| **ไฟล์ที่มีรหัสผ่าน** | ให้รหัสผ่านเมื่อโหลด: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## เคล็ดลับระดับมืออาชีพ

* **หลีกเลี่ยงการแปลงเป็นแรสเตอร์** – หากแผ่นงานมีแผนภูมิซับซ้อน ให้ตรวจสอบว่าแสดงเป็นองค์ประกอบเวกเตอร์ใน SVG หากไม่เป็น ให้เปิด `exportOptions.setExportChartAsSVG(true)` |
* **ประสิทธิภาพ** – สำหรับการแปลงเป็นชุด ใช้อ็อบเจ็กต์ `ImageOrPrintOptions` ตัวเดียวซ้ำ ๆ แทนการสร้างใหม่สำหรับแต่ละไฟล์ |
* **การทดสอบ** – ตรวจสอบ SVG ที่สร้างด้วยตัวตรวจสอบออนไลน์ (เช่น W3C SVG Validator) เพื่อค้นหา markup ที่ผิดพลาดตั้งแต่ต้น |

## ตรวจสอบการแปลง

คุณสามารถตรวจสอบโปรแกรมได้ว่าไฟล์ผลลัพธ์เป็น SVG จริงหรือไม่:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

การมีองค์ประกอบราก `<svg>` แสดงว่าการ **convert Excel to SVG** สำเร็จแล้ว

## สรุป

บทแนะนำนี้ได้แสดงวิธี **ส่งออก Excel เป็น SVG** ด้วย Aspose.Cells สำหรับ Java โดยการโหลดเวิร์กบุ๊ก ตั้งค่า `ImageOrPrintOptions` สำหรับ SVG และเรียก `save` คุณจึงสามารถ **บันทึก Excel เป็น SVG** และได้การแปลง **Excel to vector image** ที่สะอาดจาก Excel ไปยังเวกเตอร์ จากนี้คุณสามารถฝัง SVG ลงในหน้าเว็บ ใส่ในเอกสาร หรือประมวลผลต่อด้วยเครื่องมือกราฟิกเวกเตอร์ใด ๆ

### สิ่งที่ควรสำรวจต่อไป

* **ส่งออก Excel เป็น PNG หรือ JPEG** – เปลี่ยนเป็น `exportOptions.setImageFormat(ImageFormat.PNG)` เพื่อให้ได้ผลลัพธ์แบบแรสเตอร์ |
* **แปลง Excel เป็น PDF** – ใช้ `PdfSaveOptions` สำหรับเอกสารที่ต้องพิมพ์ |
* **การประมวลผลเป็นชุด** – ผสานโค้ดข้างต้นกับตัวตรวจจับระบบไฟล์เพื่อ **convert Excel to SVG** อัตโนมัติสำหรับทุกเวิร์กบุ๊กใหม่ในโฟลเดอร์ |

ทดลองปรับตัวเลือกต่าง ๆ และให้ Aspose.Cells ช่วยแปลงข้อมูล Excel ของคุณเป็นรูปแบบภาพใดก็ได้ที่ต้องการ โค้ดดิ้งอย่างสนุกสนาน!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ในโครงการของคุณเอง

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel to SVG – Step‑by‑Step Java Guide](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}