---
date: 2025-12-05
description: เรียนรู้วิธีเพิ่มป้ายข้อมูลในแผนภูมิและสร้างแผนภูมิโต้ตอบด้วย Java โดยใช้
  Aspose.Cells เพิ่มคำอธิบายเมื่อชี้เมาส์ (tooltip) ป้ายข้อมูล และฟังก์ชันการเจาะลึก
language: th
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: เพิ่มแผนภูมิป้ายข้อมูลพร้อมการโต้ตอบใน Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มแผนภูมิ Data Labels พร้อมความโต้ตอบใน Aspose.Cells Java

แผนภูมิแบบโต้ตอบช่วยให้ผู้ใช้ของคุณสามารถสำรวจข้อมูลได้แบบเรียลไทม์ ในบทเรียนนี้คุณจะ **เพิ่มแผนภูมิ data labels** ฟีเจอร์ต่าง ๆ เช่น tooltip, data labels, และการทำ drill‑down ด้วยการใช้ Aspose.Cells for Java เมื่อเสร็จแล้วคุณจะได้แผนภูมิที่ดูสวยงามและโต้ตอบได้ ทำให้ข้อมูลซับซ้อนเข้าใจได้ทันที

## คำตอบด่วน
- **What library do I need?** Aspose.Cells for Java  
- **Can I add tooltips to an Excel chart?** ใช่ – ใช้การตั้งค่า data‑label ของ API  
- **Which chart types support interactivity?** ส่วนใหญ่ของประเภทที่มาพร้อม (column, line, pie, ฯลฯ)  
- **Do I need a license for production?** จำเป็นต้องมีใบอนุญาต Aspose.Cells ที่ถูกต้อง  
- **How long does implementation take?** ประมาณ 10–15 นาทีสำหรับแผนภูมิพื้นฐาน

## แผนภูมิ “add data labels chart” คืออะไร?
*add data labels chart* คือแผนภูมิที่แต่ละจุดข้อมูลแสดงป้ายกำกับ (ค่า, ชื่อ หรือข้อความที่กำหนดเอง) ตรงบนภาพ ทำให้ผู้ชมอ่านค่าที่แน่นอนได้ง่ายขึ้นโดยไม่ต้องชี้เมาส์หรืออ้างอิงตารางอธิบายแยกต่างหาก

## ทำไมต้องสร้างโซลูชันแผนภูมิโต้ตอบด้วย Java?
การฝังความโต้ตอบ—tooltip, จุดที่คลิกได้, ลิงก์ drill‑down—ทำให้สเปรดชีตแบบคงที่กลายเป็นแดชบอร์ดสำรวจ ผู้ใช้สามารถ:
- ระบุค่าผิดปกติได้อย่างรวดเร็ว  
- เข้าถึงชั้นข้อมูลลึกด้วยการคลิกเดียว  
- เร่งความเร็วในการตัดสินใจโดยลดความต้องการรายงานแยกต่างหาก

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำตามขั้นตอน ให้ตรวจสอบว่าคุณมี:

