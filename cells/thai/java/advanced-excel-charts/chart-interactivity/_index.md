---
date: 2026-02-09
description: เรียนรู้วิธีเพิ่มป้ายข้อมูลในแผนภูมิ Excel และเปลี่ยนประเภทแผนภูมิด้วย
  Aspose.Cells for Java พร้อมทูลทิปและการโต้ตอบแบบ drill‑down
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: เพิ่มป้ายข้อมูลในแผนภูมิ Excel ด้วย Aspose.Cells Java
url: /th/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

 paragraphs, bullet points, table contents (Issue, Solution) but keep terms like "Tooltips not showing" maybe translate? Probably translate the text but keep technical terms. Keep table structure.

Also translate the "Pro tip" note.

Also translate "Last Updated", "Tested With", "Author". Keep dates.

Make sure to preserve markdown formatting.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่ม Data Labels ให้กับแผนภูมิ Excel และเปลี่ยนประเภทแผนภูมิ – Aspose.Cells Java

แผนภูมิโต้ตอบทำให้รายงาน Excel ของคุณมีระดับความเข้าใจใหม่ และ **การเพิ่ม data labels ให้กับแผนภูมิ Excel** ทำให้ข้อมูลอ่านได้ทันที ในบทเรียนนี้คุณจะได้เรียนรู้วิธี **เพิ่ม data labels ให้กับแผนภูมิ Excel**, เปลี่ยนประเภทแผนภูมิ, และสร้างโซลูชัน Java แบบโต้ตอบด้วย Aspose.Cells เราจะยังแสดงวิธีเพิ่ม tooltip และ hyperlink แบบ drill‑down อย่างง่ายเพื่อให้ผู้ชมสำรวจข้อมูลได้อย่างลึกซึ้ง

## คำตอบอย่างรวดเร็ว
- **ใช้ไลบรารีอะไร?** Aspose.Cells for Java  
- **สามารถเปลี่ยนประเภทแผนภูมิได้หรือไม่?** ได้ – เพียงแก้ไข enum `ChartType` เมื่อสร้างแผนภูมิ  
- **จะเพิ่ม tooltip ให้แผนภูมิอย่างไร?** ใช้ API ของ data‑label (`setHasDataLabels(true)`) และเปิดการแสดงค่าที่ต้องการ  
- **รองรับ drill‑down หรือไม่?** คุณสามารถแนบ hyperlink ไปยังจุดข้อมูลเพื่อให้พฤติกรรม drill‑down เบื้องต้นได้  
- **ข้อกำหนดเบื้องต้น?** Java IDE, Aspose.Cells JAR, และไฟล์ Excel ที่มีตัวอย่างข้อมูล

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java (แนะนำ JDK 8+ )  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [here](https://releases.aspose.com/cells/java/))  
- สมุดงานตัวอย่าง (`data.xlsx`) ที่มีข้อมูลที่คุณต้องการแสดงผล  

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ Java ของคุณ

1. สร้างโปรเจกต์ Java ใหม่ใน IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, เป็นต้น)  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells ไปยัง build path ของโปรเจกต์หรือกำหนดเป็น dependency ของ Maven/Gradle  

## ขั้นตอนที่ 2: โหลดข้อมูล

เพื่อทำงานกับแผนภูมิ คุณต้องโหลดสมุดงานเข้าสู่หน่วยความจำก่อน

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ขั้นตอนที่ 3: สร้างแผนภูมิ (และเปลี่ยนประเภท)

คุณสามารถเลือกประเภทแผนภูมิใดก็ได้ที่เหมาะกับการวิเคราะห์ของคุณ ด้านล่างเราจะสร้าง **column chart** แต่คุณสามารถสลับเป็น line, pie หรือ bar chart ได้โดยการเปลี่ยนค่า enum `ChartType`

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **เคล็ดลับ:** เพื่อ **เปลี่ยนประเภทแผนภูมิ Excel** ให้แทนที่ `ChartType.COLUMN` ด้วย `ChartType.LINE`, `ChartType.PIE` เป็นต้น

## ขั้นตอนที่ 4: เพิ่มความโต้ตอบ

### 4.1. การเพิ่ม Tooltip (Add Tooltips to Chart)

