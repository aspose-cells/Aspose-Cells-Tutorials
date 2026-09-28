---
category: general
date: 2026-09-27
description: วิธีส่งออกแผ่นงาน Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน Java –
  คู่มือแบบขั้นตอนต่อขั้นตอนที่ยังแสดงวิธีแปลง Excel workbook เป็นงานนำเสนอ PowerPoint
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: th
lastmod: 2026-09-27
og_description: วิธีส่งออกแผ่นงาน Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน Java.
  เรียนรู้การแปลงสมุดงาน Excel เป็นงานนำเสนอ PowerPoint พร้อมโค้ดเต็ม.
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: วิธีส่งออกแผ่นงาน Excel ไปยัง PowerPoint – คู่มือ Java กับ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: วิธีส่งออกแผ่นงาน Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน Java
url: /th/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออกแผ่นงาน Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน Java

หากคุณต้องการ **วิธีการส่งออกแผ่นงาน Excel ไปยัง PowerPoint**, บทแนะนำนี้จะให้โซลูชันที่สมบูรณ์และพร้อมใช้งาน คุณจะได้เห็นอย่างชัดเจนว่า **การแปลง Excel workbook ไปยัง PowerPoint presentation** ทำอย่างไรโดยคงไว้ซึ่งกล่องข้อความที่แก้ไขได้และการจัดรูปแบบพื้นฐาน

คู่มือสมมติว่าคุณมีสภาพแวดล้อมการพัฒนา Java ที่ทำงานได้และมีลิขสิทธิ์ Aspose.Cells for Java ที่ถูกต้อง เมื่ออ่านจบบทความคุณจะมีโปรแกรม Java ที่โหลด Excel workbook, ส่งออกแผ่นงานแรก, และเขียนไฟล์ `.pptx` ที่สามารถเปิดและแก้ไขใน Microsoft PowerPoint

## ข้อกำหนดเบื้องต้น

| ความต้องการ | ทำไมจึงสำคัญ |
|-------------|----------------|
| Java 17 หรือใหม่กว่า | Aspose.Cells รองรับ runtime ของ Java รุ่นใหม่และให้ประสิทธิภาพที่ดีกว่า |
| Aspose.Cells for Java (เวอร์ชัน 23.10 หรือใหม่กว่า) | ไลบรารีมี overload `Workbook.save(..., SaveFormat.PPTX)` ที่ใช้สำหรับการแปลง |
| สำเนาที่มีลิขสิทธิ์ของ Aspose.Cells | หากไม่มีลิขสิทธิ์ ไลบรารีจะทำงานในโหมดประเมินผลและใส่ลายน้ำ |
| ไฟล์ Excel ที่มีอย่างน้อยหนึ่งกล่องข้อความที่แก้ไขได้ | การแปลงจะคงกล่องข้อความเป็นรูปร่างที่แก้ไขได้ใน PowerPoint |
| IDE หรือเครื่องมือสร้าง (เช่น Maven, Gradle) | เพื่อคอมไพล์และรันโค้ดตัวอย่าง |

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโครงการของคุณ

หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ใน `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

สำหรับ Gradle ให้วาง snippet นี้ใน `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **เคล็ดลับ:** ประกาศ dependency ใน scope `provided` หากคุณต้องการไลบรารีเฉพาะใน runtime บนเซิร์ฟเวอร์

## ขั้นตอนที่ 2: เตรียมไฟล์ Excel workbook

สร้างไฟล์ Excel (`WorkbookWithTextbox.xlsx`) ที่มีกล่องข้อความที่แก้ไขได้บนแผ่นงานแรก คุณสามารถแทรกกล่องข้อความใน Excel ได้โดยเลือก **Insert → Text Box** บันทึกไฟล์ในโฟลเดอร์ที่สามารถอ้างอิงจาก Java ได้ เช่น `src/main/resources`

## ขั้นตอนที่ 3: เขียนโค้ดการแปลง

สร้างคลาส Java ชื่อ `ExportEditableTextbox` โค้ดด้านล่างรวมการ import ทั้งหมด, การจัดการข้อผิดพลาด, และคอมเมนต์ที่อธิบายแต่ละขั้นตอน

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

* `Workbook` แทนไฟล์ Excel ทั้งไฟล์ การโหลดจะทำการพาร์สแผ่นงาน, แผนภูมิ, และรูปร่างทั้งหมด
* `workbook.save(..., SaveFormat.PPTX)` เรียกใช้เอนจินการแปลงในตัวของ Aspose.Cells ซึ่งจะแมปเซลล์, แถว, และรูปร่างจาก Excel ไปยังสไลด์ PowerPoint พร้อมคงกล่องข้อความที่แก้ไขได้เป็นรูปร่างใน PowerPoint
* วิธีนี้จะเขียนสไลด์หนึ่งสไลด์ต่อแผ่นงาน ในตัวอย่างนี้แผ่นงานแรกจะกลายเป็นสไลด์เดียว

