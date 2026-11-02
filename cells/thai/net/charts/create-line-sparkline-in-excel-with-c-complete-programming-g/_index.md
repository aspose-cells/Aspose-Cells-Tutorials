---
category: general
date: 2026-06-30
description: สร้างสปาร์คไลน์แบบเส้นใน Excel ด้วย C# อย่างรวดเร็ว เรียนรู้วิธีเพิ่มสปาร์คไลน์,
  สร้างเวิร์กบุ๊ก Excel ด้วย C#, และเพิ่มสปาร์คไลน์ลงในเซลล์ในไม่กี่ขั้นตอน.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: th
og_description: สร้างสปาร์คไลน์แบบเส้นใน Excel ด้วย C#. บทเรียนนี้แสดงวิธีเพิ่มสปาร์คไลน์,
  สร้างเวิร์กบุ๊ก Excel ด้วย C#, และฝังสปาร์คไลน์ลงในเซลล์.
og_title: สร้างสปาร์กไลน์เส้นใน Excel ด้วย C# – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: สร้างสปาร์คไลน์แบบเส้นใน Excel ด้วย C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
url: /th/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง line sparkline ใน Excel ด้วย C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์

เคยสงสัยไหมว่า **จะสร้าง line sparkline** ในไฟล์ Excel ด้วย C# อย่างไร? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักถามว่า “จะเพิ่ม sparkline ลงในรายงานโดยไม่ต้องเปิด Excel ด้วยตนเองได้อย่างไร?” ข่าวดีคือด้วยโค้ดเพียงไม่กี่บรรทัดคุณก็สามารถสร้าง line sparkline ที่เรียบหรูภายใน workbook ได้โดยไม่ต้องมี UI

ในบทเรียนนี้เราจะเดินผ่านทุกอย่างที่คุณต้องรู้: ตั้งแต่พื้นฐาน **create Excel workbook C#**, การใส่ข้อมูล, ไปจนถึงขั้นตอนที่แม่นยำสำหรับ **add line sparkline** และ **add sparkline to cell**. เมื่อจบคุณจะมีไฟล์ *.xlsx* ที่พร้อมใช้งานซึ่งแสดงแนวโน้มการขายรายเดือนในพริบตา ไม่ได้มีเนื้อหาเกินความจำเป็น เพียงโซลูชันที่ทำงานได้จริง

---

## สิ่งที่คุณจะสร้าง

- Workbook Excel ใหม่ชื่อ *KPI_Sparklines.xlsx*  
- Worksheet ชื่อ **KPI** ที่มีตัวเลขการขายตัวอย่าง  
- **line sparkline** ที่วางในเซลล์ **D2** โดยอ้างอิงช่วงข้อมูล **B2:B13**  
- การจัดรูปแบบพื้นฐาน (สี, ความหนาของเส้น) เพื่อทำให้ sparkline โดดเด่น  

ข้อกำหนดเบื้องต้น? เพียง .NET SDK (3.1+ หรือ .NET 6) และไลบรารี Aspose.Cells for .NET ฟรี (สามารถติดตั้งผ่าน NuGet). หากคุณไม่เคยใช้ Aspose.Cells มาก่อน ให้คิดว่าเป็นเอนจิน Excel ที่ทรงพลังซึ่งคุณเรียกใช้จากโค้ด—ไม่มี COM interop, ไม่ต้องติดตั้ง Excel

---

