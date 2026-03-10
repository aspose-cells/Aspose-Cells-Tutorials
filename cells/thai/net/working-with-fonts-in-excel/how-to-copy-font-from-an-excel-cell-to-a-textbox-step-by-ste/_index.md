---
category: general
date: 2026-02-15
description: วิธีคัดลอกฟอนต์และใช้สไตล์เซลล์ใน C# ด้วยตัวอย่างง่าย ๆ เรียนรู้วิธีดึงสไตล์เซลล์และใช้การจัดรูปแบบเซลล์เพื่อกำหนดขนาดฟอนต์ของ
  textbox.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: th
og_description: วิธีคัดลอกแบบอักษรจากเซลล์ในแผ่นงานและนำสไตล์เซลล์ไปใช้กับ TextBox
  คู่มือฉบับนี้แสดงวิธีดึงสไตล์เซลล์ ใช้การจัดรูปแบบเซลล์ และตั้งขนาดฟอนต์ของ TextBox
og_title: วิธีคัดลอกฟอนต์จากเซลล์ Excel – การสอน C# อย่างครบถ้วน
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: วิธีคัดลอกฟอนต์จากเซลล์ Excel ไปยัง TextBox – คู่มือขั้นตอนโดยละเอียด
url: /th/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีคัดลอกฟอนต์จากเซลล์ Excel ไปยัง TextBox – คำแนะนำ C# ฉบับสมบูรณ์

เคยต้องการ **คัดลอกฟอนต์** จากเซลล์ในสเปรดชีตและทำให้ TextBox ของ UI มีลักษณะเหมือนกันอย่างเต็มที่หรือไม่? คุณไม่ได้เป็นคนเดียวที่ต้องการเช่นนั้น ในเครื่องมือรายงานหรือแดชบอร์ดที่กำหนดเองหลายๆ ตัว คุณมักจะดึงข้อมูลจาก Excel แล้วพยายามรักษาความเหมือนเดิมของการแสดงผล—font family, size, และ colour—ให้คงที่  

ข่าวดีคือด้วยเพียงไม่กี่บรรทัดของ C# คุณสามารถ **get cell style**, อ่านคุณสมบัติฟอนต์ของมัน, และ **apply cell style** ไปยังคอนโทรล text‑box ใดก็ได้ ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดงวิธี **use cell formatting** และแม้กระทั่ง **set textbox font size** ด้วยโปรแกรม

## สิ่งที่คุณจะได้เรียนรู้

- วิธีดึงอ็อบเจกต์ `TextBox` จากคอมโพเนนต์กริด (`gridJs` ในตัวอย่างของเรา)
- วิธีอ่าน font family, size, และ colour จากเซลล์ Excel เฉพาะ (`B2`)
- วิธีคัดลอกแอตทริบิวต์ฟอนต์เหล่านั้นไปยัง text box เพื่อให้ UI สะท้อนสเปรดชีต
- ข้อผิดพลาดทั่วไป (เช่น colour conversion) และ **pro tips** เล็กน้อยเพื่อทำให้โค้ดของคุณแข็งแรง
- โค้ดสแนปช็อตพร้อมรันที่คุณสามารถนำไปใส่ในแอปคอนโซลหรือโครงการ WinForms

**ข้อกำหนดเบื้องต้น**  
You should have:

1. .NET 6+ (หรือ .NET Framework 4.8) ติดตั้งแล้ว  
2. แพคเกจ EPPlus NuGet (สำหรับการจัดการ Excel)  
3. คอนโทรลกริดที่เปิดเผยพจนานุกรม `TextBoxes` (ตัวอย่างใช้ `gridJs` ที่เป็นเรื่องสมมติ แต่แนวคิดทำงานกับไลบรารี UI ใดก็ได้)

ตอนนี้ มาเริ่มทำกันเลย.

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และโหลด Worksheet

ขั้นแรก สร้างโปรเจกต์คอนโซลหรือ WinForms ใหม่และเพิ่ม EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

