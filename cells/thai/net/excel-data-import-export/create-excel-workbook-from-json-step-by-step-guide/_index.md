---
category: general
date: 2026-03-25
description: สร้างไฟล์ Excel จาก JSON แล้วบันทึกเป็น xlsx เรียนรู้วิธีส่งออก JSON
  ไปเป็น xlsx, สร้าง Excel จาก JSON, และเติมข้อมูลลงใน Excel จาก JSON ได้ภายในไม่กี่นาที.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: th
og_description: สร้างไฟล์ Excel จาก JSON อย่างรวดเร็ว คู่มือนี้แสดงวิธีส่งออก JSON
  เป็นไฟล์ xlsx, สร้าง Excel จาก JSON, และเติมข้อมูล Excel จาก JSON ด้วย Aspose.Cells.
og_title: สร้าง Excel Workbook จาก JSON – คอร์สสอน C# อย่างครบถ้วน
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: สร้างเวิร์กบุ๊ก Excel จาก JSON – คู่มือขั้นตอนโดยละเอียด
url: /th/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook จาก JSON – คำแนะนำ C# ฉบับสมบูรณ์

เคยต้องการ **create excel workbook** จาก JSON payload แต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว; นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องแปลงข้อมูล API ให้เป็นสเปรดชีตที่เรียบร้อย ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และ Aspose.Cells คุณสามารถ **export json to xlsx**, **generate excel from json**, และ **populate excel from json** โดยไม่ต้องใช้ตัวแปลงของบุคคลที่สาม.

ในคู่มือนี้เราจะเดินผ่านกระบวนการทั้งหมด—เริ่มจากสตริง JSON ดิบ, ใส่ลงใน SmartMarker, และสุดท้าย **save workbook as xlsx** บนดิสก์. เมื่อจบคุณจะได้ไฟล์ Excel ที่พร้อมใช้งานซึ่งมีลักษณะดังนี้:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** หากคุณกำลังใช้ Aspose.Cells อยู่แล้วในส่วนอื่นของโปรเจกต์, คุณสามารถใช้ `Workbook` อินสแตนซ์เดียวกันสำหรับการนำเข้า JSON หลายครั้ง—เหมาะสำหรับการประมวลผลเป็นชุด.

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือ .NET Framework ล่าสุดที่รองรับ C# 10)
- **Aspose.Cells for .NET** – ติดตั้งผ่าน NuGet: `dotnet add package Aspose.Cells`
- ความเข้าใจพื้นฐานของไวยากรณ์ C# (ไม่จำเป็นต้องมีความรู้เชิงลึกเกี่ยวกับ Excel)

เท่านี้เอง. ไม่มีบริการภายนอก, ไม่มี COM interop, เพียงโค้ดที่จัดการโดย .NET เท่านั้น.

## ขั้นตอนที่ 1: สร้าง Excel Workbook ใหม่

สิ่งแรกที่เราทำคือสร้างอ็อบเจกต์ workbook ใหม่. คิดว่าเป็นการเปิดไฟล์ Excel ว่างเปล่าที่เราจะใส่ข้อมูลต่อไป.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

ทำไมต้องเริ่มด้วย workbook ใหม่? มันรับประกันว่ามีสภาพเริ่มต้นที่สะอาด, ป้องกันสไตล์ที่เหลือจากการรันก่อนหน้า, และทำให้ขนาดไฟล์เล็กที่สุด—เหมาะสำหรับ pipeline อัตโนมัติ.

## ขั้นตอนที่ 2: เตรียมข้อมูล JSON ที่ต้องการนำเข้า

เพื่อการสาธิตเราจะใช้ JSON array เล็ก ๆ, แต่คุณสามารถเปลี่ยนเป็น JSON ที่ถูกต้องใด ๆ ที่คุณได้รับจากเว็บเซอร์วิส, ไฟล์, หรือการคิวรีฐานข้อมูล.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

สังเกตเครื่องหมายอัญประกาศที่ถูก escape สองครั้ง (`\"`)—เป็นเพียงไวยากรณ์สตริงของ C#. ในสถานการณ์จริงคุณอาจอ่านจากไฟล์:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## ขั้นตอนที่ 3: บอก SmartMarker ให้ถืออาเรย์ทั้งหมดเป็นเรคคอร์ดเดียว

เครื่องมือ SmartMarker ของ Aspose.Cells สามารถวนลูปคอลเลกชันโดยอัตโนมัติ. โดยเปิดใช้งาน **ArrayAsSingle**, เราจะถือ JSON array ทั้งหมดเป็นเรคคอร์ดเดียว, ซึ่งเป็นสิ่งที่เราต้องการสำหรับตารางแบบแบน.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

หากคุณลืมตั้งค่าสถานะนี้, SmartMarker จะพยายามสร้างชีตแยกสำหรับแต่ละองค์ประกอบ—แน่นอนว่าไม่ใช่สิ่งที่ต้องการเมื่อสร้างตารางง่าย ๆ.

## ขั้นตอนที่ 4: ใส่ Token ของ SmartMarker ลงใน Worksheet

