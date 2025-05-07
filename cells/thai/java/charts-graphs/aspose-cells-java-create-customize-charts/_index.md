---
"date": "2025-04-08"
"description": "บทช่วยสอนเกี่ยวกับโค้ดสำหรับ Aspose.Words Java"
"title": "Aspose.Cells Java&#58; สร้างและปรับแต่งแผนภูมิ"
"url": "/th/java/charts-graphs/aspose-cells-java-create-customize-charts/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# การเรียนรู้การสร้างและปรับแต่งแผนภูมิด้วย Aspose.Cells Java

ในโลกปัจจุบันที่ข้อมูลถูกขับเคลื่อน การสร้างภาพชุดข้อมูลที่ซับซ้อนถือเป็นสิ่งสำคัญสำหรับการตัดสินใจอย่างรอบรู้ ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น การสร้างแผนภูมิที่น่าสนใจในแอปพลิเคชันของคุณจะช่วยปรับปรุงประสบการณ์ของผู้ใช้ได้อย่างมาก บทช่วยสอนนี้จะแนะนำคุณตลอดขั้นตอนการใช้ Aspose.Cells สำหรับ Java เพื่อสร้างและปรับแต่งแผนภูมิได้อย่างง่ายดาย

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการตั้งค่า Aspose.Cells สำหรับ Java
- การสร้างและการตั้งชื่อแผ่นงาน
- การเติมข้อมูลในเซลล์
- การเพิ่มแผ่นงานแผนภูมิและการสร้างแผนภูมิคอลัมน์
- การปรับแต่งแผนภูมิของคุณด้วยรูปภาพ ชื่อเรื่อง และการกำหนดค่าชุด
- การบันทึกสมุดงาน

ด้วยขั้นตอนเหล่านี้ คุณจะสามารถสร้างแผนภูมิที่สวยงามได้ในเวลาอันรวดเร็ว

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำดิ่งลงไปใน Aspose.Cells สำหรับ Java ให้แน่ใจว่าคุณมี:

- **Java Development Kit (JDK) 8 หรือใหม่กว่า** ติดตั้งอยู่บนเครื่องของคุณแล้ว
- ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และความคุ้นเคยกับการทำงานของ Excel
  
### ห้องสมุดที่จำเป็น

ในการเริ่มต้นใช้งาน Aspose.Cells โปรดรวมการอ้างอิงต่อไปนี้ไว้ในเครื่องมือการจัดการโครงการของคุณ

#### เมเวน
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### แกรเดิล
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### การขอใบอนุญาต

Aspose เสนอบริการทดลองใช้งานฟรี ช่วยให้คุณทดสอบฟีเจอร์ทั้งหมดของไลบรารีได้ก่อนซื้อ นอกจากนี้ คุณยังสามารถขอรับใบอนุญาตชั่วคราวเพื่อการทดสอบแบบครอบคลุมได้อีกด้วย

