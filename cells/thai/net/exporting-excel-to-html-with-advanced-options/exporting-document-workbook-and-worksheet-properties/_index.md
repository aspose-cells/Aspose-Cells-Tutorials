---
"description": "เรียนรู้วิธีการส่งออกเอกสาร Excel เวิร์กบุ๊ก และคุณสมบัติของเวิร์กชีตไปยัง HTML โดยใช้ Aspose.Cells สำหรับ .NET มีคู่มือทีละขั้นตอนง่ายๆ รวมอยู่ด้วย"
"linktitle": "การส่งออกเอกสารเวิร์กบุ๊กและคุณสมบัติของเวิร์กชีตในรูปแบบ HTML"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การส่งออกเอกสารเวิร์กบุ๊กและคุณสมบัติของเวิร์กชีตในรูปแบบ HTML"
"url": "/th/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การส่งออกเอกสารเวิร์กบุ๊กและคุณสมบัติของเวิร์กชีตในรูปแบบ HTML

## การแนะนำ

เมื่อต้องจัดการกับสเปรดชีต เรามักจะพบว่าจำเป็นต้องแปลงไฟล์ Excel เป็นรูปแบบต่างๆ เพื่อใช้ในการแชร์ เก็บรักษา หรือนำเสนอ งานทั่วไปอย่างหนึ่งคือการส่งออกคุณสมบัติของเวิร์กบุ๊กและเวิร์กชีตเป็นรูปแบบ HTML ในบทความนี้ เราจะแนะนำคุณเกี่ยวกับวิธีดำเนินการนี้โดยใช้ Aspose.Cells สำหรับ .NET ไม่ต้องกังวลหากคุณเพิ่งเริ่มเขียนโค้ดหรือใช้งานไลบรารี Aspose เราจะอธิบายขั้นตอนต่างๆ ให้คุณทราบทีละขั้นตอนเพื่อให้ทำตามได้ง่าย!

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกโค้ด เรามาตรวจสอบก่อนว่าคุณมีทุกสิ่งที่จำเป็นสำหรับการเริ่มต้น:

1. .NET Framework: ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณถูกตั้งค่าด้วย .NET Framework Aspose.Cells เข้ากันได้กับ .NET Framework เวอร์ชันสูงสุดถึง 4.8
   
2. Aspose.Cells สำหรับ .NET: คุณจะต้องติดตั้ง Aspose.Cells คุณสามารถดาวน์โหลดไลบรารีได้จาก [หน้าดาวน์โหลด](https://releases-aspose.com/cells/net/). 

3. IDE: สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) ที่เหมาะสม เช่น Visual Studio จะทำให้ประสบการณ์การเขียนโค้ดของคุณง่ายดายยิ่งขึ้น

4. ตัวอย่างไฟล์ Excel: เพื่อวัตถุประสงค์ในการทดสอบ โปรดตรวจสอบให้แน่ใจว่าคุณมีไฟล์ Excel ชื่อ `sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx` ในไดเร็กทอรีการทำงานของคุณ

## แพ็คเกจนำเข้า

ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นแล้ว เรามาเริ่มต้นด้วยการนำเข้าแพ็คเกจที่จำเป็นในโครงการ C# ของเรากันเลย วิธีดำเนินการมีดังนี้:

### สร้างโครงการใหม่

- เปิด IDE ของคุณและสร้างโปรเจ็กต์ C# ใหม่ คุณสามารถเลือกแอปพลิเคชันคอนโซลซึ่งเหมาะสำหรับการรันงานประเภทนี้

### เพิ่มแพ็กเกจ Aspose.Cells NuGet

หากต้องการเพิ่มแพ็คเกจ Aspose.Cells ให้ทำตามขั้นตอนเหล่านี้:

- คลิกขวาที่โครงการของคุณใน Solution Explorer และเลือก "จัดการแพ็คเกจ NuGet"
- ในตัวจัดการแพ็กเกจ NuGet ค้นหา "Aspose.Cells" และติดตั้ง
- แพ็คเกจนี้จะให้คลาสและวิธีการที่จำเป็นสำหรับการทำงานกับไฟล์ Excel

### การนำเข้าเนมสเปซ

ที่ด้านบนสุดของไฟล์โปรแกรมหลักของคุณ ตรวจสอบให้แน่ใจว่าคุณได้รวมเนมสเปซต่อไปนี้:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

สิ่งนี้จะทำให้เราสามารถเข้าถึง `Workbook` และ `HtmlSaveOptions` คลาสที่เราจะใช้ในตัวอย่างของเรา

ตอนนี้คุณพร้อมแล้ว มาแบ่งกระบวนการออกเป็นขั้นตอนง่าย ๆ กัน

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีไฟล์ของคุณ

ขั้นแรก เราต้องระบุว่าไฟล์อินพุตและเอาต์พุตของเราอยู่ที่ไหน ในโค้ดของคุณ ให้เริ่มต้นไดเรกทอรีดังนี้:

```csharp
// ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory/";  // อัปเดตด้วยเส้นทางจริงของคุณ

// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory/";  // อัปเดตด้วยเส้นทางจริงของคุณ
```

