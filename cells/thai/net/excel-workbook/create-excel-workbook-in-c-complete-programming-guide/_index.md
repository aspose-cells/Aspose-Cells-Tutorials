---
category: general
date: 2026-06-05
description: สร้าง workbook Excel ด้วย C# อย่างรวดเร็วและเรียนรู้วิธีตั้งค่ารูปแบบตัวเลขของเซลล์,
  ส่งออกเซลล์ Excel, และแปลงค่าของเซลล์เป็นสตริงด้วยความแม่นยำสองตำแหน่งทศนิยม.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: th
og_description: สร้างไฟล์ Excel ด้วย C# และเชี่ยวชาญการตั้งค่ารูปแบบตัวเลขของเซลล์,
  การส่งออกค่าเซลล์ Excel เป็นสตริง, และการจัดรูปแบบตัวเลขให้มีทศนิยมสองตำแหน่ง.
og_title: สร้าง Excel Workbook ใน C# – คู่มือเต็มขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: สร้าง Excel Workbook ด้วย C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยสงสัยไหมว่า **create Excel workbook** ใน C# ทำอย่างไรโดยไม่ต้องต่อสู้กับ COM interop หรือเทคนิค CSV ที่ยุ่งยาก? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ นักพัฒนาจำนวนมากต้องการวิธีที่สะอาดและเป็น .NET‑native เพื่อสร้างไฟล์ .xlsx ใส่ตัวเลขลงในเซลล์ แล้วส่งออกค่าดังกล่าวเป็นสตริงที่จัดรูปแบบอย่างสวยงาม  

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนทั้งหมด—เริ่มจากเวิร์กบุ๊กเปล่า ตั้งค่ารูปแบบตัวเลขของเซลล์ จัดรูปแบบตัวเลขให้มีสองตำแหน่งทศนิยม และสุดท้ายเรียนรู้ **how to export Excel cell** เป็นสตริง. เมื่อจบคุณจะเห็นวิธี **convert cell value to string** โดยไม่สูญเสียความแม่นยำ

> **Pro tip:** วิธีด้านล่างใช้ไลบรารี **Aspose.Cells for .NET** ซึ่งเป็น API ระดับเชิงพาณิชย์ที่ผ่านการทดสอบมาอย่างดี หากคุณกำลังมองหาทางเลือกฟรี EPPlus หรือ ClosedXML ทำงานคล้ายกัน แต่โค้ดสแนปช็อตจะต่างกันเล็กน้อย

## Prerequisites

ก่อนที่เราจะลงมือทำ โปรดตรวจสอบว่าคุณมี:

- .NET 6.0 SDK (หรือเวอร์ชัน .NET ล่าสุด) ติดตั้งอยู่
- Visual Studio 2022 หรือ VS Code พร้อมส่วนขยาย C#
- แพ็กเกจ NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)

ไม่มีการพึ่งพาอื่น ๆ ที่จำเป็น—ทุกอย่างที่เหลืออยู่ในไลบรารี

## Step 1: Install Aspose.Cells and Set Up the Project

เปิดเทอร์มินัล (หรือ Package Manager Console) แล้วรัน:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

คำสั่งนี้จะสร้างแอปคอนโซลใหม่ชื่อ `ExcelDemo` และดึง assembly `Aspose.Cells` เข้ามา  

ทำไมขั้นตอนนี้สำคัญ: หากไม่มีไลบรารี คุณจะไม่สามารถ **create Excel workbook** หรือจัดการเซลล์ได้อย่างปลอดภัยในระดับประเภท

## Step 2: Create the Workbook and Grab the First Worksheet

ตอนนี้เปิดไฟล์ `Program.cs` แล้วแทนที่โค้ดเริ่มต้นด้วยสแนปช็อตด้านล่าง ซึ่งแสดงขั้นตอนแรกที่ทำเมื่อ **create Excel workbook**—การสร้างอ็อบเจ็กต์ `Workbook` และอ้างอิงไปยังชีตเริ่มต้น

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Why?** วัตถุ `Workbook` คือการแสดงผลในหน่วยความจำของไฟล์ Excel โดยค่าเริ่มต้นจะมีชีตเดียว ซึ่งเราสามารถเข้าถึงได้ผ่านดัชนีศูนย์

## Step 3: Put a Numeric Value into a Specific Cell

เราจะกำหนดแถว 5 คอลัมน์ 2 (ดัชนีศูนย์) แล้วใส่ตัวเลขทศนิยม นี่เป็นการเตรียมพื้นฐานสำหรับ **format number with two decimals** ในขั้นต่อไป

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

เมธอด `PutValue` จะเก็บค่า double ดิบไว้ ณ จุดนี้ Excel จะยังแสดงค่าความแม่นยำเต็มรูปแบบ หากเราไม่กำหนดรูปแบบ

## Step 4: Set Cell Number Format (Two Decimal Places)

นี่คือจุดที่เราจะ **set cell number format** เราจะใช้วัตถุ `Style` เพื่อกำหนดรูปแบบตัวเลขแบบกำหนดเอง `"0.00"`—สองตำแหน่งทศนิยมพอดี

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

