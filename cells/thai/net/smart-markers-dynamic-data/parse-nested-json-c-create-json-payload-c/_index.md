---
category: general
date: 2026-02-15
description: แยกวิเคราะห์ JSON ซ้อนกันใน C# ด้วย SmartMarkers และเรียนรู้วิธีสร้าง
  JSON payload ใน C# สำหรับคำสั่งซับซ้อน คู่มือขั้นตอนโดยละเอียดพร้อมโค้ดเต็มและคำอธิบาย
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: th
og_description: แยกวิเคราะห์ JSON ซ้อนใน C# อย่างทันที เรียนรู้การสร้าง JSON payload
  ด้วย C# และประมวลผลด้วย SmartMarkers ในตัวอย่างที่สมบูรณ์และสามารถรันได้.
og_title: แยกวิเคราะห์ JSON ซ้อนกันใน C# – สร้าง JSON Payload ด้วย C#
tags:
- json
- csharp
- smartmarkers
title: แยกวิเคราะห์ JSON ซ้อนใน C# – สร้าง JSON Payload ใน C#
url: /th/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แยกวิเคราะห์ JSON ซ้อนกันใน C# – สร้าง JSON Payload C#  

เคยต้อง **parse nested JSON C#** แต่ไม่รู้จะเริ่มจากตรงไหนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเมื่อข้อมูลของพวกเขามีอาเรย์อยู่ภายในอ็อบเจ็กต์ ข่าวดีคือด้วยไม่กี่บรรทัดของโค้ดคุณสามารถ **create JSON payload C#** ได้และให้ SmartMarkers เดินผ่านโครงสร้างซ้อนกันให้คุณ  

ในบทเรียนนี้เราจะสร้างสตริง JSON ที่แทนคำสั่งซื้อพร้อมรายการสินค้า (line‑items) เปิดใช้งานตัวประมวลผล SmartMarkers ให้เข้าใจช่วงซ้อนกัน แล้วตรวจสอบว่าข้อมูลถูกแยกวิเคราะห์อย่างถูกต้องหรือไม่ สุดท้ายคุณจะได้โปรแกรมที่พร้อมคัดลอก‑วางซึ่งสามารถปรับใช้กับ JSON แบบลำดับชั้นใด ๆ ที่คุณเจอ

## สิ่งที่คุณต้องมี  

- .NET 6 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ .NET Core 3.1)  
- การอ้างอิงไลบรารี SmartMarkers (หรือโปรเซสเซอร์ใด ๆ ที่รองรับช่วงซ้อนกัน)  
- ความรู้พื้นฐาน C#—ไม่มีอะไรซับซ้อน เพียง `using` ธรรมดาและเมธอด `Main`  

เท่านี้แค่นั้น ไม่ต้องติดตั้ง NuGet เพิ่มเติมนอกจากไลบรารีมาร์กเกอร์ และไม่ต้องใช้บริการภายนอก

## ขั้นตอนที่ 1: สร้าง JSON Payload C# – สร้างข้อมูล  

ก่อนอื่นเราจะสร้างสตริง JSON ที่มีอาเรย์ของคำสั่งซื้อ แต่ละคำสั่งซื้อมีอาเรย์ `Lines` ของตนเอง คิดว่าเป็นภาพสแนปช็อตของระบบจัดการคำสั่งย่อยขนาดเล็ก

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

ทำไมต้องสร้าง payload เป็นสตริงแบบ verbatim? เพราะมันรักษาการขึ้นบรรทัดใหม่และทำให้คุณมองเห็นโครงสร้างได้ในครั้งแรก—สะดวกมากเมื่อคุณกำลังดีบัก JSON ซ้อนกัน  

> **เคล็ดลับ:** หาก JSON ของคุณมาจากฐานข้อมูลหรือ API คุณสามารถแทนที่สตริงลิเทอรัลด้วย `File.ReadAllText` หรือการร้องขอเว็บ—ไม่มีส่วนใดในบทเรียนนี้พึ่งพาแหล่งที่มานั้น

## ขั้นตอนที่ 2: เปิดใช้งาน Nested Ranges ด้วย SmartMarkerOptions  

SmartMarkers ต้องการสัญญาณเล็กน้อยเพื่อให้เข้าใจว่าอาเรย์หนึ่งอาจมีอาเรย์อีกอันหนึ่ง นั่นคือสิ่งที่ `EnableNestedRanges` ทำ

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

การตั้งค่า `EnableNestedRanges` เป็น `true` บอกโปรเซสเซอร์ให้ถือคอลเลกชัน `Lines` แต่ละรายการเป็น sub‑range ของช่วง `Orders` พาเรนท์ของมัน หากไม่ตั้งค่าสถานะนี้ ลูปภายในจะถูกละเลยและคุณจะเห็นเฉพาะอ็อบเจ็กต์ระดับบนเท่านั้น

## ขั้นตอนที่ 3: ประมวลผล JSON ด้วย SmartMarkersProcessor  

ต่อไปเราจะส่งสตริง JSON และตัวเลือกไปยังโปรเซสเซอร์ การเรียกนี้ทำแบบ synchronous และไม่คืนค่าอะไร—SmartMarkers จะเขียนผลลัพธ์ลงในคอนเท็กซ์ภายใน ซึ่งคุณสามารถดึงมาใช้ต่อได้

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

