---
"description": "เรียนรู้วิธีการใช้การจัดรูปแบบตามเงื่อนไขในระหว่างการรันไทม์ใน Excel ด้วย Aspose.Cells สำหรับ .NET ในคู่มือทีละขั้นตอนที่ครอบคลุมนี้"
"linktitle": "การใช้การจัดรูปแบบตามเงื่อนไขในระหว่างการทำงานจริงใน Excel"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การใช้การจัดรูปแบบตามเงื่อนไขในระหว่างการทำงานจริงใน Excel"
"url": "/th/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การใช้การจัดรูปแบบตามเงื่อนไขในระหว่างการทำงานจริงใน Excel

## การแนะนำ

เป็นเครื่องมือที่มีประสิทธิภาพสำหรับการวิเคราะห์และแสดงภาพข้อมูล คุณลักษณะที่โดดเด่นอย่างหนึ่งของ Excel คือการจัดรูปแบบตามเงื่อนไข ซึ่งช่วยให้ผู้ใช้สามารถใช้รูปแบบการจัดรูปแบบเฉพาะกับเซลล์ตามค่าต่างๆ ของเซลล์ได้ วิธีนี้ทำให้ระบุแนวโน้มได้ง่ายขึ้น เน้นจุดข้อมูลที่สำคัญ หรือทำให้ข้อมูลอ่านง่ายขึ้น หากคุณกำลังมองหาวิธีนำการจัดรูปแบบตามเงื่อนไขไปใช้กับไฟล์ Excel ของคุณโดยการเขียนโปรแกรม คุณมาถูกที่แล้ว! ในคู่มือนี้ เราจะแนะนำวิธีการใช้การจัดรูปแบบตามเงื่อนไขในขณะรันไทม์โดยใช้ Aspose.Cells สำหรับ .NET

## ข้อกำหนดเบื้องต้น
ก่อนจะเจาะลึกโค้ด เรามาตรวจสอบก่อนว่าคุณมีทุกสิ่งที่จำเป็นในการเริ่มต้น:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว คุณสามารถใช้เวอร์ชันใดก็ได้ที่รองรับการพัฒนา .NET
2. Aspose.Cells สำหรับ .NET: คุณจะต้องติดตั้ง Aspose.Cells สำหรับ .NET คุณสามารถดาวน์โหลดได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/cells/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจชิ้นส่วนโค้ดได้ดีขึ้น
4. .NET Framework: ตรวจสอบให้แน่ใจว่าโครงการของคุณกำหนดเป้าหมายไปที่เวอร์ชันที่เข้ากันได้ของ .NET Framework

ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นแล้ว มาเริ่มส่วนสนุก ๆ กันเลย!

## แพ็คเกจนำเข้า
หากต้องการเริ่มต้นใช้งาน Aspose.Cells คุณจะต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ C# ของคุณ โดยคุณสามารถทำได้ดังนี้:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

เนมสเปซเหล่านี้จะทำให้คุณสามารถเข้าถึงคลาสและวิธีการที่จำเป็นสำหรับการจัดการไฟล์ Excel และการใช้การจัดรูปแบบตามเงื่อนไข

ตอนนี้ มาแบ่งกระบวนการการจัดรูปแบบตามเงื่อนไขออกเป็นขั้นตอนที่สามารถจัดการได้

## ขั้นตอนที่ 1: ตั้งค่าโครงการของคุณ
ขั้นแรก คุณต้องสร้างโปรเจ็กต์ C# ใหม่ใน Visual Studio ดังต่อไปนี้:

1. เปิด Visual Studio และเลือกไฟล์ > ใหม่ > โปรเจ็กต์
2. เลือกแอปคอนโซล (.NET Framework) และตั้งชื่อโครงการของคุณ
3. คลิกสร้าง

## ขั้นตอนที่ 2: เพิ่มการอ้างอิง Aspose.Cells
เมื่อตั้งค่าโครงการของคุณแล้ว คุณต้องเพิ่มการอ้างอิงไปยังไลบรารี Aspose.Cells:

1. คลิกขวาที่โครงการของคุณใน Solution Explorer
2. เลือกจัดการแพ็คเกจ NuGet
3. ค้นหา Aspose.Cells และติดตั้ง

สิ่งนี้จะทำให้คุณสามารถใช้ฟังก์ชันทั้งหมดที่มีอยู่ในไลบรารี Aspose.Cells ได้

## ขั้นตอนที่ 3: สร้างวัตถุเวิร์กบุ๊ก
ต่อไปเรามาสร้างเวิร์กบุ๊กและเวิร์กชีตใหม่ นี่คือจุดที่ความมหัศจรรย์ทั้งหมดเกิดขึ้น:

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

ในขั้นตอนนี้ เราจะกำหนดไดเรกทอรีที่จะบันทึกไฟล์ Excel สร้างเวิร์กบุ๊กใหม่ และเข้าถึงเวิร์กชีตแรก

## ขั้นตอนที่ 4: เพิ่มการจัดรูปแบบตามเงื่อนไข
ตอนนี้เรามาเพิ่มการจัดรูปแบบตามเงื่อนไขกันก่อน เราจะเริ่มต้นด้วยการสร้างวัตถุการจัดรูปแบบตามเงื่อนไขที่ว่างเปล่า:

