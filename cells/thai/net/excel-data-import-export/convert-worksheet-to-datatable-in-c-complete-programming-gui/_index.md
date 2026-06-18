---
category: general
date: 2026-06-17
description: แปลง worksheet เป็น DataTable ใน C# อย่างรวดเร็ว เรียนรู้วิธีอ่านไฟล์
  Excel ไปยัง DataTable ด้วย C# และส่งออก Excel ไปยัง DataTable ด้วย C# พร้อมโค้ดจริง.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: th
og_description: แปลง worksheet เป็น DataTable ใน C# อย่างรวดเร็ว บทเรียนนี้จะแสดงวิธีอ่านไฟล์
  Excel ไปยัง DataTable ด้วย C# และส่งออก Excel ไปยัง DataTable ด้วย C# พร้อมตัวอย่างเต็ม
og_title: แปลง Worksheet เป็น DataTable ใน C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: แปลง Worksheet เป็น DataTable ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง Worksheet เป็น DataTable ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้อง **แปลง worksheet เป็น DataTable** แต่ไม่แน่ใจว่าจะเรียก API ไหนใช่ไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องทำอัตโนมัติรายงานหรือดึงข้อมูล Excel เข้าไปในฐานข้อมูล ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# คุณก็สามารถอ่านไฟล์ Excel ไปยัง `DataTable` แล้วพร้อมทำ LINQ query, bulk insert หรืออะไรก็ตามที่ตามมา

ในคู่มือนี้เราจะพาคุณผ่านการโหลด Excel workbook, ดึงแผ่นแรก, และ **export excel to DataTable C#** อย่างไม่มีเวทมนตร์ เพียงโค้ดที่ชัดเจนเท่านั้น สุดท้ายคุณจะได้เมธอดที่นำ worksheet ใดก็ได้มาเป็น `DataTable` ที่มีชนิดข้อมูลครบถ้วน (และใช่ เราจะครอบคลุมสถานการณ์ “read Excel file into DataTable C#” สำหรับผู้ที่ต้องการบรรทัดเดียว)

## ข้อกำหนดเบื้องต้น – สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก ตรวจสอบให้แน่ใจว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานบน .NET Framework 4.6+ ด้วย)
- การอ้างอิงถึง **Aspose.Cells** (หรือไลบรารีอื่นที่มี `ExportDataTable`; ตัวอย่างใช้ Aspose เพราะใช้งานง่าย)
- ไฟล์ Excel (`.xlsx`) ที่ต้องการประมวลผล
- IDE C# เบื้องต้น (Visual Studio, Rider, หรือ VS Code)

เท่านี้—ไม่มีแพ็กเกจ NuGet เพิ่มเติมนอกจากไลบรารี Excel เอง พร้อมหรือยัง? ไปกันเลย

## ขั้นตอนที่ 1: โหลด Excel Workbook C# – นำไฟล์เข้าสู่หน่วยความจำ

อย่างแรกที่ต้องทำคือ **load excel workbook c#** เรามอง workbook เป็นภาชนะที่บรรจุ worksheet, style, และ metadata การเปิดอย่างถูกต้องทำให้เราไม่ล็อกไฟล์หรือรั่วทรัพยากร

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** คลาส `Workbook` จัดการรูปแบบไฟล์ระดับต่ำให้คุณ ไม่ต้องพาร์ส XML ด้วยตนเอง อีกทั้งจะทำการ dispose สตรีมพื้นฐานเมื่อออบเจ็กต์ออกจากสโคป ป้องกันข้อผิดพลาดไฟล์กำลังใช้งาน

### เคล็ดลับ
หากต้องจัดการกับสเปรดชีตขนาดใหญ่ ให้พิจารณาใช้ `LoadOptions` เพื่อเปิด **memory‑optimized loading**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## ขั้นตอนที่ 2: เข้าถึง Worksheet ที่ต้องการ – ส่วนใหญ่คือแผ่นแรก

สคริปต์เริ่มต้นส่วนใหญ่จะดึงแผ่นแรก แต่คุณก็เลือกได้ตามชื่อหรือดัชนี นี่คือตัวอย่าง “worksheet แรก” ที่ครอบคลุมกรณี **convert worksheet to DataTable** สำหรับไฟล์ง่าย ๆ

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **กรณีขอบ:** หาก workbook ของคุณมีแผ่นซ่อนหรือคุณต้องการแท็บเฉพาะ ให้แทนค่า `0` ด้วย `workbook.Worksheets["MySheet"]`

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการส่งออก – Export As String เพื่อให้ชนิดข้อมูลคาดเดาได้

เมื่อแปลงเป็น `DataTable` คุณมักต้องการให้ทุกเซลล์เป็นสตริงเพื่อหลีกเลี่ยงปัญหาการแปลงชนิดข้อมูลต่อมา นี่คือสิ่งที่ **export excel to datatable c#** ทำ

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

ทำไมต้องบังคับเป็นสตริง? เพราะเซลล์ Excel อาจเป็นวันที่, ตัวเลข, หรือสูตร การส่งออกทั้งหมดเป็นข้อความช่วยหลีกเลี่ยงคอลัมน์ที่ชนิดไม่ตรงกันเมื่อคุณนำข้อมูลเข้า SQL table

## ขั้นตอนที่ 4: ทำการส่งออก – โลจิกหลักของ Convert Worksheet to DataTable

