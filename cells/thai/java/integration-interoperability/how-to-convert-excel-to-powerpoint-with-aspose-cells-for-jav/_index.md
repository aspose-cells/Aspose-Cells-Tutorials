---
category: general
date: 2026-11-22
description: เรียนรู้วิธีแปลง Excel เป็น PowerPoint ด้วย Aspose.Cells สำหรับ Java
  รวมถึงขั้นตอนการส่งออกแผนภูมิ Excel ไปยัง PowerPoint ในกระบวนการทำงานเดียว
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: th
lastmod: 2026-11-22
og_description: แปลงไฟล์ Excel เป็น PowerPoint ด้วย Aspose.Cells for Java. ทำตามบทแนะนำขั้นตอนเต็มรูปแบบนี้เพื่อส่งออกแผนภูมิ
  Excel ไปยัง PowerPoint ด้วย.
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells – คู่มือ Java
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: วิธีแปลง Excel เป็น PowerPoint ด้วย Aspose.Cells สำหรับ Java
url: /th/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแปลง Excel เป็น PowerPoint ด้วย Aspose.Cells สำหรับ Java

หากคุณต้องการ **แปลง Excel เป็น PowerPoint** คู่มือนี้จะแสดงวิธีที่ง่ายดายด้วย Aspose.Cells สำหรับ Java คุณยังจะได้เห็นวิธี **ส่งออกแผนภูมิ Excel ไปยัง PowerPoint** เป็นส่วนหนึ่งของกระบวนการเดียวกัน เพื่อให้คุณสามารถฝังแผนภูมิลงในงานนำเสนอโดยตรงโดยไม่ต้องคัดลอก‑วางด้วยตนเอง

การแปลงสเปรดชีตเป็นสไลด์เด็คเป็นเรื่องทั่วไปเมื่อคุณต้องการแบ่งปันข้อมูลเชิงลึกที่ขับเคลื่อนด้วยข้อมูลให้กับผู้ชมที่ไม่ใช่เทคนิค แทนการสร้างแผนภูมิใหม่ใน PowerPoint คุณสามารถทำอัตโนมัติทั้งหมดของกระบวนการ รักษาการจัดรูปแบบให้คงเดิม และประหยัดเวลาหลายชั่วโมง

ใน tutorial นี้คุณจะ:
* ตั้งค่า Aspose.Cells ในโครงการที่ใช้ Maven หรือ Gradle.  
* โหลดเวิร์กบุ๊กที่มีข้อมูลและแผนภูมิอยู่แล้ว.  
* กำหนดค่า `ImageOrPrintOptions` เพื่อกำหนดรูปแบบเป้าหมายเป็น PPTX.  
* บันทึกเวิร์กบุ๊กเป็นงานนำเสนอ PowerPoint.  
* ตรวจสอบผลลัพธ์และจัดการกับกรณีขอบทั่วไป.  

> **ข้อกำหนดเบื้องต้น** – คุณต้องมีใบอนุญาต Aspose.Cells สำหรับ Java ที่ถูกต้อง (หรือคุณสามารถใช้เวอร์ชันประเมินผลได้) โค้ดทำงานกับ Java 8+ และ IDE ใด ๆ ที่รองรับ Maven/Gradle.

![Diagram showing conversion of Excel to PowerPoint using Aspose.Cells](convert_excel_to_powerpoint.png)

## สิ่งที่คุณต้องการ

