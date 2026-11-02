---
category: general
date: 2026-10-13
description: เรียนรู้วิธีบันทึก Excel เป็น TXT ด้วย Aspose.Cells คู่มือนี้ครอบคลุมการส่งออก
  Excel ไปเป็น TXT การเขียนค่าในเซลล์ และการตั้งค่าตัวเลขที่สำคัญในไม่กี่ขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: th
lastmod: 2026-10-13
og_description: บันทึกไฟล์ Excel เป็น TXT ด้วย Aspose.Cells. เรียนรู้วิธีส่งออก Excel
  เป็น TXT, เขียนค่าลงในเซลล์, และตั้งค่าตัวเลขสำคัญด้วยเพียงไม่กี่บรรทัดของโค้ด C#
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: บันทึก Excel เป็น TXT – คู่มือขั้นตอนสำหรับนักพัฒนา .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: วิธีบันทึกไฟล์ Excel เป็น TXT โดยใช้ Aspose.Cells ใน C#
url: /th/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีบันทึก Excel เป็น TXT ด้วย Aspose.Cells ใน C#

หากคุณต้องการ **save Excel as TXT** อย่างรวดเร็ว บทแนะนำนี้จะแสดงกระบวนการทั้งหมดภายในเวลาน้อยกว่าห้านาที คุณจะได้เห็นวิธีการ **export Excel to TXT**, **write value to cell**, และ **set significant digits** เพื่อให้ไฟล์ข้อความมีข้อมูลที่คุณคาดหวังอย่างแม่นยำ

การ **export spreadsheet** เป็น TXT มีประโยชน์เมื่อระบบ downstream รับเฉพาะข้อมูลแบบ plain‑text, เมื่อคุณต้องการสร้าง logs, หรือเมื่อคุณต้องการ dump การคำนวณที่มนุษย์สามารถอ่านได้ ตัวอย่างด้านล่างทำงานกับ Aspose.Cells v25.10 หรือใหม่กว่าและทำงานบน runtime .NET 6+ ใดก็ได้

## สิ่งที่ต้องเตรียม

* สำเนาแบบลิขสิทธิ์ของ **Aspose.Cells for .NET** (รุ่นทดลองฟรีสามารถใช้ทดสอบได้)
* .NET 6 SDK หรือใหม่กว่า ติดตั้งแล้ว
* IDE เช่น Visual Studio 2022, VS Code หรือ Rider
* ความรู้พื้นฐาน C# — ไม่จำเป็นต้องมีประสบการณ์การทำ automation ของ Excel ขั้นสูง

คุณสามารถติดตั้งแพ็กเกจ NuGet ของ Aspose.Cells ด้วย:

```bash
dotnet add package Aspose.Cells
```

## ขั้นตอนที่ 1: สร้าง workbook และเข้าถึง worksheet แรก (save excel as txt)

สิ่งแรกที่คุณทำเมื่อคุณต้องการ **save Excel as TXT** คือการสร้างอ็อบเจ็กต์ `Workbook` อ็อบเจ็กต์นี้เป็นตัวแทนของไฟล์ Excel ทั้งหมดในหน่วยความจำ

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** คลาส `Workbook` เป็นจุดเริ่มต้นสำหรับการทำงานกับสเปรดชีตทั้งหมด โดยการเริ่มต้นด้วย workbook ใหม่คุณจะหลีกเลี่ยงการฟอร์แมตที่ซ่อนอยู่ซึ่งอาจส่งผลต่อการส่งออกเป็น plain‑text

## ขั้นตอนที่ 2: เขียนตัวเลขความแม่นยำสูงลงในเซลล์ (write value to cell)

ตอนนี้คุณต้อง **write value to cell** A1 เมธอด `PutValue` จะตรวจจับประเภทข้อมูลโดยอัตโนมัติและเก็บเป็นค่าตัวเลข

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **เคล็ดลับ:** หากคุณต้องการเขียนสตริง, วันที่ หรือสูตรในภายหลัง เมธอด `PutValue` เดียวกันก็ทำงาน—เพียงส่งประเภท .NET ที่เหมาะสม

## ขั้นตอนที่ 3: กำหนดค่า export options เพื่อเก็บความแม่นยำที่ต้องการเท่านั้น (set significant digits)

เมื่อทำการ **export** ไปยังไฟล์ TXT คุณมักต้องการจำกัดจำนวนหลักเพื่อให้ไฟล์มีขนาดเล็กหรือให้ตรงกับสเปคของระบบ downstream คลาส `TxtSaveOptions` มีคุณสมบัติ `SignificantDigits` สำหรับจุดประสงค์นี้

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **ทำไมคุณควรตั้งค่า significant digits:** หากไม่ได้ตั้งค่านี้ Aspose.Cells จะเขียนค่าความแม่นยำ double‑precision ทั้งหมด ซึ่งอาจทำให้ได้สตริงยาวเช่น `12345.6789012345` การตั้งค่า `SignificantDigits = 6` จะตัดเอาต์พุตเหลือ `12345.7` ซึ่งตรงกับความต้องการของรายงานส่วนใหญ่

## ขั้นตอนที่ 4: Export workbook เป็นไฟล์ TXT (export excel to txt)

