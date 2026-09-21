---
category: general
date: 2026-03-22
description: เรียนรู้วิธีจัดรูปแบบวันที่และเวลาเป็น ISO ขณะดึงข้อมูลวันที่จาก Excel
  และแสดงวันที่ในรูปแบบ ISO ด้วย Aspose.Cells ใน C#
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: th
og_description: การแปลงวันที่และเวลาเป็นรูปแบบ ISO ทำได้ง่าย คู่มือนี้แสดงวิธีดึงวันที่จาก
  Excel และแสดงวันที่ในรูปแบบ ISO ด้วย Aspose.Cells.
og_title: แปลง datetime เป็น ISO ใน C# – บทเรียนแบบขั้นตอนต่อขั้นตอน
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: จัดรูปแบบ DateTime เป็น ISO ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง datetime เป็น iso ใน C# – คู่มือฉบับสมบูรณ์

เคยต้องการ **format datetime to iso** แต่แหล่งข้อมูลอยู่ในไฟล์ Excel ไหม? อาจเป็นไปได้ว่าตัวเซลล์มีรูปแบบยุคญี่ปุ่นเช่น “令和3年5月1日” แล้วคุณกำลังสงสัยว่าจะเปลี่ยนเป็นสตริง `2021‑05‑01` ที่สะอาดอย่างไร คุณไม่ได้อยู่คนเดียว ในบทแนะนำนี้เราจะ **extract date from excel**, แยกวิเคราะห์ยุคญี่ปุ่น, และจากนั้น **display iso date** บนคอนโซล—ทั้งหมดด้วยไม่กี่บรรทัดของ C# และ Aspose.Cells

เราจะพาคุณผ่านทุกอย่างที่ต้องการ: แพ็กเกจ NuGet ที่จำเป็น, โค้ดที่สามารถคัดลอก‑วางได้ตรง, เหตุผลที่แต่ละบรรทัดสำคัญ, และเคล็ดลับกรณีขอบบางหลายข้อ สุดท้ายคุณจะได้สแนปช็อตที่นำกลับมาใช้ใหม่ได้ซึ่งแปลง datetime เป็น iso ไม่ว่า Excel ค่าเดิมจะดูแปลกแยกอย่างไร

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดยังคอมไพล์บน .NET Framework 4.6+ ได้เช่นกัน)
- Visual Studio 2022 (หรือเครื่องมือแก้ไขใด ๆ ที่คุณชอบ)
- **Aspose.Cells for .NET** NuGet package – `Install-Package Aspose.Cells`
- ไฟล์ Excel (หรือเวิร์กบุ๊กใหม่) ที่มีวันที่ในรูปแบบยุคญี่ปุ่น

แค่นั้นเอง ไม่ต้องใช้ไลบรารีเพิ่มเติม ไม่ต้องใช้ COM interop เพียงวิธีเดียวที่มีเอกสารครบถ้วน

## ขั้นตอนที่ 1: สร้าง Workbook และเขียนวันที่ในรูปแบบยุคญี่ปุ่น  

ก่อนอื่นเราต้องมี workbook เพื่อทำงาน หากคุณมีไฟล์ Excel อยู่แล้วสามารถโหลดด้วย `new Workbook("path")` สำหรับตัวอย่างนี้เราจะสร้าง workbook ใหม่ในหน่วยความจำและใส่สตริงยุคญี่ปุ่นลงในเซลล์ **A1**  

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **ทำไมเราต้องทำเช่นนี้:** Aspose.Cells ปฏิบัติต่อค่าของเซลล์เป็นสตริงโดยค่าเริ่มต้น การใส่ข้อความยุคดิบช่วยจำลองสถานการณ์จริงที่ลูกค้าญี่ปุ่นใส่วันที่ในปฏิทินท้องถิ่นของพวกเขา

## ขั้นตอนที่ 2: เปิดใช้งานการแปลงยุคญี่ปุ่นและดึงวันที่ออกมา  

Aspose.Cells สามารถแปลงสตริงยุคญี่ปุ่นเป็นอ็อบเจ็กต์ .NET `DateTime` ได้โดยอัตโนมัติ—แต่ต้องบอกให้มันทำ `DateTimeParseOptions.EnableJapaneseEra` จะทำหน้าที่หลัก  

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **เคล็ดลับ:** หากลืมใช้ตัวเลือก `EnableJapaneseEra` ไลบรารีจะคืนค่าสตริงเดิมและการแปลงต่อไปจะล้มเหลว ตรวจสอบ `parsed.Type` เสมอหากคุณจัดการกับเนื้อหาที่ผสมกัน

## ขั้นตอนที่ 3: แปลง DateTime ที่แปลงแล้วเป็น ISO 8601  

เมื่อเรามี `DateTime` ที่ถูกต้องแล้ว การแปลงเป็นสตริงรูปแบบ ISO‑เป็นเรื่องง่ายมาก รูปแบบ `"yyyy-MM-dd"` สอดคล้องกับส่วนวันที่ของ ISO 8601 ซึ่งเป็นสิ่งที่ API ส่วนใหญ่คาดหวัง  

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

การรันโปรแกรมจะแสดงผล:

```
ISO date: 2021-05-01
```

นั่นคือ **display iso date** ที่คุณต้องการ

## ตัวอย่างเต็มที่สามารถรันได้  

