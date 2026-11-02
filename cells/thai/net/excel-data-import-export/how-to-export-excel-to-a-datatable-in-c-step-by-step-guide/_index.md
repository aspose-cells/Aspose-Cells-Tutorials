---
category: general
date: 2026-03-18
description: วิธีส่งออกข้อมูล Excel ไปยัง DataTable ใน C# ด้วยโค้ดที่จัดการเซลล์เฉพาะ,
  แปลง Excel เป็น DataTable, และจัดรูปแบบตัวเลข. เรียนรู้การส่งออกเซลล์เฉพาะและอื่น
  ๆ อีกมาก.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: th
og_description: วิธีส่งออกข้อมูล Excel ไปยัง DataTable ใน C# บทเรียนนี้แสดงวิธีส่งออกเซลล์เฉพาะ,
  แปลง Excel เป็น DataTable, และจัดรูปแบบตัวเลขอย่างง่ายดาย.
og_title: วิธีส่งออก Excel ไปยัง DataTable ใน C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: วิธีส่งออก Excel ไปยัง DataTable ใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออก Excel ไปยัง DataTable ใน C# – คู่มือขั้นตอนโดยละเอียด

เคยสงสัย **วิธีการส่งออกข้อมูล Excel** ไปยัง `DataTable` โดยไม่สูญเสียรูปแบบหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต้องดึงส่วนหนึ่งของสเปรดชีตเข้าสู่หน่วยความจำเพื่อการรายงาน, การตรวจสอบ, หรือการแทรกข้อมูลแบบ bulk‑insert อยู่เสมอ ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# คุณสามารถส่งออกช่วงที่ต้องการอย่างแม่นยำ (เช่น *A1:F11*), บังคับให้ทุกเซลล์ถูกจัดเป็นสตริง, และแม้แต่กำหนดรูปแบบตัวเลขแบบกำหนดเองได้

ในบทเรียนนี้เราจะครอบคลุมทุกอย่างที่คุณต้องรู้: ตั้งแต่การโหลดเวิร์กบุ๊ก, การกำหนดค่า **export specific cells**, การแปลงช่วงเป็น `DataTable`, และการจัดการกรณีขอบเช่นแถวว่างหรือจำนวนที่ขึ้นกับโลคัล เมื่อจบคุณจะได้เมธอดที่นำกลับมาใช้ใหม่ได้ซึ่งทำงานกับสถานการณ์ **excel to datatable c#** ในโค้ดผลิตจริง

> **Prerequisites** – คุณจะต้องมีไลบรารี Aspose.Cells for .NET (หรือ API ที่คล้ายกันที่มี `ExportDataTable`) ตัวอย่างนี้สมมติว่าใช้ .NET 6+ แต่แนวคิดสามารถใช้กับเวอร์ชันก่อนหน้าได้เช่นกัน

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **convert Excel to DataTable** ด้วย Aspose.Cells
- การส่งออกช่วงที่กำหนดเอง (`excel range to datatable`) พร้อมบังคับให้ค่าทั้งหมดเป็นสตริง
- การใช้รูปแบบตัวเลขสองตำแหน่งทศนิยม (`#,#00.00`) ระหว่างการส่งออก
- จุดบกพร่องทั่วไป (แถวเป็น null, คอลัมน์ซ่อน) และวิธีหลีกเลี่ยง
- ตัวอย่างโค้ดที่พร้อมคัดลอกและรันได้เต็มรูปแบบ

---

## ข้อกำหนดเบื้องต้นและการตั้งค่า

ก่อนที่เราจะลงลึกในโค้ด โปรดตรวจสอบว่าคุณมี:

1. **Aspose.Cells for .NET** ติดตั้งผ่าน NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. ไฟล์ Excel (`input.xlsx`) อยู่ในโฟลเดอร์ที่คุณอ้างอิงได้ เช่น `YOUR_DIRECTORY/input.xlsx`
3. โปรเจกต์ที่เป้าหมายเป็น .NET 6 หรือใหม่กว่า (คำสั่ง `using` ด้านล่างทำงานได้ทันที)

