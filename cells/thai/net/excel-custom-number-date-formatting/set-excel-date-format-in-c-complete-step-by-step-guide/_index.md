---
category: general
date: 2026-02-28
description: เรียนรู้วิธีตั้งค่ารูปแบบวันที่ใน Excel, อ่านค่า datetime จาก Excel,
  แยกวันที่ออกจาก Excel และคำนวณสูตรในเวิร์กบุ๊กโดยใช้ Aspose.Cells ใน C# ตัวอย่างที่สามารถรันได้เต็มรูปแบบ.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: th
og_description: เชี่ยวชาญการตั้งค่ารูปแบบวันที่ใน Excel, การอ่านค่า datetime ของ Excel,
  การดึงวันที่, และการคำนวณสูตรในเวิร์กบุ๊กพร้อมตัวอย่าง C# ครบถ้วน.
og_title: ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# – คู่มือขั้นตอนเต็ม
tags:
- Aspose.Cells
- C#
- Excel automation
title: ตั้งค่ารูปแบบวันที่ใน Excel ด้วย C# – คู่มือครบขั้นตอนเต็มรูปแบบ
url: /th/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งรูปแบบวันที่ใน Excel – คู่มือ C# ฉบับสมบูรณ์

เคยเจอปัญหาในการ **set excel date format** ขณะสร้างสเปรดชีตแบบไดนามิกหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอ ปัญหานี้มักเกิดขึ้นเมื่อเซลล์แสดงเป็นสตริงดิบแทนวันที่ที่ถูกต้อง โดยเฉพาะกับวันที่ตามยุคญี่ปุ่นหรือสตริงตามโลคัลที่กำหนดเอง  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างจริงที่ **sets the Excel date format**, แล้ว **reads the excel datetime**, **extracts the date from excel**, และแม้กระทั่ง **calculates workbook formulas** เพื่อให้คุณสามารถ **get datetime cell** เป็นอ็อบเจ็กต์ .NET `DateTime` ได้อย่างเป็นธรรมชาติ ไม่ต้องอ้างอิงภายนอก เพียงแค่คัดลอกโค้ดสั้น ๆ นี้ไปวางใน Visual Studio แล้วรันทันที

## สิ่งที่คุณต้องการ

- **Aspose.Cells for .NET** (เวอร์ชันล่าสุดใดก็ได้; API ที่ใช้ที่นี่ทำงานกับ 23.x และใหม่กว่า)  
- .NET 6 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ .NET Framework 4.6+)  
- ความเข้าใจพื้นฐานของไวยากรณ์ C# – หากคุณเขียน `Console.WriteLine` ได้ก็พร้อมแล้ว

แค่นั้นเอง ไม่ต้องติดตั้ง NuGet เพิ่มเติมนอกจาก Aspose.Cells ไม่ต้องมี Excel ติดตั้งบนเครื่อง

## วิธีตั้งรูปแบบวันที่ใน Excel ด้วย C#

สิ่งแรกที่เราต้องทำคือบอก Excel ว่าเซลล์นั้นเป็นวันที่ ไม่ใช่ข้อความทั่วไป Aspose.Cells มี ID ของรูปแบบตัวเลขในตัว (`14`) ที่สอดคล้องกับรูปแบบวันที่สั้นของโลคัลปัจจุบัน

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** การเรียก `CalculateFormula()` มีความสำคัญมาก หากไม่เรียก เซลล์จะยังคงเก็บสตริงดิบอยู่และ `GetDateTime()` จะโยนข้อยกเว้นบรรทัดนี้ทำให้ Aspose.Cells รันตัวแปลภายในเพื่อ **calculate workbook formulas** ให้เรา

ผลลัพธ์ที่คุณจะเห็นเมื่อรันโปรแกรมคือ:

```
Parsed DateTime: 2020-04-01
```

ซึ่งยืนยันว่าเราสามารถ **set excel date format** ได้สำเร็จและสามารถ **get datetime cell** เป็น `DateTime` ที่ถูกต้อง

## การอ่านค่า datetime จาก Excel  

ตอนนี้วันที่ถูกจัดเก็บอย่างถูกต้องแล้ว คุณอาจสงสัยว่าจะดึงค่ากลับมาอย่างไรจากไฟล์ที่มีอยู่ `GetDateTime()` ทำงานได้กับเซลล์ใด ๆ ที่มีรูปแบบวันที่อยู่แล้ว

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

หากเซลล์ไม่ได้ตั้งเป็นรูปแบบวันที่ `GetDateTime()` จะคืนค่า `DateTime.MinValue` ดังนั้นเราต้อง **set excel date format** ก่อนเสมอ

