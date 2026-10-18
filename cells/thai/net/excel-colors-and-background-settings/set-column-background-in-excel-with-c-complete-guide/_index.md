---
category: general
date: 2026-05-23
description: ตั้งค่าพื้นหลังคอลัมน์ใน Excel ด้วย C# อย่างรวดเร็ว เรียนรู้วิธีจัดรูปแบบคอลัมน์เฉพาะ
  นำเข้า DataTable ไปยัง Excel และใช้สไตล์คอลัมน์ด้วยตัวอย่างโค้ดง่าย ๆ
draft: false
keywords:
- set column background
- style specific column
- background color excel column
- import datatable excel
- apply column style
language: th
og_description: ตั้งค่าพื้นหลังคอลัมน์ใน Excel ด้วย C# ภายในไม่กี่วินาที คู่มือนี้แสดงวิธีจัดรูปแบบคอลัมน์เฉพาะ,
  นำเข้า DataTable ไปยัง Excel, และใช้สไตล์คอลัมน์ด้วย Aspose.Cells.
og_title: กำหนดพื้นหลังคอลัมน์ใน Excel ด้วย C# – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Set column background in Excel with C# quickly. Learn how to style
    specific column, import datatable excel and apply column style using a simple
    code example.
  headline: Set Column Background in Excel with C# – Complete Guide
  type: TechArticle
- description: Set column background in Excel with C# quickly. Learn how to style
    specific column, import datatable excel and apply column style using a simple
    code example.
  name: Set Column Background in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you open *StyledEmployees.xlsx*, you’ll notice:'
  - name: What if I need to style multiple columns?
    text: 'Just assign a custom `Style` to each index in the `columnStyles` array.
      For example, to give column C a yellow fill:'
  - name: Can I use a different library (e.g., EPPlus)?
    text: 'Yes, the concept stays the same: create a style, apply it to a column,
      then load the `DataTable`. EPPlus uses `ExcelRange.Style.Fill` instead of `BackgroundType.Solid`.
      The code would be a bit longer, but the steps—*prepare data, create style, import,
      save*—remain identical.'
  - name: How do I handle large data sets?
    text: When dealing with thousands of rows, consider using `ImportDataTable`’s
      overload that accepts a `DataTable` **without** loading the entire sheet into
      memory. Aspose.Cells streams data efficiently, but always test memory usage
      if you’re processing massive tables.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
title: ตั้งค่าพื้นหลังคอลัมน์ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่าพื้นหลังคอลัมน์ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์

เคยต้องการ **ตั้งค่าพื้นหลังคอลัมน์** ในแผ่นงาน Excel จาก C# แต่ไม่รู้ว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องทำการจัดรูปแบบสเปรดชีตโดยโปรแกรม วิธีที่ดีคือ เพียงไม่กี่บรรทัดของโค้ดคุณก็สามารถ **จัดรูปแบบคอลัมน์เฉพาะ**, เปลี่ยน **สีพื้นหลังของคอลัมน์ใน Excel**, และแม้กระทั่ง **นำเข้า DataTable ไปยัง Excel** ได้ในขั้นตอนเดียวอย่างราบรื่น

ในบทเรียนนี้เราจะทำตามตัวอย่างเชิงปฏิบัติที่ครอบคลุมทุกอย่างตั้งแต่การสร้างเวิร์กบุ๊กจนถึงการใช้สไตล์แบบกำหนดเองกับคอลัมน์แรก เมื่อเสร็จคุณจะได้สแนปช็อตที่สามารถ **นำสไตล์คอลัมน์ไปใช้** ได้โดยไม่ต้องง้อความ

## สิ่งที่ต้องเตรียม

