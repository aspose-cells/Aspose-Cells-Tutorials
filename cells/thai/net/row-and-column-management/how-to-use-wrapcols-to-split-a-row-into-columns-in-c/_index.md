---
category: general
date: 2026-11-16
description: เรียนรู้วิธีใช้ WRAPCOLS ใน C# เพื่อแยกแถวเป็นคอลัมน์, ทำงานอัตโนมัติกับเวิร์กบุ๊ก
  Excel, คำนวณสูตร, และบันทึกไฟล์ Excel
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: th
lastmod: 2026-11-16
og_description: วิธีใช้ WRAPCOLS ใน C# เพื่อแยกแถวเป็นคอลัมน์, ทำงานอัตโนมัติในเวิร์กบุ๊ก
  Excel, รันการคำนวณสูตร, และบันทึกไฟล์ Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: วิธีใช้ WRAPCOLS ใน C# – แบ่งแถว, คำนวณสูตร, และบันทึกไฟล์ Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: วิธีใช้ WRAPCOLS เพื่อแยกแถวเป็นคอลัมน์ใน C#
url: /th/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ WRAPCOLS เพื่อแยกแถวเป็นคอลัมน์ใน C#

หากคุณต้องการ **how to use WRAPCOLS** ในโครงการ C# นี้ คู่มือนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และสามารถรันได้ คุณจะได้เห็นวิธีแยกแถวเป็นคอลัมน์, ทำงานอัตโนมัติกับ Excel workbook, เรียกการคำนวณสูตร Excel, และสุดท้ายบันทึกไฟล์ Excel แบบ C#

การทำงานกับ Excel อย่างโปรแกรมมักหมายถึงการจัดการชุดข้อมูลขนาดใหญ่ และฟังก์ชัน `WRAPCOLS` ช่วยให้คุณปรับรูปแบบแถวเดียวเป็นเมทริกซ์โดยไม่ต้องวนลูปด้วยตนเอง ขั้นตอนต่อไปนี้ครอบคลุมทุกสิ่งที่คุณต้องการ—ตั้งแต่การสร้าง workbook จนถึงการส่งออกไฟล์ขั้นสุดท้าย—เพื่อให้คุณสามารถรวมเทคนิคนี้เข้าไปในแอปพลิเคชัน .NET ใดก็ได้

## สิ่งที่บทเรียนนี้ครอบคลุม

* สร้าง workbook ใหม่และเข้าถึง worksheet แรก.  
* เติมข้อมูลในแถวด้วยค่าต่อเนื่อง (1‑20).  
* ใช้สูตร Excel `WRAPCOLS` เพื่อแยกแถวเป็นบล็อก 5 คอลัมน์.  
* เรียก **excel formula calculation** เพื่อให้ผลลัพธ์เป็นส่วนหนึ่งของแผ่นงาน.  
* ใช้ **save excel file c#** เพื่อบันทึก workbook ไปยังดิสก์.  

ไม่จำเป็นต้องตั้งค่าภายนอกใด ๆ นอกจากไลบรารี Aspose.Cells สำหรับ .NET (หรือ API ที่เข้ากันได้ใด ๆ ที่สนับสนุน `WRAPCOLS`). เมื่อจบบทเรียนคุณจะได้ไฟล์ชื่อ `WrapColsDemo.xlsx` ที่มีสี่แถวแต่ละแถวมีห้าคอลัมน์ ซึ่งได้มาจากข้อมูลแถวเดียวเดิม

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Core 3.1 และ .NET Framework 4.7+).  
* อ้างอิงถึง **Aspose.Cells** (สามารถติดตั้งได้ผ่าน NuGet: `Install-Package Aspose.Cells`).  
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# และสูตร Excel.  

> **Pro tip:** หากคุณต้องการทางเลือกฟรี ไลบรารีโอเพนซอร์ส EPPlus ก็สนับสนุนสูตรแบบกำหนดเองเช่นกัน แต่ `WRAPCOLS` มีอยู่ในตัวเฉพาะในไลบรารีที่ทำงานเต็มรูปแบบของเอนจินการคำนวณ Excel เช่น Aspose.Cells.

## ขั้นตอนที่ 1: สร้าง workbook ใหม่และดึง worksheet แรก

การดำเนินการแรกคือการสร้างอ็อบเจ็กต์ `Workbook` และดึง worksheet เริ่มต้นของมัน อ็อบเจ็กต์นี้เป็นตัวแทนของไฟล์ Excel ทั้งหมดในหน่วยความจำ

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

