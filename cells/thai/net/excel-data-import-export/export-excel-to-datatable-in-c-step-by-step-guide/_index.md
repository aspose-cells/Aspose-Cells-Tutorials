---
category: general
date: 2026-03-25
description: เรียนรู้วิธีส่งออก Excel ไปยัง DataTable ใน C# อย่างรวดเร็ว บทเรียนนี้ครอบคลุมการส่งออก
  Excel พร้อมชื่อคอลัมน์และการส่งออกข้อมูล Excel เป็นสตริงเพื่อการจัดการข้อมูลที่เชื่อถือได้.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: th
og_description: ส่งออก Excel ไปยัง DataTable ใน C# พร้อมชื่อคอลัมน์และการแปลงเป็นสตริง — ติดตามบทแนะนำสั้น
  ๆ นี้เพื่อรับโซลูชันที่พร้อมใช้งาน.
og_title: ส่งออก Excel ไปยัง DataTable ใน C# – คู่มือครบถ้วน
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: ส่งออก Excel ไปยัง DataTable ใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออก Excel ไปยัง DataTable ใน C# – คู่มือขั้นตอนโดยละเอียด

เคยต้องการ **export Excel to DataTable** แต่ไม่แน่ใจว่าจะต้องตั้งค่าอะไรบ้าง? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อต้องดึงข้อมูลสเปรดชีตเข้าสู่ `DataTable`  

ข่าวดีคือ? ด้วยเพียงไม่กี่บรรทัดของโค้ดคุณสามารถ **export Excel with column names** และแม้กระทั่ง **export Excel data as string** เพื่อหลีกเลี่ยงปัญหา type‑mismatch ด้านล่างนี้คุณจะพบตัวอย่างที่ทำงานได้เต็มรูปแบบพร้อมคำอธิบาย “ทำไม” ของแต่ละการตั้งค่า เพื่อให้คุณปรับใช้กับโปรเจกต์ใดก็ได้โดยไม่ต้องเดา

## สิ่งที่บทเรียนนี้ครอบคลุม

* วิธีสร้าง workbook ในหน่วยความจำ (ไม่ต้องใช้ไฟล์จริง).
* เติมข้อมูลตัวอย่างหลายแถวเพื่อให้คุณเห็นผลลัพธ์ทันที.
* กำหนดค่า `ExportTableOptions` เพื่อให้ทุกเซลล์ถูกจัดการเป็น string.
* ส่งออกช่วงสี่เหลี่ยมมุมไปยัง `DataTable` พร้อมคงแถวแรกเป็นชื่อคอลัมน์.
* ตรวจสอบผลลัพธ์และพิมพ์แถวแรกไปยังคอนโซล.

ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่แล้ว หากคุณมีไฟล์ Excel อยู่บนดิสก์แล้ว เพียงเปลี่ยนบรรทัดการสร้าง workbook เป็น `new Workbook("path/to/file.xlsx")` แล้วคุณก็พร้อมใช้งาน

---

## ขั้นตอน 1: ตั้งค่าโปรเจกต์และเพิ่มแพ็กเกจ NuGet ของ Aspose.Cells

ก่อนที่เราจะเขียนโค้ดใด ๆ ตรวจสอบให้แน่ใจว่าโปรเจกต์ของคุณอ้างอิง **Aspose.Cells for .NET** (ไลบรารีที่ทำให้คลาส `Workbook` ทำงาน) คุณสามารถเพิ่มได้ผ่าน NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** ใช้เวอร์ชัน stable ล่าสุด (ณ มีนาคม 2026, คือ 22.12) เพื่อรับการแก้ไขบั๊กและปรับปรุงประสิทธิภาพล่าสุด.

---

## ขั้นตอน 2: สร้าง Workbook และเติมข้อมูลตัวอย่าง

เราจะเริ่มด้วย `Workbook` ใหม่สดและเขียนสองสามแถวเพื่อให้คุณเห็นการส่งออกทำงานจริง ขั้นตอนนี้ยังแสดง **how to export excel to datatable** เมื่อข้อมูลต้นทางอยู่ในหน่วยความจำเท่านั้น.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*ทำไมจึงสำคัญ:* โดยใส่แถวหัวตารางก่อน (`A1` & `B1`) เราสามารถบอกตัวส่งออกให้ถือแถวแรกเป็นชื่อคอลัมน์ได้—ซึ่งตรงกับความหมายของ **export excel with column names**.

---

## ขั้นตอน 3: บอก Aspose.Cells ให้ถือทุกเซลล์เป็น String

เมื่อคุณส่งออกเซลล์ที่เป็นตัวเลขหรือวันที่ Aspose จะพยายามสรุปประเภท .NET ซึ่งอาจทำให้เกิดบั๊กละเอียดอ่อนหากโค้ดต่อจากคุณคาดหวังเป็น string ธง `ExportTableOptions.ExportAsString` จะบังคับให้แปลงเป็น string อย่างสม่ำเสมอ.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*ทำไมต้องใช้วิธีนี้?* ลองนึกถึงคอลัมน์ที่บางครั้งมีตัวเลขและบางครั้งมีข้อความ (เช่น “00123” กับ “ABC”) การส่งออกทุกอย่างเป็น string จะช่วยหลีกเลี่ยงการสูญเสียศูนย์นำหน้า หรือข้อยกเว้นจากการแปลงประเภท.

