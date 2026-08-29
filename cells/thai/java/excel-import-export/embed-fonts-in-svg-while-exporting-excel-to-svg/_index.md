---
category: general
date: 2026-08-14
description: ฝังฟอนต์ใน SVG ขณะส่งออก Excel เป็น SVG ด้วย Aspose.Cells. เรียนรู้วิธีตั้งค่าพื้นที่พิมพ์,
  ตั้งค่าตัวเลือกการพิมพ์, และใช้ฟังก์ชัน WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: th
lastmod: 2026-08-14
og_description: ฝังฟอนต์ใน SVG ขณะส่งออก Excel เป็น SVG ด้วย Aspose.Cells คู่มือนี้จะแสดงวิธีตั้งค่าพื้นที่พิมพ์
  กำหนดตัวเลือกการพิมพ์ และใช้ฟังก์ชัน WRAPCOLS
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: ฝังฟอนต์ใน SVG ขณะส่งออก Excel เป็น SVG – ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: ฝังฟอนต์ใน SVG ขณะส่งออก Excel เป็น SVG
url: /th/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ฝังฟอนต์ใน SVG ขณะส่งออก Excel เป็น SVG

หากคุณต้องการ **ฝังฟอนต์ใน SVG ขณะส่งออก Excel เป็น SVG** คำแนะนำนี้จะแสดงวิธีทำอย่างละเอียดด้วย Aspose.Cells for Java เราจะอธิบายวิธี **กำหนดพื้นที่พิมพ์**, **ตั้งค่าตัวเลือกการพิมพ์**, และ **ใช้ฟังก์ชัน WRAPCOLS** เพื่อจัดรูปแบบข้อมูลโดยไม่สูญเสียเลย์เอาต์

คุณจะได้ทำตามตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งโหลดเวิร์กบุ๊กที่มีอยู่แล้ว, ใช้สูตร `WRAPCOLS`, ตั้งค่าตัวเลือกภาพเฉพาะสำหรับ SVG, กำหนดช่วงการพิมพ์, และสุดท้ายบันทึกไฟล์เป็น SVG พร้อมฝังฟอนต์ ไม่ต้องอ้างอิงเอกสารภายนอก—คัดลอกโค้ด, รัน, แล้วตรวจสอบ SVG ที่ได้

## ฝังฟอนต์ใน SVG – การกำหนดค่า ImageOrPrintOptions

การฝังฟอนต์ทำให้ SVG แสดงผลตรงกับที่เห็นใน Excel แม้บนเครื่องที่ไม่มีฟอนต์ต้นฉบับติดตั้ง

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*ทำไมจึงสำคัญ*: เมื่อเปิดใช้งาน `setEmbedFonts(true)` Aspose.Cells จะเขียนข้อมูลฟอนต์ลงในส่วน `<defs>` ของ SVG ผลลัพธ์คือไฟล์ที่เป็นอิสระและดูเหมือนกันในทุกเบราว์เซอร์และแพลตฟอร์ม

## ส่งออก Excel เป็น SVG – กระบวนการทำงานเต็มรูปแบบ

ขั้นตอนต่อไปนี้แสดงกระบวนการตั้งแต่โหลดเวิร์กบุ๊กจนถึงบันทึกไฟล์ SVG

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**ผลลัพธ์ที่คาดหวัง**: `output.svg` จะปรากฏใน `YOUR_DIRECTORY` การเปิดไฟล์ในเบราว์เซอร์จะแสดงแผ่นงานพร้อมฟอนต์ทั้งหมดที่ฝังอยู่, ข้อมูลถูกห่อเป็นสามคอลัมน์ (ขอบคุณ `WRAPCOLS`), และเฉพาะเซลล์ภายใน `A1:H30` เท่านั้นที่แสดงผล

## กำหนดพื้นที่พิมพ์สำหรับแผ่นงาน

การกำหนดพื้นที่พิมพ์จะจำกัด SVG ที่ส่งออกให้อยู่ในช่วงที่ระบุ ซึ่งช่วยลดขนาดไฟล์และทำให้ผู้ชมโฟกัสที่ข้อมูลที่สำคัญ

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*เคล็ดลับ*: ช่วงใช้รูปแบบ A1 ของ Excel หากต้องการช่วงแบบไดนามิกสามารถคำนวณได้ด้วย `ws.getCells().getMaxDisplayRange()`

## ตั้งค่าตัวเลือกการพิมพ์สำหรับการส่งออก SVG

ตัวเลือกการพิมพ์ควบคุมวิธีที่ Aspose.Cells แปลงแผ่นงานเป็นภาพ นอกจากการฝังฟอนต์แล้ว คุณยังสามารถปรับความละเอียด, การสเกล, และการจัดหน้าได้

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*ทำไมต้องตั้งค่าตัวเลือกการพิมพ์*: หากไม่กำหนดค่าโดยเจาะจง Aspose.Cells จะใช้ค่าเริ่มต้นซึ่งอาจไม่ฝังฟอนต์หรือใช้สเกลที่ไม่ต้องการ ทำให้ SVG ดูเบลอหรือสไตล์ไม่ตรง

