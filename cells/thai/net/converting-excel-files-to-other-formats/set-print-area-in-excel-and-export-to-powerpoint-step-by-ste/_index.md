---
category: general
date: 2026-03-22
description: ตั้งค่าพื้นที่พิมพ์ใน Excel และแปลง Excel เป็น PowerPoint พร้อมรูปทรงที่แก้ไขได้
  เรียนรู้วิธีทำให้แถวหัวเรื่องซ้ำ สร้าง PowerPoint จาก Excel และส่งออก Excel เป็นไฟล์
  pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: th
og_description: ตั้งค่าพื้นที่พิมพ์ใน Excel และแปลงเป็นสไลด์ PowerPoint พร้อมรูปทรงที่แก้ไขได้
  ทำตามคู่มือฉบับเต็มนี้เพื่อทำซ้ำแถวหัวเรื่องและส่งออก Excel เป็นไฟล์ pptx.
og_title: ตั้งค่าพื้นที่พิมพ์ใน Excel – การสอนการส่งออกไป PowerPoint
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: กำหนดพื้นที่พิมพ์ใน Excel และส่งออกเป็น PowerPoint – คู่มือขั้นตอนโดยละเอียด
url: /th/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งพื้นที่พิมพ์ใน Excel และส่งออกเป็น PowerPoint – คู่มือการเขียนโปรแกรมเต็มรูปแบบ

เคยต้องการ **set print area** ในแผ่นงาน Excel แล้วแปลงส่วนนั้นเป็นสไลด์ PowerPoint หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายกระบวนการรายงาน ข้อมูลเดียวกันที่พิมพ์ออกมาดีก็ต้องปรากฏในงานนำเสนอด้วย โดยมักจะทำให้แถวแรกทำซ้ำเป็นหัวเรื่อง ข่าวดีคือ ด้วยไม่กี่บรรทัดของ C# คุณสามารถ **convert excel to powerpoint**, ทำให้กล่องข้อความทั้งหมดแก้ไขได้, และแม้กระทั่ง **repeat title row** โดยอัตโนมัติ.

ในคู่มือนี้ เราจะพาคุณผ่านทุกอย่างที่ต้องรู้: ตั้งแต่การกำหนดพื้นที่พิมพ์จนถึงการสร้างไฟล์ PPTX ที่คุณสามารถแก้ไขได้โดยตรงใน PowerPoint. เมื่อจบคุณจะสามารถ **create powerpoint from excel**, ส่งออกผลลัพธ์เป็น **export excel to pptx**, และใช้โค้ดเดียวกันในโครงการ .NET ใดก็ได้. ไม่มีเวทมนตร์ เพียงขั้นตอนที่ชัดเจนและตัวอย่างที่ทำงานได้เต็มรูปแบบ.

## สิ่งที่คุณต้องมี

- **.NET 6.0** หรือใหม่กว่า (API ทำงานกับ .NET Framework ด้วย)
- **Aspose.Cells for .NET** (ไลบรารีที่ให้ `Workbook`, `ImageOrPrintOptions` เป็นต้น)
- IDE C# เบื้องต้น (Visual Studio, Rider, หรือ VS Code พร้อมส่วนขยาย C#)
- ไฟล์ Excel (`input.xlsx`) ที่มีข้อมูลที่คุณต้องการส่งออก

เท่านี้—ไม่มีแพ็กเกจ NuGet เพิ่มเติมนอกจาก Aspose.Cells. หากคุณยังไม่ได้เพิ่มไลบรารีนี้ ให้รัน:

```bash
dotnet add package Aspose.Cells
```

ตอนนี้เราพร้อมแล้ว.

## ขั้นตอนที่ 1: โหลด Workbook – จุดเริ่มต้นสำหรับการส่งออก

สิ่งแรกที่คุณต้องทำคือโหลด workbook ที่บรรจุแผ่นงานที่คุณต้องการแปลงเป็นสไลด์. ให้คิดว่า workbook คือเอกสารต้นทาง; หากไม่มีมัน สิ่งอื่นทั้งหมดก็ไม่มีความหมาย.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**ทำไมสิ่งนี้ถึงสำคัญ:** การโหลด workbook ทำให้คุณเข้าถึงคอลเลกชันของ worksheet, ตัวเลือกการตั้งค่าหน้ากระดาษ, และเอนจินการส่งออก. หากข้ามขั้นตอนนี้ คุณจะไม่สามารถตั้ง **print area** หรือทำซ้ำแถวใด ๆ ได้.

