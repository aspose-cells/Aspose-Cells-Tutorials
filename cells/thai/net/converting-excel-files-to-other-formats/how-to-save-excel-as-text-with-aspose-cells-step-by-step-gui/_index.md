---
category: general
date: 2026-10-10
description: เรียนรู้วิธีบันทึกไฟล์ Excel เป็นข้อความใน C# ด้วย Aspose.Cells คู่มือนี้ครอบคลุมการแปลง
  Excel เป็น txt, การส่งออก XLSX เป็น txt, และการสร้างไฟล์ txt จาก Excel พร้อมโค้ดเต็ม.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: th
lastmod: 2026-10-10
og_description: บันทึกไฟล์ Excel เป็นข้อความโดยใช้ Aspose.Cells for .NET. ทำตามคำแนะนำนี้เพื่อแปลง
  Excel เป็น txt, ส่งออก XLSX เป็น txt, และสร้างไฟล์ txt จาก Excel พร้อมตัวอย่างโค้ด.
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: บันทึกไฟล์ Excel เป็นข้อความใน C# – บทเรียน Aspose.Cells อย่างครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: วิธีบันทึก Excel เป็นข้อความด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียด
url: /th/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีบันทึก Excel เป็นข้อความด้วย Aspose.Cells – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **บันทึก Excel เป็นข้อความ** อย่างรวดเร็ว บทแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนที่ทำใน C# ด้วย Aspose.Cells อย่างชัดเจน คุณจะได้เรียนรู้วิธี **แปลง Excel เป็น txt**, ควบคุมความแม่นยำของตัวเลข, และจัดการกับกรณีขอบทั่วไป—ทั้งหมดในตัวอย่างที่สามารถรันได้หนึ่งเดียว

ในส่วนต่อไปนี้คุณจะได้เรียนรู้ขั้นตอนการทำงานทั้งหมด ตั้งแต่การติดตั้งไลบรารีจนถึงการตรวจสอบไฟล์ผลลัพธ์ ไม่จำเป็นต้องอ้างอิงเอกสารภายนอก; ทุกอย่างที่คุณต้องการรวมอยู่ที่นี่แล้ว

## สิ่งที่คุณจะได้ทำ

* โหลดไฟล์เวิร์กบุ๊ก `.xlsx` ใด ๆ จากดิสก์  
* กำหนดค่า `TxtSaveOptions` เพื่อจำกัดจำนวนหลักสำคัญ  
* **ส่งออก XLSX เป็น txt** ด้วยการเรียก `Save` เพียงครั้งเดียว  
* เข้าใจวิธีแก้ไขปัญหาการจัดรูปแบบเมื่อคุณ **สร้าง txt จาก Excel**

### ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.7.2+)  
* ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ของ .NET ใดก็ได้)  
* ใบอนุญาต Aspose.Cells for .NET ที่ใช้งานได้หรือคีย์ทดลองฟรี  
* ไฟล์ Excel ที่คุณต้องการแปลง (`input.xlsx` ในตัวอย่าง)

> **เคล็ดลับ:** หากคุณวางแผนจะรันบนเซิร์ฟเวอร์ ให้เก็บไฟล์ใบอนุญาตในตำแหน่งที่ปลอดภัยและโหลดเพียงครั้งเดียวเมื่อแอปพลิเคชันเริ่มทำงาน

## ขั้นตอนที่ 1: ตั้งค่าสภาพแวดล้อมการพัฒนา

1. สร้างโปรเจกต์คอนโซลใหม่:

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. เพิ่มแพ็กเกจ NuGet ของ Aspose.Cells:

   ```bash
   dotnet add package Aspose.Cells
   ```

   การทำเช่นนี้จะดึงเวอร์ชันล่าสุดที่เสถียร (ณ 2026‑10‑10 เวอร์ชันคือ 23.9).

3. (ทางเลือก) หากคุณมีไฟล์ใบอนุญาต ให้วาง `Aspose.Cells.lic` ไว้ที่โฟลเดอร์รากของโปรเจกต์และเพิ่มโค้ดต่อไปนี้ที่ส่วนเริ่มต้นของ `Program.cs`:

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   การโหลดใบอนุญาตจะลบลายน้ำการประเมินและปิดการจำกัดขนาด

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊ก Excel

บรรทัดแรกที่ทำงานสร้างอินสแตนซ์ `Workbook` ที่แทนไฟล์ Excel ทั้งหมด

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**ทำไมจึงสำคัญ:** `Workbook` เป็นการนามธรรมของแผ่นงาน, เซลล์, สูตร, และการจัดรูปแบบ โดยการโหลดไฟล์เพียงครั้งเดียว คุณจะทำให้การแปลงเร็วและใช้หน่วยความจำอย่างมีประสิทธิภาพ

## ขั้นตอนที่ 3: กำหนดค่า TxtSaveOptions เพื่อควบคุมจำนวนหลักอย่างแม่นยำ

เมื่อคุณ **แปลง Excel เป็น txt** ค่าตัวเลขอาจมีทศนิยมหลายตำแหน่ง `TxtSaveOptions` ช่วยให้คุณจำกัดผลลัพธ์ให้มีจำนวนหลักสำคัญที่กำหนด ซึ่งมักจำเป็นสำหรับระบบต่อท้ายที่ต้องการข้อความความกว้างคงที่

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**คำอธิบาย:**  
* `SignificantDigits` ตัดเสียงรบกวนของค่าจุดลอยและยังคงความแม่นยำที่เพียงพอสำหรับการคำนวณทางธุรกิจส่วนใหญ่  
* `Separator` มีค่าเริ่มต้นเป็นช่องว่าง; การตั้งค่าเป็น `\t` (แท็บ) ทำให้ไฟล์ที่ได้ง่ายต่อการนำเข้าไปยังฐานข้อมูลหรือสเปรดชีต  
* `ExportActiveWorksheetOnly` ป้องกันการส่งออกแผ่นงานที่ซ่อนโดยบังเอิญ ซึ่งอาจทำให้ไฟล์ข้อความบวมขึ้น

