---
category: general
date: 2026-06-05
description: ใช้สไตล์เซลล์ขณะนำเข้าโดยใช้ Aspose.Cells เรียนรู้วิธีนำเข้า DataTable
  พร้อมการจัดรูปแบบ, สไตล์แถว, และทำให้แผ่นงานเป็นระเบียบเรียบร้อย.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: th
og_description: ใช้สไตล์เซลล์ขณะนำเข้า DataTable ไปยังเวิร์กชีตของ Aspose.Cells คู่มือขั้นตอนโดยละเอียดพร้อมโค้ดเต็มและเคล็ดลับ
og_title: ประยุกต์ใช้สไตล์เซลล์กับ Aspose.Cells – นำเข้า DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: ใช้สไตล์เซลล์กับ Aspose.Cells – นำเข้า DataTable พร้อมการจัดรูปแบบ
url: /th/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ใช้สไตล์เซลล์กับ Aspose.Cells – นำเข้า DataTable พร้อมการจัดรูปแบบ

เคยสงสัยไหมว่า **จะใช้สไตล์เซลล์** อย่างไรเมื่อดึง `DataTable` เข้าไปในแผ่น Excel? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์การรายงานคุณต้องการให้ข้อมูลดูดีตั้งแต่แรก—ไม่ต้องทำการจัดรูปแบบด้วยตนเองภายหลัง ข่าวดีคือ Aspose.Cells ทำให้การ **นำเข้าพร้อมการจัดรูปแบบ** เป็นเรื่องง่าย ทำให้แถวของคุณเป็นสีแดงหรือสีน้ำเงิน, ตัวหนา, หรืออะไรก็ได้ที่คุณต้องการ

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดง **วิธีนำเข้า datatable** ไปยัง worksheet **พร้อมสไตล์เซลล์** ที่ถูกนำไปใช้ เมื่อเสร็จคุณจะมีแอปคอนโซล C# ที่พร้อมรัน สร้าง workbook, ตั้งค่าสไตล์ให้สองคอลัมน์แรก, และบันทึกไฟล์—ทั้งหมดโดยใช้ API `aspose cells import`

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่า Aspose.Cells ในโครงการ .NET  
- สร้าง `DataTable` ตัวอย่างที่จำลองข้อมูลจริง  
- กำหนดอ็อบเจ็กต์ `Style` สำหรับฟอนต์สีแดงและสีน้ำเงิน  
- ใช้ `Worksheet.Cells.ImportDataTable` เพื่อ **นำเข้า worksheet จาก datatable** พร้อมการใช้สไตล์  
- ตรวจสอบผลลัพธ์และบันทึก workbook  

ไม่มีเครื่องมือภายนอก เพียงแค่ C# และ Aspose.Cells เท่านั้น เริ่มกันเลย

---

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึกในโค้ด ตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 หรือใหม่กว่า | Aspose.Cells 23.x รองรับ .NET Standard 2.0+ ดังนั้น .NET 6 จะให้คุณใช้คุณสมบัติของ runtime ล่าสุด |
| Aspose.Cells สำหรับ .NET (NuGet) | ไลบรารีนี้ให้เมธอด `Workbook`, `Worksheet`, `Style` และ `ImportDataTable` ที่เราต้องการ |
| ความรู้พื้นฐาน C# | คุณจะเข้าใจคลาส, อาเรย์, และคำสั่ง `using` |
| IDE (Visual Studio, VS Code, Rider) | โปรแกรมแก้ไขใดก็ได้ทำงานได้ แต่คุณต้องกู้คืนแพ็กเกจ NuGet |

คุณสามารถติดตั้งแพ็กเกจจากบรรทัดคำสั่ง:

```bash
dotnet add package Aspose.Cells
```

---

## ขั้นตอนที่ 1: สร้าง Workbook ใหม่และเข้าถึง Worksheet แรก

เริ่มต้นกันเลย—ให้สร้าง `Workbook` แล้วดึงแผ่นแรกออกมา คิดว่า workbook คือสมุดโน้ตเปล่า; worksheet แรกคือหน้าที่เราจะเขียน

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **เคล็ดลับ:** หากต้องการหลายแผ่น เพียงเพิ่มด้วย `wb.Worksheets.Add()` และอ้างอิงโดยชื่อหรือดัชนี

