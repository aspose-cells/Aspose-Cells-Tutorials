---
category: general
date: 2026-10-04
description: เรียนรู้วิธีสร้างไฟล์ Excel ใน C# และใช้ฟังก์ชัน EXPAND, บังคับให้สูตรคำนวณ,
  และบันทึกไฟล์เป็น XLSX พร้อมกับเติมคอลัมน์ด้วยตัวเลข
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: th
lastmod: 2026-10-04
og_description: สร้างไฟล์ Excel workbook ด้วย C# โดยใช้ Aspose.Cells บทเรียนนี้แสดงวิธีใช้
  EXPAND, บังคับการคำนวณสูตร, และบันทึก workbook เป็น XLSX พร้อมกับเติมตัวเลขในคอลัมน์หนึ่ง.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: สร้างเวิร์กบุ๊ก Excel ด้วย C# – คู่มือเต็มรูปแบบกับ EXPAND และการบันทึกเป็น
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: วิธีสร้างสมุดงาน Excel ใน C# ด้วยฟังก์ชัน EXPAND
url: /th/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Excel workbook ใน C# ด้วยฟังก์ชัน EXPAND

หากคุณต้องการ **สร้าง Excel workbook** อย่างอัตโนมัติ คู่มือนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และพร้อมรัน คุณจะได้เห็นวิธี **populate column with numbers**, ใช้ฟังก์ชัน **EXPAND** เพื่อกระจายข้อมูลในแนวนอน, **force formula calculation**, และสุดท้าย **save workbook as XLSX**.  

บทแนะนำนี้ครอบคลุมทุกขั้นตอนที่คุณต้องการ ตั้งแต่การเริ่มต้น workbook จนถึงการตรวจสอบผลลัพธ์ ไม่จำเป็นต้องอ้างอิงเอกสารภายนอก—เพียงคัดลอกโค้ด รัน และคุณจะได้ไฟล์ Excel ที่ทำงานเต็มรูปแบบ

## ความต้องการเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+)
- NuGet package Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C#
- IDE เช่น Visual Studio หรือ VS Code

## ขั้นตอนที่ 1: สร้าง Excel workbook และเข้าถึง worksheet แรก

การกระทำแรกคือ **สร้าง Excel workbook** และรับอ้างอิงไปยัง worksheet เริ่มต้นของมัน Aspose.Cells จะเพิ่ม worksheet ที่ตำแหน่ง index 0 โดยอัตโนมัติ ทำให้คุณสามารถใช้งานได้ทันที

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*ทำไมจึงสำคัญ:* การสร้างอินสแตนซ์ `Workbook` จะจัดสรรโครงสร้างไฟล์ภายใน และการดึง `Worksheets[0]` จะให้วัตถุ `Worksheet` ที่ใช้จัดการแถว, คอลัมน์, และเซลล์

## ขั้นตอนที่ 2: Populate column with numbers

ต่อไป ให้เติมรายการแนวตั้งในคอลัมน์ A ซึ่งเป็นการสาธิต **populate column with numbers** และเป็นช่วงข้อมูลต้นทางสำหรับฟังก์ชัน EXPAND

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*เคล็ดลับ:* ใช้ `PutValue` สำหรับตัวเลขดิบ, สตริง, วันที่ หรือ primitive ของ .NET ใด ๆ วิธีนี้จะกำหนดประเภทเซลล์โดยอัตโนมัติ

## ขั้นตอนที่ 3: วิธีใช้ EXPAND – กระจายรายการในแนวนอน

ส่วน **how to use expand** เป็นหัวใจของบทแนะนำนี้ ฟังก์ชัน `EXPAND` จะขยายช่วงข้อมูลต้นทางเป็นรูปแบบใหม่ ที่นี่เราขยายช่วงแนวตั้ง `A1:A3` ให้เป็นแถวเดียวที่ครอบคลุมสามคอลัมน์ เริ่มที่ `B1`

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*คำอธิบาย:*  
- อาร์กิวเมนต์แรก (`A1:A3`) คือช่วงข้อมูลต้นทาง  
- อาร์กิวเมนต์ที่สอง (`1`) บังคับให้ผลลัพธ์มี **1** แถว  
- อาร์กิวเมนต์ที่สาม (`3`) บังคับให้ผลลัพธ์มี **3** คอลัมน์  

เมื่อ workbook ทำการคำนวณใหม่ เซลล์ `B1`, `C1`, และ `D1` จะมีค่า `1`, `2`, และ `3` ตามลำดับ

## ขั้นตอนที่ 4: Force formula calculation

Aspose.Cells ไม่ได้ประเมินสูตรโดยอัตโนมัติหลังจากที่คุณตั้งค่า ดังนั้นคุณต้อง **force formula calculation** ก่อนบันทึก เพื่อให้ผลลัพธ์ของ EXPAND ถูกบันทึกลงในไฟล์

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*ทำไมคุณต้องทำ:* หากไม่ได้เรียก `CalculateFormula` ไฟล์ที่บันทึกจะมีเพียงสตริงสูตรดิบ และ Excel จะคำนวณใหม่เมื่อเปิดไฟล์ สำหรับ pipeline ที่อัตโนมัติ คุณมักต้องการให้ค่าถูกเขียนลงทันที

