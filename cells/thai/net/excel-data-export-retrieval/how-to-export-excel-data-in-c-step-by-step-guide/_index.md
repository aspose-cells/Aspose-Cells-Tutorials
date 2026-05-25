---
category: general
date: 2026-03-21
description: วิธีส่งออกข้อมูล Excel พร้อมชื่อคอลัมน์ รักษาฟอร์แมตตัวเลข และอ่านแถวเฉพาะโดยใช้
  Aspose.Cells ใน C# เรียนรู้การอ่านแผ่นงาน Excel และส่งออกแถวที่ต้องการอย่างมีประสิทธิภาพ
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: th
og_description: วิธีส่งออกข้อมูล Excel พร้อมชื่อคอลัมน์ รักษาฟอร์แมตตัวเลข และอ่านแถวเฉพาะโดยใช้
  Aspose.Cells ตัวอย่างเต็มที่สามารถรันได้สำหรับนักพัฒนา C#
og_title: วิธีส่งออกข้อมูล Excel ใน C# – คู่มือการเขียนโปรแกรมครบวงจร
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: วิธีส่งออกข้อมูล Excel ด้วย C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออกข้อมูล Excel ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยสงสัย **how to export excel** ข้อมูลโดยไม่สูญเสียรูปแบบเดิมหรือไม่? บางทีคุณอาจลองคัดลอก‑วางอย่างรวดเร็วแล้วได้วันที่แสดงเป็น “44728” หรือหัวคอลัมน์หายไป นั่นทำให้หงุดหงิดใช่ไหม? ในบทเรียนนี้คุณจะได้เห็นวิธีที่สะอาดและครบวงจรในการอ่าน Worksheet ของ Excel, รักษาฟอร์แมตตัวเลข, ส่งออกพร้อมชื่อคอลัมน์, และแม้แต่เลือกแถวที่ต้องการเท่านั้น

เราจะใช้ไลบรารี Aspose.Cells เพราะให้การควบคุมระดับละเอียดบนตัวเลือกการส่งออก เมื่อจบบทเรียนนี้คุณจะมีโค้ดสแนปช็อตที่นำไปใช้ได้ในโปรเจกต์ .NET ใดก็ได้ และคุณจะเข้าใจว่าทำไมแต่ละตัวเลือกจึงสำคัญ ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่

---

## สิ่งที่คุณจะได้เรียนรู้

