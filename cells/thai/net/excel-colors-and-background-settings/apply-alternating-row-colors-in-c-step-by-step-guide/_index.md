---
category: general
date: 2026-03-18
description: เรียนรู้วิธีใช้สีแถวสลับในแผ่นงานด้วย C# รวมถึงการตั้งค่าสีพื้นหลังของแถว,
  เพิ่มสีพื้นหลังสีเหลืองอ่อน, และทำให้แถวมีสีสลับกัน.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: th
og_description: ใช้สีแถวสลับใน C# เพื่อเพิ่มความอ่านง่าย คู่มือนี้แสดงวิธีตั้งค่าสีพื้นหลังของแถว
  เพิ่มพื้นหลังสีเหลืองอ่อน และทำสีแถวสลับกัน
og_title: ใช้สีแถวสลับใน C# – คู่มือฉบับเต็ม
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: นำสีแถวสลับไปใช้ใน C# – คู่มือแบบทีละขั้นตอน
url: /th/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การใช้สีแถวสลับใน C# – บทเรียนเต็ม

เคยต้องการ **apply alternating row colors** กับแผ่นงานที่ขับเคลื่อนด้วยข้อมูลแต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว — นักพัฒนาส่วนใหญ่เจออุปสรรคนี้เมื่อลองทำให้ตารางดูเป็นมิตรมากขึ้นครั้งแรก ข่าวดีคือ? เพียงไม่กี่บรรทัดของ C# คุณสามารถ **set row background color**, เติมด้วย **add light yellow background**, และได้กริดที่ดูเรียบหรูซึ่งทำให้การอ่านข้อมูลดีขึ้นทันที

ในบทเรียนนี้ เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การดึง `DataTable` เข้าสู่หน่วยความจำจนถึงการจัดรูปแบบแต่ละแถวด้วยแถบสีเหลือง‑ขาวอ่อน ๆ เมื่อจบคุณจะสามารถ **color rows alternately** ได้อย่างมั่นใจ และคุณยังจะได้เห็นตัวแปรต่าง ๆ ที่เป็นประโยชน์สำหรับกรณีที่ต้องการเฉดสีต่าง ๆ หรือธีมแบบไดนามิก

## สิ่งที่คุณต้องการ

- โครงการ .NET ที่กำหนดเป้าหมายเป็น .NET 6 หรือใหม่กว่า (โค้ดทำงานบน .NET Framework 4.7+ ด้วย)  
- ไลบรารีสเปรดชีตที่รองรับออบเจ็กต์สไตล์ – ตัวอย่างใช้ API `Workbook`/`Worksheet` แบบทั่วไปที่คล้ายกับไลบรารีอย่าง **Aspose.Cells**, **GemBox.Spreadsheet**, หรือ **ClosedXML**  
- แหล่งข้อมูล `DataTable` – อาจมาจากการคิวรีฐานข้อมูล, การนำเข้า CSV, หรือคอลเลกชันในหน่วยความจำใด ๆ  

ไม่มีแพคเกจ NuGet เพิ่มเติมนอกเหนือจากไลบรารีสเปรดชีตเอง หากคุณใช้ Aspose.Cells, namespace คือ `Aspose.Cells`; สำหรับ ClosedXML คือ `ClosedXML.Excel`. เปลี่ยนการเรียก `CreateStyle` และ `ImportDataTable` ตามที่เหมาะสม.

## ขั้นตอนที่ 1: ดึงข้อมูลต้นทางเป็น DataTable

สิ่งแรกที่ต้องทำ—ดึงข้อมูลที่คุณต้องการแสดงออกมา ในแอปพลิเคชันจริง ๆ นี้มักหมายถึงการเชื่อมต่อฐานข้อมูล แต่เพื่อความชัดเจนเราจะสร้างเมธอดช่วยเหลือชื่อ `GetData()` ที่คืนค่า `DataTable` ที่เต็มข้อมูล

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** `DataTable` กำหนดแถวและคอลัมน์ที่จะได้รับการทำสีสลับในภายหลัง หากตารางว่างเปล่า จะไม่มีอะไรให้จัดรูปแบบ ดังนั้นควรตรวจสอบว่า `Rows.Count` > 0 ก่อนดำเนินการต่อ

### เคล็ดลับพิเศษ
หากคุณดึงข้อมูลจาก Entity Framework คุณสามารถใช้ `DataTable.Load(reader)` หลังจากรัน `SqlCommand` วิธีนี้ทำให้โค้ดเป็นระเบียบและหลีกเลี่ยงการกำหนดคอลัมน์ด้วยตนเอง

## ขั้นตอนที่ 2: จัดสรรอาร์เรย์เพื่อเก็บสไตล์สำหรับแต่ละแถว

ต่อไป เราต้องการคอนเทนเนอร์ที่มีจำนวนเท่ากับจำนวนแถว ส่วนใหญ่ของ API สเปรดชีตอนุญาตให้ส่งอาร์เรย์สไตล์ไปยังเมธอดนำเข้า ดังนั้นเราจะสร้าง `Style[]` ที่มีขนาดเท่ากับจำนวนแถว

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** การจัดสรรอาร์เรย์ล่วงหน้าช่วยหลีกเลี่ยงการสร้างออบเจ็กต์สไตล์ใหม่ในแต่ละรอบ ซึ่งสามารถเพิ่มประสิทธิภาพเมื่อจัดการกับแถวหลายพันแถว

## ขั้นตอนที่ 3: ใช้สีแถวสลับ (สีเหลืองอ่อน / สีขาว)

