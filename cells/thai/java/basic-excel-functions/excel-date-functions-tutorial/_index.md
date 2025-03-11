---
title: บทช่วยสอนเกี่ยวกับฟังก์ชันวันที่ของ Excel
linktitle: บทช่วยสอนเกี่ยวกับฟังก์ชันวันที่ของ Excel
second_title: API การประมวลผล Java Excel ของ Aspose.Cells
description: เรียนรู้ฟังก์ชันวันที่ของ Excel โดยใช้ Aspose.Cells สำหรับ Java สำรวจบทช่วยสอนแบบทีละขั้นตอนพร้อมโค้ดต้นฉบับ
weight: 19
url: /th/java/basic-excel-functions/excel-date-functions-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บทช่วยสอนเกี่ยวกับฟังก์ชันวันที่ของ Excel


## บทช่วยสอนแนะนำฟังก์ชันวันที่ของ Excel

ในบทช่วยสอนที่ครอบคลุมนี้ เราจะมาสำรวจฟังก์ชันวันที่ของ Excel และวิธีใช้ประโยชน์จากความสามารถของ Aspose.Cells สำหรับ Java เพื่อทำงานกับข้อมูลที่เกี่ยวข้องกับวันที่ ไม่ว่าคุณจะเป็นนักพัฒนามากประสบการณ์หรือเพิ่งเริ่มต้นใช้ Aspose.Cells คู่มือนี้จะช่วยให้คุณใช้ประโยชน์จากศักยภาพของฟังก์ชันวันที่ใน Excel ได้ ดังนั้นมาเริ่มกันเลย!

## ทำความเข้าใจฟังก์ชันวันที่ใน Excel

Excel มีฟังก์ชันวันที่มากมายที่ช่วยลดความซับซ้อนของการคำนวณที่เกี่ยวข้องกับวันที่ ฟังก์ชันเหล่านี้มีประโยชน์อย่างยิ่งสำหรับงานต่างๆ เช่น การคำนวณวันที่ การหาความแตกต่างระหว่างวันที่ และอื่นๆ อีกมากมาย มาสำรวจฟังก์ชันวันที่ทั่วไปกัน:

### ฟังก์ชั่น DATE

ฟังก์ชัน DATE สร้างวันที่โดยใช้ค่าปี เดือน และวันที่มีให้ เราจะสาธิตวิธีใช้กับ Aspose.Cells สำหรับ Java

### ฟังก์ชั่นวันนี้

ฟังก์ชัน TODAY ส่งคืนวันที่ปัจจุบัน เรียนรู้วิธีเรียกข้อมูลนี้โดยใช้โปรแกรมโดยใช้ Aspose.Cells

### ฟังก์ชัน DATEDIF

DATEDIF คำนวณความแตกต่างระหว่างวันที่สองวัน โดยแสดงผลลัพธ์ในหน่วยต่างๆ (เช่น วัน เดือน ปี) ค้นพบวิธีการนำฟังก์ชันนี้ไปใช้กับ Aspose.Cells สำหรับ Java

### ฟังก์ชัน EOMONTH

EOMONTH คืนค่าวันสุดท้ายของเดือนสำหรับวันที่ที่กำหนด เรียนรู้วิธีรับวันที่สิ้นเดือนด้วย Aspose.Cells

## การทำงานกับ Aspose.Cells สำหรับ Java

ตอนนี้เราได้ครอบคลุมพื้นฐานของฟังก์ชันวันที่ของ Excel แล้ว มาเจาะลึกการใช้ Aspose.Cells สำหรับ Java เพื่อทำงานกับฟังก์ชันเหล่านี้ในเชิงโปรแกรมกัน

### การตั้งค่า Aspose.Cells

ก่อนที่เราจะเริ่มเขียนโค้ด เราจะต้องตั้งค่า Aspose.Cells สำหรับ Java ในโปรเจ็กต์ของเราเสียก่อน ทำตามขั้นตอนเหล่านี้เพื่อเริ่มต้น

