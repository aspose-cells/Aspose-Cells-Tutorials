---
date: 2025-12-04
description: เรียนรู้วิธีสร้างแผนภูมิแบบโต้ตอบใน Java ด้วย Aspose.Cells, เพิ่มคำอธิบายเครื่องมือให้กับแผนภูมิและเพิ่มแผนภูมิ
  drill‑down เพื่อการแสดงผลข้อมูลที่หลากหลายยิ่งขึ้น.
language: th
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: สร้างแผนภูมิแบบโต้ตอบด้วย Java และ Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผนภูมิโต้ตอบด้วย Java

## บทนำ

แผนภูมิโต้ตอบทำให้ผู้ใช้ของคุณสามารถสำรวจจุดข้อมูล ดูรายละเอียดเมื่อชี้เมาส์ และแม้กระทั่งเจาะลึกลงไปในชุดข้อมูลที่ลึกขึ้น—ทั้งหมดโดยไม่ต้องออกจากสเปรดชีต ในบทเรียนนี้คุณจะได้เรียนรู้ **วิธีสร้างแผนภูมิโต้ตอบด้วย Java** ด้วย Aspose.Cells เราจะอธิบายการเพิ่ม tooltip, ป้ายข้อมูล, และการทำประสบการณ์ drill‑down เพื่อให้แผนภูมิของคุณน่าสนใจและให้ข้อมูลมากยิ่งขึ้น.

## คำตอบด่วน
- **ไลบรารีที่ใช้คืออะไร?** Aspose.Cells for Java  
- **ฉันสามารถเพิ่ม tooltip ให้กับแผนภูมิได้หรือไม่?** ใช่, โดยใช้ NSeries data‑label API  
- **รองรับ drill‑down หรือไม่?** ใช่, โดยการแนบ hyperlink ไปยังจุดข้อมูล  
- **ไฟล์รูปแบบที่สร้างคืออะไร?** ไฟล์ XLSX มาตรฐานที่มีแผนภูมฝังอยู่  
- **ต้องการไลเซนส์หรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง  

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

- สภาพแวดล้อมการพัฒนา Java (แนะนำ JDK 8+)  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [หน้าเผยแพร่ของ Aspose](https://releases.aspose.com/cells/java/))  
- ไฟล์ Excel ตัวอย่างชื่อ **data.xlsx** ที่มีข้อมูลที่คุณต้องการแสดงผล  

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ Java ของคุณ

1. สร้างโปรเจกต์ Java ใหม่ใน IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, VS Code ฯลฯ).  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells ไปยัง classpath ของโปรเจกต์ของคุณ—โดยวางไฟล์ JAR ในโฟลเดอร์ `libs` หรือโดยเพิ่ม dependency ของ Maven/Gradle.  

## ขั้นตอนที่ 2: โหลดข้อมูล

เพื่อสร้างแผนภูมิโต้ตอบ คุณต้องมี worksheet ที่มีข้อมูลก่อน โค้ดตัวอย่างด้านล่างจะเปิด workbook ที่มีอยู่และดึง worksheet แรกออกมา.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **เคล็ดลับ:** ตรวจสอบให้แน่ใจว่าช่วงข้อมูลที่คุณต้องการสร้างแผนภูมินั้นต่อเนื่อง; Aspose.Cells จะตรวจจับช่วงโดยอัตโนมัติเมื่อคุณผูก series.

## ขั้นตอนที่ 3: สร้างแผนภูมิ

ตอนนี้เราจะสร้างแผนภูมิคอลัมน์และวางไว้บน worksheet คุณสามารถเปลี่ยน `ChartType.COLUMN` เป็นประเภทอื่นได้ (เช่น `ChartType.LINE`) หากต้องการสไตล์ภาพที่แตกต่าง.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **เหตุผลที่สำคัญ:** การเพิ่มแผนภูมิด้วยโปรแกรมทำให้คุณควบคุมขนาด, ตำแหน่ง, และแหล่งข้อมูลได้อย่างเต็มที่ ซึ่งจำเป็นสำหรับการสร้างประสบการณ์โต้ตอบ.

## ขั้นตอนที่ 4: เพิ่มการโต้ตอบ

### วิธีเพิ่ม tooltip ให้กับแผนภูมิ

