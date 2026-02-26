---
category: general
date: 2026-02-21
description: สร้างสไตล์เซลล์ใน C# อย่างรวดเร็ว เรียนรู้วิธีการใช้สไตล์กับเซลล์ จัดกึ่งกลางข้อความในเซลล์
  ตั้งค่าการจัดแนวเซลล์ และเชี่ยวชาญการจัดรูปแบบเซลล์.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: th
og_description: สร้างสไตล์เซลล์ใน C# และเรียนรู้วิธีการนำสไตล์ไปใช้กับเซลล์, จัดข้อความให้อยู่กึ่งกลางในเซลล์,
  และตั้งค่าการจัดแนวของเซลล์ด้วยคู่มือที่ชัดเจนและเป็นขั้นตอน.
og_title: สร้างสไตล์เซลล์ใน C# – ใช้สไตล์กับเซลล์และจัดกึ่งกลางข้อความ
tags:
- C#
- Aspose.Cells
- Excel automation
title: สร้างสไตล์เซลล์ใน C# – วิธีนำสไตล์ไปใช้กับเซลล์และจัดข้อความให้อยู่กึ่งกลาง
url: /th/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

placeholders.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างสไตล์เซลล์ใน C# – คู่มือฉบับสมบูรณ์สำหรับการใช้สไตล์และการจัดศูนย์ข้อความ

เคยต้องการ **create cell style** ในแผ่นงาน Excel แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการอัตโนมัติ ความสามารถในการ **apply style to cell** กับอ็อบเจกต์เป็นสิ่งที่ทำให้สเปรดชีตธรรมดากลายเป็นรายงานที่ดูดี

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างเต็มที่สามารถรันได้ซึ่งจะแสดงให้คุณเห็น **how to center text** ภายในเซลล์ ตั้งค่าการจัดแนว และเพิ่มเส้นขอบบาง—ทั้งหมดในไม่กี่บรรทัดของ C# เมื่อจบคุณจะเข้าใจว่าทำไมแต่ละส่วนถึงสำคัญและจะปรับแต่งอย่างไรให้เหมาะกับสถานการณ์ของคุณ

## สิ่งที่คุณจะได้เรียนรู้

- ความเข้าใจที่ชัดเจนเกี่ยวกับกระบวนการ **create cell style** ด้วย Aspose.Cells (หรือไลบรารีที่คล้ายกัน)
- โค้ดที่คุณสามารถคัดลอก‑วางลงในแอปคอนโซลเพื่อ **apply style to cell**
- ความเข้าใจเกี่ยวกับ **center text in cell**, **set cell alignment**, และการจัดการกรณีขอบเช่นเซลล์ที่รวมกันหรือรูปแบบตัวเลขที่กำหนดเอง
- เคล็ดลับสำหรับการขยายสไตล์—ฟอนต์ต่าง ๆ สีพื้นหลัง หรือการจัดรูปแบบตามเงื่อนไข

