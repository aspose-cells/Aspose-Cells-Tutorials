---
category: general
date: 2026-10-26
description: เรียนรู้วิธีนำเข้า DataTable ไปยังแผ่นงาน Excel ด้วย C# และ Aspose.Cells
  พร้อมรักษารูปแบบและหัวตารางไว้ด้วยเพียงไม่กี่บรรทัดของโค้ด
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: th
lastmod: 2026-10-26
og_description: วิธีนำเข้า DataTable ไปยังแผ่นงาน Excel ด้วย C# และ Aspose.Cells — ตามคู่มือฉบับสมบูรณ์นี้เพื่อคงสไตล์,
  ส่วนหัวและการจัดรูปแบบ.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: วิธีนำเข้า DataTable ไปยังแผ่นงาน Excel – คู่มือขั้นตอน C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: วิธีนำเข้า DataTable ไปยังแผ่นงาน Excel ด้วย C#
url: /th/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการนำเข้า DataTable ไปยังแผ่นงาน Excel ด้วย C#

หากคุณต้องการ **how to import datatable** ไปยังแผ่นงาน Excel คู่มือนี้จะแสดงขั้นตอนที่แน่นอนใน C# ไม่ว่าคุณจะกำลังสร้างเครื่องมือรายงานหรือส่งออกข้อมูลตาราง คุณจะได้เห็นวิธีการรักษาหัวคอลัมน์และสไตล์ของเซลล์ให้คงเดิมด้วย Aspose.Cells โซลูชันนี้ทำงานกับ .NET 6+ และต้องการเพียงไม่กี่บรรทัดของโค้ด

การนำเข้า DataTable เป็นงานทั่วไปเมื่อทำงานกับสเปรดชีต แต่ผู้พัฒนามักลืมเปิดการถ่ายโอนสไตล์หรือส่งค่าแฟล็กหัวคอลัมน์อย่างถูกต้อง ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีกำหนดค่า **ImportTableOptions**, เปิดใช้งาน **ImportDataTableStyle**, และเรียก `ImportDataTable` อย่างปลอดภัย เมื่อเสร็จสิ้นคุณจะมีเมธอดพร้อมใช้งานที่สามารถนำไปใส่ในโปรเจกต์ C# ใดก็ได้

## สิ่งที่ต้องมี

ก่อนเริ่มทำตามขั้นตอน ให้ตรวจสอบว่าคุณมี:

* .NET 6 SDK หรือรุ่นที่ใหม่กว่าติดตั้งอยู่
* สำเนาไลเซนส์ของ **Aspose.Cells for .NET** (รุ่นทดลองฟรีใช้สำหรับทดสอบได้)
* ความคุ้นเคยพื้นฐานกับ `DataTable` และแนวคิดของ Excel
* IDE เช่น Visual Studio 2022 (หรือโปรแกรมแก้ไขใดก็ได้ที่รองรับ C#)

ไม่จำเป็นต้องติดตั้งแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Cells`

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเข้าสู่ DataTable

สิ่งแรกที่คุณทำเมื่อ **how to import datatable** คือให้มีข้อมูลพร้อมใช้งาน ในสถานการณ์จริงส่วนใหญ่ `DataTable` จะมาจากการคิวรีฐานข้อมูล, ตัวแปลง CSV, หรือคอลเลกชันในหน่วยความจำ ด้านล่างเป็นตัวอย่างขั้นต่ำที่สร้างตารางพร้อมแถวไม่กี่แถว:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*ทำไมเรื่องนี้สำคัญ*: การสร้าง `DataTable` ก่อนทำให้คุณควบคุมลำดับคอลัมน์, ชนิดข้อมูล, และชื่อหัวคอลัมน์—ทั้งหมดนี้จะถูกเก็บรักษาไว้เมื่อคุณนำเข้าตารางไปยังแผ่นงาน Excel ต่อไป

## ขั้นตอนที่ 2: สร้าง `ImportTableOptions` และเปิดการนำเข้าสไตล์

เมื่อคุณตอบ **how to import datatable** ขั้นตอนต่อไปคือการตัดสินใจว่าจะนำสไตล์ภาพ (ฟอนต์, สี, เส้นขอบ) ที่อาจกำหนดไว้บน `DataTable` ต้นทางหรือไม่ Aspose.Cells มีคลาส `ImportTableOptions` สำหรับการควบคุมระดับละเอียด การตั้งค่า `ImportDataTableStyle = true` จะคัดลอกข้อมูลสไตล์ไปยังแผ่นงานเป้าหมาย

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*ทำไมเรื่องนี้สำคัญ*: หากไม่ได้เปิด `ImportDataTableStyle` เซลล์ที่นำเข้าจะใช้สไตล์เริ่มต้นของแผ่นงาน ทำให้สูญเสียการจัดรูปแบบที่คุณกำหนดไว้ใน `DataTable` แฟล็กนี้จึงจำเป็นสำหรับการส่งออกที่ดูเป็นมืออาชีพ

## ขั้นตอนที่ 3: นำเข้า DataTable ไปยังแผ่นงาน รวมถึงหัวคอลัมน์

ตอนนี้คุณมีทุกอย่างที่จำเป็นเพื่อ **how to import datatable** ไปยังไฟล์ Excel แล้ว คุณสร้าง workbook, เลือก worksheet, และเรียก `ImportDataTable` อาร์กิวเมนต์ที่สอง (`true`) บอก Aspose.Cells ให้เขียนหัวคอลัมน์เป็นแถวแรก

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

การเรียก `ExportDataTableToExcel("Employees.xlsx")` จะสร้างไฟล์ `Employees.xlsx` ที่แถวแรกมี **Id**, **Name**, และ **Department**, และแต่ละเซลล์จะคงสไตล์ที่กำหนดใน `DataTable` ดั้งเดิม

### ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

ด้านล่างเป็นโปรแกรมคอนโซลที่สมบูรณ์และทำงานอิสระซึ่งสาธิต **how to import datatable** และบันทึกผลลัพธ์ลงในไดเรกทอรีปัจจุบัน คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่แล้วรัน

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**  
เมื่อคุณเปิด `Employees.xlsx` คุณจะเห็น:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

เซลล์ทั้งหมดคงสไตล์เริ่มต้นของ DataTable (ฟอนต์, การจัดแนว) หากคุณได้กำหนดสไตล์แบบกำหนดเองให้กับ `DataTable` ก่อนนำเข้า สไตล์เหล่านั้นจะปรากฏในแผ่นงานเช่นกัน เนื่องจาก `ImportDataTableStyle` ถูกตั้งค่าเป็น `true`

## ปัญหาที่พบบ่อยและเคล็ดลับปฏิบัติที่ดีที่สุด

| ปัญหา | สาเหตุ | วิธีหลีกเลี่ยง |
|-------|--------|----------------|
| **หัวคอลัมน์หาย** | ส่งค่า `false` เป็นอาร์กิวเมนต์ที่สองของ `ImportDataTable` ทำให้ข้ามชื่อคอลัมน์ | ใช้ `true` เสมอเมื่อต้องการหัวคอลัมน์, หรือเขียนหัวคอลัมน์ด้วยตนเองก่อนการนำเข้า |
| **สไตล์ไม่ถูกถ่ายโอน** | ลืมเปิด `ImportDataTableStyle` | ตั้งค่า `ImportDataTableStyle = true` ใน `ImportTableOptions` |
| **ตารางขนาดใหญ่ทำให้ประสิทธิภาพช้า** | นำเข้าหลายล้านแถวโดยไม่มีการแบ่งหน้า | นำเข้าเป็นชุดหรือใช้ overload ของ `ImportDataTable` ที่รับ `startRow` เพื่อสตรีมข้อมูล |
| **อ้างอิงแผ่นงานไม่ถูกต้อง** | ใช้ `workbook.Worksheets[1]` เมื่อมีเพียงแผ่นเดียว | ใช้ `workbook.Worksheets[0]` หรือสร้างแผ่นใหม่ด้วย `workbook.Worksheets.Add()` |
| **ไลเซนส์หมดอายุ** | รุ่นทดลองของ Aspose.Cells แสดงลายน้ำหลัง 30 วัน | ใส่ไลเซนส์ที่ถูกต้องด้วย `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

**เคล็ดลับพิเศษ**: หากต้องการใช้ธีมแบบกำหนดเองหลังการนำเข้า ให้เรียก `ws.Cells.ApplyStyle(style)` โดยที่ `style` เป็นอ็อบเจ็กต์ `Style` ที่คุณกำหนดค่าไว้แล้วและนำไปใช้ซ้ำหลายแถว

## การขยายโซลูชัน

เมื่อคุณรู้ **how to import datatable** แล้ว คุณสามารถสำรวจสถานการณ์ที่เกี่ยวข้องต่อไป:

* **นำเข้าตารางหลายตาราง** – ทำซ้ำการนำเข้าในแผ่นงานต่าง ๆ
* **การจัดรูปแบบตามเงื่อนไข** – หลังการนำเข้า ให้เพิ่มกฎด้วย `ws.Cells.ApplyConditionalFormatting`
* **ส่งออกเป็น CSV** – ใช้ `workbook.Save("file.csv", SaveFormat.Csv)` หากต้องการรูปแบบข้อความธรรมดา
* **อ่านกลับเป็น DataTable** – ใช้ `ws.Cells.ExportDataTable` เพื่อตรวจสอบความสมบูรณ์ของการส่งกลับ

ส่วนขยายทั้งหมดนี้อิงจากรูปแบบหลักที่แสดงข้างต้น: ดึงข้อมูล, ตั้งค่าตัวเลือกการนำเข้า, และเรียกเมธอด Aspose.Cells เพียงหนึ่งครั้ง

## สรุป

คุณได้มีคำตอบที่ครบถ้วนและพร้อมใช้งานสำหรับ **how to import datatable** ไปยังแผ่นงาน Excel ด้วย C# บทแนะนำนี้ครอบคลุมการดึงข้อมูลต้นทาง, การกำหนดค่า `ImportTableOptions` พร้อม `ImportDataTableStyle`, และการทำการนำเข้าด้วย `ImportDataTable` ด้วยการทำตามตัวอย่างโค้ด คุณจะคงหัวคอลัมน์และสไตล์โดยอัตโนมัติ และสามารถปรับใช้รูปแบบนี้กับชุดข้อมูลขนาดใหญ่, แผ่นงานหลายแผ่น, หรือการจัดรูปแบบเพิ่มเติมได้

พร้อมที่จะทำอัตโนมัติการสร้างรายงานของคุณหรือยัง? ลองเปลี่ยน `DataTable` ตัวอย่างเป็นคิวรีจากฐานข้อมูลจริง, ทดลองใช้สไตล์เซลล์แบบกำหนดเอง, และผสานเมธอดนี้เข้ากับเลเยอร์บริการที่มีอยู่ของคุณ. Happy coding!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}