---
"date": "2025-04-05"
"description": "เรียนรู้วิธีการรวมแผ่นงาน Excel หลายแผ่นเป็นไฟล์ข้อความเดียวอย่างมีประสิทธิภาพโดยใช้ Aspose.Cells สำหรับ .NET คู่มือนี้ช่วยลดความซับซ้อนในการรวมข้อมูลและการรายงาน"
"title": "วิธีการรวมแผ่นงาน Excel เข้าเป็นไฟล์ข้อความเดียวโดยใช้ Aspose.Cells สำหรับ .NET"
"url": "/th/net/workbook-operations/combine-excel-sheets-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# วิธีการรวมแผ่นงาน Excel เข้าเป็นไฟล์ข้อความเดียวโดยใช้ Aspose.Cells สำหรับ .NET

## การแนะนำ

การจัดการข้อมูลในแผ่นงาน Excel หลายแผ่นอาจเป็นเรื่องยุ่งยาก โดยเฉพาะเมื่อคุณต้องรวมข้อมูลเหล่านั้นไว้ในไฟล์ข้อความเดียวเพื่อการวิเคราะห์หรือการรายงาน บทช่วยสอนนี้จะสาธิตวิธีใช้ **Aspose.Cells สำหรับ .NET** การโหลดเวิร์กบุ๊ก Excel แปลงเวิร์กชีตแต่ละแผ่นเป็นรูปแบบที่คั่นด้วยแท็บ และผสานเข้าเป็นไฟล์ข้อความที่ครอบคลุมไฟล์เดียว

ในคู่มือนี้คุณจะได้เรียนรู้:
- วิธีตั้งค่า Aspose.Cells ในสภาพแวดล้อม .NET ของคุณ
- โหลดเวิร์กบุ๊กจากไดเร็กทอรีได้อย่างง่ายดาย
- การกำหนดค่าตัวเลือกการบันทึกข้อความสำหรับการส่งออกข้อมูล
- การรวมเวิร์กชีตหลายแผ่นเข้าเป็นอาร์เรย์ไบต์เดียว
- บันทึกข้อมูลรวมกันเป็นไฟล์ข้อความรวม

มาสำรวจกันว่าคุณสามารถทำให้กระบวนการนี้ง่ายขึ้นได้อย่างไร!

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มต้น ให้แน่ใจว่าคุณมี:
- **ห้องสมุดเซลล์ Aspose**:แนะนำให้ใช้เวอร์ชัน 21.11 ขึ้นไปเพื่อประสิทธิภาพสูงสุด
- สภาพแวดล้อมการพัฒนาที่ตั้งค่าด้วย .NET Framework หรือ .NET Core
- ความรู้พื้นฐานในการเขียนโปรแกรม C#

## การตั้งค่า Aspose.Cells สำหรับ .NET

ขั้นแรก ติดตั้ง Aspose.Cells ในโครงการของคุณโดยใช้ **.NET CLI** หรือ **ตัวจัดการแพ็คเกจ**-

### การใช้ .NET CLI
```bash
dotnet add package Aspose.Cells
```

### การใช้ตัวจัดการแพ็คเกจ
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

