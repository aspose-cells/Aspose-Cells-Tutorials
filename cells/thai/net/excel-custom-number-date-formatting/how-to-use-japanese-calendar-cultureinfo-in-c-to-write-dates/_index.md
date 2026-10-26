---
category: general
date: 2026-10-26
description: เรียนรู้วิธีใช้ CultureInfo ของปฏิทินญี่ปุ่นใน C# เมื่อทำการแยกวันที่ตามสมัยและแทรกลงในแผ่นงาน
  Excel ด้วย NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: th
lastmod: 2026-10-26
og_description: ใช้ CultureInfo ของปฏิทินญี่ปุ่นใน C# เพื่อแปลงวันที่สมัยเรอิวะและเขียนลงในแผ่นงาน
  Excel โค้ดสมบูรณ์ที่สามารถรันได้พร้อมคำอธิบาย
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: ใช้ CultureInfo ปฏิทินญี่ปุ่นใน C# – ตัวอย่าง Excel อย่างเต็ม
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: วิธีใช้ CultureInfo ปฏิทินญี่ปุ่นใน C# เพื่อเขียนวันที่ลงใน Excel
url: /th/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Japanese calendar CultureInfo ใน C# เพื่อเขียนวันที่ลงใน Excel

หากคุณต้องการ **use Japanese calendar CultureInfo** ขณะทำงานกับวันที่ใน C# คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เรียนรู้วิธีแยกวิเคราะห์สตริงวันที่ที่มีชื่อยุคญี่ปุ่น (เช่น *Reiwa 2/5/1*) แล้วเขียน `DateTime` ที่ได้ลงในเซลล์แรกของแผ่นงาน Excel โดยใช้ไลบรารี NPOI

การแยกวิเคราะห์วันที่ที่อิงยุคโดยไม่มี `CultureInfo` ที่ถูกต้องจะทำให้เกิด `FormatException` หรือค่ารายเดือน/วันที่ไม่ถูกต้อง โดยการกำหนด `CultureInfo` ให้ใช้ Japanese calendar คุณจะมั่นใจได้ว่า .NET runtime จะตีความยุคอย่างถูกต้องและค่าที่คุณบันทึกลงใน Excel จะตรงกับการเขียนแบบญี่ปุ่นเดิม

ในบทเรียนนี้คุณจะได้:

* สร้างอ็อบเจกต์ `CultureInfo` ที่ใช้ Japanese calendar
* แยกวิเคราะห์สตริงวันที่แบบยุคญี่ปุ่นด้วย `DateTime.Parse`
* ใส่ `DateTime` ที่แยกวิเคราะห์แล้วลงในเซลล์ของแผ่นงาน NPOI
* ดูโปรแกรมเต็มที่สามารถรันได้และผลลัพธ์ที่คาดหวัง

> **Prerequisites** – .NET 6.0+ (หรือ .NET Core 3.1+), แพคเกจ **NPOI** NuGet, และความเข้าใจพื้นฐานเกี่ยวกับ C# และการจัดการไฟล์ Excel

---

## สิ่งที่คุณต้องการ

| รายการ | เหตุผล |
|------|--------|
| **.NET SDK** (6.0 หรือใหม่กว่า) | ให้ runtime และไลบรารีสำหรับ `CultureInfo` |
| **NPOI** (`NPOI` NuGet package) | ช่วยให้คุณสร้างและจัดการไฟล์ Excel โดยไม่ต้องติดตั้ง Office |
| **Visual Studio Code**, **Visual Studio**, หรือ IDE C# ใดก็ได้ | เพื่อคอมไพล์และรันตัวอย่าง |
| **Japanese era date string** (เช่น `"Reiwa 2/5/1"`) | แสดงการใช้ Japanese calendar |

---

## Step 1: Install NPOI

เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package NPOI --version 2.6.1
```

แพคเกจนี้จะให้ชนิด `IWorkbook`, `ISheet` และ `ICell` ที่ใช้ในขั้นตอนต่อไป

---

## Step 2: Create a CultureInfo that uses the Japanese calendar

Japanese calendar เป็นปฏิทินที่อิงยุค คุณต้องร้องขอเวอร์ชัน *Japanese* ของ locale `ja-JP` และตั้งค่าปฏิทินเป็น `JapaneseCalendar` อย่างชัดเจน

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – Culture `ja-JP` เริ่มต้นใช้ Gregorian calendar การกำหนดคุณสมบัติ `Calendar` ใหม่ทำให้ชื่อยุคเช่น *Reiwa* ถูกรับรู้ระหว่างการแยกวิเคราะห์

---

## Step 3: Parse a Japanese era date string

เมื่อ `CultureInfo` ถูกตั้งค่าแล้ว คุณสามารถแยกวิเคราะห์สตริงที่มีชื่อยุคได้อย่างปลอดภัย

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

เมธอด `Parse` จะตีความ *Reiwa 2* เป็นปี Gregorian 2020, เดือน 5, วัน 1

### Edge case: handling invalid eras

หากผู้ใช้ระบุยุคที่ไม่รองรับ (เช่น `"Heisei 31/4/30"` หลังจากยุค Heisei สิ้นสุด) `DateTime.Parse` จะโยน `FormatException` ให้ห่อการเรียกในบล็อก try‑catch เพื่อแสดงข้อความข้อผิดพลาดที่เป็นมิตร:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Step 4: Write the parsed DateTime into an Excel worksheet

เมื่อมีอ็อบเจกต์ `DateTime` พร้อมแล้ว คุณสามารถเก็บมันลงในเซลล์ของ Excel ได้ NPOI จะฟอร์แมตค่า `DateTime` เป็นวันที่ของ Excel โดยอัตโนมัติ

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Result** – การเปิดไฟล์ *JapaneseEraDate.xlsx* จะเห็นวันที่ **2020‑05‑01** อยู่ในเซลล์ A1

### Why use NPOI?

*ทำงานบนแพลตฟอร์มใดก็ได้* (Windows, Linux, macOS) และ **ไม่** ต้องการ Microsoft Office ทำให้โซลูชันนี้เหมาะกับ CI pipelines, Docker containers, หรือการประมวลผลฝั่งเซิร์ฟเวอร์

---

## Step 5: Full, runnable program

รวมทุกอย่างเข้าด้วยกัน นี่คือแอปพลิเคชันคอนโซลเต็มที่สาธิตกระบวนการทั้งหมด:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**How to run**

```bash
dotnet run
```

หลังจากรันเสร็จ คุณจะพบไฟล์ `JapaneseEraDate.xlsx` ในโฟลเดอร์โปรเจกต์พร้อมวันที่ที่แยกวิเคราะห์อย่างถูกต้อง

---

## Common pitfalls and best‑practice tips

| ปัญหา | วิธีแก้ / คำแนะนำ |
|---------|----------------------|
| ลืมตั้งค่า `japaneseCulture.DateTimeFormat.Calendar` | ต้องกำหนดอินสแตนซ์ `JapaneseCalendar` เสมอ; มิฉะนั้นชื่อยุคจะไม่ถูกจดจำ |
| ใช้ `DateTime.TryParse` โดยไม่ระบุ `CultureInfo` ที่กำหนดเอง | ส่ง `japaneseCulture` เดียวกันให้กับ `TryParse` เพื่อให้พฤติกรรมสอดคล้อง |
| คาดว่า Excel จะแสดงชื่อยุค | ฟอร์แมตวันที่ใน Excel มีเฉพาะ Gregorian หากต้องการแสดงยุค ให้เก็บสตริงต้นฉบับในคอลัมน์แยกหรือสร้างฟอร์แมตข้อความแบบกำหนดเอง |
| ไม่ทำการ dispose `FileStream` | ใช้บล็อก `using` (ตามที่แสดง) เพื่อให้แน่ใจว่าไฟล์ถูกปล่อยอย่างทันท่วงที |
| ผสม `CultureInfo` ระหว่างเธรด | `CultureInfo` ปลอดภัยต่อการอ่านหลายเธรด แต่ควรหลีกเลี่ยงการแก้ไขคุณสมบัติ `Calendar` หลังการตั้งค่าเริ่มต้น |

---

## Conclusion

คุณได้เรียนรู้วิธี **use Japanese calendar CultureInfo** ใน C# เพื่อแยกวิเคราะห์วันที่แบบยุคญี่ปุ่นอย่างแม่นยำและเขียน `DateTime` ที่ได้ลงในเซลล์ Excel ด้วย NPOI ตัวอย่างเต็มครอบคลุมการตั้งค่า, การแยกวิเคราะห์, การจัดการข้อผิดพลาด, และการส่งออกเป็น Excel ให้คุณมีพื้นฐานที่มั่นคงสำหรับการทำรายงานหรือการแลกเปลี่ยนข้อมูลในระดับสากล

ต่อไปคุณอาจสนใจ:

* **Formatting dates with custom text** เพื่อเก็บชื่อยุคไว้ใน Excel
* **Reading dates from Excel** ด้วย `cell.DateCellValue` พร้อมคำนึงถึง Japanese calendar
* **Applying the same technique** สำหรับปฏิทินอิงยุคอื่น (เช่น Thai Buddhist calendar) โดยเปลี่ยน `JapaneseCalendar` เป็นคลาส `Calendar` ที่เหมาะสม

อย่าลังเลที่จะทดลองกับสตริงยุคต่าง ๆ, ชุดข้อมูลขนาดใหญ่ขึ้น, หรือผสานตรรกะนี้เข้าไปใน ASP.NET Core API ที่สร้างรายงาน Excel แบบไดนามิก ขอให้สนุกกับการเขียนโค้ด!

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [สร้าง Excel Workbook ด้วยวันที่ Japanese Calendar – คู่มือเต็ม](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [แยกวิเคราะห์ Japanese Era Dates ใน Excel – คู่มือเต็มสำหรับนักพัฒนา C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [วิธีสร้าง Excel workbook และแยกวิเคราะห์วันที่ญี่ปุ่นใน C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}