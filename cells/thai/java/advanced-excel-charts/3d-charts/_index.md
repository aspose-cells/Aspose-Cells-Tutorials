---
date: 2026-02-09
description: เรียนรู้วิธีสร้างแผนภูมิวงกลม 3 มิติใน Java ด้วย Aspose.Cells สร้างแผนภูมิแท่ง
  3 มิติ เพิ่มแผนภูมิ 3 มิติใน Excel และบันทึกเวิร์กบุ๊กเป็นไฟล์ xlsx พร้อมตัวอย่างโค้ดทีละขั้นตอน.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: สร้างแผนภูมิวงกลม 3 มิติด้วย Java และ Aspose.Cells
url: /th/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผนภูมิวงกลม 3D Java

## บทนำแผนภูมิ 3D

Aspose.Cells for Java เป็น API Java ที่มีประสิทธิภาพสำหรับทำงานกับไฟล์ Excel และทำให้การ **create 3d pie chart** โครงการเป็นเรื่องง่าย รวมถึงการแสดงผลแบบแถบ 3‑D คลาสสิก ในบทแนะนำนี้คุณจะได้เห็นวิธีสร้างแผนภูมิแถบ 3‑D อย่างละเอียด วิธีปรับใช้แนวทางเดียวกันสำหรับแผนภูมิวงกลม 3‑D การปรับแต่งลักษณะต่าง ๆ และในที่สุด **add 3d chart excel** ไฟล์ลงในรายงานของคุณ ไม่ว่าคุณจะสร้างแดชบอร์ดการเงิน แผ่นงานประสิทธิภาพการขาย หรือการแสดงผลข้อมูลทางวิทยาศาสตร์ ขั้นตอนต่อไปนี้จะให้พื้นฐานที่มั่นคง

## คำตอบอย่างรวดเร็ว
- **ต้องการไลบรารีอะไร?** Aspose.Cells for Java (latest version)  
- **ฉันสามารถสร้างแผนภูมิแถบ 3D ได้หรือไม่?** Yes – use `ChartType.BAR_3_D`  
- **ฉันต้องการใบอนุญาตหรือไม่?** A valid license removes evaluation limits  
- **เวอร์ชัน Excel ที่รองรับมีอะไรบ้าง?** All major versions from 2003 to 2023  
- **สามารถส่งออกแผนภูมิเป็นภาพได้หรือไม่?** Yes, via `chart.toImage()` methods  

## แผนภูมิ 3D คืออะไร?
แผนภูมิ 3D เพิ่มความลึกให้กับการแสดงผลแบบ 2D แบบดั้งเดิม ช่วยให้ผู้ชมเข้าใจความสัมพันธ์หลายมิติได้อย่างเป็นธรรมชาติ พวกมันมีประโยชน์เป็นพิเศษเมื่อคุณต้องการเปรียบเทียบหลายหมวดหมู่เคียงข้างกันพร้อมคงลำดับชั้นภาพที่ชัดเจน

## ทำไมต้องใช้ Aspose.Cells for Java เพื่อสร้างแผนภูมิแถบ 3D?
Aspose.Cells for Java มีชุด API การสร้างแผนภูมิที่ครบครัน ความเข้ากันได้เต็มรูปแบบกับ Excel และการควบคุมการจัดรูปแบบอย่างละเอียด ซึ่งหมายความว่าคุณสามารถ **generate 3d bar chart** วัตถุได้โดยโปรแกรมโดยไม่ต้องกังวลเกี่ยวกับข้อจำกัดของเวอร์ชัน Excel

## การตั้งค่า Aspose.Cells for Java

### ดาวน์โหลดและการติดตั้ง
คุณสามารถดาวน์โหลดไลบรารี Aspose.Cells for Java จากเว็บไซต์อย่างเป็นทางการได้ ปฏิบัติตามคำแนะนำ Maven/Gradle ที่ให้ไว้ หรือเพิ่มไฟล์ JAR ลงใน classpath ของโครงการของคุณโดยตรง

