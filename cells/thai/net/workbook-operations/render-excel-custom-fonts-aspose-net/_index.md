---
"date": "2025-04-05"
"description": "เรียนรู้วิธีการเรนเดอร์ไฟล์ Excel เป็นรูปแบบ PNG, TIFF และ PDF โดยใช้แบบอักษรที่กำหนดเองด้วย Aspose.Cells สำหรับ .NET รับรองว่ารูปแบบตัวอักษรจะสอดคล้องกันในทุกการแปลงเอกสาร"
"title": "เรนเดอร์ Excel เป็น PNG, TIFF, PDF ด้วยแบบอักษรที่กำหนดเองใน .NET โดยใช้ Aspose.Cells"
"url": "/th/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# เรนเดอร์ไฟล์ Excel เป็น PNG, TIFF และ PDF ด้วยแบบอักษรที่กำหนดเองโดยใช้ Aspose.Cells สำหรับ .NET

## การแนะนำ

การรักษาความสมบูรณ์ของแบบอักษรระหว่างการแปลงไฟล์ Excel เป็นรูปภาพหรือ PDF ถือเป็นสิ่งสำคัญสำหรับความสอดคล้องของแบรนด์ Aspose.Cells สำหรับ .NET นำเสนอโซลูชันที่มีประสิทธิภาพโดยให้คุณระบุแบบอักษรเริ่มต้นที่กำหนดเองในการแปลงเอกสารของคุณได้

ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับการเรนเดอร์ไฟล์ Excel เป็นรูปแบบ PNG, TIFF และ PDF โดยใช้ Aspose.Cells สำหรับ .NET ที่มีแบบอักษรเริ่มต้นแบบกำหนดเอง ซึ่งเหมาะอย่างยิ่งหากคุณ:
- มุ่งเน้นให้มีการพิมพ์ที่สม่ำเสมอในเอกสารที่แสดงผล
- จำเป็นต้องปรับแต่งการตั้งค่าแบบอักษรระหว่างการแปลง
- ต้องการสำรวจตัวเลือกการกำหนดค่าภายใน Aspose.Cells สำหรับ .NET

ให้ตั้งค่าสภาพแวดล้อมของคุณและนำคุณสมบัติเหล่านี้ไปใช้ได้อย่างราบรื่น

### ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มต้น ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- **สภาพแวดล้อม .NET**: ตั้งค่าบนเครื่องของคุณ (ควรเป็น .NET Core หรือ .NET Framework)
- **Aspose.Cells สำหรับไลบรารี .NET**:ติดตั้งไว้ในโครงการของคุณแล้ว
- **ไฟล์ Excel**:สมุดงาน Excel ที่มีข้อมูลที่จะแปลง

### การตั้งค่า Aspose.Cells สำหรับ .NET

ในการเริ่มต้น ให้เพิ่มไลบรารี Aspose.Cells ลงในโปรเจ็กต์ของคุณ:

**การใช้ .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**การใช้ตัวจัดการแพ็คเกจ:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

