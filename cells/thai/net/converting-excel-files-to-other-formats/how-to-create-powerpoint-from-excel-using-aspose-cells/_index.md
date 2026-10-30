---
category: general
date: 2026-09-18
description: สร้าง PowerPoint จาก Excel ด้วย Aspose.Cells – คัดลอกตาราง Pivot, ส่งออกช่วงข้อมูล,
  และบันทึกเป็น PPTX ด้วยโค้ด C# เพียงไม่กี่บรรทัด
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: th
lastmod: 2026-09-18
og_description: สร้าง PowerPoint จาก Excel อย่างรวดเร็ว เรียนรู้วิธีคัดลอกตาราง Pivot,
  ส่งออกช่วงข้อมูล, และบันทึกเวิร์กบุ๊กเป็นไฟล์ PPTX ด้วย Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: สร้าง PowerPoint จาก Excel ด้วย Aspose.Cells – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: วิธีสร้าง PowerPoint จาก Excel ด้วย Aspose.Cells
url: /th/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง PowerPoint จาก Excel ด้วย Aspose.Cells

หากคุณต้องการสร้าง PowerPoint จาก Excel คำแนะนำนี้จะแสดงวิธีแก้ไขแบบสั้นและครบวงจร คุณจะได้เห็นวิธีคัดลอก Pivot Table, ส่งออกช่วงที่เลือก, และบันทึกผลลัพธ์เป็นไฟล์ PPTX ด้วยเพียงไม่กี่บรรทัดของ C#  

การสร้างสไลด์เด็คโดยตรงจากข้อมูลสเปรดชีตช่วยขจัดขั้นตอนคัดลอก‑วางที่ทำให้กระบวนการรายงานช้าลง บทเรียนนี้ครอบคลุมทุกอย่างที่คุณต้องการ ตั้งแต่การตั้งค่าโปรเจกต์จนถึงไฟล์ PPTX สุดท้าย และทำงานร่วมกับ Aspose.Cells for .NET รุ่นล่าสุด

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

* **Aspose.Cells for .NET** (เวอร์ชัน 23.12 หรือใหม่กว่า) ติดตั้งผ่าน NuGet: `Install-Package Aspose.Cells`  
* สภาพแวดล้อมการพัฒนา **.NET 6+** (Visual Studio 2022 หรือ VS Code ก็ใช้ได้)  
* ไฟล์ Excel workbook (`Source.xlsx`) ที่มีข้อมูลและ Pivot Table ที่คุณต้องการนำมาใช้ใหม่  
* สิทธิ์การเขียนในโฟลเดอร์ปลายทาง  

ไม่ต้องใช้ไลบรารีของบุคคลที่สามเพิ่มเติม

## สร้าง PowerPoint จาก Excel – ขั้นตอนโดยละเอียด

กระบวนการประกอบด้วยสี่ขั้นตอนหลักที่สอดคล้องกับโค้ดตัวอย่างที่จะแสดงต่อไป

### ขั้นตอนที่ 1: โหลด workbook ต้นทางและกำหนดช่วง

คุณต้องโหลด workbook ที่บรรจุข้อมูลต้นทางและ Pivot Table การเลือกช่วงที่แม่นยำทำให้แน่ใจว่าเฉพาะเซลล์ที่ต้องการเท่านั้นจะถูกถ่ายโอน ซึ่งช่วยให้สไลด์ที่ได้มีขนาดเบา

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**ทำไมจึงสำคัญ:**  
`CreateRange` สร้างอ็อบเจ็กต์ `Range` ที่สามารถคัดลอกเป็นหนึ่งเดียวได้ การจำกัดช่วงเป็น `A1:G20` จะช่วยหลีกเลี่ยงการดึงเซลล์ที่ไม่เกี่ยวข้องซึ่งอาจทำให้ไฟล์ PowerPoint มีขนาดใหญ่ขึ้น

### ขั้นตอนที่ 2: เตรียม workbook ปลายทาง

Aspose.Cells ถือว่า PowerPoint slide เป็น workbook เมื่อคุณบันทึกเป็นรูปแบบ PPTX การสร้าง workbook ใหม่ให้คุณได้ “ผ้าใบ” ที่สะอาดสำหรับช่วงที่คัดลอกมา

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**เคล็ดลับ:** หากต้องการหลายสไลด์ คุณสามารถเพิ่ม worksheet เพิ่มเติมและบันทึกแต่ละอันเป็นไฟล์ PPTX แยกกันได้

### ขั้นตอนที่ 3: คัดลอกช่วงพร้อมคงไว้ซึ่ง Pivot Table