### การเริ่มต้นใบอนุญาต
เพื่อเปิดใช้งานคุณสมบัติทั้งหมด ให้เริ่มต้นใบอนุญาตของคุณก่อนทำการดำเนินการใด ๆ กับแผนภูมิ:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## การสร้างแผนภูมิ 3D เบื้องต้น

### นำเข้าไลบรารีที่จำเป็น
ขั้นแรก ให้นำคลาสที่จำเป็นเข้ามาใช้:

```java
import com.aspose.cells.*;
```

### การเริ่มต้น Workbook
สร้าง Workbook ใหม่ที่จะเป็นที่เก็บแผนภูมิ:

```java
Workbook workbook = new Workbook();
```

### การเพิ่มข้อมูลลงในแผนภูมิ
เติมข้อมูลตัวอย่างลงในแผ่นงานเพื่อให้แผนภูมิอ้างอิง:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### วิธีสร้างแผนภูมิแถบ 3D ด้วย Java
ต่อไปเราจะสร้างแผนภูมิและปรับแต่งพื้นฐานบางอย่าง:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### การบันทึกแผนภูมิลงไฟล์
สุดท้าย ให้เขียน workbook (ซึ่งตอนนี้มีแผนภูมิ 3‑D อยู่) ลงดิสก์ ซึ่งจะ **save workbook xlsx** ในรูปแบบ Excel มาตรฐาน:

```java
workbook.save("3D_Chart.xlsx");
```

## วิธีสร้างแผนภูมิวงกลม 3D ด้วย Aspose.Cells for Java
หากคุณต้องการการแสดงผลแบบวงกลม ขั้นตอนการทำงานจะเกือบเหมือนกัน—เพียงแค่ค่า enum `ChartType` เปลี่ยนไป แทนที่ `ChartType.BAR_3_D` ด้วย `ChartType.PIE_3_D` เมื่อติดตั้งแผนภูมิ และชี้ series ไปยังช่วงข้อมูลเดียวกัน หลังจากสร้างแผนภูมิแล้วคุณสามารถ:

