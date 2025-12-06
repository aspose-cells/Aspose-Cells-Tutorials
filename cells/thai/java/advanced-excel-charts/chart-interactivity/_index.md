---
date: 2025-12-06
description: เรียนรู้วิธีเปลี่ยนประเภทแผนภูมิ Excel และสร้างแผนภูมิโต้ตอบด้วย Java
  โดยใช้ Aspose.Cells เพิ่ม tooltip ให้กับแผนภูมิ ป้ายข้อมูล และการ drill‑down เพื่อการแสดงผลข้อมูลที่สมบูรณ์ยิ่งขึ้น
language: th
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: เปลี่ยนประเภทแผนภูมิ Excel ด้วย Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนประเภทแผนภูมิ Excel และเพิ่มการโต้ตอบ

## บทนำ

แผนภูมิโต้ตอบช่วยให้รายงาน Excel ของคุณมีระดับความเข้าใจใหม่ ให้ผู้ใช้สามารถวางเมาส์ คลิก และสำรวจจุดข้อมูลโดยตรง ในบทเรียนนี้คุณจะ **เปลี่ยนประเภทแผนภูมิ Excel** และ **สร้างโซลูชันแผนภูมิ Java แบบโต้ตอบ** ด้วย Aspose.Cells for Java เราจะพาคุณผ่านการเพิ่ม tooltip ให้แผนภูมิ, ป้ายข้อมูล, และไฮเปอร์ลิงก์ drill‑down อย่างง่าย เพื่อให้ผู้ชมของคุณสามารถเจาะลึกตัวเลขได้มากขึ้น

## คำตอบอย่างรวดเร็ว
- **ไลบรารีที่ใช้คืออะไร?** Aspose.Cells for Java  
- **ฉันสามารถเปลี่ยนประเภทแผนภูมิได้หรือไม่?** ได้ – เพียงแก้ไข enum `ChartType` เมื่อสร้างแผนภูมิ  
- **ฉันจะเพิ่ม tooltip ให้แผนภูมิอย่างไร?** ใช้ API ของ data‑label (`setHasDataLabels(true)`) และเปิดการแสดงค่าตัวเลข  
- **รองรับการ drill‑down หรือไม่?** คุณสามารถแนบไฮเปอร์ลิงก์ไปยังจุดข้อมูลเพื่อพฤติกรรม drill‑down เบื้องต้นได้  
- **ข้อกำหนดเบื้องต้น?** Java IDE, Aspose.Cells JAR, และไฟล์ Excel ที่มีข้อมูลตัวอย่าง

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java (แนะนำ JDK 8+)  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [here](https://releases.aspose.com/cells/java/))  
- เวิร์กบุ๊กตัวอย่าง (`data.xlsx`) ที่มีข้อมูลที่คุณต้องการแสดงผล  

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ Java ของคุณ

1. สร้างโปรเจกต์ Java ใหม่ใน IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse ฯลฯ)  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells ไปยังเส้นทางการสร้างของโปรเจกต์หรือ dependencies ของ Maven/Gradle  

## ขั้นตอนที่ 2: โหลดข้อมูล

เพื่อทำงานกับแผนภูมิ คุณต้องโหลดเวิร์กบุ๊กเข้าสู่หน่วยความจำก่อน

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ขั้นตอนที่ 3: สร้างแผนภูมิ (และเปลี่ยนประเภทของมัน)

คุณสามารถเลือกประเภทแผนภูมิใดก็ได้ที่เหมาะกับการวิเคราะห์ของคุณ ด้านล่างเราจะสร้าง **column chart** แต่คุณสามารถสลับเป็น line, pie หรือ bar chart ได้ง่าย ๆ เพียงเปลี่ยนค่า enum `ChartType`

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **เคล็ดลับพิเศษ:** เพื่อ **เปลี่ยนประเภทแผนภูมิ Excel** ให้แทนที่ `ChartType.COLUMN` ด้วย `ChartType.LINE`, `ChartType.PIE` เป็นต้น

## ขั้นตอนที่ 4: เพิ่มการโต้ตอบ