เมธอด `CopyRange` รับอ็อบเจ็กต์ `PasteOptions` การตั้งค่า `CopyPivotTables = true` บอก Aspose.Cells ให้รักษาโครงสร้าง Pivot Table ไว้ครบถ้วน ไม่ใช่แค่ค่าที่แสดงผลเท่านั้น

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**วิธีการทำงาน:**  
เมื่อ `CopyPivotTables` เป็น true worksheet ปลายทางจะได้รับทั้งข้อมูลต้นทางและ pivot cache ซึ่งหมายความว่า Pivot Table จะยังคงทำงานได้เต็มที่และสามารถรีเฟรชใหม่ได้หากข้อมูลต้นทางเปลี่ยนแปลง

### ขั้นตอนที่ 4: บันทึก workbook เป็นไฟล์ PowerPoint

สุดท้าย ส่งออก workbook ไปเป็นรูปแบบ PPTX ธง `SaveFormat.Pptx` บอก Aspose.Cells ให้เขียน worksheet เป็นสไลด์ PowerPoint

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**ผลลัพธ์:**  
`CopyWithPivot.pptx` เปิดใน Microsoft PowerPoint (หรือโปรแกรมดูที่รองรับ) จะมีสไลด์เดียวที่แสดงช่วงที่คัดลอก รวมถึง Pivot Table ที่ทำงานแบบไลฟ์และสามารถโต้ตอบได้ใน PowerPoint

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกไปวางในโปรเจกต์คอนโซลใหม่และรันได้ทันที

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อรันโปรแกรมจะแสดงข้อความ “PowerPoint file created successfully.” และสร้างไฟล์ชื่อ `CopyWithPivot.pptx` เปิดไฟล์ใน PowerPoint จะเห็นสไลด์เดียวที่ช่วง Excel ที่คัดลอกปรากฏเหมือนเดิมใน worksheet ต้นทาง พร้อมกับ Pivot Table ที่สามารถรีเฟรชจากภายใน PowerPoint ได้

## ความแตกต่างทั่วไปและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน |
|-----------|-------------------|
| **หลาย Pivot Table** | กำหนดอ็อบเจ็กต์ `Range` แยกสำหรับแต่ละตารางและเรียก `CopyRange` สำหรับแต่ละอัน หรือคัดลอกทั้ง sheet หากพวกมันใช้แหล่งข้อมูลเดียวกัน |
| **ชุดข้อมูลขนาดใหญ่** | เพิ่มช่วง (เช่น `"A1:Z5000"`). พิจารณาเปิดใช้งาน `PasteOptions.CompressData = true` เพื่อลดขนาด PPTX |
| **รูปแบบสไลด์ที่แตกต่าง** | หลังบันทึกเป็น PPTX ให้เปิดไฟล์ใน PowerPoint แล้วใช้เลย์เอาต์หรือธีมที่กำหนดเอง; ข้อมูลยังคงแก้ไขได้ |
| **บันทึกลงสตรีม** | ใช้ `destinationWorkbook.Save(stream, SaveFormat.Pptx)` เมื่อจำเป็นต้องส่ง PPTX กลับผ่าน Web API |
| **คงรูปแบบเซลล์** | ตั้งค่า `PasteOptions.PasteType = PasteType.All` เพื่อเก็บฟอนต์, สี, และเส้นขอบ |

**เคล็ดลับพิเศษ:** ตรวจสอบให้แน่ใจว่าโฟลเดอร์ปลายทางมีอยู่ก่อนเรียก `Save` หากโฟลเดอร์หายไป `Save` จะโยน `DirectoryNotFoundException`

## สรุป

ตอนนี้คุณรู้วิธีสร้าง PowerPoint จาก Excel, คัดลอก Pivot Table, และส่งออกผลลัพธ์เป็นไฟล์ PPTX ด้วย Aspose.Cells ขั้นตอน—โหลด workbook ต้นทาง, กำหนดช่วง, คัดลอกด้วย `CopyPivotTables`, และบันทึกเป็น PPTX—ครอบคลุมเวิร์กโฟลว์ทั้งหมดอย่างเชื่อถือได้และพร้อมใช้งานในสภาพแวดล้อมการผลิต  

ต่อไปลองสำรวจ **วิธีส่งออก Excel ไปเป็น PPTX** สำหรับหลาย worksheet, หรือเรียน **วิธีคัดลอกช่วงระหว่าง workbook** เมื่อคุณต้องรวมข้อมูลจากหลายแหล่งก่อนสร้างสไลด์เด็ค ทั้งสองหัวข้อใช้ API เดียวกันและสามารถผสานกันเพื่ออัตโนมัติขั้นตอนการรายงานที่ซับซ้อนได้

ขอให้เขียนโค้ดสนุกและเพลิดเพลินกับการเปลี่ยนสเปรดชีตของคุณให้เป็นงานนำเสนอที่ดูเป็นมืออาชีพ!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}