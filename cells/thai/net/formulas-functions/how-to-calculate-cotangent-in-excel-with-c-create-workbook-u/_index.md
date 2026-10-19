---
category: general
date: 2026-05-04
description: วิธีคำนวณโคแทนเจนต์ขณะสร้างเวิร์กบุ๊ก Excel ด้วย C# เรียนรู้การใช้ฟังก์ชัน
  EXPAND, การบันทึกเวิร์กบุ๊ก, และการทำงานอัตโนมัติของการคำนวณ
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: th
og_description: วิธีคำนวณโคแทนเจนต์ใน Excel ด้วย C# บทเรียนนี้แสดงวิธีสร้างเวิร์กบุ๊ก
  Excel, ใช้ EXPAND, และบันทึกไฟล์
og_title: วิธีคำนวณโคแทนเจนต์ใน Excel – คู่มือฉบับเต็มสำหรับ C# Workbook
tags:
- C#
- Aspose.Cells
- Excel Automation
title: วิธีคำนวณโคแทนเจนต์ใน Excel ด้วย C# – สร้างเวิร์กบุ๊ก, ใช้ EXPAND, และบันทึก
url: /th/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคำนวณ Cotangent ใน Excel ด้วย C# – คู่มือเต็ม

เคยสงสัย **วิธีคำนวณ cotangent** โดยตรงในไฟล์ Excel ที่สร้างด้วย C# ไหม? บางทีคุณอาจกำลังสร้างโมเดลการเงิน รายงานวิทยาศาสตร์ หรือแค่ทำงานอัตโนมัติบนสเปรดชีตที่น่าเบื่อ ข่าวดีคือคุณทำได้ด้วยไม่กี่บรรทัดโค้ด—ไม่ต้องพิมพ์สูตรด้วยมือ ไม่ต้องคัดลอก‑วางแบบซับซ้อน

ในบทเรียนนี้เราจะพาคุณผ่านการสร้างเวิร์กบุ๊ก Excel, การขยายอาร์เรย์ด้วยฟังก์ชัน **EXPAND**, การใส่สูตร **COT** เพื่อคำนวณ cotangent ของ 45°, และสุดท้ายการบันทึกไฟล์เพื่อให้คุณเปิดใน Excel และดูผลลัพธ์ พร้อมกับการอธิบาย **วิธีใช้ expand**, **วิธีบันทึก workbook**, และเคล็ดลับเล็ก ๆ ที่มักถูกมองข้าม

> **คำตอบสั้น:** ใช้ Aspose.Cells (หรือ Microsoft Interop) เพื่อสร้างเวิร์กบุ๊ก, ตั้งค่า `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`, ตั้งค่า `ws.Cells["B1"].Formula = "=COT(PI()/4)"`, แล้วเรียก `workbook.Save("output.xlsx")`.

---

## สิ่งที่คุณต้องมี

- **.NET 6+** (หรือ .NET runtime เวอร์ชันล่าสุดใดก็ได้)  
- **Aspose.Cells for .NET** (รุ่นทดลองฟรีหรือเวอร์ชันที่มีลิขสิทธิ์)  
- ความเข้าใจพื้นฐานของไวยากรณ์ C#  
- Visual Studio, Rider, หรือโปรแกรมแก้ไขที่คุณชอบ

ไม่ต้องติดตั้ง Excel add‑ins เพิ่มเติม; ทุกอย่างทำงานบนเซิร์ฟเวอร์และไฟล์ที่ได้ทำงานได้กับ Excel เวอร์ชันล่าสุดทุกเวอร์ชัน

---

## ขั้นตอนที่ 1: สร้าง Excel Workbook จาก C#  

