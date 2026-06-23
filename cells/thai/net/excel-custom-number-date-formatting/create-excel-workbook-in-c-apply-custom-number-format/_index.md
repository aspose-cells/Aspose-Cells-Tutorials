---
category: general
date: 2026-05-23
description: สร้างไฟล์ Excel workbook ด้วย C# และเรียนรู้วิธีการใช้รูปแบบตัวเลขแบบกำหนดเอง
  ตั้งค่าสไตล์เซลล์โดยโปรแกรมเมชัน ฟอร์แมตเซลล์เป็นรูปแบบวิทยาศาสตร์ แล้วบันทึกไฟล์เป็น
  xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: th
og_description: สร้างเวิร์กบุ๊ก Excel ด้วย C# อย่างรวดเร็ว เรียนรู้การใช้รูปแบบตัวเลขแบบกำหนดเอง
  การจัดสไตล์เซลล์ด้วยโปรแกรม การจัดรูปแบบเลขวิทยาศาสตร์ และการบันทึกเป็นไฟล์ xlsx.
og_title: สร้าง Excel Workbook ด้วย C# – ใช้รูปแบบตัวเลขแบบกำหนดเอง
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: สร้าง Excel Workbook ด้วย C# – ใช้รูปแบบตัวเลขแบบกำหนดเอง
url: /th/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook ด้วย C# – ใช้รูปแบบตัวเลขแบบกำหนดเอง

การสร้าง excel workbook ด้วย C# นั้นง่ายกว่าที่คุณคิด ในคู่มือนี้เราจะพาคุณผ่านการใช้รูปแบบตัวเลขแบบกำหนดเอง การจัดรูปแบบเซลล์เป็น scientific notation การตั้งค่า style ของเซลล์โดยโปรแกรม และสุดท้ายการบันทึก workbook เป็นไฟล์ xlsx

หากคุณเคยมองดูสเปรดชีตเปล่าแล้วสงสัยว่าจะทำให้เป็นอัตโนมัติอย่างไร—from การใส่ข้อมูลจนถึงการทำให้ตัวเลขแสดงผลตามที่ต้องการ—บทเรียนนี้เหมาะกับคุณ เมื่อเสร็จแล้วคุณจะมีไฟล์ Excel ที่ทำงานได้เต็มที่ซึ่งสามารถเปิดได้ในโปรแกรมสเปรดชีตใดก็ได้ และคุณจะเข้าใจ **ทำไม** แต่ละขั้นตอนถึงสำคัญ ไม่ใช่แค่ **วิธี** พิมพ์โค้ด

## สิ่งที่คุณต้องมี

- **.NET 6+** (หรือ .NET Framework เวอร์ชันล่าสุดที่รองรับไลบรารี)  
- **Aspose.Cells for .NET** (หรือ API อื่นที่ให้คลาส `Workbook`, `Cell`, และ `CellFormat`)  
- ประสบการณ์พื้นฐานกับ C# เล็กน้อย – หากคุณเขียน `Console.WriteLine` ได้ก็พร้อมแล้ว  

ไม่มีไฟล์การตั้งค่าเพิ่มเติม ไม่มี COM interop และแน่นอนว่าไม่ต้องติดตั้ง Excel ด้วยตนเอง

---

## สร้าง Excel Workbook – เริ่มต้นอ็อบเจ็กต์ Workbook

สิ่งแรกที่เราต้องทำคือสร้าง workbook ว่างเปล่า คิดว่า `Workbook` คลาสเป็นผ้าใบเปล่าที่คุณจะวาดแถว คอลัมน์ และสไตล์ต่าง ๆ

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

แค่นี้—บรรทัดเดียวคุณก็มีไฟล์ Excel ใหม่ในหน่วยความจำแล้ว ตัวสร้าง `Workbook` จะสร้างคอลเลกชัน worksheet เริ่มต้นไว้โดยอัตโนมัติ ทำให้คุณสามารถเริ่มใส่ข้อมูลได้ทันที

> **เคล็ดลับ:** หากต้องการหลายชีต คุณสามารถเรียก `workbook.Worksheets.Add()` ก่อนเริ่มเติมเซลล์ได้

![Create excel workbook example](image-placeholder.png "Create excel workbook screenshot")

*ข้อความแทนภาพ: ตัวอย่างการสร้าง excel workbook ที่แสดงแผ่นงาน Excel ว่างใน IDE.*

## ใช้รูปแบบตัวเลขแบบกำหนดเองกับเซลล์

ตอนนี้ workbook มีอยู่แล้ว เราจะใส่ตัวเลขลงในเซลล์ **A1** แล้วกำหนดรูปแบบแบบกำหนดเอง รูปแบบตัวเลขแบบกำหนดเองช่วยให้คุณควบคุมการแสดงผลของตัวเลข—สกุลเงิน, เปอร์เซ็นต์, วันที่ หรือในกรณีนี้คือ scientific notation

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