## ขั้นตอนที่ 4: ส่งออก XLSX เป็น txt ด้วยตัวเลือกที่กำหนดไว้

ตอนนี้คุณมีทุกอย่างที่ต้องการเพื่อ **บันทึก Excel เป็นข้อความ** เมธอด `Save` จะเขียนการแสดงผลเป็นข้อความธรรมดาไปยังเส้นทางเป้าหมาย

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

ไฟล์ `output.txt` ที่สร้างขึ้นจะมีแถวของค่าที่คั่นด้วยแท็บ, แต่ละเซลล์จะแสดงเป็นข้อความธรรมดาตามตัวเลือกที่คุณตั้งค่า

### โปรแกรมที่สามารถรันได้เต็มรูปแบบ

เมื่อนำส่วนต่าง ๆ มารวมกัน นี่คือตัวอย่างแอปพลิเคชันคอนโซลที่สมบูรณ์และทำงานได้เอง:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (คอนโซล):

```
✅ Excel workbook successfully saved as text at: output.txt
```

**ตัวอย่าง `output.txt` ที่ได้** (สามแถวแรก):

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

ตัวเลขจะถูกปัดเป็นห้าหลักสำคัญ และคอลัมน์จะคั่นด้วยแท็บ

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และจัดการกรณีขอบ

### ตรวจสอบโดยโปรแกรม

คุณสามารถอ่านไฟล์ที่สร้างขึ้นกลับเข้าสู่หน่วยความจำเพื่อยืนยันว่าการส่งออกสำเร็จ:

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### กรณีขอบทั่วไป

| สถานการณ์                              | สิ่งที่ควรระวัง                                 | วิธีแก้แนะนำ |
|----------------------------------------|---------------------------------------------------|-----------------|
| เซลล์มีสูตร                | ค่าที่ส่งออกคือ **ผลลัพธ์ที่คำนวณแล้ว**, ไม่ใช่ข้อความสูตร. | ตรวจสอบให้แน่ใจว่าเวิร์กบุ๊กคำนวณสูตรครบถ้วน (`workbook.CalculateFormula();`) ก่อนบันทึก. |
| วันที่แสดงเป็นเลขซีเรียล         | Excel เก็บวันที่เป็นตัวเลข; อาจปรากฏเป็น `44745`. | ตั้งค่า `txtOptions.ConvertDateTime = true;` เพื่อบังคับให้แสดงรูปแบบวันที่ที่มนุษย์อ่านได้. |
| แผ่นงานขนาดใหญ่ (>10 000 แถว)        | การใช้หน่วยความจำอาจพุ่งสูง.                     | ใช้ `txtOptions.ExportAllSheets = false;` และประมวลผลแต่ละแผ่นงานแยกกัน. |
| อักขระ Unicode (เช่น อีโมจิ)      | การเข้ารหัสเริ่มต้นคือ UTF‑8; ระบบเก่าอาจคาดหวัง ANSI. | ตั้งค่า `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");` หากจำเป็น. |

โดยการคาดการณ์สถานการณ์เหล่านี้ คุณสามารถ **สร้าง txt จาก Excel** ได้อย่างเชื่อถือได้ในชุดข้อมูลต่าง ๆ

## สรุป

ตอนนี้คุณรู้วิธี **บันทึก Excel เป็นข้อความ** ด้วย Aspose.Cells สำหรับ .NET ตั้งแต่การโหลดเวิร์กบุ๊กจนถึงการกำหนดค่า `TxtSaveOptions` และสุดท้าย **ส่งออก XLSX เป็น txt** ตัวอย่างนี้แสดงเส้นทางโค้ดเต็ม, อธิบายเหตุผลของแต่ละการตั้งค่า, และครอบคลุมข้อผิดพลาดทั่วไปเมื่อคุณ **แปลง Excel เป็น txt**

### ขั้นตอนต่อไปคืออะไร?

* ลองส่งออกเป็น CSV (`CsvSaveOptions`) สำหรับไฟล์คอมม่า‑เซพที่เข้ากันได้กับ Excel.  
* สำรวจคลาส `PdfSaveOptions` เพื่อ **ส่งออก Excel เป็น PDF** ด้วยบรรทัดเดียว.  
* รวมหลายแผ่นงานเป็นไฟล์ข้อความเดียวโดยวนลูปผ่าน `workbook.Worksheets`.  

คุณสามารถทดลองปรับตัวเลือกต่าง ๆ — เปลี่ยนตัวคั่น, ความแม่นยำ, หรือการเลือกแผ่นงาน — ให้เหมาะกับกระบวนการทำงานของคุณ

ขอให้เขียนโค้ดสนุก!

## สิ่งที่คุณควรเรียนต่อไปคืออะไร?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ

- [บันทึก Excel เป็นไฟล์ข้อความด้วยตัวคั่นกำหนดเองโดยใช้ Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [บันทึก Excel เป็น txt – คู่มือ C# ครบถ้วนสำหรับส่งออกตัวเลขด้วยหลักสำคัญ](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [วิธีบันทึกไฟล์ Excel ในหลายรูปแบบโดยใช้ Aspose.Cells .NET (คู่มือ 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}