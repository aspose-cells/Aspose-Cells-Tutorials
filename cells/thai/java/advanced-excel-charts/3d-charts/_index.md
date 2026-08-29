---
date: 2026-08-21
description: เรียนรู้วิธีส่งออกแผนภูมิเป็นภาพและสร้างแผนภูมิวงกลม 3 มิติใน Java ด้วย
  Aspose.Cells. สร้างแผนภูมิแท่ง 3 มิติ, เพิ่มแผนภูมิ 3 มิติลงใน Excel, และบันทึกเวิร์กบุ๊กเป็น
  XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: สร้างแผนภูมิวงกลม 3 มิติใน Java
og_description: ส่งออกแผนภูมิเป็นภาพและสร้างแผนภูมิวงกลม 3 มิติใน Java ด้วย Aspose.Cells.
  คู่มือขั้นตอนต่อขั้นตอนสำหรับการสร้างแผนภูมิแท่งและแผนภูมิวงกลม 3 มิติ, ปรับแต่งแผนภูมิ,
  และบันทึกเวิร์กบุ๊กเป็น XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: ส่งออกแผนภูมิเป็นภาพและสร้างแผนภูมิวงกลม 3 มิติใน Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: วิธีส่งออกแผนภูมิเป็นภาพและสร้างแผนภูมิวงกลม 3 มิติใน Java
url: /th/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผนภูมิวงกลม 3 มิติ Java

## บทนำสู่แผนภูมิ 3 มิติ

Aspose.Cells for Java เป็น API ของ Java ที่มีประสิทธิภาพสำหรับการทำงานกับไฟล์ Excel และทำให้การ **create 3d pie chart** โครงการเป็นเรื่องง่ายเช่นเดียวกับการแสดงผลแผนภูมิแท่ง 3‑D แบบคลาสสิก ในบทแนะนำนี้คุณจะได้เห็นวิธี **export chart as image** อย่างชัดเจน, สร้างแผนภูมิแท่ง 3‑D, ปรับวิธีเดียวกันสำหรับแผนภูมิวงกลม 3‑D, ปรับแต่งลักษณะการแสดงผล, และสุดท้าย **add 3d chart excel** ไฟล์ไปยังรายงานของคุณ ไม่ว่าคุณจะสร้างแดชบอร์ดการเงิน, แผ่นงานประสิทธิภาพการขาย, หรือการแสดงข้อมูลทางวิทยาศาสตร์ ขั้นตอนต่อไปนี้จะให้พื้นฐานที่มั่นคงแก่คุณ.

## คำตอบอย่างรวดเร็ว
- **ต้องการไลบรารีอะไร?** Aspose.Cells for Java (latest version)  
- **ฉันสามารถสร้างแผนภูมิแท่ง 3D ได้หรือไม่?** Yes – use `ChartType.BAR_3_D`  
- **ฉันต้องการใบอนุญาตหรือไม่?** A valid license removes evaluation limits  
- **เวอร์ชันของ Excel ที่รองรับมีอะไรบ้าง?** All major versions from 2003 to 2023  
- **สามารถส่งออกแผนภูมิเป็นภาพได้หรือไม่?** Yes – call `chart.toImage()` after the chart is created  

## แผนภูมิ 3D คืออะไร?
แผนภูมิ 3D เพิ่มความลึกให้กับการแสดงผลแบบ 2D แบบดั้งเดิม ช่วยให้ผู้ชมเข้าใจความสัมพันธ์หลายมิติได้อย่างเป็นธรรมชาติ พวกมันมีประโยชน์โดยเฉพาะเมื่อคุณต้องการเปรียบเทียบหลายหมวดหมู่เคียงข้างกันพร้อมกับคงลำดับชั้นการมองเห็นที่ชัดเจน โดยการเพิ่มมิติที่สาม แผนภูมิเหล่านี้สามารถเน้นความแตกต่างในขนาดที่อาจไม่ชัดเจนในรูปแบบแบน ทำให้ข้อมูลที่ซับซ้อนง่ายต่อการตีความสำหรับผู้มีส่วนได้ส่วนเสียทางธุรกิจ.

## ทำไมต้องใช้ Aspose.Cells for Java เพื่อสร้างแผนภูมิแท่ง 3D?
Aspose.Cells for Java มีประเภทแผนภูมิกว่า 150 แบบในตัวและรองรับฟังก์ชัน Excel มากกว่า 100 รายการ ให้คุณมีเอนจินที่เต็มรูปแบบซึ่งทำงานได้กับทุกเวอร์ชันของ Excel ตั้งแต่ 2003 ถึง 2023 โดยไม่ต้องใช้ Microsoft Office ซึ่งหมายความว่าคุณสามารถ **generate 3d bar chart** วัตถุได้โดยอัตโนมัติด้วยผลลัพธ์ที่คาดเดาได้และการใช้ทรัพยากรที่น้อยที่สุด.

## การตั้งค่า Aspose.Cells for Java

