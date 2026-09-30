---
category: general
date: 2026-05-23
description: วิธีแยกวันที่จากเซลล์ Excel ด้วย C#. เรียนรู้เทคนิคการจัดรูปแบบตัวเลขแบบกำหนดเองใน
  Excel, อ่านวันที่จากเซลล์, และใช้รูปแบบกำหนดเองเพื่อให้ได้ผลลัพธ์ที่แม่นยำ.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: th
og_description: วิธีแยกวันที่จากเซลล์ Excel ด้วย C# บทเรียนนี้แสดงวิธีใช้รูปแบบตัวเลขแบบกำหนดเองใน
  Excel อ่านวันที่จากเซลล์ และจัดรูปแบบวันที่ในเซลล์ Excel อย่างถูกต้อง
og_title: วิธีแปลงวันที่ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: วิธีแปลงวันที่ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแยกวิเคราะห์วันที่ใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **วิธีแยกวิเคราะห์วันที่** ที่เก็บอยู่ในแผ่นงาน Excel โดยไม่ต้องจัดการการแปลงสตริงด้วยตนเอง? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะดึงวันที่ตามปฏิทินญี่ปุ่น, การจัดรูปแบบเดือน‑วันแบบยุโรป, หรือสตริงที่ขึ้นกับภาษาท้องถิ่นใด ๆ การได้ `DateTime` ที่เชื่อถือได้ใน C# อาจรู้สึกเหมือนตามล่าหากเป้าหมายที่เคลื่อนที่  

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่เป็นรูปธรรมและครบวงจรที่ **applies a custom number format Excel** ให้กับเซลล์ข้อความ, แล้ว **reads date from cell** เป็น `DateTime` ที่ถูกต้อง สุดท้ายคุณจะรู้วิธี **format Excel cell date**, **apply custom format**, และหลีกเลี่ยงข้อผิดพลาดทั่วไปที่ทำให้นักพัฒนาส่วนใหญ่ติดขัด

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core, .NET Framework, และ .NET 5+)
- การอ้างอิงไลบรารีสเปรดชีตที่รองรับการจัดการสไตล์ – ตัวอย่างใช้ **Aspose.Cells**, แต่แนวคิดสามารถนำไปใช้กับ EPPlus, ClosedXML, หรือ NPOI
- ความรู้พื้นฐานของ C# (คุณทำได้อยู่แล้วใช่ไหม?)

> **Pro tip:** หากคุณยังไม่มี Aspose.Cells, คุณสามารถดาวน์โหลดเวอร์ชันทดลองฟรีจากเว็บไซต์ของพวกเขาและเพิ่มผ่าน NuGet: `dotnet add package Aspose.Cells`.

## ภาพรวมของโซลูชัน

1. **Create a workbook** และเลือกเซลล์แรกของแผ่นงานแรก  
2. **Insert a locale‑specific date string** (กรณีนี้เป็นวันที่ญี่ปุ่น)  
3. **Apply a custom number format** ที่บอก Excel ให้ถือสตริงเป็นวันที่  
4. **Read the cell value** กลับมาเป็นอ็อบเจ็กต์ `DateTime`  

นี่คือกระบวนการทั้งหมด – ไม่มีการแยกวิเคราะห์ด้วยตนเอง, ไม่มีการใช้ `DateTime.ParseExact` ที่ซับซ้อน มาดูรายละเอียดกัน

---

## Step 1: Set Up the Workbook and Target Cell

เริ่มต้นโดยสร้าง workbook ใหม่และดึงเซลล์ที่เราจะทำงานด้วย ซึ่งสอดคล้องกับสถานการณ์ “workbook ใหม่” ที่งานประมวลผลแบบแบตช์ส่วนใหญ่เริ่มต้นจาก

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Why this matters:** การสร้าง workbook ด้วยโปรแกรมทำให้เราควบคุมทุกแง่มุมของไฟล์ – ไม่มีการจัดรูปแบบที่ซ่อนอยู่ `Cell` object เป็นจุดเริ่มต้นของทั้งเนื้อหาและสไตล์

---

## Step 2: Insert a Japanese Date String

Excel มักรับวันที่เป็นข้อความธรรมดาโดยเฉพาะเมื่อข้อมูลมาจากระบบเก่า ที่นี่เราจำลองโดยใส่วันที่ตามยุคญี่ปุ่นลงในเซลล์โดยตรง

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Edge case note:** หากเซลล์นั้นมีค่าเป็นวันที่ Excel จริง (เลขซีเรียล) คุณสามารถข้ามขั้นตอนการกำหนดรูปแบบแบบกำหนดเองได้ คู่มือนี้มุ่งเน้นที่เส้นทางการแปลง *text‑to‑date*

---

## Step 3: Apply a Custom Number Format That Interprets the Text as a Date

ตอนนี้มาถึงจุดสำคัญ: เราบอก Excel ให้ตีความสตริงโดยใช้ **custom number format Excel** ที่รองรับภาษาญี่ปุ่น สตริงรูปแบบ `[$-ja-JP]yyyy` จะดึงส่วนปีออกมา, แต่คุณสามารถขยายให้รวมเดือนและวันได้ตามต้องการ

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### ทำไมรูปแบบกำหนดเองจึงได้ผล

