---
category: general
date: 2026-08-07
description: กำหนดช่วงที่มีชื่อใน Excel ด้วย C# และเรียนรู้วิธีเพิ่มตารางลงในแผ่นงาน
  จากนั้นบันทึกเวิร์กบุ๊กเป็นไฟล์โดยอัตโนมัติ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: th
lastmod: 2026-08-07
og_description: กำหนดช่วงที่มีชื่อใน Excel ด้วย C# และดูวิธีเพิ่มตาราง, สร้างสมุดงานโดยโปรแกรม,
  และบันทึกสมุดงานเป็นไฟล์ในขั้นตอนเดียว.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: กำหนดช่วงชื่อใน Excel ด้วย C# – บทเรียนสมุดงานเต็ม
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: กำหนดช่วงที่ตั้งชื่อใน Excel ด้วย C# – สร้างสมุดงาน
url: /th/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# กำหนดช่วงชื่อใน Excel ด้วย C# – สร้างสมุดงาน

หากคุณต้องการ **define named range in Excel** จากโค้ด C# นี้จะสอนคุณอย่างละเอียดว่าต้องทำอย่างไร คุณจะได้เห็นวิธี **add a table to a worksheet**, สร้างสมุดงาน **programmatically**, และสุดท้าย **save workbook to file** โดยไม่ต้องออกจาก IDE.

การทำงานกับไฟล์ Excel อย่างโปรแกรมมิ่งช่วยประหยัดเวลา ลดข้อผิดพลาดจากการทำมือ และทำให้สามารถสร้างสายงานการรายงานอัตโนมัติได้ ในคู่มือนี้คุณจะได้:

* สร้าง Excel workbook ใหม่ตั้งแต่ต้น.  
* เพิ่มตารางที่ครอบคลุมช่วงเซลล์ที่กำหนด.  
* กำหนด named range และจัดการกับการชนกันของชื่อ.  
* บันทึกสมุดงานลงดิสก์.

ขั้นตอนทั้งหมดใช้ไลบรารี **Aspose.Cells for .NET** ซึ่งทำงานกับ .NET 6+ และ .NET Framework 4.6+ ไม่ต้องใช้ COM interop หรือการติดตั้ง Office เพิ่มเติม.

## ข้อกำหนดเบื้องต้น

* .NET 6 SDK (หรือ .NET Framework 4.6+).  
* Visual Studio 2022 หรือ IDE ที่รองรับ C#.  
* แพ็กเกจ NuGet ของ Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Pro tip:** ใช้ไลเซนส์ทดลองฟรีในระหว่างการทดสอบ; แทนที่ด้วยไลเซนส์ผลิตภัณฑ์ก่อนการนำไปใช้งาน.

## ขั้นตอนที่ 1: สร้าง Excel workbook อย่างโปรแกรมมิ่ง

การดำเนินการแรกคือการสร้างอ็อบเจ็กต์ `Workbook` ซึ่งอ็อบเจ็กต์นี้แทนไฟล์ Excel ทั้งหมดในหน่วยความจำ.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Why this matters*: การสร้างสมุดงานด้วยโค้ดทำให้คุณควบคุมแผ่นงาน, สไตล์, และข้อมูลได้อย่างเต็มที่ ก่อนที่ไฟล์ใดจะถูกเขียนลงดิสก์.

## ขั้นตอนที่ 2: เพิ่มตารางลงใน worksheet

ตาราง (หรือที่เรียกว่า ListObject) มีฟีเจอร์การกรอง, การเรียงลำดับ, และการจัดรูปแบบในตัว ที่นี่เราจะสร้างตารางที่ครอบคลุมเซลล์ **A1:B5** และตั้งชื่อว่า **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Why this matters*: การเพิ่มตารางตั้งแต่ต้นทำให้คุณสามารถอ้างอิงข้อมูลภายหลังด้วย **named range** และการอ้างอิงแบบโครงสร้างของตารางสามารถใช้ในสูตรได้.

## ขั้นตอนที่ 3: กำหนด named range ใน Excel – จัดการการชนกัน

