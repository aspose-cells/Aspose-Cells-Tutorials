---
"description": "เรียนรู้วิธีการรับมิติของหน้าโดยใช้ Aspose.Cells สำหรับ .NET ในคู่มือทีละขั้นตอนนี้ เหมาะสำหรับนักพัฒนาที่ทำงานกับไฟล์ Excel"
"linktitle": "รับขนาดหน้า"
"second_title": "เอกสารอ้างอิง API Aspose.Cells สำหรับ .NET"
"title": "รับขนาดหน้า"
"url": "/th/net/excel-page-setup/get-page-dimensions/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# รับขนาดหน้า

## การแนะนำ

เมื่อพูดถึงการจัดการสเปรดชีตในแอปพลิเคชัน .NET ไลบรารี Aspose.Cells ถือเป็นเครื่องมือที่มีประสิทธิภาพที่ช่วยให้ผู้พัฒนาสามารถจัดการไฟล์ Excel ได้อย่างง่ายดาย แต่คุณจะรับขนาดหน้ากระดาษสำหรับกระดาษขนาดต่างๆ ได้อย่างไรด้วยไลบรารีอันทรงพลังนี้ ในบทช่วยสอนนี้ เราจะแนะนำขั้นตอนต่างๆ ทีละขั้นตอน เพื่อให้แน่ใจว่าคุณจะไม่เพียงแค่เข้าใจการทำงานของ Aspose.Cells เท่านั้น แต่ยังเชี่ยวชาญในการใช้ Aspose.Cells ในโปรเจ็กต์ของคุณอีกด้วย 

## ข้อกำหนดเบื้องต้น 

ก่อนที่เราจะเริ่มต้นเขียนโค้ด มีบางสิ่งที่คุณต้องมีเพื่อให้สามารถปฏิบัติตามได้อย่างมีประสิทธิภาพ:

### วิชวลสตูดิโอ
ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว นี่คือที่ที่คุณจะเขียนและดำเนินการโค้ด .NET

