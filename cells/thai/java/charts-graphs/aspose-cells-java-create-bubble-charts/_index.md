---
date: '2026-04-02'
description: เรียนรู้วิธีสร้างแผนภูมิและสร้างแผนภูมิบับเบิลใน Excel ด้วย Aspose.Cells
  สำหรับ Java คู่มือนี้จะพาคุณผ่านขั้นตอนการตั้งค่า ข้อมูล และการบันทึกแผนภูมิ.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'วิธีสร้างแผนภูมิ: แผนภูมิบับเบิลใน Excel ด้วย Aspose.Cells Java'
url: /th/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างแผนภูมิ: แผนภูมิบับเบิลใน Excel ด้วย Aspose.Cells Java

ปรับปรุงรายงาน Excel ของคุณด้วยแผนภูมิบับเบิลแบบไดนามิกโดยใช้ Aspose.Cells for Java ในบทเรียนนี้ คุณจะได้เรียนรู้ **วิธีสร้างแผนภูมิ** ที่แสดงข้อมูลเป็นแผนภูมิบับเบิล ทำให้การนำเสนอของคุณมีความเข้าใจลึกซึ้งและโต้ตอบได้มากขึ้น เราจะเดินผ่านทุกขั้นตอน—from การตั้งค่าสภาพแวดล้อมการพัฒนา ไปจนถึงการกำหนดค่าข้อมูลแผนภูมิและสุดท้ายการบันทึกเวิร์กบุ๊ก.

## คำตอบด่วน
- **ไลบรารีที่ดีที่สุดสำหรับแผนภูมิ Excel ใน Java คืออะไร?** Aspose.Cells for Java.
- **ฉันสามารถสร้างแผนภูมิบับเบิลใน Excel ด้วยโปรแกรมได้หรือไม่?** ใช่, โดยใช้ API ของแผนภูมิที่แสดงด้านล่าง.
- **ฉันต้องมีลิขสิทธิ์เพื่อรันโค้ดหรือไม่?** การทดลองใช้ฟรีทำงานได้, แต่ลิขสิทธิ์เต็มจะเปิดใช้งานคุณสมบัติทั้งหมด.
- **เครื่องมือสร้าง Java ใดที่รองรับ?** Maven และ Gradle ทั้งสองได้รับการสนับสนุน.
- **วิธีหลักในการตั้งค่าข้อมูลแผนภูมิบับเบิลคืออะไร?** ใช้ `setBubbleSizes`, `setXValues`, และ `setValues` บน series.

## แผนภูมิบับเบิลคืออะไร?
แผนภูมิบับเบิลเป็นรูปแบบหนึ่งของกราฟกระจายที่แต่ละจุดข้อมูลจะแสดงเป็นฟอง. แกน X และแกน Y กำหนดตำแหน่ง, ส่วนขนาดของฟองบ่งบอกมิติที่สามของข้อมูล — เหมาะอย่างยิ่งสำหรับการแสดงข้อมูลทางการเงิน, การขาย, หรือวิทยาศาสตร์.

## ทำไมต้องใช้ Aspose.Cells for Java?
- **เครื่องยนต์ Excel แบบไม่มีการติดตั้ง** – ไม่จำเป็นต้องมี Microsoft Office บนเซิร์ฟเวอร์.
- **API การสร้างแผนภูมิที่ครบครัน** – รองรับประเภทแผนภูมิสมัยใหม่ทั้งหมด รวมถึงแผนภูมิบับเบิล.
- **ข้ามแพลตฟอร์ม** – ทำงานบน Windows, Linux, และ macOS.
- **ประสิทธิภาพสูง** – ปรับให้เหมาะกับชุดข้อมูลขนาดใหญ่และการสร้างรายงานปริมาณมาก.

## ข้อกำหนดเบื้องต้น
เพื่อสร้างแผนภูมิบับเบิลโดยใช้ Aspose.Cells for Java, โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้:

### ไลบรารีและการพึ่งพาที่จำเป็น
- **Aspose.Cells for Java**: ติดตั้งเวอร์ชันล่าสุด (เช่น 25.3).

### ความต้องการการตั้งค่าสภาพแวดล้อม
- ติดตั้ง Java Development Kit (JDK) ที่เข้ากันได้.
- กำหนดค่าโปรเจกต์ของคุณให้ใช้ Maven หรือ Gradle.

### ความรู้เบื้องต้นที่จำเป็น
- ความเข้าใจพื้นฐานของการเขียนโปรแกรม Java.
- ความคุ้นเคยกับโครงสร้างไฟล์ Excel และประเภทแผนภูมิ.

## การตั้งค่า Aspose.Cells for Java
การตั้งค่าสภาพแวดล้อมของคุณเป็นสิ่งสำคัญ นี่คือวิธีเริ่มต้น:

