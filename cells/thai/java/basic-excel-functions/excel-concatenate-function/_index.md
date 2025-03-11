---
title: ฟังก์ชัน CONCATENATE ของ Excel
linktitle: ฟังก์ชัน CONCATENATE ของ Excel
second_title: API การประมวลผล Java Excel ของ Aspose.Cells
description: เรียนรู้วิธีต่อข้อความใน Excel โดยใช้ Aspose.Cells สำหรับ Java คำแนะนำทีละขั้นตอนนี้ประกอบด้วยตัวอย่างโค้ดต้นฉบับสำหรับการจัดการข้อความอย่างราบรื่น
weight: 13
url: /th/java/basic-excel-functions/excel-concatenate-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ฟังก์ชัน CONCATENATE ของ Excel


## การแนะนำฟังก์ชัน Excel CONCATENATE โดยใช้ Aspose.Cells สำหรับ Java

ในบทช่วยสอนนี้ เราจะมาเรียนรู้วิธีใช้ฟังก์ชัน CONCATENATE ใน Excel โดยใช้ Aspose.Cells สำหรับ Java CONCATENATE เป็นฟังก์ชัน Excel ที่มีประโยชน์ซึ่งช่วยให้คุณสามารถรวมหรือเชื่อมสตริงข้อความหลายรายการเข้าด้วยกันได้ ด้วย Aspose.Cells สำหรับ Java คุณสามารถบรรลุฟังก์ชันเดียวกันนี้ในโปรแกรมแอปพลิเคชัน Java ของคุณได้

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา Java: คุณควรติดตั้ง Java ไว้ในระบบของคุณพร้อมกับ Integrated Development Environment (IDE) ที่เหมาะสม เช่น Eclipse หรือ IntelliJ IDEA

2. Aspose.Cells สำหรับ Java: คุณต้องติดตั้งไลบรารี Aspose.Cells สำหรับ Java คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/cells/java/).

## ขั้นตอนที่ 1: สร้างโครงการ Java ใหม่

ขั้นแรก ให้สร้างโปรเจ็กต์ Java ใหม่ใน IDE ที่คุณต้องการ ตรวจสอบให้แน่ใจว่าคุณได้กำหนดค่าโปรเจ็กต์ของคุณให้รวมไลบรารี Aspose.Cells สำหรับ Java ไว้ใน classpath

## ขั้นตอนที่ 2: นำเข้าไลบรารี Aspose.Cells

ในโค้ด Java ของคุณ ให้นำเข้าคลาสที่จำเป็นจากไลบรารี Aspose.Cells:

```java
import com.aspose.cells.*;
```

## ขั้นตอนที่ 3: เริ่มต้นเวิร์กบุ๊ก

สร้างวัตถุเวิร์กบุ๊กใหม่เพื่อแสดงไฟล์ Excel ของคุณ คุณสามารถสร้างไฟล์ Excel ใหม่หรือเปิดไฟล์ที่มีอยู่แล้วก็ได้ ที่นี่เราจะสร้างไฟล์ Excel ใหม่:

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ขั้นตอนที่ 4: ป้อนข้อมูล

มาเติมข้อมูลลงในเวิร์กชีต Excel กัน สำหรับตัวอย่างนี้ เราจะสร้างตารางง่ายๆ ที่มีค่าข้อความที่เราต้องการเชื่อมโยงกัน

```java
// ข้อมูลตัวอย่าง
String text1 = "Hello";
String text2 = " ";
String text3 = "World";

// ป้อนข้อมูลลงในเซลล์
worksheet.getCells().get("A1").putValue(text1);
worksheet.getCells().get("B1").putValue(text2);
worksheet.getCells().get("C1").putValue(text3);
```

## ขั้นตอนที่ 5: เชื่อมโยงข้อความ

ตอนนี้ ให้ใช้ Aspose.Cells เพื่อเชื่อมข้อความจากเซลล์ A1, B1 และ C1 ลงในเซลล์ใหม่ เช่น D1