> **เคล็ดลับ:** ใช้เส้นทางแบบ absolute ระหว่างการทดสอบ, จากนั้นเปลี่ยนเป็นเส้นทางแบบ relative หรือเส้นทางที่กำหนดจากการตั้งค่าสำหรับการใช้งานจริง.

## ขั้นตอนที่ 2: กำหนดค่า Export Options – ทำให้ Text Boxes และ Shapes แก้ไขได้

เมื่อคุณส่งออกเป็น PowerPoint คุณอาจต้องการให้สไลด์ที่ได้สามารถแก้ไขได้. Aspose.Cells ให้คุณควบคุมสิ่งนี้ด้วย `ImageOrPrintOptions`. การตั้งค่า `ExportTextBoxes` และ `ExportShapeObjects` เป็น `true` บอกไลบรารีให้เก็บวัตถุเหล่านั้นเป็นองค์ประกอบ PowerPoint ดั้งเดิมแทนการแปลงเป็นภาพ.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**ทำไมสิ่งนี้ถึงสำคัญ:** หากคุณเคยต้องการ **convert excel to powerpoint** แล้วปรับแต่งสไลด์ด้วยตนเอง การตั้งค่านี้จะช่วยคุณไม่ต้องสร้าง Text Boxes ใหม่จากศูนย์. มันยังทำให้แน่ใจว่า Shapes ใด ๆ (เช่น ลูกศรหรือแผนภูมิ) จะคงเป็นวัตถุเวกเตอร์ที่คุณสามารถปรับขนาดได้.

## ขั้นตอนที่ 3: ตั้ง Print Area และทำให้แถวหัวเรื่องซ้ำ

ตอนนี้เรามาถึงหัวใจของบทเรียน: **set print area** และทำให้แถวแรกซ้ำบนทุกหน้าที่พิมพ์ (หรือในกรณีของเรา บนสไลด์ที่ส่งออก). Print area บอก Excel ว่าเซลล์ใดควรพิจารณาเพื่อพิมพ์—หรือส่งออกในสถานการณ์ของเรา.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**ทำไมสิ่งนี้ถึงสำคัญ:** การจำกัดการส่งออกเป็น `A1:G20` จะช่วยหลีกเลี่ยงการดึงช่วงว่างขนาดใหญ่, ทำให้การแปลงเร็วขึ้นและสไลด์ดูเป็นระเบียบ. บรรทัด `PrintTitleRows` ทำให้แถวแรกทำหน้าที่เป็นหัวเรื่อง—ตรงกับที่คุณต้องการเมื่อ **repeat title row** ในการนำเสนอ.

> **กรณีพิเศษ:** หากข้อมูลของคุณเริ่มที่แถว 2 ให้ปรับช่วงให้เหมาะสม (เช่น `PrintTitleRows = "$2:$2"`).

## ขั้นตอนที่ 4: บันทึก Worksheet เป็นไฟล์ PowerPoint

สุดท้าย เราเขียนสไลด์ลงดิสก์. เมธอด `Save` รับชื่อไฟล์เป้าหมายและตัวเลือกที่เราตั้งค่าก่อนหน้านี้. ผลลัพธ์คือไฟล์ PPTX ที่มี Text Boxes และ Shapes ที่แก้ไขได้, พร้อมเปิดใน PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**สิ่งที่คุณจะเห็น:** เปิด `SheetWithEditableShapes.pptx` ใน PowerPoint. แถวแรกปรากฏเป็นหัวเรื่อง, ทุกเซลล์จาก `A1:G20` ถูกเรนเดอร์, และ Shapes ใด ๆ ที่คุณเพิ่มใน Excel ยังคงย้ายและแก้ไขได้. ไม่มีภาพแรสเตอร์—เพียงวัตถุ PowerPoint ดั้งเดิม.

## ตัวอย่างทำงานเต็มรูปแบบ – รวมทุกขั้นตอน

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมคัดลอก‑วาง. รันเป็นแอปคอนโซลหรือฝังในโซลูชันที่ใหญ่ขึ้นใดก็ได้.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรันโปรแกรม, คอนโซลจะแสดงข้อความสำเร็จ, และไฟล์ PPTX จะปรากฏที่ตำแหน่งที่ระบุ. การเปิดไฟล์จะแสดงสไลด์เดียวที่มีช่วงที่เลือก, Text Boxes ที่แก้ไขได้, และ Shapes ดั้งเดิมใด ๆ.