Excel เก็บวันที่เป็นเลขซีเรียลภายใน โดยการกำหนดรูปแบบที่รับรู้ภาษาท้องถิ่น, Excel จะพยายาม *ตีความ* ข้อความตามแพทเทิร์นนั้น คำสั่ง `[$-ja-JP]` บังคับให้ใช้กฎปฏิทินญี่ปุ่น, ส่วนที่เหลือของแพทเทิร์นจะแมปอักขระเป็นปี, เดือน, และวัน

> **Alternative:** หากต้องการวิธีที่ทั่วไปกว่า, คุณสามารถใช้ `[$-en-US]mm/dd/yyyy` สำหรับรูปแบบวันที่สไตล์สหรัฐอเมริกา, หรือใช้รหัสวัฒนธรรมอื่นใดที่ Windows รองรับ

---

## Step 4: Retrieve the Parsed Date as a `DateTime` Object

สุดท้ายเราขอค่า `DateTimeValue` จากเซลล์ Aspose.Cells จะทำการแปลงข้อความที่มีรูปแบบเป็นอ็อบเจ็กต์ `DateTime` ที่ถูกต้องโดยอัตโนมัติ

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Expected console output**

```
Parsed date: 2021-05-12
```

> **What if it returns `DateTime.MinValue`?** ปกติหมายความว่ารูปแบบไม่ตรงกับเนื้อหาในเซลล์ ตรวจสอบสตริงรูปแบบกำหนดเองอีกครั้งและให้แน่ใจว่ารหัสภาษาตรงกับภาษาต้นฉบับ

---

## Bonus: Handling Other Locales and Real‑World Variations

### 1. Parsing European Dates (e.g., “12/05/2021” in French)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. When the Cell Already Contains a Serial Date

หากไฟล์ Excel ต้นทางมีค่าเป็นวันที่จริงอยู่แล้ว คุณสามารถข้ามขั้นตอนการกำหนดรูปแบบกำหนดเองได้เลย:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Fallback to Manual Parsing

บางครั้งข้อมูลอาจสกปรก (ช่องว่างเพิ่ม, ตัวอักษรซ่อน) วิธีสำรองที่ปลอดภัยคือ:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

แต่แนวทาง **apply custom format** มักจะเร็วกว่าและมีโอกาสเกิดข้อผิดพลาดน้อยกว่า เพราะใช้กลไกการแยกวิเคราะห์ของ Excel เอง

---

## Common Pitfalls and How to Avoid Them

| ปัญหา | อาการ | วิธีแก้ |
|-------|-------|--------|
| รหัสภาษาผิด (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` ค้างที่ `1/1/1900` | ตรวจสอบสตริง LCID ให้แม่นยำ; ใช้ `CultureInfo.GetCultureInfo("ja-JP").LCID` เพื่อความแน่ใจ |
| ขาดเครื่องหมายอัญประกาศรอบข้อความคงที่ | Excel ถือ `"年"` เป็นตัวแทนรูปแบบและล้มเหลว | ใส่ข้อความคงที่ในเครื่องหมายอัญประกาศคู่, เช่น `\"年\"` |
| เซลล์ถูกกำหนดรูปแบบเป็น *Text* อยู่แล้ว | รูปแบบกำหนดเองถูกละเลย | ล้าง `NumberFormat` ของเซลล์ก่อน: `firstCell.SetStyle(workbook.CreateStyle());` |
| ใช้ไลบรารีที่ไม่รองรับ property `Custom` | เกิดข้อผิดพลาดการคอมไพล์ | เปลี่ยนไปใช้ไลบรารีที่เปิดเผยรูปแบบตัวเลขกำหนดเอง (Aspose.Cells, EPPlus, ClosedXML) |

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

รันโปรแกรม, เปิด `ParsedDateExample.xlsx`, คุณจะเห็นเซลล์ **A1** แสดง `2021年5月12日` ในขณะที่ค่าที่อยู่ภายในเป็นวันที่ Excel ที่ถูกต้อง

---

## Conclusion

เราได้ครอบคลุม **how to parse date** ใน Excel ด้วย C# โดย **applying a custom number format Excel** แล้ว **reading date from cell** เป็น `DateTime` แบบเนทีฟ จุดสำคัญที่ควรจำ:

- ใช้รูปแบบกำหนดเองที่รับรู้ภาษาท้องถิ่น (`[$-ja-JP]…`) เพื่อให้ Excel ทำงานหนักให้  
- เข้าถึง `Cell.DateTimeValue` เพื่อรับ `DateTime` ที่สะอาดโดยไม่ต้องแยกวิเคราะห์ด้วยตนเอง  
- ปรับสตริงรูปแบบสำหรับวัฒนธรรมอื่น ๆ และตรวจสอบผลด้วยการพิมพ์คอนโซลสั้น ๆ  

จากนี้คุณสามารถ **format Excel cell date** สำหรับรายงาน, ส่ง `DateTime` ไปยังฐานข้อมูล, หรือทำการคำนวณโดยตรงในแอป C# ของคุณ ทดลองกับภาษาต่าง ๆ, รวมหลายเซลล์, หรือแม้กระทั่งประมวลผลเป็นชุดของแผ่นงาน – หลักการเดียวกันใช้ได้ทั้งหมด  

มีรูปแบบวันที่แปลก ๆ ที่คุณแก้ไม่ได้? แสดงความคิดเห็นได้เลย, เราจะช่วยกันแก้ไข ปรึกษาและสนุกกับการเขียนโค้ดกันต่อไป!

## บทแนะนำที่เกี่ยวข้อง

- [Excel Custom Number and Date Formatting](/cells/english/net/excel-custom-number-date-formatting/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel Custom Number Date Formatting](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}