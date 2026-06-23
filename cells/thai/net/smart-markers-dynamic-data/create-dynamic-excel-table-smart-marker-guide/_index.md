---
category: general
date: 2026-05-23
description: สร้างตาราง Excel แบบไดนามิกโดยใช้เทมเพลตและข้อมูล JSON เรียนรู้วิธีโหลดเทมเพลต
  Excel, ทำอัตโนมัติรายงาน Excel, และเติมข้อมูล Excel จาก JSON อย่างรวดเร็ว.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: th
og_description: สร้างตาราง Excel แบบไดนามิกในไม่กี่นาทีด้วยเทมเพลตและ JSON. บทเรียนนี้แสดงวิธีโหลดเทมเพลต
  Excel, ทำอัตโนมัติรายงาน Excel, และเติมข้อมูล Excel จาก JSON.
og_title: สร้างตาราง Excel แบบไดนามิก – คู่มือ Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: สร้างตาราง Excel แบบไดนามิก – คู่มือ Smart Marker
url: /th/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างตาราง Excel แบบไดนามิก – คู่มือ Smart Marker

เคยต้องการ **create dynamic excel table** ที่ขยายอัตโนมัติสำหรับแต่ละบันทึกในชุดข้อมูลของคุณหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะสร้างแดชบอร์ดการขายรายเดือนหรือชุดใบแจ้งหนี้ตามลูกค้า ความสามารถในการ **populate excel from json** โดยไม่ต้องเขียนลูปที่ไม่มีที่สิ้นสุดสามารถประหยัดเวลาหลายชั่วโมงได้

ในบทแนะนำนี้ เราจะพาคุณผ่านโซลูชันครบวงจรแบบทำมือที่แสดงวิธี **load excel template**, ฝัง Smart Marker, ป้อน JSON ให้มัน, และสุดท้ายสร้างรายงาน **automate excel report**. เมื่อเสร็จคุณจะมีโปรเจกต์ .NET ที่พร้อมรันซึ่งสร้างไฟล์ Excel ที่สวยงามจาก JSON payload เพียงหนึ่งชุด.

---

## สิ่งที่คุณต้องการ

