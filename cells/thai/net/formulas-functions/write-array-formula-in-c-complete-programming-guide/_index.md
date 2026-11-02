---
category: general
date: 2026-07-03
description: เขียนสูตรอาเรย์ใน C# เพื่อสร้างอาเรย์ 2 คอลัมน์, คำนวณเซลล์ Excel และจัดรายการเป็นคอลัมน์.
  ทำตามตัวอย่างขั้นตอนต่อขั้นตอนโดยใช้ Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: th
og_description: เขียนสูตรอาเรย์ใน C# เพื่อสร้างอาเรย์ 2 คอลัมน์ คำนวณเซลล์ Excel และจัดรายการเป็นคอลัมน์
  เรียนรู้กระบวนการทั้งหมดพร้อมโค้ดที่สามารถรันได้.
og_title: เขียนสูตรอาร์เรย์ใน C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: เขียนสูตรอาเรย์ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เขียนสูตรอาเรย์ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยต้อง **เขียนสูตรอาเรย์** ใน C# แต่ไม่แน่ใจว่าจะทำให้ Excel แสดงรายการที่จัดเรียงอย่างสวยงามได้อย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อต้อง *สร้างผลลัพธ์อาเรย์ Excel* โดยไม่เปิด UI ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างสั้น ๆ ที่ครบวงจรซึ่ง **เขียนสูตรอาเรย์**, **คำนวณเซลล์ Excel**, และ **จัดรายการเป็นคอลัมน์** เพื่อ **สร้างอาเรย์ 2‑คอลัมน์** ที่คุณสามารถบันทึกและตรวจสอบได้

เราจะใช้ไลบรารี Aspose.Cells ที่เป็นที่นิยม เพราะมันช่วยให้คุณจัดการ workbook ทั้งหมดด้วยโค้ดเท่านั้น เมื่อจบคุณจะได้สคริปต์ที่พร้อมรัน คำอธิบายของแต่ละบรรทัดอย่างชัดเจน และไอเดียในการขยายรูปแบบนี้ไปยังชุดข้อมูลขนาดใหญ่ ไม่ฟุ่มเฟือย—แค่ส่วนที่ใช้งานได้จริงที่คุณสามารถคัดลอก‑วางได้ทันที

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานบน .NET Core ด้วย)  
* การอ้างอิงถึง **Aspose.Cells** (คุณสามารถดาวน์โหลดจาก NuGet: `Install-Package Aspose.Cells`)  
* โฟลเดอร์ที่คุณสามารถอ่าน/เขียนไฟล์ Excel ได้ – เราจะเรียกมันว่า `YOUR_DIRECTORY` ในตัวอย่าง  

แค่นั้นเอง ไม่ต้องใช้ Excel interop เพิ่มเติม ไม่ต้องใช้ COM เพียว ๆ แค่โค้ดที่จัดการโดย .NET

