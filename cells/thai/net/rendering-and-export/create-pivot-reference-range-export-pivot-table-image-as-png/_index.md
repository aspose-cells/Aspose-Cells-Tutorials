---
category: general
date: 2026-02-09
description: สร้างช่วงอ้างอิงพีโวท์ใน C# และส่งออกภาพตารางพีโวท์ เรียนรู้วิธีบันทึกช่วงของ
  Excel เป็น PNG ด้วย Aspose.Cells – คู่มือสั้น ๆ ครบถ้วน
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: th
og_description: สร้างช่วงอ้างอิงพีโivot ใน C# และส่งออกภาพตารางพีโivot เป็น PNG. คู่มือขั้นตอนโดยละเอียดสำหรับการบันทึกช่วงของ
  Excel เป็น PNG.
og_title: สร้างช่วงอ้างอิง Pivot – ส่งออกภาพตาราง Pivot เป็น PNG
tags:
- Aspose.Cells
- C#
- Excel
title: สร้างช่วงอ้างอิงพีโivot – ส่งออกภาพตารางพีโivot เป็น PNG
url: /th/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างช่วงอ้างอิง Pivot – ส่งออกภาพ Pivot Table เป็น PNG

ต้องการ **สร้างช่วงอ้างอิง Pivot** ในไฟล์ Excel ด้วย C# หรือไม่? คุณยังสามารถ **ส่งออกภาพ Pivot Table** และ **บันทึกช่วงของ Excel เป็น png** ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด ตามประสบการณ์ของผม การแปลง Pivot ที่ทำงานอยู่ให้เป็นภาพคงที่เป็นวิธีที่สะดวกในการฝังการวิเคราะห์ลงในรายงาน, อีเมล หรือแดชบอร์ดโดยไม่ต้องดึงไฟล์ workbook ทั้งหมดมาด้วย

ในบทเรียนนี้เราจะพาคุณผ่านทุกอย่างที่ต้องรู้: ไลบรารีที่จำเป็น, โค้ดที่แม่นยำ, เหตุผลที่แต่ละการเรียกใช้สำคัญ, และข้อควรระวังบางอย่างที่คุณอาจเจอ สุดท้ายคุณจะสามารถสร้างไฟล์ PNG ของ Pivot Table ใดก็ได้ด้วยความมั่นใจ และจะเข้าใจวิธีปรับรูปแบบนี้สำหรับหลายแผ่นงานหรือรูปแบบภาพที่กำหนดเอง

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมี:

- **Aspose.Cells for .NET** (รุ่นทดลองฟรีใช้งานได้ดีสำหรับการทดสอบ)  
- **.NET 6.0** หรือใหม่กว่า – API ที่เราใช้เข้ากันได้เต็มที่กับ .NET Standard 2.0+ ดังนั้นเฟรมเวิร์กเก่าก็สามารถคอมไพล์ได้เช่นกัน  
- โปรเจกต์ C# เบื้องต้น (Console App, WinForms, หรือ ASP.NET – สิ่งใดที่สามารถอ้างอิง NuGet package ได้)

หากคุณยังไม่ได้ติดตั้ง Aspose.Cells ให้รัน:

```bash
dotnet add package Aspose.Cells
```

เท่านี้ – ไม่ต้องใช้ COM interop, ไม่ต้องติดตั้ง Excel บนเซิร์ฟเวอร์

## ขั้นตอนที่ 1: เปิด Workbook และเข้าถึง Worksheet แรก

สิ่งแรกที่คุณทำคือโหลดไฟล์ workbook แล้วดึง worksheet ที่มี Pivot Table เราเลือก **worksheet แรก** (`Worksheets[0]`) อย่างตั้งใจเพราะไฟล์ตัวอย่างส่วนใหญ่วาง Pivot ไว้ที่นี่ แต่คุณสามารถเปลี่ยนเป็นชื่อได้หากต้องการ

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*ทำไมจึงสำคัญ:* `Worksheet` คือจุดเริ่มต้นสำหรับการทำงานใด ๆ ที่อิงช่วง หากคุณชี้ไปที่แผ่นงานผิด `PivotTables[0]` ต่อมาจะทำให้เกิด `IndexOutOfRangeException`

## ขั้นตอนที่ 2: สร้างช่วงอ้างอิง Pivot

ต่อไปเราจะขอให้ Pivot Table ให้ **ช่วงอ้างอิง** นี้ ช่วงดังกล่าวแสดงถึงเซลล์ที่ประกอบเป็น Pivot ทั้งหัวข้อ, แถวข้อมูล, และผลรวม วิธี `CreateReferenceRange()` จะทำการประมวลผลภายในโดยอัตโนมัติ จัดการกับเซลล์ที่รวมกันและแถวที่ซ่อนอยู่ให้คุณ

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** หาก workbook ของคุณมี Pivot หลายตัว ให้วนลูป `worksheet.PivotTables` แล้วเลือกตัวที่ต้องการโดยใช้คุณสมบัติ `Name`

## ขั้นตอนที่ 3: แปลงช่วงอ้างอิงเป็นภาพ

