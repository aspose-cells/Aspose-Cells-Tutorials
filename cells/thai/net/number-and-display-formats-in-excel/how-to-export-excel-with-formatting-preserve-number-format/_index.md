---
category: general
date: 2026-03-22
description: วิธีส่งออก Excel พร้อมการจัดรูปแบบและคงรูปแบบตัวเลขไว้ เรียนรู้การแปลงช่วงของ
  Excel, การดึงผลลัพธ์สูตร, และการส่งออก Excel พร้อมการจัดรูปแบบโดยใช้ Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: th
og_description: วิธีส่งออก Excel พร้อมการจัดรูปแบบและรักษารูปแบบตัวเลขไว้ ขั้นตอนโดยละเอียดในการแปลงช่วง
  Excel, รับผลลัพธ์สูตร, และส่งออก Excel พร้อมการจัดรูปแบบใน C#
og_title: วิธีส่งออก Excel พร้อมการจัดรูปแบบ – รักษารูปแบบตัวเลข
tags:
- C#
- Aspose.Cells
- Excel automation
title: วิธีส่งออก Excel พร้อมการจัดรูปแบบ – รักษารูปแบบตัวเลข
url: /th/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออก Excel พร้อมการจัดรูปแบบ – รักษารูปแบบตัวเลข

เคยสงสัย **วิธีการส่งออก Excel** ข้อมูลโดยคงลักษณะของแต่ละเซลล์ให้เหมือนกับที่เห็นในเวิร์กบุ๊กหรือไม่? บางครั้งคุณอาจต้องส่งรายงานให้ลูกค้า, เติมข้อมูลให้กับคอนโทรลกริด, หรือเพียงแค่เก็บค่าลงฐานข้อมูล จุดอ่อนที่มักเจอคือการสูญเสียการจัดรูปแบบตัวเลขหรือสูตรที่กลายเป็นสตริงธรรมดา  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่าง C# ที่พร้อมรันเต็มรูปแบบซึ่ง **รักษารูปแบบตัวเลข**, **แปลงช่วง Excel** เป็น `DataTable`, **ดึงผลลัพธ์สูตร**, และสุดท้าย **ส่งออก Excel พร้อมการจัดรูปแบบ** ด้วย Aspose.Cells. เมื่อจบคุณจะได้เมธอดเดียวที่สามารถนำไปใส่ในโปรเจกต์ใดก็ได้และเรียกใช้ด้วยอ้างอิงเวิร์กชีต

> **ตัวอย่างสั้น:** โค้ดจะสร้างเวิร์กบุ๊ก, เขียนค่าพร้อมสูตร, บอก Aspose.Cells ให้ส่งออกเซลล์เป็นสตริงที่จัดรูปแบบแล้ว, และพิมพ์ `123.456 | 246.912` – ตรงกับที่คุณคาดว่าจะเห็นใน Excel

---

## สิ่งที่คุณต้องการ

- **Aspose.Cells for .NET** (เวอร์ชันทดลองฟรีก็ใช้ได้สำหรับการเรียน)
- .NET 6.0 หรือใหม่กว่า (API เหมือนกันบน .NET Framework)
- สภาพแวดล้อมการพัฒนา C# เบื้องต้น (Visual Studio, VS Code, Rider… เลือกตามใจ)

ไม่ต้องใช้แพ็กเกจ NuGet เพิ่มเติมนอกจาก Aspose.Cells หากคุณยังไม่ได้ติดตั้ง ให้รัน:

```bash
dotnet add package Aspose.Cells
```

---

## ขั้นตอนที่ 1 – สร้าง Workbook และเขียนค่า (รวมสูตร)

แรกเราจะสร้างเวิร์กบุ๊กใหม่และใส่ค่าตัวเลขลงใน **A1** จากนั้นเพิ่มสูตรง่าย ๆ ใน **B1** ที่คูณค่าจากเซลล์แรกสองเท่า เพื่อเตรียมการสาธิต **ดึงผลลัพธ์สูตร** ในขั้นต่อไป

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
- `PutValue` จะเก็บตัวเลขดิบ, ส่วน `PutFormula` จะเก็บสูตรคำนวณ  
- Aspose.Cells จะคงสูตร **ให้ทำงานอยู่**, ดังนั้นเมื่อเราถามค่าของเซลล์ภายหลัง เราจะได้ `246.912` จริง ๆ ไม่ใช่สตริง `"=A1*2"`

---

## ขั้นตอนที่ 2 – บอก Aspose.Cells ให้ส่งออกค่าเป็นสตริงที่จัดรูปแบบแล้ว

หากคุณเรียก `ExportDataTable` ด้วยการตั้งค่าเริ่มต้น เซลล์ตัวเลขจะถูกส่งกลับเป็นค่า `double` ดิบ ซึ่งจะลบเครื่องหมายคั่นหลักพัน, สัญลักษณ์สกุลเงิน, หรือตำแหน่งทศนิยมที่คุณตั้งไว้ `ExportTableOptions` ช่วยให้เราสามารถ **รักษารูปแบบตัวเลข** และ **ส่งออกเป็นสตริง** ได้

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**จุดสำคัญ:** `ExportNumberFormat = true` คือค่าสถานะที่ทำให้ **รักษารูปแบบตัวเลข** ทำงาน หากไม่ได้ตั้งค่านี้ คุณจะเห็น `"123.456"` และ `"246.912"` เป็นตัวเลขดิบ ซึ่งอาจดูโอเคในโค้ดแต่ไม่ตรงกับการวางข้อมูลลง UI ที่ต้องการรูปแบบเดียวกับ Excel

