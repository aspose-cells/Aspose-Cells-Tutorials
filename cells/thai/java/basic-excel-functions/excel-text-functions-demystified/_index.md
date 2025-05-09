---
"description": "ปลดล็อกความลับของฟังก์ชันข้อความใน Excel ด้วย Aspose.Cells สำหรับ Java เรียนรู้การจัดการ แยก และแปลงข้อความใน Excel ได้อย่างง่ายดาย"
"linktitle": "ไขข้อข้องใจเกี่ยวกับฟังก์ชันข้อความของ Excel"
"second_title": "API การประมวลผล Java Excel ของ Aspose.Cells"
"title": "ไขข้อข้องใจเกี่ยวกับฟังก์ชันข้อความของ Excel"
"url": "/th/java/basic-excel-functions/excel-text-functions-demystified/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ไขข้อข้องใจเกี่ยวกับฟังก์ชันข้อความของ Excel


# ไขข้อข้องใจเกี่ยวกับฟังก์ชันข้อความของ Excel โดยใช้ Aspose.Cells สำหรับ Java

ในบทช่วยสอนนี้ เราจะเจาะลึกถึงการจัดการข้อความใน Excel โดยใช้ Aspose.Cells for Java API ไม่ว่าคุณจะเป็นผู้ใช้ Excel ที่มีประสบการณ์หรือเพิ่งเริ่มต้น การทำความเข้าใจฟังก์ชันข้อความสามารถช่วยเพิ่มทักษะการใช้สเปรดชีตของคุณได้อย่างมาก เราจะสำรวจฟังก์ชันข้อความต่างๆ และให้ตัวอย่างในทางปฏิบัติเพื่ออธิบายการใช้งาน

## การเริ่มต้น

