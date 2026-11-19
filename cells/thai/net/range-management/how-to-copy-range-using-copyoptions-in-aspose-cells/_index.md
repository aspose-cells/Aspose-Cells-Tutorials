---
category: general
date: 2026-11-19
description: เรียนรู้วิธีคัดลอกช่วงโดยใช้ CopyOptions ใน Aspose.Cells พร้อมรักษาการจัดรูปแบบและตาราง
  Pivot ขณะคัดลอกช่วงของ Excel ที่มีการจัดรูปแบบ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: th
lastmod: 2026-11-19
og_description: การคัดลอกช่วงโดยใช้ CopyOptions ใน Aspose.Cells ทำให้คุณสามารถทำสำเนาข้อมูล
  Excel พร้อมการจัดรูปแบบเต็มรูปแบบและตาราง Pivot ที่คงไว้ ทำให้การจัดการเวิร์กบุ๊กเป็นไปอย่างน่าเชื่อถือ
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: คัดลอกช่วงโดยใช้ CopyOptions ใน Aspose.Cells – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีคัดลอกช่วงโดยใช้ CopyOptions ใน Aspose.Cells
url: /th/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอกช่วงโดยใช้ CopyOptions ใน Aspose.Cells

หากคุณต้องการ **copy range using CopyOptions** ใน Aspose.Cells คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าจะแนบบล็อกเซลล์หนึ่งให้ซ้ำได้อย่างไรโดยยังคงรักษาการจัดรูปแบบทั้งหมดและ Pivot Table ที่ฝังอยู่ให้สมบูรณ์ นักพัฒนาหลายคนมักประสบปัญหาในการรักษาสไตล์เมื่อย้ายข้อมูลระหว่างแผ่นงาน และคลาส `CopyOptions` ช่วยแก้ปัญหานี้ได้โดยไม่ต้องทำขั้นตอนเพิ่มเติมด้วยตนเอง

ในบทเรียนนี้คุณจะได้เรียนรู้:

* กำหนดพื้นที่ต้นทางและปลายทางในไฟล์ Excel workbook  
* ใช้ `CopyOptions` เพื่อคงรูปแบบเซลล์ ความกว้างคอลัมน์ และ Pivot Table  
* บันทึกผลลัพธ์เป็นไฟล์ใหม่พร้อมใช้ต่อในกระบวนการถัดไป

ตัวอย่างนี้ทำงานกับไฟล์ `.xlsx` ใด ๆ ก็ได้และต้องการเพียงไลบรารี Aspose.Cells for .NET

## Prerequisites

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า  
* ไลเซนส์ Aspose.Cells for .NET ที่ถูกต้อง (หรือคีย์ทดลองใช้ฟรี)  
* Visual Studio 2022 หรือ IDE C# ที่คุณชื่นชอบ  

ไม่ต้องติดตั้งแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Cells`

## Step 1: Set up the project and import namespaces

สร้างแอปพลิเคชันคอนโซลใหม่และเพิ่มการอ้างอิง Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

คำสั่ง `using Aspose.Cells;` จะทำให้คุณเข้าถึง `Workbook`, `CellArea`, และ `CopyOptions`

## Step 2: Load the workbook you want to modify

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` แทนไฟล์ Excel ทั้งไฟล์ เปลี่ยน `YOUR_DIRECTORY` ให้เป็นโฟลเดอร์ที่เก็บไฟล์ต้นทางของคุณ

