---
category: general
date: 2026-06-27
description: เรียนรู้วิธีแยกวันที่ตามสมัยญี่ปุ่นใน C# แล้วจัดรูปแบบ datetime yyyy‑mm‑dd
  สำหรับการแสดงผลแบบ ISO โค้ดทีละขั้นตอน กรณีขอบ และเคล็ดลับ
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: th
og_description: แปลงวันที่ตามสมัยญี่ปุ่นใน C# และจัดรูปแบบวันที่ yyyy‑mm‑dd อย่างง่ายดาย
  ตัวอย่างครบถ้วนพร้อมคำอธิบายและข้อควรระวัง
og_title: แปลงวันที่ตามสมัยญี่ปุ่นใน C# – คู่มือการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: แปลงวันที่สมัยญี่ปุ่นใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แยกวันที่ตามยุคญี่ปุ่นใน C# – คู่มือฉบับสมบูรณ์

เคยต้อง **แยกวันที่ตามยุคญี่ปุ่น** ในแอป .NET แล้วสงสัยว่าผลลัพธ์ดูแปลกไหม? คุณไม่ได้เป็นคนเดียว ในระบบเก่าหลายระบบ วันที่มักอยู่ในรูปแบบ “R3‑04‑01” และคุณต้องแปลงเป็นสตริง **format datetime yyyy-mm-dd** ที่สะอาดสำหรับ API หรือฐานข้อมูล  

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนที่แม่นยำเพื่อทำให้สำเร็จ อธิบายว่าทำไมแต่ละส่วนจึงสำคัญ และแสดงวิธีจัดการกับกรณีขอบที่ซับซ้อนซึ่งมักทำให้ผู้พัฒนาติดขัด

> **หมายเหตุ:** โค้ดทั้งหมดพร้อมคัดลอก‑วางลงในแอปคอนโซลที่ใช้ .NET 6 หรือใหม่กว่า.

## สิ่งที่คุณต้องการ

- .NET 6 SDK (หรือเวอร์ชันล่าสุดใดก็ได้)
- ความคุ้นเคยพื้นฐานกับ C# และเนมสเปซ `System.Globalization`
- IDE หรือ editor – Visual Studio, VS Code, Rider, หรืออะไรก็ตามที่คุณชอบ

ไม่มีแพคเกจ NuGet ภายนอกที่จำเป็น; ทุกอย่างอยู่ใน BCL.

## ขั้นตอนที่ 1: ตั้งค่าภูมิภาคญี่ปุ่นพร้อมปฏิทินจักรพรรดิ

ก่อนอื่น เราต้องการ `CultureInfo` ที่รู้จักปฏิทินจักรพรรดิของญี่ปุ่น โดยค่าเริ่มต้น `ja-JP` ใช้ปฏิทินเกรกอเรียน ดังนั้นเราจึงแทนที่ `DateTimeFormat.Calendar` ด้วยอินสแตนซ์ของ `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** `JapaneseCalendar` แปลสัญลักษณ์ยุค (เช่น “R” สำหรับ Reiwa) ให้เป็นปีเกรกอเรียนที่ถูกต้อง หากไม่มีมัน `DateTime.Parse` จะโยน `FormatException`.

## ขั้นตอนที่ 2: แยกสตริงวันที่ตามยุค

ตอนนี้เราสามารถส่งสตริงเช่น `"R3-04-01"` ให้กับ `DateTime.Parse` ได้ วัฒนธรรมที่เราตั้งค่าไว้บอกตัวแยกวิเคราะห์ว่าจะตีความส่วน “R3” อย่างไร

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

หากคุณต้องการวิธีที่ปลอดภัยกว่าและหลีกเลี่ยงข้อยกเว้นจากอินพุตที่ไม่ถูกต้อง ให้เปลี่ยน `Parse` เป็น `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **เคล็ดลับ:** รูปแบบสตริงกำหนดเอง `"ggy-MM-dd"` บอกตัวแยกวิเคราะห์อย่างชัดเจนว่าต้องคาดหวังอะไร “gg” คือสัญลักษณ์ยุค, “y” คือปีภายในยุคนั้น

## ขั้นตอนที่ 3: แปลงผลลัพธ์เป็น ISO 8601 (`format datetime yyyy-mm-dd`)

