---
category: general
date: 2026-02-15
description: สร้าง workbook ด้วย C# และส่งออก DataTable ไปยัง Excel พร้อมการจัดรูปแบบแถว
  ตั้งค่าพื้นหลังของแถว และทำงานอัตโนมัติใน Excel ภายในไม่กี่นาที.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: th
og_description: สร้างเวิร์กบุ๊กด้วย C# อย่างรวดเร็ว, ใช้สไตล์แถว, และอัตโนมัติการส่งออก
  Excel พร้อมตัวอย่างโค้ดเต็มและเคล็ดลับการปฏิบัติที่ดีที่สุด.
og_title: สร้าง Workbook C# – ส่งออก DataTable ไปยัง Excel พร้อมการจัดรูปแบบ
tags:
- C#
- Excel
- DataExport
title: สร้าง Workbook ด้วย C# – ส่งออก DataTable ไปยัง Excel พร้อมการจัดรูปแบบ
url: /th/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Workbook C# – ส่งออก DataTable ไปยัง Excel พร้อมการจัดรูปแบบ

เคยต้องการ **create workbook C#** และส่ง `DataTable` ไปยัง Excel พร้อมสไตล์ที่กำหนดเองหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายแอปพลิเคชันเชิงธุรกิจ ความต้องการคือการสร้างสเปรดชีตที่จัดรูปแบบอย่างสวยงามซึ่งผู้ใช้ที่ไม่เชิงเทคนิคสามารถเปิดและเข้าใจได้ทันที.  

ในคู่มือนี้ เราจะพาคุณผ่านโซลูชันที่สมบูรณ์และพร้อมใช้งานที่แสดงให้คุณ **how to create workbook C#**, ใช้ **excel export formatting**, ตั้งค่า **row background**, และใช้ **excel automation c#** เพื่อสร้างไฟล์ที่ดูเป็นมืออาชีพ ไม่ได้ใช้ทางลัดแบบ “ดูเอกสาร” ที่คลุมเครือ—เพียงโค้ดเต็ม, คำอธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ, และเคล็ดลับที่คุณจะใช้ได้จริงในวันพรุ่งนี้.

---

## ข้อกำหนดเบื้องต้น

- .NET 6 (หรือ .NET Framework 4.6+).  
- Visual Studio 2022 หรือ IDE ที่รองรับ C# ใด ๆ  
- แพ็กเกจ NuGet **Aspose.Cells for .NET** (หรือไลบรารีใด ๆ ที่เปิดเผย `Workbook`, `Worksheet`, `Style`)  
- ความคุ้นเคยพื้นฐานกับ `DataTable`  

หากคุณยังไม่มี Aspose.Cells ให้รัน:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** รุ่นทดลองฟรีทำงานได้กับสถานการณ์การพัฒนาส่วนใหญ่; เพียงจำไว้ว่าให้เปลี่ยนคีย์ใบอนุญาตก่อนส่งมอบ.

