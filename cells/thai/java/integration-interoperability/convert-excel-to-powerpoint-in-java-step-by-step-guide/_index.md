---
category: general
date: 2026-11-22
description: แปลง Excel เป็น PowerPoint ด้วย Java โดยใช้ Aspose.Cells. เรียนรู้วิธีสร้าง
  PowerPoint จากไฟล์ Excel, ส่งออกแผ่นงานเป็นสไลด์ PPTX, และทำงานนำเสนออัตโนมัติ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: th
lastmod: 2026-11-22
og_description: แปลง Excel เป็น PowerPoint ด้วย Java และ Aspose.Cells บทเรียนนี้จะแสดงวิธีสร้าง
  PowerPoint จากไฟล์ Excel และส่งออกไฟล์ .xlsx ไปเป็นสไลด์ .pptx
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: แปลง Excel เป็น PowerPoint ด้วย Java – คู่มือการเขียนโปรแกรมครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: แปลง Excel เป็น PowerPoint ด้วย Java – คู่มือขั้นตอนโดยละเอียด
url: /th/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง Excel เป็น PowerPoint ใน Java – คู่มือขั้นตอนต่อขั้นตอน

หากคุณต้องการ **convert Excel to PowerPoint in Java** คู่มือนี้จะแสดงวิธีทำด้วย Aspose.Cells ไม่ว่าคุณจะสร้างเครื่องมือรายงานหรือทำงานอัตโนมัติของสไลด์ คุณจะได้เรียนรู้วิธี **create PowerPoint from Excel file** ด้วยโปรแกรมและส่งออกแต่ละ worksheet เป็นสไลด์ PPTX ที่แก้ไขได้

บทแนะนำนี้ครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโครงการจนถึงการบันทึกงานนำเสนอขั้นสุดท้าย เมื่อเสร็จสิ้นคุณจะมีโปรแกรม Java ที่สามารถรันได้ซึ่งแปลงเวิร์กบุ๊ก `.xlsx` เป็นไฟล์ `.pptx` ที่คุณสามารถแก้ไขใน Microsoft PowerPoint ได้โดยไม่ต้องคัดลอก‑วางด้วยตนเอง

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* Java 17 หรือใหม่กว่า (โค้ดใช้ระบบโมดูลสมัยใหม่)  
* ใบอนุญาต Aspose.Cells for Java หรือคีย์ประเมินผลชั่วคราว  
* Maven หรือ Gradle สำหรับจัดการ dependencies (ตัวอย่างใช้ Maven)  
* ตัวอย่างเวิร์กบุ๊ก Excel (`input.xlsx`) ที่วางไว้ในโฟลเดอร์ที่รู้จัก

> **Pro tip:** Aspose.Cells รองรับทั้ง `.xls` และ `.xlsx` โค้ดเดียวกันทำงานได้กับทั้งสองรูปแบบ; เพียงเปลี่ยนนามสกุลไฟล์

## ขั้นตอนที่ 1: ตั้งค่าโครงการ Java สำหรับ **convert Excel to PowerPoint**

สร้างโครงการ Maven ใหม่ (หรือเพิ่มในโครงการที่มีอยู่) แล้วเพิ่ม dependency ของ Aspose.Cells:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

เรียกใช้ `mvn clean install` เพื่อดาวน์โหลดไลบรารี หากคุณมีไฟล์ใบอนุญาต (`Aspose.Total.lic`) ให้วางไว้ในโฟลเดอร์ `src/main/resources` โค้ดจะโหลดโดยอัตโนมัติ

## ขั้นตอนที่ 2: โหลดไฟล์ Excel workbook

ขั้นตอนการทำงานแรกในกระบวนการ **convert excel workbook to pptx slides** คือการโหลดไฟล์ต้นทาง Aspose.Cells สามารถเปิดไฟล์จากระบบไฟล์, สตรีม, หรือแม้แต่ byte array

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**Why this matters:** การโหลดเวิร์กบุ๊กจะตรวจสอบรูปแบบไฟล์และเตรียมโครงสร้างภายในที่ Aspose.Cells จะใช้แปลงเป็นอ็อบเจ็กต์ PowerPoint ต่อไป

## ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการบันทึกเพื่อ **create PowerPoint from Excel file**

