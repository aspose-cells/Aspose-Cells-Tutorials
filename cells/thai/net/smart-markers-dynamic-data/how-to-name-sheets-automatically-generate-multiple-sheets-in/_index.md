---
category: general
date: 2026-02-09
description: วิธีตั้งชื่อแผ่นงานใน C# ด้วย SmartMarker – เรียนรู้การสร้างหลายแผ่นงานและทำให้การตั้งชื่อแผ่นงานเป็นอัตโนมัติในไม่กี่บรรทัดของโค้ด
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: th
og_description: วิธีตั้งชื่อแผ่นงานใน C# ด้วยตัวเลือก SmartMarker คู่มือนี้แสดงวิธีสร้างหลายแผ่นงานและทำให้การตั้งชื่อแผ่นงานเป็นอัตโนมัติอย่างง่ายดาย
og_title: วิธีตั้งชื่อแผ่นงานอัตโนมัติ – คู่มือ C# อย่างรวดเร็ว
tags:
- C#
- Aspose.Cells
- Excel automation
title: วิธีตั้งชื่อแผ่นงานอัตโนมัติ – สร้างหลายแผ่นงานใน C#
url: /th/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งชื่อชีตอัตโนมัติ – สร้างหลายชีตใน C#

เคยสงสัย **วิธีตั้งชื่อชีต** ในไฟล์ Excel workbook โดยไม่ต้องคลิก “Rename” ด้วยตนเองทุกครั้งหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์การรายงานคุณอาจต้องจัดการกับชีตรายละเอียดหลายสิบชีตที่ต้องการชื่อที่เป็นระบบ และการทำด้วยมือเป็นเรื่องน่าอับอาย  

ข่าวดีคือ ด้วยเพียงไม่กี่บรรทัดของ C# คุณสามารถ **สร้างหลายชีต** และ **อัตโนมัติการตั้งชื่อชีต** ให้ทุกชีตรายละเอียดใหม่มีรูปแบบที่คาดเดาได้ ในบทแนะนำนี้เราจะเดินผ่านโซลูชันเต็มรูปแบบ อธิบายเหตุผลของแต่ละส่วน และให้ตัวอย่างโค้ดที่พร้อมรัน

## สิ่งที่คู่มือนี้ครอบคลุม

* การตั้งค่า workbook ที่มี SmartMarkers
* การกำหนดค่า `SmartMarkerOptions` เพื่อควบคุมชื่อฐานของชีตที่สร้างขึ้น
* การเรียก `ProcessSmartMarkers` เพื่อให้ไลบรารีสร้าง `Detail`, `Detail_1`, `Detail_2`, … โดยอัตโนมัติ
* เคล็ดลับการจัดการกรณีขอบเขต เช่น ชื่อชีตที่มีอยู่แล้วหรือรูปแบบการตั้งชื่อที่กำหนดเอง
* ตัวอย่างเต็มที่สามารถคัดลอกไปวางใน Visual Studio และเห็นผลลัพธ์ทันที

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose.Cells มาก่อน—แค่การตั้งค่า C# เบื้องต้นและ IDE ที่คุณชอบ

## ข้อกำหนดเบื้องต้น

| ความต้องการ | เหตุผลที่สำคัญ |
|-------------|----------------|
| .NET 6.0 หรือใหม่กว่า | ฟีเจอร์ภาษาใหม่และความเข้ากันได้ของไลบรารี |
| Aspose.Cells for .NET (แพ็คเกจ NuGet) | ให้การประมวลผล `SmartMarker` และการสร้างชีต |
| โปรเจกต์คอนโซลเปล่า (หรือแอป .NET ใดก็ได้) | เป็นที่ที่เราจะรันโค้ด |

ติดตั้งไลบรารีด้วย:

```bash
dotnet add package Aspose.Cells
```

เมื่อเราครอบคลุมพื้นฐานแล้ว ไปสู่การทำงานจริงกันเถอะ

## ขั้นตอนที่ 1: สร้าง Workbook ที่มี SmartMarkers

ก่อนอื่นเราต้องมี workbook ที่มีตัวแทน SmartMarker คิดว่า SmartMarker เป็นแท็กเทมเพลตที่บอกเอนจินว่าจะใส่ข้อมูลที่ไหนและในกรณีของเราเมื่อไหร่ที่จะสร้างชีตใหม่

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **เคล็ดลับ:** ทำให้ชีตเทมเพลตมีน้ำหนักเบา แค่แถวที่ต้องทำซ้ำเท่านั้นที่ควรมี SmartMarkers; ส่วนอื่น ๆ ควรคงเป็นคงที่

## ขั้นตอนที่ 2: กำหนดค่า SmartMarker Options – แกนหลักของการตั้งชื่อชีต

ต่อมาคือจุดสำคัญ โดยการตั้งค่า `DetailSheetNewName` เราบอกเอนจินว่าจะใช้ชื่อฐานอะไรสำหรับแต่ละชีตที่สร้าง ไลบรารีจะต่อ “_1”, “_2” ฯลฯ เมื่อชื่อฐานนั้นมีอยู่แล้ว

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

หากคุณต้องการรูปแบบอื่น (เช่น “Report_2023”) เพียงเปลี่ยนสตริงนั้น เอนจินจะจัดการการชนกันโดยอัตโนมัติ ซึ่งเป็นเหตุผลที่วิธีนี้ **อัตโนมัติการตั้งชื่อชีต** โดยไม่ต้องเขียนโค้ดเพิ่มเติม

