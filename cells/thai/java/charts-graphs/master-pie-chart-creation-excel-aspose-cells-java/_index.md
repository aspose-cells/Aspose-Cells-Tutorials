---
"date": "2025-04-07"
"description": "เรียนรู้วิธีสร้างและปรับแต่งแผนภูมิวงกลมใน Excel ด้วย Aspose.Cells สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนนี้เพื่อพัฒนาทักษะการแสดงภาพข้อมูลของคุณ"
"title": "สร้างแผนภูมิวงกลมใน Excel โดยใช้ Aspose.Cells สำหรับ Java - คู่มือฉบับสมบูรณ์"
"url": "/th/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# สร้างแผนภูมิวงกลมใน Excel โดยใช้ Aspose.Cells สำหรับ Java
## การแนะนำ
การสร้างแผนภูมิวงกลมที่น่าสนใจและให้ข้อมูลใน Excel สามารถเปลี่ยนข้อมูลดิบให้กลายเป็นข้อมูลเชิงลึกที่มีประสิทธิภาพ ช่วยให้คุณสามารถตัดสินใจทางธุรกิจอย่างรอบรู้ได้อย่างรวดเร็ว คุณกำลังประสบปัญหาในการใช้ฟีเจอร์ในตัวของ Microsoft Excel หรือกำลังมองหาโซลูชันที่ปรับขนาดได้ซึ่งรวมเข้ากับแอปพลิเคชัน Java ของคุณได้อย่างราบรื่นหรือไม่ Aspose.Cells สำหรับ Java อยู่ที่นี่เพื่อช่วยเหลือคุณ

บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการสร้างและปรับแต่งแผนภูมิวงกลมในไฟล์ Excel โดยใช้ Aspose.Cells สำหรับ Java ค้นพบวิธีการเพิ่มข้อมูล กำหนดค่าองค์ประกอบแผนภูมิ และสรุปเวิร์กบุ๊กของคุณอย่างมีประสิทธิภาพ ทั้งหมดนี้ทำได้ง่ายดายและแม่นยำ

**สิ่งที่คุณจะได้เรียนรู้:**
- การตั้งค่าและการใช้ Aspose.Cells สำหรับ Java
- การสร้างเวิร์กบุ๊กใหม่และเติมข้อมูลตัวอย่าง
- การเพิ่มและปรับแต่งแผนภูมิวงกลมภายในเวิร์กชีต Excel
- แนวทางปฏิบัติที่ดีที่สุดสำหรับการกำหนดค่าและเพิ่มประสิทธิภาพแผนภูมิ

