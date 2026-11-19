---
category: general
date: 2026-11-19
description: วิธีทำซ้ำแผ่นงานขณะใส่ข้อมูลอาร์เรย์ใน Excel เรียนรู้การสร้างแผ่นงานหลายแผ่นและใส่ข้อมูลลงในแผ่นงานจากรายการในไม่กี่ขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: th
lastmod: 2026-11-19
og_description: วิธีทำซ้ำแผ่นงานโดยใช้ SmartMarkerProcessor. ทำตามคำแนะนำนี้เพื่อเติมข้อมูล
  Excel ด้วยข้อมูลอาเรย์, สร้างหลายแผ่นงาน, และเติมข้อมูลแผ่นงานจากรายการ.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: วิธีทำซ้ำแผ่นงานใน Excel – คู่มือทีละขั้นตอน
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: วิธีทำซ้ำแผ่นงานใน Excel ด้วย SmartMarkerProcessor
url: /th/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำซ้ำแผ่นงานใน Excel ด้วย SmartMarkerProcessor

หากคุณต้องการ **how to repeat worksheet** ขณะสร้างรายงาน Excel คู่มือนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และสามารถรันได้ เมื่อจบบทเรียนคุณจะสามารถ **populate Excel with array** ข้อมูล, **generate multiple worksheets**, และ **populate worksheet from list** ด้วยไลบรารี SmartMarkerProcessor

การทำซ้ำแผ่นงานเป็นความต้องการทั่วไปเมื่อแต่ละแผนก, ภูมิภาค, หรือช่วงเวลา ต้องการแท็บของตนเอง ตัวอย่างด้านล่างจะแสดงขั้นตอนที่แน่นอน, อธิบายว่าทำไมการตั้งค่าแต่ละอย่างจึงสำคัญ, และครอบคลุมกรณีขอบเช่นรายการว่างหรือการตั้งชื่อแบบกำหนดเอง

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า ติดตั้งแล้ว
- อ้างอิงไปยังแพ็กเกจ NuGet **GroupDocs.Viewer** (หรือที่เทียบเท่า) ที่มี `SmartMarkerProcessor`
- เทมเพลตเวิร์กบุ๊ก Excel (`.xlsx`) ที่มีมาร์กเกอร์เช่น `${repeat:Dept}` วางไว้ในแถวที่คุณต้องการทำซ้ำ
- ความคุ้นเคยพื้นฐานกับ C# และ LINQ (ไม่จำเป็นแต่เป็นประโยชน์)

ไม่จำเป็นต้องใช้ไลบรารีของบุคคลที่สามเพิ่มเติม

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ SmartMarkerProcessor

ตัวประมวลผลทำหน้าที่ประสานการแทนที่มาร์กเกอร์และการทำซ้ำแผ่นงาน การสร้างอินสแตนซ์โดยไม่มีอาร์กิวเมนต์จะใช้ตัวเลือกค่าเริ่มต้น

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

การสร้างตัวประมวลผลตั้งแต่ต้นช่วยให้คุณกำหนดค่าตัวเลือกระดับโลกก่อนที่ข้อมูลใด ๆ จะถูกนำไปใช้ นี่คือพื้นฐานสำหรับการทำ **how to repeat worksheet** อย่างถูกต้อง

## ขั้นตอนที่ 2: เปิดใช้งานการทำซ้ำแผ่นงาน

โดยค่าเริ่มต้นตัวประมวลผลจะแทนที่มาร์กเกอร์บนแผ่นงานปัจจุบันเท่านั้น การตั้งค่า `RepeatWorksheet` เป็น `true` จะบอกเอนจินให้คัดลอกแผ่นงานทั้งหมดสำหรับแต่ละรายการในคอลเลกชันข้อมูล

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

การเปิดใช้งานตัวเลือกนี้เป็นกุญแจสำคัญสำหรับ **generate multiple worksheets** — ตัวประมวลผลจะสร้างแท็บใหม่สำหรับทุกองค์ประกอบในอาเรย์ `Dept` และคงรูปแบบเดิมไว้

## ขั้นตอนที่ 3: เตรียมแหล่งข้อมูลเป็นอาเรย์หรือรายการ

