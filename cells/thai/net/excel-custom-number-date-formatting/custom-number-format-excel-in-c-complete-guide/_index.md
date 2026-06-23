---
category: general
date: 2026-03-22
description: บทเรียนการกำหนดรูปแบบตัวเลขแบบกำหนดเองใน Excel แสดงวิธีนำเข้า DataTable
  ไปยัง Excel ตั้งค่าสีพื้นหลังของคอลัมน์ จัดรูปแบบคอลัมน์เป็นสกุลเงิน และบันทึกเวิร์กบุ๊กเป็นไฟล์
  xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: th
og_description: บทเรียนการจัดรูปแบบตัวเลขแบบกำหนดเองใน Excel ที่อธิบายขั้นตอนการนำเข้า
  DataTable, ตั้งค่าสีพื้นหลังของคอลัมน์, จัดรูปแบบคอลัมน์เป็นสกุลเงิน, และบันทึกเวิร์กบุ๊กเป็นไฟล์
  xlsx.
og_title: การกำหนดรูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย C# – คู่มือแบบขั้นตอนต่อขั้นตอน
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: การกำหนดรูปแบบตัวเลขแบบกำหนดเองใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รูปแบบตัวเลขแบบกำหนดเองใน Excel – บทเรียน Full‑Stack C#

เคยสงสัยไหมว่าจะแปลงสไตล์ **custom number format excel** อย่างไรโดยตรงจาก C#? บางทีคุณอาจเคยลองส่ง DataTable ไปยังสเปรดชีตแล้วเห็นแค่ตัวเลขธรรมดา ไม่มีสีและไม่มีการจัดรูปแบบสกุลเงิน นั่นเป็นปัญหาที่พบบ่อย—โดยเฉพาะเมื่อคุณต้องการรายงานที่ดูเป็นมืออาชีพสำหรับผู้มีส่วนได้ส่วนเสีย

ในคู่มือนี้เราจะแก้ปัญหานั้นร่วมกัน: คุณจะได้เรียนรู้วิธี **import datatable to excel**, **set column background color**, **format column as currency**, และสุดท้าย **save workbook as xlsx** พร้อมรูปแบบตัวเลขแบบกำหนดเองที่ทำให้ตัวเลขของคุณโดดเด่น ไม่มีการอ้างอิงที่คลุมเครือ เพียงโซลูชันที่สมบูรณ์และสามารถรันได้ที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์ของคุณ

---

## สิ่งที่คุณจะสร้าง

เมื่อจบบทเรียนนี้ คุณจะมีแอปคอนโซล C# ที่ทำงานได้เองซึ่ง:

1. ดึง `DataTable` (คุณสามารถแทนที่ส่วนจำลองด้วยคิวรีของคุณเอง)  
2. สร้าง Excel workbook ใหม่โดยใช้ Aspose.Cells (หรือไลบรารีที่เข้ากันได้)  
3. ใส่ฟอนต์สีน้ำเงินและหนาให้คอลัมน์แรก, พื้นหลังสีเหลืองอ่อนให้คอลัมน์ที่สอง, และรูปแบบสกุลเงิน (`$#,##0.00`) ให้คอลัมน์ที่สาม  
4. บันทึกไฟล์เป็น `DataTableWithStyleArray.xlsx` ในโฟลเดอร์ที่คุณเลือก

คุณจะเห็นอย่างชัดเจนว่าทุกบรรทัดมีส่วนช่วยอย่างไรต่อไฟล์ Excel สุดท้าย และเราจะอธิบายว่าทำไมการเลือกเหล่านั้นจึงสำคัญต่อการบำรุงรักษาและประสิทธิภาพ

---

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือรุ่นที่ใหม่กว่า (โค้ดนี้ทำงานได้กับ .NET Framework 4.7+ ด้วย)  
- Aspose.Cells สำหรับ .NET (เวอร์ชันทดลองหรือเวอร์ชันที่มีลิขสิทธิ์) ติดตั้งผ่าน NuGet:

```bash
dotnet add package Aspose.Cells
```

- ความคุ้นเคยพื้นฐานกับ `DataTable` และแอปพลิเคชันคอนโซล C#

---

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเป็น DataTable

