---
category: general
date: 2026-03-27
description: วิธีผูกข้อมูลใน C# ด้วย Aspose.Cells – เรียนรู้การบันทึกเวิร์กบุ๊กเป็น
  XLSX, เพิ่มแผนภูมิ, และส่งออก Excel พร้อมแผนภูมิในไม่กี่นาที
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: th
og_description: วิธีผูกข้อมูลใน C# ด้วย Aspose.Cells คู่มือนี้จะแสดงวิธีบันทึกเวิร์กบุ๊กเป็น
  XLSX เพิ่มแผนภูมิ และส่งออก Excel พร้อมแผนภูมิ
og_title: วิธีผูกข้อมูลใน C# – สร้างสมุดงาน Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: วิธีผูกข้อมูลใน C# – สร้าง Excel Workbook
url: /th/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีผูกข้อมูลใน C# – สร้าง Excel Workbook

เคยสงสัย **วิธีผูกข้อมูล** ไปยังแผนภูมิใน C# โดยไม่ต้องบิดผมจนเสียหัวไหม? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาจำนวนมากมักเจออุปสรรคเมื่อจำเป็นต้องสร้างไฟล์ Excel แบบโปรแกรมที่ดูเหมือนไฟล์ที่พวกเขาสร้างด้วยมือ  

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์พร้อมรันได้ทันที ซึ่งสร้าง Excel workbook, เติมข้อมูลลงไป, ผูกข้อมูลนั้นกับแผนภูมิ Waterfall, และสุดท้ายบันทึกไฟล์เป็น `.xlsx` เมื่อจบคุณจะรู้วิธี **บันทึก workbook เป็น XLSX**, **วิธีเพิ่มแผนภูมิ** ลงใน worksheet, และ **วิธีส่งออก Excel พร้อมแผนภูมิ** สำหรับการรายงานต่อไป

> **Prerequisites** – คุณต้องมี Aspose.Cells for .NET (รุ่นทดลองฟรีก็ใช้ได้) และสภาพแวดล้อมการพัฒนา .NET เช่น Visual Studio 2022 ไม่ต้องใช้แพ็กเกจ NuGet อื่นใด

---

## สิ่งที่คู่มือฉบับนี้ครอบคลุม

- **Create Excel workbook C#** – ตั้งค่า `Workbook` ใหม่และสร้าง worksheet  
- **How to bind data** – แมปชุดตัวเลขและป้ายชื่อหมวดหมู่ไปยังแหล่งข้อมูลของแผนภูมิ  
- **How to add chart** – แทรกแผนภูมิ Waterfall และกำหนดค่าชื่อเรื่อง  
- **Save workbook as XLSX** – บันทึกไฟล์ลงดิสก์เพื่อให้ใครก็เปิดได้ใน Excel  
- **Export Excel with chart** – ผลลัพธ์สุดท้ายคือ workbook ที่ทำงานเต็มรูปแบบและพร้อมแชร์  

หากคุณคุ้นเคยกับไวยากรณ์พื้นฐานของ C# คุณจะพบว่ามันง่ายเหมือนกินขนมเค้ก มาเริ่มกันเลย

---

## ขั้นตอนที่ 1: สร้าง Excel Workbook ใน C#  

อันดับแรกเราต้องมีอ็อบเจกต์ workbook เพื่อทำงาน คิดว่า `Workbook` คลาสเป็นสมุดโน๊ตเปล่าที่คุณจะเติมหน้า (worksheets) และเนื้อหาในภายหลัง

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** หากต้องการหลายแผ่นงาน เพียงเรียก `workbook.Worksheets.Add()` แล้วเก็บอ้างอิงของแต่ละ `Worksheet` ไว้

---

## ขั้นตอนที่ 2: เติมข้อมูลลง Worksheet ด้วยหมวดหมู่และค่า  

ต่อไปเราจะ **สร้างข้อมูลแบบ excel workbook c#** ตัวอย่างใช้สถานการณ์ Waterfall คลาสสิก: เริ่มต้น, รายได้, ค่าใช้จ่าย, กำไร, และสิ้นสุด  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

ทำไมต้องใส่ `0` สำหรับ “Start” และ “Profit”? ในแผนภูมิ Waterfall ศูนย์เหล่านี้ทำหน้าที่เป็น *ตัวเชื่อม* เพื่อให้การไหลของภาพดูถูกต้อง หากข้ามขั้นตอนนี้แผนภูมิจะดูขาดตอน

---

## ขั้นตอนที่ 3: วิธีเพิ่มแผนภูมิ – แทรกแผนภูมิ Waterfall  

เมื่อข้อมูลพร้อมแล้ว ถึงเวลาที่ **วิธีเพิ่มแผนภูมิ** Aspose.Cells ทำให้เรื่องนี้ง่ายเหมือนเรียก `Charts.Add`

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

พิกัด `(7,0,25,10)` กำหนดเซลล์ซ้ายบนและขวาล่างของกรอบแผนภูมิ ปรับค่าเหล่านี้ให้เข้ากับเลย์เอาต์ของคุณ

---

## ขั้นตอนที่ 4: วิธีผูกข้อมูล – เชื่อม Series และ Categories  

นี่คือหัวใจของบทเรียน: **วิธีผูกข้อมูล** ไปยังแผนภูมิ เมธอด `NSeries.Add` รับช่วงค่าตำแหน่ง Y ส่วน `CategoryData` ชี้ไปที่ป้ายชื่อแกน X

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

