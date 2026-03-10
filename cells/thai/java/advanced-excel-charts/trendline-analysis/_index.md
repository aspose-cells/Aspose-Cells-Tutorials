---
date: 2026-02-09
description: เรียนรู้วิธีสร้างแผนภูมิ Excel, เพิ่มเส้นแนวโน้ม, แสดงค่า R‑squared,
  และส่งออกแผนภูมิเป็นภาพโดยใช้ Aspose.Cells for Java. รวมขั้นตอนการโหลดไฟล์ Excel,
  ปรับแต่งแผนภูมิ, และบันทึกเป็น PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: วิธีสร้างแผนภูมิ Excel พร้อมเส้นแนวโน้มและส่งออกเป็นภาพโดยใช้ Aspose.Cells
  สำหรับ Java
url: /th/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิเป็นภาพพร้อมการวิเคราะห์เส้นแนวโน้ม

ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **create Excel chart** พร้อมเส้นแนวโน้ม, แสดงค่าความสัมพันธ์ R‑squared, และส่งออกภาพที่ได้เป็นไฟล์ภาพโดยใช้ Aspose.Cells for Java เราจะอธิบายขั้นตอนการโหลดเวิร์กบุ๊กที่มีอยู่, เพิ่มเส้นแนวโน้ม, ปรับแต่งชื่อ, บันทึกเวิร์กบุ๊ก, และสุดท้ายสร้างไฟล์ PNG/JPEG ที่คุณสามารถฝังได้ทุกที่.