### การติดตั้งผ่าน Maven
เพิ่มการพึ่งพาต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### การติดตั้งผ่าน Gradle
สำหรับผู้ใช้ Gradle, เพิ่มบรรทัดนี้ในไฟล์ `build.gradle` ของคุณ:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### การได้รับลิขสิทธิ์
Aspose.Cells มีการทดลองใช้ฟรีพร้อมฟังก์ชันจำกัด สำหรับความสามารถเต็มรูปแบบ:
- **ซื้อ**: เยี่ยมชม [purchase page](https://purchase.aspose.com/buy) เพื่อดูตัวเลือกการให้ลิขสิทธิ์.
- **ลิขสิทธิ์ชั่วคราว**: รับลิขสิทธิ์ชั่วคราวจาก [here](https://purchase.aspose.com/temporary-license/) เพื่อทดสอบเต็มรูปแบบ.

### การเริ่มต้นพื้นฐาน
ก่อนใช้ Aspose.Cells, ให้ทำการเริ่มต้นในโปรเจกต์ Java ของคุณ:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## คู่มือการดำเนินการ
เราจะอธิบายขั้นตอนการสร้างและกำหนดค่าแผนภูมิบับเบิลด้วย Aspose.Cells.

### วิธีสร้างแผนภูมิ: การเริ่มต้นอ็อบเจ็กต์ Workbook
`Workbook` แทนไฟล์ Excel ทั้งไฟล์, ให้คุณจัดการแผ่นงาน, เซลล์, และอื่น ๆ ได้ เริ่มต้นโดยทำตามนี้:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### วิธีตั้งค่าข้อมูลแผนภูมิบับเบิล: การเข้าถึงและจัดการ Worksheet
เตรียมข้อมูลที่จะใช้เป็นแหล่งข้อมูลให้กับแผนภูมิบับเบิล:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### วิธีสร้างแผนภูมิบับเบิลใน Excel: การสร้างและกำหนดค่าแผนภูมิ
สร้างแผนภูมิบับเบิลโดยเพิ่มลงใน Worksheet และกำหนดแหล่งข้อมูลของมัน:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### วิธีบันทึกแผนภูมิ: การบันทึก Workbook
บันทึก Workbook (และแผนภูมิที่ฝังอยู่) ลงดิสก์:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## การประยุกต์ใช้งานจริง
- **การรายงานทางการเงิน** – แสดงรายได้, กำไร, และส่วนแบ่งตลาดในมุมมองเดียว.
- **การวิเคราะห์ข้อมูลการขาย** – เน้นประสิทธิภาพการขายตามภูมิภาคโดยให้ขนาดฟองแสดงปริมาณ.
- **การวิจัยทางวิทยาศาสตร์** – แสดงผลการทดลองที่มีสามตัวแปรพร้อมกัน.

## การพิจารณาด้านประสิทธิภาพ
- ทำลายอ็อบเจ็กต์ที่ไม่ได้ใช้โดยเร็วเพื่อคืนหน่วยความจำ.
- ทำให้ช่วงข้อมูลแคบที่สุดเท่าที่จะเป็นไปได้; ช่วงที่ใหญ่เกินความจำเป็นอาจทำให้การเรนเดอร์ช้า.
- ใช้แนวทางปฏิบัติที่ดีที่สุดของการจัดการหน่วยความจำใน Java เมื่อประมวลผลชุดข้อมูลขนาดใหญ่.

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|----------|
| **แผนภูมิว่าง** | ช่วงข้อมูลไม่ตรงกับ series | ตรวจสอบว่า `setBubbleSizes`, `setXValues`, และ `setValues` อ้างอิงเซลล์ที่ถูกต้อง. |
| **ขนาดฟองไม่ถูกต้อง** | ความยาวช่วงไม่ตรงกัน | ตรวจสอบให้แน่ใจว่าช่วงทั้งสามมีจำนวนจุดเท่ากัน. |
| **ข้อยกเว้นลิขสิทธิ์** | รันโดยไม่มีลิขสิทธิ์ที่ถูกต้อง | ใช้ลิขสิทธิ์ชั่วคราวหรือที่ซื้อก่อนสร้าง workbook. |

## คำถามที่พบบ่อย

**Q: เวอร์ชันขั้นต่ำของ Aspose.Cells ที่ต้องการคืออะไร?**  
A: แนะนำให้ใช้เวอร์ชัน 25.3 สำหรับบทเรียนนี้เพื่อให้แน่ใจว่ารองรับคุณลักษณะที่แสดงทั้งหมด.

**Q: ฉันจะปรับแต่งสีของแผนภูมิบับเบิลได้อย่างไร?**  
A: ใช้วิธีการจัดรูปแบบของ series, เช่น `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**Q: ฉันสามารถรันโค้ดนี้บนเซิร์ฟเวอร์ Linux ได้หรือไม่?**  
A: ได้, Aspose.Cells for Java รองรับข้ามแพลตฟอร์มเต็มรูปแบบและทำงานบน OS ใดก็ได้ที่มี JDK ที่เข้ากันได้.

**Q: ควรทำอย่างไรหากได้รับข้อผิดพลาด “Data source size mismatch”?**  
A: ตรวจสอบอีกครั้งว่าช่วงของขนาดฟอง, ค่า X, และค่า Y มีจำนวนเซลล์เท่ากัน.

**Q: ฉันสามารถรับลิขสิทธิ์ชั่วคราวสำหรับการทดสอบได้จากที่ไหน?**  
A: เยี่ยมชม [Aspose's temporary license page](https://purchase.aspose.com/temporary-license/) เพื่อขอรับลิขสิทธิ์ทดลอง.

## แหล่งข้อมูล
- **เอกสาร**: สำหรับรายละเอียดเพิ่มเติม, ดูที่ [official documentation](https://reference.aspose.com/cells/java/).
- **ดาวน์โหลด**: รับเวอร์ชันล่าสุดจาก [the release page](https://releases.aspose.com/cells/java/).
- **ซื้อ**: สำรวจตัวเลือกการให้ลิขสิทธิ์ที่ [this page](https://purchase.aspose.com/buy).
- **ทดลองใช้ฟรี**: เริ่มต้นด้วยการทดลองใช้ฟรีเพื่อทดสอบความสามารถที่ [Aspose's releases section](https://releases.aspose.com/cells/java/).
- **ฟอรั่มสนับสนุน**: สำหรับคำถามใด ๆ, มี [support forum](https://forum.aspose.com/c/cells/9) ให้ใช้.

---

**อัปเดตล่าสุด:** 2026-04-02  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}