Aspose.Cells สามารถแปลง `Range` ใด ๆ ให้เป็นภาพได้ วัตถุที่คืนค่ามารองรับทั้งรูปแบบ raster (PNG, JPEG) และ vector (SVG) ที่นี่เราขอภาพ raster เริ่มต้น ซึ่งเป็นอ็อบเจ็กต์ที่เข้ากันได้กับ `System.Drawing.Image`

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*อะไรที่เกิดขึ้นเบื้องหลัง?* API จะจับภาพการจัดวางของช่วงนั้นโดยคำนึงถึงสไตล์ของเซลล์, ฟอนต์, และการจัดรูปแบบตามเงื่อนไข ถือเหมือนกับการถ่ายสกรีนช็อตแบบโปรแกรมเมติกโดยไม่มี UI

## ขั้นตอนที่ 4: บันทึกภาพที่สร้างลงไฟล์

สุดท้ายเราจะบันทึกภาพ `Save` จะเลือก PNG อัตโนมัติเมื่อคุณให้ส่วนขยาย “.png” คุณยังสามารถส่งอ็อบเจ็กต์ `SaveOptions` หากต้องการควบคุม DPI หรือใช้รูปแบบอื่นได้

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

หลังจากบรรทัดนี้ทำงานเสร็จ ให้เปิด `pivot.png` คุณจะเห็นภาพที่คมชัดของ Pivot Table พร้อมฝังได้ทุกที่

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือโปรแกรมคอนโซลที่พร้อมคัดลอกและรันได้:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** ไฟล์ชื่อ `pivot.png` อยู่ใน `YOUR_DIRECTORY` เปิดด้วยโปรแกรมดูภาพใดก็ได้ – คุณจะเห็นการจัดวางที่ตรงกับ Pivot ดั้งเดิม รวมถึงหัวคอลัมน์, แถวข้อมูล, และผลรวมรวม

## ส่งออกภาพ Pivot Table – ปรับขนาดและ DPI

บางครั้งภาพเริ่มต้นอาจเล็กเกินไปสำหรับสไลด์พรีเซนเทชัน คุณสามารถควบคุมความละเอียดได้โดยส่งอ็อบเจ็กต์ `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*ทำไมต้องปรับ DPI?* DPI ที่สูงให้ขอบคมชัดมากขึ้น โดยเฉพาะเมื่อ PNG ถูกขยายใน PowerPoint หรือ PDF

## บันทึกช่วง Excel เป็น PNG – จัดการหลาย Worksheet

หากต้องการส่งออก Pivot จากหลายแผ่น ให้วนลูป `Workbook.Worksheets` แล้วทำซ้ำขั้นตอนเดิม นี่คือตัวอย่างสั้น ๆ:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

รูปแบบนี้ **export pivot table image** สำหรับทุก Pivot ใน workbook และไฟล์แต่ละไฟล์จะตั้งชื่อตามแผ่นงานและ Pivot – เหมาะสำหรับการประมวลผลเป็นชุด

## ปัญหาที่พบบ่อย & วิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | Worksheet has no pivot tables. | Check `worksheet.PivotTables.Count` before accessing. |
| Blank image output | Pivot is filtered to hide all rows. | Ensure the pivot has visible data, or call `pivot.RefreshData();` before creating the range. |
| Low‑resolution PNG | Default DPI is 96. | Use `ImageOrVectorSaveOptions.Resolution` as shown above. |
| File‑path errors | Invalid characters in `YOUR_DIRECTORY`. | Use `Path.Combine` and `Path.GetInvalidPathChars()` to sanitize. |

## การตรวจสอบ – ทดสอบอย่างรวดเร็ว

หลังจากรันตัวอย่างเต็ม:

1. เปิด `pivot.png` ใน Windows Photo Viewer.  
2. ตรวจสอบว่าหัวคอลัมน์, แถวข้อมูล, และแถวผลรวมตรงกับมุมมองใน Excel.  
3. หากพบแถวหาย ให้ตรวจสอบว่าได้เรียกใช้เมธอด **RefreshData** ของ Pivot ก่อน `CreateReferenceRange()` หรือไม่

## โบนัส: ฝัง PNG ลงในเอกสาร Word

เพราะภาพเป็น PNG อยู่แล้ว คุณสามารถส่งต่อให้ Aspose.Words ได้โดยตรง:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

ตอนนี้คุณมีรายงาน Word ที่มีภาพสแนปช็อตของ Pivot อย่างแม่นยำ – ไม่ต้องคัดลอก‑วางด้วยมือ

## สรุป

คุณเพิ่งเรียนรู้วิธี **สร้างช่วงอ้างอิง Pivot**, **ส่งออกภาพ Pivot Table**, และ **บันทึกช่วงของ Excel เป็น png** ด้วย Aspose.Cells ใน C# สิ่งที่ควรจำคือ:

- ใช้ `PivotTable.CreateReferenceRange()` เพื่อแยกพื้นที่การแสดงผลของ Pivot  
- แปลงช่วงนั้นเป็นภาพด้วย `Range.ToImage()`  
- บันทึกภาพเป็น PNG พร้อมปรับ DPI หากต้องการคุณภาพพิมพ์

จากจุดนี้คุณสามารถสำรวจการส่งออกเป็นชุด, รูปแบบภาพอื่น ๆ (SVG, JPEG) หรือแม้แต่ฝัง PNG ลงใน PDF หรือ Word ได้ ไม่จำกัดอะไรเมื่อคุณมี Pivot เป็นกราฟิกคงที่

มีคำถามหรือกรณีที่ซับซ้อน? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}