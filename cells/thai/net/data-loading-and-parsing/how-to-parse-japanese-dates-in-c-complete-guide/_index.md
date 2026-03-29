---
category: general
date: 2026-03-29
description: วิธีแยกวันที่ญี่ปุ่นใน C# ด้วย DateTimeParser และ CultureInfo เรียนรู้การแยกวันที่ตามยุคญี่ปุ่น
  เคล็ดลับการแยกวันที่ใน C# และการจัดการกับกรณีขอบเขต.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: th
og_description: วิธีแยกวันที่ญี่ปุ่นใน C# ด้วย DateTimeParser และ CultureInfo รับวิธีแก้ปัญหาแบบขั้นตอนสำหรับการแยกวันที่ตามสมัยญี่ปุ่น.
og_title: วิธีแปลงวันที่ญี่ปุ่นใน C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- .NET
- DateTime
- Localization
title: วิธีแปลงวันที่ญี่ปุ่นใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแปลงวันที่ภาษาญี่ปุ่นใน C# – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีแปลงวันที่ภาษาญี่ปุ่น** ในสตริงภายในแอปพลิเคชัน .NET หรือไม่? บางทีคุณอาจกำลังทำงานในระบบการเงินที่ได้รับวันที่เช่น “令和3年5月12日” จากลูกค้าชาวญี่ปุ่น และคุณต้องการแปลงเป็น `DateTime` ปกติ คุณไม่ได้อยู่คนเดียว—ปัญหาการแปลภาษามักเกิดขึ้นบ่อยครั้ง  

ข่าวดีคือ ด้วยการตั้งค่าภูมิภาคที่ถูกต้องและคลาสช่วยเหลือขนาดเล็ก เพียงเล็กน้อย **วิธีแปลงวันที่ภาษาญี่ปุ่น** ก็กลายเป็นเรื่องง่าย ในบทแนะนำนี้เราจะเดินผ่านทุกขั้นตอน ตั้งแต่การตั้งค่า `CultureInfo` สำหรับ *ja‑JP* ไปจนถึงการจัดการกรณีขอบเช่นยุคประวัติศาสตร์ เมื่อเสร็จคุณจะมี `DateTimeParser` ที่นำกลับมาใช้ใหม่ได้ซึ่งทำงานกับวันที่ยุคญี่ปุ่นสมัยใหม่ใด ๆ

> **สิ่งที่คุณจะได้รับ** – ตัวอย่างที่สมบูรณ์และสามารถรันได้ คำอธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ เคล็ดลับสำหรับยุคเก่า และเช็คลิสต์สั้น ๆ เพื่อให้คุณไม่พลาดขั้นตอนใดเลย

## ความต้องการเบื้องต้น

- .NET 6+ (หรือ .NET Framework 4.7 + – API ที่เราใช้ไม่มีการเปลี่ยนแปลง)
- ความรู้พื้นฐาน C# (คุณควรคุ้นเคยกับคำสั่ง `using` และ `Console.WriteLine`)
- ไม่ต้องใช้แพ็กเกจ NuGet ภายนอก—ทั้งหมดอยู่ใน `System` และ `System.Globalization`

หากคุณมีโปรเจกต์เปิดอยู่แล้ว เยี่ยม—แค่คัดลอกโค้ดลงไป หากยังไม่มี ให้สร้างแอปคอนโซลใหม่ด้วย `dotnet new console -n JapaneseDateDemo` แล้วคุณก็พร้อมแล้ว

## ขั้นตอนที่ 1: ทำความเข้าใจระบบปฏิทินญี่ปุ่น

ก่อนที่เราจะลงลึกโค้ด มาตอบคำถาม “ทำไม” กันก่อน วันที่ญี่ปุ่นจะถูกแสดงในรูปแบบ **ยุค** (元号) ซึ่งหมายเลขปีจะรีเซ็ตเมื่อจักรพรรดิใหม่ขึ้นครองราชย์ ตัวอย่างเช่น

- **令和** (Reiwa) เริ่มตั้งแต่ 2019‑05‑01
- **平成** (Heisei) ครอบคลุมช่วง 1989‑2019
- **昭和** (Showa) ตั้งแต่ 1926‑1989

คลาส `JapaneseCalendar` ของ .NET มีข้อมูลยุคเหล่านี้อยู่แล้ว แต่คุณต้องบอกตัวแปลงว่าต้องใช้ภูมิภาคใด นั่นคือเหตุผลที่ **cultureinfo ja‑jp** มีความสำคัญ—it เชื่อมปฏิทินกับโลคัลญี่ปุ่น

