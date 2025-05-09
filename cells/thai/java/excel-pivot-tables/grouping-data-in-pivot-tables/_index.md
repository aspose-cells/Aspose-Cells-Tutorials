---
"description": "เรียนรู้วิธีการสร้างตารางสรุปข้อมูลใน Excel โดยใช้ Aspose.Cells สำหรับ Java จัดการกลุ่มข้อมูลและวิเคราะห์ข้อมูลโดยอัตโนมัติด้วยตัวอย่างโค้ดต้นฉบับ"
"linktitle": "การจัดกลุ่มข้อมูลในตารางสรุปข้อมูล"
"second_title": "API การประมวลผล Java Excel ของ Aspose.Cells"
"title": "การจัดกลุ่มข้อมูลในตารางสรุปข้อมูล"
"url": "/th/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การจัดกลุ่มข้อมูลในตารางสรุปข้อมูล


ตารางสรุปข้อมูลเป็นเครื่องมือที่มีประสิทธิภาพสำหรับการวิเคราะห์และสรุปข้อมูลในสเปรดชีต โดยช่วยให้คุณสามารถจัดกลุ่มและจัดหมวดหมู่ข้อมูลเพื่อให้ได้ข้อมูลเชิงลึกที่มีค่า ในบทความนี้ เราจะมาสำรวจวิธีการจัดกลุ่มข้อมูลในตารางสรุปข้อมูลอย่างมีประสิทธิภาพโดยใช้ Aspose.Cells สำหรับ Java พร้อมกับตัวอย่างโค้ดต้นฉบับ

## การแนะนำ

ตารางสรุปข้อมูลช่วยให้จัดระเบียบและสรุปข้อมูลจากชุดข้อมูลขนาดใหญ่ได้อย่างยืดหยุ่น โดยตารางสรุปข้อมูลเหล่านี้จะช่วยให้คุณสร้างมุมมองข้อมูลแบบกำหนดเองได้โดยการจัดกลุ่มข้อมูลเป็นหมวดหมู่หรือลำดับชั้น ซึ่งจะช่วยให้คุณระบุแนวโน้ม รูปแบบ และค่าผิดปกติในข้อมูลได้ง่ายขึ้น

## ขั้นตอนที่ 1: สร้างตารางสรุปข้อมูล

เริ่มต้นด้วยการสร้างตารางสรุปข้อมูลโดยใช้ Aspose.Cells สำหรับ Java ด้านล่างนี้เป็นตัวอย่างวิธีการสร้างตารางสรุปข้อมูลจากไฟล์ Excel ตัวอย่าง

```java
// โหลดไฟล์ Excel
Workbook workbook = new Workbook("sample.xlsx");

// เข้าถึงแผ่นงานที่ประกอบด้วยข้อมูล
Worksheet worksheet = workbook.getWorksheets().get(0);

// ระบุช่วงข้อมูล
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // สมมติว่ามีข้อมูล 20 แถว
sourceData.startColumn = 0;
sourceData.endColumn = 3; // สมมติว่ามีข้อมูล 4 คอลัมน์

// สร้างตารางสรุปข้อมูลโดยอิงตามช่วงข้อมูล
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// รับตารางสรุปข้อมูลตามดัชนี
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// เพิ่มฟิลด์ลงในแถวและคอลัมน์
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// เพิ่มค่าและใช้การรวมค่า
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// บันทึกไฟล์ Excel ที่ถูกแก้ไข
workbook.save("output.xlsx");
```

## ขั้นตอนที่ 2: จัดกลุ่มข้อมูล

ใน Aspose.Cells สำหรับ Java คุณสามารถจัดกลุ่มข้อมูลภายในตารางสรุปข้อมูลได้โดยใช้ `PivotField` คลาส นี่คือตัวอย่างวิธีการจัดกลุ่มฟิลด์ในตารางสรุปข้อมูล:

```java
// เข้าถึงฟิลด์ "ผลิตภัณฑ์" ในตารางสรุปข้อมูล
PivotField productField = pivotTable.getPivotFields().get("Product");

// จัดกลุ่มฟิลด์ "ผลิตภัณฑ์" ตามเงื่อนไขเฉพาะ เช่น ตามตัวอักษรเริ่มต้น
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// บันทึกไฟล์ Excel ที่แก้ไขแล้วพร้อมข้อมูลแบบกลุ่ม
workbook.save("output_grouped.xlsx");
```

## ขั้นตอนที่ 3: ปรับแต่งการจัดกลุ่ม

คุณสามารถปรับแต่งการตั้งค่าการจัดกลุ่มเพิ่มเติมได้ เช่น การระบุช่วงการจัดกลุ่มตามวันที่หรือกฎการจัดกลุ่มแบบกำหนดเอง นี่คือตัวอย่างการปรับแต่งการจัดกลุ่มตามวันที่:

```java
// เข้าถึงฟิลด์ "วันที่" ในตารางสรุปข้อมูล (โดยถือว่าเป็นฟิลด์วันที่)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// วันที่จัดกลุ่มตามเดือน
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// บันทึกไฟล์ Excel ที่แก้ไขแล้วพร้อมการจัดกลุ่มวันที่แบบกำหนดเอง
workbook.save("output_custom_grouping.xlsx");
```

## บทสรุป

การจัดกลุ่มข้อมูลในตารางสรุปข้อมูลเป็นเทคนิคที่มีประโยชน์สำหรับการวิเคราะห์และสรุปข้อมูลใน Excel และ Aspose.Cells สำหรับ Java ช่วยให้กระบวนการนี้เป็นไปโดยอัตโนมัติได้ง่าย ด้วยตัวอย่างโค้ดต้นฉบับที่ให้มา คุณสามารถสร้างตารางสรุปข้อมูล ปรับแต่งการจัดกลุ่ม และรับข้อมูลเชิงลึกจากข้อมูลของคุณได้อย่างมีประสิทธิภาพ

## คำถามที่พบบ่อย

### 1. วัตถุประสงค์ของตารางสรุปข้อมูลใน Excel คืออะไร

ตารางสรุปข้อมูลใน Excel ใช้เพื่อสรุปและวิเคราะห์ชุดข้อมูลขนาดใหญ่ ช่วยให้คุณสามารถสร้างมุมมองข้อมูลแบบกำหนดเองได้ ทำให้ระบุรูปแบบและแนวโน้มได้ง่ายขึ้น

### 2. ฉันจะปรับแต่งการจัดกลุ่มข้อมูลในตารางสรุปข้อมูลได้อย่างไร

คุณสามารถปรับแต่งการจัดกลุ่มข้อมูลในตารางสรุปข้อมูลได้โดยใช้ `PivotField` คลาสใน Aspose.Cells สำหรับ Java ช่วยให้คุณสามารถระบุเกณฑ์การจัดกลุ่ม เช่น ช่วงเวลาตามวันที่หรือกฎที่กำหนดเองได้

### 3. ฉันสามารถใช้ Aspose.Cells สำหรับ Java เพื่อสร้างตารางสรุปข้อมูลแบบอัตโนมัติได้หรือไม่

ใช่ คุณสามารถทำให้การสร้างตารางสรุปข้อมูลใน Excel เป็นแบบอัตโนมัติได้โดยใช้ Aspose.Cells สำหรับ Java ตามที่สาธิตในตัวอย่างโค้ดต้นฉบับที่ให้มา

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}