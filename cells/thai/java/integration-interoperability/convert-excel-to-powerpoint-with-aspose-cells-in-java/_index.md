---
category: general
date: 2026-09-21
description: แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells ใน Java – เรียนรู้วิธีส่งออกแผนภูมิเป็น
  PPTX และบันทึกเวิร์กบุ๊กเป็น PPTX เพียงไม่กี่บรรทัดของโค้ด
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: th
lastmod: 2026-09-21
og_description: แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells ใน Java บทเรียนนี้แสดงวิธีส่งออกแผนภูมิเป็นไฟล์
  PPTX และบันทึกเวิร์กบุ๊กเป็น PPTX พร้อมกล่องข้อความที่สามารถแก้ไขได้.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells – คู่มือ Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells ใน Java
url: /th/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells ใน Java

หากคุณต้องการ **แปลง Excel เป็น PowerPoint** คำแนะนำนี้จะแสดงวิธีที่กระชับและพร้อมใช้งานในระดับการผลิต คุณจะได้เห็นวิธีส่งออกแผนภูมิเป็น PPTX, รักษากล่องข้อความให้แก้ไขได้, และ **บันทึก workbook เป็น PPTX** ด้วยเพียงสามบรรทัดของโค้ด Java

นักพัฒนาหลายคนส่งออกข้อมูลเป็น PDF, แต่ PowerPoint มักเหมาะสมกว่าในการนำเสนอที่ต้องการแผนภูมิแบบสดและองค์ประกอบที่แก้ไขได้ บทแนะนำนี้ครอบคลุมทุกสิ่งที่คุณต้องการ — ตั้งแต่การตั้งค่าโครงการจนถึงการจัดการกับปัญหาที่พบบ่อย — เพื่อให้คุณสามารถสร้าง PowerPoint จากแผนภูมิ Excel ได้โดยไม่ต้องออกจาก IDE ของ Java

## ข้อกำหนดเบื้องต้น

