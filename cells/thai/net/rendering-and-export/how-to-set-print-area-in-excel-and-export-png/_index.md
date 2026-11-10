---
category: general
date: 2026-09-27
description: ตั้งค่าพื้นที่พิมพ์ใน Excel และเรียนรู้วิธีส่งออกภาพ PNG ของเซลล์ที่เลือก
  คู่มือนี้ยังครอบคลุมการบันทึกช่วงเป็นภาพและการเพิ่มรูปภาพลงในแผ่นงาน
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: th
lastmod: 2026-09-27
og_description: กำหนดพื้นที่พิมพ์ใน Excel และส่งออกเป็น PNG ด้วย Aspose.Cells ทำตามคู่มือขั้นตอนนี้เพื่อบันทึกช่วงเป็นภาพและเพิ่มรูปภาพลงในแผ่นงาน
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: ตั้งค่าพื้นที่พิมพ์ใน Excel – ส่งออก PNG ด้วย C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: วิธีตั้งพื้นที่พิมพ์ใน Excel และส่งออกเป็น PNG
url: /th/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งพื้นที่พิมพ์ใน Excel และส่งออกเป็น PNG

หากคุณต้องการ **set print area excel** ก่อนสร้างภาพ คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าต้องทำอย่างไร คุณยังจะได้เรียนรู้ **how to export png** จากช่วงที่กำหนด, **save range as image**, และ **add picture to worksheet** ในกระบวนการทำงานเดียวที่ทำซ้ำได้

