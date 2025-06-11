---
"date": "2025-04-05"
"description": "เรียนรู้วิธีการสร้างแผนภูมิอัตโนมัติใน Excel ด้วย Aspose.Cells สำหรับ .NET คู่มือนี้ครอบคลุมถึงการสร้างเวิร์กบุ๊ก การเพิ่มข้อมูล การกำหนดค่าแผนภูมิ และการบันทึกไฟล์"
"title": "วิธีการสร้างแผนภูมิใน Excel โดยใช้ Aspose.Cells สำหรับ .NET คู่มือสำหรับนักพัฒนา"
"url": "/th/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# วิธีการสร้างแผนภูมิใน Excel โดยใช้ Aspose.Cells สำหรับ .NET: คู่มือสำหรับนักพัฒนา

## การแนะนำ

ในโลกปัจจุบันที่ข้อมูลถูกขับเคลื่อน การแสดงข้อมูลในรูปแบบแผนภูมิถือเป็นสิ่งสำคัญสำหรับการตีความชุดข้อมูลที่ซับซ้อนอย่างรวดเร็ว การสร้างภาพเหล่านี้ด้วยตนเองอาจใช้เวลานานและอาจเกิดข้อผิดพลาดได้ ด้วย Aspose.Cells สำหรับ .NET คุณสามารถทำให้กระบวนการนี้เป็นแบบอัตโนมัติภายในแอปพลิเคชันของคุณได้ บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับขั้นตอนต่างๆ ในการสร้างแผนภูมิ Excel โดยใช้ Aspose.Cells สำหรับ .NET ซึ่งเป็นไลบรารีที่มีประสิทธิภาพที่ช่วยลดความซับซ้อนของงานจัดการเอกสารอัตโนมัติ

**สิ่งที่คุณจะได้เรียนรู้:**
- การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก
- การเพิ่มค่าตัวอย่างและข้อมูลหมวดหมู่ในเซลล์
- การสร้างและกำหนดค่าแผนภูมิในเวิร์กชีต
- การตั้งค่าคอลเลกชันซีรีส์ด้วยแหล่งข้อมูลที่เหมาะสม
- การบันทึกสมุดงาน Excel ที่ปรับเปลี่ยนแล้ว

มาสำรวจว่า Aspose.Cells สำหรับ .NET ช่วยปรับปรุงแอปพลิเคชันของคุณด้วยความสามารถในการสร้างแผนภูมิแบบไดนามิกได้อย่างไร

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณได้รับการตั้งค่าอย่างถูกต้อง คุณจะต้องมี:
- **Aspose.Cells สำหรับไลบรารี .NET**: เวอร์ชัน 22.x หรือใหม่กว่า
- เวอร์ชัน .NET Framework ที่เข้ากันได้ (4.5+)
- ติดตั้ง Visual Studio บนเครื่องของคุณ

**ข้อกำหนดความรู้เบื้องต้น:**
- ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม C# และ .NET
- ความคุ้นเคยกับเอกสาร Excel และแนวคิดแผนภูมิ

## การตั้งค่า Aspose.Cells สำหรับ .NET

ในการเริ่มต้น ให้ติดตั้งไลบรารี Aspose.Cells ในโปรเจ็กต์ของคุณ มีสองวิธีในการดำเนินการดังนี้:

### การใช้ .NET CLI:
```bash
dotnet add package Aspose.Cells
```

### การใช้คอนโซลตัวจัดการแพ็คเกจ:
```powershell
PM> Install-Package Aspose.Cells
```

