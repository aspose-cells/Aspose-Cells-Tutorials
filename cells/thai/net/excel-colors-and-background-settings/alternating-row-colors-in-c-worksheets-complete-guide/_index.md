---
category: general
date: 2026-05-30
description: เรียนรู้วิธีเพิ่มสีแถวสลับในแผ่นงาน C#, ตั้งค่าพื้นหลังเซลล์ด้วยลายเติมเต็มสีเดียว,
  และปรับแต่งสไตล์เซลล์ของแผ่นงานได้อย่างง่ายดาย.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: th
og_description: ทำให้การสลับสีแถวในแผ่นงาน C# ง่ายขึ้น เรียนรู้การตั้งค่าพื้นหลังเซลล์
  ใช้รูปแบบการเติมสีแบบทึบ และเชี่ยวชาญสไตล์เซลล์ของแผ่นงาน
og_title: สีแถวสลับในแผ่นงาน C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: สีแถวสลับในแผ่นงาน C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสลับสีแถวใน Worksheet ของ C# – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่าจะทำให้การส่งออก Excel ของคุณดูเป็นมืออาชีพด้วย **การสลับสีแถว**? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามวิธี *เพิ่มสีพื้นหลัง* ให้กับแถวโดยไม่ต้องเขียนโค้ดหลายพันบรรทัด  

ในบทเรียนนี้เราจะอธิบายวิธีง่าย ๆ เพื่อ **ตั้งค่าสีพื้นหลังของเซลล์** ในแต่ละแถว, ใช้ **รูปแบบการเติมสีแบบทึบ**, และควบคุม **สไตล์ของเซลล์ใน Worksheet** เพื่อให้ผลลัพธ์อ่านง่ายและดูสวยงาม

## สิ่งที่คุณจะได้เรียนรู้

- ดึงข้อมูลเข้าสู่ `DataTable` (หรือแหล่งข้อมูลตารางใด ๆ)  
- สร้างอาเรย์ของอ็อบเจกต์ `Style` ที่สลับสีสองสีกัน  
- นำเข้า `DataTable` ไปยัง Worksheet พร้อมใช้สไตล์เหล่านั้น  
- ตรวจสอบผลลัพธ์และปรับสีหรือรูปแบบตามต้องการ  

ไม่ต้องใช้เครื่องมือภายนอกนอกจากสภาพแวดล้อม .NET และไลบรารีสเปรดชีต (เราจะใช้ **Aspose.Cells** ในตัวอย่าง) เพียงเท่านี้ คุณจะได้เมธอดที่นำกลับมาใช้ใหม่ได้ในทุก pipeline ของการรายงาน

---

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเป็น `DataTable`

ก่อนอื่น—หากไม่มีข้อมูลก็ไม่มีอะไรให้จัดรูปแบบ ด้านล่างเป็นตัวช่วยขนาดเล็กที่สร้าง `DataTable` พร้อมแถวตัวอย่าง ในโปรเจกต์จริงคุณจะแทนที่ส่วนนี้ด้วยการเรียกฐานข้อมูลหรือพาร์เซอร์ CSV

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การมีข้อมูลใน `DataTable` ทำให้เครื่องยนต์ Worksheet สามารถ *นำเข้า* ข้อมูลได้ในครั้งเดียว โดยอัตโนมัติรักษาชื่อคอลัมน์และประเภทข้อมูลไว้

## ขั้นตอนที่ 2: สร้างสไตล์ **การสลับสีแถว**

ต่อไปเราจะสร้างอาเรย์ของอ็อบเจกต์ `Style` — หนึ่งอ็อบเจกต์ต่อหนึ่งแถว — เพื่อให้แถวเลขคู่ใช้สีเหลืองอ่อน ส่วนแถวเลขคี่ใช้สีฟ้าอ่อน นี่คือหัวใจของเทคนิค **การสลับสีแถว**

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### ทำไมต้องใช้ **รูปแบบการเติมสีแบบทึบ**?

คุณสมบัติ `Pattern` บอกเครื่องยนต์ว่าจะวาดสีอย่างไร การเติมแบบ `Solid` รับประกันว่าพื้นหลังของเซลล์ทั้งหมดจะถูกทาสีเต็มที่ ไม่ให้เส้นกริดบาง ๆ ปรากฏ นี่เป็นวิธีที่นิยมที่สุดในการ **ตั้งค่าสีพื้นหลังของเซลล์** เมื่อคุณต้องการลุคที่เรียบง่าย

## ขั้นตอนที่ 3: นำเข้า `DataTable` พร้อมสไตล์ที่เตรียมไว้

