---
"description": "ค้นพบวิธีตรวจสอบว่าขนาดกระดาษของเวิร์กชีตเป็นอัตโนมัติหรือไม่โดยใช้ Aspose.Cells สำหรับ .NET ในคู่มือทีละขั้นตอนโดยละเอียดของเรา"
"linktitle": "ตรวจสอบว่าขนาดกระดาษของเวิร์กชีตเป็นแบบอัตโนมัติหรือไม่"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "ตรวจสอบว่าขนาดกระดาษของเวิร์กชีตเป็นแบบอัตโนมัติหรือไม่"
"url": "/th/net/worksheet-page-setup-features/check-automatic-paper-size/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ตรวจสอบว่าขนาดกระดาษของเวิร์กชีตเป็นแบบอัตโนมัติหรือไม่

## การแนะนำ
เมื่อต้องจัดการสเปรดชีตและตรวจสอบว่าสเปรดชีตได้รับการจัดรูปแบบอย่างสมบูรณ์แบบสำหรับการพิมพ์ สิ่งสำคัญประการหนึ่งที่ต้องพิจารณาคือการตั้งค่าขนาดกระดาษ ในคู่มือนี้ เราจะมาดูวิธีตรวจสอบว่าขนาดกระดาษของเวิร์กชีตถูกตั้งค่าเป็นอัตโนมัติหรือไม่โดยใช้ Aspose.Cells สำหรับ .NET ไลบรารีนี้มีเครื่องมืออันทรงพลังสำหรับความต้องการที่เกี่ยวข้องกับ Excel ทั้งหมดของคุณ ทำให้การทำงานของคุณไม่เพียงแต่ง่ายขึ้นแต่ยังมีประสิทธิภาพมากขึ้นด้วย
## ข้อกำหนดเบื้องต้น
ก่อนจะเริ่มเขียนโค้ดจริง เรามาตรวจสอบก่อนว่าคุณได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว นี่คือข้อกำหนดเบื้องต้นที่คุณต้องมี:
1. สภาพแวดล้อมการพัฒนา C#: คุณต้องมี IDE C# เช่น Visual Studio หากคุณยังไม่ได้ติดตั้ง โปรดไปที่เว็บไซต์ของ Microsoft
2. ไลบรารี Aspose.Cells: ตรวจสอบว่าคุณมีไลบรารี Aspose.Cells แล้ว คุณสามารถดาวน์โหลดได้จาก [ลิงค์นี้](https://releases-aspose.com/cells/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับแนวคิดการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจตัวอย่างและชิ้นส่วนโค้ดได้อย่างมีประสิทธิภาพ
4. ไฟล์ตัวอย่าง Excel: ตรวจสอบให้แน่ใจว่าคุณมีไฟล์ตัวอย่าง Excel ที่มีการตั้งค่าหน้าตามต้องการ สำหรับตัวอย่างของเรา คุณจะต้องใช้ไฟล์สองไฟล์:
- `samplePageSetupIsAutomaticPaperSize-False.xlsx`
- `samplePageSetupIsAutomaticPaperSize-True.xlsx`
การมีข้อกำหนดเบื้องต้นเหล่านี้จะช่วยให้คุณประสบความสำเร็จในขณะที่เราสำรวจฟังก์ชันการทำงานที่ Aspose.Cells จัดให้
## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็นลงในโปรเจ็กต์ C# ของคุณ โดยคุณสามารถทำได้ดังนี้:
### สร้างโครงการ C# ใหม่
- เปิด Visual Studio และสร้างแอปพลิเคชันคอนโซล C# ใหม่
- ตั้งชื่อมันประมาณนี้ `CheckPaperSize`-
### เพิ่มการอ้างอิง Aspose.Cells
- คลิกขวาที่โครงการของคุณใน Solution Explorer
- เลือก "จัดการแพ็คเกจ NuGet"
- ค้นหา "Aspose.Cells" และติดตั้ง
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
เมื่อคุณเตรียมทุกอย่างเสร็จเรียบร้อยแล้ว คุณก็พร้อมที่จะไปสู่ส่วนสนุก ๆ ได้เลย!
ตอนนี้มาแบ่งกระบวนการออกเป็นขั้นตอนที่สามารถจัดการได้
## ขั้นตอนที่ 1: กำหนดไดเรกทอรีแหล่งที่มาและเอาต์พุต
ขั้นแรก เราต้องระบุว่าไฟล์ Excel ตัวอย่างของเราอยู่ที่ไหน และเราต้องการบันทึกผลลัพธ์ไว้ที่ใด 
```csharp
// ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory";
```
แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงที่จัดเก็บไฟล์ Excel ตัวอย่างของคุณ ซึ่งเป็นสิ่งสำคัญเพื่อให้โปรแกรมค้นหาไฟล์ที่ต้องการใช้งาน
## ขั้นตอนที่ 2: โหลดสมุดงาน
ต่อไปเราจะโหลดเวิร์กบุ๊ก 2 เล่มที่เราเตรียมไว้ก่อนหน้านี้ วิธีทำมีดังนี้:
```csharp
// โหลดสมุดงานแรกที่มีขนาดกระดาษอัตโนมัติเป็นเท็จ
Workbook wb1 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-False.xlsx");
// โหลดสมุดงานที่สองโดยมีขนาดกระดาษอัตโนมัติจริง
Workbook wb2 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-True.xlsx");
```
เรากำลังโหลดสมุดงานทั้งสองเล่มเข้าสู่หน่วยความจำ สมุดงานเล่มแรกถูกตั้งค่าให้ปิดใช้งานคุณสมบัติปรับขนาดกระดาษอัตโนมัติ ในขณะที่สมุดงานเล่มที่สองถูกเปิดใช้งาน การตั้งค่านี้ช่วยให้เราเปรียบเทียบสมุดงานทั้งสองเล่มได้อย่างง่ายดายในภายหลัง
## ขั้นตอนที่ 3: เข้าถึงแผ่นงาน
ตอนนี้เราจะเข้าถึงเวิร์กชีตแรกจากทั้งสองเวิร์กบุ๊กเพื่อตรวจสอบการตั้งค่าขนาดกระดาษ
```csharp
// เข้าถึงเวิร์กชีตแรกของเวิร์กบุ๊กทั้งสอง
Worksheet ws11 = wb1.Worksheets[0];
Worksheet ws12 = wb2.Worksheets[0];
```
การเข้าถึงเวิร์กชีตแรก (ดัชนี 0) จากเวิร์กบุ๊กทั้งสองเล่มจะทำให้เราเน้นที่หน้าที่เกี่ยวข้องที่เราต้องการตรวจสอบ 
## ขั้นตอนที่ 4: ตรวจสอบคุณสมบัติ IsAutomaticPaperSize
มาใช้เวลาสักครู่เพื่อตรวจสอบ `IsAutomaticPaperSize` คุณสมบัติจากแผ่นงานแต่ละแผ่น
```csharp
// พิมพ์คุณสมบัติ PageSetup.IsAutomaticPaperSize ของเวิร์กชีตทั้งสอง
Console.WriteLine("First Worksheet of First Workbook - IsAutomaticPaperSize: " + ws11.PageSetup.IsAutomaticPaperSize);
Console.WriteLine("First Worksheet of Second Workbook - IsAutomaticPaperSize: " + ws12.PageSetup.IsAutomaticPaperSize);
```
ที่นี่ เราจะพิมพ์ว่าเวิร์กชีตแต่ละแผ่นมีการเปิดใช้งานคุณสมบัติปรับขนาดกระดาษอัตโนมัติหรือไม่ คุณสมบัติ `IsAutomaticPaperSize` คืนค่าบูลีน (จริงหรือเท็จ) ที่ระบุการตั้งค่า
## ขั้นตอนที่ 5: ผลลัพธ์สุดท้ายและการยืนยัน
สุดท้ายนี้ เรามาดูผลลัพธ์ของโปรแกรมในบริบทและยืนยันว่าดำเนินการสำเร็จ
```csharp
Console.WriteLine();
Console.WriteLine("DetermineIfPaperSizeOfWorksheetIsAutomatic executed successfully.\r\n");
```
หลังจากพิมพ์การตั้งค่าแล้ว เราจะพิมพ์ข้อความแสดงความสำเร็จเพื่อระบุว่าโปรแกรมของเราทำงานได้โดยไม่มีปัญหาใดๆ
## บทสรุป
ในบทช่วยสอนนี้ เราได้กล่าวถึงวิธีการตรวจสอบว่าการตั้งค่าขนาดกระดาษของเวิร์กชีตในไฟล์ Excel ถูกตั้งค่าเป็นอัตโนมัติหรือไม่โดยใช้ Aspose.Cells สำหรับ .NET เมื่อทำตามขั้นตอนเหล่านี้แล้ว คุณจะมีทักษะพื้นฐานในการจัดการไฟล์ Excel ด้วยโปรแกรมได้อย่างง่ายดาย และตรวจสอบการกำหนดค่าเฉพาะ เช่น ขนาดกระดาษ 
## คำถามที่พบบ่อย
### Aspose.Cells คืออะไร?
Aspose.Cells เป็นไลบรารีอันทรงพลังที่ออกแบบมาเพื่อจัดการรูปแบบเอกสาร Excel ในแอปพลิเคชัน .NET
### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?
ใช่ Aspose นำเสนอเวอร์ชันทดลองใช้งานฟรี คุณสามารถดาวน์โหลดได้ [ที่นี่](https://releases-aspose.com/).
### ฉันจะซื้อใบอนุญาตสำหรับ Aspose.Cells ได้อย่างไร?
คุณสามารถซื้อใบอนุญาตได้ผ่านหน้าการซื้อที่พบ [ที่นี่](https://purchase-aspose.com/buy).
### ฉันสามารถทำงานกับไฟล์ Excel ประเภทใดได้บ้างโดยใช้ Aspose.Cells?
คุณสามารถทำงานกับรูปแบบ Excel ต่างๆ ได้ รวมถึง XLS, XLSX, CSV และอื่นๆ อีกมากมาย
### ฉันสามารถค้นหาการสนับสนุนสำหรับ Aspose.Cells ได้ที่ไหน
คุณสามารถค้นหาฟอรัมสนับสนุนและทรัพยากรได้ [ที่นี่](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}