---
"description": "เรียนรู้การอ่านเวลาที่สร้างของความคิดเห็นแบบเธรดใน Excel โดยใช้ Aspose.Cells สำหรับ .NET คำแนะนำทีละขั้นตอนพร้อมตัวอย่างโค้ดรวมอยู่ด้วย"
"linktitle": "อ่านเวลาสร้างความคิดเห็นแบบเธรดในเวิร์กชีต"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "อ่านเวลาสร้างความคิดเห็นแบบเธรดในเวิร์กชีต"
"url": "/th/net/worksheet-operations/read-threaded-comment-created-time/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# อ่านเวลาสร้างความคิดเห็นแบบเธรดในเวิร์กชีต

## การแนะนำ
เมื่อทำงานกับไฟล์ Excel การจัดการความคิดเห็นอาจเป็นส่วนสำคัญของการทำงานร่วมกันและข้อเสนอแนะเกี่ยวกับข้อมูล หากคุณใช้ Aspose.Cells สำหรับ .NET คุณจะพบว่า Aspose.Cells มีประสิทธิภาพอย่างเหลือเชื่อในการจัดการฟังก์ชันต่างๆ ของ Excel รวมถึงความคิดเห็นแบบเธรด ในบทช่วยสอนนี้ เราจะเน้นที่วิธีการอ่านเวลาที่สร้างขึ้นของความคิดเห็นแบบเธรดในเวิร์กชีต ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น คู่มือนี้จะแนะนำคุณทีละขั้นตอนในกระบวนการ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกโค้ด เรามาตรวจสอบกันก่อนว่าคุณมีทุกสิ่งที่จำเป็นสำหรับการเริ่มต้น:
1. Aspose.Cells สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.Cells แล้ว คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/cells/net/).
2. Visual Studio: การติดตั้ง Visual Studio หรือ IDE .NET อื่นๆ ที่ใช้งานได้ซึ่งคุณสามารถเขียนและดำเนินการโค้ด C# ได้
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจชิ้นส่วนโค้ดได้ดีขึ้น
4. ไฟล์ Excel: เตรียมไฟล์ Excel พร้อมคำอธิบายแบบเธรด สำหรับตัวอย่างนี้ เราจะใช้ไฟล์ชื่อ `ThreadedCommentsSample-xlsx`.
ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นแล้ว เรามานำเข้าแพ็คเกจที่จำเป็นกัน
## แพ็คเกจนำเข้า
ในการเริ่มต้นใช้งาน Aspose.Cells คุณต้องนำเข้าเนมสเปซที่จำเป็น โดยดำเนินการดังนี้:
### นำเข้าเนมสเปซ Aspose.Cells
เปิดโครงการ C# ของคุณใน Visual Studio และเพิ่มคำสั่ง using directive ต่อไปนี้ที่ด้านบนของไฟล์โค้ดของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
เนมสเปซนี้ช่วยให้คุณสามารถเข้าถึงคลาสและวิธีการทั้งหมดที่ไลบรารี Aspose.Cells จัดทำไว้
ตอนนี้เราได้จัดเตรียมฉากเรียบร้อยแล้ว มาแยกขั้นตอนการอ่านเวลาที่สร้างความคิดเห็นแบบเธรดออกเป็นขั้นตอนที่จัดการได้
## ขั้นตอนที่ 1: กำหนดไดเรกทอรีแหล่งที่มา
ขั้นแรก คุณต้องระบุไดเรกทอรีที่ไฟล์ Excel ของคุณตั้งอยู่ ซึ่งเป็นสิ่งสำคัญ เนื่องจากโปรแกรมจำเป็นต้องทราบว่าจะต้องค้นหาไฟล์ดังกล่าวที่ใด
```csharp
// ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory";
```
แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงไปยังไฟล์ Excel ของคุณ นี่อาจเป็นอะไรทำนองนี้ `"C:\\Documents\\"`-
## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊ก
ขั้นต่อไป คุณจะโหลดเวิร์กบุ๊ก Excel ซึ่งประกอบด้วยข้อคิดเห็นแบบเธรด โดยทำดังนี้:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
บรรทัดโค้ดนี้จะสร้างสิ่งใหม่ `Workbook` วัตถุโดยโหลดไฟล์ Excel ที่ระบุ หากไม่พบไฟล์ ข้อยกเว้นจะเกิดขึ้น ดังนั้นโปรดตรวจสอบให้แน่ใจว่าเส้นทางถูกต้อง
## ขั้นตอนที่ 3: เข้าถึงแผ่นงาน
เมื่อโหลดเวิร์กบุ๊กแล้ว ขั้นตอนต่อไปคือการเข้าถึงเวิร์กชีตเฉพาะที่ประกอบด้วยข้อคิดเห็น ในกรณีของเรา เราจะเข้าถึงเวิร์กชีตแรก:
```csharp
// เข้าถึงแผ่นงานแรก
Worksheet worksheet = workbook.Worksheets[0];
```
บรรทัดนี้จะดึงเวิร์กชีตแรก (ดัชนี 0) จากเวิร์กบุ๊ก หากความคิดเห็นของคุณอยู่ในเวิร์กชีตอื่น ให้ปรับดัชนีให้เหมาะสม
## ขั้นตอนที่ 4: รับความคิดเห็นแบบเธรด
ตอนนี้ถึงเวลาที่จะดึงความคิดเห็นแบบเธรดจากเซลล์ที่ระบุ ในตัวอย่างนี้ เราจะได้รับความคิดเห็นจากเซลล์ A1:
```csharp
// รับความคิดเห็นแบบเธรด
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
บรรทัดนี้จะดึงความคิดเห็นแบบเธรดทั้งหมดที่เกี่ยวข้องกับเซลล์ A1 หากไม่มีความคิดเห็น คอลเล็กชันจะว่างเปล่า
## ขั้นตอนที่ 5: ทำซ้ำผ่านความคิดเห็น
เมื่อดึงความคิดเห็นแบบเธรดกลับมาแล้ว ตอนนี้เราสามารถวนซ้ำความคิดเห็นเหล่านั้นและแสดงรายละเอียด รวมถึงเวลาที่ถูกสร้างขึ้นได้:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
ลูปนี้จะผ่านความคิดเห็นแต่ละรายการใน `threadedComments` รวบรวมและพิมพ์ข้อความความคิดเห็น ชื่อผู้เขียน และเวลาที่สร้างความคิดเห็น
## ขั้นตอนที่ 6: ข้อความยืนยัน
ในที่สุด หลังจากดำเนินการตรรกะการอ่านความคิดเห็นแล้ว ควรใส่ข้อความยืนยันไว้เสมอ ซึ่งจะช่วยในการดีบักและช่วยให้มั่นใจว่าโค้ดทำงานสำเร็จ:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## บทสรุป
ขอแสดงความยินดี! คุณได้เรียนรู้วิธีการอ่านเวลาที่สร้างขึ้นของความคิดเห็นแบบเธรดในเวิร์กชีต Excel โดยใช้ Aspose.Cells สำหรับ .NET สำเร็จแล้ว ฟังก์ชันนี้มีประโยชน์อย่างยิ่งในการติดตามคำติชมและการทำงานร่วมกันในเอกสาร Excel ของคุณ ด้วยโค้ดเพียงไม่กี่บรรทัด คุณสามารถดึงข้อมูลอันมีค่าออกมาเพื่อปรับปรุงกระบวนการวิเคราะห์ข้อมูลและการรายงานของคุณได้
## คำถามที่พบบ่อย
### Aspose.Cells สำหรับ .NET คืออะไร?
Aspose.Cells สำหรับ .NET เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงไฟล์ Excel ในแอปพลิเคชัน .NET ได้
### ฉันจะดาวน์โหลด Aspose.Cells สำหรับ .NET ได้อย่างไร?
คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/cells/net/).
### มีการทดลองใช้ฟรีหรือไม่?
ใช่ คุณสามารถทดลองใช้ Aspose.Cells ได้ฟรีโดยเข้าไปที่ [หน้าทดลองใช้งานฟรี](https://releases-aspose.com/).
### ฉันสามารถเข้าถึงความคิดเห็นจากเซลล์อื่นได้หรือไม่
แน่นอน! คุณสามารถแก้ไขการอ้างอิงเซลล์ใน `GetThreadedComments` วิธีการเข้าถึงความคิดเห็นจากเซลล์ใดๆ
### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้จากที่ไหน
หากต้องการความช่วยเหลือ สามารถเข้าไปเยี่ยมชมได้ที่ [ฟอรั่ม Aspose](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}