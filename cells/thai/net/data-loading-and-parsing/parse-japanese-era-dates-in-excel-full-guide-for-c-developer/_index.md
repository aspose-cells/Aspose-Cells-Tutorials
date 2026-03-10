---
category: general
date: 2026-02-14
description: แยกวิเคราะห์วันที่ตามสมัยญี่ปุ่นใน Excel ด้วยการแปลงวันที่แบบกำหนดเอง
  เรียนรู้วิธีโหลดเวิร์กบุ๊กจากไฟล์โดยใช้ load excel พร้อมตัวเลือกและหลีกเลี่ยงข้อผิดพลาดทั่วไป
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: th
og_description: แยกวิเคราะห์วันที่ตามสมัยญี่ปุ่นใน Excel ด้วย Aspose.Cells คู่มือนี้แสดงวิธีโหลดเวิร์กบุ๊กจากไฟล์พร้อมตัวเลือกการแยกวิเคราะห์วันที่แบบกำหนดเอง.
og_title: แปลงวันที่สมัยญี่ปุ่น – บทเรียน C# ทีละขั้นตอน
tags:
- Aspose.Cells
- C#
- Excel automation
title: แปลงวันที่ตามสมัยญี่ปุ่นใน Excel – คู่มือเต็มสำหรับนักพัฒนา C#
url: /th/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

Now ensure we preserve markdown formatting, headings, lists, tables, code placeholders.

Check for any other markdown links: none.

Now produce final content with translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แยกวิเคราะห์วันที่ตามยุคญี่ปุ่น – คำแนะนำ C# ฉบับสมบูรณ์

เคยต้อง **แยกวิเคราะห์วันที่ตามยุคญี่ปุ่น** จากแผ่น Excel แล้วสงสัยว่าทำไมค่าต่าง ๆ ถึงแปลงเป็นตัวเลขแปลก ๆ หรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจอปัญหานี้เมื่อตัวแยกวิเคราะห์ `DateTime` เริ่มต้นไม่รู้จักรูปแบบ “Reiwa 1/04/01” ที่ใช้ในปฏิทินญี่ปุ่น  

ข่าวดี: คุณสามารถบอก Aspose.Cells ให้จัดการเซลล์เหล่านั้นเป็นวันที่ตามยุคญี่ปุ่นตั้งแต่คุณ **load Excel with options**. ในคู่มือนี้เราจะอธิบายขั้นตอนการโหลดเวิร์กบุ๊กจากไฟล์, การกำหนดค่าการแยกวิเคราะห์วันที่แบบกำหนดเอง, และการตรวจสอบว่าข้อมูลวันที่ออกมาตรงตามที่คุณคาดหวัง  

โดยตอนจบของบทเรียนนี้คุณจะสามารถ:

* โหลดเวิร์กบุ๊กจากไฟล์พร้อมระบุ `DateTimeParsing.JapaneseEra`.
* เข้าถึงค่าของเซลล์เป็นอ็อบเจ็กต์ `DateTime` ที่ถูกต้อง.
* จัดการกรณีขอบเช่นเซลล์ว่างหรือปฏิทินผสม.
* ขยายวิธีนี้ไปยังสถานการณ์ **custom date parsing excel** ใด ๆ ที่คุณอาจเจอ.

> **Prerequisite** – คุณต้องมีไลบรารี Aspose.Cells for .NET (เวอร์ชัน 23.9 หรือใหม่กว่า) และ IDE ที่รองรับ .NET (Visual Studio, Rider ฯลฯ) ไม่จำเป็นต้องใช้แพคเกจอื่นใด  

---

## ขั้นตอนที่ 1: กำหนดค่า Text Load Options สำหรับการแยกวิเคราะห์วันที่ตามยุคญี่ปุ่น  

