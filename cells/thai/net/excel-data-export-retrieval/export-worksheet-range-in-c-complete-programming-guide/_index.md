---
category: general
date: 2026-05-04
description: ส่งออกช่วงข้อมูลในแผ่นงานโดยใช้ C# พร้อมการจัดรูปแบบแบบกำหนดเอง เรียนรู้วิธีส่งออกช่วง
  Excel และวิธีปรับแต่งการส่งออกเซลล์ในไม่กี่ขั้นตอนง่าย ๆ
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: th
og_description: ส่งออกช่วงแผ่นงานด้วย C#. คู่มือนี้แสดงวิธีส่งออกช่วงของ Excel และปรับแต่งการส่งออกเซลล์อย่างรวดเร็วและเชื่อถือได้.
og_title: ส่งออกช่วงแผ่นงานใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
tags:
- C#
- Excel
- Data Export
title: ส่งออกช่วงแผ่นงานใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกช่วงแผ่นงานใน C# – คู่มือการเขียนโปรแกรมเต็มรูปแบบ

เคยต้องการ **export worksheet range** แต่ผลลัพธ์เริ่มต้นไม่ตรงกับที่คุณต้องการหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องดึงบล็อกของเซลล์ไปยังไฟล์ CSV หรือ JSON ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# คุณสามารถ **export excel range** ได้ไม่เพียงเท่านั้น ยังสามารถ **customize cell export** ให้ตรงกับรูปแบบใด ๆ ที่ต้องการต่อไป

ในบทเรียนนี้เราจะเดินผ่านสถานการณ์จริง: ดึงเซลล์ *A1:D10* จากไฟล์ Excel, แปลงค่าทุกค่าให้เป็นสตริงในวงเล็บ, แล้วเขียนผลลัพธ์ลงไฟล์ สุดท้ายคุณจะรู้ **how to export worksheet range** อย่างแม่นยำพร้อมการควบคุมเต็มที่ต่อการแสดงผลของแต่ละเซลล์ พร้อมเคล็ดลับสำหรับกรณีขอบที่อาจเจอในภายหลัง

## สิ่งที่คุณต้องเตรียม

- .NET 6 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework 4.7+ ด้วย)  
- แพคเกจ NuGet **GemBox.Spreadsheet** (หรือไลบรารีใด ๆ ที่มี `ExportTableOptions`; API ที่แสดงมาจาก GemBox)  
- ความเข้าใจพื้นฐานของไวยากรณ์ C# – ไม่ต้องซับซ้อน เพียงแค่คำสั่ง `using` ปกติและการสร้างอ็อบเจ็กต์  

ถ้าคุณมีทั้งหมดนี้แล้ว คุณพร้อมจะลงมือแล้ว

## ขั้นตอนที่ 1: ตั้งค่า Export Options – จุดควบคุมหลัก  

สิ่งแรกที่ทำคือสร้างอินสแตนซ์ `ExportTableOptions` แล้วบอกให้จัดการทุกเซลล์เป็นสตริง นี่คือพื้นฐานสำหรับ **how to export excel range** พร้อมคงประเภทข้อมูลให้สอดคล้องกัน

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*ทำไมต้องบังคับให้ส่งออกเป็นสตริง?*  
เมื่อคุณปรับแต่งแต่ละเซลล์ต่อไป คุณจะใส่วงเล็บหรือสัญลักษณ์อื่น ๆ การเก็บทุกอย่างเป็นสตริงจะป้องกันการแปลงประเภทโดยไม่คาดคิด (เช่น วันที่แปลงเป็นเลขซีเรียล)

## ขั้นตอนที่ 2: ผูกกับเหตุการณ์ CellExport – ปรับแต่งแต่ละเซลล์  

ต่อมาคือส่วนสนุก: **how to customize cell export** GemBox จะปล่อยเหตุการณ์ `CellExport` สำหรับทุกเซลล์ที่กำลังจะถูกเขียน การจัดการเหตุการณ์นี้ทำให้คุณสามารถใส่วงเล็บ, เพิ่มคำนำหน้า, หรือแม้แต่ข้ามเซลล์ได้ทั้งหมด

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*เคล็ดลับ:* หากคุณต้องการแก้ไขเฉพาะเซลล์ตัวเลข ให้ตรวจสอบ `e.Value.GetType()` ก่อนใส่วงเล็บ การตรวจสอบเล็ก ๆ นี้จะช่วยป้องกันการทำลายข้อความหัวตารางโดยไม่ได้ตั้งใจ

