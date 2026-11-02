---
category: general
date: 2026-04-07
description: สร้างไฟล์ Excel, ทำให้ข้อความในคอลัมน์ห่ออัตโนมัติ, คำนวณสูตร, และบันทึกไฟล์เป็น
  XLSX พร้อมโค้ด C# ทีละขั้นตอน.
draft: false
keywords:
- create excel workbook
- wrap columns in excel
- save workbook as xlsx
- how to calculate formulas
- how to save excel
language: th
og_description: สร้างไฟล์ Excel, ทำให้คอลัมน์ห่อหุ้มใน Excel, คำนวณสูตร, และบันทึกไฟล์เป็น
  XLSX. เรียนรู้กระบวนการทั้งหมดพร้อมโค้ดที่สามารถรันได้.
og_title: สร้างสมุดงาน Excel – คู่มือ C# ฉบับสมบูรณ์
tags:
- csharp
- aspnet
- excel
- automation
title: สร้างเวิร์กบุ๊ก Excel – ห่อคอลัมน์และบันทึกเป็น XLSX
url: /th/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook – พับคอลัมน์และบันทึกเป็น XLSX

เคยต้อง **สร้าง Excel workbook** ด้วยโปรแกรมและสงสัยว่าจะทำให้ข้อมูลจัดเรียงอย่างสวยงามในรูปแบบหลายคอลัมน์ได้อย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในบทเรียนนี้เราจะพาคุณผ่านขั้นตอนการสร้าง workbook, ใช้สูตร `WRAPCOLS` เพื่อ **พับคอลัมน์ใน Excel**, บังคับให้เครื่องคำนวณผลลัพธ์, และสุดท้าย **บันทึก workbook เป็น XLSX** เพื่อให้คุณเปิดได้ในโปรแกรมสเปรดชีตใดก็ได้

เรายังจะตอบคำถามที่ตามมาที่หลีกเลี่ยงไม่ได้: *ฉันจะคำนวณสูตรแบบเรียลไทม์ได้อย่างไร?* *ถ้าต้องการเปลี่ยนจำนวนคอลัมน์ล่ะ?* และ *มีวิธีเร็ว ๆ ในการบันทึกไฟล์ไหม?* เมื่อจบคุณจะได้โค้ด C# ที่พร้อมใช้งานซึ่งทำทั้งหมดนี้และเคล็ดลับเพิ่มเติมที่คุณสามารถคัดลอกไปใช้ในโปรเจกต์ของคุณได้

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.6+ ด้วย)
- ไลบรารี **Aspose.Cells** (หรือแพคเกจประมวลผล Excel ใด ๆ ที่รองรับ `WRAPCOLS`; ตัวอย่างใช้ Aspose.Cells เพราะมีเมธอด `CalculateFormula` ที่เรียบง่าย)
- มีประสบการณ์พื้นฐานกับ C# เล็กน้อย – หากคุณเขียน `Console.WriteLine` ได้ก็พร้อมแล้ว

> **Pro tip:** หากคุณยังไม่มีลิขสิทธิ์สำหรับ Aspose.Cells คุณสามารถขอคีย์ทดลองฟรีจากเว็บไซต์ของพวกเขา; เวอร์ชันทดลองทำงานได้อย่างสมบูรณ์สำหรับการเรียนรู้

## ขั้นตอนที่ 1: สร้าง Excel Workbook

สิ่งแรกที่คุณต้องมีคืออ็อบเจกต์ workbook ว่างเปล่าที่เป็นตัวแทนไฟล์ Excel ในหน่วยความจำ นี่คือหัวใจของการ **สร้าง Excel workbook**  

```csharp
using Aspose.Cells;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet – it’s already there by default
Worksheet worksheet = workbook.Worksheets[0];
```

*ทำไมจึงสำคัญ:* คลาส `Workbook` เป็นจุดเริ่มต้นสำหรับการจัดการ Excel ใด ๆ การสร้างมันก่อนจะทำให้คุณมีผ้าใบที่สะอาดสำหรับการกระทำต่อ ๆ ไป—เช่นการพับคอลัมน์—โดยไม่มีผลข้างเคียง

