---
"description": "ค้นพบคำแนะนำทีละขั้นตอนในการลบการตั้งค่าเครื่องพิมพ์ออกจากเวิร์กชีต Excel โดยใช้ Aspose.Cells สำหรับ .NET เพื่อปรับปรุงคุณภาพการพิมพ์เอกสารของคุณได้อย่างง่ายดาย"
"linktitle": "ลบการตั้งค่าเครื่องพิมพ์ที่มีอยู่ของเวิร์กชีต"
"second_title": "เอกสารอ้างอิง API Aspose.Cells สำหรับ .NET"
"title": "ลบการตั้งค่าเครื่องพิมพ์ที่มีอยู่ของเวิร์กชีต"
"url": "/th/net/excel-page-setup/remove-existing-printer-settings-of-worksheets/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ลบการตั้งค่าเครื่องพิมพ์ที่มีอยู่ของเวิร์กชีต

## การแนะนำ

ไม่ว่าคุณจะกำลังพัฒนาแอปพลิเคชันที่จัดการไฟล์ Excel หรือเพียงแค่ปรับแต่งเพื่อใช้งานส่วนตัว การทำความเข้าใจเกี่ยวกับการจัดการการตั้งค่าเวิร์กชีตถือเป็นสิ่งสำคัญ เพราะเหตุใดจึงเป็นเช่นนั้น เนื่องจากการกำหนดค่าเครื่องพิมพ์ที่ไม่ถูกต้องอาจส่งผลต่อการพิมพ์รายงานที่ดีหรือการพิมพ์ผิดที่เลอะเทอะ นอกจากนี้ ในยุคที่มีการจัดการเอกสารแบบไดนามิก การสามารถลบการตั้งค่าเหล่านี้ได้อย่างง่ายดายจะช่วยประหยัดเวลาและทรัพยากรของคุณได้

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลบการตั้งค่าเครื่องพิมพ์ที่น่ารำคาญเหล่านี้ คุณต้องมีบางสิ่งที่จำเป็น นี่คือรายการตรวจสอบด่วนเพื่อให้แน่ใจว่าคุณพร้อมแล้ว:

1. ติดตั้ง Visual Studio: จำเป็นต้องมีสภาพแวดล้อมการพัฒนาเพื่อเขียนและดำเนินการโค้ด .NET ของคุณ หากคุณยังไม่มี ให้ไปที่เว็บไซต์ของ Visual Studio และดาวน์โหลดเวอร์ชันล่าสุด
2. Aspose.Cells สำหรับ .NET: คุณจะต้องมีไลบรารีนี้ในโปรเจ็กต์ของคุณ คุณสามารถดาวน์โหลดได้จาก [หน้าวางจำหน่าย Aspose](https://releases-aspose.com/cells/net/).
3. ไฟล์ Excel ตัวอย่าง: สำหรับการแนะนำการใช้งานนี้ คุณจะต้องมีไฟล์ Excel ตัวอย่างที่มีการตั้งค่าเครื่องพิมพ์ คุณสามารถสร้างไฟล์ดังกล่าวได้ หรือใช้ไฟล์สาธิตที่ Aspose จัดเตรียมไว้ให้

ตอนนี้เรามีทุกอย่างที่ต้องการแล้ว มาเริ่มเขียนโค้ดกันเลย!

## แพ็คเกจนำเข้า

ในการเริ่มต้น เราจำเป็นต้องนำเข้าเนมสเปซที่จำเป็นในโครงการ .NET ของเรา โดยทำดังนี้:

### เปิดโครงการของคุณ

เปิดโครงการ Visual Studio ที่มีอยู่ของคุณหรือสร้างโครงการแอปพลิเคชันคอนโซลใหม่

### เพิ่มการอ้างอิง

ในโครงการของคุณไปที่ `References`คลิกขวาและเลือก `Add Reference...`ค้นหาไลบรารี Aspose.Cells และเพิ่มลงในโปรเจ็กต์ของคุณ

### นำเข้าเนมสเปซที่จำเป็น

ที่ด้านบนสุดของไฟล์โค้ดของคุณ ให้รวมเนมสเปซเหล่านี้:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

เนมสเปซเหล่านี้ให้สิทธิ์การเข้าถึงฟังก์ชันการทำงานที่เราต้องการในการจัดการไฟล์ Excel ด้วย Aspose.Cells

ตอนนี้เรามาดูขั้นตอนในการลบการตั้งค่าเครื่องพิมพ์ออกจากเวิร์กชีต Excel ออกเป็นขั้นตอนที่สามารถจัดการได้

## ขั้นตอนที่ 1: กำหนดไดเรกทอรีแหล่งที่มาและเอาต์พุตของคุณ

ในการเริ่มต้น คุณต้องระบุว่าไฟล์ Excel ต้นฉบับของคุณอยู่ที่ใด และคุณต้องการบันทึกไฟล์ที่แก้ไขไว้ที่ใด

```csharp
//ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory";
//ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory";
```

ที่นี่คุณจะแทนที่ `"Your Document Directory"` และ `"Your Document Directory"` พร้อมเส้นทางจริงที่จัดเก็บไฟล์ของคุณ

## ขั้นตอนที่ 2: โหลดไฟล์ Excel

ขั้นตอนต่อไปคือเราต้องโหลดเวิร์กบุ๊ก (ไฟล์ Excel) เพื่อประมวลผล ซึ่งทำได้ด้วยโค้ดเพียงบรรทัดเดียว

```csharp
//โหลดไฟล์ Excel ต้นฉบับ
Workbook wb = new Workbook(sourceDir + "sampleRemoveExistingPrinterSettingsOfWorksheets.xlsx");
```

บรรทัดนี้จะเปิดไฟล์ Excel และเตรียมพร้อมสำหรับการปรับเปลี่ยน

## ขั้นตอนที่ 3: รับจำนวนแผ่นงาน

ตอนนี้เรามีสมุดงานแล้ว มาดูกันว่าภายในมีแผ่นงานกี่แผ่น:

```csharp
//รับจำนวนแผ่นงานของสมุดงาน
int sheetCount = wb.Worksheets.Count;
```

สิ่งนี้จะช่วยให้เราดำเนินการซ้ำผ่านเวิร์กชีตแต่ละแผ่นได้อย่างมีประสิทธิภาพ

## ขั้นตอนที่ 4: ทำซ้ำในแต่ละเวิร์กชีต

เมื่อนับแผ่นงานเสร็จแล้ว ก็ถึงเวลาที่จะวนซ้ำผ่านแผ่นงานแต่ละแผ่นในสมุดงาน คุณจะต้องตรวจสอบแต่ละแผ่นว่ามีการตั้งค่าเครื่องพิมพ์ที่มีอยู่หรือไม่

```csharp
for (int i = 0; i < sheetCount; i++)
{
    //เข้าถึงแผ่นงานที่ i
    Worksheet ws = wb.Worksheets[i];
```

ในลูปนี้ เราจะเข้าถึงเวิร์กชีตแต่ละรายการทีละรายการ

## ขั้นตอนที่ 5: เข้าถึงและตรวจสอบการตั้งค่าเครื่องพิมพ์

ต่อไปเราจะเจาะลึกรายละเอียดของแต่ละเวิร์กชีตเพื่อเข้าถึงการตั้งค่าหน้าและตรวจสอบการตั้งค่าเครื่องพิมพ์

```csharp
//การตั้งค่าหน้าเวิร์กชีตการเข้าถึง
PageSetup ps = ws.PageSetup;
//ตรวจสอบว่ามีการตั้งค่าเครื่องพิมพ์สำหรับเวิร์กชีตนี้หรือไม่
if (ps.PrinterSettings != null)
{
    //พิมพ์ข้อความต่อไปนี้
    Console.WriteLine("PrinterSettings of this worksheet exist.");
    //พิมพ์ชื่อแผ่นงานและขนาดกระดาษ
    Console.WriteLine("Sheet Name: " + ws.Name);
    Console.WriteLine("Paper Size: " + ps.PaperSize);
```

ที่นี่ถ้าหากว่า `PrinterSettings` พบแล้ว เราจะให้ข้อเสนอแนะผ่านคอนโซลพร้อมรายละเอียดชื่อแผ่นงานและขนาดกระดาษ

## ขั้นตอนที่ 6: ลบการตั้งค่าเครื่องพิมพ์

นี่เป็นช่วงเวลาสำคัญ! ตอนนี้เราจะลบการตั้งค่าเครื่องพิมพ์โดยตั้งค่าเป็นค่าว่าง:

```csharp
    //ลบการตั้งค่าเครื่องพิมพ์โดยตั้งค่าเป็นค่าว่าง
    ps.PrinterSettings = null;
    Console.WriteLine("Printer settings of this worksheet are now removed by setting it null.");
    Console.WriteLine("");
}
```

ในตัวอย่างนี้ เราจะล้างการตั้งค่าเครื่องพิมพ์อย่างมีประสิทธิภาพ ทำให้ทุกอย่างเป็นระเบียบเรียบร้อย

## ขั้นตอนที่ 7: บันทึกสมุดงาน

หลังจากประมวลผลเวิร์กชีตของคุณทั้งหมดแล้ว สิ่งสำคัญคือการบันทึกเวิร์กบุ๊กของคุณเพื่อรักษาการเปลี่ยนแปลงที่คุณได้ทำไว้

```csharp
//บันทึกสมุดงาน
wb.Save(outputDir + "outputRemoveExistingPrinterSettingsOfWorksheets.xlsx");
```

และเพียงแค่นั้น ไฟล์ใหม่ของคุณที่ไม่มีการตั้งค่าเครื่องพิมพ์แบบเดิมก็จะถูกเก็บไว้ในไดเร็กทอรีเอาต์พุตที่ระบุ!

## บทสรุป

และแล้วคุณก็พบมัน! คุณได้นำทางอย่างประสบความสำเร็จในการลบการตั้งค่าเครื่องพิมพ์ออกจากเวิร์กชีต Excel โดยใช้ Aspose.Cells สำหรับ .NET เป็นเรื่องน่าทึ่งมากที่โค้ดเพียงไม่กี่บรรทัดสามารถจัดระเบียบเอกสารของคุณและทำให้กระบวนการพิมพ์ของคุณราบรื่นขึ้นมากใช่หรือไม่ โปรดจำไว้ว่าด้วยพลังอันยิ่งใหญ่ (เช่น Aspose.Cells) ก็มาพร้อมกับความรับผิดชอบที่ยิ่งใหญ่ ดังนั้นควรทดสอบโค้ดของคุณเสมอ ก่อนที่จะนำไปใช้ในสภาพแวดล้อมการผลิต

## คำถามที่พบบ่อย

### Aspose.Cells คืออะไร?  
Aspose.Cells เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงไฟล์ Excel ในแอปพลิเคชัน .NET ได้

### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?  
ใช่ Aspose นำเสนอเวอร์ชันทดลองใช้งานฟรีที่คุณสามารถใช้สำรวจฟีเจอร์ต่างๆ ได้ ลองดู [ลิงค์ทดลองใช้ฟรี](https://releases-aspose.com/).

### ฉันจำเป็นต้องติดตั้ง Microsoft Excel เพื่อใช้ Aspose.Cells หรือไม่  
ไม่ Aspose.Cells ทำงานแยกจาก Microsoft Excel คุณไม่จำเป็นต้องติดตั้ง Excel บนเครื่องของคุณ

### ฉันจะได้รับการสนับสนุนได้อย่างไรหากประสบปัญหา?  
คุณสามารถเยี่ยมชม [ฟอรั่ม Aspose](https://forum.aspose.com/c/cells/9) สำหรับการสนับสนุนและทรัพยากรชุมชน

### มีใบอนุญาตชั่วคราวให้ใช้หรือไม่?  
แน่นอน! คุณสามารถสมัครได้ [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) เพื่อเข้าถึงคุณสมบัติทั้งหมดได้โดยไม่มีข้อจำกัดในระยะเวลาจำกัด

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}