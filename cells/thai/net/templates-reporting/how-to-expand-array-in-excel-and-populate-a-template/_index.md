---
category: general
date: 2026-09-18
description: เรียนรู้วิธีขยายอาเรย์ใน Excel ด้วยฟังก์ชัน EXPAND, เติมข้อมูลในเทมเพลต
  Excel, และสร้างแผ่นงาน Excel ที่มีช่วงไดนามิกด้วย C#
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: th
lastmod: 2026-09-18
og_description: วิธีขยายอาร์เรย์ใน Excel ด้วยฟังก์ชัน EXPAND, เติมข้อมูลในเทมเพลต
  Excel, และสร้างโซลูชันช่วงไดนามิกใน Excel ด้วยโค้ด C#
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: วิธีขยายอาร์เรย์ใน Excel และเติมข้อมูลลงในเทมเพลต
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: วิธีขยายอาร์เรย์ใน Excel และเติมข้อมูลลงในเทมเพลต
url: /th/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีขยายอาร์เรย์ใน Excel และเติมเทมเพลต

หากคุณต้องการ **how to expand array** ใน Excel ขณะเติมเทมเพลตที่ออกแบบล่วงหน้า คู่มือนี้จะแสดงวิธีแก้ไขแบบครบวงจร ตั้งแต่ต้นจนจบ โดยใช้ฟังก์ชัน `EXPAND` ร่วมกับ Smart Markers ของ Aspose.Cells คุณสามารถแปลงการอ้างอิงเซลล์เดียวให้เป็นช่วง 5 × 5 และแทนที่มาร์คเกอร์เช่น `{IsActive}` ด้วยข้อมูลจริงโดยอัตโนมัติ

คุณจะได้เห็นวิธี **populate excel template**, สร้าง **dynamic range excel**, และใช้งาน **use expand function** อย่างถูกต้องในโครงการ C# เมื่อจบบทเรียนคุณจะมีโปรแกรมที่สามารถรันได้ซึ่งโหลดไฟล์ `.xlsx` ขยายสูตรอาร์เรย์ ใช้ Smart Markers และบันทึกผลลัพธ์

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Core 3.1+)
* Aspose.Cells for .NET (แพ็คเกจ NuGet `Aspose.Cells`)
* ไฟล์ Excel workbook ที่มีเซลล์สูตรเป็น placeholder (เช่น `B2`) และ Smart Marker เช่น `{IsActive}`
* ความคุ้นเคยพื้นฐานกับ C# และสูตร Excel

> **Pro tip:** ฟังก์ชัน `EXPAND` มีให้ใช้เฉพาะใน Excel for Microsoft 365 และ Excel 2021+ เวอร์ชันเก่าจะคืนค่า error `#NAME?`

## ขั้นตอนที่ 1: วิธีขยายอาร์เรย์ด้วยฟังก์ชัน EXPAND

ขั้นตอนแรกคือการโหลด workbook และเขียนสูตร `EXPAND` ที่แปลงเซลล์ต้นทางเดียวให้เป็นเมทริกซ์ขนาดใหญ่ขึ้น.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

ทำไมเรื่องนี้สำคัญ: `EXPAND` ช่วยขจัดความจำเป็นในการคัดลอกสูตรด้วยตนเองไปยังแถวและคอลัมน์ เมื่อเซลล์ต้นทาง (`A2`) เปลี่ยนแปลง บล็อก 5 × 5 ทั้งหมดจะอัปเดตโดยอัตโนมัติ ทำให้คุณได้ **dynamic range excel** ที่ตอบสนองต่อการเปลี่ยนแปลงของข้อมูล

## ขั้นตอนที่ 2: เติมเทมเพลต Excel ด้วย Smart Markers

Smart Markers ให้คุณฝัง placeholder ไว้ในเทมเพลตซึ่งจะถูกแทนที่ด้วยค่าจากอ็อบเจ็กต์ C# นี่เป็นวิธีที่สะดวกที่สุดในการ **populate excel template** โดยไม่ต้องเขียนโค้ดแบบ cell‑by‑cell.  

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

คำสั่ง `SmartMarkersProcessor().Apply` จะสแกนทั้งชีต ค้นหา `{IsActive}` และใส่ค่า boolean ลงไป สูตรจะประเมินเป็น `"Active"` หรือ `"Inactive"` โดยอัตโนมัติ

