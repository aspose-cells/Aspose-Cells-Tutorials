---
category: general
date: 2026-06-27
description: วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint ด้วย Java. เรียนรู้การแปลงสเปรดชีตเป็น
  PowerPoint, บันทึกไฟล์ PPTX, และส่งออกข้อมูล Excel ไปยัง PPT อย่างง่ายดาย.
draft: false
keywords:
- how to export charts
- convert spreadsheet to powerpoint
- how to save pptx
- excel to powerpoint slide
- export excel data ppt
language: th
og_description: วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint ด้วย Java คู่มือขั้นตอนต่อขั้นตอนนี้จะแสดงวิธีแปลงสเปรดชีตเป็น
  PowerPoint, บันทึกไฟล์ PPTX, และส่งออกข้อมูล Excel ไปเป็น PPT.
og_title: วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint – บทเรียน Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  headline: How to Export Charts from Excel to PowerPoint – Full Java Guide
  type: TechArticle
- description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  name: How to Export Charts from Excel to PowerPoint – Full Java Guide
  steps:
  - name: '**Load** the workbook you want to transform.'
    text: '**Load** the workbook you want to transform.'
  - name: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
    text: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
  - name: '**Save** the workbook using the `PPTX` format and the options you configured.'
    text: '**Save** the workbook using the `PPTX` format and the options you configured.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
title: วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint – คู่มือ Java ฉบับเต็ม
url: /th/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint – คู่มือ Java ฉบับเต็ม

เคยสงสัย **วิธีส่งออกแผนภูมิ** จากเวิร์กบุ๊ก Excel ไปยังสไลด์ PowerPoint โดยตรงหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักต้องแปลงสเปรดชีตที่ขับเคลื่อนด้วยข้อมูลให้เป็นชุดสไลด์พร้อมนำเสนอโดยไม่ต้องคัดลอก‑วางด้วยตนเองในแบบอันน่าหนักใจ ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันเชิงโปรแกรมที่สะอาดตา ซึ่งทำให้คุณ **แปลงสเปรดชีตเป็น PowerPoint**, บันทึกผลลัพธ์เป็นไฟล์ PPTX, และแม้แต่ปรับแต่งการจัดการแผนภูมิได้แบบเรียลไทม์

สิ่งที่คุณจะได้คือโค้ดสแนป Java ที่พร้อมรันซึ่งรับเวิร์กบุ๊กใดก็ได้ ดึงแผนภูมิของมัน (และอ็อบเจกต์ OLE หากต้องการ) แล้วสร้างไฟล์ **excel to powerpoint slide** ที่เรียบหรูออกมา ไม่มี UI เพิ่มเติม ไม่มี VBA ที่ยุ่งยาก เพียงแค่โค้ด Java แท้ที่คุณสามารถนำไปใส่ในโปรเจคของคุณได้ทันที

## ข้อกำหนดเบื้องต้น

