---
date: 2025-11-28
description: เรียนรู้วิธีเพิ่ม tooltip, ป้ายข้อมูล และคุณลักษณะ drill‑down เพื่อสร้างแผนภูมิแบบโต้ตอบใน
  Java ด้วย Aspose.Cells.
language: th
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: วิธีเพิ่มคำอธิบายเครื่องมือในแผนภูมิแบบโต้ตอบ (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่ม Tooltip ในแผนภูมิแบบโต้ตอบ (Aspose.Cells Java)

## คำนำ

แผนภูมิแบบโต้ตอบช่วยให้ผู้ใช้สำรวจข้อมูลโดยการวางเมาส์คลิก หรือขยายรายละเอียดลงไปได้ ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีเพิ่ม tooltip** ให้กับแผนภูมิ รวมถึง **การเพิ่มป้ายข้อมูล** และการทำ **drill‑down** ผ่านลิงก์ – ทั้งหมดนี้ด้วย Aspose.Cells สำหรับ Java เมื่อติดตั้งเสร็จคุณจะสามารถสร้างแผนภูมิแบบโต้ตอบที่เต็มคุณสมบัติ ทำให้การนำเสนอข้อมูลของคุณน่าสนใจและให้ข้อมูลเชิงลึกมากยิ่งขึ้น

## คำตอบสั้น
- **ต้องใช้ไลบรารีอะไร?** Aspose.Cells for Java (เวอร์ชันล่าสุด)  
- **ฟีเจอร์หลักของคู่มือนี้คืออะไร?** การเพิ่ม tooltip ให้กับแผนภูมิ  
- **สามารถเพิ่มป้ายข้อมูลได้หรือไม่?** ได้ – ดูส่วน “การเพิ่มป้ายข้อมูล”  
- **รองรับ drill‑down หรือไม่?** ได้ ผ่านการแนบ hyperlink บนจุดข้อมูล  
- **รูปแบบไฟล์ที่สร้างคืออะไร?** ไฟล์ Excel workbook (`.xlsx`) พร้อมแผนภูมิแบบโต้ตอบ

## Tooltip คืออะไร?

Tooltip คือหน้าต่างป๊อปอัพขนาดเล็กที่ปรากฏเมื่อผู้ใช้วางเมาส์เหนือองค์ประกอบของแผนภูมิ แสดงข้อมูลเพิ่มเติม เช่น ค่าที่แน่นอนหรือข้อความที่กำหนดเอง Tooltip ช่วยเพิ่มความอ่านง่ายของข้อมูลโดยไม่ทำให้หน้าตาแออัด

## ทำไมต้องสร้างแผนภูมิแบบโต้ตอบใน Java?

- **การตัดสินใจที่ดีขึ้น:** ผู้ใช้สามารถเห็นค่าที่แม่นยำได้ทันที  
- **รายงานระดับมืออาชีพ:** องค์ประกอบแบบโต้ตอบทำให้แดชบอร์ดดูทันสมัย  
- **คอมโพเนนต์ที่นำกลับมาใช้ใหม่:** เมื่อคุณเชี่ยวชาญ API แล้ว สามารถนำไปใช้กับโซลูชันการรายงานบน Excel ใดก็ได้

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำตามขั้นตอน ตรวจสอบให้แน่ใจว่าคุณมี:

- สภาพแวดล้อมการพัฒนา Java (JDK 8 หรือใหม่กว่า)  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [ที่นี่](https://releases.aspose.com/cells/java/))  
- ไฟล์ Excel ตัวอย่างชื่อ **data.xlsx** ที่มีข้อมูลที่คุณต้องการแสดงผล

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ Java ของคุณ

1. สร้างโปรเจกต์ Java ใหม่ใน IDE ที่คุณชอบ (IntelliJ IDEA, Eclipse ฯลฯ)  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells ลงใน classpath ของโปรเจกต์

## ขั้นตอนที่ 2: โหลดข้อมูล

เพื่อสร้างแผนภูมิแบบโต้ตอบ คุณต้องมี Worksheet ที่มีข้อมูล โค้ดด้านล่างจะโหลด Worksheet แรกจาก **data.xlsx**  

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ขั้นตอนที่ 3: สร้างแผนภูมิ

ต่อไปเราจะเพิ่มแผนภูมิคอลัมน์ลงใน Worksheet แผนภูมิจะครอบคลุมเซลล์ F6 ถึง K16  

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## ขั้นตอนที่ 4: เพิ่มความโต้ตอบ

### 4.1. วิธีเพิ่ม Tooltip

โค้ดต่อไปนี้เปิดใช้งาน tooltip สำหรับซีรีส์แรกในแผนภูมิ แต่ละจุดข้อมูลจะแสดงค่าของมันเมื่อวางเมาส์  

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. เพิ่มป้ายข้อมูลให้กับแผนภูมิ

หากต้องการให้แสดงป้ายข้อมูลข้างคอลัมน์แต่ละคอลัมน์ ให้ใช้วิธี **add data labels chart** ด้านล่าง ซึ่งสอดคล้องกับคีย์เวิร์ดรอง *add data labels chart*  

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. วิธีทำ Drill Down (การทำ Drill‑Down)

Drill‑down ให้ผู้ใช้คลิกที่จุดข้อมูลแล้วกระโดดไปยังมุมมองรายละเอียด (เช่น หน้าเว็บ) ที่นี่เราจะผูก hyperlink กับจุดแรกของซีรีส์  

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **เคล็ดลับ:** คุณสามารถสร้าง URL แบบไดนามิกตามค่าของจุดเพื่อสร้างประสบการณ์ drill‑down ที่ขับเคลื่อนด้วยข้อมูลจริง

## ขั้นตอนที่ 5: บันทึก Workbook

หลังจากตั้งค่าแผนภูมิเสร็จแล้ว ให้บันทึก workbook ไฟล์ที่ได้จะมีแผนภูมิแบบโต้ตอบพร้อมเปิดใน Excel  

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|---------|
| Tooltip ไม่แสดง | ป้ายข้อมูลไม่ได้เปิดใช้งาน | ตรวจสอบให้แน่ใจว่าเรียก `setHasDataLabels(true)` ก่อนตั้งค่า `ShowValue` |
| Hyperlink ไม่คลิกได้ | ดัชนีจุดผิด | ตรวจสอบว่ากำลังอ้างอิงจุดที่ถูกต้อง (`get(0)` คือจุดแรก) |
| แผนภูมิตำแหน่งผิด | ช่วงเซลล์ไม่ถูกต้อง | ปรับค่าแถว/คอลัมน์ใน `add(ChartType.COLUMN, row1, col1, row2, col2)` |

## คำถามที่พบบ่อย

**ถาม: จะเปลี่ยนประเภทแผนภูมิได้อย่างไร?**  
ตอบ: แทนที่ `ChartType.COLUMN` ด้วยค่า enum อื่น เช่น `ChartType.LINE` หรือ `ChartType.PIE` เมื่อเรียก `worksheet.getCharts().add(...)`

**ถาม: สามารถปรับแต่งลักษณะของ tooltip ได้หรือไม่?**  
ตอบ: ได้ ใช้คุณสมบัติการจัดรูปแบบของอ็อบเจ็กต์ `DataLabel` (ขนาดฟอนต์, สีพื้นหลัง ฯลฯ) เพื่อสไตล์ข้อความ tooltip

**ถาม: จะจัดการการโต้ตอบของผู้ใช้ในเว็บแอปพลิเคชันอย่างไร?**  
ตอบ: ส่งออก workbook เป็นรูปแบบที่รองรับเว็บ (เช่น HTML) แล้วใช้ JavaScript เพื่อตรวจจับเหตุการณ์คลิกบนองค์ประกอบแผนภูมิ

**ถาม: จะหา ตัวอย่างและเอกสารเพิ่มเติมได้จากที่ไหน?**  
ตอบ: สำรวจอ้างอิง API อย่างเป็นทางการที่ [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)

**ถาม: สามารถเพิ่มลิงก์ drill‑down หลายรายการในแผนภูมิเดียวได้หรือไม่?**  
ตอบ: ทำได้แน่นอน วนลูปผ่านจุดของซีรีส์และกำหนด URL ที่ไม่ซ้ำกันให้กับคอลเลกชัน `Hyperlinks` ของแต่ละจุด

## สรุป

ในคู่มือนี้คุณได้เรียนรู้ **วิธีเพิ่ม tooltip**, **การเพิ่มป้ายข้อมูล**, และ **การทำ drill‑down** เพื่อสร้างโซลูชัน **create interactive chart java** ด้วย Aspose.Cells ฟีเจอร์เหล่านี้ทำให้แผนภูมิ Excel ที่คงที่กลายเป็นการแสดงผลแบบไดนามิกและเป็นมิตรกับผู้ใช้ ช่วยให้ผู้มีส่วนได้ส่วนเสียสำรวจข้อมูลได้อย่างง่ายดาย

---

**อัปเดตล่าสุด:** 2025-11-28  
**ทดสอบด้วย:** Aspose.Cells for Java 24.12  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}