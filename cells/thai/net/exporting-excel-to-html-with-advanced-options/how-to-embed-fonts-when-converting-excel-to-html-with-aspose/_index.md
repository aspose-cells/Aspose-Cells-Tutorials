---
category: general
date: 2026-10-01
description: เรียนรู้วิธีฝังฟอนต์ใน HTML ขณะแปลง Excel เป็น HTML ด้วย Aspose.Cells
  ส่งออก Excel เป็น HTML พร้อมฟอนต์ที่ฝังไว้ในไม่กี่ขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: th
lastmod: 2026-10-01
og_description: วิธีฝังฟอนต์ใน HTML เมื่อส่งออกไฟล์ Excel ทำตามคู่มือขั้นตอนนี้เพื่อแปลง
  Excel เป็น HTML พร้อมฟอนต์ที่ฝังไว้
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: วิธีฝังฟอนต์ใน HTML จาก Excel – คู่มือ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: วิธีฝังฟอนต์เมื่อแปลง Excel เป็น HTML ด้วย Aspose.Cells
url: /th/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีฝังฟอนต์เมื่อแปลง Excel เป็น HTML ด้วย Aspose.Cells

การฝังฟอนต์ใน HTML เมื่อแปลงเวิร์กบุ๊ก Excel เป็นสิ่งสำคัญเพื่อรักษารูปลักษณ์เดิมให้คงที่บนเบราว์เซอร์ต่าง ๆ หากคุณต้องการแปลง Excel เป็น HTML พร้อมคงฟอนต์ที่กำหนดเองไว้ คำแนะนำนี้จะแสดงกระบวนการทั้งหมด คุณจะได้เห็นวิธีส่งออก Excel เป็น HTML และเหตุผลที่การฝังฟอนต์ใน HTML มีความสำคัญต่อการแสดงผลที่สอดคล้องกัน

บทเรียนนี้ครอบคลุมทุกสิ่งที่คุณต้องรู้: ไลบรารีที่จำเป็น การกำหนดค่ารหัส และการตรวจสอบไฟล์ HTML ที่สร้างขึ้น เมื่อเสร็จสิ้นคุณจะสามารถส่งออก Excel เป็น HTML พร้อมฝังฟอนต์ได้ด้วยเพียงไม่กี่บรรทัดของ C#

## สิ่งที่คุณต้องการ

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

* **.NET 6.0 หรือใหม่กว่า** – โค้ดนี้ใช้ .NET 6 แต่เวอร์ชัน .NET ใด ๆ ที่รองรับ Aspose.Cells ก็ทำงานได้
* **Aspose.Cells for .NET** – รับใบอนุญาตหรือใช้เวอร์ชันประเมินฟรีจากเว็บไซต์ Aspose
* สภาพแวดล้อมการพัฒนา **C#** (Visual Studio, Rider หรือ VS Code) – IDE ใดก็ได้ที่สามารถคอมไพล์โปรเจกต์ .NET
* เวิร์กบุ๊ก Excel (`Styled.xlsx`) ที่ใช้ฟอนต์กำหนดเองที่คุณต้องการเก็บไว้

## ขั้นตอนที่ 1: ตั้งค่า Aspose.Cells ในโครงการ .NET ของคุณ

แรกสุด ให้เพิ่มแพ็กเกจ NuGet ของ Aspose.Cells ลงในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.Cells
```

จากนั้นให้รวมเนมสเปซที่ส่วนบนของไฟล์ C# ของคุณ:

```csharp
using Aspose.Cells;
```

การเพิ่มแพ็กเกจทำให้คลาส `Workbook`, `HtmlSaveOptions` และคลาสที่เกี่ยวข้องพร้อมใช้งาน

## ขั้นตอนที่ 2: โหลดไฟล์ Excel

การโหลดเวิร์กบุ๊กเป็นขั้นตอนแรกที่เป็นรูปธรรมใน **how to export Excel** โครงสร้าง `Workbook` จะอ่านไฟล์จากดิสก์:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*ทำไมเรื่องนี้ถึงสำคัญ:* Aspose.Cells จะทำการพาร์สเวิร์กบุ๊กรวมถึงสไตล์ของเซลล์ สูตร และข้อมูลฟอนต์ หากไฟล์ไม่พบจะเกิดข้อยกเว้น ดังนั้นให้ตรวจสอบให้แน่ใจว่าเส้นทางไฟล์ถูกต้อง

## ขั้นตอนที่ 3: กำหนดค่า HTML Save Options เพื่อฝังฟอนต์

หัวใจของ **embed fonts in html** คือคลาส `HtmlSaveOptions` ตั้งค่า `EmbedFonts` เป็น `true` เพื่อให้ฟอนต์ทุกตัวที่ใช้ในเวิร์กบุ๊กถูกเขียนลงในผลลัพธ์ HTML เป็นกฎ `@font-face` ที่เข้ารหัสเป็น Base64

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*ทำไมเรื่องนี้ถึงสำคัญ:* โดยค่าเริ่มต้น Aspose.Cells จะอ้างอิงไฟล์ฟอนต์ภายนอก ซึ่งอาจไม่มีบนเครื่องของผู้ใช้ การเปิดใช้งาน `EmbedFonts` รับประกันว่าการแสดงผล HTML จะเหมือนกับแผ่น Excel ดั้งเดิม ไม่ว่าผู้ชมจะมีฟอนต์ติดตั้งไว้หรือไม่

### กรณีขอบ: ฟอนต์ที่ไม่รองรับ

หากเวิร์กบุ๊กใช้ฟอนต์ที่ไม่ได้ติดตั้งบนเซิร์ฟเวอร์ Aspose.Cells จะเปลี่ยนไปใช้ฟอนต์ระบบเริ่มต้น เพื่อหลีกเลี่ยงสถานการณ์นี้ ให้ติดตั้งฟอนต์ที่จำเป็นบนเซิร์ฟเวอร์หรือฝังฟอนต์ด้วยตนเองหลังการส่งออก

## ขั้นตอนที่ 4: บันทึกไฟล์ Excel เป็น HTML ด้วยตัวเลือกที่กำหนด

ตอนนี้คุณสามารถเขียนไฟล์ HTML ได้แล้ว เมธอด `Save` รับพาธเอาต์พุตและอินสแตนซ์ `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

