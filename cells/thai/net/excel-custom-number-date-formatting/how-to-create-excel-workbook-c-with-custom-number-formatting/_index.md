---
category: general
date: 2026-10-01
description: เรียนรู้วิธีสร้างไฟล์ Excel ด้วย C# และกำหนดรูปแบบตัวเลขแบบกำหนดเอง ตั้งค่าจำนวนทศนิยมของเซลล์
  และบันทึกไฟล์เป็น XLSX ด้วยคู่มือขั้นตอนเต็มรูปแบบ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: th
lastmod: 2026-10-01
og_description: สร้างไฟล์ Excel ด้วย C# พร้อมรูปแบบตัวเลขแบบกำหนดเอง ตั้งค่าจำนวนตำแหน่งทศนิยมของเซลล์
  และบันทึกไฟล์เป็น XLSX ปฏิบัติตามคู่มือฉบับเต็มนี้เพื่อผลลัพธ์ตัวเลขที่แม่นยำ
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: สร้างไฟล์ Excel ด้วย C# – รูปแบบตัวเลขแบบกำหนดเองและการส่งออกเป็น XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: วิธีสร้างไฟล์ Excel ด้วย C# พร้อมการจัดรูปแบบตัวเลขแบบกำหนดเอง
url: /th/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Excel workbook C# พร้อมการจัดรูปแบบตัวเลขแบบกำหนดเอง

หากคุณต้องการ **create excel workbook c#** ที่แสดงตัวเลขตามที่คุณต้องการ คู่มือนี้จะแสดงวิธีทำในไม่กี่ขั้นตอนที่ชัดเจน คุณจะได้เรียนรู้การใช้รูปแบบตัวเลขแบบกำหนดเอง การตั้งค่าตำแหน่งทศนิยมของเซลล์ และสุดท้าย **save workbook as xlsx** เพื่อการใช้งานต่อไป

การทำงานกับข้อมูลเชิงตัวเลขมักต้องสมดุลระหว่างความแม่นยำและความอ่านง่าย เมื่อจบบทเรียนนี้คุณจะมีรูปแบบที่นำกลับมาใช้ใหม่ได้ซึ่งจำกัดจำนวนตัวเลขที่แสดงให้เป็นจำนวนหลักสำคัญที่กำหนดไว้ในขณะที่ยังคงค่าต้นฉบับในไฟล์ไว้ ไม่จำเป็นต้องใช้สคริปต์ภายนอก—เพียง C# และไลบรารี Aspose.Cells

## ข้อกำหนดเบื้องต้น