---

## ขั้นตอนที่ 2: เตรียม DataTable ตัวอย่าง (วิธีนำเข้า DataTable)

ตอนนี้เราต้องมีข้อมูลที่จะนำเข้า ในโครงการจริงคุณอาจเรียกฐานข้อมูล แต่เพื่อความชัดเจนเราจะสร้าง `DataTable` ในหน่วยความจำ

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **ทำไมเรื่องนี้สำคัญ:** การมี `DataTable` ทำให้เราทดสอบ **aspose cells import** ได้โดยไม่ต้องพึ่งพาแหล่งข้อมูลภายนอก

---

## ขั้นตอนที่ 3: กำหนดสไตล์ที่จะใช้กับเซลล์ที่นำเข้า

นี่คือจุดที่เวทมนต์เกิดขึ้น เราจะสร้างอ็อบเจ็กต์ `Style` สองตัว: ตัวหนึ่งใช้ฟอนต์สีแดง, อีกตัวใช้ฟอนต์สีน้ำเงิน สไตล์เหล่านี้จะถูกนำไปใช้ตามคอลัมน์ระหว่างการนำเข้า

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **ระวัง:** ความยาวของ `importStyles` ต้องตรงกับจำนวนคอลัมน์ที่คุณนำเข้า ไม่เช่นนั้น Aspose จะโยน `ArgumentException`

---

## ขั้นตอนที่ 4: นำเข้า DataTable ไปยัง Worksheet **พร้อมการจัดรูปแบบ**

ตอนนี้เราจะรวมทุกอย่างเข้าด้วยกัน เมธอด overload ของ `ImportDataTable` ที่เราใช้รับอาร์เรย์ `Style[]` ทำให้เราสามารถ **ใช้สไตล์เซลล์** ขณะข้อมูลถูกใส่ลงในแผ่น

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### วิธีการทำงาน

1. **Headers** – เนื่องจากเราผ่านค่า `true` Aspose จะเขียน “Name” และ “Score” ลงในแถวแรก  
2. **Data Rows** – แถวต่อจากนั้นจะได้รับสไตล์ที่สอดคล้องจาก `importStyles`  
3. **Performance** – เมธอดสตรีมข้อมูลโดยตรงเข้าสู่ worksheet ซึ่งเร็วกว่าการวนลูปเซลล์ทีละเซลล์

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และบันทึก Workbook

มาดูเซลล์แรก ๆ เพื่อให้แน่ใจว่าสไตล์ถูกนำไปใช้ แล้วบันทึกไฟล์ลงดิสก์

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

เมื่อคุณเปิด **StyledImport.xlsx** คุณจะเห็น:

- คอลัมน์ “Name” มีข้อความเป็นสี **แดง**  
- คอลัมน์ “Score” มีข้อความเป็นสี **น้ำเงิน**  
- ส่วนหัวของคอลัมน์ใช้สไตล์เริ่มต้น (คุณสามารถตั้งค่าสไตล์ให้หัวได้เช่นกัน แต่เป็นหัวข้อของบทเรียนอื่น)

