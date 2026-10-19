---
category: general
date: 2026-07-03
description: เรียนรู้วิธีส่งออกตาราง Excel ไปเป็นไฟล์ .txt และบันทึกตาราง Excel เป็นไฟล์
  .txt ด้วย C# ส่งออกข้อมูล Excel เป็นข้อความธรรมดาพร้อมตัวอย่างโค้ดเต็ม
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: th
og_description: วิธีส่งออกตาราง Excel เป็นข้อความธรรมดา คู่มือนี้จะแสดงวิธีส่งออกข้อมูล
  Excel เป็นข้อความธรรมดาและบันทึกตาราง Excel เป็นไฟล์ .txt ด้วย Aspose.Cells
og_title: วิธีส่งออกตาราง Excel – บทเรียน C# เต็ม
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: วิธีส่งออกตาราง Excel – คู่มือขั้นตอนเต็ม
url: /th/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออกตาราง Excel – คู่มือขั้นตอนเต็ม

เคยสงสัย **how to export Excel table** โดยไม่ต้องโหลดเวิร์กบุ๊กทั้งหมดเข้าสู่หน่วยความจำหรือไม่? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ ในงานอัตโนมัติมากมาย ระบบปลายทางรับไฟล์ `.txt` เพียงไฟล์เดียวเท่านั้น ดังนั้นคุณจึงต้อง **save Excel table to .txt file** อย่างรวดเร็วและเชื่อถือได้  

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชัน C# ที่สะอาดโดยใช้ Aspose.Cells เพื่อ **exports Excel data as plain text** เมื่อจบคุณจะได้โปรแกรมพร้อมรัน เข้าใจเหตุผลของแต่ละบรรทัด และรู้วิธีปรับแต่งการส่งออกให้เหมาะกับกรณีของคุณ

## สิ่งที่คุณต้องเตรียม

- **Aspose.Cells for .NET** (เวอร์ชันล่าสุดใดก็ได้ เช่น 23.12)  
- .NET 6 SDK หรือใหม่กว่า – โค้ดนี้ยังคอมไพล์ได้กับ .NET Core ด้วย  
- ตัวอย่างไฟล์ `input.xlsx` ที่มีอย่างน้อยหนึ่งตาราง Excel  
- โปรแกรมแก้ไขข้อความหรือ IDE (Visual Studio, VS Code, Rider… ตามที่คุณชอบ)

ไม่ต้องใช้แพ็กเกจ NuGet เพิ่มเติมนอกจาก Aspose.Cells และสามารถทำงานได้บน Windows, Linux หรือ macOS

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้าไลบรารี

เริ่มต้นด้วยการสร้างแอปคอนโซลและนำเนมสเปซที่จำเป็นเข้ามาในสโคป

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Pro tip:** หากคุณใช้ .NET CLI ให้รัน `dotnet new console -n ExcelTableExport` แล้วตามด้วย `dotnet add package Aspose.Cells` ก่อนวางโค้ดด้านบน

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กและดึงเวิร์กชีตแรก

อ็อบเจ็กต์ workbook แทนไฟล์ Excel ทั้งไฟล์ การโหลดเพียงครั้งเดียวช่วยลดการใช้หน่วยความจำ

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

ทำไมเราถึงเลือกเวิร์กชีตแรก? ในหลาย ๆ รายงานที่สร้างโดยอัตโนมัติ ข้อมูลมักอยู่บนชีตแรก แต่คุณก็สามารถเปลี่ยนดัชนีหรือใช้ `wb.Worksheets["SheetName"]` เพื่อระบุชีตตามชื่อได้

## ขั้นตอนที่ 3: ดึงตารางแรกที่กำหนดบนเวิร์กชีต

ตาราง Excel (ListObjects) ให้ข้อมูลที่มีโครงสร้าง ทำให้การส่งออกคาดเดาได้ง่าย

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

หากเวิร์กบุ๊กของคุณมีหลายตาราง เพียงวนลูป `ws.Tables` หรือเลือกตาม `tbl.Name`

## ขั้นตอนที่ 4: ตั้งค่าตัวเลือกการส่งออก – ส่งออกทุกเซลล์เป็นสตริง

Aspose.Cells ให้คุณควบคุมรูปแบบของแต่ละเซลล์ระหว่างการส่งออก การตั้งค่า `ExportAsString` จะทำให้ตัวเลข, วันที่ และสูตรกลายเป็นข้อความธรรมดา

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### การเพิ่ม Action การส่งออกแบบกำหนดเองเพื่อทำ Trim ช่องว่าง

บ่อยครั้งที่ข้อมูลต้นทางมีช่องว่างนำหน้าหรือท้าย การตัดช่องว่างทำให้ไฟล์ `.txt` สุดท้ายสะอาดขึ้น

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Lambda จะรับอ็อบเจ็กต์ `Cell` และ `TextWriter` คุณยังสามารถเพิ่มเงื่อนไขอื่น ๆ ได้ เช่น แทนที่เครื่องหมายคอมม่าเป็นเซมิโคลอนสำหรับผลลัพธ์แบบ CSV

## ขั้นตอนที่ 5: ส่งออกตารางจากเซลล์ A1 ไปยังไฟล์ข้อความ

