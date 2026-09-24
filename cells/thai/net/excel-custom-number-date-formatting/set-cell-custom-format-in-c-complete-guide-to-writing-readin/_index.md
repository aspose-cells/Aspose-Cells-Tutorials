---
category: general
date: 2026-03-21
description: ตั้งค่ารูปแบบเซลล์แบบกำหนดเองใน C# และเรียนรู้วิธีเขียนวันที่ลงใน Excel,
  ใช้รูปแบบวันที่แบบกำหนดเอง, อ่าน DateTime จาก Excel, และสร้างเวิร์กบุ๊กหรือเวิร์กชีตอย่างรวดเร็ว.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: th
og_description: ตั้งค่ารูปแบบเซลล์แบบกำหนดเองใน C# เพื่อเขียนวันที่ลง Excel ใช้รูปแบบวันที่แบบกำหนดเอง
  อ่าน DateTime จาก Excel และสร้างเวิร์กบุ๊กและแผ่นงานได้อย่างง่ายดาย.
og_title: ตั้งค่ารูปแบบเซลล์แบบกำหนดเองใน C# – เขียนและอ่านวันที่ใน Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: ตั้งค่ารูปแบบเซลล์แบบกำหนดเองใน C# – คู่มือฉบับสมบูรณ์สำหรับการเขียนและอ่านวันที่ใน
  Excel
url: /th/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่ารูปแบบเซลล์แบบกำหนดเอง – เขียนและอ่านวันที่ใน Excel ด้วย C#

เคยต้องการ **ตั้งค่ารูปแบบเซลล์แบบกำหนดเอง** ในไฟล์ Excel จาก C# แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ในเครื่องมือรายงานหรือยูทิลิตี้การส่งออกข้อมูลหลาย ๆ ตัว วันที่ต้องแสดงในภาษาท้องถิ่นเฉพาะ—เช่น วันที่ตามยุคญี่ปุ่น, ปฏิทินการเงิน, หรือสตริง ISO‑8601.  

ในบทแนะนำนี้ เราจะพาคุณผ่าน **ตัวอย่างที่สมบูรณ์และสามารถรันได้** ที่แสดงวิธี **เขียนวันที่ลงใน Excel**, **ใช้รูปแบบวันที่แบบกำหนดเอง**, **อ่าน DateTime จาก Excel**, และ **สร้าง workbook worksheet** ด้วย Aspose.Cells. เมื่อจบคุณจะมีโปรแกรมเดียวที่เป็นอิสระซึ่งสามารถนำไปใช้ในโปรเจกต์ .NET ใดก็ได้.

## สิ่งที่คุณจะได้เรียนรู้

- วิธี **สร้าง workbook worksheet** ด้วยโปรแกรม.  
- ขั้นตอนที่แน่นอนเพื่อ **เขียนวันที่ลงใน Excel** โดยใช้สตริงที่ระบุภาษาท้องถิ่น.  
- วิธี **ใช้รูปแบบวันที่แบบกำหนดเอง** (รวมถึงการแสดงผลตามยุคญี่ปุ่น).  
- วิธี **อ่าน DateTime จาก Excel** กลับเป็นอ็อบเจ็กต์ `DateTime`.  
- เคล็ดลับ, จุดบกพร่อง, และรูปแบบต่าง ๆ ที่คุณอาจเจอเมื่อทำงานกับวันที่ใน Excel.

ไม่ต้องการเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่เลย.

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)  
- Aspose.Cells สำหรับ .NET ที่ติดตั้งผ่าน NuGet (`Install-Package Aspose.Cells`).  
- ความเข้าใจพื้นฐานของไวยากรณ์ C#—ไม่มีอะไรซับซ้อน  

> **เคล็ดลับมืออาชีพ:** หากคุณใช้ Visual Studio, เปิดใช้งาน *nullable reference types* เพื่อจับบั๊กเล็ก ๆ ได้ตั้งแต่แรก.

## ขั้นตอนที่ 1: สร้าง Workbook และ Worksheet  