จากนั้น โหลด workbook และดึงเซลล์ที่คุณต้องการคัดลอกสไตล์

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**ทำไมเรื่องนี้สำคัญ:** EPPlus ให้คุณเข้าถึงอ็อบเจกต์ `Style` โดยตรง ซึ่งมีอ็อบเจกต์ย่อย `Font` จากนั้นคุณสามารถอ่าน `Name`, `Size`, และ `Color` ได้ นี่คือแกนหลักของการทำ **get cell style**

## ขั้นตอนที่ 2: ดึง TextBox เป้าหมายจากกริดของคุณ

สมมติว่ากริด UI ของคุณ (`gridJs`) เก็บ text box ในพจนานุกรมที่ใช้ชื่อคอลัมน์เป็นคีย์ คุณสามารถดึงอันที่ต้องการได้ดังนี้:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

หากคุณใช้ WinForms, `notesTextBox` อาจเป็นคอนโทรล `TextBox`; สำหรับ WPF อาจเป็นองค์ประกอบ `TextBox`, และสำหรับกริดบนเว็บอาจเป็นอ็อบเจกต์ JavaScript interop จุดสำคัญคือคุณมีอ้างอิงที่สามารถจัดการได้

## ขั้นตอนที่ 3: โอนย้าย Font Family

