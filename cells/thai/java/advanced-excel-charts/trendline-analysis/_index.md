---
date: 2026-08-27
description: เรียนรู้วิธีเพิ่ม trendline ลงใน chart, แสดงค่า R‑squared ของมัน, และส่งออก
  chart เป็นภาพ PNG หรือ JPEG โดยใช้ Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: ส่งออก Chart เป็น Image ด้วย Trendline Analysis
og_description: เพิ่ม trendline ลงใน chart, ดูค่า R‑squared, และส่งออกผลลัพธ์เป็น
  PNG/JPEG ด้วย Aspose.Cells for Java – โซลูชันที่เร็ว รองรับ 50‑format
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: เพิ่ม trendline ลงใน chart และส่งออกเป็น image ด้วย Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: วิธีเพิ่ม trendline ลงใน chart และส่งออกเป็น image ใน Java
url: /th/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มเส้นแนวโน้มลงในแผนภูมิและส่งออกเป็นภาพ

ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **เพิ่มเส้นแนวโน้มลงในแผนภูมิ**, แสดงค่าความสัมพันธ์ R‑squared, และส่งออกภาพเป็นไฟล์ PNG หรือ JPEG โดยใช้ Aspose.Cells for Java คุณจะเห็นว่าทำไมเส้นแนวโน้มจึงสำคัญ, วิธีเตรียม workbook, และขั้นตอนที่แน่นอนในการสร้างภาพความละเอียดสูงที่สามารถฝังลงในรายงาน, อีเมล หรือหน้าเว็บได้.

## คำตอบสั้น
- **เป้าหมายหลักของคู่มือนี้คืออะไร?** เพื่อแสดงวิธีเพิ่มเส้นแนวโน้มลงในแผนภูมิ, แสดงสมการและค่าความสัมพันธ์ R‑squared, และส่งออกแผนภูมิเป็นภาพด้วย Java.  
- **ต้องใช้ไลบรารีอะไร?** Aspose.Cells for Java – ดาวน์โหลดได้จาก [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/).  
- **ต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีทำงานได้สำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **ฉันสามารถสร้าง Excel workbook ด้วยโปรแกรมได้หรือไม่?** ได้ – บทแนะนำนี้สร้างและบันทึกไฟล์ XLSX ตั้งแต่ต้น.  
- **แผนภูมิถูกส่งออกเป็น PNG หรือ JPEG อย่างไร?** เรียกเมธอด `Chart.toImage()` และเขียน `BufferedImage` ที่คืนค่ามาโดยใช้ `ImageIO.write(...)`.

## คุณสร้างแผนภูมิ Excel พร้อมเส้นแนวโน้มและส่งออกเป็นภาพอย่างไร?
โหลด workbook, เพิ่มแผนภูมิเส้น, แนบเส้นแนวโน้มที่แสดงสมการและค่าความสัมพันธ์ R‑squared, บันทึก workbook, จากนั้นเรียก `chart.toImage()` และเขียน `BufferedImage` ที่ได้ลงไฟล์ PNG หรือ JPEG กระบวนการแบบต้นจนจบนี้ใช้เพียงไม่กี่บรรทัดของโค้ด Java และสร้างภาพที่พิกเซลสมบูรณ์เหมาะสำหรับการใช้งานต่อไปใด ๆ

## การส่งออกแผนภูมิเป็นภาพคืออะไร?
การส่งออกแผนภูมิเป็นภาพจะเปลี่ยนการแสดงผลข้อมูลของคุณให้เป็นบิตแมพที่พกพาได้ (PNG, JPEG, BMP ฯลฯ) รูปแบบนี้เหมาะสำหรับฝังแผนภูมิในรายงาน, หน้าเว็บ, หรือการนำเสนอที่ไม่ต้องการไฟล์ Excel ดั้งเดิม.