การสร้าง workbook เป็นพื้นฐาน คิดว่าเป็นการเปิดสมุดโน้ตใหม่ก่อนเริ่มเขียน

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**ทำไมจึงสำคัญ:**  
`Workbook` แทนทั้งแพ็กเกจ `.xlsx`. โดยค่าเริ่มต้นมันมีชีตเดียว ซึ่งเราจะเข้าถึงผ่าน `Worksheets[0]`. หากต้องการเพิ่มชีตในภายหลัง สามารถใช้ `workbook.Worksheets.Add()` ได้

> **Pro tip:** หากคุณกำลังทำงานกับ .NET Core, ตรวจสอบให้แน่ใจว่าแพ็กเกจ NuGet ของ Aspose.Cells ตรงกับ runtime ของคุณ เพื่อหลีกเลี่ยงการขาด dependency ที่เป็น native

---

## ขั้นตอนที่ 2: ใช้ฟังก์ชัน EXPAND เพื่อเติมคอลัมน์  

ฟังก์ชัน **EXPAND** คือวิธีของ Excel ที่เปลี่ยนอาร์เรย์คงที่ให้เป็นช่วงข้อมูลแบบไดนามิก เหมาะเมื่อคุณต้องการสร้างคอลัมน์ของค่าโดยไม่ต้องกำหนดค่าตัวเซลล์ทีละค่า

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### วิธีทำงาน  

- `{1,2,3}` คืออาร์เรย์ต้นทาง (สามตัวเลข)  
- `5` บอก Excel ให้สร้าง **5 แถว**  
- `1` บอก Excel ให้สร้าง **1 คอลัมน์**  

เมื่อคุณเปิดไฟล์ที่บันทึกไว้ เซลล์ A1 ถึง A5 จะมีค่า `1, 2, 3, 0, 0` (แถวที่เหลือเติมด้วยศูนย์)

**กรณีขอบ:** หากอาร์กิวเมนต์ `rows` มีค่าน้อยกว่าความยาวของอาร์เรย์ต้นทาง Excel จะตัดอาร์เรย์ลง ดังนั้น `=EXPAND({1,2,3},2,1)` จะเห็นแค่ `1` และ `2` เท่านั้น

---

## ขั้นตอนที่ 3: ใส่สูตร COT เพื่อคำนวณ Cotangent  

ตอนนี้มาถึงจุดสำคัญ: **วิธีคำนวณ cotangent** ใน Excel. ฟังก์ชัน `COT` ต้องการมุมเป็นเรเดียน เราจึงใส่ `PI()/4` (เท่ากับ 45°)

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### ทำไมต้องใช้ COT แทน Tan?  

Cotangent คือค่าตรงข้ามของ tangent (`cot = 1 / tan`). แม้คุณจะเขียน `=1/TAN(PI()/4)` ได้, การใช้ `COT` จะทำให้สูตรดูสะอาดและหลีกเลี่ยงข้อผิดพลาดหารด้วยศูนย์เมื่อมุมเป็น 0° หรือ 180°

**ผลลัพธ์ที่คาดหวัง:** เปิด `output.xlsx` จะเห็นค่า `1` ใน B1, เพราะ cotangent ของ 45° (π/4 เรเดียน) เท่ากับ 1

**ต้องการใช้หน่วยเป็นองศา?**  
ฟังก์ชันตรีโกณมิติของ Excel ทำงานในเรเดียน แปลงจากองศาด้วย `RADIANS(deg)`. ตัวอย่าง: `=COT(RADIANS(60))`

---

## ขั้นตอนที่ 4: บันทึก Workbook เพื่อดูผลลัพธ์  

การบันทึกเป็นขั้นตอนสุดท้ายของปริศนา คุณสามารถบันทึกไปยังโฟลเดอร์ใดก็ได้ที่คุณมีสิทธิ์เขียน

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### วิธีบันทึกในรูปแบบต่าง ๆ  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

หากต้องการสตรีมไฟล์ (เช่น สำหรับ Web API) ให้ใช้ `workbook.Save(stream, SaveFormat.Xlsx)` แทน

---