* .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า ติดตั้งแล้ว  
* Visual Studio 2022 (หรือ IDE ของ C# ใดก็ได้)  
* The **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`) – ไลบรารีนี้ให้คลาส `Workbook`, `Worksheet`, และ `ExportTableOptions` ที่ใช้ในตัวอย่าง  

ข้อกำหนดเหล่านี้เป็นขั้นต่ำ; โค้ดเดียวกันทำงานได้ใน .NET Core, .NET Framework, และแม้กระทั่งใน Azure Functions.

## ขั้นตอนที่ 1: สร้าง Excel workbook C# – เริ่มต้นไฟล์

การดำเนินการแรกคือการสร้างอ็อบเจ็กต์ `Workbook` ใหม่ อ็อบเจ็กต์นี้แทนไฟล์ Excel ทั้งหมดในหน่วยความจำและจะมีแผ่นงานเริ่มต้นโดยอัตโนมัติ

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
การสร้าง workbook ล่วงหน้าจะให้พื้นที่ทำงานที่สะอาดตา แผ่นงานเริ่มต้น (`Worksheets[0]`) พร้อมสำหรับการใส่ข้อมูล ดังนั้นคุณไม่จำเป็นต้องเพิ่มแผ่นใหม่ เว้นแต่กรณีของคุณต้องการหลายแท็บ

## ขั้นตอนที่ 2: เขียนค่าตัวเลขลงในเซลล์

ตอนนี้ใส่ตัวเลขตัวอย่างลงในเซลล์ **A1** ค่าที่เราใช้ (`123.456789`) มีตำแหน่งทศนิยมมากกว่าที่เราต้องการแสดงในที่สุด ซึ่งทำให้เราสามารถสาธิตการปัดเศษในภายหลัง

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**เคล็ดลับ:** `PutValue` ตรวจจับประเภทข้อมูลโดยอัตโนมัติ ดังนั้นคุณไม่จำเป็นต้องแปลงตัวเลขเป็นสตริง

## ขั้นตอนที่ 3: ใช้รูปแบบตัวเลขแบบกำหนดเอง – จำกัดจำนวนทศนิยมที่แสดง

เพื่อควบคุมวิธีที่ Excel แสดงตัวเลข เราจะสร้าง `Style` พร้อม **custom number format** รูปแบบ `"0.######"` บอก Excel ให้แสดงได้สูงสุดหกตำแหน่งทศนิยมแต่ละบรรทัดศูนย์ที่ต่อท้ายจะถูกละเว้น

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**วิธีการทำงาน:**  
สตริงรูปแบบนี้ตามไวยากรณ์ custom‑format ของ Excel `0` บังคับให้แสดงตัวเลข ส่วน `#` จะแสดงตัวเลขเฉพาะเมื่อมีความสำคัญ การรวมกันทำให้ได้การแสดงผลที่ยืดหยุ่นแต่ยังคงรักษาความแม่นยำเดิม

## ขั้นตอนที่ 4: ตั้งค่าตำแหน่งทศนิยมของเซลล์ – ใช้ ExportTableOptions

หากคุณต้องการ **set cell decimal places** สำหรับข้อมูลที่ส่งออก (เช่นเมื่อแปลงเป็น DataTable) Aspose.Cells ให้คุณระบุจำนวน **significant digits** ขั้นตอนนี้ทำให้ CSV หรือ DataTable ที่ส่งออกรักษากฎการปัดเศษเดียวกับที่คุณใช้ใน workbook

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**ทำไมต้องใช้ `SignificantDigits`?**  
ต่างจากการกำหนดจำนวนทศนิยมคงที่, significant digits จะรักษาขนาดของตัวเลขไว้ในขณะที่จำกัดความแม่นยำ ซึ่งมักเป็นสิ่งที่นักวิเคราะห์คาดหวังเมื่อสรุปข้อมูล

## ขั้นตอนที่ 5: ส่งออกข้อมูลแผ่นงานและ **save workbook as xlsx**

สุดท้าย ส่งออกข้อมูล (หากคุณต้องการ DataTable) และบันทึก workbook ลงดิสก์ คำสั่ง `ExportDataTable` จะเคารพ `ExportTableOptions` ที่เราตั้งค่าไว้ และ `workbook.Save` จะเขียนไฟล์ XLSX มาตรฐาน

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อคุณเปิด *SigDigits.xlsx* ใน Excel เซลล์ **A1** จะแสดง `123.5` ค่าตัวเลขพื้นฐานยังคงเป็น `123.456789` แต่ตัวเลขที่แสดงจะปฏิบัติตามกฎ 4‑significant‑digit หากคุณส่งออกแผ่นงานเป็น DataTable ค่าที่อยู่ในตารางก็จะถูกปัดเศษเป็น `123.5` ด้วย

---

## ใช้รูปแบบตัวเลขแบบกำหนดเองกับเซลล์เพิ่มเติม

หากคุณต้องการจัดรูปแบบช่วงแทนเซลล์เดียว ให้ใช้ `Style` object ซ้ำ:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**เคล็ดลับพิเศษ:** การใช้ style object ซ้ำจะลดภาระหน่วยความจำและรับประกันการจัดรูปแบบที่สอดคล้องกันทั่วทั้งแผ่นงาน

## วิธีจัดรูปแบบตัวเลขใน Excel ด้วย C# – ตัวอย่างทั่วไป

| สถานการณ์ | สตริงรูปแบบ | ผลลัพธ์ |
|----------|---------------|--------|
| จำนวนทศนิยมสองตำแหน่งคงที่ | `"0.00"` | `123.46` |
| สกุลเงิน (สหรัฐ) | `"$#,##0.00"` | `$123.46` |
| เปอร์เซ็นต์หนึ่งตำแหน่งทศนิยม | `"0.0%"` | `12,346.0%` |
| รูปแบบวิทยาศาสตร์ | `"0.00E+00"` | `1.23E+02` |

เลือกรูปแบบที่ตรงกับความต้องการรายงานของคุณ รูปแบบทั้งหมดเข้ากันได้กับคุณสมบัติ `Style.Custom` ที่แสดงไว้ก่อนหน้า

## ตั้งค่าตำแหน่งทศนิยมของเซลล์แบบไดนามิกตามอินพุตของผู้ใช้

บางครั้งความแม่นยำที่ต้องการไม่ทราบในช่วงคอมไพล์ คุณสามารถสร้างสตริงรูปแบบในขณะรันไทม์ได้:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**กรณีขอบเขต:** หาก `decimals` เป็นศูนย์ รูปแบบจะเป็น `"0"` (การแสดงเป็นจำนวนเต็ม) ควรตรวจสอบอินพุตของผู้ใช้เสมอเพื่อหลีกเลี่ยงสตริงรูปแบบที่ผิดรูป

## บันทึก workbook เป็น XLSX – แนวทางปฏิบัติที่ดีที่สุด

* **Use absolute paths** เมื่อเขียนไปยังไดเรกทอรีที่รู้จัก (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** `Workbook` หากคุณห่อหุ้มด้วย `using` เพื่อปลดปล่อยทรัพยากรที่ไม่ได้จัดการโดยเร็ว:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Version compatibility:** Aspose.Cells เขียนไฟล์ที่เข้ากันได้กับ Excel 2010‑2023 ดังนั้นผู้ใช้ต่อไปจะไม่พบปัญหารูปแบบ

---

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก วาง และรันได้ทันที รวมถึงคำสั่ง `using` ที่จำเป็นทั้งหมด คำอธิบาย และการจัดการข้อผิดพลาด

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**ขั้นตอนการตรวจสอบ**

1. รันโปรแกรม (`dotnet run`).  
2. เปิด `SigDigits.xlsx`.  
3. ยืนยันว่า **A1** แสดง `123.5`.  
4. หากคุณเปิดไฟล์ XML ของไฟล์ (`.xlsx` เป็นไฟล์ zip) คุณจะเห็นรูปแบบกำหนดเอง `"0.######"` ถูกเก็บในแอตทริบิวต์ `s` ขององค์ประกอบ `<c>`

---

## สรุป

ในบทเรียนนี้คุณได้เรียนรู้วิธี **create excel workbook c#**, **apply custom number format**, **set cell decimal places**, และ **save workbook as xlsx** ด้วย Aspose.Cells โซลูชันนี้แสดงการจัดรูปแบบเชิงภาพใน Excel และการปัดเศษในการส่งออกข้อมูลผ่าน `ExportTableOptions`

จากนี้คุณสามารถ:

* ขยายวิธีการไปยังช่วงหรือ ตารางทั้งหมด  
* รวมหลายสไตล์ (ฟอนต์, เส้นขอบ) กับ `StyleFlag`  
* อัตโนมัติการสร้างรายงานโดยวนลูปผ่านแหล่งข้อมูลและใช้ตรรกะการจัดรูปแบบเดียวกัน  

คุณสามารถทดลองใช้สตริงรูปแบบ จำนวนทศนิยม หรือ ตัวเลือกการส่งออกต่าง ๆ เพื่อให้ตรงกับความต้องการรายงานของคุณได้อย่างอิสระ ขอให้เขียนโค้ดอย่างสนุก!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ

- [สร้าง Excel Workbook C# – ใช้รูปแบบสกุลเงินและนำเข้า DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [สร้าง Excel Workbook C# – คู่มือขั้นตอนโดยละเอียดพร้อมการจัดรูปแบบตามเงื่อนไข](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [สร้าง Excel Workbook C# – เพิ่มคอมเมนต์และบันทึกเป็น XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}