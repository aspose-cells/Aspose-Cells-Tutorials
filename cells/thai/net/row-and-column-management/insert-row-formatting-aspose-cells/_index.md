---
"description": "เรียนรู้การแทรกแถวด้วยการจัดรูปแบบใน Excel โดยใช้ Aspose.Cells สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการใช้งานที่ง่ายดาย"
"linktitle": "แทรกแถวด้วยการจัดรูปแบบใน Aspose.Cells .NET"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "แทรกแถวด้วยการจัดรูปแบบใน Aspose.Cells .NET"
"url": "/th/net/row-and-column-management/insert-row-formatting-aspose-cells/"
"weight": 24
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# แทรกแถวด้วยการจัดรูปแบบใน Aspose.Cells .NET

## การแนะนำ
หากคุณเคยใช้ Excel มาก่อน คุณจะทราบดีว่าการรักษาการจัดรูปแบบข้อมูลขณะทำการเปลี่ยนแปลงนั้นมีความสำคัญเพียงใด ไม่ว่าคุณจะเพิ่มแถวหรือคอลัมน์ใหม่ หรืออัปเดตอะไรก็ตาม การรักษารูปลักษณ์และความรู้สึกของสเปรดชีตของคุณถือเป็นสิ่งสำคัญสำหรับการอ่านและการทำงานอย่างมืออาชีพ ในบทช่วยสอนนี้ เราจะแนะนำวิธีแทรกแถวโดยใช้การจัดรูปแบบโดยใช้ Aspose.Cells สำหรับ .NET เตรียมตัวให้พร้อม เพราะเราจะเจาะลึกรายละเอียดทีละขั้นตอน!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
1. Aspose.Cells สำหรับ .NET: คุณสามารถดาวน์โหลดได้ [ที่นี่](https://releases-aspose.com/cells/net/).
2. สภาพแวดล้อมการพัฒนา .NET: คุณสามารถใช้ Visual Studio หรือ IDE อื่นๆ ตามต้องการ
3. ความเข้าใจพื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับ C# เพียงเล็กน้อยจะช่วยให้เข้าใจโค้ดได้เป็นอย่างดี
## แพ็คเกจนำเข้า
หากต้องการเริ่มใช้ Aspose.Cells ในโปรเจ็กต์ของคุณ คุณจะต้องนำเข้าแพ็กเกจที่จำเป็น โดยคุณสามารถทำได้ดังนี้:
1. ติดตั้งแพ็กเกจ Aspose.Cells: เปิดคอนโซลตัวจัดการแพ็กเกจ NuGet ของคุณและรันคำสั่งต่อไปนี้:
```bash
Install-Package Aspose.Cells
```
2. เพิ่มการใช้คำสั่ง: ที่ด้านบนของไฟล์ C# ของคุณ ให้รวมเนมสเปซต่อไปนี้:
```csharp
using System.IO;
using Aspose.Cells;
```
ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นและนำเข้าแพ็คเกจแล้ว มาดูคำแนะนำทีละขั้นตอนในการแทรกแถวพร้อมการจัดรูปแบบกันเลย!
## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ
สิ่งแรกที่ต้องทำคือคุณต้องกำหนดเส้นทางไปยังไดเร็กทอรีที่ไฟล์ Excel ของคุณตั้งอยู่ นี่คือตำแหน่งที่ `book1.xls` ไฟล์จะถูกเก็บหรือเข้าถึง 
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
```
แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงบนคอมพิวเตอร์ของคุณที่บันทึกไฟล์ Excel ไว้ วิธีนี้ช่วยให้แอปพลิเคชันของคุณทราบว่าจะต้องค้นหาไฟล์ที่ใด
## ขั้นตอนที่ 2: สร้างสตรีมไฟล์
ต่อไปเราจะสร้างสตรีมไฟล์เพื่อเปิดไฟล์ Excel ซึ่งเป็นสิ่งสำคัญมาก เนื่องจากช่วยให้เราอ่านและแก้ไขเวิร์กบุ๊กได้
```csharp
// การสร้างสตรีมไฟล์ที่มีไฟล์ Excel ที่จะเปิด
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
ที่นี่เราจะเปิด `book1.xls` ไฟล์ในโหมดอ่าน ให้แน่ใจว่าไฟล์มีอยู่ในไดเร็กทอรีที่ระบุ มิฉะนั้นคุณจะพบข้อผิดพลาด
## ขั้นตอนที่ 3: สร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
ตอนนี้เรามาสร้างอินสแตนซ์ของ `Workbook` คลาสซึ่งแสดงถึงไฟล์ Excel ที่เราจะใช้ทำงานด้วย
```csharp
// การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
// การเปิดไฟล์ Excel ผ่านทางสตรีมไฟล์
Workbook workbook = new Workbook(fstream);
```
บรรทัดนี้จะเริ่มต้นวัตถุเวิร์กบุ๊กและเปิดโดยใช้สตรีมไฟล์ที่เราเพิ่งสร้างขึ้น
## ขั้นตอนที่ 4: เข้าถึงแผ่นงาน
หากต้องการทำการเปลี่ยนแปลง เราจำเป็นต้องเข้าถึงเวิร์กชีตเฉพาะภายในเวิร์กบุ๊ก สำหรับตัวอย่างนี้ เราจะใช้เวิร์กชีตแรก
```csharp
// การเข้าถึงเวิร์กชีตแรกในไฟล์ Excel
Worksheet worksheet = workbook.Worksheets[0];
```
เวิร์กชีตใน Excel จะถูกจัดทำดัชนีโดยเริ่มจาก 0 ในที่นี้ เราจะเข้าถึงเวิร์กชีตแรกซึ่งอยู่ที่ดัชนี 0
## ขั้นตอนที่ 5: ตั้งค่าตัวเลือกการจัดรูปแบบ
ขั้นต่อไป เราต้องกำหนดว่าเราต้องการแทรกแถวใหม่อย่างไร เราจะใช้ `InsertOptions` เพื่อระบุว่าเราต้องการคัดลอกการจัดรูปแบบจากแถวด้านบน
```csharp
// การตั้งค่าตัวเลือกการจัดรูปแบบ
InsertOptions insertOptions = new InsertOptions();
insertOptions.CopyFormatType = CopyFormatType.SameAsAbove;
```
โดยการตั้งค่า `CopyFormatType` ถึง `SameAsAbove`การจัดรูปแบบใดๆ (เช่น แบบอักษร สี และเส้นขอบ) จากแถวเหนือจุดแทรกโดยตรงจะถูกนำไปใช้กับแถวใหม่
## ขั้นตอนที่ 6: แทรกแถว
ตอนนี้เราพร้อมที่จะแทรกแถวลงในเวิร์กชีตแล้ว เราจะวางไว้ที่ตำแหน่งที่สาม (ดัชนี 2 เนื่องจากเป็นฐานศูนย์)
```csharp
// การแทรกแถวเข้าในเวิร์กชีตที่ตำแหน่งที่ 3
worksheet.Cells.InsertRows(2, 1, insertOptions);
```
คำสั่งนี้จะแทรกแถวใหม่หนึ่งแถวในตำแหน่งที่ระบุโดยใช้ตัวเลือกการจัดรูปแบบที่เราเพิ่งตั้งค่าไว้ เหมือนกับมีเวทมนตร์ — แถวใหม่ของคุณจะปรากฏขึ้นพร้อมรูปแบบที่ถูกต้องทั้งหมด!
## ขั้นตอนที่ 7: บันทึกไฟล์ Excel ที่ปรับเปลี่ยนแล้ว
หลังจากทำการเปลี่ยนแปลงของคุณแล้ว สิ่งสำคัญคือการบันทึกเวิร์กบุ๊กเพื่อรักษาการปรับเปลี่ยนของคุณ 
```csharp
// การบันทึกไฟล์ Excel ที่แก้ไขแล้ว
workbook.Save(dataDir + "InsertingARowWithFormatting.out.xls");
```
ที่นี่เรากำลังบันทึกสมุดงานที่แก้ไขภายใต้ชื่อใหม่ `InsertingARowWithFormatting.out.xls`เพื่อหลีกเลี่ยงการเขียนทับไฟล์ต้นฉบับ ด้วยวิธีนี้ คุณสามารถย้อนกลับได้เสมอหากจำเป็น!
## ขั้นตอนที่ 8: ปิดสตรีมไฟล์
สุดท้ายนี้ ให้ปิดสตรีมไฟล์เพื่อทำความสะอาด นี่เป็นวิธีที่ดีในการปลดปล่อยทรัพยากร
```csharp
// การปิดสตรีมไฟล์เพื่อปลดปล่อยทรัพยากรทั้งหมด
fstream.Close();
```
การปิดสตรีม จะทำให้แน่ใจได้ว่าทรัพยากรทั้งหมดที่ใช้ระหว่างกระบวนการจะได้รับการปล่อยออกอย่างถูกต้อง ซึ่งช่วยป้องกันการรั่วไหลของหน่วยความจำ
## บทสรุป
และแล้วคุณก็ทำได้! คุณเพิ่งเรียนรู้วิธีการแทรกแถวด้วยการจัดรูปแบบในไฟล์ Excel โดยใช้ Aspose.Cells สำหรับ .NET วิธีนี้ไม่เพียงแต่ช่วยให้คุณรักษาความสวยงามของสเปรดชีตของคุณไว้ได้เท่านั้น แต่ยังเพิ่มประสิทธิภาพการทำงานของคุณโดยทำให้การทำงานซ้ำๆ เป็นแบบอัตโนมัติอีกด้วย ครั้งต่อไปที่คุณต้องแก้ไขแผ่นงาน Excel โปรดจำขั้นตอนเหล่านี้ไว้ แล้วคุณจะพร้อมรับมือกับมันอย่างมืออาชีพ!
## คำถามที่พบบ่อย
### Aspose.Cells สำหรับ .NET คืออะไร?
Aspose.Cells สำหรับ .NET เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงไฟล์ Excel ในแอปพลิเคชัน .NET ได้ โดยไม่จำเป็นต้องติดตั้ง Microsoft Excel
### ฉันสามารถแทรกหลายแถวในครั้งเดียวได้ไหม
ใช่! คุณสามารถปรับเปลี่ยนได้ `InsertRows` วิธีการแทรกหลายแถวโดยเปลี่ยนพารามิเตอร์ที่สองให้เป็นจำนวนแถวที่ต้องการแทรก
### จำเป็นต้องปิดสตรีมไฟล์หรือไม่?
ใช่แล้ว การปิดสตรีมไฟล์เพื่อปล่อยทรัพยากรใดๆ ที่ถูกสตรีมเก็บไว้และป้องกันการรั่วไหลของหน่วยความจำเป็นสิ่งสำคัญ
### ฉันสามารถบันทึกไฟล์ Excel ที่แก้ไขแล้วในรูปแบบใดได้บ้าง
Aspose.Cells รองรับรูปแบบต่างๆ รวมถึง XLSX, CSV และ PDF เป็นต้น
### ฉันจะเรียนรู้เพิ่มเติมเกี่ยวกับคุณลักษณะ Aspose.Cells ได้อย่างไร
คุณสามารถสำรวจคุณสมบัติและฟังก์ชันเพิ่มเติมได้โดยเยี่ยมชม [เอกสารประกอบ](https://reference-aspose.com/cells/net/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}