---
category: general
date: 2026-02-14
description: สร้างอ็อบเจ็กต์ข้อมูลหลักใน C# และสร้างแผ่นรายละเอียดได้อย่างง่ายดาย
  เรียนรู้กระบวนการทำงานของ SmartMarker อย่างเต็มรูปแบบพร้อมตัวอย่างโค้ดที่ใช้งานได้จริง
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: th
og_description: สร้างอ็อบเจ็กต์ข้อมูลหลักใน C# และสร้างแผ่นรายละเอียดด้วย SmartMarker.
  ปฏิบัติตามบทแนะนำโดยละเอียดของเราเพื่อรับโซลูชันที่พร้อมใช้งานทันที.
og_title: สร้างอ็อบเจ็กต์ข้อมูลหลัก – คู่มือฉบับสมบูรณ์
tags:
- C#
- SmartMarker
- Excel Automation
title: สร้างวัตถุข้อมูลหลัก – คู่มือขั้นตอนต่อขั้นตอนในการสร้างแผ่นรายละเอียด
url: /th/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Master Data Object – การสอนแบบครบถ้วน

เคยต้อง **สร้าง master data object** สำหรับแผ่นงาน Excel แต่ไม่แน่ใจว่าจะเชื่อมต่อกับแผ่นรายละเอียด SmartMarker อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายสถานการณ์การรายงาน master object จะเป็นตัวขับเคลื่อนแผ่นรายละเอียดแบบไดนามิก และการต่อสายให้ถูกต้องอาจรู้สึกเหมือนประกอบปริศนาโดยไม่มีรูปภาพ  

ในคู่มือนี้เราจะเดินผ่านกระบวนการทั้งหมด—การสร้าง master data object, การกำหนดค่า SmartMarker options เพื่อ **สร้างแผ่นรายละเอียด**, และสุดท้ายการเรียกใช้ processor. เมื่อเสร็จคุณจะได้โค้ดสั้น ๆ ที่สามารถวางลงในโปรเจกต์ .NET ใด ๆ ที่ใช้ไลบรารี GrapeCity Documents for Excel (GcExcel)

## สิ่งที่คุณต้องมี

- .NET 6+ (หรือ .NET Framework 4.7.2) พร้อมอ้างอิง `GcExcel.dll`
- ความคุ้นเคยพื้นฐานกับ C# (ตัวแปร, anonymous types, object initializers)
- ไฟล์ Excel ที่มีแท็ก SmartMarker เช่น `{{OrderId}}` และตารางสำหรับรายการสินค้า
- Visual Studio, Rider, หรือเครื่องมือแก้ไขที่คุณชอบ

แค่นั้น—ไม่มีแพ็กเกจ NuGet เพิ่มเติมนอกจากการแจกจ่ายหลักของ GcExcel

## ขั้นตอนที่ 1: สร้าง Master Data Object

สิ่งแรกที่คุณต้องทำคือ **สร้าง master data object** ที่สะท้อนโครงสร้างที่แท็ก SmartMarker คาดหวัง คิดว่าเป็นโมเดลรายงานขนาดเล็กในหน่วยความจำ

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

ทำไมต้องใช้ anonymous type ที่นี่? เพราะมันทำให้คุณกำหนดคอนเทนเนอร์เบา ๆ ได้โดยไม่ต้องประกาศคลาสเต็มรูปแบบ—เหมาะสำหรับการสาธิตอย่างรวดเร็วหรือเมื่อรูปแบบข้อมูลคาดว่าจะไม่เปลี่ยนแปลง หากคุณต้องการโมเดลที่นำกลับมาใช้ใหม่ในภายหลัง เพียงเปลี่ยน `var` เป็น POCO ที่เหมาะสม

> **เคล็ดลับ:** ให้ชื่อคุณสมบัติ (`OrderId`, `Product`, `Quantity`) ตรงกับตัวแปรในแผ่นงานของคุณ; SmartMarker จะจับคู่โดยไม่สนใจตัวพิมพ์ใหญ่‑เล็ก

## ขั้นตอนที่ 2: กำหนดค่า SmartMarker Options เพื่อสร้างแผ่นรายละเอียด

ต่อไปเราบอก SmartMarker ว่าเราต้องการแผ่นงานแยกสำหรับตารางรายการสินค้า นี่คือจุดที่คีย์เวิร์ด **generate detail sheet** เข้ามามีบทบาท

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

รูปแบบ `DetailSheetNewName` ใช้ตัวแปรในวงเล็บปีกกาที่จะถูกแทนที่ขณะรัน ในตัวอย่างของเราแผ่นจะถูกตั้งชื่อว่า `Order_1`. หากคุณวนลูปหลายคำสั่งซื้อในภายหลัง แต่ละคำสั่งซื้อจะได้แท็บของตัวเอง—ตรงกับที่นักบัญชีส่วนใหญ่คาดหวัง