SmartMarkerProcessor ทำงานกับ enumerable ใด ๆ ก็ได้, แต่การใช้อาเรย์ทำให้เจตนาชัดเจนเมื่อคุณต้องการ **populate worksheet from list** ที่นี่เราสร้างอ็อบเจ็กต์แบบไม่ระบุชื่อที่มีคุณสมบัติ `Dept` เก็บอาเรย์ของสตริง

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

หากคุณมี `List<string>` อยู่แล้ว คุณสามารถส่งผ่านโดยตรง; ตัวประมวลผลจะจัดการเช่นเดียวกัน ส่วนสำคัญคือชื่อคุณสมบัติ (`Dept`) ต้องตรงกับมาร์กเกอร์ `${repeat:Dept}` ในเทมเพลต

## ขั้นตอนที่ 4: โหลดแผ่นงานเทมเพลต

สมมติว่าคุณมี `ExcelPackage` (จาก EPPlus) หรืออ็อบเจ็กต์ `Workbook`, ดึงแผ่นงานที่ต้องการทำซ้ำ ตัวแปร `ws` แสดงถึงแผ่นงานนั้น

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

หากคุณชอบใช้ไลบรารีอื่น (เช่น ClosedXML) หลักการเดียวกันก็ใช้ได้: รับอ็อบเจ็กต์แผ่นงานที่ทำตามอินเทอร์เฟซที่ต้องการ

## ขั้นตอนที่ 5: ประมวลผลแผ่นงานด้วยข้อมูล

ตอนนี้ให้ใช้ข้อมูลกับเทมเพลต ตัวประมวลผลจะคัดลอกแผ่นงานสำหรับแต่ละแผนก, แทนที่มาร์กเกอร์ `${repeat:Dept}` ด้วยชื่อแผนกจริง, และปล่อยส่วนที่เหลือของแผ่นงานไม่ถูกแก้ไข

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

หลังจาก `Process` เสร็จสิ้น, `ws` จะกลายเป็นแผ่นงานแรกจากหลายแผ่นงาน — หนึ่งแผ่นต่อหนึ่งแผนก ชื่อของแผ่นงานต้นฉบับจะคงไว้, ส่วนสำเนาจะได้รับส่วนต่อท้ายเพิ่มขึ้น (เช่น “Sheet1 (1)”, “Sheet1 (2)”). คุณสามารถเปลี่ยนชื่อภายหลังได้หากต้องการรูปแบบการตั้งชื่อแบบกำหนดเอง

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิดเวิร์กบุ๊กที่ได้, คุณควรเห็น:

- **Sheet1** – เทมเพลตต้นฉบับ (มักจะว่างเปล่าหรือใช้เป็นมาสเตอร์)
- **Sheet1 (1)** – เติมข้อมูลด้วย “HR”
- **Sheet1 (2)** – เติมข้อมูลด้วย “IT”
- **Sheet1 (3)** – เติมข้อมูลด้วย “Finance”

แต่ละแผ่นงานมีรูปแบบเดียวกันแต่ชื่อแผนกจะแทนที่ที่ `${repeat:Dept}` ปรากฏ

## การจัดการกรณีขอบ

### อาเรย์ว่างหรือ null

หาก `Dept` เป็น null หรือว่าง, ตัวประมวลผลจะไม่สร้างแผ่นงานเพิ่มเติม เพื่อหลีกเลี่ยงเวิร์กบุ๊กที่ว่างเปล่าโดยสมบูรณ์ คุณสามารถเพิ่มการตรวจสอบได้:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### ชื่อแผ่นงานแบบกำหนดเอง

รูปแบบการตั้งชื่อค่าเริ่มต้นอาจไม่เหมาะกับทุกความต้องการของรายงาน หลังจากประมวลผล, ให้เปลี่ยนชื่อแต่ละแผ่นงานด้วยลูป:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### เติมคอลัมน์เพิ่มเติม

หากคุณต้องการ **populate excel with array** ค่าที่เกินมาร์กเกอร์เดียว, ขยายอ็อบเจ็กต์ข้อมูล:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

