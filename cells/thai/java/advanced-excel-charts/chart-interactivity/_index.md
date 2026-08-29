---
date: 2026-08-21
description: เรียนรู้วิธีเพิ่ม tooltip, data label และเปลี่ยน chart type ในแผนภูมิ
  Excel ด้วย Aspose.Cells for Java – คู่มือขั้นตอนโดยละเอียดพร้อมตัวอย่างเชิงโต้ตอบ
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: เปลี่ยน chart type ของ Excel
og_description: เรียนรู้วิธีเพิ่ม tooltip, data label และเปลี่ยน chart type ในแผนภูมิ
  Excel ด้วย Aspose.Cells for Java – คู่มือขั้นตอนโดยละเอียดพร้อมตัวอย่างเชิงโต้ตอบ
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: วิธีเพิ่ม tooltip และ data label ให้กับแผนภูมิ Excel ใน Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: วิธีเพิ่ม tooltip และ data label ให้กับแผนภูมิ Excel ใน Java
url: /th/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มป้ายข้อมูลในแผนภูมิ Excel และเปลี่ยนประเภทแผนภูมิ – Aspose.Cells Java

แผนภูมิแบบโต้ตอบช่วยให้รายงาน Excel ของคุณมีระดับความเข้าใจใหม่, และ **วิธีเพิ่ม tooltip** ทำให้ข้อมูลอ่านได้ทันที ในบทเรียนนี้คุณจะได้เรียนรู้วิธี **เพิ่มป้ายข้อมูลในแผนภูมิ Excel**, **เปลี่ยนประเภทแผนภูมิ**, และสร้างโซลูชัน Java แบบโต้ตอบด้วย Aspose.Cells เราจะยังแสดงวิธีเพิ่ม tooltip และไฮเปอร์ลิงก์ drill‑down อย่างง่ายเพื่อให้ผู้ชมของคุณสำรวจข้อมูลได้อย่างละเอียด

## คำตอบอย่างรวดเร็ว
- **ไลบรารีที่ใช้คืออะไร?** Aspose.Cells for Java  
- **ฉันสามารถเปลี่ยนประเภทแผนภูมิได้หรือไม่?** ใช่ – เพียงแก้ไข `ChartType` enum เมื่อคุณสร้างแผนภูมิ  
- **ฉันจะเพิ่ม tooltip ให้กับแผนภูมิอย่างไร?** ใช้ data‑label API (`setHasDataLabels(true)`) และเปิดใช้งานการแสดงค่า  
- **รองรับการ drill‑down หรือไม่?** คุณสามารถแนบไฮเปอร์ลิงก์ไปยังจุดข้อมูลเพื่อพฤติกรรม drill‑down เบื้องต้นได้  
- **ข้อกำหนดเบื้องต้น?** Java IDE, Aspose.Cells JAR, และไฟล์ Excel ที่มีข้อมูลตัวอย่าง

## วิธีการเพิ่ม tooltip คืออะไร?
**วิธีเพิ่ม tooltip** หมายถึงกระบวนการเปิดใช้งานข้อความเมื่อเมาส์ชี้ที่จะแสดงค่าของจุดข้อมูลหรือข้อมูลที่กำหนดเองบนแผนภูมิ Excel ใน Aspose.Cells สิ่งนี้ทำได้ผ่านการตั้งค่าป้ายข้อมูลของแผนภูมิ Tooltip ช่วยให้ผู้ใช้เข้าใจข้อมูลได้อย่างรวดเร็วโดยไม่ทำให้แผนภูมิเกะกะละมัง และสามารถปรับแต่งฟอนต์ สี และรูปแบบได้

