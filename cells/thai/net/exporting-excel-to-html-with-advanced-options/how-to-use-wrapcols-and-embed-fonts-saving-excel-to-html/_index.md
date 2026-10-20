---
category: general
date: 2026-10-20
description: เรียนรู้วิธีใช้ wrapcols ใน Aspose.Cells, ฝังฟอนต์ใน HTML, และบันทึก
  Excel เป็น HTML พร้อมตัวอย่าง C# ที่สมบูรณ์
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: th
lastmod: 2026-10-20
og_description: วิธีใช้ wrapcols ใน Aspose.Cells, ฝังฟอนต์ใน HTML, และแปลงเวิร์กบุ๊กเป็น
  HTML พร้อมขั้นตอน C# ที่ชัดเจนสำหรับนักพัฒนา.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: วิธีใช้ wrapcols และฝังฟอนต์ในการส่งออก Excel เป็น HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: วิธีใช้ wrapcols และฝังฟอนต์เมื่อบันทึก Excel เป็น HTML
url: /th/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ wrapcols และฝังฟอนต์เมื่อบันทึก Excel เป็น HTML

หากคุณต้องการ **วิธีใช้ wrapcols** ในสูตร Aspose.Cells คู่มือนี้จะแสดงขั้นตอนที่ชัดเจนให้คุณ นอกจากนี้คุณยังจะได้เรียนรู้วิธี **ฝังฟอนต์ใน HTML** และ **บันทึก Excel เป็น HTML** เพื่อให้ผลลัพธ์แสดงผลเหมือนกันในทุกเบราว์เซอร์  

บทแนะนำนี้ครอบคลุมสามสถานการณ์การใช้งานจริง: การใช้ฟังก์ชัน `WRAPCOLS` การส่งออกเวิร์กบุ๊กพร้อมฟอนต์ที่ฝังไว้ และการสร้างรายงาน master‑detail ด้วย Smart Markers เมื่อจบคุณจะมีโปรแกรม C# ที่สามารถรันได้หนึ่งไฟล์ซึ่งสาธิตคุณลักษณะทั้งหมดเหล่านี้

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำตามขั้นตอน ให้ตรวจสอบว่าคุณมี:

* ติดตั้ง .NET 6.0 (หรือเวอร์ชันใหม่กว่า)
* เพิ่ม Aspose.Cells for .NET ลงในโปรเจกต์ของคุณ (`dotnet add package Aspose.Cells`)
* มีความคุ้นเคยพื้นฐานกับ C# และสูตร Excel

ไม่จำเป็นต้องใช้ไลบรารีของบุคคลที่สามเพิ่มเติม; Aspose.Cells จะจัดการการแปลงเป็น HTML และการฝังฟอนต์ภายในโดยอัตโนมัติ

## ขั้นตอนที่ 1: สาธิตฟังก์ชัน **วิธีใช้ wrapcols** ในสูตร

ฟังก์ชัน `WRAPCOLS` จะแบ่งช่วงข้อมูลแบบมิติเดียวเป็นอาเรย์สองมิติ โดยเติมข้อมูลตามคอลัมน์ก่อน นี่เป็นประโยชน์เมื่อคุณต้องการปรับรูปแบบข้อมูลสำหรับการรายงานหรือการสร้างแผนภูมิ

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**ทำไมจึงทำงานได้:**  
`WRAPCOLS` รับอาร์กิวเมนต์สองค่า – ช่วงข้อมูลต้นทางและจำนวนคอลัมน์ ฟังก์ชันจะเติมอาเรย์ตามคอลัมน์โดยละค่าที่เกินออก (ค่า `3` ในตัวอย่าง) ผลลัพธ์จะแสดงในเซลล์ซ้ายบนของช่วงเป้าหมาย (`B1`) และคุณสามารถขยายช่วงนี้ด้วยตนเองได้หากต้องการอาเรย์เต็ม

> **เคล็ดลับ:** หลังจากตั้งสูตรแล้ว ให้เรียก `workbook.CalculateFormula()` เพื่อให้แน่ใจว่าผลลัพธ์เป็นข้อมูลล่าสุดก่อนอ่านค่าจากเซลล์

## ขั้นตอนที่ 2: **แปลงเวิร์กบุ๊กเป็น HTML** และ **ฝังฟอนต์ใน html**

เมื่อคุณส่งออกไฟล์ Excel เป็น HTML ฟอนต์มักจะถูกแทนที่ด้วยฟอนต์เริ่มต้นของเบราว์เซอร์ ซึ่งอาจทำให้การจัดวางภาพเสียหาย Aspose.Cells ให้คุณฝังฟอนต์ที่ใช้ในเวิร์กบุ๊กโดยตรงลงในไฟล์ HTML

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**ทำไมการฝังฟอนต์ถึงสำคัญ:**  
เมื่อ `EmbedFonts` เป็น `true` Aspose.Cells จะเปลี่ยนฟอนต์ TrueType/OpenType ที่ใช้แต่ละตัวให้เป็นกฎ `@font-face` ที่เข้ารหัสเป็น Base64 ภายใน HTML ที่สร้างขึ้น ซึ่งทำให้ไม่จำเป็นต้องติดตั้งฟอนต์เดียวกันบนเครื่องของผู้ใช้และรับประกันการแสดงผลที่พิกเซลแม่นยำ

> **กรณีพิเศษ:** หากเวิร์กบุ๊กต้นทางอ้างอิงฟอนต์ที่ไม่ได้ติดตั้งบนเซิร์ฟเวอร์ Aspose.Cells จะใช้ฟอนต์เริ่มต้นแทนและแสดงคำเตือน ตรวจสอบให้แน่ใจว่าฟอนต์ที่ต้องการพร้อมใช้งาน

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ

- [วิธีใช้ WRAPCOLS ใน C# – สร้าง Excel Workbook ด้วยฟังก์ชัน Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [วิธีฝังฟอนต์ใน HTML – แปลง Excel เป็น HTML ด้วย C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [วิธีแปลงไฟล์ Excel เป็น HTML ด้วย Aspose.Cells for .NET: ซ่อนเนื้อหาที่ซ้อนทับ](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}