---
category: general
date: 2026-03-01
description: นำเข้าข้อมูลพร้อมการจัดรูปแบบไปยัง Excel ด้วย C# เรียนรู้วิธีนำเข้า DataTable
  ไปยัง Excel และเพิ่มสีพื้นหลังให้กับเซลล์ในไม่กี่ขั้นตอน.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: th
og_description: นำเข้าข้อมูลพร้อมการจัดรูปแบบไปยัง Excel ด้วย C# คู่มือแบบขั้นตอนที่แสดงวิธีนำเข้า
  DataTable และเพิ่มสีพื้นหลังให้กับเซลล์
og_title: นำเข้าข้อมูลพร้อมการจัดรูปแบบไปยัง Excel – คู่มือ C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: นำเข้าข้อมูลพร้อมการจัดรูปแบบไปยัง Excel ด้วย C#
url: /th/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# นำเข้าข้อมูลพร้อมการจัดรูปแบบไปยัง Excel ด้วย C#

เคยต้องการ **import data with formatting** ไปยัง workbook ของ Excel แต่กลับได้แผ่นงานที่ดูธรรมดาและน่าเบื่อหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ นักพัฒนาส่วนใหญ่มักเจอเมื่อพบว่าการนำเข้ามาตรฐานจะลบสีและสไตล์ทั้งหมดที่คุณตั้งค่าอย่างละเอียดในข้อมูลต้นทาง

ในบทแนะนำนี้ เราจะพาคุณผ่านโซลูชันที่สมบูรณ์พร้อมรันได้ทันทีที่ **imports a DataTable into Excel** และ **adds background color to Excel cells** พร้อมกัน ไม่ต้องทำการประมวลผลเพิ่มเติม—สเปรดชีตของคุณจะดูตรงตามที่ต้องการตั้งแต่แรก

## สิ่งที่คุณจะได้เรียนรู้

- วิธีดึงข้อมูลเข้าสู่ `DataTable`.
- วิธีกำหนดอาร์เรย์ของอ็อบเจ็กต์ `Style` ที่มีสีพื้นหลัง.
- วิธีเรียก `ImportDataTable` พร้อมสไตล์เหล่านั้นเพื่อให้การนำเข้ารักษาการจัดรูปแบบ.
- ตัวอย่างเต็มที่สามารถรันได้ซึ่งคุณสามารถนำไปใส่ในแอปคอนโซลและดูผลลัพธ์ได้ทันที.
- เคล็ดลับ, จุดบกพร่อง, และรูปแบบต่าง ๆ สำหรับโครงการจริง.

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานได้กับ .NET Framework 4.6+ ด้วย).
- ไลบรารี **GemBox.Spreadsheet** (เวอร์ชันฟรีเพียงพอสำหรับการสาธิต).
- ความคุ้นเคยพื้นฐานกับ C# และแนวคิดของ Excel.

หากคุณสงสัย *ทำไมต้อง GemBox?* เพราะมันมีเมธอด `ImportDataTable` แบบบรรทัดเดียวที่รับอาร์เรย์ของสไตล์—ตรงกับสิ่งที่เราต้องการเพื่อ **import data with formatting** โดยไม่ต้องเขียนลูป.

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม GemBox.Spreadsheet

เริ่มต้นโดยสร้างแอปคอนโซลใหม่:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** เวอร์ชันฟรีจำกัดจำนวนเซลล์ต่อ worksheet ที่ 150 k เซลล์ ซึ่งเพียงพอสำหรับการสาธิต หากคุณถึงขีดจำกัด ให้อัปเกรดหรือเปลี่ยนไปใช้ EPPlus แต่ API จะดูแตกต่างกันเล็กน้อย.

## ขั้นตอนที่ 2: ดึงข้อมูลต้นทางเป็น `DataTable`

สิ่งแรกที่เราต้องการคือ `DataTable` ที่จำลองข้อมูลที่คุณมักดึงจากฐานข้อมูล นี่คือฟังก์ชันช่วยเล็ก ๆ ที่สร้างขึ้นในหน่วยความจำ:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**ทำไมเรื่องนี้สำคัญ:** การแยกการดึงข้อมูลออกเป็นเมธอดของตัวเอง ทำให้คุณสามารถสลับแหล่งข้อมูลใดก็ได้—SQL, CSV, เว็บเซอร์วิส—โดยไม่ต้องแก้ไขตรรกะการนำเข้า ซึ่งทำให้โค้ดสะอาดและทำให้บทแนะนำ **how to import datatable into excel** ใช้ซ้ำได้.

## ขั้นตอนที่ 3: กำหนดสไตล์ที่ต้องการใช้

