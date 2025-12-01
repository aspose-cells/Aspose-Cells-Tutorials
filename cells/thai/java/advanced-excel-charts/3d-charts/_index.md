---
date: 2025-12-01
description: เรียนรู้วิธีสร้างแผนภูมิ 3 มิติใน Java ด้วย Aspose.Cells และบันทึกไฟล์แผนภูมิ
  Excel คู่มือขั้นตอนต่อขั้นตอนสำหรับการแสดงผลข้อมูลที่น่าทึ่ง
language: th
linktitle: How to Create 3D Chart
second_title: Aspose.Cells Java Excel Processing API
title: วิธีสร้างแผนภูมิ 3 มิติใน Java ด้วย Aspose.Cells
url: /java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างแผนภูมิ 3D ใน Java ด้วย Aspose.Cells

## บทนำ 3D Charts  

ในบทแนะนำนี้คุณจะได้ค้นพบ **วิธีสร้างแผนภูมิ 3D** ด้วยการแสดงผลโดยตรงจากโค้ด Java โดยใช้ไลบรารี Aspose.Cells เราจะอธิบายทุกขั้นตอนตั้งแต่การตั้งค่าไลบรารีจนถึงการปรับแต่งแผนภูมิและสุดท้าย **บันทึกไฟล์แผนภูมิ Excel** ด้วยบรรทัดโค้ดเดียว ไม่ว่าคุณจะต้องการสาธิตอย่างรวดเร็วหรือโซลูชันพร้อมใช้งานในขั้นตอนการผลิต คู่มือนี้จะให้เส้นทางที่ชัดเจนและทำตามได้

## คำตอบอย่างรวดเร็ว
- **ต้องการไลบรารีอะไร?** Aspose.Cells for Java  
- **ฉันสามารถบันทึกแผนภูมิเป็นไฟล์ Excel ได้หรือไม่?** ใช่ – ใช้ `workbook.save("MyChart.xlsx")`  
- **ฉันต้องการไลเซนส์หรือไม่?** ไลเซนส์จะลบข้อจำกัดการประเมินและเปิดใช้งานคุณสมบัติเต็มรูปแบบ  
- **ประเภทแผนภูมิที่รองรับคืออะไร?** 3‑D Bar, Pie, Line, Area, และอื่น ๆ  
- **โค้ดนี้เข้ากันได้กับเวอร์ชัน Java ล่าสุดหรือไม่?** ใช่ ทำงานกับ Java 8+  

## 3D Charts คืออะไร?  

แผนภูมิ 3D เพิ่มความลึกให้กับการแสดงผลแบบ 2‑D แบบดั้งเดิม ทำให้การเปรียบเทียบค่าตามหมวดหมู่และการสังเกตแนวโน้มในชุดข้อมูลหลายมิตอง่ายขึ้น

## ทำไมต้องใช้ Aspose.Cells for Java เพื่อสร้างแผนภูมิ 3D?  

Aspose.Cells มี API ที่ครบถ้วนและจัดการได้เต็มรูปแบบ ซึ่งช่วยให้คุณสร้าง ปรับสไตล์ และส่งออกแผนภูมิได้โดยไม่ต้องติดตั้ง Microsoft Office แผนภูมิที่สร้างขึ้นเข้ากันได้อย่างเต็มที่กับทุกเวอร์ชันของ Excel และไลบรารีจะจัดการการจัดรูปแบบที่ซับซ้อน โทนสี และการผูกข้อมูลให้คุณ

## การตั้งค่า Aspose.Cells for Java  

### ดาวน์โหลดและการติดตั้ง  

รับไฟล์ JAR ของ Aspose.Cells for Java เวอร์ชันล่าสุดจากเว็บไซต์ทางการและเพิ่มลงในเส้นทางการสร้างของโครงการของคุณ (Maven, Gradle หรือการใส่ JAR ด้วยตนเอง)

### การเริ่มต้นไลเซนส์  

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## วิธีสร้างแผนภูมิ 3D พื้นฐาน  

### การนำเข้าไลบรารีที่จำเป็น  

```java
import com.aspose.cells.*;
```

### การเริ่มต้น Workbook  

```java
Workbook workbook = new Workbook();
```

### การเพิ่มข้อมูลตัวอย่าง  

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

### การปรับแต่งแผนภูมิ 3D Bar  

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### วิธีบันทึกไฟล์แผนภูมิ Excel  

```java
workbook.save("3D_Chart.xlsx");
```

คำสั่ง `save` เพียงครั้งเดียวจะเขียน workbook — รวมถึงแผนภูมิ 3D ที่สร้างใหม่ — ไปยัง **ไฟล์แผนภูมิ Excel** ที่สามารถเปิดได้ในทุกเวอร์ชันของ Microsoft Excel

## ประเภทต่าง ๆ ของแผนภูมิ 3D  