การสร้าง workbook ด้วยโปรแกรมเป็นพื้นฐานของงาน **automate excel workbook**. การอ้างอิง `Worksheet` ทำให้คุณสามารถจัดการเซลล์โดยตรง

## ขั้นตอนที่ 2: เติมค่า 1‑20 ลงในแถวแรก

ต่อไป เติมค่าในเซลล์ `A1` ถึง `T1` ด้วยตัวเลข 1 ถึง 20 ลูป `for` ง่าย ๆ จะเขียนค่าต่าง ๆ ลงในคอลัมน์ที่เหมาะสม

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

ทำไมต้องเขียนค่าด้วยโปรแกรม? มันรับประกันว่าตัวอย่างทำงานบนเครื่องใดก็ได้โดยไม่ต้องป้อนข้อมูลด้วยตนเอง ซึ่งสำคัญเมื่อคุณ **automate excel workbook** การสร้างในกระบวนการแบบแบตช์

## ขั้นตอนที่ 3: ใช้ฟังก์ชัน WRAPCOLS เพื่อแยกแถวเป็นบล็อก 5 คอลัมน์

ตอนนี้เราจะใช้สูตร Excel `WRAPCOLS`. มันรับช่วงข้อมูลต้นทางและจำนวนคอลัมน์ แล้วคืนค่าเป็นอาเรย์สองมิติที่ “ห่อ” ข้อมูลต้นทางเป็นจำนวนคอลัมน์ที่กำหนด

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

การใส่สูตรในเซลล์ `A2` บอก Excel ให้เริ่มผลลัพธ์ที่แถวที่สอง ผลลัพธ์จะเป็นเมทริกซ์ 4 × 5 เนื่องจาก 20 รายการหารด้วย 5 คอลัมน์ได้สี่แถว

### วิธีการทำงานของ WRAPCOLS

* **Source range** – `A1:T1` มีค่าต้นฉบับ 20 ค่า.  
* **Column count** – `5` บอก Excel ให้สร้างห้าคอลัมน์ต่อแถว.  
* **Result** – Excel เติมเซลล์ `A2:E5` ด้วยข้อมูลที่ห่ออัตโนมัติ.  

หากคุณต้องการ **split row into columns** ด้วยขนาดบล็อกที่ต่างออกไป เพียงเปลี่ยนอาร์กิวเมนต์ที่สอง ตัวอย่างเช่น `WRAPCOLS(A1:T1,4)` จะให้ผลลัพธ์เป็นห้าแถวที่มีสี่คอลัมน์ต่อแถว

## ขั้นตอนที่ 4: คำนวณสูตรเพื่อให้ผลลัพธ์ WRAPCOLS ปรากฏจริง

สูตรที่เพิ่มใหม่จะยังไม่ได้ประเมินจนกว่าเอนจินการคำนวณจะทำงาน การเรียก `CalculateFormula()` จะทำให้ขั้นตอน **excel formula calculation** เขียนค่าจริงลงใน worksheet

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

การรันการคำนวณเป็นสิ่งสำคัญเมื่อคุณต่อมาจะ **save excel file c#** เพราะไฟล์ที่บันทึกต้องมีค่าที่คำนวณแล้ว ไม่ใช่แค่ข้อความสูตร หากข้ามขั้นตอนนี้ workbook ที่ส่งออกจะแสดง `#N/A` หรือสูตรดิบแทนตัวเลขที่คาดหวัง

## ขั้นตอนที่ 5: บันทึก workbook ลงดิสก์

สุดท้าย ให้บันทึก workbook ด้วยเมธอด `Save`. คุณสามารถระบุเส้นทางไฟล์ที่ถูกต้องใดก็ได้; ตัวอย่างใช้ไดเรกทอรี placeholder ที่คุณควรแทนที่ด้วยของคุณเอง

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

การเรียก `Save` แสดงตัวอย่าง **save excel file c#** ในรูปแบบที่ง่ายที่สุด Aspose.Cells จะเลือกฟอร์แมต XLSX อัตโนมัติตามส่วนขยายไฟล์ หากคุณต้องการไฟล์ `.xls` เก่า ให้เปลี่ยนส่วนขยายตามนั้น

### ผลลัพธ์ที่คาดหวัง

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

แถวเดียวเดิมได้ถูก **split row into columns** เป็นสี่แถว โดยแต่ละแถวมีห้าคอลัมน์

## โค้ดเต็ม

