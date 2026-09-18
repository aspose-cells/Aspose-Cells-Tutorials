---
category: general
date: 2026-03-21
description: ส่งออกตารางข้อมูล Excel ไปยัง DataTable พร้อมหัวตาราง, จำกัดจำนวนตำแหน่งทศนิยม,
  และส่งออก 100 แถวแรกโดยใช้ Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: th
og_description: เรียนรู้วิธีส่งออกตารางข้อมูล Excel ไปยัง DataTable รักษาแถวหัวตาราง
  จำกัดจำนวนทศนิยม และดึง 100 แถวแรกใน C#
og_title: ส่งออกตารางข้อมูล Excel ใน C# – คู่มือแบบทีละขั้นตอน
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: ส่งออกตารางข้อมูล Excel ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกตารางข้อมูล Excel – คู่มือเต็ม C#

ต้องการ **export excel data table** จาก workbook ไปยัง .NET `DataTable` หรือไม่? คุณมาถูกที่แล้ว—คู่มือนี้จะแสดงวิธีทำอย่างละเอียด รักษาชื่อคอลัมน์, จำกัดจำนวนตำแหน่งทศนิยม, และดึงเฉพาะ 100 แถวแรกเท่านั้น  

ถ้าคุณเคยมองตารางสเปรดชีตแล้วคิดว่า “จะเอาข้อมูลนี้เข้าแอปโดยไม่เสียรูปแบบได้อย่างไร?” คุณไม่ได้อยู่คนเดียว ในไม่กี่นาทีต่อไปเราจะเปลี่ยน “ถ้าอย่างนั้น” ให้เป็นวิธีแก้ปัญหาที่คัดลอก‑วางได้ ทำงานร่วมกับ Aspose.Cells ซึ่งเป็นไลบรารียอดนิยมสำหรับการจัดการ Excel

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **export excel to datatable** โดยใช้เมธอด `ExportDataTable`  
- วิธีเก็บชื่อคอลัมน์เดิม (`export excel with headers`)  
- วิธี **limit decimal places excel** ค่าโดยการกำหนดค่า `ExportTableOptions`  
- วิธีดึงเฉพาะแถวบนสุด 100 แถวอย่างปลอดภัย (`export first 100 rows`)  

ไม่มีสคริปต์ภายนอก ไม่มีสตริงวิเศษ—เพียง C# ธรรมดาที่คุณสามารถนำไปใส่ในโปรเจค .NET ใดก็ได้

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | ทำไมจึงสำคัญ |
|-------------|----------------|
| .NET 6 หรือรุ่นต่อไป (หรือ .NET Framework 4.7+) | Aspose.Cells รองรับทั้งสอง แต่ runtime ที่ใหม่กว่าให้ API ที่พร้อมใช้งานแบบ async |
| Aspose.Cells for .NET NuGet package | ให้ `Workbook`, `ExportTableOptions`, และตัวช่วย `ExportDataTable` |
| ตัวอย่างไฟล์ Excel (เช่น `Numbers.xlsx`) | เป็นแหล่งข้อมูลที่คุณจะส่งออก |
| ความรู้พื้นฐาน C# | คุณจะทำตามตัวอย่างโค้ด แต่ไม่จำเป็นต้องมีความรู้ขั้นสูง |

หากส่วนใดส่วนหนึ่งฟังดูแปลกใหม่ ให้ติดตั้งแพคเกจ NuGet ด้วย `dotnet add package Aspose.Cells` แล้วสร้างไฟล์ Excel เล็ก ๆ ที่มีตัวเลขสองสามค่า—เป็นข้อมูลทดสอบของคุณ

![export excel data table example](excel-data-table.png "Screenshot of an Excel sheet that will be exported to a DataTable")

## ขั้นตอนที่ 1: โหลด Workbook (export excel data table)

