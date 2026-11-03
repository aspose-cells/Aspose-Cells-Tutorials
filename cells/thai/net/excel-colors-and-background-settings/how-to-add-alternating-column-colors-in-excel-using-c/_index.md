---
category: general
date: 2026-10-01
description: สีคอลัมน์สลับใน Excel ด้วย C# – เรียนรู้การสร้างไฟล์ Excel จาก DataTable,
  ตั้งค่าสีพื้นหลังของเซลล์ด้วย C#, และนำเข้า DataTable ไปยัง Excel พร้อมคอลัมน์ที่มีสไตล์
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: th
lastmod: 2026-10-01
og_description: ทำให้การสลับสีคอลัมน์ใน Excel ง่ายขึ้น ตามคู่มือนี้เพื่อสร้างไฟล์
  Excel จาก DataTable ตั้งค่าสีพื้นหลังของเซลล์ด้วย C# และนำเข้า DataTable ไปยัง Excel
  พร้อมคอลัมน์ที่มีสไตล์
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: เพิ่มสีคอลัมน์สลับใน Excel ด้วย C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: วิธีเพิ่มสีคอลัมน์สลับใน Excel ด้วย C#
url: /th/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่มสีคอลัมน์สลับใน Excel ด้วย C#

หากคุณต้องการ **alternating column colors excel** ในรายงานที่สร้างจากแอปพลิเคชันของคุณ คำแนะนำนี้จะแสดงวิธีแก้ไขแบบครบถ้วน คุณจะได้เห็นวิธีสร้างไฟล์ Excel จาก `DataTable` ตั้งค่าสีพื้นหลังของเซลล์แบบ C# และนำ `DataTable` ไปยัง Excel พร้อมใช้สไตล์ที่แตกต่างกันสำหรับแต่ละคอลัมน์

บทเรียนนี้ครอบคลุมทุกสิ่งที่คุณต้องการ: แพคเกจ NuGet ที่จำเป็น ตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบ และคำอธิบายว่าทำไมแต่ละขั้นตอนจึงสำคัญ เมื่อตอนจบคุณจะมีเวิร์กบุ๊กที่มีสไตล์ซึ่งสามารถเปิดได้โดยตรงใน Microsoft Excel

