---
"description": "เรียนรู้การแทรกแถว DataTable ใน Excel โดยไม่ต้องเลื่อนแถวแรกลงโดยใช้ Aspose.Cells สำหรับ .NET คำแนะนำทีละขั้นตอนเพื่อการทำงานอัตโนมัติที่ง่ายดาย"
"linktitle": "เลื่อนแถวแรกลงเมื่อแทรกแถว DataTable ใน Excel"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "เลื่อนแถวแรกลงเมื่อแทรกแถว DataTable ใน Excel"
"url": "/th/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เลื่อนแถวแรกลงเมื่อแทรกแถว DataTable ใน Excel

## การแนะนำ

คุณเบื่อกับการเลื่อนแถวด้วยตนเองเมื่อแทรกข้อมูลใหม่ลงในสเปรดชีต Excel หรือไม่? ถือว่าคุณโชคดีแล้ว! ในบทความนี้ เราจะเจาะลึกถึงวิธีการทำให้กระบวนการนี้เป็นอัตโนมัติโดยใช้ Aspose.Cells สำหรับ .NET เมื่ออ่านบทช่วยสอนนี้จบ คุณจะไม่เพียงแต่เรียนรู้วิธีการทำงานกับตารางข้อมูลใน Excel เท่านั้น แต่ยังเรียนรู้วิธีปรับแต่งตัวเลือกการนำเข้าให้เหมาะกับความต้องการของคุณมากขึ้นด้วย เชื่อฉันเถอะว่าวิธีนี้จะช่วยประหยัดเวลาและความยุ่งยากให้คุณได้มาก! ดื่มกาแฟสักถ้วยแล้วเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มเขียนโค้ด เรามาตรวจสอบก่อนว่าคุณได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio แล้ว (2017 ขึ้นไปควรทำงานได้ดี)
2. Aspose.Cells สำหรับ .NET: คุณต้องมีไลบรารี Aspose.Cells หากคุณยังไม่ได้ทำ คุณสามารถดาวน์โหลดได้ [ที่นี่](https://releases-aspose.com/cells/net/).
3. ความเข้าใจพื้นฐานเกี่ยวกับ C# และ Excel: ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม C# และการทำงานของ Excel จะช่วยให้คุณทำตามได้อย่างมีประสิทธิภาพมากขึ้น

คุณจะต้องมีไฟล์ตัวอย่าง Excel ไว้ใช้ด้วย ในคู่มือนี้ เราจะใช้ตัวอย่างที่เรียกว่า `sampleImportTableOptionsShiftFirstRowDown.xlsx`คุณสามารถสร้างไฟล์นี้หรือค้นหาเทมเพลตที่เหมาะกับความต้องการของคุณได้

## แพ็คเกจนำเข้า

ก่อนที่เราจะลงมือเขียนโค้ด เราต้องแน่ใจว่าเราได้นำเข้าแพ็คเกจที่จำเป็นแล้ว ในโปรเจ็กต์ C# ของคุณ ให้รวมเนมสเปซต่อไปนี้:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

แพ็คเกจเหล่านี้มีความจำเป็นสำหรับการทำงานกับเวิร์กบุ๊ก เวิร์กชีต และตาราง

## ขั้นตอนที่ 1: ตั้งค่าโครงการของคุณ

### สร้างโครงการ C# ใหม่

เริ่มต้นด้วยการสร้างแอปพลิเคชันคอนโซล C# ใหม่ใน Visual Studio ตั้งชื่อโปรเจ็กต์ของคุณให้เหมาะสม เช่น “ExcelDataImport”

### เพิ่มแพ็กเกจ Aspose.Cells NuGet

หากต้องการเพิ่มแพ็กเกจ Aspose.Cells ให้คลิกขวาที่โปรเจ็กต์ของคุณใน Solution Explorer เลือก Manage NuGet Packages และค้นหา “Aspose.Cells” ติดตั้งแพ็กเกจเพื่อให้แน่ใจว่าคุณสามารถเข้าถึงฟังก์ชันทั้งหมดที่เราต้องการได้

## ขั้นตอนที่ 2: กำหนดตารางข้อมูล

ต่อไปเราจะดำเนินการ `ICellsDataTable` อินเทอร์เฟซเพื่อสร้างคลาสที่จัดเตรียมข้อมูลที่จะนำเข้า นี่คือวิธีที่คุณสามารถจัดโครงสร้าง `CellsDataTable` ระดับ:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... นำไปปฏิบัติกับสมาชิกท่านอื่น ...
}
```

ที่นี่ เรากำลังกำหนดชื่อคอลัมน์และข้อมูลสำหรับแต่ละคอลัมน์ ซึ่งจะช่วยอำนวยความสะดวกให้กับโครงสร้างของตารางที่นำเข้าของเรา

## ขั้นตอนที่ 3: นำสมาชิกอินเทอร์เฟซ ICellsDataTable มาใช้

ภายใน `CellsDataTable` คลาสนี้คุณต้องนำสมาชิกของ `ICellsDataTable` อินเทอร์เฟซ นี่คือการใช้งานที่จำเป็น:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

ส่วนนี้ของคลาสทำหน้าที่จัดการการดึงข้อมูล การกำหนดจำนวนแถวและคอลัมน์ และการจัดการสถานะดัชนีปัจจุบัน

## ขั้นตอนที่ 4: เขียนฟังก์ชันหลัก

ตอนนี้เรามาสร้างกัน `Run` วิธีการในการจัดเตรียมกระบวนการนำเข้าตารางทั้งหมด:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## ขั้นตอนที่ 5: ตั้งค่าตัวเลือกการนำเข้า

เพื่อควบคุมพฤติกรรมการนำเข้า คุณควรสร้างอินสแตนซ์ของ `ImportTableOptions` และตั้งค่าคุณสมบัติให้เหมาะสม โดยเฉพาะอย่างยิ่ง เราต้องการตั้งค่า `ShiftFirstRowDown` ถึง `false`-

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // เราไม่ต้องการเลื่อนแถวแรกลง
```

