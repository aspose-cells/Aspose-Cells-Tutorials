---
date: 2026-09-02
description: เรียนรู้วิธีส่งออกแผนภูมิเป็น PNG, เพิ่มชุดข้อมูล, รวมแผนภูมิ line column
  chart, บันทึก workbook เป็น XLSX และเพิ่ม legend chart ด้วย Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: ส่งออกแผนภูมิเป็น PNG และเพิ่มชุดข้อมูลสำหรับแผนภูมิรวม
og_description: ส่งออกแผนภูมิเป็น PNG ด้วย Aspose.Cells for Java, รวม line and column
  chart, เพิ่มชุดข้อมูล, และบันทึก workbook เป็น XLSX ในบทแนะนำเดียว
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: ส่งออกแผนภูมิเป็น PNG และเพิ่มชุดข้อมูลสำหรับแผนภูมิรวม
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: ส่งออกแผนภูมิเป็น PNG และเพิ่มชุดข้อมูลสำหรับแผนภูมิรวม
url: /th/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิเป็น PNG และเพิ่มชุดข้อมูลสำหรับแผนภูมิรวม

ในบทแนะนำนี้คุณจะ **เพิ่มชุดข้อมูล** ไปยังสมุดงาน Excel, **รวมแผนภูมิเส้นและคอลัมน์** และเรียนรู้วิธี **ส่งออกแผนภูมิเป็น PNG** ด้วย Aspose.Cells for Java เราจะเดินผ่านทุกขั้นตอน—ตั้งแต่การตั้งค่าสมุดงาน, การเพิ่มแผนภูมิลงในแผ่นงาน, การปรับแต่งคำอธิบาย, จนถึง **บันทึกสมุดงานเป็น XLSX** และสร้างภาพ PNG ของแผนภูมิ เมื่อเสร็จคุณจะมีแผนภูมิรวมที่พร้อมใช้งานซึ่งสามารถฝังในรายงานหรือแดชบอร์ดได้

## คำตอบสั้น
- **Which library creates combined charts?** Aspose.Cells for Java.  
- **How do I add a data series?** Call `chart.getNSeries().add(...)` with the appropriate range.  
- **How can I export chart to PNG?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **What file format can I save the workbook as?** Standard `.xlsx` (save workbook as XLSX).  
- **Do I need a license for production?** Yes – a valid Aspose.Cells license is required for production deployments.

## การส่งออกแผนภูมิเป็น PNG ใน Aspose.Cells คืออะไร
การส่งออกแผนภูมิเป็น PNG จะสร้างภาพเรสเตอร์ของแผนภูมิ Excel ที่สามารถแสดงในหน้าเว็บ, รายงาน หรืออีเมลได้โดยไม่ต้องใช้แอปพลิเคชัน Excel วิธีนี้บันทึกเลย์เอาต์, สี, และเครื่องหมายข้อมูลอย่างแม่นยำ ทำให้ได้ไฟล์ภาพที่พกพาได้

## ทำไมต้องสร้างแผนภูมิรวมเส้นและคอลัมน์
แผนภูมิรวมเส้น‑คอลัมน์ช่วยให้คุณแสดงชุดข้อมูลที่แตกต่างกันด้วยการนำเสนอที่แตกต่างกัน (เช่น ชุดเส้นเหนือชุดคอลัมน์) ในมุมมองเดียว วิธีนี้เหมาะสำหรับการเปรียบเทียบแนวโน้มกับยอดรวม, เน้นความสัมพันธ์, หรือให้ข้อมูลเชิงลึกที่หลากหลายโดยคงขนาดภาพให้เล็กลง

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือสูงกว่า  
- Aspose.Cells for Java library (download from the link below)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และแนวคิด Excel  

## เริ่มต้น

ขั้นแรก ดาวน์โหลดไลบรารี Aspose.Cells for Java จากเว็บไซต์อย่างเป็นทางการ:

