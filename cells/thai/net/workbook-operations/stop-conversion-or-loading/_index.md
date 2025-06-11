---
"description": "เรียนรู้การหยุดการแปลงเวิร์กบุ๊กใน Aspose.Cells สำหรับ .NET โดยใช้ Interrupt Monitor พร้อมด้วยบทช่วยสอนทีละขั้นตอนโดยละเอียด"
"linktitle": "หยุดการแปลงหรือการโหลดโดยใช้ Interrupt Monitor"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "หยุดการแปลงหรือการโหลดโดยใช้ Interrupt Monitor"
"url": "/th/net/workbook-operations/stop-conversion-or-loading/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# หยุดการแปลงหรือการโหลดโดยใช้ Interrupt Monitor

## การแนะนำ
การทำงานกับไฟล์ Excel ขนาดใหญ่ มักเกี่ยวข้องกับกระบวนการที่ยาวนานซึ่งอาจกินเวลาและทรัพยากร แต่จะเกิดอะไรขึ้นหากคุณสามารถหยุดกระบวนการแปลงระหว่างทางเมื่อคุณรู้ว่ามีบางอย่างที่ต้องเปลี่ยนแปลง Aspose.Cells สำหรับ .NET มีคุณลักษณะที่เรียกว่า Interrupt Monitor ซึ่งช่วยให้คุณสามารถหยุดการแปลงสมุดงานเป็นรูปแบบอื่น เช่น PDF ได้ ซึ่งอาจช่วยชีวิตได้ โดยเฉพาะเมื่อทำงานกับไฟล์ข้อมูลขนาดใหญ่ ในคู่มือนี้ เราจะแนะนำวิธีหยุดกระบวนการแปลงโดยใช้ Interrupt Monitor ใน Aspose.Cells สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่จะดำน้ำ ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1. Aspose.Cells สำหรับ .NET - ดาวน์โหลด [ที่นี่](https://releases-aspose.com/cells/net/).
2. สภาพแวดล้อมการพัฒนา .NET เช่น Visual Studio
3. ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม C# - ความคุ้นเคยกับรูปแบบไวยากรณ์ C# จะช่วยให้คุณทำตามได้
## แพ็คเกจนำเข้า
ในการเริ่มต้น ให้เราทำการอิมพอร์ตแพ็คเกจที่จำเป็น ซึ่งได้แก่:
- Aspose.Cells: ไลบรารีหลักสำหรับจัดการไฟล์ Excel
- System.Threading: สำหรับการจัดการเธรด เนื่องจากตัวอย่างนี้จะรันกระบวนการคู่ขนานสองกระบวนการ
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
มาแบ่งกระบวนการออกเป็นขั้นตอนโดยละเอียด แต่ละขั้นตอนจะช่วยให้คุณเข้าใจถึงความสำคัญของการตั้งค่าและการใช้ Interrupt Monitor ในการจัดการการแปลงเวิร์กบุ๊ก Excel
## ขั้นตอนที่ 1: สร้างคลาสและตั้งค่าไดเร็กทอรีเอาท์พุต
ขั้นแรก เราต้องมีคลาสเพื่อรวมฟังก์ชันของเราไว้พร้อมกับไดเร็กทอรีที่จะบันทึกไฟล์เอาต์พุต
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงที่คุณต้องการบันทึกไฟล์ PDF
## ขั้นตอนที่ 2: สร้าง Interrupt Monitor ทันที
ขั้นตอนต่อไปคือสร้างอ็อบเจ็กต์ InterruptMonitor มอนิเตอร์นี้จะช่วยควบคุมกระบวนการโดยตั้งค่าความสามารถในการขัดจังหวะที่จุดใดก็ได้
```csharp
InterruptMonitor im = new InterruptMonitor();
```
ตัวตรวจสอบการขัดจังหวะนี้จะแนบมากับเวิร์กบุ๊กของเรา ซึ่งช่วยให้เราสามารถจัดการกระบวนการแปลงได้
## ขั้นตอนที่ 3: ตั้งค่าเวิร์กบุ๊กสำหรับการแปลง
ตอนนี้มาสร้างวัตถุเวิร์กบุ๊ก กำหนด InterruptMonitor ให้กับมัน แล้วเข้าถึงเวิร์กชีตแรกเพื่อแทรกข้อความตัวอย่าง
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
โค้ดด้านบนจะสร้างเวิร์กบุ๊ก ตั้งค่า InterruptMonitor ให้กับเวิร์กบุ๊ก และวางข้อความไว้ในเซลล์ที่อยู่ไกลออกไป (`J1000000`) การวางข้อความในตำแหน่งเซลล์นี้จะทำให้การประมวลผลเวิร์กบุ๊กใช้เวลานานขึ้น ทำให้ InterruptMonitor มีเวลาเพียงพอในการแทรกแซง
## ขั้นตอนที่ 4: บันทึกสมุดงานเป็น PDF และจัดการการขัดจังหวะ
ตอนนี้เรามาลองบันทึกสมุดงานเป็น PDF กัน เราจะใช้ `try-catch` บล็อคเพื่อจัดการกับการขัดจังหวะใดๆ ที่อาจเกิดขึ้น
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
หากกระบวนการถูกขัดจังหวะ ข้อยกเว้นจะตรวจจับและแสดงข้อความที่เหมาะสม มิฉะนั้น เวิร์กบุ๊กจะบันทึกเป็น PDF
## ขั้นตอนที่ 5: ขัดจังหวะกระบวนการแปลง
คุณสมบัติหลักที่นี่คือความสามารถในการขัดจังหวะกระบวนการ เราจะเพิ่มการหน่วงเวลาโดยใช้ `Thread.Sleep` แล้วโทรไปที่ `Interrupt()` วิธีการหยุดการแปลงหลังจาก 10 วินาที
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
การหน่วงเวลานี้จะทำให้เวิร์กบุ๊กมีเวลาเริ่มแปลงเป็น PDF ก่อนที่จะส่งสัญญาณขัดจังหวะ
## ขั้นตอนที่ 6: ดำเนินการเธรดพร้อมกัน
ในการรวบรวมทุกอย่างเข้าด้วยกัน เราจำเป็นต้องเริ่มทั้งสองฟังก์ชันในเธรดที่แยกจากกัน วิธีนี้จะทำให้การแปลงเวิร์กบุ๊กและการรอการขัดจังหวะเกิดขึ้นพร้อมกันได้
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
โค้ดด้านบนทำงาน `CreateWorkbookAndConvertItToPdfFormat` และ `WaitForWhileAndThenInterrupt` ในเธรดคู่ขนาน โดยรวมเข้าด้วยกันเมื่อทั้งสองกระบวนการเสร็จสิ้น
## ขั้นตอนที่ 7: การดำเนินการขั้นสุดท้าย
สุดท้ายนี้เราจะเพิ่ม `Run()` วิธีการในการดำเนินการรหัส
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
นี้ `Run` วิธีการดังกล่าวเป็นจุดเริ่มต้นและสังเกตการขัดจังหวะในการดำเนินการ
## บทสรุป
ในบทช่วยสอนนี้ เราได้ศึกษาวิธีการหยุดกระบวนการแปลงใน Aspose.Cells สำหรับ .NET Interrupt Monitor เป็นเครื่องมือที่มีประโยชน์เมื่อทำงานกับไฟล์ Excel ขนาดใหญ่ โดยช่วยให้คุณหยุดกระบวนการได้โดยไม่ต้องรอให้กระบวนการเสร็จสิ้น ซึ่งมีประโยชน์อย่างยิ่งในสถานการณ์ที่เวลาและทรัพยากรมีค่า และจำเป็นต้องมีข้อเสนอแนะอย่างรวดเร็ว
## คำถามที่พบบ่อย
### Interrupt Monitor ใน Aspose.Cells สำหรับ .NET คืออะไร  
Interrupt Monitor ช่วยให้คุณหยุดการแปลงเวิร์กบุ๊กหรือโหลดกระบวนการระหว่างทางได้
### ฉันสามารถใช้ Interrupt Monitor สำหรับรูปแบบอื่นนอกเหนือจาก PDF ได้หรือไม่  
ใช่ คุณสามารถหยุดการแปลงไปเป็นรูปแบบที่รองรับอื่นได้เช่นกัน
### Thread.Sleep() ส่งผลต่อเวลาการขัดจังหวะอย่างไร  
Thread.Sleep() สร้างการหน่วงเวลาไว้ก่อนจะทริกเกอร์การขัดจังหวะ เพื่อให้มีเวลาเพียงพอในการเริ่มต้นการแปลง
### ฉันสามารถขัดจังหวะกระบวนการก่อน 10 วินาทีได้ไหม  
ใช่ครับ แก้ไขการหน่วงเวลาครับ `WaitForWhileAndThenInterrupt()` เป็นเวลาสั้นลง
### กระบวนการขัดจังหวะจะมีผลกระทบต่อประสิทธิภาพการทำงานหรือไม่?  
ผลกระทบนั้นน้อยมากและเป็นประโยชน์อย่างยิ่งในการจัดการกระบวนการที่ดำเนินการในระยะยาว
สำหรับข้อมูลเพิ่มเติมโปรดดูที่ [เอกสาร Aspose.Cells สำหรับ .NET](https://reference.aspose.com/cells/net/)หากคุณต้องการความช่วยเหลือ โปรดดู [ฟอรั่มสนับสนุน](https://forum.aspose.com/c/cells/9) หรือรับ [ทดลองใช้งานฟรี](https://releases-aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}