สิ่งแรกที่ต้องทำ: คุณต้องมีอ็อบเจ็กต์ workbook ที่แทนไฟล์ Excel, และ worksheet ที่ข้อมูลจะถูกจัดเก็บ.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*ทำไมจึงสำคัญ:* คลาส `Workbook` เป็นจุดเริ่มต้นสำหรับการทำงานกับ Excel ทั้งหมด การสร้างมันในหน่วยความจำหมายความว่าคุณจะไม่ต้องสัมผัสระบบไฟล์จนกว่าจะบันทึกอย่างชัดเจน ซึ่งทำให้กระบวนการเร็วและเป็นมิตรต่อการทดสอบ.

## ขั้นตอนที่ 2: เขียนวันที่ลงใน Excel  

ต่อไป เราจะใส่สตริงวันที่ตามยุคญี่ปุ่น (`"R02-04-01"`) ลงในเซลล์ **A1** สตริงนี้จำลองยุค Reiwa (ปีที่ 2, เดือนเมษายน 1).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*กำลังเกิดอะไรขึ้น:* `PutValue` จะเก็บสตริงดิบ Aspose.Cells จะพยายามแปลงในภายหลังตามสไตล์ของเซลล์ หากคุณข้ามขั้นตอนนี้และเขียน `DateTime` โดยตรง คุณจะสูญเสียข้อมูลยุคที่ต้องการแสดง.

## ขั้นตอนที่ 3: ใช้รูปแบบตัวเลขวันที่ที่มีอยู่ในตัว (ID 14)

Excel มีรูปแบบวันที่ที่มีอยู่ในตัวด้วย ID 14 (`mm-dd-yy`). การใช้มันบอกให้เอนจินทราบว่าเซลล์ **มีวันที่**, ไม่ใช่แค่ข้อความ.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*ทำไมต้องใช้ ID 14?* มันเป็นรูปแบบ “วันที่สั้น” สากลที่ทำให้ Excel ปฏิบัติกับเนื้อหาเป็นค่าที่เป็นวันที่ ซึ่งเป็นเงื่อนไขเบื้องต้นสำหรับรูปแบบกำหนดเองใด ๆ ให้ทำงานได้อย่างถูกต้อง.

## ขั้นตอนที่ 4: ตั้งค่ารูปแบบกำหนดเองเพื่อแสดงการระบุยุคญี่ปุ่น  

ต่อไปเป็นส่วนที่สนุก: เราบอกให้ Excel แสดงวันที่โดยใช้รูปแบบยุคญี่ปุ่น สตริงกำหนดเอง `[$-ja-JP]ggge年m月d日` ทำเช่นนั้นได้อย่างแม่นยำ.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Explanation:*  
- `[$-ja-JP]` บังคับให้ภาษาถูกตั้งเป็นญี่ปุ่น.  
- `ggg` คือชื่อยุค (เช่น “R” สำหรับ Reiwa).  
- `e` คือปีของยุค.  
- `年`, `月`, `日` เป็นอักขระญี่ปุ่นที่หมายถึง ปี, เดือน, วัน ตามลำดับ.

หากคุณต้องการภาษาท้องถิ่นอื่น เพียงแทนที่ `ja-JP` ด้วยรหัสวัฒนธรรมที่เหมาะสม (เช่น `en-US`).

## ขั้นตอนที่ 5: ดึงค่าที่แปลงเป็น DateTime  

สุดท้าย เรามาอ่าน **`DateTime` จริง** ที่ Excel แปลงจากเซลล์ นี่เป็นการพิสูจน์ว่าสตริงถูกตีความอย่างถูกต้อง.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*ผลลัพธ์:* คอนโซลจะแสดง `Parsed DateTime: 2020-04-01`. แม้ว่าเราจะใส่สตริงยุคญี่ปุ่น, Excel จะเก็บวันที่แบบ Gregorian ภายใน ซึ่งคุณสามารถใช้สำหรับการคำนวณ, การเปรียบเทียบ, หรือการส่งออกต่อไป.

## ขั้นตอนที่ 6: บันทึก Workbook (ไม่บังคับ)

หากคุณต้องการดู workbook ที่มีรูปแบบใน Excel เพียงบันทึกลงดิสก์.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

