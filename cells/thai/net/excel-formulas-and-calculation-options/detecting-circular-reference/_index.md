---
"description": "ตรวจจับการอ้างอิงแบบวงกลมใน Excel ได้อย่างง่ายดายโดยใช้ Aspose.Cells สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อให้แน่ใจว่าการคำนวณในสเปรดชีตของคุณมีความแม่นยำ"
"linktitle": "การตรวจจับการอ้างอิงแบบวงกลมในโปรแกรม Excel"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การตรวจจับการอ้างอิงแบบวงกลมในโปรแกรม Excel"
"url": "/th/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การตรวจจับการอ้างอิงแบบวงกลมในโปรแกรม Excel

## การแนะนำ
เมื่อต้องทำงานกับไฟล์ Excel ปัญหาที่น่าหงุดหงิดใจที่สุดอย่างหนึ่งที่คุณอาจพบเจอคือการอ้างอิงแบบวงกลม ซึ่งเกิดขึ้นเมื่อสูตรอ้างอิงกลับไปที่เซลล์ของตัวเองโดยตรงหรือโดยอ้อม ทำให้เกิดการวนซ้ำที่อาจทำให้โปรแกรมคำนวณของ Excel สับสนได้ แต่ไม่ต้องกังวล! ด้วย Aspose.Cells สำหรับ .NET คุณสามารถตรวจจับการอ้างอิงแบบวงกลมที่น่ารำคาญเหล่านี้ได้โดยการเขียนโปรแกรม เพื่อให้แน่ใจว่าสเปรดชีตของคุณยังคงใช้งานได้และถูกต้อง ในคู่มือนี้ เราจะแนะนำคุณทีละขั้นตอนเพื่อให้ทุกอย่างง่ายเหมือนปอกกล้วยเข้าปาก
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึกถึงรายละเอียดของการตรวจจับการอ้างอิงแบบวงกลม เรามาตรวจสอบก่อนว่าคุณได้เตรียมทุกสิ่งที่จำเป็นเพื่อเริ่มต้นแล้ว:
1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว นี่จะเป็นสภาพแวดล้อมการพัฒนาของคุณ
2. .NET Framework: ตรวจสอบให้แน่ใจว่าคุณกำลังใช้ .NET Framework เวอร์ชันที่เข้ากันได้ (อย่างน้อย .NET Framework 4.0)
3. ไลบรารี Aspose.Cells: คุณต้องมีไลบรารี Aspose.Cells คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/cells/net/).
4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะเป็นประโยชน์เนื่องจากเราจะเขียนโค้ดในภาษา C#
5. ไฟล์ Excel: เตรียมไฟล์ Excel ที่มีข้อมูลอ้างอิงแบบวงกลมสำหรับการทดสอบ คุณสามารถสร้างไฟล์แบบง่าย ๆ หรือดาวน์โหลดตัวอย่างก็ได้
ตอนนี้เรามีข้อกำหนดเบื้องต้นแล้ว มาไปสู่ส่วนที่สนุกกันเลยดีกว่า!
## แพ็คเกจนำเข้า
ก่อนที่คุณจะเริ่มเขียนโค้ด คุณต้องนำเข้าแพ็คเกจที่จำเป็นก่อน โดยทำดังนี้:
### สร้างโครงการใหม่
- เปิด Visual Studio และสร้างโปรเจ็กต์แอปพลิเคชันคอนโซล C# ใหม่
### เพิ่มการอ้างอิง Aspose.Cells
- คลิกขวาที่โครงการของคุณใน Solution Explorer
- เลือก "จัดการแพ็คเกจ NuGet"
- ค้นหา “Aspose.Cells” และติดตั้งเวอร์ชันล่าสุด
### นำเข้าเนมสเปซที่จำเป็น
ที่ด้านบนของคุณ `Program.cs` ไฟล์นำเข้าเนมสเปซที่จำเป็น:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