* ติดตั้ง Java 17 หรือใหม่กว่า
* Maven (หรือ Gradle) เพื่อจัดการ dependencies
* ใบอนุญาต Aspose.Cells for Java (รุ่นทดลองฟรีใช้สำหรับการประเมิน)
* ไฟล์ Excel (`ChartAndTextbox.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิและกล่องข้อความหนึ่งอัน

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโครงการของคุณ

ขั้นตอนแรกคือการรวมไลบรารี Aspose.Cells เข้าไป ใช้ Maven เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **เคล็ดลับ:** หากคุณใช้ Gradle, รูปแบบที่เทียบเท่าคือ:
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

การรวมไลบรารีนี้จะทำให้คุณเข้าถึง `Workbook`, `PdfSaveOptions` และ enum `SaveFormat` ที่จำเป็นสำหรับการแปลง

## ขั้นตอนที่ 2: โหลด workbook ที่มีแผนภูมิและกล่องข้อความ

ตอนนี้ให้โหลดไฟล์ Excel คลาส `Workbook` จะอ่าน workbook ทั้งหมดเข้าสู่หน่วยความจำ โดยคงรักษาแผนภูมิ, สูตร, และกล่องข้อความไว้

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**ทำไมจึงสำคัญ:** การโหลด workbook ก่อนทำให้มั่นใจว่าทุกวัตถุที่ฝังอยู่ (แผนภูมิ, รูปภาพ, กล่องข้อความ) พร้อมสำหรับกระบวนการส่งออก หากไม่พบไฟล์ Aspose.Cells จะโยน `FileNotFoundException` ที่ชัดเจน ซึ่งคุณสามารถดักจับเพื่อให้ประสบการณ์ผู้ใช้ดียิ่งขึ้น

## ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการส่งออกเพื่อให้กล่องข้อความแก้ไขได้

Aspose.Cells ใช้ `PdfSaveOptions` เพื่อควบคุมวิธีการเขียนวัตถุเมื่อรูปแบบเป้าหมายเป็น PowerPoint โดยการเปิดใช้งาน `setExportEditableTextBoxes(true)` กล่องข้อความใด ๆ ในแผ่น Excel จะยังคงแก้ไขได้หลังการแปลง

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **ทำไมต้องใช้ `PdfSaveOptions` สำหรับ PPTX?**  
> ภายใน, Aspose.Cells ใช้กระบวนการเรนเดอร์ PDF ซ้ำสำหรับการส่งออกเป็น PowerPoint ทำให้สามารถควบคุมองค์ประกอบที่แก้ไขได้อย่างละเอียด การตั้งค่าสถานะนี้เป็นวิธีที่แนะนำเพื่อรักษาความสามารถในการแก้ไขของกล่องข้อความ

## ขั้นตอนที่ 4: บันทึก workbook เป็นการนำเสนอ PowerPoint

สุดท้าย เรียก `workbook.save` ด้วย `SaveFormat.PPTX` ขั้นตอนนี้จะทำให้เวิร์กโฟลว์ **สร้าง PowerPoint จากแผนภูมิ Excel** เสร็จสมบูรณ์

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

เมื่อนำทั้งหมดมารวมกัน โปรแกรมเต็มจะเป็นดังนี้:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อรันโปรแกรมจะพิมพ์:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

เมื่อคุณเปิด `Result.pptx` ใน Microsoft PowerPoint คุณจะเห็น:

* แผนภูมิ Excel ดั้งเดิมที่แสดงเป็นแผนภูมิ PowerPoint แบบเนทีฟ (แก้ไขได้ในเครื่องมือแก้ไขแผนภูมิของ PowerPoint)
* กล่องข้อความจาก Excel ปรากฏเป็นรูปทรงที่แก้ไขได้ ทำให้คุณสามารถเปลี่ยนข้อความโดยตรงบนสไลด์

## การจัดการกับกรณีขอบที่พบบ่อย

| สถานการณ์ | แนวทางแนะนำ |
|-----------|----------------------|
| **ไฟล์ไม่พบ** | ห่อหุ้มคอนสตรัคเตอร์ `Workbook` ด้วยบล็อก `try‑catch` และแสดงข้อความที่ชัดเจน |
| **Workbook ไม่มีแผนภูมิ** | ตรวจสอบว่าแผ่นงานมีแผนภูมิ (`worksheet.getCharts().getCount() > 0`) ก่อนทำการแปลง; หากไม่มีให้ข้ามขั้นตอนหรือเพิ่มตัวแทน |
| **ไฟล์ Excel ขนาดใหญ่** | เพิ่มขนาด heap ของ JVM (`-Xmx2g`) เพื่อหลีกเลี่ยง `OutOfMemoryError` ระหว่างการเรนเดอร์ |
| **ไม่ได้ตั้งค่าไลเซนส์** | เรียก `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` ก่อนโหลด workbook เพื่อเอาน้ำลายน้ำการประเมินออก |

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถแปลงหลายแผ่นงานเป็นสไลด์ PowerPoint แยกกันได้หรือไม่?**  
ตอบ: ได้. วนลูปผ่านแต่ละแผ่นงาน, ส่งออกแผนภูมิของมันไปยังสไลด์ใหม่โดยใช้ `PdfSaveOptions`, แล้วบันทึก workbook ครั้งเดียวหลังจากประมวลผลทุกแผ่น

**ถาม: วิธีนี้รักษาการจัดรูปแบบเซลล์หรือไม่?**  
ตอบ: มีเพียงวัตถุแผนภูมิและกล่องข้อความที่ถูกย้ายไปยัง PowerPoint การจัดรูปแบบเซลล์ยังคงอยู่ในไฟล์ Excel; ไม่ปรากฏใน PPTX

**ถาม: ถ้าฉันต้องการส่งออกเป็น PDF แทน PPTX จะทำอย่างไร?**  
ตอบ: ใช้ `SaveFormat.PDF` พร้อมกับ `PdfSaveOptions` เดียวกัน ธง `setExportEditableTextBoxes` ทำงานกับ PDF ด้วยเช่นกัน

## ขั้นตอนต่อไป

ตอนนี้คุณรู้วิธี **บันทึก workbook เป็น PPTX** และ **ส่งออกแผนภูมิเป็น PPTX** แล้ว คุณอาจสำรวจ:

* เพิ่มหลายแผนภูมิไปยังสไลด์ต่าง ๆ (`create powerpoint from excel chart` ด้วยลูป)
* ปรับแต่งเค้าโครงสไลด์โดยใช้ Aspose.Slides for Java เพื่อสไตล์การนำเสนอที่หลากหลายยิ่งขึ้น
* ฝังรูปภาพจากเซลล์ Excel ลงใน PowerPoint ด้วยคลาส `Picture`

ส่วนขยายเหล่านี้ช่วยให้คุณสร้างสายงานการรายงานอัตโนมัติเต็มรูปแบบที่สร้างการนำเสนอที่ดูเป็นมืออาชีพโดยตรงจากข้อมูล Excel

---

**สรุป:** บทแนะนำนี้แสดงวิธีที่เชื่อถือได้ในการ **แปลง Excel เป็น PowerPoint** ด้วย Aspose.Cells สำหรับ Java โดยการโหลด workbook, กำหนดค่า `PdfSaveOptions` เพื่อให้กล่องข้อความแก้ไขได้, และบันทึกด้วย `SaveFormat.PPTX` คุณจะได้ไฟล์ PowerPoint ที่มีแผนภูมิสดและรูปทรงที่แก้ไขได้ — เหมาะสำหรับการนำเสนอธุรกิจแบบไดนามิก คุณสามารถปรับโค้ดสำหรับการประมวลผลเป็นชุดหรือรวมเข้ากับโซลูชันการรายงานที่ใหญ่ขึ้นได้ตามต้องการ

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณเอง

- [วิธีสร้างแผนภูมิ Excel พร้อม Trendline และส่งออกเป็นภาพโดยใช้ Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [วิธีแปลงแผนภูมิ Excel เป็น SVG โดยใช้ Aspose.Cells ใน Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [วิธีแปลง Excel เป็น PDF ใน Java ด้วย Aspose.Cells&#58; คู่มือขั้นตอนโดยขั้นตอน](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}