Aspose.Cells ใช้ `ImageOrPrintOptions` เพื่อกำหนดรูปแบบผลลัพธ์เมื่อแปลงเป็นไฟล์พรีเซนเทชัน ตั้งค่า `SaveFormat` เป็น `SaveFormat.PPTX` เพื่อสร้างสไลด์ที่แก้ไขได้

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**Why this matters:** ธง `setOnePagePerSheet(false)` บอก Aspose.Cells ให้ถือแต่ละ worksheet เป็นสไลด์แยกหนึ่งหน้า ซึ่งเป็นสถานการณ์ที่พบบ่อยที่สุดเมื่อคุณ **convert Excel to PowerPoint** สำหรับการนำเสนอ

## ขั้นตอนที่ 4: บันทึก workbook เป็นสไลด์ PPTX

ตอนนี้คุณสามารถเขียนพรีเซนเทชันลงดิสก์ได้แล้ว เมธอด `Workbook.save` รับพาธเอาต์พุตและตัวเลือกที่คุณกำหนดไว้

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

เมื่อคุณเปิด `editable.pptx` ใน Microsoft PowerPoint คุณจะเห็นสไลด์หนึ่งสไลด์ต่อ worksheet โดยทุกเซลล์จะแสดงเป็นกล่องข้อความและรูปร่างที่แก้ไขได้ คุณสามารถแก้ไขฟอนต์, สี, หรือเพิ่มแอนิเมชันโดยตรงใน PowerPoint ได้ต่อไป

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะแสดงผล:

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

และไฟล์ `editable.pptx` จะปรากฏในไดเรกทอรีที่ระบุ พร้อมสำหรับการปรับแต่งด้วยมือหรือทำอัตโนมัติต่อไป

## ขั้นตอนที่ 5: ตัวแปรทั่วไปและกรณีขอบ

### การแปลงเฉพาะชีตที่เลือก

หากคุณต้องการ **convert Excel workbook to PPTX slides** แต่ต้องการละเว้น worksheet บางชีต ให้กรองก่อนบันทึก:

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### การจัดการเวิร์กบุ๊กขนาดใหญ่

สำหรับเวิร์กบุ๊กที่มีหลายชีต การใช้หน่วยความจำอาจเพิ่มขึ้นอย่างมีนัยสำคัญ ใช้ `WorkbookSettings` เพื่อเปิดการสตรีม:

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### การรักษาสูตร

Aspose.Cells ประเมินสูตรก่อนการเรนเดอร์ หากคุณต้องการแสดงสูตรดิบบนสไลด์ ให้ตั้งค่า `opts.setExportFormulas(true)`

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์โดยโปรแกรม (ทางเลือก)

คุณสามารถโหลดไฟล์ PPTX ที่สร้างขึ้นด้วย Aspose.Slides เพื่อตรวจสอบว่าจำนวนสไลด์ตรงกับจำนวน worksheet หรือไม่:

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

การตรวจสอบเพิ่มเติมนี้มีประโยชน์ใน pipeline ของ CI ที่คุณต้องการยืนยันว่าการแปลงสำเร็จ

## สรุป

คุณมีโซลูชันที่ครบถ้วนและพร้อมใช้งานในระดับ production เพื่อ **convert Excel to PowerPoint in Java** โปรแกรมโหลดเวิร์กบุ๊ก `.xlsx` กำหนด `ImageOrPrintOptions` เพื่อ **create PowerPoint from Excel file** และบันทึกผลลัพธ์เป็นสไลด์ PPTX ที่แก้ไขได้ โดยการปรับตัวเลือกต่าง ๆ คุณสามารถปรับความละเอียด, เลือกชีตเฉพาะ, หรือสตรีมไฟล์ขนาดใหญ่ ทำให้วิธีนี้ยืดหยุ่นสำหรับหลายสถานการณ์อัตโนมัติ

**ขั้นตอนต่อไป**

* สำรวจ **java convert .xlsx to .pptx** เพิ่มเติมโดยเพิ่มเลเอาต์สไลด์แบบกำหนดเองด้วย Aspose.Slides  
* ทำอัตโนมัติการประมวลผลแบบแบชของหลายเวิร์กบุ๊กโดยใช้ตัวตรวจจับโฟลเดอร์ง่าย ๆ  
* ผสานการแปลงนี้กับการสร้างแผนภูมิตามข้อมูลเพื่อผลิตการนำเสนอแบบไดนามิก

อย่าลังเลที่จะทดลองปรับตั้งค่าและแบ่งปันผลลัพธ์ของคุณ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบพร้อมคำอธิบายขั้นตอนต่อขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ทางเลือกในโครงการของคุณเอง

- [แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells ใน Java](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [วิธีแปลง Excel เป็น PowerPoint ด้วย Aspose.Cells สำหรับ .NET: คู่มือฉบับสมบูรณ์](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [แปลง Excel เป็น Powerpoint ด้วย Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}