---
title: การสร้างการตรวจสอบข้อมูลแบบกำหนดเอง
linktitle: การสร้างการตรวจสอบข้อมูลแบบกำหนดเอง
second_title: API การประมวลผล Java Excel ของ Aspose.Cells
description: เรียนรู้วิธีสร้างการตรวจสอบข้อมูลแบบกำหนดเองโดยใช้ Aspose.Cells สำหรับ Java คำแนะนำทีละขั้นตอนพร้อมโค้ดต้นฉบับ
weight: 10
url: /th/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสร้างการตรวจสอบข้อมูลแบบกำหนดเอง


## การแนะนำ

การตรวจสอบข้อมูลช่วยรักษาความสมบูรณ์ของข้อมูลโดยป้องกันไม่ให้ผู้ใช้ป้อนข้อมูลที่ไม่ถูกต้องหรือไม่ถูกต้องลงในสเปรดชีต Excel แม้ว่า Excel จะมีตัวเลือกการตรวจสอบข้อมูลในตัว แต่ก็มีสถานการณ์บางอย่างที่คุณจำเป็นต้องกำหนดกฎการตรวจสอบแบบกำหนดเอง Aspose.Cells สำหรับ Java ช่วยให้คุณสามารถทำสิ่งนี้ได้อย่างมีประสิทธิภาพ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำดิ่งลงไปในโค้ด ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

-  Aspose.Cells สำหรับ Java: ดาวน์โหลดและติดตั้งไลบรารีจาก[ที่นี่](https://releases.aspose.com/cells/java/).

## ขั้นตอนที่ 1: การตั้งค่าโครงการ Java ของคุณ

ในการเริ่มต้น ให้สร้างโปรเจ็กต์ Java ใหม่ใน Integrated Development Environment (IDE) ที่คุณต้องการ เพิ่มไลบรารี Aspose.Cells สำหรับ Java ลงในคลาสพาธของโปรเจ็กต์ของคุณ

## ขั้นตอนที่ 2: การสร้างเวิร์กบุ๊ก Excel

เริ่มต้นด้วยการสร้างเวิร์กบุ๊ก Excel ใหม่โดยใช้ Aspose.Cells สำหรับ Java

```java
// โค้ด Java เพื่อสร้างเวิร์กบุ๊ก Excel ใหม่
Workbook workbook = new Workbook();
```

## ขั้นตอนที่ 3: การเพิ่มเวิร์กชีต

ตอนนี้ มาเพิ่มเวิร์กชีตลงในเวิร์กบุ๊กซึ่งเราจะใช้การตรวจสอบข้อมูลแบบกำหนดเอง

```java
// โค้ด Java สำหรับเพิ่มเวิร์กชีต
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ขั้นตอนที่ 4: การกำหนดเกณฑ์การตรวจสอบแบบกำหนดเอง

ในขั้นตอนนี้ เราจะกำหนดเกณฑ์การตรวจสอบแบบกำหนดเองที่ข้อมูลของเราต้องปฏิบัติตาม สมมติว่าเราต้องการจำกัดอายุที่ป้อนในเซลล์ให้อยู่ระหว่าง 18 ถึง 60 ปี

```java
// รหัส Java เพื่อกำหนดเกณฑ์การตรวจสอบแบบกำหนดเอง
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## ขั้นตอนที่ 5: การใช้การตรวจสอบข้อมูลกับช่วง

ตอนนี้เราได้กำหนดเกณฑ์การตรวจสอบแบบกำหนดเองแล้ว มาลองใช้กับช่วงเซลล์ที่เจาะจงกัน

```java
// โค้ด Java เพื่อใช้การตรวจสอบข้อมูลกับช่วง
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // ใช้การตรวจสอบกับสิบแถวแรก
area.endColumn = 0;

validation.addArea(area);
```

## ขั้นตอนที่ 6: การบันทึกไฟล์ Excel

สุดท้าย ให้บันทึกไฟล์ Excel โดยใช้กฎการตรวจสอบข้อมูลแบบกำหนดเองที่นำไปใช้

```java
// โค้ด Java สำหรับบันทึกไฟล์ Excel
workbook.save("CustomDataValidation.xlsx");
```

## บทสรุป

ในบทช่วยสอนนี้ เราได้ศึกษาวิธีการสร้างกฎการตรวจสอบข้อมูลแบบกำหนดเองโดยใช้ Aspose.Cells สำหรับ Java โดยทำตามขั้นตอนเหล่านี้ คุณสามารถมั่นใจได้ว่าข้อมูล Excel ของคุณเป็นไปตามเกณฑ์เฉพาะ ซึ่งจะช่วยเพิ่มความสมบูรณ์และความถูกต้องของข้อมูล

## คำถามที่พบบ่อย

### ฉันจะดาวน์โหลด Aspose.Cells สำหรับ Java ได้อย่างไร?

 คุณสามารถดาวน์โหลด Aspose.Cells สำหรับ Java ได้จากเว็บไซต์ที่[ที่นี่](https://releases.aspose.com/cells/java/).

### ฉันสามารถใช้การตรวจสอบข้อมูลแบบกำหนดเองกับช่วงต่างๆ ในเวิร์กชีตเดียวกันได้หรือไม่

ใช่ คุณสามารถนำการตรวจสอบข้อมูลแบบกำหนดเองไปใช้กับช่วงต่างๆ หลายช่วงภายในเวิร์กชีตเดียวกันได้ โดยทำซ้ำขั้นตอนที่ 5 สำหรับช่วงที่ต้องการแต่ละช่วง

### มีการตรวจสอบข้อมูลประเภทอื่นๆ ที่รองรับโดย Aspose.Cells สำหรับ Java หรือไม่

ใช่ Aspose.Cells สำหรับ Java รองรับการตรวจสอบข้อมูลประเภทต่างๆ รวมถึงจำนวนเต็ม ทศนิยม วันที่ เวลา ความยาวข้อความ และอื่นๆ อีกมากมาย

### ฉันจะปรับแต่งข้อความแสดงข้อผิดพลาดที่แสดงเมื่อการตรวจสอบข้อมูลล้มเหลวได้อย่างไร

 คุณสามารถปรับแต่งข้อความแสดงข้อผิดพลาดได้โดยการแก้ไข`setErrorMessage` วิธีการในขั้นตอนที่ 4 โดยที่คุณกำหนดเกณฑ์การตรวจสอบ

### Aspose.Cells สำหรับ Java ทำงานกับไฟล์ Excel ในรูปแบบที่แตกต่างกันได้หรือไม่

ใช่ Aspose.Cells สำหรับ Java รองรับรูปแบบไฟล์ Excel หลากหลาย รวมถึง XLS, XLSX, XLSM และอื่นๆ อีกมากมาย
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
