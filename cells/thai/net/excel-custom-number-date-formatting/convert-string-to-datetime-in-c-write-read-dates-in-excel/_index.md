---
category: general
date: 2026-02-23
description: แปลงสตริงเป็น DateTime ใน C# และเรียนรู้วิธีเขียนวันที่ลงใน Excel, บังคับให้สูตรคำนวณ,
  และอ่านวันที่จาก Excel ด้วย Aspose.Cells.
draft: false
keywords:
- convert string to datetime
- write date to excel
- read date from excel
- force formula calculation
- extract date from excel
language: th
og_description: แปลงสตริงเป็น DateTime ใน C# อย่างรวดเร็ว คู่มือนี้แสดงวิธีเขียนวันที่ลงใน
  Excel, บังคับให้สูตรคำนวณ, และดึงวันที่จาก Excel โดยใช้ Aspose.Cells.
og_title: แปลงสตริงเป็น DateTime ใน C# – คู่มือการจัดการวันที่ใน Excel
tags:
- C#
- Excel automation
- Aspose.Cells
title: แปลงสตริงเป็น DateTime ใน C# – เขียนและอ่านวันที่ใน Excel
url: /th/net/excel-custom-number-date-formatting/convert-string-to-datetime-in-c-write-read-dates-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงสตริงเป็น DateTime – เขียนและอ่านวันที่ใน Excel ด้วย C#

เคยต้อง **แปลงสตริงเป็น DateTime** ขณะทำงานกับไฟล์ Excel ใน C# หรือไม่? บางทีคุณอาจได้รับวันที่ในรูปแบบ `"R3/04/01"` จากระบบภายนอกและไม่แน่ใจว่าจะเปลี่ยนเป็นอ็อบเจ็กต์ `DateTime` อย่างไร ข่าวดีคือวิธีแก้ง่ายมาก—เพียงไม่กี่บรรทัดโค้ดและเทคนิค “บังคับให้สูตรคำนวณ” เล็กน้อย

ในบทเรียนนี้เราจะอธิบาย **วิธีเขียนวันที่ลงใน Excel**, **บังคับให้สูตรคำนวณ** เพื่อให้ Excel รับรู้ค่า, แล้ว **อ่านวันที่กลับมาเป็น `DateTime`**. เมื่อจบคุณจะได้ตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งสามารถนำไปใช้ในโปรเจกต์ .NET ใดก็ได้

> **สิ่งที่คุณจะได้เรียน**
> - เขียนสตริงวันที่ลงในเซลล์ (`write date to excel`)
> - เรียกการคำนวณ (`force formula calculation`) เพื่อให้ Excel แปลงสตริง
> - ดึงค่า `DateTimeValue` ของเซลล์ (`extract date from excel`)
> - จุดบกพร่องทั่วไปและเคล็ดลับเล็ก ๆ ที่เป็นประโยชน์

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework ด้วย)
- Aspose.Cells for .NET (รุ่นทดลองหรือแบบลิขสิทธิ์) ติดตั้งผ่าน NuGet:

```bash
dotnet add package Aspose.Cells
```

- ความเข้าใจพื้นฐานของไวยากรณ์ C#—ไม่ต้องมีอะไรซับซ้อน

ตอนนี้มาเริ่มกันเลย

![convert string to datetime example](image.png){alt="แปลงสตริงเป็น datetime ใน Excel ด้วย C#"}

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ Workbook ใหม่ (บริบทการแปลงสตริงเป็น DateTime)

