---
"description": "เรียนรู้วิธีสร้างแผนภูมิประเภทรวมโดยใช้ Aspose.Cells สำหรับ Java คำแนะนำทีละขั้นตอนนี้ประกอบด้วยโค้ดต้นฉบับและเคล็ดลับสำหรับการแสดงภาพข้อมูลอย่างมีประสิทธิภาพ"
"linktitle": "ประเภทแผนภูมิแบบรวม"
"second_title": "API การประมวลผล Java Excel ของ Aspose.Cells"
"title": "ประเภทแผนภูมิแบบรวม"
"url": "/th/java/advanced-excel-charts/combined-chart-types/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ประเภทแผนภูมิแบบรวม


## การแนะนำประเภทแผนภูมิรวมโดยใช้ Aspose.Cells สำหรับ Java

ในโลกแห่งการแสดงภาพข้อมูล แผนภูมิมีบทบาทสำคัญในการช่วยให้เราเข้าใจชุดข้อมูลที่ซับซ้อน Aspose.Cells สำหรับ Java เป็น Java API ที่ทรงพลังซึ่งช่วยให้คุณสร้าง จัดการ และปรับแต่งแผนภูมิประเภทต่างๆ รวมถึงแผนภูมิประเภทผสมได้ ในบทความนี้ เราจะมาสำรวจวิธีการสร้างแผนภูมิประเภทผสมโดยใช้ Aspose.Cells สำหรับ Java

## ทำความเข้าใจ Aspose.Cells สำหรับ Java

ก่อนที่จะเริ่มสร้างแผนภูมิรวม เรามาทำความเข้าใจสั้นๆ กันก่อนว่า Aspose.Cells สำหรับ Java คืออะไร Aspose.Cells เป็นไลบรารีบนพื้นฐาน Java ที่มีฟังก์ชันการทำงานที่ครอบคลุมสำหรับการทำงานกับสเปรดชีต Excel ซึ่งรวมถึงความสามารถในการสร้าง แก้ไข และปรับปรุงแผนภูมิภายในไฟล์ Excel ของคุณโดยใช้โปรแกรม

## การเริ่มต้น