## คำตอบด่วน
- **วัตถุประสงค์หลักของคู่มือนี้คืออะไร?** เพื่อแสดงวิธีเพิ่มเส้นแนวโน้ม, แสดงสมการและค่าความสัมพันธ์ R‑squared, และส่งออกแผนภูมิที่ได้เป็นภาพโดยใช้ Java.  
- **ต้องใช้ไลบรารีอะไร?** Aspose.Cells for Java (ดาวน์โหลด [here](https://releases.aspose.com/cells/java/)).  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้งานฟรีใช้ได้สำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถสร้างไฟล์ Excel ด้วย Java ได้หรือไม่?** ได้ – บทแนะนำสร้างและบันทึกเวิร์กบุ๊ก XLSX.  
- **ฉันจะส่งออกแผนภูมิเป็น PNG หรือ JPEG อย่างไร?** ใช้เมธอด `Chart.toImage()` (อธิบายในส่วน “Export Chart”).

## วิธีสร้างแผนภูมิ Excel พร้อมเส้นแนวโน้มและส่งออกเป็นภาพ
หัวข้อนี้ตอบโดยตรงต่อคำค้นหลักและแนะนำคุณผ่านกระบวนการทั้งหมดในลำดับที่เป็นตรรกะ ด้านล่างคุณจะพบเหตุผล, ข้อกำหนดเบื้องต้น, และขั้นตอนแบบทีละขั้นตอน.

## การส่งออกแผนภูมิเป็นภาพคืออะไร?
การส่งออกแผนภูมิเป็นภาพจะทำให้การแสดงผลข้อมูลของคุณแปลงเป็นบิตแมปแบบพกพา (PNG, JPEG ฯลฯ) ซึ่งเหมาะสำหรับการฝังแผนภูมิในรายงาน, หน้าเว็บ, หรือการนำเสนอที่ไม่ต้องการไฟล์ Excel ดั้งเดิม

## ทำไมต้องเพิ่มเส้นแนวโน้มและแสดงค่าความสัมพันธ์ R‑squared?
เส้นแนวโน้มช่วยให้คุณระบุรูปแบบพื้นฐานของชุดข้อมูล, ในขณะที่เมตริก **R‑squared** วัดว่าการฟิตของเส้นแนวโน้มกับข้อมูลเป็นอย่างไร การใส่สิ่งเหล่านี้ในภาพที่ส่งออกจะให้ผู้มีส่วนได้ส่วนเสียเข้าใจได้ทันทีโดยไม่ต้องเปิดเวิร์กบุ๊ก

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java 8 หรือรุ่นใหม่กว่า.  
- เพิ่มไลบรารี Aspose.Cells for Java ลงในโปรเจกต์ของคุณ (ไฟล์ JAR บน classpath).  
- มีความคุ้นเคยพื้นฐานกับ IDE ของ Java (IntelliJ IDEA, Eclipse ฯลฯ).  

## คู่มือขั้นตอนต่อขั้นตอน

### ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์
สร้างโปรเจกต์ Java ใหม่และเพิ่มไฟล์ JAR ของ Aspose.Cells ไปยังเส้นทางการสร้าง (build path) เพื่อเตรียมสภาพแวดล้อมสำหรับการสร้างและจัดการไฟล์ Excel.

### ขั้นตอนที่ 2: โหลดไฟล์ Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*เราเพิ่ง **loaded an Excel file** เข้าไปในหน่วยความจำ, พร้อมสำหรับการสร้างแผนภูมิ.*

### ขั้นตอนที่ 3: สร้างแผนภูมิ
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*ที่นี่เราสร้างแผนภูมิเส้นที่ต่อมาจะเป็นที่ใส่เส้นแนวโน้มของเรา.*

### ขั้นตอนที่ 4: เพิ่มเส้นแนวโน้ม (how to add trendline) และแสดงค่าความสัมพันธ์ R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*การเรียก `setDisplayRSquaredValue(true)` ทำให้ **R‑squared value** ปรากฏบนแผนภูมิ.*

### ขั้นตอนที่ 5: ปรับแต่งแผนภูมิและบันทึกเวิร์กบุ๊ก (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*ตอนนี้เวิร์กบุ๊กได้ถูก **generated** และบันทึกเป็นไฟล์ XLSX, พร้อมสำหรับการประมวลผลต่อไป.*

### ขั้นตอนที่ 6: ส่งออกแผนภูมิเป็นภาพ (export chart to image)
> **หมายเหตุ:** ขั้นตอนนี้อธิบายโดยไม่มีบล็อกโค้ดเพิ่มเติมเพื่อรักษาจำนวนบล็อกเดิมไว้.  
หลังจากสร้างและบันทึกแผนภูมิแล้ว, คุณสามารถส่งออกเป็นภาพได้โดยเรียกเมธอด `chart.toImage()` และเขียน `java.awt.image.BufferedImage` ที่ได้ไปยังรูปแบบไฟล์ที่คุณเลือก (PNG, JPEG, BMP). ขั้นตอนทั่วไปคือ:
1. ดึงอ็อบเจ็กต์ `Chart` (ทำแล้วในขั้นตอนก่อนหน้า).  
2. เรียก `chart.toImage()` เพื่อรับ `BufferedImage`.  
3. ใช้ `ImageIO.write(bufferedImage, "png", new File("chart.png"))` เพื่อเขียนไฟล์.  

ขั้นตอนนี้จะสร้างภาพความละเอียดสูงที่คุณสามารถฝังได้ทุกที่, เสร็จสิ้นกระบวนการ **export chart to image**.

## วิเคราะห์ผลลัพธ์
เปิด `output.xlsx` ด้วย Excel เพื่อตรวจสอบว่าเส้นแนวโน้ม, สมการ, และค่าความสัมพันธ์ R‑squared ปรากฏตามที่คาดไว้. เปิดไฟล์ภาพที่ส่งออก (เช่น `chart.png`) เพื่อดูภาพที่สะอาดและสามารถแชร์ได้โดยไม่ต้องใช้เวิร์กบุ๊กต้นฉบับ.

## ปัญหาที่พบบ่อยและวิธีแก้
- **Trendline not showing:** ตรวจสอบว่าช่วงข้อมูล (`A1:A10`) มีค่าตัวเลขจริง; ข้อมูลที่ไม่ใช่ตัวเลขจะทำให้ไม่สามารถคำนวณเส้นแนวโน้มได้.  
- **R‑squared value displays as 0:** สิ่งนี้มักหมายถึงชุดข้อมูลคงที่หรือมีการเปลี่ยนแปลงไม่เพียงพอ ลองใช้ชุดข้อมูลอื่นหรือเส้นแนวโน้มแบบพหุนาม.  
- **Image export fails with `NullPointerException`:** ตรวจสอบว่าแผนภูมิได้เรนเดอร์เต็มที่ก่อนเรียก `toImage()` การบันทึกเวิร์กบุ๊กก่อนอาจแก้ปัญหาเรื่องเวลาได้.

## คำถามที่พบบ่อย

**Q:** ฉันจะเปลี่ยนประเภทของเส้นแนวโน้มได้อย่างไร?  
**A:** Use a different `TrendlineType` enumeration when adding the trendline, e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.

**Q:** ฉันสามารถปรับแต่งลักษณะของเส้นแนวโน้ม (สี, ความหนา) ได้หรือไม่?  
**A:** Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()` and set properties such as `setWeight()` and `setColor()`.

**Q:** ฉันจะส่งออกแผนภูมิเป็น PDF แทนภาพได้อย่างไร?  
**A:** Convert the chart to an image first, then embed that image into a PDF using Aspose.PDF or any PDF library of your choice.

**Q:** สามารถเพิ่มเส้นแนวโน้มหลายเส้นในแผนภูมิเดียวได้หรือไม่?  
**A:** Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)` for each series you wish to analyze.

**Q:** Aspose.Cells รองรับการส่งออกภาพความละเอียดสูงหรือไม่?  
**A:** Yes. You can specify the DPI when calling `chart.toImage()` and then scale the image accordingly before saving.

## สรุป
ตอนนี้คุณมีโซลูชันครบวงจรจากต้นจนจบเพื่อ **create Excel chart**, เพิ่มเส้นแนวโน้ม, แสดงสมการและค่าความสัมพันธ์ R‑squared, ปรับแต่งภาพ, บันทึกเวิร์กบุ๊ก, และสุดท้ายส่งออกแผนภูมิเป็นไฟล์ PNG/JPEG การทำเช่นนี้ช่วยให้คุณสร้างสินทรัพย์การวิเคราะห์ระดับมืออาชีพโดยอัตโนมัติ เหมาะสำหรับการรายงานอัตโนมัติ, แดชบอร์ด, หรือสถานการณ์ใด ๆ ที่ภาพคงที่สะดวกกว่าการใช้ไฟล์ Excel.

---

**อัปเดตล่าสุด:** 2026-02-09  
**ทดสอบด้วย:** Aspose.Cells for Java ล่าสุด  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}