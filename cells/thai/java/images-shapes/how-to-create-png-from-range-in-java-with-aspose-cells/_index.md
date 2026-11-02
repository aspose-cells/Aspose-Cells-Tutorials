---
category: general
date: 2026-10-07
description: เรียนรู้วิธีสร้าง PNG จากช่วงและส่งออกข้อมูลเป็น PNG ใน Java คู่มือนี้จะแสดงวิธีบันทึกรูปภาพช่วง
  Excel ด้วย Aspose.Cells
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: th
lastmod: 2026-10-07
og_description: สร้าง PNG จากช่วงใน Java และส่งออกข้อมูลเป็น PNG ด้วย Aspose.Cells
  ทำตามบทเรียนฉบับเต็มนี้เพื่อบันทึกภาพช่วง Excel ได้ทันที.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: สร้าง PNG จากช่วงใน Java – คู่มือ Aspose.Cells ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: วิธีสร้าง PNG จากช่วงใน Java ด้วย Aspose.Cells
url: /th/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง PNG จากช่วงใน Java ด้วย Aspose.Cells

หากคุณต้องการ **สร้าง PNG จากช่วง** ในเวิร์กบุ๊ก Excel, บทแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด เมื่อจบคู่มือคุณจะสามารถ **ส่งออกข้อมูลเป็น PNG**, บันทึกภาพช่วงของ Excel, และนำไฟล์ไปใช้ซ้ำในรายงานหรือหน้าเว็บได้

คุณจะได้เห็นโปรแกรม Java ที่ทำงานได้เต็มรูปแบบซึ่งโหลดเวิร์กบุ๊ก, เลือกเซลล์ที่ต้องการ, แปลงเป็น PNG, และบันทึกผลลัพธ์ลงดิสก์ ไม่ต้องใช้เครื่องมือภายนอก—Aspose.Cells จัดการทุกอย่างภายใน

## สิ่งที่บทแนะนำนี้ครอบคลุม

* ข้อกำหนดเบื้องต้นและการตั้งค่า Maven สำหรับ Aspose.Cells
* การโหลดเวิร์กบุ๊กที่มี Pivot Table หรือช่วงข้อมูลใด ๆ
* การกำหนดช่วงเซลล์ที่ต้องการแปลงอย่างแม่นยำ
* การกำหนดค่า Image Options สำหรับการส่งออกเป็น PNG
* การเรนเดอร์ช่วงและบันทึกไฟล์ PNG
* ข้อผิดพลาดทั่วไปและเคล็ดลับสำหรับภาพคุณภาพสูง

หลังจากทำตามขั้นตอนเหล่านี้แล้วคุณจะสามารถ **แปลง Worksheet เป็น PNG** สำหรับช่วงใดก็ได้ ไม่ว่าจะเป็นตารางง่าย ๆ หรือแผนภูมิ Pivot ที่ซับซ้อน

## ข้อกำหนดเบื้องต้น

* Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์ด้วย JDK 11+)
* Maven 3.6+ (หรือ Gradle หากคุณต้องการ)
* Aspose.Cells for Java 23.12 หรือใหม่กว่า – เพิ่ม dependency ตามที่แสดงด้านล่าง
* ไฟล์ Excel ที่มีอยู่ (`PivotWithStyle.xlsx`) ซึ่งมีช่วงที่คุณต้องการจับภาพ

> **เคล็ดลับ:** หากคุณไม่มีลิขสิทธิ์, คุณสามารถขอคีย์การประเมินชั่วคราวจาก Aspose ได้ ไลบรารีทำงานในโหมดประเมินโดยไม่ต้องกำหนดค่าเพิ่มเติม

### การพึ่งพา Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กที่มีช่วงเป้าหมาย

การดำเนินการแรกคือการเปิดไฟล์ Excel. Aspose.Cells อ่านไฟล์เข้าสู่หน่วยความจำโดยไม่ต้องใช้ Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*ทำไมเรื่องนี้ถึงสำคัญ*: การโหลดเวิร์กบุ๊กทำให้คุณเข้าถึง worksheets, cells, และคุณสมบัติการตั้งค่าหน้ากระดาษที่จำเป็นสำหรับการเรนเดอร์.