1. ดาวน์โหลดและติดตั้ง Aspose.Cells: เยี่ยมชม[Aspose.Cells สำหรับ Java](https://releases.aspose.com/cells/java/) และดาวน์โหลดเวอร์ชันล่าสุด

2. รวม Aspose.Cells ในโครงการของคุณ: เพิ่มไลบรารี Aspose.Cells ในโครงการ Java ของคุณ

3. การกำหนดค่าใบอนุญาต: ตรวจสอบให้แน่ใจว่าคุณมีใบอนุญาตที่ถูกต้องในการใช้ Aspose.Cells

### การใช้ฟังก์ชัน DATE กับ Aspose.Cells

มาเริ่มต้นด้วยตัวอย่างการใช้งานฟังก์ชัน DATE ใน Excel โดยใช้ Aspose.Cells สำหรับ Java

```java
// สร้างสมุดงานใหม่
Workbook workbook = new Workbook();

// เข้าถึงแผ่นงานแรก
Worksheet worksheet = workbook.getWorksheets().get(0);

// ตั้งค่าวันที่โดยใช้ฟังก์ชั่น DATE
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// รับค่าวันที่คำนวณ
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// พิมพ์ผลลัพธ์
System.out.println("Calculated Date: " + calculatedDate);
```

### การทำงานกับฟังก์ชั่น TODAY

ตอนนี้เรามาดูวิธีการดึงวันที่ปัจจุบันโดยใช้ฟังก์ชัน TODAY ใน Aspose.Cells สำหรับ Java กัน

```java
// สร้างสมุดงานใหม่
Workbook workbook = new Workbook();

// เข้าถึงแผ่นงานแรก
Worksheet worksheet = workbook.getWorksheets().get(0);

// ใช้ฟังก์ชั่น TODAY เพื่อรับวันที่ปัจจุบัน
worksheet.getCells().get("A1").setFormula("=TODAY()");

// รับค่าวันที่ปัจจุบัน
String currentDate = worksheet.getCells().get("A1").getStringValue();

// พิมพ์ผลลัพธ์
System.out.println("Current Date: " + currentDate);
```

### การคำนวณความแตกต่างของวันที่ด้วย DATEDIF

คุณสามารถคำนวณความแตกต่างของวันที่ได้อย่างง่ายดายด้วยฟังก์ชัน DATEDIF ใน Excel ต่อไปนี้เป็นวิธีการดำเนินการโดยใช้ Aspose.Cells สำหรับ Java

```java
// สร้างสมุดงานใหม่
Workbook workbook = new Workbook();

// เข้าถึงแผ่นงานแรก
Worksheet worksheet = workbook.getWorksheets().get(0);

// ตั้งค่าวันที่สองค่า
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// คำนวณความแตกต่างโดยใช้ DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

//รับความแตกต่างภายในไม่กี่วัน
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// พิมพ์ผลลัพธ์
System.out.println("Days Difference: " + daysDifference);
```

### การค้นหาจุดสิ้นสุดของเดือน

ด้วย Aspose.Cells สำหรับ Java คุณสามารถค้นหาจุดสิ้นสุดของเดือนของวันที่กำหนดได้อย่างง่ายดายโดยใช้ฟังก์ชัน EOMONTH

```java
// สร้างสมุดงานใหม่
Workbook workbook = new Workbook();

// เข้าถึงแผ่นงานแรก
Worksheet worksheet = workbook.getWorksheets().get(0);

// ตั้งค่าค่าวันที่
worksheet.getCells().get("A1").putValue("2023-09-07");

// คำนวณสิ้นเดือนโดยใช้ EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// รับวันที่สิ้นเดือน
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// พิมพ์ผลลัพธ์
System.out.println("End of Month: " + endOfMonth);
```

## บทสรุป

บทช่วยสอนนี้ให้ภาพรวมที่ครอบคลุมเกี่ยวกับฟังก์ชันวันที่ของ Excel และวิธีการทำงานกับฟังก์ชันเหล่านี้โดยใช้ Aspose.Cells สำหรับ Java คุณได้เรียนรู้วิธีการตั้งค่า Aspose.Cells ใช้ฟังก์ชัน DATE, TODAY, DATEDIF และ EOMONTH และคำนวณวันที่ด้วยโปรแกรม ด้วยความรู้ดังกล่าว คุณสามารถปรับปรุงงานที่เกี่ยวข้องกับวันที่ใน Excel และปรับปรุงแอปพลิเคชัน Java ของคุณให้ดีขึ้นได้

## คำถามที่พบบ่อย

### ฉันจะจัดรูปแบบวันที่ใน Aspose.Cells สำหรับ Java ได้อย่างไร

 การจัดรูปแบบวันที่ใน Aspose.Cells นั้นทำได้ง่าย คุณสามารถใช้`Style` คลาสสำหรับกำหนดรูปแบบวันที่และนำไปใช้กับเซลล์ ตัวอย่างเช่น หากต้องการแสดงวันที่ในรูปแบบ "dd-MM-yyyy":

```java
// สร้างรูปแบบวันที่
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// ใช้รูปแบบกับเซลล์
worksheet.getCells().get("A1").setStyle(dateStyle);
```

### ฉันสามารถทำการคำนวณวันที่ขั้นสูงด้วย Aspose.Cells ได้หรือไม่

ใช่ คุณสามารถคำนวณวันที่ขั้นสูงได้ด้วย Aspose.Cells โดยการรวมฟังก์ชันวันที่ของ Excel และ Aspose.Cells API เข้าด้วยกัน คุณสามารถจัดการงานที่เกี่ยวข้องกับวันที่ที่ซับซ้อนได้อย่างมีประสิทธิภาพ

### Aspose.Cells เหมาะสำหรับการประมวลผลวันที่ขนาดใหญ่หรือไม่?

Aspose.Cells สำหรับ Java เหมาะอย่างยิ่งสำหรับการประมวลผลข้อมูลวันที่ทั้งขนาดเล็กและขนาดใหญ่ โดยให้ประสิทธิภาพและความน่าเชื่อถือสูง จึงเป็นตัวเลือกที่ยอดเยี่ยมสำหรับการจัดการข้อมูลที่เกี่ยวข้องกับวันที่ในแอปพลิเคชันต่างๆ

### ฉันสามารถหาทรัพยากรและเอกสารเพิ่มเติมสำหรับ Aspose.Cells สำหรับ Java ได้จากที่ไหน

 คุณสามารถเข้าถึงเอกสารและทรัพยากรที่ครอบคลุมสำหรับ Aspose.Cells สำหรับ Java ได้ที่[ที่นี่](https://reference.aspose.com/cells/java/).

### ฉันจะเริ่มต้นใช้งาน Aspose.Cells สำหรับ Java ได้อย่างไร?

 หากต้องการเริ่มต้นใช้งาน Aspose.Cells สำหรับ Java ให้ดาวน์โหลดไลบรารีจาก[ที่นี่](https://releases.aspose.com/cells/java/) และดูเอกสารประกอบสำหรับการติดตั้งและ
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
