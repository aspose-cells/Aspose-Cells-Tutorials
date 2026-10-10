---
category: general
date: 2026-10-10
description: ปรับรูปแบบตัวเลขใน Excel อย่างรวดเร็วโดยการนำเข้า DataTable, ตั้งค่ารูปแบบวันที่และสกุลเงิน,
  และคงแถวหัวตารางไว้ในขั้นตอนเดียว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: th
lastmod: 2026-10-10
og_description: ใช้รูปแบบตัวเลขใน Excel ด้วย C# ผ่าน Aspose.Cells เรียนรู้การตั้งค่ารูปแบบวันที่ใน
  Excel, การตั้งค่ารูปแบบสกุลเงินใน Excel, และการคงแถวหัวเรื่องใน Excel เมื่อทำการนำเข้า
  DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: ใช้รูปแบบตัวเลขใน Excel ด้วย C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: วิธีการกำหนดรูปแบบตัวเลขใน Excel ด้วย Aspose.Cells
url: /th/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการกำหนดรูปแบบตัวเลขใน Excel ด้วย Aspose.Cells

หากคุณต้องการ **กำหนดรูปแบบตัวเลขใน Excel** ขณะโหลดข้อมูลจาก `DataTable` คู่มือนี้จะแสดงวิธีทำอย่างละเอียด คุณจะได้เรียนรู้วิธี **กำหนดรูปแบบวันที่ใน Excel**, **กำหนดรูปแบบสกุลเงินใน Excel**, และ **คงแถวหัวตารางใน Excel** ระหว่างการนำเข้า เพื่อให้เวิร์กชีตที่ได้ดูเป็นมืออาชีพโดยไม่ต้องทำการปรับแต่งเพิ่มเติมหลังจากนั้น