**การได้มาซึ่งใบอนุญาต:**
หากต้องการใช้ Aspose.Cells ให้เริ่มด้วยการทดลองใช้งานฟรีโดยดาวน์โหลดจาก [เว็บไซต์อาโพส](https://releases.aspose.com/cells/net/)หากต้องการคุณสมบัติเพิ่มเติมโดยไม่มีข้อจำกัด โปรดพิจารณาซื้อใบอนุญาตหรือสมัครใบอนุญาตชั่วคราว

### การเริ่มต้นขั้นพื้นฐาน:
ต่อไปนี้เป็นวิธีการเริ่มต้นและตั้งค่าเวิร์กบุ๊กแรกของคุณโดยใช้ Aspose.Cells:

```csharp
using Aspose.Cells;

// สร้างวัตถุเวิร์กบุ๊กใหม่
tWorkbook workbook = new tWorkbook();
```

## คู่มือการใช้งาน

มาแยกกระบวนการสร้างแผนภูมิใน Excel โดยใช้ Aspose.Cells สำหรับ .NET ออกเป็นฟีเจอร์ที่แตกต่างกัน

### การสร้างอินสแตนซ์ของวัตถุเวิร์กบุ๊ก

**ภาพรวม:** เริ่มต้นด้วยการสร้างอินสแตนซ์ของ `Workbook` คลาสที่แสดงไฟล์ Excel ของคุณ นี่คือขั้นตอนพื้นฐานสำหรับงานจัดการเอกสารใดๆ

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

// สร้างวัตถุเวิร์กบุ๊กใหม่
Workbook workbook = new Workbook();
```

### การเพิ่มค่าตัวอย่างลงในเซลล์

**ภาพรวม:** เติมข้อมูลตัวอย่างลงในเวิร์กชีตของคุณ ขั้นตอนนี้เกี่ยวข้องกับการป้อนค่าตัวเลขและสตริงลงในเซลล์ที่ระบุ

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// เพิ่มค่าตัวอย่างลงในเวิร์กชีต
worksheet.Cells["A1"].PutValue(10);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(170);
worksheet.Cells["A4"].PutValue(200);
worksheet.Cells["B1"].PutValue(120);
worksheet.Cells["B2"].PutValue(320);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(40);
```

### การตั้งค่าหมวดหมู่ข้อมูลในเซลล์

**ภาพรวม:** ตั้งค่าป้ายกำกับหมวดหมู่สำหรับชุดแผนภูมิของคุณ ข้อมูลนี้จะใช้ในการติดป้ายกำกับส่วนต่างๆ ของแผนภูมิของคุณ

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// ตั้งค่าข้อมูลหมวดหมู่สำหรับป้ายแผนภูมิ
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

### การเพิ่มแผนภูมิลงในเวิร์กชีต

**ภาพรวม:** เพิ่มวัตถุแผนภูมิลงในเวิร์กชีตของคุณ บทช่วยสอนนี้เน้นที่การสร้างแผนภูมิคอลัมน์ แต่ Aspose.Cells รองรับแผนภูมิหลายประเภท

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// เพิ่มแผนภูมิคอลัมน์ลงในเวิร์กชีต
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

### การเพิ่ม SeriesCollection ลงในแผนภูมิ

**ภาพรวม:** กำหนดแหล่งที่มาของข้อมูลสำหรับแผนภูมิของคุณ ซึ่งเกี่ยวข้องกับการระบุเซลล์ที่มีข้อมูลที่จะนำมาพล็อต

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];

// เพิ่มแหล่งข้อมูลลงในแผนภูมิ
chart.NSeries.Add("A1:B4", true);
```

### การตั้งค่าหมวดหมู่ข้อมูลสำหรับ SeriesCollection

**ภาพรวม:** เชื่อมโยงป้ายหมวดหมู่ของคุณกับแผนภูมิ ขั้นตอนนี้จะช่วยให้แน่ใจว่าแต่ละชุดในแผนภูมิของคุณได้รับการติดป้ายอย่างถูกต้อง

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];

// ตั้งค่าข้อมูลหมวดหมู่สำหรับซีรีส์
chart.NSeries.Add("A1:B4", true);
chart.NSeries.CategoryData = "C1:C4";
```

### การบันทึกไฟล์ Excel

