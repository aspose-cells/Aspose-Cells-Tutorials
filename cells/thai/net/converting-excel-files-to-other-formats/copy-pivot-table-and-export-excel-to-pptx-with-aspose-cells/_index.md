---
category: general
date: 2026-09-11
description: คัดลอก Pivot Table และส่งออกไฟล์ Excel เป็น PPTX ด้วย Aspose.Cells เรียนรู้วิธีสร้างไฟล์
  PPTX ที่แก้ไขได้และบันทึกเวิร์กบุ๊กเป็น PPTX ด้วย C#
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: th
lastmod: 2026-09-11
og_description: คัดลอก Pivot Table และส่งออก Excel ไปเป็น PPTX ด้วย C# โดยใช้ Aspose.Cells
  สร้างไฟล์ PPTX ที่แก้ไขได้และบันทึกเวิร์กบุ๊กเป็น PPTX ด้วยเพียงไม่กี่บรรทัดของโค้ด.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: คัดลอก Pivot Table และส่งออก Excel ไปยัง PPTX – คู่มือ C# ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: คัดลอก Pivot Table และส่งออก Excel ไปเป็น PPTX ด้วย Aspose.Cells
url: /th/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอก Pivot Table และส่งออก Excel ไปเป็น PPTX ด้วย Aspose.Cells

หากคุณต้องการคัดลอก Pivot Table จากแผ่นงานหนึ่งไปยังอีกแผ่นงานหนึ่งและจากนั้นส่งออกไฟล์ Excel ไปเป็นงานนำเสนอ PowerPoint คำแนะนำนี้จะแสดงวิธีทำ ด้วย Aspose.Cells คุณสามารถสร้างไฟล์ PPTX ที่แก้ไขได้และบันทึกเวิร์กบุ๊กเป็น PPTX ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C#  

บทเรียนนี้ครอบคลุมทุกขั้นตอนที่จำเป็นสำหรับการย้าย Pivot Table รักษาฟังก์ชันการทำงานของมัน และสร้างไฟล์ PPTX ที่แผนภูมิและรูปร่างยังคงแก้ไขได้ ไม่ต้องใช้เครื่องมือภายนอก—เพียงไลบรารี Aspose.Cells และสภาพแวดล้อมการพัฒนา .NET

## สิ่งที่คุณจะได้เรียนรู้

* **คัดลอก Pivot Table** จากแผ่นงานต้นทางไปยังแผ่นงานปลายทางพร้อมคงการเชื่อมต่อข้อมูลทั้งหมดไว้  
* **ส่งออก Excel ไปเป็น PPTX** เพื่อให้สไลด์ที่ได้สามารถแก้ไขใน PowerPoint ได้  
* **สร้าง PPTX ที่แก้ไขได้** โดยที่แผนภูมิ ตาราง และรูปร่างไม่ถูกแปลงเป็นภาพ  
* **บันทึกเวิร์กบุ๊กเป็น PPTX** ด้วยการเรียก API ของ Aspose.Cells เดียวกัน  

### ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+)  
* Aspose.Cells for .NET (แพ็กเกจ NuGet `Aspose.Cells`)  
* ความเข้าใจพื้นฐานเกี่ยวกับแอปพลิเคชันคอนโซล C#  

> **เคล็ดลับระดับมืออาชีพ:** ติดตั้งแพ็กเกจ NuGet ผ่าน CLI เพื่อรับประกันว่าคุณมีเวอร์ชันล่าสุด:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## วิธีคัดลอก Pivot Table ระหว่างแผ่นงาน

การดำเนินการแรกคือการย้าย Pivot Table พร้อมคงคำนิยามไว้ Aspose.Cells มีเมธอด `CopyRange` พร้อมอ็อบเจ็กต์ `CopyOptions` ที่มีฟลัก `CopyPivotTable`

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**ทำไมวิธีนี้ถึงได้ผล:**  
`CopyRange` คัดลอกข้อมูลเซลล์ การจัดรูปแบบ และเมื่อ `CopyPivotTable` เป็น true จะคัดลอกแคชและเมตาดาต้าของ Pivot Table ช่วงปลายทางเริ่มที่เซลล์ `A1` (แถว 0, คอลัมน์ 0) แต่คุณสามารถเปลี่ยนค่า offset เพื่อวาง Pivot Table ไว้ที่ตำแหน่งอื่นได้  

**กรณีขอบที่พบบ่อย:** หากแผ่นงานปลายทางมี Pivot Table ที่มีชื่อเดียวกันอยู่แล้ว Aspose.Cells จะเปลี่ยนชื่อ Pivot Table ที่กำลังคัดลอกโดยอัตโนมัติ เพื่อป้องกันการชนชื่อ

## ส่งออก Excel ไปเป็น PPTX และสร้าง PPTX ที่แก้ไขได้

