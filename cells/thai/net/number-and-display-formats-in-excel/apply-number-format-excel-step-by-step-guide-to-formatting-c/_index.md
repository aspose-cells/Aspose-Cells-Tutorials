---
category: general
date: 2026-02-26
description: ใช้รูปแบบตัวเลขใน Excel อย่างรวดเร็วและเรียนรู้วิธีจัดรูปแบบคอลัมน์เป็นสกุลเงิน
  ตั้งค่ารูปแบบตัวเลขของคอลัมน์ และตั้งค่าสีฟอนต์ของคอลัมน์ เพียงไม่กี่บรรทัดของ C#
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: th
og_description: ใช้รูปแบบตัวเลขใน Excel ด้วย C# อย่างง่าย เรียนรู้การจัดรูปแบบคอลัมน์เป็นสกุลเงิน
  ตั้งค่ารูปแบบตัวเลขของคอลัมน์ และตั้งค่าสีฟอนต์ของคอลัมน์เพื่อสเปรดชีตระดับมืออาชีพ
og_title: การกำหนดรูปแบบตัวเลขใน Excel – คู่มือฉบับสมบูรณ์สำหรับการจัดสไตล์คอลัมน์
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: ใช้รูปแบบตัวเลขใน Excel – คู่มือขั้นตอนต่อขั้นตอนสำหรับการจัดรูปแบบคอลัมน์
url: /th/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

images: none.

All good.

Now produce final content with translations.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – วิธีจัดรูปแบบคอลัมน์ใน Excel ด้วย C#

เคยสงสัยหรือไม่ว่า **apply number format excel** ขณะคุณกำลังวนลูปผ่าน `DataTable` อยู่? คุณไม่ได้เป็นคนเดียว นักพัฒนาส่วนใหญ่มักเจออุปสรรคเมื่อจำเป็นต้องมีหัวข้อสีฟ้า *และ* คอลัมน์ที่มีรูปแบบสกุลเงินในกระบวนการนำเข้าครั้งเดียว ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และอ็อบเจ็กต์สไตล์ที่เหมาะสม คุณสามารถทำได้โดยไม่ต้องทำ post‑processing กับชีต

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงวิธี **format column as currency**, **set column number format** สำหรับคอลัมน์อื่น ๆ และแม้กระทั่ง **set column font color** สำหรับหัวคอลัมน์ เมื่อเสร็จคุณจะมีแพทเทิร์นที่สามารถนำไปใช้ซ้ำได้ในโปรเจกต์ Aspose.Cells (หรือที่คล้ายกัน) ใด ๆ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีดึง `DataTable` และแมปแต่ละคอลัมน์ไปยัง `Style` เฉพาะ
- ขั้นตอนที่แน่นอนเพื่อ **apply number format excel** โดยใช้ `Worksheet.Cells.ImportDataTable`
- ทำไมการสร้างสไตล์ล่วงหน้าจึงมีประสิทธิภาพมากกว่าการจัดรูปแบบเซลล์ทีละเซลล์
- การจัดการกรณีขอบเมื่อตารางต้นทางมีคอลัมน์มากกว่าที่คุณได้กำหนดสไตล์
- ตัวอย่างโค้ดเต็มรูปแบบพร้อมคัดลอก‑วางที่คุณสามารถรันได้ทันที

> **Prerequisite:** คู่มือฉบับนี้สมมติว่าคุณมี Aspose.Cells สำหรับ .NET (หรือไลบรารีใด ๆ ที่เปิดเผย API ของ `Workbook`, `Worksheet`, `Style`) ที่อ้างอิงในโปรเจกต์ของคุณ หากคุณใช้ไลบรารีอื่น แนวคิดสามารถแปลโดยตรง—เพียงเปลี่ยนชื่อประเภท

---

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเป็น DataTable

ก่อนที่การจัดรูปแบบใด ๆ จะเกิดขึ้น คุณต้องมีข้อมูลดิบ ก่อนหน้า ในสถานการณ์จริงส่วนใหญ่ ข้อมูลจะอยู่ในฐานข้อมูล, CSV หรือ API เพื่อความชัดเจน เราจะจำลอง `DataTable` ง่าย ๆ ที่มีสองคอลัมน์: *Product* (string) และ *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Why this matters:** การดึงข้อมูลเข้าสู่ `DataTable` ให้คุณได้รูปแบบตารางในหน่วยความจำที่ `ImportDataTable` สามารถใช้ได้โดยตรง ลดความจำเป็นในการแทรกเซลล์แบบแมนนวลทีละเซลล์