หากต้องการเริ่มต้นสร้างแผนภูมิรวม คุณจะต้องติดตั้งและตั้งค่า Aspose.Cells สำหรับ Java ในโปรเจ็กต์ Java ของคุณ คุณสามารถดาวน์โหลดไลบรารีจากเว็บไซต์ Aspose โดยใช้ลิงก์ต่อไปนี้: [ดาวน์โหลด Aspose.Cells สำหรับ Java](https://releases-aspose.com/cells/java/).

เมื่อคุณมีไลบรารีพร้อมแล้ว คุณสามารถดำเนินการตามขั้นตอนต่อไปนี้เพื่อสร้างแผนภูมิรวมได้

## การสร้างแผนภูมิแบบรวม

### ขั้นตอนที่ 1: นำเข้าคลาสและแพ็คเกจที่จำเป็นจาก Aspose.Cells สำหรับ Java เข้าสู่โปรเจ็กต์ Java ของคุณ

```java
import com.aspose.cells.*;
```

### ขั้นตอนที่ 2: เริ่มต้นวัตถุเวิร์กบุ๊ก

```java
Workbook workbook = new Workbook();
```

### ขั้นตอนที่ 3: เพิ่มเวิร์กชีตลงในเวิร์กบุ๊ก

```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### ขั้นตอนที่ 4: สร้างวัตถุแผนภูมิรวม

```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## การเพิ่มข้อมูลลงในแผนภูมิ

ตอนนี้เราได้สร้างแผนภูมิรวมแล้ว เรามาเพิ่มข้อมูลลงไปกัน

### ขั้นตอนที่ 5: สร้างชุดข้อมูลสำหรับแผนภูมิ

```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```

### ขั้นตอนที่ 6: ตั้งค่าช่วงข้อมูลหมวดหมู่สำหรับแผนภูมิ

```java
chart.getNSeries().setCategoryData("C1:C5");
```

## การปรับแต่งแผนภูมิ

คุณสามารถปรับแต่งลักษณะที่ปรากฏและพฤติกรรมของแผนภูมิรวมเพื่อให้ตรงตามความต้องการเฉพาะของคุณได้

### ขั้นตอนที่ 7: ปรับแต่งชื่อแผนภูมิและป้ายแกน

```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

2. ขั้นตอนที่ 8: ปรับแต่งรูปลักษณ์ของแผนภูมิ

```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## การบันทึกและการส่งออกแผนภูมิ

เมื่อคุณสร้างและปรับแต่งแผนภูมิรวมของคุณแล้ว คุณสามารถบันทึกลงในไฟล์ Excel หรือส่งออกไปยังรูปแบบต่างๆ ได้

### ขั้นตอนที่ 9: บันทึกสมุดงานไปยังไฟล์ Excel

```java
workbook.save("CombinedChart.xlsx");
```

### ขั้นตอนที่ 10: ส่งออกแผนภูมิไปยังไฟล์รูปภาพ

```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```

## บทสรุป

ในบทความนี้ เราได้ศึกษาเกี่ยวกับวิธีการสร้างแผนภูมิประเภทรวมโดยใช้ Aspose.Cells สำหรับ Java เราเริ่มต้นด้วยการทำความเข้าใจว่า Aspose.Cells สำหรับ Java คืออะไร จากนั้นจึงดำเนินการต่อด้วยคำแนะนำทีละขั้นตอนสำหรับการสร้างแผนภูมิรวม การเพิ่มข้อมูล การปรับแต่งลักษณะ และการบันทึก/ส่งออก ด้วย Aspose.Cells สำหรับ Java คุณสามารถปลดปล่อยพลังของการแสดงภาพข้อมูลในแอปพลิเคชัน Java ของคุณได้

## คำถามที่พบบ่อย

### ฉันจะติดตั้ง Aspose.Cells สำหรับ Java ได้อย่างไร?

หากต้องการติดตั้ง Aspose.Cells สำหรับ Java ให้ไปที่เว็บไซต์ Aspose และดาวน์โหลดไลบรารีจาก [ลิงค์นี้](https://releases.aspose.com/cells/java/). ปฏิบัติตามคำแนะนำในการติดตั้งซึ่งมีอยู่ในเอกสารประกอบ

### ฉันสามารถสร้างแผนภูมิประเภทอื่นด้วย Aspose.Cells สำหรับ Java ได้หรือไม่

ใช่ Aspose.Cells สำหรับ Java รองรับแผนภูมิประเภทต่างๆ มากมาย รวมถึงแผนภูมิแท่ง แผนภูมิวงกลม แผนภูมิกระจาย และอื่นๆ คุณสามารถดูตัวอย่างและการใช้งานได้ในเอกสารประกอบ

### Aspose.Cells สำหรับ Java เหมาะกับทั้งผู้เริ่มต้นและนักพัฒนา Java ที่มีประสบการณ์หรือไม่

Aspose.Cells สำหรับ Java ได้รับการออกแบบมาให้ใช้งานง่าย เหมาะสำหรับทั้งผู้เริ่มต้นและนักพัฒนาที่มีประสบการณ์ โดยให้ API ระดับสูงเพื่อให้ใช้งานง่าย พร้อมทั้งมีคุณลักษณะขั้นสูงสำหรับผู้ที่มีประสบการณ์มากขึ้น

### ฉันสามารถปรับแต่งลักษณะของแผนภูมิรวมของฉันเพิ่มเติมได้หรือไม่

แน่นอน! Aspose.Cells สำหรับ Java มีตัวเลือกการปรับแต่งมากมาย คุณสามารถเปลี่ยนสี แบบอักษร สไตล์ และอื่นๆ เพื่อปรับแต่งรูปลักษณ์ของแผนภูมิให้ตรงใจได้

### ฉันสามารถหาทรัพยากรและตัวอย่างเพิ่มเติมสำหรับ Aspose.Cells สำหรับ Java ได้ที่ไหน

คุณสามารถค้นหาเอกสารประกอบที่ครอบคลุมและตัวอย่างโค้ดมากมายบนเว็บไซต์ Aspose ได้ที่ [ที่นี่](https://reference-aspose.com/cells/java/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}