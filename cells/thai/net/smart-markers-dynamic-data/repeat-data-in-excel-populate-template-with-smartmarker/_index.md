---
category: general
date: 2026-02-21
description: ทำซ้ำข้อมูลใน Excel อย่างรวดเร็วด้วย SmartMarker—เรียนรู้วิธีเติมข้อมูลลงในเทมเพลต
  Excel และทำซ้ำแถวได้อย่างง่ายดาย
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: th
og_description: ทำซ้ำข้อมูลใน Excel ด้วย SmartMarker เรียนรู้วิธีเติมข้อมูลในเทมเพลต
  Excel ทำซ้ำแถว และอัตโนมัติสเปรดชีตของคุณ
og_title: ทำซ้ำข้อมูลใน Excel – เติมเทมเพลตด้วย SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: ทำซ้ำข้อมูลใน Excel – เติมเทมเพลตด้วย SmartMarker
url: /th/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำซ้ำข้อมูลใน Excel – เติมเทมเพลตด้วย SmartMarker

เคยต้องการ **repeat data in Excel** แต่ไม่แน่ใจว่าจะหลีกเลี่ยงการคัดลอก‑วางด้วยมือได้อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายสถานการณ์การรายงานคุณมีรายการของรายการที่ต้องขยายเป็นแถวโดยอัตโนมัติ และการทำด้วยมือเป็นสูตรสำหรับข้อผิดพลาด

นี่คือเรื่อง—การใช้ SmartMarkerProcessor จากไลบรารี **GemBox.Spreadsheet** ทำให้คุณ **populate an Excel template** ด้วยบรรทัดเดียวของ C# และทำให้แถวทำซ้ำสำหรับแต่ละรายการในคอลเลกชันของคุณ ในคู่มือนี้เราจะเดินผ่านขั้นตอนอย่างละเอียด แสดงโค้ดเต็มรูปแบบ และอธิบายว่าทำไมแต่ละส่วนจึงสำคัญ เพื่อให้คุณสามารถทำซ้ำแถวใน Excel ได้อย่างมั่นใจโดยไม่ต้องเหนื่อย

## สิ่งที่คุณจะได้เรียนรู้

* วิธีกำหนดโครงสร้างข้อมูลที่ขับเคลื่อนการทำซ้ำ  
* วิธีเชื่อม `SmartMarkerProcessor` กับเวิร์กบุ๊กที่มีแผ่นเทมเพลตซ่อนอยู่  
* วิธีที่เครื่องหมาย `${Repeat:Item}` ขยายเป็นหลายแถวโดยอัตโนมัติ  
* เคล็ดลับการจัดการกรณีขอบเช่นคอลเลกชันว่างหรือการจัดรูปแบบแบบกำหนดเอง  

เมื่อจบบทเรียนนี้คุณจะสามารถ **populate excel from data** ในวิธีที่สามารถขยายได้ง่าย ดูแลรักษาง่าย และทำงานกับโปรเจกต์ .NET ใดก็ได้

---

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดใช้คุณลักษณะ C# สมัยใหม่)  
* แพคเกจ NuGet **GemBox.Spreadsheet** (เวอร์ชันฟรีทำงานได้ถึง 150 แถว)  
* ไฟล์เทมเพลต Excel เบื้องต้น (`Template.xlsx`) ที่มีแผ่นซ่อนชื่อ `HiddenTemplate`  
* ความคุ้นเคยกับอ็อบเจ็กต์ C# และ LINQ จะช่วยได้แต่ไม่จำเป็น  

---

## ขั้นตอนที่ 1 – กำหนดโครงสร้างข้อมูลสำหรับทำซ้ำ

