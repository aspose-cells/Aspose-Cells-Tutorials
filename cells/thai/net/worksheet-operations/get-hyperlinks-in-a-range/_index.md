---
"description": "ดึงและจัดการไฮเปอร์ลิงก์จากไฟล์ Excel ได้อย่างง่ายดายด้วย Aspose.Cells สำหรับ .NET มีคำแนะนำทีละขั้นตอนและตัวอย่างโค้ดรวมอยู่ด้วย"
"linktitle": "รับไฮเปอร์ลิงก์ในช่วงใน .NET"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "รับไฮเปอร์ลิงก์ในช่วงใน .NET"
"url": "/th/net/worksheet-operations/get-hyperlinks-in-a-range/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# รับไฮเปอร์ลิงก์ในช่วงใน .NET

## การแนะนำ
คุณเคยพบว่าตัวเองจมอยู่กับสเปรดชีตจนแทบหมดแรงและสงสัยว่าจะดึงไฮเปอร์ลิงก์ออกมาอย่างมีประสิทธิภาพได้อย่างไรหรือไม่ หากเป็นเช่นนั้น คุณมาถูกที่แล้ว! ในคู่มือนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการดึงไฮเปอร์ลิงก์ในช่วงที่ระบุโดยใช้ Aspose.Cells สำหรับ .NET ไลบรารีอันทรงพลังนี้ช่วยให้คุณไม่ต้องทำงานที่น่าเบื่อกับไฟล์ Excel อีกต่อไป ทำให้คุณเรียกค้นและลบไฮเปอร์ลิงก์ได้อย่างง่ายดาย ดังนั้น จิบกาแฟสักถ้วยแล้วมาดำดิ่งสู่โลกของ Aspose.Cells กันเถอะ!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้นเขียนโค้ด เราจำเป็นต้องทราบข้อกำหนดเบื้องต้นบางประการ ไม่ต้องกังวล เพราะนี่ไม่ใช่รายการยาวๆ เลย!
### เตรียมสภาพแวดล้อมการพัฒนาของคุณให้พร้อม
1. .NET Framework: ตรวจสอบว่าคุณมีการตั้งค่าสภาพแวดล้อม .NET ที่เข้ากันได้บนเครื่องของคุณแล้ว อาจเป็น .NET Core หรือ .NET Framework แบบเต็ม ตรวจสอบให้แน่ใจว่าเวอร์ชันของคุณรองรับไลบรารี Aspose.Cells
2. ไลบรารี Aspose.Cells: คุณจะต้องมีไลบรารี Aspose.Cells คุณสามารถดาวน์โหลดเวอร์ชันล่าสุดได้จาก [ที่นี่](https://releases.aspose.com/cells/net/)หากคุณเพิ่งเริ่มต้น ให้พิจารณาใช้ [ทดลองใช้งานฟรี](https://releases.aspose.com/) เพื่อทดลองดู
3. IDE: สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) ที่ดี เช่น Visual Studio จะทำให้ชีวิตของคุณง่ายขึ้น ช่วยให้คุณเขียน แก้ไข และรันโค้ดได้อย่างราบรื่น
4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# เป็นประโยชน์ แต่ถ้าคุณเต็มใจที่จะเรียนรู้ คุณก็พร้อมแล้ว!
เมื่อเตรียมการเบื้องต้นเหล่านี้เรียบร้อยแล้ว เราก็พร้อมที่จะเริ่มใช้งานแล้ว มาดูการเขียนโค้ดพื้นฐานกัน—การนำเข้าแพ็กเกจที่จำเป็นและแบ่งตัวอย่างออกเป็นขั้นตอนต่างๆ
## แพ็คเกจนำเข้า
ขั้นตอนแรกในการเขียนโค้ดคือการนำเข้าแพ็คเกจที่จำเป็น คุณจะต้องเพิ่มการอ้างอิงไปยังไลบรารี Aspose.Cells ในโปรเจ็กต์ของคุณ ซึ่งโดยทั่วไปสามารถทำได้ผ่านตัวจัดการแพ็คเกจ NuGet วิธีดำเนินการมีดังนี้
1. เปิด Visual Studio
2. คลิกที่โครงการของคุณใน Solution Explorer
3. คลิกขวาและเลือกจัดการแพ็คเกจ NuGet
4. ค้นหา “Aspose.Cells” และติดตั้ง
```csharp
using System.IO;
using System;
using Aspose.Cells;
```
เมื่อมีไลบรารีแล้ว มาเข้าสู่โค้ดเพื่อแยกไฮเปอร์ลิงก์กันเถอะ!
## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไดเร็กทอรีของคุณ
เริ่มต้นด้วยการกำหนดเส้นทางของเอกสารของคุณ คุณต้องการตั้งค่าไดเร็กทอรีต้นทางที่ไฟล์ Excel ของคุณตั้งอยู่และไดเร็กทอรีเอาต์พุตที่จะบันทึกไฟล์ที่ประมวลผล
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string sourceDir = "Your Document Directory"; // เปลี่ยนสิ่งนี้เป็นเส้นทางของไฟล์ Excel ของคุณ
// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory"; // ตรวจสอบให้แน่ใจว่าวิธีการนี้ให้เส้นทางเอาต์พุตที่ถูกต้อง
```
ในสคริปท์นี้ ให้แทนที่ `"Your Document Directory"` โดยมีเส้นทางไปยังไดเร็กทอรีที่มีไฟล์ Excel อยู่ ซึ่งก็เหมือนกับการเตรียมฉากก่อนการแสดงของคุณ ดังนั้นการทราบว่าสื่อของคุณอยู่ที่ไหนจึงเป็นสิ่งสำคัญ
## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
ต่อไปเราจะสร้าง `Workbook` วัตถุเพื่อเปิดไฟล์ Excel ที่เรากำลังทำงานด้วย
```csharp
// สร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
// เปิดไฟล์ Excel
Workbook workbook = new Workbook(sourceDir + "HyperlinksSample.xlsx");
```
ที่นี่เราจะสร้างใหม่ `Workbook` ตัวอย่าง. `Workbook` คลาสเป็นช่องทางหลักในการเข้าสู่การดำเนินการทั้งหมดที่เกี่ยวข้องกับไฟล์ Excel คุณสามารถมองว่าคลาสเป็นการเปิดหนังสือที่มีเนื้อหาทั้งหมดของคุณ
## ขั้นตอนที่ 3: เข้าถึงแผ่นงาน
ตอนนี้เรามีเวิร์กบุ๊กพร้อมแล้ว เรามาเริ่มสร้างเวิร์กชีตแรกจากเวิร์กบุ๊กกันเลย ใน Excel เวิร์กชีตจะเหมือนกับหน้าในหนังสือ และเราต้องระบุว่าเราจะทำงานบนหน้าใด
```csharp
// รับแผ่นงานแรก (ค่าเริ่มต้น)
Worksheet worksheet = workbook.Worksheets[0];
```
โดยการเข้าถึง `Worksheets[0]`เรากำลังเลือกแผ่นงานแรก แผ่นงานจะถูกสร้างดัชนีโดยเริ่มจากศูนย์ ดังนั้นโปรดแน่ใจว่าคุณเลือกแผ่นงานที่ถูกต้อง
## ขั้นตอนที่ 4: สร้างช่วง
ตอนนี้ถึงเวลากำหนดช่วงที่เราต้องการค้นหาไฮเปอร์ลิงก์แล้ว ในกรณีของเรา สมมติว่าเราต้องการค้นหาในเซลล์ A2 ถึง B3
```csharp
// สร้างช่วง A2:B3
Range range = worksheet.Cells.CreateRange("A2", "B3");
```
โดยการโทร `CreateRange`เราระบุเซลล์เริ่มต้นและเซลล์สิ้นสุด นี่คือจุดที่ความมหัศจรรย์เกิดขึ้น เราจะตรวจสอบไฮเปอร์ลิงก์ที่อยู่ในช่วงที่ระบุในภายหลัง
## ขั้นตอนที่ 5: ดึงไฮเปอร์ลิงก์จากช่วง
ขั้นตอนนี้เป็นขั้นตอนที่เราสามารถเข้าถึงไฮเปอร์ลิงก์ในช่วงที่เรากำหนด
```csharp
// รับไฮเปอร์ลิงก์ในช่วง
Hyperlink[] hyperlinks = range.Hyperlinks;
```
การ `Hyperlinks` ทรัพย์สินของ `Range` วัตถุส่งคืนอาร์เรย์ของ `Hyperlink` วัตถุที่พบในช่วงนั้น เหมือนกับการหยิบบันทึกสำคัญทั้งหมดจากหน้าของคุณในครั้งเดียว!
## ขั้นตอนที่ 6: วนซ้ำและแสดงลิงก์
ตอนนี้เรามาลองทำซ้ำผ่านไฮเปอร์ลิงก์ที่ดึงมา เราจะพิมพ์ที่อยู่และพื้นที่ของไฮเปอร์ลิงก์เหล่านั้นในคอนโซลก่อน
```csharp
foreach (Hyperlink link in hyperlinks)
{
    Console.WriteLine(link.Area + " : " + link.Address);
}
```
ที่นี่ เราจะวนซ้ำแต่ละไฮเปอร์ลิงก์และแสดงพื้นที่และที่อยู่ของไฮเปอร์ลิงก์นั้นๆ ซึ่งก็เหมือนกับการอ่านรายละเอียดสำคัญของไฮเปอร์ลิงก์ที่คุณพบออกมาดังๆ 
## ขั้นตอนที่ 7: ทางเลือก - การลบไฮเปอร์ลิงก์
หากจำเป็น คุณสามารถลบไฮเปอร์ลิงก์ออกจากช่วงของคุณได้อย่างง่ายดาย! วิธีนี้มีประโยชน์มากหากคุณต้องการทำความสะอาดสเปรดชีตของคุณ
```csharp
foreach (Hyperlink link in hyperlinks)
{
    // หากต้องการลบลิงก์ ให้ใช้เมธอด Hyperlink.Delete()
    link.Delete();
}
```
การใช้ `Delete()` วิธีการบนไฮเปอร์ลิงก์แต่ละอันช่วยให้คุณลบไฮเปอร์ลิงก์ที่คุณอาจไม่ต้องการอีกต่อไปได้ เหมือนกับการลบข้อความที่ไม่จำเป็นออกจากหน้าของคุณ
## ขั้นตอนที่ 8: บันทึกการเปลี่ยนแปลงของคุณ
สุดท้ายเรามาบันทึกสมุดงานพร้อมการปรับแต่งทั้งหมดที่เราได้ทำกัน
```csharp
workbook.Save(outputDir + "HyperlinksSample_out.xlsx");
```
บรรทัดโค้ดนี้จะบันทึกเวิร์กบุ๊กที่คุณแก้ไขไปยังไดเรกทอรีเอาต์พุตที่ระบุ เป็นวิธีการเผยแพร่การเปลี่ยนแปลงที่คุณทำ เช่น การปิดหนังสือหลังจากแก้ไขครั้งสุดท้าย
## บทสรุป
และนี่คือคู่มือทีละขั้นตอนที่ครอบคลุมในการแยกไฮเปอร์ลิงก์จากช่วงที่ระบุในแผ่นงาน Excel โดยใช้ Aspose.Cells สำหรับ .NET! คุณได้เรียนรู้วิธีการตั้งค่าสภาพแวดล้อม เขียนโค้ด และดำเนินการกับไฮเปอร์ลิงก์ในเวิร์กบุ๊ก Excel แล้ว ไม่ว่าคุณจะจัดการข้อมูลสำหรับโครงการธุรกิจหรือส่วนตัว เครื่องมือนี้จะช่วยประหยัดเวลาให้คุณได้มากในระยะยาว
## คำถามที่พบบ่อย
### Aspose.Cells คืออะไร?
Aspose.Cells เป็นไลบรารี .NET สำหรับจัดการไฟล์ Excel โดยไม่ต้องติดตั้ง Microsoft Excel บนเครื่องของคุณ
### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?
ใช่ มีรุ่นทดลองใช้งานฟรีซึ่งช่วยให้คุณสำรวจคุณสมบัติต่างๆ ก่อนการซื้อ
### มีข้อจำกัดใด ๆ ในเวอร์ชันทดลองใช้หรือไม่?
การทดลองใช้อาจมีข้อจำกัดด้านการใช้งานบางประการ เช่น ลายน้ำบนไฟล์ที่บันทึก
### ฉันจำเป็นต้องรู้การเขียนโปรแกรมเพื่อใช้ Aspose.Cells หรือไม่?
แนะนำให้มีความรู้พื้นฐานด้านการเขียนโปรแกรมใน C# หรือ .NET เพื่อใช้งานไลบรารีได้อย่างมีประสิทธิภาพ
### ฉันจะได้รับการสนับสนุนได้อย่างไรหากฉันมีปัญหาเกี่ยวกับ Aspose.Cells?
คุณสามารถเข้าถึงฟอรั่มการสนับสนุนได้ [ที่นี่](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}