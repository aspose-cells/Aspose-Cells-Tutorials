---
category: general
date: 2026-03-01
description: วิธีสร้างเวิร์กบุ๊กใน C# อย่างรวดเร็ว—เรียนรู้การเขียนค่าไปยังเซลล์ การตั้งค่ารูปแบบตัวเลขของเซลล์
  และการจัดรูปแบบตัวเลขของเซลล์ด้วยขั้นตอนง่าย ๆ.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: th
og_description: วิธีสร้างเวิร์กบุ๊กใน C#? คู่มือนี้จะแสดงวิธีเขียนค่าลงในเซลล์ ตั้งค่ารูปแบบตัวเลขของเซลล์
  และจัดรูปแบบตัวเลขของเซลล์ เพียงไม่กี่บรรทัดของโค้ด.
og_title: วิธีสร้าง Workbook ใน C# – เขียนค่าและจัดรูปแบบตัวเลข
tags:
- C#
- Aspose.Cells
- Excel Automation
title: วิธีสร้าง Workbook ใน C# – เขียนค่าและจัดรูปแบบตัวเลข
url: /th/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Workbook ใน C# – เขียนค่าและจัดรูปแบบตัวเลข

การสร้าง workbook ใน C# เป็นงานทั่วไปเมื่อคุณต้องการสร้างไฟล์ Excel อย่างรวดเร็ว ในคู่มือนี้เราจะอธิบายวิธีเขียนค่าไปยังเซลล์และจัดรูปแบบตัวเลขของเซลล์เพื่อให้แผ่นงานสุดท้ายดูเรียบร้อย

หากคุณเคยมองตารางคำนวณเปล่า ๆ แล้วสงสัยว่าทำไมตัวเลขถึงแสดงทศนิยมมากเกินไป คุณไม่ได้เป็นคนเดียว เราจะครอบคลุมทุกอย่างตั้งแต่การเริ่มต้นอ็อบเจกต์ workbook ไปจนถึงการตั้งค่ารูปแบบตัวเลขแบบกำหนดเอง และเราจะเพิ่มเคล็ดลับสำหรับกรณีขอบที่คุณอาจเจอในภายหลัง

## สิ่งที่คุณจะได้เรียนรู้

- **Initialize** อินสแตนซ์ `Workbook` ใหม่  
- **Write value to cell** ด้วยเมธอด `PutValue`  
- **Set cell number format** ด้วยอ็อบเจกต์ `Style` เพื่อให้แสดงผลเป็นสองตำแหน่งทศนิยมอย่างสะอาด  
- ตรวจสอบผลลัพธ์โดยอ่านค่ากลับจากเซลล์หรือเปิดไฟล์ใน Excel  

ไม่จำเป็นต้องใช้ไลบรารีภายนอกใด ๆ นอกจาก Aspose.Cells มาตรฐาน (หรือ API ที่คล้ายกัน) และโค้ดทำงานบน .NET 6+ โดยไม่ต้องกำหนดค่าเพิ่มเติม

---

## วิธีสร้าง Workbook – เริ่มต้นอ็อบเจกต์

ก่อนอื่นคุณต้องมีอ็อบเจกต์ workbook เพื่อเก็บแผ่นงานของคุณ คิดว่า `Workbook` คือไฟล์ Excel ทั้งไฟล์ ในขณะที่แต่ละ `Worksheet` คือแท็บเดียว

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*ทำไมสิ่งนี้สำคัญ:* การสร้าง workbook จะจัดสรรโครงสร้างภายในที่ต่อมาจะเก็บแถว คอลัมน์ และการจัดรูปแบบ หากไม่มีอ็อบเจกต์นี้ จะไม่มีที่ใดให้เขียนค่าลงในเซลล์ได้

> **Pro tip:** หากคุณวางแผนทำงานกับไฟล์ที่มีอยู่แล้ว ให้เปลี่ยน `new Workbook()` เป็น `new Workbook("template.xlsx")` เพื่อโหลดเทมเพลตและคงสไตล์ไว้

## เขียนค่าไปยังเซลล์

ตอนนี้เรามี workbook แล้ว ให้ใส่ตัวเลขลงในเซลล์ **A1** ของ worksheet แรก

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*ทำไมเราใช้ `PutValue`*: เมธอดนี้ตรวจจับประเภทข้อมูลโดยอัตโนมัติ จึงไม่ต้องแคสต์หรือแปลงด้วยตนเอง อีกทั้งยังเคารพสไตล์ที่มีอยู่ของเซลล์ ซึ่งเป็นประโยชน์เมื่อคุณต่อมาจะ **set cell number format**

### ตรวจสอบอย่างรวดเร็ว

หากคุณอ่านค่ากลับจากเซลล์ คุณจะเห็นค่าดิบ:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

นั่นคือตัวเลขก่อนที่จะแสดงผลด้วยการจัดรูปแบบใด ๆ

## ตั้งค่ารูปแบบตัวเลขของเซลล์

การแสดงค่า double ดิบที่มีทศนิยมหลายตำแหน่งไม่ค่อยเป็นมิตรต่อผู้ใช้เสมอไป ให้จำกัดเป็นสองตำแหน่งสำคัญ

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