- **Java 17** หรือใหม่กว่า (API ทำงานบน JDK ล่าสุดใดก็ได้)
- **Aspose.Cells for Java** ไลบรารี (โค้ดใช้ `PresentationOptions` และ `SaveFormat.PPTX`)
- ความเข้าใจพื้นฐานเกี่ยวกับการตั้งค่าโปรเจค Java (Maven/Gradle)
- ไฟล์ Excel (`.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิที่คุณต้องการส่งออก

หากคุณยังไม่มี JAR ของ Aspose.Cells ให้เพิ่มผ่าน Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

หรือดาวน์โหลด JAR โดยตรงจากเว็บไซต์ Aspose แล้ววางไว้ใน classpath ของคุณ

## วิธีส่งออกแผนภูมิ – ภาพรวม

โดยสรุปขั้นตอนคือ:

1. **Load** เวิร์กบุ๊กที่คุณต้องการแปลง
2. **Configure** อินสแตนซ์ `PresentationOptions` เพื่อบอก Aspose ว่าองค์ประกอบใด (แผนภูมิ, อ็อบเจกต์ OLE ฯลฯ) ควรรวมอยู่ในชุดสไลด์
3. **Save** เวิร์กบุ๊กโดยใช้รูปแบบ `PPTX` พร้อมตัวเลือกที่คุณกำหนด

เท่านั้นเอง ไลบรารีทำหน้าที่หนักทั้งหมด—เรนเดอร์แต่ละแผนภูมิเป็นกราฟิกเวกเตอร์, รักษาเลย์เอาต์, และสร้างไฟล์ PowerPoint ที่ PowerPoint เองสามารถเปิดได้โดยไม่มีข้อบกพร่อง

ต่อไปเราจะแยกแต่ละขั้นตอน, อธิบาย *เหตุผล* ที่สำคัญ, และแสดงโค้ดที่คุณต้องการอย่างแม่นยำ

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กและกำหนดตัวเลือกการส่งออก

ก่อนอื่น เราต้องบอก Aspose ว่าจะรวมอะไรบ้างเมื่อสร้าง PowerPoint คลาส `PresentationOptions` ให้การควบคุมที่ละเอียดอ่อน การตั้งค่า `setExportCharts(true)` ทำให้ทุกแผนภูมิกลายเป็นองค์ประกอบของสไลด์, ส่วน `setExportOleObjects(true)` จะนำอ็อบเจกต์ที่ฝังอยู่ (เช่น ตาราง Excel) ที่คุณอาจมีเข้ามา

```java
import com.aspose.cells.*;

public class ExcelToPowerPointExporter {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source Excel workbook
        // -------------------------------------------------
        String srcPath = "C:/data/sourceWorkbook.xlsx";
        Workbook workbook = new Workbook(srcPath);

        // -------------------------------------------------
        // 2️⃣ Configure presentation export options
        // -------------------------------------------------
        PresentationOptions presentationOptions = new PresentationOptions();
        presentationOptions.setExportCharts(true);          // <-- how to export charts
        presentationOptions.setExportOleObjects(true);     // include embedded OLE objects

        // The next lines are optional but often useful:
        presentationOptions.setExportFormulas(false);      // skip raw formulas if you only need visuals
        presentationOptions.setExportImages(true);         // grab any pictures as well
```

**ทำไมขั้นตอนนี้สำคัญ:**  
หากคุณข้าม `setExportCharts(true)`, Aspose จะถือแผนภูมิเป็นเซลล์ปกติ, ทำให้ข้อมูลของมันถูกใส่ลงในสไลด์แทนที่จะแสดงเป็นแผนภูมิภาพ ซึ่งทำให้วัตถุประสงค์ของการนำเสนอเสียไป เช่นเดียวกัน การเปิด/ปิดการส่งออก OLE จะทำให้คุณสามารถเก็บอ็อบเจกต์ซับซ้อน (เช่น pivot table) ได้โดยไม่ต้องเขียนโค้ดเพิ่มเติม

> **เคล็ดลับ:** เมื่อทำงานกับเวิร์กบุ๊กขนาดใหญ่, พิจารณาปิด `setExportFormulas` เพื่อเร่งการแปลง ผลลัพธ์ภาพยังคงเหมือนเดิม แต่กระบวนการใช้หน่วยความจำน้อยลง

## ขั้นตอนที่ 2: บันทึกเวิร์กบุ๊กเป็นไฟล์ PowerPoint

เมื่อกำหนดตัวเลือกเรียบร้อยแล้ว การแปลงจริงเป็นเพียงบรรทัดเดียว: เรียก `workbook.save(...)` พร้อม enum `SaveFormat.PPTX` นี่คือส่วนที่เราตอบ **วิธีบันทึก pptx** ใน Java

```java
        // -------------------------------------------------
        // 3️⃣ Save the workbook as a PowerPoint file
        // -------------------------------------------------
        String outPath = "C:/output/slide.pptx";
        workbook.save(outPath, SaveFormat.PPTX, presentationOptions);

        System.out.println("✅ Conversion complete! Check " + outPath);
    }
}
```

**อะไรเกิดขึ้นภายใน?**  
Aspose จะวนผ่านแต่ละแผ่นงาน, ดึงทุกแผนภูมิ, แปลงเป็นรูปร่าง PowerPoint (โดยทั่วไปเป็นเวกเตอร์ EMF) และวางลงบนสไลด์ใหม่ หากคุณมีหลายแผ่นงาน, โดยค่าเริ่มต้นแต่ละแผ่นงานจะได้สไลด์ของตนเอง คุณสามารถจัดเรียงสไลด์ใหม่ได้ภายหลังโดยใช้ Apache POI หรือ PowerPoint เอง

### ผลลัพธ์ที่คาดหวัง

เปิด `slide.pptx` ใน Microsoft PowerPoint, คุณควรเห็น:

- หนึ่งสไลด์ต่อแผ่นงาน (หรือต่อแผนภูมิ ขึ้นอยู่กับแหล่งข้อมูลของคุณ)
- แผนภูมิแสดงอย่างคมชัด, รักษาสีและป้ายข้อมูล
- อ็อบเจกต์ OLE ใด ๆ (เช่น ตาราง Excel ที่ฝังอยู่) ปรากฏเป็นอ็อบเจกต์ที่แก้ไขได้

หากคุณไม่เห็นแผนภูมิ, ตรวจสอบอีกครั้งว่าเวิร์กบุ๊กต้นทางมีอ็อบเจกต์แผนภูมิจริง ๆ และว่า `setExportCharts(true)` ไม่ถูกเขียนทับที่อื่น

## ทางเลือก: ส่งออกแผนภูมิเดียวเป็นไฟล์ PPTX แยกอิสระ

บางครั้งคุณอาจต้องการ **excel to powerpoint slide** เฉพาะแผนภูมิหนึ่ง ไม่ใช่ทั้งเวิร์กบุ๊ก คุณสามารถทำได้โดยสร้างเวิร์กบุ๊กชั่วคราวที่มีเพียงแผนภูมิที่ต้องการเท่านั้น

```java
        // -------------------------------------------------
        // 4️⃣ Export a single chart (optional)
        // -------------------------------------------------
        // Assume the chart is on the first worksheet, first chart
        Worksheet sheet = workbook.getWorksheets().get(0);
        int chartIndex = 0; // change if you have multiple charts
        Chart chart = sheet.getCharts().get(chartIndex);

        // Clone the chart into a new workbook
        Workbook singleChartWb = new Workbook();
        Worksheet newSheet = singleChartWb.getWorksheets().get(0);
        newSheet.getCharts().addCopy(chart);

        // Use the same PresentationOptions
        singleChartWb.save("C:/output/singleChart.pptx", SaveFormat.PPTX, presentationOptions);
