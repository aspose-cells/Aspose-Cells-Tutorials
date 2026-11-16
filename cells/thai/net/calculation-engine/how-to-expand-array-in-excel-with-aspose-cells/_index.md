---
category: general
date: 2026-11-16
description: เรียนรู้วิธีขยายอาร์เรย์ใน Excel ด้วย Aspose.Cells, ฟังก์ชันอาร์เรย์แบบไดนามิก,
  และ lambda reducer แล้วเขียนไฟล์ Excel ด้วย C#
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: th
lastmod: 2026-11-16
og_description: วิธีขยายอาร์เรย์ใน Excel ด้วย Aspose.Cells, ฟังก์ชันอาร์เรย์แบบไดนามิก,
  และ lambda reducer. ติดตามตัวอย่าง C# ฉบับสมบูรณ์เพื่อเขียนไฟล์ Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: วิธีขยายอาร์เรย์ใน Excel ด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีขยายอาร์เรย์ใน Excel ด้วย Aspose.Cells
url: /th/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีขยายอาร์เรย์ใน Excel ด้วย Aspose.Cells

หากคุณต้องการ **วิธีขยายอาร์เรย์** ในแผ่นงาน Excel จาก C# tutorial นี้จะแสดงขั้นตอนที่แน่นอน คุณจะสร้างเวิร์กบุ๊ก Excel ใช้ฟังก์ชันอาร์เรย์แบบไดนามิกเช่น `EXPAND` และ `REDUCE` ใช้ **lambda** accumulator และสุดท้าย **เขียนไฟล์ Excel** ไปยังดิสก์ วิธีนี้ทำงานกับ Aspose.Cells 23.10 หรือใหม่กว่าและไม่ต้องติดตั้ง Excel ด้วยตนเอง

เมื่ออ่านจบคุณจะได้ไฟล์ `ExpandReduceDemo.xlsx` ที่ทำงานเต็มรูปแบบซึ่งแสดงพลังของสูตรอาร์เรย์แบบไดนามิกในบริบทโปรแกรม

## สิ่งที่คุณต้องมี

- .NET 6.0 (หรือเวอร์ชัน .NET ใด ๆ ที่รองรับโดย Aspose.Cells)
- แพคเกจ Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)
- โปรแกรมแก้ไขโค้ดหรือ IDE (Visual Studio, VS Code, Rider ฯลฯ)

ไม่ต้องการ COM interop หรือการติดตั้ง Office เพิ่มเติม เพราะ Aspose.Cells จัดการรูปแบบไฟล์ภายในเอง

## ขั้นตอนที่ 1: สร้าง Excel workbook

งานแรกคือ **สร้าง excel workbook** ในหน่วยความจำ Aspose.Cells มีคลาส `Workbook` ซึ่งเป็นตัวแทนของไฟล์ XLSX ทั้งไฟล์

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **ทำไมถึงสำคัญ:** การสร้างอินสแตนซ์ของ `Workbook` จะให้แคนวาสที่สะอาด พื้นฐานแผ่นงานถูกเตรียมไว้แล้ว ดังนั้นคุณไม่จำเป็นต้องเพิ่มแผ่นงานใหม่ด้วยตนเอง เว้นแต่ต้องการหลายชีต

## ขั้นตอนที่ 2: แทรกคอนสแตนท์อาร์เรย์แนวตั้ง

เอนจินอาร์เรย์แบบไดนามิกของ Excel สามารถทำงานกับคอนสแตนท์อาร์เรย์แบบลิเทรัล เราจะใส่อาร์เรย์แนวตั้ง `{1;2;3;4;5}` ลงในเซลล์ **A1**

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **เคล็ดลับ:** เครื่องหมายเซมิโคลอน (`;`) ใช้แยกแถวในคอนสแตนท์ ส่วนคอมม่า (`,`) จะใช้แยกคอลัมน์ ซึ่งสอดคล้องกับไวยากรณ์ของ Excel

## ขั้นตอนที่ 3: ขยายอาร์เรย์เป็นเมทริกซ์

ต่อไปเราตอบคำถามหลัก – **วิธีขยายอาร์เรย์** – ด้วยฟังก์ชัน `EXPAND` สูตรนี้จะขยายอาร์เรย์คอลัมน์เดียวให้เป็นเมทริกซ์ 5 แถว × 2 คอลัมน์ เริ่มที่ **B1**

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **ทำไมต้องใช้ EXPAND?** `EXPAND(source, rows, cols)` บังคับให้ช่วงต้นทางครอบคลุมขนาดที่กำหนด หากจำเป็นจะเติมช่องว่างเป็นค่าเริ่มต้น เป็นวิธีที่อ่านง่ายที่สุดในการสร้างเมทริกซ์ขนาดใหญ่จากอาร์เรย์เดียว

## ขั้นตอนที่ 4: ลดเมทริกซ์ด้วย lambda accumulator

