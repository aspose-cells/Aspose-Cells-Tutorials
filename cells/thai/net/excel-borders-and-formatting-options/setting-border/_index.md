---
title: การตั้งค่าขอบตามโปรแกรมใน Excel
linktitle: การตั้งค่าขอบตามโปรแกรมใน Excel
second_title: API การประมวลผล Excel ของ Aspose.Cells .NET
description: เรียนรู้วิธีการตั้งค่าขอบเขตในโปรแกรม Excel โดยใช้ Aspose.Cells สำหรับ .NET ประหยัดเวลาและทำให้งาน Excel ของคุณเป็นอัตโนมัติ
weight: 10
url: /th/net/excel-borders-and-formatting-options/setting-border/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การตั้งค่าขอบตามโปรแกรมใน Excel

## การแนะนำ

คุณเบื่อกับการตั้งค่าขอบเขตด้วยตนเองในแผ่นงาน Excel ของคุณหรือไม่? คุณไม่ได้เป็นคนเดียว! การตั้งค่าขอบเขตอาจเป็นงานที่น่าเบื่อ โดยเฉพาะเมื่อคุณต้องจัดการกับชุดข้อมูลขนาดใหญ่ แต่ไม่ต้องกังวล! ด้วย Aspose.Cells สำหรับ .NET คุณสามารถทำให้กระบวนการนี้เป็นแบบอัตโนมัติ ช่วยประหยัดเวลาและความพยายาม ในบทช่วยสอนนี้ เราจะเจาะลึกถึงรายละเอียดเล็กๆ น้อยๆ ของการตั้งค่าขอบเขตในเวิร์กบุ๊ก Excel ด้วยโปรแกรม ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น คุณจะพบว่าคู่มือนี้ทำตามได้ง่ายและเต็มไปด้วยข้อมูลเชิงลึกที่มีประโยชน์

