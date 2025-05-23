---
"description": "ปลดการป้องกันเวิร์กชีต Excel ได้อย่างง่ายดายโดยไม่ต้องใช้รหัสผ่านโดยใช้ Aspose.Cells สำหรับ .NET เรียนรู้การตั้งค่า ขั้นตอนการเขียนโค้ด และบันทึกเอาต์พุตได้อย่างราบรื่น"
"linktitle": "ยกเลิกการป้องกันเวิร์กชีตที่ได้รับการป้องกันโดยใช้ Aspose.Cells"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "ยกเลิกการป้องกันเวิร์กชีตที่ได้รับการป้องกันโดยใช้ Aspose.Cells"
"url": "/th/net/worksheet-security/unprotect-simply-protected/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ยกเลิกการป้องกันเวิร์กชีตที่ได้รับการป้องกันโดยใช้ Aspose.Cells

## การแนะนำ
การลบการป้องกันออกจากเวิร์กชีต Excel อาจช่วยชีวิตคุณได้เมื่อคุณจำเป็นต้องทำการเปลี่ยนแปลงเซลล์ที่ถูกล็อกหรืออัปเดตข้อมูล ด้วย Aspose.Cells สำหรับ .NET คุณสามารถทำสิ่งนี้ได้อย่างราบรื่นผ่านโค้ด ช่วยให้คุณสามารถยกเลิกการป้องกันเวิร์กชีตโดยอัตโนมัติโดยไม่ต้องใช้รหัสผ่านหากได้รับการป้องกันไว้ บทช่วยสอนนี้จะแนะนำคุณในแต่ละขั้นตอน ตั้งแต่การตั้งค่าข้อกำหนดเบื้องต้นไปจนถึงการเขียนโค้ดที่จำเป็น โดยทั้งหมดนี้ทำได้ด้วยวิธีที่ตรงไปตรงมาเพื่อให้ทุกอย่างเรียบง่ายแต่มีประสิทธิภาพ
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเจาะลึก เรามาตรวจสอบกันก่อนว่าคุณได้ตั้งค่าทุกอย่างเพื่อเริ่มการยกเลิกการป้องกันเวิร์กชีตด้วย Aspose.Cells สำหรับ .NET แล้ว:
- Aspose.Cells สำหรับ .NET: คุณจะต้องมีไลบรารีนี้เพื่อทำงานกับไฟล์ Excel ด้วยโปรแกรม คุณสามารถดาวน์โหลดได้จาก [หน้าดาวน์โหลด Aspose.Cells](https://releases.aspose.com/cells/net/) หรือเข้าถึงข้อมูลอย่างครอบคลุม [เอกสารประกอบ](https://reference-aspose.com/cells/net/).
- สภาพแวดล้อมการพัฒนา: สภาพแวดล้อมที่เหมาะสมสำหรับแอปพลิเคชัน .NET เช่น Visual Studio
- ความเข้าใจพื้นฐานเกี่ยวกับ C#: ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม C# บางส่วนจะเป็นประโยชน์ในการติดตามตัวอย่างโค้ด
## แพ็คเกจนำเข้า
หากต้องการใช้ Aspose.Cells ในโปรเจ็กต์ .NET ก่อนอื่นคุณต้องนำเข้าไลบรารี Aspose.Cells ซึ่งทำได้โดยเพิ่มแพ็กเกจ Aspose.Cells NuGet ลงในโปรเจ็กต์ของคุณ นี่คือคำแนะนำโดยย่อ:
1. เปิดโปรเจ็กต์ของคุณใน Visual Studio
2. ใน Solution Explorer ให้คลิกขวาที่โครงการของคุณ และเลือก "จัดการแพ็คเกจ NuGet"
3. ค้นหา "Aspose.Cells" และติดตั้งเวอร์ชันล่าสุด
4. เมื่อติดตั้งแล้วให้เพิ่มการนำเข้าต่อไปนี้ที่ด้านบนของไฟล์โค้ดของคุณ:
```csharp
using System.IO;
using Aspose.Cells;
```
ตอนนี้เรามาดูกระบวนการจริงในการยกเลิกการป้องกันเวิร์กชีต Excel กัน!
มาแบ่งกระบวนการออกเป็นขั้นตอนที่ทำตามได้ง่าย ตัวอย่างนี้ถือว่าเวิร์กชีตที่คุณกำลังทำงานอยู่ไม่มีล็อกที่ได้รับการป้องกันด้วยรหัสผ่าน
## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีไฟล์
ในขั้นตอนนี้ เราจะระบุไดเรกทอรีที่เก็บไฟล์ Excel ของเรา วิธีนี้จะช่วยให้เข้าถึงไฟล์อินพุตและบันทึกไฟล์เอาต์พุตในตำแหน่งที่ต้องการได้ง่ายขึ้น
```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
```
โดยการตั้งค่าเส้นทางไดเรกทอรีใน `dataDir`คุณสามารถสร้างทางลัดที่สะดวกสำหรับการเข้าถึงและบันทึกไฟล์โดยไม่จำเป็นต้องพิมพ์เส้นทางทั้งหมดซ้ำๆ กัน
## ขั้นตอนที่ 2: โหลดสมุดงาน Excel
ตอนนี้เรามาโหลดไฟล์ Excel ที่เราต้องการใช้กัน ที่นี่เราจะสร้างไฟล์ Excel `Workbook` วัตถุซึ่งแสดงถึงไฟล์ Excel ทั้งหมด
```csharp
// การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
Workbook workbook = new Workbook(dataDir + "book1.xls");
   ```
การ `Workbook` วัตถุเป็นส่วนหลักของ Aspose.Cells และช่วยให้คุณสามารถดำเนินการต่างๆ กับไฟล์ Excel ได้ โดยส่งเส้นทางของ `"book1.xls"`บรรทัดนี้จะโหลดไฟล์เป้าหมายของเราเข้าสู่โปรแกรม
## ขั้นตอนที่ 3: เข้าถึงเวิร์กชีตที่คุณต้องการยกเลิกการป้องกัน
เมื่อโหลดเวิร์กบุ๊กแล้ว ขั้นตอนต่อไปคือการระบุเวิร์กชีตที่คุณต้องการยกเลิกการป้องกัน ในตัวอย่างนี้ เราจะเข้าถึงเวิร์กชีตแรกในเวิร์กบุ๊ก
```csharp
// การเข้าถึงเวิร์กชีตแรกในไฟล์ Excel
Worksheet worksheet = workbook.Worksheets[0];
```
การ `Worksheets` คุณสมบัตินี้ช่วยให้เราเข้าถึงเวิร์กชีตทั้งหมดภายในเวิร์กบุ๊กได้ โดยระบุ `[0]`เรากำลังเข้าถึงเวิร์กชีตแรก คุณสามารถปรับดัชนีนี้ได้หากเวิร์กชีตเป้าหมายของคุณอยู่ในตำแหน่งอื่น
## ขั้นตอนที่ 4: ยกเลิกการป้องกันแผ่นงาน
ตอนนี้มาถึงส่วนสำคัญ: การยกเลิกการป้องกันแผ่นงาน เนื่องจากบทช่วยสอนนี้เน้นที่แผ่นงานที่ได้รับการป้องกันอย่างง่าย (แผ่นงานที่ไม่มีรหัสผ่าน) การยกเลิกการป้องกันจึงทำได้ง่าย
```csharp
// การยกเลิกการป้องกันแผ่นงานโดยไม่ต้องใช้รหัสผ่าน
worksheet.Unprotect();
```
ที่นี่, `Unprotect()` ถูกเรียกไปที่ `worksheet` วัตถุ เนื่องจากเรากำลังจัดการกับแผ่นงานที่ไม่ได้รับการป้องกันด้วยรหัสผ่าน จึงไม่จำเป็นต้องมีพารามิเตอร์เพิ่มเติม เวิร์กชีตควรจะไม่มีการป้องกันและสามารถแก้ไขได้แล้ว
## ขั้นตอนที่ 5: บันทึกสมุดงานที่อัปเดต
หลังจากยกเลิกการป้องกันเวิร์กชีตแล้ว เราจำเป็นต้องบันทึกเวิร์กบุ๊ก คุณสามารถเลือกที่จะเขียนทับไฟล์ต้นฉบับหรือบันทึกเป็นไฟล์ใหม่
```csharp
// การบันทึกสมุดงาน
workbook.Save(dataDir + "output.xls", SaveFormat.Excel97To2003);
```
ในบรรทัดนี้ เราบันทึกสมุดงานโดยใช้ `Save` วิธีการ. `SaveFormat.Excel97To2003` ช่วยให้แน่ใจว่าเวิร์กบุ๊กจะถูกบันทึกในรูปแบบ Excel รุ่นเก่า ซึ่งอาจมีประโยชน์หากมีปัญหาเรื่องความเข้ากันได้ เปลี่ยนรูปแบบหากคุณใช้ Excel รุ่นใหม่กว่า
## บทสรุป
เพียงเท่านี้ก็เสร็จเรียบร้อย! ด้วยโค้ดเพียงไม่กี่บรรทัด คุณก็จะสามารถยกเลิกการป้องกันเวิร์กชีตที่ได้รับการป้องกันอย่างง่ายในไฟล์ Excel ได้สำเร็จโดยใช้ Aspose.Cells สำหรับ .NET แนวทางนี้เหมาะอย่างยิ่งสำหรับการทำงานอัตโนมัติในไฟล์ Excel ช่วยประหยัดเวลาและความพยายามของคุณ นอกจากนี้ ด้วย Aspose.Cells คุณยังได้รับเครื่องมืออันทรงพลังสำหรับจัดการและปรับเปลี่ยนไฟล์ Excel ด้วยโปรแกรม ซึ่งเปิดโลกแห่งความเป็นไปได้สำหรับการทำงานอัตโนมัติในเวิร์กโฟลว์สเปรดชีตของคุณ
## คำถามที่พบบ่อย
### Aspose.Cells สำหรับ .NET คืออะไร?
Aspose.Cells สำหรับ .NET เป็นไลบรารีอันทรงพลังสำหรับการทำงานกับไฟล์ Excel ในแอปพลิเคชัน .NET ช่วยให้คุณสร้าง แก้ไข แปลง และจัดการไฟล์ Excel ได้โดยไม่ต้องติดตั้ง Microsoft Excel
### ฉันสามารถยกเลิกการป้องกันเวิร์กชีตที่ป้องกันด้วยรหัสผ่านด้วยวิธีนี้ได้หรือไม่
ไม่ วิธีนี้ใช้ได้กับเวิร์กชีตที่ได้รับการป้องกันเท่านั้น สำหรับชีตที่ได้รับการป้องกันด้วยรหัสผ่าน คุณจะต้องระบุรหัสผ่านใน `Unprotect()` วิธี.
### ฉันจำเป็นต้องติดตั้ง Microsoft Excel เพื่อใช้ Aspose.Cells หรือไม่
ไม่ Aspose.Cells ทำงานแยกจาก Microsoft Excel ดังนั้นคุณไม่จำเป็นต้องติดตั้งไว้ในระบบของคุณ
### ฉันสามารถบันทึกเวิร์กชีตที่ไม่ได้รับการป้องกันในรูปแบบ Excel ใหม่กว่าได้หรือไม่
ใช่ คุณสามารถทำได้ Aspose.Cells รองรับรูปแบบต่างๆ มากมาย รวมถึง `XLSX`. เพียงเปลี่ยนรูปแบบการบันทึกให้เหมาะสมใน `Save` วิธี.
### Aspose.Cells สามารถใช้ได้กับแพลตฟอร์มอื่นนอกเหนือจาก .NET หรือไม่
ใช่ Aspose.Cells มีเวอร์ชันสำหรับ Java และแพลตฟอร์มอื่นๆ ช่วยให้มีฟังก์ชันการทำงานที่คล้ายคลึงกันในสภาพแวดล้อมการเขียนโปรแกรมที่แตกต่างกัน


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}