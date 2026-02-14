---
category: general
date: 2026-02-14
description: สร้างเทมเพลตส่วนลดอย่างรวดเร็วและเรียนรู้วิธีการใช้ส่วนลดในสเปรดชีต,
  แทรกข้อมูลลงในเทมเพลต, และกำหนดคำนำหน้าตัวแปรสำหรับสมาร์ทมาร์คเกอร์.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: th
og_description: สร้างเทมเพลตส่วนลดด้วย C# เรียนรู้การใช้ส่วนลดในสเปรดชีต, แทรกข้อมูลลงในเทมเพลต,
  และกำหนดคำนำหน้าตัวแปรสำหรับสมาร์ทมาร์คเกอร์
og_title: สร้างเทมเพลตส่วนลด – คู่มือ C# เต็มรูปแบบ
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: สร้างเทมเพลตส่วนลดใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

reference to the `Aspose.Cells` (or similar) library that provides `SmartMarkerProcessor`, and a basic understanding of C# syntax. Nothing exotic." Keep as is but translate.

Also note the "Pro tip:" etc.

Also note "Expected output" etc.

All code block placeholders remain.

Let's produce final translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างเทมเพลตส่วนลด – คู่มือเต็ม C#

เคยต้อง **สร้างเทมเพลตส่วนลด** สำหรับรายงานการขายแต่ไม่แน่ใจว่าจะใส่ตัวเลขลงในสเปรดชีตโดยอัตโนมัติได้อย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในบทเรียนนี้เราจะสาธิตวิธี **สร้างเทมเพลตส่วนลด** อย่างละเอียด จากนั้น **ใช้ส่วนลดในเซลล์สเปรดชีต**, **ใส่ข้อมูลลงในเทมเพลต**, และแม้กระทั่ง **กำหนดคำนำหน้าตัวแปร** สำหรับ smart markers ของคุณ—ทั้งหมดด้วยโค้ด C# ที่สะอาดและกระชับ

เราจะเริ่มด้วยการอธิบายปัญหา แล้วจึงกระโดดตรงไปสู่โซลูชันที่ทำงานได้จริงและสามารถคัดลอก‑วางได้ทันที เมื่อจบคุณจะมีรูปแบบที่นำกลับมาใช้ใหม่ได้ ไม่ว่าจะเป็นการสร้างใบแจ้งหนี้, รายการราคา, หรือสเปรดชีตใด ๆ ที่ต้องการส่วนลดแบบไดนามิก

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธีออกแบบเทมเพลตสเปรดชีตที่รองรับส่วนลด
- วิธีกำหนด `VariablePrefix` / `VariableSuffix` แบบกำหนดเองเพื่อให้มาร์กเกอร์ง่ายต่อการมองเห็น
- วิธีส่งอ็อบเจ็กต์ไม่ระบุชื่อ (`discountData`) เข้าไปใน `SmartMarkerProcessor`
- วิธีที่สูตรผลลัพธ์ (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) คำนวณราคาสุดท้ายโดยอัตโนมัติ
- เคล็ดลับการจัดการกรณีขอบเช่นแถวที่ไม่มีส่วนลดหรือระดับส่วนลดหลายระดับ

**Prerequisites** – .NET runtime เวอร์ชันล่าสุด (≥ .NET 6), การอ้างอิงไลบรารี `Aspose.Cells` (หรือไลบรารีที่คล้ายกัน) ที่ให้บริการ `SmartMarkerProcessor`, และความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ C# ไม่ต้องมีอะไรซับซ้อน

---

## ขั้นตอนที่ 1: สร้างเทมเพลตส่วนลดในสเปรดชีตของคุณ

เริ่มต้นโดยเปิดเวิร์กบุ๊กใหม่ (หรือใช้เวิร์กบุ๊กที่มีอยู่) แล้ววางตัวแทนตำแหน่งที่ส่วนลดจะถูกนำไปใช้ คิดว่าเทมเพลตเป็นไฟล์ Excel ธรรมดาที่มี “smart markers” ซึ่งตัวประมวลผลจะทำการแทนที่

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**ทำไมจึงสำคัญ:** การฝัง `#Discount#` ไว้ในสูตรทำให้ตัวประมวลผลรู้ว่าค่าที่เป็นส่วนลดควรอยู่ตำแหน่งไหน `SmartMarkerProcessor` จะเปลี่ยน `#Discount#` ให้เป็นตัวเลขที่คุณระบุในภายหลัง โดยไม่กระทบส่วนอื่นของสูตร

---

## ขั้นตอนที่ 2: กำหนดคำนำหน้าตัวแปรสำหรับ Smart Markers

โดยค่าเริ่มต้นหลายไลบรารีมองหาสัญลักษณ์ `${Variable}` หรือ `{{Variable}}` ในกรณีของเราเราต้องการมาร์กเกอร์ที่อ่านง่ายจึง **กำหนดคำนำหน้าและคำนำหลังของตัวแปร** อย่างชัดเจน

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** การใช้ `#` ทำให้มาร์กเกอร์สั้นและง่ายต่อการมองเห็นในแถบสูตรของ Excel หากต้องการหลีกเลี่ยงการชนกับฟังก์ชันของ Excel ที่มีอยู่แล้ว สามารถเลือกคู่สัญลักษณ์อื่น (เช่น `[[` และ `]]`) ได้

