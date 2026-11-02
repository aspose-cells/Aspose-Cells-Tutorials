---
category: general
date: 2026-02-21
description: เรียนรู้วิธีจัดรูปแบบคอลัมน์เมื่อคุณนำเข้า DataTable ไปยัง Excel ด้วย
  C# รวมเคล็ดลับการใส่สีให้คอลัมน์ที่สองใน Excel และการนำเข้า DataTable ไปยัง Excel
  ด้วย C#
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: th
og_description: วิธีจัดรูปแบบคอลัมน์เมื่อนำเข้า DataTable ไปยัง Excel ด้วย C# โค้ดขั้นตอนต่อขั้นตอน
  การทำสีคอลัมน์ที่สองใน Excel และแนวปฏิบัติที่ดีที่สุด
og_title: วิธีจัดรูปแบบคอลัมน์ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: วิธีจัดรูปแบบคอลัมน์ใน Excel ด้วย C# – นำเข้า DataTable
url: /th/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำให้คอลัมน์ใน Excel มีสไตล์ด้วย C# – นำเข้า DataTable

เคยสงสัย **วิธีทำให้คอลัมน์มีสไตล์** ในแผ่นงาน Excel ขณะดึงข้อมูลโดยตรงจาก `DataTable` หรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาหลายคนมักติดขัดเมื่อต้องการเพิ่มสีสันอย่างรวดเร็ว—อาจเป็นสีแดงสำหรับคอลัมน์แรก, สีน้ำเงินสำหรับคอลัมน์ที่สอง—โดยไม่ต้องแก้ไขแต่ละเซลล์หลังจากการนำเข้า  

ข่าวดีคือ? คำตอบอยู่ในไม่กี่บรรทัดของโค้ด C# และคุณจะได้แผ่นงานที่มีสไตล์เต็มรูปแบบทันทีที่ข้อมูลถูกใส่ลงไป ในบทเรียนนี้เราจะครอบคลุม **import datatable to excel**, แสดงวิธี **color second column excel**, และอธิบายว่าทำไมวิธีนี้จึงทำงานได้ทั้งในโครงการ .NET Framework และ .NET 6+

---

## สิ่งที่คุณจะได้เรียนรู้

- ดึง `DataTable` ที่มีข้อมูล (หรือสร้างใหม่แบบทันที)  
- กำหนดอ็อบเจ็กต์ `Style` แยกตามคอลัมน์เพื่อกำหนดสีข้อความ  
- สร้าง workbook, ดึง worksheet แรก, และนำเข้าตารางพร้อมสไตล์ที่กำหนด  
- จัดการกรณีขอบเช่น ตารางว่าง, เริ่มแถวจากตำแหน่งที่กำหนด, และจำนวนคอลัมน์ที่เปลี่ยนแปลงได้  

เมื่อเสร็จสิ้น คุณจะสามารถสร้างไฟล์ Excel ที่มีสไตล์แล้วใส่ลงใน pipeline การรายงานใด ๆ ได้โดยไม่ต้องทำ post‑processing

> **Prerequisite:** ความคุ้นเคยพื้นฐานกับ C# และการอ้างอิงไลบรารีสเปรดชีตที่รองรับ `ImportDataTable` (เช่น Aspose.Cells, GemBox.Spreadsheet, หรือ EPPlus พร้อม helper) โค้ดด้านล่างใช้ **Aspose.Cells** เนื่องจาก overload ของ `ImportDataTable` รับ `Style[]` โดยตรง

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่มไลบรารี Excel

ก่อนที่เราจะทำสไตล์ใด ๆ เราต้องมีโปรเจกต์ที่อ้างอิงไลบรารีการจัดการ Excel

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Pro tip:* หากคุณใช้ .NET 6 ให้เพิ่มแพ็กเกจด้วยคำสั่ง `dotnet add package Aspose.Cells` ไลบรารีทำงานได้บน Windows, Linux, และ macOS ทำให้คุณพร้อมสำหรับอนาคต

---