ทำไมต้องใช้สไตล์แทนการแปลงเป็นสตริง? การเก็บเซลล์เป็นประเภทตัวเลขยังคงรักษาความสามารถในการคำนวณ (เช่น sum, average) ในขณะที่แสดงผลตามที่ต้องการ

## Step 5: Export the Cell Value as a Formatted String

บางครั้งคุณอาจต้องการ **how to export excel cell** เป็นข้อความธรรมดา—เช่นเขียนลงไฟล์บันทึกหรือส่งผ่านเว็บ API Aspose.Cells ให้คุณแนบ `ExportTableOptions` ไปยังเซลล์ เพื่อบอกไลบรารีให้เรนเดอร์ค่าเป็นสตริงโดยใช้รูปแบบเดียวกัน

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

เมื่อเราอ่านค่าของเซลล์ผ่าน API การส่งออก เราจะได้รับสตริงที่เคารพกฎสองตำแหน่งทศนิยมแล้ว

## Step 6: Retrieve the Formatted String (Convert Cell Value to String)

มาทำการส่งออกจริงและดูผลลัพธ์ เมธอด `ExportString` จะคืนค่าข้อมูลของเซลล์เป็นสตริง พร้อมใช้ `ExportTableOptions` ที่เราแนบไว้

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

เมื่อรันโปรแกรม คอนโซลจะแสดง:

```
Formatted cell value: 12345.68
```

สังเกตการปัดเศษจาก `12345.6789` เป็น `12345.68`—นี่คือผลของ **format number with two decimals**

## Step 7: (Optional) Save the Workbook to Disk

หากคุณต้องการดูผลลัพธ์ในไฟล์ `.xlsx` จริง ๆ เพียงเรียก `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

เมื่อเปิด `DemoWorkbook.xlsx` จะเห็นเลขเดียวกันในเซลล์ **C6** ที่จัดรูปแบบเป็นสองตำแหน่งทศนิยม

## Edge Cases & Common Questions

### What if the cell already has a style?

เมธอด `GetStyle` จะคืนสำเนาของสไตล์ที่มีอยู่ ดังนั้นการจัดรูปแบบก่อนหน้า (ฟอนต์, สี ฯลฯ) จะยังคงอยู่ เราเพียงแค่เขียนทับคุณสมบัติ `Custom` เท่านั้น ส่วนอื่น ๆ จะไม่ถูกเปลี่ยน

### How does culture affect the decimal separator?

Aspose.Cells เคารพ `CultureInfo` ของเธรด หากต้องการจุลภาคแทนจุด ให้ตั้งค่า:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

รูปแบบ `"0.00"` เดียวกันจะถูกแสดงเป็น `12 345,68`

### Can I export a range of cells at once?

ได้—ใช้ `Worksheet.ExportDataTable` หรือ `Worksheet.ExportString` พร้อมที่อยู่ช่วง (`range address`). `ExportTableOptions` ที่กำหนดสำหรับเซลล์เดียวสามารถนำไปใช้กับช่วงทั้งหมดได้

### What if I don’t want the value rounded but truncated?

เปลี่ยนรูปแบบกำหนดเองเป็น `"0.00"` พร้อมโหมดปัดเศษที่ต้องการ หรือทำการตัดทศนิยมก่อนใส่ค่า:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Expected console output**

```
Formatted cell value: 12345.68
```

เปิด `DemoWorkbook.xlsx` → ไปที่เซลล์ **C6** → คุณจะเห็นเลขเดียวกันที่มีสองตำแหน่งทศนิยม

## Conclusion

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **create Excel workbook** ใน C#, **set cell number format**, **format number with two decimals**, เข้าใจ **how to export Excel cell** และ **convert cell value to string** สำหรับการประมวลผลต่อไป  

ประเด็นสำคัญคือ:

1. ใช้ `Workbook` และ `Worksheet` เพื่อสร้างไฟล์ Excel ในหน่วยความจำ  
2. ใส่สไตล์กำหนดเอง (`"0.00"`) เพื่อบังคับให้แสดงสองตำแหน่งทศนิยม  
3. แนบ `ExportTableOptions` ให้เซลล์เมื่อคุณต้องการตัวแทนสตริงที่เคารพรูปแบบเดียวกัน  

จากนี้คุณสามารถทดลองเพิ่มเซลล์อื่น ๆ, ใส่การจัดรูปแบบตามเงื่อนไข, หรือแม้แต่สร้างแผนภูมิ หากสนใจการจัดรูปแบบฟอนต์หรือเพิ่มสูตร ให้ดูเอกสาร Aspose.Cells เกี่ยวกับ **cell styling** และ **formula evaluation**

มีคำถามเพิ่มเติมเกี่ยวกับการทำงานอัตโนมัติของ Excel ใน C#? แสดงความคิดเห็นได้เลย และขอให้สนุกกับการเขียนโค้ด!

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}