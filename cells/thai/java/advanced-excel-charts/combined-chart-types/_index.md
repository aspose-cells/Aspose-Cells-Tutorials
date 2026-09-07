---
date: 2026-02-14
description: เรียนรู้วิธีส่งออกแผนภูมิเป็น PNG, เพิ่มชุดข้อมูล, รวมแผนภูมิเส้นและคอลัมน์,
  บันทึกสมุดงานเป็น XLSX และเพิ่มคำอธิบายแผนภูมิโดยใช้ Aspose.Cells for Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: ส่งออกแผนภูมิเป็น PNG และเพิ่มชุดข้อมูลสำหรับแผนภูมิผสม
url: /th/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

 produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิเป็น PNG และเพิ่มชุดข้อมูลสำหรับแผนภูมิรวม

ในบทแนะนำนี้คุณจะ **เพิ่มชุดข้อมูล** ไปยังสมุดงาน Excel, **รวมแผนภูมิแบบเส้นและคอลัมน์** และเรียนรู้วิธี **ส่งออกแผนภูมิเป็น PNG** ด้วย Aspose.Cells for Java เราจะเดินผ่านทุกขั้นตอน—ตั้งค่าสมุดงาน, เพิ่มแผนภูมิไปยังแผ่นงาน, ปรับแต่งคำอธิบาย, ไปจนถึง **บันทึกสมุดงานเป็น xlsx** และสร้างภาพ PNG ของแผนภูมิ สุดท้ายคุณจะได้แผนภูมิรวมที่พร้อมใช้งานซึ่งสามารถฝังในรายงานหรือแดชบอร์ดได้

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดสร้างแผนภูมิรวม?** Aspose.Cells for Java  
- **ฉันจะเพิ่มชุดข้อมูลอย่างไร?** Use `chart.getNSeries().add(...)`  
- **ฉันจะส่งออกแผนภูมิเป็น png อย่างไร?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **ฉันสามารถบันทึกสมุดงานเป็นรูปแบบไฟล์อะไรได้บ้าง?** Standard `.xlsx` (save workbook as xlsx)  
- **ฉันต้องใช้ใบอนุญาตสำหรับการผลิตหรือไม่?** A valid Aspose.Cells license is required  

## สิ่งที่ **export chart to PNG** ใน Aspose.Cells คืออะไร?
การส่งออกแผนภูมิเป็น PNG จะสร้างภาพเรสเตอร์ของแผนภูมิ Excel ที่สามารถแสดงในหน้าเว็บ, รายงาน หรืออีเมลได้โดยไม่ต้องใช้แอปพลิเคชัน Excel

## ทำไมต้องสร้าง **combined line column chart**?
แผนภูมิรวมช่วยให้คุณแสดงชุดข้อมูลต่าง ๆ ด้วยการแสดงผลที่แตกต่างกัน (เช่น ชุดข้อมูลเส้นเหนือชุดข้อมูลคอลัมน์) ในมุมมองเดียว นี่เหมาะสำหรับการเปรียบเทียบแนวโน้มกับยอดรวม, เน้นความสัมพันธ์, หรือให้ข้อมูลเชิงลึกที่ครบถ้วนในรูปแบบที่กะทัดรัด

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือสูงกว่า  
- Aspose.Cells for Java library (ดาวน์โหลดจากลิงก์ด้านล่าง)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และแนวคิดของ Excel  

## เริ่มต้น

ขั้นแรก, ดาวน์โหลด Aspose.Cells for Java library จากเว็บไซต์อย่างเป็นทางการ:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

เมื่อเพิ่ม JAR ไปยัง classpath ของโครงการของคุณแล้ว, คุณสามารถเริ่มสร้างแผนภูมิได้

### ขั้นตอนที่ 1: นำเข้าคลาส Aspose.Cells
```java
import com.aspose.cells.*;
```

### ขั้นตอนที่ 2: สร้างสมุดงานใหม่
```java
Workbook workbook = new Workbook();
```

### ขั้นตอนที่ 3: เข้าถึงแผ่นงานแรก
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### ขั้นตอนที่ 4: เพิ่มอ็อบเจกต์แผนภูมิรวมไปยังแผ่นงาน  
เราจะเริ่มด้วยแผนภูมิแบบเส้นและต่อมาจะเพิ่มชุดข้อมูลคอลัมน์เพื่อให้ได้ผลลัพธ์ **combined line column chart**  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## การเพิ่มข้อมูลไปยังแผนภูมิ

