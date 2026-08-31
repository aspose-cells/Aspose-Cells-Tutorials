---
category: general
date: 2026-02-23
description: สร้างเวิร์กบุ๊กใหม่โดยใช้โปรแกรมใน C# และเพิ่มสูตรลงในเซลล์ เรียนรู้วิธีใช้
  EXPAND แล้วบันทึกเวิร์กบุ๊ก Excel อย่างง่ายดาย.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: th
og_description: สร้างเวิร์กบุ๊กใหม่โดยใช้โปรแกรมใน C# เพิ่มสูตรลงในเซลล์ เรียนรู้การใช้
  EXPAND และบันทึกไฟล์ Excel ในไม่กี่วินาที
og_title: สร้างเวิร์กบุ๊กใหม่ใน C# – เพิ่มสูตรและบันทึกไฟล์ Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: สร้างเวิร์กบุ๊กใหม่ใน C# – เพิ่มสูตรและบันทึกไฟล์ Excel
url: /th/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Workbook ใหม่ใน C# – เพิ่มสูตรและบันทึกไฟล์ Excel

เคยสงสัยไหมว่า **create new workbook** จากโค้ดโดยไม่ต้องเปิด Excel? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาหลายคนมักเจออุปสรรคเมื่อจำเป็นต้องสร้างสเปรดชีตแบบทันที—อาจเป็นเพื่อรายงาน การส่งออก หรือการดัมพ์ข้อมูลอย่างรวดเร็ว  

ข่าวดีคืออะไร? ในคู่มือนี้คุณจะได้เห็นวิธี **create new workbook** อย่างแม่นยำ, ใส่ **add formula to cell**, แล้ว **save excel workbook** ด้วยเพียงไม่กี่บรรทัดของ C#. เราจะเจาะลึก **how to use expand** เพื่อให้คุณสร้างอาเรย์แบบไดนามิกโดยไม่ต้องคัดลอกด้วยมือ สุดท้ายคุณจะสามารถ **create excel file programmatically** และส่งต่อให้ผู้ใช้หรือบริการ downstream ได้

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (runtime .NET ใดก็ได้ที่ทันสมัย)
- Aspose.Cells for .NET (เวอร์ชันทดลองหรือเวอร์ชันลิขสิทธิ์) – ไลบรารีนี้ให้คลาส `Workbook` และ `Worksheet` ที่ใช้ในตัวอย่างด้านล่าง
- ความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ C#—ไม่จำเป็นต้องรู้ลึกเกี่ยวกับ Excel

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม! ถ้ายังไม่มี ให้ดาวน์โหลด Aspose.Cells จาก NuGet (`Install-Package Aspose.Cells`) แล้วคุณก็พร้อมเริ่มทำงาน

---

## ขั้นตอนที่ 1: Create New Workbook – พื้นฐาน

เพื่อเริ่มต้น เราต้องสร้างอ็อบเจกต์ workbook ใหม่ เปรียบเสมือนการเปิดไฟล์ Excel ใหม่ที่ว่างเปล่าอย่างสมบูรณ์

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Why this matters:** คลาส `Workbook` เป็นจุดเริ่มต้นสำหรับการจัดการ Excel ใด ๆ การสร้างอินสแตนซ์ใหม่จะทำให้หน่วยความจำสำหรับชีต, สไตล์, และสูตรถูกจัดสรร—ทั้งหมดโดยไม่ต้องสัมผัสระบบไฟล์

## ขั้นตอนที่ 2: Access the First Worksheet

ทุก workbook ใหม่จะมาพร้อมกับ worksheet เริ่มต้น (ชื่อ *Sheet1*) เราจะดึง worksheet นี้เพื่อใส่ข้อมูลและสูตร

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** หากต้องการหลายชีต เพียงเรียก `workbook.Worksheets.Add("MySheet")` แล้วทำงานกับอ็อบเจกต์ `Worksheet` ที่คืนค่าออกมา

## ขั้นตอนที่ 3: Add Formula to Cell – Using EXPAND

ตอนนี้มาถึงส่วนที่สนุก: การใส่สูตร ฟังก์ชัน `EXPAND` เหมาะอย่างยิ่งเมื่อคุณต้องการแปลงอาเรย์คงที่ให้เป็นช่วงที่ขยายอัตโนมัติ

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### วิธีทำงานของสูตร EXPAND

| อาร์กิวเมนต์ | ความหมาย |
|----------|---------|
| `{1,2,3}` | อาเรย์ต้นฉบับ (รายการแนวนอนของสามตัวเลข) |
| `5`       | จำนวนแถวที่ต้องการในผลลัพธ์ |
| `1`       | จำนวนคอลัมน์ที่ต้องการ (ตั้งค่าเป็น 1 เพื่อให้เป็นแนวตั้ง) |

