---
"description": "เรียนรู้วิธีแยกไฟล์ MOL ที่ฝังไว้จากเวิร์กบุ๊ก Excel โดยใช้ Aspose.Cells สำหรับ .NET ในบทช่วยสอนทีละขั้นตอนโดยละเอียดนี้"
"linktitle": "แยกไฟล์ Embedded Mol จากเวิร์กบุ๊ก"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "แยกไฟล์ Embedded Mol จากเวิร์กบุ๊ก"
"url": "/th/net/workbook-operations/extract-embedded-mol-file/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# แยกไฟล์ Embedded Mol จากเวิร์กบุ๊ก

## การแนะนำ
เมื่อต้องจัดการข้อมูลในเวิร์กบุ๊ก Excel บางครั้งคุณอาจพบวัตถุฝังตัวต่างๆ ที่ไม่อยู่ในรูปแบบมาตรฐาน รูปแบบหนึ่งคือ MOL (ไฟล์โครงสร้างโมเลกุล) ซึ่งมักใช้ในเคมีเพื่อแสดงข้อมูลโมเลกุล หากคุณต้องการแยกไฟล์ MOL เหล่านี้จากเวิร์กบุ๊ก Excel โดยใช้ Aspose.Cells สำหรับ .NET คุณมาถูกที่แล้ว ในบทความนี้ เราจะแนะนำคุณทีละขั้นตอนเกี่ยวกับกระบวนการ และอธิบายแต่ละส่วนให้เข้าใจง่ายขึ้น
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มเขียนโค้ด คุณต้องแน่ใจว่าคุณมีทักษะและเครื่องมือที่จำเป็น นี่คือสิ่งที่คุณจะต้องมี:
1. ความเข้าใจพื้นฐานในการเขียนโปรแกรม .NET: คุณควรมีความคุ้นเคยกับ C# และ .NET framework
2. Aspose.Cells สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณมีไลบรารี Aspose.Cells คุณสามารถ [ดาวน์โหลดได้ที่นี่](https://releases-aspose.com/cells/net/).
3. IDE: คุณสามารถใช้ Visual Studio หรือ IDE อื่น ๆ ที่เข้ากันได้กับ .NET
4. เวิร์กบุ๊ก Excel พร้อมไฟล์ MOL ที่ฝังไว้: สำหรับบทช่วยสอนนี้ คุณต้องมีไฟล์ Excel ที่มีอ็อบเจ็กต์ MOL คุณสามารถสร้างไฟล์ของคุณเองหรือใช้ไฟล์ตัวอย่างใดก็ได้
## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณจะต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ของคุณ ซึ่งถือเป็นสิ่งสำคัญสำหรับการเข้าถึงฟังก์ชันการทำงานของ Aspose.Cells คุณสามารถทำได้ดังนี้:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

เนมสเปซเหล่านี้ช่วยให้คุณสามารถจัดการเวิร์กบุ๊ก เข้าถึงเวิร์กชีต และทำงานกับไฟล์โดยทั่วไปได้
ตอนนี้เราได้จัดการข้อกำหนดเบื้องต้นเรียบร้อยแล้ว เรามาเจาะลึกโค้ดและทำความเข้าใจแต่ละขั้นตอนที่เกี่ยวข้องกับการแยกไฟล์ MOL ที่ฝังไว้จากเวิร์กบุ๊ก Excel กัน 
## ขั้นตอนที่ 1: การตั้งค่าไดเร็กทอรีของคุณ
ขั้นตอนแรกคือการกำหนดว่าเอกสารต้นฉบับของคุณอยู่ที่ใดและคุณต้องการบันทึกไฟล์ MOL ที่แยกออกมาไว้ที่ใด มาตั้งค่าไดเรกทอรีเหล่านั้นกัน
```csharp
string SourceDir = "Your Document Directory"; // แทนที่ด้วยเส้นทางไดเร็กทอรีของคุณ
string outputDir = "Your Document Directory"; // แทนที่ด้วยเส้นทางเอาต์พุตของคุณ
```
ที่นี่คุณแทนที่ `"Your Document Directory"` โดยมีเส้นทางไปยังไดเร็กทอรีจริงของคุณ สิ่งสำคัญคือทั้งไดเร็กทอรีต้นทางและไดเร็กทอรีเอาต์พุตต้องสามารถเข้าถึงได้จากแอปพลิเคชันของคุณ
## ขั้นตอนที่ 2: การโหลดเวิร์กบุ๊ก
เมื่อคุณตั้งค่าไดเรกทอรีเรียบร้อยแล้ว ขั้นตอนต่อไปคือการโหลดเวิร์กบุ๊ก Excel มาเริ่มกันเลย

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

เรากำลังสร้างอินสแตนซ์ของ `Workbook` คลาสและส่งผ่านเส้นทางไปยังไฟล์ Excel ของเราที่ชื่อ `EmbeddedMolSample.xlsx`ขั้นตอนนี้จะเริ่มต้นเวิร์กบุ๊ก ทำให้คุณสามารถเข้าถึงเนื้อหาได้
## ขั้นตอนที่ 3: การวนซ้ำในเวิร์กชีต
เมื่อโหลดเวิร์กบุ๊กของคุณเสร็จแล้ว คุณต้องวนซ้ำผ่านเวิร์กชีตแต่ละแผ่นภายในเวิร์กบุ๊ก วิธีนี้ช่วยให้คุณตรวจสอบแต่ละชีตเพื่อหาอ็อบเจ็กต์ที่ฝังอยู่

```csharp
var index = 1; // ใช้ในการตั้งชื่อไฟล์ MOL ที่แยกออกมา
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // ตรรกะการสกัดเพิ่มเติมอยู่ที่นี่
}
```

ที่นี่คุณกำลังใช้ `foreach` วนซ้ำเพื่อนำทางผ่านเวิร์กชีต สำหรับแต่ละเวิร์กชีต คุณสามารถเข้าถึง `OleObjects` คอลเลกชันซึ่งประกอบด้วยวัตถุที่ฝังอยู่ทั้งหมด
## ขั้นตอนที่ 4: การแยกไฟล์ MOL
ตอนนี้มาถึงส่วนสำคัญแล้ว นั่นคือการแยกไฟล์ MOL ออกจากอ็อบเจ็กต์ OLE ซึ่งต้องมีการวนซ้ำอีกครั้งภายในลูปเวิร์กชีต

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

สำหรับแต่ละวัตถุ OLE ที่คุณพบ คุณกำลังสร้างไฟล์ใหม่ในไดเร็กทอรีเอาต์พุต `ObjectData` ทรัพย์สินของ `OleObject` เก็บข้อมูลของวัตถุที่ฝังไว้ซึ่งคุณเขียนลงในไฟล์ที่สร้างขึ้นใหม่โดยใช้ `FileStream`. ไฟล์มีการตั้งชื่อแบบต่อเนื่อง (`OleObject1.mol`- `OleObject2.mol`ฯลฯ) ตามหลัก `index` ตัวแปร.
## ขั้นตอนที่ 5: การยืนยันการเสร็จสิ้นกระบวนการ
ในที่สุด เมื่อแยกไฟล์ MOL ทั้งหมดแล้ว ทางที่ดีควรแจ้งให้ผู้ใช้ทราบว่ากระบวนการเสร็จสมบูรณ์แล้ว

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

บรรทัดนี้จะพิมพ์ข้อความไปยังคอนโซลเพื่อแจ้งให้คุณทราบว่าการแยกไฟล์สำเร็จแล้ว ถือเป็นการแสดงความคิดเห็นที่ดีจากผู้ใช้
## บทสรุป
และแล้วคุณก็ทำได้! คุณได้แยกไฟล์ MOL ที่ฝังไว้จากเวิร์กบุ๊ก Excel สำเร็จแล้วโดยใช้ Aspose.Cells สำหรับ .NET กระบวนการนี้ผสานรวมขั้นตอนหลักสองสามขั้นตอน เพื่อให้แน่ใจว่ามีแนวทางที่มีโครงสร้างในการจัดการวัตถุที่ฝังไว้ ไม่ว่าคุณจะอยู่ในงานวิจัยทางวิทยาศาสตร์ การวิเคราะห์ทางเคมี หรือเพียงแค่จัดการกับชุดข้อมูลที่ซับซ้อน การสามารถแยกและจัดการประเภทไฟล์เหล่านี้สามารถสร้างความแตกต่างอย่างมากในวิธีที่คุณจัดการข้อมูลของคุณ 
## คำถามที่พบบ่อย
### ฉันสามารถแยกประเภทไฟล์อื่นนอกจาก MOL ออกจาก Excel ได้หรือไม่?
ใช่ คุณสามารถแยกไฟล์ประเภทฝังตัวอื่นๆ ด้วยเทคนิคที่คล้ายกันได้
### การใช้ Aspose.Cells ฟรีหรือไม่?
Aspose.Cells เป็นไลบรารีเชิงพาณิชย์ แต่คุณสามารถ [ทดลองใช้ฟรีในระยะเวลาจำกัด](https://releases-aspose.com/).
### วิธีนี้ใช้ได้กับ Excel ทุกเวอร์ชันหรือไม่?
ใช่ ตราบใดที่รูปแบบไฟล์ได้รับการรองรับโดย Aspose.Cells
### ฉันสามารถทำให้กระบวนการสกัดนี้เป็นแบบอัตโนมัติได้หรือไม่
แน่นอน! คุณสามารถทำให้กระบวนการนี้เป็นแบบอัตโนมัติได้โดยการวางโค้ดไว้ในงานตามกำหนดเวลาหรือสคริปต์
### ฉันสามารถหาเอกสารเพิ่มเติมเกี่ยวกับ Aspose.Cells ได้จากที่ใด
คุณสามารถตรวจสอบได้ [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/net/) สำหรับรายละเอียดและตัวอย่างเพิ่มเติม

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}