มาเริ่มต้นด้วยการครอบคลุมข้อกำหนดเบื้องต้นกันก่อน
## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่มต้น ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
### ไลบรารี เวอร์ชัน และการอ้างอิงที่จำเป็น
ตรวจสอบว่า Aspose.Cells สำหรับ Java เวอร์ชัน 25.3 หรือใหม่กว่ารวมอยู่ในโปรเจ็กต์ของคุณโดยใช้ Maven หรือ Gradle
**เมเวน:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**เกรเดิ้ล:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- Java Development Kit (JDK) ติดตั้งอยู่บนระบบของคุณ
- สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น IntelliJ IDEA, Eclipse หรือ NetBeans
### ข้อกำหนดเบื้องต้นของความรู้
ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และความคุ้นเคยกับโครงสร้างไฟล์ Excel จะเป็นประโยชน์
## การตั้งค่า Aspose.Cells สำหรับ Java
Aspose.Cells เป็นไลบรารีอันทรงพลังที่ช่วยให้ผู้พัฒนาสามารถสร้าง แก้ไข และเรนเดอร์สเปรดชีต Excel ในแอปพลิเคชัน Java ได้ วิธีการตั้งค่ามีดังนี้:
1. **การติดตั้ง**:เพิ่มการอ้างอิง Maven หรือ Gradle ดังที่แสดงด้านบน
2. **การขอใบอนุญาต**-
   - รับใบอนุญาตทดลองใช้งานฟรีสำหรับการทดสอบเบื้องต้นจาก [ทดลองใช้ Aspose ฟรี](https://releases-aspose.com/cells/java/).
   - สมัครใบอนุญาตชั่วคราวเพื่อทดสอบฟีเจอร์เต็มรูปแบบโดยไม่มีข้อจำกัดผ่าน [ใบอนุญาตชั่วคราว](https://purchase-aspose.com/temporary-license/).
3. **การเริ่มต้นขั้นพื้นฐาน**:เริ่มต้นด้วยการสร้างอินสแตนซ์ของ `Workbook` คลาสซึ่งแสดงถึงไฟล์ Excel ของคุณ
```java
import com.aspose.cells.Workbook;
// สร้างและเริ่มต้นสมุดงานใหม่
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## คู่มือการใช้งาน
ตอนนี้เราลองนำคุณลักษณะแต่ละอย่างไปใช้ทีละขั้นตอนเพื่อสร้างเวิร์กบุ๊ก Excel ที่มีแผนภูมิวงกลม
### 1. การสร้างและการเริ่มต้นเวิร์กบุ๊ก
**ภาพรวม**:เราเริ่มต้นด้วยการเริ่มต้นของเรา `Workbook` วัตถุและการเข้าถึงเวิร์กชีตแรกที่เราจะเพิ่มข้อมูลและแผนภูมิ
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// สร้างอินสแตนซ์เวิร์กบุ๊กใหม่
Workbook workbook = new Workbook();
// เข้าถึงเวิร์กชีตแรกในเวิร์กบุ๊ก
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. การเพิ่มข้อมูลตัวอย่างลงในเซลล์
**ภาพรวม**:เติมแผ่นงานของคุณด้วยข้อมูลตัวอย่างที่จะแสดงในแผนภูมิวงกลม
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// เพิ่มชื่อประเทศในคอลัมน์ A
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// เพื่อไปประเทศอื่นๆต่อ...
// เพิ่มข้อมูลการขายที่สอดคล้องกันในคอลัมน์ B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// ดำเนินการต่อเพื่อข้อมูลส่วนที่เหลือ...
```
### 3. การเพิ่มแผนภูมิวงกลมลงในเวิร์กชีต
**ภาพรวม**:แทรกแผนภูมิวงกลมเข้าไปในเวิร์กชีตโดยใช้ช่วงข้อมูลที่กำหนดไว้ล่วงหน้า
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// เพิ่มแผนภูมิวงกลมตามตำแหน่งและขนาดที่ระบุ
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. การกำหนดค่าชุดแผนภูมิ
**ภาพรวม**:กำหนดช่วงข้อมูลสำหรับข้อมูลการขายและหมวดหมู่ (ชื่อประเทศ) เพื่อให้แน่ใจว่าแผนภูมิวงกลมแสดงชุดข้อมูลของคุณอย่างถูกต้อง
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// ตั้งค่าข้อมูลการขายเป็นแหล่งข้อมูลของแผนภูมิ
serieses.add("B1:B8", true);
// ระบุข้อมูลหมวดหมู่(ชื่อประเทศ)
serieses.setCategoryData("A1:A8");
// เปิดใช้งานสีสันที่หลากหลายสำหรับชิ้นพายแต่ละชิ้น
serieses.setColorVaried(true);

// แสดงตารางข้อมูลบนแผนภูมิเพื่อความชัดเจน
chart.setShowDataTable(true);
```
### 5. การตั้งชื่อและรูปแบบของแผนภูมิ
**ภาพรวม**ปรับแต่งชื่อแผนภูมิของคุณเพื่อปรับปรุงการอ่านและการนำเสนอ
```java
import com.aspose.cells.Color;

// ตั้งชื่อแผนภูมิพร้อมตัวเลือกการจัดรูปแบบ
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. การกำหนดค่าป้ายข้อมูลสำหรับชุดแผนภูมิ
**ภาพรวม**:เพิ่มป้ายข้อมูลให้กับชิ้นส่วนวงกลมแต่ละชิ้น เพื่อให้มีการแบ่งค่าได้อย่างชัดเจน
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // ติดป้ายตำแหน่งไว้ด้านในฐานของชิ้นพายแต่ละชิ้น
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // กำหนดค่าตัวเลือกการแสดงฉลาก
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. การบันทึกสมุดงาน
**ภาพรวม**:สรุปไฟล์ Excel ของคุณพร้อมข้อมูลและแผนภูมิทั้งหมดลงในดิสก์
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// บันทึกสมุดงานไปยังไฟล์ Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## การประยุกต์ใช้งานจริง
- **การวิเคราะห์ทางธุรกิจ**:ใช้แผนภูมิวงกลมในรายงานการขายเพื่อแสดงส่วนแบ่งการตลาดหรือการกระจายรายได้ในแต่ละภูมิภาค
- **เครื่องมือทางการศึกษา**:สร้างโมดูลการเรียนรู้แบบโต้ตอบโดยแสดงการกระจายข้อมูลทางสถิติ
- **การจัดการโครงการ**:แสดงการจัดสรรทรัพยากรและการใช้งบประมาณให้ผู้มีส่วนได้ส่วนเสียเห็นอย่างชัดเจน
## การพิจารณาประสิทธิภาพ
เพื่อเพิ่มประสิทธิภาพการทำงาน:
- ลดการใช้หน่วยความจำโดยการจัดการขนาดเวิร์กบุ๊กอย่างมีประสิทธิภาพ
- ใช้ประโยชน์จากคุณสมบัติของ Aspose.Cells เช่น การสตรีมไฟล์ขนาดใหญ่ หากต้องจัดการกับชุดข้อมูลจำนวนมาก
- ปฏิบัติตามแนวทางปฏิบัติที่ดีที่สุดของ Java สำหรับการจัดการหน่วยความจำ เพื่อให้แน่ใจว่าทรัพยากรจะได้รับการปล่อยอย่างเหมาะสมหลังการใช้งาน
## บทสรุป
เมื่อทำตามคำแนะนำนี้ คุณจะได้เรียนรู้วิธีสร้าง กำหนดค่า และปรับแต่งแผนภูมิวงกลมใน Excel โดยใช้ Aspose.Cells สำหรับ Java ไลบรารีอันทรงพลังนี้ช่วยให้ผู้พัฒนาสามารถผสานรวมฟังก์ชันสเปรดชีตขั้นสูงภายในแอปพลิเคชัน Java ได้อย่างราบรื่น
หากต้องการสำรวจเพิ่มเติม โปรดพิจารณาเจาะลึกประเภทแผนภูมิอื่นหรือขยายความสามารถในการจัดการข้อมูลของคุณด้วยคุณลักษณะเพิ่มเติมที่นำเสนอโดย Aspose.Cells
## ส่วนคำถามที่พบบ่อย
1. **ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?**
   - ใช่ มีรุ่นทดลองใช้งานฟรี หากต้องการใช้งานฟีเจอร์ทั้งหมดโดยไม่มีข้อจำกัด คุณสามารถสมัครใบอนุญาตชั่วคราวได้
2. **เป็นไปได้ไหมที่จะสร้างแผนภูมิประเภทอื่นโดยใช้ Aspose.Cells**
   - แน่นอน! คุณสามารถสร้างแผนภูมิแท่ง กราฟเส้น และอื่น ๆ ได้โดยการปรับ `ChartType`-
3. **ฉันจะจัดการชุดข้อมูลขนาดใหญ่ใน Excel ด้วย Java ได้อย่างไร**
   - ใช้เทคนิคการโหลดข้อมูลที่มีประสิทธิภาพและพิจารณาการสตรีมสำหรับไฟล์ขนาดใหญ่

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}