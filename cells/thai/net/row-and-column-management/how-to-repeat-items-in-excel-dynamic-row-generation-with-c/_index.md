---
category: general
date: 2026-03-25
description: เรียนรู้วิธีทำซ้ำรายการใน Excel ด้วย C# คู่มือนี้แสดงวิธีสร้างแถว Excel
  แบบไดนามิกและเติมข้อมูลในเทมเพลต Excel ด้วย C# สำหรับคอลเลกชันใดก็ได้.
draft: false
keywords:
- how to repeat items in excel
- generate excel rows dynamically
- populate excel template c#
language: th
og_description: วิธีทำซ้ำรายการใน Excel ด้วย C#? ติดตามบทเรียนฉบับเต็มนี้เพื่อสร้างแถว
  Excel อย่างไดนามิกและเติมข้อมูลลงในเทมเพลต Excel ด้วย C# อย่างง่ายดาย.
og_title: วิธีทำซ้ำรายการใน Excel – คู่มือ C# ทีละขั้นตอน
tags:
- C#
- Excel automation
- Aspose.Cells
title: วิธีทำซ้ำรายการใน Excel – การสร้างแถวแบบไดนามิกด้วย C#
url: /th/net/row-and-column-management/how-to-repeat-items-in-excel-dynamic-row-generation-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำซ้ำรายการใน Excel – การสร้างแถวแบบไดนามิกด้วย C#

เคยสงสัย **วิธีทำซ้ำรายการใน Excel** โดยไม่ต้องคัดลอกแถวด้วยตนเองหรือไม่? บางทีคุณอาจมีรายการสั่งซื้อที่แต่ละรายการมีหลายบรรทัด และต้องการแผ่นงานที่ขยายอัตโนมัติ ในบทแนะนำนี้คุณจะได้เห็นขั้นตอนนั้นอย่างชัดเจน: เราจะสร้างแถว Excel แบบไดนามิกและ **populate an Excel template C#** ด้วยคุณสมบัติ Smart Marker ที่ทรงพลังของ Aspose.Cells

เราจะเดินผ่านสถานการณ์จริง สร้างโมเดลข้อมูลขนาดเล็ก และดูไลบรารีแปลงเทมเพลตของเราให้เป็นชีตที่เต็มไปด้วยข้อมูล จากนั้นคุณจะสามารถทำซ้ำรายการใน Excel สำหรับคอลเลกชันใดก็ได้ ไม่ว่าจะเป็นคำสั่งเดียวหรือแคตาล็อกขนาดใหญ่ ไม่มีส่วนเกิน—เพียงโซลูชันทำงานที่คุณสามารถคัดลอก‑วางเข้าโปรเจคของคุณได้ทันที

## ความต้องการเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)
- Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ)
- **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`)
- ความเข้าใจพื้นฐานเกี่ยวกับประเภทนิรนามของ C#

หากคุณขาดส่วนใดส่วนหนึ่ง เพียงเพิ่ม NuGet package แล้วคุณก็พร้อมใช้งาน ไลบรารีเป็นแบบจัดการเต็มรูปแบบ ไม่ต้องใช้ COM interop หรือการติดตั้ง Office

---

## ขั้นตอนที่ 1: กำหนด Smart Marker Template – แกนหลักของ “ทำซ้ำรายการใน Excel”

สิ่งแรกที่เราต้องการคือเซลล์เทมเพลตที่บอก Aspose.Cells ว่าจะวนลูปผ่านคอลเลกชันของเราอย่างไร Smart Markers ใช้ไวยากรณ์ตัวแทนที่ง่ายซึ่งอยู่ภายใน worksheet โดยตรง

```csharp
// Put the template into cell A1
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +          // Start repeating the Orders collection
    "   ${Item:Repeat}\n" +        // For each Order, repeat the Item collection
    "      ${Item.Name}\n" +       // Insert the Name of each Item
    "   ${/Item}\n" +              // End Item repeat block
    "${/Orders}");                 // End Orders repeat block
