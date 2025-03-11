---
title: สร้างแผนภูมิวงกลม
linktitle: สร้างแผนภูมิวงกลม
second_title: API การประมวลผล Excel ของ Aspose.Cells .NET
description: เรียนรู้วิธีสร้างแผนภูมิวงกลมใน Excel โดยใช้ Aspose.Cells สำหรับ .NET ด้วยคู่มือทีละขั้นตอนนี้ สร้างภาพข้อมูลของคุณได้อย่างง่ายดาย
weight: 12
url: /th/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างแผนภูมิวงกลม

## การแนะนำ

การสร้างแผนภูมิถือเป็นสิ่งสำคัญสำหรับการแสดงข้อมูลในรูปแบบภาพ และแผนภูมิวงกลมเป็นหนึ่งในวิธีที่นิยมใช้กันมากที่สุดในการแสดงให้เห็นว่าส่วนต่างๆ ประกอบกันเป็นหนึ่งได้อย่างไร ด้วย Aspose.Cells สำหรับ .NET คุณสามารถสร้างแผนภูมิวงกลมในไฟล์ Excel โดยอัตโนมัติได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเจาะลึกถึงวิธีการสร้างแผนภูมิวงกลมตั้งแต่ต้นโดยใช้ Aspose.Cells สำหรับ .NET พร้อมคำแนะนำทีละขั้นตอนเพื่อให้กระบวนการนี้ราบรื่นและตรงไปตรงมา ไม่ว่าคุณจะเป็นมือใหม่ในการใช้เครื่องมือนี้หรือต้องการพัฒนาทักษะการทำงานอัตโนมัติของ Excel คู่มือนี้ครอบคลุมทุกอย่างที่คุณต้องการ!

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกโค้ด โปรดตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสิ่งต่อไปนี้แล้ว:

1.  Aspose.Cells สำหรับไลบรารี .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Aspose.Cells ไว้ในโปรเจ็กต์ของคุณแล้ว หากคุณยังไม่ได้ติดตั้ง คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/cells/net/).
2. สภาพแวดล้อมการพัฒนา .NET: ตรวจสอบให้แน่ใจว่าโครงการของคุณได้รับการตั้งค่าให้ใช้ .NET Framework หรือ .NET Core
3. ความรู้พื้นฐานเกี่ยวกับ C#: คุณควรจะคุ้นเคยกับการเขียนโปรแกรม C# โดยเฉพาะการเขียนโปรแกรมเชิงวัตถุ (OOP)

 สำหรับผู้ใช้ขั้นสูง สามารถใช้ใบอนุญาตชั่วคราวเพื่อปลดล็อกฟีเจอร์ทั้งหมดของ Aspose.Cells ได้ คุณสามารถขอใบอนุญาตได้จาก[ที่นี่](https://purchase.aspose.com/temporary-license/).

## แพ็คเกจนำเข้า

ในการเริ่มต้น ให้ทำการอิมพอร์ตเนมสเปซและแพ็กเกจที่จำเป็นสำหรับบทช่วยสอนนี้ ซึ่งรวมถึงการดำเนินการ I/O ขั้นพื้นฐานและแพ็กเกจ Aspose.Cells

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## ขั้นตอนที่ 1: สร้างสมุดงานใหม่

 ขั้นแรกเราต้องสร้างอินสแตนซ์ของ`Workbook` คลาสซึ่งแสดงถึงไฟล์ Excel เวิร์กบุ๊กประกอบด้วยแผ่นงานหลายแผ่น และสำหรับตัวอย่างของเรา เราจะทำงานกับแผ่นงานสองแผ่น แผ่นหนึ่งสำหรับข้อมูลและอีกแผ่นหนึ่งสำหรับแผนภูมิวงกลม

```csharp
Workbook workbook = new Workbook();
```

ขั้นตอนนี้จะเริ่มสร้างเวิร์กบุ๊ก Excel ใหม่ แต่ข้อมูลจะไปอยู่ที่ไหน เรามาจัดการเรื่องนี้ในขั้นตอนถัดไป

## ขั้นตอนที่ 2: เพิ่มข้อมูลลงในเวิร์กชีต

เมื่อสร้างเวิร์กบุ๊กแล้ว เราต้องเข้าถึงเวิร์กชีตแรกและตั้งชื่อ จากนั้นเราจะป้อนข้อมูลที่จำเป็นสำหรับแผนภูมิวงกลม

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

ตอนนี้เราสามารถป้อนข้อมูลการขายจำลองที่แสดงภูมิภาคต่างๆ ได้:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

ที่นี่ เรากำลังเพิ่มคอลัมน์สองคอลัมน์ คอลัมน์หนึ่งสำหรับภูมิภาคและอีกคอลัมน์สำหรับยอดขาย ข้อมูลนี้จะแสดงอยู่ในแผนภูมิวงกลม

## ขั้นตอนที่ 3: เพิ่มแผ่นแผนภูมิ

ต่อไปเราจะเพิ่มเวิร์กชีตแยกต่างหากเพื่อเก็บแผนภูมิวงกลม

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

แผ่นงานใหม่นี้จะโฮสต์แผนภูมิวงกลม การตั้งชื่อแผนภูมิวงกลม เช่น "แผนภูมิ" ช่วยให้ผู้ใช้ทราบว่าจะพบอะไรเมื่อเปิดไฟล์

## ขั้นตอนที่ 4: สร้างแผนภูมิวงกลม

ตอนนี้ถึงเวลาสร้างแผนภูมิจริงแล้ว เราจะระบุว่าเราต้องการแผนภูมิวงกลม และเราจะกำหนดตำแหน่งของแผนภูมิวงกลมบนแผ่นงาน

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 วิธีการ`Add()`ยอมรับพารามิเตอร์สำหรับประเภทแผนภูมิ (ในกรณีนี้คือ`ChartType.Pie`) และตำแหน่งบนแผ่นงาน ตัวเลขแสดงตำแหน่งแถวและคอลัมน์

## ขั้นตอนที่ 5: ปรับแต่งรูปลักษณ์ของแผนภูมิ

แผนภูมิวงกลมจะไม่สมบูรณ์หากขาดการปรับแต่งเล็กน้อย มาทำให้แผนภูมิของเราดูน่าสนใจด้วยการปรับแต่งสี ป้ายกำกับ และชื่อเรื่อง

### ตั้งค่าชื่อแผนภูมิ
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### ปรับแต่งพื้นที่แปลง
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

เราตั้งค่าการเติมไล่ระดับสำหรับพื้นที่พล็อตและซ่อนขอบเพื่อให้ดูสะอาดตา

## ขั้นตอนที่ 6: กำหนดข้อมูลแผนภูมิ

 ถึงเวลาที่จะเชื่อมโยงแผนภูมิกับข้อมูลของเราแล้ว`NSeries` คุณสมบัติของแผนภูมิจะเชื่อมโยงตัวเลขยอดขายและภูมิภาคเข้ากับแผนภูมิวงกลม

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 บรรทัดแรกระบุว่าเราใช้ข้อมูลการขายจากเซลล์`B2:B8` . เรายังบอกแผนภูมิให้ใช้ชื่อภูมิภาคจาก`A2:A8` เป็นป้ายหมวดหมู่

## ขั้นตอนที่ 7: เพิ่มป้ายข้อมูล

การเพิ่มป้ายกำกับลงในส่วนต่างๆ ของแผนภูมิโดยตรงจะช่วยให้เข้าใจข้อมูลได้ง่ายขึ้น ลองรวมชื่อภูมิภาคและมูลค่าการขายไว้ในส่วนต่างๆ ของแผนภูมิวงกลม

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## ขั้นตอนที่ 8: ปรับแต่งพื้นที่แผนภูมิและคำอธิบาย

สุดท้ายนี้ เรามาตกแต่งพื้นที่แผนภูมิและคำอธิบายภาพให้สวยงามยิ่งขึ้น ซึ่งจะทำให้การนำเสนอแผนภูมิโดยรวมดูดีขึ้น

### พื้นที่แผนภูมิ
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### ตำนาน
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## ขั้นตอนที่ 9: บันทึกสมุดงาน

ในที่สุด เราจะบันทึกเวิร์กบุ๊กลงในไฟล์ Excel คุณสามารถระบุไดเรกทอรีเอาต์พุตและชื่อไฟล์ตามต้องการ

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## บทสรุป

การสร้างแผนภูมิวงกลมด้วย Aspose.Cells สำหรับ .NET เป็นกระบวนการที่ตรงไปตรงมาและปรับแต่งได้ เมื่อทำตามคำแนะนำนี้ คุณก็สามารถสร้างแผนภูมิที่ดูเป็นมืออาชีพซึ่งแสดงข้อมูลเชิงลึกอันมีค่าได้ภายในไม่กี่ขั้นตอน ไม่ว่าจะใช้เพื่อการรายงานทางธุรกิจหรือเพื่อวัตถุประสงค์ทางการศึกษา การเรียนรู้การสร้างแผนภูมิจะช่วยเพิ่มทักษะการทำงานอัตโนมัติของ Excel ของคุณ โปรดจำไว้ว่า Aspose.Cells มอบความยืดหยุ่นที่คุณต้องการเพื่อสร้างไฟล์ Excel ที่สวยงามและขับเคลื่อนด้วยข้อมูลได้อย่างง่ายดาย

## คำถามที่พบบ่อย

### ฉันสามารถสร้างแผนภูมิประเภทอื่นโดยใช้ Aspose.Cells สำหรับ .NET ได้หรือไม่
ใช่! Aspose.Cells รองรับแผนภูมิประเภทต่างๆ รวมถึงแผนภูมิแท่ง แผนภูมิเส้น และแผนภูมิกระจาย

### ฉันต้องมีใบอนุญาตแบบชำระเงินเพื่อใช้ Aspose.Cells สำหรับ .NET หรือไม่
คุณสามารถใช้เวอร์ชันฟรีได้โดยมีข้อจำกัดบางประการ หากต้องการใช้ฟีเจอร์เต็มรูปแบบ คุณจะต้องมีใบอนุญาตซึ่งคุณสามารถซื้อได้[ที่นี่](https://purchase.aspose.com/buy).

### ฉันสามารถส่งออกแผนภูมิเป็นรูปแบบเช่น PDF หรือรูปภาพได้หรือไม่
แน่นอน! Aspose.Cells ช่วยให้คุณสามารถส่งออกแผนภูมิเป็นรูปแบบต่างๆ รวมถึง PDF และ PNG

### เป็นไปได้ไหมที่จะตกแต่งพายแต่ละชิ้นด้วยสีที่ต่างกัน?
 ใช่ คุณสามารถใช้สีที่แตกต่างกันกับแต่ละชิ้นได้โดยการตั้งค่า`IsColorVaried` ทรัพย์สินที่จะ`true`ตามที่แสดงในบทช่วยสอน

### ฉันสามารถสร้างแผนภูมิหลาย ๆ รายการแบบอัตโนมัติในสมุดงานเดียวได้หรือไม่
ใช่ คุณสามารถสร้างและปรับแต่งแผนภูมิได้มากเท่าที่ต้องการภายในไฟล์ Excel เดียว
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
