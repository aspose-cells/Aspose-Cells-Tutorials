---
category: general
date: 2026-02-09
description: วิธีสร้างอาเรย์ใน Excel ด้วย C# อธิบายในไม่กี่นาที – เรียนรู้การสร้างเลขลำดับ,
  ใช้ COT, และบันทึกเวิร์กบุ๊กเป็น XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: th
og_description: วิธีสร้างอาเรย์ใน Excel ด้วย C# จะอธิบายอย่างเป็นขั้นตอน รวมถึงการสร้างลำดับเลข,
  การใช้ COT, และการบันทึกเวิร์กบุ๊กเป็นไฟล์ XLSX.
og_title: วิธีสร้างอาร์เรย์ใน Excel ด้วย C# – คู่มือฉบับสั้น
tags:
- C#
- Excel
- Aspose.Cells
title: วิธีสร้างอาเรย์ใน Excel ด้วย C# – คู่มือแบบขั้นตอน
url: /th/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

-button >}}

Make sure to keep them unchanged.

Now produce final output with all translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างอาร์เรย์ใน Excel ด้วย C# – คู่มือขั้นตอนโดยละเอียด

เคยสงสัย **how to create array** ใน Excel ด้วย C# โดยไม่ต้องใช้เวลาหลายชั่วโมงค้นหาในเอกสารหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อพวกเขาต้องการช่วง spill แบบไดนามิก, ค่าทริโกโนเมตรีอย่างรวดเร็ว, หรือเพียงไฟล์ XLSX ที่สะอาดและบันทึกลงดิสก์ ในบทแนะนำนี้เราจะแก้ปัญหานั้นทันที—โดยสร้างเวิร์กบุ๊กขนาดเล็กที่เขียนสูตรอาร์เรย์ที่ขยายได้, ใส่การคำนวณ cotangent, และบันทึกทุกอย่างเป็นไฟล์ XLSX  

เราจะเพิ่มเคล็ดลับเล็ก ๆ อีกหลายอย่าง: การสร้างเลขลำดับ, การใช้ฟังก์ชัน `COT`, และการทำให้ไฟล์บันทึกลงที่คุณต้องการ สุดท้ายคุณจะได้สแนปช็อตที่นำกลับมาใช้ใหม่ได้ในโครงการ .NET ใดก็ได้ ไม่มีของฟุ่มเฟือย มีแค่โค้ดที่ทำงาน

> **Pro tip:** ตัวอย่างใช้ไลบรารี **Aspose.Cells** ที่เป็นที่นิยม, แต่แนวคิดสามารถนำไปใช้กับแพ็คเกจออโต้เมชัน Excel ตัวอื่น (EPPlus, ClosedXML) ได้โดยมีการเปลี่ยนแปลงเพียงเล็กน้อย.

## สิ่งที่คุณต้องการ

- **.NET 6** หรือใหม่กว่า (โค้ดสามารถคอมไพล์บน .NET Framework 4.7+ ได้เช่นกัน)  
- **Aspose.Cells for .NET** – คุณสามารถดาวน์โหลดได้จาก NuGet (`Install-Package Aspose.Cells`)  
- โปรแกรมแก้ไขข้อความหรือ IDE (Visual Studio, Rider, VS Code…)  
- สิทธิ์การเขียนในโฟลเดอร์ที่ไฟล์ผลลัพธ์จะถูกบันทึก  

เท่านี้—ไม่มีการกำหนดค่าเพิ่มเติม, ไม่มี COM interop, เพียงแค่แอสเซมบลีที่จัดการได้อย่างสะอาด

## ขั้นตอนที่ 1: วิธีสร้างอาร์เรย์ใน Excel – เริ่มต้น Workbook

สิ่งแรกที่ต้องทำเมื่อคุณต้องการ **how to create array** ในแผ่น Excel คือการสร้างอ็อบเจ็กต์ workbook คิดว่า workbook คือผืนผ้าใบเปล่า; worksheet คือที่คุณจะวาดสูตรของคุณ

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

ทำไมต้องใช้ `Workbook()` โดยไม่มีพารามิเตอร์? มันให้คุณได้ workbook ในหน่วยความจำพร้อมแผ่นงานเริ่มต้น ซึ่งเหมาะสำหรับงานที่ต้องทำอย่างรวดเร็วและโปรแกรมเมติก หากคุณต้องการเปิดไฟล์ที่มีอยู่ เพียงส่งพาธไฟล์ไปยังคอนสตรัคเตอร์

## ขั้นตอนที่ 2: สร้างเลขลำดับด้วย EXPAND และ SEQUENCE

ตอนนี้เรามีแผ่นงานแล้ว, มาตอบส่วน **generate sequence numbers** ของปริศนากัน Excel มีฟังก์ชันอาร์เรย์ไดนามิกใหม่ (`SEQUENCE`, `EXPAND`) ที่ให้เราสร้างรายการแนวตั้ง 3 แถวและทำการ spill อัตโนมัติเป็นช่วง 3 × 5

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**เกิดอะไรขึ้นที่นี่?**  
- `SEQUENCE(3,1,1,1)` → สร้างอาร์เรย์แนวตั้ง `{1;2;3}`.  
- `EXPAND(...,5,1)` → ขยายคอลัมน์สามแถวนี้เป็นห้าคอลัมน์, เติมเซลล์ที่เหลือด้วยค่าว่าง.  

