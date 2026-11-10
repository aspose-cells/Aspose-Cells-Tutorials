---
category: general
date: 2026-10-26
description: เรียนรู้วิธีใช้ WRAPCOLS ใน C# เพื่อแบ่งช่วงเป็นคอลัมน์, ใช้ WRAPROWS
  สำหรับแถว, และบันทึกเวิร์กบุ๊กเป็นไฟล์ XLSX ด้วยโปรแกรม.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: th
lastmod: 2026-10-26
og_description: วิธีใช้ WRAPCOLS ใน C# เพื่อแยกข้อมูลเป็นคอลัมน์, ใช้ WRAPROWS สำหรับแถว,
  และบันทึกเวิร์กบุ๊กเป็น XLSX. ปฏิบัติตามคู่มือขั้นตอนเต็มรูปแบบ.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: วิธีใช้ WRAPCOLS ใน C# – แบ่งช่วงและบันทึกเป็น XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีใช้ WRAPCOLS ใน C# และบันทึกเวิร์กบุ๊กเป็นไฟล์ XLSX
url: /th/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ WRAPCOLS ใน C# และบันทึกเวิร์กบุ๊กเป็น XLSX

หากคุณต้องการ **วิธีใช้ WRAPCOLS** เพื่อจัดระเบียบข้อมูลในไฟล์ Excel คำแนะนำนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และสามารถรันได้ คุณจะได้เห็น **ตัวอย่าง excel wrapcols**, เรียนรู้วิธี **แยกช่วงเป็นแถว** ด้วย WRAPROWS, และจบด้วย **บันทึกเวิร์กบุ๊กเป็น XLSX**—ทั้งหมดทำโดย **โปรแกรม**  

การทำงานกับ Excel จาก C# มักหมายถึงการสร้างเวิร์กบุ๊ก, ใส่สูตร, และบันทึกไฟล์ลงดิสก์ โค้ดด้านล่างใช้ไลบรารี Aspose.Cells ซึ่งช่วยให้คุณจัดการไฟล์ Excel ได้โดยไม่ต้องติดตั้ง Microsoft Office เมื่อจบบทเรียนนี้คุณจะสามารถ **สร้าง excel workbook programmatically**, แยกข้อมูลทั้งแนวนอนและแนวตั้ง, และสร้างไฟล์ `.xlsx` ที่พร้อมใช้สำหรับการประมวลผลต่อไป

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+ ด้วย)
* การอ้างอิงไปยังแพ็กเกจ **Aspose.Cells** บน NuGet  
  ```bash
  dotnet add package Aspose.Cells
  ```
* ความคุ้นเคยพื้นฐานกับ C# และสูตร Excel

## ขั้นตอนที่ 1: วิธีใช้ WRAPCOLS เพื่อแยกช่วงเป็นคอลัมน์

ฟังก์ชัน **WRAPCOLS** รับช่วงข้อมูลแบบมิติเดียวและกระจายค่าของมันไปยังจำนวนคอลัมน์ที่กำหนด ในตัวอย่างนี้เรามีค่าที่อยู่ใน `A1:A10` และสั่งให้ WRAPCOLS สร้างสามคอลัมน์

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **ผลลัพธ์:** เซลล์ `C1:E4` ตอนนี้มีรายการเดิมสิบรายการจัดเรียงเป็นสามคอลัมน์ (คอลัมน์สุดท้ายเก็บรายการที่เหลือ)

![ภาพหน้าจอแสดงวิธีใช้ WRAPCOLS เพื่อแยกช่วงเป็นคอลัมน์ใน Excel](image-url.png)

## ขั้นตอนที่ 2: แยกช่วงเป็นแถวด้วย WRAPROWS

ในขณะที่ **WRAPCOLS** ทำงานในแนวนอน **WRAPROWS** ทำงานในแนวตรงกันข้าม: กระจายช่วงข้อมูลไปยังจำนวนแถวที่กำหนด เราจะนำค่าจาก `B1:B10` จัดเรียงเป็นสองแถวโดยเริ่มที่ `F1`

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **ผลลัพธ์:** สูตรจะเติมเซลล์ `F1:K2` ด้วยค่าทั้งสิบที่กระจายอยู่บนสองแถว

## ขั้นตอนที่ 3: บันทึกเวิร์กบุ๊กเป็น XLSX

หลังจากใส่สูตรแล้ว ขั้นตอนสุดท้ายคือการบันทึกไฟล์ **save workbook as xlsx** จะเขียนเวิร์กบุ๊กที่อยู่ในหน่วยความจำลงดิสก์ในรูปแบบ OpenXML สมัยใหม่

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### รูปแบบไฟล์ที่บันทึกไว้