## ขั้นตอนที่ 2: ดึงหรือสร้าง DataTable แหล่งข้อมูล

หัวใจของบทเรียนคือการทำสไตล์ แต่คุณยังต้องมี `DataTable` ตัวอย่างด้านล่างเป็น helper สั้น ๆ ที่สร้างข้อมูลตัวอย่าง; ในการใช้งานจริงให้แทนที่ด้วยการเรียก `GetTable()` ของคุณเอง

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Why this matters:** การใช้ `DataTable` ทำให้แหล่งข้อมูลของคุณเป็นกลาง—ไม่ว่าจะมาจาก SQL, CSV, หรือคอลเลกชันในหน่วยความจำ, โลจิกการนำเข้าจะเหมือนกัน นี่คือพื้นฐานของ **how to import datatable** อย่างมีประสิทธิภาพ

---

## ขั้นตอนที่ 3: กำหนดสไตล์คอลัมน์ (หัวใจของ “How to Style Columns”)

ตอนนี้เราจะบอก worksheet ว่าคอลัมน์แต่ละอันควรมีลักษณะอย่างไร คลาส `Style` ให้คุณตั้งค่าแบบอักษร, สี, เส้นขอบ, และอื่น ๆ สำหรับตัวอย่างนี้เราจะเปลี่ยนเฉพาะสีข้อความ

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*What if you have more columns?* เพียงเพิ่มขนาดของอาร์เรย์และใส่สไตล์ที่ต้องการ คอลัมน์ที่ไม่ได้กำหนดสไตล์จะสืบทอดสไตล์เริ่มต้นของ worksheet โดยอัตโนมัติ

---

## ขั้นตอนที่ 4: สร้าง Workbook และนำเข้า DataTable พร้อมสไตล์

เมื่อข้อมูลและสไตล์พร้อมแล้ว ถึงเวลานำทุกอย่างมารวมกัน

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**What just happened?**  
- `ImportDataTable` คัดลอกแถว, คอลัมน์, และ *โดยอาจ* รวมแถวหัวตาราง  
- โดยการส่ง `columnStyles` ให้แต่ละคอลัมน์ได้รับ `Style` ที่เรากำหนดไว้ก่อนหน้า  
- คำสั่งนี้เป็นบรรทัดเดียว ทำให้ **import datatable excel c#** ง่ายเพียงเท่านี้

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ – ผลลัพธ์ที่คาดหวัง

เปิดไฟล์ `StyledDataTable.xlsx` ด้วย Excel (หรือ LibreOffice) คุณควรเห็น:

| **ID** (สีแดง) | **Name** (สีน้ำเงิน) | **Score** (ค่าเริ่มต้น) |
|----------------|-----------------------|--------------------------|
| 1              | Alice                 | 92.5                     |
| 2              | Bob                   | 85.3                     |
| …              | …                     | …                        |

- ข้อความในคอลัมน์แรกแสดงเป็น **สีแดง**, ตรงตามความต้องการ “how to style columns”  
- ข้อความในคอลัมน์ที่สองเป็น **สีน้ำเงิน**, ครอบคลุมคำค้น **color second column excel**  

หากไฟล์เปิดโดยไม่มีข้อผิดพลาด คุณได้เชี่ยวชาญ **how to import datatable** พร้อมการทำสไตล์คอลัมน์แล้ว

---

## คำถามทั่วไป & กรณีขอบ

### ถ้า DataTable ว่างจะทำอย่างไร?
`ImportDataTable` จะยังคงสร้างแถวหัวตาราง (หากคุณส่ง `true`) ไม่มีแถวข้อมูลเพิ่มเข้ามา แต่สไตล์ยังคงถูกนำไปใช้กับเซลล์หัวตาราง

### ต้องการเริ่มนำเข้าที่เซลล์อื่น?
เปลี่ยนพารามิเตอร์ `rowIndex` และ `columnIndex` ใน `ImportDataTable` ตัวอย่างเช่น เริ่มที่ `B2` ให้ใช้ `1, 1` แทน `0, 0`