## ขั้นตอนที่ 3: รัน SmartMarker Processor

เมื่อข้อมูลและตัวเลือกพร้อมแล้ว ขั้นตอนสุดท้ายคือการเรียกใช้ processor บนแผ่นงานเป้าหมาย

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

เบื้องหลัง SmartMarker จะสแกนแผ่นงานเพื่อหาตำแหน่งแท็ก, แทรกค่า `orderData` และเนื่องจาก `DetailSheet` ตั้งเป็น `true` มันจะคัดลอกเทมเพลตไปยังแผ่นใหม่ชื่อ `Order_1`. รายการสินค้าทั้งหมดจะแสดงในพื้นที่รายละเอียด พร้อมคงรูปแบบที่คุณตั้งค่าไว้ในเทมเพลต

### ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมคอนโซลที่ทำงานอิสระ เปิดไฟล์เทมเพลต (`Template.xlsx`), รันสามขั้นตอน, แล้วบันทึกผลลัพธ์เป็น `Result.xlsx`. คุณสามารถคัดลอก‑วางโค้ดนี้ลงในโปรเจกต์คอนโซลใหม่และกด **F5**

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### ผลลัพธ์ที่คาดหวัง

- **Result.xlsx** มีแผ่นชื่อ `Order_1`.
- เซลล์ `A1` (หรือที่คุณวาง `{{OrderId}}`) ตอนนี้แสดงค่า `1`.
- ตารางที่เริ่มต้นที่บล็อก SmartMarker แสดงสองแถว:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

เมื่อเปิดไฟล์ คุณจะเห็นรูปแบบจากเทมเพลตยังคงอยู่—เส้นขอบ, ฟอนต์, conditional formatting—all intact.

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้ามีหลายคำสั่งซื้อจะทำอย่างไร?

ห่อ master object ไว้ในคอลเลกชันและให้ SmartMarker ทำการวนซ้ำอัตโนมัติ:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

แต่ละคำสั่งซื้อจะสร้างแผ่นของตัวเอง (`Order_1`, `Order_2`, …). Processor จะถืออาเรย์ภายนอกเป็นคอลเลกชัน master

### จะควบคุมตำแหน่งของแผ่นได้อย่างไร?

ตั้งค่า `smartMarkerOptions.DetailSheetInsertIndex = 2;` เพื่อวางแผ่นใหม่หลังแท็บที่สอง, หรือใช้ `DetailSheetInsertAfter = "Summary"` เพื่อแทรกหลังแผ่นที่มีชื่อว่า Summary

### สามารถปิดการสร้างแผ่นรายละเอียดสำหรับการรันนี้ได้หรือไม่?

เพียงตั้งค่า `DetailSheet = false;`. SmartMarker จะเขียนรายการสินค้าลงในแผ่นเดียวกับที่มีแท็ก master อยู่

### ถ้าข้อมูลมีขนาดใหญ่จะทำอย่างไร?

SmartMarker สตรีมข้อมูลอย่างมีประสิทธิภาพ, แต่หากเกินหลายแสนแถวอาจถึงขีดจำกัด 1,048,576 แถวของ Excel. ในกรณีนั้นให้แยกข้อมูลเป็นหลาย master record หรือพิจารณาเอ็กซ์พอร์ตเป็น CSV

## ภาพรวมเชิงภาพ

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*ภาพแสดงกระบวนการจาก C# master object → SmartMarker options → การประมวลผลแผ่นงาน → แผ่นรายละเอียดใหม่*

## สรุป

คุณได้เรียนรู้วิธี **สร้าง master data object** ใน C# และกำหนดค่า SmartMarker เพื่อ **สร้างแผ่นรายละเอียด** อัตโนมัติ รูปแบบสามขั้นตอน—data, options, processor—ครอบคลุมสถานการณ์ส่วนใหญ่ของการอัตโนมัติ Excel ด้วย GcExcel  

ต่อจากนี้คุณอาจสำรวจต่อ:

- เพิ่มข้อมูล header/footer ให้แต่ละแผ่นรายละเอียด
- ใช้ conditional formatting ตามสถานะคำสั่งซื้อ
- ส่งออกไฟล์ที่สร้างเป็น PDF ด้วย `workbook.SaveAsPdf(...)`

ลองทดลอง, ทำให้เกิดข้อผิดพลาด, แล้วแก้ไขกลับมา นั่นคือวิธีที่เร็วที่สุดในการเชี่ยวชาญการอัตโนมัติแผ่นงาน. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}