![Write array formula in C# example](write-array-formula.png "Screenshot showing the generated 2‑column array in Excel – write array formula in C#")

## ขั้นตอนที่ 1: เขียนสูตรอาเรย์ด้วย Aspose.Cells

สิ่งแรกที่เราต้องทำคือ **เขียนสูตรอาเรย์** ลงในเซลล์หนึ่ง ในไวยากรณ์ของ Excel ฟังก์ชัน `WRAPCOLS` จะรับรายการแบนและจัดรูปเป็นเมทริกซ์ นี่คือตัวอย่างการทำแบบโปรแกรมเมติก:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**ทำไมสิ่งนี้ถึงสำคัญ:** คุณสมบัติ `Formula` จะเก็บสตริงสูตร Excel แบบดิบโดยตรง การใช้ `WRAPCOLS` เราบอก Excel ให้รับอาเรย์เชิงเส้น `{1,2,3,4}` แล้วจัดเรียงเป็นรูปแบบ 2‑คอลัมน์ ทำให้ **สร้างอาเรย์ 2‑คอลัมน์** สูตรเองเป็น *สูตรอาเรย์* — คุณจะเห็นวงเล็บปีกกาล้อมรอบตัวเลข

## ขั้นตอนที่ 2: คำนวณเซลล์ Excel เพื่อให้สูตรทำงาน

การเขียนสูตรอย่างเดียวไม่พอ; เราต้อง **คำนวณเซลล์ Excel** เพื่อให้เอนจินประมวลผลสูตร Aspose.Cells จะไม่ทำการคำนวณอัตโนมัติจนกว่าคุณจะสั่ง:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**ทำไมขั้นตอนนี้ถึงสำคัญ:** หากไม่เรียก `Calculate()` เซลล์จะอยู่ในสถานะ “รอคำนวณ” และไฟล์ workbook ที่บันทึกจะมีสูตรดิบอยู่ ไม่ใช่ค่าที่คำนวณแล้ว การคำนวณอย่างชัดเจนทำให้แน่ใจว่าอาเรย์ผลลัพธ์ถูกสร้างขึ้นในไฟล์

## ขั้นตอนที่ 3: จัดรายการเป็นคอลัมน์ – ดูผลลัพธ์

ตอนนี้ worksheet มีบล็อก 2‑คอลัมน์เริ่มต้นที่ `A1` หากคุณเปิดไฟล์จะเห็น:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

นี่คือการแสดงผลของ **จัดรายการเป็นคอลัมน์** ด้วยฟังก์ชัน `WRAPCOLS` หากคุณต้องการจำนวนคอลัมน์อื่น เพียงเปลี่ยนอาร์กิวเมนต์ที่สอง:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

ผลลัพธ์อาเรย์จะเป็น:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**เคล็ดลับ:** เมื่อต้องจัดการกับชุดข้อมูลขนาดใหญ่ ให้สร้างสตริงรายการแบบไดนามิก (เช่น `string.Join(",", myNumbers)`) เพื่อหลีกเลี่ยงการเขียนค่าคงที่ลงในโค้ด

## ขั้นตอนที่ 4: บันทึก workbook และตรวจสอบผลลัพธ์

สุดท้าย เราจะบันทึก workbook ลงดิสก์เพื่อให้คุณเปิดใน Excel และยืนยันการทำงานของ **generate excel array**:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

เปิด `output.xlsx` แล้วคุณจะเห็นอาเรย์ 2‑คอลัมน์ตรงตามที่อธิบายไว้ หากคุณเปลี่ยนสูตรและคำนวณใหม่ ไฟล์ที่บันทึกจะอัปเดตโดยอัตโนมัติ—ไม่ต้องรีเฟรชด้วยมือ

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถวางลงในแอปพลิเคชันคอนโซล:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เมื่อคุณเปิด `output.xlsx` เซลล์ `A1:B2` จะมีตัวเลข 1‑4 จัดเรียงเป็นสองคอลัมน์ คอนโซลจะแสดงข้อความยืนยันที่เป็นมิตร

## กรณีขอบและคำถามที่พบบ่อย

### ถ้าฉันต้องการช่วงแบบไดนามิกแทนรายการที่กำหนดล่วงหน้า?

คุณสามารถสร้างส่วนของรายการในสูตรได้ขณะรัน:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

สูตรนี้ยังคง **generate excel array** แต่ข้อมูลต้นทางมาจากตรรกะของแอปพลิเคชันของคุณ

### `WRAPCOLS` ทำงานบน Excel เวอร์ชันเก่าหรือไม่?

`WRAPCOLS` มีตั้งแต่ Excel 365/2019 หากคุณต้องรองรับเวอร์ชันเก่า จะต้องจำลองพฤติกรรมด้วยสูตร `INDEX` และ `MOD` ซึ่งค่อนข้างซับซ้อน การใช้ Aspose.Cells ทำให้คุณสามารถใช้สูตรสมัยใหม่และยังสร้างไฟล์ที่เข้ากันได้กับผู้ใช้ส่วนใหญ่

### ฉันสามารถเขียนสูตรลงในช่วงหลายเซลล์ได้หรือไม่?

ได้ — กำหนดสูตรเดียวกันให้กับเซลล์ซ้าย‑บนของช่วง แล้วเรียก `Calculate()` บนอ็อบเจกต์ช่วง:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

ผลลัพธ์จะเหมือนเดิม แต่คุณจะมีการควบคุมตำแหน่งที่อาเรย์อยู่มากขึ้น

## พิจารณาด้านประสิทธิภาพ

เมื่อคุณ **calculate excel cell** สำหรับสูตรจำนวนมาก Aspose.Cells สามารถทำการคำนวณแบบแบตช์เพื่อเพิ่มความเร็ว หากคุณสร้างอาเรย์หลายพันรายการ ให้เรียก `workbook.CalculateFormula()` หนึ่งครั้งหลังตั้งสูตรทั้งหมดเสร็จ แทนการเรียก `Calculate()` บนแต่ละเซลล์ วิธีนี้ลดภาระการคำนวณอย่างมาก

## ขั้นตอนต่อไป

ตอนนี้คุณรู้วิธี **เขียนสูตรอาเรย์**, **คำนวณเซลล์ Excel**, และ **จัดรายการเป็นคอลัมน์** เพื่อ **สร้างอาเรย์ 2‑คอลัมน์** แล้ว คุณอาจอยากสำรวจต่อ:

* **Generate Excel array** สำหรับรายงานหลายชีต  
* ใช้สไตล์ (เส้นขอบ, รูปแบบตัวเลข) กับช่วงผลลัพธ์  
* ส่งออก workbook เป็น PDF หรือ CSV เพื่อการประมวลผลต่อเนื่อง  
* ผสานกับกฎการตรวจสอบข้อมูลเพื่อทำให้สเปรดชีตเป็นแบบโต้ตอบ  

แต่ละหัวข้อข้างต้นต่อยอดจากเทคนิคหลักที่เราอธิบายไว้ ทำให้คุณสามารถอัตโนมัติกระบวนการ Excel ที่ซับซ้อนได้ทั้งหมดจาก C#

---

**สรุปสั้น ๆ** คู่มือนี้แสดงวิธี **เขียนสูตรอาเรย์** ใน C# ด้วย Aspose.Cells, บังคับขั้นตอน **calculate excel cell**, และ **จัดรายการเป็นคอลัมน์** เพื่อ **สร้างอาเรย์ 2‑คอลัมน์** ที่คุณสามารถ **generate excel array** ไฟล์ได้ โค้ดพร้อมรัน คำอธิบายครอบคลุมเหตุผลของแต่ละบรรทัด และคุณยังได้รับเคล็ดลับสำหรับการขยายและจัดการกรณีขอบอีกด้วย

ลองทำตาม ปรับจำนวนคอลัมน์ ใส่ข้อมูลของคุณเอง แล้วให้ Excel ทำงานหนักให้คุณเอง โชคดีในการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Create Excel List Objects Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Import Multi Dimensional Array Excel Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}