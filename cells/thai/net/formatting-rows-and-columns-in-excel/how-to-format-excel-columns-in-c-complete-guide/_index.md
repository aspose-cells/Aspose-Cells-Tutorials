---
category: general
date: 2026-06-27
description: วิธีจัดรูปแบบคอลัมน์ Excel ใน C# ด้วยสีสลับ เรียนรู้การสร้างไฟล์ Excel
  ด้วย C# การนำเข้า DataTable ไปยัง Excel และการส่งออกเป็นไฟล์ .xlsx
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: th
og_description: วิธีจัดรูปแบบคอลัมน์ Excel ใน C# ด้วยสีสลับ ทำตามบทแนะนำขั้นตอนต่อขั้นตอนนี้เพื่อสร้างไฟล์
  Excel ด้วย C# นำเข้า DataTable และส่งออกเป็น .xlsx
og_title: วิธีจัดรูปแบบคอลัมน์ Excel ใน C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: วิธีจัดรูปแบบคอลัมน์ Excel ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีจัดรูปแบบคอลัมน์ Excel ใน C# – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีจัดรูปแบบคอลัมน์ Excel** ใน C# โดยไม่ต้องบิดผมจนเสียไหม? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างรายงานการขายหรือดึงข้อมูลฐานข้อมูลลงสเปรดชีต การทำให้คอลัมน์ดูเรียบร้อยสามารถสร้างความแตกต่างระหว่าง “ธรรมดา” กับ “ว้าว” ได้อย่างชัดเจน

ในบทเรียนนี้เราจะเดินผ่าน **ตัวอย่างที่ทำงานได้เต็มรูปแบบ** ที่แสดงให้คุณเห็นวิธี **สร้าง Excel workbook C#**, **นำเข้า DataTable ไปยัง Excel**, และ **ใช้สีคอลัมน์สลับกัน** เพื่อให้แต่ละคอลัมน์โดดเด่น เมื่อจบคุณจะรู้วิธี **ส่งออก DataTable เป็น xlsx** ด้วยบรรทัดโค้ดเดียว ไม่ต้องอธิบายเยิ่นเย้อ เพียงโค้ดที่คุณสามารถคัดลอก‑วางได้ทันที

> **สิ่งที่คุณต้องมี**  
> - .NET 6 หรือใหม่กว่า (เวอร์ชันล่าสุดใดก็ได้)  
> - แพคเกจ NuGet **Aspose.Cells** (หรือแพคเกจที่คล้ายกัน) – เราจะใช้มันเพราะเป็น C# แท้ ๆ ไม่ต้องติดตั้ง Excel  
> - แหล่งข้อมูล `DataTable` อย่างง่าย – เราจะสร้างขึ้นมาทันทีเพื่อสาธิต

มาเริ่มกันเลย

