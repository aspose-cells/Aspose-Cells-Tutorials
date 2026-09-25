---
category: general
date: 2026-03-30
description: สร้างไฟล์ Excel ด้วย C# พร้อมการจัดรูปแบบสกุลเงิน เรียนรู้วิธีนำเข้า
  DataTable, เพิ่มรูปแบบตัวเลขใน Excel, และใช้รูปแบบสกุลเงินให้กับคอลัมน์ในเวลาไม่กี่นาที.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: th
og_description: สร้างไฟล์ Excel ด้วย C# และกำหนดรูปแบบเซลล์เป็นสกุลเงินทันที คู่มือขั้นตอนนี้แสดงวิธีนำเข้า
  DataTable ไปยัง Excel และเพิ่มรูปแบบตัวเลขใน Excel สำหรับคอลัมน์หนึ่ง
og_title: สร้าง Excel Workbook ด้วย C# – คู่มือการจัดรูปแบบสกุลเงิน
tags:
- Aspose.Cells
- C#
- Excel automation
title: สร้างไฟล์ Excel ด้วย C# – ใช้รูปแบบสกุลเงินและนำเข้า DataTable
url: /th/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook C# – ใช้รูปแบบสกุลเงินและนำเข้า DataTable

เคยต้องการ **create Excel workbook C#** ที่ดูเหมือนรายงานที่เรียบหรูแล้วหรือไม่? บางทีคุณอาจดึงตัวเลขการขายจากฐานข้อมูลและต้องการให้คอลัมน์ราคาแสดงเป็นดอลลาร์โดยไม่ต้องแก้ไข Excel ด้วยตนเอง ฟังดูคุ้นเคยไหม? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่เจออุปสรรคนี้เมื่อต้องอัตโนมัติการส่งออก Excel ครั้งแรก

ในบทแนะนำนี้เราจะพาคุณผ่านโซลูชันที่ครบถ้วนพร้อมรันได้ทันทีที่ **creates an Excel workbook C#**, นำเข้า `DataTable`, และ **formats the Price column as currency**. เมื่อเสร็จคุณจะได้ไฟล์ชื่อ `StyledTable.xlsx` ที่สามารถเปิดดูและเห็นตัวเลขที่จัดรูปแบบอย่างสวยงาม ไม่ต้องทำการประมวลผลเพิ่มเติมใด ๆ

> **สิ่งที่คุณจะได้เรียนรู้**
> - วิธีตั้งค่า Aspose.Cells ในโปรเจกต์ .NET  
> - วิธี **import datatable to excel** ด้วยอาเรย์สไตล์  
> - วิธี **add number format excel** ให้กับคอลัมน์เฉพาะ  
> - เคล็ดลับการจัดการคอลัมน์เพิ่มเติมหรือโลคัลต่าง ๆ  

> **ข้อกำหนดเบื้องต้น**  
> - .NET 6+ (หรือ .NET Framework 4.6+) ที่ติดตั้งแล้ว  
> - Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`)  
> - ความคุ้นเคยพื้นฐานกับ C# และ DataTables  

---

## ขั้นตอนที่ 1: เตรียม DataTable (import datatable to excel)

ก่อนอื่นเราต้องมีข้อมูลตัวอย่าง ในแอปจริงคุณอาจเติมตารางนี้จากการ query ฐานข้อมูล แต่ตัวอย่างที่กำหนดค่าไว้ล่วงหน้าจะทำให้เข้าใจง่าย

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*ทำไมเรื่องนี้ถึงสำคัญ*: `DataTable` เป็นสะพานเชื่อมระหว่างข้อมูลธุรกิจของคุณกับไฟล์ Excel. Aspose.Cells สามารถนำเข้ามันโดยตรง พร้อมคงชื่อคอลัมน์และประเภทข้อมูลไว้

---

## ขั้นตอนที่ 2: สร้าง Workbook ใหม่ (create excel workbook c#)

ต่อไปเราจะสร้างอ็อบเจ็กต์ไฟล์ Excel จริง ๆ คิดว่าเป็นผ้าใบเปล่าที่คุณจะวาดบนมัน

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **เคล็ดลับ:** หากต้องการหลายชีต ให้เรียก `workbook.Worksheets.Add()` และตั้งชื่อแต่ละชีตให้มีความหมาย

---

## ขั้นตอนที่ 3: กำหนดสไตล์สกุลเงิน (format cells currency)

Aspose.Cells ให้คุณสร้างอ็อบเจ็กต์ `Style` ที่บรรยายลักษณะของเซลล์ สำหรับสกุลเงินเราจะใช้หมายเลขรูปแบบในตัวที่มี ID 164 (`"$#,##0.00"`)

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*ทำไมไม่ตั้งสตริงรูปแบบโดยตรง?* การใช้ ID ในตัวช่วยให้เข้ากันได้กับหลายเวอร์ชันของ Excel และหลีกเลี่ยงปัญหาโลคัลที่อาจเกิดขึ้น

---

## ขั้นตอนที่ 4: สร้างอาเรย์สไตล์ (apply currency format column)

เมื่อทำการนำเข้า `DataTable` คุณสามารถส่งอาเรย์ของอ็อบเจ็กต์ `Style` — หนึ่งอ็อบเจ็กต์ต่อคอลัมน์ `null` หมายถึง “ใช้สไตล์เริ่มต้น”. ที่นี่เราจะใช้ `priceStyle` เฉพาะกับคอลัมน์ที่สอง

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

หากคุณเพิ่มคอลัมน์ในภายหลัง เพียงขยายอาเรย์ให้สอดคล้อง ความยาวของ `columnStyles` ต้องตรงกับจำนวนคอลัมน์ที่นำเข้า มิฉะนั้น Aspose จะโยนข้อยกเว้น

---

## ขั้นตอนที่ 5: นำเข้า DataTable พร้อมสไตล์ (import datatable to excel)

ตอนนี้จุดเปลี่ยนเกิดขึ้น—`DataTable` ของเราตกลงใน worksheet และคอลัมน์ราคาแสดงเป็นสกุลเงินทันที

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*ถ้าคุณมีคอลัมน์มากกว่าสองคอลัมน์ล่ะ?* เพียงขยาย `columnStyles` ให้แต่ละคอลัมน์ได้รับสไตล์ที่เหมาะสม (หรือ `null` สำหรับค่าเริ่มต้น). วิธีนี้เป็นวิธีที่สะอาดที่สุดในการ **add number format excel** อย่างเลือกสรร

---

## ขั้นตอนที่ 6: บันทึก Workbook (create excel workbook c#)

สุดท้าย เราจะเขียนไฟล์ลงดิสก์ เลือกโฟลเดอร์ใดก็ได้ที่คุณมีสิทธิ์เขียน

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

เปิด `StyledTable.xlsx` ใน Excel แล้วคุณควรเห็น:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

คอลัมน์ **Price** ได้รับการจัดรูปแบบเป็นสกุลเงินแล้ว—ไม่ต้องทำขั้นตอนเพิ่มเติมใด ๆ

---

## กรณีขอบและความหลากหลาย

### คอลัมน์เพิ่ม, รูปแบบต่าง ๆ

หากต้องการ **format cells currency** สำหรับหลายคอลัมน์ (เช่น Cost, Tax, Total) ให้สร้าง `Style` แยกสำหรับแต่ละคอลัมน์และเติมลงใน `columnStyles` ตามลำดับ:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### สกุลเงินตามโลคัล

สำหรับยูโรหรือปอนด์อังกฤษ ให้ใช้ ID ที่ต่างกัน (เช่น 165 สำหรับ `€#,##0.00`). หรือกำหนดสตริงรูปแบบแบบกำหนดเอง:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### ชุดข้อมูลขนาดใหญ่