จากนั้นปรับมาร์กเกอร์ในเทมเพลตเป็น `${repeat:Dept.Name}` และ `${repeat:Dept.Headcount}` ตัวประมวลผลจะทำซ้ำแถวสำหรับแต่ละแผนกและเติมข้อมูลในทั้งสองคอลัมน์

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นแอปพลิเคชันคอนโซลที่รวมทุกอย่างตั้งแต่การโหลดเทมเพลตจนถึงการบันทึกเวิร์กบุ๊กขั้นสุดท้าย

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**คำอธิบายส่วนสำคัญ**

- **Processor creation** – สร้างเอนจินที่ตีความมาร์กเกอร์
- **RepeatWorksheet option** – เปิดใช้งานฟีเจอร์หลักที่ตอบ *how to repeat worksheet*
- **Data source** – ใช้อาเรย์ (`new[]`) เพื่อสนอง **populate excel with array**
- **Template loading** – แสดงวิธีทั่วไปในการรับอ็อบเจ็กต์แผ่นงาน
- **Processing** – ทำการทำซ้ำและแทรกข้อมูลในหนึ่งคำสั่ง
- **Renaming** – แสดงวิธีเปลี่ยนชื่อ “(1)”, “(2)” ให้เป็นชื่อที่มีความหมาย, เป็นความต้องการทั่วไปหลังจาก **generate multiple worksheets**

การรันโปรแกรมนี้จะสร้าง `Result.xlsx` ที่มีแท็บเฉพาะแผนกสามแท็บ, แต่ละแท็บเติมข้อมูลจากอาเรย์

## ข้อผิดพลาดทั่วไปและเคล็ดลับระดับมืออาชีพ

- **Marker spelling** – มาร์กเกอร์ต้องตรงกับชื่อคุณสมบัติอย่างแม่นยำ (`${repeat:Dept}`). การพิมพ์ผิดจะทำให้การทำซ้ำไม่ทำงาน
- **Worksheet index** – หลังการประมวลผล, แผ่นงานต้นฉบับอยู่ที่ดัชนี 0; แผ่นงานที่สร้างใหม่จะตามลำดับ การอ้างอิงดัชนีผิดอาจทำให้เปลี่ยนชื่อแท็บผิดแผ่น
- **Large data sets** – การสร้างแผ่นงานหลายร้อยแผ่นอาจทำให้ขนาดไฟล์เพิ่มขึ้นอย่างมาก พิจารณาแยกรายงานหรือใช้แผ่นเดียวกับส่วนที่จัดกลุ่ม หากประสิทธิภาพเป็นปัญหา
- **Thread safety** – `SmartMarkerProcessor` ไม่ปลอดภัยต่อการทำงานหลายเธรด สร้างอินสแตนซ์แยกสำหรับแต่ละเธรดหากคุณประมวลผลเวิร์กบุ๊กหลายไฟล์พร้อมกัน

## สรุป

คุณได้เรียนรู้ **how to repeat worksheet** ใน Excel ด้วย SmartMarkerProcessor, วิธี **populate excel with array** ข้อมูล, วิธี **generate multiple worksheets**, และวิธี **populate worksheet from list** อย่างมีประสิทธิภาพ ตัวอย่างเต็มเชื่อมโยงแนวคิดทั้งหมดเข้าด้วยกัน, และขั้นตอนการเปลี่ยนชื่อแบบเลือกใช้ช่วยให้คุณสร้างชื่อแท็บที่สะอาดและเป็นมิตรกับผู้ใช้

ต่อไปคุณอาจสำรวจ:

- การใช้ **populate worksheet from list** กับอ็อบเจ็กต์ซับซ้อน (คอลเลกชันซ้อน)
- การใช้ conditional formatting หลังจากทำซ้ำแผ่นงาน
- การส่งออกเวิร์กบุ๊กที่สร้างเป็น PDF หรือ CSV เพื่อการใช้งานต่อเนื่อง

ปรับโค้ดให้เข้ากับสถานการณ์รายงานของคุณเองได้เลย, และสนุกกับการอัตโนมัติ Excel อย่างมั่นใจ!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณ

- [วิธีทำซ้ำแผ่นงาน – คู่มือฉบับสมบูรณ์สำหรับการทำอัตโนมัติใน Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [สร้างแผ่นงานต่อรายการ – วิธีทำซ้ำแผ่นงานใน C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [วิธีขยายอาเรย์ใน Excel และเติมข้อมูลในเทมเพลต](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}