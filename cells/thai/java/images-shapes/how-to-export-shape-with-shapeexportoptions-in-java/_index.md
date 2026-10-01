---
category: general
date: 2026-10-01
description: เรียนรู้วิธีส่งออกรูปร่างด้วย ShapeExportOptions ใน Java โดยคงให้รูปร่างสามารถแก้ไขได้เมื่อแปลงเป็น
  PPTX ด้วย Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: th
lastmod: 2026-10-01
og_description: ส่งออกรูปทรงด้วย ShapeExportOptions ใน Java เพื่อสร้างไฟล์ PPTX ที่แก้ไขได้
  บทเรียนนี้จะพาคุณผ่านกระบวนการทั้งหมดโดยใช้ Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: ส่งออกรูปร่างด้วย ShapeExportOptions ใน Java – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: วิธีส่งออกรูปร่างด้วย ShapeExportOptions ใน Java
url: /th/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออกรูปทรงด้วย ShapeExportOptions ใน Java

หากคุณต้องการ **ส่งออกรูปทรงด้วย ShapeExportOptions** จากไฟล์ Excel คำแนะนำนี้จะแสดงขั้นตอนที่แน่นอน คุณจะได้เห็นวิธีทำให้รูปทรงยังคงแก้ไขได้เมื่อแปลงเป็นไฟล์ PPTX ซึ่งสำคัญสำหรับการแก้ไขต่อใน PowerPoint

การส่งออกรูปทรงเป็นงานทั่วไปเมื่อคุณสร้างสไลด์เด็คจากสเปรดชีต — ไม่ว่าจะเป็นการสร้างสไลด์ขาย รายงานแดชบอร์ด หรือการนำเสนออัตโนมัติ บทเรียนนี้ครอบคลุมทุกอย่างที่คุณต้องการ ตั้งแต่การตั้งค่าโปรเจกต์จนถึงการตรวจสอบไฟล์ที่ส่งออก โดยใช้ไลบรารี **Aspose.Cells for Java**

## สิ่งที่คุณต้องมี

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

- Java 17 หรือใหม่กว่า (โค้ดคอมไพล์ได้กับ JDK เวอร์ชันล่าสุด)
- Maven หรือ Gradle สำหรับจัดการ dependencies
- ไฟล์ Excel (`Shapes.xlsx`) ที่มีอย่างน้อยหนึ่ง textbox หรือรูปทรงอื่น
- ความคุ้นเคยพื้นฐานกับ Aspose.Cells APIs

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ลงในโปรเจกต์ของคุณ (Aspose Cells export shape)

หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