ตอนนี้มาถึงหัวใจของเรื่อง: **apply alternating row colors** เราจะวนลูปแต่ละแถว สร้างอินสแตนซ์สไตล์ใหม่จาก workbook และตั้งค่าพื้นหลังตามดัชนีแถว แถวเลขคู่จะได้สีเติมสีเหลืองอ่อน ส่วนแถวเลขคี่จะคงสีขาว

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### ทำไมวิธีนี้ถึงได้ผล
- **`rowIndex % 2 == 0`** ตรวจสอบว่าแถวเป็นเลขคู่หรือไม่  
- **`Color.LightYellow`** ให้เฉดสีอ่อนที่ไม่รบกวน เหมาะสำหรับตารางข้อมูล  
- **`BackgroundType.Solid`** ทำให้การเติมสีครอบคลุมเซลล์ทั้งหมด ทำให้ได้ผลลัพธ์ **set row background color**

คุณสามารถเปลี่ยน `Color.LightYellow` เป็นเฉดสีอื่น (เช่น `Color.LightCyan`) หากต้องการลุคที่แตกต่าง โลจิกเดียวกันยังทำให้คุณสามารถ **color rows alternately** ตามเกณฑ์อื่น ๆ เช่น ธงสถานะ

## ขั้นตอนที่ 4: นำเข้า DataTable ไปยัง Worksheet พร้อมสไตล์ที่เตรียมไว้

สุดท้าย เราจะผลักทุกอย่างเข้าสู่ worksheet ส่วนใหญ่ของไลบรารีมี overload ของ `ImportDataTable` ที่รับอาร์เรย์สไตล์ ธง `true` บอก API ให้เขียนหัวคอลัมน์ และพิกัด `0, 0` เริ่มที่เซลล์ซ้ายบน

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** Worksheet ตอนนี้แสดงข้อมูลของคุณด้วยรูปแบบ **alternating row shading** ที่เรียบง่าย—สีเหลืองอ่อนบนแถวเลขคู่, สีขาวบนแถวเลขคี่ ผู้ใช้สามารถสแกนกริดได้โดยไม่ต้องกระพริบตาไปมาระหว่างแถว

### ผลลัพธ์ที่คาดหวัง
หากคุณเปิดสเปรดชีตที่ได้ ผลลัพธ์จะเป็นประมาณนี้:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

แถว 1, 3, 5… มี **light yellow background**, ส่วนแถว 2, 4, 6… คงเป็น **white**. แถวหัวตาราง (แถว 0) จะใช้สไตล์เริ่มต้น เว้นแต่คุณจะปรับแต่งแยกต่างหาก

## ตัวแปรเพิ่มเติม & กรณีขอบ

### 1. ใช้พาเลตสีอื่น
หากสีเหลืองอ่อนขัดแย้งกับแบรนด์ของคุณ เพียงเปลี่ยน `Color.LightYellow` เป็น `System.Drawing.Color` อื่น ๆ สำหรับธีมสีฟ้า‑เทา คุณอาจใช้:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. การทำสีแบบไดนามิกตามข้อมูล
บางครั้งคุณอาจต้องการเน้นแถวที่ตรงตามเงื่อนไข (เช่น สต็อกต่ำ) ให้รวมการตรวจสอบโมดูลัสกับการทดสอบแบบกำหนดเอง:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. ใช้สไตล์กับคอลัมน์เฉพาะเท่านั้น
หากคุณต้องการเพียง **set row background color** บนคอลัมน์บางคอลัมน์ ให้สร้างสไตล์แยกสำหรับแต่ละคอลัมน์และกำหนดหลังการนำเข้าโดยใช้ API ช่วงเซลล์ของ worksheet

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. เคล็ดลับประสิทธิภาพสำหรับตารางขนาดใหญ่
เมื่อทำงานกับแถว > 10,000 แถว ควรพิจารณาใช้สไตล์ออบเจ็กต์เดียวสำหรับแต่ละสีแทนการสร้างใหม่ทุกแถว อาร์เรย์จะเก็บอ้างอิงของสไตล์สองแบบที่ใช้ร่วมกัน ซึ่งช่วยลดการใช้หน่วยความจำอย่างมาก

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่ทำงานอิสระซึ่งคุณสามารถวางลงในแอปคอนโซลได้ มันใช้ API `Workbook`/`Worksheet` สมมติ; ให้แทนที่ประเภทด้วยประเภทจากไลบรารีที่คุณเลือกใช้

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** ไฟล์ชื่อ `AlternatingRows.xlsx` ที่แต่ละแถวสลับระหว่างการเติมสีเหลืองอ่อนและสีขาว ทำให้ตารางอ่านง่ายขึ้น

## คำถามที่พบบ่อย

**Q: วิธีนี้ทำงานกับการจัดรูปแบบตามเงื่อนไขแบบ Excel หรือไม่?**  
A: ใช่ หากไลบรารีของคุณรองรับกฎเงื่อนไข คุณสามารถแปลงโลจิกเดียวกันเป็นกฎที่ตรวจสอบ `MOD(ROW(),2)=0` วิธีที่ใช้โค้ดในที่นี้มีความพกพามากกว่าสำหรับไลบรารีที่ไม่มีการจัดรูปแบบตามเงื่อนไขในตัว

**Q: ถ้าฉันต้องการ **color rows alternately** ในตาราง PDF แทนแผ่นงาน Excel จะทำอย่างไร?**  
A: ตัวสร้างตาราง PDF ส่วนใหญ่ (เช่น iTextSharp, PdfSharp) ให้คุณตั้งค่า `BackgroundColor` ต่อแถว การคำนวณโมดูลัสเดียวกันก็ใช้ได้— 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}