### 4.1. การเพิ่ม Tooltip (เพิ่ม Tooltip ให้แผนภูมิ)

Tooltip จะปรากฏเมื่อผู้ใช้วางเมาส์เหนือจุดข้อมูล โค้ดต่อไปนี้เปิดใช้งานป้ายข้อมูลและแสดงค่าตัวเลขเป็น tooltip

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. การเพิ่ม Data Labels

Data labels ให้สัญญาณภาพถาวรบนแผนภูมิเอง คุณสามารถแสดงเป็น callout เพื่อความอ่านง่ายยิ่งขึ้น

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. การทำ Drill‑Down (Hyperlink บนจุดข้อมูล)

วิธีง่าย ๆ เพื่อเพิ่มความสามารถ drill‑down คือการแนบไฮเปอร์ลิงก์ไปยังจุดข้อมูลเฉพาะ การคลิกที่จุดนั้นจะเปิดหน้าเว็บที่มีข้อมูลรายละเอียด

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊ก

หลังจากกำหนดค่าแผนภูมิแล้ว ให้บันทึกเวิร์กบุ๊กเพื่อให้คุณลักษณะโต้ตอบถูกเก็บไว้ในไฟล์ผลลัพธ์

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | วิธีแก้ |
|-------|----------|
| **Tooltip ไม่แสดง** | ตรวจสอบให้แน่ใจว่าได้เรียก `setHasDataLabels(true)` ก่อนกำหนด `setShowValue(true)` |
| **ไฮเปอร์ลิงก์ไม่คลิกได้** | ยืนยันว่ารูปแบบไฟล์ผลลัพธ์รองรับไฮเปอร์ลิงก์ (เช่น XLSX ไม่ใช่ CSV) |
| **ประเภทแผนภูมิไม่เปลี่ยน** | ตรวจสอบว่าคุณได้แก้ไข enum `ChartType` ที่ถูกต้องเมื่อเพิ่มแผนภูมิ |

## คำถามที่พบบ่อย

**Q: ฉันจะเปลี่ยนประเภทแผนภูมิหลังจากสร้างแล้วได้อย่างไร?**  
A: คุณต้องสร้างแผนภูมิใหม่ด้วย `ChartType` ที่ต้องการ Aspose.Cells ไม่รองรับการแปลงประเภทในที่เดียว ดังนั้นให้ลบแผนภูมิเก่าและเพิ่มแผนภูมิใหม่

**Q: ฉันสามารถปรับแต่งลักษณะของ tooltip ได้หรือไม่?**  
A: ได้ ใช้คุณสมบัติของ `DataLabel` เช่น `setFontSize`, `setFontColor` และ `setBackgroundColor` เพื่อจัดรูปแบบข้อความ tooltip

**Q: ฉันจะจัดการการโต้ตอบของผู้ใช้ในเว็บแอปพลิเคชันอย่างไร?**  
A: ส่งออกเวิร์กบุ๊กเป็นไฟล์ HTML หรือ XLSX แล้วใช้ JavaScript ฝั่งไคลเอนต์เพื่อดักจับเหตุการณ์คลิกบนองค์ประกอบของแผนภูมิ

**Q: ฉันจะหา ตัวอย่างและเอกสารเพิ่มเติมได้จากที่ไหน?**  
A: เยี่ยมชม [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) เพื่อดูรายการคลาสและเมธอดที่เกี่ยวกับแผนภูมิทั้งหมด

## สรุป

คุณได้เรียนรู้วิธี **เปลี่ยนประเภทแผนภูมิ Excel**, **สร้างโซลูชันแผนภูมิ Java แบบโต้ตอบ**, และเพิ่มคุณค่าให้กับแผนภูมิด้วย tooltip, data labels, และไฮเปอร์ลิงก์ drill‑down ด้วย Aspose.Cells for Java การปรับปรุงเหล่านี้ทำให้รายงาน Excel ของคุณน่าสนใจและให้ข้อมูลเชิงลึกมากขึ้นสำหรับผู้ใช้ปลายทาง

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}