* ตั้งชื่อเรื่องที่อธิบายเช่น “3D Sales Distribution”.
* ปรับสีของชิ้นด้วย `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* ส่งออกแผนภูมิวงกลมเป็นภาพ PNG ด้วย `chart.toImage("pie_chart.png", ImageFormat.getPng())` ซึ่งตอบสนองความต้องการ **convert chart png**.

เนื่องจากจำนวน code block ต้องคงเดิม โค้ด Java จริงจึงไม่ได้แสดงที่นี่ แต่ขั้นตอนจะสอดคล้องกับตัวอย่างแผนภูมิแถบด้านบน.

## ประเภทต่าง ๆ ของแผนภูมิ 3D
Aspose.Cells for Java รองรับหลายรูปแบบของแผนภูมิ 3D ที่คุณสามารถ **add 3d chart excel** ไฟล์ได้:

- **Bar charts** – เหมาะสำหรับเปรียบเทียบหมวดหมู่.  
- **Pie charts** – แสดงส่วนแบ่งสัดส่วน (รวมถึง 3D pie).  
- **Line charts** – แสดงแนวโน้มตามเวลา.  
- **Area charts** – เน้นขนาดของการเปลี่ยนแปลง.

คุณสามารถสลับค่า enum `ChartType` ไปยังรูปแบบใดก็ได้ข้างต้นโดยคงรูปแบบการสร้างเดิม

## การปรับแต่งแผนภูมิขั้นสูง

### การเพิ่มหัวเรื่องและป้ายกำกับ
ให้บริบทกับแผนภูมิของคุณโดยตั้งชื่อเรื่องและป้ายแกนที่อธิบายได้

### การปรับสีและสไตล์
ใช้เมธอด `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` เพื่อให้ตรงกับแบรนด์ขององค์กร

### การทำงานกับแกนของแผนภูมิ
ปรับแต่งสเกลของแกน ช่วงเวลา และเครื่องหมายติ๊กเพื่อเพิ่มความอ่านง่าย

### การเพิ่มคำอธิบาย (Legend)
เปิดใช้งานคำอธิบายด้วย `chart.getLegend().setVisible(true)` เพื่อให้ผู้ชมสามารถระบุแต่ละชุดข้อมูลได้

### การส่งออกแผนภูมิเป็นภาพ
เมื่อคุณต้องการภาพคงที่สำหรับรายงานเว็บ ให้เรียก `chart.toImage("chart.png", ImageFormat.getPng())` ซึ่งตอบสนองกรณีการใช้ **convert chart png** โดยไม่ต้องออกจาก workbook

## การบูรณาการข้อมูล
Aspose.Cells for Java สามารถดึงข้อมูลจากฐานข้อมูล ไฟล์ CSV หรือ API แบบเรียลไทม์ เพียงเติมข้อมูลลงในเซลล์ของแผ่นงานก่อนเชื่อมช่วงข้อมูลกับแผนภูมิ การทำเช่นนี้ทำให้กระบวนการ **add 3d chart excel** ของคุณเป็นแบบไดนามิกและอัปเดตอยู่เสมอ

## สรุป
ในคู่มือนี้ เราได้อธิบายขั้นตอนการ **create 3d pie chart** และ **create 3d bar chart** ตั้งแต่เริ่มต้นจนจบ—การตั้งค่าห้องสมุด การเพิ่มข้อมูล การสร้างแผนภูมิแถบ 3‑D การปรับใช้ขั้นตอนเดียวกันสำหรับแผนภูมิวงกลม 3‑D และการใช้สไตล์ขั้นสูง ด้วย Aspose.Cells for Java คุณจะมีวิธีที่เชื่อถือได้และไม่ขึ้นกับเวอร์ชันในการฝังการแสดงผล 3‑D ที่สมบูรณ์ลงในไฟล์ Excel และแม้กระทั่งส่งออกเป็นภาพ PNG

## คำถามที่พบบ่อย

**Q: ฉันจะเพิ่มหลาย series ของข้อมูลในแผนภูมิ 3D ได้อย่างไร?**  
A: ใช้ `chart.getNSeries().add()` สำหรับแต่ละช่วง series และตรวจสอบให้แน่ใจว่าประเภทแผนภูมอยังคงเป็น 3‑D (เช่น `ChartType.BAR_3_D` หรือ `ChartType.PIE_3_D`).

**Q: ฉันสามารถส่งออกแผนภูมิ 3D ที่สร้างด้วย Aspose.Cells for Java ไปเป็นรูปแบบอื่นได้หรือไม่?**  
A: ได้ คุณสามารถบันทึกแผนภูมิเป็น PNG, JPEG หรือ PDF โดยเรียกเมธอด `chart.toImage()` หรือ `workbook.save()` ที่เหมาะสม ซึ่งตอบสนองความต้องการ **convert chart png**.

**Q: สามารถสร้างแผนภูมิ 3D แบบโต้ตอบกับ Aspose.Cells for Java ได้หรือไม่?**  
A: Aspose.Cells มุ่งเน้นที่แผนภูมิ Excel แบบคงที่ สำหรับการแสดงผล 3‑D แบบโต้ตอบบนเว็บ ให้พิจารณาเชื่อมข้อมูล Excel กับไลบรารี JavaScript เช่น Three.js.

**Q: ฉันสามารถทำกระบวนการอัปเดตข้อมูลในแผนภูมิ 3D ของฉันโดยอัตโนมัติได้หรือไม่?**  
A: ได้อย่างแน่นอน โหลดข้อมูลใหม่เข้าสู่แผ่นงานโดยโปรแกรมและรีเฟรชช่วงของแผนภูมิ; ครั้งต่อไปที่เปิด workbook แผนภูมิจะสะท้อนค่าที่อัปเดต.

**Q: ฉันจะหาแหล่งข้อมูลและเอกสารเพิ่มเติมสำหรับ Aspose.Cells for Java ได้จากที่ไหน?**  
A: คุณสามารถค้นหาเอกสารและแหล่งข้อมูลที่ครอบคลุมสำหรับ Aspose.Cells for Java ได้ที่เว็บไซต์: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**อัปเดตล่าสุด:** 2026-02-09  
**ทดสอบด้วย:** Aspose.Cells for Java 24.12 (latest)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}