- สภาพแวดล้อมการพัฒนา Java (แนะนำ JDK 8+).  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [here](https://releases.aspose.com/cells/java/)).  

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ Java ของคุณ

1. สร้างโปรเจกต์ Java ใหม่ใน IDE ที่คุณชอบ (IntelliJ, Eclipse, VS Code, ฯลฯ).  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells for Java ลงใน classpath ของโปรเจกต์

## ขั้นตอนที่ 2: โหลดข้อมูล

เพื่อสร้างแผนภูมิโต้ตอบคุณต้องมีข้อมูลในเวิร์กชีตก่อน ตัวอย่างโค้ดด้านล่างโหลดเวิร์กบุ๊กที่มีชื่อ **data.xlsx** อยู่แล้ว

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ขั้นตอนที่ 3: สร้างแผนภูมิ

ตอนนี้เราจะสร้างแผนภูมิคอลัมน์และวางไว้บนเวิร์กชีต คุณสามารถเปลี่ยน `ChartType.COLUMN` เป็นประเภทอื่นได้ตามต้องการ

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## ขั้นตอนที่ 4: เพิ่มความโต้ตอบ – แกนหลักของ “add data labels chart”

### 4.1. การเพิ่ม Tooltips (add tooltips excel chart)

Tooltip จะปรากฏเมื่อผู้ใช้ชี้เมาส์เหนือจุดข้อมูล โค้ดต่อไปนี้เปิดใช้งานโดยตั้งค่าให้แสดงป้ายข้อมูลและแสดงค่า

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

 4.2. การเพิ่ม Data Labels (add data labels chart)

Data Labels คือข้อความที่แสดงข้างแต่ละจุด โค้ดนี้กำหนดให้แผนภูมิแสดงป้ายเรียกออก (callout) แทนค่าปกติ

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. การทำ Drill‑Down (create interactive chart java)

Drill‑down ให้ผู้ใช้คลิกที่จุดและกระโดดไปยังมุมมองรายละเอียด เราแนบ hyperlink ไปยังจุดข้อมูลแรก; คุณสามารถทำซ้ำกับจุดอื่น ๆ ที่ต้องการได้

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## ขั้นตอนที่ 5: บันทึก Workbook

หลังจากตั้งค่าแผนภูมิแล้ว ให้บันทึกเวิร์กบุ๊กเป็นไฟล์ใหม่เพื่อเปิดใน Excel และทดสอบความโต้ตอบ

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## ปัญหาที่พบบ่อยและเคล็ดลับ

| ปัญหา | วิธีแก้ |
|-------|----------|
| **Tooltips ไม่แสดง** | ตรวจสอบให้แน่ใจว่าเรียก `setHasDataLabels(true)` ก่อนตั้งค่า `ShowValue`. |
| **Hyperlink ไม่คลิกได้** | ตรวจสอบว่า URL ถูกต้องตามรูปแบบและการตั้งค่าความปลอดภัยของ Excel อนุญาตลิงก์ภายนอก. |
| **ประเภทแผนภูมิไม่ตรงกัน** | บางประเภท (เช่น radar) มีการสนับสนุนป้ายจำกัด—เลือกประเภทที่เข้ากันได้เช่น column หรือ line. |
| **ประสิทธิภาพช้าเมื่อชุดข้อมูลใหญ่** | จำกัดจำนวนจุดที่แสดงป้ายข้อมูล; พิจารณาใช้ `setShowValue(false)` สำหรับซีรีส์ที่ไม่สำคัญ. |

## คำถามที่พบบ่อย

**Q: How can I change the chart type?**  
A: แก้ไขค่า enum `ChartType` ในบรรทัดการสร้างแผนภูมิ (เช่น `ChartType.LINE` สำหรับแผนภูมิเส้น)

**Q: Can I customize the appearance of tooltips?**  
A: ใช่—ใช้คุณสมบัติของอ็อบเจ็กต์ `DataLabel` เช่น ฟอนต์, สีพื้นหลัง, และขอบ เพื่อปรับสไตล์ tooltip

**Q: How do I handle user interactions in a web application?**  
A: ส่งออกเวิร์กบุ๊กเป็นหน้า HTML หรือใช้ Aspose.Cells Cloud เพื่อเรนเดอร์แผนภูมิ แล้วจับเหตุการณ์คลิกด้วย JavaScript

**Q: Where can I find more examples and documentation?**  
A: เยี่ยมชม [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) เพื่อดูรายการคลาสและเมธอดที่เกี่ยวกับแผนภูมิทั้งหมด

## สรุป

ในคู่มือนี้เราได้สาธิตวิธี **เพิ่มแผนภูมิ data labels** และสร้างโซลูชัน **แผนภูมิโต้ตอบด้วย Java** ด้วย Aspose.Cells โดยการเพิ่ม tooltip, ป้ายข้อมูล, และ hyperlink drill‑down คุณจะเปลี่ยนแผนภูมิ Excel แบบคงที่ให้กลายเป็นเครื่องมือสำรวจข้อมูลแบบไดนามิกที่เพิ่มความเข้าใจและการใช้งาน

---

**อัปเดตล่าสุด:** 2025-12-05  
**ทดสอบกับ:** Aspose.Cells for Java 24.12  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}