Aspose.Cells รองรับแถวหลายล้านแถว แต่การใช้สไตล์หลายอ็อบเจ็กต์จะเพิ่มการใช้หน่วยความจำ ใช้อ็อบเจ็กต์ `Style` เดียวสำหรับคอลัมน์สกุลเงินทั้งหมดเพื่อประหยัดทรัพยากร

### สไตล์หาย

หาก `columnStyles` สั้นกว่าจำนวนคอลัมน์ Aspose จะใช้สไตล์เริ่มต้นกับคอลัมน์ที่เหลือ ซึ่งเป็นประโยชน์เมื่อคุณสนใจแค่บางคอลัมน์เท่านั้น

---

## ตัวอย่างทำงานเต็มรูปแบบ (All Steps Combined)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในแอปคอนโซลได้ รวมทุกส่วนที่เราได้พูดถึง พร้อมคอมเมนต์ช่วยอธิบายเล็กน้อย

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** การเปิด `StyledTable.xlsx` จะเห็นคอลัมน์ `Price` มีสัญลักษณ์ดอลลาร์และแสดงสองตำแหน่งทศนิยม ตามที่คำสั่ง **format cells currency** ระบุไว้

---

## คำถามที่พบบ่อย

**ถาม: ทำงานได้กับ .NET Core หรือไม่?**  
ตอบ: ทำได้แน่นอน. Aspose.Cells รองรับ .NET‑standard ดังนั้นคุณสามารถใช้กับ .NET 5, .NET 6 หรือเวอร์ชันใหม่กว่าโดยไม่ต้องเปลี่ยนแปลง

**ถาม: ถ้า DataTable ของฉันมี 10 คอลัมน์ แต่ต้องการจัดรูปแบบเฉพาะคอลัมน์ที่ 5 เท่านั้นทำอย่างไร?**  
ตอบ: สร้าง `Style[]` ความยาว 10, เติมตำแหน่ง 0‑4 และ 6‑9 ด้วย `null`, แล้วใส่สไตล์ที่กำหนดเองที่ตำแหน่ง 4 (นับจากศูนย์). Aspose จะเคารพแต่ละค่า

**ถาม: สามารถซ่อนแถวหัวตารางได้หรือไม่?**  
ตอบ: หลังนำเข้าให้ตั้งค่า `worksheet.Cells.Rows[0].Hidden = true;` หรือส่ง `false` ให้พารามิเตอร์ `includeColumnNames` ใน `ImportDataTable`

---

## สรุป

เราได้ **create an Excel workbook C#**, นำเข้า `DataTable`, และ **applied a currency format column** ด้วย Aspose.Cells ขั้นตอนหลัก—การเตรียมข้อมูล, การกำหนดสไตล์, การสร้างอาเรย์สไตล์, การนำเข้าโดยใช้ `ImportDataTable`, และการบันทึก—ครอบคลุมงานอัตโนมัติ Excel ส่วนใหญ่

ต่อจากนี้คุณอาจสำรวจต่อ:

- **add number format excel** สำหรับวันที่หรือเปอร์เซ็นต์  
- การส่งออกหลายชีตในไฟล์เดียว  
- การใช้ **format cells currency** กับสัญลักษณ์โลคัลต่าง ๆ  
- การอัตโนมัติการสร้างแผนภูมิจากข้อมูลเดียวกัน  

ลองทำตามดู แล้วคุณจะกลายเป็นผู้เชี่ยวชาญด้านการรายงาน Excel ในทีมของคุณได้อย่างรวดเร็ว มีไอเดียหรือวิธีพิเศษอยากแชร์? แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}