### ดาวน์โหลดและการติดตั้ง
คุณสามารถดาวน์โหลดไลบรารี Aspose.Cells for Java จากเว็บไซต์ทางการได้ ปฏิบัติตามคำแนะนำ Maven/Gradle ที่ให้มา หรือเพิ่มไฟล์ JAR ลงใน classpath ของโครงการของคุณโดยตรง.

### การเริ่มต้นใบอนุญาต
คลาส `License` ใช้เพื่อใช้ใบอนุญาต Aspose.Cells ของคุณและปลดล็อกฟังก์ชันเต็มรูปแบบ.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## สร้างแผนภูมิ 3D เบื้องต้น

### การนำเข้าห้องสมุดที่จำเป็น
ก่อนอื่น ให้นำคลาสที่จำเป็นเข้ามาในสโคป:  
```java
import com.aspose.cells.*;
```

### การเริ่มต้นเวิร์กบุ๊ก
สร้างเวิร์กบุ๊กใหม่ที่จะเป็นที่เก็บแผนภูมิ:  
```java
Workbook workbook = new Workbook();
```

### การเพิ่มข้อมูลลงในแผนภูมิ
เติมข้อมูลตัวอย่างลงในแผ่นงานที่แผนภูมิจะอ้างอิงถึง:  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## วิธีสร้างแผนภูมิแท่ง 3D ใน Java
เพื่อสร้างแผนภูมิแท่ง 3D คุณต้องเพิ่มอ็อบเจ็กต์แผนภูมิลงในแผ่นงาน ตั้งค่าชนิดเป็น `ChartType.BAR_3_D` แล้วผูกชุดข้อมูลกับเซลล์ที่มีค่าของคุณ หลังจากกำหนดลักษณะการแสดงของแผนภูมิแล้ว คุณสามารถเรนเดอร์หรือส่งออกตามต้องการ.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## การบันทึกแผนภูมิลงไฟล์
สุดท้าย ให้เขียนเวิร์กบุ๊ก (ซึ่งตอนนี้มีแผนภูมิ 3‑D อยู่) ลงดิสก์ ซึ่งยังทำการ **save workbook xlsx** ในรูปแบบมาตรฐานของ Excel:  
```java
workbook.save("3D_Chart.xlsx");
```

## วิธีสร้างแผนภูมิวงกลม 3D ด้วย Aspose.Cells for Java
หากคุณต้องการการแสดงผลแบบวงกลม กระบวนการทำงานจะเกือบเหมือนกัน—เพียงแค่ค่า enum `ChartType` เปลี่ยนเท่านั้น แทนที่ `ChartType.BAR_3_D` ด้วย `ChartType.PIE_3_D` เมื่อเพิ่มแผนภูมิ และชี้ชุดข้อมูลไปยังช่วงข้อมูลเดียวกัน หลังจากสร้างแผนภูมิแล้วคุณสามารถตั้งชื่อเรื่องที่อธิบายได้ ปรับสีของส่วน และส่งออกผลลัพธ์เป็นภาพ วิธีนี้ทำให้คุณสามารถใช้โค้ดการเตรียมข้อมูลเดียวกันได้อีกครั้งในขณะที่นำเสนอภาพมุมมองที่แตกต่าง.

## วิธีส่งออกแผนภูมิเป็นภาพใน Java
เมธอด `toImage` ของอ็อบเจ็กต์ `Chart` จะบันทึกแผนภูมิเป็นไฟล์ภาพ คุณสามารถส่งออกแผนภูมิ 3D ใด ๆ ไปเป็นภาพเรสเตอร์ด้วยการเรียกครั้งเดียว: `chart.toImage("myChart.png", ImageFormat.getPng())`. เมธอดนี้เรนเดอร์แผนภูมิเช่นเดียวกับที่แสดงใน Excel โดยคงความลึก 3‑D สีและคำอธิบายไว้ และเขียนผลลัพธ์ไปยังเส้นทางไฟล์ที่ระบุ ใช้ PNG เพื่อคุณภาพที่ไม่สูญเสียหรือ JPEG เพื่อขนาดไฟล์ที่เล็กลงเมื่อฝังภาพในรายงานเว็บ.

## ประเภทต่าง ๆ ของแผนภูมิ 3D
Aspose.Cells for Java รองรับหลายรูปแบบของแผนภูมิ 3D ที่คุณสามารถ **add 3d chart excel** ไฟล์ได้:
- **Bar charts** – เหมาะสำหรับการเปรียบเทียบหมวดหมู่.  
- **Pie charts** – แสดงส่วนแบ่งตามสัดส่วน (รวมถึง 3D pie).  
- **Line charts** – แสดงแนวโน้มตามเวลา.  
- **Area charts** – เน้นขนาดของการเปลี่ยนแปลง.  

คุณสามารถสลับค่า enum `ChartType` ไปยังใด ๆ ข้างต้นได้โดยคงรูปแบบการสร้างเดียวกัน.

## การปรับแต่งแผนภูมิขั้นสูง

### การเพิ่มหัวเรื่องและป้ายกำกับ
ให้บริบทกับแผนภูมิของคุณโดยตั้งชื่อเรื่องที่อธิบายและป้ายแกน.

### การปรับสีและสไตล์
ใช้เมธอด `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` เพื่อให้ตรงกับแบรนด์ขององค์กร.

