---
category: general
date: 2026-10-10
description: สร้างสมุดงาน Excel ด้วย C# และใช้ฟังก์ชัน WRAPCOLS เพื่อแยกข้อมูลอาเรย์เป็นคอลัมน์
  ทำตามคู่มือขั้นตอนเต็มที่พร้อมโค้ดที่สามารถรันได้
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: th
lastmod: 2026-10-10
og_description: สร้างไฟล์ Excel workbook ด้วย C# และใช้ฟังก์ชัน WRAPCOLS เพื่อแยกข้อมูลอาร์เรย์เป็นคอลัมน์
  คู่มือฉบับนี้แสดงโค้ดเต็มและอธิบายแต่ละขั้นตอน
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: สร้างเวิร์กบุ๊ก Excel และแยกข้อมูลด้วย WRAPCOLS ใน C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีสร้างเวิร์กบุ๊ก Excel และแยกข้อมูลด้วย WRAPCOLS ใน C#
url: /th/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Excel workbook และแยกข้อมูลด้วย WRAPCOLS ใน C#

หากคุณต้องการ **สร้าง Excel workbook** ด้วยโปรแกรมนี้ คู่มือจะแสดงให้คุณเห็นขั้นตอนทั้งหมดและวิธี **แยกข้อมูลอาร์เรย์** ไปยังคอลัมน์ต่าง ๆ ด้วยฟังก์ชัน `WRAPCOLS` คุณจะได้ตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งสร้างไฟล์ `.xlsx` พร้อมข้อมูลที่กระจายไปในสามคอลัมน์

บทเรียนนี้ครอบคลุมทุกสิ่งที่คุณต้องการ: แพ็กเกจ NuGet ที่จำเป็น, โค้ดแต่ละบรรทัด, เหตุผลที่สูตร `WRAPCOLS` ทำงาน, และวิธีปรับโซลูชันสำหรับขนาดอาร์เรย์หรือจำนวนคอลัมน์ที่แตกต่างกัน เมื่อจบแล้วคุณจะสามารถฝังเทคนิค **use wrapcols function** ลงในโปรเจกต์ C# ใด ๆ ที่สร้างไฟล์ Excel ได้

## Prerequisites

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า  
* IDE สำหรับ C# (Visual Studio, VS Code, Rider ฯลฯ)  
* แพ็กเกจ NuGet **Aspose.Cells for .NET** – ไลบรารีที่ให้คลาส `Workbook` ที่ใช้ในตัวอย่าง  

คุณไม่จำเป็นต้องติดตั้ง Office; Aspose.Cells จะเขียนไฟล์ `.xlsx` โดยตรง

## Step 1 – create Excel workbook

