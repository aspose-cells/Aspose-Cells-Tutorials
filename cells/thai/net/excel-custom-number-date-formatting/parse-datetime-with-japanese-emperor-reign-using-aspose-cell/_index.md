---
category: general
date: 2026-09-24
description: แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่นโดยใช้ Aspose.Cells ใน C#.
  เปิดใช้งานปฏิทินยุคจักรพรรดิญี่ปุ่น, เขียนสตริงยุค, และดึงค่า DateTime ที่แม่นยำ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: th
lastmod: 2026-09-24
og_description: แยกวิเคราะห์ DateTime ด้วยรัชสมัยของจักรพรรดิญี่ปุ่นโดยใช้ Aspose.Cells
  ใน C# บทเรียนนี้แสดงวิธีเปิดใช้งานปฏิทินยุคญี่ปุ่น, เขียนสตริงยุค, และอ่านคืน DateTime
  ที่ถูกต้อง.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่นโดยใช้ Aspose.Cells – คู่มือ
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่นโดยใช้ Aspose.Cells
url: /th/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่นโดยใช้ Aspose.Cells

หากคุณต้องการ **แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่น** ในแอปพลิเคชัน .NET คู่มือนี้จะแสดงวิธีทำอย่างละเอียดด้วย Aspose.Cells โดยการเปิดใช้งานปฏิทินยุคจักรพรรดิญี่ปุ่น, เขียนสตริงที่อิงรัชกาล, และอ่านค่า `DateTime` ที่ได้ คุณจะได้วันที่ที่เชื่อถือได้และรับรู้วัฒนธรรมโดยไม่ต้องทำการจัดการสตริงด้วยตนเอง

การทำงานกับวันที่ตามยุคญี่ปุ่นเป็นเรื่องทั่วไปในด้านการเงิน, รัฐบาล, และระบบเดิมที่ยังคงเก็บวันที่ในรูปแบบเช่น “令和3年5月10日”. บทแนะนำนี้ครอบคลุมกระบวนการทำงานทั้งหมด ตั้งแต่การตั้งค่าโปรเจกต์จนถึงการดึงอ็อบเจ็กต์ `DateTime` ที่คุณสามารถใช้ในการคำนวณ, การบันทึก, หรือการแสดงผล UI

## สิ่งที่คุณจะได้เรียนรู้

- วิธีเพิ่มแพ็กเกจ NuGet ของ Aspose.Cells ลงในโปรเจกต์ C#  
- วิธีเปิดใช้งาน **ปฏิทินยุคจักรพรรดิญี่ปุ่น** ผ่าน `Workbook.Settings`  
- วิธีเขียนสตริงวันที่ตามยุคญี่ปุ่นลงในเซลล์และให้ Aspose.Cells แปลงอัตโนมัติ  
- วิธีอ่านค่า `DateTime` ที่แปลงแล้วโดยใช้คุณสมบัติ `DateTimeValue`  

**ข้อกำหนดเบื้องต้น**  
- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)  
- ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ใดก็ได้)  
- การเชื่อมต่ออินเทอร์เน็ตเพื่อดาวน์โหลดแพ็กเกจ Aspose.Cells  

---

## ขั้นตอนที่ 1: ติดตั้ง Aspose.Cells

เปิดโฟลเดอร์โปรเจกต์ของคุณในเทอร์มินัลหรือใน NuGet Package Manager Console แล้วรัน:

```bash
dotnet add package Aspose.Cells
```

หรือใน Visual Studio ให้คลิกขวาที่โปรเจกต์ → **Manage NuGet Packages** → ค้นหา **Aspose.Cells** แล้วคลิก **Install**.  
การทำเช่นนี้จะเพิ่ม assembly `Aspose.Cells` ที่ให้ `Workbook`, `Worksheet`, และความสามารถในการแปลงที่เราต้องการ

## ขั้นตอนที่ 2: เปิดใช้งานปฏิทินยุคจักรพรรดิญี่ปุ่น