เราจะครอบคลุมทุกขั้นตอนตั้งแต่การติดตั้งไลบรารีจนถึงการเขียนโค้ดตัวอย่างที่ทำงานได้เต็มรูปแบบ เมื่อเสร็จสิ้นคุณจะสามารถนำเข้า `DataTable` ใด ๆ ไปยังเวิร์กบุ๊ก Excel, กำหนดรูปแบบคอลัมน์ตัวเลขโดยอัตโนมัติ, และคงแถวหัวตารางไว้โดยไม่เสียหาย—ทั้งหมดในไม่กี่บรรทัดของ C# เท่านั้น

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+ ด้วย)
* Visual Studio 2022 (หรือ IDE C# ใด ๆ ที่คุณชื่นชอบ)
* **Aspose.Cells for .NET** – ติดตั้งผ่าน NuGet:

```bash
dotnet add package Aspose.Cells
```

* แหล่งข้อมูล `DataTable` – ตัวอย่างใช้เมธอดช่วยเหลือ `GetTable()` ที่คืนค่าข้อมูลตัวอย่าง

> **เคล็ดลับ:** Aspose.Cells เป็นไลบรารีเชิงพาณิชย์ แต่มีโหมดประเมินผลฟรีที่ปิดการแสดงลายน้ำได้สูงสุด 30 วัน

## ขั้นตอนที่ 1: สร้างเวิร์กบุ๊กและเข้าถึงเวิร์กชีตแรก

อ็อบเจกต์เวิร์กบุ๊กเป็นจุดเริ่มต้นสำหรับการทำงานทั้งหมดใน Excel การสร้างเวิร์กบุ๊กใหม่จะให้เวิร์กชีตเริ่มต้นที่ตำแหน่ง index 0

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*ทำไมต้องทำขั้นตอนนี้?*  
`Workbook` จัดการรูปแบบไฟล์, เอนจิ้นการคำนวณ, และคลังสไตล์ การเข้าถึง `Worksheet` ตั้งแต่แรกทำให้เราสามารถส่งแผ่นเป้าหมายให้เมธอดนำเข้าภายหลังได้

## ขั้นตอนที่ 2: ดึงข้อมูลต้นทางเป็น DataTable

ในโครงการจริง ข้อมูลมักมาจากการคิวรีฐานข้อมูล, ตัวแปลง CSV, หรือการตอบสนองจาก API สำหรับการอธิบาย เราจะสร้าง `DataTable` ง่าย ๆ ที่มีสามคอลัมน์: **Product**, **Price**, และ **ReleaseDate**

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*ทำไมต้องทำขั้นตอนนี้?*  
`DataTable` ให้การแสดงผลแบบตารางในหน่วยความจำที่ Aspose.Cells สามารถนำเข้าโดยตรงได้ โดยคงลำดับคอลัมน์และประเภทข้อมูลไว้

## ขั้นตอนที่ 3: เตรียมอาเรย์ `Style` – สไตล์หนึ่งต่อคอลัมน์

Aspose.Cells ให้คุณกำหนดสไตล์ที่แตกต่างให้แต่ละคอลัมน์ระหว่างการนำเข้าโดยส่งอาเรย์ของอ็อบเจกต์ `Style` ความยาวของอาเรย์ต้องตรงกับจำนวนคอลัมน์ในตารางต้นทาง

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*ทำไมต้องทำขั้นตอนนี้?*  
หากข้ามการสร้างสไตล์โดยเจตนา (`CreateStyle()`), การตั้งค่า `Number` จะทำให้เกิด `NullReferenceException` การกำหนดค่า `Style` แต่ละตัวล่วงหน้าช่วยให้การกำหนดค่าต่อมาสำเร็จ

## ขั้นตอนที่ 4: กำหนดรูปแบบตัวเลข – สกุลเงินและวันที่

Excel ระบุรูปแบบตัวเลขในตัวโดยใช้ ID  
* **14** – สกุลเงิน (เช่น `$1,234.00`)  
* **22** – วันที่สั้น (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **หมายเหตุ:** หากต้องการรูปแบบกำหนดเอง (เช่น `"¥#,##0.00"`), ใช้ `Style.Custom = "¥#,##0.00"` แทน ID ที่มีอยู่

*ทำไมต้องทำขั้นตอนนี้?*  
การกำหนด **รูปแบบตัวเลข** ที่ถูกต้องในขั้นตอนนำเข้า ช่วยขจัดความจำเป็นในการทำรอบสองเพื่อวนลูปเซลล์และเปลี่ยนรูปแบบ อีกทั้งยังทำให้ **รูปแบบวันที่ของเซลล์ Excel** และ **กำหนดรูปแบบสกุลเงินใน Excel** สอดคล้องกันในทุกแถว

## ขั้นตอนที่ 5: นำเข้า DataTable พร้อมคงแถวหัวตาราง

เมธอด `ImportDataTable` สามารถคัดลอกข้อมูล, คงแถวแรกเป็นหัวตาราง, และใช้สไตล์คอลัมน์ที่เราจัดเตรียมไว้

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** – เปิด `FormattedReport.xlsx` แล้วคุณจะเห็น:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

แถวหัวตารางคงอยู่, คอลัมน์ **Price** แสดงสัญลักษณ์สกุลเงิน, และคอลัมน์ **ReleaseDate** แสดงรูปแบบวันที่สั้น — ทั้งหมดโดยไม่ต้องเขียนโค้ดสไตล์เพิ่มเติม

### การจัดการกรณีขอบที่พบบ่อย

| Situation                               | Solution |
|----------------------------------------|----------|
| **More columns than styles**           | ตรวจสอบให้ `columnStyles.Length` เท่ากับ `sourceTable.Columns.Count`. รายการที่ขาดจะใช้สไตล์เริ่มต้นของเวิร์กบุ๊ก |
| **Null values in numeric columns**     | Excel จะถือ `null` เป็นเซลล์ว่าง; รูปแบบตัวเลขยังคงถูกนำไปใช้เมื่อมีค่าถูกป้อนภายหลัง |
| **Custom locale‑specific currency**    | ใช้ `columnStyles[i].Custom = "\"€\"#,##0.00"` และตั้ง `columnStyles[i].Number = -1` เพื่อปิดการใช้ ID ในตัว |
| **Large tables ( > 100 000 rows )**    | พิจารณาใช้ overload ของ `ImportDataTable` พร้อม `ImportTableOptions` เพื่อสตรีมข้อมูลและลดความกดดันของหน่วยความจำ |
| **Applying the same style to multiple columns** | ใช้ instance ของ `Style` เดียวกันในอาเรย์ (เช่น `columnStyles[1] = columnStyles[2] = dateStyle;`) |

## โบนัส: การใช้สตริงรูปแบบกำหนดเอง

หาก ID ที่มีอยู่ไม่ตรงกับความต้องการของคุณ คุณสามารถกำหนดรูปแบบตัวเลขแบบกำหนดเองได้:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

วิธีนี้ให้คุณควบคุม **รูปแบบวันที่ของเซลล์ Excel** และ **กำหนดรูปแบบสกุลเงินใน Excel** อย่างเต็มที่เหนือกว่า ID ที่กำหนดไว้ล่วงหน้า

## สรุป

คุณได้เรียนรู้วิธี **กำหนดรูปแบบตัวเลขใน Excel** อย่างมีประสิทธิภาพเมื่อทำการนำเข้า `DataTable` ด้วย Aspose.Cells ด้วยการสร้างอาเรย์ `Style` ต่อคอลัมน์, กำหนด ID ตัวเลขในตัวหรือกำหนดเอง, และใช้ overload ของ `ImportDataTable` ที่ **คงแถวหัวตารางใน Excel**, คุณสามารถสร้างเวิร์กชีตที่พร้อมเผยแพร่ได้ในขั้นตอนเดียว

### ต่อไปคืออะไร?

* สำรวจ **กำหนดรูปแบบวันที่ใน Excel** ด้วยแพทเทิร์นกำหนดเองเช่น `"dddd, mmmm dd, yyyy"`
* ผสานเทคนิคนี้กับ **การจัดรูปแบบตามเงื่อนไข** เพื่อไฮไลท์ค่าที่อยู่นอกช่วง
* ใช้ **รูปแบบวันที่ของเซลล์ Excel** ในพีโวตเทเบิลหรือแผนภูมิเพื่อการรายงานแบบไดนามิก

ลองปรับเปลี่ยน ID ตัวเลขหรือสตริงกำหนดเองต่าง ๆ เพื่อให้สอดคล้องกับแนวทางการออกแบบขององค์กรของคุณได้เลย ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}