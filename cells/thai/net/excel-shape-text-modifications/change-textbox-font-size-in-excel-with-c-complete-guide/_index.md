---
category: general
date: 2026-05-30
description: เปลี่ยนขนาดฟอนต์ของกล่องข้อความใน Excel ด้วย C#. เรียนรู้วิธีปรับฟอนต์ของกล่องข้อความใน
  Excel อย่างรวดเร็วด้วยโค้ดแบบขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: th
og_description: เปลี่ยนขนาดฟอนต์ของกล่องข้อความใน Excel ด้วย C#. คู่มือนี้แสดงวิธีแก้ไขฟอนต์ของกล่องข้อความใน
  Excel อย่างปลอดภัยและมีประสิทธิภาพ.
og_title: เปลี่ยนขนาดฟอนต์ของกล่องข้อความใน Excel ด้วย C# – บทเรียนเต็ม
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: เปลี่ยนขนาดฟอนต์ของกล่องข้อความใน Excel ด้วย C# – คู่มือฉบับสมบูรณ์
url: /th/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนขนาดฟอนต์ของ Textbox ใน Excel ด้วย C# – คู่มือครบถ้วน

ต้องการ **เปลี่ยนขนาดฟอนต์ของ textbox** ในแผ่นงาน Excel ด้วย C# หรือไม่? คุณมาถูกที่แล้ว ไม่ว่าคุณจะสร้างรายงาน, สร้างแดชบอร์ด, หรือแค่ปรับแต่งเทมเพลต การปรับลักษณะของ textbox สามารถทำให้สเปรดชีตของคุณดูเป็นมืออาชีพมากขึ้น

ในบทเรียนนี้เราจะ **แก้ไขฟอนต์ของ textbox ใน Excel** ไม่เพียงแค่ขนาดเท่านั้น—รวมถึงครอบครัวฟอนต์, ความหนา, และแม้กระทั่งการจัดการหลายรูปทรง ด้วยตอนจบคุณจะได้โค้ดสแนปช็อตที่พร้อมรันซึ่งครอบคลุมทุกขั้นตอน ตั้งแต่การเปิดเวิร์กบุ๊กจนถึงการทำความสะอาดอ็อบเจ็กต์ COM ไม่มีส่วนเกิน เพียงโค้ดที่ใช้งานได้จริงที่คุณสามารถนำไปใส่ในโปรเจกต์ของคุณได้ทันที

## ข้อกำหนดเบื้องต้น — สิ่งที่คุณต้องมี

| ข้อกำหนด | ทำไมจึงสำคัญ |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | ให้คอมไพเลอร์และรันไทม์ของ C# |
| **Microsoft.Office.Interop.Excel** NuGet package | ให้ประเภท COM interop ที่จำเป็นสำหรับการสื่อสารกับ Excel |
| **Excel installed** (any recent version) | ชั้น Interop ทำงานได้เฉพาะเมื่อมีแอป Office ติดตั้งอยู่ |
| **Basic C# knowledge** | คุณจะตามได้ง่าย แต่เราจะอธิบายทุกบรรทัด |

หากขาดสิ่งใดสิ่งหนึ่ง โปรดหยุดและติดตั้งก่อน; ส่วนที่เหลือของคู่มือนี้สมมติว่ามีครบแล้ว

## ขั้นตอน 1: ตั้งค่าโปรเจกต์และนำเข้า Namespaces

เริ่มต้นด้วยการสร้างแอปคอนโซลใหม่ (หรือรวมเข้าในแอปที่มีอยู่) แล้วนำเข้า namespace ของ interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **เคล็ดลับ:** หากคุณกำหนดเป้าหมายเป็น .NET 6+ ให้เพิ่มแพคเกจ `Microsoft.Office.Interop.Excel` ผ่านคำสั่ง `dotnet add package Microsoft.Office.Interop.Excel`. สิ่งนี้ทำให้ alias `Excel` ถูกแก้ไขอย่างถูกต้อง.

## ขั้นตอน 2: เปิดเวิร์กบุ๊กและเลือกแผ่นงานเป้าหมาย

ตอนนี้เราต้องเปิด Excel, เปิดไฟล์, และชี้ไปที่แผ่นงานที่มี textbox การห่อหุ้มโค้ดนี้ในบล็อก `try/finally` จะทำให้แน่ใจว่าอ็อบเจ็กต์ COM จะถูกปล่อยแม้จะเกิดข้อผิดพลาด

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### ทำไมเรื่องนี้ถึงสำคัญ

การเปิดเวิร์กบุ๊กผ่าน COM ทำให้เราได้โมเดลอ็อบเจ็กต์แบบเรียลไทม์—หมายความว่าการเปลี่ยนแปลงใด ๆ จะสะท้อนทันทีในไฟล์ การตั้งค่า `Visible = false` ช่วยเร่งความเร็วและหลีกเลี่ยงการเปิดหน้าต่างระหว่างการทำอัตโนมัติ