เมื่อ Excel ประมวลผลสูตรนี้ จะได้รายการ **แนวตั้ง**:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Why use EXPAND?** ฟังก์ชันนี้ช่วยขจัดความจำเป็นในการคัดลอกด้วยมือหรือวนลูป VBA ทำให้ข้อมูลถูกปรับรูปแบบแบบไดนามิก ทำให้สเปรดชีตของคุณแข็งแรงและบำรุงรักษาง่ายขึ้น

## ขั้นตอนที่ 4: Save Excel Workbook – บันทึกผลลัพธ์

เมื่อสูตรถูกใส่แล้ว ขั้นตอนสุดท้ายคือการเขียน workbook ลงดิสก์ คุณสามารถเลือกโฟลเดอร์ใดก็ได้ที่คุณมีสิทธิ์เขียน

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **What you’ll see:** เปิดไฟล์ `ExpandFormula.xlsx` ด้วย Excel แล้วเซลล์ `A1` จะโชว์อาเรย์ที่ขยาย สูตรจะคงอยู่ในเซลล์ ดังนั้นหากคุณแก้ไขอาเรย์ต้นฉบับ ผลลัพธ์จะอัปเดตโดยอัตโนมัติ

## ตัวเลือก: Verify the Output Programmatically

หากคุณไม่ต้องการเปิด Excel ด้วยตนเอง สามารถอ่านค่ากลับมาเพื่อตรวจสอบความถูกต้องได้

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

การรันโค้ดด้านบนจะพิมพ์ผลลัพธ์:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **Can I use EXPAND with a larger source array?** | แน่นอน เพียงเปลี่ยน `{1,2,3}` เป็นค่าสต็อตหรือช่วงเซลล์ใดก็ได้ เช่น `EXPAND(A1:C1,10,1)` |
| **What if I need a horizontal result?** | สลับอาร์กิวเมนต์แถว/คอลัมน์: `EXPAND({1,2,3},1,5)` จะให้ผลลัพธ์เป็น 1 แถว 5 คอลัมน์ |
| **Will this work on older Excel versions?** | `EXPAND` มีตั้งแต่ Excel 365/2021 หากใช้เวอร์ชันเก่า ต้องจำลองอาเรย์ด้วย `INDEX`/`SEQUENCE` |
| **Do I need to call `workbook.CalculateFormula()`?** | ไม่จำเป็น Aspose.Cells จะประเมินสูตรอัตโนมัติเมื่อบันทึก ทำให้ค่าปรากฏทันที |
| **How to add more than one sheet before saving?** | เรียก `workbook.Worksheets.Add("SecondSheet")` แล้วทำขั้นตอนการจัดการเซลล์บน worksheet ใหม่นั้นซ้ำอีกครั้ง |

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมรัน คัดลอกแล้ววางลงในแอปคอนโซล ปรับเส้นทางเอาต์พุตตามต้องการ แล้วกด **F5**

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Expected output in the console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

เปิดไฟล์ที่สร้างขึ้นแล้วคุณจะเห็นตัวเลขเดียวกันถูกเติมในคอลัมน์ **A**.

## สรุปภาพรวม

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*ภาพแสดง workbook ที่สร้างใหม่พร้อมผลลัพธ์จาก EXPAND*

## สรุป

ตอนนี้คุณรู้วิธี **create new workbook**, **add formula to cell**, และ **save excel workbook** ด้วย C# แล้ว การเชี่ยวชาญ **how to use expand** จะทำให้คุณสร้างอาเรย์ไดนามิกโดยไม่ต้องทำด้วยมือ และกระบวนการทั้งหมดทำให้คุณ **create excel file programmatically** สำหรับทุกสถานการณ์อัตโนมัติ

ต่อไปคุณจะทำอะไร? ลองเปลี่ยนอาเรย์คงที่เป็นการอ้างอิงช่วง, ทดลองกับมิติ `EXPAND` ต่าง ๆ, หรือเชื่อมสูตรหลายสูตรข้ามชีต รูปแบบเดียวกันนี้ยังใช้ได้กับแผนภูมิ, การจัดรูปแบบ, และแม้กระทั่ง pivot table—อย่าหยุดสำรวจ

หากคุณเจอปัญหาใด ๆ คอมเมนต์ด้านล่างได้เลย ขอให้เขียนโค้ดสนุกและเพลิดเพลินกับพลังของ Excel แบบโปรแกรมเมติก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}