ก่อนที่เราจะลงมือทำ โปรดตรวจสอบว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework ด้วย)
- Visual Studio 2022 (หรือ IDE C# ใดก็ได้ที่คุณชอบ)
- แพคเกจ **Aspose.Cells** จาก NuGet (หรือไลบรารีที่คล้ายกันซึ่งรองรับ `ImportDataTable` และการจัดรูปแบบ)
- ความเข้าใจพื้นฐานเกี่ยวกับอ็อบเจ็กต์ `DataTable`

ไม่ต้องตั้งค่าพิเศษเพิ่มเติม—แอปคอนโซลง่าย ๆ ก็เพียงพอ

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.Cells

เริ่มต้นด้วยการสร้างโปรเจกต์คอนโซลใหม่:

```bash
dotnet new console -n ExcelStyleDemo
cd ExcelStyleDemo
dotnet add package Aspose.Cells
```

> **เคล็ดลับ:** หากคุณใช้ Visual Studio ให้คลิกขวาที่โปรเจกต์ → *Manage NuGet Packages* → ค้นหา *Aspose.Cells* แล้วติดตั้ง

แพคเกจนี้จะให้คลาส `Workbook`, `Style`, และ `BackgroundType` ที่เราต้องการเพื่อ **ตั้งค่าพื้นหลังคอลัมน์** ต่อไป

## ขั้นตอนที่ 2: เตรียม DataTable ตัวอย่าง

เป้าหมายของเราคือ **นำเข้า DataTable ไปยัง Excel** ในแผ่นงานแรก สร้าง `DataTable` อย่างรวดเร็วพร้อมแถวไม่กี่แถวเพื่อให้คุณเห็นการจัดรูปแบบทำงานอย่างไร

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;   // For Color

// Helper method that returns a populated DataTable
DataTable GetSampleTable()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add("Alice", "Finance", 72000);
    dt.Rows.Add("Bob",   "HR",      56000);
    dt.Rows.Add("Carol", "IT",      95000);
    return dt;
}
```

ทำไมต้องใช้เมธอดช่วยเหลือ? เพราะมันทำให้โค้ดหลักดูสะอาดและง่ายต่อการเปลี่ยนแหล่งข้อมูลของคุณในภายหลัง—อาจเป็นการดึงข้อมูลจากฐานข้อมูลหรือการตอบสนองจาก API

## ขั้นตอนที่ 3: สร้าง Workbook และกำหนดสไตล์คอลัมน์

ต่อไปเราจะสร้าง `Workbook` ใหม่และสร้างอ็อบเจ็กต์ `Style` ที่ให้คอลัมน์แรกมี **พื้นหลังสีฟ้าอ่อน** นี่คือหัวใจของ **ตั้งค่าพื้นหลังคอลัมน์**

```csharp
// Initialize a new workbook
Workbook wb = new Workbook();

// Prepare a style array – one entry per column
Style[] columnStyles = new Style[dt.Columns.Count];

// Create a style for the first column (light‑blue background)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].ForegroundColor = Color.LightBlue;
columnStyles[0].Pattern = BackgroundType.Solid;

// Optional: Define a different style for other columns (e.g., no background)
for (int i = 1; i < columnStyles.Length; i++)
{
    columnStyles[i] = wb.CreateStyle(); // default style
}
```

**ทำไมต้องใช้แอเรย์?** เนื่องจากเมธอด `ImportDataTable` ที่เราจะเรียกใช้ต่อไปรับอาร์เรย์สไตล์ ซึ่งจะนำสไตล์แต่ละรายการไปใช้กับคอลัมน์ที่สอดคล้องโดยอัตโนมัติ วิธีนี้เป็นวิธีที่มีประสิทธิภาพที่สุดในการ **นำสไตล์คอลัมน์ไปใช้** โดยไม่ต้องวนลูปผ่านเซลล์ทีละเซลล์

## ขั้นตอนที่ 4: นำเข้า DataTable พร้อมแอเรย์สไตล์

นี่คือบรรทัดสำคัญที่รวมทุกอย่างเข้าด้วยกัน—**นำเข้า DataTable ไปยัง Excel** พร้อมกับใช้สไตล์ที่เรากำหนดไว้ในขั้นตอนก่อนหน้า

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = wb.Worksheets[0];

// Import the DataTable, include column headers, start at cell A1 (0,0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

พารามิเตอร์ `true` บอก Aspose.Cells ให้คัดลอกหัวคอลัมน์ด้วย ดังนั้นไฟล์ Excel ของคุณจะดูเหมือนกับ `DataTable` อย่างเต็มที่ แอเรย์ `columnStyles` จะทำให้คอลัมน์แรกได้รับการเติมสีฟ้าอ่อน ส่วนคอลัมน์อื่น ๆ จะคงเป็นสีเริ่มต้น

## ขั้นตอนที่ 5: บันทึก Workbook และตรวจสอบผลลัพธ์

สุดท้ายให้เขียน Workbook ลงดิสก์ คุณสามารถเปิดไฟล์ใน Excel เพื่อดู **สีพื้นหลังของคอลัมน์ใน Excel** ทำงานอย่างไร

```csharp
// Save the workbook
string outputPath = "StyledEmployees.xlsx";
wb.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled column.");
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิดไฟล์ *StyledEmployees.xlsx* คุณจะสังเกตว่า:

- คอลัมน์ **A** (Name) มีพื้นหลังสีฟ้าอ่อน
- คอลัมน์ **B** และ **C** ยังคงเป็นพื้นหลังสีขาวตามค่าเริ่มต้น
- แถวทั้งหมดจาก `DataTable` ปรากฏพร้อมหัวคอลัมน์ครบถ้วน

