---
title: ส่งออก Excel เป็น JSON
linktitle: ส่งออก Excel เป็น JSON
second_title: API การประมวลผล Java Excel ของ Aspose.Cells
description: เรียนรู้วิธีส่งออกข้อมูล Excel เป็น JSON โดยใช้ Aspose.Cells สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนนี้พร้อมโค้ดต้นฉบับเพื่อการแปลงที่ราบรื่น
weight: 17
url: /th/java/excel-import-export/export-excel-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel เป็น JSON


ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนการส่งออกข้อมูล Excel เป็นรูปแบบ JSON โดยใช้ไลบรารี Aspose.Cells สำหรับ Java คำแนะนำทีละขั้นตอนนี้จะให้ตัวอย่างโค้ดต้นฉบับแก่คุณเพื่อช่วยให้คุณแปลงไฟล์ Excel เป็นข้อมูล JSON ได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่ม โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java ไว้ในระบบของคุณแล้ว
-  Aspose.Cells สำหรับ Java: ดาวน์โหลดและติดตั้งไลบรารี Aspose.Cells สำหรับ Java จาก[ที่นี่](https://releases.aspose.com/cells/java/).
- ไฟล์ Excel: เตรียมไฟล์ Excel ที่คุณต้องการแปลงเป็น JSON

## ขั้นตอนที่ 1: นำเข้า Aspose.Cells สำหรับ Java
ขั้นแรก คุณต้องนำเข้าไลบรารี Aspose.Cells เข้าสู่โปรเจ็กต์ Java ของคุณ เพิ่มบรรทัดต่อไปนี้ลงในโค้ด Java ของคุณ:

```java
import com.aspose.cells.*;
```

## ขั้นตอนที่ 2: โหลดไฟล์ Excel
ขั้นตอนต่อไปคือโหลดไฟล์ Excel ที่คุณต้องการส่งออกเป็น JSON คุณสามารถใช้โค้ดสั้นๆ ต่อไปนี้เพื่อดำเนินการดังกล่าว:

```java
// โหลดไฟล์ Excel
Workbook workbook = new Workbook("your_excel_file.xlsx");
```

 แทนที่`"your_excel_file.xlsx"` พร้อมเส้นทางไปยังไฟล์ Excel ของคุณ

## ขั้นตอนที่ 3: แปลงเป็น JSON
ตอนนี้เรามาแปลงข้อมูล Excel เป็นรูปแบบ JSON กัน ใช้โค้ดต่อไปนี้เพื่อดำเนินการแปลง:

```java
// เริ่มต้น JsonSaveOptions
JsonSaveOptions jsonSaveOptions = new JsonSaveOptions();

// บันทึกสมุดงานเป็น JSON
workbook.save("output.json", jsonSaveOptions);
```

โค้ดนี้จะบันทึกข้อมูล Excel เป็นไฟล์ JSON ชื่อ "output.json" ในไดเร็กทอรีโครงการของคุณ

## ขั้นตอนที่ 4: การจัดการข้อมูล JSON
ตอนนี้คุณสามารถทำงานกับข้อมูล JSON ได้ตามต้องการ คุณสามารถแยกวิเคราะห์ จัดการ หรือใช้ในแอปพลิเคชันของคุณได้

## บทสรุป
ขอแสดงความยินดี! คุณได้ส่งออกข้อมูล Excel เป็น JSON โดยใช้ Aspose.Cells สำหรับ Java สำเร็จแล้ว คำแนะนำทีละขั้นตอนนี้จะให้โค้ดต้นฉบับที่จำเป็นแก่คุณเพื่อปรับปรุงกระบวนการให้มีประสิทธิภาพยิ่งขึ้น ขณะนี้ คุณสามารถแปลงไฟล์ Excel เป็น JSON ในแอปพลิเคชัน Java ของคุณได้อย่างมีประสิทธิภาพ

## คำถามที่พบบ่อย
### ฉันสามารถส่งออกแผ่นงาน Excel หลายแผ่นไปยังไฟล์ JSON เดียวได้หรือไม่
   ใช่ คุณสามารถส่งออกชีต Excel หลายชีตไปยังไฟล์ JSON เดียวได้โดยใช้ Aspose.Cells สำหรับ Java เพียงโหลดชีตแต่ละชีตแล้วบันทึกลงในไฟล์ JSON เดียวกัน

### Aspose.Cells สำหรับ Java เข้ากันได้กับรูปแบบ Excel ล่าสุดหรือไม่
   ใช่ Aspose.Cells สำหรับ Java รองรับรูปแบบ Excel ล่าสุด รวมถึง XLSX และ XLS

### ฉันจะจัดการโครงสร้างข้อมูล Excel ที่ซับซ้อนในระหว่างการส่งออก JSON ได้อย่างไร
   คุณสามารถใช้ Aspose.Cells API เพื่อนำทางและจัดการโครงสร้างข้อมูล Excel ที่ซับซ้อนก่อนส่งออกเป็น JSON

### ฉันสามารถปรับแต่งรูปแบบเอาต์พุต JSON ได้หรือไม่
   ใช่ คุณสามารถปรับแต่งรูปแบบเอาต์พุต JSON ได้โดยใช้ตัวเลือกที่ Aspose.Cells จัดทำไว้สำหรับ JsonSaveOptions ของ Java

### มี Aspose.Cells เวอร์ชันทดลองใช้สำหรับ Java หรือไม่
   ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้ของ Aspose.Cells สำหรับ Java ได้จากเว็บไซต์ของพวกเขาเพื่อประเมินคุณลักษณะต่างๆ ของมัน

อย่าลังเลที่จะสำรวจความเป็นไปได้เพิ่มเติมด้วย Aspose.Cells สำหรับ Java เพื่อปรับปรุงความสามารถในการประมวลผลข้อมูลของคุณ
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