---

## ขั้นตอนที่ 3: ใส่ข้อมูลลงในเทมเพลตด้วย SmartMarkerProcessor

ตอนนี้เราจะป้อนค่าจริงของส่วนลด ตัวประมวลผลจะสแกนเวิร์กชีต ค้นหา `#Discount#` ทุกตำแหน่ง แล้วแทนที่ด้วยค่าจากอ็อบเจ็กต์ไม่ระบุชื่อที่เราส่งเข้าไป

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

หลังจากเรียกใช้โค้ดนี้ สูตรใน `B2` จะกลายเป็น:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

เมื่อเวิร์กบุ๊กคำนวณ `B2` จะแสดง **90** ซึ่งคือราคาที่ลดลง 10 % จากราคาเดิม 100

**ทำไมถึงทำงานได้:** `StartSmartMarkerProcessing` จะเดินผ่านทุกเซลล์ ค้นหาโทเคน `#Discount#` แล้วแทนค่าตัวเลข เนื่องจากโทเคนอยู่ภายในเงื่อนไข `IF` ทำให้สเปรดชีตยังคงจัดการกรณีที่ส่วนลดเป็นศูนย์ได้อยู่ดี

---

## ขั้นตอนที่ 4: ใช้ส่วนลดในสเปรดชีต – ตรวจสอบผลลัพธ์

ให้ทำการคำนวณและแสดงราคาสุดท้ายบนคอนโซล ขั้นตอนนี้พิสูจน์ว่า workflow **apply discount in spreadsheet** ทำงานสำเร็จ

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**ผลลัพธ์ที่คาดหวัง**

```
Original: 100
Discounted (10%): 90
```

หากคุณเปลี่ยนค่า `discountData.Discount` เป็น `0.25` แล้วรันตัวประมวลผลใหม่ ผลลัพธ์จะอัปเดตเป็นส่วนลด 25 % โดยไม่ต้องแก้โค้ดเพิ่มเติม

---

## ขั้นตอนที่ 5: จัดการกรณีขอบและส่วนลดหลายระดับ

### แถวที่ไม่มีส่วนลด

บางครั้งสินค้าจะไม่มีการลดราคา เพื่อให้สูตรแข็งแรง `IF` ที่คุณใส่ไว้ก่อนหน้านี้ครอบคลุมสถานการณ์นี้แล้ว: เมื่อ `#Discount#` เป็น `0` ราคาต้นฉบับจะผ่านไปโดยไม่เปลี่ยนแปลง

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### คอลัมน์ส่วนลดหลายคอลัมน์

หากต้องการส่วนลดแยกตามแถว ให้กำหนดมาร์กเกอร์เฉพาะแต่ละแถว เช่น `#Discount1#`, `#Discount2#` แล้วส่งคอลเลกชัน:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

ตัวประมวลผลจะจับคู่มาร์กเกอร์ตามลำดับ ดังนั้นแต่ละแถวจะได้รับค่าที่ถูกต้อง

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอกและใช้งานครบทุกขั้นตอน บันทึกเป็น `Program.cs` เพิ่มการอ้างอิงไปยัง `Aspose.Cells` แล้วรัน

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

เมื่อรันโปรแกรมจะพิมพ์ตัวเลขที่คาดหวังและสร้างไฟล์ `DiscountedPricing.xlsx` ที่คุณสามารถเปิดใน Excel เพื่อดูสูตรที่ถูกคำนวณแล้ว

---

## สรุป

คุณได้เรียนรู้วิธี **สร้างเทมเพลตส่วนลด**, **ใช้ส่วนลดในสเปรดชีต**, **ใส่ข้อมูลลงในเทมเพลต**, และ **กำหนดคำนำหน้าตัวแปร** สำหรับ smart markers ทั้งหมดด้วยไม่กี่บรรทัดของ C# โค้ด รูปแบบนี้สามารถขยายได้ง่าย—เพียงเปลี่ยนอ็อบเจ็กต์ไม่ระบุชื่อหรือส่งคอลเลกชันสำหรับการอัปเดตเป็นกลุ่มเดียวกัน เทมเพลตเดียวก็จะจัดการกับทุกสถานการณ์ส่วนลดที่คุณต้องการ

พร้อมก้าวต่อไปหรือยัง? ลองทำ:

- เพิ่มการคำนวณภาษีควบคู่กับส่วนลด
- ดึงเปอร์เซ็นต์ส่วนลดจากฐานข้อมูลแทนการกำหนดค่าคงที่
- ใช้ conditional formatting เพื่อไฮไลท์แถวที่มีส่วนลดสูง

การขยายเหล่านี้ยังคงรักษาแนวคิดหลักไว้ในขณะที่เพิ่มประโยชน์ให้กับเทมเพลตส่วนลดของคุณ

มีคำถามหรือกรณีการใช้งานที่น่าสนใจ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}