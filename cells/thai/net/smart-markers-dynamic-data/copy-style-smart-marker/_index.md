---
"description": "คัดลอกสไตล์และรูปแบบจากไฟล์เทมเพลตไปยังผลลัพธ์ Excel ที่คุณสร้างขึ้นได้อย่างง่ายดาย บทช่วยสอนที่ครอบคลุมนี้จะแนะนำคุณตลอดกระบวนการทีละขั้นตอน"
"linktitle": "คัดลอกสไตล์ด้วย Smart Marker ใน Aspose.Cells .NET"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "คัดลอกสไตล์ด้วย Smart Marker ใน Aspose.Cells .NET"
"url": "/th/net/smart-markers-dynamic-data/copy-style-smart-marker/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอกสไตล์ด้วย Smart Marker ใน Aspose.Cells .NET

## การแนะนำ
ในโลกของการจัดการข้อมูลและการประมวลผลสเปรดชีต Aspose.Cells สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ช่วยให้ผู้พัฒนาสามารถสร้าง จัดการ และส่งออกไฟล์ Excel ได้ด้วยโปรแกรม หนึ่งในฟีเจอร์ที่โดดเด่นของ Aspose.Cells คือความสามารถในการทำงานกับมาร์กเกอร์อัจฉริยะ ซึ่งช่วยให้ผู้พัฒนาสามารถคัดลอกสไตล์และฟอร์แมตจากไฟล์เทมเพลตไปยังเอาต์พุตที่สร้างขึ้นได้อย่างง่ายดาย บทช่วยสอนนี้จะแนะนำคุณตลอดขั้นตอนการใช้ Aspose.Cells เพื่อคัดลอกสไตล์จากไฟล์เทมเพลตและนำไปใช้กับไฟล์ Excel ที่คุณสร้างขึ้น
## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดต่อไปนี้:
1. Aspose.Cells สำหรับ .NET: คุณสามารถดาวน์โหลด Aspose.Cells เวอร์ชันล่าสุดสำหรับ .NET ได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/cells/net/).
2. Microsoft Visual Studio: คุณจะต้องมี Microsoft Visual Studio เวอร์ชันจึงจะเขียนและรันโค้ด C# ได้
3. ความรู้พื้นฐานเกี่ยวกับ C# และ .NET: คุณควรมีความเข้าใจพื้นฐานเกี่ยวกับภาษาการเขียนโปรแกรม C# และกรอบงาน .NET
## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นจาก Aspose.Cells สำหรับ .NET เพิ่มคำสั่ง using ต่อไปนี้ที่ด้านบนของไฟล์ C# ของคุณ:
```csharp
using System.IO;
using Aspose.Cells;
using System.Data;
```
## สร้างแหล่งข้อมูล
เริ่มต้นด้วยการสร้างแหล่งข้อมูลตัวอย่างซึ่งเราจะใช้เติมข้อมูลในไฟล์ Excel ในตัวอย่างนี้ เราจะสร้าง `DataTable` เรียกว่า `dtStudent` โดยมีสองคอลัมน์คือ “ชื่อ” และ “อายุ”
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
// สร้างตารางข้อมูลนักเรียน
DataTable dtStudent = new DataTable("Student");
// กำหนดฟิลด์ในนั้น
DataColumn dcName = new DataColumn("Name", typeof(string));
dtStudent.Columns.Add(dcName);
dtStudent.Columns.Add(new DataColumn("Age", typeof(int)));
// บวกเพิ่มสามแถวเข้าไป
DataRow drName1 = dtStudent.NewRow();
DataRow drName2 = dtStudent.NewRow();
DataRow drName3 = dtStudent.NewRow();
drName1["Name"] = "John";
drName1["Age"] = 23;
drName2["Name"] = "Jack";
drName2["Age"] = 24;
drName3["Name"] = "James";
drName3["Age"] = 32;
dtStudent.Rows.Add(drName1);
dtStudent.Rows.Add(drName2);
dtStudent.Rows.Add(drName3);
```
## โหลดไฟล์เทมเพลต
ต่อไปเราจะโหลดไฟล์เทมเพลต Excel ที่ประกอบด้วยสไตล์ที่เราต้องการคัดลอก ในตัวอย่างนี้ เราจะถือว่าไฟล์เทมเพลตมีชื่อว่า "Template.xlsx" และตั้งอยู่ใน `dataDir` ไดเรกทอรี
```csharp
string filePath = dataDir + "Template.xlsx";
// สร้างสมุดงานจากไฟล์เทมเพลต Smart Markers
Workbook workbook = new Workbook(filePath);
```
## สร้างอินสแตนซ์ WorkbookDesigner
ตอนนี้เราจะสร้าง `WorkbookDesigner` อินสแตนซ์ที่จะใช้ในการประมวลผลมาร์กเกอร์อัจฉริยะในไฟล์เทมเพลต
```csharp
// สร้างอินสแตนซ์ WorkbookDesigner ใหม่
WorkbookDesigner designer = new WorkbookDesigner();
// ระบุสมุดงาน
designer.Workbook = workbook;
```
## ตั้งค่าแหล่งที่มาของข้อมูล
จากนั้นเราจะกำหนดแหล่งข้อมูลสำหรับ `WorkbookDesigner` ตัวอย่างที่เป็น `dtStudent` `DataTable` เราสร้างไว้ก่อนหน้านี้แล้ว
```csharp
// ตั้งค่าแหล่งที่มาของข้อมูล
designer.SetDataSource(dtStudent);
```
## ประมวลผลเครื่องหมายอัจฉริยะ
ต่อไปเราจะเรียก `Process()` วิธีการประมวลผลเครื่องหมายอัจฉริยะในไฟล์เทมเพลต
```csharp
// ประมวลผลมาร์กเกอร์อัจฉริยะ
designer.Process();
```
## บันทึกไฟล์ Excel
สุดท้ายเราจะบันทึกไฟล์ Excel ที่สร้างขึ้นด้วยสไตล์ที่คัดลอกมา
```csharp
// บันทึกไฟล์ Excel
workbook.Save(dataDir + "output.xlsx", SaveFormat.Xlsx);
```
เสร็จเรียบร้อย! คุณได้ใช้ Aspose.Cells สำหรับ .NET เพื่อคัดลอกสไตล์จากไฟล์เทมเพลตและนำไปใช้กับไฟล์ Excel ที่คุณสร้างขึ้นสำเร็จแล้ว
## บทสรุป
ในบทช่วยสอนนี้ คุณจะได้เรียนรู้วิธีใช้ Aspose.Cells สำหรับ .NET เพื่อคัดลอกสไตล์จากไฟล์เทมเพลตและนำไปใช้กับไฟล์ Excel ที่คุณสร้างขึ้น การใช้ความสามารถของมาร์กเกอร์อัจฉริยะจะช่วยให้คุณปรับกระบวนการสร้าง Excel ให้มีประสิทธิภาพและรับรองรูปลักษณ์และความรู้สึกที่สอดคล้องกันในสเปรดชีตของคุณ
## คำถามที่พบบ่อย
### จุดประสงค์ของการ `WorkbookDesigner` คลาสใน Aspose.Cells สำหรับ .NET?
การ `WorkbookDesigner` คลาสใน Aspose.Cells สำหรับ .NET ใช้ในการประมวลผลมาร์กเกอร์อัจฉริยะในไฟล์เทมเพลตและนำไปใช้กับไฟล์ Excel ที่สร้างขึ้น ช่วยให้นักพัฒนาสามารถคัดลอกสไตล์ รูปแบบ และแอตทริบิวต์อื่นๆ จากเทมเพลตไปยังเอาต์พุตได้อย่างง่ายดาย
### ฉันสามารถใช้ Aspose.Cells สำหรับ .NET กับแหล่งข้อมูลอื่นนอกเหนือจากนี้ได้หรือไม่ `DataTable`-
ใช่ คุณสามารถใช้ Aspose.Cells สำหรับ .NET กับแหล่งข้อมูลต่างๆ เช่น `DataSet`- `IEnumerable`หรือวัตถุข้อมูลที่กำหนดเอง `SetDataSource()` วิธีการของ `WorkbookDesigner` คลาสสามารถรับแหล่งข้อมูลหลายประเภทได้
### ฉันจะปรับแต่งรูปแบบและรูปแบบในไฟล์เทมเพลตได้อย่างไร
คุณสามารถปรับแต่งสไตล์และรูปแบบในไฟล์เทมเพลตได้โดยใช้ Microsoft Excel หรือเครื่องมืออื่นๆ Aspose.Cells สำหรับ .NET จะคัดลอกสไตล์และรูปแบบเหล่านี้ไปยังไฟล์ Excel ที่สร้างขึ้น ช่วยให้คุณรักษารูปลักษณ์และความรู้สึกที่สอดคล้องกันในสเปรดชีตของคุณได้
### มีวิธีจัดการกับข้อผิดพลาดหรือข้อยกเว้นที่อาจเกิดขึ้นระหว่างกระบวนการหรือไม่
ใช่ คุณสามารถใช้บล็อก try-catch เพื่อจัดการข้อยกเว้นใดๆ ที่อาจเกิดขึ้นระหว่างกระบวนการได้ Aspose.Cells สำหรับ .NET จะให้ข้อความข้อยกเว้นโดยละเอียดที่สามารถช่วยคุณแก้ไขปัญหาใดๆ ได้
### ฉันสามารถใช้ Aspose.Cells สำหรับ .NET ในสภาพแวดล้อมการผลิตได้หรือไม่
ใช่ Aspose.Cells สำหรับ .NET เป็นผลิตภัณฑ์เชิงพาณิชย์ที่ใช้กันอย่างแพร่หลายในสภาพแวดล้อมการผลิต โดยให้โซลูชันที่มั่นคงและเชื่อถือได้สำหรับการทำงานกับไฟล์ Excel ในเชิงโปรแกรม คุณสามารถซื้อ [ใบอนุญาต](https://purchase.aspose.com/buy) หรือลองดู [ทดลองใช้งานฟรี](https://releases.aspose.com/) เพื่อประเมินความสามารถของผลิตภัณฑ์


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}