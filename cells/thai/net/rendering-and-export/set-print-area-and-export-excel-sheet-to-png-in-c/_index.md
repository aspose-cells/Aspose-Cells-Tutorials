---
category: general
date: 2026-10-26
description: ตั้งค่าพื้นที่การพิมพ์และส่งออกแผ่นงาน Excel เป็น PNG ด้วย C# เรียนรู้ตัวเลือกการส่งออกภาพ
  วิธีการส่งออกเป็น PNG และวิธีรับภาพที่สามารถพิมพ์ได้จากสมุดงาน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: th
lastmod: 2026-10-26
og_description: กำหนดพื้นที่พิมพ์และส่งออกแผ่นงาน Excel เป็น PNG ใน C# คำแนะนำทีละขั้นตอนนี้ครอบคลุมตัวเลือกการส่งออกภาพและวิธีการส่งออก
  PNG จากสมุดงาน
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: ตั้งค่าพื้นที่พิมพ์และส่งออกแผ่นงาน Excel เป็น PNG – คู่มือ C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: ตั้งค่าพื้นที่พิมพ์และส่งออกแผ่นงาน Excel เป็น PNG ใน C#
url: /th/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่าพื้นที่พิมพ์และส่งออกแผ่นงาน Excel เป็น PNG ใน C#

หากคุณต้องการ **ตั้งค่าพื้นที่พิมพ์** ก่อนส่งออกแผ่นงาน Excel เป็น PNG คู่มือนี้จะแสดงวิธีทำ คุณจะได้เห็นตัวอย่าง C# ครบถ้วนที่กำหนดตัวเลือกการส่งออกภาพ ปรับพื้นที่พิมพ์ของแผ่นงาน และบันทึกผลลัพธ์เป็นภาพ

การส่งออกแผ่นงาน Excel เป็น PNG เป็นความต้องการที่พบบ่อยเมื่อคุณต้องการฝังภาพสแนปชอตของแผ่นงานในรายงาน อีเมล หรือหน้าเว็บ โค้ดด้านล่างทำงานกับเวิร์กบุ๊กใด ๆ ที่มี Pivot Table แต่เทคนิคนี้ก็ใช้ได้กับช่วงข้อมูลปกติเช่นกัน ไม่ต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี Aspose.Cells for .NET

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (ตัวอย่างใช้ .NET 6 แต่เวอร์ชัน .NET ล่าสุดใดก็ทำงานได้)
- Aspose.Cells for .NET (ติดตั้งผ่าน NuGet: `Install-Package Aspose.Cells`)
- ความคุ้นเคยพื้นฐานกับ C# และแนวคิดของ Excel เช่น แผ่นงานและพื้นที่พิมพ์

## ขั้นตอนที่ 1: กำหนดค่าตัวเลือกการส่งออกภาพ

สิ่งแรกที่คุณทำคือสร้างอินสแตนซ์ของ `ImageOrPrintOptions` วัตถุนี้บอก Aspose.Cells ว่าจะเรนเดอร์แผ่นงานเป็นภาพอย่างไร

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**ทำไมเรื่องนี้สำคัญ:** `ImageOrPrintOptions` ควบคุมรูปแบบการส่งออก ความละเอียด และรายละเอียดการเรนเดอร์อื่น ๆ การใช้ PNG ทำให้ได้คุณภาพแบบไม่มีการสูญเสีย ซึ่งเหมาะสำหรับรายงานที่ต้องการข้อความและกราฟิกคมชัด

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กและเข้าถึงแผ่นงานเป้าหมาย

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**ทำไมเรื่องนี้สำคัญ:** คุณต้องทำงานกับอ็อบเจ็กต์ `Worksheet` เฉพาะ เนื่องจากพื้นที่พิมพ์เป็นการตั้งค่าระดับแผ่นงาน

## ขั้นตอนที่ 3: ระบุช่วงที่คุณต้องการพิมพ์

ในหลายกรณี ข้อมูลที่คุณสนใจอยู่ภายใน Pivot Table โค้ดต่อไปนี้จะดึงช่วงข้อมูลของ Pivot Table แรกบนแผ่นงาน

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

