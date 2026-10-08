---
category: general
date: 2026-04-07
description: เขียนวันและเวลาไปยัง Excel ด้วย C# เรียนรู้วิธีแทรกวันที่ลงในแผ่นงาน,
  จัดการค่าข้อมูลวันที่ของเซลล์ Excel, และแปลงวันที่ตามปฏิทินญี่ปุ่นในไม่กี่ขั้นตอน.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: th
og_description: เขียนวันที่และเวลาไปยัง Excel อย่างรวดเร็ว คู่มือนี้จะแสดงวิธีแทรกวันที่ลงในแผ่นงาน,
  จัดการค่าที่อยู่ในเซลล์วันที่ของ Excel, และแปลงวันที่ตามปฏิทินญี่ปุ่นด้วย C#
og_title: เขียนวันเวลาไปยัง Excel – คำแนะนำ C# ทีละขั้นตอน
tags:
- C#
- Excel automation
- Aspose.Cells
title: เขียนวันที่และเวลาไปยัง Excel – คู่มือฉบับสมบูรณ์สำหรับนักพัฒนา C#
url: /th/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เขียน datetime ไปยัง Excel – คู่มือฉบับสมบูรณ์สำหรับนักพัฒนา C#

เคยต้องการ **write datetime to Excel** แต่ไม่แน่ใจว่า API ใดที่จริงๆ แล้วเก็บวันที่ Excel อย่างถูกต้อง? คุณไม่ได้เป็นคนเดียว ในเครื่องมือองค์กรหลายๆ อย่างเราต้องใส่ `DateTime` ของ C# ลงในสเปรดชีตและผลลัพธ์ควรทำงานเหมือนวันที่ Excel จริง—สามารถเรียงลำดับ, กรอง, และพร้อมสำหรับ pivot tables.  

ในบทแนะนำนี้เราจะอธิบายขั้นตอนที่แม่นยำเพื่อ *insert date into worksheet* ด้วย Aspose.Cells, อธิบายว่าทำไมการตั้งค่าภูมิภาคจึงสำคัญ, และแม้กระทั่งแสดงวิธี **convert Japanese calendar date** ให้เป็น `DateTime` ปกติก่อนที่คุณจะเขียนลงไป. เมื่อจบคุณจะได้โค้ดสั้นๆ ที่สามารถคัดลอกและวางลงในโปรเจค .NET ใดก็ได้.

## สิ่งที่คุณต้องการ

- **.NET 6+** (หรือเวอร์ชัน .NET ล่าสุดใดก็ได้; โค้ดยังทำงานบน .NET Framework ด้วย)  
- **Aspose.Cells for .NET** – แพคเกจ NuGet ที่ช่วยให้คุณจัดการไฟล์ Excel โดยไม่ต้องติดตั้ง Office.  
- ความเข้าใจพื้นฐานเกี่ยวกับ C# `DateTime` และวัฒนธรรม (culture).  

ไม่ต้องใช้ไลบรารีเพิ่มเติม, ไม่ต้องใช้ COM interop, และไม่ต้องติดตั้ง Excel. หากคุณมีอินสแตนซ์ worksheet (`ws`) อยู่แล้ว, ก็พร้อมใช้งาน.

## ขั้นตอนที่ 1: ตั้งค่าภูมิภาคญี่ปุ่น (Convert Japanese Calendar Date)