เมื่อมีคอนเทนเนอร์ของแผนภูมิแล้ว, เราต้องป้อนข้อมูลให้มัน

### ขั้นตอนที่ 5: กำหนดช่วงข้อมูลและ **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **เคล็ดลับ:** พารามิเตอร์แรก (`"A1:A5"`) คือช่วงสำหรับชุดแรก, และพารามิเตอร์ที่สอง (`"B1:B5"`) สร้างชุดที่สองที่จะรวมกับชุดแรก.

### ขั้นตอนที่ 6: ตั้งค่าข้อมูลหมวดหมู่ (แกน X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## การปรับแต่งแผนภูมิ

แผนภูมิที่ดีบอกเล่าเรื่องราว. เรามาให้หัวเรื่อง, ป้ายแกน, และคำอธิบายที่ชัดเจน

### ขั้นตอนที่ 7: **Set chart axis labels** และหัวเรื่อง
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### ขั้นตอนที่ 8: **Add legend chart** และปรับตำแหน่งของมัน
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## การบันทึกและส่งออกแผนภูมิ

หลังจากปรับแต่ง, คุณจะต้องการ **save workbook as xlsx** และสร้างภาพด้วย

### ขั้นตอนที่ 9: บันทึกสมุดงานเป็นไฟล์ Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### ขั้นตอนที่ 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> วิธี `chart.toImage` **generates excel chart** images ที่สามารถใช้ในหน้าเว็บ, รายงาน, หรืออีเมลได้.

## ปัญหาทั่วไป & การแก้ไขปัญหา

| ปัญหา | วิธีแก้ |
|-------|----------|
| **ไม่มีข้อมูลปรากฏ** | ตรวจสอบว่าช่วงเซล (`A1:A5`, `B1:B5`, `C1:C5`) มีข้อมูลจริงก่อนสร้างแผนภูมิ. |
| **คำอธิบายทับแผนภูมิ** | ตั้งค่า `chart.getLegend().setOverlay(false)` หรือย้ายคำอธิบายไปตำแหน่งอื่น (เช่น `RIGHT`). |
| **ไฟล์ภาพว่าง** | ตรวจสอบว่าแผนภูมิมีอย่างน้อยหนึ่งชุดข้อมูลและว่า `chart.toImage` ถูกเรียกหลังจากการปรับแต่งทั้งหมด. |
| **การบันทึกทำให้เกิดข้อยกเว้น** | ตรวจสอบว่าคุณมีสิทธิ์เขียนไปยังไดเรกทอรีเป้าหมายและไฟล์ไม่ได้เปิดอยู่ใน Excel. |

## คำถามที่พบบ่อย

**Q: ฉันจะติดตั้ง Aspose.Cells for Java อย่างไร?**  
A: ดาวน์โหลด JAR จากเว็บไซต์อย่างเป็นทางการและเพิ่มไปยัง classpath ของโครงการของคุณ ลิงก์ดาวน์โหลดคือ: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: ฉันสามารถสร้างประเภทแผนภูมิอื่น ๆ นอกจากเส้นและคอลัมน์ได้หรือไม่?**  
A: ใช่, Aspose.Cells รองรับแผนภูมิแบบแท่ง, พาย, กระจาย, พื้นที่, และอื่น ๆ อีกมากมาย ดูเอกสาร API เพื่อดูรายการทั้งหมด.

**Q: จำเป็นต้องมีใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?**  
A: จำเป็นต้องมีใบอนุญาต Aspose.Cells ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต มีการทดลองใช้ฟรีสำหรับการประเมินผล.

**Q: ฉันจะเปลี่ยนสีของแต่ละชุดข้อมูลได้อย่างไร?**  
A: ใช้ `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (หรือคล้ายกัน) หลังจากเพิ่มชุดข้อมูลแล้ว.

**Q: ฉันจะหาโค้ดตัวอย่างเพิ่มเติมได้จากที่ไหน?**  
A: เอกสารที่ครอบคลุมและตัวอย่างเพิ่มเติมสามารถพบได้ที่เว็บไซต์อ้างอิงของ Aspose: [here](https://reference.aspose.com/cells/java/).

---

**อัปเดตล่าสุด:** 2026-02-14  
**ทดสอบกับ:** Aspose.Cells for Java latest version  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}