---
date: 2025-12-06
description: เรียนรู้วิธีการเพิ่มชุดข้อมูล, สร้างประเภทแผนภูมิแบบผสม, บันทึกเวิร์กบุ๊กเป็น
  Excel และส่งออกแผนภูมิเป็น PNG ด้วย Aspose.Cells for Java.
language: th
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: เพิ่มชุดข้อมูลเพื่อสร้างแผนภูมิรวมโดยใช้ Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่ม series ข้อมูลเพื่อสร้างแผนภูมิรวมโดยใช้ Aspose.Cells

ในบทแนะนำนี้คุณจะ **เพิ่ม series ข้อมูล** ไปยังเวิร์กบุ๊ก Excel และเรียนรู้วิธี **สร้างแผนภูมิรวม** ด้วย Aspose.Cells for Java เราจะเดินผ่านทุกขั้นตอน—ตั้งค่าเวิร์กบุ๊ก, เพิ่ม series, ปรับแต่ง legend, ไปจนถึง **บันทึกไฟล์ Excel** และส่งออก **แผนภูมิเป็น PNG** เมื่อเสร็จคุณจะได้แผนภูมิรวมที่พร้อมใช้งานซึ่งสามารถฝังในรายงานหรือแดชบอร์ดได้

## คำตอบสั้น ๆ
- **ไลบรารีใดที่สร้างแผนภูมิรวม?** Aspose.Cells for Java  
- **จะเพิ่ม series ข้อมูลอย่างไร?** ใช้ `chart.getNSeries().add(...)`  
- **สามารถส่งออกแผนภูมิเป็นภาพได้หรือไม่?** ได้, ด้วย `chart.toImage(...)` (PNG)  
- **บันทึกเวิร์กบุ๊กเป็นรูปแบบไฟล์อะไรได้บ้าง?** มาตรฐาน `.xlsx` (Excel)  
- **ต้องมีลิขสิทธิ์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** จำเป็นต้องมีลิขสิทธิ์ Aspose.Cells ที่ถูกต้อง  

## **add data series** คืออะไรใน Aspose.Cells?
การเพิ่ม series ข้อมูลบอกแผนภูมิว่าช่วงเซลล์ใดมีค่าที่คุณต้องการพล็อต แต่ละ series สามารถเป็นเส้น, คอลัมน์, หรือประเภทแผนภูมิอื่น ๆ และคุณสามารถผสมผสานพวกมันเพื่อสร้าง **แผนภูมิรวม** ได้

## ทำไมต้องสร้าง **แผนภูมิรวม**?
แผนภูมิรวมช่วยให้คุณแสดงชุดข้อมูลที่แตกต่างกันด้วยการแสดงผลที่แตกต่างกัน (เช่น series เส้นบน series คอลัมน์) ในมุมมองเดียวกัน เหมาะสำหรับเปรียบเทียบแนวโน้มกับยอดรวม, เน้นความสัมพันธ์, หรือให้ข้อมูลเชิงลึกที่ครบถ้วนในรูปแบบที่กระชับ

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือสูงกว่า  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจากลิงก์ด้านล่าง)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และแนวคิดของ Excel  

## เริ่มต้น

ก่อนอื่น ดาวน์โหลดไลบรารี Aspose.Cells for Java จากเว็บไซต์ทางการ:

[ดาวน์โหลด Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

เมื่อเพิ่ม JAR ไปยัง classpath ของโครงการแล้ว คุณสามารถเริ่มสร้างแผนภูมิได้

### ขั้นตอนที่ 1: นำเข้าคลาส Aspose.Cells
```java
import com.aspose.cells.*;
```

### ขั้นตอนที่ 2: สร้างเวิร์กบุ๊กใหม่
```java
Workbook workbook = new Workbook();
```

### ขั้นตอนที่ 3: เข้าถึงเวิร์กชีตแรก
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### ขั้นตอนที่ 4: เพิ่มอ็อบเจ็กต์แผนภูมิรวม  
เราจะเริ่มด้วยแผนภูมิเส้นและต่อมาจะเพิ่ม series อื่นเพื่อให้ได้ผลลัพธ์ **แผนภูมิรวม**
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## การเพิ่มข้อมูลลงในแผนภูมิ

ตอนนี้คอนเทนเนอร์ของแผนภูมิมีอยู่แล้ว เราต้องป้อนข้อมูลให้มัน

### ขั้นตอนที่ 5: กำหนดช่วงข้อมูลและ **เพิ่ม series ข้อมูล**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **เคล็ดลับ:** พารามิเตอร์แรก (`"A1:A5"`) คือช่วงของ series แรก, และพารามิเตอร์ที่สอง (`"B1:B5"`) สร้าง series ที่สองที่จะถูกรวมกับ series แรก

### ขั้นตอนที่ 6: ตั้งค่าข้อมูลหมวดหมู่ (แกน X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## การปรับแต่งแผนภูมิ

แผนภูมิที่ดีบอกเล่าเรื่องราว ให้เราตั้งชื่อ, ป้ายแกน, และ legend ที่ชัดเจน

### ขั้นตอนที่ 7: ตั้งค่าชื่อแผนภูมิและป้ายแกน
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### ขั้นตอนที่ 8: **เพิ่ม legend แผนภูมิ** และปรับตำแหน่ง
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## การบันทึกและส่งออกแผนภูมิ

หลังจากปรับแต่งแล้ว คุณจะต้อง **บันทึกไฟล์ Excel** และสร้างภาพด้วย

### ขั้นตอนที่ 9: บันทึกเวิร์กบุ๊กเป็นไฟล์ Excel
```java
workbook.save("CombinedChart.xlsx");
```

### ขั้นตอนที่ 10: ส่งออก **แผนภูมิเป็น PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> เมธอด `chart.toImage` **สร้างภาพแผนภูมิ Excel** ที่สามารถใช้ในหน้าเว็บ, รายงาน, หรืออีเมลได้

## ปัญหาทั่วไป & การแก้ไขข้อผิดพลาด

| ปัญหา | วิธีแก้ |
|-------|----------|
| **ไม่มีข้อมูลแสดง** | ตรวจสอบว่าช่วงเซลล์ (`A1:A5`, `B1:B5`, `C1:C5`) มีข้อมูลจริงก่อนสร้างแผนภูมิ |
| **Legend ทับแผนภูมิ** | ตั้งค่า `chart.getLegend().setOverlay(false)` หรือย้าย legend ไปตำแหน่งอื่น (เช่น `RIGHT`) |
| **ไฟล์ภาพเป็นสีขาว** | ตรวจสอบว่าแผนภูมิมีอย่างน้อยหนึ่ง series และว่า `chart.toImage` ถูกเรียกหลังจากการปรับแต่งทั้งหมด |
| **การบันทึกทำให้เกิดข้อยกเว้น** | ตรวจสอบว่าคุณมีสิทธิ์เขียนในไดเรกทอรีเป้าหมายและไฟล์ไม่ได้เปิดอยู่ใน Excel |

## คำถามที่พบบ่อย

**ถาม: จะติดตั้ง Aspose.Cells for Java อย่างไร?**  
ตอบ: ดาวน์โหลด JAR จากเว็บไซต์ทางการและเพิ่มเข้าไปใน classpath ของโครงการ ลิงก์ดาวน์โหลดคือ: [ดาวน์โหลด Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

**ถาม: สามารถสร้างประเภทแผนภูมิอื่น ๆ นอกจากเส้นและคอลัมน์ได้หรือไม่?**  
ตอบ: ได้, Aspose.Cells รองรับแผนภูมิแบบบาร์, พาย, สเก็ตเตอร์, พื้นที่, และอื่น ๆ อีกมากมาย ดูเอกสาร API เพื่อรายการเต็ม

**ถาม: จำเป็นต้องมีลิขสิทธิ์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?**  
ตอบ: จำเป็นต้องมีลิขสิทธิ์ Aspose.Cells ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต มีรุ่นทดลองฟรีสำหรับการประเมินผล

**ถาม: จะเปลี่ยนสีของแต่ละ series ได้อย่างไร?**  
ตอบ: ใช้ `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (หรือวิธีที่คล้ายกัน) หลังจากเพิ่ม series แล้ว

**ถาม: จะหาโค้ดตัวอย่างเพิ่มเติมได้จากที่ไหน?**  
ตอบ: เอกสารครบถ้วนและตัวอย่างเพิ่มเติมมีให้ที่เว็บไซต์อ้างอิงของ Aspose: [ที่นี่](https://reference.aspose.com/cells/java/)

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**อัปเดตล่าสุด:** 2025-12-06  
**ทดสอบด้วย:** Aspose.Cells for Java 24.12  
**ผู้เขียน:** Aspose  

---