ก่อนอื่น เราต้องมีข้อมูลบางอย่างเพื่อส่งออก ในสถานการณ์จริงคุณอาจเรียกรีโพซิทอรีหรือรันคิวรี SQL เพื่อดึงข้อมูล สำหรับการอธิบายนี้เราจะสร้างตารางง่าย ๆ ในหน่วยความจำ

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **ทำไมเรื่องนี้สำคัญ:** การใช้ `DataTable` ให้แหล่งข้อมูลแบบตารางที่มีสคีมาซึ่งแมปได้อย่างตรงไปตรงมาบนแถวและคอลัมน์ของ Excel นอกจากนี้ยังทำให้คุณสามารถใช้ตรรกะการส่งออกเดียวกันสำหรับชุดข้อมูลใด ๆ โดยไม่ต้องเขียนโค้ดใหม่

---

## ขั้นตอนที่ 2: สร้าง Workbook ใหม่และดึง Worksheet แรก

ตอนนี้เราจะสร้าง Excel workbook ใหม่ คลาส `Workbook` แทนไฟล์ทั้งหมด; `Worksheets[0]` คือแผ่นงานเริ่มต้นที่เราจะใส่ข้อมูลของเรา

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **เคล็ดลับ:** หากต้องการหลายแผ่นงาน เพียงเรียก `workbook.Worksheets.Add("SheetName")` แล้วทำซ้ำขั้นตอนการจัดรูปแบบสำหรับแต่ละแผ่น

---

## ขั้นตอนที่ 3: กำหนดสไตล์คอลัมน์ – ฟอนต์, พื้นหลัง, และรูปแบบตัวเลข

การจัดรูปแบบใน Aspose.Cells ทำผ่านอ็อบเจ็กต์ `Style` เราจะสร้างอาเรย์ที่แต่ละองค์ประกอบสอดคล้องกับคอลัมน์ใน DataTable

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **ทำไมต้องใช้สไตล์อาเรย์?** การส่งอาเรย์ไปยัง `ImportDataTable` ทำให้คุณสามารถใช้สไตล์ที่แตกต่างกันสำหรับแต่ละคอลัมน์ในหนึ่งคำสั่ง ซึ่งกระชับและมีประสิทธิภาพ อีกทั้งยังรับประกันว่าการจัดรูปแบบจะสอดคล้องกับลำดับของข้อมูล

---

## ขั้นตอนที่ 4: นำเข้า DataTable พร้อมใช้สไตล์

นี่คือหัวใจของการทำงาน: เราใส่ `DataTable` ลงใน worksheet, บอก Aspose ให้รวมแถวหัวตาราง, และส่งอาเรย์ `columnStyles` ของเรา

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **อะไรเกิดขึ้นภายใน?** Aspose จะวนลูปแต่ละคอลัมน์ เขียนหัวตาราง แล้วเขียนค่าของแต่ละแถว ระหว่างนั้นจะใช้ `Style` ที่สอดคล้องจากอาเรย์ ทำให้คุณได้หัวคอลัมน์สีน้ำเงินสำหรับ “Product”, พื้นหลังสีเหลืองสำหรับ “Quantity”, และคอลัมน์ “Revenue” ที่จัดรูปแบบสกุลเงินอย่างสวยงาม

---

## ขั้นตอนที่ 5: บันทึก Workbook เป็นไฟล์ XLSX

สุดท้าย เราบันทึก workbook ลงดิสก์ เมธอด `Save` จะเลือกฟอร์แมต XLSX อัตโนมัติตามส่วนขยายของไฟล์

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **เคล็ดลับ:** หากต้องการสตรีมไฟล์ (เช่น สำหรับเว็บ API) ให้ใช้ `workbook.Save(stream, SaveFormat.Xlsx)` แทนการระบุเส้นทางไฟล์

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกไปวางในโปรเจกต์คอนโซลใหม่ มันคอมไพล์และทำงานได้ทันที สร้างไฟล์ Excel ที่มีสไตล์

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด `DataTableWithStyleArray.xlsx` คุณจะเห็น:

| **Product** (สีน้ำเงิน, หนา) | **Quantity** (สีเหลืองอ่อน) | **Revenue** (สกุลเงิน) |
|------------------------------|-------------------------------|--------------------------|
| Widget A                     | 120                           | $3,450.75                |
| Widget B                     | 85                            | $2,190.00                |
| Widget C                     | 60                            | $1,580.40                |