## ขั้นตอนที่ 2: เติมข้อมูลตัวอย่าง (ไม่จำเป็นแต่เป็นประโยชน์)

ก่อนที่เราจะพับคอลัมน์ ให้ใส่ชุดข้อมูลขนาดเล็กลงในช่วง `A1:D10` นี้จำลองสถานการณ์จริงที่คุณมีตารางดิบที่ต้องการปรับรูปแบบใหม่  

```csharp
// Fill A1:D10 with sample numbers for demonstration
for (int row = 0; row < 10; row++)
{
    for (int col = 0; col < 4; col++)
    {
        worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
    }
}
```

คุณสามารถข้ามบล็อกนี้ได้หากมีข้อมูลอยู่แล้วใน worksheet; ลอจิกการพับทำงานกับช่วงใด ๆ ที่มีอยู่

## ขั้นตอนที่ 3: พับคอลัมน์ใน Excel

ตอนนี้มาถึงจุดเด่นของบทเรียน: ฟังก์ชัน `WRAPCOLS` มันรับช่วงต้นทางและจำนวนคอลัมน์ แล้วกระจายข้อมูลไปยังเลย์เอาต์ใหม่ นี่คือตัวอย่างการใช้กับเซลล์ **A1** เพื่อให้ผลลัพธ์ครอบคลุมสามคอลัมน์  

```csharp
// Apply WRAPCOLS to A1 – the result will spill into a 3‑column layout
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";
```

**เกิดอะไรขึ้นเบื้องหลัง?**  
`WRAPCOLS(A1:D10,3)` บอก Excel ให้อ่าน 40 เซลล์ใน `A1:D10` แล้วเขียนลงแถว‑ตาม‑แถวในสามคอลัมน์ โดยสร้างแถวใหม่ตามที่ต้องการโดยอัตโนมัติ เหมาะอย่างยิ่งสำหรับการแปลงรายการยาวให้เป็นมุมมองสไตล์หนังสือพิมพ์ที่กระชับกว่า

## ขั้นตอนที่ 4: วิธีคำนวณสูตร

การตั้งสูตรเป็นเพียงครึ่งหนึ่งของการทำงาน; Excel จะไม่คำนวณผลลัพธ์จนกว่าคุณจะเรียกการคำนวณ ใน Aspose.Cells ทำได้ด้วย `CalculateFormula()`  

```csharp
// Force the workbook to evaluate all pending formulas
workbook.CalculateFormula();
```

> **ทำไมต้องทำเช่นนี้:** หากไม่เรียก `CalculateFormula` เซลล์ `A1` จะเก็บเพียงสตริงสูตรเมื่อเปิดไฟล์ และเลย์เอาต์ที่พับจะไม่ปรากฏจนผู้ใช้ทำการคำนวณใหม่ด้วยตนเอง

## ขั้นตอนที่ 5: บันทึก Workbook เป็น XLSX

สุดท้าย ให้บันทึก workbook ลงดิสก์ เมธอด `Save` จะสังเกตฟอร์แมตจากส่วนขยายไฟล์โดยอัตโนมัติ ดังนั้นการใช้ **.xlsx** จะทำให้ได้ฟอร์แมต Open XML สมัยใหม่  

```csharp
// Choose a folder you have write access to and save the file
string outputPath = @"C:\Temp\output.xlsx";
workbook.Save(outputPath);
```

เมื่อคุณเปิด `output.xlsx` ใน Excel คุณจะเห็นข้อมูลเดิมถูกพับอย่างเป็นระเบียบเป็นสามคอลัมน์ เริ่มที่เซลล์ **A1** ส่วนที่เหลือของชีตจะไม่ถูกแก้ไข ซึ่งเป็นประโยชน์หากคุณต้องการเก็บตารางต้นฉบับไว้เป็นอ้างอิง

### ภาพผลลัพธ์ที่คาดหวัง

<img src="images/wrapcols-result.png" alt="create excel workbook example" />