```

**ทำไมคุณอาจต้องการแบบนี้:**  
หากคุณกำลังสร้างชุดสไลด์แบบเรียลไทม์ (เช่น บริการรายงานที่ส่งแผนภูมิหนึ่งต่ออีเมล), การสร้างเวิร์กบุ๊กขนาดเล็กจะลดการใช้หน่วยความจำและเร่งความเร็วการทำงาน

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ปัญหา | อาการ | วิธีแก้ |
|-------|---------|-----|
| หายไปของแผนภูมิ | สไลด์เป็นค่าว่างหรือมีเฉพาะตารางข้อมูล | ตรวจสอบว่าได้เรียก `presentationOptions.setExportCharts(true)` **ก่อน** `workbook.save`. |
| ขนาดไฟล์ใหญ่ | PPTX > 30 MB สำหรับแผนภูมิไม่กี่ชิ้น | ปิดการส่งออกภาพ (`setExportImages(false)`) หรือบีบอัดภาพใน PowerPoint หลังการสร้าง |
| ไม่มีอ็อบเจกต์ OLE | ตาราง Excel ที่ฝังอยู่กลายเป็นภาพคงที่ | ตั้งค่า `setExportOleObjects(true)`; ตรวจสอบว่าอ็อบเจกต์ OLE ต้นทางไม่ได้ถูกป้องกัน |
| ข้อผิดพลาดความเข้ากันได้ | PowerPoint แจ้งว่าไฟล์เสียหาย | ใช้เวอร์ชันล่าสุดของ Aspose.Cells; เวอร์ชันเก่าอาจมีบั๊กในการสร้าง PPTX |

## วิธีส่งออกแผนภูมิใน CI/CD Pipeline

หากคุณทำอัตโนมัติการสร้างรายงานเป็นส่วนหนึ่งของการสร้าง (build), คุณสามารถฝังโค้ดข้างต้นลงในปลั๊กอิน Maven หรืองาน Gradle ได้ เพียงตรวจสอบว่า JVM มี heap เพียงพอ (เช่น `-Xmx2g`) เมื่อต้องประมวลผลเวิร์กบุ๊กขนาดใหญ่

```groovy
task exportCharts(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = 'com.example.ExcelToPowerPointExporter'
    args = []
    jvmArgs = ['-Xmx2g']
}
```

การรัน `./gradlew exportCharts` จะสร้างไฟล์ PPTX โดยไม่มีการแทรกแซงด้วยมือ—เหมาะสำหรับงานรายงานประจำคืน

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นคลาส Java ที่สมบูรณ์และเป็นอิสระซึ่งคุณสามารถวางลงใน IDE ใดก็ได้ มันรวมการ import ทั้งหมด, การจัดการข้อผิดพลาด, และคอมเมนต์ที่อธิบายแต่ละบรรทัด

```java
// FullExample.java
import com.aspose.cells.*;

