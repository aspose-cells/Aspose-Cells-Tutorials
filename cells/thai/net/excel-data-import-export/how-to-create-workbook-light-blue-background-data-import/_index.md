---
category: general
date: 2026-02-09
description: วิธีสร้างเวิร์กบุ๊กใน C# พร้อมพื้นหลังสีฟ้าอ่อนและนำเข้าข้อมูลพร้อมหัวข้อ
  เรียนรู้การเพิ่มพื้นหลังสีฟ้าอ่อน ใช้สไตล์เริ่มต้นของ Excel และนำเข้าตารางข้อมูล
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: th
og_description: วิธีสร้างเวิร์กบุ๊กใน C# พร้อมพื้นหลังสีฟ้าอ่อน, นำเข้าข้อมูลพร้อมหัวข้อ,
  และใช้สไตล์เริ่มต้นของ Excel—ทั้งหมดในคู่มือสั้นกระชับหนึ่งเดียว.
og_title: วิธีสร้างสมุดงาน – พื้นหลังสีฟ้าอ่อน, การนำเข้าข้อมูล
tags:
- C#
- Excel
- Aspose.Cells
title: วิธีสร้างสมุดงาน – พื้นหลังสีฟ้าอ่อน, การนำเข้าข้อมูล
url: /th/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Workbook – พื้นหลังสีฟ้าอ่อน, การนำเข้าข้อมูล

เคยสงสัย **how to create workbook** ใน C# ที่ดูสวยงามขึ้นมาทันทีหลังจากสร้างหรือไม่? บางทีคุณอาจดึง `DataTable` จากฐานข้อมูลและเบื่อกับเซลล์สีขาวเริ่มต้นที่น่าเบื่อ ในบทเรียนนี้เราจะอธิบายขั้นตอนการสร้าง workbook ใหม่, เพิ่มพื้นหลังสีฟ้าอ่อนให้กับคอลัมน์หนึ่ง, และนำเข้าข้อมูลพร้อมหัวข้อคอลัมน์—ทั้งหมดโดยใช้สไตล์เริ่มต้นที่ Excel มีให้

เราจะเพิ่มสถานการณ์ “ถ้า‑อย่างไร” บางอย่างเข้าไปด้วย เช่น การจัดการค่าที่เป็น null หรือการปรับแต่งมากกว่าหนึ่งคอลัมน์ สุดท้ายคุณจะได้ไฟล์ Excel ที่สไตล์ครบถ้วนพร้อมส่งให้ผู้มีส่วนได้ส่วนเสียโดยไม่ต้องทำการประมวลผลเพิ่มเติม

## ข้อกำหนดเบื้องต้น

* **.NET 6+** (โค้ดนี้ทำงานได้บน .NET Framework 4.6+ ด้วย)  
* **Aspose.Cells for .NET** – ไลบรารีที่ให้การทำงานของ `Workbook`, `Style` และ `ImportDataTable` ติดตั้งผ่าน NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* แหล่งข้อมูล `DataTable` – เราจะสร้างตัวอย่างในโค้ด, แต่คุณสามารถแทนที่ด้วยการ query ADO.NET ใด ๆ ก็ได้

ได้ครบหรือยัง? ดีมาก, เริ่มกันเลย

## ขั้นตอนที่ 1: เริ่มต้น Workbook ใหม่ (Primary Keyword)

สิ่งแรกที่คุณต้องทำคือ **how to create workbook** – อย่างแท้จริง คลาส `Workbook` แทนไฟล์ Excel ทั้งไฟล์และคอนสตรัคเตอร์ของมันให้คุณเริ่มจากแผ่นเปล่า

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การเริ่มต้นด้วย `Workbook` ใหม่ทำให้คุณควบคุมสไตล์ทุกอย่างตั้งแต่ต้น หากคุณเปิดไฟล์ที่มีอยู่แล้ว คุณจะสืบทอดสไตล์ใด ๆ ที่ผู้สร้างไฟล์เดิมตั้งไว้ ซึ่งอาจทำให้รูปแบบไม่สอดคล้องกัน

## ขั้นตอนที่ 2: เตรียม DataTable ที่จะนำเข้า