## ใช้ฟังก์ชัน WRAPCOLS เพื่อห่อข้อมูลคอลัมน์

`WRAPCOLS` คือสูตร Excel ที่กระจายช่วงแนวตั้งเป็นจำนวนคอลัมน์ที่กำหนดไว้ เหมาะเมื่อคุณต้องการแสดงรายการยาวในกริดที่กระชับ

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

เมื่อบันทึกเวิร์กบุ๊ก Aspose.Cells จะประเมินสูตรและสร้างเลย์เอาต์สามคอลัมน์ภายในพื้นที่พิมพ์ที่กำหนด เทคนิคนี้ใช้ได้กับช่วงขนาดใดก็ได้—เพียงปรับอาร์กิวเมนต์ที่สองให้เป็นจำนวนคอลัมน์ที่ต้องการ

## ตัวอย่างที่ทำงานได้เต็มรูปแบบ

ด้านล่างเป็นโปรแกรม Java เต็มรูปแบบที่คุณสามารถวางลงใน IDE ใดก็ได้ ตรวจสอบให้แน่ใจว่ามีไลบรารี Aspose.Cells for Java อยู่ใน classpath

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**ขั้นตอนการตรวจสอบ**

1. รันโปรแกรม  
2. เปิด `output.svg` ในเว็บเบราว์เซอร์  
3. ยืนยันว่าข้อความใช้ฟอนต์เดียวกับไฟล์ Excel ต้นฉบับ (ฟอนต์ถูกฝัง)  
4. ตรวจสอบว่าเฉพาะเซลล์ใน `A1:H30` ปรากฏและข้อมูลจาก `A2:A10` แสดงในสามคอลัมน์

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| ฟอนต์หายใน SVG | `setEmbedFonts(false)` หรือไฟล์ฟอนต์ไม่เข้าถึงได้ | ตรวจสอบให้ `setEmbedFonts(true)` และฟอนต์ติดตั้งบนเครื่องที่รันโค้ด |
| WRAPCOLS ไม่ทำงาน | เครื่องมือคำนวณถูกปิด | เรียก `workbook.calculateFormula()` ก่อนส่งออก, หรือให้ Aspose.Cells ประเมินระหว่างการบันทึก |
| SVG ที่ส่งออกเป็นค่าว่าง | พื้นที่พิมพ์ไม่ครอบข้อมูลใดเลย | ตรวจสอบช่วงที่ส่งให้ `setPrintArea` อีกครั้ง |
| ไฟล์ SVG ใหญ่เกินไป | ไม่ได้กำหนดสเกล, ความละเอียดภาพสูง | ปรับ `imgOptions.setResolution(96)` หรือค่าที่คล้ายกันเพื่อควบคุม DPI |

## เคล็ดลับระดับมืออาชีพ: ใช้ ImageOrPrintOptions ซ้ำสำหรับหลายแผ่นงาน

หากเวิร์กบุ๊กของคุณมีหลายชีตที่ต้องการการตั้งค่า SVG เดียวกัน ให้สร้างอินสแตนซ์ `ImageOrPrintOptions` เพียงหนึ่งตัวและกำหนดให้กับ `PageSetup` ของแต่ละชีต วิธีนี้ช่วยลดการใช้หน่วยความจำและทำให้การฝังฟอนต์สอดคล้องกันในทุกไฟล์ที่ส่งออก

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## ขั้นตอนต่อไป

* **ส่งออกเป็นรูปแบบเวกเตอร์อื่น** – เปลี่ยน `ImageFormat.SVG` เป็น `ImageFormat.PDF` เพื่อสร้าง PDF คุณภาพสูง  
* **ประมวลผลเป็นชุด** – วนลูปผ่านโฟลเดอร์ที่มีไฟล์ `.xlsx` แล้วสร้าง SVG อัตโนมัติ  
* **จัดการฟอนต์แบบกำหนดเอง** – ใช้ `FontSettings` โหลดฟอนต์จากโฟลเดอร์เฉพาะเมื่อฟอนต์ระบบไม่เพียงพอ  

เมื่อคุณเชี่ยวชาญ **ฝังฟอนต์ใน SVG**, **ส่งออก Excel เป็น SVG**, **กำหนดพื้นที่พิมพ์**, **ตั้งค่าตัวเลือกการพิมพ์**, และ **ใช้ฟังก์ชัน WRAPCOLS** คุณจะสามารถอัตโนมัติการสร้าง SVG ความละเอียดสูงสำหรับรายงาน, แดชบอร์ด, และการแสดงผลบนเว็บโดยตรงจากข้อมูล Excel ได้อย่างง่ายดาย ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้ในโครงการของคุณเอง

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}