public class FullExample {
    public static void main(String[] args) {
        try {
            // 👉 1️⃣ Load the Excel workbook you want to convert
            String srcFile = "C:/data/analysis.xlsx";
            Workbook wb = new Workbook(srcFile);

            // 👉 2️⃣ Set up export options – this is the core of how to export charts
            PresentationOptions opts = new PresentationOptions();
            opts.setExportCharts(true);          // include every chart
            opts.setExportOleObjects(true);     // keep OLE objects (tables, etc.)
            opts.setExportImages(true);         // optionally keep pictures
            opts.setExportFormulas(false);      // skip formulas for speed

            // 👉 3️⃣ Choose where the PPTX will be saved – answer to how to save pptx
            String outFile = "C:/output/analysis.pptx";

            // 👉 4️⃣ Perform the conversion
            wb.save(outFile, SaveFormat.PPTX, opts);

            System.out.println("✅ Excel file converted to PowerPoint successfully!");
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

รันคลาส, เปิด `analysis.pptx`, แล้วคุณจะเห็นทุกแผนภูมิจากสเปรดชีตต้นฉบับของคุณอยู่ในชุด PowerPoint อย่างสมบูรณ์ นั่นคือสาระของ **export excel data ppt**—ไม่มีขั้นตอนด้วยมือ, ไม่มีข้อผิดพลาดจากการคัดลอก‑วาง

## สรุปภาพรวม

![แผนภาพแสดงวิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint ด้วย Aspose.Cells](/images/export-charts-diagram.png "วิธีส่งออกแผนภูมิจาก Excel ไปยัง PowerPoint")

*ภาพประกอบข้างต้นแสดงการไหลจากเวิร์กบุ๊ก Excel → PresentationOptions → ไฟล์ PPTX.*

## สรุป

เราได้อธิบาย **วิธีส่งออกแผนภูมิ** จาก Excel ไปยัง PowerPoint ด้วย Java, แสดงโค้ดที่คุณต้องการเพื่อ **แปลงสเปรดชีตเป็น PowerPoint**, และอธิบาย **วิธีบันทึกไฟล์ pptx** อย่างเชื่อถือได้ โดยการปรับ `PresentationOptions` คุณสามารถควบคุมทุกอย่างตั้งแต่การรวมแผนภูมิจนถึงการจัดการอ็อบเจกต์ OLE, ทำให้คุณมีสะพานที่ยืดหยุ่นระหว่างการวิเคราะห์ข้อมูลและชั้นนำเสนอ

ขั้นตอนต่อไป? ลองรวมการแปลงนี้กับ **Apache POI** เพื่อจัดเรียงสไลด์โดยโปรแกรม, หรือฝังฟังก์ชันนี้ใน microservice ของ Spring Boot ที่ให้บริการรายงาน PPTX ตามความต้องการ คุณยังสามารถสำรวจการส่งออกเป็น **PDF** หรือ **HTML** ด้วยไลบรารีเดียวกัน—Aspose.Cells ทำให้ทำได้ง่าย

มีคำถามเกี่ยวกับกรณีขอบเขตหรือไม่,

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจคของคุณ

- [How to Create and Export Charts in Java Using Aspose.Cells&#58; A Complete Guide](/cells/english/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java&#58; Custom Page Sizes Guide](/cells/english/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}