## ตัวอย่างทำงานเต็มรูปแบบ  

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือโปรแกรมแบบ self‑contained ที่คุณสามารถคัดลอก‑วางลงใน console app ได้

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**การตรวจสอบผลลัพธ์:**  
- เปิด `output.xlsx`  
- คอลัมน์ A ควรแสดง `1, 2, 3, 0, 0`  
- เซลล์ B1 ควรแสดง `1`  

หากคุณเห็นค่าดังกล่าว คุณได้เรียนรู้ **วิธีคำนวณ cotangent** ด้วยโปรแกรมและ **วิธีสร้าง excel workbook**, **ใช้ฟังก์ชัน expand**, และ **บันทึก workbook** — ทั้งหมดในขั้นตอนเดียว

---

## คำถามที่พบบ่อย & จุดที่ต้องระวัง  

### `COT` ทำงานใน Excel เวอร์ชันเก่าได้หรือไม่?  
ใช่, `COT` มีตั้งแต่ Excel 2007. หากคุณต้องการรองรับ Excel 2003 (`.xls`) จะต้องเปลี่ยนเป็น `1/TAN(...)` เพราะ `COT` ไม่มีในเวอร์ชันนั้น

### ถ้าสูตรไม่คำนวณอัตโนมัติ?  
Aspose.Cells ประเมินสูตรแบบ lazy. เรียก `workbook.CalculateFormula()` ก่อนบันทึกหากต้องการให้ค่าที่คำนวณแล้วถูกบันทึกในไฟล์

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### สามารถเขียนผลลัพธ์โดยตรงโดยไม่ใช้สูตรได้หรือไม่?  
ได้, คุณสามารถคำนวณค่าใน C# (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) แล้วกำหนดให้ `ws.Cells["B1"].Value = result;`. บทเรียนนี้เน้นสูตร Excel เพราะสูตรจะทำให้สเปรดชีตยังคงเป็นไดนามิก—เปลี่ยนมุมภายหลังจะอัปเดตอัตโนมัติ

---

## เคล็ดลับระดับ Pro สำหรับโครงการจริง  

- **การทำงานเป็นชุด:** หากต้องเติมหลายพันแถว ให้ปิดการคำนวณ (`workbook.Settings.CalculateFormulaOnOpen = false`) ขณะเขียน แล้วเปิดใหม่หลังเสร็จ  
- **ตั้งชื่อช่วง:** ใช้ `ws.Cells.CreateRange("MyArray", "A1:A5")` แล้วอ้างอิงชื่อในสูตรเพื่อให้สเปรดชีตอ่านง่ายขึ้น  
- **การจัดการข้อผิดพลาด:** ห่อ `workbook.Save` ด้วย try/catch เพื่อจับปัญหาการอนุญาต (`UnauthorizedAccessException`)

---

## สรุป  

เราได้ครอบคลุม **วิธีคำนวณ cotangent** ในชีต Excel ที่สร้างด้วย C#, แสดง **วิธีใช้ expand** เพื่อเติมคอลัมน์, และอธิบาย **วิธีบันทึก workbook** เพื่อให้คุณตรวจสอบได้ทันที ตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบข้างต้นให้พื้นฐานที่มั่นคงสำหรับการอัตโนมัติสเปรดชีตที่ผสมข้อมูลคงที่กับการคำนวณตรีโกณมิติ

ขั้นตอนต่อไป? ลองเปลี่ยนมุมในสูตร `COT` ให้อ้างอิงเซลล์ (`=COT(PI()*A1/180)`) เพื่อให้ผู้ใช้ป้อนค่าองศา หรือสำรวจฟังก์ชันคณิตศาสตร์อื่น ๆ เช่น `SIN`, `COS`, และ `ATAN2`—ทั้งหมดทำงานเช่นเดียวกันใน workbook ที่สร้างอัตโนมัติ

ขอให้เขียนโค้ดสนุกและสเปรดชีตของคุณปราศจากข้อผิดพลาด! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}