คุณพร้อมที่จะเพิ่มทักษะการใช้งาน Excel อัตโนมัติแล้วหรือยัง มาเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1.  Visual Studio: คุณควรมี Visual Studio ติดตั้งอยู่บนเครื่องของคุณ หากยังไม่มี โปรดดาวน์โหลดจาก[ที่นี่](https://visualstudio.microsoft.com/downloads/).
2.  Aspose.Cells สำหรับ .NET: คุณต้องมีไลบรารี Aspose.Cells คุณสามารถรับได้โดยดาวน์โหลด DLL จาก[ลิงค์นี้](https://releases.aspose.com/cells/net/) หรือโดยใช้ NuGet ในโครงการของคุณ:
```bash
Install-Package Aspose.Cells
```
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจโค้ดได้ดีขึ้น
4. สภาพแวดล้อมการพัฒนา: ตั้งค่าแอปพลิเคชันคอนโซลหรือประเภทโปรเจ็กต์ใดๆ ที่คุณสามารถรันโค้ด C# ได้

เมื่อคุณตั้งค่าทุกอย่างเรียบร้อยแล้ว เราจะไปต่อยังส่วนสนุก ๆ ได้เลย: การเขียนโค้ด!

## แพ็คเกจนำเข้า

ตอนนี้เรามีทุกอย่างเรียบร้อยแล้ว ให้เราอิมพอร์ตเนมสเปซที่จำเป็นลงในไฟล์ C# ของเรา เพิ่มสิ่งต่อไปนี้ที่ด้านบนของไฟล์โค้ด:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

เนมสเปซเหล่านี้ช่วยให้คุณเข้าถึงฟังก์ชันการทำงานของ Aspose.Cells และฟังก์ชันสีจากเนมสเปซ System.Drawing

## ขั้นตอนที่ 1: กำหนดไดเรกทอรีเอกสารของคุณ

ขั้นแรก เราต้องระบุตำแหน่งที่จะบันทึกไฟล์ Excel ของเรา กำหนดเส้นทางไปยังไดเร็กทอรีเอกสารของคุณ:

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
```

 แทนที่`"Your Document Directory"` ด้วยเส้นทางจริงที่คุณต้องการบันทึกไฟล์ Excel ของคุณ 

## ขั้นตอนที่ 2: สร้างวัตถุเวิร์กบุ๊ก

 ต่อไปเรามาสร้างอินสแตนซ์ของ`Workbook` ชั้นเรียนนี้จะแสดงสมุดงาน Excel ของเรา

```csharp
// การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

ที่นี่ เรากำลังเข้าถึงเวิร์กชีตแรกในเวิร์กบุ๊กของเรา ง่ายมาก!

## ขั้นตอนที่ 3: เพิ่มการจัดรูปแบบตามเงื่อนไข

ตอนนี้เราจะเพิ่มการจัดรูปแบบตามเงื่อนไข ซึ่งจะทำให้เราสามารถระบุได้ว่าเซลล์ใดจะมีเส้นขอบตามเงื่อนไขบางประการ 

```csharp
// เพิ่มการจัดรูปแบบเงื่อนไขแบบว่างเปล่า
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

## ขั้นตอนที่ 4: ตั้งค่าช่วงรูปแบบตามเงื่อนไข

เรามากำหนดช่วงของเซลล์ที่เราต้องการใช้การจัดรูปแบบตามเงื่อนไขกัน ในกรณีนี้ เราจะใช้ช่วงที่ครอบคลุมแถว 0 ถึง 5 และคอลัมน์ 0 ถึง 3:

```csharp
// กำหนดช่วงรูปแบบตามเงื่อนไข
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 5;
ca.StartColumn = 0;
ca.EndColumn = 3;
fcs.AddArea(ca);
```

## ขั้นตอนที่ 5: เพิ่มเงื่อนไข

ตอนนี้เราจะเพิ่มเงื่อนไขในการจัดรูปแบบ ในตัวอย่างนี้ เราจะนำการจัดรูปแบบไปใช้กับเซลล์ที่มีค่าระหว่าง 50 ถึง 100:

```csharp
// เพิ่มเงื่อนไข.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

## ขั้นตอนที่ 6: ปรับแต่งสไตล์ขอบ

เมื่อตั้งค่าเงื่อนไขแล้ว เราจะปรับแต่งรูปแบบเส้นขอบได้ ต่อไปนี้คือวิธีที่เราจะตั้งค่าเส้นขอบทั้งสี่ให้เป็นเส้นประ:

```csharp
// ตั้งค่าสีพื้นหลัง
FormatCondition fc = fcs[conditionIndex];
fc.Style.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Dashed;
fc.Style.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Dashed;
fc.Style.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Dashed;
fc.Style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Dashed;
```

## ขั้นตอนที่ 7: ตั้งค่าสีเส้นขอบ

เราสามารถกำหนดสีให้กับแต่ละเส้นขอบได้ด้วย ลองกำหนดสีฟ้าให้กับเส้นขอบซ้าย ด้านขวา และด้านบน และสีเหลืองให้กับเส้นขอบด้านล่าง:

```csharp
fc.Style.Borders[BorderType.LeftBorder].Color = Color.FromArgb(0, 255, 255);
fc.Style.Borders[BorderType.RightBorder].Color = Color.FromArgb(0, 255, 255);
fc.Style.Borders[BorderType.TopBorder].Color = Color.FromArgb(0, 255, 255);
fc.Style.Borders[BorderType.BottomBorder].Color = Color.FromArgb(255, 255, 0);
```

## ขั้นตอนที่ 8: บันทึกสมุดงานของคุณ

สุดท้ายนี้ เรามาบันทึกสมุดงานของเรากัน โดยใช้โค้ดต่อไปนี้เพื่อบันทึกการเปลี่ยนแปลง:

```csharp
workbook.Save(dataDir + "output.xlsx");
```

 นี่จะบันทึกไฟล์ Excel ของคุณเป็น`output.xlsx` ในไดเร็กทอรีที่ระบุ 

## บทสรุป

และแล้วคุณก็ทำได้! คุณได้ตั้งค่าขอบเขตในไฟล์ Excel สำเร็จแล้วด้วยโปรแกรม Aspose.Cells สำหรับ .NET การทำให้กระบวนการนี้เป็นอัตโนมัติจะช่วยให้คุณประหยัดเวลาได้มาก โดยเฉพาะเมื่อต้องจัดการกับชุดข้อมูลขนาดใหญ่ ลองนึกภาพว่าคุณจะปรับแต่งรายงานได้โดยไม่ต้องทำอะไรเลย—นั่นคือประสิทธิภาพ

## คำถามที่พบบ่อย

### ฉันสามารถใช้ Aspose.Cells สำหรับรูปแบบไฟล์อื่นนอกเหนือจาก Excel ได้หรือไม่  
ใช่ Aspose.Cells มุ่งเน้นไปที่ Excel เป็นหลัก แต่ยังช่วยให้คุณแปลงไฟล์ Excel เป็นรูปแบบต่างๆ เช่น PDF และ HTML ได้อีกด้วย

### ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.Cells หรือไม่?  
 คุณสามารถใช้รุ่นทดลองใช้งานฟรีเพื่อทดสอบฟังก์ชันการใช้งานได้ หากต้องการใช้งานในระยะยาว คุณจะต้องซื้อใบอนุญาต ซึ่งคุณสามารถหาได้จาก[ที่นี่](https://purchase.aspose.com/buy).

### ฉันจะติดตั้ง Aspose.Cells ได้อย่างไร?  
คุณสามารถติดตั้ง Aspose.Cells ผ่าน NuGet หรือดาวน์โหลด DLL จากไซต์

### มีเอกสารประกอบใด ๆ บ้างไหม?  
 แน่นอน! คุณสามารถเข้าถึงเอกสารประกอบฉบับสมบูรณ์ได้[ที่นี่](https://reference.aspose.com/cells/net/).

### ฉันจะได้รับการสนับสนุนได้ที่ไหนหากประสบปัญหา?  
 คุณสามารถเยี่ยมชมฟอรั่มสนับสนุน Aspose หากมีคำถามหรือปัญหาใดๆ ที่คุณพบ:[ฟอรั่ม Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
