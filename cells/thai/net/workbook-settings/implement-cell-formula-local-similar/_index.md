---
"description": "ค้นพบวิธีการนำสูตรเซลล์ที่คล้ายกับฟังก์ชันการทำงานภายในสูตรช่วงใน Aspose.Cells สำหรับ .NET มาใช้ เรียนรู้การปรับแต่งชื่อฟังก์ชันในตัวของ Excel และอื่นๆ อีกมากมาย"
"linktitle": "ใช้สูตรเซลล์แบบ Local คล้ายกับสูตรช่วงแบบ Local"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "ใช้สูตรเซลล์แบบ Local คล้ายกับสูตรช่วงแบบ Local"
"url": "/th/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ใช้สูตรเซลล์แบบ Local คล้ายกับสูตรช่วงแบบ Local

## การแนะนำ
Aspose.Cells สำหรับ .NET เป็น API การจัดการสเปรดชีตที่มีประสิทธิภาพและยืดหยุ่นซึ่งช่วยให้คุณสร้าง จัดการ และแปลงไฟล์ Excel ได้ด้วยการเขียนโปรแกรม หนึ่งในฟีเจอร์มากมายที่ Aspose.Cells นำเสนอคือความสามารถในการปรับแต่งพฤติกรรมของฟังก์ชันในตัวของ Excel รวมถึงความสามารถในการสร้างชื่อฟังก์ชันภายในของคุณเอง ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนต่างๆ ในการใช้สูตรเซลล์ที่คล้ายกับฟังก์ชันภายในของสูตรช่วงใน Aspose.Cells สำหรับ .NET
## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1. ติดตั้ง Microsoft Visual Studio 2010 หรือใหม่กว่าบนระบบของคุณ
2. เวอร์ชันล่าสุดของไลบรารี Aspose.Cells for .NET ที่ติดตั้งในโปรเจ็กต์ของคุณแล้ว คุณสามารถดาวน์โหลดไลบรารีได้จาก [หน้าดาวน์โหลด Aspose.Cells สำหรับ .NET](https://releases-aspose.com/cells/net/).
## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นในโปรเจ็กต์ C# ของคุณ เพิ่มคำสั่ง using ต่อไปนี้ที่ด้านบนของไฟล์โค้ดของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## ขั้นตอนที่ 1: สร้างคลาสการตั้งค่าโลกาภิวัตน์แบบกำหนดเอง
ขั้นตอนแรกคือการสร้างแบบกำหนดเอง `GlobalizationSettings` คลาสที่จะช่วยให้คุณแทนที่พฤติกรรมเริ่มต้นของฟังก์ชัน Excel ได้ ในตัวอย่างนี้ เราจะเปลี่ยนชื่อของ `SUM` และ `AVERAGE` ฟังก์ชั่นการ `UserFormulaLocal_SUM` และ `UserFormulaLocal_AVERAGE`ตามลำดับ
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //เปลี่ยนชื่อฟังก์ชัน SUM ตามความต้องการของคุณ
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //เปลี่ยนชื่อฟังก์ชัน AVERAGE ตามความต้องการของคุณ
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## ขั้นตอนที่ 2: สร้างเวิร์กบุ๊กใหม่และกำหนดค่าการตั้งค่าสากลแบบกำหนดเอง
ขั้นตอนต่อไป ให้สร้างอินสแตนซ์เวิร์กบุ๊กใหม่และกำหนดค่าแบบกำหนดเอง `GlobalizationSettings` คลาสการใช้งานของเวิร์กบุ๊ก `Settings.GlobalizationSettings` คุณสมบัติ.
```csharp
//สร้างสมุดงาน
Workbook wb = new Workbook();
//กำหนดคลาสการใช้งาน GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## ขั้นตอนที่ 3: เข้าถึงเวิร์กชีตแรกและเซลล์
ตอนนี้เรามาเข้าถึงเวิร์กชีตแรกในเวิร์กบุ๊กและเซลล์เฉพาะภายในเวิร์กชีตนั้นกัน
```csharp
//เข้าถึงแผ่นงานแรก
Worksheet ws = wb.Worksheets[0];
//เข้าถึงเซลล์บางส่วน
Cell cell = ws.Cells["C4"];
```
## ขั้นตอนที่ 4: กำหนดสูตรและพิมพ์ FormulaLocal
สุดท้ายนี้เรามากำหนด `SUM` และ `AVERAGE` สูตรไปที่เซลล์และพิมพ์ผลลัพธ์ `FormulaLocal` คุณค่า
```csharp
//กำหนดสูตร SUM และพิมพ์ FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//กำหนดสูตร AVERAGE และพิมพ์ FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## บทสรุป
ในบทช่วยสอนนี้ คุณจะได้เรียนรู้วิธีการใช้สูตรเซลล์ที่คล้ายกับฟังก์ชันการทำงานภายในสูตรช่วงใน Aspose.Cells สำหรับ .NET โดยการสร้างสูตรเซลล์แบบกำหนดเอง `GlobalizationSettings` คุณสามารถแทนที่พฤติกรรมเริ่มต้นของฟังก์ชัน Excel และปรับแต่งชื่อฟังก์ชันท้องถิ่นให้เหมาะกับความต้องการของคุณได้ ซึ่งอาจมีประโยชน์อย่างยิ่งเมื่อทำงานกับเอกสาร Excel ที่แปลเป็นภาษาท้องถิ่นหรือภาษาต่างประเทศ
## คำถามที่พบบ่อย
### จุดประสงค์ของการ `GlobalizationSettings` คลาสใน Aspose.Cells?
การ `GlobalizationSettings` คลาสใน Aspose.Cells ช่วยให้คุณสามารถปรับแต่งลักษณะการทำงานของฟังก์ชัน Excel ในตัวได้ รวมถึงความสามารถในการเปลี่ยนชื่อฟังก์ชันภายในเครื่อง
### ฉันสามารถแทนที่พฤติกรรมของฟังก์ชันอื่นนอกเหนือจาก `SUM` และ `AVERAGE`-
ใช่ คุณสามารถแทนที่พฤติกรรมของฟังก์ชัน Excel ในตัวใดๆ ได้โดยการแก้ไข `GetLocalFunctionName` วิธีการที่คุณกำหนดเอง `GlobalizationSettings` ระดับ.
### มีวิธีรีเซ็ตชื่อฟังก์ชันกลับไปเป็นค่าเริ่มต้นหรือไม่
ใช่ คุณสามารถรีเซ็ตชื่อฟังก์ชันได้โดยการลบชื่อที่กำหนดเอง `GlobalizationSettings` คลาสหรือโดยส่งคืนสตริงว่างจาก `GetLocalFunctionName` วิธี.
### ฉันสามารถใช้ฟีเจอร์นี้เพื่อสร้างฟังก์ชันที่กำหนดเองใน Aspose.Cells ได้หรือไม่
ไม่, `GlobalizationSettings` คลาสนี้ได้รับการออกแบบมาเพื่อแทนที่พฤติกรรมของฟังก์ชันในตัวของ Excel ไม่ใช่เพื่อสร้างฟังก์ชันที่กำหนดเอง หากคุณจำเป็นต้องสร้างฟังก์ชันที่กำหนดเอง คุณสามารถใช้ `UserDefinedFunction` คลาสใน Aspose.Cells
### ฟีเจอร์นี้มีอยู่ใน Aspose.Cells ทุกเวอร์ชันสำหรับ .NET หรือไม่
ใช่ครับ `GlobalizationSettings` คลาสและความสามารถในการปรับแต่งชื่อฟังก์ชันนั้นมีอยู่ใน Aspose.Cells ทุกเวอร์ชันสำหรับ .NET


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}