งานแรกคือการสร้างอ็อบเจ็กต์ workbook ใหม่และอ้างอิงไปยัง worksheet แรก ขั้นตอนนี้เป็นพื้นฐานสำหรับการจัดการต่อไป

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` แทนไฟล์ทั้งหมด, ส่วน `Worksheet` แทนแผ่นงานเดียว การสร้าง workbook ในหน่วยความจำช่วยหลีกเลี่ยง I/O บนดิสก์จนกว่าจะบันทึกอย่างชัดเจน

## Step 2 – apply WRAPCOLS to split array columns

ต่อไปคุณจะใส่สูตรในเซลล์ **A1** ที่ใช้ `WRAPCOLS` ฟังก์ชันรับอาร์กิวเมนต์สองค่า: อาร์เรย์ต้นทางและจำนวนคอลัมน์ที่ต้องการให้อาร์เรย์ห่อหุ้ม

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**ทำไมจึงทำงานได้:** `WRAPCOLS` รับอาร์เรย์แบน `{1,2,3,4,5,6}` แล้วเติมลงใน worksheet แถวต่อแถว สร้างสามคอลัมน์ต่อแถว อาร์กิวเมนต์แรกสามารถเป็นลิเทรัลอาร์เรย์ของ Excel, ช่วงชื่อ, หรือสูตรอาร์เรย์แบบไดนามิกได้ ส่วนอาร์กิวเมนต์ที่สอง (`3`) บอก Excel ว่าจะสร้างกี่คอลัมน์ก่อนย้ายไปแถวถัดไป

### Using the function with different data types

ฟังก์ชัน `WRAPCOLS` ไม่ได้จำกัดเฉพาะตัวเลข คุณสามารถแยกค่าข้อความ, วันที่, หรือประเภทผสมได้:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

เมื่ออาร์เรย์ต้นทางมีสตริง Excel จะจัดผลลัพธ์เป็นเซลล์ข้อความโดยอัตโนมัติ ความยืดหยุ่นนี้ทำให้คุณ **excel formula split data** สำหรับการรายงาน, แดชบอร์ด, หรืองานย้ายข้อมูลได้ง่ายขึ้น

## Step 3 – calculate formulas so the worksheet is populated

สูตรจะถูกเก็บเป็นสตริงจนกว่าคุณจะสั่งให้ workbook ประเมินค่า การเรียก `CalculateFormula` จะบังคับให้ประเมินและเขียนผลลัพธ์ลงในเซลล์

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

หากไม่เรียกเมธอดนี้ ไฟล์ที่บันทึกจะมีเพียงข้อความสูตรเท่านั้น ไม่ใช่ค่าที่คำนวณ ผลลัพธ์จะถูกประมวลผลทั่วทั้ง workbook ดังนั้นคุณสามารถใส่สูตรเพิ่มเติมที่อื่นและทั้งหมดจะได้รับการคำนวณด้วยการเรียกครั้งเดียว

## Step 4 – save the workbook to see the result

สุดท้ายให้บันทึก workbook ลงดิสก์ เลือกโฟลเดอร์ที่คุณมีสิทธิ์เขียนและตั้งชื่อไฟล์ให้ชัดเจน

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

เมื่อเปิด `output.xlsx` ด้วย Excel (หรือโปรแกรมดูที่รองรับ) คุณจะเห็น:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

หากคุณใช้ตัวอย่างประเภทผสม แถวที่ 3‑4 จะมีข้อความและตัวเลขตามลำดับ

## Advanced variations and edge‑case handling

### Variable column count at runtime

บ่อยครั้งจำนวนคอลัมน์ที่ต้องการขึ้นกับการป้อนข้อมูลของผู้ใช้ คุณสามารถสร้างสตริงสูตรแบบไดนามิกได้:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Large arrays and performance

`WRAPCOLS` รองรับอาร์เรย์หลายพันรายการได้ แต่การประเมินอาร์เรย์ขนาดใหญ่มากในเซลล์เดียวอาจทำให้เวลาในการคำนวณเพิ่มขึ้น หากสังเกตว่าช้า:

* แบ่งอาร์เรย์ต้นทางเป็นชิ้นย่อยแล้วเขียนแต่ละชิ้นลงในเซลล์เริ่มต้นที่ต่างกัน  
* ใช้ `WorkbookSettings` เพื่อเปิดการคำนวณแบบหลายเธรด:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Handling empty cells

หากอาร์เรย์ต้นทางมีสตริงว่าง (`""`) หรือค่า `NULL` `WRAPCOLS` จะใส่เซลล์ว่างไว้ ทำให้คอลัมน์ยังคงรูปแบบเดิม พฤติกรรมนี้มีประโยชน์เมื่อคุณต้องการคอลัมน์สำรองสำหรับการกรอกข้อมูลในภายหลัง

### Using named ranges instead of literals

เพื่อความดูแลรักษาที่ง่ายขึ้น ให้กำหนด named range ที่เก็บข้อมูลต้นทาง แล้วอ้างอิงมัน:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

ตอนนี้สูตรจะอ่านข้อมูลจาก worksheet เอง ทำให้ **how to use wrapcols** สามารถนำไปใช้ในสถานการณ์รายงานแบบไดนามิกได้

## Common pitfalls and pro tips

* **ห้ามละเว้นอาร์กิวเมนต์ที่สอง** `WRAPCOLS(array)` โดยไม่มีจำนวนคอลัมน์จะคืนค่าเป็นคอลัมน์เดียว ซึ่งทำลายจุดประสงค์ของการแยกข้อมูล  
* **หลีกเลี่ยงการผสมมิติของอาร์เรย์** อาร์เรย์ต้นทางต้องเป็นมิติเดียว; การให้อาร์เรย์สองมิติ (เช่น `{ {1,2},{3,4} }`) จะทำให้เกิดข้อผิดพลาด `#VALUE!`  
* **บันทึกหลังจากคำนวณ** หากเรียก `wb.Save` ก่อน `CalculateFormula` ไฟล์จะมีเพียงสูตรเท่านั้น  
* **ตรวจสอบสิทธิ์ไฟล์** เมื่อทำงานในสภาพแวดล้อมที่จำกัด (เช่น ASP.NET) ให้แน่ใจว่าบัญชีผู้ใช้กระบวนการสามารถเขียนไปยังโฟลเดอร์เป้าหมายได้  

## Full working example

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก, วาง, และรันได้ รวมทุกการนำเข้า, การจัดการข้อผิดพลาด, และคอมเมนต์

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

การรันโปรแกรมจะสร้าง `output.xlsx` ที่มีสามพื้นที่แสดง **excel formula split data** ด้วยฟังก์ชัน `WRAPCOLS`

## Conclusion

คุณได้เรียนรู้วิธี **create Excel workbook** ด้วย C# และวิธี **use wrapcols function** เพื่อ **split array columns** อย่างมีประสิทธิภาพ ขั้นตอนหลัก—การสร้าง `Workbook`, ใส่สูตร `WRAPCOLS`, คำนวณ, และบันทึก—เป็นรูปแบบที่นำกลับมาใช้ได้สำหรับงานอัตโนมัติใด ๆ ที่ต้องการกระจายข้อมูลไปยังคอลัมน์

ต่อจากนี้คุณสามารถ:

* ผสาน `WRAPCOLS` กับฟังก์ชันอาร์เรย์ไดนามิกอื่น ๆ เช่น `FILTER` หรือ `SORT`  
* ส่งออกชุดข้อมูลขนาดใหญ่จากฐานข้อมูลและให้ Excel จัดรูปแบบอัตโนมัติ  
* สร้างรายงานที่ผู้ใช้กำหนดจำนวนคอลัมน์ผ่าน UI control

ลองทดลองกับแหล่งอาร์เรย์, จำนวนคอลัมน์, และสูตรเพิ่มเติมเพื่อขยายพื้นฐานนี้ ขอให้สนุกกับการเขียนโค้ด!

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}