---
category: general
date: 2026-10-01
description: สร้างเวิร์กบุ๊ก Excel ด้วย C# อย่างรวดเร็ว, เรียนรู้วิธีตั้งสูตร, คำนวณโคแทนเจนต์,
  และใช้ฟังก์ชัน PI ใน Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: th
lastmod: 2026-10-01
og_description: สร้างเวิร์กบุ๊ก Excel ด้วย C# และ Aspose.Cells. เรียนรู้วิธีตั้งสูตร,
  ใช้ฟังก์ชัน PI, และคำนวณคอตานเจนต์ในไม่กี่ขั้นตอน.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: สร้างไฟล์ Excel ด้วย C# – ตั้งสูตรและคำนวณ cot
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีสร้างเวิร์กบุ๊ก Excel ด้วย C# และกำหนดสูตร
url: /th/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Excel workbook ใน C# และตั้งสูตร

หากคุณต้องการ **create Excel workbook C#** code ที่เขียนสูตรลงในเซลล์ คู่มือนี้จะแสดงให้คุณเห็นอย่างละเอียด คุณจะได้เห็นวิธีตั้งสูตรใน worksheet, ใช้ฟังก์ชัน PI ที่มีในตัว, และคำนวณ cotangent ของมุม—ทั้งหมดด้วย Aspose.Cells

บทเรียนนี้ครอบคลุมทุกอย่างตั้งแต่การเริ่มต้น workbook ไปจนถึงการดึงผลลัพธ์ที่คำนวณแล้ว เพื่อให้คุณสามารถคัดลอกตัวอย่างเต็มรูปแบบไปใช้ในโปรเจกต์ของคุณได้โดยไม่มีส่วนใดหายไป

## สิ่งที่ต้องเตรียม

* .NET 6.0 หรือเวอร์ชันใหม่กว่า ที่ติดตั้งแล้ว  
* ใบอนุญาต Aspose.Cells ที่ถูกต้อง (หรือคีย์ประเมินผลชั่วคราว)  
* Visual Studio 2022 หรือ IDE C# ใด ๆ ที่คุณชอบ  

ไม่จำเป็นต้องติดตั้งแพคเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Cells`

## สร้าง Excel workbook ใน C#

ขั้นตอนแรกคือการสร้างอ็อบเจ็กต์ `Workbook` ใหม่ ซึ่งอ็อบเจ็กต์นี้แทนไฟล์ Excel ทั้งไฟล์ในหน่วยความจำและให้คุณเข้าถึง worksheet ต่าง ๆ ได้

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

การสร้าง workbook ด้วยวิธีนี้ทำให้ไฟล์พร้อมสำหรับการจัดการต่อไป ไม่ว่าจะเป็นการเพิ่มข้อมูล, การจัดรูปแบบเซลล์, หรือการเขียนสูตร

## ตั้งสูตรในเซลล์โดยใช้ฟังก์ชัน PI

ตอนนี้คุณจะ **write formula to cell** A1 สูตรนี้ใช้ฟังก์ชัน `PI()` เพื่อให้ค่าคงที่ π และฟังก์ชัน `COT` เพื่อคำนวณ cotangent ของมัน

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*ทำไมเรื่องนี้สำคัญ*: `PI()` เป็นฟังก์ชันใน Excel ที่ให้ค่าของ π โดยการหารด้วย 4 จะได้ 45° และ `COT` จะคืนค่า cotangent ของมุมนั้น นี่เป็นการสาธิต **how to use pi function** ภายในสูตร Excel จาก C#

## วิธีคำนวณ cot ด้วย Aspose.Cells

หากคุณสงสัย **how to calculate cot** โดยไม่ต้องแปลงมุมด้วยตนเอง ฟังก์ชัน `COT` จะทำหน้าที่หนักนี้ให้เอง มันรับค่ามุมเป็นเรเดียน ดังนั้นคุณสามารถผสานกับ `PI()` เพื่อคำนวณมุมทั่วไปได้

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

เมื่อรันโปรแกรมจะพิมพ์ผลลัพธ์:

```
Cotangent of PI/4 = 1
```

เพราะ `COT(π/4)` มีค่าเท่ากับ 1 จึงยืนยันว่าการ **set formula in cell** ทำงานถูกต้องและได้รับการประเมินผล

## เขียนสูตรลงในเซลล์ – เคล็ดลับเพิ่มเติม

* **Multiple formulas**: คุณสามารถกำหนดสูตรให้กับเซลล์ใดก็ได้โดยใช้คุณสมบัติ `Formula` เดียวกัน เช่น `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`  
* **International settings**: Aspose.Cells เคารพ locale ของ workbook ดังนั้นชื่อฟังก์ชันจะคงเป็นภาษาอังกฤษ (`PI`, `COT`) ไม่ว่าการตั้งค่าภูมิภาคของผู้ใช้จะเป็นอย่างไร  
* **Performance**: หากต้องตั้งสูตรหลายพันสูตร ให้ทำเป็นชุดและเรียก `workbook.Calculate()` ครั้งเดียวที่จบเพื่อหลีกเลี่ยงการคำนวณซ้ำหลายรอบ  

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโครงการคอนโซลได้ รวมถึงคำสั่ง `using` ที่จำเป็นทั้งหมดและแสดงขั้นตอนการทำงานตั้งแต่การสร้าง workbook ไปจนถึงการแสดงผลลัพธ์

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Expected output** เมื่อคุณรันโปรแกรม:

```
Cotangent of PI/4 = 1
```

ไฟล์ `CotExample.xlsx` ที่สร้างขึ้นจะมีสูตรในเซลล์ A1 ทำให้คุณเปิดใน Excel แล้วเห็นผลลัพธ์เดียวกัน

## สรุป

ตอนนี้คุณรู้วิธี **create Excel workbook C#** code ที่เขียนสูตร, ใช้ฟังก์ชัน `PI`, และ **calculates cot** ด้วย Aspose.Cells ตัวอย่างนี้ครอบคลุมวงจรทั้งหมด: การสร้าง workbook, **set formula in cell**, การคำนวณใหม่, และการดึงผลลัพธ์

ขั้นตอนต่อไปที่คุณอาจสนใจ:

* ใช้ **write formula to cell** สำหรับการคำนวณที่ซับซ้อนยิ่งขึ้น เช่น โมเดลการเงิน  
* ใช้ **set formula in cell** ร่วมกับการจัดรูปแบบตามเงื่อนไขเพื่อไฮไลท์ผลลัพธ์  
* ผสาน **how to use pi function** กับแผนภูมิเชิงตรีโกณเพื่อการรายงานทางวิทยาศาสตร์  

อย่ากลัวที่จะทดลองกับมุมต่าง ๆ, ฟังก์ชันต่าง ๆ, และการจัดวาง worksheet การเชี่ยวชาญการจัดการสูตรใน C# จะเปิดประตูสู่การสร้างระบบรายงาน Excel ที่อัตโนมัติเต็มรูปแบบ ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีคำนวณ Cotangent ใน Excel ด้วย C# – สร้าง Workbook, ใช้ EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [วิธีใช้ WRAPCOLS ใน C# – สร้าง Excel Workbook ด้วยฟังก์ชัน Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [วิธีสร้าง Workbook Scoped Named Ranges ใน Excel ด้วย Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}