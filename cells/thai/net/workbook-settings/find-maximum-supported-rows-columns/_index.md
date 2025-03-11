---
title: ค้นหาจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS และ XLSX
linktitle: ค้นหาจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS และ XLSX
second_title: API การประมวลผล Excel ของ Aspose.Cells .NET
description: ค้นพบจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS และ XLSX โดยใช้ Aspose.Cells สำหรับ .NET เพิ่มประสิทธิภาพการจัดการข้อมูล Excel ของคุณด้วยบทช่วยสอนที่ครอบคลุมนี้
weight: 11
url: /th/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ค้นหาจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS และ XLSX

## การแนะนำ
การจัดการชุดข้อมูลขนาดใหญ่ใน Excel อาจเป็นงานที่น่าปวดหัว โดยเฉพาะอย่างยิ่งเมื่อต้องจัดการกับจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบไฟล์ต่างๆ บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการค้นหาจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS และ XLSX โดยใช้ไลบรารี Aspose.Cells สำหรับ .NET เมื่ออ่านบทความนี้จบ คุณจะเข้าใจอย่างครอบคลุมถึงวิธีใช้เครื่องมืออันทรงพลังนี้เพื่อจัดการงานที่เกี่ยวข้องกับ Excel อย่างมีประสิทธิภาพ
## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มลงลึกในบทช่วยสอน ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:
1. [กรอบงาน .NET](https://dotnet.microsoft.com/en-us/download) หรือ[.NET แกนหลัก](https://dotnet.microsoft.com/en-us/download) ติดตั้งอยู่บนระบบของคุณแล้ว
2. [Aspose.Cells สำหรับ .NET](https://releases.aspose.com/cells/net/) ไลบรารีที่ดาวน์โหลดและอ้างอิงในโครงการของคุณ
 หากคุณยังไม่ได้ดาวน์โหลดไลบรารี Aspose.Cells สำหรับ .NET จาก[เว็บไซต์](https://releases.aspose.com/cells/net/) หรือติดตั้งได้ทาง[นูเก็ต](https://www.nuget.org/packages/Aspose.Cells/).
## แพ็คเกจนำเข้า
ในการเริ่มต้น คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นจากไลบรารี Aspose.Cells สำหรับ .NET เพิ่มคำสั่ง using ต่อไปนี้ที่ด้านบนของไฟล์ C# ของคุณ:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## ขั้นตอนที่ 1: ค้นหาจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS
เริ่มต้นด้วยการสำรวจจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS (Excel 97-2003)
```csharp
// พิมพ์ข้อความเกี่ยวกับรูปแบบ XLS
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// สร้างสมุดงานในรูปแบบ XLS
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// พิมพ์จำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
ในขั้นตอนนี้เราจะ:
1. พิมพ์ข้อความเพื่อระบุว่าเรากำลังทำงานกับรูปแบบ XLS
2.  สร้างใหม่`Workbook` อินสแตนซ์ที่ใช้`FileFormatType.Excel97To2003` enum ซึ่งแสดงถึงรูปแบบ XLS
3.  ดึงข้อมูลแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS โดยใช้`Workbook.Settings.MaxRow` และ`Workbook.Settings.MaxColumn`คุณสมบัติตามลำดับ เราเพิ่ม 1 ลงในค่าเหล่านี้เพื่อรับจำนวนแถวและคอลัมน์สูงสุดที่แท้จริง (เนื่องจากเป็นค่าฐานศูนย์)
4. พิมพ์จำนวนแถวและคอลัมน์สูงสุดไปยังคอนโซล
## ขั้นตอนที่ 2: ค้นหาแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLSX
ต่อไป เรามาดูจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLSX (Excel 2007 และใหม่กว่า)
```csharp
// พิมพ์ข้อความเกี่ยวกับรูปแบบ XLSX
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// สร้างสมุดงานในรูปแบบ XLSX
wb = new Workbook(FileFormatType.Xlsx);
// พิมพ์จำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLSX
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
ในขั้นตอนนี้เราจะ:
1. พิมพ์ข้อความเพื่อระบุว่าเรากำลังทำงานกับรูปแบบ XLSX
2.  สร้างใหม่`Workbook` อินสแตนซ์ที่ใช้`FileFormatType.Xlsx` enum ซึ่งแสดงถึงรูปแบบ XLSX
3.  ดึงข้อมูลแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLSX โดยใช้`Workbook.Settings.MaxRow` และ`Workbook.Settings.MaxColumn`คุณสมบัติตามลำดับ เราเพิ่ม 1 ลงในค่าเหล่านี้เพื่อรับจำนวนแถวและคอลัมน์สูงสุดที่แท้จริง (เนื่องจากเป็นค่าฐานศูนย์)
4. พิมพ์จำนวนแถวและคอลัมน์สูงสุดไปยังคอนโซล
## ขั้นตอนที่ 3: แสดงข้อความแสดงความสำเร็จ
ในที่สุด ให้เราแสดงข้อความแจ้งความสำเร็จเพื่อระบุว่าตัวอย่าง "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" ได้รับการดำเนินการสำเร็จแล้ว
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
ขั้นตอนนี้เพียงพิมพ์ข้อความแจ้งความสำเร็จไปยังคอนโซล
## บทสรุป
ในบทช่วยสอนนี้ คุณจะได้เรียนรู้วิธีใช้ไลบรารี Aspose.Cells สำหรับ .NET เพื่อค้นหาจำนวนแถวและคอลัมน์สูงสุดที่รองรับโดยรูปแบบไฟล์ XLS และ XLSX เมื่อเข้าใจข้อจำกัดของรูปแบบเหล่านี้แล้ว คุณจะสามารถวางแผนและจัดการโครงการที่ใช้ Excel ได้ดีขึ้น และทำให้มั่นใจได้ว่าข้อมูลของคุณจะอยู่ในช่วงที่รองรับ
## คำถามที่พบบ่อย
### จำนวนแถวสูงสุดที่รองรับโดยรูปแบบ XLS คือเท่าใด
จำนวนแถวสูงสุดที่รองรับโดยรูปแบบ XLS (Excel 97-2003) คือ 65,536 แถว
### จำนวนคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLS คือเท่าใด
จำนวนสูงสุดของคอลัมน์ที่รองรับโดยรูปแบบ XLS (Excel 97-2003) คือ 256 คอลัมน์
### จำนวนแถวสูงสุดที่รองรับโดยรูปแบบ XLSX คือเท่าใด
จำนวนแถวสูงสุดที่รองรับโดยรูปแบบ XLSX (Excel 2007 และใหม่กว่า) คือ 1,048,576 แถว
### จำนวนคอลัมน์สูงสุดที่รองรับโดยรูปแบบ XLSX คือเท่าใด
จำนวนสูงสุดของคอลัมน์ที่รองรับโดยรูปแบบ XLSX (Excel 2007 และใหม่กว่า) คือ 16,384 คอลัมน์
### ฉันสามารถใช้ไลบรารี Aspose.Cells สำหรับ .NET เพื่อทำงานกับรูปแบบไฟล์ Excel อื่นๆ ได้หรือไม่
 ใช่ ไลบรารี Aspose.Cells สำหรับ .NET รองรับรูปแบบไฟล์ Excel มากมาย รวมถึง XLS, XLSX, ODS และอื่นๆ คุณสามารถสำรวจ[เอกสารประกอบ](https://reference.aspose.com/cells/net/) เพื่อเรียนรู้เกี่ยวกับคุณลักษณะและฟังก์ชันที่มีอยู่

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