## ขั้นตอนที่ 5: Save workbook as XLSX

เมื่อ workbook พร้อมเต็มที่แล้ว **save workbook as XLSX** ไปยังตำแหน่งที่คุณเลือก ส่วนขยายไฟล์จะกำหนดรูปแบบผลลัพธ์; `.xlsx` จะสร้าง workbook แบบ Office Open XML

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*เคล็ดลับ:* หากต้องการรูปแบบอื่น (CSV, PDF, ฯลฯ) เพียงเปลี่ยนส่วนขยายไฟล์หรือใช้ `workbook.Save(outputPath, SaveFormat.Xls)` สำหรับเวอร์ชัน Excel เก่า

## ตัวอย่างเต็มที่สามารถรันได้

การรวมส่วนต่าง ๆ เข้าด้วยกันจะให้โปรแกรมแบบ self‑contained ที่ **creates Excel workbook**, เติมคอลัมน์, ใช้ **EXPAND**, บังคับการคำนวณ, และ **saves workbook as XLSX**

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หลังจากรันโปรแกรม เปิดไฟล์ `ExpandFunction.xlsx` ใน Excel คุณควรเห็น:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

ค่าตัวเลข `1`, `2`, `3` ในเซลล์ `B1:D1` ยืนยันว่า ฟังก์ชัน **EXPAND** ทำงานและขั้นตอน **force formula calculation** ทำให้ผลลัพธ์ถูกบันทึกลงอย่างสำเร็จ

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | การปรับเปลี่ยน |
|----------|------------|
| **ช่วงข้อมูลต้นทางแบบไดนามิก** | ใช้ `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` เพื่อขยายตามจำนวนแถวที่มีข้อมูล |
| **มิติผลลัพธ์ที่แตกต่าง** | เปลี่ยนอาร์กิวเมนต์ที่สองและที่สามของ `EXPAND` เพื่อควบคุมจำนวนแถวและคอลัมน์ |
| **หลาย worksheet** | วนลูปผ่าน `workbook.Worksheets` และใช้ตรรกะเดียวกันกับแต่ละชีต |
| **ชุดข้อมูลขนาดใหญ่** | เรียก `workbook.CalculateFormula()` ครั้งเดียวหลังจากตั้งสูตรทั้งหมด เพื่อหลีกเลี่ยงการคำนวณซ้ำหลายครั้ง |
| **บันทึกเป็น memory stream** | แทนที่ `workbook.Save(path)` ด้วย `workbook.Save(stream, SaveFormat.Xlsx)` เมื่อคุณต้องการไฟล์ใน response ของเว็บ API |

## รายการตรวจสอบการแก้ไขปัญหา

- **Formula not expanding:** ตรวจสอบว่าได้เรียก `CalculateFormula()` *หลัง* ตั้งสูตร  
- **File not found on save:** ตรวจสอบว่าไดเรกทอรีเป้าหมายมีอยู่และกระบวนการมีสิทธิ์เขียน  
- **Incorrect data type:** ใช้ `PutValue` สำหรับตัวเลข; สำหรับวันที่ใช้ `PutValue(DateTime.Now)` หรือ `PutDateTime`  
- **Version mismatch:** ฟังก์ชัน EXPAND ต้องการ engine การคำนวณที่เข้ากันกับ Excel 365; Aspose.Cells 23.9+ รองรับ

## สรุป

ตอนนี้คุณรู้วิธี **create Excel workbook** ใน C#, **populate column with numbers**, ใช้ฟังก์ชัน **EXPAND**, **force formula calculation**, และ **save workbook as XLSX** ตัวอย่างครบวงจรนี้สามารถปรับใช้สำหรับการรายงาน, การแปลงข้อมูล, หรือสถานการณ์อัตโนมัติใด ๆ ที่ต้องการผลลัพธ์ Excel แบบไดนามิก

### ขั้นตอนต่อไป

- สำรวจฟังก์ชันอาเรย์ไดนามิกอื่น ๆ เช่น `FILTER`, `SORT`, และ `UNIQUE`  
- ผสานการสร้าง workbook เข้าใน ASP.NET Core API เพื่อส่งไฟล์ Excel ตามความต้องการ  
- แทนที่ตัวเลขที่กำหนดไว้ล่วงหน้าด้วยข้อมูลที่อ่านจากฐานข้อมูลหรือไฟล์ CSV สำหรับการรายงานในโลกจริง

ลองทดลองกับช่วงต่าง ๆ, ชื่อชีต, และรูปแบบผลลัพธ์ที่แตกต่างได้ตามต้องการ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [วิธีคำนวณ Cotangent ใน Excel ด้วย C# – สร้าง Workbook, ใช้ EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [วิธีใช้ WRAPCOLS ใน C# – สร้าง Excel Workbook ด้วยฟังก์ชัน Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [วิธีสร้างและบันทึก Excel Workbook เป็น ODS ด้วย Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}