ตอนนี้เราได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว มาเจาะลึกโค้ดเพื่อตรวจจับการอ้างอิงแบบวงกลมในไฟล์ Excel กัน
## ขั้นตอนที่ 1: กำหนดไดเรกทอรีอินพุต
ขั้นแรก คุณต้องระบุไดเรกทอรีที่ไฟล์ Excel ของคุณตั้งอยู่ นี่คือที่ที่คุณจะโหลดไฟล์ Excel ของคุณ
```csharp
// ไดเรกทอรีอินพุต
string sourceDir = "Your Document Directory";
```
แทนที่ `"Your Document Directory"` พร้อมเส้นทางจริงไปยังไฟล์ Excel ของคุณ
## ขั้นตอนที่ 2: โหลดเวิร์กบุ๊กด้วย LoadOptions
ขั้นต่อไป คุณจะโหลดเวิร์กบุ๊ก Excel ของคุณ นี่คือจุดที่ความมหัศจรรย์เริ่มต้นขึ้น!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
ที่นี่เราจะสร้างอินสแตนซ์ใหม่ของ `LoadOptions` และโหลดเวิร์กบุ๊กจากเส้นทางที่ระบุ ตรวจสอบให้แน่ใจว่าชื่อไฟล์ Excel ของคุณตรงกัน!
## ขั้นตอนที่ 3: เปิดใช้งานการตั้งค่าการวนซ้ำ
หากต้องการให้มีการอ้างอิงแบบวงกลม คุณจำเป็นต้องเปิดใช้งานการตั้งค่าการวนซ้ำในเวิร์กบุ๊ก
```csharp
objWB.Settings.Iteration = true;
```
นี่จะบอก Aspose.Cells ให้อนุญาตให้มีการอ้างอิงแบบวงกลมระหว่างการคำนวณ
## ขั้นตอนที่ 4: สร้างตัวเลือกการคำนวณและการตรวจสอบแบบวงกลม
ตอนนี้เรามาสร้างตัวเลือกการคำนวณและจอภาพแบบวงกลมแบบกำหนดเองของเรากัน
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
ที่นี่เราจะสร้างอินสแตนซ์ของ `CalculationOptions` และแบบธรรมเนียม `CircularMonitor`จอภาพนี้จะช่วยติดตามการอ้างอิงแบบวงกลมใดๆ ที่พบระหว่างการคำนวณ
## ขั้นตอนที่ 5: คำนวณสูตร
ตอนนี้ถึงเวลาที่จะคำนวณสูตรในสมุดงานของคุณแล้ว
```csharp
objWB.CalculateFormula(copts);
```
บรรทัดนี้จะดำเนินการคำนวณและตรวจสอบการอ้างอิงแบบวงกลม
## ขั้นตอนที่ 6: นับการอ้างอิงแบบวงกลม
หลังจากการคำนวณแล้ว คุณสามารถนับจำนวนการอ้างอิงแบบวงกลมที่พบได้
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
นี่จะแสดงจำนวนการอ้างอิงแบบวงกลมที่ตรวจพบในไฟล์ Excel ของคุณ
## ขั้นตอนที่ 7: แสดงผลลัพธ์
สุดท้ายเรามาแสดงผลลัพธ์และยืนยันว่าวิธีการของเราดำเนินการสำเร็จ
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## ขั้นตอนที่ 8: นำคลาส CircularMonitor มาใช้
เพื่อให้กระบวนการเสร็จสมบูรณ์ คุณจะต้องดำเนินการตาม `CircularMonitor` คลาส คลาสนี้จะสืบทอดมาจาก `AbstractCalculationMonitor` และจัดการการตรวจจับการอ้างอิงแบบวงกลม
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
คลาสนี้จะเก็บรายละเอียดของการอ้างอิงแบบวงกลมแต่ละรายการที่พบ รวมถึงชื่อเวิร์กชีตและดัชนีเซลล์
## บทสรุป
การตรวจจับการอ้างอิงแบบวงกลมใน Excel โดยใช้ Aspose.Cells สำหรับ .NET เป็นกระบวนการที่ตรงไปตรงมาเมื่อคุณแบ่งกระบวนการออกเป็นขั้นตอนที่จัดการได้ เมื่อปฏิบัติตามคำแนะนำนี้ คุณจะสามารถระบุและจัดการการอ้างอิงแบบวงกลมในสเปรดชีตของคุณได้อย่างง่ายดาย ทำให้มั่นใจได้ว่าการคำนวณของคุณแม่นยำและเชื่อถือได้ ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น Aspose.Cells ก็มีเครื่องมืออันทรงพลังที่จะช่วยเสริมความสามารถในการจัดการ Excel ของคุณ 
## คำถามที่พบบ่อย
### การอ้างอิงแบบวงกลมใน Excel คืออะไร?
การอ้างอิงแบบวงกลมจะเกิดขึ้นเมื่อสูตรอ้างอิงกลับไปยังเซลล์ของตัวเอง ทำให้เกิดการวนซ้ำไม่สิ้นสุดในการคำนวณ
### ฉันจะตรวจจับการอ้างอิงแบบวงกลมโดยใช้โปรแกรมได้อย่างไร
คุณสามารถใช้ไลบรารี Aspose.Cells ใน .NET เพื่อตรวจจับการอ้างอิงแบบวงกลมด้วยโปรแกรมโดยการใช้งานมอนิเตอร์การคำนวณแบบกำหนดเอง
### ข้อกำหนดเบื้องต้นสำหรับการใช้ Aspose.Cells มีอะไรบ้าง?
คุณต้องติดตั้ง Visual Studio, .NET Framework และไลบรารี Aspose.Cells
### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?
ใช่ Aspose.Cells มีการทดลองใช้ฟรีซึ่งคุณสามารถใช้เพื่อสำรวจฟีเจอร์ต่างๆ ได้
### ฉันสามารถหาข้อมูลเพิ่มเติมเกี่ยวกับ Aspose.Cells ได้จากที่ไหน
คุณสามารถเยี่ยมชม [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/net/) สำหรับข้อมูลโดยละเอียดและตัวอย่าง

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}