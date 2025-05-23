---
"description": "สร้างแผนภูมิเส้นที่สวยงามโดยใช้ Aspose.Cells สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อสร้างภาพข้อมูลของคุณอย่างมีประสิทธิภาพ"
"linktitle": "การสร้างแผนภูมิเส้น"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "การสร้างแผนภูมิเส้น"
"url": "/th/net/manipulating-chart-types/create-line-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การสร้างแผนภูมิเส้น

## การแนะนำ

คุณพร้อมที่จะแสดงข้อมูลของคุณให้ชัดเจนขึ้นหรือยัง แผนภูมิเส้นเป็นวิธีที่ยอดเยี่ยมในการแสดงแนวโน้มในช่วงเวลาหนึ่งหรือความสัมพันธ์ระหว่างตัวแปรสองตัว ไม่ว่าคุณจะจัดการข้อมูลสำหรับโครงการธุรกิจหรือวิเคราะห์เมตริกส่วนบุคคล ความสามารถในการสร้างแผนภูมิเส้นด้วยโปรแกรมสามารถช่วยประหยัดเวลาและเพิ่มความคล่องตัวมากขึ้น ในคู่มือนี้ เราจะแนะนำคุณทีละขั้นตอนในการสร้างแผนภูมิเส้นโดยใช้ Aspose.Cells สำหรับ .NET พร้อมหรือยังที่จะลงมือทำ เริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มลงรายละเอียดในการสร้างแผนภูมิเส้น เรามาตรวจสอบกันก่อนว่าคุณพร้อมที่จะทำตามหรือไม่:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio บนเครื่องของคุณแล้ว เนื่องจากเป็นหนึ่งใน IDE ยอดนิยมที่สุดสำหรับการพัฒนา .NET
2. Aspose.Cells สำหรับไลบรารี .NET: คุณจะต้องมีไลบรารี Aspose.Cells ซึ่งคุณสามารถดาวน์โหลดได้จาก [ที่นี่](https://releases-aspose.com/cells/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจตัวอย่างและชิ้นส่วนโค้ดได้ดีขึ้น
4. .NET Framework หรือ .NET Core: การตั้งค่าพื้นฐานของกรอบงานใดกรอบหนึ่ง เนื่องจากจะเป็นรากฐานสำหรับแอปพลิเคชันของเรา

เมื่อคุณได้จัดการข้อกำหนดเบื้องต้นเหล่านี้เรียบร้อยแล้ว คุณก็พร้อมที่จะสร้างแผนภูมิได้แล้ว!

## แพ็คเกจนำเข้า

ตอนนี้เราได้ตั้งค่าสภาพแวดล้อมของเราเรียบร้อยแล้ว เราจำเป็นต้องนำเข้าแพ็คเกจที่จำเป็นในโค้ด C# ของเรา เช่นเดียวกับการรวบรวมเครื่องมือก่อนเริ่มโปรเจ็กต์ การนำเข้าแพ็คเกจมีความจำเป็นเพื่อให้แน่ใจว่าคุณมีทุกสิ่งที่คุณต้องการ

นี่คือวิธีการทำ:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

สายนี้นำเข้า `Aspose.Cells` เนมสเปซซึ่งมีคลาสและเมธอดทั้งหมดที่เราจะใช้ในการสร้างแผนภูมิเส้น

ตอนนี้เรามาแบ่งกระบวนการทั้งหมดออกเป็นขั้นตอนง่ายๆ ที่เข้าใจง่าย แต่ละขั้นตอนจะแนะนำคุณตลอดกระบวนการสร้างแผนภูมิเส้นโดยใช้ Aspose.Cells สำหรับ .NET

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอาต์พุต

ขั้นตอนแรกคือการกำหนดว่าคุณต้องการบันทึกไฟล์เอาต์พุตของคุณไว้ที่ใด ซึ่งก็เหมือนกับการตั้งค่าพื้นที่ทำงานของคุณก่อนจะเริ่มลงมือทำงาน 

```csharp
// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Output Directory";
```
แทนที่ `"Your Output Directory"` ด้วยเส้นทางจริงที่คุณต้องการบันทึกไฟล์ Excel ที่สร้างขึ้น

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก

ขั้นต่อไป เราต้องสร้างอินสแตนซ์เวิร์กบุ๊กใหม่ ลองนึกถึงเวิร์กบุ๊กเป็นผืนผ้าใบที่ความคิดสร้างสรรค์ของคุณจะไหลลื่น 

```csharp
// การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
Workbook workbook = new Workbook();
```
บรรทัดนี้จะเริ่มต้นเวิร์กบุ๊กใหม่ที่จะเก็บข้อมูลและภาพทั้งหมดของคุณ

## ขั้นตอนที่ 3: เข้าถึงแผ่นงาน

ในเวิร์กบุ๊กที่เราเพิ่งสร้างขึ้น เราจำเป็นต้องได้รับการอ้างอิงถึงเวิร์กชีตที่เราจะป้อนข้อมูล หากเวิร์กบุ๊กเป็นผืนผ้าใบ เวิร์กชีตก็จะเป็นจานสีของเรา

```csharp
// การรับข้อมูลอ้างอิงของเวิร์กชีตที่เพิ่มใหม่โดยส่งดัชนีชีตของมัน
Worksheet worksheet = workbook.Worksheets[0];
```
ที่นี่เราเข้าถึงแผ่นงานแรก (ดัชนี `0`-

## ขั้นตอนที่ 4: เพิ่มค่าตัวอย่างลงในเซลล์

ตอนนี้มาถึงส่วนสนุกแล้ว! เราจะใส่ค่าตัวอย่างลงในเวิร์กชีต ข้อมูลนี้จะทำหน้าที่เป็นพื้นฐานสำหรับแผนภูมิเส้นของเรา 

```csharp
// การเพิ่มค่าตัวอย่างลงในเซลล์
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
ในสไนปเป็ตนี้ เราจะเพิ่มค่าให้กับเซลล์ในคอลัมน์ A และ B โดยคอลัมน์ A แทนค่าแกน X ในขณะที่คอลัมน์ B แทนค่าแกน Y

## ขั้นตอนที่ 5: เพิ่มแผนภูมิเส้นลงในเวิร์กชีต

ต่อไปเราจะแนะนำแผนภูมิเส้นให้กับเวิร์กชีต นี่คือจุดที่ข้อมูลของคุณจะมีชีวิตชีวาอย่างแท้จริง!

```csharp
// การเพิ่มแผนภูมิลงในเวิร์กชีต
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
ที่นี่ เราเพิ่มแผนภูมิเส้นในตำแหน่งที่ระบุ พารามิเตอร์ (5, 0, 25, 10) จะกำหนดตำแหน่งและขนาดของแผนภูมิภายในเวิร์กชีต

## ขั้นตอนที่ 6: เข้าถึงอินสแตนซ์แผนภูมิใหม่

เมื่อเราเพิ่มแผนภูมิแล้ว ก็ถึงเวลาที่จะได้วัตถุแผนภูมิที่สร้างขึ้นใหม่ 

```csharp
// การเข้าถึงอินสแตนซ์ของแผนภูมิที่เพิ่มใหม่
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
โค้ดนี้เชื่อมต่อเราเข้ากับแผนภูมิเพื่อให้เราสามารถปรับเปลี่ยนเพิ่มเติมได้

## ขั้นตอนที่ 7: เพิ่ม SeriesCollection ลงในแผนภูมิ

ตอนนี้เราต้องบอกแผนภูมิของเราว่าจะแสดงข้อมูลใด ในขั้นนี้ เราจะกำหนดแหล่งข้อมูลสำหรับแผนภูมิเส้นโดยการเพิ่ม SeriesCollection

```csharp
// การเพิ่ม SeriesCollection (แหล่งข้อมูลแผนภูมิ) ลงในแผนภูมิตั้งแต่เซลล์ "A1" ถึง "B3"
chart.NSeries.Add("A1:B3", true);
```
ในตัวอย่างนี้ เราแจ้งให้แผนภูมิใช้ค่าในเซลล์ A1 ถึง B3

## ขั้นตอนที่ 8: บันทึกไฟล์ Excel

รอบชิงชนะเลิศ! หลังจากที่คุณทำงานหนักมาทั้งหมดแล้ว ก็ถึงเวลาบันทึกไฟล์ Excel และดูแผนภูมิเส้นของคุณทำงาน

```csharp
// การบันทึกไฟล์ Excel
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
บรรทัดนี้จะบันทึกสมุดงานของคุณในไดเร็กทอรีเอาท์พุตที่ระบุโดยใช้ชื่อ `outputHowToCreateLineChart-xlsx`.

## ขั้นตอนที่ 9: ดำเนินการและตรวจสอบ

ในที่สุดคุณก็สามารถรันโค้ดของคุณและตรวจสอบว่าแผนภูมิเส้นได้รับการสร้างสำเร็จแล้วในไดเร็กทอรีเอาต์พุตของคุณได้แล้ว! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
ระบบจะส่งข้อความไปยังคอนโซลของคุณ เพื่อแจ้งให้คุณทราบว่าทุกอย่างดำเนินไปอย่างราบรื่น

## บทสรุป

การสร้างแผนภูมิเส้นโดยใช้ Aspose.Cells สำหรับ .NET เป็นวิธีที่มีประสิทธิภาพในการทำให้ข้อมูลของคุณมีชีวิตชีวาขึ้น ด้วยการทำตามคำแนะนำทีละขั้นตอนนี้ คุณจะสามารถแสดงแนวโน้มและความสัมพันธ์ในชุดข้อมูลของคุณได้อย่างง่ายดาย ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น Aspose.Cells มอบความยืดหยุ่นและพลังให้กับคุณเพื่อทำให้งานแสดงภาพข้อมูลของคุณเป็นแบบอัตโนมัติ 

## คำถามที่พบบ่อย

### Aspose.Cells สำหรับ .NET คืออะไร?  
Aspose.Cells สำหรับ .NET เป็นไลบรารีอันทรงพลังที่ออกแบบมาเพื่อจัดการและปรับเปลี่ยนไฟล์ Excel ด้วยโปรแกรม ช่วยให้นักพัฒนาสามารถสร้าง แก้ไข และแปลงสเปรดชีตได้

### Aspose.Cells รองรับแผนภูมิหรือไม่  
ใช่ Aspose.Cells ให้การสนับสนุนอย่างกว้างขวางสำหรับแผนภูมิประเภทต่างๆ รวมถึงแผนภูมิเส้น แผนภูมิวงกลม แผนภูมิแท่ง และอื่นๆ อีกมากมาย

### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?  
ใช่ คุณสามารถดาวน์โหลดเวอร์ชันทดลองใช้งานฟรีเพื่อสำรวจฟีเจอร์ต่างๆ ของมันได้ หากต้องการใช้งานในระยะยาว ควรพิจารณาซื้อใบอนุญาต

### มีฟอรั่มสำหรับการสนับสนุนหรือไม่?  
แน่นอน! คุณสามารถค้นหาคำตอบและถามคำถามได้ที่ [ฟอรั่ม Aspose.Cells](https://forum-aspose.com/c/cells/9).

### ฉันจะซื้อใบอนุญาตได้อย่างไร?  
สามารถซื้อใบอนุญาตได้อย่างง่ายดายผ่านทาง [หน้าการซื้อ](https://purchase-aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}