```csharp
// เพิ่มการจัดรูปแบบเงื่อนไขแบบว่างเปล่า
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

ที่นี่ เรากำลังเพิ่มคอลเลกชันการจัดรูปแบบตามเงื่อนไขใหม่ลงในเวิร์กชีตของเรา ซึ่งจะมีกฎการจัดรูปแบบของเรา

## ขั้นตอนที่ 5: กำหนดช่วงรูปแบบ
ต่อไปเราต้องระบุช่วงของเซลล์ที่จะใช้การจัดรูปแบบตามเงื่อนไข สมมติว่าเราต้องการจัดรูปแบบแถวแรกและคอลัมน์ที่สอง:

```csharp
// กำหนดช่วงรูปแบบตามเงื่อนไข
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

ในโค้ดนี้ เราจะกำหนดพื้นที่สองแห่งสำหรับการจัดรูปแบบตามเงื่อนไข พื้นที่แรกสำหรับเซลล์ที่ (0,0) และพื้นที่ที่สองสำหรับ (1,1) คุณสามารถปรับเปลี่ยนช่วงเหล่านี้ได้ตามความต้องการเฉพาะของคุณ!

## ขั้นตอนที่ 6: เพิ่มเงื่อนไขการจัดรูปแบบตามเงื่อนไข
ตอนนี้ถึงเวลาที่จะกำหนดเงื่อนไขสำหรับการจัดรูปแบบของเราแล้ว สมมติว่าเราต้องการเน้นเซลล์ตามค่าของเซลล์:

```csharp
// เพิ่มเงื่อนไข.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// เพิ่มเงื่อนไข.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

ในขั้นตอนนี้ เราจะเพิ่มเงื่อนไขสองประการ: หนึ่งสำหรับค่าระหว่าง `A2` และ `100`และอีกอันสำหรับค่าระหว่าง `50` และ `100`สิ่งนี้ช่วยให้คุณเน้นสีเซลล์แบบไดนามิกตามค่าต่างๆ ได้

## ขั้นตอนที่ 7: ตั้งค่ารูปแบบการจัดรูปแบบ
เมื่อกำหนดเงื่อนไขเรียบร้อยแล้ว ตอนนี้เราสามารถกำหนดรูปแบบการจัดรูปแบบได้แล้ว มาเปลี่ยนสีพื้นหลังของเงื่อนไขกัน:

```csharp
// ตั้งค่าสีพื้นหลัง
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

ที่นี่ เรากำลังตั้งค่าสีพื้นหลังของเงื่อนไขแรกเป็นสีแดง คุณสามารถปรับแต่งเพิ่มเติมได้โดยเปลี่ยนสีแบบอักษร ขอบ และรูปแบบอื่นๆ ตามต้องการ!

## ขั้นตอนที่ 8: บันทึกไฟล์ Excel
ในที่สุดก็ได้เวลาบันทึกงานของเราแล้ว! เราจะบันทึกสมุดงานไปยังไดเร็กทอรีที่ระบุ:

```csharp
// การบันทึกไฟล์ Excel
workbook.Save(dataDir + "output.xls");
```

โค้ดบรรทัดนี้จะบันทึกไฟล์ Excel โดยใช้การจัดรูปแบบตามเงื่อนไข ตรวจสอบให้แน่ใจว่าได้ตรวจสอบไดเร็กทอรีที่ระบุสำหรับไฟล์เอาต์พุตของคุณแล้ว!

## บทสรุป
และแล้วคุณก็ทำได้! คุณได้ใช้การจัดรูปแบบตามเงื่อนไขในระหว่างการทำงานจริงใน Excel โดยใช้ Aspose.Cells สำหรับ .NET สำเร็จแล้ว ไลบรารีอันทรงพลังนี้ทำให้การจัดการไฟล์ Excel ด้วยโปรแกรมเป็นเรื่องง่าย ช่วยให้คุณสามารถทำงานที่น่าเบื่อโดยอัตโนมัติและปรับปรุงการนำเสนอข้อมูลของคุณ ไม่ว่าคุณจะทำงานในโปรเจ็กต์ขนาดเล็กหรือแอปพลิเคชันขนาดใหญ่ Aspose.Cells ก็สามารถช่วยให้คุณปรับกระบวนการทำงานของคุณให้มีประสิทธิภาพและเพิ่มประสิทธิภาพการทำงานของคุณได้

## คำถามที่พบบ่อย

### Aspose.Cells คืออะไร?
Aspose.Cells คือไลบรารี .NET ที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงไฟล์ Excel ได้โดยการใช้โปรแกรม

### ฉันสามารถใช้ Aspose.Cells กับภาษาการเขียนโปรแกรมอื่นได้หรือไม่
ใช่ Aspose.Cells สามารถรองรับภาษาการเขียนโปรแกรมหลายภาษา รวมถึง Java, Python และอื่นๆ อีกมากมาย

### มีรุ่นทดลองใช้งานฟรีสำหรับ Aspose.Cells หรือไม่
ใช่ คุณสามารถดาวน์โหลดรุ่นทดลองใช้งานฟรีได้จาก [เว็บไซต์อาโพส](https://releases-aspose.com/).

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้อย่างไร?
คุณสามารถรับการสนับสนุนได้โดยการเยี่ยมชม [ฟอรั่มสนับสนุน Aspose](https://forum-aspose.com/c/cells/9).

### ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.Cells หรือไม่?
ใช่ ต้องมีใบอนุญาตสำหรับการใช้งานเชิงพาณิชย์ แต่คุณสามารถขอใบอนุญาตชั่วคราวได้ [ที่นี่](https://purchase-aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}