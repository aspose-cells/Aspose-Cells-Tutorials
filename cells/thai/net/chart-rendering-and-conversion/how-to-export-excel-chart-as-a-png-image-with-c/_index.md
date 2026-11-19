---
category: general
date: 2026-11-19
description: วิธีส่งออกแผนภูมิ Excel เป็นภาพ PNG ด้วย Aspose.Cells เรียนรู้การบันทึกภาพแผนภูมิ
  Excel และตั้งค่ารูปแบบภาพเป็น PNG เพียงไม่กี่ขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: th
lastmod: 2026-11-19
og_description: วิธีส่งออกแผนภูมิ Excel เป็นภาพ PNG ด้วย Aspose.Cells. ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อบันทึกภาพแผนภูมิ
  Excel และตั้งค่ารูปแบบภาพเป็น PNG อย่างมีประสิทธิภาพ.
og_image_alt: How to export Excel chart as a PNG image
og_title: วิธีส่งออกแผนภูมิ Excel เป็นภาพ PNG – คู่มือ C# อย่างรวดเร็ว
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: วิธีส่งออกแผนภูมิ Excel เป็นภาพ PNG ด้วย C#
url: /th/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการส่งออกแผนภูมิ Excel เป็นภาพ PNG ด้วย C#

หากคุณต้องการ **how to export Excel chart** ไปเป็นภาพที่พกพาได้ คู่มือนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และพร้อมใช้งาน ด้วย Aspose.Cells คุณสามารถ **save Excel chart image** ในรูปแบบ PNG ได้ด้วยเพียงสามบรรทัดของโค้ด และบทแนะนำยังอธิบายวิธี **set image format png** และ **save Excel picture file** อย่างปลอดภัย

คุณจะจบบทความนี้ด้วยโปรแกรมที่สามารถรันได้ซึ่งโหลดเวิร์กบุ๊ก, แสดงผลแผนภูมิแรก, และเขียนไฟล์ `pivot.png` ไปยังดิสก์ ไม่ต้องใช้เครื่องมือเพิ่มเติม ไม่ต้องคัดลอก‑วางด้วยมือ—เพียงโค้ด C# ที่สะอาดคุณสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

## ข้อกำหนดเบื้องต้น

* .NET 6.0 SDK หรือรุ่นใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+ ได้เช่นกัน)
* Visual Studio 2022 หรือโปรแกรมแก้ไข C# ใดก็ได้
* ใบอนุญาต Aspose.Cells for .NET (หรือคีย์ประเมินผลชั่วคราว)
* ไฟล์ Excel (`pivot.xlsx`) ที่มีอย่างน้อยหนึ่งแผนภูมิในแผ่นงานแรก

รายการเหล่านี้เป็นการพึ่งพาภายนอกเพียงอย่างเดียว; บทแนะนำไม่จำเป็นต้องติดตั้ง Office บนเครื่อง

## ขั้นตอนที่ 1: ติดตั้ง Aspose.Cells

เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.Cells
```

แพ็กเกจนี้จะเพิ่มเนมสเปซ `Aspose.Cells` ซึ่งให้คลาส `Workbook`, `ImageOrPrintOptions` และคลาสอื่น ๆ ที่จำเป็นสำหรับการ **save Excel chart image**.

## ขั้นตอนที่ 2: สร้างโปรแกรมคอนโซลขนาดเล็ก

สร้างแอปคอนโซลใหม่ (`dotnet new console -n ExportChartDemo`) แล้วแทนที่ไฟล์ `Program.cs` ที่สร้างอัตโนมัติด้วยโค้ดต่อไปนี้ โปรแกรมนี้สาธิต **how to export Excel chart** และรวมคอมเมนต์ที่อธิบายแต่ละการตัดสินใจ

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### ทำไมแต่ละส่วนจึงสำคัญ

* **Loading the workbook** – `Workbook` วิเคราะห์ไฟล์ `.xlsx` โดยไม่ต้องติดตั้ง Microsoft Excel
* **ImageOrPrintOptions** – อ็อบเจกต์นี้ควบคุมรูปแบบผลลัพธ์ การตั้งค่า `ImageFormat = ImageFormat.Png` **sets image format png** ซึ่งเป็นรูปแบบที่ไม่มีการสูญเสียและได้รับการสนับสนุนอย่างกว้างขวาง
* **RenderToImage** – เมธอด `RenderToImage` แปลงแผนภูมิ (อ็อบเจกต์ `Picture`) เป็นไฟล์ภาพ เมธอดนี้ยังจัดการการสเกล, DPI, และความโปร่งใสโดยอัตโนมัติ
* **Error handling** – การตรวจสอบ `sheet.Pictures.Count == 0` ป้องกันข้อยกเว้นรันไทม์หากแผ่นงานไม่มีแผนภูมิ ซึ่งเป็นกรณีขอบที่พบบ่อยเมื่อผู้ใช้ชี้ไปยังแผ่นที่ผิด

## ขั้นตอนที่ 3: รันโปรแกรมและตรวจสอบผลลัพธ์

1. สร้างโปรเจกต์: `dotnet build`.
2. รันโปรแกรม: `dotnet run --project ExportChartDemo`.

หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะเห็น:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

เปิด `pivot.png` ด้วยโปรแกรมดูรูปภาพใดก็ได้ คุณควรเห็นการแสดงผลที่ตรงกับแผนภูมิ Excel อย่างชัดเจน ยืนยันว่าคุณได้ **saved Excel picture file** อย่างสำเร็จ

### ผลลัพธ์ที่คาดหวัง

ด้านล่างเป็นตัวอย่างของ PNG ที่ส่งออก (แผนภูมิจริงจะขึ้นอยู่กับไฟล์ต้นฉบับของคุณ).

![แผนภูมิ Excel ที่ส่งออกเป็นภาพ PNG](images/exported-chart.png){: .center alt="วิธีการส่งออกแผนภูมิ Excel เป็นภาพ PNG"}

## ขั้นตอนที่ 4: ตัวเลือกขั้นสูง – ส่งออกหลายแผนภูมิ

หากเวิร์กบุ๊กของคุณมีมากกว่าหนึ่งแผนภูมิ คุณสามารถวนลูปผ่านคอลเลกชัน `Pictures` ได้:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

รูปแบบนี้ทำให้คุณสามารถ **save Excel chart image** สำหรับทุกแผนภูมิในแผ่นงาน ซึ่งสะดวกสำหรับกระบวนการรายงาน

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| `ArgumentOutOfRangeException` on `Pictures[0]` | แผ่นงานไม่มีแผนภูมิหรือแผนภูมิอยู่บนแผ่นอื่น | ตรวจสอบดัชนีแผ่น (`Worksheets[0]`) และให้แน่ใจว่าแผนภูมิมีอยู่ ใช้ `Worksheets["SheetName"]` หากจำเป็น |
| Exported image is blurry | DPI ตั้งค่าต่ำเกินไป (ค่าเริ่มต้น 96) | เพิ่มค่า `HorizontalResolution` และ `VerticalResolution` ใน `ImageOrPrintOptions` |
| PNG file is empty or corrupted | ไม่มีใบอนุญาตทำให้เกิดข้อจำกัดการประเมินผล | ใช้ใบอนุญาต Aspose.Cells ที่ถูกต้องก่อนโหลดเวิร์กบุ๊ก (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| File path errors (`FileNotFoundException`) | ตัวแทน `YOUR_DIRECTORY` ไม่ถูกต้อง | ใช้เส้นทางแบบเต็มหรือ `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

การแก้ไขปัญหาเหล่านี้จะทำให้ประสบการณ์ **save excel picture file** ราบรื่น

## เคล็ดลับพิเศษ: ส่งออกโดยตรงไปยัง memory stream

บางครั้งคุณอาจต้องการภาพในหน่วยความจำ (เช่น เพื่ออัปโหลดไปยังเว็บ API) แทนการเขียนลงดิสก์:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

ตรรกะ **set image format png** เดียวกันยังใช้ได้; คุณเพียงเปลี่ยนเส้นทางไฟล์เป็นสตรีม

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to export Excel chart** เป็นไฟล์ PNG ด้วย Aspose.Cells สำหรับ .NET บทแนะนำได้ครอบคลุม:

* การติดตั้งไลบรารี
* การโหลดเวิร์กบุ๊ก
* **Setting image format png**
* **Saving Excel chart image** ไปยังดิสก์
* การจัดการหลายแผนภูมิและข้อผิดพลาดทั่วไป

ด้วยพื้นฐานนี้คุณสามารถผสานการส่งออกแผนภูมิเข้าสู่การรายงานอัตโนมัติ, เว็บเซอร์วิส, หรือยูทิลิตี้เดสก์ท็อป ต่อไปสำรวจหัวข้อที่เกี่ยวข้องเช่น **save excel picture file** เป็น JPEG (`ImageFormat.Jpeg`) หรือการแปลงแผนภูมิเป็น PDF สำหรับรายงานที่พิมพ์ได้

ขอให้เขียนโค้ดอย่างสนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ

- [แปลงแผนภูมิวงกลม Excel เป็นภาพโดยใช้ Aspose.Cells .NET: คู่มือขั้นตอนที่ละเอียด](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [ส่งออกแผนภูมิเป็น PNG – คู่มือครบถ้วนสำหรับแปลง Excel เป็น HTML ด้วย Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [ส่งออกเซลล์ Excel เป็นภาพโดยใช้ Aspose.Cells .NET: คู่มือขั้นตอนที่ละเอียด](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}