สิ่งแรกที่คุณต้องมีคืออินสแตนซ์ `Workbook` ที่ชี้ไปยังไฟล์ Excel ของคุณ คิดว่าเป็นการเปิดหนังสือก่อนจะอ่านบทใดบทหนึ่ง

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **ทำไมสิ่งนี้ถึงสำคัญ:** การโหลด workbook ทำให้คุณเข้าถึง worksheet, cell, และ style ต่าง ๆ หากเส้นทางไฟล์ผิด Aspose จะโยน `FileNotFoundException` ดังนั้นตรวจสอบตำแหน่งไฟล์ให้แน่ใจ

## ขั้นตอนที่ 2: กำหนดค่าตัวเลือกการส่งออก – limit decimal places excel

โดยค่าเริ่มต้น Aspose จะส่งออกค่าตัวเลขทุกค่าด้วยความแม่นยำเต็มรูปแบบ บ่อยครั้งที่คุณต้องการเพียงไม่กี่หลักสำคัญ โดยเฉพาะเมื่อส่งข้อมูลไปยัง UI grid หรือ API ที่คาดหวังตัวเลขที่ปัดเศษแล้ว

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **เคล็ดลับ:** หากต้องการกลยุทธ์การปัดเศษที่ต่างออกไป (เช่น ปัดขึ้นเสมอ) คุณสามารถทำ post‑process `DataTable` หลังการส่งออกได้ การตั้งค่า `SignificantDigits` เป็นวิธีที่เร็วที่สุดในการ **limit decimal places excel** โดยไม่ต้องเขียนลูปเพิ่ม

## ขั้นตอนที่ 3: ส่งออกช่วงที่ต้องการ (export first 100 rows)

ตอนนี้เราบอก Aspose ว่าเราต้องการดึงบล็อกเซลล์ใดเข้าสู่ `DataTable` ในบทเรียนนี้เราจะดึง 100 แถวแรกและ 10 คอลัมน์แรก แต่คุณสามารถปรับตัวเลขเหล่านี้ให้ตรงกับกรณีของคุณได้

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **กรณีขอบเขต:** หากชีตมีแถวน้อยกว่า 100 แถว Aspose จะส่งออกเฉพาะที่มีอยู่โดยไม่เกิดข้อผิดพลาด อย่างไรก็ตามคุณอาจต้องการตรวจสอบเพื่อป้องกันช่วงที่คาดไม่ถึงเล็กเกินไป:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ – แสดงผลสั้นใน Console

การดูข้อมูลใน debugger นั้นดี แต่การพิมพ์ไม่กี่แถวลง console จะยืนยันว่า **export excel to datatable** ทำงานสำเร็จและตำแหน่งทศนิยมถูกตัดแล้ว

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### ผลลัพธ์ที่คาดหวัง

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

สังเกตว่าคอลัมน์ตัวเลขตอนนี้แสดงเพียงสี่หลักสำคัญเท่านั้น ตรงกับการตั้งค่า `SignificantDigits = 4` ที่เราใช้เมื่อตั้งค่าในขั้นตอนก่อนหน้า

## ขั้นตอนที่ 5: สรุปทั้งหมด – ตัวอย่างที่ทำงานได้เต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในแอป console ได้ รวมถึงการจัดการข้อผิดพลาด, ตัวตรวจสอบจำนวนแถวแบบเลือกใช้, และเมธอดช่วยพิมพ์ผลลัพธ์

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

รันโปรแกรมแล้วคุณจะเห็น 100 แถวแรกของชีตของคุณ ปัดเศษอย่างสวยงาม พร้อมชื่อคอลัมน์ที่คงอยู่

## คำถามที่พบบ่อย & ข้อควรระวัง

| คำถาม | คำตอบ |
|----------|--------|
| **What if my sheet has merged cells?** | `ExportDataTable` จะทำให้เซลล์ที่รวมกันกลายเป็นค่าเดียวโดยใช้ค่าจากเซลล์บน‑ซ้าย หากต้องการการจัดการแบบกำหนดเอง ให้ยกเลิกการรวมเซลล์ก่อนหรืออ่านอ็อบเจ็กต์ `Cell` ดิบ |
| **Can I export to a `DataSet` instead?** | ใช่—ใช้ `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}