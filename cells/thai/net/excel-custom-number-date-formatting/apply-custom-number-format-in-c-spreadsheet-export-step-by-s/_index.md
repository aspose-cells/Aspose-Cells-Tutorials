---
category: general
date: 2026-04-07
description: ใช้รูปแบบตัวเลขแบบกำหนดเองกับเซลล์ในสเปรดชีตและเรียนรู้วิธีจัดรูปแบบตัวเลขในสเปรดชีตขณะส่งออกค่าของเซลล์ด้วย
  C# คู่มือที่รวดเร็วและครบถ้วน.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: th
og_description: ใช้รูปแบบตัวเลขที่กำหนดเองกับเซลล์ในสเปรดชีตและส่งออกเป็นสตริงที่จัดรูปแบบแล้ว
  เรียนรู้วิธีจัดรูปแบบตัวเลขในสเปรดชีตและส่งออกค่าของเซลล์
og_title: ใช้รูปแบบตัวเลขแบบกำหนดเอง – คำแนะนำการส่งออก C# อย่างสมบูรณ์
tags:
- C#
- Spreadsheet
- Number Formatting
title: ใช้รูปแบบตัวเลขแบบกำหนดเองในการส่งออกสเปรดชีต C# – คู่มือขั้นตอนโดยขั้นตอน
url: /th/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ใช้รูปแบบตัวเลขแบบกำหนดเองใน C# Spreadsheet Export – บทเรียนเต็ม

เคยต้อง **ใช้รูปแบบตัวเลขแบบกำหนดเอง** กับเซลล์แล้วดึงสตริงที่จัดรูปแบบแล้วออกจากสเปรดชีตหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหาเมื่อค่าดิบออกมาแทนที่จะเป็นสตริงที่สวยงามและรองรับภาษาท้องถิ่นที่คาดหวังไว้ ในคู่มือนี้เราจะสาธิตวิธีการจัดรูปแบบตัวเลขในเซลล์สเปรดชีตและวิธีการส่งออกค่าของเซลล์เป็นสตริงที่จัดรูปแบบแล้วโดยใช้ไลบรารีสเปรดชีต C# ที่เป็นที่นิยม

เมื่อทำตามขั้นตอนจนจบคุณจะสามารถ **ใช้รูปแบบตัวเลขแบบกำหนดเอง** กับเซลล์ตัวเลขใด ๆ ส่งออกผลลัพธ์ด้วย `ExportTable` และเห็นผลลัพธ์ที่ตรงกับที่คุณคาดหวังให้แสดงใน UI หรือรายงาน ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างอยู่ที่นี่แล้ว

## Prerequisites

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)
- การอ้างอิงไลบรารีสเปรดชีตที่ให้บริการ `Workbook`, `Worksheet` และ `ExportTableOptions` (เช่น **Aspose.Cells** หรือ **GemBox.Spreadsheet**; API ที่แสดงตรงกับ Aspose.Cells)
- ความรู้พื้นฐานของ C#—ถ้าคุณเขียน `Console.WriteLine` ได้ก็พร้อมแล้ว

> **Pro tip:** หากคุณใช้ไลบรารีอื่น ชื่อคุณสมบัติมักจะคล้ายกัน (`NumberFormat`, `ExportAsString`) เพียงแมปให้ตรงตามที่ต้องการ

## What the tutorial covers

1. สร้าง workbook และเลือก worksheet แรก  
2. ใส่ค่าตัวเลขลงในเซลล์  
3. ตั้งค่า `ExportTableOptions` เพื่อ **ใช้รูปแบบตัวเลขแบบกำหนดเอง** และคืนค่าเป็นสตริง  
4. ส่งออกเซลล์และพิมพ์ผลลัพธ์ที่จัดรูปแบบแล้ว  
5. การจัดการกรณีขอบ—ถ้าเซลล์มีสูตรหรือค่า null จะทำอย่างไร?

