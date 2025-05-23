---
"description": "เรียนรู้วิธีการอ่านสเปรดชีต Numbers และแปลงเป็น PDF โดยใช้ Aspose.Cells สำหรับ .NET ในบทช่วยสอนโดยละเอียดนี้"
"linktitle": "การอ่านสเปรดชีตตัวเลขโดยโปรแกรมใน .NET"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การอ่านสเปรดชีตตัวเลขโดยโปรแกรมใน .NET"
"url": "/th/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การอ่านสเปรดชีตตัวเลขโดยโปรแกรมใน .NET

## การแนะนำ
ในโลกดิจิทัลทุกวันนี้ การจัดการข้อมูลถือเป็นทักษะที่สำคัญ และสเปรดชีตถือเป็นส่วนสำคัญในการจัดระเบียบข้อมูล แต่จะเกิดอะไรขึ้นหากคุณต้องใช้สเปรดชีต Numbers ซึ่งเป็นไฟล์ที่สร้างโดยแอป Numbers ของ Apple โดยใช้ .NET ไม่ต้องกังวล คุณไม่ได้อยู่คนเดียว! ในบทช่วยสอนนี้ เราจะแนะนำขั้นตอนการอ่านสเปรดชีต Numbers ด้วยโปรแกรม Aspose.Cells สำหรับ .NET คุณจะได้เรียนรู้วิธีโหลดไฟล์ Numbers และแปลงเป็น PDF
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น มีบางสิ่งที่คุณต้องมี:
1. Aspose.Cells สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.Cells แล้ว คุณสามารถดาวน์โหลดได้ [ที่นี่](https://releases-aspose.com/cells/net/).
2. Visual Studio: ขอแนะนำให้ติดตั้ง Visual Studio (หรือ IDE อื่นๆ ที่เข้ากันได้กับ .NET) บนเครื่องของคุณ
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# เพียงเล็กน้อยจะช่วยให้คุณทำตามได้อย่างราบรื่น
4. ไดเร็กทอรีเอกสารของคุณ: คุณจะต้องมีไดเร็กทอรีที่เก็บไฟล์ Numbers พร้อมทั้งตำแหน่งสำหรับบันทึก PDF ที่แปลงแล้ว
เมื่อคุณครอบคลุมข้อกำหนดเบื้องต้นเหล่านี้แล้ว คุณก็พร้อมที่จะเริ่มต้นได้เลย!
## แพ็คเกจนำเข้า
ในการเริ่มต้น เราต้องนำเข้าแพ็คเกจที่จำเป็นเข้าสู่โปรเจ็กต์ C# ของเรา ซึ่งถือเป็นขั้นตอนที่สำคัญมาก เนื่องจากช่วยให้เราสามารถใช้ประโยชน์จากฟังก์ชันต่างๆ ที่ไลบรารี Aspose.Cells จัดเตรียมไว้ได้
1. เปิดโปรเจ็กต์ C# ของคุณใน Visual Studio
2. เพิ่มการอ้างอิงไปที่ไลบรารี Aspose.Cells:
   - หากคุณใช้ NuGet เพียงรันคำสั่งต่อไปนี้ในคอนโซลตัวจัดการแพ็คเกจ:
```
 Install-Package Aspose.Cells
 ```
3. นำเข้าเนมสเปซที่จำเป็นในโค้ดของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
ตอนนี้เราได้นำเข้าแพ็คเกจที่จำเป็นแล้ว มาดูคำแนะนำทีละขั้นตอนในการอ่านสเปรดชีต Numbers กัน
## ขั้นตอนที่ 1: ระบุไดเรกทอรีต้นทางและปลายทาง
ในขั้นตอนนี้ เราจะตั้งค่าไดเร็กทอรีที่ไฟล์ Numbers ต้นทางของคุณตั้งอยู่ และที่คุณต้องการบันทึกเอาต์พุต PDF
```csharp
// ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory"; // อัปเดตสิ่งนี้ไปยังไดเร็กทอรีจริงของคุณ
// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory"; // อัปเดตสิ่งนี้ไปยังไดเร็กทอรีจริงของคุณ
```
ที่นี่เราจะกำหนดตัวแปรสตริงสองตัว `sourceDir` และ `outputDir`เพื่อระบุตำแหน่งของไฟล์อินพุตและเอาต์พุต ตรวจสอบให้แน่ใจว่าได้แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงบนระบบของคุณ
## ขั้นตอนที่ 2: ตั้งค่าตัวเลือกการโหลดสำหรับรูปแบบตัวเลข
ต่อไปเราจะระบุตัวเลือกการโหลดสำหรับการอ่านสเปรดชีต Numbers ขั้นตอนนี้มีความสำคัญเนื่องจากจะแจ้งให้ Aspose ทราบว่าจะตีความไฟล์ Numbers อย่างไร
```csharp
// ระบุตัวเลือกการโหลด เราต้องการโหลดสเปรดชีต Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
เราสร้าง `LoadOptions` วัตถุและระบุรูปแบบเป็น `LoadFormat.Numbers`นี่จะบอกไลบรารี Aspose.Cells ว่าเรากำลังทำงานกับไฟล์ Numbers 
## ขั้นตอนที่ 3: โหลดสเปรดชีตตัวเลขลงในเวิร์กบุ๊ก
ตอนนี้ถึงเวลาโหลดสเปรดชีต Numbers จริงลงใน `Workbook` วัตถุ.
```csharp
// โหลดสเปรดชีต Numbers ลงในเวิร์กบุ๊กด้วยตัวเลือกการโหลดด้านบน
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
เราสร้างตัวอย่าง `Workbook` วัตถุและส่งเส้นทางไฟล์ของไฟล์ Numbers พร้อมกับตัวเลือกการโหลดของเรา ตรวจสอบให้แน่ใจว่าชื่อไฟล์ (`sampleNumbersByAppleInc.numbers`) ตรงกับชื่อจริงของไฟล์ Numbers ของคุณ
## ขั้นตอนที่ 4: บันทึกสมุดงานเป็น PDF
เมื่อโหลดไฟล์ Numbers สำเร็จแล้ว ขั้นตอนถัดไปคือการบันทึกในรูปแบบอื่น โดยเฉพาะ PDF
```csharp
// บันทึกสมุดงานเป็นรูปแบบ PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
ที่นี่เราเรียกว่า `Save` วิธีการบน `Workbook` วัตถุ โดยระบุเส้นทางไฟล์เอาท์พุตและรูปแบบที่เราต้องการบันทึก ในกรณีนี้ เราจะบันทึกเป็น PDF ให้แน่ใจว่าชื่อไฟล์เอาท์พุต (`outputNumbersByAppleInc.pdf`) เป็นแบบเฉพาะและจะไม่เขียนทับไฟล์ใดๆ ที่มีอยู่
## ขั้นตอนที่ 5: ยืนยันความสำเร็จ
สุดท้ายนี้ ให้เพิ่มข้อความเพื่อยืนยันว่าการดำเนินการของเราสำเร็จแล้ว
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
โค้ดบรรทัดนี้จะพิมพ์ข้อความแจ้งความสำเร็จไปยังคอนโซลเมื่อทุกอย่างเสร็จสิ้น การได้รับคำติชมถือเป็นเรื่องดีเสมอใช่หรือไม่
## บทสรุป
และแล้วคุณก็จะได้มัน! คุณได้อ่านสเปรดชีต Numbers และแปลงเป็น PDF โดยใช้ Aspose.Cells สำหรับ .NET สำเร็จแล้ว ไลบรารีอันทรงพลังนี้ช่วยให้คุณจัดการสเปรดชีตได้อย่างง่ายดาย ทำให้การจัดการข้อมูลของคุณเป็นเรื่องง่าย ไม่ว่าคุณจะกำลังพัฒนาแอปพลิเคชันหรือต้องการจัดการสเปรดชีตอย่างมีประสิทธิภาพมากขึ้น Aspose.Cells เป็นเครื่องมือที่ยอดเยี่ยมที่ควรมีไว้ในชุดเครื่องมือของคุณ
## คำถามที่พบบ่อย
### Aspose.Cells สามารถอ่านไฟล์ประเภทใดได้บ้าง?  
Aspose.Cells สามารถอ่านไฟล์รูปแบบต่างๆ รวมถึงไฟล์ XLS, XLSX, CSV และ Numbers 
### ฉันสามารถแก้ไขไฟล์ Numbers โดยใช้ Aspose.Cells ได้หรือไม่  
ใช่ คุณสามารถอ่าน จัดการ และบันทึกไฟล์ Numbers ด้วย Aspose.Cells ได้
### การใช้ Aspose.Cells ฟรีหรือไม่?  
Aspose.Cells เสนอให้ทดลองใช้งานฟรี แต่คุณจะต้องมีใบอนุญาตเพื่อใช้งานแบบขยายเวลา ตรวจสอบราคา [ที่นี่](https://purchase-aspose.com/buy).
### ฉันควรทำอย่างไรหากพบข้อผิดพลาดขณะโหลดไฟล์ Numbers?  
ตรวจสอบให้แน่ใจว่าคุณใช้ตัวเลือกการโหลดที่ถูกต้องและเส้นทางไฟล์ถูกต้อง หากต้องการความช่วยเหลือเพิ่มเติม โปรดไปที่ [ฟอรั่มสนับสนุน Aspose](https://forum-aspose.com/c/cells/9).
### ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ Aspose.Cells ได้อย่างไร  
คุณสามารถสมัครขอใบอนุญาตชั่วคราวได้ [ที่นี่](https://purchase-aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}