![สร้าง line sparkline ใน Excel ด้วย C#](https://example.com/images/create-line-sparkline.png "สร้าง line sparkline ใน Excel ด้วย C#")

*ข้อความแทนภาพ: ตัวอย่างโค้ดสร้าง line sparkline ใน Excel ด้วย C#*

---

## ขั้นตอนที่ 1: **Create Excel workbook C#** – ตั้งค่าไฟล์และ worksheet

สิ่งแรกที่ต้องทำคือสร้างอ็อบเจ็กต์ workbook และ worksheet ที่จะเก็บข้อมูล นี่คือพื้นฐานของการทำอัตโนมัติใน Excel ไม่ว่าคุณจะ **add line sparkline** หรือเขียนสูตรต่อไป

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **ทำไมจึงสำคัญ:** คลาส `Workbook` แทนไฟล์ทั้งหมด, ส่วน `Worksheet` คือผืนผ้าใบสำหรับแถว, คอลัมน์, และในที่สุด sparkline ของเรา การตั้งชื่อแผ่นงานตั้งแต่แรกช่วยให้ไฟล์เป็นระเบียบและอธิบายตัวเองได้ดี

---

## ขั้นตอนที่ 2: ใส่ข้อมูล – ช่วงข้อมูลต้นทางสำหรับ sparkline

sparkline ต้องการข้อมูลเพื่อวาดกราฟ เราจะจำลองตัวเลขการขาย 12 เดือน คุณอาจดึงข้อมูลเหล่านี้จากฐานข้อมูล, แต่เพื่อความชัดเจนเราจะสร้างขึ้นแบบไดนามิก

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **เคล็ดลับ:** `PutValue` ตรวจจับประเภทข้อมูลอัตโนมัติ, ดังนั้นคุณไม่ต้องแปลงเป็น `double` หรือ `int`. หากต้องการจัดรูปแบบเซลล์ (สกุลเงิน, คั่นหลักพัน) คุณสามารถใช้อ็อบเจ็กต์ `Style` ต่อไปได้

---

## ขั้นตอนที่ 3: **Create line sparkline** – เพิ่ม sparkline ลงในเซลล์ที่ระบุ

ตอนนี้มาถึงจุดไฮไลท์: **line sparkline**. Aspose.Cells จัดกลุ่ม sparkline, ดังนั้นเราต้องสร้าง `SparklineGroup` ชนิด `Line` ก่อน, แล้วบอกตำแหน่งที่จะแสดงผล

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **วิธีการทำงาน:**  
> - `firstRow/firstColumn` และ `lastRow/lastColumn` กำหนด *เซลล์เป้าหมาย* (ที่ sparkline ปรากฏ)  
> - `firstDataRow/lastDataRow` ชี้ไปยังช่วงข้อมูลต้นทาง  
> เนื่องจากเราใช้ **line sparkline**, ผลลัพธ์จะเป็นเส้นบาง ๆ ที่แสดงแนวโน้มของตัวเลข

### ตัวเลือก: **How to add sparkline** พร้อมการจัดสไตล์แบบกำหนดเอง

หากต้องการให้ sparkline โดดเด่น, ปรับคุณสมบัติบางอย่าง:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **ทำไมต้องสไตล์?** เส้นสีน้ำเงินเข้มบนพื้นหลังสีขาวดูสบายตา, ส่วนมาร์คเกอร์ช่วยบ่งบอกจุดข้อมูลแต่ละจุด—เหมาะสำหรับการนำเสนอ

---

## ขั้นตอนที่ 4: บันทึก workbook – ตรวจสอบผลลัพธ์

เมื่อ sparkline อยู่ในตำแหน่งแล้ว เราต้องเขียนไฟล์ลงดิสก์ เลือกโฟลเดอร์ที่คุณมีสิทธิ์เขียน; ตัวอย่างใช้พาธตัวอย่างที่คุณควรแทนที่

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **การตรวจสอบ:** เปิดไฟล์ที่สร้างขึ้นใน Excel (หรือโปรแกรมดูที่รองรับ .xlsx). คุณควรเห็น **line sparkline** ในเซลล์ **D2** ที่สะท้อนตัวเลขการขายที่เพิ่มขึ้นในคอลัมน์ **B**. การวางเมาส์เหนือ sparkline จะโชว์ tooltip พร้อมค่าต้นทาง

---

## ขั้นตอนที่ 5: ข้อผิดพลาดทั่วไปเมื่อ **add sparkline to cell**

แม้ตัวอย่างจะเรียบง่ายก็อาจทำให้ผู้เริ่มต้นติดขัดได้ นี่คือสิ่งที่ควรระวัง:

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| พิกัดเซลล์ผิด | Sparkline target ใช้ดัชนีคอลัมน์แบบ zero‑based แต่แถวเป็น one‑based | จำไว้ว่า `Cells[row, column]` ทั้ง `row` และ `column` เป็น zero‑based. ใน `SparklineGroup.Add` แถวและคอลัมน์เป็น **1‑based** |
| ไม่แสดงข้อมูล | ช่วงต้นทางว่างหรือมีค่าที่ไม่ใช่ตัวเลข | ตรวจสอบให้แน่ใจว่าช่วง (เช่น `B2:B13`) มีตัวเลข. ใช้ `PutValue` กับประเภทตัวเลข |
| Sparkline หายหลังบันทึก | เวอร์ชันไลบรารีไม่ตรงหรือไม่มีไลเซนส์ | ใช้แพคเกจ Aspose.Cells เวอร์ชันล่าสุดและใส่ไลเซนส์ที่ถูกต้องหากเกินขีดจำกัดการทดลอง |
| การจัดรูปแบบไม่ทำงาน | การเปลี่ยนสไตล์ทำก่อนเพิ่ม sparkline | ตั้งค่าสไตล์ **หลัง** สร้างกลุ่มตามที่แสดงด้านบน |

---

## โค้ดเต็ม – คัดลอกวางพร้อมใช้

ด้านล่างเป็นโปรแกรมที่พร้อมรัน เพียงวางลงในโปรเจกต์คอนโซลใหม่, เพิ่มแพคเกจ Aspose.Cells ผ่าน NuGet, แล้วกด **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เมื่อเปิด *KPI_Sparklines.xlsx*, คอลัมน์ **B** จะมีตัวเลขสิบสองค่า (5,000 → 13,250) และเซลล์ **D2** จะมี line sparkline สีน้ำเงินเข้มที่ค่อย ๆ โค้งขึ้นอย่างราบรื่น. มาร์คเกอร์จะแสดงเป็นจุดสีส้ม‑แดงเล็ก ๆ หากคุณเปิด `ShowMarkers`

---

## ต่อไป? ขยายทักษะ Sparkline ของคุณ

เมื่อคุณเชี่ยวชาญ **create line sparkline** ด้วย Aspose.Cells แล้ว ลองสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

- **Add column sparkline** – เหมาะสำหรับแสดงข้อมูลแบบ stacked  
- **Create multi‑sparkline groups** บนแผ่นเดียวเพื่อเปรียบเทียบข้างกัน  
- **Export to PDF** พร้อมรักษา sparkline (Aspose.Cells รองรับการแปลงเป็น PDF)  
- **Dynamic data sources** – ดึงตัวเลขการขายจริงจากฐานข้อมูล SQL แทนค่าคงที่  

หัวข้อเหล่านี้ทั้งหมดอิงจากแนวคิดหลักเดียวกัน: **create Excel workbook C#**, ใส่ข้อมูล, และ **add sparkline to cell** ในสไตล์ที่ต้องการ

---

### TL;DR

เราได้แสดงวิธี **create line sparkline** ใน workbook Excel ด้วย C#. ขั้นตอน—*สร้าง workbook, เติมข้อมูล, เพิ่ม sparkline, จัดสไตล์, แล้วบันทึก*—ถูกรวมไว้ในโปรแกรมเดียวที่ทำงานได้เอง อย่าลังเลปรับสี, ความหนาเส้น, หรือช่วงข้อมูลให้ตรงกับความต้องการของรายงานของคุณ

มีไอเดียหรือวิธีปรับปรุงเพิ่มเติม? แสดงความคิดเห็นด้านล่าง, แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}