ทำไมต้องดึง style มาก่อน? เพราะอ็อบเจ็กต์ `Cell` เก็บ **Style** ที่รวมฟอนต์, เส้นขอบ, การจัดแนว, และการจัดรูปแบบตัวเลขไว้ในที่เดียว การแก้ไขคุณสมบัติ `Custom` เราบอก Excel ว่า “แสดงค่านี้โดยใช้ scientific notation พร้อมทศนิยมสองตำแหน่ง”

> **คำถามที่พบบ่อย:** *ฉันสามารถใช้รูปแบบที่มีอยู่แล้วแทนการกำหนดเองได้หรือไม่?*  
> ใช่—ตั้งค่า `style.Number = 10` เพื่อใช้รูปแบบ scientific ที่มีอยู่แล้ว แต่สตริงกำหนดเองให้คุณควบคุมตำแหน่งทศนิยมได้อย่างแม่นยำ

## ตั้งค่า Style ของเซลล์โดยโปรแกรม (นอกเหนือจากรูปแบบตัวเลข)

บ่อยครั้งที่คุณต้องการมากกว่าการจัดรูปแบบตัวเลขเท่านั้น เราจะเพิ่มฟอนต์หนาและพื้นหลังสีเทาอ่อนเพื่อให้เซลล์โดดเด่นขึ้น

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

สังเกตว่าเราใช้วัตถุ `style` เดียวกันที่ปรับแต่งไว้ก่อนหน้านี้ นี่คือความสวยงามของ **set cell style programmatically**—คุณดึง style มาเพียงครั้งเดียว ปรับคุณสมบัติตามที่ต้องการ แล้วเขียนกลับไป ไม่ต้องสร้างอ็อบเจ็กต์ใหม่หรือสูญเสียรูปแบบตัวเลขที่ตั้งไว้แล้ว

## จัดรูปแบบเซลล์เป็น Scientific Notation (กรณีขอบ)

หากคุณทำงานกับตัวเลขที่ใหญ่มากหรือเล็กมาก scientific notation จะช่วยได้มาก รูปแบบกำหนดเองที่เราใช้ (`0.00E+00`) รับประกันว่ามีสองตำแหน่งหลังจุดทศนิยมและบังคับให้มีเครื่องหมายบวกสำหรับเอ็กซ์โปเนนท์ นี่คือการตรวจสอบอย่างรวดเร็ว:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

เมื่อคุณเปิดไฟล์ที่ได้ B2 จะปรากฏเป็น `1.23E-05` ยืนยันว่า **format cell scientific notation** ทำงานได้ทั้งกับตัวเลขใหญ่และเล็ก

## บันทึก Workbook เป็น XLSX

ความสนุกทั้งหมดจะหยุดเมื่อคุณเขียนไฟล์ลงดิสก์จริง ๆ วิธี `Save` จะทำงานหนักทั้งหมด แปลงข้อมูลในหน่วยความจำให้เป็นแพ็กเกจ `.xlsx` ที่สมบูรณ์

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

บรรทัดนี้ทำให้บรรลุเป้าหมาย **save workbook to xlsx** หากโฟลเดอร์ไม่อยู่ `Save` จะโยนข้อยกเว้น—ดังนั้นตรวจสอบให้แน่ใจว่าได้สร้างโฟลเดอร์ไว้ล่วงหน้าหรือห่อหุ้มการเรียกในบล็อก try/catch

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

ตอนนี้คุณมีไฟล์ Excel พร้อมแชร์ที่มีตัวเลข scientific ที่จัดรูปแบบสวยงาม ฟอนต์หนา และพื้นหลังสีเทาอ่อน

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมพร้อมคัดลอก‑วางที่รวมทุกส่วนเข้าด้วยกัน มันคอมไพล์เป็นแอปคอนโซล แต่คุณก็สามารถนำตรรกะนี้ไปใส่ในโปรเจกต์ C# ใดก็ได้

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `CustomFormatted.xlsx` แล้วคุณจะเห็น:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

ทั้งสองเซลล์เป็นฟอนต์หนา มีการเติมสีเทาอ่อน และแสดงตัวเลขใน scientific notation พร้อมทศนิยมสองตำแหน่ง

---

## สรุป

เราได้ **create excel workbook** ตั้งแต่ศูนย์, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically**, และ **save workbook to xlsx**—ทั้งหมดในไม่กี่บรรทัดของ C# วิธีนี้สามารถขยายได้: เพียงวนลูปผ่านแถว, คัดลอกอ็อบเจ็กต์ `style` แล้วคุณจะได้รายงานที่มีสไตล์ครบถ้วนในไม่กี่วินาที

### ขั้นตอนต่อไปคืออะไร?

- **การจัดรูปแบบแบบไดนามิก:** สลับรูปแบบตามขนาดค่ (เช่น สกุลเงิน vs. เปอร์เซ็นต์)  
- **หลายชีต:** ใช้ `workbook.Worksheets.Add("Summary")` เพื่อสร้างแดชบอร์ด  
- **การจัดรูปแบบขั้นสูง:** เส้นขอบ, conditional formatting, และ data validation

## บทเรียนที่เกี่ยวข้อง

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}