## ขั้นตอนที่ 2: สร้างอาร์เรย์ของ Style – หนึ่งต่อหนึ่งคอลัมน์

`ImportDataTable` overload ที่เราจะใช้รับอาร์เรย์ของอ็อบเจ็กต์ `Style` แต่ละรายการสอดคล้องกับดัชนีของคอลัมน์ หากคุณเว้นรายการเป็น `null` คอลัมน์นั้นจะสืบทอดสไตล์เริ่มต้นของเวิร์กบุ๊ก

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** การประกาศอาร์เรย์ *หลังจาก* มี `DataTable` จะทำให้ขนาดตรงกันพอดี ป้องกัน `IndexOutOfRangeException` ในภายหลัง

## ขั้นตอนที่ 3: ตั้งค่าสีฟอนต์ของคอลัมน์ (สีน้ำเงิน) สำหรับคอลัมน์แรก

คำขอที่พบบ่อยคือการเน้นหัวข้อหรือคอลัมน์สำคัญด้วยสีฟอนต์ที่แตกต่าง ที่นี่เราจะทำให้ข้อความของคอลัมน์แรกเป็นสีน้ำเงิน

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Why use a style object?** สไตล์สามารถนำกลับมาใช้ใหม่และประยุกต์ใช้เป็นกลุ่ม ซึ่งเร็วกว่าการวนลูปผ่านทุกเซลล์หลังการนำเข้าอย่างมาก เวิร์กบุ๊กจะเก็บสไตล์ไว้ในแคชหนึ่งครั้ง แล้วใช้ซ้ำสำหรับทุกเซลล์ในคอลัมน์นั้น

## ขั้นตอนที่ 4: จัดรูปแบบคอลัมน์ที่สองเป็นสกุลเงิน

รูปแบบตัวเลขที่มาพร้อมกับ Excel จะระบุด้วยดัชนี `14` ตรงกับรูปแบบสกุลเงินเริ่มต้น (เช่น `$1,234.00`). หากต้องการรูปแบบกำหนดเอง คุณสามารถกำหนดสตริงรูปแบบแทนได้

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** หากเวิร์กบุ๊กของคุณใช้โลคัลที่สัญลักษณ์สกุลเงินไม่ใช่ `$` ดัชนีเดียวกันจะปรับอัตโนมัติ (เช่น `€` สำหรับโลคัลเยอรมัน)

## ขั้นตอนที่ 5: นำเข้า DataTable ด้วยสไตล์ที่กำหนดไว้

ตอนนี้เราจะรวมทุกอย่างเข้าด้วยกัน เมธอด `ImportDataTable` จะวางข้อมูลเริ่มจากเซลล์ `A1` (แถว 0, คอลัมน์ 0) และประยุกต์สไตล์ที่เราจัดเตรียมไว้

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- พารามิเตอร์ที่สอง `true` บอก Aspose.Cells ให้ถือแถวแรกของ `DataTable` เป็นหัวคอลัมน์
- พิกัด `0, 0` ระบุมุมบน‑ซ้ายที่การนำเข้าเริ่มต้น
- `columnStyles` แมปแต่ละคอลัมน์ไปยังสไตล์ที่สอดคล้องกัน

## ขั้นตอนที่ 6: บันทึกเวิร์กบุ๊ก (ไม่บังคับ แต่สะดวกสำหรับการตรวจสอบ)

หากคุณต้องการดูผลลัพธ์ใน Excel เพียงบันทึกเวิร์กบุ๊กลงดิสก์ ขั้นตอนนี้ไม่จำเป็นสำหรับตรรกะการจัดรูปแบบ แต่มีประโยชน์สำหรับการดีบัก

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### ผลลัพธ์ที่คาดหวัง

| **Product** (สีฟอนต์สีน้ำเงิน) | **Price** (สกุลเงิน) |
|--------------------------|----------------------|
| Apple                    | $1.25                |
| Banana                   | $0.75                |
| Cherry                   | $2.10                |