![วิธีจัดรูปแบบคอลัมน์ Excel ใน C# ตัวอย่าง](excel-columns.png "วิธีจัดรูปแบบคอลัมน์ Excel ใน C#")

## ขั้นตอนที่ 1: สร้าง Excel Workbook ใน C#

สิ่งแรกที่ต้องทำคือสร้าง workbook ใหม่สด ๆ คิดว่าเป็นการเปิดสมุดโน้ตใหม่ที่คุณจะเขียนข้อมูลลงไป

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:** `Workbook` คือจุดเริ่มต้นของทุกการทำงานกับ Excel การสร้างมัน **creates excel workbook c#** แบบไม่ต้องใช้ COM interop และอ็อบเจกต์จะอยู่ในหน่วยความจำจนกว่าคุณจะบันทึก

> **เคล็ดลับ:** หากคุณกำลังทำงานบนเซิร์ฟเวอร์ ควรเลือกไลบรารีที่ไม่ต้องพึ่งพาการติดตั้ง Microsoft Office เช่น Aspose.Cells, EPPlus หรือ ClosedXML

## ขั้นตอนที่ 2: เตรียม Style – ใช้สีคอลัมน์สลับกัน

ต่อมาคือส่วนสนุก: ทำให้คอลัมน์สลับสีกัน สีเหล่านี้ช่วยให้ผู้อ่านสแกนตารางขนาดใหญ่ได้เร็วขึ้น

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**กำลังเกิดอะไรขึ้น?**  
- `workbook.CreateStyle()` ให้แคนวาสสะอาดสำหรับแต่ละคอลัมน์  
- เงื่อนไขเทอร์นารี `(i % 2 == 0) ? Color.Blue : Color.Green` คือหัวใจของ **apply alternating column colors** – คอลัมน์ที่มีดัชนีคู่จะเป็นสีน้ำเงิน, คอลัมน์คี่จะเป็นสีเขียว  
- คุณสามารถขยายบล็อกนี้เพื่อกำหนดพื้นหลัง, เส้นขอบ หรือรูปแบบตัวเลขโดยไม่ต้องแก้โค้ดส่วนอื่น

> **กรณีขอบเขต:** หากตารางของคุณมีคอลัมน์หลายสิบหรือหลายร้อยคอลัมน์ การสร้างสไตล์ต่อคอลัมน์อาจกินหน่วยความจำมาก ในกรณีนั้นให้ใช้สไตล์สองแบบ (blueStyle, greenStyle) แล้วกำหนดตามดัชนีคอลัมน์

## ขั้นตอนที่ 3: สร้าง Sample DataTable (หรือใช้ของคุณเอง)

เพื่อสาธิตแบบอิสระ เราจะสร้าง `DataTable` พร้อมแถวไม่กี่แถว ในโครงการจริงคุณจะเปลี่ยน `GetSampleData()` ให้เรียกข้อมูลของคุณเอง

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

จากนั้นนำไปต่อกับกระบวนการหลักของเรา:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## ขั้นตอนที่ 4: นำเข้า DataTable ไปยัง Worksheet พร้อม Style

Aspose.Cells ทำการนำเข้าให้เป็นบรรทัดเดียว ตัว overload ที่เราใช้ให้เราส่งอาร์เรย์สไตล์ที่สร้างไว้ก่อนหน้า

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**ทำไมต้องใช้ overload นี้?**  
- มันเคารพแถวหัวตาราง ทำให้คุณไม่ต้องเขียนชื่อคอลัมน์ด้วยตนเอง  
- มันใช้ **columnStyles** array เพื่อกำหนดสีคอลัมน์แบบสลับโดยอัตโนมัติ ไม่ต้องวนลูปเพิ่ม  
- เร็วมาก – ตารางทั้งหมดถูกโหลดเข้าสู่หน่วยความจำในหนึ่งคำสั่ง

## ขั้นตอนที่ 5: บันทึก Workbook – ส่งออก DataTable เป็น .xlsx

สุดท้ายเราบันทึก workbook ลงดิสก์ ที่นี่คือจุดที่ **export datatable as xlsx** เกิดขึ้น

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

เมื่อคุณเปิด `output.xlsx` คุณจะเห็น:

| **ID** | **Name**      | **Score** | **Date**    |
|--------|---------------|-----------|-------------|
| *1* (สีน้ำเงิน) | *Student 1* (สีเขียว) | *77* (สีน้ำเงิน) | *2026‑06‑26* (สีเขียว) |
| *2* (สีเขียว) | *Student 2* (สีน้ำเงิน) | *79* (สีเขียว) | *2026‑06‑25* (สีน้ำเงิน) |
| …      | …             | …         | …           |

*ฟอนต์สีน้ำเงินและสีเขียวสลับกันตามคอลัมน์ ตามที่เราเขียนโค้ดไว้*

## ขั้นตอนที่ 6: ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Styles not applied** | Passing `null` or a mismatched array length to `ImportDataTable`. | Ensure `columnStyles.Length == dataTable.Columns.Count`. |
| **File locked after save** | Another process (e.g., Excel) has the file open. | Close any viewers before running, or save to a temp path and move the file after. |
| **Memory blow‑up with huge tables** | Creating a style per column for thousands of columns. | Reuse two style objects and assign them based on `(col % 2)`. |
| **Wrong date format** | Excel interprets `DateTime` as a number. | Set `columnStyles[i].Number = 14; // built‑in date format` for date columns. |

## ขั้นตอนที่ 7: ขั้นตอนต่อไป – ไปไกลกว่าการจัดรูปแบบพื้นฐาน

เมื่อคุณเชี่ยวชาญ **วิธีจัดรูปแบบคอลัมน์ Excel** ด้วยฟอนต์สลับแล้ว คุณสามารถทดลอง:

- **Conditional formatting** – เน้นเซลล์ที่ตรงตามกฎธุรกิจ  
- **Table objects** – แปลงช่วงข้อมูลเป็น Excel Table เพื่อให้มีฟิลเตอร์อัตโนมัติ  
- **Chart generation** – สร้างกราฟจากข้อมูลใน workbook โดยตรง  
- **Streaming large exports** – ใช้ `SaveOptions` เพื่อเขียนไฟล์ขนาดใหญ่โดยไม่ต้องโหลดทั้งหมดใน RAM  

ทั้งหมดนี้ต่อเนื่องจากแนวคิดหลักที่เราได้อธิบายไว้: สร้าง workbook, กำหนดสไตล์ให้เซลล์, นำเข้าข้อมูล, แล้วบันทึก

---

### สรุป

คุณเพิ่งเรียนรู้ **วิธีจัดรูปแบบคอลัมน์ Excel** ใน C# ตั้งแต่ต้นจนจบ: สร้าง Excel workbook C#, ใช้สีคอลัมน์สลับกัน, นำเข้า DataTable ไปยัง Excel, และสุดท้ายส่งออก DataTable เป็นไฟล์ .xlsx โค้ดเต็มที่สามารถคัดลอก‑วางได้ทันที พร้อมคำอธิบายเหตุผลของแต่ละบรรทัด

อย่าลังเลที่จะปรับสี, เพิ่มเส้นขอบ, หรือเปลี่ยนไปใช้ไลบรารีอื่นหากคุณชอบ รูปแบบการทำงานยังคงเหมือนเดิมและผลลัพธ์จะเป็นสเปรดชีตที่ดูเป็นมืออาชีพพร้อมส่งให้ผู้มีส่วนได้ส่วนเสีย

มีคำถามหรืออยากแชร์เทคนิคการจัดรูปแบบของคุณ? ฝากคอมเมนต์ไว้ด้านล่างและมาพูดคุยต่อกันได้เลย ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจคของคุณ

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}