เมื่อคุณเปิดไฟล์ `output.xlsx` ที่สร้างขึ้น, คุณจะเห็นบล็อก 3 × 5 เริ่มที่ **A1** โดยคอลัมน์แรกมีค่า 1, 2, 3 และอีกสี่คอลัมน์ที่เหลือเป็นค่าว่าง เทคนิคนี้เป็นแกนหลักของช่วง spill แบบ **how to create array** โดยไม่ต้องเขียนแต่ละเซลล์ด้วยตนเอง

## ขั้นตอนที่ 3: How to use COT – เพิ่มสูตรตรีโกณมิติ

หากคุณสนใจเกี่ยวกับ **how to use cot** ภายในสูตร Excel, ฟังก์ชัน `COT` เป็นวิธีที่สะดวกในการหาคอตังเจนต์ของมุมที่ระบุเป็นเรเดียน ลองคำนวณ `cot(π/4)`, ซึ่งควรให้ค่า **1**

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

สังเกตว่าเราใช้ `PI()` เพื่อรับค่าระดับเรเดียนของ 180°, แล้วหารด้วย 4 เพื่อได้ 45°. Excel ทำการคำนวณหนัก, และเซลล์ **B1** จะแสดง `1` เมื่อเปิดเวิร์กบุ๊ก นี่เป็นการสาธิต **how to use cot** สำหรับการคำนวณวิศวกรรมหรือการเงินอย่างรวดเร็วโดยไม่ต้องนำไลบรารีคณิตศาสตร์แยกมาใช้

## ขั้นตอนที่ 4: Save workbook as XLSX – การบันทึกไฟล์

ความสนุกทั้งหมดของการสร้างอาร์เรย์และใส่สูตรจะสูญเปล่าหากคุณไม่บันทึกไฟล์ลงดิสก์ นี่คือวิธีที่ตรงไปตรงมาที่จะ **save workbook as xlsx** ด้วย Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

ทำไมต้องระบุ `SaveFormat.Xlsx`? เพราะมันรับประกันรูปแบบ OpenXML สมัยใหม่ ซึ่งอ่านได้ทั่วโลก (Excel, LibreOffice, Google Sheets) หากคุณต้องการไฟล์ `.xls` เก่าเพียงเปลี่ยน enum

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรัน คัดลอกและวางลงในโปรเจกต์คอนโซล, รีสโตร์แพ็กเกจ NuGet ของ Aspose.Cells, แล้วกด **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** หลังจากเปิด `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- คอลัมน์ A แสดงตัวเลข 1‑3 ที่สร้างโดย `SEQUENCE`.  
- คอลัมน์ B มีค่า **1** จากสูตร `COT`.  
- คอลัมน์ C‑E เป็นค่าว่าง, แสดงผลของการเติมเต็มโดย `EXPAND`.

## คำถามทั่วไป & กรณีขอบ

### ถ้าฉันต้องการแถวหรือคอลัมน์เพิ่ม?

เพียงปรับอาร์กิวเมนต์ของ `SEQUENCE` และ `EXPAND`.  
- `SEQUENCE(10,2,5,2)` จะให้เมทริกซ์ 10‑row × 2‑column เริ่มที่ 5 และเพิ่มทีละ 2.  
- `EXPAND(...,10,5)` จะเติมผลลัพธ์ให้เป็น 10 คอลัมน์และ 5 แถว.

### ฟังก์ชันนี้ทำงานกับเวอร์ชัน Excel เก่าได้หรือไม่?

ฟังก์ชันอาร์เรย์ไดนามิก (`SEQUENCE`, `EXPAND`) ต้องการ Excel 365 หรือ 2019+ สำหรับไฟล์เก่า คุณสามารถใช้สูตรคลาสสิกหรือเขียนค่าตรงผ่าน `Cells[row, col].PutValue(value)`.

### ฉันสามารถเขียนสูตรในรูปแบบ R1C1 ได้หรือไม่?

Absolutely. Replace `A1` with `Cells[0, 0]` and use `FormulaR1C1` property:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### แล้วตัวคั่นทศนิยมตามวัฒนธรรมล่ะ?

Aspose.Cells เคารพโลคัลของเวิร์กบุ๊ก หากคุณต้องการวัฒนธรรมเฉพาะ ให้ตั้งค่า `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` ก่อนเขียนสูตร

## สรุปภาพรวม

![วิธีสร้างอาร์เรย์ใน Excel ด้วย C#](/images/how-to-create-array-excel-csharp.png "วิธีสร้างอาร์เรย์ใน Excel ด้วย C#")

*ภาพหน้าจอแสดงช่วง spill สุดท้ายและผลลัพธ์ของ cotangent*

## สรุป

นี่แหละ—**how to create array** ใน Excel ด้วย C# ตั้งแต่ต้น, สร้างเลขลำดับ, ใช้ฟังก์ชัน `COT`, และ **save workbook as XLSX** ในโปรแกรมเดียวที่เรียบร้อย ประเด็นสำคัญคือ:

1. ใช้วัตถุ `Workbook` และ `Worksheet` เพื่อเริ่มการออโต้เมชัน Excel ของคุณ.  
2. ใช้ฟังก์ชันอาร์เรย์ไดนามิก (`SEQUENCE`, `EXPAND`) เพื่อสร้างช่วง spill ที่ยืดหยุ่น.  
3. ใส่ฟังก์ชันตรีโกณมิติอย่าง `COT` เพื่อคำนวณอย่างรวดเร็วโดยไม่ต้องใช้ไลบรารีเพิ่มเติม.  
4. บันทึกผลลัพธ์ด้วย `SaveFormat.Xlsx` เพื่อให้ได้ไฟล์ที่อ่านได้ทั่วโลก.

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเปลี่ยน `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}