การรวมทุกขั้นตอนเข้าด้วยกันให้โปรแกรมที่กระชับและเป็นอิสระ:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

คัดลอกโค้ดไปยังโปรเจกต์คอนโซลใหม่, เรียกคืนแพ็กเกจ NuGet ของ Aspose.Cells, แล้วรัน โปรแกรมจะสร้างไฟล์ Excel บนเดสก์ท็อปของคุณในไม่กี่วินาที

## การปรับเปลี่ยนทั่วไปและกรณีขอบ

การปรับเปลี่ยนเหล่านี้แสดงให้เห็นว่ารูปแบบ **how to use wrapcols** เดียวกันสามารถปรับใช้กับหลายสถานการณ์การปรับรูปแบบข้อมูลได้

| Situation | Adjustment |
|-----------|------------|
| **ขนาดบล็อกที่แตกต่าง** | Change `WRAPCOLS(A1:T1,5)` to `WRAPCOLS(A1:T1, n)` where `n` is the desired column count. |
| **หลายแถวต้นทาง** | Use `WRAPCOLS(A1:A10,5)` to wrap a vertical range into a 5‑column matrix. |
| **ช่วงต้นทางแบบไดนามิก** | Build the address string in C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) before assigning the formula. |
| **Worksheet ขนาดใหญ่** | Call `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` to skip cells that cause errors and improve performance. |
| **บันทึกเป็น CSV** | Replace `workbook.Save(outputPath)` with `workbook.Save(outputPath, SaveFormat.Csv)`. |

## เคล็ดลับการแก้ไขปัญหา

* **Formula not evaluated** – ตรวจสอบว่าคุณเรียก `workbook.CalculateFormula()` *หลังจาก* ตั้งสูตร หากข้ามขั้นตอนนี้เซลล์จะเหลือข้อความสูตรดิบ `WRAPCOLS`.  
* **File access denied** – ตรวจสอบว่าไดเรกทอรีเป้าหมายมีอยู่และกระบวนการของคุณมีสิทธิ์เขียน ใช้ `Environment.SpecialFolder.Desktop` จะหลีกเลี่ยงปัญหาการอนุญาตส่วนใหญ่.  
* **Incorrect number of rows** – ตรวจสอบอาร์กิวเมนต์ที่สองของ `WRAPCOLS` อีกครั้ง มันกำหนดจำนวนคอลัมน์ ไม่ใช่จำนวนแถว; จำนวนแถวได้มาจากจำนวนเซลล์ต้นทางทั้งหมดหารด้วยจำนวนคอลัมน์นั้น.  

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to use WRAPCOLS** ใน C# เพื่อ **split row into columns**, สร้าง **automate excel workbook** อย่างเต็มรูปแบบ, รัน **excel formula calculation**, และ **save excel file c#** ด้วยโค้ดฐานเดียวที่เรียบง่าย เทคนิคนี้ขจัดการคัดลอก‑วางด้วยมือและขยายได้อย่างง่ายดายสำหรับสายงานการแปลงข้อมูลขนาดใหญ่

### ขั้นตอนต่อไป

* สำรวจฟังก์ชันอาเรย์แบบไดนามิกอื่น ๆ เช่น `SEQUENCE`, `FILTER`, และ `UNIQUE` เพื่อเพิ่มศักยภาพให้กับชุดเครื่องมือการทำอัตโนมัติ Excel ของคุณ.  
* รวม `WRAPCOLS` กับ API การสร้างแผนภูมิเพื่อสร้างรายงานที่พร้อมเผยแพร่.  
* ผสานโค้ดเข้ากับบริการเบื้องหลังที่ประมวลผลการอัปโหลด CSV และส่งออกไฟล์ Excel ที่ปรับรูปแบบใหม่สำหรับการวิเคราะห์ต่อไป.  

คุณสามารถทดลองกับช่วงต้นทางและจำนวนคอลัมน์ที่ต่างกัน—ปรับสูตร, รันการคำนวณใหม่, และดู workbook อัปเดตทันที ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ

- [วิธีใช้ wrapcols ใน C# – คู่มือเต็มกับ Excel WRAPROWS & การคำนวณสูตรใหม่](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [วิธีใช้ WRAPCOLS – คู่มือครบสำหรับการทำอัตโนมัติ Excel ด้วย C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [วิธีใช้ WRAPCOLS ใน C# – ปรับรูปแบบอาเรย์เป็นเมทริกซ์ใน Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}