Aspose.Cells ปิดการแปลงยุคญี่ปุ่นโดยค่าเริ่มต้น คุณต้องเปิดใช้งานผ่านแฟล็ก `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

การตั้งค่า `UseJapaneseEraCalendar` เป็น `true` จะบอกไลบรารีให้ตีความสตริงที่มีชื่อยุค (`令和`, `平成`, `昭和` ฯลฯ) ตามกฎของปฏิทินญี่ปุ่นอย่างเป็นทางการ

## ขั้นตอนที่ 3: เขียนสตริงวันที่ตามรัชกาลญี่ปุ่นลงในเซลล์

ต่อไปให้ดึงแผ่นงานแรกและใส่สตริงวันที่ตามยุคญี่ปุ่นลงในเซลล์ **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**ทำไมวิธีนี้ถึงได้ผล:**  
เมื่อ `UseJapaneseEraCalendar` ทำงานอยู่, `PutValue` จะตรวจสอบสตริง, ตรวจจับคำนำหน้ายุค (`令和`), และแปลงภายในเป็นปีตามปฏิทินเกรโกเรียนที่สอดคล้อง (2021). ไลบรารีจะเก็บค่าเป็นอ็อบเจ็กต์ `DateTime` จริง, ไม่ใช่แค่ข้อความเท่านั้น

## ขั้นตอนที่ 4: ดึงค่าที่แปลงเป็น `DateTime`

ตอนนี้ให้อ่าน `DateTimeValue` ของเซลล์. Aspose.Cells จะคืนค่าปฏิทินเกรโกเรียนโดยอัตโนมัติ.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

เมื่อรันโปรแกรมจะแสดงผล:

```
Parsed Gregorian date: 2021-05-10
```

ผลลัพธ์ยืนยันว่า **แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่น** ได้แปลง “令和3年5月10日” เป็นวันที่ 10 พฤษภาคม 2021 อย่างถูกต้อง

## ขั้นตอนที่ 5: จัดการกรณีขอบและรูปแบบทั่วไป

### รูปแบบยุคหลายแบบ
Aspose.Cells จดจำรูปแบบยุคหลายแบบ:

| ยุค (ญี่ปุ่น) | ช่วงปี Gregorian |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

หากข้อมูลต้นทางของคุณผสมอักขระเต็มความกว้าง, ช่องว่าง, หรือใช้คันจิ “年”, “月”, “日”, ตัวแปลงยังคงทำงานได้ ตัวอย่างเช่น `"平成31年4月30日"` จะกลายเป็น `2019-04-30`.

### สตริงที่ไม่ถูกต้อง
เมื่อสตริงไม่สามารถแปลงได้ (เช่น `"令和99年13月40日"`), `DateTimeValue` จะคืนค่า `DateTime.MinValue`. คุณสามารถตรวจสอบเงื่อนไขนี้ได้:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### ปิดการใช้งานฟีเจอร์
หากภายหลังต้องการเก็บสตริงยุคเดิมโดยไม่แปลง, ให้ตั้งค่าแฟล็กกลับเป็น `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### เคล็ดลับประสิทธิภาพ
การเปิดใช้งานปฏิทินยุคเพิ่มภาระเล็กน้อยให้กับทุกการเรียก `PutValue` ที่เกี่ยวกับสตริง. หากคุณต้องแปลงเพียงไม่กี่เซลล์, ให้เปิดแฟล็กก่อนทำงานและปิดหลังเสร็จเพื่อให้ผลกระทบต่ำสุด

## ตัวอย่างที่สมบูรณ์และสามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก, วาง, และรันได้ทันที.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

```
Parsed Gregorian date: 2021-05-10
```

โปรแกรมนี้แสดงกระบวนการจากต้นจนจบสำหรับ **แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่น** ด้วย Aspose.Cells, ตั้งแต่การสร้าง workbook จนถึงการได้อ็อบเจ็กต์ `DateTime` ที่ใช้งานได้

---

## สรุป

คุณได้เรียนรู้วิธี **แปลง DateTime ด้วยรัชกาลของจักรพรรดิญี่ปุ่น** ใน C# โดย:

1. ติดตั้ง **Aspose.Cells**  
2. เปิดใช้งาน **ปฏิทินยุคจักรพรรดิญี่ปุ่น** ผ่าน `Workbook.Settings`  
3. เขียนสตริงตามยุคลงในเซลล์  
4. อ่านค่า `DateTimeValue` ที่ได้  

วิธีนี้ช่วยขจัดตรรกะการแปลงด้วยตนเอง, เคารพขอบเขตยุคอย่างเป็นทางการ, และทำงานร่วมกับโค้ดจัดการวันที่ของ .NET ได้อย่างราบรื่น  

**ขั้นตอนต่อไป**  
- สำรวจฟีเจอร์เฉพาะวัฒนธรรมอื่นของ Aspose.Cells, เช่น **การแปลงวันที่** สำหรับปฏิทินฮิจรีหรือพุทธศักราชไทย  
- ผสานเทคนิคนี้กับ **Workbook Settings** เช่น `CalcEngine` เพื่อประเมินสูตรที่อ้างอิงวันที่ตามยุค  
- ใช้ `DateTime` ที่แปลงแล้วในรายงาน, การจัดเก็บฐานข้อมูล, หรือคอมโพเนนต์ UI ที่ต้องการวันที่เกรโกเรียน  

อย่าลังเลทดลองกับสตริงยุคต่าง ๆ, จัดการอินพุตที่ไม่ถูกต้อง, และรวมโซลูชันนี้เข้าไปใน pipeline การนำเข้าข้อมูลขนาดใหญ่. Happy coding!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่นในโปรเจกต์ของคุณ

- [แปลงวันที่ตามยุคญี่ปุ่นใน Excel – คู่มือเต็มสำหรับนักพัฒนา C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [วิธีแปลงวันที่ญี่ปุ่นใน C# – คู่มือครบถ้วน](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [วิธีทำการตรวจสอบความถูกต้องของวันที่ใน .NET ด้วย Aspose.Cells: คู่มือเชิงลึก](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}