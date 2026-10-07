---
date: '2026-04-11'
description: เรียนรู้การทำอัตโนมัติ Excel ด้วย Java และ Aspose.Cells บทเรียนนี้แสดงวิธีสร้าง
  workbook Excel ด้วย Java, เติมข้อมูล Excel ด้วย Java, และบันทึกไฟล์ Excel ด้วย Java
  พร้อมแผนภูมิ.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'การทำงานอัตโนมัติ Excel ด้วย Java: สร้างสมุดงานและแผนภูมิด้วย Aspose'
url: /th/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Automation Java: สร้าง Workbook และแผนภูมิด้วย Aspose

## บทนำ

การทำงานอัตโนมัติของ Excel ด้วย Java สามารถประหยัดเวลาหลายชั่วโมงจากการทำงานด้วยมือ โดยเฉพาะเมื่อคุณต้องการสร้างรายงาน, แดชบอร์ด, หรือแผนภูมิที่ขับเคลื่อนด้วยข้อมูลแบบเรียลไทม์ **Excel automation java** ด้วย Aspose.Cells ให้ API ที่สะอาดและมีประสิทธิภาพสูง ซึ่งจัดการทุกอย่างตั้งแต่การสร้าง workbook ไปจนถึงการจัดรูปแบบแผนภูมิขั้นสูง ในบทเรียนนี้คุณจะได้เรียนรู้วิธีตั้งค่า Aspose.Cells, **create an Excel workbook java**, เติมข้อมูลลงใน workbook, เพิ่มแผนภูมิ, ใช้การจัดรูปแบบ 3‑D, และสุดท้าย **save the Excel file java**.

### คำตอบด่วน
- **ไลบรารีใดที่ทำให้การทำงานอัตโนมัติของ Excel ใน Java ง่ายขึ้น?** Aspose.Cells for Java.  
- **ฉันสามารถเพิ่มแผนภูมิ 3‑D ผ่านโปรแกรมได้หรือไม่?** Yes – the API supports 3‑D formatting and lighting effects.  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** A free trial license is available; a commercial license is required for production.  
- **เครื่องมือสร้าง Java ที่รองรับคืออะไร?** Maven and Gradle are both fully supported.  
- **รูปแบบไฟล์ใดที่ฉันสามารถส่งออกได้?** XLS, XLSX, CSV, PDF and many more.

## Excel automation java คืออะไร?

Excel automation java หมายถึงกระบวนการสร้าง, แก้ไข, และบันทึก Excel workbook อย่างโปรแกรมโดยใช้โค้ด Java ซึ่งช่วยขจัดการแก้ไขสเปรดชีตด้วยมือ, ทำให้เกิดความสอดคล้อง, และเปิดโอกาสการรวมกับระบบอื่น ๆ เช่นฐานข้อมูลหรือเว็บเซอร์วิส

## ทำไมต้องใช้ Aspose.Cells สำหรับ Java?

- **Rich feature set** – จากค่าของเซลล์ง่าย ๆ ไปจนถึงแผนภูมิซับซ้อน, pivot table, และ conditional formatting.  
- **No Microsoft Office dependency** – ทำงานบนสภาพแวดล้อม server‑side ใดก็ได้.  
- **High performance** – ปรับให้เหมาะกับชุดข้อมูลขนาดใหญ่และสถานการณ์ multi‑threaded.  
- **Broad format support** – อ่าน/เขียน XLS, XLSX, ODS, CSV, PDF, HTML, and more.

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 8+**  
- **Maven or Gradle** for dependency management  
- **Aspose.Cells for Java 25.3 or later** (trial or licensed)  

## การตั้งค่า Aspose.Cells สำหรับ Java

เพิ่มไลบรารีลงในโปรเจกต์ของคุณโดยใช้การกำหนดค่าต่อไปนี้

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### การขอรับใบอนุญาต

