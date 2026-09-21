---
category: general
date: 2026-09-21
description: กำหนดค่า SmartMarkerOptions ArrayAsSingle ใน C# เพื่อส่งออกอาเรย์ JSON
  เป็นค่าหนึ่งเซลล์เดียวในไฟล์ Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: th
lastmod: 2026-09-21
og_description: กำหนดค่า SmartMarkerOptions ArrayAsSingle ใน C# เพื่อส่งออกอาร์เรย์
  JSON เป็นค่าหนึ่งเซลล์เดียว เรียนรู้วิธีแก้ไขแบบครบถ้วนขั้นตอนต่อขั้นตอน
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: กำหนดค่า SmartMarkerOptions ArrayAsSingle ใน C# – คู่มือเต็ม
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: กำหนดค่า SmartMarkerOptions ArrayAsSingle ใน C# สำหรับอาร์เรย์ JSON
url: /th/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# กำหนดค่า SmartMarkerOptions ArrayAsSingle ใน C# สำหรับอาร์เรย์ JSON

หากคุณต้องการ **configure SmartMarkerOptions ArrayAsSingle** ขณะสร้างไฟล์ Excel ด้วย Aspose.Cells คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าต้องทำอย่างไร คุณจะได้เห็นวิธีการเก็บอาร์เรย์ JSON ไว้ในเซลล์เดียวโดยไม่กระจายองค์ประกอบของมันไปหลายแถว

การทำงานกับข้อมูล JSON ในสเปรดชีตมักหมายถึงการเลือกระหว่างมุมมองที่แบนและการแสดงผลแบบกะทัดรัด ในหลายสถานการณ์การรายงาน—เช่นการเก็บรายการแท็กหรือชุดของตัวระบุ—คุณต้องการให้สตริง JSON ทั้งหมดอยู่ในเซลล์เดียว ธง **ArrayAsSingle** ใน `SmartMarkerOptions` ทำให้เป็นไปได้

ในบทแนะนำนี้คุณจะได้ทำ:
* สร้าง `DataTable` ที่เก็บอาร์เรย์ JSON ในคอลัมน์หนึ่ง
* ใส่ Smart Markers ในแผ่นงาน Excel
* **Configure SmartMarkerOptions ArrayAsSingle** เพื่อให้อาร์เรย์ JSON ถูกจัดการเป็นค่าของเซลล์เดียว
* ประมวลผลมาร์คเกอร์และบันทึกเวิร์กบุ๊ก
* ตรวจสอบผลลัพธ์

> **Prerequisites** – คุณต้องมีไลบรารี Aspose.Cells สำหรับ .NET (เวอร์ชัน 23.12 หรือใหม่กว่า) และสภาพแวดล้อมการพัฒนา .NET (แนะนำ Visual Studio 2022) ความรู้พื้นฐานเกี่ยวกับ C# และ DataTables ถือเป็นสิ่งที่ต้องมี

---

## ขั้นตอนที่ 1: เตรียมแหล่งข้อมูลด้วยอาร์เรย์ JSON

ขั้นแรก สร้าง `DataTable` ที่จำลองข้อมูลที่คุณจะได้รับจากบริการหรือฐานข้อมูล คอลัมน์ **Names** จะมีสตริงที่เข้ารหัสเป็น JSON แสดงถึงอาร์เรย์ของชื่อ

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Why this step?*  
Smart Markers อ่านข้อมูลโดยตรงจากอ็อบเจ็กต์ .NET การใส่อาร์เรย์ JSON ลงในคอลัมน์สตริงทำให้คุณคงรูปแบบ JSON ที่แม่นยำไว้ ซึ่งต่อมาจะสามารถเขียนลงในเซลล์โดยไม่เปลี่ยนแปลง

## ขั้นตอนที่ 2: แทรก Smart Markers ลงในเวิร์กบุ๊กใหม่

สร้างเวิร์กบุ๊กใหม่ เลือกแผ่นงานแรก และเขียน Smart Markers ที่อ้างอิงตารางทั้งหมดและคอลัมน์ **Names** เฉพาะ

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

มาร์คเกอร์ `&=dataTable.Names` บอก Aspose.Cells ให้แทนที่เซลล์ด้วยค่าของคอลัมน์ **Names** สำหรับแต่ละแถวใน `dataTable` เนื่องจากเรามีเพียงแถวเดียว มาร์คเกอร์จะถูกประมวลผลหนึ่งครั้ง

## ขั้นตอนที่ 3: **Configure SmartMarkerOptions ArrayAsSingle**

โดยค่าเริ่มต้น Aspose.Cells จะขยายสตริงที่คล้ายอาร์เรย์เป็นหลายแถว การตั้งค่า `ArrayAsSingle` เป็น `true` จะทำให้พฤติกรรมนี้ถูกแทนที่ ทำให้สตริง JSON ทั้งหมดอยู่ในเซลล์เดียว

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Why enable `ArrayAsSingle`?*  
เมื่อ `ArrayAsSingle` เป็น `false` เอนจินจะตีความ `["Alice","Bob"]` เป็นสองค่าแยกกันและเขียนลงในแถวที่อยู่ติดกัน การตั้งค่าเป็น `true` จะถือสตริงเป็นค่าหน่วยเดียว ซึ่งจำเป็นสำหรับการคงรูปแบบ JSON ไว้ใน Excel