สุดท้าย เราแสดง `DateTime` ในรูปแบบ ISO มาตรฐาน ตัวระบุรูปแบบ `"yyyy-MM-dd"` ทำหน้าที่นั้นโดยตรง

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

การรันโปรแกรมจะแสดงผล:

```
2021-04-01
```

นั่นคือ **format datetime yyyy-mm-dd** ที่คุณต้องการ พร้อมใช้ใน JSON payloads, การแทรก SQL, หรือระบบ downstream ใด ๆ

![parse japanese era date example](placeholder.png){alt="ตัวอย่างการแยกวันที่ตามยุคญี่ปุ่น"}

## การจัดการยุคอื่นและกรณีขอบ

### หลายยุค

ญี่ปุ่นเคยผ่านหลายยุค (Meiji, Taishō, Shōwa, Heisei, Reiwa) `JapaneseCalendar` จะแมปอัตโนมัติ ดังนั้น `"H30-12-31"` (Heisei 30) จะกลายเป็น `2018-12-31` เพียงใช้ตรรกะการแยกเดียวกัน ปฏิทินจะทำงานหนักให้คุณ

### อินพุตไม่ถูกต้อง

หากสตริงไม่ตรงกับรูปแบบที่คาดไว้ `Parse` จะโยนข้อยกเว้น ใช้ `TryParseExact` ตามที่แสดงก่อนหน้า หรือทำการตรวจสอบล่วงหน้าด้วย regular expression:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### โซนเวลา

อ็อบเจกต์ `DateTime` มีค่า “kind” ที่ไม่ระบุโดยค่าเริ่มต้น หากคุณต้องการ timestamp แบบ UTC ให้เรียก:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

หรือใช้ `DateTimeOffset` เพื่อรับรู้โซนเวลาอย่างเต็มที่

## ตัวอย่างทำงานเต็มรูปแบบ

นี่คือโค้ดทั้งหมดที่คุณสามารถวางลงในโปรเจกต์คอนโซลใหม่ได้:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**ผลลัพธ์ที่คาดหวังในคอนโซล**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## สรุป

เราได้อธิบายวิธี **แยกวันที่ตามยุคญี่ปุ่น** ด้วยการ:

1. สร้าง `CultureInfo` สำหรับ `ja-JP` แล้วสลับเป็น `JapaneseCalendar`
2. ใช้ `DateTime.Parse` หรือ `TryParseExact` ที่มีความทนทานมากขึ้นพร้อมรูปแบบกำหนดเอง
3. ฟอร์แมต `DateTime` ที่ได้ด้วย `"yyyy-MM-dd"` เพื่อให้ได้ **format datetime yyyy-mm-dd** ที่ต้องการ

เท่านี้คุณก็พร้อมเชื่อมต่อข้อมูลวันที่ตามยุคเก่าเข้าสู่ระบบสมัยใหม่ที่เป็นมาตรฐาน ISO

## ถัดไปคืออะไร?

- **การประมวลผลเป็นชุด:** วนลูปไฟล์ CSV ของวันที่ตามยุคและเขียนสตริง ISO ลงฐานข้อมูล
- **การแปลภาษา:** แปลงวันที่ ISO กลับเป็นรูปแบบยุคสำหรับการแสดง UI (`ToString("ggyy年MM月dd日", japaneseCulture)`)
- **ปฏิทินแบบกำหนดเอง:** สำรวจ `TaiwanCalendar` หรือ `HijriCalendar` สำหรับความต้องการภูมิภาคอื่น ๆ

ลองทดลองได้เลย—สลับสตริงยุค, ทดสอบกรณีขอบ, หรือรวมตรรกะนี้เข้าไปใน endpoint ของ ASP.NET Core หากเจอปัญหาใด ๆ แสดงความคิดเห็นด้านล่างได้เลย; Happy coding!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [วิธีการตรวจสอบความถูกต้องของวันที่ใน .NET ด้วย Aspose.Cells: คู่มือฉบับสมบูรณ์](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [วิธีการสร้างและจัดรูปแบบคอมเมนต์ใน Excel ด้วย Aspose.Cells สำหรับ .NET: คู่มือขั้นตอนต่อขั้นตอน](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}