```

**ทำไมจึงสำคัญ:** ตัวทำเครื่องหมาย `${Orders:Repeat}` บอกตัวประมวลผลให้วนลูปผ่านอาเรย์ `Orders` ภายในลูปนั้นเราจะเริ่มบล็อก repeat อีกอันสำหรับ `Item` ทุกครั้งที่ลูปภายในทำงาน `${Item.Name}` จะถูกแทนที่ด้วยชื่อจริง เช่น “Apple” หรือ “Banana” เมื่อประมวลผลเสร็จ เทมเพลตจะขยายเป็นแถวตามจำนวนที่ต้องการ—พอดีกับสิ่งที่คุณต้องการ **generate Excel rows dynamically**

> **เคล็ดลับ:** รักษาการเยื้องภายในสตริงไว้; มันจะแปลงเป็นการจัดตำแหน่งแถวที่ถูกต้องในชีตสุดท้าย

## ขั้นตอนที่ 2: สร้าง Data Model ที่สอดคล้อง – ทำให้ “populate excel template c#” ง่ายขึ้น

เทมเพลตของเราต้องการอ็อบเจกต์ที่มีคุณสมบัติ `Orders` โดยแต่ละออร์เดอร์มีอาเรย์ `Item` เราจะสร้างอ็อบเจกต์นิรนามที่สะท้อนโครงสร้างนี้

```csharp
// Create a simple data model that matches the template
var dataModel = new
{
    Orders = new[]
    {
        new
        {
            Item = new[]
            {
                new { Name = "Apple" },
                new { Name = "Banana" }
            }
        },
        // You can add more orders here – the template will repeat automatically
        new
        {
            Item = new[]
            {
                new { Name = "Orange" },
                new { Name = "Grape" },
                new { Name = "Mango" }
            }
        }
    }
};
```

**ทำไมจึงสำคัญ:** โครงสร้างของอ็อบเจกต์นิรนามต้องตรงกับตัวทำเครื่องหมายอย่างแม่นยำ หากคุณพลาดคุณสมบัติหรือใช้ชื่อแตกต่าง ตัวประมวลผล Smart Marker จะข้ามโดยเงียบ ทำให้แถวว่างเปล่า นี่เป็นข้อผิดพลาดทั่วไปเมื่อพยายาม **populate excel template c#** ครั้งแรก

## ขั้นตอนที่ 3: เรียกใช้ Smart Marker Processor – เครื่องยนต์ที่ทำซ้ำรายการ

ตอนนี้เรามีเทมเพลตและโมเดลข้อมูลแล้ว เราจะส่งทั้งสองให้ Aspose.Cells ตัวประมวลผลจะเดินผ่าน worksheet ขยายบล็อก repeat และเขียนค่า

```csharp
// Process the template with the data model
worksheet.SmartMarkerProcessor.Process(dataModel);
```

นี่คือทั้งหมดที่คุณต้องมีเพื่อ **ทำซ้ำรายการใน Excel** หลังจากการเรียกเสร็จ worksheet จะมี:

| A (generated) |
|---------------|
| Apple         |
| Banana        |
| Orange        |
| Grape         |
| Mango         |

แต่ละรายการจะแสดงบนแถวของมันเอง ไม่ว่าคุณจะเพิ่มออร์เดอร์หรือรายการกี่รายการก็ได้ในโมเดล

## ตัวอย่างทำงานเต็มรูปแบบ – ตั้งแต่เริ่มต้นจนจบ

ด้านล่างเป็นแอปพลิเคชันคอนโซลที่พร้อมรันครบวงจร คัดลอกไปยังโปรเจค C# ใหม่ เพิ่ม NuGet package ของ Aspose.Cells แล้วรัน ไฟล์ `Output.xlsx` จะปรากฏในโฟลเดอร์ bin

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // 2️⃣ Define the Smart Marker template (Step 1)
            worksheet.Cells["A1"].PutValue(
                "${Orders:Repeat}\n" +
                "   ${Item:Repeat}\n" +
                "      ${Item.Name}\n" +
                "   ${/Item}\n" +
                "${/Orders}");

            // 3️⃣ Build the data model (Step 2)
            var dataModel = new
            {
                Orders = new[]
                {
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Apple" },
                            new { Name = "Banana" }
                        }
                    },
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Orange" },
                            new { Name = "Grape" },
                            new { Name = "Mango" }
                        }
                    }
                }
            };

            // 4️⃣ Process the template (Step 3)
            worksheet.SmartMarkerProcessor.Process(dataModel);

            // 5️⃣ Save the result
            workbook.Save("Output.xlsx");
            Console.WriteLine("Excel file generated! Open Output.xlsx to see the repeated items.");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิด `Output.xlsx` แล้วคุณจะเห็นคอลัมน์ที่มีชื่อผลไม้ห้าชนิด แต่ละชื่ออยู่บนแถวของมันเอง ไม่ต้องคัดลอกด้วยตนเอง

### ถ้า Collection ของฉันว่าง?

หาก `Orders` หรืออาเรย์ `Item` ใดว่าง ตัวประมวลผล Smart Marker จะข้ามบล็อกนั้นโดยอัตโนมัติ ไม่สร้างแถวใด ๆ นี่เป็นประโยชน์เมื่อคุณต้อง **generate Excel rows dynamically** ตามข้อมูลที่เป็นตัวเลือก—ไม่มีข้อมูลเพิ่มเติมปรากฏ

### การจัดการชุดข้อมูลขนาดใหญ่

สำหรับแถวหลายพันแถว ตัวประมวลผลยังคงเร็วอยู่ เพราะทำงานในหน่วยความจำและเขียนโดยตรงไปยัง workbook อย่างไรก็ตาม คุณอาจต้อง:

- ปิดการคำนวณ (`workbook.CalculateFormula = false`) ก่อนประมวลผล
- ใช้ `MemoryStream` หากต้องการส่งไฟล์ผ่านเว็บ API โดยไม่ต้องเขียนลงไฟล์ระบบ

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Markers don’t expand | Misspelled property name or wrong case | Ensure the anonymous object’s property names match the markers exactly (`Orders`, `Item`, `Name`). |
| Blank rows appear | Extra newline characters inside the template string | Trim trailing `\n` or keep the template concise. |
| Processor throws `NullReferenceException` | Data model contains `null` for a collection | Guard against `null` by initializing empty arrays (`new object[0]`). |
| Output file is corrupted | Workbook not saved properly (e.g., using wrong format) | Use `workbook.Save("file.xlsx")` with the `.xlsx` extension. |

## การขยายเทมเพลต – มากกว่าชื่อเพียงอย่างเดียว

Smart Markers รองรับคุณสมบัติใดก็ได้ สูตรคำนวณ และแม้กระทั่งบล็อกเงื่อนไข ตัวอย่างเช่น การเพิ่มคอลัมน์ราคา:

```csharp
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +
    "   ${Item:Repeat}\n" +
    "      ${Item.Name}\t${Item.Price}\n" +
    "   ${/Item}\n" +
    "${/Orders}");
