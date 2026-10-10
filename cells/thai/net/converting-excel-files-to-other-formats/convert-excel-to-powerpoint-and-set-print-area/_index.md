---
category: general
date: 2026-10-10
description: แปลง Excel เป็น PowerPoint และตั้งค่าพื้นที่พิมพ์ใน C# ด้วย Aspose.Cells
  – เรียนรู้วิธีส่งออก Excel ตั้งค่าพื้นที่พิมพ์ และสร้างไฟล์ PPTX
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: th
lastmod: 2026-10-10
og_description: แปลง Excel เป็น PowerPoint ด้วย Aspose.Cells บทเรียนนี้แสดงวิธีตั้งค่าพื้นที่พิมพ์,
  ส่งออก Excel, และสร้างไฟล์ PPTX ด้วย C#
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: แปลง Excel ไปเป็น PowerPoint – คู่มือเต็มสำหรับนักพัฒนา C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: แปลง Excel เป็น PowerPoint และตั้งค่าพื้นที่พิมพ์
url: /th/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง Excel เป็น PowerPoint และตั้งค่าพื้นที่พิมพ์

หากคุณต้องการ **convert Excel to PowerPoint**, คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าทำอย่างไรใน C#. โดยกำหนดพื้นที่พิมพ์ก่อน คุณจะควบคุมว่าเซลล์ใดปรากฏบนแต่ละสไลด์ และไฟล์ PPTX สุดท้ายจะตรงกับการจัดวางที่คุณคาดหวัง โซลูชันนี้ยังตอบคำถาม “how to export Excel” และ “how to set print area” ด้วยโค้ดฐานเดียวกัน

ในบทเรียนนี้คุณจะได้:

* โหลดเวิร์กบุ๊กที่มีอยู่
* ตั้งค่าพื้นที่พิมพ์สำหรับแผ่นงาน (ขั้นตอน **set print area excel**)
* กำหนดค่าตัวเลือกการแปลงสำหรับผลลัพธ์ PowerPoint
* สร้างไฟล์ **convert excel to pptx** ในการเรียกเมธอดเดียว

โค้ดที่จำเป็นทั้งหมดรวมอยู่แล้ว คุณจึงสามารถคัดลอก วาง และรันได้ทันที

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| **.NET 6.0 หรือใหม่กว่า** | ตัวอย่างนี้ใช้ .NET 6+ แต่เวอร์ชัน .NET ใดก็ได้ที่รองรับ C# 10 ก็ทำงานได้ |
| **Aspose.Cells for .NET** | ไลบรารีนี้ให้ `Workbook`, `ImageOrPrintOptions` และเมธอด `ConvertToPdf` (ใช้สำหรับ PPTX) ติดตั้งผ่าน NuGet: `dotnet add package Aspose.Cells` |
| **ไฟล์ Excel อินพุต** | คู่มือใช้ไฟล์ `input.xlsx`. วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้ |
| **สิทธิ์การเขียนไปยังโฟลเดอร์ผลลัพธ์** | โปรแกรมจะเขียนไฟล์ `output.pptx`. ตรวจสอบให้แน่ใจว่าไดเรกทอรีมีอยู่และสามารถเขียนได้ |

> **เคล็ดลับ:** หากคุณทำงานกับหลายแผ่นงาน ให้ทำขั้นตอนพื้นที่พิมพ์ซ้ำสำหรับแต่ละแผ่นก่อนการแปลง

## ขั้นตอนที่ 1: สร้างโปรเจกต์คอนโซล C# ใหม่

เปิดเทอร์มินัลหรือหน้าต่าง PowerShell แล้วรัน:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

คำสั่งนี้จะสร้างโปรเจกต์ใหม่ชื่อ **ExcelToPowerPointDemo** และเพิ่มแพคเกจ Aspose.Cells ซึ่งเป็นการพึ่งพาหลักสำหรับ **how to export Excel** ไปยังรูปแบบอื่น

## ขั้นตอนที่ 2: เขียนโค้ดการแปลง

แทนที่เนื้อหาของ `Program.cs` ด้วยตัวอย่างเต็มด้านล่าง โค้ดนี้แสดง **convert excel to powerpoint**, แสดง **how to set print area**, และสร้างไฟล์ **convert excel to pptx**

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### ทำไมแต่ละส่วนจึงสำคัญ

