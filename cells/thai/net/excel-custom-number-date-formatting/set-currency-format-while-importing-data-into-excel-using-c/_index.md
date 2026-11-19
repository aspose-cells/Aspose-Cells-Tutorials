---
category: general
date: 2026-11-19
description: ตั้งค่ารูปแบบสกุลเงินใน Excel ด้วย C# – เรียนรู้วิธีตั้งค่ารูปแบบตัวเลขและสไตล์คอลัมน์ใน
  Excel ระหว่างการนำเข้าแผ่นงาน Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: th
lastmod: 2026-11-19
og_description: ตั้งค่ารูปแบบสกุลเงินใน Excel ด้วย C# และค้นหาวิธีการตั้งค่ารูปแบบตัวเลข,
  กำหนดรูปแบบตัวเลข, และจัดสไตล์คอลัมน์ของ Excel ระหว่างการนำเข้าแผ่นงาน Excel
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: ตั้งค่ารูปแบบสกุลเงินใน Excel ด้วย C# – คู่มือแบบขั้นตอนเต็ม
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: ตั้งค่ารูปแบบสกุลเงินขณะนำเข้าข้อมูลไปยัง Excel ด้วย C#
url: /th/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่ารูปแบบสกุลเงินขณะนำเข้าข้อมูลไปยัง Excel ด้วย C#

หากคุณต้องการ **ตั้งค่ารูปแบบสกุลเงิน** ในแผ่นงาน Excel คู่มือนี้จะแสดงวิธี **ตั้งค่ารูปแบบตัวเลข** และจัดรูปแบบคอลัมน์ขณะทำการ **นำเข้าแผ่นงาน Excel** คุณจะได้เห็นตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งกำหนดรูปแบบตัวเลขที่ถูกต้องให้กับแต่ละคอลัมน์ของ `DataTable` และนำเข้าข้อมูลพร้อมสไตล์ที่ต้องการ

การทำงานกับ Excel จาก C# มักต้องการมากกว่าการใส่ค่าดิบลงไปเท่านั้น—คุณต้องควบคุมวิธีการแสดงตัวเลข ไม่ว่าคุณจะสร้างใบแจ้งหนี้ รายงานการเงิน หรือแดชบอร์ด การจัดรูปแบบสกุลเงิน เปอร์เซ็นต์ หรือวันที่อย่างถูกต้องจะทำให้ผลลัพธ์อ่านง่ายทันที

## ข้อกำหนดเบื้องต้น

