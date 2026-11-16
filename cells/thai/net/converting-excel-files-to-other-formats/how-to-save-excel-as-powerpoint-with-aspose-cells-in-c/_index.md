---
category: general
date: 2026-11-16
description: เรียนรู้วิธีบันทึก Excel เป็น PowerPoint และแปลง Excel เป็น PowerPoint
  อย่างอัตโนมัติ คู่มือขั้นตอนต่อขั้นตอนนี้ยังครอบคลุมการส่งออก Excel ไปเป็นไฟล์ PPTX
  และการบันทึกเวิร์กบุ๊กเป็น PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: th
lastmod: 2026-11-16
og_description: บันทึก Excel เป็น PowerPoint ด้วย Aspose.Cells. ทำตามคู่มือนี้เพื่อแปลง
  Excel เป็น PowerPoint, ส่งออก Excel เป็น PPTX, และบันทึกเวิร์กบุ๊กเป็น PPTX ภายในไม่กี่นาที.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: บันทึก Excel เป็น PowerPoint – คู่มือ C# ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: วิธีบันทึก Excel เป็น PowerPoint ด้วย Aspose.Cells ใน C#
url: /th/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีบันทึก Excel เป็น PowerPoint ด้วย Aspose.Cells ใน C#

หากคุณต้องการ **บันทึก Excel เป็น PowerPoint** อย่างอัตโนมัติ คำแนะนำนี้จะให้โซลูชันที่พร้อมใช้งานและทำงานได้ทันที ไม่ว่าคุณจะสร้างเครื่องมือรายงานหรือโปรแกรมสร้างสไลด์อัตโนมัติ ขั้นตอนต่อไปนี้จะช่วยให้คุณแปลงแผ่นงาน Excel ไปเป็นสไลด์ PPTX ที่แก้ไขได้เพียงไม่กี่บรรทัดของโค้ด

