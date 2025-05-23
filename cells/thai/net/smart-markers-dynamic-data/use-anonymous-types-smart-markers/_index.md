---
"description": "เรียนรู้วิธีใช้ประเภทที่ไม่ระบุชื่อกับมาร์กเกอร์อัจฉริยะใน Aspose.Cells สำหรับการสร้างรายงาน Excel แบบไดนามิกใน .NET ทำตามคำแนะนำง่ายๆ ของเรา"
"linktitle": "ใช้ประเภทที่ไม่ระบุชื่อกับ Smart Markers Aspose.Cells"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "ใช้ประเภทที่ไม่ระบุชื่อกับ Smart Markers Aspose.Cells"
"url": "/th/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ใช้ประเภทที่ไม่ระบุชื่อกับ Smart Markers Aspose.Cells

## การแนะนำ
ในการสร้างรายงาน Excel แบบไดนามิกในแอปพลิเคชัน .NET Aspose.Cells ถือเป็นเครื่องมือที่มีประสิทธิภาพที่โดดเด่น ฟีเจอร์ที่ดีที่สุดอย่างหนึ่งคือความสามารถในการทำงานกับมาร์กเกอร์อัจฉริยะและชนิดที่ไม่ระบุชื่อ หากคุณเพิ่งรู้จักแนวคิดนี้ ไม่ต้องกังวล! คู่มือนี้จะอธิบายทุกสิ่งที่คุณจำเป็นต้องรู้ ตั้งแต่ข้อกำหนดเบื้องต้นไปจนถึงตัวอย่างปฏิบัติจริง โดยยังคงให้ความรู้ที่น่าสนใจและทำตามได้ง่าย
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเจาะลึกโค้ด เรามาตรวจสอบให้แน่ใจก่อนว่าคุณมีทุกสิ่งที่จำเป็นในการรันตัวอย่างในบทช่วยสอนนี้ได้อย่างราบรื่น
### 1. สภาพแวดล้อม .NET
ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อม .NET ที่ใช้งานได้บนเครื่องของคุณแล้ว คุณสามารถใช้ Visual Studio หรือ IDE อื่น ๆ ตามที่คุณต้องการ
### 2. ไลบรารี Aspose.Cells
คุณจะต้องมีไลบรารี Aspose.Cells หากคุณยังไม่ได้ดาวน์โหลด คุณสามารถค้นหาได้อย่างง่ายดาย [ที่นี่](https://releases.aspose.com/cells/net/). คุณยังสามารถทดลองใช้งานฟรีได้ที่ [ลิงค์นี้](https://releases-aspose.com/).
### 3. ความรู้พื้นฐานเกี่ยวกับ C#
ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม C# จะช่วยให้คุณเรียนรู้บทช่วยสอนได้ง่ายขึ้น หากคุณคุ้นเคยกับคำศัพท์อย่างคลาส อ็อบเจ็กต์ และคุณสมบัติ ก็แสดงว่าคุณพร้อมแล้ว!
## แพ็คเกจนำเข้า
หากต้องการใช้ไลบรารี Aspose.Cells ในโปรเจ็กต์ของคุณ คุณต้องนำเข้าเนมสเปซที่เกี่ยวข้อง เพิ่มคำสั่ง using ต่อไปนี้ที่ด้านบนของไฟล์ C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
เนมสเปซเหล่านี้จะทำให้คุณสามารถเข้าถึงคลาสและวิธีการที่จำเป็นทั้งหมดซึ่งจะกล่าวถึงในภายหลัง
ตอนนี้เรามาเริ่มที่เนื้อหาหลักของบทช่วยสอนกันเลย คุณจะได้เรียนรู้วิธีการสร้างไฟล์ Excel ที่มีมาร์กเกอร์อัจฉริยะโดยใช้คลาสที่กำหนดเอง ไม่ต้องกังวล เราจะแบ่งทุกอย่างออกเป็นขั้นตอนที่จัดการได้เอง!
## ขั้นตอนที่ 1: สร้างคลาสที่กำหนดเอง
ขั้นแรก เราต้องมีคลาสง่ายๆ เพื่อแสดงข้อมูลที่เราต้องการเพิ่มลงในไฟล์ Excel คลาสนี้จะเก็บข้อมูลเกี่ยวกับบุคคล
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
ที่นี่เราจะกำหนดคลาสที่เรียกว่า `Person` มีคุณสมบัติ 2 ประการ `Name` และ `Age`ผู้สร้างจะกำหนดค่าคุณสมบัติเหล่านี้ 
## ขั้นตอนที่ 2: ตั้งค่าตัวออกแบบเวิร์กบุ๊ก
ต่อไปเรามาสร้างอินสแตนซ์ของ `WorkbookDesigner` คลาสที่เราจะใช้ในการออกแบบไฟล์ Excel ด้วยมาร์กเกอร์อัจฉริยะ
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
// สร้างอินสแตนซ์ของวัตถุตัวออกแบบเวิร์กบุ๊ก
WorkbookDesigner report = new WorkbookDesigner();
```
แทนที่ `"Your Document Directory"` ด้วยเส้นทางไฟล์จริงของคุณที่คุณต้องการบันทึกไฟล์ Excel `WorkbookDesigner` คลาสเป็นหัวใจของการดำเนินการนี้ ซึ่งคุณจะกำหนดเทมเพลตของคุณเอง
## ขั้นตอนที่ 3: เพิ่มเครื่องหมายลงในเซลล์
ตอนนี้เราต้องเพิ่มมาร์กเกอร์อัจฉริยะลงในเวิร์กชีต มาร์กเกอร์เหล่านี้จะเป็นตัวแทนสำหรับข้อมูลที่เราจะป้อนในภายหลัง
```csharp
// รับแผ่นงานแรกในสมุดงาน
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// ใส่เครื่องหมายบางอย่างลงในเซลล์
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
เรากำหนดเวิร์กชีตแรกและตั้งค่าสำหรับเซลล์ส่วนหัว มาร์กเกอร์อัจฉริยะจะขึ้นต้นด้วย `&=` ซึ่งแจ้งให้ Aspose ทราบว่าสิ่งเหล่านี้เป็นตัวแทนสำหรับข้อมูลที่จะแทรกในภายหลัง
## ขั้นตอนที่ 4: สร้างรายชื่อบุคคล
ตอนนี้เรามาสร้างรายชื่อคนที่ใช้ของเรา `Person` คลาสที่เราจะใช้ในการเติมสมาร์ทมาร์กเกอร์
```csharp
// สร้างตัวอย่างคอลเลกชันรายการตามคลาสที่กำหนดเอง
IList<Person> list = new List<Person>();
// ระบุค่าสำหรับเครื่องหมายโดยใช้คลาสวัตถุแบบกำหนดเอง
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
เราสร้างรายการและเพิ่มอินสแตนซ์ของ `Person` รายการนี้ทำหน้าที่เป็นแหล่งข้อมูลของเราเมื่อเติมข้อมูลลงในเทมเพลต Excel
## ขั้นตอนที่ 5: ตั้งค่าแหล่งข้อมูลและเครื่องหมายกระบวนการ
หลังจากที่เรามีรายการพร้อมแล้ว เราจะต้องตั้งค่าเป็นแหล่งข้อมูลสำหรับรายการของเรา `WorkbookDesigner` จากนั้นทำการประมวลผลเครื่องหมาย
```csharp
// ตั้งค่าแหล่งที่มาของข้อมูล
report.SetDataSource("MyProduct", list);
// ดำเนินการตามเครื่องหมาย
report.Process(false);
```
การ `SetDataSource` วิธีนี้จะเชื่อมโยงรายการที่เรากำหนดไว้ก่อนหน้านี้กับเครื่องหมาย `Process` วิธีการนี้จะแทนที่เครื่องหมายอัจฉริยะในเวิร์กบุ๊กด้วยค่าจริงจากวัตถุของเรา
## ขั้นตอนที่ 6: บันทึกไฟล์ Excel
สุดท้ายเราจะบันทึกสมุดงานที่แก้ไขแล้วไปยังไดเร็กทอรีที่เรากำหนด
```csharp
// บันทึกไฟล์ Excel
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
บรรทัดนี้จะบันทึกเวิร์กบุ๊กไปยังเส้นทางไฟล์ที่ระบุ คุณสามารถเปิดไฟล์นี้โดยใช้ Excel เพื่อดูข้อมูลที่แทรกเข้าไป
## บทสรุป
และแล้วคุณก็ทำได้สำเร็จ! คุณได้สร้างไฟล์ Excel สำเร็จแล้วโดยใช้มาร์กเกอร์อัจฉริยะใน Aspose.Cells ด้วยคลาสที่กำหนดเองของคุณ วิธีนี้ไม่เพียงแต่ทำให้การจัดการข้อมูลของคุณมีความคล่องตัวมากขึ้น แต่ยังทำให้โค้ดของคุณสะอาดและเป็นระเบียบอีกด้วย
ดังนั้น ไม่ว่าคุณจะกำลังสร้างรายงานสำหรับการวิเคราะห์ ติดตามข้อมูล หรือทำงานใดๆ ที่เกี่ยวข้องกับข้อมูล มาร์กเกอร์อัจฉริยะจะเป็นพันธมิตรของคุณในการทำให้รายงาน Excel จัดการและยืดหยุ่นมากขึ้น!
## คำถามที่พบบ่อย
### สมาร์ทมาร์กเกอร์ใน Aspose.Cells คืออะไร?
เครื่องหมายอัจฉริยะคือตัวแทนพิเศษในเอกสาร Excel ของคุณที่ช่วยให้คุณแทรกข้อมูลแบบไดนามิกระหว่างการรันไทม์ได้
### ฉันสามารถใช้ประเภทที่ไม่ระบุชื่อสำหรับเครื่องหมายอัจฉริยะได้หรือไม่
ใช่! สามารถใช้มาร์กเกอร์อัจฉริยะกับประเภทวัตถุใดๆ ก็ได้ รวมถึงประเภทที่ไม่ระบุชื่อ ตราบใดที่ตรงตามโครงสร้างข้อมูลที่คาดหวัง
### การใช้ Aspose.Cells ฟรีหรือไม่?
Aspose.Cells เป็นผลิตภัณฑ์ที่ต้องชำระเงิน แต่คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรีเพื่อสำรวจคุณสมบัติของมันได้
### Aspose.Cells รองรับรูปแบบไฟล์อะไรบ้าง?
รองรับรูปแบบไฟล์หลากหลาย รวมถึง XLS, XLSX, CSV และอื่นๆ
### ฉันสามารถหาข้อมูลเพิ่มเติมเกี่ยวกับ Aspose.Cells ได้จากที่ไหน
สำหรับรายละเอียดเพิ่มเติมโปรดตรวจสอบ [เอกสารประกอบ](https://reference.aspose.com/cells/net/) หรือเยี่ยมชม [ฟอรั่มสนับสนุน](https://forum-aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}