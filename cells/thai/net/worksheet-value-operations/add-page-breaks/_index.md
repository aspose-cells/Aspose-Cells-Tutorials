---
"description": "เรียนรู้วิธีการเพิ่มตัวแบ่งหน้าแนวนอนและแนวตั้งใน Excel โดยใช้ Aspose.Cells สำหรับ .NET ด้วยคู่มือทีละขั้นตอนนี้ ทำให้ไฟล์ Excel ของคุณพิมพ์ได้"
"linktitle": "เพิ่มตัวแบ่งหน้าในเวิร์กชีตโดยใช้ Aspose.Cells"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "เพิ่มตัวแบ่งหน้าในเวิร์กชีตโดยใช้ Aspose.Cells"
"url": "/th/net/worksheet-value-operations/add-page-breaks/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มตัวแบ่งหน้าในเวิร์กชีตโดยใช้ Aspose.Cells

## การแนะนำ
ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนการเพิ่มตัวแบ่งหน้าทั้งแนวนอนและแนวตั้งในเวิร์กชีต Excel ของคุณ นอกจากนี้ คุณยังจะได้พบกับคำแนะนำทีละขั้นตอนเกี่ยวกับวิธีใช้ Aspose.Cells สำหรับ .NET เพื่อจัดการตัวแบ่งหน้าได้อย่างง่ายดาย และเมื่ออ่านคู่มือนี้จบ คุณจะคุ้นเคยกับการใช้เทคนิคเหล่านี้ในโปรเจ็กต์ของคุณเอง เริ่มกันเลย!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกโค้ด เรามาตรวจสอบกันก่อนว่าคุณพร้อมที่จะทำตามบทช่วยสอนนี้แล้วหรือไม่ นี่คือข้อกำหนดเบื้องต้นบางประการ:
- Visual Studio: คุณจะต้องติดตั้ง Visual Studio ไว้ในระบบของคุณ
- Aspose.Cells สำหรับ .NET: คุณควรติดตั้งไลบรารี Aspose.Cells หากคุณยังไม่ได้ติดตั้ง ไม่ต้องกังวล! คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้งานฟรีเพื่อเริ่มต้นใช้งานได้ (คุณสามารถรับได้ [ที่นี่](https://releases.aspose.com/cells/net/)-
- .NET Framework: บทช่วยสอนนี้ถือว่าคุณกำลังใช้งาน .NET Framework หรือ .NET Core หากคุณใช้สภาพแวดล้อมอื่น กระบวนการอาจแตกต่างกันเล็กน้อย
นอกจากนี้ คุณควรมีความคุ้นเคยพื้นฐานกับการเขียนโปรแกรม C# และแนวคิดเรื่องการแบ่งหน้าใน Excel
## แพ็คเกจนำเข้า
ในการเริ่มทำงานกับ Aspose.Cells เราจำเป็นต้องนำเข้าเนมสเปซที่เกี่ยวข้องเข้าสู่โปรเจ็กต์ของเรา ซึ่งจะช่วยให้เราเข้าถึงฟังก์ชันที่ Aspose.Cells จัดเตรียมไว้เพื่อจัดการไฟล์ Excel ได้
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
เมื่อคุณนำเข้าเนมสเปซเหล่านี้แล้ว คุณสามารถเริ่มโต้ตอบกับไฟล์ Excel และปรับเปลี่ยนต่าง ๆ รวมถึงการเพิ่มตัวแบ่งหน้า
ตอนนี้คุณได้ตั้งค่าเรียบร้อยแล้ว มาดูขั้นตอนในการเพิ่มตัวแบ่งหน้าในเวิร์กชีตกัน เราจะแบ่งแต่ละส่วนของกระบวนการออกเป็นส่วนๆ พร้อมทั้งอธิบายโค้ดแต่ละบรรทัดอย่างละเอียด
## ขั้นตอนที่ 1: ตั้งค่าสมุดงานของคุณ
ขั้นแรกคุณต้องสร้างสมุดงานใหม่ `Workbook` คลาสใน Aspose.Cells แสดงถึงเวิร์กบุ๊ก Excel และเป็นจุดเริ่มต้นในการจัดการไฟล์ Excel
```csharp
// กำหนดเส้นทางไปยังไดเร็กทอรีที่ไฟล์ของคุณจะถูกบันทึก
string dataDir = "Your Document Directory";
// สร้างวัตถุเวิร์กบุ๊กใหม่
Workbook workbook = new Workbook();
```
ในโค้ดนี้:
- `dataDir` ระบุตำแหน่งที่จะบันทึกไฟล์ของคุณ
- การ `Workbook` สร้างวัตถุซึ่งจะใช้ในการเก็บและจัดการไฟล์ Excel ของคุณ
## ขั้นตอนที่ 2: เพิ่มตัวแบ่งหน้าแนวนอน
ต่อไปเราจะเพิ่มตัวแบ่งหน้าแนวนอนให้กับเวิร์กชีต ตัวแบ่งหน้าแนวนอนจะแบ่งเวิร์กชีตออกเป็นสองส่วนในแนวนอน ซึ่งหมายความว่าตัวแบ่งหน้าจะกำหนดว่าเนื้อหาจะแบ่งที่ใดในหน้าใหม่ในแนวตั้งเมื่อทำการพิมพ์
```csharp
// เพิ่มตัวแบ่งหน้าแนวนอนที่แถวที่ 30
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
ในตัวอย่างนี้:
- `Worksheets[0]` หมายถึงแผ่นงานแรกในเวิร์กบุ๊ก (โปรดจำไว้ว่าเวิร์กชีตจะมีดัชนีเป็นศูนย์)
- `HorizontalPageBreaks.Add("Y30")` เพิ่มตัวแบ่งหน้าที่แถวที่ 30 ซึ่งหมายความว่าเนื้อหาที่อยู่ก่อนแถวที่ 30 จะปรากฏในหน้าหนึ่ง และทุกอย่างที่อยู่ด้านล่างจะเริ่มต้นในหน้าใหม่
## ขั้นตอนที่ 3: เพิ่มตัวแบ่งหน้าแนวตั้ง
ในทำนองเดียวกัน คุณสามารถเพิ่มตัวแบ่งหน้าแนวตั้งได้ ซึ่งจะแบ่งเวิร์กชีตในคอลัมน์ที่ระบุ ทำให้แน่ใจได้ว่าเนื้อหาทางด้านซ้ายของตัวแบ่งจะปรากฏในหน้าหนึ่ง และเนื้อหาทางด้านขวาจะปรากฏในหน้าถัดไป
```csharp
// เพิ่มตัวแบ่งหน้าแนวตั้งที่คอลัมน์ Y
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
ที่นี่:
- การ `VerticalPageBreaks.Add("Y30")` วิธีการนี้จะเพิ่มตัวแบ่งหน้าแนวตั้งที่คอลัมน์ Y (นั่นคือ หลังคอลัมน์ที่ 25) ซึ่งจะสร้างตัวแบ่งหน้าระหว่างคอลัมน์ X และ Y
## ขั้นตอนที่ 4: บันทึกสมุดงาน
หลังจากเพิ่มตัวแบ่งหน้าแล้ว ขั้นตอนสุดท้ายคือการบันทึกเวิร์กบุ๊กลงในไฟล์ คุณสามารถระบุเส้นทางที่คุณต้องการบันทึกไฟล์ Excel ได้
```csharp
// บันทึกไฟล์ Excel
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
การดำเนินการนี้จะบันทึกเวิร์กบุ๊กพร้อมตัวแบ่งหน้าเพิ่มเติมไปยังเส้นทางไฟล์ที่ระบุ (`AddingPageBreaks_out.xls`-
## บทสรุป
การเพิ่มตัวแบ่งหน้าใน Excel เป็นฟีเจอร์สำคัญเมื่อคุณกำลังทำงานกับชุดข้อมูลขนาดใหญ่หรือกำลังเตรียมเอกสารสำหรับการพิมพ์ ด้วย Aspose.Cells สำหรับ .NET คุณสามารถทำให้กระบวนการแทรกตัวแบ่งหน้าทั้งแนวนอนและแนวตั้งในเวิร์กชีต Excel ของคุณเป็นแบบอัตโนมัติได้อย่างง่ายดาย ทำให้มั่นใจได้ว่าเอกสารของคุณได้รับการจัดระเบียบอย่างดีและอ่านง่าย
## คำถามที่พบบ่อย
### ฉันจะเพิ่มตัวแบ่งหน้าหลายตัวใน Aspose.Cells สำหรับ .NET ได้อย่างไร
คุณสามารถเพิ่มตัวแบ่งหน้าหลายหน้าได้ด้วยการเรียกใช้ `HหรือizontalPageBreaks.Add()` or `VerticalPageBreaks.Add()` วิธีการหลายครั้งด้วยการอ้างอิงเซลล์ที่แตกต่างกัน
### ฉันสามารถเพิ่มตัวแบ่งหน้าในเวิร์กชีตเฉพาะของเวิร์กบุ๊กได้หรือไม่
ใช่ คุณสามารถระบุแผ่นงานได้โดยใช้ `Worksheets[index]` ทรัพย์สินที่ `index` เป็นดัชนีฐานศูนย์ของเวิร์กชีต
### ฉันจะลบตัวแบ่งหน้าใน Aspose.Cells สำหรับ .NET ได้อย่างไร
คุณสามารถลบตัวแบ่งหน้าได้โดยใช้ `HหรือizontalPageBreaks.RemoveAt()` or `VerticalPageBreaks.RemoveAt()` วิธีการโดยการระบุดัชนีของตัวแบ่งหน้าที่คุณต้องการลบ
### จะเกิดอะไรขึ้นหากฉันต้องการเพิ่มตัวแบ่งหน้าโดยอัตโนมัติตามขนาดเนื้อหา?
Aspose.Cells ไม่มีคุณลักษณะอัตโนมัติในการเพิ่มตัวแบ่งหน้าตามขนาดเนื้อหา แต่คุณสามารถคำนวณโดยอัตโนมัติว่าตัวแบ่งหน้าควรเกิดขึ้นที่ใดโดยอิงจากจำนวนแถว/คอลัมน์
### ฉันสามารถตั้งค่าตัวแบ่งหน้าตามช่วงเซลล์ที่เจาะจงได้หรือไม่
ใช่ คุณสามารถระบุตัวแบ่งหน้าสำหรับเซลล์หรือช่วงใดๆ ได้โดยการระบุการอ้างอิงเซลล์ที่สอดคล้องกัน เช่น "A1" หรือ "B15"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}