สิ่งแรกที่เราต้องการคืออ็อบเจ็กต์ workbook ใหม่ที่พร้อมใช้งาน คิดว่าเป็นไฟล์ Excel ว่างเปล่าที่อยู่ในหน่วยความจำจนกว่าจะบันทึก

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1 – initialize a workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();
```

> **ทำไมเรื่องนี้สำคัญ:**  
> การเริ่มต้นด้วย `Workbook` ที่สะอาดช่วยรับประกันว่าไม่มีการจัดรูปแบบหรือสูตรที่ซ่อนอยู่แทรกแซงตรรกะการแปลงวันที่ของเรา

## ขั้นตอนที่ 2: เขียนสตริงวันที่ลงในเซลล์ A1 (`write date to excel`)

ต่อไปเราจะใส่สตริงดิบ `"R3/04/01"` ลงในเซลล์ **A1** สตริงนี้ใช้รูปแบบกำหนดเอง (R3 = ปี 2023, เดือน 04, วัน 01) Excel จะสามารถตีความได้เมื่อเราบังคับให้คำนวณ

```csharp
        // Step 2 – put the raw date string into A1
        // The string "R3/04/01" means 2023‑04‑01 in our custom format
        workbook.Worksheets[0].Cells["A1"].PutValue("R3/04/01");
```

> **เคล็ดลับ:** หากคุณมีหลายวันที่ ควรวนลูปผ่านช่วงและใช้ `PutValue` ภายในลูป วิธีนี้จะตรวจจับประเภทข้อมูลอัตโนมัติ แต่สำหรับรูปแบบกำหนดเองของเราต้องทำขั้นตอนต่อไป

## ขั้นตอนที่ 3: บังคับให้สูตรคำนวณ (`force formula calculation`)

Excel ไม่ได้แปลงสตริงวันที่กำหนดเองโดยอัตโนมัติ การเรียก `CalculateFormula()` จะทำให้เอนจินประมวลผลชีตใหม่ ซึ่งกระตุ้นตรรกะการแปลงวันที่ภายในขั้นตอนนี้สำคัญมาก; หากไม่ทำ `DateTimeValue` จะคืนค่า `DateTime.MinValue`

```csharp
        // Step 3 – force the workbook to evaluate formulas and parse dates
        workbook.CalculateFormula();
```

> **ทำไมต้องบังคับคำนวณ:**  
> การเรียก `CalculateFormula` บอก Aspose.Cells ให้ทำงานเหมือนผู้ใช้กด **F9** ใน Excel การแปลงนี้จะเปลี่ยนข้อความเป็นวันที่เชิงลำดับที่ .NET สามารถเข้าใจได้

## ขั้นตอนที่ 4: ดึงค่าของเซลล์เป็นอ็อบเจ็กต์ DateTime (`read date from excel` & `extract date from excel`)

ตอนนี้เราสามารถอ่าน `DateTimeValue` ของเซลล์ได้อย่างปลอดภัย Aspose.Cells จะเปิดให้เข้าถึงเป็นโครงสร้าง `DateTime` ที่แปลงมาจากหมายเลขซีเรียลของ Excel แล้ว

```csharp
        // Step 4 – read the parsed date back as a DateTime
        DateTime dateFromCell = workbook.Worksheets[0].Cells["A1"].DateTimeValue;

        // Display the result
        Console.WriteLine($"Parsed date: {dateFromCell:yyyy-MM-dd}");
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล**

```
Parsed date: 2023-04-01
```

