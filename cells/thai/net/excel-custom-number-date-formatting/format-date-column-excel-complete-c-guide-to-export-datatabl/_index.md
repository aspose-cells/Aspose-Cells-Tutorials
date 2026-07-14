---
category: general
date: 2026-07-13
description: จัดรูปแบบคอลัมน์วันที่ใน Excel ขณะส่งออก DataTable จาก C#. เรียนรู้การส่งออก
  DataTable ไปยัง Excel ด้วย C# และการนำเข้า DataTable ไปยัง Excel พร้อมสไตล์ในไม่กี่นาที.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: th
lastmod: 2026-07-13
og_description: จัดรูปแบบคอลัมน์วันที่ใน Excel อย่างง่ายดาย คู่มือนี้จะแสดงวิธีการส่งออก
  DataTable จาก C# ไปยัง Excel และนำเข้า DataTable ไปยัง Excel พร้อมสไตล์ที่กำหนดเอง.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: จัดรูปแบบคอลัมน์วันที่ใน Excel – ขั้นตอนโดยละเอียดการส่งออกด้วย C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: จัดรูปแบบคอลัมน์วันที่ใน Excel – คู่มือ C# ฉบับสมบูรณ์สำหรับการส่งออก DataTable
url: /th/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ฟอร์แมตคอลัมน์วันที่ Excel – คู่มือ C# ฉบับสมบูรณ์สำหรับการส่งออก DataTable

เคยต้องการ **format date column Excel** ขณะดึงข้อมูลจากฐานข้อมูล แต่เซลล์กลับแสดงค่า timestamp ดิบอยู่หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายแอปธุรกิจการส่งออกค่าเริ่มต้นจะใส่ค่า `DateTime` เช่น `2024‑03‑15 00:00:00` และไม่มีใครต้องการความยุ่งยากนั้น  

ข่าวดีคือคุณสามารถควบคุมรูปแบบของแต่ละคอลัมน์โดยตรงจาก C# ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจรที่ **excel export datatable c#**, ใส่สไตล์วันที่ให้คอลัมน์แรก, สไตล์สกุลเงินให้คอลัมน์ที่สอง, และสุดท้าย **import datatable to excel** ด้วยการจัดรูปแบบที่ไม่มีความยุ่งยาก  

เมื่อจบคุณจะได้เมธอดที่นำกลับมาใช้ใหม่ได้ซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้ ไม่ว่าจะใช้ .NET 6, .NET Framework 4.8 หรือเวอร์ชันที่ใหม่กว่า

---

## สิ่งที่คุณต้องเตรียม

- **Aspose.Cells for .NET** (หรือไลบรารีใดก็ได้ที่มี `CreateStyle` และ `ImportDataTable`). ตัวอย่างโค้ดใช้ Aspose เพราะ API ของมันสะอาดและได้รับการยอมรับอย่างกว้างขวาง.
- **DataTable** ที่คุณได้ทำการเติมข้อมูลจาก SQL, CSV หรือแหล่งอื่นใดแล้ว
- Visual Studio (หรือ IDE ที่คุณชื่นชอบ)  
- .NET runtime 5.0+ (ตัวอย่างมุ่งเป้าไปที่ .NET 6 แต่เฟรมเวิร์กเก่าก็ทำงานได้เช่นกัน)

หากคุณยังไม่มี Aspose.Cells ให้รับทดลองใช้ฟรีจากเว็บไซต์ทางการ—ไม่ต้องใช้บัตรเครดิต

---

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเป็น DataTable

สิ่งแรกที่ต้องทำคือคุณต้องมี `DataTable` ในสถานการณ์จริงมักจะมาจาก `SqlDataAdapter.Fill` แต่เพื่อความชัดเจนเราจะจำลองตารางง่าย ๆ ดังนี้:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro tip:** เมื่อคุณดึงข้อมูลโดยตรงจาก stored procedure ให้ตรวจสอบให้แน่ใจว่าชนิดคอลัมน์ตรงกับรูปแบบ Excel ที่ต้องการ คอลัมน์ `datetime` จะเป็นเป้าหมายสำหรับสไตล์ **format date column excel** ของเราในภายหลัง.

---

## ขั้นตอนที่ 2: สร้าง Excel Workbook และกำหนดสไตล์คอลัมน์

ตอนนี้เราจะสร้าง workbook ใหม่ เทคนิคในการ **format date column excel** อยู่ที่การสร้างอ็อบเจกต์ `Style` ตั้งค่า property `Number` ให้เป็นรูปแบบวันที่ใน Excel ที่มีมาให้ (code 14) และกำหนดสไตล์นั้นให้กับดัชนีคอลัมน์ที่ต้องการ

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

ทำไมต้อง `Number = 14`? Excel เก็บวันที่เป็นเลขอนุกรม; รูปแบบ 14 บอกโปรแกรมให้แสดงเลขเหล่านั้นด้วยรูปแบบวันที่สั้นของโลคัล หากคุณต้องการรูปแบบกำหนดเอง (เช่น `dd‑MMM‑yyyy`) คุณสามารถตั้งค่า `columnStyles[0].Custom = "dd-MMM-yyyy"` แทนได้.

---

## ขั้นตอนที่ 3: นำ DataTable เข้าสู่ Worksheet พร้อมสไตล์

