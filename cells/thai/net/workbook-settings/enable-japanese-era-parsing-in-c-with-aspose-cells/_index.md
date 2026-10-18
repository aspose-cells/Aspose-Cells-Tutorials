---
category: general
date: 2026-05-30
description: เปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่นใน C# ด้วย Aspose.Cells. เรียนรู้วิธีตั้งค่าภาษา
  (culture) ของเวิร์กบุ๊ก, การแยกวิเคราะห์วันที่ตามยุค, และการจัดการปฏิทินญี่ปุ่นในแผ่นงาน
  Excel.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: th
og_description: เปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่นใน C# ด้วย Aspose.Cells คู่มือนี้แสดงวิธีตั้งค่าภาษาให้กับสมุดงาน,
  เปิดการสนับสนุนยุค, และทำงานกับวันที่ญี่ปุ่น.
og_title: เปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่นใน C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: เปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่นใน C# ด้วย Aspose.Cells
url: /th/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่นใน C# ด้วย Aspose.Cells

เคยต้องการ **enable japanese era parsing** เมื่อต้องสร้างไฟล์ Excel ให้กับลูกค้าชาวญี่ปุ่นหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเมื่อปฏิทินญี่ปุ่นแบบดั้งเดิม (令和, 平成, ฯลฯ) ปรากฏในข้อมูล ข่าวดีคือ Aspose.Cells ทำให้การรับรู้วันที่ตามยุคเหล่านี้และแปลงเป็นค่ากริกอเรียนมาตรฐานเป็นเรื่องง่าย

ในบทเรียนนี้เราจะพาคุณผ่านขั้นตอนที่แม่นยำเพื่อ **enable japanese era parsing** ด้วย Aspose.Cells ตั้งค่าภูมิภาคของเวิร์กบุ๊กเป็นภาษาญี่ปุ่น และแทรกวันที่ในรูปแบบยุคลงในเซลล์ เมื่อเสร็จคุณจะได้โค้ด C# ที่ทำงานได้ซึ่งแยก “令和3年5月1日” ให้เป็นอ็อบเจกต์วันที่ `2021‑05‑01` ที่ถูกต้อง ไม่ต้องอ้างอิงเอกสารภายนอก—แค่คัดลอก วาง แล้วรัน

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core, .NET Framework, และ .NET 5+)
- Aspose.Cells for .NET (แพ็กเกจ NuGet `Aspose.Cells`)
- ความรู้พื้นฐานของ C#—ถ้าคุณสามารถเขียน `Console.WriteLine` ได้ก็พร้อม
- IDE ที่คุณชอบ (Visual Studio, VS Code, Rider…)

> **เคล็ดลับ:** ควรอัปเดตเวอร์ชัน Aspose.Cells ของคุณให้เป็นเวอร์ชันล่าสุด; เวอร์ชัน 24.10+ มีการกำหนดยุคญี่ปุ่นล่าสุด

## ทำไมต้องเปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่น?

ปฏิทินญี่ปุ่นใช้ยุคที่เชื่อมโยงกับการครองราชย์ของจักรพรรดิ สำหรับแอปพลิเคชันสมัยใหม่ส่วนใหญ่คุณจะต้องเก็บวันที่ในรูปแบบกริกอเรียนที่คุ้นเคย แต่ข้อมูลต้นทางอาจยังคงมาในรูป “令和3年5月1日” หากคุณละเลย **enable japanese era parsing** สตริงนั้นจะถูกถือเป็นข้อความธรรมดา ทำให้การคำนวณ การจัดเรียง และการสร้างแผนภูมิเกิดข้อผิดพลาด การเปิดใช้งานการสนับสนุนยุคทำให้ Aspose.Cells แปลงสตริงเหล่านั้นเป็นค่า `DateTime` ที่ถูกต้องโดยอัตโนมัติ ทั้งช่วยให้ผู้ใช้ญี่ปุ่นอ่านง่ายและยังคงความถูกต้องเชิงตัวเลขสำหรับการประมวลผลต่อไป

## ขั้นตอนที่ 1: ตั้งค่าภูมิภาคของ Workbook เป็นภาษาญี่ปุ่น

สิ่งแรกที่คุณต้องทำคือบอก Aspose.Cells ว่าโลเคลเริ่มต้นของเวิร์กบุ๊กคือภาษาญี่ปุ่น (`ja-JP`) เพื่อให้การแยกวิเคราะห์ตามวัฒนธรรม (รวมถึงชื่อยุค) ปฏิบัติตามกฎของญี่ปุ่น

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **ทำไมเรื่องนี้สำคัญ:** อ็อบเจกต์ `CultureInfo` ควบคุมรูปแบบตัวเลข ตัวคั่นวันที่ และที่สำคัญที่สุดสำหรับเรา ระบบปฏิทินที่ใช้เมื่อแยกวิเคราะห์สตริง

## ขั้นตอนที่ 2: เปิดใช้งานการแยกวิเคราะห์ยุคญี่ปุ่น

เมื่อกำหนดภูมิภาคแล้ว คุณต้องสลับสวิตช์ที่บอก Aspose.Cells ให้รับรู้วันที่ตามยุค นี่คือหัวใจของ **enable japanese era parsing**

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **ข้อผิดพลาดทั่วไป:** ลืมตั้งค่าสถานะนี้จะทำให้ “令和3年5月1日” คงเป็นสตริงตามตัวอักษร หากเปิดใช้งาน Aspose.Cells จะแมปยุคไปยังปีกริกอเรียนที่ถูกต้องโดยอัตโนมัติ

