---
category: general
date: 2026-03-29
description: วิธีแทนที่ตัวแปรใน JSON ด้วย SmartMarker – เรียนรู้การใช้ if expression,
  ใช้ตรรกะเชิงเงื่อนไข, คูณค่า, และสร้าง JSON อย่างง่ายดาย.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: th
og_description: วิธีแทนที่ตัวแปรใน JSON ด้วย SmartMarker ค้นพบวิธีใช้เงื่อนไข if,
  ประยุกต์ตรรกะเชิงเงื่อนไข, คูณค่า, และสร้าง JSON ได้ในไม่กี่นาที.
og_title: วิธีแทนที่ตัวแปรใน JSON ด้วย SmartMarker – ขั้นตอนโดยละเอียด
tags:
- C#
- SmartMarker
- JSON templating
title: วิธีแทนที่ตัวแปรใน JSON ด้วย SmartMarker – คู่มือฉบับสมบูรณ์
url: /th/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแทนที่ตัวแปรใน JSON ด้วย SmartMarker – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีแทนที่ตัวแปร** ภายใน payload ของ JSON โดยไม่ต้องเขียน parser เองหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์การบูรณาการ—เช่น ใบแจ้งหนี้, ระบบกำหนดราคา, หรือไฟล์การกำหนดค่าที่เปลี่ยนแปลงได้—คุณต้องแทรกค่าที่รันไทม์, ใช้เงื่อนไขง่าย ๆ, และอาจทำการคูณอย่างรวดเร็วด้วย บทแนะนำนี้จะแสดงให้คุณเห็น **วิธีแทนที่ตัวแปร** โดยใช้ไลบรารี SmartMarker ทั้งหมดนี้โดยยังคงทำให้ JSON สะอาดและอ่านง่าย

เราจะเดินผ่านตัวอย่างจากโลกจริงที่ครอบคลุม **use if expression**, **how to apply conditional**, **how to multiply values**, และ **how to generate json** อย่างรวดเร็ว เมื่อจบคุณจะมีสคริปต์ C# ที่พร้อมรันที่คุณสามารถนำไปใส่ในโปรเจค .NET ใดก็ได้

## สิ่งที่คุณจะได้เรียนรู้

- ตั้งค่า `SmartMarkerOptions` เพื่อเก็บตัวแปรที่สามารถนำกลับมาใช้ใหม่ได้.  
- เขียนเทมเพลต JSON ที่มี `if` expression สำหรับตรรกะเงื่อนไข.  
- คูณค่าด้วยตัวแปรภายในเทมเพลต.  
- ประมวลผลเทมเพลตด้วย `SmartMarkerProcessor` และรับสตริง JSON ขั้นสุดท้าย.  
- แก้ไขปัญหาที่พบบ่อย เช่น ตัวแปรหายหรือ expression ที่ผิดรูปแบบ.

ไม่มีบริการภายนอก, ไม่มีการพึ่งพาที่หนักหน่วง—เพียงแค่ C# ธรรมดาและแพคเกจ NuGet ของ SmartMarker

## วิธีแทนที่ตัวแปร – ภาพรวมขั้นตอนโดยละเอียด

ด้านล่างเป็นภาพระดับสูงของกระบวนการทำงาน คิดว่าเป็นท่อส่งที่เทมเพลต JSON ดิบของคุณเข้าสู่ด้านซ้าย, เครื่องยนต์ SmartMarker ทำเวทมนตร์ของมัน, และ JSON ที่เรนเดอร์เต็มรูปแบบออกทางด้านขวา

