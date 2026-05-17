---
category: general
date: 2026-02-21
description: บันทึก Excel เป็นไฟล์ txt พร้อมการควบคุมจำนวนหลักสำคัญอย่างแม่นยำ ส่งออก
  Excel เป็น txt ด้วย C# และตั้งค่าจำนวนหลักสำคัญได้อย่างง่ายดาย.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: th
og_description: บันทึก Excel เป็น txt อย่างรวดเร็ว เรียนรู้วิธีส่งออก Excel เป็น txt
  ตั้งค่าตัวเลขที่สำคัญ และควบคุมการแสดงผลข้อความด้วย C#
og_title: บันทึก Excel เป็น txt – ส่งออกตัวเลขพร้อมหลักสำคัญใน C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: บันทึก Excel เป็น txt – คู่มือ C# ฉบับสมบูรณ์สำหรับการส่งออกตัวเลขพร้อมหลักสำคัญ
url: /th/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บันทึก Excel เป็น txt – คู่มือ C# ฉบับสมบูรณ์สำหรับการส่งออกตัวเลขด้วยหลักสำคัญ

เคยต้องการ **save Excel as txt** แต่กังวลว่าตัวเลขจะสูญเสียความแม่นยำหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อพยายาม export Excel to txt แล้วได้ผลลัพธ์ที่มีทศนิยมเกินไปหรือถูกปัดเศษอย่างไม่เหมาะสม  

ในบทแนะนำนี้ เราจะสาธิตวิธี **export Excel to txt** อย่างตรงไปตรงมาพร้อมกับ **setting significant digits** เพื่อให้ผลลัพธ์ออกมาตรงตามที่คุณต้องการ ท้ายบทคุณจะได้โค้ด C# ที่พร้อมรันเพื่อบันทึก workbook เป็นข้อความ ส่งออกตัวเลขเป็น txt และควบคุมรูปแบบตัวเลขได้อย่างเต็มที่

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้าง workbook ใหม่และเขียนข้อมูลตัวเลข
- วิธีที่ถูกต้องในการ **set significant digits** ด้วย `TxtSaveOptions`
- วิธี **save workbook as text** และตรวจสอบผลลัพธ์
- การจัดการกรณีขอบ (ตัวเลขใหญ่, ค่าติดลบ, ปัญหาภาษา/โลคัล)
- เคล็ดลับเร็วสำหรับการปรับแต่งผลลัพธ์เพิ่มเติม (การเปลี่ยน delimiter, การเข้ารหัส)

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานบน .NET Framework 4.6+ ด้วยเช่นกัน)
- แพคเกจ NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)
- ความเข้าใจพื้นฐานของไวยากรณ์ C# — ไม่จำเป็นต้องมีความรู้ลึกเกี่ยวกับ Excel interop

> **เคล็ดลับระดับมืออาชีพ:** หากคุณใช้ Visual Studio ให้เปิดใช้งาน *nullable reference types* (`<Nullable>enable</Nullable>`) เพื่อจับบั๊ก null ที่อาจเกิดขึ้นตั้งแต่ต้น

---

## ขั้นตอนที่ 1: เริ่มต้น Workbook และเขียนตัวเลข

ก่อนอื่น เราต้องมีอ็อบเจกต์ workbook คิดว่าเป็นการแสดงผลไฟล์ Excel ในหน่วยความจำ  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
การสร้าง workbook ด้วยโค้ดช่วยหลีกเลี่ยงการใช้ COM interop ที่ซับซ้อน และ `PutValue` จะตรวจจับประเภทข้อมูลโดยอัตโนมัติ ทำให้เซลล์ถูกจัดเป็นตัวเลข—not a string

---

## ขั้นตอนที่ 2: กำหนดค่า TxtSaveOptions เพื่อควบคุม Significant Digits

คลาส `TxtSaveOptions` คือที่ที่ “เวทมนตร์” เกิดขึ้น โดยการตั้งค่า `SignificantDigits` คุณบอก Aspose.Cells ว่าจะเก็บหลักสำคัญกี่หลักเมื่อเขียนไฟล์ออกมา  

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**ทำไมคุณควรตั้งค่านี้:**  
เมื่อคุณ **export numbers to txt** บ่อยครั้งต้องการการแสดงผลที่กระชับ (เช่น ระบบรายงานที่รับความแม่นยำจำกัด) คุณสมบัติ `SignificantDigits` รับประกันการปัดเศษที่สอดคล้องกันไม่ว่าตัวเลขต้นฉบับจะยาวแค่ไหน

---

## ขั้นตอนที่ 3: บันทึก Workbook เป็นไฟล์ข้อความ