Token ของ SmartMarker มีรูปแบบ `${jsonArray}`. เมื่อโปรเซสเซอร์ทำงาน, มันจะแทนที่ token ด้วยข้อมูลจากแหล่ง JSON. เราจะใส่ token ลงในเซลล์ **A1** เพื่อให้ผลลัพธ์เริ่มที่มุมซ้ายบน.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

คุณยังสามารถจัดรูปแบบแถวหัวตารางล่วงหน้าก่อนการประมวลผลได้. ตัวอย่างเช่น, ตั้งฟอนต์หนาในแถวแรก:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## ขั้นตอนที่ 5: รัน SmartMarker Processor

ตอนนี้จุดมหัศจรรย์เกิดขึ้น. โปรเซสเซอร์อ่าน JSON, แมปแต่ละ property ไปยังคอลัมน์, และเขียนแถวลงใต้ token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

เบื้องหลัง, Aspose.Cells:
1. แปลง JSON เป็นอ็อบเจกต์ .NET.
2. จับคู่ชื่อ property (`Name`, `Score`) กับหัวคอลัมน์.
3. เขียนแต่ละองค์ประกอบของอาเรย์เป็นแถวใหม่.

หาก JSON ของคุณมีอ็อบเจกต์ซ้อนกัน, คุณสามารถอ้างอิงด้วย dot notation (`${parent.child}`) – ฟีเจอร์ที่สะดวกสำหรับรายงานที่ซับซ้อนขึ้น.

## ขั้นตอนที่ 6: บันทึก Workbook เป็นไฟล์ XLSX

สุดท้าย, บันทึก workbook ลงดิสก์. ส่วนขยายไฟล์ `.xlsx` บอก Excel (และแอปสเปรดชีตอื่น ๆ ส่วนใหญ่) ว่านี่คือ OpenXML workbook.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

คุณสามารถสตรีม workbook โดยตรงไปยัง HTTP response ได้หากคุณกำลังสร้างเว็บ API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มรูปแบบพร้อมรันที่รวมทุกขั้นตอนข้างต้น. คัดลอกและวางลงในโปรเจกต์คอนโซลใหม่และกด **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Expected result:** การเปิด `json-single.xlsx` จะเห็นสองแถวใต้หัวตารางหนา—`John` ที่มีคะแนน `90` และ `Anna` ที่มี `85`. ชื่อคอลัมน์จะถูกสรุปอัตโนมัติจากชื่อ property ของ JSON.

## คำถามทั่วไป & กรณีขอบ

### ถ้า key ของ JSON มีช่องว่างหรืออักขระพิเศษจะทำอย่างไร?

SmartMarker คาดหวังชื่อ identifier ที่ถูกต้อง. แทนที่ช่องว่างด้วย underscores หรือใช้การแมปแบบกำหนดเอง:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### จะทำอย่างไรเมื่อส่งออก JSON array ขนาดใหญ่ (หลายพันแถว)?

โปรเซสเซอร์สตรีมข้อมูลภายใน, ดังนั้นการใช้หน่วยความจำจะคงที่. อย่างไรก็ตาม, คุณอาจต้อง:
- เพิ่มขีดจำกัด `MaxRows` ของ worksheet (`worksheet.Cells.MaxRow = 1_048_576;` – ค่าสูงสุดของ Excel).
- ปิด gridlines เพื่อประสิทธิภาพ (`worksheet.IsGridlinesVisible = false;`).

### สามารถเพิ่มหลายตาราง JSON ลงใน workbook เดียวได้หรือไม่?

ได้เลย. เพียงใส่ SmartMarker token ต่าง ๆ ลงในช่วงแยกกัน (เช่น `${orders}` ใน `A10`, `${customers}` ใน `D1`) และเรียก `Process` ครั้งละ token หรือครั้งเดียวกับอ็อบเจกต์ JSON เชิงประกอบที่มีทั้งสองอาเรย์.

## โบนัส: เพิ่มแผนภูมิแบบง่าย (เลือกได้)

หากต้องการแสดงคะแนนเป็นภาพ, เพิ่มแผนภูมิคอลัมน์อย่างรวดเร็วหลังจากข้อมูลถูกเติมเต็ม:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to create excel workbook** จากสตริง JSON, **export json to xlsx**, **generate excel from json**, และ **populate excel from json** ด้วยฟีเจอร์ SmartMarker ของ Aspose.Cells. โซลูชันเต็มรูปแบบ—การเริ่มต้น workbook, การตั้งค่า SmartMarker, การประมวลผล JSON, และการบันทึกไฟล์—ใช้เพียงไม่กี่บรรทัด แต่สามารถขยายได้กับชุดข้อมูลขนาดใหญ่.

ขั้นตอนต่อไป? ลองเปลี่ยน JSON คงที่เป็นการเรียก API, เพิ่มการจัดรูปแบบตามเงื่อนไขตามคะแนน, หรือสร้างหลายชีตสำหรับโดเมนข้อมูลต่าง ๆ. รูปแบบเดียวกันทำงานกับ CSV, XML, หรือแม้แต่ผลลัพธ์จากฐานข้อมูล—เพียงเปลี่ยนสตริงแหล่งข้อมูลและปรับ SmartMarker token.

ขอให้เขียนโค้ดอย่างสนุกสนาน, และสเปรดชีตของคุณเป็นระเบียบเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}