แค่นั้น—การจัดรูปแบบ Excel แบบโปรแกรมของคุณสำเร็จแล้ว

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมรันครบทุกขั้นตอน คัดลอกและวางลงใน `Program.cs` แล้วกด **F5**

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Step 2: Create sample data
        DataTable dt = GetSampleTable();

        // Step 3: Initialize workbook and define styles
        Workbook wb = new Workbook();
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Style for first column (light‑blue)
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].ForegroundColor = Color.LightBlue;
        columnStyles[0].Pattern = BackgroundType.Solid;

        // Default styles for remaining columns
        for (int i = 1; i < columnStyles.Length; i++)
        {
            columnStyles[i] = wb.CreateStyle();
        }

        // Step 4: Import data with style array
        Worksheet sheet = wb.Worksheets[0];
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = "StyledEmployees.xlsx";
        wb.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled column.");
    }

    // Helper: generate a demo DataTable
    static DataTable GetSampleTable()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add("Alice", "Finance", 72000);
        dt.Rows.Add("Bob",   "HR",      56000);
        dt.Rows.Add("Carol", "IT",      95000);
        return dt;
    }
}
```

![ตัวอย่างการตั้งค่าพื้นหลังคอลัมน์](/images/set-column-background.png "ตั้งค่าพื้นหลังคอลัมน์ใน Excel ด้วย C#")

*ข้อความแทนภาพ:* **ตั้งค่าพื้นหลังคอลัมน์** – ภาพหน้าจอของไฟล์ Excel ที่สร้างขึ้นแสดงคอลัมน์แรกที่มีสไตล์

## คำถามที่พบบ่อยและกรณีขอบ

### ถ้าต้องการจัดรูปแบบหลายคอลัมน์ล่ะ?

เพียงกำหนด `Style` ที่กำหนดเองให้กับแต่ละดัชนีในแอเรย์ `columnStyles` ตัวอย่างเช่น เพื่อให้คอลัมน์ C มีสีเติมเหลือง:

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].ForegroundColor = Color.Yellow;
columnStyles[2].Pattern = BackgroundType.Solid;
```

### สามารถใช้ไลบรารีอื่นได้หรือไม่ (เช่น EPPlus)?

ได้ แนวคิดยังคงเหมือนเดิม: สร้างสไตล์, นำไปใช้กับคอลัมน์, แล้วโหลด `DataTable` EPPlus ใช้ `ExcelRange.Style.Fill` แทน `BackgroundType.Solid` โค้ดอาจยาวขึ้นเล็กน้อย แต่ขั้นตอน—*เตรียมข้อมูล, สร้างสไตล์, นำเข้า, บันทึก*—ยังคงเหมือนกัน

### จะจัดการกับชุดข้อมูลขนาดใหญ่อย่างไร?

เมื่อทำงานกับหลายพันแถว ควรใช้ overload ของ `ImportDataTable` ที่รับ `DataTable` **โดยไม่ต้อง** โหลดชีตทั้งหมดเข้าสู่หน่วยความจำ Aspose.Cells สามารถสตรีมข้อมูลได้อย่างมีประสิทธิภาพ แต่ควรทดสอบการใช้หน่วยความจำเสมอหากต้องประมวลผลตารางขนาดมหาศาล

## สรุป

เราได้สาธิตวิธี **ตั้งค่าพื้นหลังคอลัมน์** ใน Excel ด้วย C# โดยการสร้างแอเรย์สไตล์และส่งให้ `ImportDataTable` คุณจึงสามารถ **จัดรูปแบบคอลัมน์เฉพาะ**, ควบคุม **สีพื้นหลังของคอลัมน์ใน Excel**, และ **นำเข้า DataTable ไปยัง Excel** ได้อย่างราบรื่น พร้อมโค้ดที่กระชับและดูแลรักษาง่าย

ต่อไปคุณอาจลอง:

- เพิ่ม **สไตล์เส้นขอบ** หรือ **การจัดรูปแบบฟอนต์** เพื่อทำให้หัวคอลัมน์โดดเด่น
- ใช้การจัดรูปแบบตามเงื่อนไขเพื่อไฮไลท์แถวตามค่า
- ส่งออกเป็นรูปแบบอื่นเช่น CSV หรือ PDF พร้อมคงสไตล์ไว้

อย่าลืมปรับสี, ขยายแอเรย์สไตล์, หรือเชื่อมต่อแหล่งข้อมูลของคุณเอง ความเป็นไปได้ไม่มีขีดจำกัดเมื่อผสาน Aspose.Cells API ที่ทรงพลังกับความคิดสร้างสรรค์ใน C# ของคุณ ขอให้สนุกกับการเขียนโค้ด!

## บทเรียนที่เกี่ยวข้อง

- [How to Set Excel Column Width in Pixels Using Aspose.Cells .NET | Guide for Developers](/cells/english/net/formatting/set-column-width-pixels-aspose-cells-dotnet/)
- [How to Set Column Width in Excel Using Aspose.Cells for .NET - A Complete Guide](/cells/english/net/formatting/set-column-width-excel-aspose-cells-net/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}