Aspose.Cells รองรับสไตล์แผนภูมิ 3‑D หลากหลายประเภท:

- **Bar charts** – เปรียบเทียบค่าตามหมวดหมู่.  
- **Pie charts** – แสดงสัดส่วนของแต่ละส่วนต่อทั้งหมด.  
- **Line charts** – แสดงแนวโน้มตามเวลาในมุมมองสามมิติ.  
- **Area charts** – เน้นขนาดของการเปลี่ยนแปลง.  

คุณสามารถสลับค่า enum `ChartType` เพื่อสร้างแผนภูมิใด ๆ เหล่านี้ด้วยขั้นตอนการทำงานเดียวกันที่แสดงข้างต้น

## การปรับแต่งแผนภูมิขั้นสูง  

### การเพิ่มหัวเรื่องและป้ายกำกับ  

ให้บริบทโดยการตั้งค่าหัวเรื่องของแผนภูมิ, หัวเรื่องแกน, และป้ายกำกับข้อมูล

### การปรับสีและสไตล์  

ใช้เมธอด `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRed())` (หรือที่คล้ายกัน) เพื่อให้ตรงกับพาเล็ตต์ของแบรนด์ของคุณ

### การทำงานกับแกนของแผนภูมิ  

ควบคุมสเกลของแกน, ช่วง, และเครื่องหมายติ๊กเพื่อการตีความข้อมูลที่ชัดเจนยิ่งขึ้น

### การเพิ่ม Legend  

เปิดใช้งาน legend ด้วย `chart.getLegend().setVisible(true)` เพื่ออธิบายแต่ละชุดข้อมูล

## การบูรณาการข้อมูล  

Aspose.Cells สามารถดึงข้อมูลจากฐานข้อมูล, ไฟล์ CSV, หรือ API สด เพื่อให้แผนภูมิ 3‑D ของคุณอัปเดตอยู่เสมอโดยไม่ต้องแก้ไขด้วยตนเอง

## สรุป  

เราได้ครอบคลุมทุกสิ่งที่คุณต้องการ **วิธีสร้างแผนภูมิ 3D** ใน Java ด้วย Aspose.Cells — ตั้งแต่การตั้งค่าและการสร้างแผนภูมิพื้นฐานจนถึงการสไตล์ขั้นสูงและการบันทึก workbook เป็น **ไฟล์แผนภูมิ Excel** ด้วยเครื่องมือเหล่านี้ คุณสามารถสร้างการแสดงผลที่น่าสนใจและดูเหมือนโต้ตอบได้โดยตรงจากแอปพลิเคชัน Java ของคุณ

## คำถามที่พบบ่อย  

### ฉันจะเพิ่มหลายชุดข้อมูลในแผนภูมิ 3D ได้อย่างไร?  

เพื่อเพิ่มหลายชุดข้อมูล ให้เรียก `chart.getNSeries().add()` สำหรับแต่ละช่วงที่คุณต้องการพล็อต ตรวจสอบให้แน่ใจว่าชุดข้อมูลแต่ละชุดใช้ประเภทแผนภูมิเดียวกันเพื่อความสอดคล้อง  

### ฉันสามารถส่งออกแผนภูมิ 3D ที่สร้างด้วย Aspose.Cells for Java ไปยังรูปแบบอื่นได้หรือไม่?  

ได้ ใช้ `workbook.save("Chart.png", SaveFormat.PNG)` หรือ `SaveFormat.PDF` เพื่อส่งออกแผนภูมิเป็นภาพหรือ PDF  

### สามารถสร้างแผนภูมิ 3D โต้ตอบได้ด้วย Aspose.Cells for Java หรือไม่?  

Aspose.Cells สร้างแผนภูมิแบบคงที่สำหรับ Excel สำหรับการแสดงผลแบบโต้ตอบบนเว็บ คุณอาจรวมภาพที่ส่งออกกับไลบรารี JavaScript เช่น Plotly หรือ Highcharts  

### ฉันสามารถทำกระบวนการอัปเดตข้อมูลในแผนภูมิ 3D ของฉันโดยอัตโนมัติได้หรือไม่?  

แน่นอน โหลดข้อมูลใหม่เข้าสู่ worksheet ด้วยโปรแกรม แล้วเรียก `chart.refresh()` (หรือเพียงบันทึก workbook ใหม่) เพื่อแสดงการเปลี่ยนแปลง  

### ฉันจะหาแหล่งข้อมูลและเอกสารเพิ่มเติมสำหรับ Aspose.Cells for Java ได้จากที่ไหน?  

คุณสามารถค้นหาเอกสารและแหล่งข้อมูลที่ครอบคลุมสำหรับ Aspose.Cells for Java ได้ที่เว็บไซต์: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/)

**อัปเดตล่าสุด:** 2025-12-01  
**ทดสอบกับ:** Aspose.Cells for Java 24.12  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}