* **Loading the workbook** – นี่คือขั้นตอนแรกในทุกสถานการณ์ **how to export Excel**. `Workbook` อ่านไฟล์เข้าสู่หน่วยความจำ ทำให้คุณเข้าถึงแผ่นงาน เซลล์ และการจัดรูปแบบได้อย่างเต็มที่.
* **Setting the print area** – โดยการกำหนดค่า `PageSetup.PrintArea` คุณบอก Aspose.Cells ว่าเซลล์ใดจะต้องเรนเดอร์ นี่คือหัวใจของ **set print area excel**; หากไม่มี จะทำการส่งออกแผ่นงานทั้งหมด ซึ่งอาจทำให้สไลด์ใหญ่และอ่านไม่ออก
* **Choosing `SaveFormat.Pptx`** – วัตถุ `ImageOrPrintOptions` ให้คุณเปลี่ยนรูปแบบผลลัพธ์ การตั้งค่า `SaveFormat` เป็น `Pptx` จะเปิดใช้งานกระบวนการ **convert excel to pptx**
* **Calling `ConvertToPdf`** – แม้ชื่อเมธอดจะเป็น `ConvertToPdf` แต่เมื่อ `SaveFormat` เป็น `Pptx` ไลบรารีจะสร้างไฟล์ PowerPoint นี่เป็นวิธีที่แนะนำให้ **convert excel to powerpoint** ด้วยการเรียกเดียว

## ขั้นตอนที่ 3: รันโปรแกรม

จากโฟลเดอร์โปรเจกต์ ให้เรียกใช้:

```bash
dotnet run
```

หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณควรเห็นผลลัพธ์ในคอนโซลคล้ายกับ:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

เปิดไฟล์ `output.pptx` ด้วย Microsoft PowerPoint หรือโปรแกรมดูที่รองรับแต่ละสไลด์จะสอดคล้องกับหน้าที่พิมพ์ของแผ่นงาน จำกัดตามช่วงที่คุณกำหนด

## การจัดการหลายแผ่นงาน

หากเวิร์กบุ๊กของคุณมีมากกว่าหนึ่งแผ่นและคุณต้องการให้แต่ละแผ่นเป็นชุดสไลด์ของตนเอง ให้วนลูปผ่านคอลเลกชัน:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

รูปแบบนี้แสดง **how to export Excel** ข้อมูลแบบแผ่นต่อแผ่น พร้อมกับ **setting print area** แยกแต่ละแผ่น

## กรณีขอบและเคล็ดลับการปฏิบัติที่ดีที่สุด

| สถานการณ์ | แนวทางที่แนะนำ |
|-----------|----------------------|
| **แผ่นงานขนาดใหญ่มาก** | ลดพื้นที่พิมพ์หรือเพิ่ม `HorizontalResolution`/`VerticalResolution` เพื่อให้ขนาด PPTX ควบคุมได้ |
| **การวางแนวหน้าต่างๆ** | ตั้งค่า `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` ก่อนการแปลง |
| **ขนาดสไลด์แบบกำหนดเอง** | ใช้ `conversionOptions.OnePagePerSheet = false;` และปรับ `conversionOptions.Width` / `conversionOptions.Height` |
| **ไฟล์อินพุตหาย** | ห่อหุ้มโค้ดการโหลดด้วยบล็อก `try { … } catch (FileNotFoundException)` เพื่อให้ข้อความแสดงข้อผิดพลาดที่ชัดเจน |
| **อักขระที่ไม่ใช่ ASCII** | ตรวจสอบให้แน่ใจว่าเวิร์กบุ๊กบันทึกด้วยการเข้ารหัส UTF‑8; Aspose.Cells จัดการ Unicode โดยอัตโนมัติ |

## โค้ดต้นฉบับเต็มสำหรับอ้างอิง

ด้านล่างเป็นโปรแกรมทั้งหมด รวมถึงคำสั่ง `using` และคอมเมนต์ บันทึกเป็น `Program.cs` ภายในโปรเจกต์ที่สร้างใน **Step 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะสร้างไฟล์ PowerPoint (`output.pptx`) ที่มี:

* หนึ่งสไลด์ต่อหน้าที่พิมพ์ของแผ่นงาน
* เฉพาะเซลล์ในช่วง **A1:G30** ที่มองเห็นได้บนแต่ละสไลด์
* การจัดรูปแบบที่คงไว้ (ฟอนต์, สี, เส้นขอบ) ตามที่แสดงใน Excel

เปิดไฟล์ใน PowerPoint เพื่อตรวจสอบว่าการจัดวางตรงกับพื้นที่พิมพ์ที่กำหนด

## สรุป

ตอนนี้คุณรู้วิธี **convert Excel to PowerPoint** พร้อมกับการ **set print area excel** อย่างแม่นยำโดยใช้ Aspose.Cells ใน C#. คู่มือนี้ครอบคลุม **how to export Excel**, แสดง **how to set print area**, และแสดงตัวอย่างเต็มของ **convert excel to pptx**

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}