**custom number format excel** ที่คุณระบุ (`$#,##0.00`) ทำให้ทุกเซลล์ของรายได้แสดงสัญลักษณ์ดอลลาร์, ตัวคั่นหลักพัน, และทศนิยมสองตำแหน่ง — ตรงกับที่ทีมการเงินคาดหวัง

---

## คำถามที่พบบ่อยและกรณีขอบ

### ฉันสามารถใช้กับไลบรารี Excel อื่นได้หรือไม่?

ได้เลย แนวคิด—การสร้างสไตล์ต่อคอลัมน์และนำไปใช้ระหว่างการนำเข้า—สามารถนำไปใช้กับ EPPlus, ClosedXML หรือ NPOI ได้ การเรียก API อาจแตกต่างกัน แต่รูปแบบยังคงเหมือนเดิม

### ถ้า DataTable ของฉันมีคอลัมน์มากกว่าสไตล์ล่ะ?

Aspose จะใช้สไตล์เริ่มต้นกับคอลัมน์ใด ๆ ที่ไม่มีรายการที่ตรงกันในอาเรย์ `columnStyles` เพื่อหลีกเลี่ยงความประหลาดใจ ให้กำหนดขนาดอาเรย์ให้เท่ากับ `dataTable.Columns.Count` หรือสร้างสไตล์แบบไดนามิกในลูป

### ฉันจะตั้งรูปแบบตัวเลขแบบกำหนดเองสำหรับวันที่อย่างไร?

เพียงตั้งค่า `style.Custom = "dd‑mm‑yyyy"` (หรือสตริงฟอร์แมต Excel ที่ถูกต้องใด ๆ) วิธีการแบบอาเรย์เดียวกันนี้ทำงานได้กับวันที่, เปอร์เซ็นต์ หรือโนเทชันเชิงวิทยาศาสตร์

### มีวิธีทำให้คอลัมน์ออโต้ไซส์หลังการนำเข้าหรือไม่?

ใช่—เรียก `worksheet.AutoFitColumns();` หลังการนำเข้า มันจะคำนวณความกว้างโดยอิงจากเนื้อหาในเซลล์อย่างรวดเร็ว

### แล้วข้อมูลชุดใหญ่ (100k+ แถว) ล่ะ?

`ImportDataTable` ถูกปรับให้ทำงานกับการดำเนินการแบบ bulk อย่างมีประสิทธิภาพ แต่คุณอาจเจอข้อจำกัดของหน่วยความจำ ในกรณีนั้น พิจารณาสตรีมแถวด้วยตนเองโดยใช้ `Cells[i, j].PutValue(...)` และใช้ `Style` ตัวเดียวซ้ำเพื่อ ลดภาระ

---

## เคล็ดลับระดับมืออาชีพและข้อผิดพลาดทั่วไป

- **หลีกเลี่ยงการกำหนดค่าเส้นทางแบบฮาร์ดโค้ด** ในโค้ดการผลิต; ใช้ `Environment.GetFolderPath` หรือการตั้งค่าในไฟล์คอนฟิก  
- **ทำการ Dispose workbook** หากอยู่ในบริการที่ทำงานต่อเนื่อง—ห่อไว้ในบล็อก `using` เพื่อปล่อยทรัพยากรเนทีฟ  
- **ระวังตัวคั่นที่ขึ้นกับวัฒนธรรม** รูปแบบกำหนดเอง `$#,##0.00` บังคับให้ใช้จุดเป็นตัวคั่นทศนิยมไม่ว่าภาษา OS จะเป็นอะไร ซึ่งโดยทั่วไปเป็นสิ่งที่ต้องการสำหรับรายงานการเงิน  
- **อย่าลืมอ้างอิง System.Drawing** (หรือ `System.Drawing.Common` บน .NET Core) สำหรับโครงสร้างสีที่ใช้ในการจัดรูปแบบ  
- **ทดสอบผลลัพธ์บนเวอร์ชัน Excel ต่าง ๆ**; เวอร์ชันเก่าอาจตีความรูปแบบกำหนดเองบางอย่างแตกต่างกันเล็กน้อย

---

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **custom number format excel** ไฟล์จาก C#: ดึงข้อมูลจาก `DataTable`, **import datatable to excel**, ใช้ **set column background color**, ใช้ **format column as currency**, และสุดท้าย **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}