ต่อมาคือส่วนที่สนุก: เราจะสร้างอาร์เรย์ของอ็อบเจ็กต์ `Style` แต่ละอันมี `ForegroundColor` ที่แตกต่างกัน GemBox ให้คุณตั้งค่า `BackgroundPatternColor` (สีพื้นหลังของเซลล์) และ `ForegroundColor` (สีข้อความ) สำหรับการสาธิตนี้ เราจะให้สีแตกต่างกันในสองคอลัมน์แรก.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**คำอธิบาย:**  
- อ็อบเจ็กต์ `Style` เป็นคอนเทนเนอร์ที่มีน้ำหนักเบา; คุณไม่จำเป็นต้องสร้างใหม่สำหรับทุกเซลล์.  
- โดยจัดลำดับของอาร์เรย์ให้ตรงกับลำดับคอลัมน์, GemBox จะใช้สไตล์ที่ตรงกันโดยอัตโนมัติระหว่างการนำเข้า.  
- นี่คือกุญแจสำคัญสำหรับ **import data with formatting**—การจัดรูปแบบจะเดินทางพร้อมกับข้อมูล, ไม่ได้ทำภายหลัง.

## ขั้นตอนที่ 4: นำเข้า `DataTable` ไปยัง Worksheet พร้อมสไตล์

เมื่อข้อมูลและสไตล์พร้อมแล้ว เราสามารถสร้าง workbook, เลือก worksheet แรก, และเรียก `ImportDataTable`. ลายเซ็นของเมธอดมีดังนี้:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

นี่คือตัวอย่างการใช้:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**สิ่งที่เกิดขึ้นภายใน:**  
- `true` บอก GemBox ให้เขียนชื่อคอลัมน์เป็นแถวแรก.  
- `0, 0` กำหนดตำแหน่งการนำเข้าที่เซลล์ A1.  
- `importStyles` เชื่อมแต่ละคอลัมน์กับสีที่เรากำหนดไว้ก่อนหน้า.  

เมื่อคุณเปิด *Report.xlsx*, คุณจะเห็นคอลัมน์ **ID** มีพื้นหลังสีฟ้าอ่อน, คอลัมน์ **Name** มีพื้นหลังสีเขียวอ่อน, และคอลัมน์ **Score** ไม่เปลี่ยนแปลง นั่นคือ **import data with formatting** ในการเรียกครั้งเดียว.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ (ผลลัพธ์ที่คาดหวัง)

เปิดไฟล์ `Report.xlsx` ที่สร้างขึ้น คุณควรเห็นดังนี้:

| ID (สีฟ้าอ่อน) | Name (สีเขียวอ่อน) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- เซลล์ในคอลัมน์ **ID** มีพื้นหลังสีฟ้าอ่อน.
- เซลล์ในคอลัมน์ **Name** มีพื้นหลังสีเขียวอ่อน.
- คอลัมน์ **Score** ยังคงพื้นหลังสีขาวตามค่าเริ่มต้น.

![แผ่นงาน Excel แสดง import data with formatting – คอลัมน์ ID สีฟ้าอ่อน, คอลัมน์ Name สีเขียวอ่อน](excel-screenshot.png "ตัวอย่าง import data with formatting")

*ข้อความ alt ของรูปภาพรวมถึงคีย์เวิร์ดหลักสำหรับ SEO*

## คำถามทั่วไปและกรณีขอบ

### สามารถใช้ได้มากก่าสีพื้นหลังหรือไม่?

แน่นอน. `Style` ให้คุณตั้งค่าแบบอักษร, เส้นขอบ, รูปแบบตัวเลข, และแม้กระทั่ง conditional formatting. ตัวอย่างเช่น เพื่อทำให้คะแนนที่มากกว่า 90 เป็นตัวหนาและสีแดง:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### ถ้า `DataTable` ของฉันมีคอลัมน์มากกว่าจำนวนสไตล์จะทำอย่างไร?

GemBox จะใช้สไตล์เฉพาะกับคอลัมน์ที่มีรายการที่ตรงกันในอาร์เรย์ คอลัมน์ที่เหลือจะใช้สไตล์เริ่มต้น—ไม่มีข้อผิดพลาดเกิดขึ้น.

### วิธีนี้ทำงานกับชุดข้อมูลขนาดใหญ่หรือไม่?

ใช่, แต่ควรระวังขีดจำกัดเซลล์ของเวอร์ชันฟรี (150 k เซลล์). สำหรับรายงานขนาดใหญ่, พิจารณาใช้ไลเซนส์แบบชำระเงินหรือสตรีมข้อมูลทีละแถวด้วย `worksheet.Cells[row, col].Value = …`—แม้ว่าจะเสียความสะดวกของการเรียกแบบบรรทัดเดียว.

### จะนำเข้าข้อมูลพร้อมการจัดรูปแบบจากเทมเพลต Excel ที่มีอยู่ได้อย่างไร?

คุณสามารถโหลดเทมเพลต workbook ก่อนได้:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

วิธีนี้ทำให้คุณคงโลโก้ส่วนหัว, ส่วนท้าย, และสไตล์ที่มีอยู่ก่อนหน้าไว้ได้พร้อมกับยังคง **import data with formatting** สำหรับส่วนที่เป็นข้อมูลแบบไดนามิก.

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

นี่คือตัวอย่างเต็มที่พร้อมคัดลอก‑วาง:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

เรียกใช้โปรแกรม (`dotnet run`) และเปิดไฟล์ *Report.xlsx* ที่สร้างขึ้นเพื่อดูสีที่ถูกนำไปใช้ทันที.

## สรุป

คุณตอนนี้มีพื้นฐานที่มั่นคง, สิ้นสุด

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}