## ขั้นตอนที่ 3: ตรวจสอบช่วงที่ขยายและผลลัพธ์ที่เติม

หลังจากใช้สูตร `EXPAND` และ Smart Markers แล้ว คุณสามารถอ่านค่าเซลล์บางเซลล์โดยโปรแกรมเพื่อยืนยันว่าทุกอย่างทำงานตามที่คาดหวัง  

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

การรันโปรแกรมควรพิมพ์ค่าต้นฉบับจาก `A2` (หรือผลลัพธ์อาร์เรย์) และแสดง **Active** หรือ **Inactive** ขึ้นอยู่กับค่าแฟล็ก `IsActive`

## ขั้นตอนที่ 4: บันทึก workbook – ผลลัพธ์สุดท้าย

สุดท้าย ให้เขียน workbook ที่แก้ไขแล้วลงดิสก์ ขั้นตอนนี้แสดงกระบวนการครบวงจรตั้งแต่การโหลด การขยาย การเติม จนถึงการบันทึกไฟล์  

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

ไฟล์ `output.xlsx` ที่บันทึกแล้วตอนนี้มีเมทริกซ์ 5 × 5 ที่สร้างโดยสูตร `EXPAND` และเซลล์ที่แสดงค่าของ `{IsActive}` เปิดไฟล์ใน Excel เพื่อดู dynamic range ทำงาน

## กรณีขอบและแนวทางปฏิบัติที่ดีที่สุด

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Excel version does not support `EXPAND`| ใช้สูตรคลาสสิก `=OFFSET` หรือ `=INDEX` แทน หรืออัปเกรดเป็น Office 365. |
| Need to expand to a variable size      | ใช้ `ROWS(source)` และ `COLUMNS(source)` ภายใน `EXPAND` เพื่อความยืดหยุ่นจริง.   |
| Multiple Smart Markers in the same sheet| เรียก `SmartMarkersProcessor().Apply` ครั้งเดียวพร้อมอ็อบเจ็กต์ข้อมูลแบบรวม.      |
| Large workbooks ( > 10 000 rows)       | ปิดการคำนวณขณะเขียนสูตร (`workbook.Settings.CheckFormula = false`). |

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มรูปแบบที่สามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้  

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**ผลลัพธ์ที่คาดหวังเมื่อคุณรันโปรแกรม** (สมมติว่า `A2` มีค่าเลข `42`)  

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

การเปิด `output.xlsx` จะแสดงบล็อก 5 × 5 ที่เต็มด้วยค่าที่ได้จาก `A2` และเซลล์ที่แสดง **Active**.

## สรุป

ตอนนี้คุณทราบ **how to expand array** ใน Excel ด้วยฟังก์ชัน `EXPAND` วิธี **populate excel template** ด้วย Smart Markers และวิธีสร้าง **dynamic range excel** ที่ปรับตัวอัตโนมัติตามข้อมูลต้นทาง ตัวอย่างยังแสดงวิธีที่ถูกต้องในการ **use expand function** และ **expand array formula** ในสถานการณ์อัตโนมัติ C# จริง

ต่อไป พิจารณาการขยายโซลูชัน:

* แทนที่มิติ `5,5` คงที่ด้วย `ROWS(A2:A10), COLUMNS(A2:E2)` เพื่อให้ช่วงเป็นตัวแปรจริง.
* รวมหลาย Smart Markers เพื่อสร้างรายงานเต็มรูปแบบ (เช่น รายชื่อพนักงาน ตารางขาย).
* สำรวจ API การจัดรูปแบบของ Aspose.Cells เพื่อจัดรูปแบบบล็อกที่ขยายโดยอัตโนมัติ.

อย่าลังเลที่จะทดลองกับอาร์เรย์ต้นทาง ชื่อมาร์คเกอร์ และรูปแบบ workbook ต่าง ๆ ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ

- [ส่งออกข้อมูลไปยัง Excel: เติมเทมเพลตจากอาร์เรย์ใน C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [วิธีสร้างอาร์เรย์ใน Excel ด้วย C# – คู่มือขั้นตอน](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [การประมวลผลข้อมูลด้วยฟังก์ชันอาร์เรย์ใน Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}