[ดาวน์โหลด Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

เมื่อเพิ่ม JAR ลงใน classpath ของโครงการแล้ว คุณสามารถเริ่มสร้างแผนภูมิได้

### ขั้นตอนที่ 1: นำเข้าคลาส aspose.cells
`Workbook` คืออ็อบเจ็กต์หลักของ Aspose.Cells ที่แสดงไฟล์ Excel ทั้งหมดในหน่วยความจำ.  
```java
import com.aspose.cells.*;
```

### ขั้นตอนที่ 2: สร้างสมุดงานใหม่
`Worksheet` แสดงแผ่นงานเดี่ยวภายใน `Workbook` และให้เข้าถึงเซลล์, แถว, และแผนภูมิ.  
```java
Workbook workbook = new Workbook();
```

### ขั้นตอนที่ 3: เข้าถึงแผ่นงานแรก
`Chart` คืออ็อบเจ็กต์ที่เก็บการตั้งค่าที่เกี่ยวกับแผนภูมิทั้งหมด, ชุดข้อมูล, และตัวเลือกการเรนเดอร์.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### ขั้นตอนที่ 4: เพิ่มอ็อบเจ็กต์แผนภูมิรวมลงในแผ่นงาน  
เราจะเริ่มด้วยแผนภูมิเส้นและต่อมาจะเพิ่มชุดคอลัมน์เพื่อให้ได้ผลลัพธ์ **แผนภูมิรวมเส้นคอลัมน์**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## เพิ่มข้อมูลลงในแผนภูมิ

ตอนนี้คอนเทนเนอร์ของแผนภูมิมีอยู่แล้ว เราต้องป้อนข้อมูลให้มัน

### ขั้นตอนที่ 5: กำหนดช่วงข้อมูลและเพิ่มชุดข้อมูล
`NSeries` เป็นคอลเลกชันที่เก็บชุดข้อมูลแต่ละชุดสำหรับแผนภูมิ การเพิ่มชุดข้อมูลจะเชื่อมช่วงเซลล์กับแผนภูมิ.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** พารามิเตอร์แรก (`"A1:A5"`) คือช่วงสำหรับชุดแรก, และพารามิเตอร์ที่สอง (`"B1:B5"`) สร้างชุดที่สองที่จะรวมกับชุดแรก

### ขั้นตอนที่ 6: ตั้งค่าข้อมูลหมวดหมู่ (แกน X)
`CategoryAxis` แทนแกนแนวนอนของแผนภูมิ, ควบคุมป้ายที่แสดงตามแกน X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## ปรับแต่งแผนภูมิ

แผนภูมิที่ดีบอกเล่าเรื่องราว ให้เราตั้งชื่อ, ป้ายแกน, และคำอธิบายที่ชัดเจน

### ขั้นตอนที่ 7: ตั้งค่าป้ายแกนและชื่อเรื่องของแผนภูมิ
`Title` ตั้งชื่อหลักของแผนภูมิ, และอ็อบเจ็กต์ `Axis` แทนแกน X และ Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### ขั้นตอนที่ 8: เพิ่มคำอธิบายแผนภูมิและปรับตำแหน่ง
`Legend` ควบคุมตำแหน่งและลักษณะของคำอธิบายชุดข้อมูลในแผนภูมิ.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## การบันทึกและส่งออกแผนภูมิ

หลังจากปรับแต่งแล้ว คุณจะต้อง **บันทึกสมุดงานเป็น XLSX** และสร้างภาพด้วย

### ขั้นตอนที่ 9: บันทึกสมุดงานเป็นไฟล์ Excel (XLSX)
`Workbook.save` เขียนสมุดงานในหน่วยความจำลงไฟล์ในรูปแบบที่ระบุ.  
```java
workbook.save("CombinedChart.xlsx");
```

### ขั้นตอนที่ 10: ส่งออกแผนภูมิเป็น PNG
`Chart.toImage` แสดงแผนภูมิเป็นไฟล์ภาพในรูปแบบที่เลือก.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> วิธี `chart.toImage` **สร้างภาพแผนภูมิ Excel** ที่สามารถใช้ในหน้าเว็บ, รายงาน, หรืออีเมลได้

## ปัญหาทั่วไปและการแก้ไขปัญหา

| ปัญหา | วิธีแก้ |
|-------|----------|
| **No data appears** | ตรวจสอบว่าช่วงเซลล์ (`A1:A5`, `B1:B5`, `C1:C5`) มีข้อมูลจริงก่อนสร้างแผนภูมิ |
| **Legend overlaps chart** | ตั้งค่า `chart.getLegend().setOverlay(false)` หรือย้ายคำอธิบายไปตำแหน่งอื่น (เช่น `RIGHT`) |
| **Image file is blank** | ตรวจสอบว่าแผนภูมิมีอย่างน้อยหนึ่งชุดข้อมูลและว่า `chart.toImage` ถูกเรียกหลังจากการปรับแต่งทั้งหมด |
| **Saving throws an exception** | ตรวจสอบว่าคุณมีสิทธิ์เขียนไปยังไดเรกทอรีเป้าหมายและไฟล์ไม่ได้เปิดอยู่ใน Excel |

## คำถามที่พบบ่อย

**Q: ฉันจะติดตั้ง Aspose.Cells for Java อย่างไร?**  
A: ดาวน์โหลด JAR จากเว็บไซต์อย่างเป็นทางการและเพิ่มลงใน classpath ของโครงการของคุณ ลิงก์ดาวน์โหลดคือ: [ดาวน์โหลด Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

**Q: ฉันสามารถสร้างแผนภูมิประเภทอื่นนอกจากเส้นและคอลัมน์ได้หรือไม่?**  
A: ได้, Aspose.Cells รองรับแผนภูมิแท่ง, พาย, กระจาย, พื้นที่, และหลายประเภทอื่น ๆ ดูเอกสาร API เพื่อรายการเต็ม

**Q: จำเป็นต้องมีใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?**  
A: จำเป็นต้องมีใบอนุญาต Aspose.Cells ที่ถูกต้องสำหรับการใช้งานในผลิตภัณฑ์ มีรุ่นทดลองฟรีสำหรับการประเมิน

**Q: ฉันจะเปลี่ยนสีของแต่ละชุดข้อมูลได้อย่างไร?**  
A: ใช้ `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (หรือวิธีที่คล้ายกัน) หลังจากเพิ่มชุดข้อมูล

**Q: จะหาโค้ดตัวอย่างเพิ่มเติมได้จากที่ไหน?**  
A: เอกสารครบถ้วนและตัวอย่างเพิ่มเติมมีให้ที่เว็บไซต์อ้างอิงของ Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/)

---

**อัปเดตล่าสุด:** 2026-09-02  
**ทดสอบกับ:** Aspose.Cells for Java รุ่นล่าสุด  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเพิ่มป้ายกำกับในแผนภูมิ Excel ด้วย Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [วิธีสร้างแผนภูมิ Excel พร้อมเส้นแนวโน้มและส่งออกเป็นภาพโดยใช้ Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [ส่งออกแผนภูมิ Excel เป็น PDF ด้วย Aspose.Cells for Java: คู่มือขนาดหน้ากระดาษแบบกำหนดเอง](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}