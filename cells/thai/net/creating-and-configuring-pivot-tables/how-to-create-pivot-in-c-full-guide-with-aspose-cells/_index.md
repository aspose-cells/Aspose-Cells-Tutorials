---
category: general
date: 2026-03-27
description: วิธีสร้าง Pivot ใน C# ด้วย Aspose.Cells – เรียนรู้การเพิ่มข้อมูล, เปิดใช้งานการรีเฟรช,
  และบันทึกเวิร์กบุ๊กเป็นไฟล์ xlsx ในบทเรียนเดียว
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: th
og_description: วิธีสร้าง Pivot ใน C# ด้วย Aspose.Cells คู่มือนี้จะแสดงวิธีเพิ่มข้อมูล
  เปิดใช้งานการรีเฟรช และบันทึกเวิร์กบุ๊กเป็นไฟล์ xlsx.
og_title: วิธีสร้าง Pivot ใน C# – บทเรียน Aspose.Cells อย่างสมบูรณ์
tags:
- Aspose.Cells
- C#
- Excel automation
title: วิธีสร้าง Pivot ใน C# – คู่มือเต็มกับ Aspose.Cells
url: /th/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง Pivot ใน C# – คู่มือ Aspose.Cells ฉบับสมบูรณ์

เคยสงสัย **วิธีสร้าง pivot** ใน C# โดยไม่ต้องต่อสู้กับ COM interop หรือไม่? คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูลหลาย ๆ ครั้ง เราต้องการวิธีที่รวดเร็วในการแปลงตัวเลขยอดขายดิบให้เป็นสรุปที่เป็นระเบียบ และ Aspose.Cells ทำให้เรื่องนี้ง่ายเหมือนเค้ก  

ในบทเรียนนี้เราจะเดินผ่านทุกขั้นตอน: การเพิ่มข้อมูล, การสร้างตาราง pivot, การเปิดใช้งานการรีเฟรชอัตโนมัติ, และสุดท้าย **บันทึก workbook เป็น xlsx** เพื่อให้ผู้ใช้ของคุณเปิดใน Excel ได้ทันที เมื่อเสร็จคุณจะมีไฟล์ `PivotRefresh.xlsx` พร้อมใช้งานและเข้าใจเหตุผลที่แต่ละบรรทัดสำคัญอย่างไร

## ข้อกำหนดเบื้องต้น

- .NET 6+ (หรือ .NET Framework 4.7.2 ขึ้นไป) – รันไทม์รุ่นใหม่ใดก็ได้
- Aspose.Cells for .NET – สามารถดึงจาก NuGet (`Install-Package Aspose.Cells`)
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# – ไม่จำเป็นต้องมีความรู้ลึกเกี่ยวกับ Excel

> **เคล็ดลับ:** หากคุณทำงานบนเครื่องของบริษัท อย่าลืมใส่ลิขสิทธิ์ของ Aspose; ไม่เช่นนั้นไฟล์ที่สร้างจะมีลายน้ำ

## ขั้นตอนที่ 1 – วิธีเพิ่มข้อมูลลงใน Workbook ใหม่

ก่อนที่ pivot จะมีอยู่ ต้องมีตารางแหล่งข้อมูลก่อน เราจะสร้าง workbook ใหม่, ตั้งชื่อ worksheet แรกเป็น *SalesData*, แล้วใส่แถวข้อมูลบางส่วนที่จำลองข้อมูลยอดขายจริง

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**ทำไมต้องทำแบบนี้:**  
- การใช้ `PutValue` จะตั้งค่าชนิดเซลล์โดยอัตโนมัติ ทำให้คุณไม่ต้องกังวลเรื่องความไม่ตรงกันระหว่างสตริงและตัวเลขในภายหลัง  
- การกำหนดหัวข้อในแถว 1 ให้ engine ของ pivot มีสิ่งอ้างอิงเมื่อคุณแมปฟิลด์

## ขั้นตอนที่ 2 – สร้าง Worksheet ที่จะเป็นโฮสต์ของ Pivot Table

Pivot table จะอยู่บนชีตของมันเอง เพื่อให้ข้อมูลแหล่งที่มาสะอาดและรายงานเป็นระเบียบ

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **ถ้าคุณมีชีตอยู่แล้วล่ะ?** เพียงอ้างอิงโดยใช้ดัชนี (`workbook.Worksheets["MySheet"]`) แทนการเพิ่มชีตใหม่

## ขั้นตอนที่ 3 – กำหนดช่วงแหล่งข้อมูล (How to Add Data → Define Range)

Aspose.Cells ต้องการ `CellArea` หรือสตริงช่วงที่ครอบคลุมทั้งหัวข้อและข้อมูล ที่นี่เรากำหนดสูงสุด 100 แถว; ปรับตามต้องการ

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**กรณีขอบ:** หากชุดข้อมูลของคุณเป็นแบบไดนามิก คุณสามารถคำนวณแถวสุดท้ายที่ใช้ได้ด้วย `salesDataSheet.Cells.MaxDataRow` แล้วสร้างช่วงตามนั้น

## ขั้นตอนที่ 4 – วิธีสร้าง Pivot – Insert the Pivot Table

