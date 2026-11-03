---
category: general
date: 2026-10-01
description: แปลงวันที่ตามสมัยญี่ปุ่นเป็นวันที่ตามปฏิทินเกรกอเรียนโดยใช้ Aspose.Cells
  ใน C#. เรียนรู้วิธีแปลงปฏิทินญี่ปุ่นอย่างรวดเร็ว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: th
lastmod: 2026-10-01
og_description: แปลงวันที่ยุคญี่ปุ่นเป็น DateTime เกรกอเรียนใน C#. บทเรียนนี้อธิบายวิธีแปลงปฏิทินญี่ปุ่นอย่างแม่นยำด้วย
  Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: แปลงวันที่ตามสมัยญี่ปุ่นเป็นวันที่เกรกอเรียนใน C# – คู่มือขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: วิธีแปลงวันที่ตามสมัยญี่ปุ่นเป็นปฏิทินเกรกอเรียนใน C#
url: /th/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแปลงวันที่ตามสมัยญี่ปุ่นเป็นวันที่เกรกอเรียนใน C#

หากคุณต้องการ **แปลงสตริงวันที่ตามสมัยญี่ปุ่น** ให้เป็นวันที่เกรกอเรียนใน C# คู่มือนี้จะแสดงวิธีทำอย่างละเอียด ไม่ว่าคุณจะกำลังประมวลผลข้อมูลเก่า, อ่านค่าจากผู้ใช้, หรือสร้างรายงาน, ไลบรารี Aspose.Cells จะทำให้การแปลงเป็นเรื่องง่าย นอกจากนี้คุณยังจะได้พบวิธีที่ดีที่สุดในการ **แปลงปฏิทินญี่ปุ่น** เมื่อทำงานกับสเปรดชีต

บทเรียนนี้ครอบคลุมทุกขั้นตอน—ตั้งแต่การสร้างเวิร์กบุ๊กจนถึงการดึงค่า `DateTime`—เพื่อให้คุณสามารถคัดลอก‑วางโปรแกรมที่ทำงานได้ครบถ้วน ไม่ต้องอ้างอิงเอกสารภายนอก; เพียงทำตามโค้ดและคำอธิบายด้านล่าง

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน, โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+)
* ไลเซนส์สำหรับ **Aspose.Cells** (รุ่นทดลองฟรีใช้สำหรับทดสอบได้)
* สภาพแวดล้อมการพัฒนา เช่น Visual Studio 2022 หรือ VS Code
* ความคุ้นเคยพื้นฐานกับแอปพลิเคชันคอนโซล C#

## แปลงวันที่ตามสมัยญี่ปุ่นด้วย Aspose.Cells

แกนหลักของการแปลงอยู่ในไม่กี่คำสั่ง API ง่าย ๆ Aspose.Cells จะตีความสตริงตามสมัยญี่ปุ่นโดยอัตโนมัติ (เช่น “Reiwa 2/04/01”) และให้ผลลัพธ์เป็นอ็อบเจกต์ `DateTime` หลังจากที่เวิร์กชีตถูกคำนวณใหม่

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### ทำไมแต่ละขั้นตอนจึงสำคัญ

| ขั้นตอน | จุดประสงค์ | วิธีที่ช่วยการแปลง |
|------|---------|-----------------------------|
| **Create workbook** | สร้างคอนเทนเนอร์ที่เข้าใจสูตร Excel และระบบวันที่ | กลไกวันที่ภายในไลบรารีทำงานได้เฉพาะภายในเวิร์กบุ๊ก |
| **Insert era string** | ใส่ข้อความปฏิทินญี่ปุ่นดิบที่ต้องการแปลง | Aspose.Cells จดจำชื่อสมัยเช่น *Reiwa*, *Heisei*, *Showa* เป็นต้น |
| **Set style** | บังคับให้เซลล์ถือเป็นค่าแทนที่จะเป็นสตริงธรรมดา | หากไม่มีสไตล์, เมธอด `Calculate` อาจละเลยเซลล์และทิ้งข้อความไว้ |
| **Calculate** | เริ่มกระบวนการแยกสตริงสมัยและแปลงเป็นเลขซีเรียลของวันที่ | ไลบรารีแปลง “Reiwa 2/04/01” → เลขซีเรียล → `DateTime` เกรกอเรียน |
| **Read `DateTimeValue`** | คืนค่าอ็อบเจกต์ .NET `DateTime` ที่แปลงแล้ว | ตอนนี้คุณมี `DateTime` มาตรฐานที่สามารถใช้กับ API .NET ใดก็ได้ |

## วิธีแปลงปฏิทินญี่ปุ่นในสถานการณ์อื่น ๆ