## ขั้นตอนที่ 3: ส่งออกช่วงที่ต้องการ – การทำงานหลัก  

เมื่อกำหนดตัวเลือกเรียบร้อยแล้ว ให้เรียก `ExportTable` เมธอดนี้รับเวิร์กบุ๊กที่โหลดไว้, ที่อยู่ของช่วงที่ต้องการ, และตัวเลือกที่คุณตั้งค่าไว้

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

โอเวอร์โหลดที่เราใช้จะเขียนโดยตรงไปยังไฟล์ (ค่าเริ่มต้นเป็น CSV) หากคุณต้องการสตริงในหน่วยความจำ ให้เปลี่ยนอาร์กิวเมนต์สุดท้ายเป็น `StringWriter` แล้วอ่านผลลัพธ์ต่อไป

### ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นแอปคอนโซลที่สมบูรณ์ คุณสามารถคัดลอกไปยังโปรเจกต์ใหม่และรันได้ทันที (เพียงเปลี่ยนเส้นทางไฟล์)

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**ผลลัพธ์ที่คาดหวัง (ส่วนของ CSV):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

ทุกเซลล์จาก *A1* ถึง *D10* จะถูกใส่วงเล็บสี่เหลี่ยมตามที่เรากำหนดในตัวจัดการ `CellExport`

## การจัดการกรณีขอบทั่วไป  

### 1. เซลล์ว่าง  
หากเซลล์ว่าง `e.Value` จะเป็น `null` การพยายามฟอร์แมตด้วย string interpolation จะทำให้เกิดข้อยกเว้น ให้ตรวจสอบก่อน:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. ช่วงขนาดใหญ่  
การส่งออกหลายล้านแถวอาจทำให้หน่วยความจำเต็ม ในกรณีนั้นให้สตรีมผลลัพธ์แทนการโหลดเวิร์กบุ๊กทั้งหมดเข้าสู่หน่วยความจำ:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. ตัวคั่นที่แตกต่าง  
CSV ไม่ได้เป็นรูปแบบเดียวที่คุณอาจต้องการ ปรับตัวคั่นโดยแก้ไข `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## คำถามที่พบบ่อย  

**Q: Does this work with .xlsx files created by Excel 365?**  
Absolutely. GemBox reads the modern OpenXML format without extra configuration.

**Q: Can I export multiple non‑contiguous ranges at once?**  
Not directly via a single `ExportTable` call. Loop over each range string (`"A1:D10"`, `"F1:H5"` etc.) and concatenate the outputs yourself.

**Q: What if I need to apply different formatting per column?**  
Inside the `CellExport` handler you have access to `e.ColumnIndex`. Use a `switch` statement to apply column‑specific logic.

## สรุป  

เราได้อธิบาย **how to export worksheet range** พร้อมการควบคุมเต็มที่ต่อการแสดงผลของแต่ละเซลล์, แสดง **how to export excel range** ด้วย `ExportTableOptions`, และแสดง **how to customize cell export** ผ่านเหตุการณ์ `CellExport` โซลูชันทั้งหมดอยู่ในไม่กี่สิบบรรทัดของ C# แต่ยืดหยุ่นพอสำหรับสถานการณ์ระดับผลิตภัณฑ์

ขั้นตอนต่อไป? ลองเปลี่ยนการใส่วงเล็บเป็นรูปแบบที่เป็นมิตรกับ JSON, หรือทดลองใช้ตรรกะเงื่อนไขที่ข้ามแถวที่ซ่อนอยู่ คุณอาจสำรวจการส่งออกโดยตรงไปยัง `MemoryStream` สำหรับการตอบสนองของเว็บ‑API — ไม่ต้องใช้ไฟล์ชั่วคราว

หากคุณทำตามขั้นตอนทั้งหมดแล้ว คุณจะมีแพทเทิร์นที่แข็งแรงและนำกลับมาใช้ใหม่ได้สำหรับการส่งออกช่วงแผ่นงานใด ๆ อย่างแม่นยำ Happy coding, and feel free to drop a comment if you hit a snag!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}