![แผนภาพแสดงวิธีแทนที่ตัวแปรใน JSON](https://example.com/images/smartmarker-flow.png "วิธีแทนที่ตัวแปรใน JSON")

*ข้อความแทนภาพ: แผนภาพแสดงวิธีแทนที่ตัวแปรใน JSON.*

## ขั้นตอนที่ 1: ติดตั้งและนำเข้า SmartMarker

ก่อนที่คุณจะเริ่ม, ตรวจสอบให้แน่ใจว่าแพคเกจ SmartMarker ถูกอ้างอิงในโปรเจคของคุณ หากคุณใช้ .NET CLI ให้รัน:

```bash
dotnet add package SmartMarker
```

จากนั้น, เพิ่มคำสั่ง `using` ที่จำเป็นที่ส่วนหัวของไฟล์ C# ของคุณ:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **เคล็ดลับ:** เวอร์ชันล่าสุด (ณ เดือนมีนาคม 2026) คือ 2.4.1 รองรับ .NET 6 และรุ่นต่อไป, แต่ก็ทำงานได้ดีเช่นกันกับ .NET Framework 4.7

## ขั้นตอนที่ 2: สร้าง SmartMarker Options และกำหนดตัวแปร

ตอนนี้เราจะสร้างอินสแตนซ์ของ `SmartMarkerOptions` ที่จะเก็บตัวแปรใด ๆ ที่เราต้องการใช้ซ้ำในเทมเพลต นี่คือที่ที่เราตอบคำถาม **วิธีแทนที่ตัวแปร**—ตัวแปรทำหน้าที่เป็นตัวแทนที่ SmartMarker จะเปลี่ยนภายหลัง.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

ทำไมต้องเก็บอัตราใน `Variables` แทนการเขียนค่าตายตัว? เพราะคุณอาจดึงตัวเลขนั้นจากฐานข้อมูล, ไฟล์ config, หรืออินพุตของผู้ใช้ การเก็บไว้ใน options ทำให้เทมเพลตสามารถนำกลับมาใช้ใหม่และทดสอบได้

## ขั้นตอนที่ 3: เขียนเทมเพลต JSON พร้อม `if` Expression

นี่คือจุดที่คีย์เวิร์ด **use if expression** ส่องแสง SmartMarker ให้คุณฝังตรรกะเงื่อนไขโดยตรงในสตริง JSON ไวยากรณ์ดูคล้ายกับชื่อ property, แต่ SmartMarker จะตีความเป็นคำสั่ง.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

สังเกตคีย์ `if(Amount>500)` SmartMarker จะประเมิน expression `Amount>500`; หากเป็นจริง ค่าที่สอดคล้อง (`${Amount * Rate}`) จะถูกแทรกลงในผลลัพธ์ ไวยากรณ์ `${...}` คือ *เครื่องมือแทนที่ตัวแปร*—ที่นี่เรากำลัง **วิธีคูณค่า** (`Amount * Rate`) ก่อนใส่ผลลัพธ์

## ขั้นตอนที่ 4: ประมวลผลเทมเพลตและดึง JSON ขั้นสุดท้าย

เมื่อ options และเทมเพลตพร้อม, เราจะส่งทั้งหมดให้กับ processor วิธี `ProcessJson` จะพาร์สเทมเพลต, ใช้เงื่อนไข, ทำการคูณ, และคืนสตริง JSON ที่สะอาด

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

การรันสคริปต์จะแสดงผล:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**เกิดอะไรขึ้น?**  
- `Amount` มีค่า 1000, ซึ่งตรงกับเงื่อนไข `Amount>500`.  
- SmartMarker ประเมิน `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- คีย์เงื่อนไขเดิม (`if(Amount>500)`) ถูกแทนที่ด้วยชื่อ property ที่สะอาด (`Result`). โดยค่าเริ่มต้น SmartMarker ใช้ `"Result"` แต่คุณสามารถปรับแต่งได้ (รายละเอียดต่อไป)

หากคุณเปลี่ยน `Amount` เป็น `400`, ผลลัพธ์จะเป็น:

```json
{
  "Amount": 400
}
```

บล็อกเงื่อนไขหายไปเพราะ expression ประเมินเป็น `false`. นั่นคือแก่นของ **วิธีใช้เงื่อนไข** ใน JSON.

## ขั้นตอนที่ 5: ปรับแต่งชื่อ Property ของผลลัพธ์ (ทางเลือก)

บางครั้งคุณอาจไม่ต้องการคีย์ `"Result"` ทั่วไป SmartMarker ให้คุณระบุชื่อที่กำหนดเองโดยใช้ตัวเลือก `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

ผลลัพธ์:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

ตอนนี้ค่าที่เป็นเงื่อนไขจะถูกเก็บภายใต้ชื่อ property ที่มีความหมายมากขึ้น—เหมาะอย่างยิ่งสำหรับบริการ downstream ที่คาดหวังฟิลด์เฉพาะ

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|---------|
| ตัวแปรไม่พบ | คุณอ้างอิงตัวแปรที่ไม่ได้อยู่ใน `smartMarkerOptions.Variables`. | ตรวจสอบการสะกดอีกครั้งและให้แน่ใจว่าตัวแปรถูกเพิ่มก่อนการประมวลผล. |
| ไวยากรณ์ `if` ไม่ถูกต้อง | ขาดวงเล็บหรือใช้โอเปอเรเตอร์ผิด (`>`, `<`, `==`). | ใช้รูปแบบ `if(<expression>)` อย่างเคร่งครัด; SmartMarker รองรับการเปรียบเทียบเชิงตัวเลขแบบง่ายเท่านั้น. |
| JSON ผิดรูปแบบ | โดยบังเอิญทิ้งคอมม่าไว้ท้ายบล็อกเงื่อนไข. | ให้ SmartMarker จัดการลบ; รักษาเทมเพลตต้นฉบับให้ถูกต้องตามไวยากรณ์. |
| รูปแบบตัวเลขที่ไม่คาดคิด | ผลลัพธ์ปรากฏเป็นสตริง `"80"` แทนที่จะเป็นตัวเลข. | ทำการแคสต์หรือพาร์เซภายหลัง, หรือใช้ `${(Amount * Rate):N0}` สำหรับการจัดรูปแบบตัวเลข. |

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคอมไพล์และรันได้ มันแสดง **วิธีสร้าง json** ด้วยตัวแปรแบบไดนามิก, เงื่อนไข, และคณิตศาสตร์—ทั้งหมดในไม่เกิน 30 บรรทัด

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**ผลลัพธ์คอนโซลที่คาดหวัง**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

คุณสามารถเปลี่ยนค่า `Amount` เพื่อทดสอบสาขาเงื่อนไข, หรือปรับ `Rate` เพื่อดูการคำนวณส่วนลดที่ต่างกัน

## การขยายรูปแบบ – สถานการณ์ “วิธีทำ” เพิ่มเติม

- **How to substitute variables** จากไฟล์คอนฟิก: โหลด `Dictionary<string, object>` จาก `appsettings.json` แล้วใส่เข้าไปใน `smartMarkerOptions.Variables`.  
- **How to use if expression** สำหรับหลายเงื่อนไข: เชื่อมต่อเช่น `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker รองรับ AND/OR เชิงตรรกะ.  
- **How to apply conditional** การจัดรูปแบบ: ใช้ `${Amount:0.00}` ภายใน expression เพื่อควบคุมตำแหน่งทศนิยม.  
- **How to multiply values** ด้วยคณิตศาสตร์ที่ซับซ้อนกว่า: `${(Amount - Discount) * TaxRate}` ทำงานเช่นเดียวกัน.  
- **how to generate json** สำหรับอ็อบเจ็กต์ซ้อนกัน: วางบล็อกเงื่อนไขภายในอ็อบเจ็กต์ JSON อื่น, แล้ว SmartMarker จะรักษาโครงสร้างลำดับชั้น.

## สรุป

เราได้ครอบคลุม **วิธีแทนที่ตัวแปร** ใน JSON ด้วย SmartMarker, แสดง **use if expression** สำหรับการรวมเงื่อนไข, อธิบาย **วิธีใช้เงื่อนไข** , แสดง **วิธีคูณค่า** ภายในเทมเพลต, และสุดท้ายอธิบาย **วิธีสร้าง json** ที่พร้อมสำหรับการใช้งาน downstream วิธีนี้เบา, ไม่ต้องพึ่งเอนจินเทมเพลตภายนอก, และเข้ากันได้ดีกับโค้ด C# ใด ๆ

ลองใช้ดู—ปรับตัวแปร, เพิ่มเงื่อนไข, หรือห่อทั้งหมดในคลาสช่วยเหลือเพื่อใช้ซ้ำในโซลูชันของคุณ เมื่อคุณต้องการสร้าง JSON แบบไดนามิกอย่างรวดเร็ว, SmartMarker เป็นตัวเลือกที่มั่นคงและพร้อมใช้งานในผลิตภัณฑ์

**ขั้นตอนต่อไป**

- สำรวจคุณลักษณะขั้นสูงของ SmartMarker เช่น ลูป (`foreach`) และฟังก์ชันกำหนดเอง.  
- ผสานเทคนิคนี้กับ endpoint ของ ASP.NET Core เพื่อให้บริการ JSON API แบบไดนามิก.  
- สำรวจไลบรารีเทมเพลตอื่น ๆ (เช่น Handlebars.NET) เพื่อเปรียบเทียบ, โดยเฉพาะหากคุณต้องการไวยากรณ์ที่หลากหลายกว่า.

มีคำถามหรือกรณีการใช้งานเฉพาะที่คุณกำลังเผชิญอยู่? แสดงความคิดเห็นด้านล่าง, แล้วเรามาแก้ไขปัญหาร่วมกัน. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}