สำหรับ Gradle ให้วางโค้ดนี้ใน `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **เคล็ดลับ:** ลงทะเบียนไลเซนส์ตั้งแต่แรกเพื่อหลีกเลี่ยงลายน้ำของรุ่นทดลอง  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กที่มีรูปทรงอยู่

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

อ็อบเจ็กต์ `Workbook` แทนไฟล์ Excel ทั้งไฟล์ การโหลดเป็นขั้นตอนแรกที่จำเป็นสำหรับการจัดการรูปทรงใด ๆ

## ขั้นตอนที่ 3: เข้าถึงเวิร์กชีตและดึงรูปทรงที่ต้องการ (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **ทำไมเรื่องนี้สำคัญ:** รูปทรงถูกจัดเก็บต่อเวิร์กชีต ดังนั้นคุณต้องไปยังชีตที่ถูกต้องก่อนจึงจะส่งออกรูปทรงเฉพาะได้

## ขั้นตอนที่ 4: ตั้งค่า **ShapeExportOptions** เพื่อให้รูปทรงยังคงแก้ไขได้ (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

การตั้งค่า `ExportAsEditable` เป็น `true` จะบอก Aspose.Cells ให้รักษาข้อมูลเวกเตอร์ของรูปทรงไว้ ทำให้ผู้ใช้ PowerPoint สามารถแก้ไขรูปทรงหลังจากนำเข้าได้

## ขั้นตอนที่ 5: ส่งออกรูปทรงโดยตรงเป็นไฟล์ PPTX (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

เมธอด `exportToImage` ทำงานกับหลายรูปแบบภาพ; เมื่อชื่อไฟล์เป้าหมายลงท้ายด้วย `.pptx` Aspose.Cells จะเขียนสไลด์ PowerPoint ที่มีรูปทรงนั้นอยู่

### ผลลัพธ์ที่คาดหวัง

- ปรากฏไฟล์ `textbox.pptx` ในไดเรกทอรีที่ระบุ
- เปิดไฟล์ใน PowerPoint จะเห็นสไลด์เดียวที่มี textbox เดิม
- textbox สามารถแก้ไขได้เต็มที่ (เปลี่ยนข้อความ, ฟอนต์, ขนาด ฯลฯ)

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์และจัดการกรณีขอบทั่วไป

### ตรวจสอบโดยโปรแกรม

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

หาก `slideCount` มีค่าเท่ากับ `1` การส่งออกสำเร็จ

### กรณีขอบ: รูปทรงหลายอัน

หากเวิร์กชีตมีหลายรูปทรงและคุณต้องการเพียงอันเดียว ให้ค้นหาตามชื่อ:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### กรณีขอบ: ไม่พบรูปทรง

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### กรณีขอบ: ส่งออกเป็นรูปแบบอื่น

`ShapeExportOptions` ยังรองรับ PNG, JPEG, SVG, และ EMF เปลี่ยนส่วนขยายไฟล์และอาจตั้งค่า `exportOptions.setImageFormat(ImageFormat.PNG)` เพิ่มเติมได้

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกส่วนเข้าด้วยกันจะได้โปรแกรมที่พร้อมคัดลอก‑วางลงใน IDE ของคุณ:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

เมื่อรันโปรแกรมจะสร้างไฟล์ `textbox.pptx` เปิดไฟล์ใน PowerPoint คลิกขวาที่ textbox แล้วคุณจะเห็นตัวจัดการแก้ไขตามปกติ — ยืนยันว่า **export shape with ShapeExportOptions** รักษาความสามารถในการแก้ไขไว้

## คำถามที่พบบ่อย

| Question | Answer |
|----------|--------|
| *Can I export a chart shape?* | Yes. The same `exportToImage` call works for charts, images, and SmartArt. |
| *What if I need a higher resolution PNG?* | Set `options.setImageFormat(ImageFormat.PNG)` and adjust `options.setResolution(300)` before exporting. |
| *Is the exported PPTX compatible with older PowerPoint versions?* | The library writes Office Open XML (PPTX) which is supported by PowerPoint 2007 and later. |
| *Do I need a license for this to work?* | A free evaluation works but adds a watermark. Register a license to remove it. |

## ขั้นตอนต่อไป

- สำรวจ **Aspose.Slides for Java** หากต้องการรวมหลายรูปทรงที่ส่งออกไว้ในสไลด์เด็คเดียว
- ใช้ **ShapeExportOptions.setExportAsEditable(false)** เมื่อคุณต้องการภาพเรสเตอร์ (PNG/JPEG) เพื่อเรนเดอร์เร็วขึ้น
- ทำอัตโนมัติแบบแบตช์: วนลูปทุกเวิร์กชีตและส่งออกทุกรูปทรงเป็นไฟล์ PPTX แยกกัน

---

### สรุป

ตอนนี้คุณรู้วิธี **export shape with ShapeExportOptions** ใน Java แล้ว โดยรักษาความสามารถในการแก้ไขเมื่อแปลง textbox (หรือรูปทรงอื่น) เป็นไฟล์ PPTX ตามขั้นตอนที่อธิบาย — ตั้งค่าไลบรารี, โหลดเวิร์กบุ๊ก, กำหนด `ShapeExportOptions`, แล้วเรียก `exportToImage` — คุณสามารถผสานการส่งออกรูปทรงเข้าไปในกระบวนการรายงานอัตโนมัติของคุณได้

ลองทดลองกับรูปทรงต่าง ๆ, รูปแบบผลลัพธ์, และการตั้งค่าความละเอียด หากบทแนะนำนี้เป็นประโยชน์ อย่าลืมแชร์กับทีมงานหรือบันทึกไว้เพื่ออ้างอิงในอนาคต ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [How to Adjust Shape Margins in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [How to Apply 3D Shape Formatting in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Workbook Shape Copying Guide](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}