![ตัวอย่างการสร้าง workbook C# ที่แสดงแถวที่มีสไตล์ใน Excel]( "ตัวอย่างการสร้าง workbook C# พร้อมสีพื้นหลังของแถว")

---

## ขั้นตอนที่ 1: เริ่มต้น Workbook และ Worksheet (Create Workbook C#)

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ของ `Workbook`. คิดว่าเป็นการเปิดไฟล์ Excel ใหม่เต็มรูปแบบในหน่วยความจำ.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**ทำไม?**  
`Workbook` เก็บเอกสาร Excel ทั้งหมด, ส่วน `Worksheet` แทนแท็บเดียว. การเริ่มต้นด้วย workbook ที่สะอาดช่วยให้คุณควบคุมทุกแง่มุมของผลลัพธ์—ไม่มีสไตล์เริ่มต้นที่ซ่อนอยู่แอบเข้ามา.

---

## ขั้นตอนที่ 2: เตรียม DataTable ตัวอย่าง (Export DataTable Excel)

ในโครงการจริงคุณจะดึงข้อมูลจากฐานข้อมูล, แต่เพื่อเป็นตัวอย่างเราจะสร้าง `DataTable` เล็ก ๆ ขึ้นมาทันที.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**ทำไมเรื่องนี้สำคัญ:**  
การส่งออก `DataTable` เป็นวิธีที่พบบ่อยที่สุดในการย้ายข้อมูลเชิงตารางจากแอปพลิเคชันไปยัง Excel. วิธีข้างต้นเป็นอิสระเต็มรูปแบบ, ดังนั้นคุณสามารถคัดลอกและวางลงในโครงการใดก็ได้และมันจะทำงาน.

---

## ขั้นตอนที่ 3: สร้าง Style ต่อแถว (Excel Export Formatting)

เพื่อให้แต่ละแถวมีสีพื้นหลังของตนเอง, เราจะสร้างอ็อบเจ็กต์ `Style` สำหรับทุกแถวใน `DataTable`. นี่คือจุดที่ **excel export formatting** ส่องแสง.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**ทำไมต้องสไตล์ต่อแถว?**  
หากคุณต้องการเน้นบันทึกเฉพาะ (เช่น ใบแจ้งหนี้ที่ค้างชำระ) คุณสามารถแทนที่การวนสีแบบง่ายด้วยตรรกะเงื่อนไข—เพียงตั้งค่า `style.ForegroundColor` ตามข้อมูลของแถว.

---

## ขั้นตอนที่ 4: นำเข้า DataTable พร้อมสไตล์แถว (Set Row Background)

ตอนนี้เรานำทุกอย่างมารวมกัน: ข้อมูล, workbook, และสไตล์.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**สิ่งที่คุณจะเห็น:**  
การเปิด `EmployeesReport.xlsx` จะเห็นแถวหัวเรื่องในรูปแบบเริ่มต้น, ตามด้วยแถวข้อมูลสี่แถวที่แต่ละแถวถูกทาด้วยสีพื้นหลังอ่อน. ผลลัพธ์ดูเหมือนรายงานที่ทำด้วยมือ, ไม่ใช่การดัมพ์ที่น่าเบื่อ.

---

## ขั้นตอนที่ 5: เคล็ดลับการทำ Excel Automation C# ขั้นสูง (Excel Automation C#)

ต่อไปนี้เป็นเคล็ดลับสั้น ๆ ที่คุณสามารถเพิ่มลงบนตัวอย่างพื้นฐานได้:

| เคล็ดลับ | โค้ดสแนปช็อต | เมื่อควรใช้ |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | หลังจากนำเข้าข้อมูลเพื่อหลีกเลี่ยงข้อความถูกตัด |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | เมื่อ ตารางอาจเลื่อนออกนอกหน้าจอ |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | เน้นเงินเดือนที่เกินเกณฑ์ |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | เมื่อคุณต้องการรายงานแบบอ่านอย่างเดียว |

สแนปช็อตเหล่านี้แสดงถึงความหลากหลายของ **excel automation c#**—คุณสามารถขยาย workbook ต่อไปได้โดยไม่ต้องเขียนตรรกะการนำเข้าใหม่.

---

## คำถามทั่วไป & กรณีขอบ

**ถ้า DataTable มีหลายพันแถวจะทำอย่างไร?**  
Aspose.Cells สตรีมข้อมูลอย่างมีประสิทธิภาพ, แต่คุณอาจต้องการปิดการสร้างสไตล์สำหรับทุกแถวเพื่อประหยัดหน่วยความจำ. แทนที่จะทำเช่นนั้น, ให้ใช้สไตล์เดียวกับช่วง:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**ฉันสามารถส่งออกเป็น .csv แทน .xlsx ได้หรือไม่?**  
ได้—เพียงเปลี่ยนรูปแบบการบันทึก:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

สไตล์จะหายไป (CSV ไม่มีสไตล์), แต่การส่งออกข้อมูลยังคงเหมือนเดิม.

**โค้ดนี้ทำงานบน .NET Core หรือไม่?**  
ใช่. Aspose.Cells รองรับ .NET Standard 2.0 และรุ่นต่อ ๆ ไป, ดังนั้นโค้ดเดียวกันทำงานบน .NET 6, .NET 7, หรือ .NET Framework.

---

## ตัวอย่างทำงานเต็ม (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}