เมื่อ Pivot Table อยู่ในตำแหน่งแล้ว คุณสามารถส่งออกเวิร์กบุ๊กทั้งหมดเป็นไฟล์ PPTX ได้ คลาส `ImageOrPrintOptions` ให้คุณระบุ `ExportImageFormat = ImageFormat.Pptx` ซึ่งบอก Aspose.Cells ให้ประมวลผลผลลัพธ์เป็นงานนำเสนอ PowerPoint แทนภาพเรสเตอร์

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**ทำไมวิธีนี้ถึงได้ผล:**  
เมื่อ `ExportImageFormat` ตั้งเป็น `Pptx` Aspose.Cells จะแปลงแต่ละแผ่นงานเป็นสไลด์ รูปร่าง แผนภูมิ และ Pivot Table จะถูกเขียนเป็นอ็อบเจ็กต์ PowerPoint แบบดั้งเดิม ดังนั้นคุณสามารถดับเบิล‑คลิกใน PowerPoint เพื่อแก้ไขข้อมูลพื้นฐานได้  

**เคล็ดลับสำหรับเวิร์กบุ๊กขนาดใหญ่:** หากคุณต้องการส่งออกเฉพาะบางแผ่นงาน ให้เรียก `workbook.Worksheets.RemoveAt(index)` เพื่อลบแผ่นงานที่ไม่ต้องการก่อนเรียก `Save` เพื่อลดขนาดไฟล์ PPTX

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่เชื่อมโยงขั้นตอนก่อนหน้าเข้าด้วยกัน แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงบนเครื่องของคุณ

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะแสดงผล:

```
Pivot table copied and workbook exported to PPTX successfully.
```

เมื่อคุณเปิด `output.pptx` ใน Microsoft PowerPoint คุณจะเห็นสไลด์ที่มี Pivot Table ที่คัดลอกมาเป็นแผนภูมิที่แก้ไขได้ การดับเบิล‑คลิกแผนภูมิจะเปิด PowerPoint Chart Editor ให้คุณแก้ไขซีรีส์ แกน และป้ายข้อมูลโดยไม่ต้องกลับไปที่ Excel

## การจัดการกับข้อผิดพลาดทั่วไป

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| Pivot Table ปรากฏเป็นภาพคงที่ | ไม่ได้ตั้งค่า `CopyPivotTable` หรือ `ExportImageFormat` เป็น `Png` | ตรวจสอบให้ `CopyPivotTable = true` และ `ExportImageFormat = ImageFormat.Pptx` |
| แผ่นงานปลายทางแสดงเซลล์ว่าง | ช่วงต้นทางไม่ครอบคลุมพื้นที่ Pivot Table ทั้งหมด | ขยายช่วง (เช่น `"A1:H30"`) เพื่อรวมฟิลด์ Pivot ทั้งหมด |
| ไฟล์ PPTX ที่ส่งออกมีขนาดใหญ่ | มีแผ่นงานที่ไม่จำเป็นรวมอยู่ | ลบแผ่นงานที่ไม่ต้องการก่อนเรียก `Save` |
| PowerPoint ไม่สามารถแก้ไขแผนภูมิได้ | ใช้ Aspose.Cells เวอร์ชันเก่าที่ไม่มีการสนับสนุน PPTX | อัปเกรดเป็นเวอร์ชันล่าสุดของ Aspose.Cells (ตรวจสอบ release notes) |

## ขั้นตอนต่อไปและหัวข้อที่เกี่ยวข้อง

* **ส่งออกแผ่นงาน Excel ไปเป็น PPTX ด้วยเลย์เอาต์สไลด์แบบกำหนดเอง** – สำรวจ `WorksheetToPdfConverter` เพื่อควบคุมลักษณะสไลด์ได้ละเอียดขึ้น  
* **ส่งออก Excel ไปเป็น PDF** – แทนที่ `ImageFormat.Pptx` ด้วย `ImageFormat.Pdf` เพื่อสร้างไฟล์ PDF  
* **แก้ไข PPTX อย่างโปรแกรมเมติกหลังการส่งออก** – ใช้ไลบรารี `Aspose.Slides` เพื่อเพิ่มแอนิเมชันหรือโน้ตผู้บรรยาย  

ด้วยการเชี่ยวชาญ **คัดลอก Pivot Table**, **ส่งออก Excel ไปเป็น PPTX**, และ **สร้าง PPTX ที่แก้ไขได้** คุณสามารถสร้างไพพ์ไลน์การรายงานแบบครบวงจรที่ย้ายข้อมูลจากสเปรดชีตตรงไปยังเด็คการนำเสนอโดยไม่สูญเสียความสามารถในการแก้ไข

---


## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณเอง

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}