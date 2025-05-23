---
"description": "เรียนรู้การสร้างตารางสรุปข้อมูลด้วยโปรแกรมใน .NET โดยใช้ Aspose.Cells พร้อมคำแนะนำทีละขั้นตอนของเรา วิเคราะห์ข้อมูลของคุณอย่างมีประสิทธิภาพ"
"linktitle": "สร้างตารางสรุปข้อมูลใหม่ด้วยโปรแกรมใน .NET"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "สร้างตารางสรุปข้อมูลใหม่ด้วยโปรแกรมใน .NET"
"url": "/th/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้างตารางสรุปข้อมูลใหม่ด้วยโปรแกรมใน .NET

## การแนะนำ
การสร้างตารางสรุปข้อมูลอาจดูเหมือนเป็นงานที่น่ากลัว โดยเฉพาะอย่างยิ่งเมื่อคุณทำโดยใช้โปรแกรม แต่ไม่ต้องกังวล! ด้วย Aspose.Cells สำหรับ .NET การสร้างตารางสรุปข้อมูลไม่เพียงแต่จะตรงไปตรงมาเท่านั้น แต่ยังมีประสิทธิภาพมากสำหรับการวิเคราะห์ข้อมูลอีกด้วย ในบทช่วยสอนนี้ เราจะแนะนำคุณทีละขั้นตอนเกี่ยวกับวิธีการสร้างตารางสรุปข้อมูลใหม่ในแอปพลิเคชัน .NET ไม่ว่าคุณจะเพิ่มข้อมูลสำหรับการขาย กีฬา หรือตัวชี้วัดทางธุรกิจอื่นๆ คู่มือนี้จะช่วยให้คุณสร้างตารางสรุปข้อมูลได้ในเวลาไม่นาน

## ข้อกำหนดเบื้องต้น
ก่อนจะเริ่มลงมือ เรามาตรวจสอบกันก่อนว่าคุณเตรียมทุกอย่างพร้อมแล้ว นี่คือสิ่งที่คุณต้องทำ:

1. ติดตั้ง .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET framework ไว้ในเครื่องของคุณแล้ว Aspose.Cells รองรับเวอร์ชันต่างๆ มากมาย แต่ควรใช้เวอร์ชันล่าสุดจะดีกว่า
2. ไลบรารี Aspose.Cells: คุณต้องมีไลบรารี Aspose.Cells คุณสามารถ [ดาวน์โหลดได้ที่นี่](https://releases.aspose.com/cells/net/) หรือรับ [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) เพื่อการประเมินผล
3. การตั้งค่า IDE: เตรียม IDE ที่เข้ากันได้กับ C# เช่น Visual Studio ซึ่งคุณสามารถเริ่มโปรเจ็กต์ใหม่ได้
4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณทำตามได้โดยไม่ต้องติดขัดมากเกินไป

คุณพร้อมแล้วหรือยัง? เยี่ยมเลย! มาเริ่มนำเข้าแพ็คเกจที่จำเป็นกันเลย

## แพ็คเกจนำเข้า
ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นไปยังโปรเจ็กต์ C# ของคุณ เปิดไฟล์ C# และเพิ่มคำสั่งต่อไปนี้:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

เนมสเปซเหล่านี้ช่วยให้คุณเข้าถึงฟังก์ชันการทำงานของเวิร์กบุ๊ก เวิร์กชีต และตารางสรุปข้อมูลที่เราจะใช้ตลอดบทช่วยสอนนี้

## ขั้นตอนที่ 1: สร้างวัตถุเวิร์กบุ๊ก
การสร้างเวิร์กบุ๊กเป็นจุดเริ่มต้นของการเดินทางของคุณ เริ่มต้นด้วยการสร้างเวิร์กบุ๊กใหม่และเข้าถึงเวิร์กชีตแรก

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
// การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
Workbook workbook = new Workbook();

// การรับข้อมูลอ้างอิงของแผ่นงานที่เพิ่มใหม่
Worksheet sheet = workbook.Worksheets[0];
```

ในขั้นตอนนี้เราจะสร้าง `Workbook` อินสแตนซ์ที่แสดงไฟล์ Excel ของเราและคว้าเวิร์กชีตแรกซึ่งจะเป็นสนามเด็กเล่นสำหรับตารางสรุปข้อมูลของเรา

## ขั้นตอนที่ 2: แทรกข้อมูลลงในเซลล์
ต่อไปเรามาเติมข้อมูลตัวอย่างลงในเวิร์กชีตของเรา เราจะป้อนแถวสำหรับตัวเลขกีฬา ไตรมาส และยอดขายต่างๆ เพื่อให้ตารางสรุปข้อมูลมีข้อมูลไว้สรุป

```csharp
Cells cells = sheet.Cells;

// การกำหนดค่าให้กับเซลล์
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// การเติมข้อมูลเซลล์ = cells["A2"];
cell.PutValue("Golf");
// ... ข้อมูลเพิ่มเติม
```

ที่นี่ เราจะกำหนดส่วนหัวของคอลัมน์และแทรกค่าภายใต้ส่วนหัวแต่ละส่วน ข้อมูลนี้จะทำหน้าที่เป็นแหล่งที่มาของตารางสรุปข้อมูล ดังนั้นโปรดตรวจสอบให้แน่ใจว่ามีการจัดระเบียบอย่างดี ปฏิบัติตามบล็อกนี้ แล้วคุณจะสร้างชุดข้อมูลที่ครอบคลุม

## ขั้นตอนที่ 3: การเพิ่มตารางสรุปข้อมูล
เมื่อข้อมูลพร้อมแล้ว ก็ถึงเวลาสร้างตารางสรุปข้อมูล เราจะใช้คอลเลกชันตารางสรุปข้อมูลจากเวิร์กชีตเพื่อเพิ่มตารางสรุปข้อมูลใหม่

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// การเพิ่ม PivotTable ลงในเวิร์กชีต
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

ในสไนปเป็ตนี้ เราเพิ่มตารางสรุปข้อมูลลงในเวิร์กชีตซึ่งอ้างอิงช่วงข้อมูลของเรา (ในกรณีนี้คือเซลล์ A1 ถึง C8) เราวางตารางสรุปข้อมูลโดยเริ่มจากเซลล์ E3 และตั้งชื่อว่า "PivotTable2" ง่ายใช่ไหมล่ะ

## ขั้นตอนที่ 4: ปรับแต่งตารางสรุปข้อมูล
ตอนนี้เรามีตารางสรุปข้อมูลแล้ว มาปรับแต่งตารางให้แสดงข้อมูลสรุปที่มีความหมายกันดีกว่า เราสามารถควบคุมสิ่งที่จะปรากฏในแถว คอลัมน์ และพื้นที่ข้อมูลของตารางสรุปข้อมูลได้

```csharp
// การเข้าถึงอินสแตนซ์ของ PivotTable ที่เพิ่มเข้ามาใหม่
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// ไม่แสดงผลรวมทั้งหมดของแถว
pivotTable.RowGrand = false;

// การลากฟิลด์แรกไปยังพื้นที่แถว
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// การลากฟิลด์ที่ 2 ไปยังพื้นที่คอลัมน์
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// การลากฟิลด์ที่สามไปยังพื้นที่ข้อมูล
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

ในขั้นตอนนี้ เราจะสั่งให้ตารางสรุปข้อมูลซ่อนยอดรวมทั้งหมดสำหรับแถว จากนั้นจึงระบุฟิลด์ที่จะใส่ในแถว คอลัมน์ และพื้นที่ข้อมูล ชื่อกีฬาจะใส่ในแถว ไตรมาสจะใส่ในคอลัมน์ และตัวเลขยอดขายจะให้ข้อมูลสรุป

## ขั้นตอนที่ 5: บันทึกสมุดงาน
ในที่สุดเราต้องการบันทึกสมุดงานที่เราสร้างขึ้นใหม่เพื่อดูผลงานจากการทำงานของเรา

```csharp
// การบันทึกไฟล์ Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

เพียงระบุเส้นทางที่เหมาะสม แล้วคุณจะมีผลลัพธ์ตารางสรุปข้อมูลถูกบันทึกลงในไฟล์ Excel ที่คุณสามารถเปิดและตรวจสอบได้

## บทสรุป
การสร้างตารางสรุปข้อมูลด้วยโปรแกรม Aspose.Cells สำหรับ .NET จะช่วยประหยัดเวลาของคุณได้อย่างมาก โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการกับชุดข้อมูลขนาดใหญ่ คุณได้เรียนรู้วิธีการตั้งค่าโครงการ นำเข้าแพ็กเกจที่จำเป็น เติมข้อมูล และสร้างตารางสรุปข้อมูลแบบกำหนดเองได้ตั้งแต่ต้น ดังนั้น ครั้งต่อไปที่คุณต้องจมอยู่กับตัวเลข ให้จำบทช่วยสอนนี้ไว้และให้ Aspose.Cells จัดการงานหนักๆ แทนคุณ

## คำถามที่พบบ่อย
### Aspose.Cells คืออะไร?
Aspose.Cells เป็นไลบรารี .NET อันทรงพลังสำหรับการสร้างและจัดการสเปรดชีต Excel ด้วยโปรแกรม

### มีการทดลองใช้ Aspose.Cells ฟรีหรือไม่
ใช่ คุณสามารถรับการทดลองใช้ฟรีได้ [ที่นี่](https://releases-aspose.com/).

### ฉันสามารถปรับแต่งลักษณะของตารางสรุปข้อมูลได้หรือไม่
แน่นอน! คุณสามารถปรับแต่งรูปแบบ เค้าโครง และแม้แต่สไตล์ของตารางสรุปข้อมูลตามความต้องการของคุณได้

### ฉันสามารถหาตัวอย่างและเอกสารเพิ่มเติมเกี่ยวกับ Aspose.Cells ได้จากที่ใด
คุณสามารถตรวจสอบได้ [เอกสารประกอบ](https://reference.aspose.com/cells/net/) สำหรับคำแนะนำและตัวอย่างที่ครอบคลุม

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.Cells ได้อย่างไร
คุณสามารถรับการสนับสนุนได้ผ่านทาง [ฟอรั่ม Aspose](https://forum-aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}