- ไดเรกทอรีแหล่งที่มา: นี่คือที่ที่ไฟล์ Excel อินพุตของคุณ (`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) ได้ถูกเก็บไว้
- ไดเรกทอรีเอาต์พุต: นี่คือเส้นทางที่คุณต้องการบันทึกไฟล์ HTML เอาต์พุต

## ขั้นตอนที่ 2: โหลดไฟล์ Excel ของคุณ

ตอนนี้เราต้องโหลดไฟล์ Excel โดยใช้ `Workbook` ระดับ:

```csharp
// โหลดไฟล์ตัวอย่าง Excel
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

- ตัวอย่างสมุดงาน: `Workbook` constructor จะนำเส้นทางไฟล์ไปยังไฟล์ Excel ของคุณและสร้างอินสแตนซ์ใหม่ที่คุณสามารถจัดการได้

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการบันทึก HTML

ต่อไปเราจะระบุวิธีที่เราต้องการบันทึกข้อมูล Excel ของเราลงใน HTML:

```csharp
// ระบุตัวเลือกการบันทึก HTML
HtmlSaveOptions options = new HtmlSaveOptions();

// ป้องกันการส่งออกเอกสาร สมุดงาน และคุณสมบัติของเวิร์กชีต
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: คลาสนี้ช่วยจัดการวิธีการแปลงไฟล์ Excel เป็น HTML
- เราตั้งค่าตัวเลือกต่างๆ ไว้ `false` เนื่องจากเราไม่ต้องการรวมคุณสมบัติของเวิร์กบุ๊กและเวิร์กชีตไว้ในผลลัพธ์ HTML ของเรา

## ขั้นตอนที่ 4: ส่งออกทุกอย่างไปยัง HTML

ตอนนี้เราพร้อมที่จะบันทึกสมุดงานของเราเป็นรูปแบบ HTML แล้ว:

```csharp
// ส่งออกไฟล์ Excel เป็น HTML ด้วยตัวเลือกการบันทึก HTML
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

- การ `Save` วิธีนี้ใช้พารามิเตอร์สองตัว ได้แก่ เส้นทางไฟล์สำหรับไฟล์ HTML เอาต์พุตและตัวเลือกที่เราได้ตั้งค่าไว้ การรันวิธีนี้จะสร้างไฟล์ HTML ของคุณในไดเร็กทอรีเอาต์พุตที่กำหนด

## ขั้นตอนที่ 5: ข้อเสนอแนะจากคอนโซล

สุดท้ายนี้ ขอให้เราส่งคำติชมผ่านคอนโซลเพื่อทราบว่ากระบวนการเสร็จสมบูรณ์แล้ว:

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## บทสรุป

และเพียงแค่นั้น คุณก็ส่งออกคุณสมบัติของเวิร์กบุ๊กและเวิร์กชีตไปยัง HTML ได้สำเร็จโดยใช้ Aspose.Cells สำหรับ .NET! คุณได้ทำตามขั้นตอนที่ตรงไปตรงมา ตั้งแต่การตั้งค่าสภาพแวดล้อมไปจนถึงการส่งออกข้อมูล Excel ของคุณ ข้อดีของการใช้ไลบรารีอย่าง Aspose.Cells คือมันช่วยทำให้กระบวนการที่ซับซ้อนราบรื่นขึ้น ทำให้ชีวิตของนักพัฒนาง่ายขึ้น ตอนนี้คุณสามารถแชร์สเปรดชีตของคุณกับ HTML ได้อย่างกว้างขวางขึ้น เหมือนกับการปล่อยให้คนทั้งโลกเห็นเวิร์กบุ๊กของคุณโดยไม่ต้องให้หนังสือทั้งเล่มแก่พวกเขา

## คำถามที่พบบ่อย

### ฉันจะติดตั้ง Aspose.Cells สำหรับ .NET ได้อย่างไร?  
คุณสามารถติดตั้งไลบรารี Aspose.Cells ผ่าน NuGet ในโปรเจ็กต์ Visual Studio ของคุณผ่านทางตัวจัดการแพ็กเกจ NuGet

### ฉันสามารถปรับแต่งผลลัพธ์ HTML ได้หรือไม่  
ใช่ Aspose.Cells มีตัวเลือกต่างๆ ให้เลือก `HtmlSaveOptions` เพื่อปรับแต่งวิธีการแปลงไฟล์ Excel ของคุณเป็น HTML

### มีวิธีรวมคุณสมบัติเอกสารในไฟล์ส่งออก HTML หรือไม่  
คุณสามารถตั้งค่าได้ `ExportDocumentProperties`- `ExportWorkbookProperties`, และ `ExportWorksheetProperties` ถึง `true` ใน `HtmlSaveOptions` หากคุณต้องการรวมไว้ด้วย

### ฉันสามารถส่งออกไฟล์ Excel เป็นรูปแบบอื่นใดได้อีก นอกจาก HTML?  
Aspose.Cells รองรับรูปแบบต่างๆ รวมถึง PDF, CSV, XML และอื่นๆ

### มีเวอร์ชันทดลองใช้งานไหม?  
ใช่ คุณสามารถรับ Aspose.Cells เวอร์ชันทดลองใช้งานฟรีได้จาก [เว็บไซต์](https://releases-aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}