ก่อนอื่นคุณต้องมีแหล่งข้อมูลที่เครื่องมือ SmartMarker สามารถวนลูปได้ ในแอปจริงส่วนใหญ่ข้อมูลนี้จะมาจากฐานข้อมูล, API หรือไฟล์ CSV เพื่อความชัดเจนเราจะใช้ชนิดไม่ระบุชื่อที่มีคุณสมบัติเพียงอย่างเดียวชื่อ `Item` ซึ่งเก็บอาร์เรย์ของสตริง

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Why this matters:** เครื่องหมาย `${Repeat:Item}` ภายในเทมเพลต Excel จะมองหาคุณสมบัติชื่อ `Item` หากคุณเปลี่ยนชื่อคุณสมบัติ ต้องอัปเดตเครื่องหมายให้ตรงกัน การเชื่อมโยงอย่างแน่นหนานี้ทำให้เทมเพลตสอดคล้องกับโค้ดของคุณง่ายขึ้น ทำให้ **populate excel template** ง่ายกว่าโดยไม่ต้องเดาชื่อคอลัมน์

### การเปลี่ยนแปลงทั่วไป

* **Complex objects:** แทนการใช้แอเรย์สตริงง่าย ๆ คุณสามารถส่งรายการอ็อบเจ็กต์ (`new[] { new { Name = "A", Qty = 10 } }`) เครื่องหมายจะทำซ้ำแถวและคุณสามารถอ้างอิง `${Item.Name}` และ `${Item.Qty}` ในแผ่นได้  
* **Empty collections:** หาก `Item` ว่าง SmartMarker จะลบบล็อกทำซ้ำออกโดยอัตโนมัติ ทำให้เทมเพลตคงเดิม—เหมาะกับส่วนที่เป็นตัวเลือก  

---

## ขั้นตอนที่ 2 – สร้าง SmartMarkerProcessor สำหรับแผ่นเทมเพลตที่ซ่อนอยู่

ต่อไปให้โหลดเวิร์กบุ๊กของคุณและสร้างอินสแตนซ์ `SmartMarkerProcessor` ชี้ไปที่เวิร์กบุ๊กที่มีแผ่นเทมเพลตซ่อนอยู่; SmartMarker จะคัดลอกแผ่นนั้นไปยังแผ่นที่มองเห็นได้และขยายเครื่องหมายทำซ้ำ

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** หากคุณมีหลายเทมเพลตในไฟล์เดียว คุณสามารถระบุชื่อแผ่นต้นทางเมื่อเรียก `processor.Process` สิ่งนี้ช่วยเมื่อคุณต้อง **repeat rows in excel** สำหรับส่วนต่าง ๆ ของรายงาน  

### การจัดการกรณีขอบ

* **Missing template sheet:** ห่อการโหลดด้วย try/catch แล้วบันทึกข้อผิดพลาดที่ชัดเจน—จะป้องกันความล้มเหลวเงียบเมื่อเส้นทางไฟล์ผิด  
* **Large data sets:** สำหรับหลายพันแถว พิจารณา stream ผลลัพธ์ไปยังไฟล์ (`processor.Save`) แทนการเก็บทั้งหมดในหน่วยความจำ  

---

## ขั้นตอนที่ 3 – นำข้อมูลไปใช้และขยายเครื่องหมาย `${Repeat:Item}`

ตอนนี้มาถึงบรรทัดมหัศจรรย์ที่ทำการทำซ้ำแถวจริง ๆ ส่งอ็อบเจ็กต์ที่คุณสร้างในขั้นตอน 1 ไปยัง `processor.Process` SmartMarker จะค้นหาเครื่องหมาย `${Repeat:Item}` ทุกตัว คัดลอกแถวสำหรับแต่ละรายการ และแทนที่ตัวแปรด้วยค่าจริง

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### สิ่งที่คุณควรเห็น

เมื่อคุณเปิด `Result.xlsx` แผ่นเทมเพลตที่ซ่อนจะถูกคัดลอกไปยังแผ่นที่มองเห็นได้ใหม่ (โดยค่าเริ่มต้นชื่อ `Sheet1`) แถวที่มี `${Repeat:Item}` จะปรากฏสามครั้ง โดยเซลล์แสดง **A**, **B**, และ **C** ตามลำดับ

