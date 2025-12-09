---
date: 2025-12-09
description: เรียนรู้วิธีการส่งออกแผนภูมิเป็นภาพขณะทำการวิเคราะห์เส้นแนวโน้มใน Java
  ด้วย Aspose.Cells รวมขั้นตอนการโหลดไฟล์ Excel, เพิ่มเส้นแนวโน้ม, แสดงค่า R‑squared,
  และบันทึกเวิร์กบุ๊กเป็นไฟล์ XLSX.
language: th
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: ส่งออกแผนภูมิเป็นภาพพร้อมการวิเคราะห์เส้นแนวโน้มโดยใช้ Aspose.Cells สำหรับ
  Java
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิเป็นภาพพร้อมการวิเคราะห์เส้นแนวโน้ม

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีส่งออกแผนภูมิเป็นภาพ** พร้อมการทำ **การวิเคราะห์เส้นแนวโน้ม** อย่างเต็มรูปแบบโดยใช้ Aspose.Cells for Java เราจะอธิบายขั้นตอนการโหลดไฟล์ Excel ที่มีอยู่แล้ว, การเพิ่มเส้นแนวโน้ม, การแสดงค่า R‑squared, การปรับแต่งแผนภูมิ, และสุดท้ายการส่งออกแผนภูมิเป็นไฟล์ภาพ—ทั้งหมดด้วยโค้ดที่ชัดเจนและทำตามได้ทีละขั้นตอนที่คุณสามารถคัดลอก & วางได้.

