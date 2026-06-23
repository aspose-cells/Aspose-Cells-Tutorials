---
date: '2026-04-08'
description: เรียนรู้วิธีสร้างแผนภูมิคอลัมน์ใน Java ด้วย Aspose.Cells ครอบคลุมการสร้างแผนภูมิใน
  Java, การเพิ่มแผ่นแผนภูมิ, และการส่งออกเวิร์กบุ๊กเป็น Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: สร้างแผนภูมิคอลัมน์ด้วยบทแนะนำ Aspose.Cells Java
url: /th/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผนภูมิคอลัมน์ด้วย Aspose.Cells Java

ในแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **การสร้างแผนภูมิคอลัมน์** อย่างรวดเร็วและโดยโปรแกรมสามารถเปลี่ยนตัวเลขดิบให้เป็นข้อมูลเชิงภาพที่ชัดเจน ไม่ว่าคุณจะสร้างแดชบอร์ดรายงาน, เครื่องมือวิเคราะห์, หรือฟีเจอร์ส่งออกแบบง่าย, Aspose.Cells for Java มอบ API ที่ไหลลื่นเพื่อ **create chart java** โปรเจกต์โดยไม่ต้องจัดการกับ UI ของ Excel ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีตั้งค่าห้องสมุด, **populate Excel cells**, เพิ่ม **chart sheet**, ปรับแต่ง **chart title**, และสุดท้าย **export workbook excel** ไปยังไฟล์

## คำตอบด่วน
- **What does “generate column chart” mean?** มันสร้างการแสดงผลแบบแถบแนวตั้งจากข้อมูลตาราง  
- **Which library is required?** Aspose.Cells for Java (มีการทดลองใช้ฟรี)  
- **Do I need an Excel installation?** ไม่, ห้องสมุดทำงานโดยอิสระจาก Microsoft Excel.  
- **Can I export to formats other than XLS?** ได้ – PDF, PNG, SVG, ฯลฯ, ผ่าน `workbook.save()`.  
- **Is a license mandatory for production?** ใช่, จำเป็นต้องมีใบอนุญาตที่ซื้อหรือใบอนุญาตชั่วคราว

## แผนภูมิคอลัมน์คืออะไร?
แผนภูมิคอลัมน์แสดงชุดข้อมูลเป็นแถบแนวตั้ง ทำให้เปรียบเทียบค่าต่าง ๆ ระหว่างหมวดหมู่เช่น ภูมิภาค, เดือน, หรือสายผลิตภัณฑ์ได้ง่าย Aspose.Cells ให้คุณสร้างแผนภูมินี้ทั้งหมดด้วยโค้ด ให้คุณควบคุมข้อมูล, การจัดรูปแบบ, และรูปแบบผลลัพธ์ได้อย่างเต็มที่

## ทำไมต้องใช้ Aspose.Cells เพื่อสร้าง chart java?
- **No COM interop** – ทำงานบนระบบปฏิบัติการใดก็ได้ที่มี JVM.  
- **Rich styling options** – ภาพ, การไล่สี, คำอธิบาย, และฟอนต์ที่กำหนดเอง.  
- **High performance** – เหมาะสำหรับชุดข้อมูลขนาดใหญ่.  
- **Multiple export formats** – XLS, XLSX, PDF, PNG, และอื่น ๆ.

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8+** installed.  
- ความรู้พื้นฐานของ Java และความคุ้นเคยกับแนวคิดของ Excel

### ไลบรารีที่จำเป็น
เพิ่ม Aspose.Cells ไปยังโปรเจกต์ของคุณโดยใช้หนึ่งในโค้ดตัวอย่างด้านล่าง

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### การรับใบอนุญาต
Aspose มีการทดลองใช้ฟรีและใบอนุญาตชั่วคราวสำหรับการทดสอบอย่างกว้างขวาง