- **ทดลองใช้งานฟรี**- [ดาวน์โหลดฟรี](https://releases.aspose.com/cells/java/)
- **ใบอนุญาตชั่วคราว**- [ขอคำร้องได้ที่นี่](https://purchase.aspose.com/temporary-license/)

## การตั้งค่า Aspose.Cells สำหรับ Java

เมื่อคุณเตรียมสภาพแวดล้อมของคุณให้พร้อมแล้ว ให้เริ่มต้นไลบรารีโดยสร้างใหม่ `Workbook` ตัวอย่างนี้จะเป็นพื้นฐานสำหรับการสร้างแผนภูมิของเรา

```java
import com.aspose.cells.Workbook;

// เริ่มต้นสมุดงานใหม่
Workbook workbook = new Workbook();
```

## คู่มือการใช้งาน

### 1. การสร้างและตั้งชื่อเวิร์กชีต

#### ภาพรวม
เริ่มต้นด้วยการตั้งค่าแผ่นข้อมูลของคุณซึ่งจะเก็บข้อมูลที่จำเป็นทั้งหมดสำหรับแผนภูมิ

#### ขั้นตอน:

**สร้างสมุดงานใหม่**
```java
import com.aspose.cells.Worksheet;

// สร้างอินสแตนซ์เวิร์กบุ๊กใหม่
Workbook workbook = new Workbook();
```

**ตั้งชื่อแผ่นงาน**

```java
// เข้าถึงเวิร์กชีตแรกและตั้งชื่อเป็น "ข้อมูล"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. การเติมข้อมูลลงในเซลล์

#### ภาพรวม
การกรอกข้อมูลลงในเวิร์กชีตของคุณถือเป็นสิ่งสำคัญสำหรับการสร้างแผนภูมิที่มีความหมาย

#### ขั้นตอน:

**เข้าถึงคอลเลกชันเซลล์**

```java
import com.aspose.cells.Cells;

// รับคอลเลกชันเซลล์จากแผ่นงาน "ข้อมูล"
Cells cells = sheet.getCells();
```

**การแทรกข้อมูล**

```java
// ใส่ชื่อภูมิภาคและตัวเลขยอดขาย
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. การเพิ่มแผ่นงานแผนภูมิ

#### ภาพรวม
เพิ่มแผ่นงานแผนภูมิเฉพาะเพื่อแยกข้อมูลและการแสดงภาพของคุณออกจากกัน

#### ขั้นตอน:

**สร้างแผ่นงานแผนภูมิ**

```java
import com.aspose.cells.SheetType;

// เพิ่มแผ่นงานแผนภูมิใหม่
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// ตั้งชื่อแผ่นงานว่า “แผนภูมิ”
chartSheet.setName("Chart");
```

### 4. การสร้างแผนภูมิ

#### ภาพรวม
สร้างแผนภูมิคอลัมน์เพื่อแสดงข้อมูลการขายตามภูมิภาค

#### ขั้นตอน:

**สร้างแผนภูมิคอลัมน์**

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// เพิ่มแผนภูมิคอลัมน์ใหม่ลงในแผ่นงาน "แผนภูมิ"
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. ตั้งค่ารูปภาพเป็นพื้นหลัง เติมพื้นที่พล็อตแผนภูมิ

#### ภาพรวม
เพิ่มความน่าสนใจให้กับแผนภูมิของคุณด้วยการเพิ่มรูปภาพพื้นหลัง

#### ขั้นตอน:

**ตั้งค่าข้อมูลภาพ**

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

### 6. การกำหนดค่าชื่อแผนภูมิและชุดข้อมูล

#### ภาพรวม
ปรับแต่งแผนภูมิของคุณด้วยชื่อ ชุดข้อมูล และตำแหน่งของคำอธิบายแผนภูมิ

#### ขั้นตอน:

**ตั้งค่าชื่อแผนภูมิ**

```java
// กำหนดค่าคุณสมบัติชื่อแผนภูมิ
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

**กำหนดค่าข้อมูลซีรีส์**

```java
// ตั้งค่าชุดข้อมูลและหมวดหมู่สำหรับแผนภูมิ
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// วางตำแหน่งตำนานไว้ที่ด้านบนของแผนภูมิ
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 7. การบันทึกสมุดงาน

#### ภาพรวม
รับรองว่าการทำงานหนักทั้งหมดของคุณได้รับการบันทึกโดยการส่งออกสมุดงาน

#### ขั้นตอน:

**บันทึกสมุดงาน**

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## การประยุกต์ใช้งานจริง

- **รายงานทางธุรกิจ**:สร้างรายงานการขายและประสิทธิภาพแบบไดนามิก
- **เครื่องมือวิเคราะห์ข้อมูล**:ปรับปรุงการแสดงภาพข้อมูลในซอฟต์แวร์วิเคราะห์
- **การบูรณาการแดชบอร์ด**:รวมแผนภูมิเข้ากับแดชบอร์ดเพื่ออัปเดตแบบเรียลไทม์

## การพิจารณาประสิทธิภาพ

- เพิ่มประสิทธิภาพโดยลดจำนวนการดำเนินการบนชุดข้อมูลขนาดใหญ่ให้เหลือน้อยที่สุด
- จัดการหน่วยความจำอย่างมีประสิทธิภาพด้วยการกำจัดสิ่งของที่ไม่ได้ใช้ทันที

## บทสรุป

ตอนนี้คุณได้เชี่ยวชาญการสร้างและปรับแต่งแผนภูมิโดยใช้ Aspose.Cells ใน Java แล้ว หากต้องการดำเนินการต่อ โปรดสำรวจฟีเจอร์อื่นๆ เช่น ช่วงข้อมูลแบบไดนามิกหรือประเภทแผนภูมิอื่นๆ 

## ส่วนคำถามที่พบบ่อย

1. **ฉันจะเพิ่มซีรีส์หลายชุดลงในแผนภูมิได้อย่างไร**
   - ใช้ `add` วิธีการบน `NSeries` ที่มีหลายช่วง

2. **ฉันสามารถปรับแต่งป้ายแกนของแผนภูมิได้หรือไม่**
   - ใช่ เข้าถึงและกำหนดค่าแกนโดยใช้ `chart.getCategหรือyAxis()` or `chart-getValueAxis()`.

3. **จะเกิดอะไรขึ้นหากไฟล์รูปภาพของฉันไม่แสดงอย่างถูกต้องในพื้นที่พล็อต?**
   - ตรวจสอบให้แน่ใจว่าเส้นทางไฟล์ถูกต้องและรูปแบบภาพได้รับการรองรับโดย Aspose.Cells

4. **ฉันจะจัดการชุดข้อมูลขนาดใหญ่ได้อย่างมีประสิทธิภาพได้อย่างไร**
   - พิจารณาการอ่านข้อมูลเป็นส่วนๆ และอัปเดตเซลล์แบบเพิ่มทีละน้อย

5. **สามารถส่งออกแผนภูมิไปยังรูปแบบอื่นเช่น PDF หรือ PNG ได้หรือไม่**
   - ใช่ครับ ใช้ `workbook.save()` โดยมีนามสกุลไฟล์ที่เหมาะสมกับรูปแบบต่างๆ

## ทรัพยากร

- [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/java/)
- [ดาวน์โหลด Aspose.Cells](https://releases.aspose.com/cells/java/)
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ทดลองใช้งานฟรี](https://releases.aspose.com/cells/java/)
- [การขอใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มสนับสนุน](https://forum.aspose.com/c/cells/9)

หากทำตามคำแนะนำนี้ คุณจะสามารถสร้างและปรับแต่งแผนภูมิในแอปพลิเคชัน Java โดยใช้ Aspose.Cells ได้อย่างง่ายดาย ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}