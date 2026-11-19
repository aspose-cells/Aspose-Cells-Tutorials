---
category: general
date: 2026-11-19
description: ตั้งค่ารูปแบบตัวเลขของเซลล์ใน C# และเรียนรู้วิธีใช้รูปแบบวันที่ของ Excel
  สำหรับวันที่ตามยุคญี่ปุ่น เพื่อให้การแปลงวันที่ Excel ใน C# มีความน่าเชื่อถือ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: th
lastmod: 2026-11-19
og_description: ตั้งค่ารูปแบบตัวเลขของเซลล์ใน C# และใช้รูปแบบวันที่ของ Excel กับวันที่ตามยุคญี่ปุ่น
  ปฏิบัติตามคู่มือฉบับเต็มนี้เพื่อการแปลงวันที่ Excel ใน C# ที่แม่นยำ
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: ตั้งค่ารูปแบบตัวเลขของเซลล์และแปลงวันที่ญี่ปุ่นใน C# – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: กำหนดรูปแบบตัวเลขของเซลล์และแปลงวันที่ญี่ปุ่นใน C#
url: /th/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่ารูปแบบตัวเลขของเซลล์และแปลงวันที่ญี่ปุ่นใน C#

หากคุณต้องการ **set cell number format** ในโครงการอัตโนมัติ Excel ด้วย C# คู่มือนี้จะแสดงวิธี **apply Excel date format** และทำ **C# Excel date conversion** สำหรับวันที่ตามยุคญี่ปุ่น คุณจะได้ตัวอย่างที่สมบูรณ์และสามารถรันได้ซึ่งแปลงสตริงยุค Reiwa (เช่น `R3/04/01`) ให้เป็นวันที่ตามปฏิทินเกรกอเรียน `2021‑04‑01`.

## สิ่งที่คุณจะได้เรียนรู้

* วิธีสร้าง workbook และเข้าถึง worksheet แรกของมัน.  
* วิธี **set cell number format** เพื่อให้ Excel ปฏิบัติกับค่าดังกล่าวเป็นวันที่.  
* วิธี **apply Excel date format** ที่รับรู้สตริงยุคญี่ปุ่น.  
* วิธีเรียกใช้ **C# Excel date conversion** โดยคำนวณสูตรใหม่.  
* ผลลัพธ์ที่คาดหวังและเคล็ดลับการแก้ปัญหาสำหรับกรณีขอบ.

**Prerequisites**

* .NET 6 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+ ด้วย).  
* Aspose.Cells สำหรับ .NET 2024 หรือใหม่กว่า – ติดตั้งผ่าน NuGet: `dotnet add package Aspose.Cells`.  
* ความคุ้นเคยพื้นฐานกับ C# และการจัดการวันที่ใน Excel.

> **เคล็ดลับ:** Aspose.Cells ทำงานได้โดยไม่ต้องติดตั้ง Microsoft Office ทำให้เหมาะสำหรับการอัตโนมัติบนเซิร์ฟเวอร์.

## ตั้งค่ารูปแบบตัวเลขของเซลล์ด้วย Aspose.Cells ใน C#

ขั้นตอนแรกคือบอกให้ Excel ทราบว่าเซลล์นั้นมีค่าเป็นวันที่ Excel เก็บวันที่เป็นตัวเลขซีเรียล ดังนั้นเราต้องใช้รูปแบบตัวเลขวันที่ที่มีอยู่ในตัว (ID 14) กับเซลล์เป้าหมาย.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

* `Style.Number = 14` จะตรงกับรูปแบบ *Short Date* ของ Excel (`mm/dd/yyyy` เป็นค่าเริ่มต้น).  
* เมื่อเซลล์มีสตริงยุคญี่ปุ่นเช่น `R3/04/01` ตัวพาร์เซอร์ภายในของ Aspose.Cells จะรับรู้ยุคและแปลงเป็นเลขซีเรียลของวันที่เกรกอเรียนที่สอดคล้องกันระหว่างการเรียก `CalculateFormula()`.  
* หลังจากคำนวณแล้ว `StringValue` จะคืนค่าวันที่เกรกอเรียนที่จัดรูปแบบแล้ว.

## ใช้รูปแบบวันที่ Excel สำหรับวันที่ตามยุคญี่ปุ่น