คุณจะได้เรียนรู้วิธี **แปลง Excel เป็น PowerPoint** ส่งออกแผ่นงานเป็นไฟล์ PPTX และทำให้กล่องข้อความและรูปทรงต่าง ๆ สามารถแก้ไขได้ – ทั้งหมดโดยไม่ต้องออกจากสภาพแวดล้อม .NET

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ตรวจสอบให้แน่ใจว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7.2+)
* ไลเซนส์ Aspose.Cells ที่ถูกต้อง (รุ่นทดลองฟรีใช้สำหรับการประเมิน)
* Visual Studio 2022 (หรือ IDE สำหรับ C# ใดก็ได้)
* ไฟล์ Excel workbook ที่มีข้อมูลและรูปทรงที่คุณต้องการส่งออก

## ขั้นตอนที่ 1: ติดตั้ง Aspose.Cells

เพิ่มแพคเกจ NuGet ของ Aspose.Cells ไปยังโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.Cells
```

> **เคล็ดลับ:** ใช้แฟล็ก `-v` เพื่อระบุเวอร์ชันที่ต้องการ เช่น `Aspose.Cells.24.5`.

## ขั้นตอนที่ 2: โหลด workbook ที่ต้องการส่งออก

การทำงานแรกในกระบวนการ **บันทึก Excel เป็น PowerPoint** คือการโหลด workbook ต้นทาง

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*เหตุผลที่สำคัญ:* การโหลด workbook ทำให้คุณเข้าถึงแผ่นงาน การตั้งค่าหน้ากระดาษ และวัตถุการวาดที่ต่อไปจะกลายเป็นรูปทรง PowerPoint ที่แก้ไขได้

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการส่งออกสำหรับสไลด์ PPTX ที่แก้ไขได้

เพื่อ **แปลง Excel เป็น PowerPoint** พร้อมคงความสามารถในการแก้ไข คุณต้องกำหนดคุณสมบัติบางอย่างบน `ImageOrPrintOptions`

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*คำอธิบาย:*  
* `SaveFormat = SaveFormat.Pptx` บอก Aspose.Cells ให้สร้างไฟล์ PowerPoint  
* `ExportEditableText` และ `ExportEditableShapes` ทำให้สไลด์ที่ได้ทำงานเหมือน PowerPoint ดั้งเดิม – คุณสามารถคลิกที่กล่องข้อความหรือรูปทรงและแก้ไขโดยตรงใน PowerPoint

## ขั้นตอนที่ 4: กำหนดพื้นที่ส่งออกและปรับให้พอดีกับสไลด์เดียว

เมื่อคุณ **ส่งออก Excel ไปเป็น PPTX** ปกติคุณต้องการให้ช่วงข้อมูลเฉพาะปรากฏบนสไลด์ การตั้งค่า print area และตัวเลือกการปรับขนาดจะทำให้ผลลัพธ์เป็นสไลด์เดียวที่เรียบร้อย

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*เหตุผลที่สำคัญ:* `PrintArea` จำกัดการส่งออกให้เฉพาะเซลล์ A1 ถึง G30 ส่วน `FitToPagesTall` และ `FitToPagesWide` จะบีบทุกอย่างให้พอดีในสไลด์เดียว ป้องกันไม่ให้สร้างหน้าที่ไม่ต้องการเพิ่มขึ้น

## ขั้นตอนที่ 5: บันทึกแผ่นงานเป็นไฟล์ PPTX ที่แก้ไขได้

ตอนนี้คุณสามารถ **บันทึก workbook เป็น PPTX** และสรุปกระบวนการ **บันทึก Excel เป็น PowerPoint** ได้แล้ว

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

หลังจากรันโปรแกรมแล้ว ให้เปิดไฟล์ `EditableShapes.pptx` ด้วย Microsoft PowerPoint คุณจะเห็นสไลด์ที่สะท้อนช่วง Excel ที่เลือก และกล่องข้อความรวมถึงรูปทรงทั้งหมดสามารถแก้ไขได้อย่างเต็มที่

### ผลลัพธ์ที่คาดหวัง

* ไฟล์ชื่อ `EditableShapes.pptx` อยู่ในโฟลเดอร์ `C:\Output\`
* สไลด์ PowerPoint หนึ่งสไลด์ที่มีช่วง A1:G30
* กล่องข้อความ, แผนภูมิและรูปทรงที่คุณสามารถดับเบิล‑คลิกและแก้ไขโดยตรงใน PowerPoint

## โค้ดเต็ม (พร้อมคัดลอก)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## คำถามที่พบบ่อยและการจัดการกรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้ามีหลายแผ่นงานจะทำอย่างไร?** | วนลูป `workbook.Worksheets` และทำซ้ำขั้นตอน 3‑5 สำหรับแต่ละแผ่นงาน โดยเปลี่ยนชื่อไฟล์ผลลัพธ์ (เช่น `Sheet1.pptx`, `Sheet2.pptx`) |
| **สามารถส่งออก workbook ทั้งหมดเป็นชุด PowerPoint เดียวได้หรือไม่?** | ทำได้ ตั้งค่า `ExportAllSheets = true` บน `ImageOrPrintOptions` แต่ละแผ่นงานจะกลายเป็นสไลด์แยกกัน |
| **รูปทรงของฉันแสดงเป็นภาพ ไม่ใช่วัตถุที่แก้ไขได้** | ตรวจสอบให้แน่ใจว่า `ExportEditableShapes = true` และคุณใช้ Aspose.Cells 24.5+ (เวอร์ชันก่อนหน้าไม่มีฟีเจอร์นี้) |
| **ไฟล์ PPTX ที่สร้างมีขนาดใหญ่เกินไป** | ลดขอบเขตการพิมพ์ หรือปรับความละเอียดภาพโดยใช้ `exportOptions.ImageResolution` |
| **ต้องการไลเซนส์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** | ไลเซนส์แบบชำระเงินจะลบลายน้ำการประเมินและเปิดใช้งานประสิทธิภาพเต็มที่ รุ่นทดลองใช้ได้สำหรับการทดสอบ |

## เคล็ดลับสำหรับโค้ดผลิตภัณฑ์ที่มั่นคง

* **ตรวจสอบเส้นทางไฟล์** ก่อนเรียก `Workbook` หรือ `Save` เพื่อหลีกเลี่ยง `FileNotFoundException`  
* **ห่อการส่งออกด้วย try/catch** เพื่อจัดการข้อผิดพลาดเกี่ยวกับไลเซนส์ (`Aspose.Cells.LicenseException`)  
* **ทำลาย workbook** (`workbook.Dispose()`) เมื่อเสร็จเพื่อคืนทรัพยากรที่ไม่ได้จัดการ  
* **ใช้ async I/O** (`FileStream` พร้อม `await`) หากต้องส่งออกแผ่นงานขนาดใหญ่หลายแผ่นในเว็บเซอร์วิส

## ขั้นตอนต่อไป

เมื่อคุณรู้วิธี **บันทึก Excel เป็น PowerPoint** แล้ว คุณสามารถสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

* **ส่งออก Excel ไปเป็น PPTX พร้อมรูปแบบสไลด์ที่กำหนดเอง** – ปรับ `SlideSize` และเพิ่ม master slide  
* **แปลงสไลด์ Excel เป็น PDF** – ใช้ `SaveFormat.Pdf` เพื่อสร้างเวอร์ชันที่พิมพ์ได้  
* **แปลงหลายไฟล์ในโฟลเดอร์** – ผสานลูปที่แสดงข้างต้นกับ `Directory.GetFiles`

ลองปรับเปลี่ยนพื้นที่การพิมพ์, ตัวเลือกการสเกล, และธีม PowerPoint เพื่อให้ผลลัพธ์สอดคล้องกับแบรนด์ขององค์กรคุณ

---

*ขอให้สนุกกับการเขียนโค้ด! หากคำแนะนำนี้ช่วยคุณ **แปลง Excel เป็น PowerPoint** ได้ อย่าลืมแชร์ให้เพื่อนร่วมทีมหรือเปิด issue ในรีโพซิทอรี Aspose.Cells บน GitHub เพื่อขอความช่วยเหลือเพิ่มเติม*

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีบันทึก Excel เป็น PowerPoint ด้วย C# และ Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [วิธีบันทึก PPTX จาก Excel – คู่มือเต็มสำหรับการส่งออกแผ่นงาน Excel ไปเป็น PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [แปลง Excel เป็น PowerPoint – คู่มือเต็มขั้นตอน](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}