## ขั้นตอนที่ 4: รันโปรแกรม

คอมไพล์และรันคลาสด้วยเครื่องมือสร้างของคุณ:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

หรือ หากคุณใช้ Gradle:

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

เมื่อโปรแกรมทำงานเสร็จ ให้เปิด `Worksheet.pptx` ใน Microsoft PowerPoint คุณควรเห็นสไลด์ที่สะท้อนแผ่นงาน Excel และกล่องข้อความที่คุณสร้างใน Excel จะปรากฏเป็นรูปร่างที่แก้ไขได้โดยการดับเบิล‑คลิก

## ขั้นตอนที่ 5: จัดการหลายแผ่นงาน (ทางเลือก)

หากต้องการส่งออก **ทั้งหมด** ของแผ่นงานใน workbook ให้แทนที่การเรียกแบบแผ่นงานเดียวด้วยลูป:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

แต่ละการทำซ้ำจะสร้างไฟล์ PowerPoint แยก (`Worksheet_0.pptx`, `Worksheet_1.pptx`, …) สำหรับการนำเสนอเดียวที่มีหลายสไลด์ Aspose.Cells จะเพิ่มสไลด์ต่อแผ่นงานโดยอัตโนมัติเมื่อคุณเรียก `save` ครั้งเดียว; ไม่จำเป็นต้องเขียนโค้ดเพิ่มเติม

## กรณีขอบและแนวปฏิบัติที่ดีที่สุด

| สถานการณ์ | วิธีการที่แนะนำ |
|-----------|----------------------|
| Workbook ขนาดใหญ่ (หลายร้อย MB) | เพิ่ม heap ของ JVM (`-Xmx4g`) และพิจารณาส่งออกแผ่นงานแยกกันเพื่อหลีกเลี่ยงข้อผิดพลาด out‑of‑memory |
| Workbook ที่มีการป้องกันด้วยรหัสผ่าน | ใช้ `LoadOptions` เพื่อระบุรหัสผ่านก่อนโหลด: `new LoadOptions(LoadFormat.XLSX, "pwd")` |
| ต้องการคงสูตร Excel | PowerPoint ไม่รองรับสูตร; สูตรจะถูกแปลงเป็นค่าคงที่ในระหว่างการแปลง |
| ต้องการเลย์เอาต์สไลด์แบบกำหนดเอง | หลังการแปลง ให้จัดการไฟล์ `.pptx` ที่สร้างด้วย Aspose.Slides for Java เพื่อปรับ master สไลด์หรือเพิ่มแอนิเมชัน |
| รันในเว็บเซอร์วิส | ส่งสตรีมผลลัพธ์โดยตรงไปยัง HTTP response แทนการเขียนไฟล์: `workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## ผลลัพธ์ที่คาดหวัง

การรันตัวอย่างจะสร้างไฟล์ชื่อ `Worksheet.pptx` เปิดไฟล์ใน PowerPoint จะเห็น:

* สไลด์หนึ่งสไลด์ที่มีลักษณะตรงกับแผ่นงาน Excel แรก
* กล่องข้อความที่แก้ไขได้อยู่ในตำแหน่งเดียวกับใน Excel
* การจัดรูปแบบเซลล์พื้นฐาน (ขนาดฟอนต์, สี, เส้นขอบ) ถูกคงไว้

คอนโซลจะแสดงผล:

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## สรุป

คุณได้เรียนรู้ **วิธีการส่งออกแผ่นงาน Excel ไปยัง PowerPoint** ด้วย Aspose.Cells for Java และเข้าใจวิธี **การแปลง Excel workbook ไปยัง PowerPoint presentation** ในสถานการณ์จริง โซลูชันนี้ทำงานได้กับการส่งออกแผ่นงานเดียว, workbook หลายแผ่นงาน, และสามารถขยายต่อด้วย Aspose.Slides เพื่อปรับแต่งสไลด์เพิ่มเติมได้

---

### ขั้นตอนต่อไป

* สำรวจ **Aspose.Slides for Java** เพื่อเพิ่มแอนิเมชัน, แผนภูมิ, หรือ master สไลด์แบบกำหนดเองหลังการแปลง  
* ลองแปลง workbook ที่มีแผนภูมิ; Aspose.Cells จะเรนเดอร์แผนภูมิเป็นวัตถุแผนภูมิของ PowerPoint ที่เป็นเนทีฟ  
* ศึกษาการประมวลผลเป็นชุดโดยอ่านโฟลเดอร์ของไฟล์ Excel และสร้าง PowerPoint ต่อไฟล์

Feel free to experiment with the code, adapt the file paths, and integrate the conversion into larger Java applications such as reporting services or automated document pipelines. Happy coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}