เมื่อคุณได้รับวันที่เช่น `"R02/05/01"` (Reiwa 2, 1 พฤษภาคม) คุณต้องบอก .NET ว่าจะตีความสัญลักษณ์ยุคอย่างไร. ปฏิทินญี่ปุ่นไม่ใช่ปฏิทิน Gregorian เริ่มต้น, ดังนั้นเราจึงสร้าง `CultureInfo` ที่สลับปฏิทินเป็น `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
หากคุณพาร์สสตริงด้วยภูมิภาคเริ่มต้น, .NET จะโยนข้อยกเว้นรูปแบบเนื่องจากไม่สามารถแมป `R` (ยุค Reiwa) ไปยังปีได้. ด้วยการสลับเป็น `JapaneseCalendar`, ตัวพาร์สจะเข้าใจสัญลักษณ์ยุคและแปลงเป็นปี Gregorian ที่ถูกต้อง.

## ขั้นตอนที่ 2: พาร์สสตริงที่อิงยุคเป็น `DateTime`

เมื่อภูมิภาคพร้อมแล้ว, เราสามารถเรียก `DateTime.ParseExact` ได้อย่างปลอดภัย. สตริงรูปแบบ `"ggyy/MM/dd"` บอกตัวพาร์สว่า:

- `gg` – ตัวระบุยุค (เช่น `R` สำหรับ Reiwa)  
- `yy` – ปีสองหลักภายในยุค  
- `MM/dd` – เดือนและวัน.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**เคล็ดลับ:** หากคุณอาจได้รับวันที่ในรูปแบบอื่น (เช่น `"Heisei 30/12/31"`), ให้ห่อการพาร์สด้วย `try/catch` และใช้ `DateTime.TryParseExact` เป็นทางเลือก. สิ่งนี้จะป้องกันไม่ให้งานนำเข้าทั้งหมดล่มจากแถวที่มีข้อมูลไม่ถูกต้องหนึ่งแถว.

## ขั้นตอนที่ 3: เขียน `DateTime` ลงในเซลล์ Excel (Excel Cell Date Value)

Aspose.Cells ปฏิบัติต่อ .NET `DateTime` เป็นวันที่ Excel แบบดั้งเดิมเมื่อคุณใช้ `PutValue`. ไลบรารีจะเปลี่ยน ticks ให้เป็นหมายเลขซีเรียลของ Excel (จำนวนวันตั้งแต่ 1900‑01‑00) โดยอัตโนมัติ. นั่นหมายความว่าเซลล์จะแสดง **excel cell date value** ที่ถูกต้องและคุณสามารถจัดรูปแบบภายหลังโดยใช้สไตล์วันที่ใน Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**สิ่งที่คุณจะเห็นใน Excel:**  
เซลล์ C1 ตอนนี้มีหมายเลขซีเรียล `44796`, ซึ่ง Excel แสดงเป็น `2020‑05‑01` (หรือรูปแบบใดที่คุณตั้ง). ค่าที่อยู่ภายในเป็นวันที่จริง, ไม่ใช่สตริง, ดังนั้นการเรียงลำดับทำงานตามที่คาดหวัง.

## ขั้นตอนที่ 4: บันทึก Workbook (Wrap‑Up)

หากคุณยังไม่ได้บันทึก workbook, ทำเลยตอนนี้. ขั้นตอนนี้ไม่ได้เกี่ยวกับการเขียน datetime โดยตรง, แต่เป็นการสรุปกระบวนการ.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

เท่านี้—สี่ขั้นตอนสั้นๆ, และคุณได้ **write datetime to Excel** อย่างสำเร็จ, พร้อมจัดการวันที่แบบยุคญี่ปุ่นระหว่างทาง.

---

![ตัวอย่างการเขียน datetime ไปยัง Excel](/images/write-datetime-to-excel.png "ภาพหน้าจอแสดงโปรเจค C# ที่เขียน DateTime ลงในเซลล์ Excel C1")

*ภาพด้านบนแสดงไฟล์ Excel สุดท้ายที่วันที่แสดงอย่างถูกต้องในเซลล์ C1.*

## คำถามทั่วไป & กรณีขอบ

### ถ้า ตัวแปร worksheet ยังไม่ได้พร้อม?

คุณสามารถสร้าง workbook ใหม่ได้ทันที:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### ฉันจะเก็บสตริงยุคญี่ปุ่นต้นฉบับในชีตอย่างไร?

หากคุณต้องการทั้งสตริงต้นฉบับและวันที่ที่พาร์สแล้ว, ให้เขียนลงในเซลล์ที่อยู่ติดกัน:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### วิธีนี้ทำงานกับ .NET เวอร์ชันเก่าได้หรือไม่?

ใช่. `JapaneseCalendar` มีตั้งแต่ .NET 2.0, และ Aspose.Cells รองรับ .NET Framework 4.5+. เพียงตรวจสอบว่าคุณอ้างอิง assembly ที่ถูกต้อง.

### แล้วเรื่องเขตเวลา (time zones) ล่ะ?

`DateTime.ParseExact` คืนค่า **Kind** ของ `Unspecified`. หากแหล่งข้อมูลของคุณเป็น UTC, ให้แปลงก่อน:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### ฉันสามารถตั้งรูปแบบวันที่แบบกำหนดเอง (เช่น “yyyy年MM月dd日”) ได้หรือไม่?

แน่นอน. ใช้คุณสมบัติ `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

ตอนนี้ Excel จะแสดง `2020年05月01日` ในขณะที่ยังคงเก็บค่าที่เป็นวันที่จริง.

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **write datetime to Excel** จาก C#:

1. **Configure** ภูมิภาคญี่ปุ่นด้วย `JapaneseCalendar` เพื่อ **convert Japanese calendar date** สตริง.  
2. **Parse** สตริงที่อิงยุคโดยใช้ `DateTime.ParseExact`.  
3. **Insert** `DateTime` ที่ได้ลงในเซลล์, เพื่อให้ได้ **excel cell date value** ที่ถูกต้อง.  
4. **Save** workbook เพื่อให้ข้อมูลคงอยู่.

ด้วยสี่ขั้นตอนนี้คุณสามารถ **insert date into worksheet** อย่างปลอดภัยโดยไม่คำนึงถึงรูปแบบแหล่งข้อมูล. โค้ดพร้อมทำงานเต็มรูปแบบ, ต้องการเพียง Aspose.Cells, และทำงานบน .NET runtime สมัยใหม่ใดก็ได้.

## ขั้นตอนต่อไปคืออะไร?

- **Bulk import:** วนลูปผ่านแถวใน CSV, พาร์สวันที่ญี่ปุ่นแต่ละรายการ, และเขียนลงในเซลล์ต่อเนื่อง.  
- **Styling:** ใช้ conditional formatting เพื่อไฮไลต์วันที่ล่าช้า.  
- **Performance:** ใช้ `WorkbookDesigner` หรือการแคช `CellStyle` เมื่อต้องจัดการกับหลายพันแถว.  

ลองทดลองได้ตามสบาย—สลับยุคญี่ปุ่นเป็นปฏิทิน Gregorian, เปลี่ยนเซลล์เป้าหมาย, หรือส่งออกเป็นรูปแบบไฟล์อื่น (CSV, ODS). แนวคิดหลักยังคงเหมือนเดิม: พาร์ส, แปลง, และ **write datetime to Excel** อย่างมั่นใจ.

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้สเปรดชีตของคุณเรียงลำดับได้อย่างถูกต้องเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}