---

## ขั้นตอน 4: ส่งออกช่วงที่ต้องการไปยัง DataTable

ตอนนี้เราจริง ๆ **export excel to datatable** เมธอด `ExportDataTable` รับพารามิเตอร์แถว/คอลัมน์เริ่มต้น จำนวนแถว/คอลัมน์ ธงสำหรับดึงชื่อคอลัมน์ และตัวเลือกที่เราสร้างไว้.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*อะไรที่เกิดขึ้นเบื้องหลัง?*  
- `startRow: 0` ชี้ไปที่แถวแรกของ Excel (แถวหัวตาราง).  
- `exportColumnNames: true` บอก Aspose ให้ยก “Name” และ “Age” ไปยังคอลเลกชันคอลัมน์ของ `DataTable`.  
- `totalRows`/`totalColumns` สามารถใหญ่กว่าข้อมูลจริง; เซลล์ส่วนเกินจะกลายเป็นสตริงว่างเนื่องจาก `ExportAsString`.

---

## ขั้นตอน 5: ตรวจสอบผลลัพธ์ – พิมพ์แถวแรก

การพิมพ์ผลลัพธ์สั้น ๆ ที่คอนโซลยืนยันว่าการแปลงสำเร็จและชื่อคอลัมน์ยังคงอยู่.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Expected output**

```
First row: Alice, 30
```

หากคุณเปลี่ยนข้อมูลตัวอย่าง คอนโซลจะแสดงการเปลี่ยนแปลงนั้นโดยอัตโนมัติ—ไม่ต้องเขียนโค้ดเพิ่มเติม.

---

## คำถามที่พบบ่อย & กรณีขอบ

| Question | Answer |
|----------|--------|
| **ฉันสามารถส่งออกชีตที่มีอยู่แล้วบนดิสก์ได้หรือไม่?** | ได้—เปลี่ยน `new Workbook()` เป็น `new Workbook("myFile.xlsx")`. ขั้นตอนที่เหลือเหมือนเดิม. |
| **ถ้าไฟล์ Excel ของฉันมีเซลล์ที่รวมกันล่ะ?** | เซลล์ที่รวมกันจะถูกแยก; ค่าของเซลล์ซ้ายบนจะใช้สำหรับช่วงที่รวมทั้งหมด. |
| **ฉันต้องกังวลเรื่องรูปแบบตัวเลขตามวัฒนธรรมหรือไม่?** | ไม่ต้องเมื่อ `ExportAsString = true`; ทุกอย่างจะมาถึงเป็นสตริงดิบที่แสดงใน Excel. |
| **ฉันสามารถส่งออกแถวได้กี่แถวต่อครั้ง?** | Aspose.Cells สามารถจัดการได้หลายล้านแถว, แต่การใช้หน่วยความจำจะเพิ่มตามขนาดของ `DataTable`. ควรพิจารณาแบ่งหน้า (paging) หากถึงขีดจำกัด. |
| **แล้วคอลัมน์ที่ซ่อนล่ะ?** | คอลัมน์ที่ซ่อนจะถูกส่งออกเว้นแต่คุณตั้งค่า `ExportHiddenColumns = false` ใน `ExportTableOptions`. |

---

## โบนัส: ส่งออกเป็น CSV แทน DataTable

บางครั้งคุณอาจต้องการไฟล์แบนด์เดียว ตัวเลือก `ExportTableOptions` เดียวกันสามารถใช้ซ้ำกับ `ExportDataTableToCSV` ได้:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

บรรทัดเดียวนี้จะให้ไฟล์ CSV ที่พร้อมนำเข้าได้ในขณะที่ยังคง **exporting excel data as string**.

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

รันโปรแกรม (`dotnet run`) แล้วคุณจะเห็นผลลัพธ์ของ **export excel to datatable** ที่พิมพ์บนคอนโซล เปลี่ยนข้อมูลตัวอย่าง, ปรับ `totalRows`/`totalColumns`, หรือชี้ workbook ไปยังไฟล์จริง—ทุกอย่างจะปรับขนาดได้.

---

## สรุป

ตอนนี้คุณมี **โซลูชันครบถ้วนและอิสระสำหรับการส่งออก Excel ไปยัง DataTable** ใน C# แล้ว การกำหนดค่า `ExportTableOptions.ExportAsString` จะรับประกันว่า **export excel data as string**, และการตั้งค่า `exportColumnNames: true` จะทำให้คุณได้หัวคอลัมน์ที่คุ้นเคยเมื่อคุณ **export excel with column names**.  

- ส่ง `DataTable` ไปยัง Entity Framework หรือ Dapper เพื่อทำการแทรกแบบ bulk.  
- ส่งต่อไปยังเครื่องมือรายงานเช่น **FastReport** หรือ **RDLC**.  
- แปลงเป็น JSON สำหรับการตอบสนอง API (`JsonConvert.SerializeObject(table)`).  

ลองทดลองได้ตามใจ—อาจลองส่งออกชีตที่ใหญ่ขึ้น, หรือรวมกับ **how to export excel to datatable** จากแชร์เครือข่าย รูปแบบยังคงเหมือนเดิมและโค้ดพร้อมใช้ในโปรดักชัน.

![Diagram of Excel → DataTable conversion flow – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}