เพื่อเป็นตัวอย่าง เราจะสร้าง `DataTable` ง่าย ๆ ขึ้นมา ในสถานการณ์จริงคุณอาจเรียก stored procedure หรือเมธอดของ ORM

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **เคล็ดลับ:** หากต้องการรักษาลำดับคอลัมน์ให้ตรงกับที่ฐานข้อมูลแสดง, ตั้งค่าพารามิเตอร์ `importColumnNames` ของ `ImportDataTable` เป็น `true` ซึ่งบอก Aspose.Cells ให้เขียนหัวคอลัมน์ให้คุณ

## ขั้นตอนที่ 3: กำหนดสไตล์คอลัมน์ – เริ่มต้น + พื้นหลังสีฟ้าอ่อน

ตอนนี้เราตอบส่วน **add light blue background** ของปริศนา Aspose.Cells ให้คุณส่งอาเรย์ของอ็อบเจกต์ `Style` ที่สอดคล้องกับแต่ละคอลัมน์ที่นำเข้า รายการแรกคือสไตล์ของคอลัมน์ 0, รายการที่สองของคอลัมน์ 1, ฯลฯ หากสไตล์น้อยกว่าจำนวนคอลัมน์ คอลัมน์ที่เหลือจะใช้สไตล์เริ่มต้นโดยอัตโนมัติ

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **ทำไมถึงมีแค่สองสไตล์?** ในตัวอย่างของเรามีสี่คอลัมน์ แต่เราต้องการให้คอลัมน์ที่สอง (Name) โดดเด่น อาเรย์ไม่จำเป็นต้องมีความยาวเท่ากับจำนวนคอลัมน์; รายการที่ขาดหายจะสืบทอดสไตล์เริ่มต้นของ workbook โดยอัตโนมัติ

## ขั้นตอนที่ 4: นำเข้า DataTable พร้อมหัวข้อและสไตล์

นี่คือจุดที่เรานำ **excel import datatable c#** และ **import data with headers** มารวมกัน เมธอด `ImportDataTable` ทำหน้าที่หลัก: เขียนชื่อคอลัมน์, แถวข้อมูล, และใช้สไตล์อาเรย์ที่เราสร้างไว้

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### ผลลัพธ์ที่คาดหวัง

หลังจากรันโปรแกรม, `workbook` จะมี worksheet เดียวที่มีลักษณะดังนี้:

| **ID** | **Name** (สีฟ้าอ่อน) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* คอลัมน์ **Name** มีพื้นหลังสีฟ้าอ่อน แสดงว่าการใช้สไตล์อาเรย์ทำงานได้
* หัวคอลัมน์ถูกสร้างอัตโนมัติเนื่องจากเราใส่ค่า `true` ให้กับ `importColumnNames`
* ค่าที่เป็น null จะปรากฏเป็นเซลล์ว่าง ซึ่งเป็นพฤติกรรมเริ่มต้นของ Aspose.Cells

## ขั้นตอนที่ 5: บันทึก Workbook (Optional but Useful)

คุณอาจต้องการบันทึกไฟล์ลงดิสก์หรือสตรีมกลับไปยังไคลเอนต์เว็บ การบันทึกทำได้ง่าย ๆ ดังนี้:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** หากคุณต้องการรองรับเวอร์ชัน Excel เก่า, เปลี่ยน `SaveFormat.Xlsx` เป็น `SaveFormat.Xls` API จะจัดการการแปลงให้คุณเอง

## Edge Cases & Variations

### หลายคอลัมน์ที่มีสไตล์

หากต้องการสไตล์หลายคอลัมน์ เพียงขยายอาเรย์ `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

ตอนนี้ทั้ง **Name** และ **Salary** จะเป็นสีฟ้าอ่อน

### การจัดรูปแบบตามเงื่อนไขแทนสไตล์คงที่

บางครั้งคุณต้องการให้คอลัมน์เปลี่ยนเป็นสีแดงเมื่อค่ามากกว่าขีดจำกัด นั่นคือจุดที่ **use default style excel** พบกับ conditional formatting:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### การนำเข้าโดยไม่มีหัวข้อ

หากระบบ downstream ของคุณมีหัวข้อของตนเองอยู่แล้ว ให้ส่งค่า `false` ให้กับอาร์กิวเมนต์ `importColumnNames` ข้อมูลจะเริ่มที่ `A1` และคุณสามารถเขียนหัวข้อแบบกำหนดเองต่อไปได้

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## ตัวอย่างทำงานเต็ม (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}