ภาพด้านบนแสดงเลย์เอาต์สุดท้าย: ตัวเลขจาก `A1:D10` ตอนนี้แสดงในสามคอลัมน์ โดยมีแถวที่สร้างขึ้นอัตโนมัติเพื่อรองรับค่าทั้งหมด

## ความแปรผันทั่วไปและกรณีขอบ

### การเปลี่ยนจำนวนคอลัมน์

หากต้องการจำนวนคอลัมน์ที่ต่างออกไป เพียงปรับอาร์กิวเมนต์ที่สองของ `WRAPCOLS`  

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,5)"; // five‑column layout
```

อย่าลืมเรียก `CalculateFormula()` อีกครั้งหลังจากเปลี่ยนค่าใด ๆ

### การพับช่วงที่ไม่ต่อเนื่อง

`WRAPCOLS` ทำงานได้เฉพาะกับช่วงต่อเนื่อง หากข้อมูลต้นทางของคุณกระจายอยู่หลายพื้นที่ ให้รวมข้อมูลก่อน (เช่น ใช้ `UNION` ในคอลัมน์ช่วยเหลือ) แล้วจึงพับ

### ชุดข้อมูลขนาดใหญ่

สำหรับตารางขนาดใหญ่มาก การคำนวณอาจใช้เวลาสักครู่ คุณสามารถเพิ่มประสิทธิภาพได้โดยปิดการคำนวณอัตโนมัติก่อนตั้งสูตรและเปิดใหม่หลังจากนั้น  

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D1000,4)";
workbook.CalculateFormula();
workbook.Settings.CalcMode = CalcMode.Automatic;
```

### การบันทึกลง Stream

หากคุณกำลังสร้างเว็บ API และต้องการส่งไฟล์ตรงให้ลูกค้า สามารถเขียนลง `MemoryStream` แทนการบันทึกไฟล์จริงได้  

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // reset for reading
// return ms as a FileResult in ASP.NET Core, for example
```

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่พร้อมคัดลอก‑วางใช้งานได้ทันที  

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Fill A1:D10 with sample data (optional)
        for (int row = 0; row < 10; row++)
        {
            for (int col = 0; col < 4; col++)
            {
                worksheet.Cells[row, col].PutValue(row * 4 + col + 1);
            }
        }

        // 3️⃣ Apply WRAPCOLS to produce a 3‑column layout
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A1:D10,3)";

        // 4️⃣ Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // 5️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

รันโปรแกรมนี้ เปิด `output.xlsx` ที่สร้างขึ้น และคุณจะเห็นข้อมูลถูกพับตามที่อธิบายไว้

## สรุป

คุณได้เรียนรู้ **วิธีสร้าง Excel workbook** ด้วย C#, ใช้ฟังก์ชัน `WRAPCOLS` ที่ทรงพลังเพื่อ **พับคอลัมน์ใน Excel**, **คำนวณสูตร** ตามต้องการ, และ **บันทึก workbook เป็น XLSX** เพื่อใช้งานต่อไป กระบวนการแบบปลายถึงปลายนี้ครอบคลุมสถานการณ์ที่พบบ่อยที่สุด ตั้งแต่การสาธิตง่าย ๆ จนถึงการทำอัตโนมัติระดับผลิตภัณฑ์

### ขั้นตอนต่อไปคืออะไร?

- ทดลองใช้ฟังก์ชันอาเรย์ไดนามิกอื่น ๆ เช่น `FILTER`, `SORT`, หรือ `UNIQUE`
- ผสาน `WRAPCOLS` กับการจัดรูปแบบตามเงื่อนไขเพื่อไฮไลต์แถวเฉพาะ
- ผสานตรรกะนี้เข้าไปใน endpoint ของ ASP.NET Core เพื่อให้ผู้ใช้ดาวน์โหลดรายงานที่ปรับแต่งได้ด้วยคลิกเดียว

ปรับจำนวนคอลัมน์, ช่วงต้นทาง, หรือเส้นทางการบันทึกให้ตรงกับความต้องการของโปรเจกต์ของคุณ หากเจอปัญหาใด ๆ แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}