## ทำไมต้องใช้แผนภูมิแบบโต้ตอบกับ Aspose.Cells?
Aspose.Cells รองรับ **รูปแบบการนำเข้าและส่งออกกว่า 50 แบบ**—รวมถึง XLSX, CSV, PDF, และ HTML—และสามารถประมวลผลเวิร์กบุ๊กที่มี **มากกว่า 1 000 แผ่น** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้การสร้างแผนภูมิบนเซิร์ฟเวอร์เร็วขึ้นสำหรับการรายงานระดับองค์กร แผนภูมิแบบโต้ตอบยังอนุญาตให้ฝังไฮเปอร์ลิงก์, การอัปเดตข้อมูลแบบไดนามิก, และการส่งออกเป็นรูปแบบที่เหมาะกับเว็บ ทำให้เหมาะสำหรับแดชบอร์ดและพอร์ทัลการรายงาน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java (แนะนำ JDK 8+)  
- ไลบรารี Aspose.Cells for Java (ดาวน์โหลดจาก [Aspose.Cells for Java download page](https://releases.aspose.com/cells/java/))  
- เวิร์กบุ๊กตัวอย่าง (`data.xlsx`) ที่มีข้อมูลที่คุณต้องการแสดงผล  

## ขั้นตอนที่ 1: ตั้งค่าโครงการ Java ของคุณ

1. สร้างโครงการ Java ใหม่ใน IDE ที่คุณชื่นชอบ (IntelliJ IDEA, Eclipse, ฯลฯ).  
2. เพิ่มไฟล์ JAR ของ Aspose.Cells ไปยังเส้นทางการสร้างของโครงการหรือ dependencies ของ Maven/Gradle.  

## ขั้นตอนที่ 2: โหลดข้อมูล

เพื่อทำงานกับแผนภูมิคุณต้องมีเวิร์กบุ๊กที่โหลดเข้าสู่หน่วยความจำก่อน

คลาส `Workbook` แทนไฟล์ Excel, และ `Worksheet` แทนแผ่นเดียวภายในไฟล์นั้น.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## วิธีการเปลี่ยนประเภทแผนภูมิใน Aspose.Cells?

สร้างแผนภูมิใหม่ด้วย `ChartType` enum ที่ต้องการ; Aspose.Cells ไม่แก้ไขประเภทของแผนภูมิที่มีอยู่โดยตรง, ดังนั้นคุณต้องเพิ่มแผนภูมิใหม่ที่มีประเภทที่ถูกต้องและอาจลบแผนภูมิเก่าออก วิธีนี้รับประกันว่าซีรีส์และแกนทั้งหมดจะถูกสร้างใหม่อย่างถูกต้องสำหรับการแสดงผลใหม่

## ขั้นตอนที่ 3: สร้างแผนภูมิ (และเปลี่ยนประเภทของมัน)

คุณสามารถเลือกประเภทแผนภูมิใดก็ได้ที่เหมาะกับการวิเคราะห์ของคุณ ด้านล่างเราจะสร้าง **แผนภูมิคอลัมน์**, แต่คุณสามารถสลับเป็นแผนภูมิเส้น, พาย, หรือบาร์ได้โดยการเปลี่ยน `ChartType` enum.

อ็อบเจ็กต์ `Chart` มีเมธอดสำหรับกำหนดการแสดงผลข้อมูลใน worksheet.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **เคล็ดลับ:** เพื่อ **เปลี่ยนประเภทแผนภูมิ Excel**, แทนที่ `ChartType.COLUMN` ด้วย `ChartType.LINE`, `ChartType.PIE` เป็นต้น.

## วิธีการเพิ่ม tooltip ให้กับแผนภูมิ Excel?

โหลดแผนภูมิของคุณ, เปิดใช้งานป้ายข้อมูล, และตั้งค่าแฟล็ก `showValue`. Tooltip จะทำการแสดงค่าของเซลล์พื้นฐานเมื่อผู้ใช้ชี้เมาส์ที่จุดข้อมูลในไฟล์ Excel ที่แสดงผลหรือมุมมอง HTML คุณยังสามารถปรับแต่งฟอนต์, สี, และพื้นหลังของ tooltip ให้ตรงกับสไตล์ของรายงานของคุณได้.

คลาส `DataLabel` ควบคุมลักษณะและเนื้อหาของป้ายข้อมูล, ซึ่งยังทำหน้าที่เป็น tooltip ด้วย.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## ขั้นตอนที่ 4: เพิ่มการโต้ตอบ

### 4.1. การเพิ่ม tooltip (add tooltips to chart)

Tooltip จะปรากฏเมื่อผู้ใช้ชี้เมาส์ที่จุดข้อมูล โค้ดต่อไปนี้เปิดใช้งานป้ายข้อมูลและแสดงค่าเป็น tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. การเพิ่มป้ายข้อมูล – **add data labels to excel chart**

ป้ายข้อมูลให้สัญญาณภาพถาวรบนแผนภูมิเอง คุณสามารถแสดงเป็น callout เพื่อความอ่านง่ายขึ้น.

คลาส `DataLabel` ควบคุมลักษณะของป้ายบนแต่ละซีรีส์ โดยเรียก `setHasDataLabels(true)` และกำหนดคุณสมบัติเช่น `setShowValue(true)`, คุณจะฝังค่าตัวเลขลงบนแผนภูมิโดยตรง ทำให้มองเห็นได้ทันทีโดยไม่ต้องโต้ตอบ ตัวเลือกเพิ่มเติมให้คุณแสดงชื่อซีรีส์, เปอร์เซ็นต์, หรือข้อความกำหนดเองเพื่อให้บริบทสมบูรณ์ยิ่งขึ้น.

> **ทำไมต้องเพิ่มป้ายข้อมูล?** การใส่ป้ายข้อมูลโดยตรงบนแผนภูมิทำให้ไม่ต้องให้ผู้ใช้ชี้เมาส์หรือเดาค่า ช่วยเพิ่มความชัดเจนของรายงาน

### 4.3. การทำ drill‑down (hyperlink on a data point)

วิธีง่ายๆ ในการเพิ่มความสามารถ drill‑down คือการแนบไฮเปอร์ลิงก์ไปยังจุดเฉพาะ การคลิกที่จุดนั้นจะเปิดหน้าเว็บที่มีข้อมูลรายละเอียด

คลาส `Hyperlink` แนบลิงก์ที่คลิกได้ไปยังองค์ประกอบของแผนภูมิ, ทำให้สามารถนำทางแบบ drill‑down ได้.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## วิธีการเพิ่มป้ายข้อมูลให้กับแผนภูมิ Excel?

คลาส `DataLabel` ควบคุมลักษณะของป้ายบนแต่ละซีรีส์ โดยเรียก `setHasDataLabels(true)` และกำหนดคุณสมบัติเช่น `setShowValue(true)`, คุณจะฝังค่าตัวเลขลงบนแผนภูมิโดยตรง ทำให้มองเห็นได้ทันทีโดยไม่ต้องโต้ตอบ ตัวเลือกเพิ่มเติมให้คุณแสดงชื่อซีรีส์, เปอร์เซ็นต์, หรือข้อความกำหนดเองเพื่อให้บริบทสมบูรณ์ยิ่งขึ้น.

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊ก

หลังจากกำหนดค่าแผนภูมิแล้ว ให้บันทึกเวิร์กบุ๊กเพื่อให้คุณลักษณะโต้ตอบถูกเก็บไว้ในไฟล์ผลลัพธ์.

การเรียก `workbook.save` จะเขียนเวิร์กบุ๊กที่แก้ไขแล้วลงไฟล์ในรูปแบบที่เลือก.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## ปัญหาทั่วไป & วิธีแก้

| ปัญหา | วิธีแก้ |
|-------|----------|
| **Tooltip ไม่แสดง** | ตรวจสอบว่าได้เรียก `setHasDataLabels(true)` ก่อนกำหนดค่า `setShowValue(true)`. |
| **ไฮเปอร์ลิงก์ไม่คลิกได้** | ตรวจสอบว่ารูปแบบผลลัพธ์รองรับไฮเปอร์ลิงก์ (เช่น XLSX, ไม่ใช่ CSV). |
| **ประเภทแผนภูมิไม่เปลี่ยน** | ตรวจสอบอีกครั้งว่าคุณได้แก้ไข `ChartType` enum ที่ถูกต้องเมื่อเพิ่มแผนภูมิ. |

## คำถามที่พบบ่อย

**Q: ฉันจะเปลี่ยนประเภทแผนภูมิหลังจากสร้างแล้วได้อย่างไร?**  
A: คุณต้องสร้างแผนภูมิใหม่ด้วย `ChartType` ที่ต้องการ Aspose.Cells ไม่รองรับการแปลงประเภทในที่เดียว, ดังนั้นให้ลบแผนภูมิเก่าและเพิ่มใหม่

**Q: ฉันสามารถปรับแต่งลักษณะของ tooltip ได้หรือไม่?**  
A: ได้. ใช้คุณสมบัติของ `DataLabel` เช่น `setFontSize`, `setFontColor`, และ `setBackgroundColor` เพื่อจัดรูปแบบข้อความ tooltip.

**Q: ฉันจะจัดการการโต้ตอบของผู้ใช้ในเว็บแอปพลิเคชันอย่างไร?**  
A: ส่งออกเวิร์กบุ๊กเป็นไฟล์ HTML หรือ XLSX และใช้ JavaScript ฝั่งไคลเอนต์เพื่อจับเหตุการณ์คลิกบนองค์ประกอบของแผนภูมิ.

**Q: ฉันจะหา ตัวอย่างและเอกสารเพิ่มเติมได้จากที่ไหน?**  
A: เยี่ยมชม [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) เพื่อดูรายการคลาสและเมธอดที่เกี่ยวกับแผนภูมิทั้งหมด.

## สรุป

คุณตอนนี้รู้วิธี **เพิ่มป้ายข้อมูลในแผนภูมิ Excel**, **เปลี่ยนประเภทแผนภูมิ Excel**, **สร้างโซลูชันแผนภูมิ Java แบบโต้ตอบ**, และเสริมด้วย tooltip, ป้ายข้อมูล, และไฮเปอร์ลิงก์ drill‑down ด้วย Aspose.Cells for Java การปรับปรุงเหล่านี้ทำให้รายงาน Excel ของคุณน่าสนใจและให้ข้อมูลเชิงลึกมากขึ้นสำหรับผู้ใช้ปลายทาง.

---

**อัปเดตล่าสุด:** 2026-08-21  
**ทดสอบกับ:** Aspose.Cells for Java 24.12  
**ผู้เขียน:** Aspose

## บทเรียนที่เกี่ยวข้อง

- [วิธีแก้ไขแผนภูมิ Excel และป้ายข้อมูลโดยใช้ Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [สกัดป้ายแกนแผนภูมิ Excel ด้วย Aspose.Cells Java: คู่มือฉบับสมบูรณ์](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [สร้างแผนภูมิบับเบิลใน Excel ด้วย Aspose.Cells for Java: คู่มือทีละขั้นตอน](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}