ฟังก์ชัน `REDUCE` จะวนลูปผ่านช่วงและรวมค่าโดยใช้ **lambda** expression ที่นี่เราจะบวกค่าของแต่ละคอลัมน์เข้าด้วยกันเป็นคอลัมน์เดียว แล้วใส่ผลลัพธ์ที่ **D1**

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **วิธีใช้ lambda:** `LAMBDA(acc, val, acc+val)` รับค่า accumulator ปัจจุบัน (`acc`) และค่าของเซลล์ถัดไป (`val`) แล้วคืนค่า accumulator ใหม่ ซึ่งทำหน้าที่เป็นการสะสมผลรวมแบบต่อเนื่อง นี้แสดง **วิธีใช้ lambda** ในสูตร Excel จากโค้ด

## ขั้นตอนที่ 5: คำนวณสูตรเพื่อให้ผลลัพธ์ปรากฏ

Aspose.Cells ไม่ได้ประเมินสูตรอัตโนมัติเมื่อคุณตั้งค่า การเรียก `CalculateFormula` จะบังคับให้เอนจินคำนวณสูตรทั้งหมดในเวิร์กบุ๊ก

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **หมายเหตุ:** หากคุณเปิดไฟล์ที่สร้างขึ้นใน Excel ค่าต่าง ๆ จะปรากฏแล้ว เพราะได้ถูกคำนวณล่วงหน้า

## ขั้นตอนที่ 6: เขียนไฟล์ Excel ไปยังดิสก์

สุดท้าย **เขียน excel file** ด้วยเมธอด `Save` เลือกโฟลเดอร์ที่คุณมีสิทธิ์เขียนได้

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **คอลัมน์ B** และ **C** มีเมทริกซ์ 5 × 2 ที่สร้างโดย `EXPAND`
- **เซลล์ D1** แสดงค่า `15` ซึ่งเป็นผลรวมของตัวเลขทั้งหมดที่คำนวณโดยสูตร `REDUCE` + **lambda**

## คำถามที่พบบ่อยและกรณีขอบ

- **ฉันสามารถขยายให้มีคอลัมน์มากกว่าที่แหล่งข้อมูลมีได้หรือไม่?**  
  ใช่ `EXPAND` จะเติมคอลัมน์ที่ขาดหายด้วยเซลล์ว่าง ทั้งแถวก็ทำเช่นเดียวกัน

- **ถ้าอาร์เรย์ต้นทางเป็นแนวนอน (`{1,2,3,4,5}`) จะเป็นอย่างไร?**  
  `EXPAND` จะถือว่าเป็นแถวเดียว คุณยังคงสามารถระบุจำนวนแถวและคอลัมน์เพื่อปรับรูปร่างได้

- **`REDUCE` ทำงานกับข้อมูลที่ไม่ใช่ตัวเลขได้หรือไม่?**  
  Lambda ต้องคืนค่าที่เข้ากันได้กับประเภทของ accumulator สำหรับการต่อข้อความคุณอาจใช้ `LAMBDA(acc, val, acc & val)`

- **ต้องเรียก `CalculateFormula` ทุกครั้งที่มีการเปลี่ยนแปลงหรือไม่?**  
  เรียกเฉพาะเมื่อคุณต้องการค่าที่คำนวณแล้วก่อนบันทึก Excel จะคำนวณใหม่เมื่อเปิดไฟล์หากคุณข้ามขั้นตอนนี้

## เคล็ดลับระดับมืออาชีพ

- **ประสิทธิภาพ:** สำหรับเวิร์กบุ๊กขนาดใหญ่ให้เรียก `workbook.CalculateFormula` ครั้งเดียวหลังตั้งสูตรทั้งหมดเสร็จ ไม่ต้องเรียกหลังแต่ละเซลล์
- **ความปลอดภัยของเวอร์ชัน:** `EXPAND` และ `REDUCE` มีใน Excel 365 และใหม่กว่า Aspose.Cells รองรับฟังก์ชันเหล่านี้โดยไม่คำนึงถึงเวอร์ชัน Excel เป้าหมาย เพราะเครื่องมือคำนวณเป็นของในตัว
- **ดีบักสูตร:** ใช้ `sheet.Cells["B1"].Formula` เพื่ออ่านสตริงสูตรที่ตั้งไว้ ช่วยเมื่อต้องสร้างสูตรแบบไดนามิก

## สรุป

ตอนนี้คุณรู้ **วิธีขยายอาร์เรย์** ใน Excel ด้วย Aspose.Cells ใช้ **ฟังก์ชันอาร์เรย์แบบไดนามิก** ประยุกต์ **lambda** กับ `REDUCE` และ **เขียน excel file** จาก C# ตัวอย่างครบวงจรนี้สามารถปรับใช้กับการแปลงข้อมูลที่ซับซ้อนยิ่งขึ้น เช่น การสลับเมทริกซ์, ผลรวมสะสม, หรือการรวมข้อมูลแบบกำหนดเอง

---

*ขั้นตอนต่อไป:*  
- สำรวจฟังก์ชันไดนามิกอื่น ๆ เช่น `FILTER`, `SORT` และ `UNIQUE`  
- รวมหลาย `LAMBDA` เพื่อสร้างฟังก์ชันผู้ใช้ที่กำหนดเองได้  
- นำการสร้างเวิร์กบุ๊กเข้ากับ ASP.NET Core API เพื่อสร้างรายงานแบบเรียลไทม์

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}