| Item |
|------|
| A    |
| B    |
| C    |

หากคุณเพิ่มคอลัมน์อื่น ๆ เช่น `${Item.Price}` ค่าจะถูกเติมอัตโนมัติจากแหล่งข้อมูล  

---

## วิธีทำซ้ำแถวใน Excel โดยไม่ใช้ SmartMarker (เปรียบเทียบอย่างรวดเร็ว)

| วิธี                     | ความซับซ้อนของโค้ด | การบำรุงรักษา | ประสิทธิภาพ |
|-------------------------|---------------------|---------------|--------------|
| Manual copy‑paste       | High                | Low           | Poor         |
| VBA macro               | Medium              | Medium        | Good         |
| **SmartMarkerProcessor**| Low                 | High          | Excellent    |

ตามที่เห็น การใช้ SmartMarker เพื่อ **repeat data in excel** ให้การแยกส่วนที่สะอาดที่สุดระหว่างการออกแบบเทมเพลตและตรรกะธุรกิจ นอกจากนี้ยังเป็นภาษาที่ไม่ขึ้นกับภาษา—แนวคิดคล้ายกันมีใน Java, Python, และไลบรารี JavaScript  

---

## เคล็ดลับขั้นสูง & ข้อผิดพลาดทั่วไป

### 1. การจัดรูปแบบแถวที่ทำซ้ำ

SmartMarker คัดลอกแถวทั้งหมดรวมถึงสไตล์เซลล์, เส้นขอบ, และการจัดรูปแบบตามเงื่อนไข หากคุณต้องการสไตล์ที่แตกต่างสำหรับแถวแรกหรือแถวสุดท้าย ให้เพิ่มเครื่องหมายพิเศษเช่น `${If:Item.IsFirst}` และใช้สูตรเงื่อนไขใน Excel  

### 2. การจัดการกับชุดข้อมูลขนาดใหญ่

เมื่อทำงานกับ > 10 000 แถว ให้ปิดการคำนวณอัตโนมัติของ Excel ก่อนประมวลผล:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

เปิดการคำนวณใหม่หลังบันทึกเพื่อให้ประสิทธิภาพคงที่  

### 3. เติมข้อมูล Excel จากฐานข้อมูลจริง

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

จากนั้นใช้ `${Repeat:Order}` ในเทมเพลตเพื่อแสดงรายการสั่งซื้อทั้งหมด แพทเทิร์นนี้แสดงให้เห็นว่าการ **populate excel from data** จาก Entity Framework ทำได้ง่ายแค่ไหน  

### 4. การใช้หลายบล็อกทำซ้ำ

คุณสามารถมีเครื่องหมาย `${Repeat:...}` หลายตัวบนแผ่นเดียวหรือแผ่นต่าง ๆ SmartMarker จะประมวลผลตามลำดับ ดังนั้นลำดับสำคัญเฉพาะเมื่อบล็อกหนึ่งพึ่งพาผลลัพธ์ของอีกบล็อกหนึ่ง  

---

## ตัวอย่างที่สามารถรันได้ครบถ้วน

ด้านล่างเป็นแอปคอนโซลที่เป็นอิสระ คุณสามารถคัดลอกไปวางใน Visual Studio แล้วรันได้ทันที แสดงขั้นตอนทั้งสามพร้อมการบันทึกไฟล์

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Expected output:** `Result.xlsx` มีแผ่นที่แถวที่มี `${Repeat:Item}` ปรากฏสามครั้ง แสดง A, B, และ C ไม่ต้องปรับแก้ด้วยมือ  

---

## สรุป

คุณตอนนี้รู้วิธี **repeat data in excel** อย่างมีประสิทธิภาพโดยใช้ SmartMarkerProcessor โดยการกำหนดอ็อบเจ็กต์ข้อมูลง่าย ๆ โหลดเทมเพลตเวิร์กบุ๊ก และเรียก `Process` คุณสามารถ **populate excel template**, **repeat rows in excel**, และโดยทั่วไป **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}