การทำงานกับ Excel อย่างโปรแกรมมิ่งมักหมายถึงคุณต้องการเพียงส่วนย่อยของเซลล์—เช่น ตาราง Pivot หรือแผนภูมิ—ให้กลายเป็นภาพ การกำหนดพื้นที่พิมพ์ก่อนจะทำให้มั่นใจว่าภาพ PNG ที่ส่งออกมาจะมีเฉพาะเซลล์ที่คุณต้องการเท่านั้น ไม่มากกว่าหรือไม่น้อยกว่า บทเรียนนี้จะพาคุณผ่านทุกขั้นตอน ตั้งแต่การโหลดเวิร์กบุ๊กจนถึงการบันทึกไฟล์ PNG สุดท้าย พร้อมอธิบายว่าการตั้งค่าแต่ละอย่างมีความสำคัญอย่างไร

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า ที่ติดตั้งแล้ว  
* Visual Studio 2022 (หรือ IDE C# ใดก็ได้)  
* The **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`)  
* ไฟล์ Excel (`input.xlsx`) ที่อยู่ในไดเรกทอรีที่ทราบ  

ข้อกำหนดเหล่านี้ทำให้โค้ดทำงานได้โดยไม่ต้องกำหนดค่าเพิ่มเติม

## ขั้นตอนที่ 1: โหลดเวิร์กบุ๊กที่คุณต้องการทำงานด้วย

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

คลาส `Workbook` แทนไฟล์ Excel ทั้งไฟล์ การโหลดก่อนทำให้คุณเข้าถึง worksheets, cells, และตัวเลือกการตั้งค่าหน้ากระดาษได้

## ขั้นตอนที่ 2: **Set print area excel** สำหรับช่วงเป้าหมาย

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

การตั้งค่า **print area** บอก Excel (และ Aspose.Cells) ว่าเซลล์ใดเป็นส่วนของหน้าที่พิมพ์ได้ เมื่อคุณส่งออกแผ่นงานเป็นภาพในภายหลัง จะเรนเดอร์เฉพาะพื้นที่นี้เท่านั้น ซึ่งเป็นสิ่งจำเป็นสำหรับการ **export selected cells image** ที่สะอาดตา

## ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการส่งออกภาพ – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` ควบคุมรูปแบบผลลัพธ์ โดยเลือก `ImageFormat.Png` คุณจะได้ภาพความละเอียดสูงพร้อมพื้นหลังโปร่งใสที่ทำงานได้ดีในเว็บและเดสก์ท็อป

## ขั้นตอนที่ 4: สร้างรูปภาพจากช่วงที่กำหนดและ **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

เมธอด `Pictures.Add` แทรกรูปภาพใหม่ลงใน worksheet โดยส่งผ่านช่วงที่สร้างในขั้นตอน 2 คุณจึง **save range as image** โดยตรงบนแผ่นงาน ซึ่งมีประโยชน์หากต้องอ้างอิงรูปภาพในส่วนอื่นของเวิร์กบุ๊กต่อไป

## ขั้นตอนที่ 5: **Save the picture as an image file** – สรุปกระบวนการ **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

การเรียก `Save` จะเขียนรูปภาพลงในระบบไฟล์โดยใช้ตัวเลือกที่กำหนดในขั้นตอน 3 ไฟล์ `selected_range.png` ที่ได้จะมีเซลล์ที่กำหนดโดยคำสั่ง **set print area excel** เท่านั้น

## ตัวอย่างเต็มที่สามารถรันได้

การรวมส่วนต่าง ๆ เข้าด้วยกันจะได้โปรแกรมกะทัดรัดที่สามารถวางลงในแอปพลิเคชันคอนโซลใดก็ได้:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

Running the program prints:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

และคุณจะพบไฟล์ `selected_range.png` ที่แสดงเฉพาะเซลล์ A1 ถึง G20 จาก `input.xlsx`

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| ภาพที่ส่งออกแสดงทั้งแผ่นงาน | ไม่ได้กำหนดพื้นที่พิมพ์ | ตรวจสอบให้แน่ใจว่าคุณ **set print area excel** ก่อนสร้างรูปภาพ |
| PNG เบลอ | DPI เริ่มต้นต่ำ | ตั้งค่า `imageOptions.DpiX` และ `imageOptions.DpiY` ให้สูงขึ้น (เช่น 300) |
| เกิดข้อผิดพลาดไฟล์ไม่พบ | เส้นทางไดเรกทอรีผิด | ใช้ `Path.Combine` หรือตรวจสอบให้แน่ใจว่าโฟลเดอร์มีอยู่ |
| รูปภาพแสดงตำแหน่งผิด | ดัชนีแถว/คอลัมน์ไม่ถูกต้อง | พารามิเตอร์สองตัวแรกของ `Pictures.Add` คือเซลล์บน‑ซ้ายที่วางรูปภาพ; ตั้งค่าเป็น `0,0` เพื่อการส่งออกที่สะอาด |

## เคล็ดลับพิเศษ: ส่งออกหลายช่วงในการทำงานครั้งเดียว

หากคุณต้องการ **export selected cells image** สำหรับหลายพื้นที่ ให้ทำซ้ำขั้นตอน 2‑5 ภายในลูปและเปลี่ยนค่า `printArea` ในแต่ละรอบ จำเป็นต้องตั้งชื่อไฟล์รูปภาพให้ไม่ซ้ำกัน ไม่เช่นนั้นการบันทึกครั้งต่อมาจะเขียนทับไฟล์ก่อนหน้า

## สรุป

คุณได้เรียนรู้วิธี **set print area excel**, กำหนดค่า **how to export png**, **save range as image**, และ **add picture to worksheet** ด้วย Aspose.Cells โซลูชันแบบครบวงจรนี้ทำให้คุณแปลงบล็อกเซลล์ใด ๆ ให้เป็น PNG คุณภาพสูงได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C#

ต่อไปคุณอาจสำรวจ:

* เพิ่มขอบหรือลายน้ำให้ PNG ที่ส่งออก (ค้นหา *add picture to worksheet* พร้อมสไตล์)
* ส่งออกโดยตรงเป็น PDF สำหรับรายงานที่พิมพ์ได้ (*export selected cells image* → กระบวนการ PDF)
* ทำอัตโนมัติสำหรับหลายเวิร์กบุ๊กในงานแบตช์

ทดลองปรับช่วง, การตั้งค่า DPI, หรือรูปแบบภาพต่าง ๆ ให้เหมาะกับความต้องการของโครงการของคุณได้เลย Happy coding!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการใช้งานอื่น ๆ ในโปรเจกต์ของคุณ

- [ตั้งพื้นที่พิมพ์ใน Excel และส่งออกเป็น PowerPoint – คู่มือแบบขั้นตอน](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [ส่งออกพื้นที่พิมพ์ของ Excel เป็น HTML ด้วย Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [วิธีตั้งพื้นที่พิมพ์ใน Excel ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}