- **Aspose.Cells for .NET** (หรือไลบรารีใด ๆ ที่รองรับ Smart Markers) ตัวอย่างใช้เวอร์ชัน 24.5 แต่เวอร์ชันล่าสุดใด ๆ ก็ทำงานได้
- Visual Studio 2022 (หรือ IDE C# ที่คุณชื่นชอบ)
- ไฟล์เทมเพลต Excel อย่างง่าย (`template.xlsx`) ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม
- สตริง JSON ที่มีคอลเลกชันชื่อ `Customers`

เท่านี้—ไม่มีบริการเพิ่มเติม, ไม่มีการเชื่อมต่อฐานข้อมูล, เพียงแค่โค้ดเท่านั้น

---

## ขั้นตอนที่ 1: สร้าง Template Workbook – Load Excel Template

สิ่งแรกที่เราทำคือ **load excel template** ลงในหน่วยความจำ คิดว่าเทมเพลตเป็นผืนผ้าใบที่มีตัวแทนพิเศษบอกโปรเซสเซอร์ว่าจะทำซ้ำแถวที่ไหน.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** การโหลดเทมเพลตเพียงครั้งเดียวทำให้การอ่าน/เขียนไฟล์เหลือน้อยที่สุดและให้คุณใช้เลเอาต์เดียวกันซ้ำหลายรายงาน นอกจากนี้ยังแยกตรรกะ Smart Marker ออกจากโค้ดส่วนอื่น ซึ่งเป็นการแยกความรับผิดชอบที่ชัดเจน

---

## ขั้นตอนที่ 2: แทรก Smart Marker – Create Dynamic Excel Table

ตอนนี้เราฝัง **Smart Marker** ที่จะทำซ้ำตารางสำหรับแต่ละรายการในคอลเลกชัน `Customers` ไวยากรณ์ `${Customers.RepeatWorksheet}` บอก Aspose.Cells ให้คัดลอกเวิร์กชีตทั้งหมดสำหรับแต่ละลูกค้า.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Pro tip:** หากคุณต้องการทำซ้ำแค่แถวแทนการทำซ้ำทั้งเวิร์กชีต ให้ใช้ `${Customers.Repeat}` บนแถวแรกของตาราง การทำซ้ำระดับเวิร์กชีตเป็นประโยชน์เมื่อแต่ละลูกค้าได้แท็บของตัวเอง

---

## ขั้นตอนที่ 3: เตรียม SmartMarkerProcessor – Automate Excel Report

เมื่อมีมาร์คเกอร์อยู่แล้ว เราจะสร้าง `SmartMarkerProcessor` วัตถุนี้จัดการการผูกข้อมูลระหว่าง JSON กับเทมเพลต Excel

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Processor นี้มีน้ำหนักเบา; คุณสามารถใช้ซ้ำสำหรับหลาย JSON payload ได้หากต้องการ

---

## ขั้นตอนที่ 4: ป้อนข้อมูล JSON – Populate Excel from JSON

นี่คือจุดที่เวทมนต์เกิดขึ้น เราป้อนสตริง JSON ที่มีอาร์เรย์ของลูกค้า แต่ละลูกค้าอาจมีฟิลด์เช่น `Name`, `Email`, และ `Total`

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Why JSON?** JSON เป็นภาษาที่ไม่ขึ้นกับภาษาและง่ายต่อการสร้างจาก API, ฐานข้อมูล หรือแม้แต่การป้อนข้อมูลด้วยตนเอง การใช้ `ApplyJson` หมายความว่าคุณไม่ต้องแมปอ็อบเจกต์ด้วยตนเอง; Processor จะทำงานหนักให้

---

## ขั้นตอนที่ 5: บันทึกผลลัพธ์ – Generate Excel Report JSON

สุดท้าย เราเขียนเวิร์กบุ๊กที่เติมข้อมูลแล้วลงดิสก์ ไฟล์ผลลัพธ์ตอนนี้มีเวิร์กชีตแยกสำหรับแต่ละลูกค้า แต่ละเวิร์กชีตเต็มด้วยข้อมูลจาก JSON ของเรา

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### ผลลัพธ์ที่คาดหวัง

- **output.xlsx** จะมีสามเวิร์กชีตชื่อ `Sheet1`, `Sheet2`, `Sheet3` (หรือชื่อใดก็ได้ตามรูปแบบการตั้งชื่อของเทมเพลตของคุณ)
- แต่ละชีตจะแสดงค่า `Name`, `Email`, และ `Total` ของลูกค้าแต่ละราย
- เลเอาต์ที่คุณออกแบบใน `template.xlsx` (หัวตาราง, การจัดรูปแบบ, สูตร) จะถูกเก็บรักษาไว้ในทุกชีตที่สร้าง

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรัน คัดลอกและวางลงในแอปคอนโซล ปรับเส้นทางไฟล์ตามต้องการ แล้วกด **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

รันโปรแกรม, เปิด `output.xlsx`, แล้วคุณจะเห็น **create dynamic excel table** ทำงาน—แต่ละลูกค้าได้ชีตของตัวเอง พร้อมการจัดรูปแบบเต็มตามที่คุณออกแบบ

---

## คำถามทั่วไป & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| *ถ้า JSON ของฉันมีอ็อบเจกต์ซ้อนกันล่ะ?* | Smart Markers รองรับการใช้ dot notation (`${Customers.Address.City}`) ตราบใดที่โครงสร้าง JSON ตรงกัน |
| *ฉันสามารถตั้งชื่อเวิร์กชีตที่สร้างตามชื่อลูกค้าได้ไหม?* | ได้—เพิ่มมาร์คเกอร์เช่น `${Customers.Name}` ในเซลล์ชื่อเวิร์กชีต หรือใช้ `processor.ApplyJson(customersJson, \"Customers\")` พร้อมรูปแบบการตั้งชื่อ |
| *ข้อมูลชุดใหญ่ (10 k+ แถว) จะเป็นอย่างไร?* | Processor จะสตรีมข้อมูลอย่างมีประสิทธิภาพ แต่ควรตรวจสอบการใช้หน่วยความจำ พิจารณาแยกรายงานเป็นหลายไฟล์หากถึงขีดจำกัดประสิทธิภาพ |
| *ต้องการไลเซนส์สำหรับ Aspose.Cells หรือไม่?* | การประเมินฟรีใช้ได้สำหรับการทดสอบ แต่เวอร์ชันที่มีไลเซนส์จะลบลายน้ำการประเมินและให้ฟีเจอร์เต็ม |
| *ฉันสามารถใช้วิธีนี้กับ .NET Core ได้ไหม?* | แน่นอน—Aspose.Cells รองรับ .NET 6/7/8 เพียงอ้างอิงแพคเกจ NuGet แล้วโค้ดยังคงเหมือนเดิม |

---

## เคล็ดลับสำหรับการใช้งานในระดับ Production

- **Validate JSON** ก่อนป้อนให้ `ApplyJson` payload ที่ผิดรูปแบบจะทำให้เกิด `JsonParseException`
- **Cache the template** หากคุณสร้างรายงานหลาย ๆ รายการในช่วงเวลาสั้น ๆ การโหลดจากดิสก์ซ้ำ ๆ จะเป็น I/O ที่ไม่จำเป็น
- **Lock the workbook** ระหว่างการประมวลผล หากคุณรันในเว็บเซอร์วิสแบบหลายเธรดเพื่อหลีกเลี่ยง race condition
- **Add error handling** รอบ `workbook.Save` เพื่อจัดการกับปัญหาการอนุญาตหรือไฟล์ที่ถูกล็อกอย่างราบรื่น
- **Customize styling** ในเทมเพลต (conditional formatting, formulas) เพื่อให้ชีตที่สร้างรักษาตรรกะธุรกิจโดยไม่ต้องเขียนโค้ดเพิ่มเติม

---

## สรุป

ตอนนี้คุณมีรูปแบบครบวงจรที่มั่นคงสำหรับการ **create dynamic excel table** ด้วยการใช้เทมเพลต, Smart Markers, และข้อมูล JSON โดย **loading excel template**, แทรกมาร์คเกอร์ทำซ้ำ, และ **populate excel from json**, คุณสามารถ **automate excel report** ได้ด้วยเพียงไม่กี่บรรทัดของ C#

ขั้นตอนต่อไป? ลองเพิ่มแผนภูมิที่อ้างอิงตารางไดนามิก, หรือส่งออก JSON เดียวกันเป็น PDF ด้วย Aspose.Words คุณอาจทดลอง **generate excel report json** จากการคิวรีฐานข้อมูลเพื่อปิดวงจร

## บทแนะนำที่เกี่ยวข้อง

- [สร้าง Pivot Table ใน Excel ด้วย Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [สร้าง Dynamic Line Charts ใน Excel ด้วย Aspose.Cells for .NET&#58; คู่มือขั้นตอน](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [วิธีสร้าง Checkboxes ใน Excel ด้วย Aspose.Cells for .NET | บทแนะนำ Data Validation](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}