## ขั้นตอน 3: ดึง Shape ของ Textbox

Excel ถือว่า textbox เป็นอ็อบเจ็กต์ `Shape` ภายใต้คอลเลกชัน `Shapes` ไม่ได้เป็นคอลเลกชัน `TextBox` แยกต่างหาก นั่นคือเหตุผลที่โค้ดด้านล่างดูแตกต่างจากสแนปช็อตที่คุณอาจเคยเห็นออนไลน์.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **ระวัง:** คอลเลกชัน `Shapes` เริ่มจาก 1 ดังนั้นเราต้องเพิ่ม `+1` ให้กับ `textboxIndex` ที่เริ่มจาก 0 ที่คุณส่งเข้าไป การลืมทำเช่นนี้จะทำให้เกิดข้อผิดพลาด “index out of range” ที่แก้ไขยาก

## ขั้นตอน 4: เปลี่ยนขนาดฟอนต์ของ Textbox (และชื่อฟอนต์)

นี่คือจุดที่เราจะ **เปลี่ยนขนาดฟอนต์ของ textbox**. คุณสมบัติ `TextFrame2` ให้เราเข้าถึงตัวเลือกการจัดรูปแบบข้อความแบบ rich‑text ซึ่งรวมถึง `Font.Name` และ `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### ทำไมเราจึงใช้ `TextFrame2`

`TextFrame2` เป็นโมเดลอ็อบเจ็กต์รุ่นใหม่ที่แนะนำตั้งแต่ Office 2007 รองรับคุณลักษณะการพิมพ์ขั้นสูงและมักจะเสถียรกว่า `TextFrame` รุ่นเก่า การใช้มันทำให้การ **เปลี่ยนขนาดฟอนต์ของ textbox** ของเราทำงานได้บนเวอร์ชัน Excel สมัยใหม่

## ขั้นตอน 5: บันทึก, ทำความสะอาด, และตรวจสอบ

หลังจากปรับฟอนต์แล้ว เราต้องบันทึกการเปลี่ยนแปลงและปล่อยอ้างอิง COM ทุกตัว การละเลยการทำความสะอาดอาจทำให้กระบวนการ Excel ที่ค้างอยู่ในพื้นหลัง

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **เคล็ดลับ:** หากคุณต้องการ **แก้ไขฟอนต์ของ textbox ใน Excel** บนหลายแผ่นงาน ให้ห่อโค้ดภายในในลูปที่วนผ่าน `Workbook.Worksheets`. เพียงจำไว้ว่าให้รีเซ็ต `textboxIndex` สำหรับแต่ละแผ่นงาน.

## การจัดการกรณีขอบเขต — หลาย Textbox และ Shape ที่หายไป

สเปรดชีตในโลกจริงมักมีมากกว่าหนึ่ง textbox ด้านล่างเป็นสองกลยุทธ์ที่คุณสามารถนำไปใช้ได้โดยไม่ต้องเขียนเมธอดใหม่ทั้งหมด

### 1. เปลี่ยน *ทั้งหมด* ของ textbox บนแผ่นงาน

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. ระบุ textbox ด้วย **Name** แทนการใช้ดัชนี

หากคุณตั้งชื่อ textbox ของคุณให้มีความหมาย (เช่น “TitleBox”) คุณสามารถดึงมันโดยตรงได้:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

ทั้งสองวิธีทำให้คุณ **แก้ไขฟอนต์ของ textbox ใน Excel** อย่างแม่นยำ ไม่ว่าตารางงานจะมีโครงสร้างอย่างไร

## ภาพรวมโดยรวม (ตัวเลือก)

หากคุณต้องการภาพสรุปอย่างรวดเร็ว ลองนึกภาพแผนภาพต่อไปนี้:

![ภาพหน้าจอแสดงแผ่นงาน Excel พร้อม textbox ที่ไฮไลท์ – แสดงวิธีเปลี่ยนขนาดฟอนต์ของ textbox](change-textbox-font-size.png)

*ข้อความแทนภาพ:* *เปลี่ยนขนาดฟอนต์ของ textbox ใน Excel – textbox ที่ไฮไลท์พร้อมสำหรับการปรับฟอนต์.*

## ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลและรันได้ทันที (เพียงอัปเดตเส้นทางไฟล์และชื่อแผ่นงาน).



## คุณควรเรียนรู้อะไรต่อไป?

- [การเปลี่ยนขนาดฟอนต์ใน Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [วิธีปรับขนาดฟอนต์ในเซลล์ Excel ด้วย Aspose.Cells .NET | คู่มือครบถ้วน](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [วิธีตั้งค่าแบบอักษรใน Excel ด้วย Aspose.Cells for .NET (คู่มือขั้นตอนต่อขั้นตอน)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}