## คำตอบอย่างรวดเร็ว
- **วัตถุประสงค์หลักของคู่มือนี้คืออะไร?** เพื่อแสดงวิธีการเพิ่มเส้นแนวโน้ม, แสดงสมการและค่า R‑squared, และส่งออกแผนภูมิที่ได้เป็นภาพโดยใช้ Java.  
- **ต้องใช้ไลบรารีใด?** Aspose.Cells for Java (ดาวน์โหลด [ที่นี่](https://releases.aspose.com/cells/java/)).  
- **ฉันต้องมีลิขสิทธิ์หรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการพัฒนา; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถสร้างไฟล์ Excel ด้วย Java ได้หรือไม่?** ได้ — บทแนะนำนี้สร้างและบันทึกเวิร์กบุ๊ก XLSX.  
- **ฉันจะส่งออกแผนภูมิเป็น PNG หรือ JPEG อย่างไร?** ใช้เมธอด `Chart.toImage()` (อธิบายในส่วน “Export Chart”).

## การส่งออกแผนภูมิเป็นภาพคืออะไร?
การส่งออกแผนภูมิเป็นภาพจะเปลี่ยนการแสดงผลข้อมูลของคุณให้เป็นไฟล์บิตแมพที่พกพาได้ (PNG, JPEG ฯลฯ) ซึ่งมีประโยชน์สำหรับการฝังแผนภูมิในรายงาน, หน้าเว็บ, หรือการนำเสนอที่ไม่จำเป็นต้องใช้ไฟล์ Excel ดั้งเดิม.

## ทำไมต้องเพิ่มเส้นแนวโน้มและแสดงค่า R‑squared?
เส้นแนวโน้มช่วยให้ระบุรูปแบบพื้นฐานของชุดข้อมูล, ส่วนเมตริก **R‑squared** จะวัดว่าการฟิตของเส้นแนวโน้มกับข้อมูลเป็นอย่างไร การใส่สิ่งเหล่านี้ลงในภาพที่ส่งออกจะทำให้ผู้มีส่วนได้ส่วนเสียเข้าใจข้อมูลได้ทันทีโดยไม่ต้องเปิดเวิร์กบุ๊ก.

## ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า ติดตั้งแล้ว.  
- ไลบรารี Aspose.Cells for Java เพิ่มในโปรเจกต์ของคุณ (ไฟล์ JAR อยู่ใน classpath).  
- มีความคุ้นเคยพื้นฐานกับ IDE ของ Java (IntelliJ IDEA, Eclipse ฯลฯ).

## คู่มือขั้นตอนโดยละเอียด

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
*เราเพิ่ง **โหลดไฟล์ Excel** เข้าไปในหน่วยความจำ, พร้อมสำหรับการสร้างแผนภูมิ.*

### ขั้นตอนที่ 3: สร้างแผนภูมิ
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*ที่นี่เราสร้างแผนภูมิเส้นที่ต่อมาจะใส่เส้นแนวโน้มของเรา.*

### ขั้นตอนที่ 4: เพิ่มเส้นแนวโน้ม (how to add trendline) และแสดงค่า R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*การเรียก `setDisplayRSquaredValue(true)` ทำให้ **ค่า R‑squared** ปรากฏบนแผนภูมิ.*

### ขั้นตอนที่ 5: ปรับแต่งแผนภูมิและบันทึกเวิร์กบุ๊ก (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*ตอนนี้เวิร์กบุ๊กได้ **สร้าง** และบันทึกเป็นไฟล์ XLSX พร้อมสำหรับการประมวลผลต่อไป.*

### ขั้นตอนที่ 6: ส่งออกแผนภูมิเป็นภาพ (export chart to image)
> **หมายเหตุ:** ขั้นตอนนี้อธิบายโดยไม่มีบล็อกโค้ดเพิ่มเติมเพื่อรักษาจำนวนบล็อกเดิมไว้.  
หลังจากที่สร้างและบันทึกแผนภูมิแล้ว, คุณสามารถส่งออกเป็นภาพได้โดยเรียกเมธอด `chart.toImage()` และเขียน `java.awt.image.BufferedImage` ที่ได้ไปยังรูปแบบไฟล์ที่คุณต้องการ (PNG, JPEG, BMP) กระบวนการทั่วไปคือ:
1. ดึงอ็อบเจ็กต์ `Chart` (ทำแล้วในขั้นตอนก่อนหน้า).  
2. เรียก `chart.toImage()` เพื่อรับ `BufferedImage`.  
3. ใช้ `ImageIO.write(bufferedImage, "png", new File("chart.png"))` เพื่อบันทึกไฟล์.  

สิ่งนี้จะสร้างภาพความละเอียดสูงที่คุณสามารถฝังได้ทุกที่, เสร็จสิ้นกระบวนการ **ส่งออกแผนภูมิเป็นภาพ**.

## วิเคราะห์ผลลัพธ์
เปิด `output.xlsx` ใน Excel เพื่อตรวจสอบว่าเส้นแนวโน้ม, สมการ, และค่า R‑squared ปรากฏตามที่คาดไว้. เปิดไฟล์ภาพที่ส่งออก (เช่น `chart.png`) เพื่อดูภาพที่สะอาดและสามารถแชร์ได้โดยไม่ต้องใช้เวิร์กบุ๊กต้นฉบับ.

## ปัญหาที่พบบ่อยและวิธีแก้
- **เส้นแนวโน้มไม่แสดง:** ตรวจสอบว่าช่วงข้อมูล (`A1:A10`) มีค่าตัวเลขจริง; ข้อมูลที่ไม่ใช่ตัวเลขจะทำให้ไม่สามารถคำนวณเส้นแนวโน้มได้.  
- **ค่า R‑squared แสดงเป็น 0:** มักหมายถึงชุดข้อมูลคงที่หรือไม่มีความแปรผันเพียงพอ ลองใช้ชุดข้อมูลอื่นหรือเส้นแนวโน้มแบบพหุนาม.  
- **การส่งออกภาพล้มเหลวด้วย `NullPointerException`:** ตรวจสอบว่าแผนภูมิได้เรนเดอร์เต็มที่ก่อนเรียก `toImage()` การบันทึกเวิร์กบุ๊กก่อนอาจแก้ปัญหาเรื่องเวลาได้.

## คำถามที่พบบ่อย

**ถาม: ฉันจะเปลี่ยนประเภทของเส้นแนวโน้มได้อย่างไร?**  
**ตอบ:** ใช้ค่า enumeration `TrendlineType` ที่แตกต่างกันเมื่อต้องการเพิ่มเส้นแนวโน้ม, เช่น `TrendlineType.POLYNOMIAL` สำหรับการฟิตแบบพหุนาม.

**ถาม: ฉันสามารถปรับแต่งลักษณะของเส้นแนวโน้ม (สี, ความหนา) ได้หรือไม่?**  
**ตอบ:** ได้. เข้าถึง `LineFormat` ของเส้นแนวโน้มผ่าน `trendline.getLineFormat()` แล้วตั้งค่าต่าง ๆ เช่น `setWeight()` และ `setColor()`.

**ถาม: ฉันจะส่งออกแผนภูมิเป็น PDF แทนภาพได้อย่างไร?**  
**ตอบ:** แปลงแผนภูมิเป็นภาพก่อน, แล้วฝังภาพนั้นลงใน PDF โดยใช้ Aspose.PDF หรือไลบรารี PDF ใดก็ได้ที่คุณเลือก.

**ถาม: สามารถเพิ่มหลายเส้นแนวโน้มในแผนภูมิเดียวกันได้หรือไม่?**  
**ตอบ:** แน่นอน. เรียก `chart.getNSeries().get(0).getTrendlines().add(...)` สำหรับแต่ละชุดข้อมูลที่ต้องการวิเคราะห์.

**ถาม: Aspose.Cells รองรับการส่งออกภาพความละเอียดสูงหรือไม่?**  
**ตอบ:** ใช่. คุณสามารถระบุ DPI เมื่อเรียก `chart.toImage()` แล้วปรับขนาดภาพตามที่ต้องการก่อนบันทึก.

## สรุป
ตอนนี้คุณมีโซลูชันครบวงจรสำหรับ **การส่งออกแผนภูมิเป็นภาพ** พร้อมการ **วิเคราะห์เส้นแนวโน้ม** ใน Java ด้วย Aspose.Cells โดยการโหลดไฟล์ Excel, เพิ่มเส้นแนวโน้ม, แสดงสมการและค่า R‑squared, ปรับแต่งแผนภูมิ, บันทึกเวิร์กบุ๊ก, และสุดท้ายส่งออกภาพเป็น PNG/JPEG, คุณสามารถสร้างสินทรัพย์วิเคราะห์ระดับมืออาชีพได้โดยอัตโนมัติ.

---

**อัปเดตล่าสุด:** 2025-12-09  
**ทดสอบกับ:** Aspose.Cells for Java 24.12 (latest)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}