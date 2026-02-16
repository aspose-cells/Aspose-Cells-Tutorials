---
category: general
date: 2026-02-15
description: วิธีจัดรูปแบบสกุลเงินอย่างรวดเร็วโดยใช้การตั้งค่ารูปแบบตัวเลขของคอลัมน์และใช้รูปแบบตัวเลขแบบกำหนดเองใน
  C#. เรียนรู้การดึงคอลัมน์ตามชื่อและการตั้งค่าการจัดแนวคอลัมน์ในกริด.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: th
og_description: วิธีจัดรูปแบบสกุลเงินในคอลัมน์กริดโดยใช้ C#. บทเรียนนี้แสดงวิธีดึงคอลัมน์ตามชื่อ,
  ตั้งค่ารูปแบบตัวเลขของคอลัมน์, ใช้รูปแบบตัวเลขแบบกำหนดเอง, และตั้งค่าการจัดแนวคอลัมน์กริด.
og_title: วิธีจัดรูปแบบสกุลเงินในคอลัมน์กริด – คู่มือฉบับสมบูรณ์
tags:
- C#
- GridFormatting
- UI
title: วิธีจัดรูปแบบสกุลเงินในคอลัมน์กริด – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

dash.

Also need to translate the TL;DR blockquote content.

Also translate "What You’ll Need", "Step‑by‑Step Implementation", etc.

Also translate "Full Working Example", "Expected console output", "Frequently Asked Questions & Edge Cases", table headings and rows.

Also translate "Wrap‑Up" and final paragraph.

Also translate bullet points.

Make sure to keep code block placeholders unchanged.

Also keep the blockquote formatting: > **TL;DR** – By the end you’ll have a ready‑to‑run snippet...

Translate that.

Now produce final content.

Let's translate.

I'll produce Thai translation.

Be careful with punctuation.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีจัดรูปแบบสกุลเงินในคอลัมน์ของ Grid – บทเรียนโปรแกรมเต็มรูปแบบ

เคยสงสัย **วิธีจัดรูปแบบสกุลเงิน** ในคอลัมน์ของกริดโดยไม่ต้องบิดหัวไหม? คุณไม่ได้เป็นคนเดียว เมื่อคุณมองตัวเลขธรรมดาอย่าง `1234.5` แล้วอยากให้มันแสดงเป็น `$1,234.50` อย่างมหัศจรรย์ คำตอบมักจะเป็นเพียงไม่กี่บรรทัดของการตั้งค่า  

ในคู่มือนี้เราจะ **ดึงคอลัมน์ตามชื่อ**, **ตั้งค่ารูปแบบตัวเลขของคอลัมน์**, และ **ใช้รูปแบบตัวเลขแบบกำหนดเอง** ที่สอดคล้องกับรูปแบบบัญชีทั่วไป พร้อมกับ **ตั้งค่าการจัดแนวคอลัมน์ของกริด** และเพิ่มเส้นขอบบางเพื่อให้ UI ดูเรียบหรู

> **TL;DR** – เมื่อจบคุณจะได้โค้ดสั้น ๆ ที่พร้อมรันเพื่อแปลงค่าทศนิยมดิบให้เป็นสกุลเงินที่จัดรูปแบบอย่างสวยงามในคอนโทรลสไตล์ `GridJs` ใด ๆ

---

## สิ่งที่คุณต้องเตรียม