**ภาพรวม:** สุดท้าย ให้บันทึกสมุดงานของคุณเพื่อคงการเปลี่ยนแปลงทั้งหมดไว้ ขั้นตอนนี้มีความสำคัญเพื่อให้แน่ใจว่าแผนภูมิและการปรับเปลี่ยนข้อมูลของคุณยังคงอยู่

```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];

// บันทึกสมุดงาน
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

## การประยุกต์ใช้งานจริง

1. **การรายงานทางการเงิน:** สร้างรายงานทางการเงินรายไตรมาสโดยอัตโนมัติพร้อมแผนภูมิแบบไดนามิกที่แสดงรายรับและรายจ่าย
2. **การจัดการโครงการ:** แสดงภาพกำหนดเวลาของโครงการและการจัดสรรทรัพยากรเพื่อปรับปรุงประสิทธิภาพของทีม
3. **การวิเคราะห์การขาย:** สร้างแดชบอร์ดประสิทธิภาพการขายที่อัปเดตแบบเรียลไทม์เมื่อมีการป้อนข้อมูลใหม่

## การพิจารณาประสิทธิภาพ

- **เพิ่มประสิทธิภาพการโหลดข้อมูล:** โหลดเฉพาะช่วงข้อมูลที่จำเป็นเพื่อลดการใช้หน่วยความจำ
- **ประเภทแผนภูมิที่มีประสิทธิภาพ:** เลือกประเภทแผนภูมิที่เหมาะสมสำหรับข้อมูลของคุณเพื่อเพิ่มความสามารถในการอ่านและความเร็วในการประมวลผล
- **การจัดการหน่วยความจำ:** กำจัดสิ่งของขนาดใหญ่ทันทีหลังใช้งานเพื่อประหยัดทรัพยากร

## บทสรุป

ตอนนี้คุณได้เรียนรู้วิธีการสร้าง กำหนดค่า และบันทึกแผนภูมิใน Excel โดยใช้ Aspose.Cells สำหรับ .NET แล้ว ไลบรารีอันทรงพลังนี้ช่วยให้นักพัฒนาสามารถทำงานเอกสารที่ซับซ้อนได้อย่างอัตโนมัติและมีประสิทธิภาพ เรียนรู้คุณลักษณะอื่นๆ ของ Aspose.Cells ต่อไปเพื่อปรับปรุงแอปพลิเคชันของคุณให้ดียิ่งขึ้น

**ขั้นตอนต่อไป:**
- ทดลองใช้แผนภูมิประเภทต่างๆ
- บูรณาการฟังก์ชันนี้เข้ากับโปรเจ็กต์หรือเวิร์กโฟลว์ที่ใหญ่กว่า

นำเทคนิคเหล่านี้ไปใช้ในโครงการถัดไปของคุณและดูว่าเทคนิคเหล่านี้สามารถปรับปรุงเวิร์กโฟลว์ของคุณได้อย่างไร!

## ส่วนคำถามที่พบบ่อย

1. **Aspose.Cells สำหรับ .NET คืออะไร?**
   - เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถจัดการเอกสาร Excel ด้วยโปรแกรมโดยไม่จำเป็นต้องติดตั้ง Microsoft Office
2. **ฉันสามารถใช้ Aspose.Cells สำหรับโครงการเชิงพาณิชย์ได้หรือไม่**
   - ใช่ แต่คุณจะต้องซื้อใบอนุญาตหรือสมัครใบอนุญาตชั่วคราวจากเว็บไซต์ Aspose
3. **Aspose.Cells รองรับแผนภูมิประเภท Excel ทั้งหมดหรือไม่**
   - ใช่ รองรับแผนภูมิประเภทต่างๆ มากมาย เช่น แผนภูมิคอลัมน์ แผนภูมิเส้น แผนภูมิวงกลม และอื่นๆ อีกมากมาย
4. **ภาษาโปรแกรมอะไรบ้างที่สามารถใช้กับ Aspose.Cells ได้?**
   - รองรับ C# และ VB.NET เป็นหลัก แต่ยังมี API สำหรับ Java, Python และภาษาอื่นๆ อีกด้วย

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}