เมื่อเรามีสไตล์ต้นทางและคอนโทรลปลายทางแล้ว ให้คัดลอก font family

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**เคล็ดลับ:** ไม่ใช่ทุก UI framework ที่เปิดเผย property `FontFamily` ที่รับสตริงธรรมดา ใน WinForms คุณจะตั้งค่า `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. ปรับให้เหมาะสม

## ขั้นตอนที่ 4: โอนย้าย Font Size

ขนาดฟอนต์ถูกเก็บเป็น `float` ใน EPPlus ใช้โดยตรง:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

หากคอนโทรลของคุณใช้หน่วย points (ซึ่งส่วนใหญ่ทำ) คุณสามารถกำหนดค่าได้โดยไม่ต้องแปลง สำหรับกริดที่ใช้ CSS อาจต้องต่อท้ายด้วย `"pt"`

## ขั้นตอนที่ 5: โอนย้าย Colour ของฟอนต์

การแปลงสีเป็นส่วนที่ซับซ้อนที่สุด เนื่องจาก EPPlus เก็บสีเป็นจำนวนเต็ม ARGB ในขณะที่ UI framework ส่วนใหญ่คาดหวัง `System.Drawing.Color` หรือสตริง hex ของ CSS

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **ทำไมวิธีนี้ถึงได้ผล:** `GetColor()` แก้ไขสีที่อิงธีมและคืนค่า `System.Drawing.Color` ที่เป็นรูปธรรม หากเซลล์ใช้สีเริ่มต้น (ไม่มีการตั้งค่าเฉพาะ) เราจะตั้งค่าเป็นสีดำเพื่อหลีกเลี่ยงข้อยกเว้น null reference

## ตัวอย่างทำงานเต็มรูปแบบ

เมื่อรวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างแอปคอนโซลขนาดเล็กที่อ่านไฟล์ Excel, ดึงฟอนต์จาก **B2**, และนำไปใช้กับ text box จำลอง

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง (สมมติว่า B2 ใช้ Arial, 12 pt, สีฟ้า):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

รันโปรแกรม, เปิด UI ของคุณ, และคุณจะเห็น text box “Notes” ตอนนี้สะท้อนสไตล์ฟอนต์ของเซลล์ **B2** อย่างตรงกัน ไม่ต้องปรับด้วยมือ

## คำถามที่พบบ่อยและกรณีขอบ

### ถ้าเซลล์ใช้สีธีมแทนค่า RGB ที่ระบุโดยตรง?

`GetColor()` ของ EPPlus จะทำการแก้ไขสีธีมเป็น `System.Drawing.Color` ที่เป็นรูปธรรมโดยอัตโนมัติ อย่างไรก็ตาม หากคุณใช้ไลบรารีเก่าที่คืนค่าเฉพาะดัชนีธีม คุณจะต้องแมปดัชนีนั้นไปยังพาเลตสีด้วยตนเอง

### ฉันสามารถคัดลอกแอตทริบิวต์สไตล์อื่นได้หรือไม่ (เช่น bold, italic)?

แน่นอน. อ็อบเจกต์ `ExcelStyle.Font` ยังเปิดเผย `Bold`, `Italic`, `Underline`, และ `Strike`. เพียงตั้งค่า property ที่สอดคล้องบนคอนโทรล UI ของคุณ:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### ถ้าคอนโทรลกริดไม่เปิดเผย property `FontColor`?

ส่วนใหญ่ของ UI framework สมัยใหม่มี property นี้, แต่ถ้าของคุณรับสตริง CSS เท่านั้น ให้แปลง `Color` เป็นรูปแบบ hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### ฉันจะจัดการหลายเซลล์พร้อมกันอย่างไร?

วนลูปผ่านช่วงที่ต้องการ, ดึงสไตล์ของแต่ละเซลล์, และนำไปใช้กับ text box ที่สอดคล้องกัน จำไว้ว่าให้แคชอ็อบเจกต์สไตล์หากคุณประมวลผลหลายแถวเพื่อหลีกเลี่ยงการลดประสิทธิภาพ

## เคล็ดลับระดับมืออาชีพและข้อผิดพลาดทั่วไป

- **Cache the ExcelPackage** – การเปิดและปิดไฟล์สำหรับแต่ละเซลล์มีค่าใช้จ่ายสูง โหลด workbook ครั้งเดียวแล้วใช้ซ้ำอ็อบเจกต์ `ExcelWorksheet`
- **Watch out for null colours** – เซลล์ที่สืบทอดสีเริ่มต้นจะคืนค่า `null`. ควรให้ค่า fallback เสมอ (สีดำหรือค่าเริ่มต้นของคอนโทรล)
- **Mind DPI scaling** – หากคุณมุ่งเป้าไปที่จอแสดงผล DPI สูง ขนาดฟอนต์อาจดูใหญ่ขึ้นเล็กน้อย ปรับโดยใช้ `Graphics.DpiX` หากจำเป็น
- **Thread safety** – EPPlus ไม่ปลอดภัยต่อการทำงานหลายเธรด หากคุณประมวลผลหลายชีตพร้อมกัน ควรสร้าง `ExcelPackage` แยกสำหรับแต่ละเธรด

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to copy font** จากเซลล์ Excel และ **apply cell style** ไปยังคอนโทรล text‑box ใดก็ได้ด้วย C#. โดยการดึง `Style` ของเซลล์, แยกคุณสมบัติ `Font` ของมัน, และกำหนดให้กับองค์ประกอบ UI, คุณจะรักษาความสอดคล้องของการแสดงผลโดยไม่ต้องคัดลอกด้วยมือ  

โซลูชันเต็มรูปแบบ—การโหลด workbook, การดึงสไตล์ของเซลล์, และการตั้งค่า font family, size, และ colour ของ textbox—ครอบคลุมแกนหลักของ **use cell formatting** และแสดงวิธี **set textbox font size** อย่างถูกต้อง  

ต่อไป ลองขยายตัวอย่างเพื่อคัดลอกสีพื้นหลัง, เส้นขอบ, หรือแม้แต่เนื้อหาเต็มของเซลล์ หากคุณทำงานกับไลบรารี data‑grid ที่รองรับการเรนเดอร์เซลล์แบบเต็มรูปแบบ คุณสามารถส่งข้อมูลสไตล์เดียวกันที่ดึงจาก Excel ไปให้มันได้ ทำให้ UI และรายงานของคุณสอดคล้องกันอย่างสมบูรณ์  

มีคำถามเพิ่มเติมไหม? ฝากคอมเมนต์หรือสำรวจหัวข้อที่เกี่ยวข้องเช่น “dynamic Excel‑to‑UI binding” และ “theme‑aware colour conversion”. โค้ดดิ้งสนุก!

![ตัวอย่างการคัดลอกฟอนต์](placeholder-image.jpg "การคัดลอกฟอนต์จากเซลล์ Excel ไปยัง TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}