---
category: general
date: 2026-04-07
description: เพิ่มสีพื้นหลังให้แถวใน Excel ด้วย C# เรียนรู้วิธีใช้สีแถวสลับ, ตั้งค่าสไตล์พื้นหลังแบบทึบ,
  และนำเข้าตารางข้อมูลไปยัง Excel ในขั้นตอนเดียว
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: th
og_description: เพิ่มสีพื้นหลังให้แถวใน Excel ด้วย C# คู่มือนี้แสดงวิธีตั้งค่าสีแถวสลับ,
  ตั้งค่าสีพื้นหลังแบบทึบ, และนำเข้า DataTable ไปยัง Excel อย่างมีประสิทธิภาพ.
og_title: เพิ่มสีพื้นหลังใน Excel – สไตล์แถวสลับใน C#
tags:
- C#
- Excel
- DataTable
- Styling
title: เพิ่มสีพื้นหลังใน Excel – สไตล์แถวสลับใน C#
url: /th/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add background color excel – Alternating Row Styles in C#

เคยต้องการ **add background color excel** แถวแต่ไม่แน่ใจว่าจะทำอย่างไรโดยไม่ต้องเขียนโค้ดหลายพันบรรทัดไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่ก็เจออุปสรรคนี้เมื่อต้องการทำให้สเปรดชีตของพวกเขาดูมากกว่าการ dump ข้อมูลแบบดิบ  

ข่าวดีคืออะไร? ในเวลาเพียงไม่กี่นาทีคุณก็สามารถ **apply alternating row colors**, ตั้งค่า **solid background**, และแม้กระทั่ง **import datatable to excel** ด้วยแพทเทิร์นที่สะอาดและนำกลับมาใช้ใหม่ได้ใน C#  

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การดึงข้อมูลเข้า `DataTable` ไปจนถึงการจัดสไตล์แต่ละแถวด้วยลายเส้นสีเหลือง‑ขาวอ่อน ไม่ต้องใช้ไลบรารีภายนอกนอกจากแพคเกจจัดการ Excel ที่มั่นคง (เช่น **ClosedXML** หรือ **GemBox.Spreadsheet**) และคุณจะเห็นว่าทำไมวิธีนี้จึงมีประสิทธิภาพและง่ายต่อการบำรุงรักษา

## What You’ll Learn

- วิธีดึงข้อมูลและใส่ลงใน worksheet ของ Excel
- วิธี **style excel rows** ด้วยสีพื้นหลังสลับ
- กลไกของการ **set solid background** ด้วยอ็อบเจ็กต์ `Style`
- วิธี **import datatable to excel** พร้อมคงสไตล์ของแถว
- เคล็ดลับการจัดการ edge cases เช่น ตารางว่างหรือโครงสร้างสีที่กำหนดเอง

> **Pro tip:** หากคุณกำลังใช้อ็อบเจ็กต์ workbook (`wb`) จากไลบรารีที่รองรับการสร้างสไตล์ คุณสามารถใช้ `Style` เดียวกันซ้ำในหลาย worksheet—ช่วยประหยัดหน่วยความจำและทำให้โค้ดของคุณเป็นระเบียบ

---

## Step 1: Retrieve the Data – Preparing the DataTable

ก่อนที่การจัดสไตล์ใด ๆ จะเกิดขึ้น เราต้องมีแหล่งข้อมูลของแถว ในสถานการณ์จริงส่วนใหญ่ข้อมูลมาจากฐานข้อมูล, API, หรือไฟล์ CSV สำหรับการอธิบาย เราจะสร้าง `DataTable` ง่าย ๆ ในหน่วยความจำ

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** การใช้ `DataTable` ให้คุณได้คอนเทนเนอร์แบบตารางที่รับรู้สกีม่า ซึ่งไลบรารี Excel สามารถนำเข้าโดยตรง ลดความจำเป็นในการเขียนลูปเซลล์‑ต่อ‑เซลล์

---

## Step 2: Create Row Styles – **Apply alternating row colors**

