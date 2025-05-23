---
"description": "เรียนรู้วิธีการจัดการกล่องข้อความใน Excel โดยใช้ Aspose.Cells สำหรับ .NET ด้วยบทช่วยสอนแบบทีละขั้นตอนที่ทำตามได้ง่ายนี้"
"linktitle": "การจัดการตัวควบคุม TextBox ใน Excel"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การจัดการตัวควบคุม TextBox ใน Excel"
"url": "/th/net/excel-shapes-controls/manipulate-textbox-controls-excel/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การจัดการตัวควบคุม TextBox ใน Excel

## การแนะนำ
หากคุณเคยทำงานกับ Excel คุณคงเคยพบกับกล่องข้อความเล็กๆ ที่ช่วยให้คุณสามารถเพิ่มข้อความลอยตัวลงในสเปรดชีตได้ แต่จะเป็นอย่างไรหากคุณจำเป็นต้องจัดการกล่องข้อความเหล่านี้ด้วยโปรแกรม? นั่นคือจุดที่ Aspose.Cells สำหรับ .NET มีประโยชน์ ด้วยโปรแกรมนี้ คุณสามารถเข้าถึงและแก้ไขกล่องข้อความได้อย่างง่ายดาย ทำให้เหมาะอย่างยิ่งสำหรับการทำงานอัตโนมัติหรือปรับแต่งรายงาน ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการจัดการกล่องข้อความใน Excel โดยใช้ Aspose.Cells สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกโค้ดจริง เรามาตรวจสอบให้แน่ใจก่อนว่าคุณได้ตั้งค่าทุกอย่างอย่างถูกต้องแล้ว:
1. Aspose.Cells สำหรับ .NET: คุณต้องดาวน์โหลดไลบรารี Aspose.Cells สำหรับ .NET คุณสามารถค้นหาลิงก์ดาวน์โหลด [ที่นี่](https://releases-aspose.com/cells/net/).
2. สภาพแวดล้อมการพัฒนา .NET: IDE ใด ๆ ที่รองรับ .NET เช่น Visual Studio ก็สามารถใช้งานได้
3. ความรู้พื้นฐานเกี่ยวกับ C#: บทช่วยสอนนี้ถือว่าคุณมีความคุ้นเคยกับไวยากรณ์ C# ขั้นพื้นฐานและโครงสร้างของเวิร์กบุ๊ก Excel
4. ไฟล์ Excel: ไฟล์ Excel ที่มีอยู่พร้อมกล่องข้อความ (เราจะใช้ `book1.xls` ในตัวอย่างนี้)
5. ใบอนุญาต Aspose: หากคุณไม่ได้ใช้เวอร์ชันทดลองใช้งานฟรี คุณจะต้อง [ซื้อ](https://purchase.aspose.com/buy) ใบอนุญาตหรือได้รับ [อันชั่วคราว](https://purchase-aspose.com/temporary-license/).
ตอนนี้เรามาดูขั้นตอนกันเลย!
## แพ็คเกจนำเข้า
ก่อนที่คุณจะจัดการเวิร์กบุ๊ก Excel และกล่องข้อความโดยใช้ Aspose.Cells คุณต้องนำเข้าเนมสเปซที่จำเป็น นี่คือตัวอย่างโค้ดที่คุณจะใช้ที่ด้านบนของไฟล์ C#:
```csharp
using System.IO;
using Aspose.Cells;
```
แพ็คเกจเหล่านี้ทำให้คุณสามารถเข้าถึงการจัดการเวิร์กบุ๊ก การเข้าถึงเวิร์กชีต และวัตถุการวาด (เช่น กล่องข้อความ)
ตอนนี้เราได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว มาแบ่งกระบวนการจัดการกล่องข้อความออกเป็นขั้นตอนที่ทำตามได้ง่ายกัน
## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีสมุดงานของคุณ
ขั้นตอนแรกคือการระบุว่าไฟล์ Excel ของคุณอยู่ที่ใดในระบบของคุณ คุณจะต้องแทนที่ตัวแทน `Your Document Directory` ด้วยเส้นทางจริงไปยังไฟล์ของคุณ เส้นทางนี้จะถูกเก็บไว้ใน `dataDir` ตัวแปรเพื่อให้อ้างอิงได้ง่ายตลอดทั้งโค้ด
```csharp
string dataDir = "Your Document Directory";
```
สิ่งนี้จะช่วยให้โปรแกรมของคุณทราบว่าจะค้นหาไฟล์ Excel อินพุตได้ที่ใด (`book1.xls`) และจะบันทึกไฟล์เอาท์พุตไว้ที่ไหน
## ขั้นตอนที่ 2: เปิดไฟล์ Excel
ขั้นตอนต่อไป คุณจะต้องโหลดไฟล์ Excel ที่มีอยู่ลงในอ็อบเจ็กต์ Aspose.Cells Workbook เวิร์กบุ๊กนี้ทำหน้าที่เป็นคอนเทนเนอร์สำหรับข้อมูล Excel ของคุณ ทำให้คุณสามารถเข้าถึงเวิร์กชีตและอ็อบเจ็กต์รูปวาดใดๆ (เช่น กล่องข้อความ) ได้
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
การ `Workbook` คลาสจาก Aspose.Cells จะโหลดไฟล์ Excel ที่ระบุจากไดเร็กทอรีของคุณ หากไฟล์ไม่มีอยู่ในไดเร็กทอรีที่ระบุ ระบบจะแสดงข้อยกเว้น ดังนั้นโปรดตรวจสอบให้แน่ใจว่าเส้นทางถูกต้อง
## ขั้นตอนที่ 3: เข้าถึงแผ่นงานแรก
ตอนนี้คุณได้โหลดเวิร์กบุ๊กแล้ว คุณสามารถเข้าถึงเวิร์กชีตของเวิร์กบุ๊กได้ ในตัวอย่างนี้ เราจะเข้าถึงเวิร์กชีตแรกในเวิร์กบุ๊ก ซึ่งจัดเก็บอยู่ที่ดัชนี 0
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
การ `Worksheets` คุณสมบัตินี้ช่วยให้คุณเข้าถึงแผ่นงานทั้งหมดในเวิร์กบุ๊กได้ ที่นี่ เราจะสนใจเฉพาะแผ่นงานแรกเท่านั้น แต่คุณสามารถทำงานกับแผ่นงานใดๆ ก็ได้โดยระบุดัชนีที่ถูกต้อง
## ขั้นตอนที่ 4: รับวัตถุ TextBox แรก
กล่องข้อความในแผ่นงาน Excel ถือเป็นวัตถุรูปวาด คลาส Aspose.Cells.Drawing.TextBox มีคุณสมบัติและวิธีการในการจัดการวัตถุเหล่านี้ หากต้องการเข้าถึงกล่องข้อความแรกบนเวิร์กชีต คุณเพียงแค่อ้างอิงถึง `TextBoxes` การรวบรวมตามดัชนี
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
การดำเนินการนี้จะดึงวัตถุกล่องข้อความแรกจาก `TextBoxes` คอลเลกชัน หากเวิร์กชีตของคุณไม่มีกล่องข้อความที่ดัชนีนั้น ระบบจะแสดงข้อยกเว้น ดังนั้น โปรดตรวจสอบให้แน่ใจว่าดัชนีนั้นถูกต้องเสมอ
## ขั้นตอนที่ 5: ดึงข้อความจาก TextBox แรก
หลังจากเข้าถึงกล่องข้อความแล้ว คุณสามารถแยกข้อความที่มีอยู่โดยใช้ `.Text` คุณสมบัติ.
```csharp
string text0 = textbox0.Text;
```
นี่จะจับข้อความจากกล่องข้อความแรกลงใน `text0` สตริง ตอนนี้คุณสามารถแสดง จัดการ หรือประมวลผลสตริงนั้นในแอปพลิเคชันของคุณได้
## ขั้นตอนที่ 6: เข้าถึงวัตถุ TextBox ที่สอง
ในการจัดการกล่องข้อความหลายกล่อง เราสามารถดึงกล่องข้อความเพิ่มเติมจากเวิร์กชีตได้ ที่นี่ เราจะเข้าถึงกล่องข้อความที่สองในลักษณะเดียวกับกล่องข้อความแรก:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
อีกครั้งเราเข้าถึงกล่องข้อความที่สองโดยใช้ดัชนี 1 จาก `TextBoxes` ของสะสม.
## ขั้นตอนที่ 7: ดึงข้อความจาก TextBox ที่สอง
เช่นเดียวกับกล่องข้อความแรก คุณสามารถดึงข้อความจากกล่องข้อความที่สองและจัดเก็บไว้ในสตริงได้:
```csharp
string text1 = textbox1.Text;
```
การกระทำนี้จะจับข้อความปัจจุบันจากกล่องข้อความที่สอง
## ขั้นตอนที่ 8: แก้ไขข้อความในกล่องข้อความที่สอง
ตอนนี้ สมมติว่าคุณต้องการแก้ไขข้อความภายในกล่องข้อความที่สอง คุณสามารถทำได้ง่ายๆ โดยกำหนดสตริงใหม่ให้กับ `.Text` คุณสมบัติของวัตถุกล่องข้อความ
```csharp
textbox1.Text = "This is an alternative text";
```
การดำเนินการนี้จะเปลี่ยนข้อความภายในกล่องข้อความที่สองเป็นเนื้อหาใหม่ คุณสามารถแทรกข้อความใดๆ ก็ได้ที่นี่ตามความต้องการของคุณ
## ขั้นตอนที่ 9: บันทึกไฟล์ Excel ที่อัปเดต
ในที่สุด หลังจากปรับเปลี่ยนกล่องข้อความแล้ว ก็ถึงเวลาบันทึกการเปลี่ยนแปลงของคุณ Aspose.Cells ช่วยให้คุณบันทึกเวิร์กบุ๊กที่ปรับเปลี่ยนโดยใช้ `.Save()` วิธีการ คุณสามารถระบุชื่อไฟล์ใหม่หรือเขียนทับไฟล์ที่มีอยู่ได้
```csharp
workbook.Save(dataDir + "output.out.xls");
```
การดำเนินการนี้จะบันทึกไฟล์ Excel ที่แก้ไขแล้วไปยังเส้นทางเอาต์พุตที่คุณกำหนดไว้ จากนั้น เมื่อคุณเปิดไฟล์ Excel คุณจะเห็นการเปลี่ยนแปลงที่คุณทำกับกล่องข้อความ
## บทสรุป
และแล้วคุณก็ได้เรียนรู้วิธีจัดการกล่องข้อความใน Excel โดยใช้ Aspose.Cells สำหรับ .NET แล้ว ไม่ว่าคุณจะกำลังสร้างรายงานอัตโนมัติ ปรับแต่งแผ่นงาน Excel หรือสร้างเนื้อหาแบบไดนามิก Aspose.Cells จะทำให้การควบคุมทุกแง่มุมของไฟล์ Excel ของคุณทำได้ง่ายด้วยโปรแกรม ตั้งแต่การแยกและแก้ไขข้อความไปจนถึงการบันทึกไฟล์ที่อัปเดต ไลบรารีนี้เป็นเครื่องมืออันทรงพลังสำหรับนักพัฒนาที่ทำงานกับ Excel ในสภาพแวดล้อม .NET
## คำถามที่พบบ่อย
### ฉันสามารถจัดการวัตถุรูปวาดอื่น ๆ ด้วย Aspose.Cells นอกเหนือจากกล่องข้อความได้หรือไม่
ใช่ Aspose.Cells ช่วยให้คุณสามารถจัดการวัตถุวาดรูปอื่นๆ เช่น รูปร่าง แผนภูมิ และรูปภาพได้
### จะเกิดอะไรขึ้นหากฉันพยายามเข้าถึงกล่องข้อความที่ไม่มีอยู่?
หากดัชนีของกล่องข้อความอยู่นอกช่วง `IndexOutOfRangeException` จะถูกโยนออกไป
### ฉันสามารถเพิ่มกล่องข้อความใหม่ลงในเวิร์กชีต Excel ด้วย Aspose.Cells ได้หรือไม่
ใช่ Aspose.Cells ช่วยให้คุณสามารถเพิ่มกล่องข้อความใหม่โดยใช้ `AddTextBox` วิธี.
### ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.Cells หรือไม่?
ใช่ คุณจะต้องซื้อใบอนุญาต แต่ Aspose ยังเสนอ [ทดลองใช้งานฟรี](https://releases-aspose.com/).
### ฉันสามารถใช้ Aspose.Cells กับภาษาการเขียนโปรแกรมอื่นนอกเหนือจาก C# ได้หรือไม่
ใช่ Aspose.Cells สามารถใช้ร่วมกับภาษาใดๆ ที่รองรับ .NET เช่น VB.NET ได้

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}