* .NET 6.0 (หรือใหม่กว่า) ติดตั้งแล้ว
* อ้างอิงถึง **Aspose.Cells for .NET** (หรือไลบรารีใด ๆ ที่เปิดเผยคลาส `Style` พร้อมคุณสมบัติ `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.
* ความคุ้นเคยพื้นฐานกับ `DataTable` และคอลเลกชันของ C#.
* IDE เช่น Visual Studio 2022 หรือ VS Code.

## ขั้นตอนที่ 1: ดึงข้อมูลที่จะเขียนลงในแผ่นงาน

เริ่มต้นโดยรับ `DataTable` ที่มีข้อมูลดิบที่คุณต้องการส่งออก ในโครงการจริงข้อมูลนี้อาจมาจากการสืบค้นฐานข้อมูล การเรียก API หรือการแปลงไฟล์ CSV

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การนำเข้า `DataTable` ที่เต็มไปด้วยข้อมูลทำให้คุณแยกตรรกะการดึงข้อมูลออกจากตรรกะการสร้าง Excel ซึ่งช่วยเพิ่มความสามารถในการทดสอบและการบำรุงรักษา

## ขั้นตอนที่ 2: สร้างอาเรย์สไตล์ – รายการหนึ่งต่อคอลัมน์ใน DataTable

Aspose.Cells ต้องการ `Style[]` ที่ความยาวตรงกับจำนวนคอลัมน์ที่คุณตั้งใจจะนำเข้า แต่ละองค์ประกอบสามารถเก็บรูปแบบตัวเลขเฉพาะได้

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **เคล็ดลับ:** แม้ว่าคุณจะต้องการจัดรูปแบบเพียงบางคอลัมน์เท่านั้น คุณก็ยังต้องสร้างอินสแตนซ์ `Style` สำหรับทุกคอลัมน์; มิฉะนั้นคุณจะเจอ `NullReferenceException` ระหว่างการนำเข้า

## ขั้นตอนที่ 3: กำหนดรูปแบบตัวเลขให้กับคอลัมน์ที่ต้องการ

ตัวเลขสไตล์ที่มีมาให้แตกต่างกันตามไลบรารี ใน Aspose.Cells:

* `0` → General (จำนวนเต็ม)  
* `2` → Currency (เช่น `$#,##0.00`)  
* `3` → Date, เป็นต้น

ที่นี่เราจะ **กำหนดรูปแบบตัวเลข** ให้กับสองคอลัมน์: คอลัมน์แรก (Id) จะคงเป็นจำนวนเต็ม ส่วนคอลัมน์ที่สอง (Amount) จะได้รับรูปแบบสกุลเงิน

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **วิธีตั้งค่ารูปแบบตัวเลข:** การใช้คุณสมบัติ `Number` เป็นวิธีที่เร็วที่สุดในการเลือกรูปแบบที่มีมาให้ สำหรับสกุลเงินที่ขึ้นกับโลคัล ให้พิจารณาใช้สตริงรูปแบบกำหนดเองที่รวมสัญลักษณ์สกุลเงินที่เหมาะสม

## ขั้นตอนที่ 4: นำเข้า DataTable ไปยังแผ่นงาน พร้อมใช้สไตล์คอลัมน์

เมื่ออาเรย์สไตล์พร้อมแล้ว ให้นำเข้าข้อมูล วิธี `ImportDataTable` จะเคารพสไตล์ที่คุณส่งผ่าน

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด **FinancialReport.xlsx** คุณจะเห็น:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*คอลัมน์ **Amount** แสดงด้วยรูปแบบสกุลเงินที่คุณตั้งค่าไว้ ส่วน **Id** ยังคงเป็นจำนวนเต็ม*

## วิธีตั้งค่ารูปแบบตัวเลขสำหรับสถานการณ์เพิ่มเติม

### กำหนดรูปแบบตัวเลขให้กับคอลัมน์วันที่

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### ใช้รูปแบบตัวเลขกำหนดเองสำหรับเปอร์เซ็นต์

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### การจัดรูปแบบนอกเหนือจากรูปแบบตัวเลข

คุณยังสามารถตั้งค่าแบบอักษร สีพื้นหลัง หรือการจัดแนวบนอ็อบเจ็กต์ `Style` เดียวกันได้:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **ทำไมวิธีนี้ถึงได้ผล:** อ็อบเจ็กต์ `Style` รวมคุณสมบัติวิสัยทั้งหมดของเซลล์ไว้ เมื่อคุณส่งอาเรย์ไปยัง `ImportDataTable` แต่ละเซลล์จะสืบทอดสไตล์ที่กำหนดโดยอัตโนมัติ

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ข้อผิดพลาด | อาการ | วิธีแก้ |
|------------|-------|----------|
| ลืมสร้างอินสแตนซ์ `Style` แต่ละตัว | `NullReferenceException` ระหว่างการนำเข้า | วนลูปผ่านอาเรย์และเรียก `CreateStyle()` ก่อนตั้งค่าคุณสมบัติ |
| ใช้ดัชนีรูปแบบตัวเลขที่มีมาให้ผิด | รูปแบบผิด (เช่น วันที่แสดงเป็นจำนวนเต็ม) | ตรวจสอบเอกสารของไลบรารีเพื่อหาค่าคงที่ `Number` ที่ถูกต้อง |
| ไม่ได้บันทึก workbook | ไม่มีไฟล์ผลลัพธ์หรือไฟล์ว่าง | เรียก `workbook.Save(...)` หลังจากการนำเข้าเสร็จ |
| ไม่ตรงกันของโลคัลสำหรับสัญลักษณ์สกุลเงิน | `$` ปรากฏแม้ในโลคัลที่ไม่ใช่สหรัฐ | ใช้สตริงรูปแบบกำหนดเองพร้อมสัญลักษณ์ที่เหมาะสม (เช่น `"€#,##0.00"`) |

## ตัวอย่างเต็มที่สามารถรันได้



## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณ

- [สร้างไฟล์ Excel ด้วย C# – จัดรูปแบบเซลล์และตั้งค่ารูปแบบสกุลเงิน](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [วิธีจัดรูปแบบคอลัมน์ Excel ใน C# – คู่มือฉบับสมบูรณ์](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [สร้าง Excel Workbook ด้วย C# – ใช้รูปแบบสกุลเงินและนำเข้า DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}