ตอนนี้จุดสำคัญเกิดขึ้น เราเรียก `ExportDataTable` บนออบเจ็กต์ `Worksheet` พร้อมพารามิเตอร์แถว/คอลัมน์เริ่มต้น, จำนวนแถว/คอลัมน์, ธงรวมหัวคอลัมน์, และตัวเลือกของเรา

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### สิ่งที่คุณจะได้
`dataTable` ตอนนี้สะท้อน worksheet:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

ค่าทั้งหมดเป็นสตริง ทำให้การประมวลผลต่อไปคาดเดาได้

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ – ตรวจสอบอย่างรวดเร็ว (read excel file into datatable c#)

วิธีเร็ว ๆ เพื่อยืนยันว่าการแปลงสำเร็จคือการพิมพ์แถวแรก ๆ ไปที่คอนโซล ซึ่งยังแสดงรูปแบบ **read excel file into datatable c#** ในการทำงานจริง

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

หากคุณเห็นค่าที่คั่นด้วย pipe ตามที่คาดหวัง แสดงว่าคุณได้ **convert worksheet to DataTable** สำเร็จแล้ว

## ขั้นตอนที่ 6: สรุป – เมธอดช่วยเหลือที่ใช้ซ้ำได้

โปรเจคส่วนใหญ่ต้องการการแปลงนี้หลายที่ ดังนั้นเราจะบรรจุทุกอย่างไว้ในเมธอดสเตติกเดียว ทำให้การเรียก **read excel file into datatable c#** ง่ายเหมือนบรรทัดเดียว

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

ตัวอย่างการใช้งาน:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

นี่คือทั้งหมด—ไม่มีลูปเพิ่ม, ไม่มี COM interop, เพียงข้อมูลที่สะอาดและมีชนิด

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|---------|----------------|-----|
| **ไฟล์ถูกล็อกโดยโปรเซสอื่น** | การเปิด workbook โดยไม่มี `LoadOptions` ทำให้แฮนด์เดิลไฟล์ค้างอยู่ | ใช้ `LoadOptions` กับ `MemorySetting.MemoryPreference` หรือห่อ `Workbook` ด้วยบล็อก `using` |
| **ไม่มีหัวคอลัมน์** | หากแถวแรกเป็นข้อมูลแทนหัว, `ExportDataTable` จะถือเป็นข้อมูล | ส่งค่า `false` ให้พารามิเตอร์ `includeColumnNames` แล้วเพิ่มชื่อคอลัมน์ด้วยตนเอง |
| **ชนิดข้อมูลผสมทำให้เกิดข้อยกเว้น** | เมื่อ `ExportAsString` เป็น `false` เซลล์ตัวเลขจะเป็น `double`, วันที่จะเป็น `DateTime` | คง `ExportAsString = true` เว้นแต่คุณต้องการชนิดที่เข้มงวด แล้วจัดการการแปลงด้วยตนเอง |
| **แผ่นขนาดใหญ่มากทำให้ OutOfMemory** | การส่งออกหลายล้านแถวพร้อมกันอาจทำให้ heap พุ่งขึ้น | ส่งออกเป็นชิ้นส่วน: ลูปตามบล็อกแถวแล้วต่อ `DataTable` เข้าด้วยกัน |

## โบนัส: ส่งออกหลายแผ่นพร้อมกัน

หากต้องการ **export excel to datatable c#** สำหรับทุกแผ่น เพียงวนลูป `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

ตอนนี้ `tables` จะเก็บ `DataTable` ต่อแผ่นโดยใช้ชื่อแผ่นเป็นคีย์—สะดวกสำหรับการนำเข้าแบบชุด

## สรุป

เราได้พาคุณจากไฟล์ Excel เปล่า ไปสู่ `DataTable` ที่เต็มรูปแบบด้วย workflow **convert worksheet to DataTable** ที่กระชับ ขั้นตอนที่ครอบคลุมการโหลด workbook, เลือกแผ่น, ตั้งค่าตัวเลือกการส่งออก, และสุดท้ายดึงข้อมูลเข้าสู่ `DataTable` ด้วยเมธอดช่วยเหลือที่ใช้ซ้ำได้ ตอนนี้คุณสามารถ **read excel file into datatable c#** ได้ทุกที่ในโค้ดของคุณ และยังมีรูปแบบ **export excel to datatable c#** สำหรับหลายแผ่นอีกด้วย

ต่อไปทำอะไร? ลองนำ `DataTable` ที่ได้ไปใช้กับ `BulkInsert` ของ Entity Framework, สร้างรายงาน CSV, หรือใช้ LINQ filter เพื่อสกัดข้อมูลเชิงลึก ไม่จำกัดอะไรเลยเมื่อข้อมูล Excel ของคุณอยู่ในหน่วยความจำเป็นตารางที่แท้จริง

มีคำถามหรือไฟล์ Excel ที่ซับซ้อนจนแก้ไม่ได้? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจคของคุณ

- [วิธีนำเข้า DataTable ไปยัง Excel ด้วย Aspose.Cells สำหรับ .NET (คู่มือขั้นตอน) ](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [ส่งออกข้อมูล Excel ไปยัง DataTable ด้วย Aspose.Cells สำหรับ .NET: คู่มือฉบับสมบูรณ์](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [ส่งออก HTML Strings จาก Excel ไปยัง DataTable ด้วย Aspose.Cells สำหรับ .NET: คู่มือขั้นตอน](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}