ตอนนี้ถึงส่วนสนุก: เราบอก Aspose.Cells ให้สร้าง pivot ที่เชื่อมโยงกับช่วงที่เราตั้งค่าไว้

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

สังเกตการอ้างอิงแบบสูตร (`=SalesData!A1:D100`) นั่นคือไวยากรณ์เดียวกับที่คุณพิมพ์ใน Excel ทำให้ API ใช้งานง่าย

## ขั้นตอนที่ 5 – ตั้งค่า Row, Column, และ Data Fields (How to Add Data → Fields)

เราจะวาง *Region* บนแถว, *Product* บนคอลัมน์, และรวมผล *Units* กับ *Revenue*

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**ทำไมต้องใช้ดัชนีเหล่านี้?**  
Aspose.Cells เริ่มนับคอลัมน์จาก 0, ดังนั้น `0` หมายถึง *Region* เมธอด `DataFields.Add` ให้คุณตั้งชื่อฟิลด์ใหม่ (เช่น “Sum of Units”) และเลือกประเภทการรวม – `Sum` เป็นตัวเลือกที่ใช้บ่อยที่สุดสำหรับข้อมูลเชิงตัวเลข

## ขั้นตอนที่ 6 – วิธีเปิดใช้งาน Refresh – ทำให้ Pivot อัปเดตอัตโนมัติเมื่อเปิด

หากข้อมูลแหล่งที่มามีการเปลี่ยนแปลงในภายหลัง คุณอาจต้องการให้ pivot แสดงการเปลี่ยนแปลงนั้นโดยอัตโนมัติ นั่นคือจุดที่ `RefreshDataOnOpen` ทำงาน

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **หมายเหตุ:** ธงนี้ทำงานเฉพาะเมื่อ workbook ถูกเปิดใน Excel; มันจะไม่คำนวณใหม่ภายใน Aspose.Cells เว้นแต่คุณจะเรียก `pivotTable.RefreshData()` ด้วยตนเอง

## ขั้นตอนที่ 7 – บันทึก Workbook เป็น XLSX (How to Save Workbook as XLSX)

สุดท้าย เราจะบันทึกไฟล์ลงดิสก์ รูปแบบ `.xlsx` คือไฟล์ Excel แบบ zip‑based สมัยใหม่ที่ทำงานได้ทุกที่

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

เมื่อรันโปรแกรมจะสร้างไฟล์ชื่อ **PivotRefresh.xlsx** ในโฟลเดอร์ที่ทำงาน เปิดไฟล์ใน Excel แล้วคุณจะเห็น pivot ที่จัดเรียงอย่างเป็นระเบียบโดยมีแถว *Region*, คอลัมน์ *Product*, และค่าที่รวมของ *Units* กับ *Revenue* เนื่องจากเราเปิดใช้งาน refresh การแก้ไขใด ๆ ที่คุณทำในชีต *SalesData* จะอัปเดต pivot อัตโนมัติในครั้งต่อไปที่เปิด workbook

### ผลลัพธ์ที่คาดหวัง

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(ตัวเลขอาจแตกต่างตามแถวที่คุณเพิ่ม)*

---

## คำถามที่พบบ่อย & ความแปรผัน

### ถ้าต้องการหลาย Pivot Table จะทำอย่างไร?

คุณสามารถทำซ้ำ **ขั้นตอน 4** ด้วยชื่อและตำแหน่งที่ต่างกัน ทุกการเรียก `PivotTables.Add` จะคืนค่าอินเด็กซ์ใหม่ที่คุณใช้เพื่อดึงอ็อบเจกต์ตาราง

### จะเปลี่ยนการรวมเป็น *Average* แทน *Sum* ได้อย่างไร?

แทนที่ `PivotTableDataAggregationType.Sum` ด้วย `PivotTableDataAggregationType.Average` ในการเรียก `DataFields.Add`

### สามารถจัดรูปแบบ Pivot (ฟอนต์, สี) ได้หรือไม่?

ทำได้ หลังจากสร้าง pivot แล้วคุณสามารถเข้าถึงคุณสมบัติ `Style` หรือใช้การจัดรูปแบบเซลล์กับช่วงที่บรรจุ pivot ตัวอย่างเช่น:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### สามารถเพิ่มแถวเพิ่มเติมหลังจากบันทึก Workbook ได้หรือไม่?

ทำได้เลย โหลดไฟล์ด้วย `new Workbook("PivotRefresh.xlsx")`, เพิ่มแถวในชีต *SalesData*, แล้วเรียก `pivotTable.RefreshData()` ก่อนบันทึกอีกครั้ง

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

บันทึกไฟล์, รันมัน, แล้วเปิด **PivotRefresh.xlsx** ที่สร้างขึ้น – คุณเพิ่งเชี่ยวชาญ **วิธีสร้าง pivot** ใน C# แล้ว

---

## สรุป

เราได้ครอบคลุม **วิธีสร้าง pivot** ตารางโดยโปรแกรม, **วิธีเพิ่มข้อมูล**, **วิธีเปิดใช้งาน refresh**, และสุดท้าย **วิธีบันทึก workbook เป็น xlsx** ด้วย Aspose.Cells โค้ด

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}