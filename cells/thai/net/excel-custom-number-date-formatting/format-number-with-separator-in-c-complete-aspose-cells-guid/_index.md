---
category: general
date: 2026-03-30
description: เรียนรู้วิธีจัดรูปแบบตัวเลขด้วยตัวคั่นโดยใช้ Aspose.Cells ใน C# รวมถึงการตั้งค่ารูปแบบตัวเลขแบบกำหนดเอง
  การเพิ่มตัวคั่นหลักพัน การจัดรูปแบบตำแหน่งทศนิยม และวิธีจัดรูปแบบเซลล์
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: th
og_description: จัดรูปแบบตัวเลขด้วยตัวคั่นใน C#. คู่มือนี้แสดงวิธีตั้งค่ารูปแบบตัวเลขแบบกำหนดเอง,
  เพิ่มตัวคั่นหลักพัน, กำหนดรูปแบบตำแหน่งทศนิยม, และวิธีจัดรูปแบบเซลล์โดยใช้ Aspose.Cells.
og_title: จัดรูปแบบตัวเลขด้วยตัวคั่นใน C# – บทเรียน Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: จัดรูปแบบตัวเลขด้วยตัวคั่นใน C# – คู่มือ Aspose.Cells ฉบับสมบูรณ์
url: /th/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การจัดรูปแบบตัวเลขด้วยตัวคั่นใน C# – คู่มือ Aspose.Cells ฉบับสมบูรณ์

เคยต้อง **จัดรูปแบบตัวเลขด้วยตัวคั่น** ในสเปรดชีตแต่ไม่แน่ใจว่าจะใช้ API ใด? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต้องต่อสู้กับตัวคั่นหลักพัน, จำนวนตำแหน่งทศนิยม, และรูปแบบกำหนดเองเมื่อต้องส่งออกข้อมูลบ่อยครั้ง  

ข่าวดี: Aspose.Cells ทำให้เรื่องนี้ง่ายดายมาก ในบทเรียนนี้เราจะเดินผ่านตัวอย่างจริงที่ **ตั้งค่ารูปแบบตัวเลขแบบกำหนดเอง**, **เพิ่มตัวคั่นหลักพัน**, **กำหนดตำแหน่งทศนิยม**, และแสดง **วิธีจัดรูปแบบเซลล์** ให้เป็นสตริง สุดท้ายคุณจะได้โค้ดสั้น ๆ ที่พร้อมรันและสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

## สิ่งที่คู่มือนี้ครอบคลุม

* แพคเกจ NuGet ที่ต้องใช้และวิธีติดตั้ง  
* โค้ดขั้นตอนต่อขั้นตอนที่สร้าง workbook, เขียนค่าตัวเลข, และใช้รูปแบบกำหนดเอง  
* ทำไม `ExportTableOptions.ExportAsString` ถึงเป็นวิธีที่แนะนำในการดึงค่าที่จัดรูปแบบแล้ว  
* จุดบกพร่องทั่วไป—เช่น ลืมเปิด `ExportAsString` หรือใช้รูปแบบมาสก์ผิด  
* วิธีปรับมาสก์รูปแบบหากต้องการจำนวนตำแหน่งทศนิยมหรือสไตล์ตัวคั่นที่ต่างกัน  

ไม่มีลิงก์เอกสารภายนอกที่จำเป็น; ทุกอย่างที่คุณต้องการอยู่ที่นี่แล้ว ไปดูกันเลย

---

