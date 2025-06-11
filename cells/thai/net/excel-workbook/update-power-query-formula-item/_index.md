---
"description": "อัปเดตรายการสูตร Power Query ใน Excel ได้อย่างง่ายดายโดยใช้ Aspose.Cells สำหรับ .NET คำแนะนำทีละขั้นตอนเพื่อปรับปรุงกระบวนการจัดการข้อมูลของคุณ"
"linktitle": "อัปเดตรายการสูตร Power Query"
"second_title": "เอกสารอ้างอิง API Aspose.Cells สำหรับ .NET"
"title": "อัปเดตรายการสูตร Power Query"
"url": "/th/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# อัปเดตรายการสูตร Power Query

## การแนะนำ

หากคุณเคยทำงานกับ Excel คุณจะรู้ว่า Excel มีประสิทธิภาพเพียงใด โดยเฉพาะอย่างยิ่งเมื่อคุณเริ่มเรียนรู้ Power Query ซึ่งเป็นเคล็ดลับที่ช่วยให้คุณแปลง ทำความสะอาด และวิเคราะห์ข้อมูลได้อย่างง่ายดาย วิธีหนึ่งที่ชาญฉลาดในการจัดการสูตร Power Query ใน Excel คือการใช้ Aspose.Cells สำหรับ .NET วันนี้ เราจะแนะนำคุณเกี่ยวกับการอัปเดตรายการสูตร Power Query ทีละขั้นตอน ดังนั้น คว้าหมวกแห่งการเขียนโค้ดของคุณแล้วเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มเขียนโค้ด มีบางสิ่งที่คุณจะต้องตั้งค่าไว้:

1. Visual Studio: คุณจะต้องมีสภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เพื่อเขียนและรันโค้ด .NET Visual Studio เป็นตัวเลือกที่เหมาะสมที่สุด
2. ไลบรารี Aspose.Cells: ตรวจสอบว่าคุณมีไลบรารี Aspose.Cells อยู่ในโปรเจ็กต์ของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์](https://releases-aspose.com/cells/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ในขณะที่เราจะเดินผ่านสิ่งนี้ไปด้วยกัน การมีความเข้าใจพื้นฐานเกี่ยวกับ C# บางอย่างก็จะเป็นประโยชน์อย่างแน่นอน โดยเฉพาะอย่างยิ่งเมื่อนำทางผ่านคลาสและวิธีการที่แตกต่างกัน
4. ไฟล์ Excel ตัวอย่าง: คุณจะต้องมีไฟล์ Excel ที่ระบุไว้ในโค้ดตัวอย่าง โปรดตรวจสอบว่าคุณมี:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: ตรวจสอบให้แน่ใจว่าโครงการของคุณกำหนดเป้าหมายไปที่ .NET Framework เวอร์ชันที่เข้ากันได้

ตอนนี้เรามีชุดอุปกรณ์พร้อมแล้ว ก็สามารถเริ่มขั้นตอนสนุก ๆ ได้เลย: การเขียนโค้ด!

## แพ็คเกจนำเข้า

ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็น วิธีดำเนินการมีดังนี้:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

การเพิ่มเนมสเปซเหล่านี้แสดงว่าคุณกำลังแจ้งให้คอมไพเลอร์ทราบว่าคุณต้องการใช้คลาสและเมธอดจากไลบรารี Aspose.Cells ขั้นตอนนี้มีความสำคัญมาก เนื่องจากเป็นการวางรากฐานสำหรับโค้ดที่จะตามมา

มาแยกส่วนโค้ดที่คุณให้มากัน บทช่วยสอนนี้จะอธิบายแต่ละส่วนให้คุณเข้าใจอย่างถ่องแท้ว่าเกิดอะไรขึ้น

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีการทำงาน

ในขั้นตอนนี้ เราจะกำหนดว่าไฟล์ต้นทางและไฟล์เอาท์พุตของเราอยู่ที่ใด ซึ่งจะทำให้ Aspose ทราบว่าจะต้องค้นหาไฟล์ Excel ของคุณที่ใด

```csharp
// ไดเรกทอรีการทำงาน
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊ก

ตอนนี้เรามาโหลดไฟล์ Excel ที่มี Power Query อยู่กัน

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
การ `Workbook` คลาสคือจุดเข้าสู่ไฟล์ Excel ของคุณ โดยการผ่านเส้นทางของไฟล์ต้นฉบับของเรา เราจะสร้างอินสแตนซ์ที่ให้เราจัดการไฟล์นั้นได้ ลองนึกภาพว่าเหมือนกับการเปิดหนังสือ—คุณกำลังเตรียมอ่าน (หรือแก้ไข) เนื้อหาของหนังสือ

## ขั้นตอนที่ 3: เข้าถึง Data Mashup

ต่อไปเราจะเข้าถึงสูตร Power Query ที่เก็บไว้ใน Data Mashup ของเวิร์กบุ๊ก

```csharp
DataMashup mashupData = workbook.DataMashup;
```
การ `DataMashup` คลาสนี้ประกอบด้วยสูตร Power Query ทั้งหมดที่เกี่ยวข้องกับเวิร์กบุ๊กของคุณ นี่คือจุดที่เราจะทำงานหนักๆ เหมือนกับตอนที่คุณเปิดกล่องเครื่องมือเพื่อซ่อมแซม

## ขั้นตอนที่ 4: วนซ้ำสูตร Power Query

ตอนนี้มาถึงส่วนที่เราต้องการดำเนินการซ้ำผ่านสูตร Power Query เพื่อค้นหาสูตรที่เราต้องการอัปเดต

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- เราวนผ่านแต่ละ `PowerQueryFormula` ใน `mashupData`-
- ภายในลูปนั้น เราจะเจาะลึกแต่ละอย่าง `PowerQueryFormulaItem`-
- เราตรวจสอบว่าชื่อรายการตรงกับ "แหล่งที่มา" หรือไม่ หากตรงกัน เราจะอัปเดตค่าเพื่อลิงก์ไปยังไฟล์แหล่งที่มาใหม่ของเรา

คล้ายกับการค้นหาหน้าที่ถูกต้องในคู่มือ จากนั้นทำการอัปเดตตามที่จำเป็น ซึ่งเป็นกระบวนการตรงไปตรงมาและพิถีพิถัน

## ขั้นตอนที่ 5: บันทึกสมุดงานที่อัปเดต

หลังจากทำการอัปเดตแล้วก็ถึงเวลาบันทึกการเปลี่ยนแปลงของเรา

```csharp
// บันทึกสมุดงานเอาท์พุต
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
การ `Save` วิธีการนี้จะเขียนเวิร์กบุ๊กที่อัปเดตไปยังไดเร็กทอรีเอาต์พุตที่ระบุ เหมือนกับการปิดผนึกการแก้ไขของคุณในคู่มือเวอร์ชันใหม่ที่พร้อมให้ผู้อื่นนำไปใช้!

## บทสรุป

ขอแสดงความยินดี! คุณได้อัปเดตรายการสูตร Power Query โดยใช้ Aspose.Cells สำหรับ .NET สำเร็จแล้ว ด้วยวิธีนี้ คุณสามารถทำให้การปรับเปลี่ยนสูตร Power Query ในไฟล์ Excel ของคุณเป็นแบบอัตโนมัติ ช่วยประหยัดเวลาและความพยายามอันมีค่าของคุณ

## คำถามที่พบบ่อย

### Aspose.Cells คืออะไร?
Aspose.Cells เป็นไลบรารีอันทรงพลังสำหรับการจัดการไฟล์ Excel ในแอปพลิเคชัน .NET โดยไม่จำเป็นต้องติดตั้ง Microsoft Excel

### ฉันต้องมี Microsoft Excel จึงจะเรียกใช้ Aspose.Cells ได้หรือไม่
ไม่ Aspose.Cells ช่วยให้คุณสามารถสร้างและแก้ไขไฟล์ Excel ตามโปรแกรมโดยไม่ต้องใช้ Excel บนเซิร์ฟเวอร์หรือเครื่องพัฒนาของคุณ

### ฉันสามารถทำงานกับไฟล์ Excel ประเภทใดได้บ้างโดยใช้ Aspose.Cells?
คุณสามารถทำงานกับ .xlsx, .xls, .xlsm และรูปแบบ Excel อื่นๆ อีกมากมายได้โดยใช้ Aspose.Cells

### มีเวอร์ชันทดลองใช้สำหรับ Aspose.Cells หรือไม่
ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้งานฟรีได้จาก [หน้าการเปิดตัว Aspose Cells](https://releases-aspose.com/).

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้อย่างไร?
คุณสามารถเข้าถึงการสนับสนุนได้ผ่านทาง [ฟอรั่ม Aspose](https://forum.aspose.com/c/cells/9)ซึ่งคุณสามารถถามคำถามและหาคำตอบจากชุมชนและทีมงาน Aspose ได้

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}