**named range** คืออัตลักษณ์ที่ชี้ไปยังเซลล์หรือช่วง ทำให้สูตรอ่านง่ายขึ้น หากมีชื่อซ้ำอยู่แล้ว (เช่น ชื่อตาราง **SalesData**) Excel จะเกิดข้อขัดแย้ง โค้ดด้านล่างแสดงวิธีดักจับข้อยกเว้นนั้นและดำเนินการต่ออย่างปลอดภัย.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Why this matters*: การจัดการการชนกันของชื่อช่วยป้องกันการหยุดทำงานของโปรแกรมในงานอัตโนมัติ ช่วงชื่อที่สอง **SalesTotal** แสดงการอ้างอิงคอลัมน์ของตารางในสูตร.

## ขั้นตอนที่ 4: บันทึก workbook ลงไฟล์

หลังจากทำการแก้ไขทั้งหมดแล้ว ให้บันทึกสมุดงานลงดิสก์ เมธอด `Save` รองรับหลายรูปแบบ; ที่นี่เราใช้ค่าเริ่มต้น `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Why this matters*: การใช้ **save workbook to file** อย่างโปรแกรมมิ่งทำให้สามารถประมวลผลเป็นชุด, สร้างรายงานตามกำหนดเวลา, และรวมกับเว็บ API ได้.

## โค้ดต้นฉบับทั้งหมดในมุมมองเดียว

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

* ไฟล์ Excel ชื่อ **NameConflictHandled.xlsx** ปรากฏใน `C:\Temp`.  
* Sheet 1 มีตารางที่จัดรูปแบบแล้วชื่อ **SalesData** พร้อมแถวสินค้า‑จำนวน.  
* เซลล์ **B6** แสดงผลรวมของคอลัมน์ **Units** ที่คำนวณจาก named range **SalesTotal**.  
* คอนโซลพิมพ์ข้อความเกี่ยวกับการชนกันของชื่อ (ถ้ามี) และยืนยันตำแหน่งไฟล์.

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| **ฉันสามารถกำหนด named range ที่ครอบคลุมหลาย worksheet ได้หรือไม่?** | ได้. ใช้ `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` แล้วอ้างอิงจากแผ่นใดก็ได้. |
| **ถ้าต้องการเขียนทับไฟล์ที่มีอยู่จะทำอย่างไร?** | เรียก `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **จะเพิ่ม named range โดยไม่เกิดการชนกันเมื่อชื่อมีอยู่แล้วทำอย่างไร?** | ใช้ `worksheet.Names.Remove("ExistingName")` ก่อนเพิ่มใหม่, หรือสร้างตัวระบุที่ไม่ซ้ำ (เช่น `Guid.NewGuid().ToString("N")`). |
| **มีวิธีใดที่จะกำหนดสไตล์ให้ตารางโดยอัตโนมัติหรือไม่?** | ตั้งค่า `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` หลังจากสร้างตาราง. |
| **วิธีนี้ทำงานบน .NET Core หรือไม่?** | Aspose.Cells รองรับ .NET Core, .NET 5/6/7, และ .NET Framework. เพียงอ้างอิงแพ็กเกจ NuGet เดียวกัน. |

## สรุป

ตอนนี้คุณรู้วิธี **define named range in Excel** ด้วย C#, **add a table to a worksheet**, และ **save workbook to file** อย่างโปรแกรมมิ่ง ตัวอย่างเต็มแสดงการสร้าง Excel workbook ตั้งแต่ต้น, จัดการการชนกันของชื่อ, และสร้างไฟล์รายงานที่ใช้งานได้ในขั้นตอนเดียวที่ทำซ้ำได้.

ต่อไปลองสำรวจหัวข้อที่เกี่ยวข้องเช่น **adding charts to a worksheet**, **exporting to PDF**, หรือ **reading existing workbooks** แต่ละหัวข้ออิงจากพื้นฐานเดียวกันที่อธิบายไว้ที่นี่ ทำให้คุณพร้อมขยายโซลูชันไปสู่การทำงานอัตโนมัติที่ซับซ้อนยิ่งขึ้น ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการใช้งานอื่นในโครงการของคุณ.

- [สร้าง Named Range ของเซลล์ใน Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [วิธี Implement Named Range Formulas ใน .NET ด้วย Aspose.Cells สำหรับการทำ Automation ของ Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [วิธีสร้าง Workbook Scoped Named Ranges ใน Excel ด้วย Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}