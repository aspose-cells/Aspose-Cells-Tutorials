---
category: general
date: 2026-03-18
description: สร้างเวิร์กบุ๊กใหม่และส่งออกไฟล์ Excel เป็น TXT พร้อมรักษาความแม่นยำของตัวเลข
  เรียนรู้วิธีบันทึกแผ่นงานเป็น TXT และแปลงแผ่นงานเป็น TXT อย่างมีประสิทธิภาพ
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: th
og_description: สร้างเวิร์กบุ๊กใหม่และส่งออกไฟล์ Excel เป็น TXT อย่างแม่นยำ บทเรียนนี้แสดงวิธีบันทึกแผ่นงานเป็น
  txt และแปลงแผ่นงานเป็น txt ด้วย C#
og_title: สร้างเวิร์กบุ๊กใหม่ – คู่มือการส่งออก Excel เป็น TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: สร้างสมุดงานใหม่ – ส่งออก Excel เป็น TXT ด้วยความแม่นยำเต็ม
url: /th/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง workbook ใหม่ – ส่งออก Excel เป็น TXT ด้วยความแม่นยำเต็มรูปแบบ

เคยต้อง **create new workbook** ใน C# เพียงเพื่อบันทึกข้อมูลลงไฟล์ข้อความธรรมดาไหม? บางทีคุณอาจดึงรายงานจากระบบเก่าและเครื่องมือด้านล่างรับเฉพาะฟีด `.txt` ข่าวดีคือ? คุณไม่จำเป็นต้องเสียความแม่นยำของตัวเลขและแน่นอนว่าไม่ต้องสร้างสตริง CSV ด้วยตนเอง.

ในคู่มือนี้เราจะพาคุณผ่านขั้นตอนทั้งหมดของ **export excel to txt** ตั้งแต่การเริ่มต้น workbook จนถึงการรักษาเลขศูนย์ต่อท้ายเมื่อคุณ **save worksheet as txt** เมื่อเสร็จคุณจะได้โค้ดสั้นที่พร้อมใช้งานซึ่งสามารถใส่ลงในโปรเจค .NET ใดก็ได้ — ไม่ต้องใช้ยูทิลิตี้เพิ่มเติม.

## สิ่งที่คุณต้องการ

- **ASP.NET/ .NET 6+** (โค้ดทำงานบน .NET Framework 4.6+ ด้วยเช่นกัน)  
- **Aspose.Cells for .NET** – ไลบรารีที่ให้พลังกับคลาส `Workbook`, `Worksheet` และ `TxtSaveOptions`. คุณสามารถดาวน์โหลดได้จาก NuGet ด้วยคำสั่ง `Install-Package Aspose.Cells`.  
- ความเข้าใจพื้นฐานของ C# (ถ้าคุณคุ้นเคยกับคำสั่ง `using` คุณก็พร้อมแล้ว).  

แค่นั้นแหละ — ไม่ต้องใช้ Excel interop, ไม่ต้องใช้ COM objects, และแน่นอนว่าไม่ต้องต่อสตริงด้วยมือ.

---

## ขั้นตอนที่ 1: เริ่มต้น New Workbook (Primary Keyword)

สิ่งแรกที่คุณต้องทำคือ **create new workbook**. ให้คิดว่า workbook คือผืนผ้าใบเปล่าที่คุณจะวางตัวเลข, ข้อความ หรือสูตรต่อไป.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การสร้างอินสแตนซ์ `Workbook` โดยไม่โหลดไฟล์ใดๆ จะให้คุณเริ่มจากศูนย์ คุณจึงสามารถเพิ่มข้อมูลโดยโปรแกรมได้ ซึ่งเหมาะอย่างยิ่งสำหรับสถานการณ์ **convert worksheet to txt** ที่คุณไม่มีไฟล์ `.xlsx` อยู่แล้ว.

---

## ขั้นตอนที่ 2: เติมข้อมูลในเซลล์ – รักษาเลขศูนย์ต่อท้าย

ข้อผิดพลาดทั่วไปเมื่อบันทึกตัวเลขเป็นข้อความคือการสูญเสียเลขศูนย์ต่อท้าย (`123.45000` กลายเป็น `123.45`). หากระบบ downstream พึ่งพาฟิลด์ความกว้างคงที่ การสูญเสียนี้อาจทำให้ทุกอย่างพัง.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **เคล็ดลับ:** `PutValue` จะสรุปประเภทข้อมูลโดยอัตโนมัติ หากคุณต้องการสตริงที่ดูเหมือนตัวเลข ให้ใช้ `PutValue("123.45000")` แทน.

---

## ขั้นตอนที่ 3: ตั้งค่า TXT Save Options – รักษาความแม่นยำของตัวเลข

นี่คือจุดที่เวทมนต์เกิดขึ้น โดยการสลับ `PreserveNumericPrecision` คุณบอก Aspose.Cells ให้เขียนค่าที่คุณใส่ไว้โดยตรง รวมถึงเลขศูนย์ต่อท้ายที่ไม่มีความสำคัญด้วย.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **ทำไมต้องเปิดใช้งาน?** เมื่อคุณ **save excel as txt** พฤติกรรมเริ่มต้นจะตัดทศนิยมที่ไม่จำเป็น การตั้งค่า `PreserveNumericPrecision = true` รับประกันว่าผลลัพธ์จะสะท้อนค่าที่แสดงในเซลล์ ซึ่งสำคัญสำหรับรายงานการเงินหรือข้อมูลทางวิทยาศาสตร์.

---