มาเริ่มกันเลย

![apply custom number format example](https://example.com/image.png "ใช้รูปแบบตัวเลขแบบกำหนดเอง")

## Step 1 – Create a workbook and get the first worksheet

สิ่งแรกที่คุณต้องมีคืออ็อบเจ็กต์ workbook คิดว่าเป็นไฟล์ Excel ที่คุณเปิดในแอป Office เมื่อได้แล้วให้ดึง worksheet แรก—ส่วนใหญ่บทเรียนเริ่มจากที่นี่เพื่อให้ตัวอย่างกระชับ

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**ทำไมสิ่งนี้ถึงสำคัญ:** workbook ใหม่ให้ “กระดานว่าง” ที่ไม่มีการจัดรูปแบบแอบซ่อนใด ๆ ที่อาจขัดขวางรูปแบบตัวเลขแบบกำหนดเองของเราในภายหลัง

## Step 2 – Put a numeric value into cell B2 (the cell we will export)

ต่อไปเราต้องมีค่าที่จะจัดรูปแบบ เซลล์ **B2** เป็นตำแหน่งที่สะดวก—อ้างอิงง่ายและห่างจากมุม A1 เริ่มต้นพอที่จะหลีกเลี่ยงการเขียนทับโดยบังเอิญ

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**ถ้าค่าที่ใส่เป็นสูตรล่ะ?**  
หากคุณเปลี่ยนค่าดิบเป็นสูตรในภายหลัง (เช่น `=SUM(A1:A10)`) ขั้นตอนการส่งออกยังคงเคารพรูปแบบตัวเลขที่เรากำหนดในขั้นตอนต่อไป เพราะการจัดรูปแบบถูกผูกกับเซลล์ ไม่ได้ผูกกับประเภทค่าที่อยู่ในเซลล์

## Step 3 – Configure export options to receive the value as a formatted string

นี่คือหัวใจของบทเรียน: เราบอกไลบรารีให้ **ใช้รูปแบบตัวเลขแบบกำหนดเอง** ขณะส่งออก สตริง `NumberFormat` ใช้รูปแบบเดียวกับที่คุณใช้ในหมวด “Custom” ของ Excel

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` ทำให้เมธอดคืนค่าเป็น `string` แทน `double` ดิบ  
- `NumberFormat = "#,##0.00;(#,##0.00)"` ตรงกับรูปแบบของ Excel: คอมม่าแยกหลักพัน, ทศนิยมสองตำแหน่ง, และวงเล็บสำหรับจำนวนลบ

> **ทำไมต้องใช้รูปแบบกำหนดเอง?** มันรับประกันความสอดคล้องระหว่างวัฒนธรรม (เช่น US vs. European) และให้คุณฝังสไตล์เฉพาะธุรกิจเช่นวงเล็บบัญชี

## Step 4 – Export the cell using the configured options

ตอนนี้เราจะดึงค่าจาก worksheet โดยให้ไลบรารีทำการจัดรูปแบบตามที่กำหนดไว้

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**กรณีขอบ – เซลล์ว่าง:** หาก `B2` ว่างเปล่า `formattedResult` จะเป็น `null` คุณสามารถป้องกันได้ด้วยการตรวจสอบ null อย่างง่ายก่อนพิมพ์

## Step 5 – Display the formatted string

สุดท้ายเราจะเขียนผลลัพธ์ลงคอนโซล ในแอปจริงคุณอาจส่งสตริงนี้ไปยัง PDF, อีเมล, หรือป้าย UI

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**ผลลัพธ์ที่คาดหวัง**

```
1,234.56
```

หากคุณเปลี่ยนค่าดิบเป็น `-9876.54` รูปแบบเดียวกันจะให้ผลลัพธ์เป็น `(9,876.54)` — ตรงกับที่หลายรายงานบัญชีต้องการ

## Full, runnable example

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางไปในโปรเจกต์คอนโซลใหม่ มันคอมไพล์และทำงานได้ทันที หากคุณได้เพิ่มแพ็กเกจ NuGet ที่เหมาะสมสำหรับไลบรารีสเปรดชีต

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Quick sanity check

- **คอมไพล์ได้หรือไม่?** ได้—แค่ตรวจสอบให้แน่ใจว่าได้อ้างอิง DLL ของ `Aspose.Cells` (หรือไลบรารีเทียบเท่า) แล้ว  
- **ทำงานกับวัฒนธรรมอื่นได้หรือไม่?** สตริงรูปแบบเป็นแบบ culture‑agnostic; ไลบรารีจะปฏิบัติตามรูปแบบที่คุณกำหนด หากต้องการตัวคั่นตาม locale สามารถใส่การจัดการ `CultureInfo` ก่อนส่งออกได้

## Common questions & variations

### วิธี **format number in spreadsheet** ด้วยรูปแบบอื่น?

เปลี่ยนสตริง `NumberFormat` ตัวอย่างเช่น หากต้องการแสดงเป็นเปอร์เซ็นต์พร้อมทศนิยมหนึ่งตำแหน่ง:

```csharp
NumberFormat = "0.0%";
```

### ถ้าต้องการ **how to export cell value** เป็น HTML แทนข้อความธรรมดา?

ไลบรารีส่วนใหญ่มี overload ที่รับประเภทการส่งออก คุณตั้งค่า `ExportAsString = true` แล้วเพิ่ม `ExportHtml = true` (หรือคล้ายกัน) หลักการยังคงเหมือนเดิม: กำหนดรูปแบบแล้วเลือกตัวแทนผลลัพธ์

### สามารถใช้รูปแบบนี้กับช่วงหลายเซลล์ได้หรือไม่ ไม่ใช่แค่เซลล์เดียว?

ทำได้แน่นอน คุณสามารถกำหนด `NumberFormat` ให้กับอ็อบเจ็กต์ `Style` แล้วนำสไตล์นั้นไปใช้กับ `Range` การเรียกส่งออกจะไม่เปลี่ยนแปลง; มันจะดึงสไตล์โดยอัตโนมัติ

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### จะเกิดอะไรขึ้นเมื่อเซลล์มีสูตร?

ขั้นตอนการส่งออกจะประเมินสูตรก่อน แล้วจึงจัดรูปแบบค่าตัวเลขที่ได้ ไม่ต้องเขียนโค้ดเพิ่ม—แค่ตรวจสอบว่าได้เรียก `Calculate` หากคุณปิดการคำนวณอัตโนมัติ

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusion

ตอนนี้คุณรู้วิธี **ใช้รูปแบบตัวเลขแบบกำหนดเอง** กับเซลล์สเปรดชีต, **format number in spreadsheet** ในบริบทต่าง ๆ, และ **how to export cell value** เป็นสตริงที่พร้อมแสดงผล ตัวอย่างโค้ดสั้น ๆ ด้านบนครอบคลุมทุกขั้นตอน—from การสร้าง workbook จนถึงการแสดงผลสุดท้าย—เพื่อให้คุณนำไปใช้ในโปรเจกต์จริงได้ทันที

พร้อมรับความท้าทายต่อไปหรือยัง? ลองผสมเทคนิคนี้กับ **how to format numeric cell** สำหรับวันที่, สัญลักษณ์สกุลเงิน, หรือ conditional formatting หรือสำรวจการส่งออกหลายเซลล์เป็น CSV พร้อมรักษารูปแบบกำหนดเองของแต่ละเซลล์ ไม่ว่าคุณจะทำอะไรพื้นฐานเหล่านี้จะเป็นฐานที่มั่นคง

ขอให้เขียนโค้ดสนุกและอย่าลืมทดลอง—บางครั้งคำตอบที่ดีที่สุดจะปรากฏเมื่อคุณปรับสตริงรูปแบบเพียงเล็กน้อย!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}