> **Pro tip:** หากคุณใช้ไลบรารีอื่น (เช่น EPPlus หรือ ClosedXML) แนวคิดก็ยังเหมือนเดิม—โหลดเวิร์กบุ๊ก, เลือกช่วง, แล้วเรียกเมธอดที่คืนค่า `DataTable`

---

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กและดึง Worksheet แรก

สิ่งแรกที่คุณต้องการคืออ็อบเจ็กต์ `Workbook` ที่แทนไฟล์ Excel ของคุณ เมื่อได้แล้วคุณสามารถเข้าถึง Worksheet ใดก็ได้โดยใช้ดัชนีหรือชื่อ

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**ทำไมจึงสำคัญ:** การโหลดเวิร์กบุ๊กตั้งแต่ต้นทำให้คุณตรวจสอบโครงสร้าง (เช่น ชีตที่ซ่อน, การป้องกัน) ก่อนตัดสินใจว่าจะส่งออกเซลล์ใด หากไฟล์ใหญ่ ควรใช้ `LoadOptions` เพื่อสตรีมเฉพาะส่วนที่ต้องการเท่านั้น

---

## ขั้นตอนที่ 2: กำหนดค่า Export Options – ทำให้ค่าทั้งหมดเป็นสตริง

เมื่อคุณส่งออกข้อมูลเพื่อการประมวลผลต่อ (เช่น bulk insert เข้า SQL) คุณมักต้องการ **representation ของสตริงที่สอดคล้องกัน** เพื่อหลีกเลี่ยงข้อผิดพลาดประเภท type‑mismatch

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Explanation:**  
- `ExportAsString = true` บอก Aspose.Cells ให้ละเลยประเภทเซลล์ดั้งเดิมและคืนค่าข้อความที่จัดรูปแบบแล้ว  
- `NumberFormat = "#,##0.00"` ทำให้ตัวเลขเช่น `1234.5` กลายเป็น `"1,234.50"` — มีประโยชน์สำหรับรายงานการเงิน

หากคุณต้องการประเภทข้อมูลเดิม เพียงตั้งค่า `ExportAsString` เป็น `false` แล้วจัดการแปลงด้วยตนเอง

---

## ขั้นตอนที่ 3: ส่งออกช่วงเฉพาะ (A1:F11) ไปยัง DataTable

ต่อมาคือหัวใจของ **export specific cells** เมธอด `ExportDataTable` รับพารามิเตอร์แถว/คอลัมน์เริ่มต้นและสิ้นสุด (เริ่มจากศูนย์) พร้อมแฟล็กกำหนดว่าต้องรวมหัวข้อหรือไม่

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**What you get:** `DataTable` ที่มี 11 แถว (รวมหัวข้อ) และ 6 คอลัมน์ (`A`‑`F`) ค่าทั้งหมดเป็นสตริงตามรูปแบบที่กำหนดใน `exportOptions`

---

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ – พิมพ์ลง Console

ควรตรวจสอบผลลัพธ์ก่อนส่งต่อให้คอมโพเนนต์อื่นเสมอ

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

สังเกตว่าคอลัมน์ตัวเลขแสดงสองตำแหน่งทศนิยมตามที่เรากำหนดไว้

---

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมครบชุดที่เชื่อมทุกส่วนเข้าด้วยกัน ใส่ลงในโปรเจกต์คอนโซลใหม่ ปรับเส้นทางไฟล์ แล้วรัน — ไม่ต้องตั้งค่าเพิ่มเติม

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Key takeaways from the code:**

- อ็อบเจ็กต์ `ExportTableOptions` สามารถนำกลับมาใช้ใหม่ได้; คุณสามารถส่งต่อให้กับหลายการเรียก `ExportDataTable` หากต้องการส่งออกหลายช่วง  
- การนับดัชนีเริ่มที่ **0** ดังนั้น `A1` ตรงกับ `(0,0)`  
- ตั้งค่า `includeColumnNames` เป็น `true` จะใช้แถวแรกเป็นหัวข้อคอลัมน์โดยอัตโนมัติ — เหมาะสำหรับการทำงานต่อกับ `DataTable`