#### การขอใบอนุญาต
Aspose.Cells เสนอใบอนุญาตทดลองใช้งานฟรีเพื่อทดสอบความสามารถทั้งหมด คุณสามารถขอรับใบอนุญาตชั่วคราวได้ [ที่นี่](https://purchase.aspose.com/temporary-license/) หรือซื้อใบอนุญาตเต็มรูปแบบหากจำเป็น

เมื่อติดตั้งแล้ว ให้เริ่มต้น Aspose.Cells โดยการรวมเนมสเปซต่อไปนี้ไว้ในไฟล์ C# ของคุณ:
```csharp
using Aspose.Cells;
```

## คู่มือการใช้งาน

มาแบ่งกระบวนการออกเป็นขั้นตอนต่างๆ เพื่อความชัดเจน

### โหลดสมุดงาน

#### ภาพรวม
โหลดเวิร์กบุ๊ก Excel จากไดเร็กทอรีที่ระบุ

#### ขั้นตอนการดำเนินการ
1. **ตั้งค่าไดเรกทอรีแหล่งที่มา**
   กำหนดเส้นทางที่ไฟล์ Excel ของคุณตั้งอยู่
   ```csharp
   string SourceDir = "YOUR_SOURCE_DIRECTORY";
   ```
2. **โหลดสมุดงาน**
   สร้างใหม่ `Workbook` วัตถุที่จะโหลดไฟล์ Excel ของคุณ
   ```csharp
   Workbook workbook = new Workbook(SourceDir + "/book1.xls");
   ```

### ตัวเลือกการบันทึกข้อความเริ่มต้น

#### ภาพรวม
กำหนดค่าวิธีการบันทึกแผ่นงานแต่ละแผ่นเป็นรูปแบบข้อความโดยใช้ค่าที่คั่นด้วยแท็บ (TSV)

#### ขั้นตอนการดำเนินการ
1. **สร้างตัวเลือก TxtSave**
   สร้างตัวอย่าง `TxtSaveOptions` เพื่อระบุตัวคั่น
   ```csharp
   TxtSaveOptions opts = new TxtSaveOptions();
   opts.Separator = '\t'; // ใช้แท็บเป็นตัวคั่นสำหรับรูปแบบ TSV
   ```

### แปลงและรวมแผ่นงานเป็นรูปแบบข้อความ

#### ภาพรวม
แปลงแผ่นงานแต่ละแผ่นเป็นรูปแบบข้อความและรวมเข้าเป็นอาร์เรย์ไบต์เดียว

#### ขั้นตอนการดำเนินการ
1. **เริ่มต้นไบต์อาร์เรย์**
   เตรียมอาร์เรย์ไบต์ว่างเพื่อเก็บข้อมูลรวมจากเวิร์กชีตทั้งหมด
   ```csharp
   byte[] workbookData = new byte[0];
   ```
2. **ทำซ้ำผ่านแผ่นงาน**
   วนซ้ำผ่านแต่ละเวิร์กชีต บันทึกเป็นข้อความ และรวมเอาต์พุต
   ```csharp
   for (int idx = 0; idx < workbook.Worksheets.Count; idx++) {
       workbook.Worksheets.ActiveSheetIndex = idx;
       
       using (MemoryStream ms = new MemoryStream()) {
           workbook.Save(ms, opts);
           
           ms.Position = 0;
           byte[] sheetData = ms.ToArray();
           
           byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
           Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
           Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
           
           workbookData = combinedArray;
       }
   }
   ```

### บันทึกข้อมูลสมุดงานรวมลงในไฟล์

#### ภาพรวม
บันทึกข้อมูลข้อความรวมจากเวิร์กชีตทั้งหมดลงในไฟล์เดียว

#### ขั้นตอนการดำเนินการ
1. **ตั้งค่าไดเรกทอรีเอาท์พุต**
   กำหนดว่าไฟล์ข้อความเอาต์พุตของคุณจะถูกบันทึกที่ไหน
   ```csharp
   string OutputDir = "YOUR_OUTPUT_DIRECTORY";
   ```
2. **เขียนลงไฟล์**
   ใช้ `File.WriteAllBytes` เพื่อบันทึกอาร์เรย์ไบต์เป็น `.txt` ไฟล์.
   ```csharp
   File.WriteAllBytes(OutputDir + "/out.txt", workbookData);
   ```

## การประยุกต์ใช้งานจริง

วิธีการนี้มีประโยชน์ในสถานการณ์เช่น:
1. **การรวมข้อมูล**:รวมข้อมูลจากรายงานต่างๆ ไว้ในเอกสารที่ครอบคลุมหนึ่งฉบับ
2. **การรายงานอัตโนมัติ**:สร้างไฟล์ข้อความรวมเพื่อการวิเคราะห์และการรายงานที่ง่ายขึ้น
3. **โครงการการย้ายถิ่นฐาน**:อำนวยความสะดวกในการโยกย้ายข้อมูล Excel ไปยังระบบอื่นๆ ที่ยอมรับการป้อนข้อความ
4. **เวิร์กโฟลว์การทำงานร่วมกัน**:ปรับปรุงการแชร์โดยการแปลงสเปรดชีตที่ซับซ้อนให้เป็นรูปแบบที่ง่ายกว่าและเข้าถึงได้ทั่วไป

## การพิจารณาประสิทธิภาพ

เพื่อให้แน่ใจว่าได้ประสิทธิภาพสูงสุดเมื่อใช้ Aspose.Cells:
- ลดการใช้หน่วยความจำให้เหลือน้อยที่สุดโดยประมวลผลเวิร์กชีตตามลำดับและปลดปล่อยทรัพยากรอย่างทันท่วงที
- ใช้โครงสร้างข้อมูลที่มีประสิทธิภาพ เช่น อาร์เรย์ไบต์สำหรับการดำเนินการภายในหน่วยความจำ
- สร้างโปรไฟล์แอปพลิเคชันของคุณเพื่อระบุคอขวดและเพิ่มประสิทธิภาพเส้นทางโค้ด

## บทสรุป

เราได้สาธิตวิธีการใช้ Aspose.Cells สำหรับ .NET เพื่อรวมแผ่นงาน Excel หลายแผ่นเข้าเป็นไฟล์ข้อความเดียวอย่างมีประสิทธิภาพ เทคนิคนี้ช่วยปรับปรุงเวิร์กโฟลว์การจัดการข้อมูล ทำให้วิเคราะห์และรายงานชุดข้อมูลขนาดใหญ่ได้ง่ายขึ้น

หากต้องการสำรวจเพิ่มเติม โปรดพิจารณาการรวมฟังก์ชันนี้เข้ากับระบบอื่นๆ หรือทำให้กระบวนการเป็นอัตโนมัติเป็นส่วนหนึ่งของไปป์ไลน์ ETL ที่ใหญ่กว่า

## ส่วนคำถามที่พบบ่อย

**คำถามที่ 1: ฉันสามารถใช้ Aspose.Cells สำหรับ .NET กับไฟล์ Excel ที่เก่ากว่า 2003 ได้หรือไม่**
A1: ใช่ Aspose.Cells รองรับรูปแบบต่างๆ มากมาย รวมถึง `-xls`.

**คำถามที่ 2: ข้อกำหนดของระบบสำหรับการใช้ Aspose.Cells บนเครื่องของฉันคืออะไร**
A2: คุณจะต้องมีการติดตั้ง .NET Framework หรือ .NET Core เวอร์ชันที่เข้ากันได้

**คำถามที่ 3: ฉันจะจัดการไฟล์ Excel ขนาดใหญ่ด้วยวิธีนี้ได้อย่างไร**
A3: ประมวลผลแผ่นงานแต่ละแผ่นแยกกันและจัดการหน่วยความจำอย่างระมัดระวังเพื่อหลีกเลี่ยงการใช้ทรัพยากรมากเกินไป

**คำถามที่ 4: มีข้อจำกัดเกี่ยวกับจำนวนเวิร์กชีตที่สามารถรวมกันได้หรือไม่**
A4: ไม่มีข้อจำกัดที่แน่นอน แต่ประสิทธิภาพอาจลดลงหากมีสมุดงานขนาดใหญ่หรือจำนวนแผ่นงานที่มากเกินไป

**คำถามที่ 5: สามารถปรับแต่งตัวคั่นใน TxtSaveOptions ได้หรือไม่**
A5: แน่นอน คุณสามารถตั้งค่าได้ `opts.Separator` เป็นอักขระใดๆ ก็ได้ตามที่คุณต้องการให้เหมาะกับกรณีการใช้งานของคุณ

## ทรัพยากร
สำหรับข้อมูลเพิ่มเติมและทรัพยากร:
- [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/net/)
- [ดาวน์โหลด Aspose.Cells](https://releases.aspose.com/cells/net/)
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ทดลองใช้งานฟรี](https://releases.aspose.com/cells/net/)
- [ใบสมัครใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มสนับสนุน](https://forum.aspose.com/c/cells/9)

ทดลองใช้เครื่องมือและเทคนิคเหล่านี้เพื่อเชี่ยวชาญการจัดการข้อมูล Excel ในแอปพลิเคชัน .NET!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}