หลังจากทำงานเสร็จ `Styled.html` จะมีข้อมูลสเปรดชีตและบล็อก `<style>` ที่มีการกำหนด `@font-face` ที่เข้ารหัส Base64 สำหรับฟอนต์กำหนดเองแต่ละตัว

## ขั้นตอนที่ 5: ตรวจสอบการฝังฟอนต์

เปิด `Styled.html` ในเบราว์เซอร์ ตรวจสอบส่วน `<head>` คุณควรเห็นอย่างเช่น:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

หากฟอนต์แสดงผลอย่างถูกต้องในตารางที่เรนเดอร์ การฝังฟอนต์สำเร็จ หากพบอักขระหายไป ให้ตรวจสอบว่าฟอนต์ต้นฉบับได้ติดตั้งบนเครื่องที่ทำการแปลงหรือไม่

## ตัวแปรทั่วไปและตัวเลือกเพิ่มเติม

### การแปลงหลายแผ่นงาน

หากคุณต้องการ **convert Excel to HTML** สำหรับทุกแผ่นงาน ให้ตั้งค่า `ExportActiveWorksheetOnly = false` (ค่าเริ่มต้น) Aspose.Cells จะสร้างไฟล์ HTML แยกต่างหากสำหรับแต่ละแผ่น

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### การควบคุมการออก CSS

คุณสามารถลดขนาด HTML ได้โดยปิดการใช้ CSS แบบอินไลน์:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### การใช้สตรีมแทนไฟล์

เมื่อนำไปใช้ร่วมกับ Web API ให้เขียน HTML ลงใน `MemoryStream` แล้วส่งกลับโดยตรง:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## เคล็ดลับพิเศษ: ใบอนุญาตผลิตภัณฑ์เพื่อกำจัดลายน้ำการประเมิน

หากคุณใช้เวอร์ชันประเมิน HTML ที่สร้างอาจมีคอมเมนต์ลายน้ำ ให้ใช้ใบอนุญาต Aspose.Cells ก่อนโหลดเวิร์กบุ๊กเพื่อให้ได้ผลลัพธ์ที่สะอาด:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่ทำงานได้เต็มรูปแบบซึ่งสาธิต **how to embed fonts**, **convert excel to html**, และ **export excel as html** พร้อมกัน:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรันโปรแกรม `Styled.html` จะปรากฏใน `YOUR_DIRECTORY` การเปิดไฟล์ในเบราว์เซอร์สมัยใหม่ใด ๆ จะเห็นสเปรดชีตพร้อมฟอนต์เดียวกับไฟล์ Excel ดั้งเดิม แม้บนเครื่องที่ไม่มีฟอนต์เหล่านั้น

## สรุป

คุณได้เรียนรู้ **how to embed fonts** เมื่อ **convert Excel to HTML** ด้วย Aspose.Cells แล้ว และได้เห็นขั้นตอนทั้งหมดตั้งแต่การโหลดเวิร์กบุ๊กจนถึงการตรวจสอบฟอนต์ที่ฝัง วิธีนี้รับประกันว่าความเที่ยงตรงของการแสดงผล Excel จะคงอยู่ใน HTML ที่สร้างขึ้น ทำให้เหมาะสำหรับการรายงานบนเว็บ, จดหมายข่าวอีเมล, หรือสถานการณ์ใด ๆ ที่ต้อง **export Excel as HTML** พร้อมการพิมพ์แบบกำหนดเอง

ต่อไปให้สำรวจหัวข้อที่เกี่ยวข้องเช่น **exporting Excel as PDF**, **styling HTML output with custom CSS**, หรือ **batch‑processing multiple workbooks** ทุกหัวข้อใช้รูปแบบ `HtmlSaveOptions` เดียวกัน คุณจึงสามารถปรับโค้ดได้ด้วยการเปลี่ยนแปลงเล็กน้อย

Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [วิธีส่งออก Excel เป็น HTML – คู่มือขั้นตอนโดยละเอียด](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [วิธีฝังฟอนต์ใน HTML – คู่มือ C# ฉบับสมบูรณ์](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [วิธีฝังฟอนต์เมื่อแปลง Excel เป็น PDF – คู่มือขั้นตอนโดยละเอียด](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}