สุดท้ายคุณ **export Excel to TXT** โดยเรียก `Workbook.Save` พร้อมกับตัวเลือกที่กำหนดไว้ก่อนหน้า

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

เมื่อโค้ดทำงานเสร็จ `LimitedDigits.txt` จะมีเนื้อหา:

```
12345.7
```

> **การตรวจสอบผลลัพธ์:** เปิดไฟล์ด้วยโปรแกรมแก้ไขข้อความใดก็ได้ (Notepad, VS Code) เพื่อยืนยันว่ามีเพียงหกหลักสำคัญเท่านั้นและไม่มีคอมมาหรือแท็บเพิ่มเติม

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นแอปพลิเคชันคอนโซลที่ทำงานได้เองซึ่งคุณสามารถคัดลอก, วาง, และรันได้ทันที

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**คำอธิบายของแต่ละบล็อก**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | นำเข้า namespace Aspose.Cells ที่จำเป็นสำหรับ `Workbook`, `Worksheet` และ `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | สร้างอินสแตนซ์ของ Excel workbook ว่างในหน่วยความจำ. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 ด้วยตัวเลข double‑precision. |
| `TxtSaveOptions` | กำหนดพฤติกรรม **set significant digits** สำหรับการ **export** เป็น TXT. |
| `workbook.Save(..., txtOptions);` | ดำเนินการ **export excel to txt** สร้างไฟล์ plain‑text. |

## กรณีขอบและเคล็ดลับเพิ่มเติม

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (หลายแถว/คอลัมน์) | ใช้ `txtOptions.Encoding = Encoding.UTF8` หากต้องการสนับสนุน Unicode และพิจารณา stream ไฟล์ด้วย `Workbook.Save(Stream, txtOptions)` เพื่อลดการใช้หน่วยความจำสูง. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` ยังมี `Separator` — ตั้งค่าเป็น `','` เพื่อสร้างผลลัพธ์แบบ CSV‑style แม้จะใช้รูปแบบ TXT. |
| **Preserving formulas** | ตั้งค่า `txtOptions.ExportFormulas = true` เพื่อเขียนข้อความสูตรแทนค่าที่คำนวณได้. |
| **Locale‑specific decimal separators** | ปรับ `txtOptions.DecimalSeparator` เป็น `','` สำหรับโลคัลยุโรป. |
| **Multiple worksheets** | วนลูปผ่าน `workbook.Worksheets` และเรียก `Save` สำหรับแต่ละอัน โดยเพิ่มชื่อ worksheet ลงในชื่อไฟล์. |

## คำถามที่พบบ่อย

**ถาม: `SignificantDigits` ทำการปัดเศษหรือการตัดทอน?**  
**ตอบ:** มันจะปัดเศษเป็นค่าที่ใกล้ที่สุดตามจำนวนหลักสำคัญที่ระบุ ทำให้ผลลัพธ์มีความแม่นยำทางคณิตศาสตร์ตามความละเอียดนั้น.

**ถาม: ฉันสามารถ export โดยตรงไปยัง memory stream ได้หรือไม่?**  
**ตอบ:** ได้. แทนที่เส้นทางไฟล์ด้วยอินสแตนซ์ `MemoryStream`: `workbook.Save(stream, txtOptions);`. วิธีนี้สะดวกสำหรับเว็บ API ที่ต้องการส่งคืนเนื้อหา TXT โดยไม่ต้องเขียนไฟล์ลงระบบ.

**ถาม: ถ้าฉันต้องการรักษาการฟอร์แมตเดิม (เช่น วันที่) จะทำอย่างไร?**  
**ตอบ:** ใช้ `txtOptions.ExportFormattedValues = true`. วิธีนี้บังคับให้ Aspose.Cells เขียนข้อความที่แสดงในเซลล์แทนค่าดิบ.

## สรุป

ตอนนี้คุณรู้วิธี **save Excel as TXT** พร้อมการควบคุมความแม่นยำ, ฟอร์แมต, และตำแหน่งการส่งออกอย่างเต็มที่ โดยทำตามสี่ขั้นตอน—สร้าง workbook, **write value to cell**, **set significant digits**, และ **export Excel to TXT**—คุณสามารถรวมการส่งออกเป็น plain‑text เข้าไปในแอปพลิเคชัน .NET ใดก็ได้

ต่อไปสำรวจหัวข้อที่เกี่ยวข้องเช่น **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, หรือ **use Aspose.Cells to generate JSON reports**. แต่ละหัวข้ออิงจากแนวคิดหลักเดียวกันที่แสดงในที่นี้ ให้คุณมีชุดเครื่องมือที่หลากหลายสำหรับการแลกเปลี่ยนข้อมูลระหว่างแพลตฟอร์ม

ขอให้เขียนโค้ดอย่างสนุก!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ

- [บันทึก Excel เป็นข้อความ – คู่มือ C# ครบถ้วนสำหรับ Export Excel ไปเป็น TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [สร้าง Workbook ใหม่และ Export Excel ไปเป็น TXT ด้วยความแม่นยำ](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [สร้าง Workbook ใหม่ – Export Excel ไปเป็น TXT ด้วยความแม่นยำเต็ม](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}