> **Prerequisite:** Visual Studio 2022 (หรือ IDE ของ C# ใดก็ได้) และแพคเกจ NuGet Aspose.Cells for .NET ไม่ต้องมีการพึ่งพาอื่น ๆ

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า Namespaces

ก่อนที่เราจะ **create cell style** เราต้องมีโปรเจกต์ที่อ้างอิงไลบรารี Excel

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Why this matters:* การนำเข้า `Aspose.Cells` ทำให้เรามีสิทธิ์เข้าถึงคลาส `Workbook`, `Worksheet`, `Style` และ `Border` หากคุณใช้ไลบรารีอื่น (เช่น EPPlus) ชื่อคลาสอาจเปลี่ยนไปแต่แนวคิดยังคงเหมือนเดิม

---

## ขั้นตอนที่ 2: สร้าง Workbook และดึงเซลล์แรก

ตอนนี้เราจะ **create cell style** โดยเริ่มจากการอ้างอิงเซลล์ที่ต้องการจัดรูปแบบ

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

สังเกตว่าเราใช้ `Cell` แทน `var` แบบทั่วไป—การระบุประเภทอย่างชัดเจนทำให้โค้ดอ่านง่ายสำหรับผู้เริ่มต้น การเรียก `PutValue` จะเขียนสตริงเพื่อให้เรามองเห็นผลของสไตล์ได้ภายหลัง

---

## ขั้นตอนที่ 3: กำหนดสไตล์ – จัดศูนย์ข้อความ, เพิ่มเส้นขอบบาง

นี่คือหัวใจของการ **create cell style** เราจะตั้งค่าการจัดแนวนอน, เส้นขอบบาง, และคุณสมบัติเสริมบางอย่าง

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Why we do this:*  
- **HorizontalAlignment** และ **VerticalAlignment** ร่วมกันตอบคำถาม “**how to center text** in a cell?”  
- การเพิ่มเส้นขอบทั้งสี่ด้านทำให้เซลล์ดูเหมือนป้ายกล่อง ซึ่งมีประโยชน์สำหรับหัวตาราง  
- สีพื้นหลังไม่จำเป็นต้องใช้ แต่ช่วยแสดงวิธีขยายสไตล์ในภายหลัง

---

## ขั้นตอนที่ 4: ใช้สไตล์ที่กำหนดกับเซลล์ที่เลือก

เมื่อสไตล์พร้อมแล้ว เรา **apply style to cell** ด้วยการเรียกเมธอดเดียว

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

แค่นั้น—Aspose.Cells จะจัดการคัดลอกสไตล์เข้าไปในคอลเลกชันสไตล์ภายในของเซลล์ หากคุณต้องการรูปแบบเดียวกันบนช่วงหลายเซลล์ สามารถใช้ `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`

---

## ขั้นตอนที่ 5: บันทึก Workbook และตรวจสอบผลลัพธ์

การบันทึกอย่างรวดเร็วทำให้คุณเปิดไฟล์ใน Excel และยืนยันว่าข้อความถูกจัดศูนย์จริง ๆ และเส้นขอบปรากฏ

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Expected output:* เมื่อคุณเปิด **StyledCell.xlsx** เซลล์ **A1** จะมีข้อความ “Hello, styled world!” จัดศูนย์ทั้งแนวนอนและแนวตั้ง ล้อมรอบด้วยเส้นขอบสีเทาบาง และพื้นหลังสีเทาอ่อน

---

## ความแตกต่างทั่วไป & กรณีขอบ

### 1. จัดศูนย์ข้อความในพื้นที่ที่รวมกัน

หากคุณรวมเซลล์ **A1:C1** และยังต้องการให้ข้อความอยู่ตรงกลาง คุณต้องใช้สไตล์กับเซลล์ซ้ายบน **หลัง** การรวมเซลล์:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. ใช้รูปแบบตัวเลข

บางครั้งคุณต้อง **set cell alignment** *และ* แสดงตัวเลขด้วยรูปแบบเฉพาะ:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

การจัดแนวยังคงอยู่ตรงกลางในขณะที่ตัวเลขแสดงเป็น `12,345.68`

### 3. การใช้สไตล์อย่างมีประสิทธิภาพ

การสร้าง `Style` ใหม่สำหรับทุกเซลล์อาจทำให้ประสิทธิภาพลดลง แทนที่จะสร้างหลาย ๆ ครั้ง ให้สร้างอ็อบเจกต์สไตล์หนึ่งครั้งและใช้ซ้ำหลายเซลล์หรือหลายช่วง `StyleFlag` ช่วยให้คุณสามารถใช้เฉพาะส่วนที่ต้องการได้ ลดการใช้หน่วยความจำ

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## เคล็ดลับระดับมืออาชีพ & สิ่งที่ควรระวัง

- **อย่าลืมการจัดแนวแนวตั้ง** – การจัดศูนย์เฉพาะแนวนอนมักดูแปลก โดยเฉพาะกับแถวที่สูงขึ้น  
- **ประเภทเส้นขอบ**: `CellBorderType.Thin` เหมาะกับรายงานส่วนใหญ่ แต่คุณสามารถเปลี่ยนเป็น `Medium` หรือ `Dashed` เพื่อสร้างลำดับชั้นภาพ  
- **การจัดการสี**: เมื่อตั้งเป้าหมาย .NET Core ให้ใช้ `System.Drawing.Color` จากแพคเกจ `System.Drawing.Common` มิฉะนั้นจะเกิดข้อผิดพลาดรันไทม์  
- **รูปแบบการบันทึก**: หากต้องการความเข้ากันได้กับเวอร์ชัน Excel เก่า ให้เปลี่ยน `SaveFormat.Xlsx` เป็น `SaveFormat.Xls`

---

![ตัวอย่างการสร้างสไตล์เซลล์](https://example.com/images/create-cell-style.png "สร้างสไตล์เซลล์ใน C#")

*Alt text: ภาพหน้าจอแสดงเซลล์ที่มีข้อความจัดศูนย์และเส้นขอบบางที่สร้างโดยบทเรียนการสร้างสไตล์เซลล์*

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

รันโปรแกรมนี้ เปิด **StyledCell.xlsx** แล้วคุณจะเห็นผลลัพธ์ที่อธิบายไว้ก่อนหน้านี้ อย่าลังเลที่จะแก้ไขข้อความ, สไตล์เส้นขอบ หรือสีพื้นหลังให้ตรงกับแบรนด์ของคุณ

---

## สรุป

เราได้ **created cell style** ตั้งแต่ต้น, **applied style to cell**, และสาธิต **how to center text** ทั้งแนวนอนและแนวตั้ง ด้วยการเชี่ยวชาญบล็อกพื้นฐานเหล่านี้ คุณสามารถจัดรูปแบบหัวตาราง, เน้นผลรวม, หรือสร้างเทมเพลตรายงานทั้งหมดโดยไม่ต้องออกจาก C#  

หากคุณอยากลองขั้นต่อไป ลอง:

- **Applying the same style to a whole row** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`)  
- **Adding conditional formatting** เพื่อเปลี่ยนสีพื้นหลังตามค่าของเซลล์  
- **Exporting to PDF** พร้อมคงสไตล์ไว้

จำไว้ว่า การจัดสไตล์ไม่ได้มีแค่เรื่องความสวยงาม แต่ยังเกี่ยวกับการอ่านง่าย ทดลอง ปรับปรุง แล้วสเปรดชีตของคุณจะดูเป็นมืออาชีพเท่ากับโค้ดของคุณ

*Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}