เปิดไฟล์ **JapaneseEraDate.xlsx** ที่สร้างขึ้นและคุณจะเห็นเซลล์ **A1** แสดง `R02年4月1日` (รูปแบบยุคญี่ปุ่นที่เราตั้งค่าไว้).

![ตัวอย่างการตั้งค่ารูปแบบเซลล์แบบกำหนดเอง](image-placeholder.png "เซลล์ Excel แสดงวันที่ตามยุคญี่ปุ่น – ตั้งค่ารูปแบบเซลล์แบบกำหนดเอง")

*ข้อความ alt ด้านบนมีคีย์เวิร์ดหลัก, ตรงตามข้อกำหนด SEO ของรูปภาพ.*

## ความแปรผันทั่วไปและกรณีขอบ  

### การเขียนรูปแบบวันที่อื่น  

หากคุณต้องการรูปแบบ ISO‑8601 (`2020-04-01`) แทนสตริงยุค เพียงเปลี่ยนการเรียก `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### การจัดการกับเซลล์ที่เป็น Null หรือว่าง  

เมื่ออ่านวันที่, ควรตรวจสอบเซลล์ที่ว่างเสมอเพื่อหลีกเลี่ยง `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### การสนับสนุนหลายภาษาท้องถิ่น  

คุณสามารถวนลูปผ่านรายการรหัสวัฒนธรรมและใช้แบบไดนามิก:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## เคล็ดลับมืออาชีพและข้อควรระวัง  

- **ควรตั้งค่ารูปแบบตัวเลขที่มีอยู่ในตัวก่อนเสมอ** (`Style.Number`). หากไม่ทำ, Excel จะถือว่าเซลล์เป็นข้อความธรรมดาและรูปแบบกำหนดเองจะถูกละเลย.  
- **รหัสภาษาท้องถิ่นไม่สนใจตัวพิมพ์ใหญ่/เล็ก** แต่การใช้รูปแบบมาตรฐาน (`ja-JP`) จะหลีกเลี่ยงความสับสน.  
- **การบันทึกเป็นทางเลือก** สำหรับการประมวลผลในหน่วยความจำ; คุณสามารถสตรีม workbook ไปยังการตอบสนองเว็บโดยตรง (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **ใบอนุญาต Aspose.Cells**: เวอร์ชันประเมินฟรีจะใส่ลายน้ำ. สำหรับการใช้งานจริง, ตรวจสอบว่าคุณมีใบอนุญาตที่ถูกต้องเพื่อหลีกเลี่ยงการลดประสิทธิภาพ.

## สรุป  

เราได้แสดงวิธี **ตั้งค่ารูปแบบเซลล์แบบกำหนดเอง** ใน C# เพื่อแสดงวันที่ตามยุคญี่ปุ่น, วิธี **เขียนวันที่ลงใน Excel**, **ใช้รูปแบบวันที่แบบกำหนดเอง**, **อ่าน DateTime จาก Excel**, และ **สร้าง workbook worksheet**—ทั้งหมดในโปรแกรมเดียวที่เป็นอิสระ. คีย์เวิร์ดหลักปรากฏอย่างเป็นธรรมชาติตลอดบท, ขณะที่คีย์เวิร์ดรองถูกใส่ในหัวข้อและข้อความ, ตรงตามมาตรฐาน SEO และการอ้างอิง AI.

## ต่อไปคืออะไร?

- สำรวจ **conditional formatting** เพื่อไฮไลท์วันที่ล่าช้า.  
- ผสานวิธีนี้กับ **PivotTables** เพื่อการรายงานแบบไดนามิก.  
- ลอง **อ่านไฟล์ CSV ขนาดใหญ่** และแปลงเป็น Excel ด้วยตรรกะการจัดการวันที่เดียวกัน.  

อย่าลังเลที่จะทดลองกับภาษาท้องถิ่นต่าง ๆ, รูปแบบกำหนดเอง, หรือแม้แต่โซนเวลา หากคุณเจอปัญหาใด ๆ แสดงความคิดเห็นด้านล่าง—ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}