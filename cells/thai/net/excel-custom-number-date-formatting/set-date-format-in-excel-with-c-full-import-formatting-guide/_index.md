---
category: general
date: 2026-06-17
description: ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# พร้อมตั้งค่าพื้นหลังของเซลล์, ใช้สีตัวอักษร,
  และทำสีคอลัมน์ใน Excel ระหว่างการนำเข้า เรียนรู้ขั้นตอนโดยละเอียด.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: th
og_description: ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# พร้อมกำหนดพื้นหลังของเซลล์, ใส่สีข้อความ,
  และทำสีคอลัมน์ใน Excel ระหว่างการนำเข้า. บทเรียนเต็ม.
og_title: ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# – คู่มือการจัดรูปแบบการนำเข้าเต็มรูปแบบ
url: /th/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# – คู่มือการจัดรูปแบบการนำเข้าเต็มรูปแบบ

เคยต้อง **ตั้งค่ารูปแบบวันที่** ในแผ่น Excel ที่สร้างจากโค้ด C# แล้วอยากให้คอลัมน์มีพื้นหลังหรือสีข้อความแบบกำหนดเองหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ สถานการณ์การรายงานคุณจะดึง `DataTable` จากฐานข้อมูล ใส่ลงในเวิร์กชีต แล้วรีบจัดรูปแบบวันที่ให้ดูถูกต้องและทำให้คอลัมน์โดดเด่นด้วยสีที่ต้องการ  

ในบทเรียนนี้เราจะพาไปผ่านโซลูชันแบบครบวงจรที่ **ตั้งค่ารูปแบบวันที่** , **ตั้งค่าพื้นหลังเซลล์** , **กำหนดสีข้อความ** และแม้กระทั่ง **ทำให้คอลัมน์ใน Excel มีสี** ขณะนำเข้าข้อมูล เมื่อเสร็จคุณจะได้แพทเทิร์นที่นำกลับมาใช้ใหม่ได้สำหรับ **excel import formatting** โดยไม่ต้องลองผิดลองถูก

> **สิ่งที่คุณต้องมี**  
> * .NET 6+ (หรือ .NET Framework 4.7+)  
> * Aspose.Cells for .NET (เวอร์ชันทดลองฟรีใช้ทดสอบได้)  
> * แหล่งข้อมูล `DataTable` – คำสั่ง ADO.NET ใด ๆ ก็ได้  
> * Visual Studio หรือ IDE ที่คุณชื่นชอบ  

มาเริ่มกันเลย

---

## ภาพรวมของโซลูชัน

เราจะแบ่งปัญหาออกเป็นสามส่วนหลัก:

1. **ดึงข้อมูลต้นทาง** – `DataTable` ที่มีแถวที่คุณต้องการส่งออก  
2. **สร้างสไตล์เฉพาะคอลัมน์** – สไตล์หนึ่งสำหรับคอลัมน์วันที่ อีกสไตล์หนึ่งสำหรับคอลัมน์ข้อความ พร้อมสไตล์เพิ่มเติมตามที่ต้องการ  
3. **นำเข้าตารางพร้อมสไตล์** – ใช้ `Worksheet.Cells.ImportDataTable` เพื่อให้แต่ละคอลัมน์สืบทอดสไตล์ที่เตรียมไว้

ทำไมต้องใช้วิธีนี้? เพราะ Aspose.Cells ให้คุณแนบอาเรย์ `Style` เข้าไปในคำสั่ง `ImportDataTable` ได้โดยตรง หมายความว่าไม่ต้องทำการจัดรูปแบบซ้ำอีกครั้ง มันเร็วกว่า ลดข้อผิดพลาด และทำให้โค้ดของคุณดูเรียบร้อย

---

## ขั้นตอนที่ 1: ดึงข้อมูลเพื่อส่งออก

อันดับแรกคุณต้องมี `DataTable` ในโครงการจริงคุณอาจเรียก stored procedure หรือใช้ Entity Framework เพื่อเติมข้อมูล แต่เพื่ออธิบายง่ายเราจะจำลองตารางง่าย ๆ ที่มีคอลัมน์วันที่และคอลัมน์ข้อความ

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **เคล็ดลับ:** หากแหล่งข้อมูลของคุณใช้วันที่ที่เป็น nullable ให้ตรวจสอบให้คอลัมน์เป็น `typeof(DateTime?)` – Aspose จะยังคงเคารพรูปแบบที่คุณกำหนดต่อไป

---

## ขั้นตอนที่ 2: เตรียมอาเรย์สไตล์ – หนึ่งสไตล์ต่อคอลัมน์

ต่อไปเราจะสร้าง `Style[]` ที่ความยาวเท่ากับจำนวนคอลัมน์ใน `DataTable` แต่ละรายการจะเก็บการจัดรูปแบบของคอลัมน์ที่สอดคล้องกัน

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 ตั้งค่ารูปแบบวันที่สำหรับคอลัมน์แรก

คอลัมน์แรก (`OrderDate`) ควรแสดงเป็น “MM/dd/yyyy” Aspose ใช้ดัชนีรูปแบบตัวเลขในตัวที่ 14 สำหรับวันที่สั้น ๆ แต่คุณก็สามารถกำหนดสตริงรูปแบบแบบกำหนดเองได้หากต้องการ

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**เหตุผลที่สำคัญ:** Excel เก็บวันที่เป็นเลขลำดับ (serial number) การกำหนดรูปแบบตัวเลขทำให้ Excel แสดงเลขเหล่านั้นเป็นวันที่ที่มนุษย์อ่านได้แทนการแสดงเป็นตัวเลขดิบ