## ขั้นตอนที่ 6: นำเข้า DataTable

ตอนนี้เราสามารถนำเข้าข้อมูลจากของเรา `CellsDataTable` ลงในแผ่นงาน

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

คำสั่งนี้จะแทรกตารางข้อมูลของคุณโดยตรงโดยเริ่มต้นจากแถวและคอลัมน์ที่ระบุ

## ขั้นตอนที่ 7: บันทึกสมุดงาน

ในที่สุดเราจะบันทึกสมุดงานที่แก้ไขแล้วกลับไปยังไฟล์:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## บทสรุป

และแล้วคุณก็รู้! คุณได้เรียนรู้วิธีการแทรกแถว DataTable ลงในแผ่นงาน Excel โดยไม่ต้องย้ายแถวแรกโดยใช้ Aspose.Cells สำหรับ .NET แล้ว กระบวนการนี้ไม่เพียงแต่ทำให้การจัดการข้อมูลภายใน Excel มีประสิทธิภาพมากขึ้นเท่านั้น แต่ยังช่วยเพิ่มประสิทธิภาพการทำงานของแอปพลิเคชันของคุณด้วยการทำให้กระบวนการที่มักจะยุ่งยากกลายเป็นงานอัตโนมัติ ด้วยความรู้เหล่านี้ในชุดเครื่องมือของคุณ คุณจะสามารถจัดการงานอัตโนมัติของ Excel ได้ดีขึ้น ช่วยให้คุณประหยัดเวลาและความพยายาม

## คำถามที่พบบ่อย

### Aspose.Cells สำหรับ .NET คืออะไร?
Aspose.Cells สำหรับ .NET เป็นไลบรารีการเขียนโปรแกรมที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงไฟล์ Excel ในแอปพลิเคชัน .NET ได้

### ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.Cells หรือไม่?
ใช่ คุณต้องมีใบอนุญาตที่ถูกต้องจึงจะใช้ฟีเจอร์ทั้งหมดได้ อย่างไรก็ตาม มีรุ่นทดลองใช้งานฟรีสำหรับการทดสอบเบื้องต้น

### ฉันสามารถใช้ Aspose.Cells ในแอปพลิเคชั่นเว็บได้หรือไม่
แน่นอน! Aspose.Cells เหมาะอย่างยิ่งสำหรับเดสก์ท็อป เว็บ และแอปพลิเคชันบนคลาวด์ที่พัฒนาใน .NET

### ฉันสามารถสร้างไฟล์ Excel ประเภทใดได้บ้างโดยใช้ Aspose.Cells?
คุณสามารถสร้างไฟล์ Excel ได้หลายรูปแบบ รวมถึง XLSX, XLS, CSV และอื่นๆ อีกมากมาย

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้จากที่ไหน
คุณสามารถสอบถามหรือขอความช่วยเหลือได้ที่ [ฟอรั่ม Aspose](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}