## คำถามทั่วไป & ปัญหาที่พบบ่อย

| Question | Answer |
|----------|--------|
| **ทำงานได้กับหลาย Worksheet หรือไม่?** | ใช่. วนลูปผ่าน `workbook.Worksheets` และทำซ้ำขั้นตอนเดียวกันสำหรับแต่ละแผ่น, เปลี่ยนชื่อไฟล์ผลลัพธ์ในแต่ละครั้ง. |
| **ถ้าต้องการส่งออกมากกว่าหนึ่งสไลด์จะทำอย่างไร?** | เรียก `workbook.Save` หลายครั้งโดยใช้ `ImageOrPrintOptions` ที่แตกต่างกัน, แต่ละอันตั้งค่า `PageSetup` ที่ต่างกันหากจำเป็น. |
| **สามารถเปลี่ยนขนาดสไลด์ได้หรือไม่?** | ใช้ `exportOptions.ImageFormat` เพื่อตั้งค่า DPI, หรือปรับ `sheet.PageSetup.PaperSize` ก่อนบันทึก. |
| **Aspose.Cells ฟรีหรือไม่?** | มีการประเมินฟรีพร้อมลายน้ำ. สำหรับการใช้งานจริง จำเป็นต้องมีลิขสิทธิ์. |
| **สูตร Excel จะเป็นอย่างไร?** | ค่าที่ส่งออกคือ **ผลลัพธ์ที่คำนวณแล้ว** ณ เวลาที่ส่งออก. หากต้องการสูตรสดใน PowerPoint คุณจะต้องใช้วิธีอื่น. |

## เคล็ดลับสำหรับการทำงานที่ราบรื่น

- **เคล็ดลับ:** ตั้งค่า `Workbook.Settings.CalcMode = CalculationModeType.Automatic` ก่อนส่งออกเพื่อรับประกันว่าทุกสูตรเป็นรุ่นล่าสุด.
- **ระวัง:** ช่วงที่ใหญ่เกินไปอาจทำให้ใช้หน่วยความจำมาก. ลด Print Area ให้เล็กที่สุดที่จำเป็น.
- **เคล็ดลับด้านประสิทธิภาพ:** ใช้ `ImageOrPrintOptions` ตัวเดียวซ้ำหากส่งออกหลายแผ่น; การสร้างใหม่ทุกครั้งเพิ่มภาระ.
- **บันทึกเวอร์ชัน:** โค้ดข้างต้นมุ่งเป้าไปที่ Aspose.Cells 23.10 (ออกในเดือนพฤศจิกายน 2023). เวอร์ชันต่อมายังคง API เดียวกัน, แต่ควรตรวจสอบบันทึกการปล่อยเพื่อหาการเปลี่ยนแปลงที่ทำให้โค้ดเสีย.

## สรุป

เราได้อธิบายวิธี **set print area** ในแผ่นงาน Excel, ทำให้แถวแรกเป็นหัวเรื่อง, และจากนั้น **export excel to pptx** พร้อมคง Text Boxes และ Shapes ที่แก้ไขได้. สรุปคือ คุณรู้วิธีที่เชื่อถือได้ในการ **convert excel to powerpoint**, **repeat title row**, และ **create powerpoint from excel** ด้วยเพียงไม่กี่บรรทัดของ C#.

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองทำการแปลงเป็นชุดของหลายสิบรายงานอัตโนมัติ, หรือเพิ่มเลย์เอาต์สไลด์แบบกำหนดเองโดยใช้ PowerPoint SDK หลังการส่งออก. ไม่มีขีดจำกัด—ทดลอง, ทำลายสิ่งต่าง ๆ, และสนุกกับพลังของการสร้างเอกสารแบบโปรแกรม.

หากคุณพบว่าบทเรียนนี้มีประโยชน์, แชร์ให้คนอื่น, แสดงความคิดเห็นพร้อมการปรับแต่งของคุณ, หรือสำรวจคู่มืออื่น ๆ ของเราที่เกี่ยวกับ **export excel to pptx** และหัวข้อการทำอัตโนมัติเกี่ยวข้อง. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}