## ขั้นตอนที่ 4: ประมวลผล Smart Markers ด้วยตัวเลือกที่กำหนดค่าแล้ว

ตอนนี้ให้เรียกใช้เอนจิน Smart Marker โดยส่งอ็อบเจ็กต์ตัวเลือกที่คุณเพิ่งกำหนดค่า

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

ระหว่างการประมวลผล Aspose.Cells จะอ่าน `dataTable` ใช้มาร์คเกอร์และเคารพธง `ArrayAsSingle` ทำให้อาร์เรย์ JSON ไม่ถูกแก้ไข

## ขั้นตอนที่ 5: บันทึกเวิร์กบุ๊กและตรวจสอบผลลัพธ์

สุดท้าย ให้บันทึกเวิร์กบุ๊กลงดิสก์ เปิดไฟล์ที่สร้างขึ้นใน Excel หรือโปรแกรมดูสเปรดชีตใดก็ได้เพื่อยืนยันว่าเซลล์ **A2** มีสตริง JSON ตรงตามที่ต้องการ

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### ผลลัพธ์ที่คาดหวัง

| A   |
|-----|
| **["Alice","Bob"]** |

เซลล์ **A2** แสดงอาร์เรย์ JSON เป็นค่าข้อความเดียว โดยตรงตามที่เก็บใน `DataTable` ไม่ได้สร้างแถวเพิ่มเติม

## การปรับเปลี่ยนทั่วไปและการจัดการกรณีขอบ

| สถานการณ์ | วิธีปรับใช้ |
|-----------|--------------|
| **หลายแถวที่มีอาร์เรย์ JSON** | การตั้งค่า `ArrayAsSingle` เดียวกันทำงานได้; อาร์เรย์ JSON ของแต่ละแถวจะอยู่ในเซลล์ของมันเอง |
| **โครงสร้าง JSON ที่แตกต่าง (อ็อบเจ็กต์, อาร์เรย์ซ้อน)** | ตราบใดที่ JSON เป็นสตริง `ArrayAsSingle` จะคงไว้โดยไม่เปลี่ยนแปลง สำหรับอ็อบเจ็กต์ที่ซับซ้อนอาจต้องหลบเลี่ยงเครื่องหมายคำพูด |
| **ใช้แหล่งข้อมูลอื่น (เช่น List\<T\>)** | แทนที่ `DataTable` ด้วยคอลเลกชันที่สามารถวนได้; รูปแบบมาร์คเกอร์ (`&=myList.Property`) ยังคงเหมือนเดิม |
| **ส่งออกเป็น CSV แทน XLSX** | `ArrayAsSingle` ยังใช้ได้ แต่จำไว้ว่า CSV ไม่คงรูปแบบเซลล์; คุณอาจต้องใส่ JSON ในเครื่องหมายคำพูด |

**เคล็ดลับ:** ควรตั้งค่า `ArrayAsSingle` *ก่อน* เรียก `ProcessSmartMarkers` การเปลี่ยนแ旗หลังจากการประมวลผลจะไม่มีผลต่อเซลล์ที่สร้างแล้ว

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในแอปพลิเคชันคอนโซลได้ รวมถึงคำสั่ง `using` ทั้งหมดและคอมเมนต์เพื่อความชัดเจน

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

เรียกโปรแกรม เปิดไฟล์ `SmartMarkerJson.xlsx` แล้วคุณจะเห็นอาร์เรย์ JSON ถูกเก็บไว้ในเซลล์ **A2**

## สรุป

ตอนนี้คุณรู้วิธี **configure SmartMarkerOptions ArrayAsSingle** ใน C# เพื่อเก็บอาร์เรย์ JSON เป็นค่าของเซลล์เดียวเมื่อใช้ smart markers ของ Aspose.Cells ขั้นตอน—การเตรียม `DataTable`, การแทรกมาร์คเกอร์, การตั้งค่าธง `ArrayAsSingle`, การประมวลผลและการบันทึก—เป็นรูปแบบที่ทำซ้ำได้และคุณสามารถนำไปใช้ในสถานการณ์ใด ๆ ที่ต้องการการแสดงผล JSON แบบกะทัดรัดใน Excel

ต่อไปคุณอาจสำรวจ:
* **Aspose.Cells smart markers** สำหรับการวนลูปผ่านคอลเลกชัน
* การส่งออก **nested JSON objects** โดยปรับรูปแบบเซลล์
* การรวม **conditional formatting** กับ smart markers เพื่อรายงานที่สมบูรณ์ยิ่งขึ้น

อย่าลังเลที่จะทดลองกับโครงสร้างข้อมูลต่าง ๆ และแบ่งปันผลการค้นพบของคุณ ขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ

- [สร้าง Excel Workbook จาก JSON – คู่มือ Aspose.Cells ฉบับสมบูรณ์](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [สร้างและกำหนดค่า Excel Workbook Aspose Cells .NET](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [สร้างและกำหนดค่า Excel Workbook Aspose Cells .NET](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}