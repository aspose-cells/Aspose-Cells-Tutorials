---
"description": "เรียนรู้วิธีระบุ HTML CrossType ใน Aspose.Cells สำหรับ .NET ปฏิบัติตามบทช่วยสอนทีละขั้นตอนของเราเพื่อแปลงไฟล์ Excel เป็น HTML อย่างแม่นยำ"
"linktitle": "การระบุ HTML CrossType ในโปรแกรมเอาท์พุต HTML ใน .NET"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การระบุ HTML CrossType ในโปรแกรมเอาท์พุต HTML ใน .NET"
"url": "/th/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การระบุ HTML CrossType ในโปรแกรมเอาท์พุต HTML ใน .NET

## การแนะนำ
เมื่อต้องแปลงไฟล์ Excel เป็น HTML ในแอปพลิเคชัน .NET คุณอาจพบว่าคุณต้องระบุวิธีการจัดการการอ้างอิงแบบไขว้ในผลลัพธ์ คลาส HtmlSaveOptions ใน Aspose.Cells สำหรับ .NET มีการตั้งค่าต่างๆ เพื่อควบคุมกระบวนการแปลง และตัวเลือกหนึ่งคือ HtmlCrossType ในบทช่วยสอนนี้ เราจะอธิบายวิธีระบุ HTML แบบไขว้ในเชิงโปรแกรมเมื่อส่งออกไฟล์ Excel เป็นรูปแบบ HTML 
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกโค้ด ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- Aspose.Cells สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.Cells ไว้ในโปรเจ็กต์ของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/cells/net/).
- Visual Studio: การติดตั้งการทำงานของ Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET อื่นๆ
- ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจตัวอย่างต่างๆ ได้ดีขึ้น
- ไฟล์ตัวอย่าง Excel: เตรียมไฟล์ตัวอย่าง Excel ให้พร้อมสำหรับการใช้งาน สำหรับตัวอย่างนี้ เราจะใช้ `sampleHtmlCrossStringType-xlsx`.
## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณจะต้องนำเข้าเนมสเปซ Aspose.Cells ที่จำเป็น นี่คือวิธีที่คุณสามารถทำได้:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
ให้เราแบ่งขั้นตอนนี้ออกทีละขั้นตอนเพื่อให้คุณทำตามและนำฟังก์ชันนี้ไปใช้ในโปรเจ็กต์ของคุณเองได้อย่างง่ายดาย
## ขั้นตอนที่ 1: กำหนดไดเรกทอรีแหล่งที่มาและเอาต์พุตของคุณ
ขั้นแรก คุณต้องตั้งค่าไดเร็กทอรีสำหรับไฟล์ Excel ต้นทางและตำแหน่งที่คุณต้องการบันทึกไฟล์ HTML เอาท์พุต
```csharp
// ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory";
// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory";
```
## ขั้นตอนที่ 2: โหลดไฟล์ตัวอย่าง Excel
ขั้นตอนต่อไป โหลดไฟล์ Excel ตัวอย่างของคุณลงใน `Workbook` วัตถุ นี่คือจุดที่ความมหัศจรรย์ทั้งหมดเริ่มต้น
```csharp
// โหลดไฟล์ตัวอย่าง Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
ที่นี่แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงที่ไฟล์ Excel ของคุณตั้งอยู่ บรรทัดนี้จะอ่านไฟล์ Excel ลงในหน่วยความจำเพื่อให้คุณสามารถจัดการไฟล์ได้
## ขั้นตอนที่ 3: ระบุตัวเลือกการบันทึก HTML
ตอนนี้เราจะสร้างอินสแตนซ์ของ `HtmlSaveOptions`ซึ่งช่วยให้คุณสามารถกำหนดค่าวิธีการแปลงไฟล์ Excel เป็น HTML ได้
```csharp
// ระบุประเภท HTML Cross
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
ในขั้นตอนนี้เราได้ตั้งค่า `HtmlCrossStringType` ถึง `HtmlCrossType.Default`ซึ่งเป็นหนึ่งในตัวเลือกที่มีให้สำหรับการจัดการการอ้างอิงแบบไขว้ในผลลัพธ์ HTML
## ขั้นตอนที่ 4: เปลี่ยนประเภทครอสตามต้องการ
คุณสามารถระบุประเภทที่แตกต่างกันได้ `HtmlCrossStringType` ตามความต้องการของคุณ ต่อไปนี้คือตัวเลือกต่างๆ ที่คุณสามารถใช้ได้:
- `HtmlCrossType.Default`: ประเภทข้ามเริ่มต้น
- `HtmlCrossType.MSExport`:ส่งออก HTML ด้วยพฤติกรรมคล้ายกับ MS Excel
- `HtmlCrossType.Cross`: สร้างการอ้างอิงแบบไขว้
- `HtmlCrossType.FitToCell`:ปรับการอ้างอิงแบบไขว้ให้ตรงกับขนาดเซลล์
คุณสามารถปรับเปลี่ยนได้ `HtmlCrossStringType` แบบนี้:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpหรือt;
// หรือ 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## ขั้นตอนที่ 5: บันทึกไฟล์ HTML เอาท์พุต
เมื่อคุณกำหนดค่าตัวเลือกของคุณเสร็จแล้ว ก็ถึงเวลาบันทึกไฟล์ HTML ที่แปลงแล้ว ใช้ `Save` วิธีการของคุณ `Workbook` วัตถุ:
```csharp
// เอาท์พุต HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
ที่นี่เราจะตั้งชื่อไฟล์เอาท์พุตตาม `HtmlCrossStringType` เราได้ตั้งค่าไว้แล้ว ด้วยวิธีนี้ คุณสามารถระบุได้อย่างง่ายดายว่ามีการใช้ประเภทครอสใดในการแปลง
## ขั้นตอนที่ 6: ยืนยันการดำเนินการสำเร็จ
สุดท้ายนี้ การยืนยันว่าการดำเนินการของคุณประสบความสำเร็จถือเป็นแนวทางปฏิบัติที่ดี คุณสามารถพิมพ์ข้อความไปยังคอนโซลได้:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
วิธีนี้จะทำให้คุณทราบว่ากระบวนการเสร็จสมบูรณ์โดยไม่มีข้อผิดพลาดใดๆ
## บทสรุป
และแล้วคุณก็จะได้มัน! คุณได้ระบุ HTML cross-type สำหรับการส่งออก Excel ของคุณใน .NET โดยใช้ Aspose.Cells สำเร็จแล้ว ฟังก์ชันนี้มีประโยชน์อย่างยิ่งเมื่อคุณต้องรักษาการจัดรูปแบบหรือการอ้างอิงเฉพาะในผลลัพธ์ HTML ของคุณ เพื่อให้แน่ใจว่าเอกสารที่แปลงแล้วของคุณตรงตามความต้องการของคุณ
## คำถามที่พบบ่อย
### HtmlCrossType ใน Aspose.Cells คืออะไร?  
HtmlCrossType กำหนดวิธีการจัดการการอ้างอิงแบบไขว้ในไฟล์ Excel ระหว่างการแปลง HTML คุณสามารถเลือกตัวเลือกต่างๆ เช่น Default, MSExport, Cross และ FitToCell
### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?  
Aspose.Cells นำเสนอเวอร์ชันทดลองใช้งานฟรี คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์](https://releases-aspose.com/).
### ฉันจะติดตั้ง Aspose.Cells ในโครงการ .NET ของฉันได้อย่างไร?  
คุณสามารถติดตั้ง Aspose.Cells ผ่าน NuGet Package Manager ใน Visual Studio ได้โดยรันคำสั่ง: `Install-Package Aspose-Cells`.
### ฉันสามารถค้นหาเอกสารสำหรับ Aspose.Cells ได้ที่ไหน  
คุณสามารถค้นหาเอกสารประกอบที่ครอบคลุมเกี่ยวกับ Aspose.Cells ได้ [ที่นี่](https://reference-aspose.com/cells/net/).
### ฉันควรทำอย่างไรหากพบข้อผิดพลาดขณะบันทึกไฟล์ HTML?  
ตรวจสอบให้แน่ใจว่าเส้นทางไดเรกทอรีถูกต้องและคุณมีสิทธิ์ในการเขียนสำหรับไดเรกทอรีเอาต์พุต หากปัญหายังคงมีอยู่ โปรดตรวจสอบฟอรัมสนับสนุน Aspose เพื่อขอความช่วยเหลือ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}