## ขั้นตอนที่ 4: บันทึก Worksheet เป็น TXT – การส่งออกขั้นสุดท้าย

ตอนนี้เราจริงๆ แล้ว **save worksheet as txt**. คุณสามารถระบุพาธใดก็ได้ที่คุณมีสิทธิ์เขียน; ตัวอย่างใช้โฟลเดอร์สัมพันธ์ชื่อ `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **ผลลัพธ์ที่คาดหวัง** (`num-preserve.txt`):

```
123.45000
```

สังเกตว่าเลขศูนย์ต่อท้ายยังคงอยู่ — ตรงตามที่คุณต้องการ.

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ – การตรวจสอบอย่างรวดเร็ว

หลังจากโปรแกรมทำงานเสร็จ ให้เปิด `num-preserve.txt` ในโปรแกรมแก้ไขข้อความใดก็ได้ คุณควรเห็นบรรทัดเดียว `123.45000`. หากคุณเห็น `123.45` แทน ให้ตรวจสอบอีกครั้งว่า `PreserveNumericPrecision` ถูกตั้งค่าเป็น `true` และคุณกำลังใช้ Aspose.Cells เวอร์ชันล่าสุด (v23.10+).

---

## ความแตกต่างทั่วไป & กรณีขอบ

### ส่งออกหลายเซลล์หรือช่วง

หากคุณต้องการ **export excel to txt** สำหรับช่วงทั้งหมด เพียงเติมเซลล์เพิ่มเติมก่อนบันทึก:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose จะเขียนแต่ละเซลล์ในบรรทัดใหม่โดยค่าเริ่มต้น คุณยังสามารถเปลี่ยนตัวคั่น (แท็บ, คอมม่า) ผ่าน `txtSaveOptions.Separator`.

### แปลง Worksheet เป็น TXT ด้วยการเข้ารหัสที่ต่างกัน

บางครั้งระบบ downstream ต้องการ UTF‑8 BOM หรือ ASCII ปรับการเข้ารหัสดังนี้:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### จัดการกับ Workbook ขนาดใหญ่

เมื่อจัดการกับชีตขนาดใหญ่ (หลายแสนแถว) ควรพิจารณาการสตรีมผลลัพธ์:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## เคล็ดลับ & สิ่งที่ควรระวัง

- **อย่าลืมสร้างไดเรกทอรี output** ก่อนเรียก `Save` มิฉะนั้นคุณจะได้รับ `DirectoryNotFoundException`.  
- **ระวังตัวคั่นทศนิยมตามโลคัล** หากสภาพแวดล้อมของคุณใช้คอมม่า (`1,23`) ให้ตั้งค่า `txtSaveOptions.DecimalSeparator = '.'` เพื่อบังคับให้ใช้จุด.  
- **ความเข้ากันได้ของเวอร์ชัน**: ฟลัก `PreserveNumericPrecision` ถูกเพิ่มใน Aspose.Cells 20.6 หากคุณใช้เวอร์ชันเก่า ฟลักจะไม่มีและคุณต้องจัดรูปแบบเซลล์เป็นข้อความก่อนบันทึก.

![ตัวอย่างการสร้าง workbook ใหม่](excel-to-txt.png "สร้าง workbook ใหม่")

*ข้อความแทนภาพ: "สร้าง workbook ใหม่และส่งออก Excel เป็น TXT โดยรักษาความแม่นยำของตัวเลขไว้"*

---

## สรุป – สิ่งที่เราได้ครอบคลุม

- **Create new workbook** ด้วย Aspose.Cells.  
- เติมเซลล์ด้วยตัวเลขที่มีเลขศูนย์ต่อท้าย.  
- ตั้งค่า `TxtSaveOptions.PreserveNumericPrecision = true` เพื่อ **save excel as txt** โดยไม่สูญเสียความแม่นยำ.  
- เขียนไฟล์ลงดิสก์และตรวจสอบว่าผลลัพธ์ตรงกับค่าต้นฉบับ.  

นี่คือขั้นตอนการทำงาน **convert worksheet to txt** ทั้งหมดในน้อยกว่า 50 บรรทัดของ C#.

---

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

ตอนนี้คุณสามารถ **export excel to txt** ด้วยความแม่นยำที่สมบูรณ์แล้ว คุณอาจอยากสำรวจ:

- **Exporting to CSV** ด้วยตัวคั่นที่กำหนดเอง (`TxtSaveOptions.Separator`).  
- **Saving as other plain‑text formats** เช่น TSV (`SaveFormat.TabDelimited`).  
- **Batch processing** หลาย workbook ในโฟลเดอร์โดยใช้ `Directory.GetFiles`.  
- **Integrating with Azure Functions** เพื่อการแปลงตามความต้องการในคลาวด์.  

แต่ละหัวข้อเหล่านี้สร้างบนรูปแบบ `Workbook` → `Worksheet` → `TxtSaveOptions` เดียวกัน ทำให้คุณคุ้นเคยได้อย่างรวดเร็ว.

---

### ความคิดสุดท้าย

หากคุณทำตามจนจบ คุณจะรู้วิธี **create new workbook** อย่างแม่นยำ เติมข้อมูล และ **save worksheet as txt** พร้อมรักษาทศนิยมทุกตำแหน่งที่คุณต้องการ มันเป็นโค้ดสั้นๆ แต่แก้ปัญหาที่พบบ่อยเมื่อระบบเก่าต้องการข้อมูลแบบข้อความธรรมดา.

ลองใช้ปรับแต่งตัวเลือกต่างๆ แล้วให้ข้อมูลไหลตามที่คุณต้องการ ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}