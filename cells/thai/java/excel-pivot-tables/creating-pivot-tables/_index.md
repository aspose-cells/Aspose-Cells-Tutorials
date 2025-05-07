---
"description": "เรียนรู้วิธีการสร้าง Pivot Table อันทรงพลังใน Java ด้วย Aspose.Cells เพื่อการวิเคราะห์และการแสดงข้อมูลที่ได้รับการปรับปรุง"
"linktitle": "การสร้างตารางสรุปข้อมูล"
"second_title": "API การประมวลผล Java Excel ของ Aspose.Cells"
"title": "การสร้างตารางสรุปข้อมูล"
"url": "/th/java/excel-pivot-tables/creating-pivot-tables/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสร้างตารางสรุปข้อมูล

## การแนะนำ
Pivot Table เป็นเครื่องมือที่ขาดไม่ได้สำหรับการวิเคราะห์และแสดงข้อมูล ในบทช่วยสอนนี้ เราจะมาเรียนรู้วิธีสร้าง Pivot Table โดยใช้ Aspose.Cells for Java API เราจะให้คำแนะนำทีละขั้นตอนพร้อมตัวอย่างโค้ดต้นฉบับเพื่อให้กระบวนการนี้ราบรื่น

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.Cells สำหรับ Java แล้ว คุณสามารถดาวน์โหลดได้จาก [ที่นี่](https://releases-aspose.com/cells/java/).

## ขั้นตอนที่ 1: สร้างสมุดงาน
```java
// นำเข้าคลาสที่จำเป็น
import com.aspose.cells.Workbook;

// สร้างสมุดงานใหม่
Workbook workbook = new Workbook();
```

## ขั้นตอนที่ 2: โหลดข้อมูลลงในเวิร์กบุ๊ก
คุณสามารถโหลดข้อมูลของคุณลงในเวิร์กบุ๊กจากแหล่งต่าง ๆ เช่น ฐานข้อมูลหรือไฟล์ Excel

```java
// โหลดข้อมูลลงในสมุดงาน
workbook.open("data.xlsx");
```

## ขั้นตอนที่ 3: เลือกข้อมูลสำหรับตารางสรุปข้อมูล
ระบุช่วงข้อมูลที่คุณต้องการรวมไว้ในตารางสรุปข้อมูล 

```java
// ระบุช่วงข้อมูลสำหรับตารางสรุปข้อมูล
String sourceData = "Sheet1!A1:D100"; // เปลี่ยนสิ่งนี้เป็นช่วงข้อมูลของคุณ
```

## ขั้นตอนที่ 4: สร้างตารางสรุปข้อมูล
ตอนนี้เรามาสร้าง Pivot Table กัน

```java
// สร้างตารางสรุปข้อมูล
int index = workbook.getWorksheets().add();
Worksheet worksheet = workbook.getWorksheets().get(index);
int pivotIndex = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");
PivotTable pivotTable = worksheet.getPivotTables().get(pivotIndex);
```

## ขั้นตอนที่ 5: กำหนดค่าตารางสรุปข้อมูล
คุณสามารถกำหนดค่าตารางสรุปข้อมูลได้โดยการเพิ่มแถว คอลัมน์ และค่า การตั้งค่าตัวกรอง และอื่นๆ

```java
// กำหนดค่าตารางสรุปข้อมูล
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);  // เพิ่มแถว
pivotTable.addFieldToArea(PivotFieldType.COLUMN, 1);  // เพิ่มคอลัมน์
pivotTable.addFieldToArea(PivotFieldType.DATA, 2);  // เพิ่มค่า
```

## ขั้นตอนที่ 6: ปรับแต่งตารางสรุปข้อมูล
คุณสามารถปรับแต่งลักษณะที่ปรากฏและพฤติกรรมของ Pivot Table ได้ตามต้องการ

```java
// ปรับแต่งตารางสรุปข้อมูล
pivotTable.refreshData();
pivotTable.calculateData();
```

## ขั้นตอนที่ 7: บันทึกสมุดงาน
สุดท้าย ให้บันทึกสมุดงานด้วยตารางสรุปข้อมูล

```java
// บันทึกสมุดงาน
workbook.save("output.xlsx");
```

## บทสรุป
ในบทช่วยสอนนี้ เราจะแนะนำขั้นตอนการสร้าง Pivot Table โดยใช้ Aspose.Cells for Java API ตอนนี้คุณสามารถปรับปรุงความสามารถในการวิเคราะห์และแสดงข้อมูลได้อย่างง่ายดาย

## คำถามที่พบบ่อย
### Pivot Table คืออะไร?
   Pivot Table เป็นเครื่องมือประมวลผลข้อมูลที่ใช้สรุป วิเคราะห์ และแสดงข้อมูลจากแหล่งต่างๆ

### ฉันสามารถเพิ่มตารางสรุปข้อมูลหลายตารางลงในเวิร์กชีตเดียวได้หรือไม่
   ใช่ คุณสามารถเพิ่มตารางสรุปข้อมูลหลายตารางลงในเวิร์กชีตเดียวกันได้ตามต้องการ

### Aspose.Cells เข้ากันได้กับรูปแบบข้อมูลที่แตกต่างกันหรือไม่
   ใช่ Aspose.Cells รองรับรูปแบบข้อมูลหลากหลาย รวมถึง Excel, CSV และอื่นๆ อีกมากมาย

### ฉันสามารถปรับแต่งการจัดรูปแบบของตารางสรุปข้อมูลได้หรือไม่
   แน่นอน คุณสามารถปรับแต่งลักษณะที่ปรากฏและการจัดรูปแบบของ Pivot Table ให้ตรงตามความต้องการของคุณได้

### ฉันสามารถสร้าง Pivot Table แบบอัตโนมัติในแอปพลิเคชัน Java ได้อย่างไร
   คุณสามารถทำให้การสร้าง Pivot Table ใน Java เป็นอัตโนมัติได้โดยใช้ Aspose.Cells สำหรับ Java API ตามที่สาธิตในบทช่วยสอนนี้

ตอนนี้คุณมีความรู้และโค้ดในการสร้าง Pivot Table ที่มีประสิทธิภาพใน Java โดยใช้ Aspose.Cells แล้ว ทดลองใช้แหล่งข้อมูลและการกำหนดค่าต่างๆ เพื่อปรับแต่ง Pivot Table ให้เหมาะกับความต้องการของคุณ วิเคราะห์ข้อมูลอย่างสนุกสนาน!
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}