สิ่งแรกที่เราทำคือบอกให้ตัวโหลดเข้าใจข้อความที่ดูเหมือนวันที่ตามยุคญี่ปุ่น ซึ่งทำได้ผ่าน `TxtLoadOptions` และ enum `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**ทำไมสิ่งนี้ถึงสำคัญ:** หากไม่มีแฟล็ก `JapaneseEra` Aspose.Cells จะถือเซลล์เป็นสตริงธรรมดา ทำให้คุณต้องแยกชื่อยุคและแปลงด้วยตนเอง แฟล็กนี้ทำงานหนักแทนคุณ ทำให้โค้ดสะอาดและลดความผิดพลาด  

---

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กจากไฟล์โดยใช้ตัวเลือก  

ตอนนี้เราจะเปิดไฟล์ Excel จริง ๆ ให้สังเกตว่าอ็อบเจ็กต์ `loadOptions` ถูกส่งไปยังคอนสตรัคเตอร์ `Workbook`—นี่คือขั้นตอน **load workbook from file** ที่เคารพกฎการแยกวิเคราะห์ที่กำหนดเองของเรา.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

หากไฟล์อยู่ที่อื่น (เช่นแชร์เครือข่าย) ให้ปรับ `filePath` ตามนั้น ส่วนสำคัญคือใช้อินสแตนซ์ `loadOptions` เดียวกัน; มิฉะนั้นการแปลงยุคญี่ปุ่นจะไม่ทำงาน  

---

## ขั้นตอนที่ 3: เข้าถึงวันที่ที่แยกวิเคราะห์แล้ว  

เมื่อเวิร์กบุ๊กโหลดแล้ว คุณสามารถดึงค่าของเซลล์ได้เช่นเดียวกับวันที่ปกติ API จะคืนค่าอ็อบเจ็กต์ `DateTime` โดยอัตโนมัติ

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า A1 มีค่า “R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

หากเซลล์มีวันที่ตามปฏิทินเกรกอเรียนเช่น “2023‑12‑31” ตัวแยกวิเคราะห์ยังทำงาน—มันจะคืนค่าวันที่เดิมโดยไม่เปลี่ยนแปลง  

---

## ขั้นตอนที่ 4: ตรวจสอบวันที่ทั้งหมดในคอลัมน์  

บ่อยครั้งคุณต้องสแกนคอลัมน์ทั้งหมดของวันที่ตามยุคญี่ปุ่น ด้านล่างเป็นลูปแบบกะทัดรัดที่แสดงวิธีจัดการเซลล์ว่างและเนื้อหาผสมอย่างราบรื่น

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**เคล็ดลับ:** `CellValueType.IsDateTime` เป็นวิธีที่ปลอดภัยที่สุดในการตรวจสอบว่าตัวแยกวิเคราะห์สำเร็จหรือไม่ มันป้องกัน `InvalidCastException` เมื่อเซลล์มีข้อความที่ไม่คาดคิด  

---

## ขั้นตอนที่ 5: ข้อผิดพลาดทั่วไปและวิธีจัดการ  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **เซลล์ว่างคืนค่า `DateTime.MinValue`** | ตัวแยกวิเคราะห์ถือสตริงว่างเป็นวันที่ขั้นต่ำ. | ตรวจสอบ `cell.IsNull` ก่อนเข้าถึง `DateTimeValue`. |
| **ปฏิทินผสม (ญี่ปุ่น + เกรกอเรียน) ในคอลัมน์เดียว** | ตัวแยกวิเคราะห์จัดการทั้งสองแบบได้ แต่คุณอาจต้องแยกแยะสำหรับการรายงาน. | ใช้ `cell.StringValue` เพื่อตรวจสอบข้อความต้นฉบับเมื่อ `cell.Type` เป็น `IsString`. |
| **ยุคไม่ถูกต้อง (เช่น “H30” สำหรับ Heisei) หลังปี 2019** | Heisei สิ้นสุดในปี 2019; วันที่หลังจากนั้นควรใช้ “R”. | ตรวจสอบคำนำหน้ายุคก่อนเชื่อผลลัพธ์ที่แยกวิเคราะห์. |
| **ประสิทธิภาพช้าลงเมื่อไฟล์ใหญ่** | การโหลดด้วยตัวเลือกกำหนดเองเพิ่มภาระงานเล็กน้อย. | โหลดเฉพาะเวิร์กชีตที่ต้องการ (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## ขั้นตอนที่ 6: ตัวอย่างทำงานเต็มรูปแบบ  

รวมทุกอย่างเข้าด้วยกัน นี่คือแอปคอนโซลแบบ self‑contained ที่คุณสามารถคัดลอก‑วางและรันได้ มันแสดง **custom date parsing excel** ตั้งแต่ต้นจนจบ

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**สิ่งที่คุณควรเห็น** เมื่อไฟล์ `japan_dates.xlsx` มี:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (blank) | R2/02/15 |

ผลลัพธ์ในคอนโซล:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

ไฟล์ที่บันทึกแล้วจะเก็บเซลล์วันที่ที่ถูกต้อง ซึ่งคุณสามารถเปิดใน Excel และเห็นรูปแบบวันที่ตามปกติ  

---

## สรุป  

เราได้แสดงวิธี **แยกวิเคราะห์วันที่ตามยุคญี่ปุ่น** ใน Excel โดยกำหนดค่า `TxtLoadOptions`, **load workbook from file** ด้วยตัวเลือกเหล่านั้น และทำงานกับค่า `DateTime` ที่ได้ รูปแบบเดียวกัน—การตั้งค่าแฟล็กการแยกวิเคราะห์แบบกำหนดเองแล้วโหลดเวิร์กบุ๊ก—ใช้ได้กับความต้องการ **custom date parsing excel** ใด ๆ ไม่ว่าจะเป็นช่วงงบประมาณ, หมายเลขสัปดาห์ ISO, หรือรูปแบบเฉพาะ  

มียุคอื่นหรือสเปรดชีตที่มีปฏิทินผสม? เพียงเปลี่ยน `DateTimeParsing.JapaneseEra` เป็นค่า enum อื่น (เช่น `DateTimeParsing.Custom`) และให้สตริงรูปแบบ ความยืดหยุ่นของ Aspose.Cells ทำให้คุณไม่ต้องเขียนโค้ดแปลงด้วยตนเองบ่อยครั้ง  

**ขั้นตอนต่อไป** ที่คุณอาจสำรวจ:

* **Load Excel with options** สำหรับไฟล์ CSV (`CsvLoadOptions`) เพื่อจัดการตัวคั่นตามภูมิภาค.  
* ใช้ `Workbook.Save` กับ `SaveFormat.Xlsx` เพื่อส่งออกข้อมูลที่ทำความสะอาด.  
* ผสานวิธีนี้กับ **Aspose.Slides** หรือ **Aspose.Words** สำหรับกระบวนการรายงาน.  

ลองใช้ปรับตัวเลือก แล้วให้ไลบรารีทำงานหนักแทนคุณ โค้ดดิ้งให้สนุก!  

![Screenshot of parsed Japanese era dates in a console window – parse japanese era dates example](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}