## ขั้นตอนที่ 3: ประมวลผล SmartMarkers และสร้างชีต

เมื่อ workbook, ข้อมูล, และตัวเลือกพร้อมแล้ว การเรียกเมธอดเดียวก็ทำงานหนักทั้งหมดให้เสร็จ

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด *GeneratedSheets.xlsx* คุณจะเห็น:

| ชื่อชีต | เนื้อหา |
|------------|---------|
| Template   | โครงร่างมาร์กเกอร์ดั้งเดิม (เก็บไว้เพื่ออ้างอิง) |
| Detail     | ชุดแถวแรก (Apple, Banana, Cherry) |
| Detail_1   | สำเนาที่สอง – ข้อมูลเดียวกัน (มีประโยชน์เมื่อมีหลายคอลเลกชัน) |
| Detail_2   | …ต่อไปตามจำนวนกลุ่ม SmartMarker ที่แตกต่างกัน |

รูปแบบการตั้งชื่อ (`Detail`, `Detail_1`, `Detail_2`) แสดง **วิธีตั้งชื่อชีต** อย่างโปรแกรมเมติกพร้อมกับ **การสร้างหลายชีต** ตามที่ต้องการ

## กรณีขอบเขตและรูปแบบต่าง ๆ

### 1. ชื่อชีตที่มีอยู่แล้ว

หาก workbook ของคุณมีชีตชื่อ “Detail” อยู่แล้ว เอนจินจะเริ่มที่ “Detail_1” เพื่อป้องกันการเขียนทับโดยไม่ตั้งใจ

### 2. รูปแบบการเพิ่มเลขแบบกำหนดเอง

ต้องการ “Detail‑A”, “Detail‑B” แทนเลขหรือไม่? คุณสามารถประมวลผลชื่อหลังจาก `ProcessSmartMarkers` ได้:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. กลุ่ม SmartMarker หลายกลุ่ม

หาก workbook ของคุณมีมากกว่าหนึ่งกลุ่ม SmartMarker (เช่น `{{invoice}}` และ `{{detail}}`) แต่ละกลุ่มจะสร้างชุดชีตของตนเองโดยอิงจาก `DetailSheetNewName` เดียวกัน หากต้องการให้แต่ละกลุ่มมีคำนำหน้าแตกต่างกัน ให้สร้างอินสแตนซ์ `SmartMarkerOptions` แยกกันและเรียก `ProcessSmartMarkers` สำหรับแต่ละคอลเลกชัน

## เคล็ดลับจากสนามจริง

* **เคล็ดลับ:** ปิด `AllowDuplicateNames` ใน `WorkbookSettings` หากคุณต้องการให้ไลบรารีโยนข้อยกเว้นแทนการเปลี่ยนชื่อชีตโดยเงียบ ๆ วิธีนี้ช่วยจับบั๊กของตรรกะการตั้งชื่อได้ตั้งแต่แรก
* **ระวัง:** ชื่อฐานที่ยาวเกินไป Excel จำกัดชื่อชีตที่ 31 ตัวอักษร; ไลบรารีจะตัดให้โดยอัตโนมัติ แต่คุณอาจเจอชื่อที่คลุมเครือ
* **หมายเหตุประสิทธิภาพ:** การสร้างหลายร้อยชีตอาจใช้หน่วยความจำมาก ควรทำ `wb.Dispose()` ทันทีเมื่อเสร็จ หากรันในบริการที่อายุการทำงานยาว

## ภาพรวมเชิงภาพ

![แผนภาพการตั้งชื่อชีต](image.png "แผนภาพแสดงกระบวนการจากเทมเพลต SmartMarker ไปยังชีตที่สร้าง – วิธีตั้งชื่อชีต")

*Alt text includes the primary keyword to satisfy SEO.*

## โค้ดเต็ม (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

รันโปรแกรม เปิดไฟล์ที่สร้างขึ้น และคุณจะเห็นชีตที่ตั้งชื่ออัตโนมัติตามรูปแบบที่เรากำหนด

## สรุป

คุณได้เรียนรู้ **วิธีตั้งชื่อชีต** ใน workbook C# แล้ว, **วิธีสร้างหลายชีต** ด้วย SmartMarker, และ **วิธีอัตโนมัติการตั้งชื่อชีต** เพื่อไม่ต้องเปลี่ยนชื่อด้วยมืออีกต่อไป วิธีนี้สามารถขยายจากไม่กี่หน้าไปจนถึงหลายร้อยหน้า และรูปแบบเดียวกันทำงานกับคอลเลกชันใด ๆ ที่คุณส่งเข้า `ProcessSmartMarkers`

ต่อไปทำอะไรดี? ลองเปลี่ยนแหล่งข้อมูลเป็นการ query จากฐานข้อมูล, ทดลองรูปแบบ suffix ที่กำหนดเอง, หรือเชื่อมหลายกลุ่ม SmartMarker เพื่อสร้างเครื่องมือรายงานเต็มรูปแบบ ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อให้ไลบรารีจัดการงานตั้งชื่อที่ทำซ้ำ ๆ  

หากคุณพบว่าคู่มือนี้เป็นประโยชน์ อย่าลืมกดดาวบน GitHub, แชร์กับทีม, หรือแสดงความคิดเห็นด้านล่างพร้อมเทคนิคการตั้งชื่อของคุณเอง ขอให้เขียนโค้ดอย่างสนุกสนาน!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}