หากคุณใช้ไลบรารีอื่น ให้แทนที่ `ws.SmartMarkersProcessor.Process` ด้วยเมธอดที่เหมาะสม; หลักการยังคงเหมือนเดิม—ส่ง JSON และการตั้งค่าที่เปิดใช้งานการจัดการซ้อนกัน

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ที่แยกวิเคราะห์แล้ว  

หลังจากประมวลผลแล้ว คุณมักต้องการยืนยันว่าทุกคำสั่งซื้อและรายการสินค้าถูกเยี่ยมชมแล้ว ด้านล่างเป็นวิธีง่าย ๆ ในการพิมพ์ข้อมูลกลับไปที่คอนโซลโดยใช้เมธอดสมมติ `GetProcessedData` (แทนที่ด้วย accessor ของไลบรารีคุณ)

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**ผลลัพธ์คอนโซลที่คาดหวัง**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

การเห็นโครงสร้างลำดับชั้นถูกสร้างขึ้นใหม่ยืนยันว่า **parse nested json c#** ทำงานตามที่ต้องการ

## ขั้นตอนที่ 5: กรณีขอบและข้อผิดพลาดทั่วไป  

### คอลเลกชันว่าง  
หากคำสั่งซื้ไม่มี `Lines` โปรเซสเซอร์ยังคงสร้างช่วงว่างไว้ ตรวจสอบให้แน่ใจว่าโค้ดต่อจากนั้นสามารถจัดการรายการว่างได้โดยไม่โยน `NullReferenceException`

### โครงสร้างซ้อนลึก  
`EnableNestedRanges` ทำงานสำหรับการซ้อนระดับสองโดยอัตโนมัติ สำหรับระดับสามหรือมากกว่านั้น คุณอาจต้องตั้งค่า `MaxNestedDepth` (หากไลบรารีเปิดให้ใช้) หรือเรียกโปรเซสเซอร์แบบเรียกซ้ำบนแต่ละซับ‑อ็อบเจ็กต์

### ตัวอักษรพิเศษ  
สตริง JSON ที่มีเครื่องหมายอัญประกาศ, backslashes หรือ Unicode ต้องการการ escape ที่ถูกต้อง การใช้สตริง verbatim (`@""`) อย่างที่เราทำช่วยหลีกเลี่ยงปัญหาส่วนใหญ่ แต่หากคุณสร้าง JSON อย่างโปรแกรมมิ่ง ให้ให้ `System.Text.Json.JsonSerializer` จัดการการ escape ให้คุณ

### ประสิทธิภาพ  
การแยกวิเคราะห์ payload ขนาดใหญ่ (หลายเมกะไบต์) อาจใช้หน่วยความจำมาก พิจารณา stream JSON ด้วย `Utf8JsonReader` แล้วส่งชิ้นส่วนให้โปรเซสเซอร์ถ้าพบคอขวดด้านประสิทธิภาพ

## ภาพรวมเชิงภาพ  

![ภาพแสดงการไหลของ parse nested json c# ผ่านการประมวลผลของ SmartMarkers](parse-nested-json-csharp-diagram.png "แผนภาพ parse nested json c#")

ภาพแสดงการเดินทางจาก JSON ดิบ → SmartMarkerOptions → Processor → โมเดลอ็อบเจ็กต์ที่แยกวิเคราะห์แล้ว

## สรุป  

เราได้เดินผ่านตัวอย่าง **parse nested json c#** อย่างครบถ้วน ตั้งแต่ **create json payload c#** จนถึงการตรวจสอบข้อมูลซ้อนกันหลังการประมวลผล ข้อสรุปสำคัญคือ:

1. สร้างสตริง JSON ที่มีโครงสร้างดีและสอดคล้องกับอ็อบเจ็กต์โดเมนของคุณ  
2. เปิดใช้งาน `EnableNestedRanges` (หรือเทียบเท่า) เพื่อให้ตัวแยกวิเคราะห์เคารพอาเรย์ภายใน  
3. รันโปรเซสเซอร์และตรวจสอบผลลัพธ์เพื่อให้แน่ใจว่าทุกระดับถูกเยี่ยมชม  

## ขั้นตอนต่อไปคืออะไร?  

- **Payload แบบไดนามิก:** แทนที่สตริงคงที่ด้วยอ็อบเจ็กต์ที่ serialize ผ่าน `System.Text.Json`  
- **มาร์กเกอร์แบบกำหนดเอง:** ขยาย SmartMarkers ด้วยแท็กของคุณเองเพื่อแทรกฟิลด์ที่คำนวณได้ในแต่ละรายการสินค้า  
- **การจัดการข้อผิดพลาด:** ห่อการเรียก `Process` ด้วย try/catch แล้วบันทึกรายละเอียด `SmartMarkerException` เพื่อการแก้ปัญหา  

ลองทดลองดู—สลับอาเรย์ `Orders` เป็นลูกค้า, ใบแจ้งหนี้, หรือข้อมูลลำดับชั้นใด ๆ ที่คุณต้อง **parse nested json c#** รูปแบบจะยังคงเหมือนเดิม  

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}