## ข้อกำหนดเบื้องต้น

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 หรือใหม่กว่า | Aspose.Cells 23.10+ รองรับ .NET Standard 2.0+, ดังนั้น .NET 6 จึงปลอดภัยและเป็นเวอร์ชันล่าสุด |
| Visual Studio 2022 (หรือ IDE C# ใดก็ได้) | ทำให้การดีบักและการจัดการแพคเกจเป็นเรื่องง่าย |
| Aspose.Cells for .NET NuGet package | มีคลาส `Workbook`, `Worksheet`, และ `ExportTableOptions` ที่เราจะใช้ |

คุณสามารถติดตั้งแพคเกจได้ผ่าน Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

เท่านี้—ไม่มี DLL เพิ่มเติม, ไม่มี COM interop, เพียงอ้างอิง NuGet เพียงหนึ่งเดียว

---

## ขั้นตอนที่ 1: เริ่มต้น Workbook ใหม่ (วิธีจัดรูปแบบเซลล์)

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ `Workbook` ใหม่ ถือเป็นไฟล์ Excel ว่างเปล่าที่พร้อมรับข้อมูล

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **ทำไมเรื่องนี้สำคัญ:** `Workbook` เป็นจุดเริ่มต้นของทุกการทำงานใน Aspose.Cells การดึง worksheet แรก (`Worksheets[0]`) จะให้แคนวาสที่สะอาดโดยไม่ต้องตั้งชื่อแผ่น

---

## ขั้นตอนที่ 2: เขียนค่าตัวเลขลงในเซลล์เป้าหมาย

ต่อไปเราจะใส่ตัวเลขดิบลงในเซลล์ **A1** ค่าที่ใส่ยังไม่ได้จัดรูปแบบ—เป็นแค่ double เท่านั้น

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **เคล็ดลับ:** ใช้ `PutValue` แทน `PutString` เมื่อคุณต้องการใช้การจัดรูปแบบตัวเลขต่อไป นี้จะรักษาชนิดข้อมูลเดิมไว้ ทำให้ Excel สามารถคำนวณได้อย่างถูกต้อง

---

## ขั้นตอนที่ 3: ตั้งค่ารูปแบบตัวเลขแบบกำหนดเอง (เพิ่มตัวคั่นหลักพัน & กำหนดตำแหน่งทศนิยม)

ตอนนี้มาถึงหัวใจของบทเรียน: กำหนดมาสก์รูปแบบที่บอก Aspose.Cells ว่าจะแสดงตัวเลขอย่างไร มาสก์ `#,##0.00` ทำสามอย่าง:

1. **`#,##0`** – เพิ่มตัวคั่นหลักพัน (คอมม่าเป็นค่าเริ่มต้น)  
2. **`.00`** – บังคับให้มีสองตำแหน่งทศนิยมเท่านั้น  

ถ้าต้องการตำแหน่งทศนิยมจำนวนอื่น เพียงเปลี่ยนจำนวน `0` หลังจุดทศนิยม

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **ทำไมต้องใช้ `ExportAsString`**: โดยค่าเริ่มต้น `ExportString` จะคืนค่าดิบ การตั้งค่า `ExportAsString = true` จะบังคับให้ API ใช้มาสก์ `NumberFormat` ก่อนแปลงเป็นข้อความ ซึ่งจำเป็นเมื่อคุณต้องการสตริงที่ตรงกับรูปแบบสำหรับรายงาน, JSON, หรือการแสดงผล UI

---

## ขั้นตอนที่ 4: ส่งออกข้อความที่จัดรูปแบบแล้ว (วิธีจัดรูปแบบเซลล์)

เมื่อกำหนดตัวเลือกเรียบร้อย เราเรียก `ExportString` บนเซลล์เดียวกัน วิธีนี้จะเคารพมาสก์ที่ตั้งไว้และคืนสตริงที่จัดรูปแบบอย่างสวยงาม

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

เมื่อรันโปรแกรมจะพิมพ์ **`12,345.68`** ไปยังคอนโซล—ตรงกับรูปแบบที่เราต้องการ

> **กรณีขอบ:** หากตัวเลขต้นฉบับมีทศนิยมมากกว่าสองตำแหน่ง มาสก์จะทำการปัดเศษ หากต้องการตัดทศนิยมแทนการปัดเศษ ต้องทำการประมวลผลค่าก่อนด้วย `Math.Truncate` แล้วค่อยเรียก `PutValue`

---

## ขั้นตอนที่ 5: ปรับแต่งรูปแบบ – ตัวแปรที่พบบ่อย

### 5.1 เปลี่ยนความแม่นยำของทศนิยม

ต้องการสามตำแหน่งทศนิยม? แค่เปลี่ยนมาสก์เป็น:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 ใช้ตัวคั่นหลักพันแบบอื่น

บางภูมิภาคต้องการช่องว่างหรือจุด คุณสามารถใส่ตัวอักษรนั้นโดยตรง:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

หรือให้ workbook ใช้การตั้งค่าภูมิภาค:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 เพิ่มคำนำหน้า หรือ คำต่อท้าย (สกุลเงิน, เปอร์เซ็นต์)

ใส่เครื่องหมายดอลลาร์หรือเปอร์เซ็นต์ลงในมาสก์ได้เลย:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **หมายเหตุ:** มาสก์แยกแยะตัวพิมพ์ใหญ่‑เล็ก `$` และ `%` เป็นสัญลักษณ์ตัวอักษร; พวกมันไม่ได้เปลี่ยนค่าตัวเลขพื้นฐาน

---

## ขั้นตอนที่ 6: ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกไปใส่ในแอปคอนโซลใหม่ได้ รวมทุกขั้นตอน, คอมเมนต์, และการตรวจสอบผลลัพธ์สุดท้าย

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

รันโปรแกรม (`dotnet run` จากเทอร์มินัลหรือกด F5 ใน Visual Studio) แล้วคุณจะเห็นตัวเลขที่จัดรูปแบบพิมพ์ออกมาตรงตามที่แสดง

---

## คำถามที่พบบ่อย (FAQ)

**Q: วิธีนี้ทำงานกับ Excel เวอร์ชันเก่าได้หรือไม่?**  
A: ทำได้. มาสก์รูปแบบสอดคล้องกับไวยากรณ์ของ Excel ดังนั้นเวอร์ชันใดที่เข้าใจ `#,##0.00` จะให้ผลลัพธ์เดียวกัน

**Q: ถ้าต้องการจัดรูปแบบหลายเซลล์พร้อมกันทำอย่างไร?**  
A: วนลูปผ่านช่วงที่ต้องการและใช้ `ExportTableOptions` เดียวกันกับแต่ละเซลล์ หรือกำหนด `Style.Custom` ให้กับช่วงแล้วเรียก `ExportString` จากเซลล์เดียว

**Q: สามารถส่งออกเป็น CSV พร้อมรูปแบบเหล่านี้ได้หรือไม่?**  
A: แน่นอน. ใช้ `Workbook.Save("output.csv", SaveFormat.CSV);` หลังจากตั้งค่ารูปแบบให้แต่ละเซลล์แล้ว Aspose.Cells จะเคารพ `Style` ของเซลล์เมื่อสร้าง CSV

---

## สรุป

เราได้แสดงวิธี **จัดรูปแบบตัวเลขด้วยตัวคั่น** ใน C# ด้วย Aspose.Cells ครอบคลุมตั้งแต่ **ตั้งค่ารูปแบบตัวเลขแบบกำหนดเอง** ไปจนถึง **เพิ่มตัวคั่นหลักพัน**, **กำหนดตำแหน่งทศนิยม**, และ **วิธีจัดรูปแบบเซลล์** เพื่อส่งออกเป็นสตริง โค้ดทั้งหมดเป็นอิสระ, ทำงานกับ .NET 6+ และปรับได้ตามภูมิภาคหรือความแม่นยำที่ต้องการ

ต่อไปคุณอาจลอง:

* ใช้เทคนิคเดียวกันกับวันที่และเวลา (`NumberFormat = "dd‑MMM‑yyyy"`)  
* อัตโนมัติการส่งออกจำนวนมากที่แต่ละคอลัมน์ต้องการมาสก์ต่างกัน  
* ผสานสตริงที่จัดรูปแบบแล้วเข้ากับรายงาน PDF ด้วย Aspose.Words  

ลองทำตามดู แล้วคุณจะกลายเป็นผู้เชี่ยวชาญด้านการจัดรูปแบบสเปรดชีตในทีมของคุณได้อย่างรวดเร็ว Happy coding!  

![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="ตัวเลขที่จัดรูปแบบด้วยตัวคั่นแสดงในผลลัพธ์ของ Aspose.Cells"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}