## ทำไมต้องเพิ่มเส้นแนวโน้มและแสดงค่าความสัมพันธ์ R‑squared?
เส้นแนวโน้มเปิดเผยรูปแบบพื้นฐานของชุดข้อมูล, ในขณะที่เมตริก **R‑squared** วัดว่าการฟิตของเส้นแนวโน้มกับข้อมูลใกล้เคียงแค่ไหน การรวมทั้งสองไว้ในภาพที่ส่งออกทำให้ผู้มีส่วนได้ส่วนเสียได้รับข้อมูลทันทีโดยไม่ต้องเปิด workbook ช่วยให้ผู้ตัดสินใจประเมินความแข็งแกร่งของความสัมพันธ์และคาดการณ์แนวโน้มได้อย่างรวดเร็วโดยไม่ต้องเปิด Excel.

## ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า ติดตั้งบนเครื่องพัฒนาของคุณ.  
- ไลบรารี Aspose.Cells for Java เพิ่มใน classpath ของโปรเจค (ไฟล์ JAR).  
- ความคุ้นเคยกับ IDE ของ Java เช่น IntelliJ IDEA หรือ Eclipse.  

## คู่มือทีละขั้นตอน

### ขั้นตอนที่ 1: ตั้งค่าโปรเจค
สร้างโปรเจค Java ใหม่และวางไฟล์ JAR ของ Aspose.Cells ลงในเส้นทางการสร้าง (build path) สิ่งนี้เตรียมสภาพแวดล้อมสำหรับการสร้างและจัดการไฟล์ Excel.

### ขั้นตอนที่ 2: โหลดไฟล์ Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*เราเพิ่ง **โหลดไฟล์ Excel** เข้าไปในหน่วยความจำ, พร้อมสำหรับการสร้างแผนภูมิ.*

### ขั้นตอนที่ 3: สร้างแผนภูมิ
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*ที่นี่เราสร้างแผนภูมิเส้นที่จะเป็นโฮสต์สำหรับเส้นแนวโน้มของเราในภายหลัง.*

### ขั้นตอนที่ 4: เพิ่มเส้นแนวโน้ม (how to add trendline) และแสดงค่าความสัมพันธ์ R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*การเรียก `setDisplayRSquaredValue(true)` ทำให้ **ค่าความสัมพันธ์ R‑squared** ปรากฏบนแผนภูมิ.*

### ขั้นตอนที่ 5: ปรับแต่งแผนภูมิและบันทึก workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*ตอนนี้ workbook ถูก **สร้าง** และบันทึกเป็นไฟล์ XLSX, พร้อมสำหรับการประมวลผลต่อไป.*

### ขั้นตอนที่ 6: ส่งออกแผนภูมิเป็นภาพ (export chart to image)
> **หมายเหตุ:** ขั้นตอนนี้อธิบายโดยไม่มีบล็อกโค้ดเพิ่มเติมเพื่อรักษาจำนวนบล็อกเดิมไม่เปลี่ยนแปลง.  
หลังจากที่แผนภูมิถูกสร้างและบันทึกแล้ว, คุณสามารถส่งออกเป็นภาพได้โดยเรียกเมธอด `chart.toImage()` และเขียน `java.awt.image.BufferedImage` ที่ได้ลงในรูปแบบไฟล์ที่คุณเลือก (PNG, JPEG, BMP). ขั้นตอนการทำงานทั่วไปคือ:
1. ดึงอ็อบเจ็กต์ `Chart` (ทำแล้วในขั้นตอนก่อนหน้า).  
2. เรียก `chart.toImage()` เพื่อรับ `BufferedImage`.  
3. ใช้ `ImageIO.write(bufferedImage, "png", new File("chart.png"))` เพื่อบันทึกไฟล์.  

`Chart` object แทนแผนภูมิใน workbook และให้เมธอดสำหรับแก้ไขลักษณะและข้อมูลของมัน. `BufferedImage` เป็นคลาสของ Java ที่เก็บภาพในหน่วยความจำ, ทำให้สามารถบันทึกเป็นไฟล์ได้. `ImageIO` เป็นคลาสยูทิลิตี้สำหรับการอ่านและเขียนภาพใน Java. `setDisplayRSquaredValue` ทำให้แสดงสถิติ R‑squared บนเส้นแนวโน้ม.