## ขั้นตอนที่ 2: เข้าถึง Worksheet ที่มีช่วง

ส่วนใหญ่เวิร์กบุ๊กจะมีชีตเริ่มต้นที่ดัชนี 0, แต่คุณก็สามารถใช้ชื่อชีตได้เช่นกัน.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

หากข้อมูลของคุณอยู่บนชีตอื่น, ให้แทนที่ `0` ด้วยดัชนีที่เหมาะสมหรือใช้ `workbook.getWorksheets().get("SheetName")`.

## ขั้นตอนที่ 3: กำหนดช่วงเซลล์ที่ต้องการแปลง

คุณสามารถระบุพื้นที่สี่เหลี่ยมใด ๆ ด้วยการใช้รูปแบบ A1. ในตัวอย่างนี้เราจะจับภาพ `A1:D15`, ซึ่งอาจเป็น Pivot Table หรือบล็อกข้อมูลทั่วไป.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*กรณีขอบ*: เมื่อช่วงรวมเซลล์ที่ merged, Aspose.Cells จะขยายภาพโดยอัตโนมัติเพื่อรวมพื้นที่ที่ merged ไว้ด้วย.

## ขั้นตอนที่ 4: เตรียมตัวเลือกภาพ PNG

`ImageOrPrintOptions` ให้คุณควบคุมรูปแบบ, ความละเอียด, และรายละเอียดการเรนเดอร์อื่น ๆ การตั้งค่า save format เป็น PNG จะรับประกันคุณภาพแบบไม่มีการสูญเสีย.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

การเพิ่ม DPI มีประโยชน์เมื่อเซลล์ต้นทางมีฟอนต์ขนาดเล็กหรือแผนภูมิที่ละเอียด.

## ขั้นตอนที่ 5: จำกัดพื้นที่เรนเดอร์ให้เป็นช่วงที่เลือก

โดยการกำหนดช่วงเป็นพื้นที่พิมพ์, Aspose.Cells จะเรนเดอร์เฉพาะเซลล์เหล่านั้นและละเว้นส่วนที่เหลือของชีต.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

หากข้ามขั้นตอนนี้, Worksheet ทั้งหมดจะถูกแปลงเป็น raster ซึ่งอาจทำให้ใช้หน่วยความจำมากและสร้างภาพที่มีขนาดใหญ่ขึ้น.

## ขั้นตอนที่ 6: เรนเดอร์ช่วงและเพิ่มรูปภาพลงใน Worksheet (ทางเลือก)

หากคุณต้องการฝัง PNG ที่สร้างขึ้นกลับเข้าไปในเวิร์กบุ๊ก (เพื่อการแสดงตัวอย่าง), คุณสามารถเพิ่มเป็นรูปภาพได้ ขั้นตอนนี้เป็นทางเลือกสำหรับกรณีการส่งออกอย่างเดียว.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*ทำไมคุณอาจทำเช่นนี้*: กระบวนการทำงานบางอย่างต้องการให้ภาพเป็นส่วนหนึ่งของเวิร์กบุ๊กก่อนการแจกจ่าย เช่น การสร้างรายงานที่พิมพ์ได้ซึ่งผสมเซลล์ดั้งเดิมและภาพเข้าด้วยกัน.

## ขั้นตอนที่ 7: บันทึกไฟล์ PNG ลงดิสก์