- คอลัมน์ *Product* ปรากฏเป็นสีน้ำเงิน ทำให้โดดเด่น
- คอลัมน์ *Price* แสดงค่าด้วยสัญลักษณ์สกุลเงินเริ่มต้นและทศนิยมสองตำแหน่ง

---

## คำถามที่พบบ่อยและรูปแบบต่าง ๆ

### ฉันจะ **set column number format** สำหรับมากกว่าสองคอลัมน์ได้อย่างไร?

เพียงขยายอาร์เรย์ `columnStyles` ตัวอย่างเช่น เพื่อแสดงเปอร์เซ็นต์ในคอลัมน์ที่สาม:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### ถ้าฉันต้องการรูปแบบสกุลเงิน *custom* เช่น “USD 1,234.00” จะทำอย่างไร?

แทนที่คุณสมบัติ `Number` ด้วยสตริงรูปแบบ:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### ฉันสามารถ **set column font color** ให้กับคอลัมน์ตัวเลขโดยไม่กระทบรูปแบบตัวเลขได้หรือไม่?

ได้เลย สไตล์สามารถประกอบกันได้ คุณสามารถตั้งค่า `Font.Color` และ `Number` บนอินสแตนซ์ `Style` เดียวกัน:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### จะเกิดอะไรขึ้นหาก `DataTable` มีคอลัมน์มากกว่าสไตล์?

คอลัมน์ใดที่ไม่มีสไตล์ชัดเจน (`null` entry) จะสืบทอดสไตล์เริ่มต้นของเวิร์กบุ๊ก เพื่อหลีกเลี่ยง `null` ที่ไม่ตั้งใจ คุณสามารถเริ่มต้นอาร์เรย์ทั้งหมดด้วยสไตล์พื้นฐานก่อน:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

จากนั้นจึงเขียนทับเฉพาะคอลัมน์ที่คุณต้องการเท่านั้น.

### วิธีนี้ทำงานกับชุดข้อมูลขนาดใหญ่ (10k+ แถว) หรือไม่?

ใช่ เพราะการจัดรูปแบบจะถูกประยุกต์ *หนึ่งครั้งต่อคอลัมน์* ก่อนการนำเข้า การดำเนินการจึงอยู่ในระดับ O(N) ตามจำนวนแถวและการใช้หน่วยความจำน้อย หลีกเลี่ยงการวนลูปผ่านแต่ละเซลล์หลังการนำเข้า—ที่นั่นคือจุดที่ประสิทธิภาพลดลง

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

รันโปรแกรม เปิดไฟล์ `StyledReport.xlsx` แล้วคุณจะเห็นผลลัพธ์ของ **apply number format excel** ทันที

## สรุป

เราเพิ่งแสดงวิธีที่สะอาดและมีประสิทธิภาพในการ **apply number format excel** ให้กับ `DataTable` ที่นำเข้า โดยการเตรียมอาร์เรย์ `Style[]` ล่วงหน้า คุณสามารถ **format column as currency**, **set column number format**, และ **set column font color** ในหนึ่งคำสั่ง—ไม่ต้องทำ post‑processing  

คุณสามารถขยายแพทเทิร์นนี้ได้: เพิ่มการจัดรูปแบบตามเงื่อนไข, ผสานเซลล์สำหรับหัวเรื่อง, หรือแม้กระทั่งแทรกสูตร หลักการเดียวกันจะช่วยให้โค้ดของคุณเป็นระเบียบและสเปรดชีตดูเป็นมืออาชีพ

### ต่อไปคืออะไร?

- สำรวจ **conditional formatting** เพื่อไฮไลท์ค่าที่เกินเกณฑ์
- ผสานเทคนิคนี้กับ **pivot table generation** เพื่อการรายงานแบบไดนามิก
- ลอง **setting column number format** สำหรับวันที่, เปอร์เซ็นต์, หรือโนเทชันทางวิทยาศาสตร์แบบกำหนดเอง

คุณมีวิธีพิเศษที่ลองแล้วหรือไม่? แชร์ในคอมเมนต์—ให้เราต่อเนื่อง

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}