![ตัวอย่างการใช้สไตล์เซลล์](https://example.com/images/apply-cell-styles.png "การใช้สไตล์เซลล์ใน Aspose.Cells")

> **หมายเหตุ:** ภาพด้านบนแสดงลักษณะสุดท้าย `alt` มีคีย์เวิร์ดหลักเพื่อให้เป็นไปตามข้อกำหนด SEO

---

## คำถามทั่วไปและกรณีขอบ

### What if My DataTable Has More Columns Than Styles?

Aspose จะใช้สไตล์สุดท้ายในอาร์เรย์กับคอลัมน์ที่เหลือ เพื่อหลีกเลี่ยงสีที่ไม่คาดคิด ให้แน่ใจว่าความยาวของอาร์เรย์ตรงกับจำนวนคอลัมน์ หรือส่ง `null` สำหรับคอลัมน์ที่ไม่ต้องการสไตล์

### Can I Apply Different Styles to Specific Rows?

แน่นอน หลังจากนำเข้าแล้ว คุณสามารถวนลูปแถวและกำหนดอ็อบเจ็กต์ `Style` ใหม่ตามเงื่อนไข (เช่น ไฮไลท์คะแนน > 90 เป็นสีเขียว) ตัวอย่างสั้น ๆ มีดังนี้:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Does This Work with Large DataSets?

ใช่ `ImportDataTable` สตรีมข้อมูลอย่างมีประสิทธิภาพ และการใช้สไตล์แบบคงที่เพิ่มภาระเพียงเล็กน้อย สำหรับหลายล้านแถว ควรพิจารณานำเข้าเป็นชิ้นส่วนหรือใช้ `Cells.ImportDataTable` ร่วมกับ `DataReader` เพื่อประหยัดหน่วยความจำมากขึ้น

### How Do I Preserve Existing Formatting in the Worksheet?

หากช่วงเป้าหมายมีการจัดรูปแบบที่คุณต้องการเก็บไว้ ให้ตั้งค่าพารามิเตอร์ `importOptions` ของ overload `ImportDataTable` (`ImportTableOptions`) และปรับ `ImportDataTableOptions.PreserveCellFormatting` พฤติกรรมเริ่มต้นจะเขียนทับสไตล์ด้วยสไตล์ที่คุณส่งเข้าไป

---

## สรุป: สิ่งที่เราบรรลุ

- **ใช้สไตล์เซลล์** ระหว่างการทำ **aspose cells import**  
- แสดง **การนำเข้าพร้อมการจัดรูปแบบ** ด้วยการส่งอาร์เรย์ `Style[]`  
- แสดง **วิธีนำเข้า datatable** ไปยัง worksheet และบันทึกผลลัพธ์  
- ครอบคลุมกรณีขอบเช่นจำนวนสไตล์ไม่ตรงและการตั้งค่าสไตล์ตามเงื่อนไขของแถว  

ทั้งหมดนี้ทำในแอปคอนโซลเดียวที่รวมทุกอย่างไว้—ไม่มีสคริปต์ภายนอก ไม่ต้องจัดการ Excel ด้วยตนเอง ตอนนี้คุณมีพื้นฐานที่มั่นคงสำหรับฟีเจอร์การรายงานหรือการส่งออกข้อมูลที่ต้องการผลลัพธ์ Excel ที่สวยงาม

---

## ขั้นตอนต่อไป

พร้อมจะก้าวต่อหรือยัง? นี่คือไอเดียบางส่วนที่ต่อยอดจากสิ่งที่คุณเรียนรู้:

- **ตั้งค่าสไตล์ให้แถวหัวคอลัมน์** (เช่น ตัวหนา, สีพื้นหลัง)  
- **ใช้ conditional formatting** ผ่าน `Worksheet.Cells[i, j].ConditionalFormattingCollection`  
- **ส่งออกเป็นรูปแบบอื่น** เช่น CSV หรือ PDF ด้วย `wb.Save("file.pdf", SaveFormat.Pdf)`  
- **รวมหลาย DataTable** ลงใน workbook เดียว แต่ละแผ่นบน sheet ของมันเอง โดยใช้วิธีตั้งค่าสไตล์เดียวกัน  

หากเจออุปสรรคใด ๆ แสดงความคิดเห็นหรือดูเอกสารอย่างเป็นทางการของ Aspose เกี่ยวกับ `ImportDataTable` ขอให้เขียนโค้ดอย่างสนุกและเพลิดเพลินกับไฟล์ Excel ที่สไตล์สวยงาม!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีนำเข้า DataTable ไปยัง Excel ด้วย Aspose.Cells สำหรับ .NET (คู่มือขั้นตอน)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [วิธีตั้งค่าสไตล์ฟอนต์ใน Excel ด้วย Aspose.Cells สำหรับ .NET (คู่มือขั้นตอน)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [วิธีใช้เงาข้อความใน Excel ด้วย Aspose.Cells .NET: คู่มือขั้นตอน](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}