| Item | Reason |
|------|--------|
| **Java Development Kit (JDK) 8 หรือใหม่กว่า** | จำเป็นสำหรับการคอมไพล์และรันตัวอย่าง |
| **Maven หรือ Gradle** | ทำให้การจัดการ dependencies สำหรับ Aspose.Cells ง่ายขึ้น |
| **Aspose.Cells for Java** | ให้ API `Workbook` และ `ImageOrPrintOptions` ที่ใช้สำหรับการแปลง |
| **ไฟล์ Excel (`shapes.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิ** | แสดงสถานการณ์ *ส่งออกแผนภูมิ Excel ไปยัง PowerPoint* |

## ขั้นตอนที่ 1: เพิ่ม Aspose.Cells ไปยังโครงการของคุณ

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **ทำไมขั้นตอนนี้ถึงสำคัญ** – การเพิ่มไลบรารีทำให้คลาส `Workbook`, `ImageOrPrintOptions` และ `SaveFormat` พร้อมใช้งาน หากไม่มี dependency ที่ถูกต้อง โค้ดจะไม่คอมไพล์

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กที่มีแผนภูมิ(ๆ) อยู่

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**คำอธิบาย:**  
`Workbook` เป็นจุดเริ่มต้นสำหรับการทำงานทั้งหมดกับ Excel โดยการโหลด `shapes.xlsx` คุณจะนำตารางข้อมูลและแผนภูมิที่ฝังอยู่ทั้งหมดเข้าสู่หน่วยความจำ ทำให้การแปลงต่อไปเป็นไปได้

## ขั้นตอนที่ 3: สร้างตัวเลือกการแปลงและกำหนดรูปแบบเป้าหมายเป็น PPTX

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**ทำไมต้องใช้ `ImageOrPrintOptions`?**  
ตัวเลือกเหล่านี้ควบคุมวิธีการเรนเดอร์แต่ละแผ่นงานหรือแผนภูมิ การตั้งค่า `SaveFormat.PPTX` จะสั่งให้ไลบรารีวางแต่ละชีต (หรือแผนภูมิ) บนสไลด์ของตนเอง เพื่อรักษาความแม่นยำของภาพ

## ขั้นตอนที่ 4: บันทึกเวิร์กบุ๊กเป็นงานนำเสนอ PowerPoint

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**อะไรเกิดขึ้นที่นี่?**  
Aspose.Cells จะวนลูปผ่านแผ่นงานและแผนภูมิของเวิร์กบุ๊ก, แปลงเป็นกราฟิกที่เข้ากันได้กับสไลด์, แล้วเขียนแพ็กเกจ `.pptx` ไปยังตำแหน่งที่ระบุ ไฟล์ที่ได้สามารถเปิดได้ใน Microsoft PowerPoint, Google Slides หรือโปรแกรมดู PPTX ใด ๆ ที่รองรับ

## ขั้นตอนที่ 5: ตรวจสอบการแปลง

1. เปิด `withShapes.pptx` ใน PowerPoint.  
2. ยืนยันว่าแต่ละแผ่นงาน Excel ปรากฏเป็นสไลด์แยกกัน.  
3. ตรวจสอบว่าแผนภูมิยังคงสี, คำอธิบาย, และป้ายข้อมูลเดิม.  

หากแผนภูมิดูบิดเบี้ยว คุณอาจต้องปรับค่า DPI ของ `ImageOrPrintOptions`:

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## ส่งออกแผนภูมิ Excel ไปยัง PowerPoint – การปรับเปลี่ยนแบบเน้นจุด

บางครั้งคุณอาจต้องการย้ายแผนภูมิเดียวแทนที่จะเป็นเวิร์กบุ๊กทั้งหมด คุณสามารถทำได้โดยแปลงแผนภูมิเป็นภาพก่อนแล้วแทรกลงในสไลด์ PowerPoint ด้วยตนเอง แต่ Aspose.Cells ทำให้กระบวนการนี้ง่ายขึ้น:

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
โค้ดส่วนนี้แยกแผนภูมิเดียว, ลดขนาดไฟล์, และให้คุณควบคุมภาพที่กลายเป็นสไลด์ได้ละเอียดขึ้น นี่เป็นวิธีที่ตรงที่สุดในการ **ส่งออกแผนภูมิ Excel ไปยัง PowerPoint** เมื่อคุณไม่ต้องการเวิร์กบุ๊กเต็มรูปแบบ

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Issue | Cause | Fix |
|-------|-------|-----|
| **สไลด์ว่าง** | แผ่นงานไม่มีข้อมูลที่มองเห็นได้หรือแผนภูมิเช่นนั้นถูกซ่อน | ตรวจสอบให้แน่ใจว่าแผนภูมิมองเห็นได้และแผ่นงานมีข้อมูลก่อนบันทึก |
| **ภาพความละเอียดต่ำ** | DPI เริ่มต้นคือ 96 ซึ่งอาจไม่เพียงพอสำหรับสไลด์ที่พิมพ์ | เรียก `options.setResolution(200‑300)` ก่อน `workbook.save` |
| **ประเภทแผนภูมิที่ไม่รองรับ** | ประเภทแผนภูมิที่ใหม่หรือกำหนดเองอาจไม่แสดงผลอย่างสมบูรณ์ | ส่งออกแผนภูมิเป็นภาพ (`ImageFormat.PNG`) แล้วแทรกด้วยตนเอง |
| **ข้อผิดพลาดเส้นทางไฟล์** | เส้นทางสัมพัทธ์ไม่ถูกต้องบนระบบปฏิบัติการต่าง ๆ | ใช้ `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` เพื่อเส้นทางที่เป็นอิสระต่อแพลตฟอร์ม |

## เคล็ดลับระดับมืออาชีพสำหรับการแปลงในระดับการผลิต

* **การประมวลผลเป็นชุด:** วนลูปผ่านไดเรกทอรีของไฟล์ Excel และเรียกใช้ตรรกะการแปลงเดียวกัน.  
* **การจัดการหน่วยความจำ:** สำหรับเวิร์กบุ๊กขนาดใหญ่ ให้เรียก `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` เพื่อลดการใช้ heap.  
* **การเปิดใช้งานใบอนุญาต:** วางไฟล์ใบอนุญาตของคุณ (`Aspose.Cells.lic`) ไว้ใน classpath และเรียก `License license = new License(); license.setLicense("Aspose.Cells.lic");` ก่อนใช้ API ของ Aspose ใด ๆ.  
* **ความปลอดภัยของเธรด:** แต่ละเธรดควรทำงานกับอินสแตนซ์ `Workbook` ของตนเอง; วัตถุ Aspose.Cells ไม่ปลอดภัยต่อการใช้งานหลายเธรด.

## ตัวอย่างการทำงานเต็มรูปแบบ

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  

การรันโปรแกรมจะแสดงข้อความ `Conversion completed successfully.` และสร้างไฟล์สองไฟล์:

* `withShapes.pptx` – ชุดสไลด์ที่แต่ละแผ่นงาน (และแผนภูมิของมัน) ปรากฏบนสไลด์แยกกัน.  
* `singleChart.pptx` – งานนำเสนอแบบสไลด์เดียวที่มีเพียงแผนภูมิแรกจากเวิร์กบุ๊ก.

เปิดไฟล์เหล่านี้ใน PowerPoint เพื่อยืนยันว่าแผนภูมิยังคงสไตล์และป้ายข้อมูลเดิม

## สรุป

คุณได้เรียนรู้วิธี **แปลง Excel เป็น PowerPoint** ด้วย Aspose.Cells สำหรับ Java แล้ว และคุณยังได้เห็นวิธีที่มีประสิทธิภาพที่สุดในการ **ส่งออกแผนภูมิ Excel ไปยัง PowerPoint** เมื่อต้องการภาพเฉพาะเท่านั้น โดยการกำหนดค่า `ImageOrPrintOptions` และตั้งค่า `SaveFormat` เป็น `PPTX` ไลบรารีจะทำงานหนักในการเรนเดอร์แผ่นงานและแผนภูมิให้เป็นกราฟิกที่เข้ากันได้กับสไลด์

จากนี้คุณสามารถ:
* ทำการแปลงเป็นชุดอัตโนมัติสำหรับกระบวนการรายงาน.  
* รวม PPTX ที่สร้างขึ้นกับสไลด์อื่น ๆ ด้วย Apache POI `XSLF` API.  
* สำรวจรูปแบบการส่งออกเพิ่มเติมเช่น PDF หรือ HTML สำหรับการกระจายหลายช่องทาง.

คุณสามารถทดลองปรับค่าการตั้งค่า DPI, รูปแบบสไลด์ที่กำหนดเอง, หรือฝัง PPTX ที่สร้างขึ้นในกระบวนการทำงานของอีเมลได้ตามต้องการ. ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณเอง.

- [วิธีส่งออกแผ่นงาน Excel ไปยัง PowerPoint ด้วย Aspose.Cells ใน Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [วิธีแปลง Excel เป็น PDF ใน Java ด้วย Aspose.Cells: คู่มือขั้นตอนโดยละเอียด](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [วิธีส่งออกแผนภูมิเป็น docx จาก Excel ด้วย Aspose.Cells สำหรับ Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}