### ห้องสมุดเซลล์ Aspose
คุณจะต้องดาวน์โหลดและอ้างอิงไลบรารี Aspose.Cells ในโปรเจ็กต์ของคุณ คุณสามารถรับได้จาก:
- ลิงค์ดาวน์โหลด: [Aspose.Cells สำหรับ .NET](https://releases.aspose.com/cells/net/)

### ความรู้พื้นฐานเกี่ยวกับ C#
จะเป็นประโยชน์หากคุณมีความเข้าใจพื้นฐานเกี่ยวกับ C# บทช่วยสอนนี้จะใช้แนวคิดการเขียนโปรแกรมพื้นฐานที่ควรจะทำตามได้ง่าย

พร้อมแล้วหรือยัง? เริ่มกันเลย!

## การนำเข้าแพ็คเกจ

ขั้นตอนแรกในการเดินทางของเราคือการนำเข้าแพ็กเกจ Aspose.Cells ที่จำเป็นเข้าสู่โปรเจ็กต์ C# ของเรา คุณสามารถทำได้ดังนี้:

### สร้างโครงการใหม่

เปิด Visual Studio และสร้างโปรเจ็กต์ C# Console Application ใหม่ คุณสามารถตั้งชื่อได้ตามต้องการ มาเริ่มกันเลย `GetPageDimensions`-

### เพิ่มการอ้างอิง

ในการใช้ Aspose.Cells คุณจะต้องเพิ่มการอ้างอิงไปยังไลบรารี:
- คลิกขวาที่โครงการของคุณใน Solution Explorer
- เลือก “จัดการแพ็คเกจ NuGet”
- ค้นหา “Aspose.Cells” และติดตั้ง

### เพิ่มการใช้คำสั่ง

ที่ด้านบนของคุณ `Program.cs` ไฟล์ ให้แทรกสิ่งนี้โดยใช้คำสั่งเพื่อเข้าถึงฟังก์ชันการทำงานของ Aspose.Cells:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

ตอนนี้เราได้นำเข้าแพ็คเกจที่จำเป็นแล้ว คุณก็ไปได้สวยแล้ว! 

ตอนนี้เรามาดูวิธีการดึงขนาดกระดาษขนาดต่างๆ โดยดำเนินการตามแต่ละขั้นตอนกัน 

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ของคลาสเวิร์กบุ๊ก

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของคลาส Workbook จาก Aspose.Cells คลาสนี้แสดงถึงไฟล์ Excel

```csharp
Workbook book = new Workbook();
```

ที่นี่ เราเพียงสร้างเวิร์กบุ๊กใหม่ที่จะเก็บข้อมูลสเปรดชีตและการกำหนดค่าของเรา

## ขั้นตอนที่ 2: เข้าถึงแผ่นงานแรก

หลังจากสร้างอินสแตนซ์ของเวิร์กบุ๊กแล้ว คุณจะต้องการเข้าถึงเวิร์กชีตแรก เวิร์กบุ๊กแต่ละอันสามารถมีเวิร์กชีตได้หลายแผ่น แต่สำหรับการสาธิตนี้ เราจะยึดตามแผ่นแรก

```csharp
Worksheet sheet = book.Worksheets[0];
```

บรรทัดนี้จะดึงเวิร์กชีตแรก ซึ่งทำให้เราสามารถตั้งค่าขนาดกระดาษและดึงข้อมูลขนาดที่เกี่ยวข้องได้

## ขั้นตอนที่ 3: ตั้งค่าขนาดกระดาษเป็น A2 และดึงขนาดกลับมา

ตอนนี้ถึงเวลาตั้งค่าขนาดกระดาษและกำหนดขนาดแล้ว! เราเริ่มต้นด้วยขนาดกระดาษ A2

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

โค้ดนี้จะกำหนดขนาดกระดาษเป็น A2 และแสดงความกว้างและความสูงทันที จุดเด่นของ Aspose.Cells อยู่ที่ความเรียบง่าย!

## ขั้นตอนที่ 4: ทำซ้ำสำหรับขนาดกระดาษอื่นๆ

คุณอาจต้องการทำซ้ำขั้นตอนนี้สำหรับกระดาษขนาดอื่นๆ เช่น A3, A4 และ Letter โดยคุณสามารถทำได้ดังนี้:

สำหรับ A3:

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

สำหรับ A4:

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

สำหรับจดหมาย:

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

## ขั้นตอนที่ 5: สรุปผลลัพธ์

สุดท้ายนี้ คุณจะต้องยืนยันว่าการดำเนินการทั้งหมดเสร็จสมบูรณ์แล้ว คุณสามารถบันทึกสถานะนี้ลงในคอนโซลได้:

```csharp
Console.WriteLine("GetPageDimensions executed successfully.\r\n");
```

## บทสรุป

ขอแสดงความยินดี! ตอนนี้คุณได้เรียนรู้วิธีการดึงข้อมูลขนาดหน้ากระดาษสำหรับขนาดกระดาษต่างๆ โดยใช้ Aspose.Cells สำหรับ .NET สำเร็จแล้ว ไม่ว่าคุณจะกำลังพัฒนาเครื่องมือรายงาน สเปรดชีตอัตโนมัติ หรือฟังก์ชันการวิเคราะห์ข้อมูล การดึงข้อมูลขนาดหน้ากระดาษสำหรับรูปแบบต่างๆ ถือเป็นสิ่งที่มีค่าอย่างยิ่ง 

## คำถามที่พบบ่อย

### Aspose.Cells คืออะไร?
Aspose.Cells เป็นไลบรารี .NET ที่ใช้ในการสร้าง จัดการ และแปลงไฟล์ Excel โดยไม่ต้องใช้ Microsoft Excel

### ฉันจำเป็นต้องติดตั้ง Microsoft Excel เพื่อใช้ Aspose.Cells หรือไม่
ไม่ Aspose.Cells เป็นไลบรารีแบบสแตนด์อโลนและไม่จำเป็นต้องติดตั้ง Excel

### ฉันสามารถหาตัวอย่างเพิ่มเติมของ Aspose.Cells ได้ที่ไหน
คุณสามารถตรวจสอบเอกสารได้ที่นี่: [เอกสารประกอบ Aspose.Cells](https://reference-aspose.com/cells/net/).

### มี Aspose.Cells เวอร์ชันทดลองใช้งานฟรีหรือไม่
ใช่! คุณสามารถรับเวอร์ชันทดลองใช้งานฟรีได้จาก: [Aspose.Cells ทดลองใช้งานฟรี](https://releases-aspose.com/).

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้อย่างไร?
คุณสามารถรับความช่วยเหลือได้จากการเยี่ยมชมฟอรัมสนับสนุน Aspose: [การสนับสนุน Aspose.Cells](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}