---

## ขั้นตอนที่ 3 – พิมพ์ข้อมูลที่ส่งออก (ตรวจสอบ)

ตอนนี้เรามี `DataTable` ที่เต็มไปด้วยสตริงที่จัดรูปแบบแล้ว, ให้เราดึงข้อมูลออกมาพิมพ์ที่คอนโซล นอกจากนี้ยังแสดงให้เห็นว่าเรา **ดึงผลลัพธ์สูตร** ได้สำเร็จโดยไม่ต้องคำนวณสูตรด้วยตนเอง

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

การรันโปรแกรมจะพิมพ์:

```
123.456 | 246.912
```

สังเกตว่าคอลัมน์ที่สองแสดง **ผลลัพธ์สูตร**, ไม่ใช่ข้อความสูตร นี่คือสิ่งที่คุณต้องการเมื่อ **ส่งออก Excel พร้อมการจัดรูปแบบ** เพื่อการประมวลผลต่อไป

---

## ขั้นตอนที่ 4 – แปลงช่วง Excel ขนาดใหญ่ (ทางเลือก)

ตัวอย่างข้างต้นจัดการกับส่วน `A1:B1` เล็ก ๆ เท่านั้น, แต่ในสถานการณ์จริงมักต้องส่งออกตารางเต็มรูปแบบ วิธีเดียวกันทำงานกับบล็อกสี่เหลี่ยมใด ๆ – เพียงปรับค่า `firstRow`, `firstColumn`, `totalRows`, และ `totalColumns` ให้ตรงกับช่วงของคุณ

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**เคล็ดลับ:** หากแผ่นของคุณมีแถวหัวตารางอยู่แล้ว, ตั้งค่า `includeColumnNames` เป็น `true`. Aspose.Cells จะใช้แถวแรกของช่วงเป็นชื่อคอลัมน์, ซึ่งสะดวกเมื่อคุณต้องผูก `DataTable` กับกริด UI ต่อไป

---

## ขั้นตอนที่ 5 – ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Numbers lose commas or currency symbols** | `ExportAsString` เป็น `false` หรือไม่ได้ตั้งค่า `ExportNumberFormat` | ตั้งค่า `ExportAsString = true` **และ** `ExportNumberFormat = true` |
| **Formula cells return the formula text** | ไม่ได้เรียก `CalculateFormula` ก่อนส่งออก (จำเป็นเฉพาะเมื่อเวิร์กบุ๊กไม่ได้ตั้งค่า auto‑calculate) | เปิดใช้งาน auto‑calculate (`workbook.CalculateFormula()`) หรือใช้ `ExportAsString` ที่บังคับให้ประเมินสูตร |
| **Headers appear as data rows** | `includeColumnNames` ตั้งเป็น `false` แต่ช่วงของคุณมีแถวหัวตาราง | ตั้งค่า `includeColumnNames = true` เพื่อให้แถวแรกเป็นชื่อคอลัมน์ |
| **Large ranges cause memory pressure** | การส่งออกทั้งชีตในครั้งเดียวทำให้โหลดข้อมูลทั้งหมดเข้าสู่หน่วยความจำ | ส่งออกเป็นชิ้นย่อย (เช่น 500 แถวต่อครั้ง) แล้วรวม `DataTable` หากจำเป็น |

---

## ขั้นตอนที่ 6 – ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมด ตั้งแต่ `using` จนถึง `Main`. คัดลอกไปใส่ในแอปคอนโซลและกด **F5** – คุณจะเห็นผลลัพธ์ที่จัดรูปแบบทันที

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

```
123.456 | 246.912

Press any key to exit...
```

นี่คือขั้นตอน **วิธีส่งออก Excel** ทั้งหมด, รักษาการจัดรูปแบบ, ประเมินผลลัพธ์สูตร, และได้ `DataTable` ที่พร้อมใช้ใน .NET ใด ๆ

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องรู้เกี่ยวกับ **วิธีการส่งออก Excel** ขณะ **รักษารูปแบบตัวเลข**, **แปลงช่วง Excel** เป็น `DataTable`, และ **ดึงผลลัพธ์สูตร** โดยไม่ต้องทำการพาร์สเพิ่มเติม. กุญแจสำคัญคือการตั้งค่า `ExportTableOptions` – เพียงตั้งค่า `ExportAsString` และ `ExportNumberFormat` เป็น `true`, Aspose.Cells จะทำงานหนักให้คุณ

ต่อจากนี้คุณสามารถ:

- ผูก `DataTable` ไปยัง `DataGrid` ของ WPF หรือมุมมอง ASP.NET MVC
- เขียนตารางเป็นไฟล์ CSV พร้อมคงรูปแบบที่มองเห็นได้
- ขยายวิธีนี้ไปยังหลายชีตหรือช่วงไดนามิก

ลองเล่นกับรูปแบบต่าง ๆ (สกุลเงิน, เปอร์เซ็นต์) และบล็อกข้อมูลขนาดใหญ่ หากเจอข้อผิดพลาดใด ๆ ให้กลับไปดูตาราง **ข้อผิดพลาดทั่วไป** – มันครอบคลุมปัญหาที่พบบ่อยที่สุดเมื่อ **ส่งออก Excel พร้อมการจัดรูปแบบ**

ขอให้เขียนโค้ดสนุกและสเปรดชีตที่ส่งออกออกมาดูดีเท่าต้นฉบับเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}