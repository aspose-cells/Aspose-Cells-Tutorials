---
category: general
date: 2026-07-03
description: ใช้สีแถวสลับเมื่อคุณนำเข้าตารางข้อมูลไปยัง Excel ด้วย C# เรียนรู้วิธีส่งออก
  DataTable ของ C# ไปยัง Excel บันทึกไฟล์ Excel ที่มีสไตล์ตาราง และรักษาการจัดรูปแบบของเวิร์กบุ๊กไว้
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: th
og_description: ใช้สีแถวสลับใน Excel ด้วย C# บทเรียนนี้แสดงวิธีการนำเข้า DataTable
  ไปยัง Excel, ส่งออก DataTable ของ C# ไปยัง Excel, และบันทึกเวิร์กบุ๊กพร้อมการจัดรูปแบบ.
og_title: ใช้สีแถวสลับใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: การใช้สีแถวสลับใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การใช้สีแถวสลับใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์

เคยต้อง **ใช้สีแถวสลับ** เมื่อคุณส่งออก `DataTable` ของ C# ไปยัง Excel หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามวิธีทำให้สเปรดชีตดูเรียบร้อยโดยไม่ต้องแก้ไข Excel ด้วยตนเองหลังจากนั้น ข่าวดีคือคุณสามารถทำได้โดยโปรแกรมเมติกในไม่กี่บรรทัดของโค้ด

ในบทเรียนนี้เราจะอธิบายขั้นตอน **import datatable to excel**, แสดงวิธี **export c# datatable to excel** พร้อมตารางที่มีสไตล์, และสุดท้าย **save styled table excel** โดยคงรูปแบบไว้ หลังจากจบคุณจะสามารถ **save workbook with formatting** ที่พร้อมใช้ในการประชุมกับลูกค้าได้ทันที

## Prerequisites

- .NET 6.0 หรือใหม่กว่า (ตัวอย่างใช้ .NET 6 แต่เวอร์ชันล่าสุดใดก็ใช้ได้)
- Aspose.Cells for .NET (รุ่นทดลองหรือแบบลิขสิทธิ์) – ไลบรารีนี้ทำให้การจัดสไตล์เป็นเรื่องง่าย
- แหล่งข้อมูล `DataTable` (อาจมาจากฐานข้อมูล, CSV, หรือคอลเลกชันในหน่วยความจำ)

> **Pro tip:** หากคุณยังไม่มี Aspose.Cells คุณสามารถดาวน์โหลดได้จาก NuGet ด้วยคำสั่ง `dotnet add package Aspose.Cells`.

## Step 1: Set Up the Project and Load Your Data

