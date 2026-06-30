---
category: general
date: 2026-06-30
description: ส่งออกแผนภูมิเป็น PNG ในขณะที่คุณแปลง Excel เป็น HTML ด้วย Aspose.Cells
  เรียนรู้การฝังรูปภาพเป็น Base64 และบันทึกเวิร์กบุ๊กเป็น HTML ในไม่กี่นาที
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: th
og_description: ส่งออกแผนภูมิเป็น PNG และฝังรูปภาพเป็น Base64 ขณะแปลง Excel เป็น HTML
  ทำตามบทแนะนำ C# ทีละขั้นตอนนี้เพื่อบันทึกเวิร์กบุ๊กเป็น HTML อย่างง่ายดาย.
og_title: ส่งออกแผนภูมิเป็น PNG – แปลง Excel เป็น HTML ด้วย Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: ส่งออกแผนภูมิเป็น PNG – คู่มือเต็มสำหรับการแปลง Excel เป็น HTML ด้วย Aspose.Cells
url: /th/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ส่งออกแผนภูมิเป็น PNG – คู่มือครบวงจรในการแปลง Excel เป็น HTML ด้วย Aspose.Cells

เคยสงสัยไหมว่า **ส่งออกแผนภูมิเป็น PNG** โดยตรงจากไฟล์ Excel พร้อมกับแปลงแผ่นงานทั้งหมดเป็น HTML ที่สะอาดและตอบสนองต่ออุปกรณ์? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อต้องการรายงานพร้อมใช้งานบนเว็บที่แสดงแผนภูมิโดยไม่ต้องจัดการไฟล์รูปภาพแยกต่างหาก ข่าวดีคือ Aspose.Cells ทำให้เรื่องนี้ง่ายดาย

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนทั้งหมดเพื่อ **แปลง Excel เป็น HTML**, **ฝังรูปภาพเป็น Base64**, และสุดท้าย **บันทึกเวิร์กบุ๊กเป็น HTML** — ทั้งหมดนี้พร้อมรับประกันว่าแต่ละแผนภูมิจะถูกบันทึกเป็นไฟล์ PNG เมื่อเสร็จคุณจะได้ไฟล์ HTML เพียงไฟล์เดียวที่สามารถใส่ลงในหน้าเว็บใดก็ได้ และแผนภูมิทุกชิ้นจะแสดงทันทีโดยไม่ต้องมีไฟล์เพิ่มเติม

## สิ่งที่คุณจะได้เรียนรู้

- วิธีโหลดเวิร์กบุ๊กที่มีแผนภูมิอยู่แล้ว  
- ธง `HtmlSaveOptions` ใดที่ควบคุมการส่งออกภาพ, รูปแบบแผนภูมิ, และการตอบสนองต่ออุปกรณ์  
- โค้ดที่จำเป็นเพื่อ **ส่งออกแผนภูมิเป็น PNG** และฝัง PNG เหล่านั้นเป็นสตริง Base64  
- วิธี **บันทึกเวิร์กบุ๊กเป็น HTML** ด้วยการเรียกเมธอดเดียว  
- เคล็ดลับการแก้ไขปัญหาที่พบบ่อย เช่น รูปภาพแผนภูมิหายหรือสตริง Base64 ขนาดใหญ่เกินไป  

**ข้อกำหนดเบื้องต้น:**  
- .NET 6+ (หรือ .NET Framework 4.6+) ติดตั้งแล้ว  
- ใบอนุญาต Aspose.Cells ที่ถูกต้อง (หรือคีย์ทดลองใช้ชั่วคราว)  
- ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ที่คุณชอบ)  

หากส่วนใดส่วนหนึ่งยังไม่คุ้นเคย ให้หยุดพักและตั้งค่าให้พร้อมก่อน; ส่วนที่เหลือของคู่มือสมมติว่าคุณพร้อมแล้ว

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose.Cells

ก่อนที่เราจะ **ส่งออกแผนภูมิเป็น PNG** เราต้องมีโปรเจกต์ C# ที่อ้างอิงไลบรารี Aspose.Cells

1. เปิด Visual Studio และสร้าง **Console App** ใหม่ (`dotnet new console`)  
2. เพิ่มแพคเกจ NuGet ของ Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (ทางเลือก) หากคุณมีไฟล์ใบอนุญาต ให้วางไว้ที่โฟลเดอร์รากของโปรเจกต์และเปิดใช้งานในเวลารัน:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **เคล็ดลับ:** เก็บไฟล์ใบอนุญาตให้อยู่ไกลจากระบบควบคุมเวอร์ชัน ใช้ตัวแปรสภาพแวดล้อมหรือที่เก็บความลับที่ปลอดภัยสำหรับการใช้งานจริง