คุณสมบัติ `Number` สอดคล้องกับ ID ของรูปแบบตัวเลขที่มีใน Excel `2` หมายถึง “Number with two decimal places” หากคุณต้องการรูปแบบอื่น—เช่นสกุลเงินหรือวันที่—คุณจะใช้ ID อื่นหรือสตริงรูปแบบกำหนดเอง

### ทางเลือก: สตริงรูปแบบกำหนดเอง

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*ทำไมต้องเลือกสไตล์กำหนดเอง?* มันให้คุณควบคุมเต็มที่ โดยเฉพาะเมื่อ ID ที่มีใน Excel ไม่ครอบคลุมการตั้งค่าภูมิภาคของคุณ

## ตรวจสอบผลลัพธ์ (เป็นตัวเลือกแต่แนะนำ)

หลังจากใช้สไตล์แล้ว คุณสามารถบันทึก workbook และเปิดใน Excel เพื่อยืนยันลักษณะการแสดงผล

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

คุณควรเห็น **123.46** ในเซลล์ A1—สองตำแหน่งทศนิยมพอดี ขอบคุณรูปแบบที่เราตั้งค่าไว้

---

### ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกขั้นตอนเข้าด้วยกัน นี่คือโปรแกรมที่สามารถคัดลอกและวางลงในแอปคอนโซลได้

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**ผลลัพธ์ที่คาดว่าจะได้เมื่อรันโปรแกรม:**

```
Cell A1 shows: 123.46
```

เปิด `FormattedWorkbook.xlsx` ใน Excel แล้วคุณจะเห็นค่าที่จัดรูปแบบเดียวกัน

---

## ความแตกต่างทั่วไปและกรณีขอบ

### 1. รูปแบบตัวเลขที่แตกต่าง

| Goal | Format ID | Code Snippet |
|------|-----------|--------------|
| สกุลเงิน (สองตำแหน่งทศนิยม) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| เปอร์เซ็นต์ (ไม่มีทศนิยม) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| รูปแบบวิทยาศาสตร์ | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

หากไม่มี ID ใดตรงกับความต้องการของคุณ ให้ใช้สตริงกำหนดเองตามที่แสดงไว้ก่อนหน้า

### 2. ตัวคั่นทศนิยมตามวัฒนธรรม

บางภูมิภาคใช้เครื่องหมายจุลภาคเป็นตัวคั่นทศนิยม คุณสามารถบังคับใช้รูปแบบที่รับรู้วัฒนธรรมได้:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. การเขียนข้อความแทนตัวเลข

เมื่อคุณต้องการ **วิธีเขียนเซลล์** ด้วยสตริง เพียงส่งสตริงไปยัง `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

ไม่จำเป็นต้องกำหนดรูปแบบตัวเลข แต่คุณยังสามารถใช้สไตล์ฟอนต์ได้

### 4. ชุดข้อมูลขนาดใหญ่

หากคุณกำลังใส่ข้อมูลหลายพันแถว การแทรกแบบแบตช์ (`Cells.ImportArray`) จะเร็วกว่าการวนลูป `PutValue` วิธีการจัดรูปแบบยังคงเหมือนเดิม; เพียงแค่ใช้สไตล์กับช่วง:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## คำถามที่พบบ่อย

**Q: Does this work with .NET Core?**  
A: Absolutely. Aspose.Cells supports .NET Standard 2.0 and later, so you can target .NET 5, .NET 6, or .NET 7 without changes.

**Q: What if I need more than two decimal places?**  
A: Change the `Number` property to the appropriate built‑in ID (e.g., `3` for three decimals) or tweak the custom format string (`"#,##0.000"`).

**Q: Can I apply the format to an entire column at once?**  
A: Yes. Use `Cells["A:A"]` to get the whole column and then `SetStyle`.

---

## สรุป

คุณตอนนี้รู้แล้ว **วิธีสร้าง workbook** ใน C#, **เขียนค่าไปยังเซลล์**, และ **ตั้งค่ารูปแบบตัวเลขของเซลล์** เพื่อให้ตัวเลขแสดงผลตามที่ต้องการ การเข้าใจพื้นฐานเหล่านี้จะทำให้คุณสามารถสร้างรายงาน Excel, ใบแจ้งหนี้ หรือการส่งออกข้อมูลที่ดูเป็นมืออาชีพได้อย่างง่ายดาย

ต่อไปคุณอาจสำรวจ **format cell number** สำหรับวันที่, เปอร์เซ็นต์, หรือการจัดรูปแบบตามเงื่อนไข—แต่ละอย่างสร้างบนหลักการเดียวกันที่เราได้ครอบคลุมแล้ว ค้นคว้าเอกสาร Aspose.Cells เพื่อดูตัวเลือกการสไตล์ที่ลึกซึ้งยิ่งขึ้น หรือลองรวมหลาย worksheet เข้าไว้ใน workbook เดียวเพื่อรายงานที่มีความหลากหลายมากขึ้น

Happy coding, and remember: a well‑formatted spreadsheet is just

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}