- **Read Excel worksheet** เข้าไปในหน่วยความจำด้วย Aspose.Cells
- **Export specific rows** (เช่น แถว 0‑49) พร้อมคงชื่อคอลัมน์
- **Preserve number format** เพื่อให้สกุลเงิน, วันที่, และเปอร์เซ็นต์คงรูปแบบเดิม
- วิธี **export with column names** และรวมคอมเมนต์ของเซลล์หากต้องการ
- ตัวอย่าง C# ที่พร้อมรันเต็มรูปแบบพร้อมเคล็ดลับหลีกเลี่ยงข้อผิดพลาดทั่วไป

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+ ด้วย)
- Aspose.Cells for .NET ที่ติดตั้งผ่าน NuGet (`Install-Package Aspose.Cells`)
- ไฟล์ Excel (`input.xlsx`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้

> **Pro tip:** หากคุณทำงานบน CI pipeline ให้ดึงแพ็กเกจ NuGet จากฟีดส่วนตัวเพื่อหลีกเลี่ยงปัญหาไลเซนส์ที่ไม่คาดคิด

---

## ขั้นตอนที่ 1 – ติดตั้ง Aspose.Cells และเพิ่ม Namespaces

ก่อนอื่นตรวจสอบให้แน่ใจว่าแพ็กเกจ Aspose.Cells อยู่ในโปรเจกต์ของคุณแล้ว เปิด Package Manager Console แล้วรัน:

```powershell
Install-Package Aspose.Cells
```

จากนั้นเพิ่ม `using` directives ที่ส่วนหัวของไฟล์ C# ของคุณ:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

การนำเข้าเหล่านี้ทำให้คุณเข้าถึง `Workbook`, `Worksheet`, `ExportTableOptions`, และ `DataTable`—ส่วนสำคัญสำหรับ **reading an Excel worksheet** และการส่งออกข้อมูล

---

## ขั้นตอนที่ 2 – โหลด Workbook (อ่านไฟล์ Excel)

ตอนนี้เราจะ **read the Excel worksheet** จริง ๆ ตัวสร้าง `Workbook` รับพาธของไฟล์และ Aspose.Cells จะจัดการทั้งรูปแบบ `.xlsx` และ `.xls` เก่า

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **ทำไมเรื่องนี้สำคัญ:** การโหลด workbook เพียงครั้งเดียวแล้วใช้ `Worksheet` เดิมซ้ำหลายครั้งนั้นมีประสิทธิภาพกว่าการเปิดไฟล์หลาย ๆ ครั้ง โดยเฉพาะกับสเปรดชีตขนาดใหญ่

---

## ขั้นตอนที่ 3 – ตั้งค่า Export Options (Preserve Number Format & Column Names)

ตรงนี้เราจะบอก Aspose.Cells *วิธี* ส่งออก `ExportTableOptions` ให้เราปรับแต่งผลลัพธ์ได้ เราจะเปิดใช้สามฟลัก:

1. `ExportAsString = true` – บังคับให้ทุกเซลล์เป็นสตริง เพื่อให้ตัวเลขคงรูปแบบที่มองเห็น
2. `IncludeCellComments = true` – คัดลอกคอมเมนต์ที่แนบกับเซลล์ (สะดวกสำหรับเอกสารประกอบ)
3. `PreserveNumberFormat = true` – รักษาฟอร์แมตตัวเลขเดิม (สัญลักษณ์สกุลเงิน, รูปแบบวันที่ ฯลฯ)

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **กรณีขอบ:** หากตั้ง `ExportAsString` เป็น `false` แต่ยังต้องการคงฟอร์แมตตัวเลข คุณอาจเจอค่าตัวเลขดิบ (เช่น 44728 สำหรับวันที่) การเปิดทั้งสองฟลักจะช่วยหลีกเลี่ยงสถานการณ์นั้น

---

## ขั้นตอนที่ 4 – ดึง Worksheet แรก (Read Excel Worksheet)

ไฟล์ง่าย ๆ ส่วนใหญ่มีข้อมูลที่ต้องการอยู่บนแผ่นแรก เราจึงดึงโดยใช้ดัชนี หากต้องการแผ่นอื่นให้เปลี่ยน `0` เป็นดัชนีที่ต้องการหรือใช้ `workbook.Worksheets["SheetName"]`

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **ทำไมจึงเป็นประโยชน์:** การเข้าถึงอ็อบเจ็กต์ worksheet โดยตรงให้คุณควบคุมคอลเลกชัน `Cells` ได้เต็มที่ ซึ่งจำเป็นสำหรับ **export specific rows** ในขั้นตอนต่อไป

---

## ขั้นตอนที่ 5 – ส่งออกช่วงเซลล์ (Export Specific Rows)

นี่คือหัวใจของบทเรียน: ส่งออกแถว 0‑49 และคอลัมน์ 0‑4 (แถวแรก 50 แถวและคอลัมน์แรก 5 คอลัมน์) ไปยัง `DataTable` พร้อมให้ Aspose.Cells ใส่ชื่อคอลัมน์เป็นแถวแรกของ `DataTable`

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### สิ่งที่ทำงานนี้ทำ

- **`startRow: 0`** – เริ่มจากด้านบนสุดของแผ่น
- **`totalRows: 50`** – ดึง 50 แถวแรก (**export specific rows**)
- **`totalColumns: 5`** – จำกัดการส่งออกเพียง 5 คอลัมน์แรก
- **`includeColumnNames: true`** – ทำให้หัวคอลัมน์ของ `DataTable` ตรงกับแถวหัวของ Excel, ตอบโจทย์ **export with column names**
- **`exportOptions`** – ใช้การตั้งค่าจากขั้นตอน 3 เพื่อให้ค่าตัวเลขแสดงเป็น “$1,234.56” แทน “1234.56”

---

## ขั้นตอนที่ 6 – ตรวจสอบผลการส่งออก (What the Result Looks Like)

พิมพ์แถวแรก ๆ ลงคอนโซลเพื่อให้คุณเห็นว่าฟอร์แมตยังคงอยู่

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**ผลลัพธ์ที่คาดหวัง (ตัวอย่าง):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

สังเกตว่าข้อมูลวันที่แสดงในรูปแบบ `MM/dd/yyyy` และสกุลเงินยังคงมีสัญลักษณ์ `$`—ทั้งหมดนี้มาจาก **preserve number format**

---

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| วันที่แปลงเป็นตัวเลขขนาดใหญ่ | `ExportAsString` left `false` | ตั้งค่า `ExportAsString = true` หรือแปลงเซลล์ด้วยตนเอง |
| ไม่มีหัวคอลัมน์ | `includeColumnNames` set to `false` | ตั้งค่าเป็น `true` เมื่อคุณต้องการ **export with column names** |
| คอมเมนต์หาย | `IncludeCellComments` not enabled | เปิดใช้งาน `IncludeCellComments` ใน `ExportTableOptions` |
| ส่งออกแผ่นงานผิด | Using `Worksheets[0]` on a multi‑sheet file | ระบุชื่อแผ่นงาน: `workbook.Worksheets["Data"]` |
| ข้อยกเว้นเกินช่วง | `totalRows` exceeds actual rows | ใช้ `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## โบนัส: ส่งออกทั้งแผ่นงานพร้อมคงฟอร์แมต

หากในภายหลังต้องการส่งออกทั้งแผ่น ให้เปลี่ยน `totalRows` และ `totalColumns` เป็นขนาดสูงสุดของแผ่นงาน:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

ตอนนี้คุณมี **read excel worksheet** routine ที่ทำงานกับขนาดใดก็ได้ พร้อม **preserving number format** และ **exporting with column names**

---

## ตัวอย่างเต็มที่พร้อมรัน (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถวางลงในแอปคอนโซลได้ รวมทุกขั้นตอน, การนำเข้า, และการพิมพ์ผลตรวจสอบอย่างง่าย

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

บันทึกเป็น `Program.cs`, รัน `dotnet run` แล้วคุณจะเห็นตัวอย่างข้อมูลที่จัดรูปแบบไว้ในเทอร์มินัลของคุณ

---

## สรุป

เราได้เดินผ่าน **how to export excel** ด้วย Aspose.Cells ตั้งแต่การโหลด workbook, การคงฟอร์แมตตัวเลข, การส่งออกพร้อมชื่อคอลัมน์, และการจำกัดแถวที่ต้องการ โค้ดนี้เป็นอิสระ, รันได้ทันที, และรวมการป้องกันข้อผิดพลาดที่พบบ่อยที่สุด

พร้อมรับความท้าทายต่อไปหรือยัง? ลองส่งออกเป็น CSV โดยยังคงฟอร์แมตตัวเลขเดิม หรือส่ง `DataTable` ไปยัง Entity Framework Core เพื่อทำการแทรกข้อมูลจำนวนมาก ทั้งสองกรณีใช้พื้นฐานเดียวกับที่เราเรียนในที่นี้

ถ้าคุณพบว่าคู่มือเล่มนี้เป็นประโยชน์

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}