### อยากทำสไตล์ให้แถวแทนคอลัมน์?
คุณสามารถวนลูป `worksheet.Cells.Rows` หลังการนำเข้าและกำหนด `Style` ให้แต่ละแถวได้ อย่างไรก็ตาม การทำสไตล์ระดับคอลัมน์จะทำงานได้เร็วกว่าเพราะไลบรารีกำหนดสไตล์เพียงครั้งเดียวต่อคอลัมน์

### ใช้ EPPlus หรือ ClosedXML?
ไลบรารีเหล่านั้นไม่มี overload ของ `ImportDataTable` ที่รับอาร์เรย์สไตล์โดยตรง วิธีแก้คือให้นำเข้าตารางก่อน แล้ววนลูปช่วงคอลัมน์เพื่อกำหนด `Style.Font.Color.SetColor(...)` โลจิกยังคงเหมือนเดิม เพียงเพิ่มไม่กี่บรรทัด

---

## เคล็ดลับระดับ Production‑Ready

- **Reuse Styles:** การสร้าง `Style` ใหม่สำหรับทุกคอลัมน์อาจทำให้ใช้ทรัพยากรเกิน ควรเก็บสไตล์ที่ใช้บ่อยใน dictionary โดยใช้สีหรือความหนาของฟอนต์เป็นคีย์  
- **Avoid Hard‑Coded Column Counts:** ตรวจจับ `dataTable.Columns.Count` แล้วสร้างอาร์เรย์ `columnStyles` อย่างไดนามิก  
- **Thread Safety:** หากคุณสร้าง workbook หลายไฟล์พร้อมกัน ให้สร้าง `Workbook` แยกตามเธรด; อ็อบเจ็กต์ของ Aspose.Cells ไม่ปลอดภัยต่อการทำงานหลายเธรดพร้อมกัน  
- **Performance:** สำหรับตารางที่ใหญ่กว่า 10 k แถว ควรปิด `AutoFitColumns` (ทำการสแกนทุกเซลล์) และกำหนดความกว้างคอลัมน์ด้วยตนเอง

---

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste Ready)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

รันโปรแกรม เปิดไฟล์ `StyledDataTable.xlsx` ที่สร้างขึ้น คุณจะเห็นคอลัมน์ที่มีสีทันที นั่นคือ workflow ทั้งหมดของ **import datatable excel c#** ในหนึ่งย่อหน้า

---

## สรุป

เราได้อธิบาย **วิธีทำให้คอลัมน์มีสไตล์** ขณะ **import datatable to excel** ด้วย C# โดยการกำหนดอาร์เรย์ `Style[]` แล้วส่งให้ `ImportDataTable` คุณสามารถทำให้คอลัมน์แรกเป็นสีแดง, คอลัมน์ที่สองเป็นสีน้ำเงิน, และคอลัมน์ที่เหลือคงค่าเริ่มต้น—ทั้งหมดในบรรทัดเดียวของโค้ด  

วิธีนี้ขยายได้ง่าย: เพิ่ม `Style` สำหรับคอลัมน์เพิ่มเติม, ปรับแถวเริ่มต้น, หรือสลับไลบรารี Aspose.Cells ไปเป็นไลบรารีอื่นที่มี API คล้ายกัน ตอนนี้คุณสามารถสร้างรายงาน Excel ที่ดูเป็นมืออาชีพโดยไม่ต้องแก้ไขไฟล์ด้วยตนเอง

**ขั้นตอนต่อไป** ที่คุณอาจสนใจ:

- ใช้ **conditional formatting** เพื่อไฮไลต์ค่าตามเงื่อนไข (เชื่อมโยงกับ “color second column excel”)  
- ส่งออกหลาย worksheet จากชุด `DataTable` เดียว (เหมาะสำหรับแดชบอร์ดรายเดือน)  
- ผสานกับการแปลง **CSV → DataTable** เพื่อสร้างโซลูชันแบบ end‑to‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}