แนวทางเดียวกันใช้ได้กับชื่อสมัยญี่ปุ่นใด ๆ ที่ Aspose.Cells รองรับ:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### การจัดการสตริงที่ไม่ถูกต้องหรือคล ambiguous

* **ชื่อสมัยไม่ถูกต้อง** – Aspose.Cells จะโยน `FormatException` ให้ห่อการแปลงด้วย `try/catch` เพื่อแสดงข้อความข้อผิดพลาดที่เป็นมิตร
* **ขาดปี/เดือน/วัน** – ไลบรารีคาดหวังรูปแบบเต็ม “Era Year/Month/Day” หากได้รับข้อมูลบางส่วน ให้เติมส่วนที่ขาดหรือปฏิเสธอินพุตตั้งแต่ต้น
* **การตั้งค่าภูมิภาคต่างกัน** – การแปลง **ไม่** พึ่งพา Culture ของเธรดปัจจุบัน; มันใช้แผนที่สมัยญี่ปุ่นที่ฝังอยู่ใน Aspose.Cells เสมอ ทำให้วิธีนี้ปลอดภัยสำหรับการประมวลผลฝั่งเซิร์ฟเวอร์

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## เคล็ดลับปฏิบัติและข้อผิดพลาดที่พบบ่อย

* **ต้องเรียก `SetStyle`** ก่อน `Calculate` เสมอ การข้ามขั้นตอนนี้เป็นสาเหตุของบั๊กบ่อยครั้งเพราะเซลล์ยังคงเป็นตัวเก็บข้อความธรรมดา
* **ใช้เวิร์กบุ๊กเดียวกัน** หากต้องแปลงหลายวันที่ การสร้างเวิร์กบุ๊กใหม่สำหรับแต่ละครั้งจะเพิ่มภาระที่ไม่จำเป็น
* **แปลงเป็นชุด** – เติมคอลัมน์ด้วยสตริงสมัย, เรียก `worksheet.Calculate()` หนึ่งครั้ง, แล้วอ่านคอลัมน์ `DateTimeValue` ทั้งหมด วิธีนี้มีประสิทธิภาพกว่าการคำนวณต่อเซลล์
* **ความเข้ากันได้ของเวอร์ชัน** – โลจิกการแปลงสมัยถูกเพิ่มใน Aspose.Cells 22.9 ตรวจสอบให้แน่ใจว่าคุณใช้เวอร์ชันนี้หรือใหม่กว่า; รุ่นเก่าจะถือสตริงเป็นข้อความธรรมดา

## ตัวอย่างทำงานเต็มรูปแบบ (แอปคอนโซล)

ด้านล่างเป็นโปรแกรมอิสระที่คุณสามารถคอมไพล์และรันได้ทันที แสดงการแปลงทั้ง Reiwa และ Heisei พร้อมการจัดการข้อผิดพลาดอย่างสุภาพ

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

การรันโปรแกรมนี้ยืนยันว่าไลบรารีสามารถ **convert japanese era date** สตริงได้อย่างถูกต้องและรายงานค่าที่ไม่รองรับอย่างเหมาะสม

## สรุป

คุณได้เรียนรู้วิธี **แปลงสตริงวันที่ตามสมัยญี่ปุ่น** ให้เป็นอ็อบเจกต์ `DateTime` เกรกอเรียนมาตรฐานโดยใช้ Aspose.Cells ใน C# กระบวนการสรุปได้เพียงแค่ใส่ข้อความสมัย, ตั้งค่าสไตล์, คำนวณเวิร์กชีต, แล้วอ่าน `DateTimeValue` ด้วยขั้นตอนเหล่านี้คุณยังสามารถตอบคำถามที่กว้างขึ้นเกี่ยวกับ **how to convert Japanese calendar** ในปริมาณมาก, จัดการข้อผิดพลาด, และเพิ่มประสิทธิภาพการทำงานได้อีกด้วย

### ขั้นตอนต่อไป

* สำรวจ **ตัวเลือกการจัดรูปแบบ** เพื่อเขียนวันที่เกรกอเรียนกลับไปยังเวิร์กชีตด้วยรูปแบบตัวเลขที่กำหนดเอง
* ผสานการแปลงนี้กับ **pipeline การนำเข้าข้อมูล** (เช่น การอ่านไฟล์ CSV ที่มีวันที่สมัย)
* ตรวจสอบฟีเจอร์อื่น ๆ ของ Aspose.Cells เช่น **date arithmetic** และ **regional settings** สำหรับสถานการณ์ปฏิทินที่ซับซ้อนยิ่งขึ้น

ขอให้เขียนโค้ดอย่างสนุกสนานและปรับตัวอย่างให้เข้ากับ workflow การประมวลผลข้อมูลของคุณได้เลย!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}