---

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กที่มีแผนภูมิอยู่

ต่อไปเราจะโหลดไฟล์ Excel ที่มีแผนภูมิที่ต้องการ **ส่งออกแผนภูมิเป็น PNG**

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **ทำไมจึงสำคัญ:** การโหลดเวิร์กบุ๊กตั้งแต่แรกทำให้เราสามารถเข้าถึงทุกชีต, แผนภูมิ, และออบเจ็กต์ฝังได้ หากเวิร์กบุ๊กโหลดไม่สำเร็จ ขั้นตอน **ส่งออกแผนภูมิเป็น PNG** ต่อไปจะไม่ทำงานเลย

---

## ขั้นตอนที่ 3: ตั้งค่า HtmlSaveOptions

หัวใจของวิธีแก้ปัญหาอยู่ที่ `HtmlSaveOptions` การสลับคุณสมบัติบางอย่างทำให้เราสามารถ:

- **ExportChartImageFormat = ImageFormat.Png** → ทำให้ทุกแผนภูมิแปลงเป็น PNG  
- **ExportImagesAsBase64 = true** → ฝังข้อมูล PNG ลงใน HTML โดยตรง ไม่ต้องมีไฟล์ภายนอก  
- **IsResponsive = true** → ทำให้ตารางที่สร้างขึ้นปรับตัวตามหน้าจอมือถือ  
- **ExportPrintingHeadersFooters = false** → ลบข้อมูลเมตาที่ใช้สำหรับการพิมพ์ออก  

นี่คือการกำหนดค่าครบถ้วน:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### ทำไมต้องตั้งค่าเหล่านี้?

- **ExportChartImageFormat = ImageFormat.Png** เป็นวิธีเดียวที่รับประกันภาพแผนภูมิที่ไม่มีการสูญเสียคุณภาพและเหมาะกับเว็บ  
- **ExportImagesAsBase64 = true** ทำให้คุณ **ฝังรูปภาพเป็น Base64** ได้ ซึ่งเหมาะกับรายงานอีเมลหรือการปรับใช้แบบไฟล์เดียว  
- **IsResponsive = true** แก้ปัญหาที่พบบ่อย: ตารางล้นบนสมาร์ทโฟน  
- **ExportPrintingHeadersFooters = false** ทำให้ HTML มีน้ำหนักเบา — ไม่มีข้อมูลพิมพ์ที่ไม่จำเป็นบนเว็บ  

---

## ขั้นตอนที่ 4: บันทึกเวิร์กบุ๊กเป็น HTML

เมื่อกำหนดค่าเรียบร้อยแล้ว บรรทัดสุดท้ายคือการเรียกเมธอดเดียวที่ทำทั้ง **แปลง Excel เป็น HTML** และ **ส่งออกแผนภูมิเป็น PNG** เบื้องหลัง

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

เมื่อบรรทัดนี้ทำงานเสร็จ คุณจะได้ไฟล์ชื่อ `Report.html` เปิดไฟล์นี้ด้วยเบราว์เซอร์ใดก็ได้ แล้วคุณจะเห็น:

- ข้อมูลทุกชีตแสดงเป็นตาราง HTML ที่สะอาด  
- แผนภูมิทุกชิ้นแสดงเป็นภาพ PNG แบบอินไลน์ (ขอบคุณการฝัง Base64)  
- ไม่มีไฟล์รูปภาพแยกอยู่ข้างๆ HTML  

### ผลลัพธ์ที่คาดหวัง

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

สังเกต attribute `src="data:image/png;base64,..."` — นั่นคือ **การฝังรูปภาพเป็น base64** ที่ทำงานอยู่ ไม่ได้สร้างไฟล์ `.png` แยกบนดิสก์

---

## ขั้นตอนที่ 5: ตรวจสอบการส่งออก PNG และปรับแต่งหากจำเป็น

บางครั้งแผนภูมิอาจดูเบลอหลังการแปลง โดยเฉพาะหากใช้ฟอนต์กำหนดเองหรือไล่สีซับซ้อน ต่อไปนี้คือวิธีตรวจสอบ:

1. เปิด HTML ที่สร้างขึ้นใน Chrome คลิกขวาที่ภาพแผนภูมิและเลือก **Open image in new tab** URL จะยังคงเริ่มต้นด้วย `data:image/png;base64,`  
2. หากภาพดูเบลอ ให้ลองเพิ่มความละเอียดของแผนภูมิก่อนบันทึก:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. สำหรับแผนภูมิที่อ้างอิงแหล่งข้อมูลภายนอก ให้แน่ใจว่าเวิร์กบุ๊กรีเฟรชเต็มที่ก่อนบันทึก:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

การปรับแต่งเหล่านี้ทำให้ขั้นตอน **ส่งออกแผนภูมิจาก Excel เป็น PNG** ให้ผลลัพธ์คมชัดพร้อมใช้งานในสภาพแวดล้อมการผลิต

---

## ขั้นตอนที่ 6: ปล่อย HTML ไปที่ไหนก็ได้

เพราะรูปภาพทั้งหมดถูกฝังไว้แล้ว คุณสามารถ:

- ส่งอีเมล HTML เป็นไฟล์แนบเดียว  
- วาง HTML ลงใน CMS ที่รับโค้ดดิบ  
- โฮสต์บนเว็บไซต์สแตติกโดยไม่ต้องกังวลไฟล์ PNG หาย  

หากคุณต้องการไฟล์ PNG แยก (เช่น สำหรับ PDF ต่อไป) คุณสามารถสลับ `ExportImagesAsBase64` เป็น `false` แล้วกำหนดโฟลเดอร์ปลายทางสำหรับรูปภาพใน `HtmlSaveOptions`

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

ตอนนี้ HTML จะอ้างอิงไฟล์ PNG ภายนอก ยังคงทำ **ส่งออกแผนภูมิเป็น PNG** แต่ให้ไฟล์ภาพแยกสำหรับการใช้งานอื่น

---

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|-------|-------------------|----------|
| แผนภูมิหายจาก HTML | `ExportChartImageFormat` ยังเป็นค่าเริ่มต้น (`Jpeg`) และเบราว์เซอร์บล็อกเนื้อหาผสม | ตั้งค่า `ExportChartImageFormat = ImageFormat.Png` |
| ไฟล์ HTML ใหญ่ (หลาย MB) | แผนภูมิขนาดใหญ่หรือหลายภาพความละเอียดสูงฝังเป็น Base64 | ลด `htmlOptions.ImageResolution` หรือบีบอัดแผนภูมิใน Excel ก่อนแปลง |
| ตารางล้นบนมือถือ | `IsResponsive` ไม่ได้เปิดใช้งาน | ตรวจสอบให้ `IsResponsive = true` ใน `HtmlSaveOptions` |
| สตริง Base64 มีอักขระขึ้นบรรทัดใหม่ | .NET เวอร์ชันเก่าอาจตัดสตริงยาว | อัปเกรดเป็น .NET 6+ หรือกำหนด `htmlOptions.ExportBase64StringInOneLine = true` |

---

## โบนัส: สร้างเมธอดที่ใช้ซ้ำได้

หากคุณต้องทำการแปลงนี้บ่อย ๆ ให้ห่อหุ้มโลจิกทั้งหมดไว้ในเมธอดหนึ่ง

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

ตอนนี้คุณสามารถเรียก `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` จากที่ใดก็ได้ในโค้ดของคุณ

---

## สรุป

คุณเพิ่งเรียนรู้วิธี **ส่งออกแผนภูมิเป็น PNG** ขณะเดียวกัน **แปลง Excel เป็น HTML**, **ฝังรูปภาพเป็น Base64**, และ **บันทึกเวิร์กบุ๊กเป็น HTML** ด้วย Aspose.Cells สิ่งสำคัญคือการตั้งค่า `HtmlSaveOptions` ที่เลือกอย่างดี ทำให้คุณได้ไฟล์ HTML เดียวที่ทำงานบนทุกอุปกรณ์ — ไม่ต้องมีไฟล์ PNG แยก ไม่ต้องจัดการโฟลเดอร์ยุ่งยาก

พร้อมรับความท้าทายต่อไปหรือยัง? ลองผสานวิธีนี้กับ **ส่งออกแผนภูมิจาก Excel เป็น PNG** สำหรับการสร้าง PDF, หรือทดลองใช้ CSS กำหนดสไตล์ตารางให้สวยขึ้น ไม่จำกัดอะไรเลยเมื่อคุณควบคุมทั้งข้อมูลและการนำเสนอด้วยโปรแกรม

หากเจออุปสรรคหรืออยากแชร์วิธีที่คุณปรับใช้ในโปรเจกต์ของคุณ อย่าลังเลที่จะคอมเมนต์ไว้ ขอบคุณและขอให้สนุกกับการโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}