สุดท้าย, เขียนภาพลงไฟล์. เมธอด `save` จะเคารพรูปแบบที่ระบุใน `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

เมื่อโปรแกรมทำงานเสร็จ, `PivotImage.png` จะมีภาพสแนปชอตที่พิกเซลสมบูรณ์ของเซลล์ `A1:D15`.

### ผลลัพธ์ที่คาดหวัง

* ไฟล์ชื่อ `PivotImage.png` ที่อยู่ใน `YOUR_DIRECTORY`.
* ภาพแสดงการจัดวาง, ฟอนต์, สี, และเส้นขอบที่ตรงกับช่วงที่เลือก.
* หากช่วงต้นทางมี Pivot Table, ภาพที่เรนเดอร์จะรวมสไตล์และค่าที่คำนวณเช่นเดียวกับที่แสดงใน Excel.

## การจัดการสถานการณ์ทั่วไป

### การส่งออกช่วงที่ไม่ต่อเนื่อง

Aspose.Cells ไม่สามารถเรนเดอร์ช่วงที่แยกกันเป็นภาพเดียวได้. เพื่อส่งออกหลายพื้นที่, ให้สร้างภาพแยกสำหรับแต่ละช่วงและรวมเข้าด้วยกันภายหลังโดยใช้ไลบรารีประมวลผลภาพ (เช่น ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### การบันทึก Worksheet ขนาดใหญ่เป็น PNG

การเรนเดอร์ชีตทั้งหมดที่มีหลายพันแถวอาจใช้หน่วยความจำมาก. ลดผลกระทบนี้โดย:

* ลด DPI (`imageOptions.setResolution(72)`) เพื่อให้ไฟล์มีขนาดเล็กลง.
* ใช้ `setPageCount` เพื่อจำกัดจำนวนหน้าที่เรนเดอร์.
* ส่งออกหนึ่งหน้าที่พิมพ์ได้ต่อครั้งผ่าน `worksheet.getPageSetup().setPrintArea(...)`.

### การรักษาสูตรในเซลล์

ภาพ PNG เป็นรูปแบบ raster; สูตรจะไม่ถูกเก็บไว้. หากผู้ใช้ต่อไปต้องการข้อมูลดิบ, ให้ส่งออกช่วงเป็น CSV หรือ JSON ด้วย `Range.exportDataTable()`.

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นคลาส Java เต็มรูปแบบที่คุณสามารถคัดลอก‑วางลงใน IDE ของคุณ. แทนที่ `YOUR_DIRECTORY` ด้วยพาธแบบ absolute หรือ relative บนเครื่องของคุณ.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

เรียกใช้โปรแกรมด้วย `mvn compile exec:java` (หรือเครื่องมือสร้างที่คุณชอบ). หลังจากทำงานเสร็จ, เปิด `PivotImage.png` เพื่อตรวจสอบผลลัพธ์.

## สรุป

ตอนนี้คุณรู้วิธี **สร้าง PNG จากช่วง** ใน Java ด้วย Aspose.Cells, อย่างมีประสิทธิภาพ **ส่งออกข้อมูลเป็น PNG** และ **บันทึกภาพช่วง Excel** สำหรับสถานการณ์การรายงานหรือการแชร์ใด ๆ ขั้นตอน—การโหลดเวิร์กบุ๊ก, การกำหนดช่วง, การตั้งค่า image options, การกำหนดพื้นที่พิมพ์, และการบันทึกไฟล์—ครอบคลุมเวิร์กโฟลว์ทั้งหมดสำหรับ **แปลง Worksheet เป็น PNG** และ **บันทึกเซลล์เป็น PNG**.

### ขั้นตอนต่อไป

* ทดลองใช้ค่า `Resolution` ต่าง ๆ เพื่อปรับสมดุลระหว่างคุณภาพและขนาดไฟล์.
* ใช้ `ImageOrPrintOptions.setTransparent(true)` หากคุณต้องการ PNG ที่มีพื้นหลังโปร่งใส.
* รวมภาพหลายช่วงเป็น PDF เดียวโดยใช้ `PdfSaveOptions` สำหรับรายงานหลายหน้า.
* สำรวจการส่งออกเป็นรูปแบบ raster อื่น ๆ (JPEG, BMP) โดยเปลี่ยน `setSaveFormat`.

คุณสามารถปรับใช้รูปแบบนี้กับแผนภูมิ, ตาราง, หรือแม้แต่ Worksheet ทั้งหมดได้ตามต้องการ. ขอให้เขียนโค้ดสนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ.

- [วิธีส่งออก Worksheet ของ Excel เป็น PNG ด้วย Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [แปลง Excel เป็น PNG ด้วย Aspose.Cells for Java: คู่มือแบบขั้นตอน](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [สร้าง Union Range ใน Excel ด้วย Aspose.Cells Java: คู่มือฉบับสมบูรณ์](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}