เริ่มต้นด้วยการสร้างแอปคอนโซล (หรือโปรเจกต์ C# ใดก็ได้) แล้วเพิ่ม `using` ที่จำเป็น จากนั้นดึงข้อมูลเข้าสู่ `DataTable` สำหรับตัวอย่างนี้เราจะสร้างตารางง่าย ๆ ขึ้นมาแบบไดนามิก

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การมี `DataTable` พร้อมใช้งานหมายความว่าคุณสามารถ **import datatable to excel** ได้ด้วยการเรียกครั้งเดียว ลดความจำเป็นในการใส่ข้อมูลเซลล์ทีละเซลล์ด้วยตนเอง

## Step 2: Create a Workbook and Define the Alternating Row Styles

ต่อไปเราจะสร้าง `Workbook` ใหม่ เทคนิคในการ **apply alternating row colors** อยู่ที่ `ImportTableOptions.StyleArray` เราจะใช้สไตล์ในตัวสองแบบแรก (โดยทั่วไปคือสีขาวและสีเทาอ่อน) แต่คุณสามารถปรับแต่งได้ในภายหลัง

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Explanation:** `ImportTableOptions` บอก Aspose.Cells ว่าจะจัดการแต่ละแถวอย่างไรระหว่างการนำเข้า โดยการให้ `StyleArray` ที่มีสองรายการ ไลบรารีจะทำการทาสีอัตโนมัติให้แถวคี่ใช้สไตล์แรกและแถวคู่ใช้สไตล์ที่สอง — พอดีกับความต้องการ **apply alternating row colors** ของคุณ

## Step 3: Pull the DataTable Into the Worksheet (Including Headers)

เมื่อเวิร์กบุ๊กและสไตล์พร้อมแล้ว เราจะ **import datatable to excel** เมธอด `ImportDataTable` ทำหน้าที่หลัก: เขียนหัวคอลัมน์, ปฏิบัติตามอาเรย์สไตล์, และวางข้อมูลเริ่มจากเซลล์ A1

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**ทำไมเราถึงใส่ `true` เป็นอาร์กิวเมนต์ที่สอง:** คำสั่งนี้บอกเมธอดให้เขียนชื่อคอลัมน์เป็นแถวแรก ซึ่งเป็นสิ่งจำเป็นสำหรับรายงานที่ดูเป็นมืออาชีพ

## Step 4: Fine‑Tune the Table (Optional but Handy)

หากคุณต้องการให้คอลัมน์ปรับขนาดอัตโนมัติหรือเพิ่มแถวกรอง สามบรรทัดเพิ่มเติมก็ทำให้ตารางดูดีขึ้น

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

การปรับแต่งเหล่านี้ไม่กระทบต่อสีสลับของแถว แต่ช่วยเพิ่มประสบการณ์ผู้ใช้โดยรวมของไฟล์ **save styled table excel** ได้ดีขึ้น

## Step 5: Save the Workbook While Keeping All Formatting

สุดท้ายเราจะบันทึกไฟล์ลงดิสก์ เมธอด `Save` จะคงสไตล์ทุกอย่างที่ตั้งค่าไว้ ทำให้แถวสลับคงอยู่โดยไม่มีการเปลี่ยนแปลง

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

เมื่อคุณเปิด `StyledEmployees.xlsx` คุณจะเห็นตารางที่แถวสลับระหว่างสีขาวและสีเทาอ่อน — สัญญาณภาพที่ผู้ใช้หลายคนพึ่งพาเพื่อความอ่านง่าย

### Expected Output

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- แถว 1, 3 … → พื้นหลังสีขาว  
- แถว 2, 4 … → พื้นหลังสีเทาอ่อน  

นี่คือกระบวนการทั้งหมดของ **save workbook with formatting** 

## Common Questions & Edge Cases

### What if my DataTable has thousands of rows?

เมธอด `ImportDataTable` จะสตรีมข้อมูลอย่างมีประสิทธิภาพ แต่หากตารางมีขนาดใหญ่มากอาจเจอข้อจำกัดของหน่วยความจำ ในกรณีนั้นลองแบ่งการส่งออกเป็นหลายแผ่นงานหรือใช้ overload ของ `ImportDataTable` ที่ให้คุณระบุแถวและคอลัมน์เริ่มต้นได้

### Can I use custom colors instead of the built‑in ones?

ได้เลย เพียงเปลี่ยนการกำหนดค่า `ForegroundColor` ใน `styleWhite` และ `styleGray` ให้เป็น `System.Drawing.Color` ใดก็ได้ที่คุณต้องการ — เช่น สีฟ้าอ่อนหรือสีแบรนด์ของบริษัท

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### How do I ensure the alternating style works when the user adds rows later?

หากผู้ใช้แก้ไขไฟล์ด้วยตนเอง อาเรย์สไตล์เดิมจะไม่ขยายอัตโนมัติ วิธีแก้ง่าย ๆ คือแปลงช่วงข้อมูลเป็น Excel Table (`ListObject`) หลังการนำเข้า; Excel จะทำซ้ำรูปแบบให้แถวใหม่โดยอัตโนมัติ

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

ตอนนี้แถวใหม่ใด ๆ จะสืบทอดสีสลับโดยอัตโนมัติ

## Full Working Example (All Steps in One Place)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

เรียกใช้โปรแกรม เปิดไฟล์ที่สร้างขึ้น คุณจะเห็นสีสลับที่ถูกนำไปใช้โดยอัตโนมัติ — ไม่ต้องทำการจัดรูปแบบด้วยมือ

## Conclusion

เราได้สาธิตวิธี **apply alternating row colors** เมื่อ **import datatable to excel** ด้วย C# กระบวนการนี้ครอบคลุมทุกสิ่งที่คุณต้องการเพื่อ **export c# datatable to excel**, **save styled table excel**, และ **save workbook with formatting** ที่ดูเป็นมืออาชีพตั้งแต่แรก

ขั้นตอนต่อไป? ลองสลับสไตล์สองแบบเพื่อสร้างธีมของคุณเอง หรือแปลงช่วงเป็น Excel Table เพื่อให้ผู้ใช้สามารถจัดเรียงและกรองข้อมูลได้พร้อมคงรูปแบบสีอยู่ คุณยังสามารถสำรวจการจัดรูปแบบตามเงื่อนไขผ่าน `ConditionalFormattingCollection` เพื่อเพิ่มสัญญาณภาพแบบไดนามิกได้อีกด้วย

มีอะไรเพิ่มเติม

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ในโปรเจกต์ของคุณเอง

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}