### 2.2 ตั้งค่าพื้นหลังเซลล์สำหรับคอลัมน์ที่สอง

ให้คอลัมน์ `CustomerName` มีพื้นหลังสีฟ้าอ่อน นี่คือจุดที่ **set cell background** เข้ามาใช้

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **หมายเหตุ:** หากไม่ตั้งค่า `Pattern` เป็น `Solid` สีพื้นหน้า (foreground) จะไม่แสดงผล เพราะแพทเทิร์นเริ่มต้นคือ “None”

### 2.3 กำหนดสีข้อความ (Foreground) – เพิ่มเติมตามต้องการ

หากต้องการให้ข้อความมีสีที่ตัดกันกับพื้นหลัง คุณสามารถปรับสไตล์เดียวกันได้:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

ขั้นตอนนี้ทำให้ **apply foreground color** เสร็จสมบูรณ์โดยยังคงรักษาพื้นหลังของคอลัมน์ไว้

---

## ขั้นตอนที่ 3: นำเข้า DataTable พร้อมสไตล์ที่กำหนด

เมื่อสไตล์พร้อมแล้ว ขั้นตอนสุดท้ายคือบรรทัดเดียวที่นำเข้าข้อมูลและใช้สไตล์ตามคอลัมน์

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**วิธีทำงาน:** Aspose จะอ่านอาเรย์ `columnStyles` แล้วแมป `Style` แต่ละอันกับดัชนีคอลัมน์ที่สอดคล้อง ส่วนแถวหัวตารางจะสืบทอดสไตล์เริ่มต้น เว้นแต่คุณจะให้สไตล์แยกต่างหากสำหรับแถว 0

### 3.1 บันทึกเวิร์กบุ๊ก

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

รันโปรแกรม เปิดไฟล์ *FormattedReport.xlsx* แล้วคุณจะเห็น:

- คอลัมน์ **OrderDate** แสดงเป็นวันที่ (เช่น `06/15/2026`)  
- คอลัมน์ **CustomerName** มีพื้นหลังสีฟ้าอ่อนและข้อความสีฟ้าเข้ม  

นี่คือกระบวนการ **excel import formatting** ทั้งหมดในประมาณ 30 บรรทัดของ C#

---

## สรุปขั้นตอนแบบเป็นขั้นเป็นตอน (พร้อมเหตุผล)

| ขั้นตอน | สิ่งที่ทำ | ทำไมถึงสำคัญ |
|------|-------------|----------------|
| **ดึงข้อมูล** | เรียก `GetData()` เพื่อเติม `DataTable` | ให้แหล่งข้อมูลที่โครงสร้างพร้อมให้ Aspose ดึงเข้าได้โดยตรง |
| **สร้างอาเรย์สไตล์** | จอง `Style[]` ให้ตรงกับจำนวนคอลัมน์ | ทำให้สามารถกำหนดสไตล์ต่อคอลัมน์ได้ในคำสั่งนำเข้าเดียว |
| **ตั้งค่ารูปแบบวันที่** | `columnStyles[0].Number = 14;` | ทำให้วันที่แสดงผลอย่างถูกต้องใน Excel |
| **ตั้งค่าสีพื้นหลัง** | `ForegroundColor = LightBlue; Pattern = Solid;` | เน้นคอลัมน์ตามที่ต้องการ ตรงกับ **set cell background** |
| **กำหนดสีข้อความ** | `Font.Color = DarkBlue;` | เพิ่มความอ่านง่ายและสอดคล้องกับ **apply foreground color** |
| **นำเข้าพร้อมสไตล์** | `ImportDataTable(..., columnStyles);` | การนำเข้าครั้งเดียวที่เคารพการจัดรูปแบบทั้งหมด |
| **บันทึกเวิร์กบุ๊ก** | `wb.Save(...);` | เก็บผลลัพธ์ไว้ให้ผู้ใช้ต่อไป |

---

## การจัดการกรณีขอบและคำถามที่พบบ่อย

### ถ้ามีคอลัมน์มากกว่าสองคอลัมน์?

เพียงขยายอาเรย์ `columnStyles` แล้วกำหนด `Style` ให้กับดัชนีที่ต้องการ คอลัมน์ที่ไม่ได้กำหนดจะใช้สไตล์เริ่มต้น ซึ่งก็ไม่มีปัญหา

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### จะตั้งค่าคอลัมน์เป็นสกุลเงินอย่างไร?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### สามารถเปลี่ยนสไตล์ของแถวหัวตารางแยกต่างหากได้หรือไม่?

ได้ หลังจากนำเข้าแล้วคุณสามารถดึงแถวแรกและกำหนดสไตล์ที่แตกต่างได้:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### ถ้า DataTable มีวันที่เป็น null จะเกิดอะไรขึ้น?

Aspose จะปล่อยเซลล์นั้นว่างเปล่า หากคุณต้องการให้แสดงข้อความเช่น “N/A” คุณสามารถทำการประมวลผลตารางล่วงหน้า:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

จากนั้นปรับสไตล์ให้แสดงรูปแบบกำหนดเองที่แสดง “N/A” สำหรับค่าตัวแทน

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วาง ใช้เป็นแอปคอนโซลและคุณจะได้ไฟล์ Excel ที่จัดรูปแบบสวยงาม



## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}