สังเกตว่าเรากำหนดช่วงเซลล์เดียวกับที่เติมไว้ก่อนหน้า (`A2:A6` สำหรับหมวดหมู่, `B2:B6` สำหรับจำนวน) หากคุณเปลี่ยนโครงสร้างข้อมูล เพียงอัปเดตช่วงเหล่านี้ให้สอดคล้อง

---

## ขั้นตอนที่ 5: บันทึก Workbook เป็น XLSX – เก็บไฟล์  

สุดท้ายเราจะ **บันทึก workbook เป็น XLSX** เมธอด `Save` จะเลือกฟอร์แมตที่ถูกต้องโดยอัตโนมัติตามนามสกุลไฟล์

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

เมื่อคุณเปิด `WaterfallChart.xlsx` ใน Excel คุณจะเห็นแผนภูมิ Waterfall ที่แสดงผลอย่างสวยงามตรงกับข้อมูลที่ใส่ นั่นคือขั้นตอน **export excel with chart** เสร็จสมบูรณ์

---

## ผลลัพธ์ที่คาดหวัง  

- **ไฟล์ Excel:** `WaterfallChart.xlsx` อยู่ในโฟลเดอร์ที่คุณระบุ  
- **โครงสร้าง Worksheet:** คอลัมน์ A เก็บหมวดหมู่, คอลัมน์ B เก็บจำนวน, และแผนภูมิอยู่ด้านล่างตาราง  
- **ลักษณะแผนภูมิ:** แผนภูมิ Waterfall ชื่อ “Quarterly Waterfall” มีห้าคอลัมน์แทน Start, Revenue, Cost, Profit, และ End  

![ตัวอย่างแผนภูมิ waterfall ที่ผูกข้อมูล](waterfall_chart.png "แผนภูมิ Waterfall ที่สร้างโดย Aspose.Cells")

*ข้อความ alt ของรูปภาพรวมคีย์เวิร์ดหลัก ช่วยทั้ง SEO และการอ้างอิงโดย AI*

---

## คำถามทั่วไป & กรณีขอบเขต  

### ถ้าตัวแหล่งข้อมูลของฉันเป็นแบบไดนามิกล่ะ?  
เปลี่ยนแอเรย์คงที่เป็นลูปที่อ่านจากฐานข้อมูลหรือ API เพียงเขียนค่าไปยังช่วงเซลล์เดียวกัน โค้ดผูกข้อมูลก็ไม่ต้องแก้ไข

### ฉันสามารถเปลี่ยนประเภทแผนภูมิได้ไหม?  
ได้เลย แค่สลับ `ChartType.Waterfall` เป็น `ChartType.Column`, `ChartType.Line` เป็นต้น จำไว้ว่าอาจต้องปรับข้อมูล Series หากแผนภูมิใหม่ต้องการการจัดเรียงที่ต่างกัน

### จะตั้งค่าสีของแผนภูมิอย่างไร?  
ใช้ `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (หรือ `System.Drawing.Color` ใดก็ได้) เหมาะเมื่อต้องการให้คอลัมน์ “Profit” โดดเด่น

### ถ้าต้องการส่งออกเป็น PDF แทน XLSX จะทำอย่างไร?  
เรียก `workbook.Save("Report.pdf", SaveFormat.Pdf);` แผนภูมิจะถูกเรนเดอร์ใน PDF โดยอัตโนมัติ

---

## เคล็ดลับสำหรับโค้ดพร้อมใช้งานใน Production  

- **Dispose objects** – ห่อ `Workbook` ด้วย `using` หากใช้ .NET Core เพื่อคืนทรัพยากรทันที  
- **Path handling** – ใช้ `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` เพื่อหลีกเลี่ยงการกำหนดตัวคั่นแบบฮาร์ดโค้ด  
- **Error handling** – ดัก `Exception` รอบ `Save` เพื่อแจ้งปัญหาการอนุญาตหรือพื้นที่ดิสก์ล่วงหน้า  
- **Version check** – Aspose.Cells 23.10+ มีการสนับสนุน Waterfall ที่ดีขึ้น ตรวจสอบให้ใช้เวอร์ชันล่าสุดเพื่อผลลัพธ์ที่ดีที่สุด

---

## สรุป  

ตอนนี้คุณมีตัวอย่างครบวงจรที่แสดง **วิธีผูกข้อมูล** ใน C#, **สร้าง excel workbook c#**, **วิธีเพิ่มแผนภูมิ**, **บันทึก workbook เป็น xlsx**, และ **export excel with chart** โค้ดพร้อมใส่ลงในโปรเจค .NET ใดก็ได้ และแนวคิดนี้สามารถขยายไปยังชุดข้อมูลขนาดใหญ่หรือประเภทแผนภูมิอื่น ๆ ได้

พร้อมก้าวต่อไปหรือยัง? ลองเพิ่ม Series หลายชุด, ทดลองแผนภูมิแบบ stacked, หรืออัตโนมัติการสร้างรายงานรายเดือนที่ส่งอีเมลให้ผู้มีส่วนได้ส่วนเสีย ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณเชี่ยวชาญการอัตโนมัติ Excel ด้วย Aspose.Cells

Happy coding, and may your spreadsheets always render perfectly!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}