## สิ่งที่ต้องมี

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 (หรือใหม่กว่า) SDK ติดตั้งแล้ว  
* Visual Studio 2022 (หรือ IDE ที่รองรับ C# ใด ๆ)  
* ไลบรารี **Aspose.Cells for .NET** – ติดตั้งด้วย  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells ให้คลาส `Workbook`, `Worksheet`, `Style` และ `BackgroundType` ที่ใช้ในตัวอย่าง

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเป็น `DataTable`

งานแรกคือการรับข้อมูลที่คุณต้องการส่งออก ในโครงการจริงคุณอาจเติม `DataTable` จากการคิวรีฐานข้อมูล, การเรียก API, หรือคอลเลกชันในหน่วยความจำใด ๆ

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**ทำไมขั้นตอนนี้สำคัญ:**  
`DataTable` เป็นคอนเทนเนอร์สากลที่แมปได้อย่างสะอาดกับแผ่นงาน Excel การใช้ `DataTable` ทำให้คุณ **create excel file from datatable c#** ได้โดยไม่ต้องเขียนลูปกำหนดค่าเองสำหรับแต่ละคอลัมน์

## ขั้นตอนที่ 2: สร้างเวิร์กบุ๊กใหม่และดึงแผ่นงานแรก

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**คำอธิบาย:**  
`Workbook` คืออ็อบเจ็กต์ราก; `Worksheets[0]` ให้แผ่นงานเริ่มต้นที่ข้อมูลจะถูกวางไว้

## ขั้นตอนที่ 3: เตรียมสไตล์ที่แตกต่างสำหรับแต่ละคอลัมน์ (สีพื้นหลังสลับ)

เพื่อให้ได้ **alternating column colors excel** เราจะสร้าง `Style` สำหรับทุกคอลัมน์และกำหนดสีพื้นหลังอ่อนที่สลับกันระหว่างสองเฉดสี

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**ทำไมต้องใช้ลูป:**  
ลูปทำให้แน่ใจว่า **set cell background color c#** ถูกนำไปใช้อย่างสม่ำเสมอ แม้จำนวนคอลัมน์จะเปลี่ยนแปลงในขณะรันโค้ด ซึ่งทำให้วิธีนี้ทนทานต่อรายงานแบบไดนามิก

## ขั้นตอนที่ 4: นำ `DataTable` เข้าสู่แผ่นงาน พร้อมใช้สไตล์คอลัมน์

Aspose.Cells สามารถนำเข้า `DataTable` ได้โดยตรง และเราสามารถส่งอาร์เรย์สไตล์เพื่อกำหนดสีให้แต่ละคอลัมน์

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**สิ่งที่เกิดขึ้นเบื้องหลัง:**  
`ImportDataTable` เขียนแถวหัวตารางก่อน แล้วตามด้วยแถวข้อมูลแต่ละแถว เนื่องจากเราให้ `columnStyles` ไว้ ทุกเซลล์ในคอลัมน์ที่กำหนดจะได้รับสไตล์ที่สอดคล้องกัน ทำให้ได้สีสลับตามที่ต้องการ

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กที่มีสไตล์ลงไฟล์

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

เมื่อคุณเปิดไฟล์ *StyledTable.xlsx* ใน Excel คุณจะเห็นแต่ละคอลัมน์มีสีพื้นหลังสลับกัน ทำให้ตารางอ่านง่ายขึ้น

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกส่วนเข้าด้วยกัน นี่คือโปรแกรมแบบอิสระที่คุณสามารถคัดลอก วาง และรันได้

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### ผลลัพธ์ที่คาดหวัง

* ไฟล์ชื่อ **StyledTable.xlsx** อยู่ที่ `C:\Temp\`.  
* แผ่นงานแสดงสามคอลัมน์ (`Id`, `Name`, `Score`) โดยมีสีพื้นหลังสลับ: คอลัมน์ 1 และ 3 เป็น *LightYellow*, คอลัมน์ 2 เป็น *LightCyan*.  
* ทุกแถวจาก `DataTable` ปรากฏใต้แถวหัวตาราง

## คำถามทั่วไปและกรณีขอบ

| Question | Answer |
|----------|--------|
| *Can I use other colors?* | ใช่. แทนที่ `System.Drawing.Color.LightYellow` และ `LightCyan` ด้วยค่า `System.Drawing.Color` ใดก็ได้ |
| *What if the DataTable has many columns?* | ลูปจะสร้างสไตล์ให้แต่ละคอลัมน์โดยอัตโนมัติ ดังนั้นรูปแบบจะสเกลได้โดยไม่ต้องแก้โค้ด |
| *Do I need to dispose of the workbook?* | Aspose.Cells implements `IDisposable`. หากคุณห่อ `Workbook` ด้วยบล็อก `using` จะทำให้ทรัพยากรถูกปล่อยออกอย่างทันท่วงที |
| *How to apply the same alternating colors to rows instead of columns?* | สร้าง `Style[]` สำหรับแถวและเรียก `worksheet.Cells.ImportDataTable(..., rowStyles)` – Aspose.Cells มี overload รองรับทั้งสองแบบ |
| *Can I write the file directly to a stream (e.g., for a web API)?* | ได้. ใช้ `workbook.Save(stream, SaveFormat.Xlsx);` แทนการระบุพาธไฟล์ |

## เคล็ดลับจากสนาม

* **Pro tip:** แคชอ็อบเจ็กต์สไตล์หากคุณสร้างหลายแผ่นงานในรันเดียว – การสร้างสไตล์ค่อนข้างเบา แต่การนำกลับมาใช้ซ้ำช่วยลดการใช้หน่วยความจำ |
* **Watch out for:** เมื่อใช้ `System.Drawing.Color` บนแพลตฟอร์มที่ไม่ใช่ Windows ให้เพิ่มแพคเกจ `System.Drawing.Common` ผ่าน NuGet และตรวจสอบให้แน่ใจว่า runtime รองรับ GDI+

## สรุป

ตอนนี้คุณรู้วิธี **alternating column colors excel** โดยการสร้างไฟล์ Excel จาก `DataTable` ใน C# ตั้งค่าสีพื้นหลังของเซลล์ด้วย Aspose.Cells และ **import datatable to excel** พร้อมอาร์เรย์สไตล์คอลัมน์ วิธีนี้เร็ว ดูแลรักษาง่าย และทำงานได้กับชุดข้อมูลขนาดใดก็ได้

### ขั้นตอนต่อไป

* สำรวจ **set cell background color c#** สำหรับการจัดรูปแบบตามเงื่อนไข (เช่น ไฮไลท์คะแนนต่ำ)  
* ผสานเทคนิคนี้กับ **create excel file from datatable c#** เพื่อสร้างรายงานหลายแผ่นงาน  
* ศึกษา API การสร้างแผนภูมิของ Aspose.Cells เพื่อเพิ่มสรุปภาพลงในเวิร์กบุ๊กเดียวกัน

ปรับสี รูปแบบไฟล์ หรือแหล่งข้อมูลให้ตรงกับความต้องการของโครงการของคุณได้ตามใจ อย่าลืมสนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}