ขอรับใบอนุญาตทดลองฟรีจากเว็บไซต์ Aspose, หรือซื้อใบอนุญาตเต็มสำหรับการใช้งานในผลิตภัณฑ์ วางไฟล์ใบอนุญาตในโปรเจกต์ของคุณและโหลดใน runtime

## การเริ่มต้นและตั้งค่าเบื้องต้น

เมื่อการอ้างอิงไลบรารีเสร็จสิ้น, คุณสามารถเริ่มเขียนโค้ดได้

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## คู่มือขั้นตอน

### ขั้นตอนที่ 1: วิธีสร้าง excel workbook java

สร้างอินสแตนซ์ workbook ใหม่ที่จะเก็บ worksheet ทั้งหมดของคุณ

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### ขั้นตอนที่ 2: เพิ่ม worksheet (รวมถึงแผ่นแผนภูมิ)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### ขั้นตอนที่ 3: วิธีเติมข้อมูล excel java

ใส่ข้อมูลตัวอย่างที่แผนภูมิจะอ้างอิง

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### ขั้นตอนที่ 4: เพิ่มแผนภูมิคอลัมน์ลงใน workbook

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### ขั้นตอนที่ 5: ใช้การจัดรูปแบบสีในพื้นที่แผนภูมิ

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### ขั้นตอนที่ 6: กำหนดค่า legend และ series ของข้อมูล

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### ขั้นตอนที่ 7: ใช้การจัดรูปแบบ 3D กับ series

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### ขั้นตอนที่ 8: ตั้งค่าสีของ series เพื่อความแตกต่างที่ชัดเจน

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### ขั้นตอนที่ 9: วิธีบันทึกไฟล์ excel java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## การประยุกต์ใช้งานจริง

- **Financial Reporting** – สร้างรายงานไตรมาสพร้อมแผนภูมิกระ动态.  
- **Data‑Analysis Dashboards** – สร้างแดชบอร์ดเชิงโต้ตอบที่รีเฟรชอัตโนมัติ.  
- **Inventory Management** – ส่งออกระดับสต็อกและแนวโน้มไปยัง Excel เพื่อการตรวจสอบของผู้มีส่วนได้ส่วนเสีย.  
- **Project Planning** – สร้างแผนภูมิแบบ Gantt‑style โดยตรงจากระบบกำหนดเวลาที่พัฒนาใน Java.

## เคล็ดลับประสิทธิภาพสำหรับ Excel Automation Java

- **Reuse Workbook Objects** เมื่อประมวลผลหลายแผ่นเพื่อ ลดการใช้หน่วยความจำ.  
- **Batch Cell Updates** โดยใช้ `Cells.importArray` สำหรับชุดข้อมูลขนาดใหญ่แทนการเรียก `putValue` ทีละเซลล์.  
- **Dispose Resources** โดยเรียก `book.dispose()` หลังจากบันทึกไฟล์ขนาดใหญ่.

## คำถามที่พบบ่อย

**Q: ฉันสามารถสร้าง XLSX แทน XLS ได้หรือไม่?**  
A: Yes – simply change the file extension in `book.save("output.xlsx")`; Aspose automatically selects the correct format.

**Q: จำเป็นต้องมีใบอนุญาตสำหรับการพัฒนาหรือไม่?**  
A: A free trial license works for development and testing. Production deployments require a purchased license.

**Q: ฉันจะเพิ่มประเภทแผนภูมิอื่น ๆ ได้อย่างไร?**  
A: Use `ChartType` enum (e.g., `ChartType.PIE`, `ChartType.LINE`) when calling `charts.add(...)`.

**Q: ถ้าฉันต้องการป้องกัน workbook จะทำอย่างไร?**  
A: Call `book.getSettings().setPassword("yourPassword")` before saving.

**Q: Aspose.Cells รองรับไฟล์ที่มีแมโครหรือไม่?**  
A: Yes – you can create or preserve VBA macros in XLSM workbooks.

---

**อัปเดตล่าสุด:** 2026-04-11  
**ทดสอบกับ:** Aspose.Cells 25.3 (Java)  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}