Tooltip (หรือป้ายข้อมูลที่แสดงค่า) ช่วยให้ผู้ใช้เห็นค่าที่แน่นอนของแต่ละแท่งได้ทันที โค้ดต่อไปนี้จะเปิดใช้งานป้ายข้อมูลและตั้งค่าให้แสดงค่า.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### วิธีเพิ่มป้ายข้อมูล (callout)

หากคุณต้องการให้ป้ายแสดงเป็น callout แทนข้อความธรรมดา ให้สลับคุณสมบัติ `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### วิธีเพิ่มแผนภูมิ drill‑down

Drill‑down ทำให้ผู้ใช้คลิกที่จุดข้อมูลและกระโดดไปยังมุมมองรายละเอียดที่เกี่ยวข้อง—มักทำด้วย hyperlink ด้านล่างเราจะแนบ URL ไปยังจุดแรกของ series.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **ข้อผิดพลาดทั่วไป:** อย่าลืมตั้งค่าเป้าหมายของ hyperlink ให้เป็นหน้าที่สามารถแสดงข้อมูลรายละเอียดได้ (เช่น รายงานเว็บหรือแผ่น Excel อื่น) มิฉะนั้นการคลิกจะนำไปสู่ลิงก์ที่ไม่มีเนื้อหา.

## ขั้นตอนที่ 5: บันทึก Workbook

หลังจากตั้งค่าแผนภูมิแล้ว ให้บันทึก workbook ไฟล์ที่ได้จะมีแผนภูมิโต้ตอบพร้อมเปิดใน Excel หรือโปรแกรมดูที่รองรับ.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## สรุป

ในคู่มือนี้คุณได้เรียนรู้ **วิธีสร้างแผนภูมิโต้ตอบด้วย Java** ด้วย Aspose.Cells ครอบคลุม:

- การโหลดข้อมูลจาก workbook ที่มีอยู่  
- การสร้างแผนภูมิคอลัมน์ด้วยโปรแกรม  
- การเพิ่ม tooltip และป้ายข้อมูลแบบ callout  
- การทำงาน drill‑down ผ่าน hyperlink  
- การบันทึก workbook สุดท้าย  

เทคนิคเหล่านี้ทำให้สเปรดชีตแบบคงที่กลายเป็นแดชบอร์ดที่ไดนามิกและเป็นมิตรต่อผู้ใช้ ช่วยเพิ่มความเข้าใจในข้อมูลและการตัดสินใจ.

## คำถามที่พบบ่อย

**ถาม: ฉันจะเปลี่ยนประเภทแผนภูมิได้อย่างไร?**  
**ตอบ:** ปรับค่า enum `ChartType` ในเมธอด `add` (เช่น `ChartType.LINE` สำหรับแผนภูมิเส้น)

**ถาม: ฉันสามารถปรับแต่งลักษณะของ tooltip ได้หรือไม่?**  
**ตอบ:** ใช่, คุณสามารถปรับขนาดฟอนต์, สี, พื้นหลัง, และคุณสมบัติสไตล์อื่น ๆ ผ่านอ็อบเจ็กต์ `DataLabels`

**ถาม: ฉันจะจัดการการโต้ตอบของแผนภูมิในเว็บแอปพลิเคชันอย่างไร?**  
**ตอบ:** ส่งออก workbook เป็น XLSX แล้วใช้ไลบรารีแผนภูมิจาวาสคริปต์ (เช่น Highcharts) เพื่อแสดงข้อมูลบนฝั่งคลไอเอนท์, หรือฝังไฟล์ Excel ใน Office Web Viewer ที่รองรับ hyperlink

**ถาม: ฉันจะหา ตัวอย่างเพิ่มเติมได้จากที่ไหน?**  
**ตอบ:** เยี่ยมชม [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) อย่างเป็นทางการเพื่อดูรายการคลาสและเมธอดที่เกี่ยวกับแผนภูมิทั้งหมด

**ถาม: ฉันต้องการไลเซนส์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?**  
**ตอบ:** ใช่, จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง; มีไลเซนส์ทดลองฟรีสำหรับการทดสอบ

---

**อัปเดตล่าสุด:** 2025-12-04  
**ทดสอบด้วย:** Aspose.Cells for Java 24.12 (ล่าสุด ณ เวลาที่เขียน)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}