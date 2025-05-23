---
"description": "เรียนรู้การเพิ่มและปรับแต่งตัวควบคุมบรรทัดในเวิร์กชีต Excel โดยใช้ Aspose.Cells สำหรับ .NET ในบทช่วยสอนที่ครอบคลุมนี้"
"linktitle": "เพิ่มการควบคุมบรรทัดลงในเวิร์กชีตใน Excel"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "เพิ่มการควบคุมบรรทัดลงในเวิร์กชีตใน Excel"
"url": "/th/net/excel-shapes-controls/add-line-control-to-worksheet-excel/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มการควบคุมบรรทัดลงในเวิร์กชีตใน Excel

## การแนะนำ
สเปรดชีต Excel ไม่ใช่แค่เรื่องของแถวและคอลัมน์ของข้อมูลเท่านั้น แต่ยังเป็นผืนผ้าใบสำหรับการแสดงภาพอีกด้วย การเพิ่มตัวควบคุมบรรทัดสามารถปรับปรุงวิธีการแสดงข้อมูลในเวิร์กชีตของคุณ ทำให้ความสัมพันธ์และแนวโน้มชัดเจนขึ้นมาก ลองใช้ Aspose.Cells สำหรับ .NET ซึ่งเป็นไลบรารีอันทรงพลังที่ช่วยลดความซับซ้อนของกระบวนการสร้างและจัดการไฟล์ Excel ด้วยโปรแกรม ในคู่มือนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนต่างๆ ในการเพิ่มตัวควบคุมบรรทัดในเวิร์กชีตโดยใช้ Aspose.Cells หากคุณพร้อมที่จะยกระดับเกม Excel ของคุณแล้ว มาเริ่มกันเลย!
## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่มเพิ่มบรรทัดลงในเวิร์กชีต Excel ของคุณ นี่คือสิ่งที่คุณต้องการ:
1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว หากยังไม่ได้ติดตั้ง คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์](https://visualstudio-microsoft.com/).
2. Aspose.Cells สำหรับ .NET: ไลบรารีนี้จะต้องมีการอ้างอิงในโปรเจ็กต์ของคุณ คุณสามารถดูเอกสารรายละเอียดได้ [ที่นี่](https://reference.aspose.com/cells/net/) และดาวน์โหลดห้องสมุด [ที่นี่](https://releases-aspose.com/cells/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจโค้ดที่เราจะดู
4. สภาพแวดล้อม Windows: เนื่องจาก Aspose.Cells ได้รับการออกแบบมาสำหรับแอปพลิเคชัน .NET จึงต้องการสภาพแวดล้อม Windows
## แพ็คเกจนำเข้า
มาตั้งค่าสภาพแวดล้อมการเขียนโค้ดก่อนที่เราจะเริ่มเพิ่มบรรทัดลงในเวิร์กชีต Excel ของคุณ ต่อไปนี้คือวิธีนำเข้าแพ็กเกจ Aspose.Cells ที่จำเป็นลงในโปรเจ็กต์ของคุณ
### สร้างโครงการใหม่
- เปิด Visual Studio
- สร้างโปรเจ็กต์แอปพลิเคชันคอนโซลใหม่ คุณสามารถตั้งชื่อได้ตามต้องการ—อาจใช้ชื่อว่า "ExcelLineDemo" เพื่อความชัดเจน
### ติดตั้ง Aspose.Cells
- ไปที่ตัวจัดการแพ็กเกจ NuGet ใน Visual Studio (`Tools` - `NuGet Package Manager` - `Manage NuGet Packages for Solution`-
- ค้นหา `Aspose.Cells` และติดตั้ง การดำเนินการนี้จะเพิ่มไลบรารีที่จำเป็นให้กับโครงการของคุณ
### นำเข้าเนมสเปซ
ที่ด้านบนของไฟล์โปรแกรมหลักของคุณ เพิ่มคำสั่ง using ต่อไปนี้เพื่อให้สามารถเข้าถึง Aspose.Cells ได้:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
การดำเนินการนี้จะทำให้คุณใช้ฟังก์ชันทั้งหมดจากไลบรารี Aspose.Cells ได้โดยไม่ต้องใส่คำนำหน้าฟังก์ชันเหล่านั้น
ตอนนี้เราตั้งค่าเรียบร้อยแล้ว ถึงเวลาเพิ่มบรรทัดลงในเวิร์กชีตของเรา เราจะอธิบายแต่ละขั้นตอนโดยละเอียด
## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสาร
ก่อนที่คุณจะเริ่มทำงานกับไฟล์ Excel คุณต้องกำหนดตำแหน่งที่จะบันทึกไฟล์ โดยทำได้ดังนี้:
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
```
แทนที่ `"Your Document Directory"` โดยมีเส้นทางที่ถูกต้องบนระบบของคุณซึ่งคุณต้องการจัดเก็บไฟล์เอาต์พุต
## ขั้นตอนที่ 2: สร้างไดเรกทอรี
การตรวจสอบให้แน่ใจว่าไดเรกทอรีมีอยู่ถือเป็นแนวทางปฏิบัติที่ดี หากไม่มี คุณสามารถสร้างไดเรกทอรีนั้นได้โดยใช้โค้ดต่อไปนี้:
```csharp
// สร้างไดเร็กทอรีหากยังไม่มีอยู่
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
โค้ดสั้นๆ นี้จะตรวจสอบว่าไดเร็กทอรีที่ระบุมีอยู่หรือไม่ และจะสร้างไดเร็กทอรีนั้นขึ้นมาใหม่หากไม่มี ซึ่งก็เหมือนกับการตรวจสอบกระเป๋าเป้ของคุณก่อนจะออกไปเดินป่า—คุณต้องแน่ใจว่าคุณมีทุกสิ่งที่คุณต้องการ!
## ขั้นตอนที่ 3: สร้างเวิร์กบุ๊กใหม่
ตอนนี้เรามาสร้างเวิร์กบุ๊ก Excel ใหม่กัน นี่คือพื้นที่ที่คุณจะวาดเส้น
```csharp
// สร้างเวิร์กบุ๊กใหม่
Workbook workbook = new Workbook();
```
การสร้างอินสแตนซ์ใหม่ของ `Workbook` ช่วยให้คุณมีไฟล์ Excel เปล่าใหม่ไว้ใช้งาน
## ขั้นตอนที่ 4: เข้าถึงแผ่นงานแรก
ทุกสมุดงานมีเวิร์กชีตอย่างน้อยหนึ่งแผ่น และเราจะใช้แผ่นแรกสำหรับบรรทัดของเรา
```csharp
// รับแผ่นงานแรกในหนังสือเล่มนี้
Worksheet worksheet = workbook.Worksheets[0];
```
ที่นี่เราจะเลือกแผ่นงานแรกโดยเข้าถึงผ่าน `Worksheets` การรวบรวมของ `Workbook`-
## ขั้นตอนที่ 5: เพิ่มบรรทัดแรก
มาเริ่มเพิ่มเส้นกันก่อน เส้นแรกจะดูมีสไตล์ชัดเจน
```csharp
// เพิ่มบรรทัดใหม่ให้กับเวิร์กชีต
Aspose.Cells.Drawing.LineShape line1 = worksheet.Shapes.AddLine(5, 0, 1, 0, 0, 250);
```
ในคำชี้แจงนี้:
- `AddLine` วิธีการเพิ่มบรรทัดเริ่มต้นที่พิกัด `(5, 0)` และจบลงที่ `(1, 0)` ขยายไปถึงความสูง `250`-
- พิกัด `(5, 0)` แสดงถึงตำแหน่งเริ่มต้นบนแผ่นงานในขณะที่ `(1, 0, 0, 250)` หมายถึงระยะทางสิ้นสุด
## ขั้นตอนที่ 6: ตั้งค่าคุณสมบัติเส้น
ทีนี้ มาปรับแต่งเส้นกันสักหน่อย—กำหนดรูปแบบและตำแหน่งของเส้นประ
```csharp
// ตั้งค่ารูปแบบเส้นประ
line1.Line.DashStyle = MsoLineDashStyle.Solid;
// ตั้งค่าตำแหน่งการวาง
line1.Placement = PlacementType.FreeFloating;
```
ที่นี่เราบอกให้บรรทัดคงอยู่ที่เดิมโดยไม่คำนึงถึงการเปลี่ยนแปลงในโครงสร้างเวิร์กชีตโดยใช้ `PlacementType-FreeFloating`.
## ขั้นตอนที่ 7: เพิ่มบรรทัดเพิ่มเติม
มาเพิ่มบรรทัดที่ 2 ด้วยรูปแบบที่ต่างออกไปโดยใช้รูปแบบเส้นประ
```csharp
// เพิ่มอีกบรรทัดหนึ่งในเวิร์กชีต
Aspose.Cells.Drawing.LineShape line2 = worksheet.Shapes.AddLine(7, 0, 1, 0, 85, 250);
// ตั้งค่ารูปแบบเส้นประ
line2.Line.DashStyle = MsoLineDashStyle.DashLongDash;
// ตั้งค่าน้ำหนักของเส้น
line2.Line.Weight = 4;
// ตั้งค่าตำแหน่งการวาง
line2.Placement = PlacementType.FreeFloating;
```
สังเกตว่าเราปรับตำแหน่งและเปลี่ยนสไตล์ของเส้นประอย่างไร `DashLongDash`คุณสมบัติน้ำหนักช่วยให้คุณควบคุมความหนาของเส้นได้
## ขั้นตอนที่ 8: เพิ่มบรรทัดที่สาม
เพิ่มเส้นทึบอีกหนึ่งเส้นเพื่อให้รูปวาดของเราเสร็จสมบูรณ์
```csharp
// เพิ่มบรรทัดที่สามลงในเวิร์กชีต
Aspose.Cells.Drawing.LineShape line3 = worksheet.Shapes.AddLine(13, 0, 1, 0, 0, 250);
```
อีกครั้ง เรากำหนดค่าคุณสมบัติให้คล้ายกับวิธีที่เราตั้งค่าบรรทัดก่อนหน้านี้
## ขั้นตอนที่ 9: ซ่อนเส้นตาราง
เพื่อให้ภาพวาดของเราดูสะอาดตา เรามาซ่อนเส้นตารางของเวิร์กชีตกัน
```csharp
// ทำให้เส้นตารางมองไม่เห็นในเวิร์กชีตแรก
workbook.Worksheets[0].IsGridlinesVisible = false;
```
การซ่อนเส้นตารางช่วยให้ผู้ใช้สามารถโฟกัสที่เส้นจริงที่คุณเพิ่มได้มากขึ้น ซึ่งก็คล้ายกับที่จิตรกรเคลียร์พื้นที่รอบๆ ผืนผ้าใบเพื่อหลีกเลี่ยงสิ่งรบกวน
## ขั้นตอนที่ 10: บันทึกสมุดงาน
สุดท้ายนี้ เรามาบันทึกสมุดงานของเราไว้ เพื่อที่การทำงานหนักของเราจะได้ไม่สูญเปล่า!
```csharp
// บันทึกไฟล์ Excel
workbook.Save(dataDir + "book1.out.xls");
```
คุณสามารถตั้งชื่อไฟล์เอาท์พุตเป็นชื่ออะไรก็ได้ที่คุณต้องการ เพียงแต่ให้แน่ใจว่ามันลงท้ายด้วย `.xls` หรือนามสกุลไฟล์ Excel อื่น ๆ ที่รองรับ
## บทสรุป
ขอแสดงความยินดี! คุณได้เรียนรู้วิธีการเพิ่มตัวควบคุมบรรทัดในเวิร์กชีต Excel โดยใช้ Aspose.Cells สำหรับ .NET สำเร็จแล้ว ด้วยโค้ดเพียงไม่กี่บรรทัด คุณสามารถปรับปรุงไฟล์ Excel ของคุณได้อย่างยอดเยี่ยม โดยนำเสนอภาพข้อมูลของคุณที่สามารถช่วยสื่อสารข้อมูลเชิงลึกได้อย่างมีประสิทธิภาพมากขึ้น ไม่ว่าคุณต้องการสร้างรายงาน งานนำเสนอ หรือเครื่องมือวิเคราะห์ การเชี่ยวชาญไลบรารีเช่น Aspose.Cells จะทำให้เวิร์กโฟลว์ของคุณราบรื่นและมีประสิทธิภาพมากขึ้น
## คำถามที่พบบ่อย
### Aspose.Cells สำหรับ .NET คืออะไร?
Aspose.Cells สำหรับ .NET เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงไฟล์ Excel ได้โดยไม่ต้องใช้ Microsoft Excel
### ฉันสามารถเพิ่มรูปร่างอื่นนอกจากเส้นได้ไหม
ใช่ Aspose.Cells มีรูปร่างต่างๆ มากมาย เช่น สี่เหลี่ยมผืนผ้า วงรี และอื่นๆ อีกมากมาย คุณสามารถสร้างรูปทรงเหล่านี้ได้ง่ายๆ โดยใช้วิธีการที่คล้ายกัน
### การใช้ Aspose.Cells ฟรีหรือไม่?
Aspose.Cells เป็นไลบรารีที่ต้องชำระเงิน แต่คุณสามารถเริ่มต้นด้วย [ทดลองใช้งานฟรี](https://releases.aspose.com/) เพื่อสำรวจคุณสมบัติของมัน
### ฉันสามารถปรับแต่งสีของเส้นได้ไหม?
แน่นอน! คุณสามารถตั้งค่าคุณสมบัติสีของเส้นได้โดยใช้เส้น `LineColor` คุณสมบัติ.
### ฉันสามารถขอความช่วยเหลือด้านเทคนิคได้ที่ไหน?
คุณสามารถรับการสนับสนุนได้จาก [ฟอรั่ม Aspose](https://forum.aspose.com/c/cells/9) โดยที่สมาชิกชุมชนและสมาชิกทีม Aspose ช่วยเหลือผู้ใช้

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}