Tooltip จะปรากฏเมื่อผู้ใช้ชี้เมาส์เหนือจุดข้อมูล โค้ดต่อไปนี้เปิดใช้งาน data labels และแสดงค่าเป็น tooltip

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. การเพิ่ม Data Labels – **add data labels to excel chart**

Data labels ให้สัญญาณภาพถาวรบนแผนภูมิเอง คุณสามารถแสดงเป็น callout เพื่อความอ่านง่ายยิ่งขึ้น

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **ทำไมต้องเพิ่ม data labels?** การใส่ data labels ไว้บนแผนภูมิโดยตรงช่วยขจัดความจำเป็นที่ผู้ใช้ต้องชี้เมาส์หรือเดาค่า ทำให้รายงานชัดเจนยิ่งขึ้น

### 4.3. การทำ Drill‑Down (Hyperlink บนจุดข้อมูล)

วิธีง่าย ๆ ในการเพิ่มความสามารถ drill‑down คือการแนบ hyperlink ไปยังจุดข้อมูลเฉพาะ การคลิกที่จุดนั้นจะเปิดหน้าเว็บที่มีข้อมูลรายละเอียด

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## ขั้นตอนที่ 5: บันทึกสมุดงาน

หลังจากตั้งค่าแผนภูมิแล้ว ให้บันทึกสมุดงานเพื่อให้คุณลักษณะโต้ตอบถูกเก็บไว้ในไฟล์ผลลัพธ์

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## ปัญหาที่พบบ่อย & วิธีแก้ไข

| Issue | Solution |
|-------|----------|
| **Tooltips not showing** | ตรวจสอบว่าได้เรียก `setHasDataLabels(true)` ก่อนกำหนด `setShowValue(true)` |
| **Hyperlink not clickable** | ยืนยันว่ารูปแบบไฟล์ผลลัพธ์รองรับ hyperlink (เช่น XLSX ไม่ใช่ CSV) |
| **Chart type doesn’t change** | ตรวจสอบว่าคุณได้แก้ไข enum `ChartType` ที่ถูกต้องเมื่อเพิ่มแผนภูมิ |

## คำถามที่พบบ่อย

**Q: จะเปลี่ยนประเภทแผนภูมิหลังจากสร้างแล้วได้อย่างไร?**  
A: คุณต้องสร้างแผนภูมิใหม่ด้วย `ChartType` ที่ต้องการ Aspose.Cells ไม่รองรับการแปลงประเภทในที่เดียว ดังนั้นให้ลบแผนภูมิเดิมและเพิ่มแผนภูมิใหม่

**Q: สามารถปรับแต่งลักษณะของ tooltip ได้หรือไม่?**  
A: ได้ ใช้คุณสมบัติของ `DataLabel` เช่น `setFontSize`, `setFontColor`, และ `setBackgroundColor` เพื่อจัดรูปแบบข้อความ tooltip

**Q: จะจัดการการโต้ตอบของผู้ใช้ในแอปเว็บอย่างไร?**  
A: ส่งออกสมุดงานเป็นไฟล์ HTML หรือ XLSX แล้วใช้ JavaScript ฝั่งไคลเอนต์เพื่อจับเหตุการณ์คลิกบนองค์ประกอบแผนภูมิ

**Q: จะหา ตัวอย่างและเอกสารเพิ่มเติมได้จากที่ไหน?**  
A: เยี่ยมชม [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) เพื่อดูรายการคลาสและเมธอดที่เกี่ยวกับแผนภูมิทั้งหมด

## สรุป

คุณได้เรียนรู้วิธี **เพิ่ม data labels ให้กับแผนภูมิ Excel**, **เปลี่ยนประเภทแผนภูมิ Excel**, **สร้างโซลูชันแผนภูมิ Java แบบโต้ตอบ**, และเพิ่ม tooltip, data labels, และ hyperlink แบบ drill‑down ด้วย Aspose.Cells for Java การปรับปรุงเหล่านี้ทำให้รายงาน Excel ของคุณน่าสนใจและให้ข้อมูลเชิงลึกมากขึ้นสำหรับผู้ใช้ปลายทาง

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}