```java
// เชื่อมข้อความจากเซลล์ A1, B1 และ C1 ลงใน D1
worksheet.getCells().get("D1").setFormula("=CONCATENATE(A1, B1, C1)");
```

## ขั้นตอนที่ 6: คำนวณสูตร

เพื่อให้แน่ใจว่าสูตร CONCATENATE ได้รับการประเมิน คุณจำเป็นต้องคำนวณสูตรใหม่ในเวิร์กชีต

```java
// คำนวณสูตรใหม่
workbook.calculateFormula();
```

## ขั้นตอนที่ 7: บันทึกไฟล์ Excel

สุดท้ายให้บันทึกสมุดงาน Excel ลงในไฟล์

```java
workbook.save("concatenated_text.xlsx");
```

## บทสรุป

 ในบทช่วยสอนนี้ เราได้เรียนรู้วิธีการต่อข้อความใน Excel โดยใช้ Aspose.Cells สำหรับ Java เราได้ครอบคลุมขั้นตอนพื้นฐานตั้งแต่การเริ่มต้นเวิร์กบุ๊กไปจนถึงการบันทึกไฟล์ Excel นอกจากนี้ เรายังได้สำรวจวิธีทางเลือกสำหรับการต่อข้อความโดยใช้`Cell.putValue` วิธีการ ตอนนี้คุณสามารถใช้ Aspose.Cells สำหรับ Java เพื่อเชื่อมต่อข้อความในแอปพลิเคชัน Java ของคุณได้อย่างง่ายดาย

## คำถามที่พบบ่อย

### ฉันจะเชื่อมข้อความจากเซลล์ต่างๆ ใน Excel โดยใช้ Aspose.Cells สำหรับ Java ได้อย่างไร

หากต้องการเชื่อมข้อความจากเซลล์ต่างๆ ใน Excel โดยใช้ Aspose.Cells สำหรับ Java ให้ทำตามขั้นตอนเหล่านี้:

1. สร้างการเริ่มต้นวัตถุเวิร์กบุ๊ก

2. ป้อนข้อมูลข้อความลงในเซลล์ที่ต้องการ

3.  ใช้`setFormula` วิธีการสร้างสูตร CONCATENATE เพื่อเชื่อมข้อความจากเซลล์เข้าด้วยกัน

4.  คำนวณสูตรใหม่ในเวิร์กชีตโดยใช้`workbook.calculateFormula()`.

5. บันทึกไฟล์ Excel

เสร็จเรียบร้อย! คุณได้เชื่อมโยงข้อความใน Excel โดยใช้ Aspose.Cells สำหรับ Java สำเร็จแล้ว

### ฉันสามารถเชื่อมสตริงข้อความมากกว่าสามรายการโดยใช้ CONCATENATE ได้หรือไม่

ใช่ คุณสามารถเชื่อมสตริงข้อความได้มากกว่าสามสตริงโดยใช้ CONCATENATE ใน Excel และ Aspose.Cells สำหรับ Java เพียงขยายสูตรเพื่อรวมการอ้างอิงเซลล์เพิ่มเติมตามต้องการ

### มีทางเลือกอื่นสำหรับ CONCATENATE ใน Aspose.Cells สำหรับ Java หรือไม่

 ใช่ Aspose.Cells สำหรับ Java ให้ทางเลือกในการต่อข้อความโดยใช้`Cell.putValue` วิธีการนี้ คุณสามารถเชื่อมโยงข้อความจากหลายเซลล์และกำหนดผลลัพธ์ในเซลล์อื่นได้โดยไม่ต้องใช้สูตร

```java
// เชื่อมข้อความจากเซลล์ A1, B1 และ C1 ลงใน D1 โดยไม่ต้องใช้สูตร
String concatenatedText = text1 + text2 + text3;
worksheet.getCells().get("D1").putValue(concatenatedText);
```

วิธีการนี้อาจเป็นประโยชน์หากคุณต้องการเรียงข้อความโดยไม่ต้องพึ่งสูตร Excel
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