เมื่อคุณเปิด `wrapcols_wraprows_output.xlsx` ใน Excel คุณจะเห็น:

| C | D | E |
|---|---|---|
| รายการ 1 | รายการ 4 | รายการ 7 |
| รายการ 2 | รายการ 5 | รายการ 8 |
| รายการ 3 | รายการ 6 | รายการ 9 |
|  |  | รายการ 10 |

และ

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| ค่า 1 | ค่า 3 | ค่า 5 | ค่า 7 | ค่า 9 | |
| ค่า 2 | ค่า 4 | ค่า 6 | ค่า 8 | ค่า 10 | |

สูตรยังคงอยู่ในเซลล์ ดังนั้นการเปลี่ยนแปลงใด ๆ ในช่วงข้อมูลต้นทางในภายหลังจะถูกอัปเดตโดยอัตโนมัติ

## ขั้นตอนที่ 4: การเปลี่ยนแปลงทั่วไปและกรณีขอบ

### การเปลี่ยนจำนวนคอลัมน์หรือแถว

* **คอลัมน์เพิ่ม:** เพิ่มอาร์กิวเมนต์ที่สองของ `WRAPCOLS`  
  ตัวอย่าง: `=WRAPCOLS(A1:A10,5)` จะสร้างห้าคอลัมน์ โดยปล่อยเซลล์ว่างไว้เมื่อข้อมูลหมด
* **จำนวนคอลัมน์แบบไดนามิก:** ใช้การอ้างอิงเซลล์แทนค่าคงที่  
  `=WRAPCOLS(A1:A10, G1)` โดยที่ `G1` มีจำนวนคอลัมน์ที่ต้องการ

### การจัดการเซลล์ที่ว่างหรือไม่เป็นตัวเลข

WRAPCOLS และ WRAPROWS จะละเว้นเซลล์ว่างโดยค่าเริ่มต้น แต่จะคงลำดับของค่าที่ไม่ว่างไว้ หากต้องการคงเซลล์ว่างไว้ ให้ห่อช่วงต้นด้วยฟังก์ชัน `IFERROR` หรือ `TEXT` ก่อนใช้ WRAPCOLS

### การบันทึกเป็นรูปแบบอื่น

แม้ว่าบทเรียนนี้จะเน้น **save workbook as xlsx** แต่ Aspose.Cells รองรับหลายรูปแบบ (`.xls`, `.csv`, `.pdf`, ฯลฯ):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## เคล็ดลับระดับมืออาชีพและข้อควรระวัง

* **เคล็ดลับ:** ตั้งค่า `Workbook.Settings.CalcEngineEnabled = true` หากคุณต้องการประเมินสูตรทันทีหลังบันทึก
* **ระวัง:** ช่วงข้อมูลต้นทางขนาดใหญ่สามารถสร้างพื้นที่ spill ที่ใหญ่มาก ซึ่งอาจส่งผลต่อประสิทธิภาพ ควรจำกัดขนาดช่วงหรือแยกการทำงานเป็นหลายแผ่นงาน
* **ความปลอดภัยของเธรด:** วัตถุ Aspose.Cells **ไม่** ปลอดภัยต่อการทำงานหลายเธรด สร้างอินสแตนซ์ `Workbook` แยกสำหรับแต่ละเธรดหากคุณประมวลผลไฟล์พร้อมกันหลายไฟล์

## สรุป

คุณได้เรียนรู้ **วิธีใช้ WRAPCOLS** เพื่อแยกช่วงแนวตั้งเป็นหลายคอลัมน์, **แยกช่วงเป็นแถว** ด้วย WRAPROWS, และ **บันทึกเวิร์กบุ๊กเป็น XLSX** หลังจากทำการแปลงเหล่านี้แล้ว คุณสามารถ **สร้าง excel workbook programmatically**, ใส่สูตร spill ที่ทรงพลัง, และสร้างไฟล์ Excel ที่พร้อมแชร์โดยไม่ต้องทำด้วยมือ

### ต่อไปคืออะไร?

* สำรวจ **conditional formatting** เพื่อไฮไลท์ข้อมูลที่ spill
* ผสาน **WRAPCOLS** กับ **SORT** หรือ **FILTER** เพื่อสร้างแดชบอร์ดแบบไดนามิก
* ใช้ **charting API** ของ Aspose.Cells เพื่อสร้างกราฟจากข้อมูลที่จัดเรียงใหม่โดยตรงจากโค้ด

ขอให้สนุกกับการเขียนโค้ดและเพลิดเพลินกับการอัตโนมัติการทำงานใน Excel ของคุณ!

## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}