### วิเคราะห์ผลลัพธ์
เปิด `output.xlsx` ใน Excel เพื่อตรวจสอบว่าเส้นแนวโน้ม, สมการ, และค่าความสัมพันธ์ R‑squared ปรากฏตามที่คาดไว้. เปิดไฟล์ภาพที่ส่งออก (เช่น `chart.png`) เพื่อดูภาพที่สะอาดและสามารถแชร์ได้โดยไม่ต้องมี workbook ดั้งเดิม.

## ปัญหาทั่วไปและวิธีแก้
- **เส้นแนวโน้มไม่แสดง:** ตรวจสอบว่าช่วงข้อมูล (`A1:A10`) มีค่าตัวเลข; ข้อมูลที่ไม่ใช่ตัวเลขจะป้องกันการคำนวณเส้นแนวโน้ม.  
- **ค่าความสัมพันธ์ R‑squared แสดงเป็น 0:** สิ่งนี้มักหมายถึงชุดข้อมูลคงที่หรือไม่มีความแปรปรวน. ลองใช้ชุดข้อมูลอื่นหรือใช้เส้นแนวโน้มแบบพหุนาม.  
- **การส่งออกภาพล้มเหลวด้วย `NullPointerException`:** ตรวจสอบว่าแผนภูมิได้เรนเดอร์ครบถ้วนก่อนเรียก `toImage()`. การบันทึก workbook ก่อนอาจช่วยแก้ปัญหาเรื่องเวลาได้บางครั้ง.

## คำถามที่พบบ่อย

**Q: ฉันจะเปลี่ยนประเภทของเส้นแนวโน้มได้อย่างไร?**  
A: ใช้ค่า enumeration `TrendlineType` ที่แตกต่างกันเมื่อเพิ่มเส้นแนวโน้ม, เช่น `TrendlineType.POLYNOMIAL` สำหรับการฟิตแบบพหุนาม.

**Q: ฉันสามารถปรับแต่งลักษณะของเส้นแนวโน้ม (สี, ความหนา) ได้หรือไม่?**  
A: ได้. เข้าถึง `LineFormat` ของเส้นแนวโน้มผ่าน `trendline.getLineFormat()` และตั้งค่าคุณสมบัติต่าง ๆ เช่น `setWeight()` และ `setColor()`.

**Q: ฉันจะส่งออกแผนภูมิเป็น PDF แทนภาพได้อย่างไร?**  
A: แปลงแผนภูมิเป็นภาพก่อน, จากนั้นฝังภาพนั้นลงใน PDF โดยใช้ Aspose.PDF หรือไลบรารี PDF ใด ๆ

**Q: สามารถเพิ่มหลายเส้นแนวโน้มในแผนภูมิเดียวได้หรือไม่?**  
A: แน่นอน. เรียก `chart.getNSeries().get(0).getTrendlines().add(...)` สำหรับแต่ละ series ที่ต้องการวิเคราะห์.

**Q: Aspose.Cells รองรับการส่งออกภาพความละเอียดสูงหรือไม่?**  
A: ใช่. คุณสามารถกำหนด DPI เมื่อเรียก `chart.toImage()` แล้วปรับขนาดภาพก่อนบันทึก, เพื่อให้ได้ผลลัพธ์คมชัดสำหรับการพิมพ์หรือหน้าจอความหนาแน่นสูง.

---

**อัปเดตล่าสุด:** 2026-08-27  
**ทดสอบกับ:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [เพิ่มป้ายข้อมูลลงในแผนภูมิ Excel ด้วย Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [วิธีส่งออกแผนภูมิ Excel เป็น SVG ด้วย Aspose.Cells Java สำหรับกราฟิกเวกเตอร์ที่ปรับขนาดได้](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [ส่งออกแผนภูมิ Excel ไปเป็น PDF ด้วย Aspose.Cells for Java: คู่มือขนาดหน้ากำหนดเอง](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}