```

และอัปเดตโมเดลข้อมูล:

```csharp
new { Name = "Apple", Price = 0.99M },
new { Name = "Banana", Price = 0.59M }
```

ผลลัพธ์จะเป็นสองคอลัมน์—หนึ่งสำหรับชื่อ อีกหนึ่งสำหรับราคา—อีกครั้งที่ถูกสร้าง **dynamically**

## สรุป

ตอนนี้คุณมีโซลูชันครบวงจรและอิสระสำหรับ **วิธีทำซ้ำรายการใน Excel** ด้วย C# โดยการกำหนด Smart Marker template, สร้างโมเดลข้อมูลที่สอดคล้อง, และเรียก `SmartMarkerProcessor.Process` คุณสามารถ **generate Excel rows dynamically** สำหรับคอลเลกชันใดก็ได้และ **populate excel template c#** ได้อย่างง่ายดาย

ต่อไปคุณจะทำอะไร? ลองเพิ่มผลรวม, การจัดรูปแบบตามเงื่อนไข, หรือส่งออกข้อมูลเดียวกันเป็น CSV รูปแบบเดียวกันทำงานกับคอลเลกชันซ้อนกัน, การจัดกลุ่ม, และแม้กระทั่งอ็อบเจกต์แบบกำหนดเอง—ดังนั้นอย่ากลัวที่จะทดลอง

หากคุณพบว่าคู่มือนี้เป็นประโยชน์ อย่าลืมกดดาวบน GitHub, แชร์ให้เพื่อนร่วมทีม, หรือแสดงความคิดเห็นด้านล่าง ขอให้เขียนโค้ดอย่างสนุกและเพลิดเพลินกับพลังของการสร้าง Excel อัตโนมัติ!

![ภาพหน้าจอของแถว Excel ที่สร้างขึ้นแสดงวิธีทำซ้ำรายการใน Excel](/images/repeat-items-excel.png "วิธีทำซ้ำรายการใน Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}