## การดึงวันที่จากเซลล์ Excel  

บางครั้งเซลล์อาจมี timestamp เต็มรูป (วันที่ + เวลา) แต่คุณต้องการเฉพาะส่วนวันที่เท่านั้น คุณสามารถตัดส่วนเวลาออกได้โดยใช้ `.Date` บน `DateTime` ที่คืนมา

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

วิธีนี้ทำงานได้ไม่ว่ารูปแบบตัวเลขของ Excel จะเป็นแบบใด ตราบใดที่เซลล์ถูกจดจำเป็นวันที่

## การคำนวณสูตรใน Workbook  

ถ้าวันที่มาจากสูตร เช่น `=TODAY()` หรือ `=DATE(2022,5,10)` Aspose.Cells จะประเมินสูตรเมื่อคุณเรียก `CalculateFormula()` หลังจากนั้นเซลล์จะทำงานเหมือนวันที่ที่ป้อนด้วยมือ

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

สังเกตว่าเราไม่จำเป็นต้องเปลี่ยนสไตล์ของเซลล์; Excel จะถือผลลัพธ์ของสูตรเป็นวันที่เมื่อสูตรคืนค่าเป็นเลขซีเรียลที่แมปกับวันที่

## การดึงค่า datetime จาก Workbook ที่มีอยู่  

รวมทุกอย่างเข้าด้วยกัน นี่คือฟังก์ชันสั้น ๆ ที่คุณสามารถใส่ในโปรเจกต์ใดก็ได้เพื่อเปิดไฟล์ Excel, ตรวจสอบให้แน่ใจว่าเซลล์วันที่ทั้งหมดถูกตีความอย่างถูกต้อง, และคืนรายการของอ็อบเจ็กต์ `DateTime`

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

การเรียก `ExtractAllDates("Sample.xlsx")` จะให้คุณได้ทุกวันที่ที่ **set excel date format** อย่างถูกต้องในชีตแรก

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| `GetDateTime()` throws `ArgumentException` | เซลล์ไม่ถูกจดจำเป็นวันที่ (ขาดรูปแบบตัวเลข) | Apply `Style.Number = 14` **before** calling `CalculateFormula()` |
| Date appears as `1900‑01‑00` | เลขซีเรียล 0 ของ Excel ถูกตีความเป็น epoch | Ensure the cell actually contains a valid serial (>0) |
| Japanese era strings don’t parse | Aspose.Cells จะพาร์สสตริงยุคหลัง `CalculateFormula()` | Keep the raw string, set a date format, then call `CalculateFormula()` |
| Time zone shifts | `DateTime` ถูกเก็บโดยไม่มีข้อมูลโซน, แต่แอปของคุณอาจแสดงในโลคัลอื่น | Use `DateTimeKind.Utc` or convert explicitly if needed |

## รูปภาพ – สรุปภาพรวม  

![ตัวอย่างการตั้งรูปแบบวันที่ใน Excel](excel-date-format.png "ตัวอย่างการตั้งรูปแบบวันที่ใน Excel")

แผนภาพแสดงกระบวนการ: **write string → apply number format → recalculate → retrieve DateTime**.

## สรุป  

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **set excel date format**, **read excel datetime**, **extract date from excel**, **calculate workbook formulas**, และสุดท้าย **get datetime cell** เป็นอ็อบเจ็กต์ .NET ดั้งเดิม โค้ดที่สมบูรณ์พร้อมรันพร้อมคัดลอก‑วาง และคำอธิบายให้คุณเข้าใจ “ทำไม” ของแต่ละขั้นตอน เพื่อให้คุณปรับใช้กับสถานการณ์ที่ซับซ้อนยิ่งขึ้นได้

### สิ่งต่อไป?

- **Bulk import/export:** ใช้ฟังก์ชัน `ExtractAllDates` เพื่อประมวลผลรายงานขนาดใหญ่เป็นชุด  
- **Custom date formats:** แทนที่ `Style.Number = 14` ด้วย `Style.Custom = "yyyy/mm/dd"` เพื่อให้รูปแบบไม่ขึ้นกับโลคัล  
- **Time‑zone aware dates:** ผสาน `DateTimeOffset` กับเลขซีเรียลของ Excel สำหรับแอปพลิเคชันระดับโลก  

ทดลองปรับแต่ง เพิ่มการจัดรูปแบบตามเงื่อนไข หรือบันทึกวันที่ลงฐานข้อมูลได้ตามใจ หากเจออุปสรรคใด ๆ คอมเมนต์ไว้ได้เลย — Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}