เมื่ออาเรย์สไตล์พร้อม การเรียก import จะเป็นบรรทัดเดียว นี่คือหัวใจของ **excel export datatable c#** และเป็นจุดที่เราทำ **import datatable to excel** พร้อมคงรูปแบบไว้

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

`ImportDataTable` overload ที่เราใช้รับอาเรย์สไตล์และนำสไตล์แต่ละอันไปใช้กับคอลัมน์ที่ตรงกันขณะเขียนข้อมูล ไม่ต้องวนลูปหลังการประมวลผล—คอลัมน์วันที่ของคุณจะถูกฟอร์แมตอย่างสวยงามแล้ว

---

## ขั้นตอนที่ 4: บันทึก Workbook (หรือสตรีมโดยตรงไปยัง Browser)

ขึ้นอยู่กับสถานการณ์ของคุณ คุณอาจบันทึกลงดิสก์, สตรีมในหน่วยความจำ, หรือส่งไฟล์เป็น HTTP response ต่อไปนี้เป็นรูปแบบที่พบบ่อยสามแบบ:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Watch out for:** หากคุณใช้ `FileResult` ใน ASP.NET Core อย่าลืมตั้งค่า `Response.Headers["Cache-Control"] = "no-cache"` เมื่อไฟล์ถูกสร้างแบบเรียลไทม์ เพื่อป้องกันไม่ให้เบราว์เซอร์ให้บริการเวอร์ชันที่ล้าสมัย.

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ – รูปแบบของแผ่น Excel

หลังจากรันโค้ดแล้ว เปิดไฟล์ `ExportedReport.xlsx` คุณควรจะเห็น:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

![ตัวอย่าง format date column excel](/images/format-date-column-excel.png)

*ข้อความแทนภาพ: format date column excel – ภาพหน้าจอของแผ่น Excel ที่มีคอลัมน์วันที่ถูกฟอร์แมตอย่างถูกต้อง.*

---

## คำถามทั่วไป & กรณีขอบ

### ถ้า DataTable ของฉันมีมากกว่าสามคอลัมน์?

เพียงขยายอาเรย์ `columnStyles` สำหรับคอลัมน์ใดที่คุณไม่ได้กำหนดสไตล์โดยตรง ให้ใส่ค่า `null` ไว้; Excel จะใช้รูปแบบ General เริ่มต้น

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### จะตั้งรูปแบบวันที่กำหนดเองอย่างไร (เช่น “dd‑MMM‑yyyy”)?

แทนที่หมายเลขที่มีมาให้ด้วยสตริงกำหนดเอง:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### สามารถใช้วิธีนี้กับ EPPlus หรือ ClosedXML ได้หรือไม่?

ได้, แนวคิดเหมือนกัน: สร้างอ็อบเจกต์สไตล์, กำหนดให้กับคอลัมน์, จากนั้นโหลด `DataTable` API อาจแตกต่างกัน แต่รูปแบบ **excel export datatable c#** ยังคงเหมือนเดิม

### จะทำอย่างไรกับ DataSet ขนาดใหญ่ (100k+ แถว)?

`ImportDataTable` ถูกปรับให้เหมาะกับการเขียนเป็นชุดใหญ่ แต่คุณอาจเจอข้อจำกัดของหน่วยความจำ ในกรณีนั้นพิจารณาสตรีมแถวด้วย `Cells.ImportDataTable` เป็นชิ้นส่วน, หรือใช้ `Worksheet.Cells["A1"].PutValue` ในลูปพร้อมใช้สไตล์อ็อบเจกต์ซ้ำ

---

## ตัวอย่างทำงานเต็มรูปแบบ (ทุกขั้นตอนในเมธอดเดียว)

ด้านล่างเป็นเมธอดที่ทำงานอิสระซึ่งคุณสามารถคัดลอกและวางลงในแอปคอนโซลหรือคอนโทรลเลอร์ ASP.NET ใดก็ได้ มันแสดงกระบวนการทั้งหมด—from การดึงข้อมูลจนถึงการส่งออก Excel ที่มีสไตล์

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

รันโปรแกรม, เปิดไฟล์ `StyledExport.xlsx` แล้วคุณจะเห็น **format date column excel** ถูกนำไปใช้อย่างสมบูรณ์

---

## สรุป & ขั้นตอนต่อไป

เราเพิ่งอธิบายวิธี **format date column excel** เมื่อทำ **excel export datatable c#**, และวิธี **import datatable to excel** ด้วยการจัดสไตล์ต่อคอลัมน์ในหนึ่งคำสั่ง จุดสำคัญที่ควรจำ:

1. สร้าง `Style` สำหรับแต่ละคอลัมน์ที่คุณต้องการฟอร์แมต.  
2. ใช้ `Number = 14` สำหรับวันที่, `Number = 2` สำหรับสกุลเงิน, หรือรูปแบบกำหนดเองใด ๆ ที่คุณต้องการ.  
3. ส่งอาเรย์สไตล์ไปยัง `ImportDataTable`—ไลบรารีจะทำงานหนักให้

คุณอาจสำรวจต่อไปอะไรได้บ้าง?

- **Conditional formatting** เพื่อเน้นวันที่เกินกำหนด.  
- **

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบทางเลือกในโปรเจกต์ของคุณ.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}