ก่อนที่เราจะเริ่ม ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Aspose.Cells สำหรับ Java แล้ว คุณสามารถดาวน์โหลดได้ [ที่นี่](https://releases.aspose.com/cells/java/)เมื่อคุณตั้งค่าเสร็จแล้ว มาดำดิ่งสู่โลกอันน่าหลงใหลของฟังก์ชันข้อความใน Excel กันเลย

## CONCATENATE - การรวมข้อความ

การ `CONCATENATE` ฟังก์ชันนี้ช่วยให้คุณรวมข้อความจากเซลล์ต่างๆ เข้าด้วยกัน มาดูกันว่าจะทำอย่างไรกับ Aspose.Cells สำหรับ Java:

```java
// โค้ด Java สำหรับการเชื่อมต่อข้อความโดยใช้ Aspose.Cells
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
Cell cell = worksheet.getCells().get("A1");

cell.putValue("Hello, ");
cell = worksheet.getCells().get("B1");
cell.putValue("World!");

// เชื่อม A1 และ B1 เข้าใน C1
cell = worksheet.getCells().get("C1");
cell.setFormula("=CONCATENATE(A1,B1)");

workbook.calculateFormula();
```

ตอนนี้เซลล์ C1 จะมีข้อความ "Hello, World!"

## ซ้ายและขวา - การแยกข้อความ

การ `LEFT` และ `RIGHT` ฟังก์ชันช่วยให้คุณดึงอักขระจำนวนหนึ่งจากด้านซ้ายหรือด้านขวาของสตริงข้อความได้ ต่อไปนี้คือวิธีการใช้งาน:

```java
// โค้ด Java สำหรับการแยกข้อความโดยใช้ Aspose.Cells
Cell cell = worksheet.getCells().get("A2");
cell.putValue("Excel Rocks!");

// แยกตัวอักษร 5 ตัวแรกออกมา
cell = worksheet.getCells().get("B2");
cell.setFormula("=LEFT(A2, 5)");

// แยกตัวอักษร 5 ตัวสุดท้ายออกมา
cell = worksheet.getCells().get("C2");
cell.setFormula("=RIGHT(A2, 5)");

workbook.calculateFormula();
```

เซลล์ B2 จะมีคำว่า "Excel" และเซลล์ C2 จะมีคำว่า "Rocks!"

## LEN - การนับตัวอักษร

การ `LEN` ฟังก์ชันนับจำนวนอักขระในสตริงข้อความ มาดูวิธีใช้งานกับ Aspose.Cells สำหรับ Java กัน:

```java
// โค้ด Java สำหรับการนับอักขระโดยใช้ Aspose.Cells
Cell cell = worksheet.getCells().get("A3");
cell.putValue("Excel");

// นับตัวอักษร
cell = worksheet.getCells().get("B3");
cell.setFormula("=LEN(A3)");

workbook.calculateFormula();
```

เซลล์ B3 จะมี "5" เนื่องจากมี 5 อักขระใน "Excel"

## UPPER และ LOWER - เปลี่ยนเคส

การ `UPPER` และ `LOWER` ฟังก์ชันนี้ช่วยให้คุณแปลงข้อความเป็นตัวพิมพ์ใหญ่หรือตัวพิมพ์เล็กได้ โดยคุณสามารถทำได้ดังนี้:

```java
// โค้ด Java สำหรับการเปลี่ยนตัวพิมพ์เล็ก-ใหญ่โดยใช้ Aspose.Cells
Cell cell = worksheet.getCells().get("A4");
cell.putValue("java programming");

// แปลงเป็นตัวพิมพ์ใหญ่
cell = worksheet.getCells().get("B4");
cell.setFormula("=UPPER(A4)");

// แปลงเป็นตัวพิมพ์เล็ก
cell = worksheet.getCells().get("C4");
cell.setFormula("=LOWER(A4)");

workbook.calculateFormula();
```

เซลล์ B4 จะมี "JAVA PROGRAMMING" และเซลล์ C4 จะมี "JAVA programming"

## ค้นหาและแทนที่ - การค้นหาและแทนที่ข้อความ

การ `FIND` ฟังก์ชันนี้ช่วยให้คุณระบุตำแหน่งของอักขระหรือข้อความเฉพาะภายในสตริงได้ ในขณะที่ `REPLACE` ฟังก์ชันนี้ช่วยให้คุณแทนที่ข้อความได้ มาดูการใช้งานกัน:

```java
// โค้ด Java ในการค้นหาและแทนที่โดยใช้ Aspose.Cells
Cell cell = worksheet.getCells().get("A5");
cell.putValue("Search for me");

// ค้นหาตำแหน่งของ “สำหรับ”
cell = worksheet.getCells().get("B5");
cell.setFormula("=FIND(\"for\", A5)");

// แทนที่ "for" ด้วย "with"
cell = worksheet.getCells().get("C5");
cell.setFormula("=REPLACE(A5, B5, 3, \"with\")");

workbook.calculateFormula();
```

เซลล์ B5 จะมี "9" (ตำแหน่งของ "สำหรับ") และเซลล์ C5 จะมี "ค้นหากับฉัน"

## บทสรุป

ฟังก์ชันข้อความใน Excel เป็นเครื่องมือที่มีประสิทธิภาพในการจัดการและวิเคราะห์ข้อมูลข้อความ ด้วย Aspose.Cells สำหรับ Java คุณสามารถรวมฟังก์ชันเหล่านี้ลงในแอปพลิเคชัน Java ได้อย่างง่ายดาย ทำให้การทำงานที่เกี่ยวข้องกับข้อความเป็นแบบอัตโนมัติและปรับปรุงความสามารถของ Excel ของคุณ สำรวจฟังก์ชันข้อความเพิ่มเติมและปลดปล่อยศักยภาพทั้งหมดของ Excel ด้วย Aspose.Cells สำหรับ Java

## คำถามที่พบบ่อย

### ฉันจะเชื่อมข้อความจากหลายเซลล์ได้อย่างไร

หากต้องการเชื่อมข้อความจากหลายเซลล์ ให้ใช้ `CONCATENATE` ฟังก์ชั่น เช่น:
```java
Cell cell = worksheet.getCells().get("A1");
cell.setFormula("=CONCATENATE(A1, B1)");
```

### ฉันสามารถแยกตัวอักษรตัวแรกและตัวสุดท้ายจากสตริงข้อความได้หรือไม่

ใช่คุณสามารถใช้ `LEFT` และ `RIGHT` ฟังก์ชันสำหรับแยกอักขระจากจุดเริ่มต้นหรือจุดสิ้นสุดของสตริงข้อความ ตัวอย่างเช่น:
```java
Cell cell = worksheet.getCells().get("A2");
cell.setFormula("=LEFT(A2, 5)");
```

### ฉันจะนับอักขระในสตริงข้อความได้อย่างไร

ใช้ `LEN` ฟังก์ชันนับจำนวนอักขระในสตริงข้อความ ตัวอย่างเช่น:
```java
Cell cell = worksheet.getCells().get("A3");
cell.setFormula("=LEN(A3)");
```

### สามารถเปลี่ยนตัวพิมพ์ใหญ่-เล็กของข้อความได้ไหม?

ใช่ คุณสามารถแปลงข้อความเป็นตัวพิมพ์ใหญ่หรือตัวพิมพ์เล็กได้โดยใช้ `UPPER` และ `LOWER` ฟังก์ชั่น เช่น:
```java
Cell cell = worksheet.getCells().get("A4");
cell.setFormula("=UPPER(A4)");
```

### ฉันจะค้นหาและแทนที่ข้อความภายในสตริงได้อย่างไร

ในการค้นหาและแทนที่ข้อความภายในสตริง ให้ใช้ `FIND` และ `REPLACE` ฟังก์ชั่น เช่น:
```java
Cell cell = worksheet.getCells().get("A5");
cell.setFormula("=FIND(\"for\", A5)");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}