## ขั้นตอนที่ 2: สร้าง Wrapper ขนาดเล็ก – `DateTimeParser`

แทนที่จะกระจาย `CultureInfo` ไปทั่ว เราจะห่อหุ้มตรรกะไว้ในตัวช่วยขนาดเล็ก ซึ่งทำให้โค้ดนำกลับมาใช้ใหม่ได้และทำให้ส่วนอื่นของแอปสะอาดขึ้น

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**ทำไมต้องมีตัวช่วยนี้?**  
- **ความรับผิดชอบเดียว** – การแปลงที่ขึ้นกับโลคัลทั้งหมดอยู่ในที่เดียว  
- **การจัดการข้อผิดพลาด** – เราแสดงข้อความที่ชัดเจนเมื่อรูปแบบไม่ถูกต้อง  
- **พร้อมอนาคต** – หากต้องการสนับสนุนยุค *Taisho* หรือ *Meiji* เก่า ๆ เพียงปรับแพทเทิร์นหรือเพิ่ม fallback

## ขั้นตอนที่ 3: เชื่อมทุกอย่างใน `Program.cs`

ตอนนี้เราจะใช้ wrapper เพื่อแปลงสตริงตัวอย่าง ดูวิธีที่เราดึงโลคัลญี่ปุ่นด้วย `CultureInfo.GetCultureInfo("ja-JP")` ซึ่งตอบสนองความต้องการ **cultureinfo ja‑jp** และทำให้ `JapaneseCalendar` ทำงาน

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

เมื่อคุณรัน `dotnet run` คุณจะเห็นผลลัพธ์:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

นี่คือแกนหลักของ **วิธีแปลงวันที่ภาษาญี่ปุ่น** ง่ายใช่ไหม?

## ขั้นตอนที่ 4: การจัดการกรณีขอบและยุคเก่า

### 4.1 วันที่ประวัติก่อนปี 1912

`JapaneseCalendar` ที่มาพร้อม .NET รองรับเฉพาะยุคสมัยใหม่ (ตั้งแต่ Meiji ขึ้นไป) หากคุณต้องการแปลงวันที่จากยุค *Taisho* (1912‑1926) หรือ *Meiji* (1868‑1912) แพทเทิร์นเดียวกันก็ใช้ได้—แค่ตรวจสอบให้สตริงมีชื่อยุคที่ถูกต้อง (“大正”, “明治”) ตัวแปลงจะยังคงคืนค่า `DateTime` ของเกรโกเรียนที่ถูกต้อง

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 ไม่มียุค (ข้อมูลที่คลุมเครือ)

หากลูกค้าส่ง “2021年5月12日” โดยไม่มียุค ตัวแปลงจะล้มเหลวเพราะแพทเทิร์นคาดหวังยุค (`ggg`) คุณมีสองทางเลือก

1. **สมมติเป็น Gregorian** – ใช้ fallback ไปยัง `CultureInfo.InvariantCulture` พร้อมแพทเทิร์นอื่น  
2. **ปฏิเสธข้อมูล** – แจ้งผู้เรียกว่าต้องระบุยุค

นี่คือตัวอย่างการปรับแต่งอย่างรวดเร็ว:

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 หมายเหตุเรื่องความปลอดภัยต่อเธรด

อ็อบเจกต์ `CultureInfo` จะเป็นแบบอ่าน‑อย่าง‑เดียวหลังจากสร้างแล้ว ดังนั้นคุณจึงสามารถใช้อินสแตนซ์เดียวกันข้ามเธรดได้อย่างปลอดภัย `DateTimeParser` เองไม่มีสถานะที่เปลี่ยนแปลง ทำให้ **ปลอดภัยต่อเธรด** – ข้อดีสำหรับ API เว็บที่ต้องรับส่งข้อมูลจำนวนมาก

## ขั้นตอนที่ 5: รวมทั้งหมด – ตัวอย่างพร้อมคัดลอก

ด้านล่างเป็นซอร์สเต็มรูปแบบที่คุณสามารถวางลงในโปรเจกต์คอนโซลใหม่ได้ ไม่ต้องใช้แพ็กเกจภายนอก ไม่ต้องพึ่งพาไลบรารีที่ซ่อนอยู่

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}