### การทำงานกับแกนของแผนภูมิ
ปรับแต่งสเกลของแกน ช่วงเวลา และเครื่องหมายติ๊กเพื่อเพิ่มความอ่านง่าย.

### การเพิ่มคำอธิบาย
เปิดใช้งานคำอธิบายด้วย `chart.getLegend().setVisible(true)` เพื่อให้ผู้ชมสามารถระบุชุดข้อมูลแต่ละชุดได้.

### การส่งออกแผนภูมิเป็นภาพ
เมื่อคุณต้องการภาพคงที่สำหรับรายงานเว็บ ให้เรียก `chart.toImage("chart.png", ImageFormat.getPng())`. สิ่งนี้ตอบสนองกรณีการใช้ **convert chart png** โดยไม่ต้องออกจากเวิร์กบุ๊ก.

## การบูรณาการข้อมูล
Aspose.Cells for Java สามารถดึงข้อมูลจากฐานข้อมูล ไฟล์ CSV หรือ API สดได้ เพียงเติมข้อมูลลงในเซลล์ของแผ่นงานด้วยข้อมูลที่ดึงมา ก่อนเชื่อมช่วงข้อมูลกับแผนภูมิ วิธีนี้ทำให้กระบวนการ **add 3d chart excel** ของคุณเป็นแบบไดนามิกและเป็นปัจจุบัน.

## สรุป
ในคู่มือนี้ เราได้อธิบายขั้นตอนการ **create 3d pie chart** และ **create 3d bar chart** ตั้งแต่ต้นจนจบ—การตั้งค่าไลบรารี การเพิ่มข้อมูล การสร้างแผนภูมิแท่ง 3‑D การปรับขั้นตอนเดียวกันสำหรับแผนภูมิวงกลม 3‑D และการใช้สไตล์ขั้นสูง ด้วย Aspose.Cells for Java คุณจะมีวิธีที่เชื่อถือได้และไม่ขึ้นกับเวอร์ชันในการฝังการแสดงผล 3‑D ที่สมบูรณ์แบบโดยตรงในเวิร์กบุ๊ก Excel และแม้กระทั่ง **export chart as image** เพื่อใช้ในแดชบอร์ดหรือรายงาน.

## คำถามที่พบบ่อย

**Q: ฉันจะเพิ่มหลายชุดข้อมูลในแผนภูมิ 3D ได้อย่างไร?**  
A: ใช้ `chart.getNSeries().add()` สำหรับแต่ละช่วงของชุดข้อมูลและตรวจสอบให้แน่ใจว่าชนิดของแผนภูมอยังคงเป็น 3‑D (เช่น `ChartType.BAR_3_D` หรือ `ChartType.PIE_3_D`).

**Q: ฉันสามารถส่งออกแผนภูมิ 3D ที่สร้างด้วย Aspose.Cells for Java ไปเป็นรูปแบบอื่นได้หรือไม่?**  
A: ได้ คุณสามารถบันทึกแผนภูมิเป็น PNG, JPEG หรือ PDF โดยเรียก overload ของ `chart.toImage()` ที่เหมาะสมหรือ `workbook.save()` พร้อมรูปแบบภาพหรือ PDF ซึ่งตอบสนองความต้องการ **convert chart png**.

**Q: สามารถสร้างแผนภูมิ 3D แบบโต้ตอบด้วย Aspose.Cells for Java ได้หรือไม่?**  
A: Aspose.Cells มุ่งเน้นที่แผนภูมิ Excel แบบคงที่ สำหรับการแสดงผล 3‑D แบบโต้ตอบบนเว็บ ให้พิจารณาเชื่อมข้อมูล Excel กับไลบรารี JavaScript เช่น Three.js.

**Q: ฉันสามารถทำกระบวนการอัปเดตข้อมูลในแผนภูมิ 3D ของฉันโดยอัตโนมัติได้หรือไม่?**  
A: แน่นอน โหลดข้อมูลใหม่เข้าสู่แผ่นงานโดยอัตโนมัติและรีเฟรชช่วงของแผนภูมิ; ครั้งต่อไปที่เปิดเวิร์กบุ๊ก แผนภูมิจะแสดงค่าที่อัปเดต.

**Q: ฉันจะหาแหล่งข้อมูลและเอกสารเพิ่มเติมสำหรับ Aspose.Cells for Java ได้จากที่ไหน?**  
A: คุณสามารถค้นหาเอกสารและแหล่งข้อมูลที่ครอบคลุมสำหรับ Aspose.Cells for Java ได้ที่เว็บไซต์: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**อัปเดตล่าสุด:** 2026-08-21  
**ทดสอบด้วย:** Aspose.Cells for Java 24.12 (latest)  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [สร้างแผนภูมิวงกลมใน Excel ด้วย Aspose.Cells for Java: คู่มือครบถ้วน](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – สร้างแผนภูมิ Excel พร้อมคำอธิบาย](/cells/java/advanced-excel-charts/chart-annotations/)
- [เพิ่มป้ายข้อมูลในแผนภูมิ Excel ด้วย Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}