- **Free Trial**: [Download Free](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Request Here](https://purchase.aspose.com/temporary-license/)

## การตั้งค่า Aspose.Cells สำหรับ Java

ขั้นแรก, สร้างอินสแตนซ์ `Workbook` – ซึ่งจะเป็นผ้าใบสำหรับข้อมูลและแผนภูมิของเรา

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## คู่มือขั้นตอนโดยละเอียด

### 1. สร้างและตั้งชื่อ Worksheet
เราจะเก็บข้อมูลดิบในชีทที่ชื่อ **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. เติมข้อมูลในเซลล์ Excel
แทรกชื่อภูมิภาคและตัวเลขการขายที่แผนภูมิคอลัมน์จะทำการแสดงผล

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. เพิ่ม Chart Sheet
การแยกแผนภูมิออกจากข้อมูลดิบทำให้สมุดงานเป็นระเบียบ

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. สร้าง Column Chart
ตอนนี้เราจะสร้างอ็อบเจกต์ **generate column chart** จริง ๆ

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. ตั้งรูปภาพเป็นพื้นหลังใน Plot Area
ภาพพื้นหลังสามารถทำให้แผนภูมิดูโดดเด่น

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. ตั้งชื่อแผนภูมิ
การปรับแต่ง **set chart title** ช่วยเพิ่มความอ่านง่าย

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. กำหนดข้อมูลซีรีส์และ Legend
เชื่อมช่วงข้อมูลกับแผนภูมิและกำหนดตำแหน่งของ legend

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. ส่งออก Workbook Excel
สุดท้าย, **export workbook excel** ไปยังไฟล์ XLS (หรือรูปแบบที่รองรับอื่นใด)

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## การประยุกต์ใช้งานจริง
- **Business Reports** – สร้างแผนภูมิการขายอัตโนมัติสำหรับ PDF รายเดือน.  
- **Data Analysis Tools** – ฝังแผนภูมิกระแสไหลในแดชบอร์ดวิเคราะห์แบบกำหนดเอง.  
- **Enterprise Dashboards** – รีเฟรชภาพแผนภูมิแบบทันทีสำหรับการเฝ้าติดตามแบบเรียลไทม์.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- อัปเดตเซลล์เป็นชุดเมื่อทำงานกับชุดข้อมูลขนาดใหญ่เพื่อลดภาระ.  
- ปล่อยทรัพยากร (`workbook.dispose()`) หากคุณประมวลผลสมุดงานหลาย ๆ ใบในลูป.  

## ปัญหาทั่วไปและวิธีแก้
- **Image not showing** – ตรวจสอบเส้นทางไฟล์และรูปแบบภาพ (PNG, JPEG) ว่าได้รับการสนับสนุน.  
- **Chart appears blank** – ตรวจสอบให้แน่ใจว่าการอ้างอิงช่วงข้อมูล (`Data!B2:B8`) ตรงกับเซลล์ที่เติมข้อมูล.  
- **Out‑of‑memory errors** – ประมวลผลข้อมูลเป็นส่วน ๆ และเรียก `System.gc()` หลังการบันทึกขนาดใหญ่.  

## คำถามที่พบบ่อย

**Q: ฉันจะเพิ่มหลายซีรีส์ในแผนภูมิคอลัมน์ได้อย่างไร?**  
A: เรียก `chart.getNSeries().add()` ซ้ำหลายครั้งโดยใช้ช่วงข้อมูลที่ต่างกัน, เช่น `"Data!C2:C8"` สำหรับซีรีส์ที่สอง.

**Q: ฉันสามารถเปลี่ยนป้ายแกนได้หรือไม่?**  
A: ได้. ใช้ `chart.getCategoryAxis().setTitle("Regions")` และ `chart.getValueAxis().setTitle("Sales")`.

**Q: ฉันสามารถส่งออกเป็นรูปแบบใดบ้างนอกจาก XLS?**  
A: ใช้ `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, หรือ `workbook.save("chart.xlsx")` สำหรับ PDF, PNG, และ XLSX ตามลำดับ.

**Q: จำเป็นต้องมีใบอนุญาตสำหรับการสร้างเวอร์ชันพัฒนาไหม?**  
A: การทดลองใช้ฟรีใช้ได้สำหรับการประเมิน, แต่ต้องมีใบอนุญาตถาวรหรือชั่วคราวสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

**Q: ฉันจะปรับปรุงความเร็วการเรนเดอร์สำหรับหลายพันแถวได้อย่างไร?**  
A: เติมเซลล์โดยใช้ `cells.importArray()` และลดการวาดแผนภูมิซ้ำโดยสร้างแผนภูมิหลังจากโหลดข้อมูลทั้งหมดแล้ว.

---

**อัปเดตล่าสุด:** 2026-04-08  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

## แหล่งข้อมูล

- [เอกสาร Aspose.Cells](https://reference.aspose.com/cells/java/)  
- [ดาวน์โหลด Aspose.Cells](https://releases.aspose.com/cells/java/)  
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)  
- [ทดลองใช้ฟรี](https://releases.aspose.com/cells/java/)  
- [ขอใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)  
- [ฟอรั่มสนับสนุน](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}