## ขั้นตอนที่ 3: แทรกวันที่ในรูปแบบยุคลงในเซลล์

เมื่อเตรียมภูมิภาคและการสนับสนุนยุคเรียบร้อย การแทรกสตริงวันที่ญี่ปุ่นเป็นเรื่องง่าย ไลบรารีจะทำการแยกวิเคราะห์และเก็บค่า `DateTime` ที่แท้จริง

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

- **Cell A1** ในไฟล์ `JapaneseEraDemo.xlsx` ที่สร้างขึ้นจะแสดง **2021‑05‑01** (หรือรูปแบบวันที่ญี่ปุ่นที่แสดงใน Excel หากเปิดด้วยโลเคลญี่ปุ่น)
- ค่าที่เก็บอยู่เป็น `DateTime` แท้จริง ดังนั้นคุณจึงสามารถใช้ในสูตร ตาราง Pivot หรือการคำนวณ C# ต่อได้อย่างปลอดภัย

## ขั้นตอนที่ 4: ตรวจสอบวันที่ที่แยกวิเคราะห์โดยโปรแกรม (ทางเลือก)

หากต้องการยืนยันว่าการแยกวิเคราะห์สำเร็จก่อนบันทึก คุณสามารถอ่านค่ากลับจากเซลล์ได้:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

ขั้นตอนการตรวจสอบเล็ก ๆ นี้มีประโยชน์ในยูนิตเทสหรือเมื่อประมวลผลไฟล์ Excel ที่ผู้ใช้ส่งมา

## กรณีขอบและความแปรผัน

| สถานการณ์ | วิธีทำ |
|----------|------------|
| **หลายยุคในเวิร์กบุ๊กเดียว** | คง `UseJapaneseEra = true`; Aspose.Cells จะรับรู้ทุกยุคที่รองรับ (令和, 平成, 昭和, 大正, 明治) |
| **สตริงกริกอเรียนและยุคผสมกัน** | ตัวแยกวิเคราะห์จะแยกแยะอัตโนมัติ; สตริงกริกอเรียนจะคงอยู่โดยไม่เปลี่ยนแปลง |
| **ความต้องการปฏิทินแบบกำหนดเอง** | คุณยังสามารถตั้งค่า `Workbook.Settings.Calendar` ให้เป็นอินสแตนซ์ `Calendar` เฉพาะได้หากต้องการการควบคุมเพิ่มเติม |
| **เวอร์ชัน .NET เก่า** | โค้ดเดียวกันทำงานบน .NET Framework 4.6+; เพียงตรวจสอบให้แน่ใจว่าคอนสตรัคเตอร์ `System.Globalization.CultureInfo` มีให้ใช้ |

## เคล็ดลับการใช้งานจริงสำหรับโครงการ

- **Cache the CultureInfo** หากคุณสร้างเวิร์กบุ๊กหลายไฟล์ในลูป; การสร้างอ็อบเจกต์ซ้ำ ๆ จะเพิ่มภาระงาน
- **Validate input** ก่อนเรียก `PutValue`; สตริงยุคที่ผิดรูปแบบจะทำให้เกิดข้อยกเว้น
- **Turn off era parsing** (`UseJapaneseEra = false`) เมื่อคุณมั่นใจว่าข้อมูลไม่มีวันที่ตามยุค—จะช่วยเพิ่มประสิทธิภาพเล็กน้อย
- **Use `Workbook.SaveOptions`** เพื่อควบคุมรูปแบบการส่งออก (XLSX, XLS, CSV) พร้อมคงค่าที่แยกวิเคราะห์ไว้

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

รันโปรแกรม เปิดไฟล์ที่สร้างขึ้น แล้วคุณจะเห็น **2021‑05‑01** ในเซลล์ A1—เป็นหลักฐานว่าเราสามารถ **enable japanese era parsing** ได้สำเร็จ

## สรุป

เราได้แสดงวิธี **enable japanese era parsing** ใน C# ด้วย Aspose.Cells ตั้งค่าภูมิภาคของเวิร์กบุ๊ก และแปลงวันที่ตามยุคเช่น “令和3年5月1日” ให้เป็นค่ากริกอเรียนมาตรฐาน ขั้นตอนสั้น กระชับ โค้ดครบถ้วน และผลลัพธ์ทำงานได้อย่างสมบูรณ์ใน Excel

พร้อมรับความท้าทายต่อไปหรือยัง? ลองผสาน **set workbook culture** กับการจัดรูปแบบตัวเลขเป็นเยนญี่ปุ่น, หรือสร้างรายงานหลายชีตที่ผสมวันที่กริกอเรียนและยุค คุณมีพื้นฐานที่พร้อมจัดการกับข้อบกพร่องของปฏิทินญี่ปุ่นในโครงการอัตโนมัติ Excel ด้วย .NET ของคุณแล้ว

---

*หากคู่มือนี้เป็นประโยชน์ต่อคุณ โปรดให้ดาวที่รีโปของ Aspose.Cells บน GitHub หรือแชร์เคล็ดลับของคุณในคอมเมนต์ ขอให้โค้ดดิ้งสนุก!*

## คุณควรเรียนรู้อะไรต่อไป?

- [โหลดเวิร์กบุ๊ก Excel ด้วยวันที่ตามวัฒนธรรมโดยใช้ Aspose.Cells สำหรับ .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [วิธีตั้งค่าภาษาในไฟล์ Excel ด้วย Aspose.Cells .NET สำหรับการสนับสนุนหลายภาษา](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [โหลดเวิร์กบุ๊กวันที่ตามวัฒนธรรม Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}