- โปรเจกต์ .NET (เวอร์ชันใดก็ได้ที่รองรับ C# 8.0+ – Visual Studio 2022 ทำงานได้ดี)  
- คอมโพเนนต์กริดที่เปิดเผยคอลเลกชัน `Columns` (ตัวอย่างใช้คลาสสมมติ `GridJs` แต่แนวคิดสามารถนำไปใช้กับ DevExpress, Telerik หรือ Syncfusion grids)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# – ไม่ต้องการเทคนิคขั้นสูง

ถ้าคุณมีทั้งหมดแล้ว เยี่ยมมาก หากยังไม่มี ก็สร้างแอปคอนโซลง่าย ๆ; สามารถจำลองกริดเพื่ออธิบายได้

---

## การดำเนินการแบบขั้นตอน

ด้านล่างแต่ละขั้นตอนคุณจะเห็นบล็อกโค้ดสั้น ๆ คำอธิบายสั้น ๆ เกี่ยวกับ **ทำไม** บรรทัดนั้นสำคัญ และเคล็ดลับเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป

### ## ขั้นตอน 1 – ดึงคอลัมน์ “Amount” ตามชื่อ

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**ทำไมถึงสำคัญ:**  
ส่วนใหญ่ API ของกริดจะเปิดเผยคอลัมน์ผ่านตัวดัชนีแบบคล้ายพจนานุกรม การดึงคอลัมน์โดยใช้ชื่อหัว (`"Amount"`) ทำให้คุณสามารถปรับเปลี่ยนลักษณะการแสดงผลได้โดยไม่ต้องแก้ไขแหล่งข้อมูลพื้นฐาน  

**เคล็ดลับ:** ตรวจสอบให้แน่ใจว่าจัดการกรณีที่ได้ `null` กลับมา – การพิมพ์ชื่อคอลัมน์ผิดหรือสคีมาที่เปลี่ยนแปลงแบบไดนามิกอาจทำให้เกิด `NullReferenceException` ขณะรัน

---

### ## ขั้นตอน 2 – ตั้งค่ารูปแบบตัวเลขของคอลัมน์ด้วยมาสก์สกุลเงินกำหนดเอง

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**ทำไมถึงสำคัญ:**  
สตริงรูปแบบนี้อิงตามแนวทางการจัดรูปแบบบัญชีของ Excel:

- `_(* #,##0.00_)` → ตัวเลขบวก, จัดแนวขวา พร้อมช่องว่างนำหน้าสำหรับสัญลักษณ์สกุลเงิน  
- `_(* (#,##0.00)` → ตัวเลขลบอยู่ในวงเล็บ  
- `_(* \"-\"??_)` → ค่าศูนย์แสดงเป็นขีด  
- `_(@_)` → ค่าข้อความคงเดิมไม่เปลี่ยน

การ **apply custom numeric format** ให้คุณควบคุมคั่นหลักพัน, จำนวนตำแหน่งทศนิยม, และตำแหน่งของสัญลักษณ์สกุลเงินได้อย่างเต็มที่  

**กรณีขอบ:** หากแอปของคุณต้องรองรับโลคัลอื่น (เช่น ยูโรแทนดอลลาร์) ให้แทนที่ช่องว่างนำหน้าด้วยสัญลักษณ์ที่เหมาะสมหรือใช้การจัดรูปแบบที่รับรู้ `CultureInfo` ในแหล่งข้อมูล

---

### ## ขั้นตอน 3 – จัดแนวเนื้อหาคอลัมน์ไปทางขวาเพื่อความอ่านง่าย

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**ทำไมถึงสำคัญ:**  
ค่าทางการเงินจะสแกนได้ง่ายเมื่อจัดแนวตามตำแหน่งจุดทศนิยม การตั้งค่า **set grid column alignment** เป็น `Right` จะทำให้แสดงผลคล้ายกับสเปรดชีต  

**ข้อควรระวัง:** บางกริดอาจละเลยการจัดแนวบนเซลล์ที่ใช้เทมเพลตแบบกำหนดเอง หากคุณพบว่าการจัดแนวไม่ทำงาน ตรวจสอบว่าคอลัมน์ไม่ได้ใช้ renderer เซลล์แบบกำหนดเอง

---

### ## ขั้นตอน 4 – เพิ่มเส้นขอบสีเทาบางรอบเซลล์คอลัมน์

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**ทำไมถึงสำคัญ:**  
เส้นขอบที่ละเอียดช่วยแยกคอลัมน์ “Amount” จากคอลัมน์ข้างเคียง โดยเฉพาะเมื่อกริดมีสีแถวสลับ มันเป็นสัญญาณวิชวลว่าข้อมูลนี้เป็นตัวเลขทางการเงินที่แยกจากกัน  

**เคล็ดลับ:** หากต้องการเส้นหนาสำหรับการพิมพ์ ให้เปลี่ยน `BorderLineStyle` เป็น `Medium` หรือเปลี่ยน `Color` เป็น `Color.Black`

---

## ตัวอย่างทำงานเต็มรูปแบบ

นี่คือตัวอย่างโค้ดทั้งหมดที่คุณสามารถวางลงในโปรเจกต์ WinForms หรือ WPF ที่ใช้คอนโทรลสไตล์ `GridJs` ตัวอย่างยังพิมพ์ค่าที่จัดรูปแบบแล้วลงคอนโซลเพื่อให้คุณตรวจสอบผลลัพธ์โดยไม่ต้องมี UI

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

สังเกตว่าตัวเลขบวกจัดแนวขวา, ตัวเลขลบอยู่ในวงเล็บ, และศูนย์แสดงเป็นขีด – พอดีกับสิ่งที่สตริงรูปแบบกำหนดไว้

---

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| *ถ้ากริดใช้โลคัลอื่น (เช่น € แทน $) จะทำอย่างไร?* | แทนที่ช่องว่างนำหน้าในสตริงรูปแบบด้วยสัญลักษณ์ที่ต้องการ หรือให้แหล่งข้อมูลส่งสตริงที่จัดรูปแบบแล้วโดยใช้ `CultureInfo.CurrentCulture`. |
| *ฉันสามารถใช้รูปแบบเดียวกันกับหลายคอลัมน์ได้หรือไม่?* | ทำได้แน่นอน เก็บสตริงรูปแบบไว้ในคอนสแตนท์ (`const string CurrencyMask = "...";`) แล้วกำหนดให้กับคอลัมน์ที่ต้องการ. |
| *ถ้าคอลัมน์มีค่าเป็นสตริงจะเกิดอะไรขึ้น?* | สตริงรูปแบบจะส่งผลต่อชนิดตัวเลขเท่านั้น ค่าข้อความจะผ่านโดยไม่เปลี่ยนแปลง ซึ่งเป็นเหตุผลที่ส่วนสุดท้ายของมาสก์ (`_(@_)`) มีไว้เพื่อรักษาเนื้อหาที่ไม่ใช่ตัวเลข. |
| *มีผลต่อประสิทธิภาพหรือไม่?* | แทบไม่มี ผลรูปแบบจะถูกนำไปใช้ในขั้นตอนการเรนเดอร์ ไม่ได้ทำในขณะดึงข้อมูล หากคุณไม่ได้เรนเดอร์หลายพันแถวต่อเฟรม คุณจะไม่สังเกตเห็นความช้า. |
| *จะทำให้เส้นขอบหนาขึ้นสำหรับรายงานที่พิมพ์ได้อย่างไร?* | เปลี่ยน `BorderLineStyle.Thin` เป็น `BorderLineStyle.Medium` หรือ `BorderLineStyle.Thick`. บางไลบรารียังให้กำหนดความกว้างเป็นพิกเซลโดยตรงได้. |

---

## สรุป

เราได้อธิบาย **วิธีจัดรูปแบบสกุลเงิน** ในคอลัมน์ของกริดตั้งแต่ต้นจนจบ: ดึงคอลัมน์ตามชื่อ, ตั้งค่ารูปแบบตัวเลขของคอลัมน์, ใช้รูปแบบตัวเลขกำหนดเอง, จัดแนวเซลล์, และเพิ่มเส้นขอบที่ดูดี ตัวอย่างเต็มรูปแบบพร้อมทำงานทันทีและแสดงผลภาพที่คุณคาดหวัง  

หากคุณพร้อมจะต่อยอดต่อไป ลอง:

- **โลคัลแบบไดนามิก** – สลับสตริงรูปแบบตามโลคัลของผู้ใช้  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}