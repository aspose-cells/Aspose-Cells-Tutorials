---
"description": "รักษาความปลอดภัยไฟล์ Excel ที่คุณแชร์โดยใช้ Aspose.Cells สำหรับ .NET ด้วยคำแนะนำง่าย ๆ ของเราเกี่ยวกับเทคนิคการป้องกันและการไม่ป้องกันด้วยรหัสผ่าน"
"linktitle": "การป้องกันด้วยรหัสผ่านหรือการยกเลิกการป้องกันสมุดงานที่แชร์"
"second_title": "เอกสารอ้างอิง API Aspose.Cells สำหรับ .NET"
"title": "การป้องกันด้วยรหัสผ่านหรือการยกเลิกการป้องกันสมุดงานที่แชร์"
"url": "/th/net/excel-workbook/password-protect-or-unprotect-shared-workbook/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การป้องกันด้วยรหัสผ่านหรือการยกเลิกการป้องกันสมุดงานที่แชร์

## การแนะนำ

ในพื้นที่ทำงานดิจิทัลในปัจจุบัน การแชร์เอกสารถือเป็นสถานการณ์ทั่วไปที่ต้องพิจารณาความปลอดภัยอย่างรอบคอบ เมื่อทำงานกับไฟล์ Excel โดยเฉพาะสมุดงานที่แชร์ การปกป้องข้อมูลที่ละเอียดอ่อนจึงกลายเป็นสิ่งสำคัญที่สุด ในคู่มือนี้ ฉันจะพาคุณผ่านขั้นตอนต่างๆ ของการป้องกันด้วยรหัสผ่านและการเลิกป้องกันสมุดงานที่แชร์โดยใช้ Aspose.Cells สำหรับ .NET เมื่ออ่านจบ คุณจะรู้สึกมั่นใจในการจัดการความปลอดภัยของ Excel ได้อย่างมืออาชีพ!

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกโค้ด ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้พร้อมแล้ว:

- ความรู้พื้นฐานเกี่ยวกับ C#: คุณไม่จำเป็นต้องเป็นผู้เชี่ยวชาญด้านการเขียนโค้ด แต่คุณควรจะคุ้นเคยกับรูปแบบและแนวคิดของ C#
- Aspose.Cells สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารีในโปรเจ็กต์ของคุณแล้ว คุณสามารถ [ดาวน์โหลดได้ที่นี่](https://releases-aspose.com/cells/net/).
- .NET SDK: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET SDK ไว้เพื่อเรียกใช้แอปพลิเคชัน
- Visual Studio หรือ IDE ใดๆ: ตั้งค่าสภาพแวดล้อมการเขียนโค้ดที่คุณต้องการเพื่อเขียนและดำเนินการโค้ด

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็น ในโปรเจ็กต์ C# ของคุณ ให้รวมไลบรารี Aspose.Cells คุณสามารถทำได้ดังนี้:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

เมื่อมีแพ็คเกจที่เหมาะสม เราก็สามารถนำทางในการสร้าง ปกป้อง และยกเลิกการป้องกันสมุดงานที่แชร์ของเราได้อย่างราบรื่น 

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอาต์พุต

สิ่งแรกที่คุณต้องทำคือกำหนดว่าจะบันทึกไฟล์เอาต์พุตของคุณไว้ที่ไหน ซึ่งก็เหมือนกับการตั้งค่าโฟลเดอร์ก่อนสร้างผลงานของคุณ ดังต่อไปนี้:

```csharp
// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory";
```

โค้ดบรรทัดนี้จะดึงเส้นทางไดเรกทอรีที่ไฟล์ที่สร้างขึ้นจะถูกจัดเก็บไว้ โปรดตรวจสอบให้แน่ใจว่าไดเรกทอรีนี้มีอยู่ มิฉะนั้น คุณอาจพบข้อผิดพลาดไม่พบไฟล์ในภายหลัง

## ขั้นตอนที่ 2: สร้างสมุดงานใหม่

ขั้นต่อไป เราจะสร้างอินสแตนซ์ของเวิร์กบุ๊ก Excel ใหม่ ลองนึกภาพว่านี่เป็นการปูผ้าใบเปล่าเพื่อเริ่มสร้างผลงานชิ้นเอกของคุณ

```csharp
// สร้างไฟล์ Excel เปล่า
Workbook wb = new Workbook();
```

บรรทัดนี้จะเริ่มต้นวัตถุเวิร์กบุ๊กใหม่ที่ชื่อ `wb`ตอนนี้เราก็พร้อมที่จะทำงานบนผืนผ้าใบใหม่นี้แล้ว

## ขั้นตอนที่ 3: ปกป้องสมุดงานที่แชร์ด้วยรหัสผ่าน

ตอนนี้มาถึงส่วนที่น่าสนใจ นั่นคือการปกป้องสมุดงานของเรา การใช้รหัสผ่านจะช่วยให้มั่นใจได้ว่าเฉพาะผู้ที่มีข้อมูลประจำตัวที่ถูกต้องเท่านั้นจึงจะทำการเปลี่ยนแปลงได้ วิธีดำเนินการมีดังนี้:

```csharp
// ปกป้องสมุดงานที่แชร์ด้วยรหัสผ่าน
wb.ProtectSharedWorkbook("1234");
```

ในกรณีนี้ "1234" คือรหัสผ่านของเรา คุณสามารถเปลี่ยนรหัสผ่านเป็นรหัสอื่นได้ตามต้องการ คำสั่งนี้จะล็อกเวิร์กบุ๊กเพื่อป้องกันการแก้ไขโดยไม่ได้รับอนุญาต

## ขั้นตอนที่ 4: (ทางเลือก) ยกเลิกการป้องกันสมุดงาน

หากคุณเปลี่ยนใจหรือต้องการแก้ไขสมุดงานในภายหลัง คุณสามารถปลดล็อกได้ง่ายๆ โดยยกเลิกการแสดงความคิดเห็นในบรรทัดด้านล่าง เหมือนกับมีกุญแจสำหรับตู้เซฟของคุณ:

```csharp
// ยกเลิกความคิดเห็นบรรทัดนี้เพื่อยกเลิกการป้องกันสมุดงานที่แชร์
// wb.UnprotectSharedWorkbook("1234");
```

เมื่อคุณพร้อมที่จะแก้ไขอีกครั้ง คุณเพียงเรียกใช้วิธีนี้ด้วยรหัสผ่านที่ถูกต้อง

## ขั้นตอนที่ 5: บันทึกไฟล์ Excel เอาท์พุต

ขั้นตอนสุดท้ายคือการบันทึกสมุดงานของคุณ นี่คือที่ที่งานหนักของคุณจะถูกเก็บไว้เพื่อใช้ในอนาคต คล้ายกับการบันทึกเอกสารบนคอมพิวเตอร์ของคุณ

```csharp
// บันทึกไฟล์ Excel เอาท์พุต
wb.Save(outputDir + "outputProtectSharedWorkbook.xlsx");
```

บรรทัดนี้จะบันทึกสมุดงานที่ได้รับการป้องกันของคุณในไดเร็กทอรีเอาต์พุตที่กำหนดโดยใช้ชื่อ "outputProtectSharedWorkbook.xlsx" 

## ขั้นตอนที่ 6: ตรวจสอบการดำเนินการ

หลังจากบันทึกสมุดงานแล้ว ควรตรวจสอบว่าทุกอย่างเป็นไปด้วยดีหรือไม่ นี่คือข้อความยืนยันง่ายๆ:

```csharp
Console.WriteLine("PasswordProtectOrUnprotectSharedWorkbook executed successfully.\r\n");
```

ด้วยวิธีนี้ คุณจะรู้ว่าโค้ดของคุณถูกดำเนินการตามที่คาดหวัง และไฟล์ Excel ของคุณก็พร้อมใช้งานแล้ว!

## บทสรุป

ในบทช่วยสอนนี้ เราได้แนะนำวิธีการป้องกันและยกเลิกการป้องกันสมุดงานที่แชร์โดยใช้ Aspose.Cells สำหรับ .NET โดยทำตามขั้นตอนเหล่านี้ คุณสามารถมั่นใจได้ว่าไฟล์ Excel ของคุณจะยังคงปลอดภัยในขณะที่ยังอนุญาตให้ทำงานร่วมกันได้ ไม่ว่าคุณจะแชร์ข้อมูลทางการเงินที่ละเอียดอ่อนหรือข้อมูลลูกค้า การปกป้องงานของคุณถือเป็นสิ่งสำคัญในสภาพแวดล้อมปัจจุบัน

## คำถามที่พบบ่อย

### ฉันสามารถใช้รหัสผ่านที่ซับซ้อนกว่านี้ได้หรือไม่
แน่นอน! คุณสามารถใช้สตริงใดๆ ที่ตรงตามข้อกำหนดนโยบายรหัสผ่านของคุณได้

### จะเกิดอะไรขึ้นหากฉันลืมรหัสผ่าน?
หากคุณลืมรหัสผ่าน คุณจะไม่สามารถยกเลิกการป้องกันสมุดงานได้โดยไม่ต้องใช้เครื่องมือหรือผู้เชี่ยวชาญจากบุคคลที่สาม

### การใช้ Aspose.Cells ฟรีหรือไม่?
Aspose.Cells เป็นผลิตภัณฑ์เชิงพาณิชย์ แต่คุณสามารถลองใช้ได้ฟรีเป็นเวลาจำกัดผ่านการทดลองใช้ฟรี: [ทดลองใช้งานฟรี](https://releases-aspose.com/).

### มีวิธีนำสิ่งนี้ไปใช้ในภาษาการเขียนโปรแกรมอื่น ๆ หรือไม่?
Aspose.Cells รองรับ .NET เป็นหลัก แต่ก็มีไลบรารีสำหรับ Java และภาษาอื่นๆ ด้วยเช่นกัน ตรวจสอบเว็บไซต์ของพวกเขาเพื่อดูข้อมูลเพิ่มเติม!

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้อย่างไร
คุณสามารถติดต่อขอความช่วยเหลือได้ผ่านทางฟอรัมสนับสนุน: [การสนับสนุน Aspose](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}