ด้านล่างเป็นบล็อกโค้ดเต็มที่คุณสามารถคัดลอกไปใส่ในโปรเจกต์คอนโซลได้โดยตรง ไม่ต้องมีการพึ่งพาที่ซ่อนอยู่หรือการตั้งค่าเพิ่มเติม  

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **ผลลัพธ์ที่คาดหวัง:** `ISO date: 2021-05-01`

## การวิเคราะห์ทีละขั้นตอน (ทำไมแต่ละส่วนถึงสำคัญ)

| ขั้นตอน | สิ่งที่เกิดขึ้น | ทำไมจึงสำคัญ |
|------|--------------|--------------------|
| **Create workbook** | เริ่มต้นคอนเทนเนอร์ Excel ในหน่วยความจำ | ให้ sandbox สำหรับทดสอบโดยไม่ต้องเข้าถึงไฟล์ระบบ |
| **PutValue** | เก็บสตริงยุคญี่ปุ่นดิบใน **A1** | จำลองการป้อนข้อมูลจริง; ทำให้ parser เห็นข้อความที่ตรงกัน |
| **GetValue with `EnableJapaneseEra`** | แปลงสตริงยุคเป็น .NET `DateTime` | จัดการการแปลงปฏิทินโดยอัตโนมัติ—ไม่ต้องใช้ตาราง lookup ด้วยมือ |
| **`ToString("yyyy-MM-dd")`** | ฟอร์แมต `DateTime` เป็น ISO 8601 | รับประกันสตริงวันที่ที่เป็น culture‑invariant, สามารถเรียงลำดับได้และรับโดย REST API, ฐานข้อมูล ฯลฯ |
| **Console.WriteLine** | แสดง ISO date สุดท้าย | ยืนยันว่าทั้งกระบวนการทำงานจากต้นจนจบ |

## การจัดการกับความแปรผันทั่วไป  

### 1. ตำแหน่งเซลล์ที่ต่างกัน  

หากวันที่ของคุณอยู่ใน **B2** หรือชื่อช่วง ให้เปลี่ยน `"A1"` เป็นที่อยู่ที่ต้องการแทน:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. หลายวันที่อยู่ในคอลัมน์เดียว  

เมื่อคุณต้องการ **extract date from excel** สำหรับหลายแถว ให้วนลูปผ่านช่วงที่ใช้:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. ตัวสำรองสำหรับค่าที่ไม่ใช่ยุค  

หากเซลล์มีสตริงวันที่มาตรฐานอยู่แล้ว parser ยังทำงานได้ แต่คุณอาจต้องการเฝ้าระวัง:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

แฟล็ก `TryParse` ป้องกันข้อยกเว้นและคืนค่าต้นฉบับหากการแปลงล้มเหลว

### 4. ส่วนเวลา  

หากต้องการส่วนเวลาเพิ่มเติม ให้ใช้รูปแบบ `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

จะได้ timestamp แบบ ISO 8601 เต็มรูปแบบ (`2021-05-01T00:00:00`)

## ภาพประกอบ  

![format datetime to iso example](image.png "An example of formatting datetime to iso in C#")

*ข้อความแทนภาพ:* *ตัวอย่างการแปลง datetime เป็น iso แสดงผลบนคอนโซล*

## คำถามที่พบบ่อย  

- **สามารถใช้กับไฟล์ .xls ได้หรือไม่?**  
  ใช่ Aspose.Cells รองรับ `.xls`, `.xlsx`, `.csv` และรูปแบบอื่น ๆ อีกมากมายโดยตรง  

- **ถ้าเวิร์กบุ๊กมีการป้องกันด้วยรหัสผ่านจะทำอย่างไร?**  
  โหลดด้วย `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`  

- **รูปแบบ ISO ขึ้นกับโลคัลหรือไม่?**  
  ไม่ รูปแบบ `"yyyy-MM-dd"` เป็น culture‑invariant ทำให้ได้สตริงเดียวกันบนเครื่องใดก็ได้  

- **ทำงานบน .NET Core ได้หรือไม่?**  
  แน่นอน—Aspose.Cells รองรับ .NET Standard 2.0  

## สรุป  

เราได้ครอบคลุมวิธี **format datetime to iso** โดย **extracting date from excel**, แยกวิเคราะห์สตริงยุคญี่ปุ่น, และสุดท้าย **displaying iso date** บนคอนโซล ขั้นตอนหลัก—สร้าง workbook, เขียนหรือโหลดข้อความยุค, เปิดใช้งานการแปลงยุคญี่ปุ่น, และฟอร์แมตด้วย `ToString("yyyy-MM-dd")`—เป็นทั้งหมดที่คุณต้องการสำหรับสถานการณ์ส่วนใหญ่

ต่อไปคุณอาจต้องการ:

- เขียนวันที่ ISO กลับไปยังคอลัมน์อื่นสำหรับการประมวลผลต่อไป
- ส่งออกเวิร์กบุ๊กที่แปลงแล้วเป็น CSV เพื่อการนำเข้าจำนวนมาก
- ผสานตรรกะนี้กับเว็บ API ที่รับไฟล์ Excel อัปโหลดและคืนค่า JSON‑encoded ISO dates

ลองทดลองกับรูปแบบวันที่ต่าง ๆ, โซนเวลา, หรือแม้แต่ปฏิทินกำหนดเอง ความยืดหยุ่นของ Aspose.Cells ทำให้คุณแทบไม่เจออุปสรรคใด ๆ  

Happy coding, and may all your dates be perfectly ISO‑compliant!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}