ตอนนี้เราจะเขียนตารางลงดิสก์จริง ๆ เมธอด `ExportTable` จะเดินตารางทีละแถวตามตัวเลือกที่เรากำหนดไว้

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**What you’ll see:** แต่ละแถวของตาราง Excel จะกลายเป็นบรรทัดใน `Table.txt` คอลัมน์จะแยกด้วยอักขระแท็บ (`\t`) เป็นค่าเริ่มต้น – เหมาะสำหรับการแยกข้อมูลต่อไป

### ตัวอย่างผลลัพธ์ที่คาดหวัง

สมมติว่า `input.xlsx` มีตารางที่มีสามคอลัมน์ (`ID`, `Name`, `Score`) และสองแถวข้อมูล `Table.txt` จะมีลักษณะดังนี้:

```
1    Alice    85
2    Bob      92
```

สังเกตว่าช่องว่างถูกตัดออกและทุกอย่างเป็นข้อความธรรมดา – ตรงตามความต้องการของ **export excel data as plain text** อย่างแท้จริง

## การจัดการกับกรณีขอบทั่วไป

| Situation | What to Do | Why |
|-----------|------------|-----|
| **ตารางมีเซลล์ว่าง** | Lambda จะเขียน `cell.StringValue.Trim()` ซึ่งจะคืนค่าว่างสำหรับเซลล์ที่ไม่มีค่า | รักษาการจัดแนวคอลัมน์โดยไม่เพิ่มอักขระที่ไม่ต้องการ |
| **คุณต้องการตัวคั่นแบบกำหนดเอง** | แทนที่ `writer.Write(cell.StringValue.Trim());` ด้วย `writer.Write($"{cell.StringValue.Trim()},");` แล้วตัดตัวคั่นส่วนท้ายหลังแต่ละแถว | ระบบบางแห่งต้องการคอมม่า หรือพายป์แทนแท็บ |
| **เวิร์กชีตขนาดใหญ่ ( > 100 k แถว )** | ใช้ `ExportTableOptions` พร้อม `ExportAsString = true` แล้วสตรีมไฟล์ตามที่แสดง; Aspose.Cells จะประมวลผลแถวแบบสตรีมเพื่อหลีกเลี่ยง OOM | รับประกันความสามารถในการขยาย |
| **หลายตารางในชีตเดียว** | วนลูป `ws.Tables` แล้วเรียก `ExportTable` สำหรับแต่ละตาราง หากต้องการอาจเพิ่มบรรทัดคั่นระหว่างการส่งออก | ทำให้คุณ **save Excel table to .txt file** สำหรับทุกตาราง |

## ตัวอย่างโปรแกรมทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคัดลอก‑วางลงใน `Program.cs` แทนที่ `YOUR_DIRECTORY` ด้วยพาธที่มีอยู่บนเครื่องของคุณ (แบบสัมบูรณ์หรือสัมพัทธ์)

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

รันโปรแกรมด้วย `dotnet run` หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะเห็นข้อความยืนยันและไฟล์ `Table.txt` ที่สร้างใหม่ซึ่งมี **export excel data as plain text** อยู่ภายใน

## โบนัส: การยืนยันด้วยภาพ (ทางเลือก)

หากคุณต้องการดูภาพหน้าจอของไฟล์ที่ได้ คุณสามารถเปิดไฟล์ในโปรแกรมแก้ไขข้อความใดก็ได้ ด้านล่างเป็นภาพตัวอย่างที่แสดงเลย์เอาต์ที่คาดหวัง

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Alt text:* **how to export excel table** – แสดงผลลัพธ์เป็นข้อความธรรมดาของตาราง Excel ที่ส่งออก

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุมทุกอย่างที่คุณต้องรู้ **how to export Excel table** ด้วย Aspose.Cells ตั้งแต่การโหลดเวิร์กบุ๊ก การตัดค่าเซลล์ และสุดท้ายการเขียนไฟล์ `.txt` ที่สะอาด  

- ตอนนี้คุณเข้าใจ **save Excel table to .txt file** พร้อมตรรกะกำหนดเองแล้ว  
- คุณสามารถปรับ Lambda เพื่อจัดการวันที่, ตัวเลข หรือกำหนดตัวคั่นแบบกำหนดเองได้  
- สำหรับโครงการขนาดใหญ่ ควรห่อหุ้มตรรกะนี้เป็นเมธอดหรือคลาสที่นำกลับมาใช้ใหม่ได้  

**What’s next?** ลองส่งออกหลายตาราง หรือเปลี่ยนรูปแบบผลลัพธ์เป็น CSV โดยเปลี่ยนตัวคั่น คุณอาจสำรวจ **export excel data as plain text** โดยตรงไปยังสตรีมเครือข่ายสำหรับการบูรณาการแบบเรียลไทม์ด้วย

มีคำถามหรือเจออุปสรรค? แสดงความคิดเห็นได้เลย และขอให้เขียนโค้ดสนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีการส่งออกไฟล์ Excel ใน .NET ด้วย Aspose.Cells: คู่มือฉบับสมบูรณ์](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [วิธีการส่งออกแถว Excel ที่มองเห็นได้ด้วย Aspose.Cells สำหรับ .NET: คู่มือขั้นตอน](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [วิธีการรวมแผ่น Excel เป็นไฟล์ข้อความเดียวด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}