ตอนนี้เราจะเขียน workbook ลงดิสก์โดยใช้ตัวเลือกที่กำหนดไว้  

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**สิ่งที่คุณจะเห็น:**  
เปิด `Numbers.txt` คุณจะได้บรรทัดเดียว:

```
12350
```

ค่าต้นฉบับ `12345.6789` ถูกปัดเป็น **สี่หลักสำคัญ** ตามที่กำหนดไว้

---

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ (ไม่บังคับแต่แนะนำ)

การทดสอบอัตโนมัติเป็นนิสัยที่ดี นี่คือตัวตรวจสอบอย่างเร็วที่คุณสามารถรันได้ทันทีหลังบันทึก  

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

การรันบล็อกนี้จะพิมพ์เครื่องหมายถูกสีเขียวหากทุกอย่างตรงกัน ให้คุณมั่นใจว่าการ **save excel as txt** ทำงานตามที่คาดหวัง

---

## ความแปรผันทั่วไปและกรณีขอบ

### การส่งออกหลายเซลล์หรือช่วง

หากต้องการ **export excel to txt** สำหรับช่วงทั้งหมด เพียงเติมค่าในเซลล์เพิ่มเติมก่อนบันทึก:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

`TxtSaveOptions` เดียวกันจะใช้กฎ 4‑digit กับแต่ละค่า ผลลัพธ์เป็น:

```
12350
0.0001235
-98800
```

### การเปลี่ยน Delimiter

ระบบบางระบบต้องการค่าแยกด้วยแท็บ ปรับ delimiter ดังนี้:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

ตอนนี้แต่ละเซลล์ในแถวจะแยกด้วยแท็บ

### การจัดการตัวคั่นทศนิยมตาม Locale

หากผู้ใช้ของคุณใช้คอมม่าเป็นตัวคั่นทศนิยม ให้ตั้งค่า culture:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

ผลลัพธ์จะเคารพ locale ทำให้ `12350` แสดงเป็น `12 350` (ช่องว่างเป็นตัวคั่นหลักพันในภาษาฝรั่งเศส)

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**เนื้อหา `Numbers.txt` ที่คาดหวัง (delimiter เริ่มต้น, 4 significant digits):**

```
12350	0.0001235	-98800
```

แท็บ (`\t`) ปรากฏเพราะเราไม่ได้เปลี่ยน delimiter (ค่าตั้งต้นคือแท็บ) หากต้องการเป็นคอมม่าให้เปลี่ยนเป็น CSV ได้ตามต้องการ

---

## สรุป

คุณรู้แล้วว่า **how to save Excel as txt** อย่างแม่นยำโดยควบคุมจำนวนหลักสำคัญ ขั้นตอน—สร้าง workbook, ตั้งค่า `TxtSaveOptions.SignificantDigits`, แล้วบันทึก—เป็นทั้งหมดที่ต้องทำเพื่อ **export excel to txt** อย่างเชื่อถือได้  

จากนี้คุณสามารถ:

- **Export numbers to txt** สำหรับชุดข้อมูลขนาดใหญ่
- ปรับ delimiter, encoding หรือการตั้งค่า culture ให้ตรงกับระบบปลายทางใดก็ได้
- ผสานวิธีนี้กับคุณลักษณะอื่นของ Aspose.Cells (สไตล์, สูตร) ก่อนทำการส่งออก

ลองปรับ `SignificantDigits` เป็น 2 หรือ 6 แล้วดูการเปลี่ยนแปลง ผลลัพธ์ของ **save workbook as text** จะช่วยให้คุณมีเครื่องมือที่ยืดหยุ่นในกระบวนการแลกเปลี่ยนข้อมูลใด ๆ

---

### หัวข้อที่เกี่ยวข้องที่คุณอาจสนใจต่อไป

- **Export Excel to CSV** ด้วยการจัดเรียงคอลัมน์แบบกำหนดเอง
- **Read txt files back into a workbook** (`Workbook.Load` กับ `LoadOptions`)
- **Batch processing** หลาย worksheet และรวมเป็นไฟล์ txt เดียว
- **Performance tuning** สำหรับการส่งออกขนาดใหญ่ (streaming vs. in‑memory)

หากคุณมีคำถามหรืออยากแชร์วิธีที่คุณปรับแต่งการส่งออกสำหรับโปรเจกต์ของคุณ อย่าลังเลที่จะคอมเมนต์ไว้ได้เลย Happy coding!  

---  

*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*  
*Alt text: “ไฟล์ Numbers.txt แสดงค่า 12350, 0.0001235, และ -98800 หลังบันทึก Excel เป็น txt ด้วย 4 หลักสำคัญ.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}