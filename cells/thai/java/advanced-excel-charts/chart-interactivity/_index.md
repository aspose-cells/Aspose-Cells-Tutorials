---
date: 2025-12-01
description: เรียนรู้วิธีเปลี่ยนประเภทแผนภูมิ Excel และเพิ่มคุณลักษณะเชิงโต้ตอบ เช่น
  ทูลทิป ป้ายข้อมูล และการเจาะลึกโดยใช้ Aspose.Cells สำหรับ Java.
language: th
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: เปลี่ยนประเภทแผนภูมิ Excel และเพิ่มการโต้ตอบ – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนประเภทแผนภูมิ Excel และเพิ่มการโต้ตอบ

## บทนำ

แผนภูมิแบบโต้ตอบช่วยให้ผู้ชมสำรวจข้อมูลได้แบบเรียลไทม์ ในขณะที่การ **เปลี่ยนประเภทแผนภูมิ Excel** ให้ความยืดหยุ่นในการนำเสนอข้อมูลในรูปแบบที่เห็นภาพที่สุด ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีใช้ Aspose.Cells for Java เพื่อเปลี่ยนประเภทของแผนภูมิ เพิ่ม tooltip ฝังป้ายข้อมูล และแม้กระทั่งสร้างลิงก์ drill‑down — ทั้งหมดนี้โดยไม่ต้องออกจากโค้ด Java ของคุณ เมื่อเสร็จสิ้นคุณจะมีเวิร์กบุ๊ก Excel แบบโต้ตอบเต็มรูปแบบที่สามารถฝังลงในรายงาน แดชบอร์ด หรือแอปพลิเคชันเว็บได้

## คำตอบสั้น
- **ฉันสามารถเปลี่ยนประเภทแผนภูมิโดยโปรแกรมได้หรือไม่?** ใช่ – ใช้ enum `ChartType` เมื่อสร้างหรืออัปเดตแผนภูมิ  
- **จะเพิ่ม tooltip ให้แผนภูมิอย่างไร?** เปิดใช้งานป้ายข้อมูลและตั้งค่า `ShowValue` เป็น true  
- **วิธีที่ง่ายที่สุดในการเพิ่มลิงก์ drill‑down คืออะไร?** แนบ hyperlink ให้กับจุดข้อมูลผ่าน `getHyperlinks().add(url)`  
- **ต้องใช้ไลเซนส์สำหรับ Aspose.Cells หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการพัฒนา; ต้องมีไลเซนส์สำหรับการใช้งานในโปรดักชัน  
- **เวอร์ชัน Java ที่รองรับคืออะไร?** รองรับ Java 8 ขึ้นไปทั้งหมด

## “เปลี่ยนประเภทแผนภูมิ Excel” คืออะไร?

การเปลี่ยนประเภทแผนภูมิหมายถึงการสลับการแสดงผลภาพ (เช่น จากแผนภูมิคอลัมน์เป็นแผนภูมิเส้น) โดยยังคงข้อมูลพื้นฐานเดิมไว้ นี่เป็นประโยชน์เมื่อคุณพบว่าประเภทแผนภูมิอื่นสื่อสารแนวโน้ม การเปรียบเทียบ หรือการกระจายได้ดีกว่า

## ทำไมต้องเพิ่มการโต้ตอบให้แผนภูมิ Excel?

- **เพิ่มความเข้าใจข้อมูล:** Tooltip และป้ายข้อมูลทำให้ผู้ใช้เห็นค่าที่แน่นอนได้โดยไม่ต้องเลื่อนดู  
- **การนำเสนอที่ดึงดูด:** องค์ประกอบโต้ตอบทำให้ผู้ชมสนใจต่อเนื่อง  
- **ความสามารถ drill‑down:** Hyperlink ช่วยให้ผู้ใช้กระโดดไปยังแผ่นงานรายละเอียดหรือแหล่งข้อมูลภายนอกได้  
- **สินทรัพย์ที่นำกลับมาใช้ใหม่:** เวิร์กบุ๊กเดียวสามารถใช้ในหลายสถานการณ์รายงานโดยการสลับประเภทแผนภูมิเท่านั้น

## ข้อกำหนดเบื้องต้น

- สภาพแวดล้อมการพัฒนา Java (JDK 8+)  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [here](https://releases.aspose.com/cells/java/))  
- ไฟล์ Excel ตัวอย่าง (`data.xlsx`) ที่มีข้อมูลที่คุณต้องการแสดงผล

## คู่มือขั้นตอนโดยละเอียด

### ขั้นตอนที่ 1: ตั้งค่าโครงการ Java ของคุณ

1. สร้างโครงการ Java ใหม่ใน IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, VS Code ฯลฯ)  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells ลงใน classpath ของโครงการ

### ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กต้นฉบับ

เราจะเริ่มด้วยการโหลดเวิร์กบุ๊กที่มีข้อมูลสำหรับแผนภูมิของเรา

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### ขั้นตอนที่ 3: สร้างแผนภูมิและ **เปลี่ยนประเภทของมัน**

ต่อไปเราจะสร้างแผนภูมิคอลัมน์ แล้วสาธิตวิธีสลับเป็นแผนภูมิเส้นหากต้องการ

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **เคล็ดลับ:** การเปลี่ยนประเภทแผนภูมิหลังจากสร้างเสร็จง่ายเพียงเรียก `setChartType(...)` ซึ่งตอบโจทย์คีย์เวิร์ดหลัก **change Excel chart type** โดยไม่ต้องสร้างอ็อบเจกต์แผนภูมิใหม่

### ขั้นตอนที่ 4: เพิ่มการโต้ตอบ

#### 4.1 เพิ่ม tooltip ให้แผนภูมิ

Tooltip จะปรากฏเมื่อผู้ใช้ชี้เมาส์เหนือจุดข้อมูล ใน Aspose.Cells จะทำผ่านป้ายข้อมูล

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 เพิ่มป้ายข้อมูล (**add data labels chart**)

ป้ายข้อมูลสามารถแสดงค่าที่แน่นอน ชื่อหมวดหมู่ หรือทั้งสองอย่าง เราจะใช้สไตล์ callout

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implement drill‑down (**add drill down excel**)

ลิงก์ drill‑down ให้ผู้ใช้คลิกที่จุดและกระโดดไปยังมุมมองรายละเอียด ไม่ว่าจะอยู่ภายในเวิร์กบุ๊กหรือบนหน้าเว็บ

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊ก

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## ปัญหาที่พบบ่อยและวิธีแก้

| Issue | Reason | Fix |
|-------|--------|-----|
| Tooltips not showing | `HasDataLabels` not enabled | Ensure `setHasDataLabels(true)` is called before configuring `ShowValue`. |
| Drill‑down link does nothing | Hyperlink URL is malformed | Verify the URL starts with `http://` or `https://`. |
| Chart type doesn’t change | Using an older Aspose.Cells version | Upgrade to the latest version (tested with 24.12). |

## คำถามที่พบบ่อย

**Q: จะเปลี่ยนประเภทแผนภูมิหลังจากสร้างแล้วได้อย่างไร?**  
A: เรียก `chart.setChartType(ChartType.YOUR_CHOICE)` บนวัตถุ `Chart` ที่มีอยู่แล้ว วิธีนี้ตรงกับความต้องการ **change Excel chart type** โดยตรง

**Q: สามารถปรับแต่งลักษณะของ tooltip ได้หรือไม่?**  
A: ใช่ ใช้ `chart.getNSeries().get(0).getPoints().getDataLabels()` เพื่อกำหนดขนาดฟอนต์ สี และพื้นหลัง

**Q: สามารถเพิ่มหลายลิงก์ drill‑down ในแผนภูมิเดียวได้หรือไม่?**  
A: แน่นอน วนลูปผ่านจุดต่าง ๆ แล้วเรียก `getHyperlinks().add(url)` สำหรับแต่ละจุดที่ต้องการเชื่อมโยง

**Q: Aspose.Cells รองรับประเภทแผนภูมิอื่น ๆ เช่น พายหรือเรดาร์หรือไม่?**  
A: รองรับทุกประเภทที่กำหนดใน enum `ChartType` รวมถึง `PIE`, `RADAR`, `AREA` เป็นต้น

**Q: จะหา ตัวอย่างเพิ่มเติมได้จากที่ไหน?**  
A: เยี่ยมชม [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) เพื่อดูรายการเมธอดที่เกี่ยวกับแผนภูมิทั้งหมด

## สรุป

คุณได้เรียนรู้วิธี **เปลี่ยนประเภทแผนภูมิ Excel**, ฝัง **tooltip**, เพิ่ม **ป้ายข้อมูล**, และสร้างลิงก์ **drill‑down** ด้วย Aspose.Cells for Java คุณสมบัติการโต้ตอบเหล่านี้ทำให้สเปรดชีตแบบคงที่กลายเป็นเครื่องมือสำรวจข้อมูลแบบไดนามิก เหมาะสำหรับแดชบอร์ด รายงาน และการวิเคราะห์บนเว็บ

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}