## Step 3: Define the source and destination ranges

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` สร้างพื้นที่สี่เหลี่ยมโดยอ้างอิงจากที่อยู่เซลล์มุมบนซ้ายและมุมล่างขวา คุณสามารถปรับพิกัดให้ตรงกับขนาดบล็อกที่ต้องการคัดลอกได้

## Step 4: Copy the range while preserving formatting and pivot tables

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

อ็อบเจกต์ `CopyOptions` บอก Aspose.Cells ว่าต้องการเก็บอะไรไว้ การตั้งค่า `CopyPivotTables = true` คือกุญแจสำคัญสำหรับ **copy range using CopyOptions** เมื่อแหล่งข้อมูลของคุณมี Pivot Table ธงอื่น ๆ ทำให้ **copy excel range with formatting** สำเร็จโดยอัตโนมัติ—ไม่ต้องเขียนโค้ดเพิ่มเติมเพื่อใส่สไตล์หลังการคัดลอก

### Why `CopyOptions` matters

* **Performance** – ไลบรารีทำการคัดลอกเป็นการดำเนินการภายในเดียว แทนการคัดลอกเซลล์ทีละเซลล์  
* **Accuracy** – ลักษณะการแสดงผลทั้งหมด (ฟอนต์, สี, เส้นขอบ) จะคงอยู่หลังการย้าย ลดความคลาดเคลื่อนในรายงานที่สร้างขึ้น  
* **Reliability** – Pivot Table ยังคงทำงานได้ เพราะแคชและการอ้างอิงแหล่งข้อมูลถูกทำสำเนาไปด้วย

## Step 5: Save the modified workbook

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

หลังจากเรียก `Save` ไฟล์ `output.xlsx` จะมีข้อมูลเดิมพร้อมบล็อกที่คัดลอกซ้ำที่ตำแหน่งปลายทาง พร้อมรูปแบบและ Pivot Table อย่างครบถ้วน

## Full source code for reference

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

เมื่อรันโปรแกรมนี้จะแสดงผล:

```
Range copied successfully. Output saved to output.xlsx
```

เปิด `output.xlsx` ใน Excel – คุณจะเห็นบล็อก A1:H30 ถูกคัดลอกซ้ำที่ A35:H64 พร้อมสีเซลล์, เส้นขอบ, รูปแบบตัวเลข และ Pivot Table ทั้งหมดคงอยู่

## Common questions and edge‑case handling

### What if the destination area overlaps the source?

Aspose.Cells จะโยน `ArgumentException` เพื่อหลีกเลี่ยงสถานการณ์นี้ ให้คำนวณตำแหน่งปลายทางที่ไม่ทับซ้อนกับแหล่งข้อมูล หรือคัดลอกไปยังแผ่นงานอื่น:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### How to copy between different workbooks?

สร้างอินสแตนซ์ `Workbook` ตัวที่สองสำหรับไฟล์เป้าหมายและใช้ `CopyOptions` เดียวกัน:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Does `CopyOptions` also copy merged cells?

ใช่. ธง `CopyStyle` รวมข้อมูลเซลล์ที่รวมกันไว้ด้วย หากต้องการควบคุมละเอียดเพิ่มเติม ให้ตั้งค่า `options.CopyMergedCells = true` (มีในเวอร์ชันใหม่)

### What about large ranges (thousands of rows)?

การดำเนินการนี้ใช้หน่วยความจำน้อย แต่สำหรับไฟล์ขนาดใหญ่มากอาจต้องเพิ่ม `WorkbookSettings` `MemorySetting` เป็น `MemorySetting.MemoryPreference`

## Pro tips

* **Reuse the same `CopyOptions`** instance สำหรับการคัดลอกหลายครั้ง – จะลดภาระการสร้างอ็อบเจกต์ใหม่  
* **Validate ranges** ก่อนคัดลอก: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` ช่วยจับข้อผิดพลาดจากการพิมพ์ผิดได้ตั้งแต่แรก  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) ระหว่างคัดลอกข้อมูลจำนวนมากเพื่อเร่งความเร็ว แล้วเรียก `workbook.CalculateFormula()` หลังคัดลอกหากต้องการผลลัพธ์ที่อัปเดต

## Conclusion

คุณได้เรียนรู้วิธี **copy range using CopyOptions** ใน Aspose.Cells เพื่อทำ **copy excel range with formatting** อย่างครบถ้วน พร้อมคง Pivot Table และคุณลักษณะขั้นสูงอื่น ๆ วิธีนี้ช่วยลดการทำซ้ำสไตล์ด้วยมือและทำให้การอัตโนมัติ Excel ของคุณมั่นคงและดูแลได้ง่ายขึ้น

ขั้นตอนต่อไปที่คุณอาจสนใจ:

* ใช้ `CopyOptions` คัดลอกแผ่นงานทั้งหมด  
* ผสานการคัดลอกกับ `WorksheetCollection.AddCopy` เพื่อสร้างรายงานจากเทมเพลต  
* นำโค้ดนี้รวมเข้าใน ASP.NET Core API เพื่อให้บริการแปลง Excel แบบเรียลไทม์

ลองปรับเปลี่ยนพิกัดต้นทาง/ปลายทางตามต้องการและแชร์ผลลัพธ์ของคุณในคอมเมนต์!

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}