เมื่ออาเรย์สไตล์พร้อม การเรียกนำเข้าก็เหลือเพียงบรรทัดเดียว Aspose.Cells จะใช้สไตล์ที่ตรงกับแต่ละแถวโดยอัตโนมัติ

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **อะไรเกิดขึ้นเบื้องหลัง?**  
> ไลบรารีวนลูปผ่านแต่ละแถว คัดลอกค่าไปยังเซลล์ แล้วนำ `Style` ที่ตรงจาก `rowStyles` ไปใช้ เนื่องจากเราได้กำหนด **รูปแบบการเติมสีแบบทึบ** ไว้แล้ว ทุกเซลล์ในแถวนั้นจึงรับสีพื้นหลังเดียวกัน ทำให้ได้ **การสลับสีแถว** อย่างสมบูรณ์แบบ

## ขั้นตอนที่ 4: บันทึก Workbook และตรวจสอบผลลัพธ์

การบันทึกอย่างรวดเร็วทำให้คุณเปิดไฟล์ใน Excel (หรือโปรแกรมดูที่รองรับ) และเห็นผลลัพธ์ได้ทันที

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

เมื่อเปิดไฟล์ แถว 1, 3, 5… จะเป็นสีเหลืองอ่อน ส่วนแถว 2, 4, 6… จะเป็นสีฟ้าอ่อน ส่วนหัวคอลัมน์ยังคงสีขาว ทำให้ข้อมูลโดดเด่น

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*ข้อความแทนภาพ:* **การสลับสีแถว** ภาพหน้าจอของ Worksheet ที่พื้นหลังของแต่ละแถวสลับระหว่างสีเหลืองอ่อนและสีฟ้าอ่อน

## ขั้นตอนที่ 5: ปรับแต่งเพิ่มเติม (ตามต้องการ)

### เปลี่ยนสี

หากแบรนด์ของคุณใช้สีอื่น เพียงเปลี่ยน `Color.LightYellow` และ `Color.LightCyan` เป็น `System.Drawing.Color` ใดก็ได้ที่คุณต้องการ ตัวอย่างเช่น:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### ใช้ **ประเภทพื้นหลัง** แบบอื่น

แม้ว่า `BackgroundType.Solid` จะเป็นที่นิยมที่สุด คุณก็สามารถทดลองใช้ `BackgroundType.Gray125`, `BackgroundType.Horizontal` หรือรูปแบบใด ๆ ที่ไลบรารีสนับสนุน การเปลี่ยนนี้จะทำให้พื้นผิวดูแตกต่างในขณะที่ยัง **เพิ่มสีพื้นหลัง** อยู่

### ใช้ **Worksheet Cell Style** กับคอลัมน์เฉพาะ

บางครั้งคุณอาจต้องการให้เอฟเฟกต์สลับสีใช้เฉพาะคอลัมน์ข้อมูล โดยให้คอลัมน์แรก (เช่น ID) คงสีเดิม สร้างสไตล์แยกสำหรับคอลัมน์นั้นและกำหนดหลังการนำเข้า:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## สรุป

คุณได้วิธีแก้ปัญหา **การสลับสีแถว** ใน Worksheet ของ C# ที่ครบถ้วนและนำกลับมาใช้ใหม่ได้ ด้วยการสร้างอาเรย์ของอ็อบเจกต์ `Style`, **ตั้งค่าสีพื้นหลัง** ด้วย **รูปแบบการเติมสีแบบทึบ**, และนำเข้า `DataTable` ในหนึ่งขั้นตอน คุณสามารถสร้างรายงานที่ดูเป็นมืออาชีพด้วยโค้ดเพียงเล็กน้อย  

ต่อจากนี้คุณอาจ:

- **เพิ่มสีพื้นหลัง** ให้กับแถวหัวตารางเพื่อเน้นย้ำเพิ่มเติม  
- ผสานเทคนิคนี้กับการจัดรูปแบบตามเงื่อนไขเพื่อให้ได้สัญญาณภาพแบบไดนามิก  
- สำรวจคุณสมบัติอื่น ๆ ของ **Worksheet Cell Style** เช่น ฟอนต์, เส้นขอบ, หรือรูปแบบตัวเลข  

ลองใช้ในกระบวนการส่งออกครั้งต่อไปของคุณ—ผู้ใช้จะขอบคุณคุณสำหรับสเปรดชีตที่สะอาดตาและอ่านง่าย ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

- [ตั้งค่าความสูงของแถวใน Worksheet ด้วย Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [แปลงชื่อเซลล์ Excel เป็นดัชนีแถวและคอลัมน์โดยใช้ Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [ตั้งค่าสีแท็บ Worksheet ใน Excel ด้วย Aspose.Cells .NET - คู่มือฉบับสมบูรณ์](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}