ต่อไปเราจะสร้างอาร์เรย์ของอ็อบเจ็กต์ `Style` — หนึ่งอ็อบเจ็กต์ต่อหนึ่งแถว — เพื่อให้แต่ละแถวสามารถรับพื้นหลังของตนเองได้ รูปแบบที่เราจะใช้คือสีเหลืองอ่อนสำหรับแถวคู่และสีขาวสำหรับแถวคี่

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**คำอธิบาย:**  
- `wb.CreateStyle()` ให้คุณได้อ็อบเจ็กต์สไตล์ที่สะอาดซึ่งคุณสามารถปรับแต่งได้โดยไม่กระทบต่ออื่น  
- ตัวดำเนินการ ternary `(i % 2 == 0)` ตัดสินใจว่าแถวเป็นเลขคู่ (สีเหลืองอ่อน) หรือเลขคี่ (สีขาว)  
- การตั้งค่า `Pattern = BackgroundType.Solid` เป็นขั้นตอนสำคัญที่ **set solid background**; หากไม่ทำสีจะถูกละเลย

---

## Step 3: Grab the Target Worksheet

ไลบรารีส่วนใหญ่จะเปิดเผยคอลเลกชันของ worksheet เราจะทำงานกับอันแรก แต่คุณสามารถเลือกตามดัชนีหรือชื่อที่ต้องการได้

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

หาก workbook เป็นใหม่ไลบรารีมักจะสร้าง sheet เริ่มต้นให้โดยอัตโนมัติ หากไม่เป็นเช่นนั้นคุณสามารถเพิ่ม sheet อย่างชัดเจนได้:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Step 4: Import the DataTable with Row Styles – **Import datatable to excel**

เมื่อสไตล์พร้อม ขั้นตอนสุดท้ายคือการนำ `DataTable` ไปใส่ใน sheet พร้อมใช้สไตล์ที่สอดคล้องกับแต่ละแถว

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**อะไรที่เกิดขึ้นเบื้องหลัง?**  
- `true` บอกเมธอดให้เขียนหัวคอลัมน์เป็นแถวแรก  
- `0, 0` ระบุตำแหน่งมุมบนซ้าย (A1) เป็นจุดแทรก  
- `rowStyles` จัดสไตล์ `Style` ให้ตรงกับแถวข้อมูลที่สอดคล้องกัน ทำให้ได้สีสลับที่เราจัดเตรียมไว้ก่อนหน้า

---

## Step 5: Save the Workbook

ส่วนสุดท้ายของปริศนาคือการบันทึก workbook ลงไฟล์เพื่อให้คุณเปิดใน Excel และดูผลลัพธ์

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

เปิดไฟล์และคุณควรเห็น sheet ที่จัดรูปแบบอย่างเรียบร้อย:

- แถวหัวเรื่องเป็นตัวหนา (สไตล์เริ่มต้นของไลบรารี)  
- แถว 1, 3, 5… มีพื้นหลังสีขาวสะอาด  
- แถว 2, 4, 6… มีสีเติมสีเหลืองอ่อนเบา ทำให้สแกนง่าย

### Expected Output Snapshot

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

แถว 2, 4, 6, … ปรากฏด้วยพื้นหลังสีเหลืองอ่อน — ตรงกับเอฟเฟกต์ **apply alternating row colors** ที่เราตั้งเป้าไว้

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt text includes the primary keyword for SEO.)*

---

## Handling Edge Cases & Variations

### Empty DataTable

หาก `dataTable.Rows.Count` เป็นศูนย์ อาร์เรย์ `rowStyles` จะว่างเปล่าและ `ImportDataTable` ยังเขียนแถวหัวเรื่อง (หาก `includeHeaders` เป็น `true`) ไม่เกิดข้อยกเว้น แต่คุณอาจต้องป้องกันการสร้างไฟล์ที่เกือบว่างเปล่า:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Custom Colour Schemes

ต้องการลายเส้นสีน้ำเงิน/เท้าแทนสีเหลือง/ขาว? เพียงเปลี่ยนค่า `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

ลองดึงสีจากไฟล์คอนฟิกเพื่อให้ผู้ที่ไม่ใช่นักพัฒนาสามารถปรับพาเลตต์ได้โดยไม่ต้องแก้โค้ด

### Re‑using Styles Across Multiple Worksheets

หากคุณส่งออกหลายตารางไปยัง workbook เดียวกัน คุณสามารถสร้างอาร์เรย์สไตล์ครั้งเดียวแล้วใช้ซ้ำได้:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

แค่ต้องระวังให้ตารางทั้งสองมีจำนวนแถวเท่ากัน หรือสร้างอาร์เรย์ใหม่ต่อแต่ละ sheet

---

## Full Working Example

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่สามารถคัดลอก‑วางลงในแอปคอนโซลได้

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

รันโปรแกรม, เปิด `Report.xlsx`, แล้วคุณจะเห็นพื้นหลังสลับตามที่อธิบายไว้

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}