รับใบอนุญาตเพื่อเข้าถึงคุณสมบัติเต็มรูปแบบ:
- **ทดลองใช้งานฟรี**: เยี่ยม [ทดลองใช้ Aspose ฟรี](https://releases.aspose.com/cells/net/) สำหรับการเข้าถึงเบื้องต้น
- **ใบอนุญาตชั่วคราว**:รับได้จาก [ใบอนุญาตชั่วคราว Aspose](https://purchase-aspose.com/temporary-license/).
- **ซื้อ**:สำหรับใบอนุญาตถาวร ให้ไปที่ [การซื้อ Aspose](https://purchase-aspose.com/buy).

หลังจากได้รับใบอนุญาตแล้ว ให้เริ่มต้น Aspose.Cells ในแอปพลิเคชันของคุณ:
```csharp
// ตั้งค่าใบอนุญาตสำหรับ Aspose.Cells
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## คู่มือการใช้งาน

### การเรนเดอร์เป็น PNG ด้วยฟอนต์เริ่มต้นแบบกำหนดเอง

การเรนเดอร์เวิร์กชีต Excel เป็นไฟล์ PNG พร้อมตั้งค่าแบบอักษรเริ่มต้นแบบกำหนดเองจะช่วยให้ภาพมีความสอดคล้องกัน ดังต่อไปนี้:

#### ขั้นตอนที่ 1: กำหนดค่าตัวเลือกภาพ

กำหนดค่าตัวเลือกการเรนเดอร์สำหรับเอาท์พุตภาพของคุณ
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// ระบุไดเรกทอรี
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// เปิดไฟล์ Excel
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// ตั้งค่าตัวเลือกการเรนเดอร์ภาพ
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // ใช้แบบอักษรแบบกำหนดเองสำหรับแบบอักษรที่หายไปในเวิร์กบุ๊ก
imgOpt.DefaultFont = "Times New Roman";
```

#### ขั้นตอนที่ 2: เรนเดอร์และบันทึก

เรนเดอร์แผ่นงานของคุณเป็นไฟล์รูปภาพโดยใช้การตั้งค่าเหล่านี้
```csharp
// เรนเดอร์เวิร์กชีตแรกเป็นภาพ PNG
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### การเรนเดอร์เป็น TIFF ด้วยฟอนต์เริ่มต้นแบบกำหนดเอง

รูปแบบ TIFF เหมาะอย่างยิ่งสำหรับรูปภาพคุณภาพสูง ต่อไปนี้เป็นวิธีที่คุณสามารถเรนเดอร์เวิร์กบุ๊กทั้งหมดเป็นไฟล์ TIFF:

#### ขั้นตอนที่ 3: ตั้งค่าตัวเลือกภาพสำหรับ TIFF

กำหนดค่าตัวเลือกการเรนเดอร์สำหรับเอาท์พุต TIFF โดยเฉพาะ
```csharp
// ใช้ไดเร็กทอรีที่กำหนดไว้ก่อนหน้านี้ซ้ำและเปิดไฟล์ Excel
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// กำหนดค่าตัวเลือกการแสดงภาพสำหรับ TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### ขั้นตอนที่ 4: เรนเดอร์เวิร์กบุ๊กทั้งหมดเป็น TIFF

แปลงเวิร์กบุ๊กทั้งหมดเป็นไฟล์ TIFF เดียว
```csharp
// เรนเดอร์เวิร์กบุ๊กเป็นรูปภาพ TIFF
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### การเรนเดอร์เป็น PDF ด้วยฟอนต์เริ่มต้นแบบกำหนดเอง

การบันทึกเวิร์กบุ๊ก Excel เป็น PDF พร้อมรับประกันความสม่ำเสมอของแบบอักษรถือเป็นสิ่งสำคัญสำหรับการจัดทำเอกสารระดับมืออาชีพ

#### ขั้นตอนที่ 5: กำหนดค่าตัวเลือกการบันทึก PDF

ตั้งค่าตัวเลือกที่จำเป็นสำหรับการบันทึกไฟล์ของคุณเป็น PDF
```csharp
using Aspose.Cells;

// เปิดสมุดงานอีกครั้ง
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// ตั้งค่าตัวเลือกการบันทึก PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // ใช้แบบอักษรแบบกำหนดเองสำหรับแบบอักษรที่หายไปในเวิร์กบุ๊ก
```

#### ขั้นตอนที่ 6: บันทึกเป็น PDF

ส่งออกสมุดงานของคุณไปยังเอกสาร PDF
```csharp
// บันทึกสมุดงานเป็นไฟล์ PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## การประยุกต์ใช้งานจริง

- **รายงานทางธุรกิจ**:รับรองการสร้างแบรนด์ที่สอดคล้องกันในรายงานที่ส่งออกทั้งหมดด้วยการใช้แบบอักษรที่กำหนดเอง
- **การเก็บเอกสารถาวร**:แปลงไฟล์ Excel รุ่นเก่าเป็น PDF เพื่อการแบ่งปันและเก็บถาวรได้อย่างง่ายดายด้วยรูปแบบตัวอักษรที่เป็นมาตรฐาน
- **การออกแบบกราฟิก**:สร้างภาพ TIFF ที่มีความละเอียดสูงของข้อมูล Excel สำหรับการนำเสนอหรือโปรเจ็กต์ออกแบบ

การบูรณาการกับระบบอื่นๆ เช่น แพลตฟอร์ม CRM หรือโซลูชันการจัดการเอกสารสามารถปรับปรุงกรณีการใช้งานเหล่านี้ได้ดียิ่งขึ้นด้วยการทำการส่งออกอัตโนมัติตามทริกเกอร์หรือเหตุการณ์เฉพาะ

## การพิจารณาประสิทธิภาพ

การเพิ่มประสิทธิภาพกระบวนการเรนเดอร์ของคุณเป็นสิ่งสำคัญ:
- **การจัดการหน่วยความจำ**: กำจัดทิ้ง `Workbook`- `SheetRender`, และ `WorkbookRender` วัตถุเพื่อปลดปล่อยทรัพยากรอย่างทันท่วงที
- **การประมวลผลแบบแบตช์**:หากต้องจัดการกับไฟล์หลายไฟล์ ให้ใช้การประมวลผลแบบแบตช์เพื่อการจัดการที่มีประสิทธิภาพ
- **การดำเนินการแบบอะซิงโครนัส**:ใช้วิธีการแบบอะซิงโครนัสเมื่อทำได้เพื่อปรับปรุงการตอบสนองในแอปพลิเคชัน

## บทสรุป

ตอนนี้คุณได้เชี่ยวชาญการเรนเดอร์เวิร์กบุ๊ก Excel เป็นรูปแบบ PNG, TIFF และ PDF แล้ว พร้อมทั้งตั้งค่าฟอนต์เริ่มต้นแบบกำหนดเองโดยใช้ Aspose.Cells สำหรับ .NET ความสามารถนี้ช่วยให้มั่นใจว่าเอกสารของคุณรักษาความสมบูรณ์ของภาพบนแพลตฟอร์มและการใช้งานต่างๆ

สำรวจคุณลักษณะเพิ่มเติมที่ Aspose.Cells นำเสนอเพื่อปรับปรุงความสามารถในการจัดการเอกสารให้ดียิ่งขึ้น สำหรับข้อมูลเพิ่มเติมหรือความช่วยเหลือ โปรดไปที่ [ฟอรั่ม Aspose](https://forum-aspose.com/c/cells/9).

## ส่วนคำถามที่พบบ่อย

**1. Aspose.Cells สำหรับ .NET คืออะไร**
   — Aspose.Cells สำหรับ .NET เป็นไลบรารีที่ให้คุณสมบัติที่แข็งแกร่งสำหรับการจัดการและแปลงไฟล์ Excel ด้วยโปรแกรม

**2. ฉันสามารถใช้ Aspose.Cells ในแอปพลิเคชั่นเว็บได้หรือไม่**
   — ใช่ สามารถรวม Aspose.Cells เข้ากับ ASP.NET หรือแอปพลิเคชันเว็บอื่นๆ ที่ใช้ .NET ได้

**3. ฉันจะจัดการกับแบบอักษรที่หายไประหว่างการเรนเดอร์ได้อย่างไร**
   — โดยการตั้งค่า `CheckWorkbookDefaultFont` เป็นเท็จและระบุ `DefaultFont`คุณต้องแน่ใจว่าข้อความทั้งหมดใช้แบบอักษรที่คุณเลือก แม้ว่าแบบอักษรต้นฉบับจะไม่สามารถใช้ได้ก็ตาม

**4. มีการสนับสนุนรูปแบบอื่นนอกจาก PNG, TIFF และ PDF หรือไม่**
   — ใช่ Aspose.Cells รองรับรูปแบบภาพต่างๆ เช่น JPEG, BMP เป็นต้น และมีความสามารถในการแปลงเอกสารอย่างครอบคลุม

**5. แนวทางปฏิบัติที่ดีที่สุดสำหรับการใช้ Aspose.Cells ในแอปพลิเคชันขนาดใหญ่คืออะไร**
   — ใช้เทคนิคการจัดการหน่วยความจำที่มีประสิทธิภาพ การประมวลผลแบบแบตช์สำหรับการจัดการไฟล์หลายไฟล์ และพิจารณาการทำงานแบบอะซิงโครนัสเพื่อปรับปรุงประสิทธิภาพของแอปพลิเคชัน

## ทรัพยากร
- **เอกสารประกอบ**- [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/net/)
- **ดาวน์โหลด**- [การเปิดตัว Aspose.Cells](https://releases.aspose.com/cells/net/)
- **ซื้อ**- [ซื้อ Aspose.Cells](https://purchase.aspose.com/buy)
- **ทดลองใช้งานฟรี**- [ทดลองใช้ Aspose.Cells ฟรี](https://releases.aspose.com/cells/net/)
- **ใบอนุญาตชั่วคราว**- [รับใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}