หากแผ่นงานของคุณไม่มี Pivot Table คุณสามารถแทนที่ `pivotDataRange` ด้วย `CellArea` ใด ๆ ที่คุณสร้างด้วยตนเอง เช่น:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## ขั้นตอนที่ 4: **ตั้งค่าพื้นที่พิมพ์** ให้ตรงกับช่วงที่เลือก

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**ทำไมเรื่องนี้สำคัญ:** พื้นที่พิมพ์บอก Excel (และ Aspose.Cells) ว่าเซลล์ใดบ้างที่จะรวมเมื่อเรนเดอร์แผ่นงานเป็นภาพ โดยการจัดให้พื้นที่พิมพ์สอดคล้องกับช่วงข้อมูล Pivot คุณจะหลีกเลี่ยงขอบว่างและทำให้ PNG ที่ส่งออกมีเฉพาะข้อมูลที่เกี่ยวข้องเท่านั้น

## ขั้นตอนที่ 5: ส่งออกแผ่นงานเป็นภาพ PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**ทำไมเรื่องนี้สำคัญ:** `worksheet.ToImage` เคารพพื้นที่พิมพ์ที่ตั้งไว้ก่อนหน้า ดังนั้นไฟล์ PNG จะมีเซลล์ที่คุณกำหนดเท่านั้น การกำหนดภาพให้กับรูปภาพรูปแบบ (picture shape) ทำให้คุณสามารถฝังกลับเข้าไปในเวิร์กบุ๊กได้หากต้องการ ในขณะที่การบันทึกลงดิสก์ทำให้ได้ไฟล์แยกอิสระ

## ตัวอย่างการทำงานเต็มรูปแบบ

การรวมทุกขั้นตอนเข้าด้วยกันจะได้โปรแกรมที่ทำงานอิสระซึ่งคุณสามารถรันได้ทันที

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะสร้างไฟล์ `C:\Temp\WorksheetExport.png` การเปิดไฟล์จะแสดงภาพ PNG คมชัดที่มีเฉพาะเซลล์ที่กำหนดโดย **การตั้งค่าพื้นที่พิมพ์** (ข้อมูล Pivot Table ในตัวอย่างนี้) ภาพนี้สามารถแทรกลงในเอกสาร Word, สไลด์ PowerPoint หรือหน้าเว็บโดยไม่ต้องทำขั้นตอนการแปลงเพิ่มเติม

## การจัดการหลายแผ่นงานหรือหลาย Pivot Table

- **หลายแผ่นงาน:** วนลูปผ่าน `wb.Worksheets` และทำซ้ำขั้นตอนที่ 3‑5 สำหรับแต่ละแผ่นงานที่ต้องการส่งออก
- **หลาย Pivot Table:** เลือก `PivotTables[index]` ที่เหมาะสมหรือวนลูปผ่าน `worksheet.PivotTables` เพื่อส่งออกแต่ละตารางแยกกัน
- **ไม่มี Pivot Table:** สร้าง `CellArea` ด้วยตนเอง (ดูคอมเมนต์ในขั้นตอน 3) แล้วกำหนดให้กับ `PrintArea`

## เคล็ดลับเชิงปฏิบัติ (E‑E‑A‑T)

- **เคล็ดลับมืออาชีพ:** ตั้งค่า `HorizontalResolution` และ `VerticalResolution` เป็น 300 DPI สำหรับ PNG ที่พร้อมพิมพ์; ค่าต่ำกว่าจะทำให้ไฟล์มีขนาดเล็กลงสำหรับการใช้บนเว็บ
- **ระวังรูปภาพรูปแบบว่าง:** หากแผ่นงานไม่มี picture shapes ให้เพิ่มหนึ่งรูปก่อนกำหนดภาพ:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **ประสิทธิภาพ:** การใช้ `ImageOrPrintOptions` ตัวเดียวซ้ำสำหรับหลายแผ่นงานช่วยหลีกเลี่ยงการจัดสรรหน่วยความจำที่ไม่จำเป็น
- **ความเข้ากันได้:** Aspose.Cells 23.9+ รองรับ .NET 6 และรุ่นต่อไปอย่างเต็มที่; เวอร์ชันก่อนหน้าอาจต้องปรับชื่อ API

## สรุป

ตอนนี้คุณรู้วิธี **ตั้งค่าพื้นที่พิมพ์** และส่งออก Excel

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ

- [วิธีส่งออก Excel เป็น PNG – คู่มือขั้นตอนเต็ม](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [วิธีส่งออกช่วง Excel เป็นภาพด้วย C# และ Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [แผ่นงาน Excel เป็น PNG – ส่งออก Pivot Table เป็น PNG ใน C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}