---

## การจัดการกรณีขอบและคำถามทั่วไป

### ถ้า Worksheet มีแถวหรือคอลัมน์ที่ซ่อนอยู่จะทำอย่างไร?

Aspose.Cells เคารพการมองเห็นโดยค่าเริ่มต้น หากต้องการส่งออกข้อมูลที่ซ่อน ให้ตั้งค่า `exportOptions.ExportHiddenRows = true` และ `ExportHiddenColumns = true`

### ไฟล์ Excel ของฉันมีสูตร—จะได้ค่าที่คำนวณแล้วหรือไม่?

ใช่ โดยค่าเริ่มต้น `ExportDataTable` จะคืนค่า **displayed value** (ผลลัพธ์ของสูตร) หากต้องการข้อความสูตรดิบ ให้ตั้งค่า `exportOptions.ExportFormulas = true`

### จะข้ามแถวที่ว่างเปล่าอย่างสมบูรณ์ได้อย่างไร?

หลังการส่งออก คุณสามารถตัดแถวว่างออกจาก `DataTable` ได้:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### สามารถส่งออกช่วงที่ไม่ต่อเนื่องได้หรือ (เช่น A1:B5 และ D1:E5)?

Aspose.Cells ไม่รองรับช่วงไม่ต่อเนื่องในคำเรียกเดียว ให้ส่งออกแต่ละบล็อกแยกกันแล้วรวม `DataTable` ที่ได้ด้วยตนเอง

---

## เคล็ดลับด้านประสิทธิภาพ

- **Reuse `ExportTableOptions`** สำหรับการส่งออกหลายครั้ง; การสร้างอินสแตนซ์ใหม่ทุกครั้งเพิ่มภาระโดยไม่จำเป็นและทำให้โค้ดรกขึ้น  
- **Stream ไฟล์ขนาดใหญ่** ด้วย `LoadOptions` เพื่อหลีกเลี่ยงการโหลดเวิร์กบุ๊กทั้งหมดเข้าสู่หน่วยความจำ  
- **หลีกเลี่ยง `DataTable`** หากคุณต้องการแค่ส่งออกเป็น CSV อย่างรวดเร็ว — `ExportDataTable` สะดวกแต่ไม่ใช่วิธีที่ประหยัดหน่วยความจำที่สุดสำหรับชีตขนาดมหาศาล

---

## สรุป

เราได้อธิบาย **วิธีการส่งออก Excel** ไปยัง `DataTable` พร้อมควบคุมรูปแบบ, จัดการช่วงเซลล์เฉพาะ, และทำให้ค่าทุกค่าเป็นสตริง ตัวอย่างเต็มแสดงวิธีที่สะอาดและพร้อมใช้งานในผลิตภัณฑ์ ซึ่งคุณสามารถปรับใช้กับ **convert excel to datatable**, **export specific cells**, หรือสถานการณ์ **excel range to datatable** ใด ๆ ที่เจอ

ลองปรับเปลี่ยน: เปลี่ยนช่วง, สลับ `ExportAsString`, หรือส่ง `DataTable` ตรงเข้า Entity Framework เพื่อ bulk insert ไม่ว่าคุณจะทำอะไร ฐานรากนี้จะช่วยให้คุณก้าวไปได้ไกล

### ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

- **Importing DataTable back into Excel** – เรียนรู้การทำงานย้อนกลับด้วย `ImportDataTable`  
- **Bulk inserting a DataTable into SQL Server** – ใช้ `SqlBulkCopy` เพื่อโหลดข้อมูลอย่างเร็วแรง  
- **Working with EPPlus or ClosedXML** – ดูวิธีทำเดียวกันด้วยไลบรารีทางเลือก  
- **Formatting cells on export** – สำรวจ `ExportTableOptions` เพิ่มเติมสำหรับรูปแบบวันที่, การตั้งค่าภูมิภาคแบบกำหนดเอง, และอื่น ๆ  

มีคำถามหรือกรณีการใช้งานอื่น? แสดงความคิดเห็นได้เลย แล้วเราจะต่อเนื่องสนทนากันต่อ Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}