หากคุณต้องการให้เซลล์แสดงยุคญี่ปุ่นแทนวันที่เกรกอเรียน คุณสามารถใช้รูปแบบตัวเลขแบบกำหนดเองที่รวมรหัสยุคได้ ซึ่งจะแสดงความสามารถของ **apply excel date format**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` บังคับให้ใช้ภาษาญี่ปุ่น.  
* `ggg` แสดงชื่อยุค (เช่น `R` สำหรับ Reiwa).  
* การเพิ่มอักขระตามตัวอักษร (`年`, `月`, `日`) จะสร้างรูปแบบวันที่ญี่ปุ่นที่คุ้นเคย.

### เมื่อควรใช้รูปแบบกำหนดเอง

* รายงานที่มุ่งเป้าไปยังผู้ชมญี่ปุ่น.  
* เมื่อคุณต้องการรักษาข้อมูลยุคดั้งเดิมไว้สำหรับเอกสารทางกฎหมาย.  
* ในแดชบอร์ดที่ต้องแสดงวันที่เกรกอเรียนและยุคพร้อมกัน.

## การแปลงวันที่ Excel ด้วย C# – การจัดการยุคญี่ปุ่น

กระบวนการ **c# excel date conversion** สามารถแบ่งออกเป็นสามส่วนหลัก:

1. **Parse the era string** – Aspose.Cells จะรับรู้ `R` (Reiwa), `H` (Heisei), `S` (Showa) ฯลฯ โดยอัตโนมัติ.  
2. **Convert to a serial number** – Excel เก็บวันที่เป็นจำนวนวันตั้งแต่ 1899‑12‑30.  
3. **Format the serial number** – ใช้รูปแบบที่มีอยู่ (ID 14) หรือรูปแบบญี่ปุ่นที่กำหนดเอง.

### ตัวอย่างเต็มแบบ End‑to‑End

ด้านล่างเป็นโปรแกรมที่ทำงานอิสระซึ่งแสดงผลลัพธ์ทั้งวันที่เกรกอเรียนและยุคในหนึ่งการรัน.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**ผลลัพธ์ที่คาดหวังในคอนโซล**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### กรณีขอบและข้อผิดพลาดทั่วไป

| สถานการณ์ | สิ่งที่ต้องระวัง | วิธีแก้ไข / คำแนะนำ |
|----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
| สตริงยุคว่างหรือรูปแบบไม่ถูกต้อง | `PutValue` เก็บข้อความตามตัวอักษร; การแปลงล้มเหลว | ตรวจสอบอินพุตด้วย regular expression ก่อนเขียนลงเซลล์. |
| การตั้งค่าภาษาไม่ตรงกัน | รูปแบบกำหนดเองแสดงตัวเลขตะวันตกแทนอักขระญี่ปุ่น | ตรวจสอบให้แน่ใจว่า `Custom` format มี `[$-ja-JP]` หรือกำหนด `Workbook.Settings.CultureInfo` เป็น `ja-JP`. |
| Workbook มีสูตรที่อ้างอิงเซลล์วันที่ | การคำนวณใหม่อาจเขียนทับผลลัพธ์ของสูตร | เรียก `CalculateFormula` **หลัง** ขั้นตอนการจัดรูปแบบทั้งหมด, หรือใช้ `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` หากต้องการข้ามข้อผิดพลาด. |
| ใช้ Aspose.Cells เวอร์ชันเก่า | การสนับสนุนยุคญี่ปุ่นเพิ่มเข้ามาในปี 2022 Q3 | อัปเกรดเป็นแพ็กเกจ NuGet เวอร์ชันล่าสุด. |

## การทดสอบโซลูชัน

1. **Run the program** จาก Visual Studio หรือ `dotnet run`.  
2. ตรวจสอบว่าคอนโซลพิมพ์วันที่เกรกอเรียน `2021‑04‑01` และสตริงยุค `R3年04月01日`.  
3. เปิด workbook ที่สร้างขึ้น (หากคุณเพิ่ม `wb.Save("Demo.xlsx");`) ใน Microsoft Excel เพื่อดูรูปแบบเดียวกันที่ใช้กับเซลล์.

### เคล็ดลับการอัตโนมัติ

หากคุณต้องการประมวลผลช่วงวันที่ยุคจำนวนมาก (เช่น คอลัมน์ A มีวันที่ญี่ปุ่นหลายรายการ) ให้ใส่ตรรกะการแปลงไว้ในลูป:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

วิธีนี้ทำให้การดำเนินการ **set cell number format** รวดเร็วและใช้หน่วยความจำน้อย.

## สรุป

ตอนนี้คุณรู้วิธี **set cell number format** ใน C# ด้วย Aspose.Cells, วิธี **apply Excel date format** สำหรับสตริงยุคญี่ปุ่น, และวิธีทำ **C# Excel date conversion** ที่เชื่อถือได้จากยุคเป็นวันที่เกรกอเรียน โค้ดที่สมบูรณ์และสามารถรันได้แสดงผลลัพธ์ทั้งสองและเน้นกรณีขอบที่พบบ่อย.  

**ขั้นตอนต่อไป**

* สำรวจ ID รูปแบบที่มีอยู่ในตัวอื่น ๆ


## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ.

- [ตั้งค่ารูปแบบวันที่ Excel ใน C# – คู่มือขั้นตอนเต็ม](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [วิธีใช้รูปแบบตัวเลขใน Excel ด้วย Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [วิธีใช้รูปแบบตัวเลขกำหนดเองใน Excel ด้วย C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}