หากคุณรันโปรแกรมและเห็นบรรทัดข้างต้น แสดงว่าคุณได้ **แปลงสตริงเป็น datetime** แล้ว, เขียนวันที่ลง Excel, บังคับให้สูตรคำนวณ, และดึงวันที่กลับมาเรียบร้อย

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่ได้ ไม่ขาดส่วนใดและคอมไพล์ได้ทันที

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Write the raw date string to cell A1
        workbook.Worksheets[0].Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ Force Excel to evaluate formulas (parses the date)
        workbook.CalculateFormula();

        // 4️⃣ Retrieve the parsed date as a DateTime object
        DateTime dateFromCell = workbook.Worksheets[0].Cells["A1"].DateTimeValue;

        // Verify the conversion
        Console.WriteLine($"Parsed date: {dateFromCell:yyyy-MM-dd}");
    }
}
```

### เช็คลิสต์สั้น ๆ

| ✅ | งาน |
|---|------|
| ✅ | **Write date to excel** – `PutValue("R3/04/01")` |
| ✅ | **Force formula calculation** – `CalculateFormula()` |
| ✅ | **Read date from excel** – `DateTimeValue` |
| ✅ | **Extract date from excel** – แปลงเป็นรูปแบบ `yyyy‑MM‑dd` |
| ✅ | โค้ดสมบูรณ์, สามารถรันได้ |

## กรณีขอบเขตทั่วไป & วิธีจัดการ

| สถานการณ์ | สิ่งที่ต้องระวัง | วิธีแก้แนะนำ |
|-----------|-------------------|---------------|
| **รูปแบบกำหนดเองที่แตกต่าง** (เช่น `"R4/12/31"` สำหรับ 2024‑12‑31) | Excel อาจไม่รับรู้คำนำหน้า “R” อัตโนมัติ | ทำการประมวลผลล่วงหน้า: แทนที่ `R` ด้วย `20` ก่อน `PutValue` |
| **เซลล์ว่างหรือค่า null** | `DateTimeValue` จะคืนค่า `DateTime.MinValue` | ตรวจสอบคุณสมบัติ `IsDate` ก่อนอ่าน: `if (cell.IsDate) …` |
| **ชุดข้อมูลขนาดใหญ่** | การคำนวณใหม่ทั้งหมดทุกครั้งอาจช้า | เรียก `CalculateFormula()` ครั้งเดียวหลังจากเขียนวันที่ทั้งหมด |
| **การตั้งค่าภูมิภาค** | บางภูมิภาคคาดหวังลำดับวัน‑เดือน‑ปี | ตั้งค่า `WorkbookSettings.CultureInfo` เป็น `CultureInfo.InvariantCulture` หากจำเป็น |

## เคล็ดลับสำหรับโครงการจริง

1. **ประมวลผลเป็นชุด** – เมื่อมีหลายพันแถว ให้เขียนสตริงทั้งหมดก่อน แล้วค่อยเรียก `CalculateFormula()` ครั้งเดียว เพื่อลดภาระการคำนวณอย่างมาก
2. **การจัดการข้อผิดพลาด** – ห่อการแปลงด้วย try/catch และบันทึกเซลล์ที่ `IsDate` เป็น false จะช่วยให้คุณตรวจพบข้อมูลที่ผิดรูปแบบได้เร็วขึ้น
3. **บันทึก workbook** – หากต้องการเก็บสำเนา เพียงเพิ่ม `workbook.Save("output.xlsx");` หลังขั้นตอนที่ 4
4. **ประสิทธิภาพ** – สำหรับกรณีอ่าน‑อย่างเดียว ให้ใช้ `LoadOptions` กับ `LoadFormat.Xlsx` เพื่อเร่งการโหลดไฟล์ขนาดใหญ่

## สรุป

ตอนนี้คุณมีรูปแบบครบวงจรสำหรับ **แปลงสตริงเป็น datetime** ขณะทำงานกับ Excel ใน C# โดย **เขียนวันที่ลง Excel**, **บังคับให้สูตรคำนวณ**, แล้ว **อ่าน `DateTimeValue`** คุณจึงสามารถแปลงสตริงรูปแบบใดก็ได้ให้เป็น `DateTime` ของ .NET ได้อย่างเชื่อถือได้  

อย่ากลัวทดลองเปลี่ยนสตริงอินพุต, ทดลองกับภูมิภาคต่าง ๆ, หรือขยายตรรกะให้ครอบคลุมคอลัมน์ทั้งหมด เมื่อคุณเชี่ยวชาญพื้นฐานเหล่านี้ การจัดการวันที่ใน Excel จะกลายเป็นเรื่องง่ายเหมือนเค้ก

**ขั้นตอนต่อไป** – สำรวจหัวข้อที่เกี่ยวข้องเช่น **การจัดรูปแบบเซลล์เป็นวันที่**, **การใช้รูปแบบตัวเลขกำหนดเอง**, หรือ **การส่งออก workbook กลับเป็นสตรีมสำหรับ Web API**. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}